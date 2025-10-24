---
title: "CircuitPython on RP2040 boards"
date: 2025-10-15T15:36:09-04:00
tags: [TIL, python, Raspberry Pi]
---

Finally getting around to practicing with [CircuitPython][circuitpy] again. I figure I'll document my journey a bit this time. I'm setting this up using Panic's [Nova text editor][nova], but the instructions should apply to just about any text editor/terminal combination. 

To start off, I'm using both the [Feather RP2040][feather-2040] and the [Seeed Studio XIAO RP2040][xiao-2040]. The Feather ecosystem is a little better established, but the XIAO boards are so cheap and small I had to try them out. The default programming environment (boot loader, language, etc.) is Arduino, but as you may have noticed, I've invested most of my resources in Python, so I'm shifting to the CircuitPython ecosystem.[^fn1] 

The first step in moving to CircuitPython is to load it onto the microcontroller. Holding down the BOOT button on the board while plugging it into the host computer mounts to boot partition. From there, dragging the appropriate UF2 file downloaded from the [CircuitPython downloads page][circuitpy-downloads] will start the flashing process. Once complete, the board will remount with the name CIRCUITPY. That volume should have a text file called `code.py` and a `lib` folder for storing relevant Python libraries. The CircuitPython site has a tab where you can download the [latest version of the libraries][circuitpy-libraries]. 

The board will automatically start running the code in `code.py`. When that file is saved, the code is reloaded and run again. The classic LED blink test makes for a nice confirmation that everything is working. The `time` and `board` libraries are built in to CircuitPython, but you'll need to copy the `neopixel.mpy` library to the `lib` folder on your board to make the following code work. 

```python
# """CircuitPython Essentials Internal RGB LED red, green, blue example"""

import time
import board
import neopixel

led = neopixel.NeoPixel(board.NEOPIXEL, 1)

led.brightness = 0.02

print("Hello, world!")

while True:
	led[0] = (255, 0, 0)
	time.sleep(0.5)
	led[0] = (0, 255, 0)
	time.sleep(0.5)
	led[0] = (0, 0, 255)
	time.sleep(0.5)
```

The NeoPixel included on these boards is _bright_ leading me to probe for the dimmest value I could set for brightness. Some experimentation showed that the cutoff was 0.00781. A little more investigation showed me that was 1 / 128, so the brighness is a 7-bit value. I've since changed the code to set the brightness with `led.brightness = 1 / 128`, making sure the numerator is an integer. 

Notice the `print` command—it's possible to connect to the serial output of the board to see output data. To connect to the serial console from a terminal, use the `screen` command to connect to the relevant TTY. On my system (macOS 26 Tahoe), I list the files under `/dev/tty.*`. There's only one with a `usb` value, so I simply run `screen /dev/tty.usb` <kbd>TAB</kbd> which fills in the correct values and press return.[^fn2] Now, each time I save the `code.py` file, I get a message that says 
```
Code stopped by auto-reload. Reloading soon.
soft reboot

Auto-reload is on. Simply save files over USB to run them or enter REPL to disable.
code.py output:
Hello, world!
```
and the NeoPixel starts cycling. 

The `screen` utility has some odd interactions, so normal exit commands (<kbd>Ctrl</kbd>-<kbd>C</kbd>) don't work to exit. The `screen` manual is pretty comprehensive, but the section on [session management][screen-manual] shows how to detach (suspend) and quit (<kbd>Ctrl</kbd>-<kbd>a</kbd> <kbd>Ctrl</kbd>-<kbd>\\</kbd>) sessions. 

[circuitpy]: https://circuitpython.org
[nova]: https://nova.app
[feather-2040]: https://www.adafruit.com/product/4884
[xiao-2040]: https://www.seeedstudio.com/XIAO-RP2040-v1-0-p-5026.html
[circuitpy-downloads]: https://circuitpython.org/downloads
[circuitpy-libraries]: https://circuitpython.org/libraries
[screen-manual]: https://www.gnu.org/software/screen/manual/screen.html#Session-Management

[^fn1]: Yes, there is also the MicroPython project. Apparently it's lighter weight, but less like standard Python. I haven't seen a reason (or had a project idea) that required me to be too sparse on resources, so I don't see a reason to work in MicroPython. If I'm going to move away from Python for something, might as well step to Arduino.
[^fn2]: If you have multiple `usb` entries, you may need to list them before and after plugging in your board to figure out which entry corresponds to the device.  
