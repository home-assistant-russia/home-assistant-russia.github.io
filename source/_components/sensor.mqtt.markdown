---
layout: page
title: "MQTT Sensor"
description: "Instructions on how to integrate MQTT sensors within Home Assistant."
date: 2015-05-30 23:21
sidebar: true
comments: false
sharing: true
footer: true
logo: mqtt.png
ha_category: Sensor
ha_release: 0.7
ha_iot_class: depends
---


This `mqtt` sensor platform uses the MQTT message payload as the sensor value. If messages in this `state_topic` are published with *RETAIN* flag, the sensor will receive an instant update with last known value. Otherwise, the initial state will be undefined.

To use your MQTT sensor in your installation, add the following to your `configuration.yaml` file:

```yaml
# Example configuration.yml entry
sensor:
  - platform: mqtt
    state_topic: "home/bedroom/temperature"
```

{% configuration %}
state_topic:
  description: The MQTT topic subscribed to receive sensor values.
  required: true
  type: string
name:
  description: Name of the MQTT sensor.
  required: false
  type: string
  default: MQTT Sensor
qos:
  description: The maximum QoS level of the state topic.
  required: false
  type: int
  default: 0
unit_of_measurement:
  description: Defines the units of measurement of the sensor, if any.
  required: false
  type: string
icon:
  description: Icon for the sensor (e.g. `mdi:gauge`).
  required: false
  type: string
expire_after:
  description: Defines the number of seconds after the value expires if it's not updated.
  required: false
  type: int
  default: 0
value_template:
  description: "Defines a [template](/docs/configuration/templating/#processing-incoming-data) to extract the value."
  required: false
  type: template
force_update:
  description: Sends update events even if the value hasn't changed. Useful if you want to have meaningful value graphs in history.
  reqired: false
  type: boolean
  default: False
availability_topic:
  description: The MQTT topic subscribed to receive availability (online/offline) updates.
  required: false
  type: string
payload_available:
  description: The payload that represents the available state.
  required: false
  type: string
  default: online
payload_not_available:
  description: The payload that represents the unavailable state.
  required: false
  type: string
  default: offline
json_attributes:
  description: A list of keys to extract values from a JSON dictionary payload and then set as sensor attributes.
  reqired: false
  type: list, string
unique_id:
  description: "An id that uniquely identifies this sensor. If 2 sensors have the same unique id, Home Assistant will raise an exception.**"
  required: false
  type: string
{% endconfiguration %}

## {% linkable_title Examples %}

In this section you find some real life examples of how to use this sensor.

### {% linkable_title JSON attributes configuration %}

The example sensor below shows a configuration example which uses JSON in the state topic to add extra attributes. It also makes use of the availability topic. Attributes can then be extracted in [Templates](configuration/templating/#attributes); Example to extract data from the sensor below {% raw %}'{{ states.sensor.bs_client_name.attributes.ClientName }}'{% endraw %}.

{% raw %}
```yaml
# Example configuration.yml entry
sensor:
  - platform: mqtt
    state_topic: "HUISHS/BunnyShed/NodeHealthJSON"
    name: "BS RSSI"
    unit_of_measurement: "dBm"
    value_template: '{{ value_json.RSSI }}'
    availability_topic: "HUISHS/BunnyShed/status"
    payload_available: "online"
    payload_not_available: "offline"
    json_attributes:
      - ClientName
      - IP
      - MAC
      - RSSI
      - HostName
      - ConnectedSSID  
```
{% endraw %}

### {% linkable_title Get battery level %}

If you are using the [Owntracks](/components/device_tracker.owntracks/) and enable the reporting of the battery level then you can use a MQTT sensor to keep track of your battery. A regular MQTT message from Owntracks looks like this: 

```bash
owntracks/tablet/tablet {"_type":"location","lon":7.21,"t":"u","batt":92,"tst":144995643,"tid":"ta","acc":27,"lat":46.12}
```

Thus the trick is extracting the battery level from the payload.

{% raw %}
```yaml
# Example configuration.yml entry
sensor:
  - platform: mqtt
    state_topic: "owntracks/tablet/tablet"
    name: "Battery Tablet"
    unit_of_measurement: "%"
    value_template: '{{ value_json.batt }}'
```
{% endraw %}

### {% linkable_title Get temperature and humidity %}

If you are using a DHT sensor and a NodeMCU board (esp8266), you can retrieve temperature and humidity with a MQTT sensor. A code example can be found [here](https://github.com/mertenats/open-home-automation/tree/master/ha_mqtt_sensor_dht22). A regular MQTT message from this example looks like this: 

```json
office/sensor1
  {
    "temperature": 23.20,
    "humidity": 43.70
  }
```

Then use this configuration example to extract the data from the payload:

{% raw %}
```yaml
# Example configuration.yml entry
sensor:
  - platform: mqtt
    state_topic: 'office/sensor1'
    name: 'Temperature'
    unit_of_measurement: '°C'
    value_template: '{{ value_json.temperature }}'
  - platform: mqtt
    state_topic: 'office/sensor1'
    name: 'Humidity'
    unit_of_measurement: '%'
    value_template: '{{ value_json.humidity }}'
```
{% endraw %}

### {% linkable_title Get sensor value from a device with ESPEasy %}

Assuming that you have flashed your ESP8266 unit with [ESPEasy](https://github.com/letscontrolit/ESPEasy). Under "Config" set a name ("Unit Name:") for your device (here it's "bathroom"). A "Controller" for MQTT with the protocol "OpenHAB MQTT" is present and the entries ("Controller Subscribe:" and "Controller Publish:") are adjusted to match your needs. In this example the topics are prefixed with "home". Also, add a sensor in the "Devices" tap with the name "analog" and "brightness" as value. 

As soon as the unit is online, you will get the state of the sensor.

```bash
home/bathroom/status Connected
...
home/bathroom/analog/brightness 290.00
```

The configuration will look like the example below:

{% raw %}
```yaml
# Example configuration.yml entry
sensor:
  - platform: mqtt
    state_topic: 'home/bathroom/analog/brightness'
    name: Brightness
```
{% endraw %}


