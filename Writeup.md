# CTF Name – Google Capture The Flag 2019 (Quals)

* **Category:** Web
* **Points:** 500

## Challenge

> Upload your photoz. FYI: /info.php

>Alternative: http://gphotos2.ctfcompetition.com:1337
> http://gphotos.ctfcompetition.com:1337/


### Recon

So starting out I decided to look at the source code of the web page and found out that there was a link to the php source code. I downloaded the php code and looked through it. Noticing a comment saying totally not copy&pasted from somewhere... so I decided to copy and past the first couple lines of the code and found https://jbz.team/midnightsunctfquals2019/Rubenscube. It was a challenge from another CTF Called Midnight Sun CTF 2019 Quals - Rubenscube. At that point I knew that in order to get the flag there was some sort of XXE involved.

## The troubles

I decided to copy and paste the svg code into my own file and uploaded it. I waited and nothing happened it didn't even display on the page. I got really frustrated because at this point there was 4 hours left until the CTF was over. So I kept looking on the internet and kept copying and pasting svg code and every time nothing worked. Then it hit me I needed to add an xml beginning tag to the top of the svg code. So I did that uploaded it and the image was on the page but no XXE happened. At this point I lost all hope and wasn't able to finish on time. 

## The next day

I decided to give it another shot and saw that Bushwackers uploaded his write up and it was completely different from what I had tried. So being the stubborn person I am I kept going with my way and decided to make an image named hello.png and found out that exiftool can add comments just like imagemagick using the command
> exiftool -Comment='<?php eval($_GET["cmd"]);' hello.png
I uploaded the picture and it failed then I realized the image had to be 100x100 and went into pinta and resized it. I uploaded it to the page and it went through. So I downloaded the image to make sure the comment metadata stayed on the image but it didn't. So I got a little upset took a look at the code and noticed these lines
>$size = get_size($path, $mime_type);
        >if ($size[0] * $size[1] > 65536) {
         >   die;
        >}

I assumed that meant that the size of the image has to be bigger than 65536 to keep the comment metadata. So I drew an image and would keep checking to see if my image was over 65536. (I am assuming that 65536 is bits which would be 8.192 kb). After I got above that 65536 number I added the comment and sent it to the website. I downloaded the image, low and behold the comment metadata was still there. So then I made a svg file that returns the png file.

## Solution

upload/dd22ec3ed24a93b7f8d769aa30ceef35/aacccd6f148ecfd67df49aac4c92c7df.png

```

```