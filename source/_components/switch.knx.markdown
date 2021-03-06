---
layout: page
title: "KNX Switch"
description: "Instructions on how to integrate KNX switches with Home Assistant."
date: 2016-06-24 12:00
sidebar: true
comments: false
sharing: true
footer: true
logo: knx.png
ha_category:
  - Switch
ha_release: 0.24
ha_iot_class: Local Polling
---

The `knx` switch integration is used as in interface to switching actuators.

The `knx` integration must be configured correctly, see [KNX Component](/components/knx).

## Configuration

To use your KNX switch in your installation, add the following to your `configuration.yaml` file:

```yaml
switch:
  - platform: knx
    name: Kitchen.Coffee
    address: '1/1/6'
```

{% configuration %}
address:
  description: KNX group address for switching the switch on/off.
  required: true
  type: string
name:
  description: A name for this device used within Home Assistant.
  required: false
  default: KNX Switch
  type: string
state_address:
  description: Separate KNX group address for retrieving the switch state.
  required: false
  type: string
{% endconfiguration %}

Some KNX devices can change their state internally without any messages on the KNX bus, e.g., if you configure a timer on a channel. The optional `state_address` can be used to inform Home Assistant about these state changes. If a KNX message is seen on the bus addressed to the given state address, this will overwrite the state of the switch object.
For switching actuators that are only controlled by a single group address and can't change their state internally, you don't have to configure the state address.
