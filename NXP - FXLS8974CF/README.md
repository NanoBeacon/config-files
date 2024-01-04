## Using the IN100 with the FXLS8974CF

The FXLS8974CF is a 3-axis MEMs accelerometer by NXP. It is designed for industrial and medical IOT applications that require ultra low-power wakeup on montion.

### File Description

#### NXP_FXLS8974CF.cfg

The I2C command sequence on this config file activates the FXLS8974CF with default settings and periodically reads the X, Y, and Z axis settings on wakeup. When operating during sleep, the accelerometer and IN100 together result in a passive current consumption of about 188 uA:

![image](https://github.com/NanoBeacon/config-files/assets/108510134/78112926-c12f-4ebe-837d-62c5a2999e5c)
Figure 1: NXP_FXLS8974CF Passive Current Consumption

During an active transmission event, the current consumption on average is 3.2 mA:

![image](https://github.com/NanoBeacon/config-files/assets/108510134/8fb53f71-435e-4638-be55-aef6e02dbdc5)
Figure 2: NXP_FXLS8974CF Active Current Consumption

This power consumption allows for a low power approach for motion detection. This simple use case can be iterated upon for more complex configurations of the NXP FXLS8974CF such as making it activate an interrupt pin in response to motion. 



