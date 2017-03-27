# Thermostat-Controller

This Projekt improves the **Junkers TRQ 21 T** Thermostat with the following features:

* mute the ticking clock  
  By disconnecting the timer clock from the thermostat the clock will stop ticking eventually
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
The Arduino will be connected via WiFi and communiacates via [mqtt](http://mqtt.org/) with your msart home (e.g. [openHAB](http://www.openhab.org/)).  
You can optionally integrate a button to change the current mode without switching to manual mode on the thermostat. But this may require damaging the original case.

## What you need


* **Arduino**: Wemos D1 mini (pro) 
  [Website](https://www.wemos.cc/product/d1-mini-pro.html)
* **Relay**: Panasonic DS2Y-5-DC5V  
  [Datasheet](https://www3.panasonic.biz/ac/e_download/control/relay/signal/catalog/mech_eng_ds2y.pdf)
* **DC-DC Converter**: Mean Well SCW05B-05  
  [Website](https://www.meanwell-web.com/en/product-info/dc-dc-converter/pcb/4-10-w/scw05/product/SCW05B-05)  
  [Datasheet](https://www.meanwell-web.com/en/download_datasheet.php?products_id=SCW05B-05&type=3)
* **Temp sensor**: Dallas DS18B20  
  [Website[(https://www.maximintegrated.com/en/products/analog/sensors-and-sensor-interface/DS18B20.html)
  [Datasheet](https://datasheets.maximintegrated.com/en/ds/DS18B20.pdf)

## Photos

### Thermostat

*tbd*

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




[breakboard]: Fritzing/Thermostat-Controller_bb.png "breakboard view"
[timer_clock]: photos/timer_clock.jpg
[timer_clock_connector]: photos/timer_clocl_connector.jpg