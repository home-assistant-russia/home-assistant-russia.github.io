---
layout: post
title: "Home Assistant 0.45: Automation editor, Z-Wave panel, OCR"
description: "AXIS and Keene support, PiFace, Raspihats, and Datadog integration"
date: 2017-05-20 13:00:00 +0000
date_formatted: "May 20, 2017"
author: Paulus Schoutsen & Fabian Affolter
author_twitter: balloob
comments: true
categories: Release-Notes
og_image: /images/blog/2017-05-0.45/components.png
---

<a href='/components/#version/0.45'><img src='/images/blog/2017-05-0.45/components.png' style='border: 0;box-shadow: none;'></a>

Welcome to another great release of Home Assistant! While some of contributors and users are gathering at PyCon US 2017, we still managed to get a great release together!

First thing for this release is a feature that has been requested a lot: an automation editor! It's still experimental - and many things are still in progress - but it works! You can create new automations and edit existing ones. If you start a new config, you're all good to go. Otherwise check [these instructions](/docs/automation/editor/) to get your automations ready for editing in the UI.

<p class='img'>
  <img src='{{site_root}}/images/blog/2017-05-0.45/trigger.png' />
</p>

Check this [video](https://youtu.be/0j_hWdCTip4) by [Ben](https://twitter.com/BRUHautomation) from [BRUHautomation](http://www.bruhautomation.com/) to see the new release in action.

<div class='videoWrapper'>
<iframe width="560" height="315" src="https://www.youtube.com/embed/0j_hWdCTip4" frameborder="0" allowfullscreen></iframe>
</div>

As the editor is experimental, there are some limitations. These include that Chrome/Chromium is the only supported browser, we don't support all triggers and actions and there is no support for conditions yet. But the foundation is there and so if you want to contribute to this, come help!

On the Z-Wave front a lot has happened. The biggest one is that we have a major extension of the Z-Wave panel thanks to [@turbokongen]! You will now be able to change config parameters and manage your devices.

<p class='img'>
  <img src='{{site_root}}/images/blog/2017-05-0.45/zwave.png' />
</p>
Thanks to the work by the Python Open Z-Wave team we are now able to install it on demand from PyPi! There is no longer a need to pre-compile it yourself. This should give us the guarantee that we work with the Python Open Z-Wave version that the code expects.

<p class='note warning'>
If you have a security key set in your Open Z-Wave `options.xml`, copy `options.xml` to your Home Assistant configuration directory. This is the only place where options will get persisted.
</p>

Next to that [@armills] has lead the charge and managed to get full test coverage for Z-Wave! Thanks for all the hard work!

This release also contains two integrations which could help you to make non-smart devices a little smarter. The [`file` sensor][sensor.file docs] and the [`seven_segments` OCR image processing platform][image_processing.seven_segments docs]. The first simply reads a plain-text file which was created by a logger or alike. The latter one extracts the value from a captured image that shows a seven-segments display.

<p class='img'>
  <img src='{{site_root}}/images/blog/2017-05-0.45/power-meter.png' />
</p>

And last, but not least, our Docker image is now based off Python 3.6. This version is faster and uses less memory than Python 3.5. Win!

If you are using our [experimental Hass.io image][hass.io], we made a breaking change in how the panel is served. If you have an existing installation, make sure you update your supervisor to the latest version before updating Home Assistant. If you are going to flash a new Hass.io image, make sure to only flash the new 0.8 image as linked on [the installation page][hass.io-install].

[hass.io]: https://community.home-assistant.io/t/introducing-hass-io/17296
[hass.io-install]: /hassio/installation/

## {% linkable_title New integrations %}

- Add new raspihats component ([@florincosta] - [#7392]) ([raspihats docs]) (new-platform)
- Add datadog component ([@nunofgs] - [#7158]) ([datadog docs]) (new-platform)
- Add support for automation config panel ([@balloob] - [#7509]) ([config.automation docs]) (new-platform)
- Z-Wave panel API ([@turbokongen] - [#7456]) ([zwave docs]) ([zwave.api docs]) (new-platform)
- myStrom Buttons support ([@fabaff] - [#7099]) ([binary_sensor.mystrom docs]) (new-platform)
- Support for the PiFace Digital I/O module ([@basschipper] - [#7494]) ([rpi_pfio docs]) ([binary_sensor.rpi_pfio docs]) ([switch.rpi_pfio docs]) (new-platform)
- Add raspihats binary sensor ([@florincosta] - [#7508]) ([binary_sensor.raspihats docs]) (new-platform)
- Support lutron serena shades ([@gurumitts] - [#7565]) ([lutron_caseta docs]) ([cover.lutron_caseta docs]) (new-platform)
- Add Kira component to sensor and remote platforms ([@stu-gott] - [#7479]) ([kira docs]) ([remote.kira docs]) ([sensor.kira docs]) (new-platform)
- File sensor ([@fabaff] - [#7569]) ([sensor.file docs]) (new-platform)
- Seven segments OCR image processing ([@fabaff] - [#7632]) ([image_processing.seven_segments docs]) (new-platform)
- Axis component ([@Kane610] - [#7381]) ([axis docs]) (new-platform)

## {% linkable_title Release 0.45.1 - May 22 %}

- Fix telegram chats ([@azogue] - [#7689]) ([notify.telegram docs]) ([telegram_bot.__init__ docs])
- Fix playback control of web streams ([@cgtobi] - [#7683]) ([media_player.volumio docs])
- device_tracker.ubus: Handle empty results ([@tobygray] - [#7673]) ([device_tracker.ubus docs])
- Allow fetching hass.io panel without auth ([@balloob] - [#7714]) ([hassio docs])

## {% linkable_title If you need help... %}
...don't hesitate to use our very active [forums][forum] or join us for a little [chat][discord]. The release notes have comments enabled but it's preferred if you use the former communication channels. Thanks.

## {% linkable_title Reporting Issues %}
Experiencing issues introduced by this release? Please report them in our [issue tracker][issue]. Make sure to fill in all fields of the issue template.

## {% linkable_title Breaking changes %}

- PyPI Openzwave ([@JshWright] - [#7415]) ([zwave docs]) (breaking change)
- Remove listening to `homeassistant_start` with event automation ([@balloob] - [#7474]) ([automation.event docs]) (breaking change)

<!--more-->
## {% linkable_title All changes %}

- Add hass to rfxtrx object ([@danielhiversen] - [#6844])
- Add new raspihats component ([@florincosta] - [#7392]) ([raspihats docs]) (new-platform)
- sensor.envirophat: add missing requirement ([@imrehg] - [#7451]) ([sensor.envirophat docs])
- PyPI Openzwave ([@JshWright] - [#7415]) ([zwave docs]) (breaking change)
- Add datadog component ([@nunofgs] - [#7158])
- Add tests for deprecation helpers ([@armills] - [#7452])
- Forecasts for weather underground ([@pezinek] - [#7062]) ([sensor.wunderground docs])
- sensor.envirophat: add missing requirement ([@imrehg] - [#7451]) ([sensor.envirophat docs])
- Switch russound, pymysensors, and pocketcasts to pypi ([@andrey-git] - [#7449])
- Upgrade pymysensors to 0.10.0 ([@MartinHjelmare] - [#7469])
- Upgrade Dockerfile to Python 3.6 ([@balloob] - [#7471])
- Test only dependencies ([@balloob] - [#7472])
- Update to pyunifi 2.12 ([@finish06] - [#7468]) ([device_tracker.unifi docs])
- Remove listening to homeassistant_start with event automation ([@balloob] - [#7474]) ([automation.event docs]) (breaking change)
- Fix plant MIN_TEMPERATURE, MAX_TEMPERATURE validation ([@frog32] - [#7476]) ([plant docs])
- Forecasts for weather underground ([@pezinek] - [#7062]) ([sensor.wunderground docs])
- Upgrade pymysensors to 0.10.0 ([@MartinHjelmare] - [#7469])
- Fix plant MIN_TEMPERATURE, MAX_TEMPERATURE validation ([@frog32] - [#7476]) ([plant docs])
- Update to pyunifi 2.12 ([@finish06] - [#7468]) ([device_tracker.unifi docs])
- Uses pypi for deps ([@gurumitts] - [#7485]) ([lutron_caseta docs])
- 0.44.2 ([@balloob] - [#7488])
- LIFX: avoid out-of-bounds hue aborting the colorloop effect ([@amelchio] - [#7495])
- Upgrade async_timeout to 1.2.1 ([@fabaff] - [#7490])
- Prevent printing of packets. ([@aequitas] - [#7492]) ([rflink docs])
- Upgrade beautifulsoup4 to 4.6.0 ([@fabaff] - [#7491]) ([device_tracker.linksys_ap docs]) ([sensor.scrape docs])
- Switch onkyo to pypi ([@andrey-git] - [#7497]) ([media_player.onkyo docs])
- Fixed potential AttributeError when checking for deleted sources ([@scarface-4711] - [#7502]) ([media_player.denonavr docs])
- Refactor sun component for correctness ([@armills] - [#7295])
- new source only forces "play" if the current state is "playing" ([@abmantis] - [#7506]) ([media_player.spotify docs])
- Correct retrieval of spotify shuffle state ([@andersonshatch] - [#7505]) ([media_player.spotify docs])
- Fix sonos sleep timer ([@frog32] - [#7503]) ([media_player.sonos docs])
- Add support for automation config panel ([@balloob] - [#7509]) ([automation.__init__ docs]) ([config.automation docs]) ([config.__init__ docs]) (new-platform)
- Zwave panel api ([@turbokongen] - [#7456]) ([zwave docs]) ([zwave.api docs]) (new-platform)
- Update docker dev environment to python3.6 ([@frog32] - [#7520])
- Switch basicmodem and python-roku to pypi ([@andrey-git] - [#7514]) ([media_player.roku docs]) ([sensor.modem_callerid docs])
- sensor.envirophat: do not set up platform if hardware is not attached ([@imrehg] - [#7438]) ([sensor.envirophat docs])
- Telegram Bot enhancements with callback queries and new notification services ([@azogue] - [#7454]) ([telegram_bot docs]) ([notify.telegram docs]) ([telegram_bot.polling docs]) ([telegram_bot.services.yaml docs]) ([telegram_bot.webhooks docs])
- Add password parameter to uvc component ([@nunofgs] - [#7499]) ([camera.uvc docs])
- Don't interact with hass directly ([@fabaff] - [#7099]) ([binary_sensor.mystrom docs]) (new-platform)
- Support for the PiFace Digital I/O module ([@basschipper] - [#7494]) ([rpi_pfio docs]) ([binary_sensor.rpi_pfio docs]) ([switch.rpi_pfio docs]) (new-platform)
- Upgrade limitlessled to 1.0.7 ([@corneyl] - [#7525]) ([light.limitlessled docs])
- Update docstrings and log messages ([@fabaff] - [#7526]) ([light.blinksticklight docs]) ([light.enocean docs]) ([light.flux_led docs]) ([light.insteon_local docs]) ([light.insteon_plm docs]) ([light.isy994 docs]) ([light.limitlessled docs]) ([light.mystrom docs])
- Try to request current_location Automatic scope ([@armills] - [#7447]) ([device_tracker.automatic docs])
- Add myStrom binary sensor ([@fabaff] - [#7530])
- Add not-context-manager ([@fabaff] - [#7523])
- Threadsafe configurator ([@Kane610] - [#7536]) ([configurator docs])
- Fix for #7459 ([@jumpkick] - [#7544]) ([alexa docs])
- Upgrade sendgrid to 4.1.0 ([@fabaff] - [#7538]) ([notify.sendgrid docs])
- Automatic version bump ([@armills] - [#7555]) ([device_tracker.automatic docs])
- Upgrade dweepy to 0.3.0 ([@fabaff] - [#7550]) ([dweet docs]) ([sensor.dweet docs])
- Add SSL support to NZBGet sensor ([@tboyce021] - [#7553]) ([sensor.nzbget docs])
- Do not install all dependencies in dev mode ([@balloob] - [#7548])
- Hide proximity updates in logbook ([@armills] - [#7549]) ([logbook docs])
- Only install tox in dev mode ([@balloob] - [#7557])
- Support adding different server locations for Microsoft face component ([@tsvi] - [#7532]) ([microsoft_face docs])
- Treat swing and fan level as optional in Sensibo Climate. ([@andrey-git] - [#7560]) ([climate.sensibo docs])
- LIFX: add lifx_set_state service call ([@amelchio] - [#7552]) ([light.lifx docs])
- Add raspihats binary sensor ([@florincosta] - [#7508]) ([binary_sensor.raspihats docs]) (new-platform)
- update pywebpush to 1.0.0 ([@perosb] - [#7561]) ([notify.html5 docs])
- Initialize sun with correct values. ([@aequitas] - [#7559]) ([sun docs])
- Comment RasPi specific requirements ([@Juggels] - [#7562]) ([sensor.envirophat docs])
- Update netdisco ([@balloob] - [#7563])
- Support lutron serena shades ([@gurumitts] - [#7565]) ([lutron_caseta docs]) ([cover.lutron_caseta docs]) (new-platform)
- Tests for zwave discovery logic ([@armills] - [#7566])
- Tests for zwave setup features ([@armills] - [#7570])
- Blink version bump ([@fronzbot] - [#7571]) ([blink docs]) ([sensor.blink docs])
- Fix systematic warning in influxdb sensor ([@bestlibre] - [#7541]) ([sensor.influxdb docs])
- Fix Kodi specific services registry and add descriptions ([@azogue] - [#7551]) ([media_player.kodi docs])
- Add Kira component to sensor and remote platforms ([@stu-gott] - [#7479]) ([kira docs]) ([remote.kira docs]) ([sensor.kira docs]) (new-platform)
- Add tests for zwave network events ([@armills] - [#7573])
- Additional Wink lock features ([@w1ll1am23] - [#7445])
- Websocket_api: avoid parallel drain ([@balloob] - [#7576]) ([websocket_api docs])
- Remove more test requirements ([@balloob] - [#7574])
- camera.zoneminder: Handle old versions of zoneminder ([@mnoorenberghe] - [#7589]) ([camera.zoneminder docs])
- Pass additional arguments to tox in test_docker ([@frog32] - [#7591])
- Fix websocket api reaching queue ([@balloob] - [#7590]) ([websocket_api docs])
- SMTP notify enhancements: full HTML emails and custom `product_name` in email headers ([@azogue] - [#7533]) ([notify.smtp docs])
- Automation State Change For timer attribute fix ([@armills] - [#7584]) ([automation.state docs])
- Add posibility to specify snmp protocol version ([@jhemzal] - [#7564]) ([sensor.snmp docs])
- Add sonos alarm clock update service ([@frog32] - [#7521]) ([media_player.sonos docs])
- Fix handling of single user ([@mezz64] - [#7587]) ([eight_sleep docs])
- File sensor ([@fabaff] - [#7569]) ([sensor.file docs]) (new-platform)
- Make miflora monitored_conditions parameter optional ([@frog32] - [#7598]) ([sensor.miflora docs])
- Force automation ids to always be a string ([@balloob] - [#7612]) ([automation.__init__ docs])
- Update Docker base image to python 3.6 ([@pschmitt] - [#7613])
- Add Content-type: image/jpeg for camera proxy ([@olekenneth] - [#7581]) ([camera.__init__ docs])
- Fix typo and update style to match the other platforms ([@fabaff] - [#7621]) ([image_processing.opencv docs])
- Bump pyvera - fixes issue with % in brightness levels. ([@pavoni] - [#7622]) ([vera docs])
- Add kelvin/brightness_pct alternatives to light.turn_on ([@amelchio] - [#7596]) ([light.lifx docs]) ([light.__init__ docs])
- Add support for disabling tradfri groups ([@cnrd] - [#7593]) ([tradfri docs]) ([light.tradfri docs])
- Update docstrings and comments ([@fabaff] - [#7626]) ([image_processing.openalpr_cloud docs]) ([image_processing.openalpr_local docs])
- Upgrade Sphinx to 1.6.1 ([@fabaff] - [#7624])
- Update docstrings ([@fabaff] - [#7630]) ([image_processing.demo docs]) ([image_processing.dlib_face_detect docs]) ([image_processing.dlib_face_identify docs]) ([image_processing.microsoft_face_detect docs]) ([image_processing.microsoft_face_identify docs]) ([image_processing.opencv docs])
- Kodi specific service to call Kodi API methods ([@azogue] - [#7603]) ([media_player.kodi docs])
- Updated limitlessled requirement to v1.0.8 ([@corneyl] - [#7629])
- Osram lightify Removed wrong assignment ([@commento] - [#7615]) ([light.osramlightify docs])
- Updated dependency ([@danielperna84] - [#7638]) ([homematic docs])
- Seven segments OCR image processing ([@fabaff] - [#7632]) ([image_processing.seven_segments docs]) ([image_processing.__init__ docs]) (new-platform)
- Abort tests when instances leaked ([@balloob] - [#7623])
- Coerce color_temp to int even when passed in as kelvin ([@amelchio] - [#7640]) ([light.__init__ docs])
- Fix automation failing to setup if no automations specified ([@balloob] - [#7647]) ([automation.__init__ docs])

[#6844]: https://github.com/home-assistant/home-assistant/pull/6844
[#7062]: https://github.com/home-assistant/home-assistant/pull/7062
[#7099]: https://github.com/home-assistant/home-assistant/pull/7099
[#7158]: https://github.com/home-assistant/home-assistant/pull/7158
[#7295]: https://github.com/home-assistant/home-assistant/pull/7295
[#7381]: https://github.com/home-assistant/home-assistant/pull/7381
[#7392]: https://github.com/home-assistant/home-assistant/pull/7392
[#7415]: https://github.com/home-assistant/home-assistant/pull/7415
[#7438]: https://github.com/home-assistant/home-assistant/pull/7438
[#7445]: https://github.com/home-assistant/home-assistant/pull/7445
[#7447]: https://github.com/home-assistant/home-assistant/pull/7447
[#7449]: https://github.com/home-assistant/home-assistant/pull/7449
[#7451]: https://github.com/home-assistant/home-assistant/pull/7451
[#7452]: https://github.com/home-assistant/home-assistant/pull/7452
[#7454]: https://github.com/home-assistant/home-assistant/pull/7454
[#7456]: https://github.com/home-assistant/home-assistant/pull/7456
[#7468]: https://github.com/home-assistant/home-assistant/pull/7468
[#7469]: https://github.com/home-assistant/home-assistant/pull/7469
[#7471]: https://github.com/home-assistant/home-assistant/pull/7471
[#7472]: https://github.com/home-assistant/home-assistant/pull/7472
[#7474]: https://github.com/home-assistant/home-assistant/pull/7474
[#7476]: https://github.com/home-assistant/home-assistant/pull/7476
[#7479]: https://github.com/home-assistant/home-assistant/pull/7479
[#7485]: https://github.com/home-assistant/home-assistant/pull/7485
[#7488]: https://github.com/home-assistant/home-assistant/pull/7488
[#7490]: https://github.com/home-assistant/home-assistant/pull/7490
[#7491]: https://github.com/home-assistant/home-assistant/pull/7491
[#7492]: https://github.com/home-assistant/home-assistant/pull/7492
[#7494]: https://github.com/home-assistant/home-assistant/pull/7494
[#7495]: https://github.com/home-assistant/home-assistant/pull/7495
[#7497]: https://github.com/home-assistant/home-assistant/pull/7497
[#7499]: https://github.com/home-assistant/home-assistant/pull/7499
[#7502]: https://github.com/home-assistant/home-assistant/pull/7502
[#7503]: https://github.com/home-assistant/home-assistant/pull/7503
[#7505]: https://github.com/home-assistant/home-assistant/pull/7505
[#7506]: https://github.com/home-assistant/home-assistant/pull/7506
[#7508]: https://github.com/home-assistant/home-assistant/pull/7508
[#7509]: https://github.com/home-assistant/home-assistant/pull/7509
[#7514]: https://github.com/home-assistant/home-assistant/pull/7514
[#7520]: https://github.com/home-assistant/home-assistant/pull/7520
[#7521]: https://github.com/home-assistant/home-assistant/pull/7521
[#7523]: https://github.com/home-assistant/home-assistant/pull/7523
[#7525]: https://github.com/home-assistant/home-assistant/pull/7525
[#7526]: https://github.com/home-assistant/home-assistant/pull/7526
[#7530]: https://github.com/home-assistant/home-assistant/pull/7530
[#7532]: https://github.com/home-assistant/home-assistant/pull/7532
[#7533]: https://github.com/home-assistant/home-assistant/pull/7533
[#7536]: https://github.com/home-assistant/home-assistant/pull/7536
[#7538]: https://github.com/home-assistant/home-assistant/pull/7538
[#7541]: https://github.com/home-assistant/home-assistant/pull/7541
[#7544]: https://github.com/home-assistant/home-assistant/pull/7544
[#7548]: https://github.com/home-assistant/home-assistant/pull/7548
[#7549]: https://github.com/home-assistant/home-assistant/pull/7549
[#7550]: https://github.com/home-assistant/home-assistant/pull/7550
[#7551]: https://github.com/home-assistant/home-assistant/pull/7551
[#7552]: https://github.com/home-assistant/home-assistant/pull/7552
[#7553]: https://github.com/home-assistant/home-assistant/pull/7553
[#7555]: https://github.com/home-assistant/home-assistant/pull/7555
[#7557]: https://github.com/home-assistant/home-assistant/pull/7557
[#7559]: https://github.com/home-assistant/home-assistant/pull/7559
[#7560]: https://github.com/home-assistant/home-assistant/pull/7560
[#7561]: https://github.com/home-assistant/home-assistant/pull/7561
[#7562]: https://github.com/home-assistant/home-assistant/pull/7562
[#7563]: https://github.com/home-assistant/home-assistant/pull/7563
[#7564]: https://github.com/home-assistant/home-assistant/pull/7564
[#7565]: https://github.com/home-assistant/home-assistant/pull/7565
[#7566]: https://github.com/home-assistant/home-assistant/pull/7566
[#7569]: https://github.com/home-assistant/home-assistant/pull/7569
[#7570]: https://github.com/home-assistant/home-assistant/pull/7570
[#7571]: https://github.com/home-assistant/home-assistant/pull/7571
[#7573]: https://github.com/home-assistant/home-assistant/pull/7573
[#7574]: https://github.com/home-assistant/home-assistant/pull/7574
[#7576]: https://github.com/home-assistant/home-assistant/pull/7576
[#7581]: https://github.com/home-assistant/home-assistant/pull/7581
[#7584]: https://github.com/home-assistant/home-assistant/pull/7584
[#7587]: https://github.com/home-assistant/home-assistant/pull/7587
[#7589]: https://github.com/home-assistant/home-assistant/pull/7589
[#7590]: https://github.com/home-assistant/home-assistant/pull/7590
[#7591]: https://github.com/home-assistant/home-assistant/pull/7591
[#7593]: https://github.com/home-assistant/home-assistant/pull/7593
[#7596]: https://github.com/home-assistant/home-assistant/pull/7596
[#7598]: https://github.com/home-assistant/home-assistant/pull/7598
[#7603]: https://github.com/home-assistant/home-assistant/pull/7603
[#7612]: https://github.com/home-assistant/home-assistant/pull/7612
[#7613]: https://github.com/home-assistant/home-assistant/pull/7613
[#7615]: https://github.com/home-assistant/home-assistant/pull/7615
[#7621]: https://github.com/home-assistant/home-assistant/pull/7621
[#7622]: https://github.com/home-assistant/home-assistant/pull/7622
[#7623]: https://github.com/home-assistant/home-assistant/pull/7623
[#7624]: https://github.com/home-assistant/home-assistant/pull/7624
[#7626]: https://github.com/home-assistant/home-assistant/pull/7626
[#7629]: https://github.com/home-assistant/home-assistant/pull/7629
[#7630]: https://github.com/home-assistant/home-assistant/pull/7630
[#7632]: https://github.com/home-assistant/home-assistant/pull/7632
[#7638]: https://github.com/home-assistant/home-assistant/pull/7638
[#7640]: https://github.com/home-assistant/home-assistant/pull/7640
[#7647]: https://github.com/home-assistant/home-assistant/pull/7647
[@JshWright]: https://github.com/JshWright
[@Juggels]: https://github.com/Juggels
[@Kane610]: https://github.com/Kane610
[@MartinHjelmare]: https://github.com/MartinHjelmare
[@abmantis]: https://github.com/abmantis
[@aequitas]: https://github.com/aequitas
[@amelchio]: https://github.com/amelchio
[@andersonshatch]: https://github.com/andersonshatch
[@andrey-git]: https://github.com/andrey-git
[@armills]: https://github.com/armills
[@azogue]: https://github.com/azogue
[@balloob]: https://github.com/balloob
[@basschipper]: https://github.com/basschipper
[@bestlibre]: https://github.com/bestlibre
[@cnrd]: https://github.com/cnrd
[@commento]: https://github.com/commento
[@corneyl]: https://github.com/corneyl
[@cribbstechnologies]: https://github.com/cribbstechnologies
[@danielhiversen]: https://github.com/danielhiversen
[@danielperna84]: https://github.com/danielperna84
[@fabaff]: https://github.com/fabaff
[@finish06]: https://github.com/finish06
[@florincosta]: https://github.com/florincosta
[@frog32]: https://github.com/frog32
[@fronzbot]: https://github.com/fronzbot
[@gurumitts]: https://github.com/gurumitts
[@imrehg]: https://github.com/imrehg
[@jhemzal]: https://github.com/jhemzal
[@jminardi]: https://github.com/jminardi
[@jumpkick]: https://github.com/jumpkick
[@mezz64]: https://github.com/mezz64
[@mnoorenberghe]: https://github.com/mnoorenberghe
[@nunofgs]: https://github.com/nunofgs
[@olekenneth]: https://github.com/olekenneth
[@pavoni]: https://github.com/pavoni
[@perosb]: https://github.com/perosb
[@pezinek]: https://github.com/pezinek
[@pschmitt]: https://github.com/pschmitt
[@robbiet480]: https://github.com/robbiet480
[@scarface-4711]: https://github.com/scarface-4711
[@stu-gott]: https://github.com/stu-gott
[@tboyce021]: https://github.com/tboyce021
[@tsvi]: https://github.com/tsvi
[@turbokongen]: https://github.com/turbokongen
[@w1ll1am23]: https://github.com/w1ll1am23
[alexa docs]: /components/alexa/
[axis docs]: /components/axis/
[config.automation docs]: /docs/automation/editor/
[automation.event docs]: /docs/configuration/events/
[automation.state docs]: /docs/configuration/state_object/
[binary_sensor.mystrom docs]: /components/binary_sensor.mystrom/
[binary_sensor.raspihats docs]: /components/binary_sensor.raspihats/
[binary_sensor.rpi_pfio docs]: /components/binary_sensor.rpi_pfio/
[blink docs]: /components/blink/
[camera.__init__ docs]: /components/camera.__init__/
[camera.uvc docs]: /components/camera.uvc/
[camera.zoneminder docs]: /components/camera.zoneminder/
[climate.sensibo docs]: /components/climate.sensibo/
[config.__init__ docs]: /components/config.__init__/
[configurator docs]: /components/configurator/
[cover.lutron_caseta docs]: /components/cover.lutron_caseta/
[datadog docs]: /components/datadog/
[device_tracker.automatic docs]: /components/device_tracker.automatic/
[device_tracker.linksys_ap docs]: /components/device_tracker.linksys_ap/
[device_tracker.unifi docs]: /components/device_tracker.unifi/
[dweet docs]: /components/dweet/
[eight_sleep docs]: /components/eight_sleep/
[homematic docs]: /components/homematic/
[image_processing.__init__ docs]: /components/image_processing.__init__/
[image_processing.demo docs]: /components/image_processing.demo/
[image_processing.dlib_face_detect docs]: /components/image_processing.dlib_face_detect/
[image_processing.dlib_face_identify docs]: /components/image_processing.dlib_face_identify/
[image_processing.microsoft_face_detect docs]: /components/image_processing.microsoft_face_detect/
[image_processing.microsoft_face_identify docs]: /components/image_processing.microsoft_face_identify/
[image_processing.openalpr_cloud docs]: /components/image_processing.openalpr_cloud/
[image_processing.openalpr_local docs]: /components/image_processing.openalpr_local/
[image_processing.opencv docs]: /components/image_processing.opencv/
[image_processing.seven_segments docs]: /components/image_processing.seven_segments/
[kira docs]: /components/kira/
[light.__init__ docs]: /components/light.__init__/
[light.blinksticklight docs]: /components/light.blinksticklight/
[light.enocean docs]: /components/light.enocean/
[light.flux_led docs]: /components/light.flux_led/
[light.insteon_local docs]: /components/light.insteon_local/
[light.insteon_plm docs]: /components/light.insteon_plm/
[light.isy994 docs]: /components/light.isy994/
[light.lifx docs]: /components/light.lifx/
[light.limitlessled docs]: /components/light.limitlessled/
[light.mystrom docs]: /components/light.mystrom/
[light.osramlightify docs]: /components/light.osramlightify/
[light.tradfri docs]: /components/light.tradfri/
[logbook docs]: /components/logbook/
[lutron_caseta docs]: /components/lutron_caseta/
[media_player.denonavr docs]: /components/media_player.denonavr/
[media_player.kodi docs]: /components/media_player.kodi/
[media_player.onkyo docs]: /components/media_player.onkyo/
[media_player.roku docs]: /components/media_player.roku/
[media_player.sonos docs]: /components/media_player.sonos/
[media_player.spotify docs]: /components/media_player.spotify/
[microsoft_face docs]: /components/microsoft_face/
[notify.html5 docs]: /components/notify.html5/
[notify.sendgrid docs]: /components/notify.sendgrid/
[notify.smtp docs]: /components/notify.smtp/
[notify.telegram docs]: /components/notify.telegram/
[plant docs]: /components/plant/
[raspihats docs]: /components/raspihats/
[remote.kira docs]: /components/remote.kira/
[rflink docs]: /components/rflink/
[rpi_pfio docs]: /components/rpi_pfio/
[sensor.blink docs]: /components/sensor.blink/
[sensor.dweet docs]: /components/sensor.dweet/
[sensor.envirophat docs]: /components/sensor.envirophat/
[sensor.file docs]: /components/sensor.file/
[sensor.influxdb docs]: /components/sensor.influxdb/
[sensor.kira docs]: /components/sensor.kira/
[sensor.miflora docs]: /components/sensor.miflora/
[sensor.modem_callerid docs]: /components/sensor.modem_callerid/
[sensor.nzbget docs]: /components/sensor.nzbget/
[sensor.scrape docs]: /components/sensor.scrape/
[sensor.snmp docs]: /components/sensor.snmp/
[sensor.wunderground docs]: /components/sensor.wunderground/
[sun docs]: /components/sun/
[switch.rpi_pfio docs]: /components/switch.rpi_pfio/
[telegram_bot docs]: /components/telegram_bot/
[telegram_bot.polling docs]: /components/telegram_bot.polling/
[telegram_bot.services.yaml docs]: /components/telegram_bot.services.yaml/
[telegram_bot.webhooks docs]: /components/telegram_bot.webhooks/
[tradfri docs]: /components/tradfri/
[vera docs]: /components/vera/
[websocket_api docs]: /components/websocket_api/
[zwave docs]: /components/zwave/
[zwave.api docs]: /components/zwave.api/
[forum]: https://community.home-assistant.io/
[issue]: https://github.com/home-assistant/home-assistant/issues
[#7673]: https://github.com/home-assistant/home-assistant/pull/7673
[#7683]: https://github.com/home-assistant/home-assistant/pull/7683
[#7689]: https://github.com/home-assistant/home-assistant/pull/7689
[#7714]: https://github.com/home-assistant/home-assistant/pull/7714
[@cgtobi]: https://github.com/cgtobi
[@tobygray]: https://github.com/tobygray
[device_tracker.ubus docs]: /components/device_tracker.ubus/
[hassio docs]: /components/hassio/
[media_player.volumio docs]: /components/media_player.volumio/
[telegram_bot.__init__ docs]: /components/telegram_bot.__init__/
[discord]: https://discord.gg/c5DvZ4e
