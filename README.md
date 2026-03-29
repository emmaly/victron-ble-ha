# victron-ble-ha

Custom Home Assistant component that patches the built-in `victron_ble` integration to support connectable Victron devices (AC chargers like the Blue Smart IP22, Phoenix Smart, etc.).

## The Problem

The built-in HA Victron BLE integration only discovers devices that advertise as `connectable: false`. Many Victron chargers advertise as `connectable: true`, so HA's Bluetooth discovery framework never passes their advertisements to the integration. The device shows up in HA's generic BLE list but the Victron integration says "no unconfigured devices."

See [home-assistant/core#157417](https://github.com/home-assistant/core/issues/157417).

## The Fix

This custom component is an exact copy of the upstream `victron_ble` integration with one change: `manifest.json` adds a second Bluetooth matcher that accepts `connectable: true` devices.

## Installation

Copy the `custom_components/victron_ble/` directory into your Home Assistant config directory:

```
<ha-config>/custom_components/victron_ble/
```

Restart Home Assistant. The custom component overrides the built-in integration. Your AC charger should now appear in the Victron BLE integration setup flow.

## Removal

When the upstream fix lands in a future HA release, delete the `custom_components/victron_ble/` directory and restart. The built-in integration will take over with the same entity IDs and device configuration.

## Source

All files except `manifest.json` are unmodified from [home-assistant/core](https://github.com/home-assistant/core/tree/dev/homeassistant/components/victron_ble) (`dev` branch, retrieved 2026-03-29).
