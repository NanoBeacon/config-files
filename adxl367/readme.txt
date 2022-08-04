The ADXL367 is an ultralow power, 3-axis microelectromechanical systems (MEMS) accelerometer 
that consumes only 0.89 uA at a 100 Hz output data rate and 180 nA when in motion-triggered wake-up mode.

i2c_adxl367_50hz_odr_with_temp.cfg
  1. hardware
    IN100 GPIO2 as I2C SCL
    IN100 GPIO3 as I2C SDA
  2. ADXL367 works in Measurement Mode , 50Hz ODR
  3. I2C read 9 bytes:status, xdata_h,  xdata_l,  ydata_h,  ydata_l,  zdata_h,  zdata_l,  temp_h,  temp_l 


i2c_adxl367_motion_detect.cfg
  1. hardware
    IN100 GPIO2 as I2C SCL
    IN100 GPIO3 as I2C SDA
    ADXL367 INT2 connect with IN100 MGPIO5 that trigger IN100 advertising
  2. ADXL367 works in Measurement Mode , 50Hz ODR.
     Enable the activity and inactivity detection functions in loop mode
     map the AWAKE bit to the ADXL367 INT2 pin.

  3. I2C read 9 bytes:status, xdata_h,  xdata_l,  ydata_h,  ydata_l,  zdata_h,  zdata_l,  temp_h,  temp_l 
