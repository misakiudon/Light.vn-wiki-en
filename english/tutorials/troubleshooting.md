---
title: 80. Troubleshooting
description: Common Issues and Resolutions
published: true
date: 2025-06-13T01:51:58.739Z
tags: 
editor: markdown
dateCreated: 2025-06-12T20:37:06.418Z
---

## Sharing Bugs

**If you notice something might be an engine bug**

- try creating a minimally reproducible example as a [Plugin](./extensions.md#developer-extensions-plugins)
- post the Plugin in Discord with an explanation

**If you run into an error that you just cannot understand, or rarely run into**

Option 1:
- Click `Pause` to pause the game such that no more changes occur
  - Use the various editor features to diagnose

Option 2:
- Click `Debug Save` in the editor `Interop` tab during test play
  - Will create `SaveData/saveslot_debug.xml`
- Share your project as-is along with `SaveData/`
  - Post in Discord with an explanation + ask if someone can help look.
    - Click `Debug Load` to load back to that point during test play

![image](https://github.com/user-attachments/assets/6a4be95e-055b-45b0-a930-866b6188a546)

## Logical Errors

If you notice something odd, a potential logical error in your script, try the following:

- use `breakpoint` or `SystemError` in potential error locations
  - both will pause the editor if reached, and you can then use the info in the editor at that point to diagnose
- if the error is potentially due to variables, combine the commands with `if` to make sure assumptions in your script are actually true
  - ex. `if (my_variable != 0) SystemError "my_variable is {{my_variable}}!"`

## Changing the default textbox name macro

By default we use `【】` as a macro to display character names.

![image](https://github.com/user-attachments/assets/33a48aad-7f54-4dc2-832e-8f5a1429eb8f)

If you'd like to change it, open up the script containing macro by checking the `Macros` tab.  
You will notice a macro like:
```
~macro "~【(.*)】" "~script /Plugins/lvui/_system/textbox.txt name \"$1\""
```

Update to for example the below to use `<>` instead:
```
~macro "~<(.*)>" "~script /Plugins/lvui/_system/textbox.txt name \"$1\""
```

## My object isn't showing!

Try the steps below.

Make sure the command(s) is actually fine
- Start test play right before the command(s) that you expect to create + show the object. 
  - If no error message, continue.

Check if the object exists
- Set the script to the location where your object should be displaying.
- Under the `Objects` tab, insert the name of your object - make sure it appears.

![image](https://github.com/user-attachments/assets/776ffc0d-d704-413a-8ad5-2839d4d1c61b)

Check if the object is under something else
- Under the `Objects` tab, look at the `Center R` column.
- Check if there is any object(s) with a higher value that seems suspect: 
  - in which case just remove those objects in the script. (ex. `fadeout`)

![image](https://github.com/user-attachments/assets/0adcd4f9-f0ed-479b-8689-e599ea4a1c46)

Check if the object is off screen
- Switch the camera mode to `Free Camera`
- Move the camera (ex. zoom out by rolling the mouse wheel), and check if the object displays outside the camera.
  - (for example in the image below, the black texture was displaying outside the camera)
  - If yes, then you just need to update your object's coordinates.

![image](https://github.com/user-attachments/assets/dcb477f3-5e63-4b2a-b536-58bf3c2559d2)

## My object suddenly changed!

If you notice your object, variable, etc. has changed in a way you don't understand,  
utilise the `Created at` column in the various editor tabs. 

![image](https://github.com/user-attachments/assets/447b1811-21bc-43bf-98c8-d2000cc08760)

In the case of some tabs, ex. `Variables` `Key Triggers`,  
the `Created at` column also refers to the `last line the thing was updated`.

![image](https://github.com/user-attachments/assets/7e13210d-7832-430d-9884-5523584cc3b5)

## My object suddenly disappeared!

- Figure out the object `name`
- Place `onDestroy [name] SystemError "my object disappeared!"` on a line after it's creation.
- When the object destroys, the editor shall pause and display the error
  - Check the `Scripts` tab: this shall give you the rough location where the destruction occurred.

## My Game is Slow!

This is likely due to having a bunch of unused objects on the screen.

![image](https://github.com/user-attachments/assets/33f099ff-c48c-4bcc-9719-d5b1a4dbccf9)

- Check `Render Count` on the bottom left of the editor
- Check the `Objects` tab and see if you have objects leftover from previous scenes that are no longer needed
  - you can use the `Created at` column to quickly scan where the objects originate

**PRO Tip**: In the majority of cases, slowness can be avoided by making sure to add
```
clear
```
at the start and end of scenes. 
