---
title: Elecrow CrowPanel 2.1" Rotary ESPHome Media Player
description: Install ESPHome Media Player on the Elecrow CrowPanel 2.1-inch round rotary display, a knob-controlled Home Assistant music controller.
---

# Elecrow CrowPanel 2.1" Rotary (round)

2.1" (480×480) round IPS touchscreen with a clicking rotary knob and an ESP32-S3. The layout is adapted for the round glass: track info is centred, play/pause sits at the bottom centre, and the progress bar is lifted clear of the bezel.

This device is added in the [gurul/esphome-media-player](https://github.com/gurul/esphome-media-player) fork, so its packages are served from that fork.

## Where to buy

<PurchaseLinks device="crowpanel-21-rotary" />

## Controls

| Input | Action |
| --- | --- |
| Turn the knob | Volume, 2% per click. The volume dial opens while you turn. |
| Press the knob | Play / pause |
| Swipe left / right | Next / previous track |
| Swipe down / up | Open / close the volume and speakers panel |
| Tap | Show or hide the track info |
| Hold 5 seconds | Turn the screen off |

When the screen is dimmed or off, the first turn or press only wakes it.

In a speaker group, turning the knob changes the volume of the selected speaker.

## Apple Music

The dashboard follows any Home Assistant `media_player` entity. To control Apple Music, choose the entity that plays it. That is usually an Apple TV or HomePod added through Home Assistant's Apple TV integration. Artwork, track info, volume and play/pause come from that entity.

## Install

<InstallButton device="crowpanel-21-rotary" />

::: warning
The browser installer only offers firmware that has been published as a release. This fork does not publish releases yet, so install through the ESPHome dashboard instead. See [ESPHome Config](/advanced/esphome-config). This device uses the `devices/elecrow-crowpanel-esp32-s3-21-rotary/packages.yaml` package.
:::

To flash for the first time, connect the board over USB-C. If the flash fails with `No serial data received`, hold **BOOT**, tap **RESET**, then release **BOOT** to force download mode.

## Knob options

Set these in your ESPHome YAML under `substitutions`:

| Substitution | Default | Meaning |
| --- | --- | --- |
| `knob_volume_step` | `"2"` | Volume change per knob click, in percent |
| `knob_direction` | `"1"` | Set to `"-1"` if turning clockwise lowers the volume |

## Rotation

Use **Screen Rotation** in the device web settings page or Home Assistant to rotate the display and touch input together. The supported values are `0`, `90`, `180`, and `270`.

## First boot checklist

This configuration compiles, but it has not yet been tested on this board. Check these on first boot:

1. **Colours.** Album art should look natural. If reds and blues are swapped, swap the `red` and `blue` pin lists in `device/device.yaml`.
2. **Picture.** If the image shears or shows bands, lower `pclk_frequency` in `device/device.yaml`. If it flickers, raise it.
3. **Touch.** A tap should land where you touched.
4. **Knob.** Clockwise should raise the volume. If it lowers it, set `knob_direction: "-1"`.
5. **Press.** One press should toggle play/pause.

## Known limitations

- The web settings page is served from the upstream project, which does not know this device's profile. Settings still load and save. The one difference: the S3 "pause the display while settings are open" optimisation does not run.
- Firmware update checks point at the upstream release feed, which has no build for this device. The update entity stays empty.
