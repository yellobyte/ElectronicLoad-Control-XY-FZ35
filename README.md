# XY-FZ35 Electronic Load Control Program
 
This program can be used to control "Electronic Load" devices XY-FZ25 and XY-FZ35, sold on different internet sites, mainly from Asia. Instruction manuals for those devices can often be found on the resellers web sites. In folder [**Doc**](https://github.com/yellobyte/ElectronicLoad_Control_XY-FZ35/blob/main/Doc) you find some specs.

![github](https://github.com/yellobyte/ElectronicLoad-Control-XY-FZ35/blob/main/Doc/XY-FZ35.jpg)

A programmable electronic load emulates DC or AC resistance loads required to perform functional tests of batteries, power supplies or solar cells.
In the simpliest case an electronic load just sinks current (absorbes power). The amount of current can be set and the load tries to keep it stable even when the applied voltage changes.

## The Control Program ##

I'm using the combination program + electronic load mainly to do accu/battery discharge tests and sometimes for testing solar power cells. The program displays a chart, can write the final chart to hard drive, load a chart from hard drive, print the chart, etc.
For more pics pls look in folder [**Doc**](https://github.com/yellobyte/ElectronicLoad_Control_XY-FZ35/blob/main/Doc). You find the executable in folder [**Program**](https://github.com/yellobyte/ElectronicLoad_Control_XY-FZ35/blob/main/Program). The program runs on Win8.1/Win10. In rare cases you need to install the visual studio 2017 runtime libraries (easily found on the internet).

![github](https://github.com/yellobyte/ElectronicLoad_Control_XY-FZ35/blob/main/Doc/Load1a.JPG)

You find a few real world charts in folder [**Program**](https://github.com/yellobyte/ElectronicLoad_Control_XY-FZ35/blob/main/Program). You can load them into the program and have a look at them.

## Wiring ##

The devices provide a possibility to communicate via serial port (9600,8,N,1) with TTL-level (3.3V !). This program uses this option to control the devices.
The only thing needed is a cheap USB-TTL converter between PC and the load.

![github](https://github.com/yellobyte/ElectronicLoad-Control-XY-FZ35/blob/main/Doc/USB-TTL-Wiring.jpg)

## XY-FZ25 & XY-FZ35 Integrated Overload Protection ##

The devices have different protection mechanisms built in, in order to protect themself.

- OVP...Over Voltage Protection: When the voltage is greater then a set value the load will turn itself off.
- OCP...Over Current Protection: When the current is greater then a set value the load will turn itself off.
- OPP...Over Power Protection: When the power it absorbes gets greater then a set value then the load will turn itself off.

When turned on the load will monitor various parameters and triggers an alarm plus turning itself off if required:
- LVP...Low Voltage Protection: When the voltage drops below a set value then the load will turn itself off. This is important for discharge tests on batteries in order to protect the battery.
- OAH...Maximum Discharge Capacity: When the load is turned on it calculates the accumulated discharge capacity (in Ah) and turns itself off when a set value has been reached. This feature too is for protecting the battery when doing discharge tests.
- OHP...Maximum Discharge Time: When the runtime reaches a set timespan than the load will turn itself off. Important for discharge tests. 

Please note:   
Some alarms (OPP,OAH,OHP) can't be cleared via serial communication. In those cases the On/Off Button on the device itself must be pressed to end the alarm and get the device operational again. Message Boxes will tell you if that's the case.

## Important: ##
Don't forget to set the hardware version of the device before controlling the device (Settings->Hardware Version->25W/35W) !