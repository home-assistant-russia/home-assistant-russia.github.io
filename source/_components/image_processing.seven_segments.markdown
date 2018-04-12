---
layout: page
title: "Seven segments display"
description: "Instructions on how to use OCR for seven segments displays into Home Assistant."
date: 2017-05-18 08:00
sidebar: true
comments: false
sharing: true
footer: true
logo: home-assistant.png
ha_category: Image Processing
featured: false
ha_release: 0.45
og_image: /images/screenshots/ssocr.png
ha_iot_class: "Local Polling"
---

The `seven_segments` image processing platform allows you to read physical seven segments displays through Home Assistant. [`ssocr`](https://www.unix-ag.uni-kl.de/~auerswal/ssocr/) is used to extract the value shown on the display which is observed by a [camera](/components/camera/).

<p class='note'>
If you are using [Hass.io](/hassio/) then just move forward to the configuration as all requirements are already fulfilled.
</p>

`ssocr` needs to be available on your system. Check the installation instruction below:

```bash
$ sudo dnf -y install imlib2-devel # Fedora
$ sudo apt install libimlib2-dev # Ubuntu
$ brew install imlib2 # macOS
$ git clone https://github.com/auerswal/ssocr.git
$ cd ssocr
$ make
$ sudo make PREFIX=/usr install # On most systems
$ make deb # (Optional) This allows you to make a deb so that you apt is aware of ssocr
```

To enable the OCR of a seven segment display in your installation, add the following to your `configuration.yaml` file:

```yaml
# Example configuration.yaml entry
image_processing:
  - platform: seven_segments
    source:
      - entity_id: camera.seven_segments
```

Configuration variables:

- **ssocr_bin** (*Optional*): The command line tool `ssocr`. Set it if you use a different name for the executable. Defaults to `ssocr`.
- **x_position** (*Optional*): X coordinate of the upper left corner of the area to crop. Defaults to `0`.
- **y_position** (*Optional*):  Y coordinate of the upper left corner of the area to crop. Defaults to `0`.
- **height** (*Optional*): Height of the area to crop. Defaults to `0`.
- **width** (*Optional*): Width of the area to crop. Defaults to `0`.
- **rotate** (*Optional*): Rotation of the image. Defaults to `0`.
- **threshold** (*Optional*): Threshold for the difference between the digits and the background. Defaults to `0`.
- **digits** (*Optional*): Number of digits in the display. Defaults to `-1`.
- **extra_arguments** (*Optional*): Other arguments to use. Like `-D`, `dilation`, `erosion`, `greyscale`, `make_mono`, etc.
- **source** array (*Required*): List of image sources.
  - **entity_id** (*Required*): A camera entity id to get picture from.
  - **name** (*Optional*): This parameter allows you to override the name of your `image_processing` entity.


### {% linkable_title Setup process %}

It's suggested that the first attempt to determine the needed parameters is using `ssocr` directly. This may require a couple of iterations to get the result

```bash
$ ssocr -D erosion crop 390 250 490 280 -t 20 -d 4 seven-seg.png
```

This would lead to the following entry for the `configuration.yaml` file:

```yaml
camera:
  - platform: local_file
    file_path: /home/homeassistant/.homeassistant/seven-seg.png
    name: seven_segments
image_processing:
  - platform: seven_segments
    x_position: 390
    y_position: 250
    height: 280
    width: 490
    threshold: 20
    digits: 4
    source:
      - entity_id: camera.seven_segments
```

<p class='img'>
  <img src='{{site_root}}/images/screenshots/ssocr.png' />
</p>

With the help of a [template sensor](/components/sensor.template/), the value can be shown as badge.

{% raw %}
```yaml
sensor:
  - platform: template
    sensors:
      power_meter:
        value_template: '{{ states.image_processing.sevensegment_ocr_seven_segments.state }}'
        friendly_name: 'Ampere'
        unit_of_measurement: 'A'
```
{% endraw %}
