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

![image](https://github.com/user-attachments/assets/63863795-cdc2-4777-8c0e-921762f9a5de)

## Use | when appropriate

`|` is a symbol to use multiple commands on the same line.  
If you have for example script pieces that look like the following:  
  
Example A)
```
~cg0 logo light_splash_1280.png 0 0 90
.fadein logo 800
```

Consider updating to  
  
Example B)  
```
~cg0 logo light_splash_1280.png 0 0 90 | .fadein logo 800
```

With `Example A`, if you want to edit the position of the object, you need to
- edit the line with `cg0`
- then re-place your cursor on `.fadein` to check the results in realtime preview
- repeat until you've placed things in the right position.

With `Example B`, all you need to do is
- update the position in the command `cg0`: it displays **immediately** since .fadein is also on the same line.

Light.vn's sample uses `Example A` in may places to make it beginner-friendly,  
But the pragmatic recommendation is to use `Example B` when possible! 

![image](https://github.com/user-attachments/assets/bceeb69f-046b-4d0d-96e9-d68acdc3bf48)

## Use | when appropriate (2)

Button commands like the following
```
~button0 choice_02 30 50 80 jump my_file.txt choice
zoom choice_02 95% | .fadein choice_02 600 a3
~btnText choice_02 font.otf 40 "my text"
```

can be updated to
```
~button0 choice_02 30 50 80 "jump my_file.txt choice" | zoom choice_02 95% | .fadein choice_02 600 a3
~btnText choice_02 font.otf 40 "my text"
```

to leverage the realtime preview advantages mentioned above.  

Many of Light.vn's commands that accept a command, can be wrapped in `""` to make it clear what the command is.  
This also makes it clearer what `|` should mean to the engine.

## '.' for new lines

A quick note that . at the start of a scenario line will create a new line.
You can use more than one!
```
...hello
```
Will create 3 new lines.
