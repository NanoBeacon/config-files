# InPlay-Technologies IN100 Githup Page
### Links
#### [Website](https://inplay-tech.com)
#### [NanoBeacon Config Tool](https://inplay-tech.com/nanobeacon-config-tool)
#### [IN100 Development Kit](https://www.digikey.com/en/products/detail/inplay-inc/IN1BN-DKC0-100-C0/15652914?s=N4IgTCBcDaIJIDsCMAGFIC6BfIA)
#### [IN100 DFN8](https://www.digikey.com/en/products/detail/inplay-inc/IN100-D1-R-RC0I/15652913) and [IN100 QFN18](https://www.digikey.com/en/products/detail/inplay-inc/IN100-Q1-R-RC0I/15652915)

### IN100 Support

This GitHub page contains a set of examples for using the IN100. To use an example, 
download the NanoBeacon Config Tool and load one of the config files found here.

## How to use a config file

In order to use a config file, download the [NanoBeacon Config Tool](https://inplay-tech.com/nanobeacon-config-tool) from our website.

Once installed, open the application and click on Load in the bottom right corner

![image](https://user-images.githubusercontent.com/114425682/193160993-83471116-5d56-492c-ab94-f5873a315d6a.png)

Navigate to where the config file is being stored and select it.

## File Description

### ADXL367

The ADXL367 is an ultralow power, 3-axis microelectromechanical systems (MEMS) accelerometer
made by Analog devices. This directory contains configuration files to configure the
IN100 to interface with the ADXL367 sensor.

### Doc

This directory contains I2C sensor one shot mode and I2C sensor power control guides.
THis directory also contains Scalable Vector Graphics files on I2C timings.

### SGP40

The SGP40 is a digital gas sensor designed for easy integration into air purifiers 
or demand controlled ventilation systems made by Adafruit. This directory contains
configuration files to use the SGP40 with the IN100.

### i2cbma400.cfg

The BMA400 is a 12-bit triaxal acceleration sensor with position and motion triggered 
interrupt features. This configuration file configures the IN100 to communicate with
the BMA400.

### i2c_device_with_sw0_power_control.cfg

This file activates power switching for the i2c. Power switching is recommended for
use cases with longer advertising intervals. The longer the time between advertising
events, the more efficient it is for the IN100 to use power switching for its i2c
configuration.

### i2c_sht4x.cfg

The SHT4x sensor series is a low power, high accuracy, 16-bit relative humidity and
temperature sensor made by Sensirion. This configuration file uses a typical write-
delay-read sequence to communicate with the SHT40 sensor.

### i2c_sht4x_low_power.cfg

This configuration file uses a low power consumption i2c sequence. It accomplishes
this by using the sleeping time of the sensor to process i2c write commands. This
reduces the use of i2c delay/wait commands and as a result, allows the sensor to
minimize time spent awake abnd advertising.

### i2c_tmp102.cfg

The TMP102 is a lowpower digital temperature sensor made by Sparkfun. This file
configures the IN100 i2c to communciates with the TMP102.

