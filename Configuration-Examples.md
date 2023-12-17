## Use Ethernet/PoE Instead of Wi-Fi

```yaml
ethernet:
  type: IP101
  mdc_pin: GPIO23
  mdio_pin: GPIO18
  clk_mode: GPIO0_IN
  phy_addr: 1
  power_pin: GPIO5

# Remove all things related to Wifi as the PoESP32 series does not support it
 wifi: !remove
 ap: !remove
 captive_portal: !remove
 improv_serial: !remove

 platform: !remove wifi_signal
```

## m5Stack ATOM Lite Customizations

```yaml
substitutions:
  board: m5stack-atom

binary_sensor:
  - platform: gpio
    id: atom_button
    pin:
      number: GPIO39
      inverted: true
    name: "ATOM Lite Button"
    icon: "mdi:gesture-tap-button"
    entity_category: "diagnostic"
    disabled_by_default: true

light:
  - platform: esp32_rmt_led_strip
    name: "ATOM Lite LED"
    id: atom_led
    pin: GPIO27
    chipset: SK6812
    num_leds: 1
    rmt_channel: 0
    rgb_order: GRB
    icon: "mdi:led-off"
    entity_category: "config"
    disabled_by_default: true
    effects:
      - random:
      - flicker:
      - addressable_rainbow:
      - pulse:
          name: "Slow Pulse"
          transition_length: 1.5s
          update_interval: 2s
      - pulse:
          name: "Fast Pulse"
          transition_length: 0.5s
          update_interval: 0.5s

output:
  - platform: template
    id: atom_led_output
    type: binary
    write_action:
      if:
        condition:
          lambda: return state;
        then:
          - light.turn_on: atom_led
        else:
          - light.turn_off: atom_led
```