---
title: 80. Troubleshooting
description: Common Issues and Resolutions
published: true
date: 2025-06-13T01:51:58.739Z
tags: 
editor: markdown
dateCreated: 2025-06-12T20:37:06.418Z
---

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

