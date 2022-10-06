## Using the IN100 with the SHT4X

The SHT4X is a high accuracy, low-power, 16-bit relative humidity and temperature sensor.

It uses a I2C protocol to handle serial communication. This makes it an excellent option
to work with the IN100.

### File Description

#### i2c_device_with_sw0_power_control.cfg

This config files shows the magic commands enetered into the Advanced tab of the
NanoBeacon Config Tool. These commands are how power switching is enabled for the
IN100.

#### i2c_sht4x.cfg

This config file shows the typical I2C communication sequence. It executes all
commands both in warm and cold boot up. The sequence starts by issuing a write
command to the register 0xFD telling the sensor to measure the temperature and
relative humidity. It then waits for the command to process and reads all 6
bits from the processed write command.

#### i2c_sht4x_low_power.cfg

This configuration implements a power saving method, improving performance
over the configuration in i2c_sht4x.cfg. In cold boot up, it follows the
same method in i2c_sht4x.cfg, but issues another write command at the end
of the sequence. In warm boot up, it reads the 6 bits from the write command
at the end of the cold boot up. It then ends by issuing another write command.
This is an improvement because it eliminates the need to use a wait command
while active by letting the write command be processed while the device
is asleep. This only works because the sleeping time of the device
is longer than the command processing time by a few mili-seconds. 

