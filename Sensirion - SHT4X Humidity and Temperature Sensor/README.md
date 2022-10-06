## Using the IN100 with the SHT4X

The SHT4X is a high accuracy, low-power, 16-bit relative humidity and temperature sensor.

It uses a I2C protocol to handle serial communication. This makes it an excellent option
to work with the IN100.

### File Description

#### i2c_device_sw0_power_control_settings.cfg

This config files shows the magic commands enetered into the Advanced tab of the
NanoBeacon Config Tool. These commands are how power switching is enabled for the
IN100.

#### i2c_sht4x.cfg

This config file shows the typical I2C communication sequence. It executes all
commands both in warm and cold boot up. The sequence starts by issuing a write
command to the register 0xFD telling the sensor to measure the temperature and
relative humidity. It then waits for the command to process and reads all 6
bits from the processed write command.

![image](https://user-images.githubusercontent.com/114425682/194431751-14c2eeeb-a095-4c62-b2bb-24870082c7f9.png)

Figure 1: Current over advertising event for i2c_sht4x.cfg. 3.3 V at 1 second advertising interval

![image](https://user-images.githubusercontent.com/114425682/194431925-229a2ac2-3bf7-4dc4-a717-f04ec9d1f582.png)

Figure 2: Current over passive time for i2c_sht4x.cfg. 3.3 V at 1 second advertising interval

![image](https://user-images.githubusercontent.com/114425682/194432055-10a458d3-c4b8-4e6f-b09b-8e2a8679d16d.png)

Table 1: Current analysis of I2C sequence in i2c_sht4x.cfg. 3.3 V at 1 second advertising interval

In table 1 and figures 1 & 2, one can see the expected results of using the I2C sequence in i2c_sht4x.cfg. The very small sleep current of 683.3 nA allows the device to be very power efficient over time. The longer the advertising interval, the more dominant the sleep current is over the active current. 

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

![image](https://user-images.githubusercontent.com/114425682/194432683-cf9aa2d4-670d-42bd-a8c0-400b1eeaa7b3.png)

Figure 3: Current over advertising event for i2c_sht4x_low_power.cfg. 3.3 V at 1 second advertising interval

![image](https://user-images.githubusercontent.com/114425682/194433497-6defc99a-c96b-4dc2-bb31-b1d2abc2ca22.png)

Figure 4: Current over passive time for i2c_sht4x_low_power.cfg. 3.3 V at 1 second advertising interval

![image](https://user-images.githubusercontent.com/114425682/194433586-7b49df1e-b4c6-4bed-ab08-04685f547574.png)

Table 2: Current analysis of I2C sequence in i2c_sht4x_low_power.cfg. 3.3 V at 1 second advertising interval

From the results in table 2 and figures 3 & 4, the low power mode is far more energy efficient. The only downside to this method is that it requires the sensor to have a sleeping time greater than the processing time of the write command by a few mili-seconds. Fortunately, this is true for the Sensirion SHT4X.

#### i2c_sht4x_power_switching.cfg

This config file follows the same I2C sequence as i2c_sht4x.cfg, but with additional commands to account for power switching being enabled. To enable power switching, refer to i2c_device_sw0_power_control_settings.cfg. To account for power switching, an additional wait command is added to the beginning of the cold and warm boot up sequences. This allows the device time to wake up from being powered off.

![image](https://user-images.githubusercontent.com/114425682/194437400-0358d29c-22c9-4878-b8d7-32ad45c1c7a3.png)

Figure 5: Current over advertising event for i2c_sht4x_power_switching.cfg. 3.3 V at 1 second advertising interval

![image](https://user-images.githubusercontent.com/114425682/194437439-a788fcd6-b727-4dd2-a6ce-f883b7c4111e.png)

Figure 6: Current over passive time for i2c_sht4x_power_switching.cfg. 3.3 V at 1 second advertising interval

![image](https://user-images.githubusercontent.com/114425682/194437668-64cdfbf2-2c2f-4a4c-8cec-21abb65b08e1.png)

Table 3: Current analysis of I2C sequence in i2c_sht4x_power_switching.cfg. 3.3 V at 1 second advertising interval

As seen in table 3 and figures 5 & 6, the power switching does not at first seem better than previous methods. However, this is over a relatively small interval of 1 second. The longer the interval, the more efficient power switching becomes. Look at section "I2C Method Comparison" for an analysis of the methods in the files discussed in this directory.

### I2C Method Comparison

![image](https://user-images.githubusercontent.com/114425682/194438540-17f53ae9-fb53-42bb-a16a-2ce5514cec11.png)

Table 4: Survival time estimation comparison between I2C methods. 1.8 V at varying advertising intervals. CR2032 coin cell battery used for calculations.

According to Table 4, the method implemented in i2c_sht4x_low_power.cfg has the best performance at most advertising intervals. However, the longer the interval, the more implementing power switching helps the IN100 last longer. Even with the worst performing option, the IN100 can last years powered by a simple CR2032 coincell battery.
