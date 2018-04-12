---
layout: page
title: "Owntracks"
description: "Instructions on how to use Owntracks to track devices in Home Assistant."
date: 2015-09-22 07:00
sidebar: true
comments: false
sharing: true
footer: true
logo: owntracks.png
ha_category: Presence Detection
featured: false
ha_release: 0.7.4
---

This platform allows you to detect presence using [Owntracks](http://owntracks.org/). OwnTracks allows users to track their location on iOS phones and publish it to an MQTT broker. This platform will connect to the broker and monitor for new locations.

This component requires [the MQTT component](/components/mqtt/) to be set up and works very well together with [the zone component](/components/zone/).

To integrate Owntracks in Home Assistant, add the following section to your `configuration.yaml` file:

```yaml
# Example configuration.yaml entry
device_tracker:
  - platform: owntracks
```

Configuration variables:

- **max_gps_accuracy** (*Optional*): Sometimes Owntracks can report GPS location with a very low accuracy (few kilometers). That can trigger false zoning in your Home Assistant installation. With the parameter, you can filter these GPS reports. The number has to be in meter. For example, if you put 200 only GPS report with an accuracy under 200 will be take in account.
- **waypoints** (*Optional*): Owntracks users can define [waypoints](http://owntracks.org/booklet/features/waypoints/) (a.k.a regions) which are similar in spirit to Home Assistant zones. If this configuration variable is `True`, the Owntracks users who are in `waypoint_whitelist` can export waypoints from the device and Home Assistant will import them as zone definitions. Defaults to `True`.
- **waypoint_whitelist** (*Optional*): A list of user names (as defined for [Owntracks](/components/device_tracker.owntracks/)) who can export their waypoints from Owntracks to Home Assistant.  This would be the `username` portion of the Base Topic Name, (e.g., owntracks/**username**/iPhone). Defaults to all users who are connected to Home Assistant via Owntracks.
- **secret** (*Optional*): [Payload encryption key](http://owntracks.org/booklet/features/encrypt/). This is usable when communicating with a third-party untrusted server or a public server (where anybody can subscribe to any topic). By default the payload is assumed to be unencrypted (although the communication between Home Assistant and the server might still be encrypted). This feature requires the `libsodium` library to be present.
- **mqtt_topic** (*Optional*): The topic to subscribe for Owntracks updates on your MQTT instance (defaults to `owntracks/#`).
- **events_only** (*Optional*): Home Assistant will ignore all location updates and rely solely on geofence enter/leave events.
- **region_mapping** (*Optional*): Dictionary to remap names of regions as configured in the Owntracks app to Home Assistant zones. Use this if you have multiple homes or Home Assistant instances and want to map a different label to 'home'. `key: value` maps Owntracks region `key` to Home Assistant zone `value`.

A full sample configuration for the `owntracks` platform is shown below:

```yaml
# Example configuration.yaml entry
device_tracker:
  - platform: owntracks
    max_gps_accuracy: 200
    waypoints: True
    mqtt_topic: "owntracks/#"
    events_only: True
    waypoint_whitelist:
      - jon
      - ram
    region_mapping:
      cabin: home
      office: work
```

### {% linkable_title Using Owntracks with other device trackers %}

Owntracks can also be used with other device trackers, such as [Nmap](/components/device_tracker.nmap_tracker/) or [Netgear](/components/device_tracker.netgear/). To do this, fill in the `mac` field to the Owntracks entry in `known_devices.yaml` with the MAC address of the device you want to track. This way the state of the device will be determined by the source that reported last. The naming convention for known device list is `<username>_<device-id>` and could be set in app configuration. More details about this config can found in [device tracker](/components/device_tracker/).

An example showing the inclusion of the `mac` field for multiple component tracking. The `mac` field will need to be added to the `owntracks` device and will enable tracking by all components that track via the `mac` address.

```yaml
USERNAME_DEVICE_ID:
  name: Friendly Name
  mac: EA:AA:55:E7:C6:94
  picture: https://www.home-assistant.io/images/favicon-192x192.png
  gravatar: test@example.com
  track: yes
  hide_if_away: no
```

### {% linkable_title Using Owntracks regions %}

Owntracks can track regions, and send region entry and exit information to Home Assistant (HA). You set up a region in the Owntracks app which you should name the same as your HA Zone, and then make sure to turn on the `share` option for the region in the owntracks app. Please see the [owntracks documentation](http://owntracks.org/booklet/guide/waypoints/).

Home Assistant will use the enter and leave messages to set your zone location. Your location will be set to the center of zone when you enter. Location updates from OwnTracks will be ignored while you are inside a zone.

When you exit a zone, Home Assistant will start using location updates to track you again. To make sure that Home Assistant correctly exits a zone (which it calculates based on your GPS coordinates), you may want to set your Zone radius in HA to be slightly smaller that the Owntracks region radius.

### {% linkable_title Using Owntracks regions - forcing Owntracks to update using  %}iBeacons

When run in the usual *significant changes mode* (which is kind to your phone battery), Owntracks sometimes doesn't update your location as quickly as you'd like when you arrive at a zone. This can be annoying if you want to trigger an automation when you get home. You can improve the situation using iBeacons.

iBeacons are simple Bluetooth devices that send out an "I'm here" message. They are supported by IOS and some Android devices. Owntracks explain more [here](http://owntracks.org/booklet/guide/beacons/).

When you enter an iBeacon region, Owntracks will send a `region enter` message to HA as described above. So if you want to have an event triggered when you arrive home, you can put an iBeacon outside your front door. If you set up an OwnTracks iBeacon region called `home` then getting close to the beacon will trigger an update to HA that will set your zone to be `home`.

When you exit an iBeacon region HA will switch back to using GPS to determine your location. Depending on the size of your zone, and the accuracy of your GPS location this may change your HA zone.

Sometimes Owntracks will lose connection with an iBeacon for a few seconds. If you name your beacon starting with `-` Owntracks will wait longer before deciding it has exited the beacon zone. HA will ignore the `-` when it matches the Owntracks region with Zones. So if you call your Owntracks region `-home` then HA will recognize it as `home`, but you will have a more stable iBeacon connection.

### {% linkable_title Using Owntracks iBeacons to track devices %}

iBeacons don't need to be stationary. You could put one on your key ring, or in your car.

When your phone sees a mobile iBeacon that it knows about, it will tell HA the location of that iBeacon. If your phone moves while you are connected to the iBeacon, HA will update the location of the iBeacon. But when your phone loses the connection, HA will stop updating the iBeacon location.

To use mobile iBeacons with HA, you just set up a region that doesn't match your Zone names. If HA sees an entry event for an iBeacon region that doesn't match a Zone name (say `keys`) - it will start tracking it, calling the device `device_tracker.beacon_keys`).

This allows you to write zone automations for devices that can't track themselves (for example *alert me if I leave the house and my keys are still at home*). Another example would be *open the gates if my car arrives home*.

### {% linkable_title Using mobile and fixed iBeacons together %}

You can use iBeacons of both types together, so if you have a Zone `drive` with an iBeacon region called `-drive` and you arrive home with a mobile iBeacon called `-car`, then `device_tracker.beacon_car` will be set to a state of `drive`.

### {% linkable_title Importing Owntracks waypoints as zones %}

By default, any Owntracks user connected to Home Assistant can export their waypoint definitions (from the *Export - Export to Endpoint* menu item) which will then be translated to zone definitions in Home Assistant. The zones will be named `<user>-<device> - <waypoint name>`. This functionality can be controlled in 2 ways:

1. The configuration variable `waypoints` can be set to `False` which will disable importing waypoints for all users.
2. The configuration variable `waypoint_whitelist` can contain a list of users who are allowed to import waypoints.
