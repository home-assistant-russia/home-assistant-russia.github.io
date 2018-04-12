---
layout: post
title: "0.8: Honeywell Thermostats, Orvibo switches and Z-Wave switches and lights "
description: "Home Assistant 0.8 can now interact with Honeywell thermostats, Orvibo switches and has improved Z-Wave support."
date: 2015-11-16 21:27:00 0000
date_formatted: "November 16, 2015"
author: Paulus Schoutsen
author_twitter: balloob
comments: true
categories: Release-Notes
---

<img src='/images/screenshots/custom-icons.png' style='float: right;' />We have all been hard at work to get this latest release ready. One of the big highlights in this release is the introduction of an extended iconset to be used in the frontend (credits to [@happyleavesaoc] for idea and prototype). To get started with customizing, pick any icon from [MaterialDesignIcons.com], prefix the name with `mdi:` and stick it into your `customize` section in `configuration.yaml`:

```yaml
homeassistant:
  customize:
    switch.ac:
      icon: 'mdi:air-conditioner'
```

#### Breaking changes

 - Any existing zone icon will have to be replaced with one from [MaterialDesignIcons.com].
 - LimitlessLED light services require colors to be specified in RGB instead of XY.

#### Changes

<img src='/images/supported_brands/honeywell.png' style='clear: right; border:none; box-shadow: none; float: right; margin-bottom: 16px;' height='50' /><img src='/images/supported_brands/orvibo.png' style='clear: right;  border:none; box-shadow: none; float: right; margin-bottom: 16px;' height='50' /><img src='/images/supported_brands/pushetta.png' style='clear: right; border:none; box-shadow: none; float: right; margin-bottom: 16px;' height='50' />

 * Thermostat: [Honeywell](/components/thermostat.honeywell/) now supported ([@sander76])
 * Switch: [Orvibo](/components/switch.orvibo/) now supported ([@happyleavesaoc])
 * Camera: [mjpeg camera's](/components/camera.mjpeg/) now supported ([@ryanturner])
 * Notify: [Pushetta](/components/notify.pushetta/) now supported ([@fabaff])
 * Light: [MQTT](/components/light.mqtt/) now supported ([@hexxter])
 * Light: [Z-Wave](/components/zwave/) now supported ([@leoc])
 * Switch: [Z-Wave](/components/zwave/) now supported ([@leoc])
 * New component [logger](/components/logger/) allows filtering logged data ([@badele])
 * New component [updater](/components/updater/) will notify users if an update for Home Assistant is available ([@rmkraus])
 * Notify: [PushBullet](/components/notify.pushbullet/) now allows targeting contacts/channels/specific devices ([@tomduijf])
 * Light: Allow controlling color temperature ([@tomduijf])
 * Frontend: about page added ([@balloob])
 * Switch RGB as the color unit used in light component ([@balloob])
 * Re-install platform and component dependencies after a Home Assistant version upgrade ([@balloob])

[MaterialDesignIcons.com]: https://MaterialDesignIcons.com
[@sander76]: https://github.com/sander76
[@happyleavesaoc]: https://github.com/happyleavesaoc
[@ryanturner]: https://github.com/ryanturner
[@fabaff]: https://github.com/fabaff
[@hexxter]: https://github.com/hexxter
[@leoc]: https://github.com/leoc
[@badele]: https://github.com/badele
[@rmkraus]: https://github.com/rmkraus
[@tomduijf]: https://github.com/tomduijf
[@balloob]: https://github.com/balloob
