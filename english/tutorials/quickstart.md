---
title: 00. Quickstart
description: Your goto first tutorial on Light.vn
published: true
date: 2025-06-13T01:49:48.720Z
tags: 
editor: markdown
dateCreated: 2025-06-12T03:04:59.242Z
---

## Starter tips on your first [Light.vn](https://soulengineproject.itch.io/lightvn) Project

- Play through the entire sample game
  - This will give you an idea of what you can copy paste / customise for your game.
- Open up `LightEditor.exe`
  - Create a new script by pressing the button on the top right: `New Script`
  - Open up `Project` -> `Settings`, then update `Start Script` to the filepath of your new script
  - Paste:
```
~bg0 id0 bg/street_bg_noon.png | .fadein id0 300

script /Plugins/lvui/_system/macros.txt // macros

~textbox_bottom

"This is my project!

~cg0 id1 scg2.png 310 125 80 | zoom id1 100% | .fadein id1 300
```
- **PRO Tip**: Make sure to have joined the Discord server
  - It's the central place to ask questions + chat

## Getting to know the editor (editor shortcuts)

- `ctrl + f`: find and replace
- `ctrl + c` `ctrl + v`: copy paste
- `ctrl + z`: undo
- `tab` `shift + tab` indent, reverse indent

## Getting to know the editor (1: navigating the current script)

When first using [Light.vn](https://soulengineproject.itch.io/lightvn), I'd recommend first learning how to navigate the editor: LightEditor.exe.
I recommend the following steps:

- Choose a file (ex. start0.txt)
- Open up the Scripts tab
- Click on different lines in the script: notice how 
  - the preview screen updates
  - the line number changes in the tab info to the current cursor position

![image](https://github.com/user-attachments/assets/0e7a0742-eda9-4eed-b711-c557b5061858)

## Getting to know the editor  (2: test play <-> edit mode)

- click on a particular line, and press F5 to start test play.
- notice again how
  - the preview screen updates
  - the line number changes in the Scripts tab info to the current line being played.
- press F5 again to return to edit mode. 
  - the preview will return again to the line which the script cursor is
  - which can again be confirmed in the Scripts tab.

Slam F5 back and forth until you get a good feel for this back and forth.

![image](https://github.com/user-attachments/assets/dc47dd62-8cd5-4f9f-9683-9cb15c28df0b)

## How to read the Command Syntax

![image](https://github.com/user-attachments/assets/19fdb11b-4ca5-4ef1-875d-e76f3552137b)

Double clicking on any command in the script will bring up the `Commands` tab.  
The syntax for each command is displayed like the following:
```
cg [name] [filename / animation name] [x] [y] [layer] (camera_option)
```
- inputs in `[]` are compulsory inputs
- inputs in `()` are optional inputs

Thus resulting in being able to write both:
- `cg alice2 alice.png 150 30 50`
- `cg alice2 alice.png 150 30 50 on_camera`

## Command Insertion Buttons on the Left

Command insertion buttons exist on the left (blue) to accelerate common use cases.  
The command will insert at the location of the current script cursor.  
  
The current script cursor location can be found using the `Scripts` tab in the editor. (pink)

When in test play mode, the line auto updates to the current line that's been executed, so you can also know what's currently being executed. 

![image](https://github.com/user-attachments/assets/4f2062cb-2739-4bd4-9113-b7d3eb09c221)

## What makes a 'Script'?

- [Light.vn](https://soulengineproject.itch.io/lightvn) scripts are .txt files that can be opened in LightEditor.exe, or your favourite text editor.
- Script contents can be divided into 3 main components
  - [Light.vn](https://soulengineproject.itch.io/lightvn) commands
  - Dialogue
  - Macros

**[Light.vn](https://soulengineproject.itch.io/lightvn) commands**, are for example:
```
fadein title_bg0 1500
```
- you know it's a command by: 
  - when double clicking on it, LightEditor.exe taking you to the `Commands` tab with the syntax and usage info.

![image](https://github.com/user-attachments/assets/dcf5fee4-4cc1-4ece-859f-4fd1143b7247)

**Dialogue**, is any part of the script that is highlighted completely in `Blue`.  
It is started by the following commands:
- `"`
- `-"`

All lines after are treated as a dialogue section.  
To transition back to a [Light.vn](https://soulengineproject.itch.io/lightvn) command section, start a new line with a `~`

![image](https://github.com/user-attachments/assets/056caff1-6acc-4fa6-8a8b-96160a7524c0)

**Macros**, are created through ex. commandMacro or macro command.  
You know it's a macro by:
- It's not blue
- Double clicking on it doesn't take you to the Commands section in LightEditor.exe

If the macro was registered through `commandMacro`, double clicking on it will take you to the Macros tab, which should also make it clear that it is a macro. 

![image](https://github.com/user-attachments/assets/35a108f1-1660-41a4-8b62-4eeb3db7d088)

A macro is basically a find and replace: replacing any match of source with changed result.  
The function of a macro is usually an encapsulation of a [Light.vn](https://soulengineproject.itch.io/lightvn) command, to prevent needing to write out the same long command(s) - thus just a convenience feature.

Some examples can be found in: `/Plugins/lvui/_system/macros.txt`

![image](https://github.com/user-attachments/assets/c0611c86-a103-40b4-b3e2-3a6b408a21e3)

## How is a Script Processed?

2 main things to remember:

- By default, a script will continue to read until it sees a `wait` command
  - (or any other command that triggers the wait state).
- A script will exit the wait state and continue to read upon the `continueRead` command.

Thus you'll see `continueRead` bound to a bunch of keyDown commands inside ex. `/Plugins/lvui/_system/keys.txt`: 
such that when a particular key is pressed, the script will continue to read. 

(note: `/Plugins/lvui/_system/keys.tx` is called within `/Plugins/lvui/_system/textbox.txt`
which is why when calling the default textbox, key bindings come for free)

**Quick TIP**: if your script isn't continuing, you've likely forgotten to bind `continueRead` to a `keyDown` command.
(or just add `script /Plugins/lvui/_system/keys.txt keybind_continueRead` in the problem location)

You can check key bindings in the `Key Triggers` tab in the editor. 

![image](https://github.com/user-attachments/assets/13979a26-5d85-412f-9d1d-e91503bf3215)

## How is a Script Processed? 2

A script reads top to bottom.
There are 2 main commands that can change that:

- `jump`
- `script`

`jump `
- takes the current script parser, and jumps to a different script, or the same script but a different bookmark.
- after the jump, the script will continue reading at the destination. (thus clearing any previous wait states)
- as you can see, it can be used for creating ex. user choices.

![image](https://github.com/user-attachments/assets/ccdecd67-1a25-49ff-be61-35534db82cb1)

`script`
- will create a new script parser with the target file and push it to the top of the script stack.
- the script stack can be viewed in the `Scripts` tab.
- once the script has finished reading (signalled by the `script_fin` command),  
  the parser will pop, and the caller will continue reading.

We can see the script stack increasing by ex. 

- starting the game (`start0.txt`)
- right clicking to bring up the menu (`/Plugins/lvui/_system/menu.txt`) (script stack increase 1 => 2)
- clicking config to bring up the config page (`/Plugins/lvui/_system/config-system.txt`) (script stack increase 2 => 3)

We know which script a particular script in the stack came from by looking at the ID tab.
- `0 (from: n/a)`: n/a, thus this script has no source, which is right.
- `1 (from: 0)`: thus we know this script was called by the script with ID: 0
- `7 (from: 1)`: thus we know this script was called by the script with ID: 1

Which would match our understanding with how the scripts were called in order. 

![image](https://github.com/user-attachments/assets/a2068ed8-5f06-4441-9533-888563f45647)

![image](https://github.com/user-attachments/assets/d8541cb1-8d07-4e25-8258-e287d868d75e)

And then in reverse order,

- we right click to exit the config page and back to the menu (script stack reduces 3 => 2)
- we right click to exit the menu to get back to the main game (script stack reduces 2 => 1)

Thus coming back to `start0.txt` line: 211, which is the location we started from.  
(and can now continue)

![image](https://github.com/user-attachments/assets/43203e71-f765-49e6-a541-59278b050b16)

## How is a Script Processed? (example: User Choices)

From the sections above, you can start to understand how user choices are created in [Light.vn](https://soulengineproject.itch.io/lightvn).

- `wait preventContinueRead`
  - puts the parser into the wait state
  - prevents `continueRead` (bound to ex. `keyDown`) from unlocking the wait state and further parsing
- `jump` is attached to the user choice buttons
  - when the user clicks the button, the `jump` command activates
  - the wait state releases, and the parser continues to parse at the specified destination

Result: the user is forced to make a choice (button click) to continue 

![image](https://github.com/user-attachments/assets/1ab82570-1708-42c1-964f-b850e6453dd7)

## Object layers and what appears first

By default, objects with higher layers (`r` values) appear higher than those with lower values.  
  
Objects with the same layer value, have **no guarantee** as to what appears before the other. (**may even change mid game!**)

You can check object layer values in the editor `Objects` tab:
- The blue highlight means the r value overlaps with another object.
- If the values overlap, you'd better make sure that the object images don't directly overlap!
  - (which is why it's fine for ex. the skip, auto, etc. controls under the textbox to have the same layer value)

![image](https://github.com/user-attachments/assets/e56e9742-9c69-4769-b6ac-607375ae418c)

## Exporting your game

Can be done through `Project` -> `Publish`

![image](https://github.com/user-attachments/assets/9a5b9732-9d5b-4cfc-90f9-1fad118625e1)

**Q. Can I delete LightTests.exe from the published game?**

- We recommend that you keep it.
- `LightTests.exe` is [Light.vn](https://soulengineproject.itch.io/lightvn)'s method of checking whether the player has all the necessary settings to properly run your game.
  - (If prior to publishing, LightTests will also check whether your PC is fit for development)
- If the program passes, then your game will likely run fine. 
  - If it fails, you can almost be sure something will go wrong.
- We think this is a much better method for users to check whether their game will run fine, vs for example a manual checklist provided in a website.
  - If a player reports your game not working, you as the dev can immediately first ask: "Did LightTests.exe run fine?"

## App Icon Updates

- [Article By Smileflower](https://en.yorubox.eu/light-vn-tutorial-ep-09-export-game-change-app-icon/#change-application-icon-in-lightvn)

## What is a Plugin

A plugin is a self-contained folder (module) that can be placed under `Data/Plugins/`.  
You should be able to copy the folder and paste it into another project, and work **as-is**.

It allows us to
- distribute custom plugins for others to use (ex. UI plugins that you can sell)
- share problems we're having as a minimal reproducible project for others to help debug.

### How to create your own Plugin

- Create a folder under `Data/Plugins` (ex. `my_plugin`)
- Stuff all resources you will use in your plugin under that folder
- From the editor: create a new script inside that plugin folder (ex. `plugin.txt`)
  - make sure all resources used inside that script(s) reference the resources in the plugin by providing the absolute path:
    - ex. `/Plugins/my_plugin/Common_PopupBg.png`

Then you can zip your plugin folder, and share!  
Users can then call your script as ex.  
- `script /Plugins/my_plugin/plugin.txt`

![image](https://github.com/user-attachments/assets/83ef0abe-69f3-4349-a212-1c5c46b7cd9e)

![image](https://github.com/user-attachments/assets/b72a7434-33dd-494c-83a0-ddc1d2b5b30a)

![image](https://github.com/user-attachments/assets/08d42040-fd91-47f9-9628-99d43903bc93)

## How to reload resources

Starting [Light.vn](https://soulengineproject.itch.io/lightvn) 16.7, if you need to load a new version of any resource (text file, image, etc.), 
you can click 

`Project` -> `Reload Resources`

and we'll fetch the updated copy. 

![image](https://github.com/user-attachments/assets/4fc29fe0-7f17-4ab5-a305-6c40b58c1fde)
