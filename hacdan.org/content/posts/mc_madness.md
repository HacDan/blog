---
title: "MC Madness"
date: 2016-07-08
draft: false
toc: true
images:
tags:
  - untagged
--- 
# MC Madness


 


## Heading On Down To Crazy Town


So, this week I’ve been struggling on what I should write about. I honestly took it easy this week, and was having trouble even picking a topic I could write a few words on. I have a couple of projects I wanted to complete this week that I honestly didn’t even start. With the holiday just a few days ago, I’ve been a bit lazy.


Yesterday I had a day to myself that I was going to sit down and knock out a project and then sit down tonight and was going to write a nice detailed post on my thoughts. Well, yesterday came and went and no projects were finished. (Watched a few good movies though!) I did get a few things off the tech todo list though that I wanted to write about; here we go!


## Just One More Space


I manage a [Minecraft server](http://hacdan.org/post/odroid_plus_minecraft/) for a few friends and myself. It mainly runs itself, but I’m always looking into ways to make things better. Recently I’d stumbled across a way to change up the icon displayed for the server, along with the message displayed beneath the server name. While these seem like very trivial changes, I believe it will make a bigger difference if we ever take the server public. And hey, I learned something!


To the how to!


## How did I do that?


I’ll start with the easy one, the server icon. This just needs to be a 64 pixel by 64 pixel PNG sitting in the root of your server folder. The root is considered where your server JAR file lives. The name of this file should be *server-icon.png*. Just as long as it is a valid image that is of said dimensions, the server will pick this image up and serve it over the network to the Multiplayer List within the game. I have not tried using larger images, but even if they do work, I’m sure they would be scaled down to 64x64, so might as well stick with that.


The not so easy part really wasn’t that hard, but can turn into quite the mess if you’re not using something to generate, and that’s setting the (M)essage (O)f (T)he (D)ay. Before going about all of this, I did have this set, but to a much simpler version, that honestly no one had read. Now that I’ve gone ahead changed things up, I’ve noticed a lot more people have commented on it. Anyway, to set the MOTD, go ahead and open up your server.properties file in your favorite plain text editor. This file is located in the root of your server folder(Position explained above). Once you have this open, you’re looking for the line that says *motd=*. If you cannot find this line, go ahead and add it anywhere in the file.


Anything that is placed after the equals sign will be shown as your server MOTD on the multiplayer screen. As with most things on a Minecraft server, this can be customized beyond just standard text with colos and font weights. To do this you can either use the [Minecraft Wiki](http://minecraft.gamepedia.com/Formatting_codes) or use a text generator that understands these codes. I decided to use a generator that gave me near instant feedback on what I was doing to the text. I find this to be the better option, but you can choose either, as they both will end in the same way. The generator I used was on [minecraft.tools](http://minecraft.tools/en/motd.php). This gives you a decent preview along with a render to aid in creation. I didn’t have any issues with this one, but I’m sure others exist that do the same thing.


Once you’ve generated your MOTD, go ahead and paste it after the equals sign in your *server.properties* and reboot your Minecraft server, and that’s all there is to it!


## One More Thing!


I know, I know, this isn’t an Apple KeyNote, but I needed some… ~~clickbait~~ …thing to catch your eye, ya, that’s it. Anywho, this is about garbage. Well, more specifically about garbage collection. I was experimenting with the G1 Garbage Collector on the odroid to try to reduce some tick lag I was receiving when RedStone was active. Now I’m not talking a huge complex RedStone mechanism here, lets just say one comparator clock was dropping my tickrate right around 15. This is bad, really bad. So I had assumed it was either a limitation of the ODroid, or a problem with the game version I was running. It turns out that my specific combiniation of the G1 Garbage Collector and the ODroid caused MAJOR tick lag on the machine, along with HUGE spike in CPU usage, which of course is what actually reduced my tickrate. After switching back to the normal Garbage Collector, things smoothed out quite considerably, and while I’m still limited on the size of RedStone projects that can be created, It is far from what it was.


I guess the lesson learned here is while some *optimizations* are worthwhile crossplatform, some are tuned for specific setups, that while most would consider generic, in the case of running a sever on a single board ARM computer, not all optimizations are created equal!


#### Ze End

