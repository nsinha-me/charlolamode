---
title: Flashing effect with ImageMagick and FFmpeg
date: 2023-03-13
description: 
type: page
---


Recently, I had been experimenting with Imagemagick, and suddenly got an idea to make a flashing effect with Imagemagick, FFmpeg and shell script. Before sharing the procedure, let me show you the cool output.  



{{< figure src="/images/blog/flashing-effect/output.gif" title="" height="300px">}}


### 1. Creating basic image using ImageMagick


We will use the `convert` tool of the Imagemagick to create a black canvas of size 1080x1080. Now we will add text to the canvas. For the text color I have chosen white, `FreeMono` as font style with fontsize 120. The `gravity` property defines the position of the text. 

``` bash
convert \
-size 1080x1080 \
-background black \
-pointsize 120 \
-font FreeMono \
-fill white \
-gravity center \
caption:"nsinha.me" \
output.jpg
```

### 2. Shell Script

Here the magic happens. The logic is, we will create 400 images of alternating colors i.e. the first image will have white background with black color text, the second image will have black background with white color text and so on. 

``` bash
#!/bin/bash

n=500

i=101
while [ $i -le $n ]   
do  
	rs=`expr $i % 2`
	if [ $rs == 0 ]
	then
	convert -size 1080x1080 -background black -pointsize 120 -font FreeMono -fill white -gravity center caption:"nsinha.me" $i.jpg
	fi
	((++i))  
done


i=101
while [ $i -le $n ]
do
	rs=`expr $i % 2`
	if [ $rs != 0 ]
	then
	convert -size 1080x1080 -background white -pointsize 120 -font FreeMono -fill black -gravity center caption:"nsinha.me" $i.jpg
	fi
	((++i))
done
```

We are naming the images created depending on the value of variable `i` as `101.jpg`, `102.jpg`,...,`500.jpg`.


### 3. Creating video with FFmpeg 

This step is the easiest one. We have all the images in a directory. So, now we will tell FFmpeg to take all the images with the extension `.jpg` and create a video out of it. I have set the framerate as `50`, adjust it according to your need.

``` bash
ffmpeg \
-framerate 50 \
-pattern_type glob \
-i '*.jpg' \
-c:v libx264 \
-r 30 \
-pix_fmt yuv420p \
output.mp4
```

### Final thought

I was happy after creating this flashing effect. Creating something visual by purely using code was something new for me. Also learnt some shell scripting in this process.

I would love to hear your opinions and experiences about this topic. And also the mistakes and improvements in the code/blog. You can mail me at nikhil@nsinha.me .  
