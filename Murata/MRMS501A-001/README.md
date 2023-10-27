# Introduction

The MRMS501A-001 is a magnetic switch made by Murata. It is rated for 1.6 - 3.5 V making it ideal for the the IN100 which has a range of 1.1 - 3.6 V. 

## Use with the IN100

The MRMS501A-001 can be used for magnetic activation from sleep by sending a falling edge onto one of the GPIOs. When affected by the appropriately strong magnetic field, the VOUT will be low (0.3 V). To connect to the IN100, it must share the same VCC (or powered by IN100 through a GPIO or switch) and GND as well as have its VOUT connected to one of the GPIOs for magnetic activation. 

This setup is demonstrated with the MURATA_MS201AE.cfg config file in this directory.

## Power Consumption

When in the sleep state where the IN100 is not advertising, the current consumption is around 650 nA:

![image](https://github.com/NanoBeacon/config-files/assets/108510134/b6cd8353-2a82-412b-90a0-c94e88706f8b)

When awake and advertising from the MRMS501A-001 VOUT going low to activate, the average current consumption of the awake state is 2.5 mA:

![image](https://github.com/NanoBeacon/config-files/assets/108510134/831f552b-33b1-4ad0-a8e4-cdb5839edd51)

When advertising 6 times in a row at a 1 second interval as in the MURATA_MS201AE.cfg config file, the average current consumption during this event is 13.56 uA:

![image](https://github.com/NanoBeacon/config-files/assets/108510134/e3ad2474-aab9-41d8-9cca-ab657d90b066)

*Note: Current consumption will change based on settings such as Tx power level and advertising interval. 



