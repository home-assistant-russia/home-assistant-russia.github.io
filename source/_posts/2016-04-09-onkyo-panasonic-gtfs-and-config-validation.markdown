---
layout: post
title: "0.17: Onkyo, Panasonic, GTFS and config validation"
description: "Home Assistant 0.17 has arrived."
date: 2016-04-09 23:10:00 UTC
date_formatted: "April 9, 2016"
author: Paulus Schoutsen
author_twitter: balloob
comments: true
categories: Release-Notes
---

Another awesome release ready to hit your homes. YAML can be hard for beginners and more experienced automators. So to help catch those pesky errors that sneak into your files we've been hard at work to introduce config validation! Especially huge thanks to [@jaharkes] for his hard work on this. Config validation is still in its early stages. More common platforms and components have been added but we didn't do everything yet.

When we encounter an invalid config we will now write a warning to your logs. You can see those in the frontend by clicking on the last developer tool. We're looking into options to make it more clear - it is a work in progress.

Another big thing is the addition of GTFS support. You probably don't know it, but GTFS is the standard that public transit companies all over the world use to distribute their schedule. This means that you can now have the time of the next bus/train/etc right in your frontend.

<img src='/images/supported_brands/onkyo.png' style='clear: right; margin-left: 5px; border:none; box-shadow: none; float: right; margin-bottom: 16px;' width='150' /><img src='/images/supported_brands/loop.png' style='clear: right; margin-left: 5px; border:none; box-shadow: none; float: right; margin-bottom: 16px;' width='150' /><img src='/images/supported_brands/panasonic.png' style='clear: right; margin-left: 5px; border:none; box-shadow: none; float: right; margin-bottom: 16px;' width='150' />

 - Config validation ([@balloob], [@jaharkes])
 - Sensor: [GTFS] support (public transit open standard) ([@robbiet480])
 - Camera: [Raspberry PI] support added ([@LucaSoldi])
 - Z-Wave: improved startup reliability ([@srcLurker])
 - Media Player: [Onkyo receiver] now supported ([@danieljkemp])
 - Sensor: [Loop Energy] now supported ([@pavoni])
 - Thermostat: [Z-Wave] now supported ([@coteyr], [@turbokongen], [@luxus])
 - Sensor: [NZBGet] now supported ([@justyns])
 - Media Player: [Panasonic Viera TV] now supported ([@florianholzapfel])
 - Thermostats: Use whole degrees if user uses Fahrenheit ([@JshWright])
 - Frontend: more material love ([@balloob])

[@balloob]: https://github.com/balloob/
[@coteyr]: https://github.com/coteyr/
[@danieljkemp]: https://github.com/danieljkemp/
[@florianholzapfel]: https://github.com/florianholzapfel/
[@jaharkes]: https://github.com/jaharkes/
[@JshWright]: https://github.com/JshWright/
[@justyns]: https://github.com/justyns/
[@LucaSoldi]: https://github.com/LucaSoldi/
[@luxus]: https://github.com/luxus/
[@pavoni]: https://github.com/pavoni/
[@robbiet480]: https://github.com/robbiet480/
[@srcLurker]: https://github.com/srcLurker/
[@turbokongen]: https://github.com/turbokongen/
[GTFS]: /components/sensor.gtfs/
[Loop Energy]: /components/sensor.loop_energy/
[NZBGet]: /components/sensor.nzbget/
[Onkyo receiver]: /components/media_player.onkyo/
[Panasonic Viera TV]: /components/media_player.panasonic_viera/
[Raspberry PI]: /components/camera.rpi_camera/
[Z-Wave]: /components/thermostat.zwave/

### Breaking changes

As of now we are not aware of any breaking changes. However, it might be that Home Assistant will not start for you because of an invalid configuration. A common mistake that people are making is that they are still referring to `execute_service` in their script configs. This should be `service`.
