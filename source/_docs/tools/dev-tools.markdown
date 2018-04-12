---
layout: page
title: "Development Tools"
description: "Description of the Developer Tools."
release_date: 2017-02-23 11:00:00
sidebar: true
comments: false
sharing: true
footer: true
---

The frontend contains a section called "Developer Tools".

<p class='img'>
<img src='/images/screenshots/developer-tools.png' />
Screenshot of Home Assistant's Developer Tools.
</p>

| Section | Icon | Description |
| ------- |------| ----- |
| Services | <img src='/images/screenshots/developer-tool-services-icon.png' alt='service developer tool icon' class="no-shadow" height="38" /> | Calls services from components |
| States | <img src='/images/screenshots/developer-tool-states-icon.png' alt='service developer tool icon' class="no-shadow" height="38" /> | Sets the representation of an entity |
| Events | <img src='/images/screenshots/developer-tool-events-icon.png' alt='service developer tool icon' class="no-shadow" height="38" /> | Fires events |
| Templates | <img src='/images/screenshots/developer-tool-templates-icon.png' alt='service developer tool icon' class="no-shadow" height="38" /> | Renders templates |
| Info | <img src='/images/screenshots/developer-tool-about-icon.png' alt='service developer tool icon' class="no-shadow" height="38" /> | Details about Home Assistant |

## What can I do with Developer Tools?
The Developer Tools is meant for **all** (not just for the developers) to quickly try out things - like calling services, update states, raising events, and publish messages in mqtt…etc.). It is also a necessary tool for those who write custom automations and scripts by hand. The following describes each of the section in detail.

{% linkable_title Services %}

This section is used to call Services that are available in the ServiceRegistry.

The list of services in the “Service” drop down are automatically populated based on the components that are found in the configuration, automation and script files.  If a desired service does not exist, it means either the component is not configured properly or not defined in the configuration, automation or script files.

When a Service is selected, and if that service requires an `entity_id` to be passed, the “Entity” drop down will automatically be populated with corresponding entities.

A Service may also require additional input to be passed. It is commonly referred to as “service data”. The service data is only accepted in the JSON format, and it may be optional depending on the service.

When an entity is selected from the Entity drop down, it automatically populates service data with the corresponding `entity_id`. The service data JSON can then be modified to pass additional \[optional\] parameters. The following is an illustration on how to call a `light.turn_on` service.

To turn on a light bulb, use the following steps:
1.	Select `light.turn_on` from the Service drop down
2.	Select the entity (typically the light bulb) from the Entity drop down (if no entity_id is selected, it turns on ALL lights)
3.	If an entity is selected, the service data is populated with basic JSON that will be passed to the service. An additional data can also be passed by updating the JSON as below.

```json
{
  "entity_id": "light.bedroom",
  "brightness": 255,
  "rgb_color": [255, 0, 0]
}
```
{% linkable_title States %}

This section shows all the available entities, their corresponding state and the attribute values. The state and the attribute information is what Home Assistant sees at run time. To update the entity with a new state, or a new attribute value, click on the entity, scroll to the top, and modify the values, and click on “SET STATE” button.

Note that this is the state representation of a device within Home Assistant. That means, it is what Home Assistant sees, and it does not communicate with the actual device in any manner. The updated information can still be used to trigger events, and state changes. To communicate with the actual device, it is recommended to call services in the services section above, instead of updating state.

For ex: Changing the `light.bedroom` state from `off` to `on` does not turn on the light. If there is an automation that triggers on the `state` change of the `light.bedroom`, it will be triggered – even though the actual bulb has not turned on. Also, when the bulb state changes – the state information will be overridden. In other words, the changes that are made through the “States” section are temporary, and is recommended to use for testing purposes only.

{% linkable_title Events %}

This Events section is as basic as it can get. It does only one thing – fires events on the event bus.
To fire an event, simply type the name of the event, and pass the event data in JSON format.
For ex: To fire a custom event, enter the `event_type` as `event_light_state_changed` and the event data JSON as

```json
{ "state":"on" }
```

If there is an automation that handles that event, it will be automatically triggered. See below:
```yaml
- alias: Capture Event
  trigger:
    platform: event
    event_type: event_light_state_changed
  action:
    - service: notify.notify
      data_template:
        message: "Light is turned {{ trigger.event.data.state }}"
```

{% linkable_title Template Editor %}

The Template Editor provides a way to test the template code quickly. When the Template Editor page is loaded, it comes with a sample template code that illustrates how the code can be written and tested.

It has two sections, code goes on the left hand side, and the output is shown on the right hand side. The code can be removed and replaced, and when the page is loaded/refreshed, the default sample code will be loaded back.

It is a good practice to test the template code in the template editor prior to putting it in automations and scripts.

For more information about jinja2, visit [jinja2 documentation](http://jinja.pocoo.org/docs/dev/templates/), and also read templating document [here](/topics/templating/)


{% linkable_title mqtt %}

This section is only visible if the MQTT component is configured. To configure MQTT, add `mqtt:` to the `configuration.yaml` file. For more information, refer to the [mqtt](/components/mqtt/) component.

Even though MQTT in general provides deeper functionality, the developer tools section of MQTT is limited to publishing messages to a given topic. It supports templates for the payload. To publish a message, simply specify the topic name and the payload and click “PUBLISH” button.

{% linkable_title Info %}

The Information tab simply provides information about the current installed version, additional links and credits. The tab also contains a section that shows `syslog` information, and the contents of `home-assistant.log` with an option to clear and refresh the logs.
