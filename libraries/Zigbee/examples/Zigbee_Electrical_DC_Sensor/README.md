# Arduino-ESP32 Zigbee DC Electrical Measurement Example

This example shows how to configure the Zigbee end device and use it as a Home Automation (HA) DC electrical measurement device that reports voltage, current, and power measurements.

# Supported Targets

Currently, this example supports the following targets.

| Supported Targets | ESP32-C6 | ESP32-H2 |
| ----------------- | -------- | -------- |

## DC Electrical Measurement Functions

 * After this board first starts up, it would be configured locally to report DC electrical measurements:
   - DC voltage in millivolts (0-5000 mV)
   - DC current in milliamps (0-1000 mA)
   - DC power in milliwatts (0-5000 mW)
 * Holding the button (BOOT) for more than 3 seconds will trigger a factory reset of the device.
 * The device reports measurements every 30 seconds if the value changes by more than the configured delta.

## Measurement Precision

The example demonstrates how to set up proper measurement precision using multiplier and divisor values:
 * Voltage: 1/1000 = 0.001 V (1 unit = 1 mV)
 * Current: 1/1000 = 0.001 A (1 unit = 1 mA)
 * Power: 1/1000 = 0.001 W (1 unit = 1 mW)

These settings ensure accurate reporting of measurements with proper decimal precision in the Zigbee network.

## Hardware Required

* A USB cable for power supply and programming

### Configure the Project

Set the ADC GPIO by changing the `analogPin` variable. By default, it's the pin `A0`.
Set the Button GPIO by changing the `button` variable. By default, it's the pin `BOOT_PIN` (BOOT button on ESP32-C6 and ESP32-H2).

#### Using Arduino IDE

To get more information about the Espressif boards see [Espressif Development Kits](https://www.espressif.com/en/products/devkits).

* Before Compile/Verify, select the correct board: `Tools -> Board`.
* Select the End device Zigbee mode: `Tools -> Zigbee mode: Zigbee ED (end device)`
* Select Partition Scheme for Zigbee: `Tools -> Partition Scheme: Zigbee 4MB with spiffs`
* Select the COM port: `Tools -> Port: xxx` where the `xxx` is the detected COM port.
* Optional: Set debug level to verbose to see all logs from Zigbee stack: `Tools -> Core Debug Level: Verbose`.

## Troubleshooting

If the End device flashed with this example is not connecting to the coordinator, erase the flash of the End device before flashing the example to the board. It is recommended to do this if you re-flash the coordinator.
You can do the following:

* In the Arduino IDE go to the Tools menu and set `Erase All Flash Before Sketch Upload` to `Enabled`.
* Add to the sketch `Zigbee.factoryReset();` to reset the device and Zigbee stack.

By default, the coordinator network is closed after rebooting or flashing new firmware.
To open the network you have 2 options:

* Open network after reboot by setting `Zigbee.setRebootOpenNetwork(time);` before calling `Zigbee.begin();`.
* In application you can anytime call `Zigbee.openNetwork(time);` to open the network for devices to join.

***Important: Make sure you are using a good quality USB cable and that you have a reliable power source***

* **LED not blinking:** Check the wiring connection and the IO selection.
* **Programming Fail:** If the programming/flash procedure fails, try reducing the serial connection speed.
* **COM port not detected:** Check the USB cable and the USB to Serial driver installation.

If the error persists, you can ask for help at the official [ESP32 forum](https://esp32.com) or see [Contribute](#contribute).

## Contribute

To know how to contribute to this project, see [How to contribute.](https://github.com/espressif/arduino-esp32/blob/master/CONTRIBUTING.rst)

If you have any **feedback** or **issue** to report on this example/library, please open an issue or fix it by creating a new PR. Contributions are more than welcome!

Before creating a new issue, be sure to try Troubleshooting and check if the same issue was already created by someone else.

## Resources

* Official ESP32 Forum: [Link](https://esp32.com)
* Arduino-ESP32 Official Repository: [espressif/arduino-esp32](https://github.com/espressif/arduino-esp32)
* ESP32-C6 Datasheet: [Link to datasheet](https://www.espressif.com/sites/default/files/documentation/esp32-c6_datasheet_en.pdf)
* ESP32-H2 Datasheet: [Link to datasheet](https://www.espressif.com/sites/default/files/documentation/esp32-h2_datasheet_en.pdf)
* Official ESP-IDF documentation: [ESP-IDF](https://idf.espressif.com)
