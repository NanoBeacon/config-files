## Using the MVH4000D with the IN100 NanoBeacon

The MVH4000D is a high accuracy, fast, precision temperature and humidity sensor made by Mems-Vision. It is compatible with the I2C interface and has a very low sleep current of around 10 nA, making it ideal for low power applications with the IN100.

### File Description

#### MVH4000D_temp_humidity_read.cfg

This config file uses the I2C interface of the IN100 to request a no-hold measurement of the temperature and humidity from the MVH4000D. It waits about 1.7 ms for the result to be ready, and then reads the result plus CRC. The time to read is configurable by changing the sensor's resolution. By default, the resolution is 14-bits.

### Sensor Performance

![image](https://github.com/NanoBeacon/config-files/assets/108510134/b21e5607-c6fa-4824-9e28-bbe616afc962)

Figure 1: MVH4000D_temp_humidity_read.cfg Current Consumption During Sleep

In figure 1, the average current consumption is shown to be 748.9 nA. The IN100 typical current consumption is in the range of 650 - 720 nA, and the MVH4000D typically being around 10 nA.

![image](https://github.com/NanoBeacon/config-files/assets/108510134/e49bd774-36a5-40a7-8def-f5564e045d49)

Figure 2: MVH4000D_temp_humidity_read.cfg Current Consumption During Awake and Tx

In figure 2, the average current consumption of the sensor plus the IN100 during an awake state is ~2.9 mA. An awake state includes the IN100 time to prepare to transmit, the sensor reading and I2C transactions, the IN100 transmitting the result, and the time to go back to sleep. 

![image](https://github.com/NanoBeacon/config-files/assets/108510134/75323f4b-d246-41da-a6f4-715837cf8bef)

Figure 3: MVH4000D_temp_humidity_read.cfg Over 10 Minutes Time

In figure 3, the average current consumption over 10 minutes of letting the IN100 advertise periodically on a 5 second interval is about 4.4 uA. 



