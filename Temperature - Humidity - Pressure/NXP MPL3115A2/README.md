## Using the MPL311A2 with the IN100

The NXP MPL311A2 is a compact, piezoresistive, absolute pressure sensor manufactured by NXP. It supports I2C serial communciation which makes it a good choice for pressure and temperature sensing applications with the IN100 BLE beacon. 

### File Description

#### NXP_MPL311A2.cfg

This configuration file configures the pressure sensor to raise data ready flags for the pressure and temperature sensor. It then requests for pressure data, waits for the required ~6 ms for the data to be ready, then reads 4 bytes of pressure data. 

##### Power Consumption

The configuration file NXP_MPL311A2 is set to wakeup the IN100, execute the I2C commands, and advertise the pressure results on a 5 second advertising interval. The timing and other configurations settings both for the IN100 and the NXP pressure sensor are configurable to better match a user's use case.

![image](https://github.com/NanoBeacon/config-files/assets/108510134/636f7aa2-62a2-40b2-bcce-69598237df03)

Figure 1: IN100 with MPL311A2 active current

From Figure 1, the average current consumption over the ~11.96 ms awake state is about 2.6 mA. Keep in mind that the sensor configuration adds a wait time of about 6 ms to give time for the sensor data to be ready to read. To optimize power consumption for this sensor, it is recommended to have less frequent advertising so that the low sleep current of the IN100 will dominate the overall current consumption. Also, turning off the sensor during sleep using the IN100's power switches will further reduce current consumption.

![image](https://github.com/NanoBeacon/config-files/assets/108510134/43796311-17ca-4bcf-beb0-a9dd7103e519)

Figure 2: IN100 with MPL311A2 passive current

The average current while the IN100 is asleep is around 725.3 nA. The typical current consumption of the IN100 ranges from about 620 - 720 nA with some chip-to-chip variance. The longer the advertising interval of the IN100, the more this lesser current will dominate the overall current consumption.

![image](https://github.com/NanoBeacon/config-files/assets/108510134/7e3cdd28-4302-4504-93ef-c5f9c72be4c2)

Figure 3: IN100 with MPL311A2F average current over 10 minutes

The average current consumption of this setup is about 7 uA. 
