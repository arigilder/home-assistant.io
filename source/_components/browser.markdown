---
layout: page
title: "Browser"
description: "Instructions on how to setup the browser integration with Home Assistant."
date: 2015-01-24 14:39
sidebar: true
comments: false
sharing: true
footer: true
logo: home-assistant.png
ha_category:
  - Utility
ha_qa_scale: internal
ha_release: pre 0.7
---

The `browser` integration provides a service to open URLs in the default browser on the host machine.

## Configuration

To load this component, add the following lines to your `configuration.yaml`:

```yaml
# Example configuration.yaml entry
browser:
```

#### Service `browser/browse_url`

| Service data attribute | Optional | Description |
| ---------------------- | -------- | ----------- |
| `url`                  |       no | The URL to open.


### Usage

To use this service, choose **Call Service** from the **Developer Tools**. Choose the service *browser/browse_url* from the list of **Available services:** and enter the URL into the **Service Data** field and hit **CALL SERVICE**.

```json
{"url": "http://www.google.com"}
```

This will open the given URL on the host machine.
