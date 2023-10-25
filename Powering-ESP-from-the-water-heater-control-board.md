Below is copied from what elmoret said at
https://discord.com/channels/1148015790038188073/1148327349620838511/1162186716635988009

Also - has any probed out the other pins on that port? Might there be 3.3v or 5v lurking? Would be nice to not have to run power externally. I'm sure I could grab power from somewhere on the water heater's control board, but would be nice to keep it contained to that port.

Pulled out the control board on my XE50T10H45U0

<img width="800" src="https://github.com/esphome-econet/esphome-econet/assets/9987465/1a3ade79-ec41-4dd2-bb18-120e11d90ec8">
<img width="800" src="https://github.com/esphome-econet/esphome-econet/assets/9987465/e95d3641-3f3a-47c2-a68d-6dba4567ff79">
<img width="800" src="https://github.com/esphome-econet/esphome-econet/assets/9987465/93add6cf-152e-436e-98e9-2ad9651496d1">
<img width="800" src="https://github.com/esphome-econet/esphome-econet/assets/9987465/ae2ea860-c2ec-412e-9635-7cf8ca81b222">

It doesn't look like pins 1/6 of the RJ12 port are of any use. I see 300kohms to ground on pin 1 (towards the white connector next to the RJ12 port). I see open circuit on pin 6 to ground. 

There's a test point with 3.3v over on the edge of the board. 3.3v to ground is ~2.2kohms. I see 2.2kohms to ground up on J32, so there's probably 3.3v up there. Looks like that's the touchpanel connector.

There's 5v down at the bottom of the board, on J30. There's a DC/DC down there, a AP62200WU - so the 5v is probably just on that port I'd guess. No idea what that port is for, from the owners manual, maybe its for the anode depletion rod? Wasn't connected on my unit

<img width="359" src="https://github.com/esphome-econet/esphome-econet/assets/9987465/f3789296-b05f-4398-88eb-989b957bf84e">


MCU is a Renesas Electronics R5F52318ADFP. Wifi is a Anatel 01874-16-03657
J31 doesn't appear to have anything useful on it, a ground and two seemingly-not-power pins

Putting it back together now. If anyone else is interested, its pretty easy. Bezel pops off, 2 screws remove the assembly from the chassis, then there's a black plastic cover on the back that looks like it might be heatstaked to the mounting holes but actually pops off with a bit of force

I tacked a lead onto the 3.3v test pad, so I don't have to run power or a cable to the water heater anymore. Snaked it out through the opening for the RJ12, everything self-contained now

![C40873A0-BDD5-492E-89D2-1E4D63DBB2EE](https://github.com/esphome-econet/esphome-econet/assets/9987465/8c1e6a7b-f9ee-4ccd-b32d-48e14fa79483)
