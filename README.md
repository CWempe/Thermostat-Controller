## define a Switch

Not all GPIOs work for switches.
successfully tested:

```
GPIO1
GPIO3
GPIO4
GPIO12
```

Execute via Console:
```
SwitchMode1 2
SwitchTopic1 <device>-switch
```

different than the actiual device/topic name

## Used parts

* **Relay**: Panasonic DS2Y-5-DC5V  
   [Datasheet](https://www3.panasonic.biz/ac/e_download/control/relay/signal/catalog/mech_eng_ds2y.pdf)
* **DC-DC Converter**: Mean Well SCW05B-05  
   [Website](https://www.meanwell-web.com/en/product-info/dc-dc-converter/pcb/4-10-w/scw05/product/SCW05B-05)  
   [Datasheet](https://www.meanwell-web.com/en/download_datasheet.php?products_id=SCW05B-05&type=3)
* **Temp sensor**: Dallas DS18B20  
   [Website[(https://www.maximintegrated.com/en/products/analog/sensors-and-sensor-interface/DS18B20.html)
   [Datasheet](https://datasheets.maximintegrated.com/en/ds/DS18B20.pdf)
   