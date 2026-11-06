---
title: inkVision
description: Instructions on how to integrate the inkVision Atmos Smart Clock into Home Assistant.
ha_categories:
  - sensors.air_quality
  - sensors.temperature_humidity
ha_release: 2026.12
ha_iot_class: Local Push
ha_config_flow: true
ha_codeowners:
  - '@11ado33'
ha_domain: inkvision
ha_zeroconf: true
ha_platforms:
  - sensor
ha_integration_type: device
ha_quality_scale: bronze
---

The **inkVision** {% term integration %} connects the [inkVision](https://inkvision.eu) Atmos Smart Clock to Home Assistant. The Atmos Smart Clock is a desk clock with an LED matrix display and an environment sensor that measures temperature, humidity, air pressure, and indoor air quality.

Home Assistant talks to the clock directly on your local network. The clock pushes its readings to Home Assistant, and no cloud account is needed.

## Use cases

- Show the temperature and humidity of a room on your dashboard.
- Get a notification to open a window when the indoor air quality gets worse.
- Turn on a fan or ventilation when the CO₂ equivalent rises.

## Supported devices

- Atmos Smart Clock

## Prerequisites

- The clock is set up and connected to your Wi-Fi network, for example with the HomeBrainz Hub app.
- Home Assistant and the clock are on the same network.

{% include integrations/config_flow.md %}

Home Assistant usually discovers the clock on your network by itself and shows it as **Discovered**. To add a clock that was not discovered, enter its address.

{% configuration_basic %}
Host:
  description: "The IP address or hostname of the clock, for example `192.168.1.50`. You can find it in your router's list of connected devices."
{% endconfiguration_basic %}

## Supported functionality

### Sensors

- **Temperature**
- **Humidity**
- **Atmospheric pressure**
- **Indoor air quality**: The indoor air quality index of the Bosch BME680 sensor, from 0 (clean air) to 500 (heavily polluted air).
- **CO₂ equivalent**: An estimate of the CO₂ concentration, calculated from the volatile organic compounds that the sensor measures.
- **Breath VOC**: An estimate of the concentration of volatile organic compounds in breath.
- **Gas resistance**: The raw reading of the gas sensor. Disabled by default.
- **Signal strength**: The Wi-Fi signal strength of the clock. Disabled by default.

After the clock starts, its environment sensor calibrates itself, which can take some hours. Until then, the air quality values are less accurate.

## Data updates

The clock sends new readings over a WebSocket connection every few seconds. If the connection drops, Home Assistant reconnects to it and, until it does, checks the clock every 5 minutes.

## Removing the integration

This integration follows standard integration removal. No extra steps are required. The clock keeps working on its own and keeps its settings.

{% include integrations/remove_device_service.md %}
