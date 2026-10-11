
# ESPAC Smart Wifi Thermostat

This piece of software is a thermostat, based on ESPHome, that drive airton AC's throught its available serial port.

"ESPAC" is available under two edition : "Wifi" (standalone webserver) and "Home assistant" with better integration.

It is a substitution to closed source "ACW02" wifi module / ref 409729, commonly sold with airton air conditioner, with my own QOL functionnalities added.

## Global Features

- Should Works with most Airton AC ( at least ref : 409934, 409935, 409936 ) 
- Automation : Automatic double setpoint thermostat
- Care: ESPHome thermostat timers limit commanded transitions; the AC retains its internal regulation.
- Controls : Modes (heat, cold...), flaps position, fan speed, screen on/off, beeper on/off
- Privacy : Lan communication through wifi (web server, home assistant api or both)
- Home Assistant thermostat card (Home Assistant edition) 
- Customizable temperature sensor source (Home Assistant edition)

## Actual state of project

 ![espac unit](/images/header.webp)

```
<proto
 data-measurement="mm"
 height="44"
 width="36"
 alt="9"
 weigth="14" unit="g"
 />
```
> It's small, light and easy to fit under the hood.
 
## Appendix

- [Start Making your own](#start-making-your-own)
  - [What you need](#what-you-need)
  - [Pinout and Soldering](#pinout-and-soldering)
  - [3D model case to print](#3d-model-case-to-print)
- [Home Assistant edition](#home-assistant-edition)
- [Wifi edition](#wifi-edition)
- [Installation and first start](#installation-and-first-start)
- [Missing features to implement](#missing-features-to-implement)
- [Support project](#support-project)
- [Order wifi edition unit](#order-wifi-edition-unit)

## Start making your own

  ### What you need

| Hardware  |  | |
| ------------- | ------------- | ------------- |
| ESP32 D1 mini  | Required | ![d1mini](/images/d1mini.webp)  |
| JST connector - 4 pins - 2.54mm pitch  | Required | ![jst](/images/jst.webp)  |
| 3D Printer  | Optionnal | ![jst](/images/3dprinter.webp)  |

That's it !

Of course, you also need a soldering iron and some tin to complete the job !

 ### Pinout and Soldering

  This is how to solder the jst connector's wires on the d1 mini.
  
  ![Pinout & soldering](/images/soldering.webp)
  
  | Wire | GPIO | Wire color D1 side | wire color AC side |
  | ------------- | ------------- | ------------- | ------------- |
  | 5V | VCC | Black | Red | 
  | Ground | GND | Yellow | Purple |
  | TX | 16 | Red | Blue |
  | RX | 17 | White | Green |

 ### 3D Model case to print
  Small form factor case. Stl file avaiblable [here](/3d_case/espac_case_final.stl)  

  ![case 3d model](/images/case.webp)


## Home Assistant edition
 Home assistant edition has to be flashed on your own with your Home assistant api key. 

  ### Setup

  - Copy the repository source tree: the edition YAML includes packages/core.yaml.
  - Copy home_assistant_edition/secrets.yaml.example to secrets.yaml beside your YAML and fill your own values.
  - Adjust the ESP32 board and device name if needed. Default framework: ESP-IDF.
  - Validate and compile with the ESPHome version pinned in requirements.txt, then flash your device.
  - Add the device to Home Assistant using its native encrypted API.
  - The default sensor is the indoor unit sensor; an optional Home Assistant sensor is described in [maintenance](docs/maintenance.md).
  - No web server is included in the API edition; the personal example combines web and API.

  Startup observes three consistent Airton frames, then waits for an explicit thermostat command. It does not force fan mode. At one frame per minute, this can take up to three minutes.


   ![home assistant thermostat](/images/ha_thermostat.webp)

   > Home Assistant Thermostat Card
     
## Wifi edition

The existing v1.0.0 binary and Wi-Fi edition are unchanged by this source update. No updated Wi-Fi firmware is provided here.

  Wifi edition is web based thermostat, without esphome features, directly connected to your local network through your home wifi.
  You can configure your thermostat with any browser on any device connected to your local network.

  ### Setup
   - Download firmware from release page
   - Flash firmware with usb cable
   - Plug on ac unit ! [see](#installation-and-first-start)
   - Connect to device temporary wifi Access Point, name "ESPAC", password "12345678".
   - Open webpage http://192.168.1.4/, select your wifi network ssid, enter your wifi password, submit !
   - Device will then connect to your network and get an internal ip adressfrom your DHCP.
   - Connect to device with either mobile or desktop browser.

  ![standalone thermostat](/images/standalone_thermostat.webp)
  
  > Standalone controls web interface

## Installation and first start
 
 It's as simple as to plug 4 pin jst connector. Use some double tape to stick it to the main unit body. then :
  - Red LED must light on immediatly. If not, press wifi button on your remote control.
  - Wait until espac take control on device over serial. Blue light should blink at least once. If erverything is ok, the legacy Wi-Fi firmware may enter "fan_only" mode. The updated API edition instead waits for three consistent frames and an explicit command (up to about three minutes).

![plug jst connector](/images/plug.webp)
![plug jst connector 2](/images/plug2.webp)

> [!WARNING]
> Main voltage hazard. Please, security first ! if you dont know how to deal with main voltage and breaker, call an electrician.

## Missing features to implement
  - Eco mode
  - Timer
  - Humidity percent setting for "huimidity based" mode. (should be default 60% in actual state) 
  - Automatic profile switching ( ie day / night )

## Support Project

if you want to support hard work, you can [buy me a beer](https://buymeacoffee.com/dohmotik)

Thanks for your support !

## Order "wifi edition" unit

  You can order a "wifi edition" unit from [buymeacoffee](https://buymeacoffee.com/dohmotik/e/436984)
  
  All units are shipped "ready to plug" flashed with "wifi edition" firmware, also available on release page. 
  
  It can be flash with any edition you want though its usb-c port.

  Thanks.
  
  

## Source maintenance and license

The API edition and personal example share `packages/core.yaml`; there is no duplicated UART driver or thermostat logic. The existing Wi-Fi binary is outside this refactor. See [maintenance and validation](docs/maintenance.md) and [changelog](CHANGELOG.md).

The updated ESPAC source is licensed under **GPL-3.0-only**; see [LICENSE](LICENSE) and [NOTICE](NOTICE). Derivative source and firmware projects, including Jeedom adaptations, are welcome under this license. Preserve attribution and the relevant source/license notices.
