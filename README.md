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

## I2C Communication with the IN100

### I2C Configuration in NanoBeacon Config Tool

The NanoBeacon Config Tool supports I2C configuration for connecting to external sensors. The IN100 chip comes in two packages; the DFN8 and the QFN18. Only the QFN18 has support for I2C.

To configure I2C in the NanoBeacon Config Tool, click on the “I2C” tab on the left of the window.

![image](https://user-images.githubusercontent.com/114425682/193654770-2d3fe272-cd26-421c-82d2-2711b76596d6.png)

Figure 1 NanoBeacon Config Tool with I2C tab highlighted

Once in this tab, the user has three I2C slaves available for configuration. To use one, click “Enable” at the top of the screen above “Edit.”

![image](https://user-images.githubusercontent.com/114425682/193654814-4a9045e9-35f3-42e7-8f3d-50304474f910.png)

Figure 2 NanoBeacon Config Tool with I2C enable highlighted

Click on “Edit” to continue to settings.

In the “Edit” section there are various options for the I2C slave.

![image](https://user-images.githubusercontent.com/114425682/193654851-e2bd7759-1db7-4abb-b614-95df68d97b77.png)

Figure 3 I2C settings

Pin Select allows choosing from the available pins on the IN100 to be the data line and the clock line for the I2C.

GPIO 1, 2 and MGPIO 4, 5, 7 are the available options.

Address Mode has options between 7 bit and 10 bit addressing. 7 bit addressing is industry standard, but 10 bit is available if needed. Which mode to go with is dependent on the customer’s specific application.

I2C Speed allows a standard mode speed of 100Kbps or a fast mode 400 Kbps. Again, this is dependent on the specific application.

Slave Address is specific to the sensor connecting to the IN100. The user should check the data sheet of the sensor being used to verify the slave address. The following sections will use a sample sensor which has a slave address of 68 (0x44 in hexadecimal). 

Read Data Storage Settings can change the length of data read by the I2C. For this example, the length is set to 6 bytes.

Click on “I2C Commands” to change the commands issued to the I2C on cold bootup and warm bootup.

### I2C Commands

There are three commands here of note. Read, write, and delay. There is an extra command labeled write_stop_read, which is a concatenation of write and read.

![image](https://user-images.githubusercontent.com/114425682/193654921-37671083-a5f6-4321-85b3-098cdcdee719.png)

Figure 4 I2C select commands

In Figure 5, the commands are highlighted in the red box. To add a command to the command line, click on the command, add in the information needed, then click “Add” at the left of the command box at the bottom.

Additionally, the user needs to decide if the command will be executed in cold boot, warm boot, or both. Cold boot is when the sample sensor activates from a state of being powered down. Usually, this is only the first active period. The warm boot is when the device wakes up from a “sleep” state where it is not shut down, but is also not actively transmitting or receiving.

To execute a command in warm/cold boot, click on option before adding to the command box. The user can choose either cold boot, warm boot, or both, but cannot add a command without any option selected.

A command can be inserted between two other commands with the insert button. The command is always added above the one currently highlighted.

To delete a command, click on the command in the command box and click delete.

### I2C Command Formatting

Formatting for I2C commands in the NanoBeacon Config Tool follow a general structure. All commands start with “i2c,” followed by the type of command. Then a colon, a number indicating when the command is executed, and then the data needed by the command. The following read command will be used as an example:

i2c rx: 3

The first part of the command, “i2c,” is the same for every i2c command. The “rx” is short for receive, indicating this is a write command. Next is the colon, separating the type from the data. Finally, the “3,” means the command will be executed in both warm boot up and cold boot up. When the command is in warm boot up, the “3” would be a “1” instead. If it was cold boot up only, the “3” would be a “0.”

For another example:

i2c tx: 1 fd

The tx in this example is short for transmit, showing this is a write command. The “1” means it executes in warm boot up, and the “fd” is the data, in this case the address being written too.

Another example:

i2c wait: 0 1 4e

This command is a delay or a wait command, as indicated by the word “wait.” The “0” means it executes in cold bootup only. “1 4e” is the hexadecimal value 0x014e, which is the time, in microseconds, that the device should delay. Wait can also be used as a stop indicator for a train of Tx/Rx commands. It only performs a stop indicator when the boot condition matches the command. So, a warm boot wait would not insert a stop bit during a cold boot Tx or Rx command.

Finally, one last example:

i2c null:

This is a null command that has 4 zero bits, which is the initial state of the eFuse. It can be used to fill up space which is left blank on purpose. It also marks the end of a sequence of Tx or Rx commands. It allows the I2C to complete the chain of commands and send a stop bit to the I2C bus.

### I2C Write

The I2C write command, as discussed in section 1 of this document, tells the I2C to convert its measurements. To issue a write command, the command line needs an address to write to. For the SHT40, the available addresses to write to are available on the data sheet. For example, to read the temperature for the SHT40, the user would issue a write command to 0xFD.

![image](https://user-images.githubusercontent.com/114425682/193655026-aa88dd94-bb9c-480f-9fbb-b1b5bf74e590.png)

Figure 5 I2C write command example

### I2C Read

The I2C read command only needs a length to function. This determines how many times the I2C will read, not the length of the read itself. The length of the read itself is determined the Read Data Storage Settings shown previously in section 2.1.0.

![image](https://user-images.githubusercontent.com/114425682/193655056-5512c5bc-cc3b-46bd-b4fc-cc413915039c.png)

Figure 6 I2C read command example

### I2C Delay

There are multiple reasons one might want to delay between issuing I2C commands. The common example already mentioned in section 1 is to give the device time to write and convert data before it is ready to be read. The amount of time needed to wait is sensor dependent and can be found on the sensor’s data sheet.

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

