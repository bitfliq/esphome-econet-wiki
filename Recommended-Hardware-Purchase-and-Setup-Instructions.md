## Suggested Hardware Setup

For a simple and proven platform on which to run this package you will need an RS485 interface and an ESP32 board. These are available as follows:

- One M5Stack ATOM RS485 K045 Kit: [mouser](https://www.mouser.com/ProductDetail/M5Stack/K045?qs=81r%252BiQLm7BQ2ho0A5VkoNw%3D%3D) has them while stock is available. M5Stack has discontinued the combined K045 Package.
- Or, the same thing, but ordered as two separate parts: The M5Stack *A131 RS485 Base* [M5Stack A131](https://shop.m5stack.com/products/atomic-rs485-base) and the M5Stack *C008 Atom Lite* [M5Stack C008](https://shop.m5stack.com/products/atom-lite-esp32-development-kit?variant=32259605200986).
  - Both Digikey and Mouser have the Atom. The RS485 Base is not available from either vendor as of this update.
    - [Digikey C008](https://www.digikey.com/en/products/detail/m5stack-technology-co-ltd/C008/12088545) (Never mind the image Digikey displays, see the datasheet)
    - [Mouser C008](https://www.mouser.com/ProductDetail/M5Stack/C008?qs=sGAEpiMZZMuqBwn8WqcFUj1SFkunHY10TJ3jnDGC7E4NSjPubczP2Q%3D%3D)

- One cable: [digikey](https://www.digikey.com/en/products/detail/assmann-wsw-components/AT-S-26-6-4-S-7-OE/1972674) or [mouser](https://www.mouser.com/ProductDetail/Bel/BC-64SS007F?qs=wnTfsH77Xs4cyAAV7TLsUQ%3D%3D), or any other similar RJ11/12 cable as long as it is 6P/6C or 6P/4C (we only need 3 wires for this but the 6 wire version is fine too)

You can also use many other ESP32 or ESP8266 development boards with the required RS485 converter - the above is just an easy pre-wired setup that only requires you to cut, strip, and attach 3 wires to the screw terminal with no soldering required. See [these schematics](https://github.com/esphome-econet/esphome-econet/wiki/Schematics) how to DIY wire an ESP32 or ESP8266 with an RS485-TTL module.

### Installation Overview

Three wires from a RJ11/12 cable attach via screw terminals to the RS485 interface, and a USB-C cable provides power and an initial programming interface to the ATOM.  Once deployed, the ATOM communicates via WiFi to the local network and the RS485 converter provides the interface between the water heater and the ATOM.  No configuration is required for the converter. The esphome-econet software is compiled and loaded onto the ATOM using standard ESPHome tools.

### Hardware Installation

Cut the connector off one one end of the RJ11/12 cable, then strip and connect the wires to the RS485 device's screw terminals. Pin 3 to B, Pin 4 to A, and Pin 5 to GND.  A and B are for data communication, and G is ground. 12V is left empty.

*NOTE: Wire colors can vary from cable to cable. Ensure you are matching the pins as shown in the diagram below regardless of cable color, i.e. Pin 3 to B, Pin 4 to A, Pin 5 to G.*

```text
    6P4C RJ11/RJ12 male connector end view   
    
               +---------+
            1  ---       |
            2  ---       +--+      
        B   3  ---          |     
        A   4  ---          |        
       GND  5  ---       +--+
            6  ---       |
               +---------+
```

This picture shows a correctly wired setup. While wire colors can vary, this images shows the most common color layout reported by users (Green -> B, Red -> A, Black -> GND):

<img src="https://github.com/esphome-econet/econet-docs/blob/main/photos-and-screenshots/Correctly-Wired-K045.jpeg?raw=true" alt="A correctly wired K045 unit." width=50%>

**If your device is not working please double-check your wiring. Swapped wires are the most common cause of units not reading data.**