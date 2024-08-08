---
title: "EWW guide[WIP]"
draft: false
---

# Warning
This is a guide for [eww](https://github.com/elkowar/eww) i have been writing for the past few months, and isn't finished, but i still thought about posting it. Be warned that this isn't polished and still lacks things such as workspace module examples.

# Introduction
This is a simple, comprehensive and short guide on how to make a small Elkowar's Wacky Widgets setup, including a couple of basic widgets with some sample code. This is geared towards absolute beginners on EWW and will most likely be redundant information if you're already familiar with it.

By the end of this post you'll be a tiny bit familiarized with this amazing piece of software, hopefully it'll encourage you to create your own custom setup using EWW.

Just for context: EWW is a widget system for Unix-based systems, mostly used in Linux machines. It works on both X11 and Wayland display managers.
## Getting things set up
This guide assumes you already have the thing installed, if you don't refer to [this] guide on EWW's documentation. I'm going to use a very basic `bspwm` setup as a base, but rest assured, this setup can be used on top of any WM, since EWW doesn't really do window management stuff (like AwesomeWM) and it's sole purpose is widgets. There for the code is functional for both X and Wayland so you don't have to worry about it.
## First Steps
Let's say you have the same setup as above, but you want to minimize dependencies by not using Polybar or any related bar. You can obviously mimic most of Polybar's configuration, since it's relatively simple, but you might be stuck on implementing some modules such as Workspaces or Volume. So that's why we are going to start with writing a bar.

>[!info]
>If you want some more Polybar Modules on EWW, refer to this repository:
>[user/polybar-replacement](https://github.com/)
## Coding a Bar
### The Main Window
Let's begin by writing two files on `~/.config/eww/` (feel free to copy-paste this code):

```scss
// eww.scss
// You can set theme properties here, such as margin/padding and colors. This is basic CSS by the way.
* {
  all: unset;
}

$background: #262626;
$foreground: #DEE1E6;

.window {
  background: $background;
  color: $foreground;
  font: Roboto, sans-serif;
  font-size: 14px;
}
```

As of general coding and CSS advice. Try to avoid letting empty classes lying around on your code.

Now we get to the spicy part. EWW uses a custom Lisp-based syntax, called `yuck` for it's main configuration and logic, this is the language you're gonna spend the most time in, if you don't like writing Lisp, this is your chance to close this and never touch EWW again, but if you're a **functional** language addict, you're gonna love this.

Let's write some Yuck:

```clojure
;; eww.yuck
;; You can set window geometry and widgets here.

(defwindow bar
  :windowtype "dock"
  :geometry (geometry
  :anchor "top center"
  :width "100%"
  :height "5%"
  :x "0px"
  :y "0px")
  (foo))

(defwidget container [even]
  (box :class "container"
    :space-evenly false))

(defwidget foo []
  (centerbox
    (container :halign "start"
      (label :text "hi"))
    (container :halign "center"
      (label :text "bar :D!!"))
    (container :halign "end"))
```

Here's an ~~brief~~ explanation on what this code does:
First of all, you can call a block of code using [defwindow] followed by name and define other options, followed by the component you want. Afterwards, you define the `bar` widget. Also note that i used an extra widget called `container` for making theming easier.

>[!note] Observation
This might not be immediately useful to you but, if you have multiple configurations, you can point to a specific one using the `-c` flag pointing to a specific directory:
>
>```
> eww open foo -c /path/to/eww/config
>```

### Coding a Clock
Now that we have a pretty much functional and perfectly working bar. We can work on smaller widgets that'll go inside of it, we can start by making a simple clock to display the time. For that, we'll need two things:
- A clock widget (optional, alternatively can be used on `bar` widget directly),
- A way to fetch the time.

For the widget definition, you first name it and then add a label with `:text` set as either `timecmd` without quotes or `"${timecmd}"`.

```  clojure
(defwidget clock []
  (label :text "${timecmd}"))
```

Next, you need to assign a command through `deflisten`. To get the current operating system's hours and minutes you can use the `date` command:

```
$ date +%H:%M
11:27
```

%`H` displays hours in the *24 hour format*, but you can also use `%I`, with the *AM/PM* indicator `%p`

```
date "+%I:%M %p"
1:27am
```

And, finally, for putting the formatted command on a `deflisten`, you can use this formatting:

 ```clojure
 (deflisten timecmd :timeout "1s"
 "time +%H:%M")
 ```
%%
### Workspaces
Making a working workspace widget can be pretty hacky to do at first, but it is really useful for managing which workspaces are available and which are occupied.

>[!Warning]
>Workspace widgets are done through scripts made for your specific window manager, so it won't work if you use a diffrent window manager. **Rember, this guide is for bspwm.**

Let's begin defining the widget with Yuck:

```clojure
(defwidget workspace_button [cmd]
  (button :class "workspaces" :onclick cmd))

(defwidget workspaces []
  (container
    (workspace_button :cmd )))
```