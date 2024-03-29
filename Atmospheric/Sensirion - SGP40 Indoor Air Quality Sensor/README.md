## Using the IN100 with the SGP40

The SGP40 is a digital gas sensor designed for easy integration into air purifier 
or demand controlled ventilation systems.

### example_i2c_sgp40_measure_raw_signal.cfg and i2c_sgp40_measure_raw_signal.cfg

#### i2c_sgp40_measure_raw_signal.cfg

In order to get the SGP40 working with the IN100, the i2c is configured to write
to a set of internal registers. Referring to the [SGP40 datasheet](https://docs.rs-online.com/1956/A700000007055193.pdf),
the set of commands "starts/continues the VOC measurement mode, 
leaves humidity compensation disabled by sending the default values 
and returns the measured raw signal SRAW as 2 bytes (+ 1 CRC byte)."

What this means is that the IN100 will measure the raw signal data in order to
advertise. After writing those commands, the sequence reads the 3 bytes of data
and then issues the same write commmand in warm boot.

The data read is the following:

I2C read 3 bytes: data[15:8] data[7:0] CRC[7:0]

#### example_i2c_sgp40_measure_raw_signal.cfg

This configuration file configures the IN100 to communicate with
the SGP40 with the i2c protocal as described above. It then continuously
advertises the data gathered from the sensor.

In order to use these files, the user will need

 1. hardware: IN100 GPIO5 as I2C SCL and IN100 GPIO4 as I2C SDA
    
 2. SGP40 sensor

 3. IN100 Programmer board and development board.

 4. NanoBeacon Config Tool to load the config file onto the NanoBeacon.
 
### example_i2c_sgp40_measure_raw_with_sw0_power.cfg and i2c_sgp40_measure_raw_signal_with_sw0_power.cfg

#### i2c_sgp40_measure_raw_signal_with_sw0_power.cfg

Like in i2c_sgp40_measure_raw_signal.cfg, this file uses a similar sequence,
with the difference being that all commands are executed in both warm and
cold boot up. This is done since it uses power switching through register
commands to save power over longer advertising intervals. The longer the
advertising interval, the more efficient it is to use power switching
as a method for i2c communication.

The data collected through the i2c in this file is as follows:

I2C read 3 bytes: data[15:8] data[7:0] CRC[7:0]

#### example_i2c_sgp40_measure_raw_with_sw0_power.cfg

This configuration file configures the IN100 to communicate with
the SGP40 with the i2c protocal as described above. It then continuously
advertises the data gathered from the sensor.

In order to use these files, the user will need

 1. hardware: IN100 GPIO5 as I2C SCL, IN100 GPIO4 as I2C SDA, and IN100 SW0 used for power. 
    
 2. SGP40 sensor

 3. IN100 Programmer board and development board.

 4. NanoBeacon Config Tool to load the config file onto the NanoBeacon.

### Current Analysis

As a demonstration of the IN100's energy saving capabilities, the following figures and table drive the IN100 with the SGP40 at 1.8 V with a 1 second advertising interval. This uses the i2c_sgp40_measure_raw_signal.cfg config file.

![image](https://user-images.githubusercontent.com/114425682/194930692-fdc622b2-4695-4822-b7aa-01a6d40aedd5.png)

Figure 1: Current while passive for example_i2c_sgp40_measure_raw_signal.cfg

![image](https://user-images.githubusercontent.com/114425682/194930862-0a9184d3-4be6-40d5-b467-169fe34f3378.png)

Figure 2: Current while active for example_i2c_sgp40_measure_raw_signal.cfg

![image](https://user-images.githubusercontent.com/114425682/194934553-2e006a0c-7c37-4cdd-bece-d1587408ff6c.png)

Table 1: Estimated survival time with CR2032 coin cell battery

From the table and figures 1 & 2, the IN100 can advertise at the relatively fast interval of 1 second driven at a 1.8 and still last for over one year.
