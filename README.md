# PinguReset

An automatic resetter for single instance Minecraft speedrunning, requiring the Atum and WorldPreview mods.  
**RUNS THAT USE THIS WILL BE UNVERIFIABLE**

*Temporary problem: the program now only works with 1920x1080 resolution, fullscreen, gui scale 2, and (probably) no FastReset mod. I know this is stupid, and it is my next priority to fix this.*

## Roadmap (soon™)

- improve checks for water and sand
- maybe change screenshot library, for wayland compatibility
- manual selecting of seeds
- maybe add checks for village blocks?? (btw right now path blocks are considered as sand OMEGA)

## How to install

This uses Python with the Pillow and Pynput libraries.
Install Python, then open a shell and run:
```
pip install pynput
pip install Pillow
```
(didn't test on Windows, apparently it works the same)

If you do not use fullscreen, use this simple program to determine where the bottom-left corner of your instance is:
```
from pynput.mouse import Controller
import time
ms = Controller()
time.sleep(10)
print(ms.position)
```
(Run this program, align the cursor to the bottom-left of your Minecraft, wait 10 seconds, copy the result in the leftPos, bottomPos setting)

## How this works

Screenshots and color-reading are done when needed, to determine whether a preview of a world contains both water and sand.  
If it does, the program pauses by itself. If it doesn't, it resets using Atum.  
You can choose to reset by yourself, but you can't choose to *not* reset (this will be implemented in the future)

## Current issues

- On Linux, Pillow.ImageGrab doesn't support the Wayland display server, so you will have to disable it in `/etc/gdm3/custom.conf`.  
This may cause various graphical issues. I will try to find another library that supports Wayland.
- People complained about the script taking screenshots even outside of Minecraft... fair enough kekw, I will try to find a solution.
