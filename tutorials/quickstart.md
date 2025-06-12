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
