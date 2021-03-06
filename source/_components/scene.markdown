---
layout: page
title: "Scenes"
description: "Instructions on how to setup scenes within Home Assistant."
date: 2015-03-23 19:59
sidebar: true
comments: false
sharing: true
footer: true
logo: home-assistant.png
ha_category:
  - Organization
ha_qa_scale: internal
ha_release: 0.15
---

You can create scenes that capture the states you want certain entities to be. For example, a scene can specify that light A should be turned on and light B should be bright red.

```yaml
# Example configuration.yaml entry
scene:
  - name: Romantic
    entities:
      light.tv_back_light: true
      light.ceiling:
        state: true
        xy_color: [0.33, 0.66]
        brightness: 200
  - name: Movies
    entities:
      light.tv_back_light:
        state: true
        brightness: 100
      light.ceiling: false
      media_player.sony_bravia_tv:
        source: HDMI 1
```

{% configuration %}
name:
  description: Friendly name of scene.
  required: true
  type: string
entities:
  description: Entities to control.
  required: true
  type: list
{% endconfiguration %}

As you can see, there are two ways to define the states of each `entity_id`:

- Define the `state` directly with the entity.
- Define a complex state with its attributes.

The mapping from states to services is done with the [state helper](https://github.com/home-assistant/home-assistant/blob/master/homeassistant/helpers/state.py#L82). So, please have a look there for available states for your scenes.

Scenes can be activated using the service `scene.turn_on` (there is no 'scene.turn_off' service).

```yaml
# Example automation
...
automation:
  trigger:
    platform: state
    entity_id: device_tracker.sweetheart
    from: 'not_home'
    to: 'home'
  action:
    service: scene.turn_on
    entity_id: scene.romantic
```

<p class='note'>
Please note that the scene integration for the most part only supports one service call per entity to achieve the state. Due to this limitation, you cannot set states belonging to different services. A workaround for this limitation is to write a script, which you then turn on in your scene. A few integrations have direct support for multiple service calls per state, Currently this is the media_player and climate components.
</p>
