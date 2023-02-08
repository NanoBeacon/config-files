## Using the IN100 with the BMA40

The BMA400 is an ultra-low power, 3 axes accelerometer. It features SPI and I2C serial digital communication. With the IN100, only the I2C is compatible. 

### File Description

#### i2c_tap_bma400.cfg

This I2C command sequence configures the accelerometer to send trigger interrupts to the IN100 when a "tap" event is detected. This is a way for the BMA400 to act as a motion detector with the IN100 being able to report the motion when it occurs.

![image](https://user-images.githubusercontent.com/108510134/215597700-f8e85a8e-7eeb-4742-ae54-c82c7ff19c7f.png)

Figure 1: Current between advertising events for i2c_tap_bma400.cfg

![image](https://user-images.githubusercontent.com/108510134/215597926-95fc062b-9aa7-4253-b21e-8fadb11d7b62.png)

Figure 2: Active Current for i2c_tap_bma400.cfg

In the figures above, the passive current consumption is larger than the IN100's usual passive consumption. However, this is during an interrupt event where 6 advertisements are sent out in rapid succession. See the file i2c_tap_bma400.cfg as reference for the operation of the advertising set being sent. The life expectancy of this configuration is very dependent on how often it triggers. If the movement is constant, the consumption will be very high, with the passive current dominating over time. If the motion is periodic, the power consumption drops to 9.457 uA.

![image](https://user-images.githubusercontent.com/108510134/217399548-66aa3644-e5f5-44a1-b8d8-d5d0cb5cab98.png)

Figure 3: Multiple tap events

In Figure 3, above. The broadcasting event is triggered multiple times in short succession. This can result in overlapping advertising events, but also highly time-accurate reporting of the movement. 

![image](https://user-images.githubusercontent.com/108510134/217400086-d89432c4-21d0-4036-8fc2-e35739e855e2.png)

Figure 4: InPlay App Capturing Tap Configuration

In Figure 4, the tap event is captured by the InPlay mobile app for Android and iOS.

#### i2c_bma400.cfg

The I2C sequence used in the config file works by resetting all of the settings by writing to the appropriate registers. It then writes to the sensor data in warm boot and reads it. This is meant for periodic reading of axis data.

As a demonstration of the IN100's energy saving capabilities, the following figures and table drive the IN100 with the BMA400 at 1.8 V with a 10 milisecond advertising interval. This uses the i2c_sgp40_measure_raw_signal.cfg config file.

![image](https://user-images.githubusercontent.com/114425682/194935651-bcda0473-f8e8-4c80-9ee7-10990d41610e.png)

Figure 5: Current while passive for i2c_bma400.cfg

![image](https://user-images.githubusercontent.com/114425682/194935768-053e9a9f-63d2-4040-818e-f5d7ed2895fe.png)

Figure 6: Current while active for i2c_bma400.cfg

![image](https://user-images.githubusercontent.com/114425682/194937167-404772d4-293c-424d-879b-d5d744ff2c78.png)

Table 1:

In table 1 and figures 5 & 6, the survivability of the IN100 with the BMA40 is very impressive, even with a rapid advertising interval of 10 ms.
