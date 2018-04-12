---
layout: page
title: "HTU21D Temperature and humidity sensor"
description: "Instructions on how to integrate a HTU21D Temperature and humidity sensor into Home Assistant."
date: 2017-06-10 00:00
sidebar: true
comments: false
sharing: true
footer: true
logo: raspberry-pi.png
ha_category: Sensor
ha_release: 0.48
ha_iot_class: "Local Push"
---


The `htu21d` sensor platform allows you to read the temperature and humidity from a [HTU21D sensor](http://www.datasheetspdf.com/PDF/HTU21D/779951/1) connected via [I2c](https://en.wikipedia.org/wiki/I²C) bus (SDA, SCL pins).

Tested devices:

- [Raspberry Pi](https://www.raspberrypi.org/)

To use your HTU21D sensor in your installation, add the following to your `configuration.yaml` file:

```yaml
# Example configuration.yaml entry
sensor:
  - platform: htu21d
```

Configuration variables:

- **name** (*Optional*): The name of the sensor
- **i2c_bus** (*Optional*): I2c bus where the sensor is. Defaults to 1, for Raspberry Pi 2 and 3.


## {% linkable_title Customizing the sensor data %}

Give the values friendly names and icons, add the following to your `customize:` section.

```yaml
# Example configuration.yaml entry
customize:
  sensor.htu21d_sensor_temperature:
    icon: mdi:thermometer
    friendly_name: "Temperature"
  sensor.htu21d_sensor_humidity:
    icon: mdi:weather-rainy
    friendly_name: "Humidity"
```

To create a group, add the following to your `groups` section.

```yaml
# Example configuration.yaml entry
group:
  ambient_sensor:
    name: HTU21D Environment sensor
    entities:
      - sensor.htu21d_sensor_temperature
      - sensor.htu21d_sensor_humidity
```

## {% linkable_title Directions for installing smbus support on Raspberry Pi %}

Enable I2c interface with the Raspberry Pi configuration utility:

```bash
# pi user environment: Enable i2c interface
$ sudo raspi-config
```

Select `Interfacing options->I2C` choose `<Yes>` and hit `Enter`, then go to `Finish` and you'll be prompted to reboot.

Install dependencies for use the `smbus-cffi` module and enable your _homeassistant_ user to join the _i2c_ group:

```bash
# pi user environment: Install i2c dependencies and utilities
$ sudo apt-get install build-essential libi2c-dev i2c-tools python-dev libffi-dev

# pi user environment: Add homeassistant user to the i2c group
$ sudo addgroup homeassistant i2c

# pi user environment: Reboot Raspberry Pi to apply changes
$ sudo reboot
```

### {% linkable_title Check the i2c address of the sensor %}

After installing `i2c-tools`, a new utility is available to scan the addresses of the connected sensors:

```bash
$ /usr/sbin/i2cdetect -y 1
```

It will output a table like this:
```text
     0  1  2  3  4  5  6  7  8  9  a  b  c  d  e  f
00:          -- -- -- -- -- -- -- -- -- -- -- -- --
10: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
20: -- -- -- 23 -- -- -- -- -- -- -- -- -- -- -- --
30: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
40: 40 -- -- -- -- -- UU -- -- -- -- -- -- -- -- --
50: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
60: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
70: -- -- -- -- -- -- -- 77
```

So you can see the sensor is present at the **0x40** address (there are more i2c sensors in that Raspberry Pi).
