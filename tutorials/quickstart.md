---
title: Quickstart
description: Your goto first tutorial on Light.vn
published: true
date: 2025-06-12T03:09:59.237Z
tags: 
editor: markdown
dateCreated: 2025-06-12T03:04:59.242Z
---

## Starter tips on your first [Light.vn](https://soulengineproject.itch.io/lightvn) Project

- Create a new script by pressing the button on the top right: "New Script"
- Open up Project -> Settings, then update "Start Script" to the filepath of your new script
- Paste:
```
~bg0 id0 bg/street_bg_noon.png | .fadein id0 300

script system/macros.txt // macros

~textbox_bottom

"This is my project!

~cg0 id1 scg2.png 310 125 80 | zoom id1 100% | .fadein id1 300
```

## Command Insertion Buttons on the Left

When using the command insertion buttons on the left (blue), the command will insert at the location of the current script cursor.

The current script cursor location can be found using the [Scripts] tab in the editor. (pink)

When in test play mode, the line auto updates to the current line that's been executed, so you can also know what's currently being executed. 

![image](https://github.com/user-attachments/assets/4f2062cb-2739-4bd4-9113-b7d3eb09c221)

## Getting to know the editor (1: navigating the current script)

When first using Light.vn, I'd recommend first learning how to navigate the editor: LightEditor.exe.
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

## What makes a 'Script'?

- Light.vn scripts are .txt files that can be opened in LightEditor.exe, or your favourite text editor.
- Script contents can be divided into 3 main components
  - Light.vn commands
  - Dialogue
  - Macros

**Light.vn commands**, are for example:
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
To transition back to a Light.vn command section, start a new line with a `~`

![image](https://github.com/user-attachments/assets/056caff1-6acc-4fa6-8a8b-96160a7524c0)

**Macros**, are created through ex. commandMacro or macro command.  
You know it's a macro by:
- It's not blue
- Double clicking on it doesn't take you to the Commands section in LightEditor.exe

If the macro was registered through commandMacro, double clicking on it will take you to the Macros tab, which should also make it clear that it is a macro. 

![image](https://github.com/user-attachments/assets/35a108f1-1660-41a4-8b62-4eeb3db7d088)

A macro is basically a find and replace: replacing any match of source with changed result.  
The function of a macro is usually an encapsulation of a Light.vn command, to prevent needing to write out the same long command(s) - thus just a convenience feature.

Some examples can be found in: `Data/Plugins/lvui/_system/macros.txt`

![image](https://github.com/user-attachments/assets/c0611c86-a103-40b4-b3e2-3a6b408a21e3)
