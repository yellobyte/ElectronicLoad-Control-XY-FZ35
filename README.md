# XY-FZ25 & XY-FZ35 Electronic Load Control Program
 
This program controls "Electronic Load" devices XY-FZ25 and XY-FZ35, sold on different webshops, mainly from Asia. Most of them provide detailed instruction manuals as well. In folder [**Doc**](https://github.com/yellobyte/ElectronicLoad_Control_XY-FZ35/tree/main/Doc) you find some specs.

<p align="center"><img src="https://github.com/yellobyte/ElectronicLoad-Control-XY-FZ35/raw/main/Doc/XY-FZ35a.jpg" width="400"/></p>

A **programmable electronic load** emulates DC or AC resistance loads required to perform functional tests on batteries, all sorts of power supplies, solar cells, technical equipment, etc. There are many other useful scenarios.
In the simplest case an electronic load just sinks current (absorbes power). The amount of current can be set and the load tries to keep it stable even when the applied voltage changes.  

The XY-FZ25 is limited to 4A/25W and the XY-FZ35 to 5A/35W. That doesn't sound much but really is enough for most cases. I use the combination program + electronic load mainly for battery/accumulator discharge tests and solar power cell tests every now and then.  

## :zap: The Control Program

The program "Electronic Load" in folder [**Program**](https://github.com/yellobyte/ElectronicLoad_Control_XY-FZ35/tree/main/Program) does **display** live readings in a chart. Furthermore it can:  
- **save** charts as **data file** (_.eld_), **bitmap file** (_*.bmp_) or **csv file** (_*.csv_)
- **print** charts
- **load** previously saved charts (_*.eld_ data files), which gives you the easy ability to compare the various test results later on

If you **associate** _*.eld_ files with this program you only need to double click them to see saved charts.

For more pics have a look at folder [**Doc**](https://github.com/yellobyte/ElectronicLoad_Control_XY-FZ35/tree/main/Doc). The program was tested and runs on Win8.1/Win10/Win11. 

![github](https://github.com/yellobyte/ElectronicLoad_Control_XY-FZ35/raw/main/Doc/Load1a.JPG)

You find some real world charts (*.eld) in folder [**Program**](https://github.com/yellobyte/ElectronicLoad_Control_XY-FZ35/tree/main/Program). Load them into the program and have a look at them.

### :hammer_and_wrench: Operational settings

The program lets you set various operational parameters. The most important of course is the  
- **Maximum Load Current**

As of V1.5.1 the maximal adjustable current value can be limited with a REG_EXPAND_SZ registry entry:  
&ensp;&ensp;&ensp;&ensp; _HKEY_CURRENT_USER\Software\YelloByte\ElectronicLoad\CurrentLimit_  
Simply edit the supplied file _current_limit.reg_ in folder [**Program**](https://github.com/yellobyte/ElectronicLoad_Control_XY-FZ35/tree/main/Program) and import it into your PC's registry.  
The control program will then limit the possible current setting to the given value. After starting the program the event window will tell if a current limit has been applied.

Additionally the load will monitor various definable parameters and trigger an alarm plus turn itself off if required:

- **LVP**...Low Voltage Protection: When the load voltage drops below a set limit. This is important for discharge tests in order to protect the accumulator/battery.
- **OAH**...Maximum Discharge Capacity: When the load reaches a defined accumulated discharge capacity limit (in Ah). This feature too is for protecting the accumulator/battery when doing discharge tests.
- **OHP**...Maximum Discharge Time: When the runtime reaches a set timespan. Important for tests that need to run for hours or even days. 

Changing those values can be done either via the programs menu (Settings) or by clicking with the mouse on the value in the main dialog. The respective dialog will then show up.

Mouse clicks on the left chart axis will change its scale. This can also be done via menu of course.

### :heavy_exclamation_mark: Important I
Don't forget to set the correct **hardware version** of the device before controlling it (Settings->Hardware Version->25W/35W) !  

### :bangbang: Important II
XY-FZx5 devices sold on various Chinese sales platforms (e.g. Aliexpress) use the official **communication protocol** as shown [here](https://github.com/yellobyte/ElectronicLoad-Control-XY-FZ35/raw/main/Doc/Communication.jpg). Such devices need the protocol setting 1 (Settings->Protocol Version->Version 1 (Standard)).  

For whatever reason, devices sold on amazon.co.jp use a different protocol which is documented nowhere and also behave slightly different. Protocol setting 2 is required here (Settings->Protocol Version->Version 2). Many thanks to Takano from Japan (https://ps-tec.jp) for his support and especially for sponsoring me such device which only made it possible to integrate this protocol into the control program.

## :information_source: Installation
Depending on your Windows architecture copy the 32bit or 64bit version of the executable into a program folder and that's basically it.  

In case you get a windows error message trying to run the program (like "mfc14xx.dll missing" or similar) depending on your Windows installation you additionally need to install the **Microsoft Visual C++ Redistributables 2022 (x86/x64)** or higher. Momentarily (02/2024) they are available from [here](https://docs.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170).  

## :safety_vest: XY-FZ25 & XY-FZ35 Integrated Overload Protection

The devices have different self protection mechanisms built in and will turn off when triggered:

- **OVP**...Over Voltage Protection: When the load voltage gets higher than the set OVP voltage limit.
- **OCP**...Over Current Protection: When the load current gets higher than the set OCP current limit.
- **OPP**...Over Power Protection: When the power it absorbes gets greater than the set OPP power limit.

Pressing CTRL+L will retrieve the actual protection limits from the device and show them in the program window (top left section), provided the device is properly connected.  

If reading limits is not possible a warning is displayed. Same when sending limits to the device hasn't been successful or the device didn't answer as expected. In all error cases the values in section "Protection Limits" will stay at zero.  

**Please note:**  
Some alarms (OPP, OAH, OHP) can't be cleared via serial communication. In such cases the On/Off Button on the device itself must be pressed to end the alarm and get the device operational again. Message Boxes will tell you if that's the case.  

## :information_source: Wiring

The devices provide a possibility to communicate via serial port (9600,8,N,1) with TTL-level (3.3V !). They accept operating instructions and send status messages if requested.  

This program uses this option to control the devices. For that you only need a cheap **USB-TTL converter module** (mostly with IC CP210x/CH340/FTDI232) between your Laptop/PC and device.

![github](https://github.com/yellobyte/ElectronicLoad-Control-XY-FZ35/raw/main/Doc/USB-TTL-Wiring.jpg)

## :information_source: Revision history

- 2025/04: V1.5.1, Registry entry to limit the maximal adjustable current value.
- 2025/01: V1.5.0, Integration of a new communication protocol needed for XY-FZx5 devices sold on amazon.co.jp. Improved export function for *.csv files.
- 2024/03: V1.4.0, New settings option will request the system to stay awake and not enter sleep mode while load is switched ON. This will not work on all systems though, esp. not on systems with active "modern standby" feature (e.g. newer laptops) while running on battery. You actually have to try it out on your particular machine before you can rely on it.
- 2024/02: V1.3.2, If the voltage drops from above LVP straight down to 0.00V then the load unexpectedly stays on and does not report a LVP alarm. This is now detected and the load is then instructed to switch off. This scenario can happen if the battery has been disconnected manually or the internal battery BMS turned the battery output off before the decreasing battery voltage hit the set LVP level.
- 2024/02: V1.3.1, A nasty 2-digit COM error fixed. Load current can now be set to 0.00A which is helpful for monitoring only. Option to display LVP voltage in chart added. Horizontal scrolling on event list box activated. 
- 2022/03: V1.2.0, Error messages improved.  
- 2022/02: V1.1.0, Export chart to *.csv added. 7-digit display for load status added. VS2022.  
- 2019/10: V1.0.5, Some bugfixing to catch all alarms properly.  
- 2019/05: V1.0.0, Initial version, built with MS Visual Studio 2019. 

## :relaxed: Postscript

If you run into trouble with this program or have suggestions how to improve it, feel free to contact me.
