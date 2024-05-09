## Using the ENS210 Sensor with the IN100

The ScioSense ENS210 is a humidity and high accuracy temperature sensor. It is compatible with the I2C serial interface, making it a good choice for the IN100.

### File Description

#### ENS210_Example.cfg

This config file sets up the ENS210 sensor to read the temperature and humidity data. It starts by waiting for the sensor to start up from an off state with a delay. It then reads the data by writing to register 0x30, 
and then sets up the next measurement to be processed during sleep by calling registers 0x22 and 0x03. This improves the power consumption of the system by allowing the IN100 to be asleep while the sensor processes the next measurement.
