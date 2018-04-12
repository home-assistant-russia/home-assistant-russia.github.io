---
layout: page
title: "SleepIQ"
description: "Instructions for how to integrate SleepIQ beds within Home Assistant."
date: 2016-08-28 8:56
sidebar: true
comments: false
sharing: true
footer: true
logo: sleepiq.png
ha_category: Hub
ha_release: 0.29
ha_iot_class: "Local Polling"
---

The SleepIQ implementation lets you view sensor data from [SleepIQ by SleepNumber](http://www.sleepnumber.com/sn/en/sleepiq-sleep-tracker). In particular, it lets you see the occupancy and current SleepNumber (ie current firmness) of each side of a SleepNumber bed.

You will need an account on [SleepIQ](https://sleepiq.sleepnumber.com/) to use this component.

To set it up, add the following information to your `configuration.yaml` file:

```yaml
# Example configuration.yaml entry
sleepiq:
  username: YOUR_USERNAME
  password: YOUR_PASSWORD
```

{% configuration %}
username:
  description: Your SleepIQ username (usually an e-mail address).
  required: true
  type: string
password:
  description: Your SleepIQ password.
  required: true
  type: string
{% endconfiguration %}

