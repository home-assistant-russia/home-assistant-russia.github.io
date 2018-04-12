---
layout: page
title: "Harmony Hub Remote"
description: "Instructions on how to integrate Harmony Hub remotes into Home Assistant."
date: 2016-11-05 17:00
sidebar: true
comments: false
sharing: true
footer: true
logo: logitech.png
ha_category: Remote
ha_iot_class: "Local Push"
ha_release: "0.34"
---


The `harmony` remote platform allows you to control the state of your [Harmony Hub Device](http://www.logitech.com/en-us/product/harmony-hub).

Supported units:

- Harmony Hub
- Harmony Companion
- Harmony Pro
- Harmony Elite

The preferred way to setup the Harmony remote is by enabling the [discovery component](/components/discovery/).

However, if you want to manually configure the device, you will need to add its settings to your `configuration.yaml` file:

```yaml
# Example configuration.yaml entry
remote:
  - platform: harmony
    name: Bedroom
    host: 10.168.1.13
```

You can override some default configuration values on a discovered hub (e.g., the `port` or `activity`) by adding a `configuration.yaml` setting. In this case leave the `host` setting empty so the platform will discover the host IP automatically, but set the `name` in the config to match exactly the name you have set for your Hub so the platform knows what Hub you are trying to configure.

```yaml
# Example configuration.yaml entry with discovery
  - platform: harmony
    name: Living Room 
    activity: Watch TV
```

Configuration variables:

- **name** (*Required*): The hub's name to display in the frontend. This name must match the name you have set on the Hub.
- **host** (*Optional*): The Harmony device's IP address. Leave empty for the IP to be discovered automatically.
- **port** (*Optional*): The Harmony device's port. Defaults to 5222.
- **activity** (*Optional*): Activity to use when `turn_on` service is called without any data. Overrides the `activity` setting for this discovered hub.
- **delay_secs** (*Optional*): Default duration in seconds between sending commands to a device.

Configuration file:

Upon startup one file will be written to your Home Assistant configuration directory per device in the following format: `harmony_REMOTENAME.conf`. The file will contain:

- List of all programmed activity names and ID numbers
- List of all programmed device names and ID numbers
- List of all available commands per programmed device

### {% linkable_title Service `remote.turn_off` %}

Turn off all devices that were switched on from the start of the current activity.

| Service data attribute | Optional | Description |
| ---------------------- | -------- | ----------- |
| `entity_id`            |      yes | Only act on a specific remote, else target all.

### {% linkable_title Service `remote.turn_on` %}

Start an activity. Will start the default `activity` from configuration.yaml if no activity is specified.  The specified activity can either be the activity name or the activity ID from the configuration file written to your [Home Assistant configuration directory](/docs/configuration/).

| Service data attribute | Optional | Description |
| ---------------------- | -------- | ----------- |
| `entity_id`            |      yes | Only act on a specific remote, else target all.
| `activity`             |      yes | Activity ID or Activity Name to start.

### {% linkable_title Service `remote.send_command` %}

Send a single command or a set of commands to one device, device ID and available commands are written to the configuration file at startup. You can optionally specify the number of times you wish to repeat the command(s) and delay you want between repeated command(s).

| Service data attribute | Optional | Description |
| ---------------------- | -------- | ----------- |
| `entity_id`            |      yes | Only act on a specific remote, else target all.
| `device`               |       no | Device ID to send the command to.
| `command`              |       no | A single command or a list of commands to send.
| `num_repeats`          |      yes | The number of times to repeat the command(s).
| `delay_secs`           |      yes | The number of seconds between sending each command.

A typical service call for sending several button presses looks like this:

```yaml
service: remote.send_command
data:
  entity_id: remote.tv_room
  command:
    - home
    - 1
    - 2
  device: 4576546
  delay_secs: 0.6
```

### {% linkable_title Service `remote.harmony_sync` %}

Synchronize the Harmony device with the Harmony web service if any changes are made from the web portal or app.

| Service data attribute | Optional | Description |
| ---------------------- | -------- | ----------- |
| `entity_id`            |      yes | Only act on a specific remote, else target all.

### {% linkable_title Examples %}

Template sensors can be utilized to display current activity in the frontend.

{% raw %}
```yaml
sensor:
  - platform: template
    sensors:
      family_room:
        value_template: '{{ states.remote.family_room.attributes.current_activity }}'
        friendly_name: 'Family Room'
      bedroom:
        value_template: '{{ states.remote.bedroom.attributes.current_activity }}'
        friendly_name: 'bedroom'
```
{% endraw %}

The example below shows how to control an `input_boolean` switch using the Harmony remote's current activity. The switch will turn on when the remote's state changes and the Kodi activity is started and off when the remote's state changes and the current activity is "PowerOff".

{% raw %}
```yaml
automation:
  - alias: "Watch TV started from harmony hub"
    trigger:
      platform: state
      entity_id: remote.family_room
    condition:
      condition: template
      value_template: '{{ trigger.to_state.attributes.current_activity == "Kodi" }}'
    action:
      service: input_boolean.turn_on
      entity_id: input_boolean.notify
  - alias: "PowerOff started from harmony hub"
    trigger:
      platform: state
      entity_id: remote.family_room
    condition:
      condition: template
      value_template: '{{ trigger.to_state.attributes.current_activity == "PowerOff" }}'
    action:
      service: input_boolean.turn_off
      entity_id: input_boolean.notify
```
{% endraw %}
