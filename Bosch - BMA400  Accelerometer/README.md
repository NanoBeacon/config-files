## Using the IN100 with the BMA40

The BMA400 is an ultra-low power, 3 axes accelerometer. It features SPI and I2C serial digital communication. With the IN100, only the I2C is compatible. 

The I2C sequence used in the config file works by resetting all of the settings by writing to the appropriate registers. It then writes to the sensor data in warm boot and reads it.

### Current Analysis

As a demonstration of the IN100's energy saving capabilities, the following figures and table drive the IN100 with the BMA400 at 1.8 V with a 10 milisecond advertising interval. This uses the i2c_sgp40_measure_raw_signal.cfg config file.

![image](https://user-images.githubusercontent.com/114425682/194935651-bcda0473-f8e8-4c80-9ee7-10990d41610e.png)

Figure 1: Current while passive for i2c_bma400.cfg

![image](https://user-images.githubusercontent.com/114425682/194935768-053e9a9f-63d2-4040-818e-f5d7ed2895fe.png)

Figure 2: Current while active for i2c_bma400.cfg

![image](https://user-images.githubusercontent.com/114425682/194937167-404772d4-293c-424d-879b-d5d744ff2c78.png)

Table 1:

In table 1 and figures 1 & 2, the survivability of the IN100 with the BMA40 is very impressive, even with a rapid advertising interval of 10 ms.
