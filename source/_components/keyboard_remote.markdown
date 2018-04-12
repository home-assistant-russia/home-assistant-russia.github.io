---
layout: page
title: "Keyboard Remote"
description: "Instructions on how to use a keyboard to remote control Home Assistant."
date: 2016-09-28 14:39
sidebar: true
comments: false
sharing: true
footer: true
logo: keyboard.png
ha_category: Other
ha_release: 0.29
ha_iot_class: "Local Push"
---

Receive signals from a keyboard and use it as a remote control.

This component allows you to use a keyboard as remote control. It will fire `keyboard_remote_command_received` events which can then be used in automation rules. 

The `evdev` package is used to interface with the keyboard and thus this is Linux only. It also means you can't use your normal keyboard for this because `evdev` will block it.


```yaml
# Example configuration.yaml entry
keyboard_remote:
  type: 'key_up'
```

Configuration variables:

- **type** (*Required*): Possible values are `key_up`, `key_down`, and `key_hold`. Be careful, `key_hold` will fire a lot of events.
- **device_descriptor** (*Optional*): Path to the local event input device file that corresponds to the keyboard.
- **device_name** (*Optional*): Name of the keyboard device.

Either `device_name` or `device_descriptor` must be present in the configuration entry. Indicating a device name is useful in case of repeating disconnections and re-connections of the device (for example, a bluetooth keyboard): the local input device file might change, thus breaking the configuration, while the name remains the same.
In case of presence of multiple devices of the same model, `device_descriptor` must be used.

A list of possible device descriptors and names is reported in the debug log at startup when the device indicated in the configuration entry could not be found.

A full configuration for Keyboard Remote could look like the one below:

```yaml
keyboard_remote:
  device_descriptor: '/dev/input/by-id/bluetooth-keyboard'
  type: 'key_up'
```

or like the following:

```yaml
keyboard_remote:
  device_name: 'Bluetooth Keyboard'
  type: 'key_down'
```

And an automation rule to breathe life into it:

```yaml
automation:
  alias: Keyboard all lights on
  trigger:
    platform: event
    event_type: keyboard_remote_command_received
    event_data:
      key_code: 107 # inspect log to obtain desired keycode
  action:
    service: light.turn_on
    entity_id: light.all
```

## {% linkable_title Disconnections %}
This component manages disconnections and re-connections of the keyboard, for example in the case of a Bluetooth device that turns off automatically to preserve battery.

If the keyboard disconnects, the component will fire an event `keyboard_remote_disconnected`.
When the keyboard reconnects, an event `keyboard_remote_connected` will be fired.

Here's an automation example that plays a sound through a media player whenever the keyboard connects/disconnects:
```yaml
automation:
  - alias: Keyboard Connected
    trigger:
      platform: event
      event_type: keyboard_remote_connected
    action:
      - service: media_player.play_media
        data:
          entity_id: media_player.speaker
          media_content_id: keyboard_connected.wav
          media_content_type: music
  - alias: Keyboard Disconnected
    trigger:
      platform: event
      event_type: keyboard_remote_disconnected
    action:
      - service: media_player.play_media
        data:
          entity_id: media_player.speaker
          media_content_id: keyboard_disconnected.wav
          media_content_type: music
```

## {% linkable_title Permissions %}
There might be permissions problems with the event input device file. If this is the case, the user that Home Assistant runs as must be allowed read and write permissions with:

```bash
$ sudo setfacl -m u:HASS_USER:rw /dev/input/event*
```

where `HASS_USER` is the user who runs Home Assistant.

If you want to make this permanent, you can use a udev rule that sets it for all event input devices. Add a file `/etc/udev/rules.d/99-userdev-input.rules` containing:

```bash
KERNEL=="event*", SUBSYSTEM=="input", RUN+="/usr/bin/setfacl -m u:HASS_USER:rw $env{DEVNAME}"
```

You can check ACLs permissions with

```bash
$ getfacl /dev/input/event*
```
