---
layout: page
title: "Rain Bird"
description: "Instructions on how to integrate your Rain Bird LNK WiFi Module within Home Assistant."
date: 2017-12-07 12:00
sidebar: true
comments: false
sharing: true
footer: true
logo: rainbird.png
ha_category: Hub
ha_release: 0.61
ha_iot_class: "Local Polling"
---

This `rainbird` component allows interacting with [LNK WiFi](http://www.rainbird.com/landscape/products/controllers/LNK-WiFi.htm) module of the Rain Bird Irrigation system in Home Assistant.

To enable it, add the following to your `configuration.yaml` file:

```yaml
# Example configuration.yaml entry
rainbird:
  host: IP_ADDRESS_OF_MODULE
  password: YOUR_PASSWORD
```

{% configuration %}
host:
  description: v
  required: true
  type: string
password:
  description: The password for accessing the module.
  required: true
  type: string
{% endconfiguration %}

Finish its configuration by visiting the [Rain Bird sensor](/components/sensor.rainbird/) and [Rain Bird switch](/components/switch.rainbird/) documentation.

Please note that due to the implementation of the API within the LNK Module, there is a concurrency issue. For example, the Rain Bird app will give connection issues (like already a connection active).
