## Using the FXLS8974CF with the IN100

The NXP FXLS8974CF is a low power, 12-bit digital IoT accelerometer manufactured by NXP. It supports I2C serial communciation, offers a wakeup-on-motion feature, and a low and high power mode which makes it a well rounded and felixble option for an accelerometer with the IN100. 

### File Description

#### NXP_FXLS8974CF.cfg

This configuration file configures the acceleromter to default settings, sets it to active mode, then reads the X, Y, and Z axis accelerometer data.

##### Power Consumption

The configuration file NXP_FXLS8974CF is set to wakeup the IN100, execute the I2C commands, and advertise the accelerometer results on a 5 second advertising interval. The timing and other configurations settings both for the IN100 and the NXP accelerometer are configurable to better match a user's use case.

![image](https://github.com/NanoBeacon/config-files/assets/108510134/1ea5894d-046d-420a-864e-41387461698f)

Figure 1: IN100 with FXLS8974CF active current

From Figure 1, the average current consumption over the ~6 ms awake state is about 2.788 mA. Keep in mind that the sensor configuration adds a wait time of about 1 ms to give time for the sensor data to be ready to read.

![image](https://github.com/NanoBeacon/config-files/assets/108510134/90076f80-cee2-4e47-83d9-0873e4ba3ef1)

Figure 2: IN100 with FXLS8974CF passive current

The average current while the IN100 is asleep is around 766 nA. The typical current consumption of the IN100 ranges from about 620 - 720 nA with some chip-to-chip variance. The longer the advertising interval of the IN100, the more this lesser current will dominate the overall power consumption.

![image](https://github.com/NanoBeacon/config-files/assets/108510134/ea6f142e-d706-41d6-a2e3-6f66f600acd5)

Figure 3: IN100 with FXLS8974CF average current over 10 minutes

The average current consumption of this setup is about 4.48 uA. 


