---
title: 20. Packaging
description: 
published: true
date: 2025-07-18T22:36:52.668Z
tags: 
editor: markdown
dateCreated: 2025-07-18T22:36:52.668Z
---

## Common

All packaging starts with `Project` -> `Publish` and executing the type of package you want published.

## C++ (Desktop)

The C++ version of Light.vn has the following customisations you may want to consider after deployment. 

- Write Directory customisation
  - open up `Settings.xml` to find the `writeDirectoryType` attribute. It can be customised to the following:
    - `0`: data will be written in the folder where the game resides
    - `1`: data will be written to ex. `C:\Users\{user name}\AppData\Roaming\{sysProjectFolder}`
      - this is useful for projects where the game folder cannot be guaranteed to be write-able. (ex. burned to a CD, etc.)
      - you will see ex. the following error when Light.vn tries to write to a folder that it cannot:
      - <img alt="image" src="https://github.com/user-attachments/assets/3d91a6d0-667c-4ef3-bdc8-9af11d52c633" />

**Patches**

Sometimes you may want to update your users' game version, but having them redownload the entire game may be costly or difficult. In which case, you can create a minimal `Patch` for your users.

- <img width="830" height="699" alt="image" src="https://github.com/user-attachments/assets/83581d27-41ac-49e9-a74c-1141400b3b05" />
- This will result in a `Patch` folder. zip it and have your users place it in the root folder of your game. 

## Web

**Differences between the C++ version**

- Features not implemented or things to understand
  - Text input
  - Command: `open` is restricted to urls
  - If you use `lua`, note that you cannot use functions that assume Windows
  - Audio does not play until the page is clicked
- Feature differences
  - All resources are loaded at game startup
  - The FPS is capped at `60`

**Deployment customisations**

- settings.xml
  - `disallowOpen`: controls whether to allow the `open` command
    - depending on the platform you deploy, the game might stop if a url is attempted to be opened.
    - ex. due to the server's `Content-Security-Policy`
  - `disallowPopups`: controls whether to show error alerts
    - unlike desktop games, users may be more intolerant of errors

**When deploying to your own server, make sure**

- `Response Header` is set with
  - `"Cross-Origin-Opener-Policy", "same-origin"`
  - `"Cross-Origin-Embedder-Policy", "require-corp"`
  - refer to `server.py`

**Optimisation is important!**

As the whole game is loaded at startup, file optimisations to reduce disk space is very important. 
- Try to aim for less than `90MB`
