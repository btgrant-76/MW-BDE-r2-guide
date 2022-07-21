## BDEGrant's Unofficial Big Dill Extended rev2 Build Guide

## Intro
This is an *unofficial* build guide for the [Big Dill Extended rev2](https://mechwild.com/product/big-dill-extended-bde/). This build has a lot in common with the MurphPad build, and several sections of text have been referenced or directly copied from [its build guide](https://mechwild.com/guides/build-guides/murphpad-build-guide) for conformity's sake.

It should be said that I have no formal relationship with MechWild. I built my BDE before the official guide was released. This document is only an attempt to describe the steps/resources that I used.

Yours truly,
btgrant, aka, BDEGrant

---

## Build Guide

### Required Tools and Components

- Soldering iron
  - A temperature-controlled iron is recommended.
- Solder wire
  - Wire with a rosin or no-clean flux core that is 0.8mm (0.031") or less in diameter is recommended.
- #0 Phillips screwdriver
  - A #1 could probably work. Try an eyeglass repair kit screwdriver in a pinch.
- [Flush cutters](https://mechwild.com/product/flush-cutters/)
  - Or some other way to trim the diode legs short. Large pliers may gouge the surface of the PCB, so be careful.

The owners of MechWild have assembled [a kit of some of the tools they use if you're looking for ideas](https://kit.co/MechWild/keyboard-soldering).

### Step 0: Inspect PCBs and Components

#### Included Components

These components are *always* included with your kit. If any are missing or scuffed, [contact MechWild](https://mechwild.com/contact/).

There may be extras of some components (diodes, screws, standoffs, etc) just in case.

| Description                        | Image (if available) |
| ---------------------------------- | -------------------- |
| 1x PCB                             | (unavailable)        |
| 1x Switch Plate                    | (unavailable)        |
| 1x Bottom Plate                    | (unavailable)        |
| 40x 1N4148 Diodes                  | ![Photo of through-hole diodes](https://i0.wp.com/mechwild.com/wp-content/uploads/2021/10/20211001_102452.jpg?resize=200%2C138) |
| 1x 0.91" I2C OLED & 4x header pins | ![Photo of Includes header pins](https://i0.wp.com/mechwild.com/wp-content/uploads/2021/01/OLED-Screen.jpg?resize=200%2C192) |
| 1x Rotary Encoder                  | ![EC11](https://i0.wp.com/mechwild.com/wp-content/uploads/2021/04/Encoder.jpg?resize=200%2C200) |
| 1x 6x6mm Button                    | ![a.k.a. tact switch, momentary switch](https://i0.wp.com/mechwild.com/wp-content/uploads/2021/04/Reset-Button.jpg?resize=200%2C200) |
| 1x Encoder Knob                    | ![Both colors pictured, but kit only comes with one.](https://i0.wp.com/mechwild.com/wp-content/uploads/2021/04/Knobs.jpg?resize=200%2C200) |
| 8x M2x12mm Standoffs                    | ![Brass standoffs](https://i0.wp.com/mechwild.com/wp-content/uploads/2021/07/20210702_180318.jpg?resize=200%2C200) |
| 16x M2x4mm Screws                  | ![Phillips head, black](https://i0.wp.com/mechwild.com/wp-content/uploads/2021/07/20210702_180354.jpg?resize=200%2C200) |
| 4x Rubber Feet                     | ![a.k.a. bumpons, bumpers](https://i0.wp.com/mechwild.com/wp-content/uploads/2021/04/feet.png?resize=200%2C146)|

#### Other Components

Double-check your order to verify which of these you may or may not have included.

There may be extras of some components (sockets, LEDs, etc) just in case.

| Description                                 | Image                | Notes |
| ------------------------------------------- | -------------------- | :---: |
| 1x Pro Micro & 18x header pins             | ![Photo of Pro Micro with header pins](https://i0.wp.com/mechwild.com/wp-content/uploads/2020/12/pro_micro.png?resize=200%2C145) | :warning: **A Pro Micro[^1] is *required*, unlike the other items on this list!** :warning: |
| 1x RGB LED strip (8 LEDs)                   | (unavailable)        | SMD LEDs will not work for this build.      |
| 90x 0305 Mill-Max sockets                   | (unavailable)        | Used for making the switches hot-swappable. |
| 90x 7305 Mill-Max sockets                   | (unavailable)        | Used for making the switches hot-swappable. More expensive and more difficult to solder. |
| SIP socket (18x positions) & 18x brass pins | ![Photo of SIP socket with Mill-Max pins](https://i0.wp.com/mechwild.com/wp-content/uploads/2021/10/sockets_pins.png?resize=200%2C200) | Used to socket the Pro Micro, which makes it removable without desoldering. |
| 1x Diode Bender                             | ![Multiple diode benders pictured](https://media.discordapp.net/attachments/837441710698004531/998729928654737488/IMG_9335.jpg?width=200&height=150)        | Helps you [bend multiple diodes at a time consistently](https://mechwild.com/guides/general/diodes/). |

### Step 1: Program, Test, and Solder Pins on Pro Micro[^1]

:bulb: If you run into trouble with any of this, don't hesitate to stop by [MechWild's Discord](https://discord.gg/nfxHnsm) and ask for assistance in #keyboard-help. It is much better to triple-check than to have to desolder a Pro Micro!

#### :warning: Planning to use an Elite-C? :warning:

**The OLED will not work out of the box on Elite-Cs.** Its `VCC` (power) pin is wired to [`RAW` on a typical Pro Micro](https://pbs.twimg.com/media/CnZcb2sWAAADDSa?format=jpg&name=large). The Elite-C [puts `B0` in this position instead](https://deskthority.net/wiki/images/7/7d/Elite-C-black.png).

**Therefore:** if using an Elite-C, do not solder the `B0` pin. Solder a wire connecting `VBUS` or `VCC` on the Elite-C to `VCC` on the OLED instead. If using pin headers, breaking off an extra pin so `B0` can't accidentally be soldered would be a good idea.[^2]

<!-- TODO: most of the info below SHOULD be migrated to a general guide that also contains detailed info on known problems and specific troubleshooting steps. (e.g. power-only cables, USB-C Alt Mode problems, "NO DRIVER" for flashing on Windows...) -->

### Step 1A: Program Pro Micro

:warning: **You must program the Pro Micro with BDE Rev2 firmware before it will work as a keyboard.** :warning:

Don't skip this step; you're only postponing the inevitable, and if it turns out your microcontroller is defective you'll regret it.

When you plug the PM in before flashing, it should show up to your OS as a new device:

| Windows                                  | macOS                            | Linux                           |
| -----------------------------------------| -------------------------------- | --------------------------------|
| `Settings > Bluetooth and other devices` | `System Preferences > Bluetooth` | `dmesg -w` (requires superuser) |

If you don't see anything new here, you may need to try a different cable or USB port.

---

#### ...using QMK firmware

Recent [Vial](https://get.vial.today) and [VIA](https://usevia.app/) firmware builds are downloadable from [MechWild's firmware repository](https://github.com/MechWild/mw_firmware).

Firmware can also be generated with [QMK Configurator](https://github.com/MechWild/mw_firmware), but Configurator builds will lack features such as dynamic key remapping and matrix testing.

Once the firmware has been downloaded, [follow these instructions to program (flash) the Pro Micro](https://mechwild.com/guides/general/flashing-a-pro-micro/).

#### ...using ZMK firmware

[Follow these instructions](https://github.com/lesshonor/bde-rev2-zmk-config/blob/main/README.md).

Note that [specific hardware](https://zmk.dev/docs/hardware), like a [nice!nano](https://nicekeyboards.com/nice-nano/), is required to use ZMK firmware. ZMK is not compatible with any 8-bit AVR microcontrollers (Pro Micro, Elite-C, atmega328p, etc).

---

### Step 1B: Test Pro Micro

Once the firmware has been flashed, verify that the Pro Micro now shows up to your computer as a keyboard named `BDE Rev2`.

If it still shows up as the original device, the flash did not work. If you are using QMK Toolbox, pay close attention to the messages in its console to try and figure out what went wrong. Just because the program says `Flash complete` does not mean the flash completed *successfully!*

### Step 1C: Solder Pins to Pro Micro

#### ...using header pins

[The guide for preparing the Pro Micro](https://mechwild.com/guides/general/flashing-a-pro-micro/) also has images of how it is soldered. Since the microcontroller is attached to the bottom of the PCB, it might look like it is upside down as you install it.

#### ...using Mill-Max pins and SIP sockets

The [Visual Guide to Socket a Microcontroller](https://filterpaper.github.io/socket-mcu.html) demonstrates the process with the correct orientation.

- Painter's tape or masking tape can be used instead of polyimide ("Kapton") tape.
- The SIP sockets may have been shipped as one long row; break or cut it at the right length.
- Try not to panic if the Pro Micro ends up soldered into the sockets; the keyboard will still work.

### Step 2: Reset Button

Insert the 6x6mm button into the spot marked `SW1` on the bottom of the PCB and solder it in place.

Once it is soldered on, you can press this button once to reboot the board, and twice to reset to bootloader for flashing[^3].

### Step 3: Diodes

[Follow these instructions](https://mechwild.com/guides/general/diodes/). Like the reset button, the diodes are inserted on the bottom of the PCB.

Avoid accidentally connecting the metal legs/solder joints of two different diodes. If they aren't kept separate, you may end up with unintentional key presses.

### Step 4: Attach Pro Micro to PCB

#### :warning: The keyboard won't work if the PM is on the wrong side! :warning:

If using pin headers, solder the Pro Micro to the bottom of the PCB [just like step 5 of the MurphPad build guide](https://mechwild.com/guides/build-guides/murphpad-build-guide/#step5) and clip the pins.

If using SIP sockets, feel free to reinsert the Pro Micro if you took it out after soldering the pins in; this is technically optional until step 8.

### Step 5X: RGB Strip

If you do not have an RGB strip, [skip to step 6](#step-6-oled).

The RGB strip can be attached at any time before soldering switches in—or at any time if you use mill-max sockets to make the board hotswap. However, it is the only part left that attaches to the back of the board and is soldered on the top.

<!-- TODO: non-BDE-specific info below SHOULD be migrated to a general guide that also contains info on known problems and specific troubleshooting steps. (e.g. strip soldered on backwards, metal parts of wires touching, some of the LEDs aren't lit...) -->

---

#### ...with a connector attached

The strip should be wired as follows:

| **Red** | **Green** | **White** |
| :-----: | :-------: | :-------: |
| 5V      | RGB Data  | GND       |

The connector and extra 5V/GND wires can be cut off; they aren't necessary. If the strip doesn't work, cut off the heatshrink to inspect the joints on the strip; it isn't strictly necessary either.

#### ...that is loose with separate wires

Using the same color scheme the presoldered strip uses is optional, but be sure to solder the wires to the correct end of the strip. The triangular arrow on the strip always points *away* from the wires.

---

The 5V, RGB and GND pads aren't labeled on the BDE PCB; this image illustrates which is which.

![RGB, 5V & GND pads](https://cdn.discordapp.com/attachments/837441710698004531/937861235456741396/IMG_29222.jpg)

1. If the colored wires are stuck together, peel them far enough apart to work with separately.
2. Cut some amount of insulation away from each wire and thread the metal core through the PCB.
   - Wire strippers are the intended tool for this job, but a pair of fingernail clippers, scissors, or even flush cutters and a very careful hand can accomplish the same goal.
   - If using stranded wire, twist the metal core wires together to make them easier to work with.

Cutting more of the insulation off may make things easier, but make sure the metal parts of different wires do not end up touching each other when soldered onto the PCB and/or strip.

:warning: **Not keeping the metal wires separate may stop the keyboard from working!** :warning:

Note that the wires between the PCB and the strip will end up *crossing over* each other and the central RGB Data wire. This image illustrates a completed, working example:

![Cross the wires, Peter!](https://cdn.discordapp.com/attachments/837441710698004531/940402438098280459/B58769AB-16DD-4473-BA54-7A74EC036EAA.jpg)

### Step 6: OLED

This is the first part that goes on the top of the PCB. [Just like step 6 of the MurphPad build guide](https://mechwild.com/guides/build-guides/murphpad-build-guide/#step6):

1. Solder the OLED module to the small pin header it was packaged with; if the pin header has one too many pins, break or clip off the extra.
2. Pry the plastic spacer off with tweezers.
3. Line the OLED module up well, and solder it into place.
4. Clip the header pins on top and bottom.

### Step 7X: Encoder

If you are not using an encoder, [skip to step 8](#step-8-plug-in-and-test).

Insert into the top of the PCB and solder. [Just like step 7 of the MurphPad build guide](https://mechwild.com/guides/build-guides/murphpad-build-guide/#step7). You may need to bend some pins back if they were bent out of place during shipment.

### Step 8: Plug In and Test

If you didn't already attach the Pro Micro to the PCB in step 4, do it now.

1. Plug the board in. If the OLED (and optionally RGB strip) light up, congratulations! :tada:
2. Use metal tweezers or a bent paper clip to check each switch position.
   - If you used an encoder, twist *and* press down on it.

#### Testing in Vial and VIA

[Vial](https://get.vial.today) and [VIA](https://usevia.app/) have dedicated matrix testing modes, which take a lot of guesswork out of the testing process. Using them is strongly recommended.

| Program | Screenshot |
| ---- | ---- |
| Vial | ![Test Matrix mode in Vial](https://cdn.discordapp.com/attachments/837441710698004531/886197994100240394/unknown.png) |
| VIA  | ![Test Matrix mode in VIA](https://cdn.discordapp.com/attachments/837441710698004531/885969317743718400/unknown.png) |

The encoder turn won't show on the matrix, but the press should.

#### Testing in QMK Configurator

Load [QMK Configurator with the expected keymap](https://config.qmk.fm/) in one tab and [QMK Configurator in test mode](https://config.qmk.fm/#/test) in another, and make sure all the keys do what the keymap expects. Keep an eye out for layer keys.

### Step 9X: Install 0305/7305 Mill-Max Sockets

If you did not purchase these sockets, [skip to step 10](#step-10-install-switches).

#### ...by taping them to the PCB

1. Insert one Mill-Max socket into each switch pin hole. The lip of the socket sits on the top of the PCB, while the rest falls through the hole.
2. Place painter's tape, masking tape or polyimide ("Kapton") tape on top of the PCB, to hold the sockets in place while the PCB is upside down.
   - Electrical tape will also work, but may leave an unpleasant residue.
   - Scotch tape is not recommended.
3. Flip the PCB, and solder each socket into place.

#### ...by inserting switches into the PCB

[Follow these instructions](https://docs.splitkb.com/hc/en-us/articles/360012930919-How-do-I-install-Mill-Max-Hot-Swap-Sockets-).

### Step 10: Install Switches

1. Insert four switches into the top (switch) plate, one in or near each corner. These should click into place.
2. Place this plate + switch assembly onto the PCB. Verify all eight switch pins are sticking through the holes in the PCB.
3. Continue inserting switches into the plate, making sure both pins on each switch poke through the holes in the PCB. It may be necessary to hold the PCB in place to prevent it from being pushed off, especially in the beginning.

It can be helpful to balance the PCB and plate perpendicular to your work surface, then insert the switches one row at a time. Look down between the two sides to verify pin alignment as each switch is inserted.

If you are not using Mill-Max sockets, you will need to solder the switches after putting them in place.

If positions that worked perfectly in [#step-7-plug-in-and-test](step 7) begin misbehaving after switches are inserted, make sure neither of the switch pins were accidentally bent against the PCB instead of going through the holes. This is more common with Mill-Max sockets as they are harder to align.

### Step 11: Assemble

[Like the Mercutio, the BDE Rev2 uses a sandwich mount](https://mechwild.com/guides/build-guides/mercutio-build-guide/#step16). The bottom and top plates are screwed together via standoffs, and the PCB hangs from the switches between them. Screw the standoffs onto the bottom plate, then set the plate + PCB assembly on top and add the final screws.

### Step 12: Customize and Enjoy

If you flashed with [Vial](https://get.vial.today) or [VIA](https://usevia.app/) firmware, you may use those utilities to dynamically remap your keys without having to reflash. Note that the Vial program is backwards-compatible with VIA firmware[^4], if the VIA browser app is not a reasonable option.

[^1]: More precisely: a Pro Micro pin-compatible microcontroller (e.g. Elite-C, nice!nano). It might not be a Pro Micro per se, but for the sake of simplicity this guide will refer to all microcontrollers of this type as "Pro Micros" or "PMs".

[^2]: *Theoretically*, it might be possible to power the OLED using the `B0` pin by modifying the firmware to pull that pin high on boot and keep it that way while the board runs. Testing this workaround is left as an exercise for adventurous readers. The author(s) of this guide and MechWild as a company eschew all responsibility for any such experiments, unless it ends up working perfectly.

[^3]: Note that entering bootloader this way will not clear the EEPROM. This matters if you're trying to reflash because something is messed up.

[^4]: As of Vial 0.6 and VIA 1.3.1. This may not hold true forever.
