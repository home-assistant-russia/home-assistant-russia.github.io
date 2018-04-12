---
layout: page
title: "Dark Sky"
description: "Instructions on how to integrate Dark Sky within Home Assistant."
date: 2016-09-29 09:00
sidebar: true
comments: false
sharing: true
footer: true
featured: true
logo: dark_sky.png
ha_category: Weather
ha_release: 0.61
ha_iot_class: "Cloud Polling"
---

The `darksky` platform uses the [Dark Sky](https://darksky.net/) web service as
a source for meteorological data for your location.

You need an API key which is free but requires
[registration](https://darksky.net/dev/register). The free tier allows up to
1000 calls per day, this platform updates at most every 3 minutes, using up to
480 of those calls.

<p class='note warning'>
[Dark Sky](https://darksky.net/dev/) will charge you $0.0001 per API call if you
enter your credit card details and create more than 1000 calls per day.
</p>

To add Dark Sky to your installation, add the following to your `configuration.yaml` file:

```yaml
# Example configuration.yaml entry
weather:
  - platform: darksky
    api_key: YOUR_API_KEY
```

{% configuration %}
api_key:
  description: "Your API key for [Dark Sky](https://darksky.net/dev/)."
  required: true
  type: string
latitude:
  description: Manually specify latitude. By default the value will be taken from the Home Assistant configuration.
  required: false
  type: number
  default: Provided by Home Assistant configuration
longitude:
  description: Manually specify longitude. By default the value will be taken from the Home Assistant configuration.
  required: false
  type: number
  default: Provided by Home Assistant configuration
units:
  description: "Manually specify unit system. Valid values are: `auto`, `us`, `si`, `ca`, `uk` and `uk2`."
  required: false
  type: string
  default: "`si` if Home Assistant unit system is metric, `us` if imperial."
name:
  description: Name to use in the frontend.
  required: false
  type: string
  default: Open Sky
{% endconfiguration %}

<p class='note'>
This platform is an alternative to the [`darksky`](/components/sensor.darksky/)
sensor.
</p>

Details about the API are available in the [Dark Sky documentation](https://darksky.net/dev/docs).
