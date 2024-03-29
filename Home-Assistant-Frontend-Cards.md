
Mushroom Dark Theme       |  Waves Dark Theme
:-------------------------:|:-------------------------:
![Mushroom Dark Theme](https://github.com/esphome-econet/esphome-econet/assets/9987465/f30f3c85-622b-4ea7-87b7-1f542cff6d26) | ![Waves Dark](https://github.com/esphome-econet/esphome-econet/assets/9987465/beb66354-a930-48f2-8f71-bc775a27e8ac) |


### What's Displayed (Water Heater):
- The state of the water heater compressor (`Currently: Idle` or `Currently: ON`)
- The water heater set temperature
- The state of the heating element
- The current mode of the water heater
- The available hot water

### Card Dependencies:
- [Card mod](https://github.com/thomasloven/lovelace-card-mod)
- [Mushroom Card](https://github.com/piitaya/lovelace-mushroom)
- [Simple Thermostat](https://github.com/nervetattoo/simple-thermostat)
- [Stack in Card](https://github.com/custom-cards/stack-in-card)

A custom picture of the water heater is not required for the code to work simply swap out `picture` for `icon` if that's desired. I'll attach the picture I used for my heatpump water heater and thermostat.

- Get a picture preferably 600x600 or less sometimes I get lucky and find one that size already. If not I have to shrink the picture using picture resizing tools [online](https://www.adobe.com/express/feature/image/resize) ideally while keeping the zoom in on the object to avoid the picture looking too small on the frontend.
- Use a background remover online to remove the background such as [adobe express background remover](https://express.adobe.com/tools/remove-background/#)
- Upload the picture to a folder home assistant has access to. I use `www/icons/custom_icons/econet-water-heater.png` if you don't already know `www` is read in by homeassistant as `local`
- That's it now you can use pictures across the frontend whether that's entity customizations with entity pictures being specified in yaml, the mushroom template card or others that accept pictures.
### YAML Breakdown
- First caveat, this was designed for mobile use and specifically a Samsung galaxy and worked well on an s22 ultra and s23 ultra. You may need to play with padding to get it to fit your screen the way it fits mine.
- The styling done on the simple thermostat card comes from the [css variables](https://github.com/nervetattoo/simple-thermostat#css-vars-for-theming) provided from the card.

<details>
  <summary>Water Heater YAML </summary>

```yaml

type: custom:stack-in-card
keep:
  margin: false
  box_shadow: false
  background: false
cards:
  - type: grid
    square: false
    columns: 2
    cards:
      - type: custom:mushroom-template-card
        primary: Water Heater
        secondary: >
          Currently: {{
          iif(states('binary_sensor.econet_heatpump_water_heater_compressor_relay')
          == 'on','Running','Idle') }}
        picture: local/icons/custom_icons/econet-water-heater.png
        card_mod:
          style: |
            mushroom-shape-icon {
              --shape-color: none !important;
            }
            ha-card {
              padding-bottom: 14px !important;
            }
        entity: climate.econet_heatpump_water_heater_water_heater
        tap_action:
          action: more-info
      - type: vertical-stack
        cards:
          - type: custom:simple-thermostat
            style: |
              ha-card {
                --st-spacing: 0px;
              }
              ha-card .current--value {
                color: #ffffff;
              }
              header {
                margin-bottom: 10px !important;
                padding-bottom: 0px !important;
              }
              ha-card .thermostat-trigger { 
                color: #6f6f6f;
              }
            entity: climate.econet_heatpump_water_heater_water_heater
            header:
              name: false
              icon: false
            decimals: '0'
            fallback: Error
            hide:
              temperature: true
              state: true
            layout:
              mode:
                names: false
                icons: false
                headings: false
              step: row
            step_size: '1'
            control:
              preset:
                Eco Mode: false
                Electric: false
                Heat Pump: false
                High Demand: false
                Vacation: false
                'Off': false
              hvac:
                auto: false
                'off': false
  - type: custom:mushroom-chips-card
    card_mod:
      style:
        div:
          mushroom-template-chip:nth-child(2): |
            ha-card {
              --chip-box-shadow: none;
              --chip-background: none;
              --chip-spacing: 0px;
              --chip-padding: 0 0.2em
              }
    alignment: justify
    chips:
      - type: template
        content: '{{states(entity) | float(0) | round(0) }} °F'
        entity: sensor.econet_heatpump_water_heater_upper_tank_temperature
        icon: mdi:thermometer-water
        tap_action:
          action: more-info
        icon_color: red
        style: |
          ha-card {
            margin-left: 6px;
          }
      - type: template
        entity: binary_sensor.econet_heatpump_water_heater_fan_control
        content: >
          {{
          states('sensor.econet_heatpump_water_heater_water_heater_heating_element_state')
          }}
        icon: mdi:heating-coil
        icon_color: >-
          {% set status =
          states('sensor.econet_heatpump_water_heater_water_heater_heating_element_state')
          %} {% if status != 'Off' %} red {% elif status == 'Off' %} gray {%
          else %} blue {% endif %}
        tap_action: none
      - type: template
        tap_action:
          action: more-info
        content: |
          {{ state_attr(entity,'preset_mode') | upper }}
        entity: climate.econet_heatpump_water_heater_water_heater
        icon: mdi:water-boiler
        icon_color: blue
        hold_action:
          action: none
      - type: template
        double_tap_action:
          action: none
        content: '{{ states(''sensor.econet_heatpump_water_heater_hot_water'') }}%'
        entity: ssensor.econet_heatpump_water_heater_hot_water
        icon: mdi:water
        icon_color: blue
        tap_action:
          action: none
        hold_action:
          action: none
card_mod:
  style: |
    ha-card {
    --ha-card-background: transparent
```
</details>

### Custom Pictures

![Heat pump water heater](https://github.com/esphome-econet/esphome-econet/assets/9987465/a978e8c0-1579-4d8c-b758-06d66d353947)
![Thermostat](https://github.com/esphome-econet/esphome-econet/assets/9987465/660d5826-180e-4b54-b27f-e30e4a89d2d3)
