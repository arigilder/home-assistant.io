---
layout: page
title: "Remote Raspberry Pi GPIO"
description: "Instructions on how to integrate the GPIO capability of a Remote Raspberry Pi into Home Assistant."
date: 2019-02-20 19:00
sidebar: true
comments: false
sharing: true
footer: true
logo: raspberry-pi.png
ha_category:
  - DIY
  - Binary Sensor
  - Switch
ha_release: 0.94 
ha_iot_class: Local Push
---

The `rpi_gpio` integration is the base for all related GPIO platforms in Home Assistant. There is no setup needed for the integration itself, for the platforms please check their corresponding sections.

## Binary Sensor

The `remote_rpi_gpio` binary sensor platform allows you to read sensor values of the GPIOs of a [Remote Raspberry Pi](https://www.raspberrypi.org/).

To use your Remote Raspberry Pi's GPIO in your installation, add the following to your `configuration.yaml` file:

```yaml
# Example configuration.yaml entry
binary_sensor:
  - platform: remote_rpi_gpio
    host: IP_ADDRESS_OF_REMOTE_PI
    ports:
      11: PIR Office
      12: PIR Bedroom
```

{% configuration %}
host:
  description: IP Address of remote Raspberry Pi.
  required: true
  type: string
ports:
  description: List of used ports.
  required: true
  type: map
  keys:
    "port: name":
      description: The port numbers (BCM mode pin numbers) and corresponding names.
      required: true
      type: string
invert_logic:
  description: If `true`, inverts the output logic
  required: false
  type: boolean
  default: "`false` (ACTIVE HIGH)"
pull_mode:
  description: >
    Type of internal pull resistor to use.
    Options are `UP` - pull-up resistor and `DOWN` - pull-down resistor.
    Pull-Up defaults to active LOW and Pull-down defaults to active HIGH.  This can be adjusted with invert_logic
  required: false
  type: string
  default: "`UP`"
{% endconfiguration %}

For more details about the GPIO layout, visit the Wikipedia [article](https://en.wikipedia.org/wiki/Raspberry_Pi#GPIO_connector) about the Raspberry Pi.

## Switch

The `remote_rpi_gpio` switch platform allows you to control the GPIOs of a [Remote Raspberry Pi](https://www.raspberrypi.org/).

To use your Remote Raspberry Pi's GPIO in your installation, add the following to your `configuration.yaml` file:

```yaml
# Example configuration.yaml entry
switch:
  - platform: remote_rpi_gpio
    host: IP_ADDRESS_OF_REMOTE_PI
    ports:
      11: Fan Office
      12: Light Desk
```

{% configuration %}
host:
  description: IP Address of remote Raspberry Pi.
  required: true
  type: string
ports:
  description: Array of used ports.
  required: true
  type: list
  keys:
    port:
      description:  Port numbers and corresponding names (GPIO #).
      required: true
      type: [integer, string]
invert_logic:
  description: If true, inverts the output logic to ACTIVE LOW.
  required: false
  default: false
  type: boolean
{% endconfiguration %}

For more details about the GPIO layout, visit the Wikipedia [article](https://en.wikipedia.org/wiki/Raspberry_Pi#GPIO_connector) about the Raspberry Pi.

<p class='note warning'>
Note that a pin managed by HASS is expected to be exclusive to HASS.
</p>

A common question is what does port refer to, this number is the actual GPIO #, not the pin #.
For example, if you have a relay connected to pin 11 its GPIO # is 17.

```yaml
# Example configuration.yaml entry
switch:
  - platform: remote_rpi_gpio
    host: 192.168.0.123
    ports:
      17: Speaker Relay
```
