---
layout: page
title: "Xiaomi Mi WiFi Repeater 2"
description: "Instructions how to integrate your Xiaomi Mi WiFi Repeater 2 within Home Assistant."
date: 2018-04-01 21:06
sidebar: true
comments: false
sharing: true
footer: true
logo: xiaomi.png
ha_category: Sensor
ha_version: 0.67
ha_iot_class: "Local Polling"
---

The `xiaomi_miio` device tracker platform is observing your Xiaomi Mi WiFi Repeater 2 and reporting all associated WiFi clients.

Please follow the instructions on [Retrieving the Access Token](/components/vacuum.xiaomi_miio/#retrieving-the-access-token) to get the API token.

To add a Xiaomi Mi Air Quality Monitor to your installation, add the following to your `configuration.yaml` file:

```yaml
device_tracker:
  - platform: xiaomi_miio
    host: 192.168.130.73
    token: YOUR_TOKEN
```

{% configuration %}
host:
  description: The IP address of your miio device.
  required: true
  type: string
token:
  description: The API token of your miio device.
  required: true
  type: string
{% endconfiguration %}
