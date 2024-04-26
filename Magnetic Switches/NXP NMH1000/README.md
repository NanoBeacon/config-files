## Using the NMH1000 with the IN100

The NXP NMH1000 is a hall effect magnetic field switch produced by NXP. It is compatible with the I2C interface to configure the switch and read back the sensor data. This makes it a good choice to use with the IN100 for magnetic switch and magnetometer applications. 

### File Description

#### NXP_NMH1000.cfg

This configuration file configures the magnetic switch to automatic mode, then reads the 4 bytes of Hall sensor data.

##### Power Consumption

![image](https://github.com/NanoBeacon/config-files/assets/108510134/e5008943-4cf4-4b83-8ab2-71b7207e7cc6)

Figure 1: IN100 with NMH1000 active current

From Figure 1, the average current consumption over the 5.54 ms awake state is about 2.893 mA.

![image](https://github.com/NanoBeacon/config-files/assets/108510134/85d171bb-5984-434d-a3ea-3490541695a6)

Figure 2: IN100 with NMH1000 passive current

The average current while the IN100 is asleep is around 776 nA. The typical current consumption of the IN100 ranges from about 620 - 720 nA with some chip-to-chip variance. The longer the advertising interval of the IN100, the more this lesser current will dominate the overall power consumption.

![image](https://github.com/NanoBeacon/config-files/assets/108510134/668d63ca-b835-43ae-bb8e-b309419e2902)

Figure 3: IN100 with NMH100 average current over 10 minutes

The average current consumption of this setup is about 4.229 uA. 


