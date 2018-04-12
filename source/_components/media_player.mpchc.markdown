---
layout: page
title: "MPC-HC"
description: "Instructions on how to integrate MPC-HC into Home Assistant."
date: 2016-07-27 21:21
sidebar: true
comments: false
sharing: true
footer: true
logo: mpchc.png
ha_category: Media Player
featured: false
ha_release: 0.25
ha_iot_class: "Local Polling"
---


The `mpchc` platform allows you to connect a [Media Player Classic Home Cinema](https://mpc-hc.org/) to Home Assistant. It will allow you to see the current playing item, and respond to changes in the player's state.

For this component to function, you will need to enable the Web Interface in the MPC-HC options dialog.

<p class='img'>
  <img src='{{site_root}}/images/screenshots/mpc-hc.png' />
</p>

If the server running Home Assistant is not the same device that is running MPC-HC, you will need to ensure that the *allow access from localhost only* option is not set.

<p class='note warning'>
The MPC-HC web interface is highly insecure, and allows remote clients full player control file-system access without authentication. Never allow access to the Web UI from outside of your trusted network, and if possible [use a proxy script to restrict control or redact sensitive information](https://github.com/abcminiuser/mpc-hc-webui-proxy).
</p>

To add MPC-HC to your installation, add the following to your `configuration.yaml` file:

```yaml
# Example configuration.yaml entry
media_player:
  - platform: mpchc
    host: http://192.168.0.123
```

Configuration variables:

- **host** (*Required*): The host name or address of the device that is running MPC-HC.
- **port** (*Optional*): The port number. Defaults to 13579.
- **name** (*Optional*): The name of the device used in the frontend.
