---
title: 70. Extensions
description: How to extend the engine and application
published: true
date: 2025-06-22T14:56:25.178Z
tags: 
editor: markdown
dateCreated: 2025-06-22T14:55:54.953Z
---

## Developer Extensions: Plugins

A plugin is a self-contained folder (module) that can be placed under `Data/Plugins/`.  
You should be able to copy the folder and paste it into another project, and work **as-is**.

It allows us to
- distribute custom plugins for others to use (ex. UI plugins that you can sell)
- share problems we're having as a minimal reproducible project for others to help debug.

**How to create your own Plugin**

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

## Player Extensions: Resource Customisations

A developer may allow players to customise the game by making certain resource publicly swappable.

This can be done so through `Data/encrypt_exclusions.txt`, which can be set to something like:
```
// --------------------------------------------------------
//
// Add filepaths or folders of 
// assets you don't want encrypted on deployment.
// (add each filepath / folder on a new line)
// 
// ex：Scripts/scenario/        <- excludes entire folder
// ex：Images/extra/extra0.png
//
// --------------------------------------------------------

// ex. to allow audience to freely 
//     translate the csv scenario files
Scripts/scenario_tables/
```
