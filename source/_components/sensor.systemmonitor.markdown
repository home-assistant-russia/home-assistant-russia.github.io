---
layout: page
title: "System Monitor"
description: "Instructions on how to monitor the Home Assistant host."
date: 2015-03-23 19:59
sidebar: true
comments: false
sharing: true
footer: true
logo: system_monitor.png
ha_category: System Monitor
ha_release: pre 0.7
ha_iot_class: "Local Push"
---

The `systemmonitor` sensor platform allows you to monitor disk usage, memory usage, CPU usage, and running processes. This platform has superseded the process component which is now considered deprecated.

To add this platform to your installation, add the following to your `configuration.yaml` file:

```yaml
# Example configuration.yaml entry
sensor:
  - platform: systemmonitor
    resources:
      - type: disk_use_percent
        arg: /home
      - type: memory_free
```

Configuration variables:

- **resources** array (*Required*): Contains all entries to display.
  - **type** (*Required*): The type of the information to display, please check the table below for details.
  - **arg** (*Optional*): Argument to use, please check the table below for details.

The table contains types and their argument to use in your `configuration.yaml` file.

| Type (`type:`)      | Argument (`arg:`)         |
| :------------------ |:--------------------------|
| disk_use_percent    | Path, eg. `/`             |
| disk_use            | Path, eg. `/`             |
| disk_free           | Path, eg. `/`             |
| memory_use_percent  |                           |
| memory_use          |                           |
| memory_free         |                           |
| swap_use_percent    |                           |
| swap_use            |                           |
| swap_free           |                           |
| load_1m             |                           |
| load_5m             |                           |
| load_15m            |                           |
| network_in          | Interface, eg. `eth0`     |
| network_out         | Interface, eg. `eth0`     |
| packets_in          | Interface, eg. `eth0`     |
| packets_out         | Interface, eg. `eth0`     |
| ipv4_address        | Interface, eg. `eth0`     |
| ipv6_address        | Interface, eg. `eth0`     |
| processor_use       |                           |
| process             | Binary, e.g., `octave-cli` |
| last_boot           |                           |
| since_last_boot     |                           |

## {% linkable_title Linux specific %}

To retrieve all available network interfaces on a Linux System, execute the `ifconfig` command.

```bash
$ ifconfig -a | sed 's/[ \t].*//;/^$/d'
```

## {% linkable_title Windows specific %}

When running this platform on Microsoft Windows, Typically, the default interface would be called `Local Area Connection`, so your configuration might look like:

```yaml
sensor:
  - platform: systemmonitor
    resources:
      - type: network_in
        arg: 'Local Area Connection'
```

If you need to use some other interface, open a command line prompt and type `ipconfig` to list all interface names. For example a wireless connection output from `ifconfig` might look like:

```bash
Wireless LAN adapter Wireless Network Connection:

   Media State . . . . . . . . . . . : Media disconnected
   Connection-specific DNS Suffix  . :
```

Where the name is `Wireless Network Connection`
