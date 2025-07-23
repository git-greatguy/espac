
# ESPAC Smart Wifi Thermostat

This piece of software is a thermostat, based on esphome / arduino, that drive airton AC's throught its available serial port.

"ESPAC" is available under two edition : "Wifi" (standalone webserver) and "Home assistant" with better integration.

It is a substitution to closed source "ACW02" wifi module / ref 409729, commonly sold with airton air conditioner, with my own QOL functionnalities added.

## Global Features

- Should Works with most Airton AC ( at least ref : 409934, 409935, 409936 ) 
- Automation : Automatic double setpoint thermostat
- Care : Timer protection - ensure compressor minimal runtime when kicked in.
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
It's small, light and easy to fit under the hood.
 
## Appendix

- [Start making your own](#start-make-your-own)
- [Pinout & Soldering](#pinout-soldering)
- [3D Model case to print](#3d-model-case-to-print)
- [Flash Procedure](#flash-procedure)
- [How to install](#how-to-install)
- [Missing features and improvement](#missing-features-and-improvement)
- [Support project](#support-project)
- [Order an ESPAC wifi unit](#order-an-espac-wifi-unit)
- [](#) 

## Start making your own
  ### What you need : 

| Hardware  |  | |
| ------------- | ------------- | ------------- |
| ESP32 D1 mini  | Required | ![d1mini](/images/d1mini.webp)  |
| JST connector - 4 pins - 2.54mm pitch  | Required | ![jst](/images/jst.webp)  |
| 3D Printer  | Optionnal | ![jst](/images/3dprinter.webp)  |

That's it !

Of course, you also need a soldering iron and some tin to complete the job !

 ### Pinout & Soldering

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


## Home Assistant edition :
 Home assistant edition has to be flashed on your own with your Home assistant api key. 

  ### Setup
   - Configure a new esphome device with your api, ota, wifi informations.
   - Add yaml configuration avaible [here](/home_assistant_edition/espac_configuration.yaml) to your device configuration.
   - Optional configuraion for an external temperature sensor. Please check yaml configuration.  
   - Compile and Flash firmware with usb cable.
   - Plug device on indoor AC unit. [see](#how to install)
   - Device should be available in Home Assistant after soime time, then add it to you devices. 
   - Add a new card to your Home Assistant dashboard. Example thermostat configuration card is available [here](/home_assistant_edition/thermostat_card).

 ### Home Assistant thermostat :

   ![home assistant thermostat](/images/ha_thermostat.webp)
     
## Wifi edition :

  Wifi edition is web based thermostat, without esphome feature, directly connected to your local network through your home wifi hotspot.
  You can configure your thermostat with any browser on any device connected to your local network.

  ### Setup
   - Download firmware from release page
   - Flash firmware with usb cable
   - Plug on ac unit ! [see](#how to install)
   - Connect to device temporary wifi Access Point, name "ESPAC", password "12345678".
   - Open webpage http://192.168.1.4/, select your wifi network ssid, enter your wifi password, submit !
   - Device will then connect to your network and get an internal ip adressfrom your DHCP.
   - Connect to device with either mobile or desktop browser.

#### Standalone controls web interface :

![standalone thermostat](/images/standalone_thermostat.webp)

## How to install
  - It's as simple as to plug 4 pin jst connector on your airton compatible ac unit. Red LED must light instantly. if not, press wifi button on your remote control.  
  - Wait until espac take control over unit. Blue light should blink at least once, wifi led whould light on AC unit, "fan_only" mode would kick in. ( can take up to 1 min )
  - Connect to configuration webpage (ip give by DHCP) and set your parameters ! ex : https://192.168.0.24

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
  
  All units are shipped "ready to plug" flashedf with wifi edition firmware available on our release page. 
  
  It can be flash, as you wish, with Home Assistant edition though its usb-c port.

  Thanks.
  
  
