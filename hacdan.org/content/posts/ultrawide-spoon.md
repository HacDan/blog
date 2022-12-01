---
title: "Ultrawide Spoon"
date: 2022-11-30T20:53:03-05:00
toc: false
images:
tags:
  - automation
  - macos
  - productivity
---

## Ultrawide monitors
With the big push for ultra-wide monitors, and the M-Series MacBook Air only supporting one external monitor, I chose to change to an ultra-wide monitor at my desk. I'm not gonna lie, I hated it at first. It seemed to be such a waste of space when fullscreening apps, and as we all know, window management on macOS is lackluster at best, unless you're full screening apps, which is something I rarely need to do. 

Enter [Hammerspoon](https://hammerspoon.org)

## Window Management, But With A Twist
Hammerspoon is far from just a window management addon for macOS. In fact I would say that it isn't specifically and even really taylored for managment windows on MacOS. Hammerspoon markets itself as a "...a tool for powerful automation of macOS. At it's core is just a bridge between the operating system and a Lua scripting engine." So, why am I bringing it up when talking about monitors and window management? Because, it can, with a little work, be your one stop shop for automations on macOS!

You see, as Hammerspoon mentions on it's website, Hammerspoon is an interface for the macOS API's via Lua. Which is just plain awesome. The main uses I've used it for have been Window managemnt, but I've only scratched the surface of it's powers! 

## Enough Blab, Let's Get To The Code!
Okay, okay. So, Hammerspoon, by default, doesn't do anything once it's installed. You have to write an `init.lua` script and place it in `~/.hammpersoon/init.lua`. For me, the most useful use of the ultra-wide was to split the screen into three columns. So, I wrote a few functions tied to specific keybinds to accomplish this. 

They all work on the currently focused window. From there, depending on the pressed keybind, will send said window to the center, left, right, or fullscreen. Now, I know this sounds complicated, but it really wasn't that bad. I've posted my keybind and function for sending the currently focused to the right hand side of the screen and setting the size of the window to one third of the screen size. 

```lua
tripleMash = {"cmd", "ctrl", "alt"}

hs.hotkey.bind(tripleMash, "Right", function()
  local win = hs.window.focusedWindow()
  local f = win:frame()
  local screen = win:screen()
  local max = screen:frame()

  if max.w > 2500 then f.x = max.x + (max.w / 1.5) else f.x = max.x + (max.w / 2) end
  f.y = max.y
  if max.w > 2500 then f.w = max.w / 3 else f.w = max.w / 2 end
  f.h = max.h
  win:setFrame(f)
end)
```

As you can see, not too many lines, and most of this is reused for the other functions I've written. `hs.hotkey.bind` does exactly what it says on the tin. It allows you to bind keys to a function. I inline the function, but you don't have to. I would like to note that the inline if statements are for when I'm not using my ultra-wide monitor and I'm using just the built-in monitor on the Macbook Air. This way it only splits the screen in half. 

## But why? 
That is the question, right? Why would someone bother to write functions for window management or even want to control their windows with just the keyboard instead of the mouse? Haven't we evolved passed just using the keyboard? Sure, I can see all of those points, but when you look at the fact that most of us use a computer for 4-8 hours a day, reducing the amount of times I have to touch the mouse greatly reduces the chance of an RSI injury. 

Sure, there's the cool factor of being able to slide your windows wherever you want them with just your keyboard, but in reality, it has real world benefits as well. 

If you don't want to use Hammerspoon, there are other apps that greatly improve macOS window management, but I'd say that Hammerspoon does it best, because it can do so much more. App switching with a shortcut? Sure, no problem. Sequence of tasks you do daily on your computer? Automate it with Hammerspoon! I'd rather not have 3-5 apps running in the background when one can do just fine. 

I will say, the other huge side-benefit for me is every time I write a new function in my Hammerspoon `init.lua` it puts a smile on my face. Why? I dunno, but it's worth it. Give it a shot! 

