---
title: "Odroid + Minecraft = Possible"
date: 2016-04-23
draft: false
toc: true
images:
tags:
  - untagged
--- 
# Odroid + Minecraft = Possible


 


## Introduction


ARM based CPU’s have always interested me. Long before they had gained the reputation that they have today, I was hacking away on them. Finding out everything that I could do with them. Over the past few years, there has been a huge interest in optimizations for the architexture along with many operating systems being specificially(at least originally) developed for them. While I’m still working my way to replacing all of the hardware in my house with an ARM CPU, I feel at least in the server department, it should be an easy venture.


This has proven, however to be a bit more work than a few apt-get installs and we’re off to the races. No, it’s been a bit more than that, but, not much! Which I think is awesome!


The first major migration for me was to move a [Minecraft](https://minecraft.net/) server over to an [ODROID - XU4](http://www.hardkernel.com/main/products/prdt_info.php?g_code=G143452239825).


This little beast of a machine has proven to be quite the workhorse, and I may even try to expand on it even more with a webserver running and possibly file storage down the road. It is hosted at a friends house, as it’s his, but I did the majority of the software work to migrate everything over.


### A few specs on the XU4:


* Samsung Exynos 5422
	+ 4 A15 Cores @ 2Ghz
		- 4 A7 Cores @ 1.5Ghz
		- Mali-T628 MP6 GPU
		- 2 GB LPDDR3 RAM
		- Gigabit Ethernet
		- 2 USB3 Ports
		- 1 USB2 Port
		- 1 HDMI Port


Now, on paper, if you ignore the part that makes these cores ARM cores, this is a beastly machine. However, even though these are ARM cores, and not traditional x86(64) cores, they are still quite quick! From the get-go my only concern with the hardware was the 2GB of DDR3 RAM. This is where I had to work a bit of magic and modify the setup just a bit, to have a usable server for the amount of users that are normally present.


Now, onto the how!


## Setup - How do I do that?


The XU4 has a few different options when it comes to storage, and I do not believe this is within the scope of this post, but for the most part, I would count on needing at least 8GB of storage for the software along with the actual map files needed. This is honestly on the small side though, so if you’re thinking you’re going to have a big world, I’d go for at least 16GB of storage.


### Storage


The type of storage doesn’t really matter. While an eMMC module would be optimal, using a MicroSD card or even a spinning disk drive with the cloud box for the XU4 wouldn’t change that much. Minecraft does have a decent amount of disk activity, but not to the point where that will be your bottleneck. This server has a 16GB eMMC module which has been more than enough so far.


### Software Setup


While the OpenJDK is available for the XU4, I would recommend the Oracle build of Java 8. I’m using the latest build as of writing this post. I did test the OpenJDK initially, and it worked just fine, but the Oracle Java package is more optimized, so out with the FOSS and in with Oracle. (*I hope to never have to write that again!*)


Spigot’s optimizations have proven to be the saving grace of running a Minecraft Server on the XU4. If you haven’t heard of Spigot, it is a rewire to the popular Bukkit server, that focuses on optimizations for the server. Another main feature is the plugin API. While Spigot has (pretty much) full support for Bukkit plugins, it has, as far as I know, rewritten the API hooks to be even more optimal for, you guessed it, performance.


## Which plugins should you be using?


While most plugins should be fine for using with the XU4, I’ve found there are a few quintessential ones that are really needed for optimal performance.


### Plugin List:


* [NoSpawnChunks](http://dev.bukkit.org/bukkit-plugins/nospawnchunks/)
* [Essentials](https://hub.spigotmc.org/jenkins/job/Spigot-Essentials/)
* [Essentials Spawn](https://hub.spigotmc.org/jenkins/job/Spigot-Essentials/)


These are the only plugins currently in use on the server, and I feel they are all really needed for a clean Spigot setup and also an optimal one. The key plugin in that list though is NoSpawnChunks. This plugin unloads the spawn chunks as if they were any other chunk in the gaame. This reduces the memory usage of the server by around 10% when people are online and in the spawn chunks because not all of them are loaded. Around 15% when they are online and not in the spawn chunks.


The downsides to this plugin, however, is that no processing is done in the spawn chunks when no one is online. What this boils down to is that farms that need to be built in the spawn chunks will not work, including Iron farms. Now, some versions of these farms will work if they do not require the farm to be loaded all the time, but anything that depends on the farm being loaded all the time will not.


I find this to be a minor setback as while a server iron farm is a nice thing to have, we are using it more as a restriction to force us to mine.


Some testing was completed without this plugin, and things are definetely still playable, even smooth, the problem being it further limits the number of players that can log on to the server. The decision was made more players was a better trade off.


Essentials and Essentials Spawn are Bukkit plugins that are great for admining the server and allowing players to set warps. While far from required for this setup, I would recommend using them, just for ease of use.


## To pre-generate or not to pre-generate


In some initial testing, terrain generation was proven to be the bottleneck of the XU4. While it was more than capable of generating terrain, it could not keep up with more than one person generating chunks at the same time. To resolve this issue, the decision was made to pre-generate the world. The map files were moved to a more powerful machineto speed up the process, but this was far from necessary. The generation was completed in about an hour with a modified server that moves the spawn point around and uses normal generation.


The downsides to being pre-generated means if there is an update that chagnes generation, players will need to move out quite a ways in the world to find this new generation, but again, this was a tradoff that was decided on deemed worth it by the player base.


The program used to pregenerate was [MinecraftLandGenerator](https://github.com/Morlok8k/MinecraftLandGenerator). While it eneded a bit of modification to work with our chosen seed and teh current version of minecraft, generation was completed in about an hour for a 10,000 by 10,000 area. This only generated the overworld, and not the nether or the end.


Research is being conducted on how to generate those regions, as they are now much more important in the current patch. The server hasn’t progressed to the point of being in need of those regions yet though, so I have some time.


## Optimization - What you need to know


In regards to optimization, there wasn’t a whole lot that was done. The server OS in use is Ubuntu 14.04 LTS Minimal, which is available from the ODROID downloads page [here](http://odroid.in/ubuntu_14.04lts/). Basic scripts were put in place to start the server up in a tmux session. Currently there is 1.5GB of RAM dedicated to the Java VM and this is proving to be a bit overkill for the current playerbase, but being as there is no use for the rest of the resources on the server at the moment, the settings have stayed.


One thing that is currently being worked on is underclocking the GPU to save a bit on power, as this is a headless server. In the process a custom kernel may be compiled to help with performance as well, but it is far from needed. If you have any questions, please feel free to comment below or at the [forum post](http://forum.odroid.com/viewtopic.php?f=93&t-20337) started by the hoster on the ODroid forums.


### Links


* [Odroid forum link](http://forum.odroid.com/viewtopic.php?f=93&t=20337)

