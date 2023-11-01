If you don't have an electrical outlet nearby to power the ESP board, none of the pins of the RJ12 port provide power, but you can get power from the water heater control board.

If you have M5Stack A131 RS485 Base you should be able to power via the 12V test pad on the control board. If you have ESP32 or ESP8266 and a generic RS485 converter you can power via the 3.3V test pad.

Thanks to elmoret at
https://discord.com/channels/1148015790038188073/1148327349620838511/1162186716635988009

"If anyone else is interested, it's pretty easy. Bezel pops off, 2 screws remove the assembly from the chassis, then there's a black plastic cover on the back that looks like it might be heatstaked to the mounting holes but actually pops off with a bit of force

I tacked a lead onto the 3.3v test pad, so I don't have to run power or a cable to the water heater anymore. Snaked it out through the opening for the RJ12, everything self-contained now"

![C40873A0-BDD5-492E-89D2-1E4D63DBB2EE](https://github.com/esphome-econet/esphome-econet/assets/9987465/8c1e6a7b-f9ee-4ccd-b32d-48e14fa79483)

![XE50T10H45U0 front](https://github.com/esphome-econet/esphome-econet/assets/9987465/6a1fb947-5125-4c17-8064-d691ebeaac7a)

![image](https://github.com/esphome-econet/esphome-econet/assets/9987465/f88b8259-446b-4f4f-be45-723f90600ace)
