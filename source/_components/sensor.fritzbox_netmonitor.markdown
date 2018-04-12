---
layout: page
title: "FRITZ!Box Net Monitor"
description: "Instructions on how to integrate an AVM FRITZ!Box monitor into Home Assistant."
date: 2017-01-17 22:00
sidebar: true
comments: false
sharing: true
footer: true
logo: avm.png
ha_category: System Monitor
ha_release: 0.36
ha_iot_class: "Local Polling"
---


The `fritzbox_netmonitor` sensor monitors the network statistics exposed by [AVM Fritz!Box](http://avm.de/produkte/fritzbox/) routers.

<p class='note warning'>
It might be necessary to install additional packages: <code>$ sudo apt-get install libxslt-dev libxml2-dev python3-lxml</code>
If you are working with the All-in-One installation, you may also need to execute also within your virtual environment the command <code> pip install lxml</code>; be patient this will take a while.</p>

To use the Fritz!Box network monitor in your installation, add the following to your `configuration.yaml` file:

```yaml
# Example configuration.yaml entry
sensor:
  - platform: fritzbox_netmonitor
```

Configuration variables:

- **host** (*Optional*): The IP address of your router, eg. 192.168.1.1. It is optional since every fritzbox is also reachable by using the IP address 169.254.1.1.

The following statistics will be exposed as attributes.

|Attribute              |Description                                                  |
|:----------------------|:------------------------------------------------------------|
|is_linked              |True if the FritzBox is physically linked to the provider    |
|is_connected           |True if the FritzBox has established an internet-connection  |
|wan_access_type        |Connection-type, can be `DSL` or `Cable`                     |
|external_ip            |External ip address                                          |
|uptime                 |Uptime in seconds                                            |
|bytes_sent             |Bytes sent                                                   |
|bytes_received         |Bytes received                                               |
|transmission_rate_up   |Current upstream speed in bytes/s                            |
|transmission_rate_down |Current downstream speed in bytes/s                          |
|max_byte_rate_up       |Maximum upstream-rate in bytes/s                             |
|max_byte_rate_down     |Maximum downstream-rate in bytes/s                           |

The sensor's state corresponds to the `is_linked` attribute and is either `online`, `offline`, or `unavailable` (in case connection to the router is lost).
