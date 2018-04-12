---
layout: page
title: "Conversation"
description: "Instructions on how to have conversations with your Home Assistant."
date: 2015-03-15 00:39
sidebar: true
comments: false
sharing: true
footer: true
logo: home-assistant.png
ha_category: "Voice"
---

The conversation component allows you to converse with Home Assistant. You can either converse by pressing the microphone in the frontend (supported browsers only (no iOS)) or by calling the `conversation/process` service with the transcribed text.

<p class='img'>
  <img src="/images/screenshots/voice-commands.png" />
  Screenshot of the conversation interface in Home Assistant.
</p>

```yaml
# Example base configuration.yaml entry
conversation:
```

{% configuration %}
intents:
  description: Intents that the conversation component should understand.
  required: false
  type: map
  keys:
    '`<INTENT NAME>`':
      description: Sentences that should trigger this intent.
      required: true
      type: list
{% endconfiguration %}

## {% linkable_title Adding custom sentences %}

By default, it will support turning devices on and off. You can say things like "turn on kitchen lights" or "turn the living room lights off". You can also configure your own sentences to be processed. This works by mapping sentences to intents and then configure the [intent script component](/components/intent_script/) to handle these intents.

Here is a simple example to be able to ask what the temperature in the living room is.

```yaml
# Example configuration.yaml entry
conversation:
  intents:
    LivingRoomTemperature:
     - What is the temperature in the living room

intent_script:
  LivingRoomTemperature:
    speech:
      text: It is currently {% raw %}{{ states.sensor.temperature }}{% endraw %} degrees in the living room.
```

## {% linkable_title Adding advanced custom sentences %}

Sentences can contain slots (marked with curly braces: `{name}`) and optional words (marked with square brackets: `[the]`). The values of slots will be passed on to the intent and are available inside the templates.

The following configuration can handle the following sentences:

 - Change the lights to red
 - Change the lights to green
 - Change the lights to blue
 - Change the lights to the color red
 - Change the lights to the color green
 - Change the lights to the color blue

```yaml
# Example configuration.yaml entry
conversation:
  intents:
    ColorLight:
     - Change the lights to [the color] {color}
{% raw %}
intent_script:
  ColorLight:
    speech:
      text: Changed the lights to {{ color }}.
    action:
      service: light.turn_on
      data_template:
        rgb_color:
          - "{% if color == 'red' %}255{% else %}0{% endif %}"
          - "{% if color == 'green' %}255{% else %}0{% endif %}"
          - "{% if color == 'blue' %}255{% else %}0{% endif %}"
{% endraw %}
```
