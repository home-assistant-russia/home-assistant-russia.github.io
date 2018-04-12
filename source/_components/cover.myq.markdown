---
layout: page
title: "MyQ Cover"
description: "Instructions on how to integrate MyQ-Enabled garage door covers into Home Assistant."
date: 2017-02-14 14:21
sidebar: true
comments: false
sharing: true
footer: true
logo: myq.png
ha_category: Cover
ha_release: 0.39
ha_iot_class: Cloud Polling
---

The `myq` cover platform lets you control MyQ-Enabled garage doors through Home Assistant. Device names in Home Assistant are generated based on the names defined in your MyQ Device mobile app.

To use your MyQ cover in your installation, add the following to your `configuration.yaml` file:

```yaml
# Example configuration.yml entry
cover:
  - platform: myq
    username: YOUR_USERNAME
    password: YOUR_PASSWORD
    type: chamberlain
```

{% configuration %}
username:
  description: Your MyQ account username.
  required: true
  type: string
password:
  description: Your MyQ account password.
  required: true
  type: string
password:
  description: "Your device type/brand. Supported types are `chamberlain`, `liftmaster`, `craftsman` and `merlin`."
  required: true
  type: string
{% endconfiguration %}

