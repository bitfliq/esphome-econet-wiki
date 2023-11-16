## Software Installation

Setup can be done from the command line using the esphome docker image, or via a (mostly) graphical interface by using an esphome dashboard installation; see Getting Started at <https://esphome.io/index.html> for full ESPHome installation and usage instructions. Initial installation must be done over USB. After this, updates and configuration changes can be made entirely over WiFi.

Installation is a three-step process:

1. Customize the basic configuration yaml for your device and environment
2. Deploy to the device via command line or ESPHome Dashboard
3. Add your device to Home Assistant

### Step 1: Customizing the esphome-econet yaml for Your Device

Before installing, you will need to create a customized yaml for your device/environment. Start with one of the starter yaml's in in the [build-yaml directory](https://github.com/esphome-econet/esphome-econet/tree/main/build-yaml) of the repo, choosing the appropriate file for your appliance and ESP hardware (choose ESP32 for the standard ATOM Lite hardware described above):

- **Heatpump Water Heaters**: `econet-hpwh-*.yaml`
- **Tankless Water Heaters**: `econet_tlwh-*.yaml`
- **Electric Tank Water Heaters**: `econet-etwh-*.yaml`
- **HVAC Systems**: `econet_hvac-*.yaml`

At a minimum, you will want to either [put in your own WiFi network details](https://esphome.io/components/wifi) or provide a `secrets.yaml` file with the `wifi_ssid` and `wifi_password` fields configured. An example `secret.yaml` would look like:

```yaml
wifi_ssid: "your ssid"
wifi_password: "your password"
```

If you are using hardware other than the kit recommended above, you may also need to update the GPIO Pin fields. See the individual device configuration files for more customizable options.

### Step 2: Compiling and Uploading esphome-econet to Your Device

Once you've customized your YAML you can install it either by copying your yaml file (and `secrets.yaml` file) to the config directory of your esphome-dashboard installation and running the install command, or by using the ESPHome command line via Docker.

#### Installing via ESPHome in a Docker Container

Run `ls /dev/ttyUSB*` from a command line to list the USB ports currently in use.  Then, plug the USB-C cable into the ATOM and into the computer running ESPHome. Run `ls /dev/ttyUSB*` again and note the new port shown, e.g. `/dev/ttyUSB1` (there should be one more than before).  That is the port used by the ATOM ESP32 board, and is the port to which the esphome-econet program will need to be installed.

Run the following command from the directory containing your configuration file and your `secrets.yaml` to compile and upload esphome-econet to the ATOM.  This assumes that your configuration file is `example-esp32.yaml` and that the ATOM is found on `/dev/ttyUSB1`; change as necessary.

```bash
docker run --rm -v "${PWD}":/config --device=/dev/ttyUSB1 -it esphome/esphome run example-esp32.yaml
```

The program should compile and ask whether to install OTA or via USB. Choose USB.  It should then upload.  

Once uploaded, unplug the USB cable from the computer and move the device to the water heater.  Connect the RJ11/12 cable to the port on the display panel and provide power from a wall wart to the USB cable that is plugged into the ATOM.

### Step 3: Adding New Device to Home Assistant

Open Home Assistant and add a new [ESPHome Integration](https://my.home-assistant.io/redirect/config_flow_start?domain=esphome), inputting the hostname of your device (e.g. "econet-hpwh.local" by default for Heat Pump Water Heaters).  The device may be discovered automatically, in which case just accept the new device and wait a few moments.  Once added, you can visit the device's details page (via `Settings -> Devices & Services`) to see all of the provided sensors are working.