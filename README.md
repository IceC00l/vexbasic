# vexbasic
A Vectrex multicartridge (gerber files) based on the design by Jeroen Domburg (Sprite) and the Vextreme iteration by Brett Walach (@technobly)

This is basically a cut down version of the Vextreme cart pcb, without LEDs and without level shifter with all components on one side (bottom) to make the "self" production easier if you're not interested in the LED effects. The code has been modified to add high-Z on the data lines when not in use so you need the stm32.bin file in this repo for it to work properly. This file is equivalent in functionality to the sw v0.4 version from the current vextreme repo at the time of this writing with the level shifter mod and some modifications to support more files (255) under the /rom folders. It also is set to make the MCU run @100MHz to avoid known predictable crashes (reproduceable on the standard vextreme HW v0.3 @120MHz) I encountered with certain bins such as "SMASH-TV" in Y-MUSIC and corruption in the gun turrets in the game THRUST. I have used this code and hardware pretty extensively for a couple of months and found no further issues with this hardware design, but as I am the only "beta tester" I cannot be 100% certain there may be still quirks. The gerber files can be manufactured by the usual JLCPCB or PCBWAY or your local pcb manufacturer - just remember to set the standard 1.6mm PCB thickness. I personally camfer the slot insertion edges with a file manually to roughly about a 45 degree angle - highly suggested to avoid wearing down the Vectrex connector contacts "prematurely" as they have certainly been stressed out by now. You needn't solder any jumpers to JP2 nor JP1 (dfu mode enable) - just place a jumper with pin header in JP1 holding it at an angle while connecting the USB-C cable, it will enter DFU mode. JP2 is just the serial RX/TX lines (TTL!) and are not needed but I added them in case of debugging purposes.

You flash the code after bridging the JP1 jumper before connecting the USB-C port to the PC using the dfu-util.exe or (dfu-util-static.exe) the same way:

dfu-util-static -a 0 -d 0483:df11 -s 0x08000000 -D stm32.bin

Remember to FAT32 format the drive the first time you reconnect it to your PC after you've flashed the firmware. Copy the bins under the /rom folder which you need to create initially (or under additional subfolders if you wish).

You can download a game I ported and modified (100jumps.org -> 100jumpss.bin) and try it out.

Have fun!
