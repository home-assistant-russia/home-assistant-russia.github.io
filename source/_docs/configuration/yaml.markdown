---
layout: page
title: "YAML"
description: "Details about YAML to configure Home Assistant."
date: 2015-03-23 12:50
sidebar: true
comments: false
sharing: true
footer: true
redirect_from: /getting-started/yaml/
---

Home Assistant uses the [YAML](http://yaml.org/) syntax for configuration. YAML might take a while to get used to but is really powerful in allowing you to express complex configurations.

For each component that you want to use in Home Assistant, you add code in your `configuration.yaml` file to specify its settings.
The following example entry specifies that you want to use the [notify component](/components/notify) with the [pushbullet platform](/components/notify.pushbullet).


```yaml
notify:
  platform: pushbullet
  api_key: "o.1234abcd"
  name: pushbullet
```

- A **component** provides the core logic for some functionality (like `notify` provides sending notifications).
- A **platform** makes the connection to a specific software or hardware platform (like `pushbullet` works with the service from pushbullet.com).

The basics of YAML syntax are block collections and mappings containing key-value pairs. Each item in a collection starts with a `-` while mappings have the format `key: value`. If you specify duplicate keys, the last value for a key is used. This is somewhat similar to a Hashtable or more specifically a dictionary in Python. These can be nested as well.

Note that indentation is an important part of specifying relationships using YAML. Things that are indented are nested "inside" things that are one level higher. So in the above example, `platform: pushbullet` is a property of (nested inside) the `notify` component.

Getting the right indentation can be tricky if you're not using an editor with a fixed width font. Tabs are not allowed to be used for indentation. Convention is to use 2 spaces for each level of indentation.

You can use the online service [YAMLLint](http://www.yamllint.com/) to check if your YAML syntax is correct before loading it into Home Assistant which will save you some time. If you do so, be aware that this is a third-party service and is not maintained by the Home Assistant community.

<p class='note'>
Please pay attention on not storing private data (passwords, API keys, etc.) directly in your `configuration.yaml` file. Private data can be stored in a [separate file](/docs/configuration/secrets/) or in [environmental variables](/docs/configuration/yaml/#using-environment-variables), which circumvents this problem of security.
</p>

Text following a `#` are comments and are ignored by the system.

The next example shows an [input_select](/components/input_select) component that uses a block collection for the options values.
The other properties (like name) are specified using mappings. Note that the second line just has `threat:` with no value on the same line. Here threat is the name of the input_select and the values for it are everything nested below it.

```yaml
input_select:
  threat:
    name: Threat level
# A collection is used for options
    options:
     - 0
     - 1
     - 2
     - 3
    initial: 0
```

The following example shows nesting a collection of mappings in a mapping. In Home Assistant, this would create two sensors that each use the MQTT platform but have different values for their `state_topic` (one of the properties used for MQTT sensors).

```yaml
sensor:
  - platform: mqtt
    state_topic: sensor/topic
  - platform: mqtt
    state_topic: sensor2/topic
```

### {% linkable_title Using Environment Variables %}

You can include values from your system's environment variables with `!env_var`.

```yaml
http:
  api_password: !env_var PASSWORD
```

#### Default Value

If an environment variable is not set, you can fallback to a default value.

```yaml
http:
  api_password: !env_var PASSWORD default_password
```

### {% linkable_title Including Separate Files %}

To improve readability, you can source out certain domains from your main configuration file with the `!include`-syntax.

```yaml
lights: !include lights.yaml
```

More information about this feature can also be found at [splitting configuration](/docs/configuration/splitting_configuration/).
