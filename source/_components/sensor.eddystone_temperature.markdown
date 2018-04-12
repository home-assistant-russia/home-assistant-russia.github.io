---
layout: page
title: "Eddystone Beacon"
description: "Instructions on how to integrate Eddystone beacons with Home Assistant in order to receive temperature data."
date: 2017-03-26 01:00
sidebar: true
comments: false
sharing: true
footer: true
logo: eddystone.png
ha_category: DIY
ha_release: 0.42
ha_iot_class: "Local Polling"
---

The `eddystone_temperature` sensor platform reads temperature information from Bluetooth LE advertisements transmitted by [Eddystone](https://en.wikipedia.org/wiki/Eddystone_(Google)) beacons. Your beacons must be configured to transmit UID frames (for identification) and TLM frames (for temperature).
All beacons that support the Eddystone protocol, have a temperature sensor and can transmit TLM frames are compatible with this platform. For example [Gimbal](https://store.gimbal.com/collections/beacons/), [Estimote](http://estimote.com/) or [kontakt.io](https://kontakt.io/). For more manufacturers see [this overview](https://developers.google.com/beacons/eddystone#beacon_manufacturers) by Google.

## Requirements

As this platform uses `bluez` to scan for Bluetooth LE devices **a Linux OS with bluez installed** is required. In addition to that, the `libbluetooth` headers need to be installed:

```bash
$ sudo apt-get install libbluetooth-dev 
```

Scanning for Bluetooth LE devices also requires special permissions. To grant these to the python executable execute the following:

```bash
$ sudo apt-get install libcap2-bin
$ sudo setcap 'cap_net_raw,cap_net_admin+eip' $(readlink -f $(which python3))
```

To use your Eddystone beacon in your installation, add the following to your `configuration.yaml` file:

```yaml
# Example configuration.yaml entry
sensor:
  - platform: eddystone_temperature
    bt_device_id: 0  # optional
    beacons:
      living_room:
        namespace: "112233445566778899AA"
        instance: "000000000001"
      kitchen:
        namespace: "112233445566778899AA"
        instance: "000000000002"
```
Configuration variables:
- **bt_device_id** (*Optional*): The id of the Bluetooth device that should be used for scanning (hci*X*). You can find the correct one using `hcitool dev` (default: 0). 
- **beacons** array (*Required*): The beacons that should be monitored.
  - **[entry]** (*Required*): Name of the beacon.
    - **namespace** (*Required*): Namespace ID of the beacon in hexadecimal notation. Must be exactly 20 characters (10 bytes) long.
    - **instance** (*Required*): Instance ID of the beacon in hexadecimal notation. Must be exactly 12 characters (6 bytes) long.
    - **name** (*Optional*): Friendly name of the beacon.
