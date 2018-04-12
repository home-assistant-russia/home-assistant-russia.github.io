---
layout: page
title: "Samsung SyncThru Printer"
description: "Instructions on how to integrate a Samsung printer providing SyncThru within Home Assistant."
date: 2018-02-19 23:33
sidebar: true
comments: false
sharing: true
footer: true
logo: samsung.png
ha_category: Sensor
ha_iot_class: "Local Polling"
ha_release: 0.66
---

The Samsung SyncThru Printer platform allows you to read current data from your local Samsung printer.

It usually provides information about the device's state, the left amount of ink or toner and the state of paper trays.
The platform automatically monitors every supported part.

If you wish not to include certain monitored values specify the values that you would like to see in the front-end via the `monitored_conditions` setting.

```yaml
# Example configuration.yaml entry
sensor:
  - platform: syncthru
    resource: http://my-printer.address
    name: My Awesome Printer
    monitored_conditions:
        - toner_black
        - output_tray_0
```

{% configuration %}
  resource:
    description: The address for connecting to the printer. Equal to the SyncThru Webservice address.
    required: true
    default: false
    type: url
  name:
    description: A user specified name for the printer. Defaults to "Samsung Printer" and the friendly name will be the name of the printer model.
    required: false
    default: Samsung Printer
    type: string
  monitored_conditions:
    description: Conditions to display in the frontend.
    required: false
    default: all values
    type: list
    keys:
      toner_black:
        description: Black toner fill level
      toner_cyan:
        description: Cyan toner fill level
      toner_magenta:
        description: Magenta toner fill level
      toner_yellow:
        description: Yellow toner fill level
      drum_black:
        description: Black drum state
      drum_cyan:
        description: Cyan drum state
      drum_magenta:
        description: Magenta drum state
      drum_yellow:
        description: Yellow drum state
      tray_1:
        description: First paper input tray state
      tray_2:
        description: Second paper input tray state
      tray_3:
        description: Third paper input tray state
      tray_4:
        description: Fourth paper input tray state
      tray_5:
        description: Fifth paper input tray state
      output_tray_0:
        description: First paper output tray state
      output_tray_1:
        description: Second paper output tray state
      output_tray_2:
        description: Third paper output tray state
      output_tray_3:
        description: Fourth paper output tray state
      output_tray_4:
        description: Fifth paper output tray state
      output_tray_5:
        description: Sixth paper output tray state
{% endconfiguration %}
