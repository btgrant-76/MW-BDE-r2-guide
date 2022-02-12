## BDEGrant's Unofficial Big Dill Extended rev 2 build guide

## Intro
This is an *unofficial* build guide for the [Big Dill Extended rev 2](https://mechwild.com/product/big-dill-extended-bde/). With the exception of links to one or two third-party pages, the actual build steps come from existing, MechWild guides. 

It should be said that I have no, formal relationship with MechWild. I built my BDE before the official guide was released. This document is only an attempt to describe the steps/resources that I used. 

## Build Guide
- [Required Tools and Components](https://mechwild.com/guides/build-guides/murphpad-build-guide/#required)
- [Recommended Tools](https://mechwild.com/guides/build-guides/murphpad-build-guide/#recommended)
- [Step 0: Inspect PCBs and Components](https://mechwild.com/guides/build-guides/murphpad-build-guide/#step0)
- [Step 1: Test, Program, and Solder Pins on Pro Micro](https://mechwild.com/guides/build-guides/murphpad-build-guide/#step1)
	- The MurphPad's guide is a good reference because the MCU's orientation to the PCB is the same. Since the MCU is attached to the bottom of the PCB, it might look like the MCU is upside down as you install it.
	- If you are attaching the MCU using sockets, the [Visual Guide to Socket a Microcontroller](https://github.com/filterpaper/filterpaper.github.io/blob/main/socket-mcu.md) demonstrates the process with the correct orientation.
	- At the time of this writing:
		- [this Discord message](https://discord.com/channels/753705260031148103/837441710698004531/934541929868296202) links to the BDE's firmware. It might be worth double-checking the `#keyboard-help` pins to make sure there isn't a newer one.
		- VIA and Vial can't load the BDE rev 2 layout definition automatically yet. In the mean time [the JSON file from this Discord message](https://discord.com/channels/753705260031148103/837441710698004531/934542027545251921) can be used. Load it into VIA's Design tab or Vial's "Sideload VIA JSON" function.
-   [Step 3: Buttons](https://mechwild.com/guides/build-guides/murphpad-build-guide/#step3)
	-   There's only one button on the BDE. It attaches to the *opposite* side of the PCB from the MCU's USB jack.
-   [Step 4: Diodes](https://mechwild.com/guides/build-guides/murphpad-build-guide/#step4)
-   [Step 5: Solder Pro Micro to PCB](https://mechwild.com/guides/build-guides/murphpad-build-guide/#step5)
	-   If you've used sockets, now is the time to plug the Pro Micro into the sockets.
-   [Step 6: OLED](https://mechwild.com/guides/build-guides/murphpad-build-guide/#step6)
-   [Step 7: Encoder](https://mechwild.com/guides/build-guides/murphpad-build-guide/#step7)
-   [Step 8: Plug In and Test](https://mechwild.com/guides/build-guides/murphpad-build-guide/#step8)
-   [Step 9: RGB Strip](https://mechwild.com/guides/build-guides/obe-build-guide/#step9)
	- The 5V and GND pads aren't labeled on the BDE; this image illustrates which is which:  
		- ![RBG 5V & GND pads](https://cdn.discordapp.com/attachments/837441710698004531/937861235456741396/IMG_29222.jpg)
	- Note that the wires between the pads and the RGB strip will end up *crossing over* each other and the center, RGB/Din wire. This image illustrates a completed, working example: 
		- ![Cross the wires, Peter!](https://cdn.discordapp.com/attachments/837441710698004531/940402438098280459/B58769AB-16DD-4473-BA54-7A74EC036EAA.jpg)
-   [Step 10: Standoffs, Screws](https://mechwild.com/guides/build-guides/murphpad-build-guide/#step9)
-   [Step 11: Customize and Enjoy](https://mechwild.com/guides/build-guides/murphpad-build-guide/#step9)
