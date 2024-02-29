## Using the BME280 with the IN100

The BME280 is a low energy, high performance pressure, temperature, and humidity sensor.

It has I2C serial communication which allows it to interface with the IN100 through the UART pins.

### File Description

#### i2c_bme280_forced_mode

This config file contains a basic beacon setup that uses a set of I2C commands to configure the BME280 into forced mode with 1x oversampling on all parameters, then it reads from the registers on every warm boot.

Since it is in forced mode, it means the device needs to be set on every wakeup. There is also measurement time needed before data is available to read. The datasheet for the BME280 provides an equation for calculating the measurement time in both forced and normal mode. The config file takes this into account by issuing a wait command between reading the measurements.

Normally forced mode is reserved for use cases with long wait times before measurements, like a weather monitor. Fortunately, we still see good performance at a 1 second advertising interval:

![image](https://user-images.githubusercontent.com/108510134/211436060-cdb6e131-cf15-48e6-ab4b-6af1fe74bc22.png)
Figure 1: Current consumption over 1 advertising event

![image](https://user-images.githubusercontent.com/108510134/211436214-567f3575-8aad-4b92-99ae-57e7c4fd7fc6.png)
Figure 2: Passive current consumption

From Figure 1 and Figure 2 above, the current during the active period is somewhat high, but the passive current remains low at 874.2 nA. Since the passive current is dominant, the overall average current consumption becomes 21.35688 uA.
 
