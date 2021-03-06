# Thermostat-Controller

This Project improves the **Junkers TRQ 21 T** Thermostat with the following features:

* mute the ticking clock  
  By disconnecting the timer clock from the thermostat the clock will stop ticking eventually  
  (might take a few weeks before the battery dies)
* support weekends  
  The default timer clock does not differentiate between work days and weekends  
  By controlling the thermostat with your smart home, you can define every timer rule you want
* support presence detection and geo location  
  If your smart home supports it, your thermostat will do too now
* support disabling when windows are open  
  If your smart home supports it, ...

Best of all: Your thermostat will not be managed and you can still change to day and night mode manually like before.

## How does it work

You will replace the internal timer clock with an Arduino (esp8266) to switch between day and night mode.  
The Arduino will be connected via WiFi and communicates via [mqtt](http://mqtt.org/) with your smart home (e.g. [openHAB](http://www.openhab.org/)).  
You can optionally integrate a button to change the current mode without switching to manual mode on the thermostat. But this may require damaging the original case if want it to look good.

## What you need

Beside some standard components, you need:  

* **Arduino**: Wemos D1 mini (pro)  
  [Website](https://www.wemos.cc/product/d1-mini-pro.html)  
* **Relay**: Panasonic DS2Y-5-DC5V  
  [Datasheet](https://www3.panasonic.biz/ac/e_download/control/relay/signal/catalog/mech_eng_ds2y.pdf)
* **DC-DC Converter**: Recom R-78B5.0-1.0L  
  [Website](https://www.recom-power.com/de/emea/home.html)  
  [Datasheet]([https://www.recom-power.com/pdf/Innoline/R-78Bxx-1.0_L.pdf)
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
  
![ext_comopnents]

![breakboard]

![pcb]

## Photos

You can find more photos of the finished project in the photos directory.

## configure Arduino (Sonoff-Tasmota)

Open the web interface of your controller.  
Click `Configuration` and then `Configure Mode`. Select the `Module Type`.  
Here : "18 Wemos D1 mini".

Define the Sensors for the GPIOs.

* GPIO12: "17 Relay1"
* GPIO13: "09 Switch1" (optional, if you add a switch to the project)
* GPIO14: "04 DS18x20"

Click `Save`

If you added a switch to your project, execute the following commands in the `Console` in the web interface.

```
SwitchMode1 2
SwitchTopic1 wemos01-switch
```

See [this page](https://github.com/arendst/Sonoff-Tasmota/wiki/Understanding-SwitchMode-and-SwitchTopic) for more details.

## configure openhab

You can find some example configuration files in the openhab folder.

You basically need an item for the relay and an item for the temperature sensor.
To make use of some smart automation rules and manual override you might want to configure some virtual items.
If you have any windows or door contacts connected to your smart home you also might want to turn the thermostat off while you let some fresh air in.

You can also use a transformation file to display more accurate terms than "ON" and "OFF" for day and night mode.

Finally I renamed some openhab2 classic icons to thermostat*.png/svg. (see /openhab/icons)

### Example (openHAB)
![openhab_screenshot]  
The current mode is "Nachtabsenkung" (night mode)
The target mode is set to "Normalbetrieb" (day mode).  
The override mode is set to "automatic" (this means no override).  
The window is open.  

While the current mode should be "day mode", because of the target mode, it actually is "night mode", because the window is open.
Once the window closes the mode changes to "day mode" (target mode).

[ext_comopnents]: Fritzing/Thermostat-Controller_external_components_bb.png "external components"
[breakboard]: Fritzing/Thermostat-Controller_bb.png "breakboard view"
[pcb]: Fritzing/Thermostat-Controller_pcb.png "pcb view"
[thermostat]: photos/Junkers_TRQ21_Thermostat.jpg
[timer_clock]: photos/timer_clock.jpg
[timer_clock_connector]: photos/timer_clock_connector.jpg
[openhab_screenshot]: photos/openhab_screenshot_thermostat.png