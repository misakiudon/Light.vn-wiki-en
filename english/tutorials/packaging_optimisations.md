---
title: 21. Packaging Optimisations
description: Optimisations when packaging your game
published: true
date: 2025-07-18T22:37:32.456Z
tags: 
editor: markdown
dateCreated: 2025-07-18T22:37:32.456Z
---

## File optimisations

**Recommended File Formats**

We recommend optimising files to the following formats to reduce disk space as much as possible.

- Audio: ogg
- Images: webp
  - use ex. [tinypng](https://tinypng.com/) for conversion

**Recommended Filenames**

We recommend only using alphanumerics and `_` in filenames if you want to deploy to as many different OSes as possible.  
Ex. `momo_costume_1.webp`

## Hardware optimisations

- We recommend utilising the [Steam Hardware & Software Survey](https://store.steampowered.com/hwsurvey/Steam-Hardware-Software-Survey-Welcome-to-Steam) to determine the median user specs you might be able to expect from your users.
  - Note that depending on the GPU you target, the `maximum texture size` will differ!
- As a a general rule of thumb, assume for Windows that you will only be able to utilise at max 50% of the user's RAM and VRAM.  
An attempt to utilise more may **crash** the game. 
  - ex. a `1920 x 1080` image when decompressed on to the GPU's VRAM will be
    - 1920 x 1080 x 4 (rgba) bytes = 8,294,400 bytes ~= 8MB
    - if the users's VRAM is 8GB, means 8GB / 2 = 4GB
      - 4GB / 8MB ~= 500 images
        - not as much as you may think, especially when using animations!
        - in Computer Science, `time` (ex. load time of resources) and `space` (ex. RAM / disk space) are always tradeoffs
