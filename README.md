# D1 Mini IR Shield

## Description

A simple board for controlling IR devices using an ESP8266 DevKit and ESPHome.

I wanted a way to control my IR devices, such as TVs and air conditioners, without the need for cloud enabled devices or inflexible solutions such as Broadlink Universal Remotes. Moreover, I wanted something that could run ESPHome so that I can customize it as I see fit, and access the multitude of free and public libraries that are available. The solution was to develop my own board: the D1 Mini IR Shield!

## Getting Started with ESPhome

Open ESPhome and create a new device config as follows. You will need to define the following secrets in ESPhome:

- wifi_ssid
- wifi_password
- apikey
- ota_password
- gateway
- subnet

```yaml
substitutions:
  name: "irremote-office"
  room: "Office"
  friendly_name: "IRRemote ${room}"
  project_name: "D1MiniIRRemote.Remote"
  project_version: v1.0rc1

packages:
  remote_package:
    url: https://github.com/s-gordon/D1MiniIRShield
    ref: v1.0rc1
    refresh: 1d
    files:
      - esphome/packages/base.yaml
      # choose one of these as appropriate
      # comment out the others
      - esphome/packages/daikin.yaml
      - esphome/packages/coolix.yaml

# Enable Home Assistant API
api:
  encryption:
    key: !secret apikey

ota:
  password: !secret ota_password

wifi:
  ssid: !secret wifi_ssid
  password: !secret wifi_password
  fast_connect: on
  manual_ip:
    static_ip: !secret irremote_office_ip
    gateway: !secret gateway
    subnet: !secret subnet
```

## Preview

| 3D | 2D |
| -- | -- |
| ![3-dimensional view](/images/PCB.png) | ![2-dimensional view](/images/PCB-2d.png) |

## Credits

Created and maintained by Shane Gordon (@s-gordon).
