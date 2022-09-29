## Using the IN100 with the ADXL367

The ADXL367 is an ultralow power, 3-axis microelectromechanical systems (MEMS) accelerometer 
that consumes only 0.89 uA at a 100 Hz output data rate and 180 nA when in motion-triggered wake-up mode.
This directory contains four files for configuring the IN100 to capture and broadcast data from
the ADXL367 sensor

### i2c_adxl367_50hz_odr_with_temp.cfg and example_adxl367_50hz_odr_with_temp.cfg

#### i2c_adxl367_50hz_odr_with_temp.cfg

This file configures the i2c to communicate with the ADXL367.
The sequence it uses writes to a set of registers to reset
its configuration settings and prepare the sensor for transmitting
data. Once in warm boot up, the sequence sets the register status to read
and reads the following bytes:

I2C read 9 bytes: status, xdata_h,  xdata_l,  ydata_h,  ydata_l,  zdata_h,  zdata_l,  temp_h,  temp_l

See https://www.analog.com/media/en/technical-documentation/data-sheets/ for
information on available registers for i2c communication with the ADXL367
sensor.

#### example_adxl367_50hz_odr_with_temp.cfg

This file configures the IN100 to communicate with the ADXL367 as shown in
i2c_adxl367_50hz_odr_with_temp.cfg, and continuously advertises the data from
the i2c slave.

In order to use this file, the user will need:

  1. hardware:
      IN100 GPIO2 as I2C SCL
      IN100 GPIO3 as I2C SDA
      
  2. ADXL367 works in Measurement Mode , 50Hz ODR.
  
  3. IN100 Programmer board and development board.
  
  4. NanoBeacon Config Tool to load the config file onto the nanobeacon.

### example_adxl367_motion_detect.cfg and i2c_adxl367_motion_detect.cfg

#### i2c_adxl367_motion_detect.cfg

This file configures the i2c to communicate with the ADXL367.
The sequence it uses writes to a set of registers to reset
its configuration settings and prepare the sensor for transmitting
data. The primary difference between this file and the files above is the registers written 
to in order to get the data. For this configuration, it is requesting the motion sensor 
data specifically. Once in warm boot up, the sequence sets the register status to read
and reads the following bytes:

I2C read 9 bytes:status, xdata_h,  xdata_l,  ydata_h,  ydata_l,  zdata_h,  zdata_l,  temp_h,  temp_l 

#### example_adxl367_motion_detect.cfg

This file configures the IN100 to communicate with the ADXL367 as shown in
i2c_adxl367_motion_detect.cfg, and continuously advertises the data from
the i2c slave.

In order to use this file, the user will need:

  1. hardware
      IN100 GPIO2 as I2C SCL
      IN100 GPIO3 as I2C SDA
      
  2. ADXL367 INT2 connect with IN100 MGPIO5 that trigger IN100 advertising
  
  3. ADXL367 works in Measurement Mode , 50Hz ODR.
     Enable the activity and inactivity detection functions in loop mode
     map the AWAKE bit to the ADXL367 INT2 pin.

  4. IN100 Programmer board and development board.
  
  5. NanoBeacon Config Tool to load the config file onto the nanobeacon.
