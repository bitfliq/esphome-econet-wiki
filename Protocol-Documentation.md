Addresses

Commands
* READ_COMMAND (30)
* ACK (6)
* WRITE_COMMAND (31)

Object Strings

| String        | Units         | Gas Tankless | Heat Pump    | Electric |
| ------------- | ------------- |------------- |------------- |--------- |
| WHTRSETP      | hex float     |              |       X       |          |
| Content Cell  | Content Cell  |              |              |          |


set temperature to 124f = WHTRSETP 0x42, 0xF8, 0x00, 0x00 = 124 (decimal converted from hex float)
set temperature to 110f = WHTRSETP 0x42, 0xDC, 0x00, 0x00 = 110 (decimal converted from hex float)
"Enable" = WHTRENAB 0x3F, 0x80, 0x00, 0x00 = 1 (decimal converted from hex float)
"Disable" = WHTRENAB 0x00, 0x00, 0x00, 0x00
"Off" = WHTRCNFG 0x00, 0x00, 0x00, 0x00
"Energy Saver" = WHTRCNFG 0x3F, 0x80, 0x00, 0x00 = 1 (decimal converted from hex float)
"Heat Pump" = WHTRCNFG 0x40, 0x00, 0x00, 0x00 = 2 (decimal converted from hex float)
"High Demand" = WHTRCNFG 0x40, 0x40, 0x00, 0x00 = 3 (decimal converted from hex float)
"Electric/Gas" = WHTRCNFG 0x40, 0x80, 0x00, 0x00 = 4 (decimal converted from hex float)