---
layout: page
title: "Particulate matter Sensor"
description: "Instructions on how to integrate particulate matter (dust) sensors with Home Assistant."
date: 2016-08-11 12:00
sidebar: true
comments: false
sharing: true
footer: true
logo: serial_pm.png
ha_category: DIY
ha_release: 0.26
ha_iot_class: "Local Polling"
---

Particulate matter sensors measure the amount of very small particles in the air. A short introduction how these sensors work can be found on [Open Home Automation](https://www.open-homeautomation.com/2016/07/19/measuring-air-quality/).

Cheap LED based sensors usually use a GPIO interface that is hard to attach to computers. However, there are a lot of laser LED based sensors on the market that use a serial interface and can be [connected to your Home Assistant system easily with an USB to serial converter](https://www.open-homeautomation.com/2016/07/20/connecting-an-particulate-matter-sensor-to-your-pc-or-mac/).

At this time, the following sensors are supported:

* oneair,s3
* novafitness,sds021
* novafitness,sds011
* plantower,pms1003
* plantower,pms5003
* plantower,pms7003
* plantower,pms2003
* plantower,pms3003

To use your PM sensor in your installation, add the following to your `configuration.yaml` file:

```yaml
sensor:
  - platform: serial_pm
    serial_device: /dev/tty.SLAB_USBtoUART
    name: Nova
    brand: novafitness,sds011
```

- **serial_device** (*Required*): The serial port to use. On *nix systems, it can often be identified by `$ ls /dev/tty*`
- **name** (*Optional*): The name displayed in the frontend.
- **brand** (*Required*): Manufacturer and type of the sensor.

