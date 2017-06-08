---
layout: post
title:  "From PC/Linux to macOS as a dev"
categories: dev
tags: macOS
---
# [WIP] From PC/Linux to macOS as a dev

<blockquote>
So you got this shiny new Macbook Pro at your new job, it's great ! Though you prefer using 
Windows or Linux at home, you can't develop macOS or iOS apps on those because Apple decided to.
You don't want to be lost switching between your work and home computer, 
and that's why you're reading this article!
</blockquote>

Whether you're a PC or Linux user, you're used to some common behaviours in your OS.
Apple took very diverging stances on several topics. Let's fix that by customizing macOS!

## The trackpad
The Macbooks trackpads are pretty great, but their default configuration can be frustrating for new Mac users.

### Right-clicking
By default, your Mac trackpad triggers menus when you touch the pad with two fingers.
Let's enable our right-click in `System Preferences/Trackpad/Point & Click`:
change `Secondary click` option to `Click in bottom right corner`.

![image]

### Force Touch
Force click / Taptic engine / Force touch is the gadget of the MBP. It's fun for 10 minutes,
but when you want to do some actual work, you're constantly bothered by this feature automatically 
opening definitions and what not. Let's disable this behavior in `System Preferences/Trackpad/Point & Click`:
disable `Look up & data detectors`. 

[image]

### Horizontal scroll
By default, the trackpad is configured to switch between pages when you swipe with 2 fingers.
This makes it impossible to scroll horizontally in long web pages (like Trello), as it navigates back 
in your history. In `System Preferences/Trackpad/More Gestures`, set the `Swipe between pages` option 
to `Swipe with three fingers` (or disable it).

[image]

## The keyboard

This is the most frustrating thing ever. Look at this, it's just ridiculous :

 [image Mac][image Windows]
 
By the way, Microsoft added their Windows key after Apple

### PC layout
You probably already have done that. Change your keyboard layout to the PC one in
`System Preferences/Keyboard/Input sources`, click the + and look for `PC`.

[image]

Obviously, don't do that if you look at your keyboard when you're typing.
Otherwise, you may become really confused with which key is which.

### The control and command keys
Yep, on Apple's computers, the Control key is quite useless whereas the Command key,
which is equivalent to the Windows key, is used for pretty much everything.
Copy pasting becomes a real pain on macOS. Let's fix that by going to
`System Preferences/Keyboard` and clicking on `Modifier keys`.
Here, switch the Control and Command keys.

[image]

Here's a quick tip about cut/paste. You can't do a `Control+X` (previously `Command+X`) on macOS 
to cut files. Sure, you can have multiple Windows open (how ironic), and then drag and drop, 
but there exists a simpler but hidden shortcut in Finder.
You have to copy and then, instead of pasting with `Control+V` (previously `Command+V`), 
do a `Control+Alt+V` (previously `Command+Option+V`). That should move the file, instead of copying it.

### Quit shortcut
By default, there's a `Command+Q` shortcut that quits the current focused program.
That's one of the most inconvenient thing ever. Especially on French keyboards, 
where the `Q` is directly at the left of the `S`, which makes you quit your program 
when you wanted to save your document.

The most straightforward way to fix this is to create a new system-wide Command+Q shortcut.
Let's override the `Invert colors` shortcut to do just that. Head over to
`System Preferences/Keyboard/Shortcuts/Accessibility`.

[image]

### Lock session shortcut
When you click on the Apple icon, you can "Log out", but this will close your applications 
and that costs time when logging in back later. To fix that, we'll use a screen saver shortcut.

First, head over to `System Preferences/Security & Privacy`, and enable `Require password...`.
[image]

Next, go to `System Preferences/Desktop & Screen Saver/Screen Saver`, and choose and customize 
your favorite Screen Saver (try my [360° Panorama / Photo Sphere Screen Saver](TODO link)!).

[TODO image avec Panorama Screen Saver]

Finally, in the same panel, click Hot Corners` and add a shortcut there.
You can also add a new shortcut in the `System Preferences/Keyboard/Shortcuts` menu.`

[image]

### Switch windows shortcut
You can't do a `Alt+Tab` without compromising other shortcuts. TODO Control + the key above Tab.
