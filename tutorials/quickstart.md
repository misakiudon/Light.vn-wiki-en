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
