---
title: Productivity Tips
description: Tips on How to Boost Productivity
published: true
date: 2025-06-13T01:36:24.676Z
tags: 
editor: markdown
dateCreated: 2025-06-13T01:36:24.676Z
---

## How can I quickly create prototype buttons?

```
textureCreateRect btn_prototype.png 300 50 255 0 0
textureCreateRect btn_prototype_touch.png 300 50 0 255 0
textureCreateRect btn_prototype_click.png 300 50 0 0 255

~touchableRes btn_prototype.png btn_prototype_touch.png btn_prototype_click.png
~button test1 100 300 80
~btnText test1 NotoSansCJKjp-Regular.otf 24 "click me"

~button test2 100 400 80
~btnText test2 NotoSansCJKjp-Regular.otf 24 "click me too"
```

`textureCreateRect` functions similarly to commands like animation, textureCreate, etc. where the name gets cached into the game for continuous use. 
- (in this case, cached as Images/btn_prototype.png, Images/btn_prototype_touch.png, etc.)
- Thus you can ex. stash it in a script somewhere for use with all your initial button prototypes.
- (and then delete them once you've created actual image(s) - making them the same name will prevent script changes)