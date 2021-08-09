# "Wassmon" the watermonitor

For my camper truck I was looking for a super accurate monitor, that shows how much water was still left in my tank. When browsing the available solutions, I found out that most devices seem to be from the stone ages using three or four metal rods contacting the water thus showing 25%/50%/75%/100% levels. 
Some (very expensive, $200++) devices use radar sensors mounted in the top of the tank to determine the fill level, but they don't work if the waterlevel in the tank is not level and will then show inaccurate values.  
In this repo you can download the circuits and gerber files to create your own, very cheap water monitor ("Wassermonitor" in German, short "Wassmon").
It uses an affordable flow sensor as counting device input and is very accurate in all positions, even while moving. Additionally, it can be equipped with a sensor that - when refilling your tank - signals the FULL level to WassMon, which can then beep or whatever you like.
Even more PLUS: You can even add a temperature Sensor to the device to show how hot your boiler gets, for example.

For powering the device you can use a range of voltages, depending on the voltage regulator. You can choose any regulator that is pin compatible with a 7805 and produces 5V output.

This repo contains all the files you need to produce your own hardware for "Wassmon", **inculding a super cool case as STL files, for printing on a 3D printer!** 

## Files
In the **gerber** directory you will find all files that are needed for production by a PCB factory. The directory contains all the single files but as well a ZIP file that you can upload to whatever PCB manufacturer you like. Most factories want you to upload the files as a ZIP archive.

The file **assembly.jpg** in the root directory shows how to assemble the finished PCB.

In the **case** directory you will find the STL files for printing the case and some pictures on how the case looks

In the **pictures** directory you will find some pictures on how this device could look when it is filled with working code as an example or even a guide.

## Assembly/BOM
What you need to assemble this project:

1x PCB
1x LED 3.5mm ALARMLED
1x ceramic capacitor each:
C1          100n
C2          22p (optional)
C3          22p (optional)

1x polarized capacitor each:
C4          47µ
C5          100µ

1x diode each:
D1          1N4004
D2          P6KE30A <-- this overvoltage protection diode should match your voltage regulator

1x self resetting fuse 100mA F1
1x pin header female 1x3 each:
ENTER
FILLTOGGLE
LIGHTTOGGLE
NEXT
PREV

1x pin header male 2x3 JP5
1x pin header female 1x20 JP7

1x IC1         ATMEGA328-20P
1x IC2         7805 voltage regulator or compatible (I use one of these: https://www.aliexpress.com/item/1005002556018480.html )
1x IC3         74LS04N Hex INVERTER                                                                     
1x L1          47µ inductor, 100mA
1x Q1          20MHz crystal (optional)

1x resistor 1/8W each:
R1          10k
R2          1k
R4          470
R7          4k7

1x SG1         buzzer
1x T1          N2222A transistor

1x X1 Wago type screw clamp 2 terminal (# W237-102) 12V-IN
1x Wago type screw clamp 3 terminal (# W237-103) each:
X2          FILLSENSE     W237-103        W237-103     WAGO SCREW CLAMP                                     237-103 unknown    18M7116  
X4          TEMP          W237-103        W237-103     WAGO SCREW CLAMP                                     237-103 unknown    18M7116  
X5          AUSlauf       W237-103        W237-103     WAGO SCREW CLAMP                                     237-103 unknown    18M7116  

6x capacitive touch sensor (e.g. https://www.aliexpress.com/item/33062790002.html )
**Attention: 2 of these sensores (LIGHTTOGGLE, FILLTOGGLE) have to be configured to toggle ON/OFF, you have to bridge jumper B for that**
5x extra high pin headers male 1x3 (e.g. https://www.aliexpress.com/item/32911455899.html ), I used 17mm height.
1x LCD 12864 128x64 dot matrix (e.g. https://www.aliexpress.com/item/1420941126.html )
1x pin header male 1x20 (soldered to the display)
1x DS18B20 TEMPSENSOR waterproof temperature sensor (optional) with desired cable lenght (e.g. https://www.aliexpress.com/item/1005001621930325.html )
1x YF-B1 FÜLLSENSOR, flow sensor (e.g. https://www.aliexpress.com/item/32887166092.html )

## Connecting
**Watch all the polarities printed on the PCB!**
Your toggle-mode set fill sensor connects to FILLTOGGLE and should be mounted on your tank, where you want the "full" water level to be. Just put the sensor with the "touch" side towards the tank and place some tape over it to hold it. Easy peasy. Connect a cable of desired length to reach WassMon.
The other toggle-mode sensor (LIGHTTOGGLE) and the momentary-mode sensor will be mounted into the case. Solder the extra high male pin headers onto them, so that they face away from the "touch" side. Sit them into their sockets into the case and push them a little down. It should be a tight fit and they should hold in. If they are a little loose, use a drop of glue to hold them in place.
Screw the display into the case using some generic screws. Do not overtighten.

Now your case should have 5 sensors mounted in it plus a display. All should have male pin headers sticking out and they all should roughly be the same height.

Connect the flow sensor directly to the output of your tank and connect a cable of the needed length to reach WassMon.

Now populate the PCB, the LED should be mounted last and you should **not** clip off the legs. Leave them long, so the LED pops out from the case a little. This looks better. Using Q1/C2/C3 is optional, depending on your desired code. The WassMon works just fine with 8MHz internal clock for me.
Take very good care when soldering in the female pin headers into the PCB as they have to align with the male pin headers sticking out from the devices in the case.

Next drill a hole into the case where you wand the cables to go through. Use a cable entry guide to prevent bending or breaking cables.
Fiddle the cables for 12V-IN, the FÜLLSENSOR and the TEMPSENSOR through the cable entry guide and connect to the corresponding Wago clamps. Leave some slack.

Now mount the PCB into the case, this can be a little tricky, depending how accurate you soldered everything. Align all the pin headers over their corresponding counterpart and push the PCB onto the headers. Be careful not to miss or bend a pin :)
If you are done, the PCB should hold itself in place very well. Finally attach the back of the case. Again, it should be a tight fit, of not, use a drop of glue.

**Congrats, you are done :)**

## Code
As you can see, this repo only provides the hardware for WassMon and not the software, as I do not want to force stuff onto people. Use whatever software you like, write your own! It is not that hard. If - for whatever reason - you cannot or do not want to write your own software for the WassMon, get in touch (see below) and I will see what I can do for you.

## Problems/Warranty
Nothing is working? Get a magnifier and check for solder bridges, short circuits, etc. This PCB has been produced and assembled many times and works very nicely. Be very careful when assembling and connecting this hat! You may easily fry something, when mixing connections or ignoring polarity. Double check everything! I can and will not be held responsible for you destroying your equipment!

## License
Free for non-commercial use only. If you want to use this commercially or sell this PCB, you must contact me first for clarification of terms! In this case write an email to info@aj.de
