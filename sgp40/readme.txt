The SGP40 is a digital gas sensor designed for easy integration into air purifier s or demand controlled ventilation systems.
Indoor Air Quality Sensor for VOC Measurements.

i2c_sgp40_measure_raw_signal.cfg
  1. hardware
    IN100 GPIO5 as I2C SCL
    IN100 GPIO4 as I2C SDA
  2. I2C read 3 bytes: data[15:8] data[7:0] CRC[7:0]


i2c_sgp40_measure_raw_signal_with_sw0_power.cfg
  1. hardware
    IN100 GPIO5 as I2C SCL
    IN100 GPIO4 as I2C SDA
	IN100 SW0 is used for power
  2. I2C read 3 bytes: data[15:8] data[7:0] CRC[7:0]
