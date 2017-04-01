# Thermostat-Controller

This Projekt improves the **Junkers TRQ 21 T** Thermostat with the following features:

* mute the ticking clock  
  By disconnecting the timer clock from the thermostat the clock will stop ticking eventually  
  (might take a few weeks before the battery dies)
* support weekends  
  The default timer clock does not differenciate between work days and weekends  
  By controlling the thermostat with your smart home, you can define every timer rule you want
* support presents detection and geolocation  
  If your smart home supports it, your thermastat will do too now
* support disableing when windows ar eopen  
  If your smart home supports it, ...

Best of all: Your thermostat will not be managed and you can still change to day and night mode manually like before.

## How does it work

You will replace the internal timer clock with an Arduino (esp8266) to switch between day and night mode.  
The Arduino will be connected via WiFi and communiacates via [mqtt](http://mqtt.org/) with your smart home (e.g. [openHAB](http://www.openhab.org/)).  
You can optionally integrate a button to change the current mode without switching to manual mode on the thermostat. But this may require damaging the original case if want it to look good.

## What you need


* **Arduino**: Wemos D1 mini (pro)  
  [Website](https://www.wemos.cc/product/d1-mini-pro.html)  
* **Relay**: Panasonic DS2Y-5-DC5V  
  [Datasheet](https://www3.panasonic.biz/ac/e_download/control/relay/signal/catalog/mech_eng_ds2y.pdf)
* **DC-DC Converter**: Mean Well SCW05B-05  
  [Website](https://www.meanwell-web.com/en/product-info/dc-dc-converter/pcb/4-10-w/scw05/product/SCW05B-05)  
  [Datasheet](https://www.meanwell-web.com/en/download_datasheet.php?products_id=SCW05B-05&type=3)
* **Temp sensor**: Dallas DS18B20  
  [Website](https://www.maximintegrated.com/en/products/analog/sensors-and-sensor-interface/DS18B20.html)  
  [Datasheet](https://datasheets.maximintegrated.com/en/ds/DS18B20.pdf)  
* **Wire-to-Board connector**  
 *  molex SPOX™ Wire-to-Board Crimp Housing  
  2.50mm Pitch SPOX™ Wire-to-Board Crimp Housing, Friction Lock, 5 Circuits  
  [Website](http://www.molex.com/molex/products/datasheet.jsp?part=active/0050375053_CRIMP_HOUSINGS.xml&channel=Products&Lang=en-US)  
  [Datasheet](http://www.molex.com/webdocs/datasheets/pdf/en-us/0050375053_CRIMP_HOUSINGS.pdf)  
 * molex SPOX™ BMI Connector System (5x)  
  2.50mm Pitch SPOX™ Crimp Terminal, 22-28 AWG, Bag  
  [Website](http://www.molex.com/molex/products/datasheet.jsp?part=active/0008701040_CRIMP_TERMINALS.xml&channel=Products&Lang=en-US)  
  [Datasheet](http://www.molex.com/webdocs/datasheets/pdf/en-us/0008701040_CRIMP_TERMINALS.pdf)
  
## Photos

### Thermostat

![thermostat]

### timer clock

![timer_clock]

![timer_clock_connector]

  
## Circiut Diagram
  
![breakboard]
  
## define a Switch

Not all GPIOs work for switches.
successfully tested:

```
GPIO1
GPIO3
GPIO4
GPIO12
```

Execute via Web-Console:
```
SwitchMode1 2
SwitchTopic1 <device>-switch
```

different than the actiual device/topic name


## configure openhab

You can find some example configuration files in the openhab folder.

You basicly need an item for the relay and an item for the temperature sensor.
To make use of some smart automation rules and manual override you might want to configure some virtual items.
If you have any windows or door contacts connected to your smart home you also might want to turn the thermostat off while you let some fresh air in.

You can also use a transformation file to display more accurate terms than "ON" and "OFF" for day and night mode.

Finally I renamed some openhab2 classic icons to thermostat*.png/svg.

![openhab_screenshot]

[breakboard]: Fritzing/Thermostat-Controller_bb.png "breakboard view"
[thermostat]: photos/Junkers_TRQ21_Thermostat.jpg
[timer_clock]: photos/timer_clock.jpg
[timer_clock_connector]: photos/timer_clock_connector.jpg
[openhab_screenshot]: photos/openhab_screenshot_thermostat.png