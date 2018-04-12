---
layout: post
title: "0.7.5: Blinkstick, SNMP, Telegram"
description: "Home Assistant 0.7.5 has been released with support for RFXtrx, Blinkstick, SNMP and Telegram."
date: 2015-10-11 10:10:00 -0700
date_formatted: "October 11, 2015"
author: Paulus Schoutsen
author_twitter: balloob
comments: true
categories: Release-Notes
---

We discovered two issues annoying enough to warrant the release of 0.7.5:

- Home Assistant package did not include the CloudMQTT certificate.
- A bug in the core caused issues when some platforms are loaded twice.

This release also includes some new platforms (because they keep coming!):

<img src='/images/supported_brands/blinkstick.png' style='border:none; box-shadow: none; float: right;' height='50' /><img src='/images/supported_brands/rfxtrx.png' style='border:none; box-shadow: none; float: right; clear: right;' height='50' /><img src='/images/supported_brands/telegram.png' style='border:none; box-shadow: none; float: right; clear: right;' height='50' />

 - Light: [blinkstick platform](/components/light.blinksticklight/) added ([@alanbowman](https://github.com/alanbowman))
 - Device Tracker: [SNMP platform](/components/device_tracker.snmp/) added ([@tomduijf](https://github.com/tomduijf))
 - Light: [rfxtrx platform](/components/light.rfxtrx/) added ([@badele](https://github.com/badele))
 - Switch: [rfxtrx platform](/components/switch.rfxtrx/) added ([@badele](https://github.com/badele))
 - Notify: [telegram platform](/components/notify.telegram/) added ([@fabaff](https://github.com/fabaff))

Also, the media player was extended by [@maddox](https://github.com/maddox) to support the play media command. This has been implemented for the [iTunes platform](/components/media_player.itunes/).
