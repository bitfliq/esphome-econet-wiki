These schematics are based on https://github.com/syssi/esphome-solax-x1-mini#schematics and https://github.com/KlausLi/Esp-Soyosource-Controller/blob/main/BastelPlan3000_Soyosource_Controller_by_BavarianSuperGuy.png

#### RS485-TTL module without flow control pin

(This is for modules such as HW-0519)

```text
             RS485                        UART
  ┌─────┐              ┌─────────────┐           ┌─────────────────┐
  │     │              │          GND│<--------->│GND              │
┌-┘   3 │<-----B- ---->│  RS485   RXD│<--------->│RX    ESP32/     │
|     4 │<---- A+ ---->│  to TTL  TXD│<--------->│TX    ESP8266    │
└-┐   5 │<--- GND ---->│  module  VCC│<--------->│3.3V          VCC│<--
  │     │              │             │           │              GND│<--
  └─────┘              └─────────────┘           └─────────────────┘

```

Note: for some RS485-TTL modules such as MAX13487 you need to connect the RX pin of the ESP board to the TX pin of the RS485-TTL module, and the TX pin to the RX pin, see wiring with photos [here](https://github.com/esphome-econet/esphome-econet/issues/130).

#### RS485-TTL module with flow control pin

(This is for modules such as MAX485)

```text
             RS485                        UART
  ┌─────┐              ┌─────────────┐           ┌─────────────────┐
  │     │              │           DI│<--------->│TX               │
┌-┘   3 │<-----B- ---->│  RS485    DE│<--┐       │         ESP32/  │
|     4 │<---- A+ ---->│  to TTL   RE│<--┴------>│GPIO0   ESP8266  │
└-┐   5 │<--- GND ---->│  module   RO│<--------->│RX               │
  │     │              │             │           │                 │
  └─────┘              │          VCC│<--------->│3.3V          VCC│<--
                       │          GND│<--------->│GND           GND│<--
                       └─────────────┘           └─────────────────┘
```

Please make sure to power the RS485 module with 3.3V because it affects the TTL (transistor-transistor logic) voltage between RS485 module and ESP.

If you have a module with a flow control pin you need to add the following in your yaml (you need to match the actual pin you used):

```yaml
econet:
  flow_control_pin: GPIO0
```