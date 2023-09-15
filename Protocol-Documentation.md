
## Protocol Documentation

Example commands to change a heat pump water heater settings [here](https://github.com/esphome-econet/esphome-econet/blob/506a2ff15b94b1fcc48e3254fc29214be74fc517/m5atom-rs485-econet.yaml)

Decode this into Charcode [here](https://gchq.github.io/CyberChef/#recipe=From_Charcode('Space',16)Strings('Single%20byte',4,'Alphanumeric%20%2B%20punctuation%20(A)',false,false,false/disabled)&input=MHg4MCwgMHgwMCwgMHgxMiwgMHg4MCwgMHgwMCwgMHg4MCwgMHgwMCwgMHgwMywgMHg0MCwgMHgwMCwgMHgxMiwgMHgwMCwgMHgwMCwgMHgxRiwgMHgwMSwgMHgwMSwgMHgwMCwgMHgwNywgMHgwMCwgMHgwMCwgMHg1NywgMHg0OCwgMHg1NCwgMHg1MiwgMHg1MywgMHg0NSwgMHg1NCwgMHg1MCwgMHg0MiwgMHhGOCwgMHgwMCwgMHgwMCwgMHhFNCwgMHhFRQ)

Addresses

Commands

- READ_COMMAND 0x1E (30)
- ACK 0x06 (6)
- WRITE_COMMAND 0x1F (31)

Object Strings

| String        | Units         | Gas Tankless | Heat Pump    | Electric | Values     |
| ------------- | ------------- |------------- |------------- |--------- |------------|
| WHTRENAB      |               | Y            |Y             |          | 1,0        |
| WHTRSETP      |               | Y            |Y             |          |            |
| WHTRMODE      |               | Y            |              |          |            |
| WHTRCNFG      |               |              |Y             |          | 0,1,2,3,4  |
| FLOWRATE      |               | Y            |              |          |            |
| TEMP_OUT      |               | Y            |              |          |            |
| TEMP__IN      |               | Y            |              |          |            |
| WTR_USED      |               | Y            |              |          |            |
| WTR_BTUS      |               | Y            |              |          |            |
| IGNCYCLS      |               | Y            |              |          |            |
| BURNTIME      |               | Y            |              |          |            |

Credits:

- <https://github.com/syssi/esphome-solax-x1-mini>
- <https://github.com/glmnet/esphome_devices>
- <https://github.com/esphome/esphome/tree/dev/esphome/components/tuya>