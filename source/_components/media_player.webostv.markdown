---
layout: page
title: "LG webOS Smart TV"
description: "Instructions on how to integrate a LG webOS Smart TV within Home Assistant."
date: 2016-04-18 23:24
sidebar: true
comments: false
sharing: true
footer: true
logo: webos.png
ha_category: Media Player
ha_iot_class: "Local Polling"
ha_release: 0.18
---

The `webostv` platform allows you to control a [LG](http://www.lg.com/) webOS Smart TV.

### {% linkable_title Setup %}

To begin with enable *LG Connect Apps* feature in *Network* settings of the TV [instructions](http://www.lg.com/uk/support/product-help/CT00008334-1437131798537-others).

Once basic configuration is added to your `configuration.yaml` *Configuration* card should prompt on your HA's States. Follow the instructions and accept pairing request on your TV.

Pairing information will be saved to the `filename:` provided in configuration; this process is IP sensitive, in case the IP address of your TV would change in future.


### {% linkable_title Configuration %}

To add a TV to your installation, add the following to your `configuration.yaml` file:

```yaml
# Example configuration.yaml entry
media_player:
  - platform: webostv
```

Configuration variables:

- **host** (*Optional*): The IP of the LG webOS Smart TV, e.g., `192.168.0.10`.
- **turn_on_action** (*Optional*): Defines an [action](/docs/automation/action/) to turn the TV on.
- **name** (*Optional*): The name you would like to give to the LG webOS Smart TV.
- **timeout** (*Optional*): The timeout for connections to the TV in seconds.
- **filename** (*Optional*): The filename where the pairing key with the TV should be stored. This path is relative to Home Assistant's config directory. It defaults to `webostv.conf`.
- **customize** array (*Optional*): List of options to customize.
  - ***sources** array (*Optional*): List of hardware and webOS App inputs.

If you do not specify `host:`, all LG webOS Smart TVs within your network will be auto-discovered.

A full configuration example will look like the sample below:

```yaml
# Example configuration.yaml entry
media_player:
  - platform: webostv
    host: 192.168.0.10
    name: Living Room TV  
    timeout: 5
    filename: webostv.conf
    turn_on_action:
      service: persistent_notification.create
      data:
        message: "Turn on action"
    customize:
      sources:
        - livetv
        - youtube
        - makotv
        - netflix
```
** avoid using `[ ]` in the `name:` of your device.


*Turn On Action*

Home Assistant is able to turn on a LG webOS Smart TV if you specify an action, like HDMI-CEC or WakeOnLan.

Common for webOS 3.0 and higher would be to use WakeOnLan feature. 
To use this feature your TV should be connected to your network via Ethernet rather than Wireless and you should enable *LG Connect Apps* feature in *Network* settings of the TV [instructions](http://www.lg.com/uk/support/product-help/CT00008334-1437131798537-others) (or *Mobile App* in *General* settings for older models) (*may vary by version).

```yaml
# Example configuration.yaml entry
wake_on_lan: # enables `wake_on_lan` domain

media_player:
  - platform: webostv
    host: 192.168.0.10
    #other settings
    turn_on_action:
      service: wake_on_lan.send_magic_packet
      data:
        mac: B4:E6:2A:1E:11:0F
```
Any other [actions](/docs/automation/action/) to power on the device can be configured. 


*Sources*

To obtain complete list of available sources currently configured on the TV, once the webOS TV is configured and linked, while its powered on head to the **Developer Tools** > **States**, find your `media_player.<name>` and use the sources listed in `source_list:` remembering to split them per line into your `sources:` configuration.
