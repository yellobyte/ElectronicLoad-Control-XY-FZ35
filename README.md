# XY-FZ25 & XY-FZ35 Electronic Load Control Program
 
This program controls "Electronic Load" devices XY-FZ25 and XY-FZ35, sold on different internet sites, mainly from Asia. Instruction manuals for those devices can often be found on the resellers web sites. In folder [**Doc**](https://github.com/yellobyte/ElectronicLoad_Control_XY-FZ35/tree/main/Doc) you find some specs.

   ![github](https://github.com/yellobyte/ElectronicLoad-Control-XY-FZ35/raw/main/Doc/XY-FZ35a.jpg)

A **programmable electronic load** emulates DC or AC resistance loads required to perform functional tests of batteries, different types of power supplies, solar cells, technical equipment, etc. There are many other useful scenarios.
In the simpliest case an electronic load just sinks current (absorbes power). The amount of current can be set and the load tries to keep it stable even when the applied voltage changes.  

The XY-FZ25 is limited to 4A/25W and the XY-FZ35 to 5A/35W. That doesn't sound much but really is enough for most cases.

I use the combination program + electronic load mainly for accu/battery discharge tests and also solar power cell tests every now and then.  

## :zap: The Control Program

The program "Electronic Load" in folder [**Program**](https://github.com/yellobyte/ElectronicLoad_Control_XY-FZ35/tree/main/Program) does **display** live readings in a chart, can **save** the final chart to hard drive as **data file** (_.eld_), **bitmap** (_*.bmp_) or **csv file** (_*.csv_). Additionally it can **print** the chart and **load** a previously saved chart (_*.eld_ data file) from hard drive. That gives you the easy ability to compare the final test results of various batteries/accus/etc.  

If you associate _*.eld_ files with this program you only need to double click on them to see saved charts.

For more pics have a look at folder [**Doc**](https://github.com/yellobyte/ElectronicLoad_Control_XY-FZ35/tree/main/Doc). The program was tested and runs on Win8.1/Win10/Win11. 

![github](https://github.com/yellobyte/ElectronicLoad_Control_XY-FZ35/raw/main/Doc/Load1a.JPG)

You also find two real world charts (*.eld) in folder [**Program**](https://github.com/yellobyte/ElectronicLoad_Control_XY-FZ35/tree/main/Program). You can load them into the program and have a look at them.

### :hammer_and_wrench: Operational settings

The program lets you set various operational parameters. The most important of course is the  
- **Maximum Current**

Additionally the load will monitor various definable parameters and triggers an alarm plus turning itself off if required:

- **LVP**...Low Voltage Protection: When the voltage drops below a set value then the load will turn itself off. This is important for discharge tests on batteries in order to protect the battery.
- **OAH**...Maximum Discharge Capacity: When the load is turned on it calculates the accumulated discharge capacity (in Ah) and turns itself off when a set value has been reached. This feature too is for protecting the battery when doing discharge tests.
- **OHP**...Maximum Discharge Time: When the runtime reaches a set timespan than the load will turn itself off. Important for discharge tests. 

### :heavy_exclamation_mark: Important
Don't forget to **set the correct hardware version** of the device before controlling it (Settings->Hardware Version->25W/35W) !  

## :information_source: Installation
Just copy the 32bit or 64bit version of the executable into a folder and that's basically it.  
In case you get a windows error message trying to run the program (like "mfc140u.dll missing" or similar) depending on your Windows installation you additionally have to install the 32bit (x86) or 64bit (x64) version of the **Microsoft Visual C++ Redistributables 2019** or higher. Those packages are easily available on Microsofts websites, as of today (02/2022) from [here](https://docs.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170) for example.


## :safety_vest: XY-FZ25 & XY-FZ35 Integrated Overload Protection

The devices have different protection mechanisms built in, in order to protect themself.

- **OVP**...Over Voltage Protection: When the voltage is greater then a set value the load will turn itself off.
- **OCP**...Over Current Protection: When the current is greater then a set value the load will turn itself off.
- **OPP**...Over Power Protection: When the power it absorbes gets greater then a set value then the load will turn itself off.  

## :information_source: Wiring

The devices provide a possibility to communicate via serial port (9600,8,N,1) with TTL-level (3.3V !). They accept operating instructions and send status messages if requested.  
This program uses this option to control the devices. For that you only need a cheap **USB-TTL converter module** (mostly with IC CP210x/CH340/FTDI232) between your Laptop/PC and the device.

![github](https://github.com/yellobyte/ElectronicLoad-Control-XY-FZ35/raw/main/Doc/USB-TTL-Wiring.jpg)

**Please note:**  
Some alarms (OPP,OAH,OHP) can't be cleared via serial communication. In those cases the On/Off Button on the device itself must be pressed to end the alarm and get the device operational again. Message Boxes will tell you if that's the case.

## :clap:  Supporters

[![Stargazers repo roster for @yellobyte/ElectronicLoad-Control-XY-FZ35](https://reporoster.com/stars/yellobyte/ElectronicLoad-Control-XY-FZ35)](https://github.com/yellobyte/ElectronicLoad-Control-XY-FZ35/stargazers) 