# Introduction

The IMX-060 is a pyroelectric ifrared sensor evaluation board by Murata rated to operate at 3.3 V. Pyroeletric infrared sensors detect the change in IR distributuion in the area it is detecting. In the case of the IMX-060 development board, this chang is reflected on the COUT pin which drives low when it detects AOUT varying.

## Use with the IN100

The IMX-060 setup or on board PIR sensor can be used with the IN100 to trigger an advertisement by sending a falling or rising edge to one of the GPIOs. See the config file MURATA_PIR in this directory for an example. To connect, the IN100 and IMX-060 must share the same VCC and GND, and COUT or AOUT of the IMX-060 should be connected to whichever GPIO is chosen to trigger the advertisement. 

## Power Consumption

When connected to the IN100, the average current consumption while the IN100 is asleep is around 164.95 uA

![image](https://github.com/NanoBeacon/config-files/assets/108510134/8b4d5504-819f-4157-b8be-51faee47e5c1)

While hte IN100 is awake and advertising, the current consumption is about 2.5 mA

![image](https://github.com/NanoBeacon/config-files/assets/108510134/ff4a8db8-83cd-4a3f-8ea4-75ebeff7182d)

Using the example MURATA_PIR.cfg config file where the awake state is triggered, and advertises 6 times per trigger at a 1 second interval, the average current consumption during that triggered burst is around 188 uA

![image](https://github.com/NanoBeacon/config-files/assets/108510134/cf918d56-78a1-4c7d-abca-eec38372121a)


