# musicKnob

A round music knob for Home Assistant. Turn it for volume, press it to play or pause, and see the album art on a 2.1" round screen.

It runs on the [Elecrow CrowPanel 2.1" rotary display](https://www.elecrow.com/crowpanel-2-1inch-hmi-esp32-rotary-display-480-480-ips-round-touch-knob-screen.html), the same board as [spotKnob](https://github.com/gurul/spotify-knob). Where spotKnob talks to Spotify directly, musicKnob controls any Home Assistant `media_player`, so it works with Apple Music too.

musicKnob is a fork of [ESPHome Media Player](https://github.com/jtenniswood/esphome-media-player) by James Tenniswood. The fork adds the CrowPanel board, knob controls and a layout for the round screen.

> [!NOTE]
> The firmware compiles, but it has not been tested on the board yet. Check the [first boot checklist](docs/devices/crowpanel-21-rotary.md#first-boot-checklist) the first time you flash it.

## Controls

| Input | Action |
| --- | --- |
| Turn the knob | Volume, 2% per click |
| Press the knob | Play / pause |
| Swipe left / right | Next / previous track |
| Swipe down / up | Open / close the volume and speakers panel |
| Tap | Show or hide the track info |
| Hold 5 seconds | Turn the screen off |

When the screen is dimmed or off, the first turn or press only wakes it.

## Hardware

| Part | Detail |
| --- | --- |
| Board | Elecrow CrowPanel 2.1" HMI ESP32 Rotary Display |
| Chip | ESP32-S3, 16 MB flash, 8 MB PSRAM |
| Screen | 480 x 480 round IPS (ST7701S) with CST826 touch |
| Knob | Rotary encoder with push switch |

Pin assignments are the ones spotKnob verified on this board. The details are in [`devices/elecrow-crowpanel-esp32-s3-21-rotary/device/device.yaml`](devices/elecrow-crowpanel-esp32-s3-21-rotary/device/device.yaml).

## Apple Music

musicKnob follows one Home Assistant `media_player` entity. For Apple Music, pick the entity that plays it. This is usually an Apple TV or HomePod added through Home Assistant's [Apple TV integration](https://www.home-assistant.io/integrations/apple_tv/). Artwork, track info, volume and play/pause all come from that entity.

## Install

You need Home Assistant with the ESPHome add-on, and a USB-C data cable for the first flash.

1. In the ESPHome dashboard, create a new device and paste this config:

   ```yaml
   substitutions:
     name: "music-knob"
     friendly_name: "Music Knob"

   wifi:
     ssid: !secret wifi_ssid
     password: !secret wifi_password

   packages:
     music_dashboard:
       url: https://github.com/gurul/music-knob
       files: [devices/elecrow-crowpanel-esp32-s3-21-rotary/packages.yaml]
       ref: main
       refresh: 1s
   ```

2. Connect the board over USB-C and install. If the flash fails with `No serial data received`, hold **BOOT**, tap **RESET**, then release **BOOT**.
3. Adopt the device in Home Assistant, then open its web page and choose the media player to control.

After the first flash, updates install over Wi-Fi from the ESPHome dashboard.

### Options

Set these under `substitutions`:

| Substitution | Default | Meaning |
| --- | --- | --- |
| `knob_volume_step` | `"2"` | Volume change per knob click, in percent |
| `knob_direction` | `"1"` | Set to `"-1"` if clockwise lowers the volume |
| `display_rotation` | `"0"` | Screen rotation: `0`, `90`, `180` or `270` |

## More

- [Device page](docs/devices/crowpanel-21-rotary.md): the first boot checklist and known limitations.
- [Upstream documentation](https://jtenniswood.github.io/esphome-media-player/): the web settings page, speaker grouping, screen saver and troubleshooting. These features work the same way on musicKnob.

## Other screens

This fork still builds every screen the upstream project supports:

<!-- generated:supported-screens:start -->
| Device | Size | Buy |
|--------|------|-----|
| [Guition ESP32-S3 4848S040](https://jtenniswood.github.io/esphome-media-player/devices/esp32-s3-4848s040) | 4 in (480 x 480) | [AliExpress](https://s.click.aliexpress.com/e/_c3sIhvBv) |
| [ESP32-P4 86 Panel](https://jtenniswood.github.io/esphome-media-player/devices/esp32-p4-86-panel) | 4 in (720 x 720) | [Waveshare](https://www.waveshare.com/esp32-p4-wifi6-touch-lcd-4b.htm) |
| [Guition ESP32-P4 JC4880P443](https://jtenniswood.github.io/esphome-media-player/devices/esp32-p4-jc4880p443) | 4.3 in (800 x 480) | [AliExpress](https://www.aliexpress.com/item/1005009618259341.html) |
| [Guition ESP32-P4 JC1060P470](https://jtenniswood.github.io/esphome-media-player/devices/esp32-p4-jc1060p470) | 7 in (1024 x 600) | [AliExpress](https://s.click.aliexpress.com/e/_c4LLo3rH) |
| [Guition ESP32-P4 JC8012P4A1](https://jtenniswood.github.io/esphome-media-player/devices/esp32-p4-jc8012p4a1) | 10.1 in (1280 x 800) | [AliExpress](https://s.click.aliexpress.com/e/_c3wsnU43) |
| [Elecrow CrowPanel 2.1" Rotary](https://github.com/gurul/music-knob/blob/main/docs/devices/crowpanel-21-rotary.md) | 2.1 in (480 x 480) | [Elecrow](https://www.elecrow.com/crowpanel-2-1inch-hmi-esp32-rotary-display-480-480-ips-round-touch-knob-screen.html) |
<!-- generated:supported-screens:end -->

## License

[PolyForm Noncommercial License 1.0.0](LICENSE.md), inherited from the upstream project. You can use, share and modify it for non-commercial purposes. The required notice for the original work is at the top of the license file.
