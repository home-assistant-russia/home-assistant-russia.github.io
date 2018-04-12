---
layout: post
title: "0.14: Steam, D-Link smart plugs and Neurio Energy Sensors"
description: "Home Assistant 0.14 has arrived."
date: 2016-02-27 14:15:00 -0800
date_formatted: "February 28, 2016"
author: Paulus Schoutsen
author_twitter: balloob
comments: true
categories: Release-Notes
og_image: /images/blog/2016-02-release-14/social.png
---

It's been another two weeks which means it's time for release: 0.14!

<img src='/images/supported_brands/neurio.png' style='clear: right; margin-left: 5px; border:none; box-shadow: none; float: right; margin-bottom: 16px;' width='150' /><img src='/images/supported_brands/dlink.png' style='clear: right; margin-left: 5px; border:none; box-shadow: none; float: right; margin-bottom: 16px;' width='150' /><img src='/images/supported_brands/steam.png' style='clear: right; margin-left: 5px; border:none; box-shadow: none; float: right; margin-bottom: 16px;' width='90' />

 - Notify: [Command line platform][notify.command_line] added ([@stefan-jonasson])
 - Sensor: [Verisure] mousedetectors now supported ([@turbokongen])
 - Core: Entities can now expose if they assume their state representation is correct ([@balloob])
 - Sensor: [TCP][sensor.tcp] platform added ([@flyte])
 - Binary Sensor: [TCP][binary_sensor.tcp] platform added ([@flyte])
 - Sensor: [Neurio energy sensor] now supported ([@infamy])
 - Binary Sensor: [nx584] support added ([@kk7ds])
 - Improve and clarify CI testing ([@sdague])
 - Automation: State [triggers] and [conditions] now takes optional `for` config parameter to only trigger when a state hasn't changed for a certain period of time ([@pavoni], [@stefan-jonasson])
 - Sensor: [Nest] weather data added ([@w1ll1am23])
 - Device Tracker: [Ubiquiti Unifi] now supported ([@kk7ds])
 - Binary Sensor: [MySensors] now supported ([@MartinHjelmare])
 - Binary Sensor: [Bloomsky] now supported ([@balloob])
 - Binary Sensor: [Z-Wave] now supported ([@tpatja])
 - Switch: [D-Link smart plugs] now supported ([@LinuxChristian])
 - Script: Toggle support added ([@Andythigpen])
 - Light: [Wemo] now supported ([@jaharkes])
 - Rollershutter: [Command line platform][rollershutter.command_line] added ([@t30])
 - Sensor: [Steam] now supported ([@GreenTurtwig])
 - Binary Sensor: [Wink] now supported ([@w1ll1am23])
 - Demo has been updated ([@kfgoode])
 - Frontend: new UI for camera's ([@balloob])

<p class='img'>
  <img src='/images/blog/2016-02-release-14/screenshot-webcam.png'>
  Camera feeds are now directly embedded in the frontend.
</p>

### Backwards incompatible changes
 - Component: Simple Alarm has been removed. Still available in [the cookbook].
 - Script: Turning on a [script] that is already on is now a no-op instead of skipping current delay.
 - Wemo switches now have to be set up via the main [Wemo component]
 - Command line platforms for [switch][switch.cmd], [sensor][sensor.cmd] and [binary_sensor][binary_sensor.cmd] have been renamed to `command_line`.
 - The rfxtrx sensors entity ids will incur a one time change to move to a stable format. See [the docs][sensor.rfxtrx] for more details.

[sensor.rfxtrx]: /components/sensor.rfxtrx/
[notify.command_line]: /components/notify.command_line/
[Verisure]: /components/sensor.verisure/
[binary_sensor.tcp]: /components/binary_sensor.tcp/
[sensor.tcp]: /components/sensor.tcp/
[Neurio energy sensor]: /components/sensor.neurio_energy/
[nx584]: /components/binary_sensor.nx584/
[triggers]: /getting-started/automation-trigger/#state-trigger
[conditions]: /getting-started/automation-condition/#state-condition
[Nest]: /components/sensor.nest/
[Ubiquiti Unifi]: /components/device_tracker.unifi/
[MySensors]: /components/binary_sensor.mysensors/
[Bloomsky]: /components/binary_sensor.bloomsky/
[Z-Wave]: /components/binary_sensor.zwave/
[D-Link smart plugs]: /components/switch.dlink/
[Wemo]: /components/light.wemo/
[rollershutter.command_line]: /components/rollershutter.command_line/
[Steam]: /components/sensor.steam_online/
[Wink]: /components/binary_sensor.wink/
[the cookbook]: /cookbook/python_component_simple_alarm/
[script]: /components/script/
[Wemo component]: /components/wemo/
[switch.cmd]: /components/switch.command_line/
[sensor.cmd]: /components/sensor.command_line/
[binary_sensor.cmd]: /components/binary_sensor.command_line/

[@stefan-jonasson]: https://github.com/stefan-jonasson
[@turbokongen]: https://github.com/turbokongen
[@balloob]: https://github.com/balloob
[@flyte]: https://github.com/flyte
[@infamy]: https://github.com/infamy
[@kk7ds]: https://github.com/kk7ds
[@sdague]: https://github.com/sdague
[@pavoni]: https://github.com/pavoni
[@w1ll1am23]: https://github.com/w1ll1am23
[@MartinHjelmare]: https://github.com/MartinHjelmare
[@tpatja]: https://github.com/tpatja
[@LinuxChristian]: https://github.com/LinuxChristian
[@Andythigpen]: https://github.com/Andythigpen
[@jaharkes]: https://github.com/jaharkes
[@t30]: https://github.com/t30
[@GreenTurtwig]: https://github.com/GreenTurtwig
[@kfgoode]: https://github.com/kfgoode
