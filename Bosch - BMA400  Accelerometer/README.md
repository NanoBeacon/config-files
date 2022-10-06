## Using the IN100 with the BMA40

The BMA400 is an ultra-low power, 3 axes accelerometer. It features SPI and I2C serial digital communication. With the IN100, only the I2C is compatible. 

The I2C sequence used in the config file works by resetting all of the settings by writing to the appropriate registers. It then writes to the sensor data in warm boot and reads it.
