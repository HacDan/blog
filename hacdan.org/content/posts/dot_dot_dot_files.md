---
title: "Dot Dot Dot Files"
date: 2016-07-01
draft: false
toc: false
images:
tags:
  - untagged
---
# Dot Dot Dot Files

 2016.07.01


Dot files. A power user’s bread and butter. We have our special tweaks and custom commands built into our files that tweak our systems just a bit from the next guy. Personally mine are still growing, but I wanted to share them with you for my first blog post of this year long journey. While they’re nothing special, I would like to point out that they do not need to be.


This set of configurations has grown a bit over the years, but not by much. While this is more a reflection of my lazyness to update my dotfiles as opposed to a growing need for more… ya I’m getting off track. The point is, you don’t need a lot in your dot files, but you should probably at least take a look into them. They can be a huge time saver. I know I’ve saved many keystrokes just by adding simple things to my dotfiles, and I suggest you do the same.


Now for me, I work mainly from a terminal session over ssh, so having a completely configured system underneath my fingertips really improves my workflow. While I’m sure I could do what I do without these customizations, they just make things that much easier.


Now, you don’t need to only work from the command line to benefit from these tweaks; it just happens to be how I work.


# What The Dot?(files)


I’m not sure how many times I just typed out the word *dotfiles* but I’m sure it was way more than I needed to. Anyway… The word dotfiles while rooted in files that start with a period, to hide them from most file systems, has really expanded to cover any specific configuration file a user would use on their system that customizes their experience with daily used applications.


The most common would be your terminal profile, something like a bashrc or profile, but any configuration file that you use to customize your experience within an appication could be considered a *dotfile*.


# How to Version your Dotfiles


Now, because these files give users customization and time shortcuts, they do require some time to be put into them. Because of this, it is best to keep your dotfiles backed up, or better yet versioned. For myself, I’ve recently finally made the leap and started versioning them. While they still need to be cleaned up, [here](https://github.com/HacDan/DotFiles) they are. Right now this contains my tmux.conf, vimrc, and bashrc. I’ll be cleaning these up over the next couple of days, as they’re a bit of a mess, and I recently started rebuilding my bashrc, so that one is still a bit bare and needs some organization. For the most part this is what I use on a daily basis to help improve my workflow.


To setup a quick repo and version my dot files I followed this blog post [here](https://developer.atlassian.com/blog/2016/02/best-way-to-store-dotfiles-git-bare-repo/) This post is a writeup of a [post](https://news.ycombinator.com/item?id=11070797) on hacker news outlining how *polm23* keeps his dotfiles versioned. I thought it was a great idea when I found the thread recently and have since implemented it. I haven’t had to restore from the repo yet, but the post contains a pretty simple one liner to help you do so, along with a few more instructions if you’re cloning onto another machine.


# Quick Run Down of Mine


To wrap things up, I just wanted to give a quick run down of my dotfiles. I have more I need to add into the repo, but for now I’m sticking to what I have in there.


## .bashrc


As mentioned previously, my bashrc is being rebuilt from the ground up and I’m adding things in as I notice them missing. I lost my old bashrc, hence the rebuild. For now it really just contains a mess of exports for working with GOLANG and a simple mkcd function which I use all the time that does what it says on the tin. Makes a directory then changes you into that directory. It’s simple things like this that save me just a few keystrokes per operation, but add up to a lot at the end of the day.


## .vimrc


This one is a bit more in depth, and I may have to come back and revist this in another post, but I’ll go over some hightlights that I think are noteworthy. Now I don’t have some 3000lc vimrc, there are, what I consider, a good amount of plugins in there, which would take a bit to go over, along with some remappings to keep my fingers from reaching all over the board. Here we go…


### Vundle


My go to plugin manager of choice. I know there are many, and at times I’m not very happy with Vundle, but it gets the job done and that’s what counts. I’ve learned it’s qwirks and tamed it to my liking.


The one plugin I will hightlight, as a lot of them have been covered in numerous blog posts, like Command-T and NerdTree, is [snipmate](https://github.com/garbas/vim-snipmate). This is a very feature complete version of TextMates snippets. While I never really got into TextMate or it’s snippets, I find that having something to insert boilerplate into code is *very* helpful, and definetely saves a lot of keystrokes. I have many different snippets configured that I will put into the repo soon to show off what I do with it, but anything you find yourself typing a lot, is usually worth putting into snipmate.


### Remappings


Now, the one remaping that I recommend you do take away from this is the leader binding right at the top of the file. I’ve remapped the leader to the very common comma. While I tend to be a bit hipsterish when coming up with keybindings, I’ve found there’s a reason everyone remaps to the comman. It’s awesome. End of story. Give it a shot, and even if you don’t like there, there are other options that may be worth looking into over the default.


### Settings


Now for settings, I have wordwrap turned off, and my tabs inserted as spaces like any sane person would do, but one thing I do use that I’ve found isn’t as populat, but is gaining popularity, is relativenumber. This allows you to quickly spot how many lines down a file you want to operate on with a vim movement and off to the races you go. Besides, who wants to figure out in their head the difference between line 156 and line 194. Not I said the pig.


## .tmux.conf


Alright, final file for this post.


The main thing to take away from my tmux config is that I even use tmux! I jest, while I do really enjoy using tmux, I’m not here to start a screen war or anything. In regards to the configuration file, I’ve mainly rebound the leader, or as tmux calls it, prefix key to CTRL-J. I find this to be much easier to reach/remember than the default which I’ve honestly already forgotten. I’ve also rebound the pane movement to represent VIM style movements, which helps when bouncing between the two, as it is one less thing for me to remember.


I’ve also rebound the split window bindings because I couldn’t keep the defaults straight. I tried, I really did, but I didn’t have much luck. There are some other settings in there for the status bar, but I’m honestly still not quite happy with it, so that will be modified over the next couple of days(hopefully).


# Wrapper it up


To wrap things up, as I mentioned my dot files aren’t extensive, but they are my own. They get me through the day to day grind of my side projects and now a couple of things at work. While I’m sure there’s a thousand more tweaks I could do, I’m okay for now(if you don’t count my bashrc). If you’re into that sort of thing, keep an eye on the repo, I’m sure I’ll be updating it more often now that I have to rebuild my .bashrc from scratch.


## Inspriational Repos


* [Steve Losh’s DotFiles](https://bitbucket.org/sjl/dotfiles/src)
* [JLACROIX’s Tmux Configuration](http://pastebin.com/4ZCTcf7m)
