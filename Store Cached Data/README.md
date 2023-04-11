# Transmitting Cached Data

Some users want to use the IN100 for data transmission, however, there is apprehension regarding the potential for missed transmissions. Fortunately, the IN100 contains special register settings available through the “Advanced” tab of the NanoBeacon Config tool. This functionality allows the user to copy data from a register directly into memory, which can then be broadcasted on the advertising payload.

![image](https://user-images.githubusercontent.com/108510134/231279535-d1867b0b-0452-4853-b518-4fcd2e85dc21.png)
Figure 1: NanoBeacon Config Tool Advanced User Settings 

Through this advanced tab, the user can write commands directly to register or memory addresses. 
## Register write and delay commands

Commands are written into the advanced settings. Each command follows a set structure that are detailed below.

### Write Command:
	write: coldwarm, trigger, size, address, value

### Delay Command
	delay: coldwarm, trigger, delay-time

NOTE: The actual commands have the parameters separated by spaces, and not by commas.

The coldwarm parameter denotes the bootup condition when the command is executed. This is either warm or cold bootup. The Table 1 defines the coldwarm values.

![image](https://user-images.githubusercontent.com/108510134/231279678-5504ce11-b9fa-4753-98e1-0c4aba861f3c.png)
Table 1: Coldwarm Values

The trigger parameter in the context of the IN100 pertains to the specific moment during the device's wakeup state when a given command will execute. It's worth noting that this trigger parameter is distinct from the GPIO/sensor trigger sources that are present within the Nanobeacon Config Tool. Table 2 furnishes a comprehensive breakdown of the various trigger conditions and their associated values.

![image](https://user-images.githubusercontent.com/108510134/231279734-f1c61635-f244-4b63-b7df-1f94d5999c9d.png)

Table 2: Trigger Condition Values

The other parameters for the commands are described in Table 3:

![image](https://user-images.githubusercontent.com/108510134/231279764-fd91a7fc-941e-4427-ae4a-9967b6c569ce.png)
Table 3: Other Parameters for Advance Setting Commands Description and Values

### Command Examples

#### Write Command Examples

To trigger a command on wakeup during cold bootup, you can use the following command as an example:

	write: 0 1 0 a1c 23

In this command, the first parameter '0' represents the cold bootup condition according to Table 1. The second parameter '1' represents the trigger condition, indicating that the command will be executed on wakeup, as described in Table 2. The next parameter, '0', indicates the size of the data being written, which in this case is only one byte. 'a1c' represents the address of the register that the command will be written to, and '23' is the value that will be written to that address.

Here's another example: The user wants to trigger a command after the ADC operation is done and write it on both warm and cold bootup. The command to achieve this is:
	
	write: 3 a 3 23f 00112233

The first parameter, '3', sets the coldwarm parameter to both cold and warm bootup, similar to the previous example. The second parameter, 'a', specifies that the trigger condition is for after the ADC operation is done.

The third parameter, '3', represents the size parameter, indicating that the data being written is one word. The fourth parameter, '23f', is the address of the register that the data will be written to, and the final parameter, '00112233', is the data that will be written to the register.

#### Delay Command Example

If the user wants to add a delay of 100 ms after wakeup on warm bootup, they can use the following command:

	delay: 1 1 186A0

Similar to the write command examples, the delay command starts with a '1' to signify that the delay is for warm bootup, and the trigger condition is set to wakeup.

The final parameter, '186A0', represents the value of the delay in microseconds. In this case, it corresponds to 100,000 microseconds or 100 milliseconds.

## Register Definitions

To implement this strategy, two registers are crucial: register 0x14c0 reg_cp_ctrl and register 0x14c4 reg_cp_addr_ctrl. These registers are responsible for specifying the register to be copied, its destination, and when the copying process should start. The details for these registers are defined in the following register definitions.

### reg_cp_ctrl
register copy control 
 
•  Absolute Base Address:	0x 14C0

•  Size:	32

•  Reset Value:	0x 00000000

•  Access:	read-write

![image](https://user-images.githubusercontent.com/108510134/231280588-adb90c7d-08ed-49b7-ab3d-996adfb28a37.png)

### reg_cp_addr_ctrl
register copy control 
 
•  Absolute Base Address:	0x 14C4

•  Size:	32

•  Reset Value:	0x 00000000

•  Access:	read-write

![image](https://user-images.githubusercontent.com/108510134/231280208-42f4bdd9-9283-4ace-9881-da356c85b7df.png)

## Implementing Cached Data Feature

To implement the desired feature, the proposed strategy involves using write commands and registers 0x14C0 and 0x14C4 to copy data from shared direct memory. The copying process involves overwriting the existing memory with new data, storing the new measurement at the starting memory address, and shifting the old data over.

To accomplish this, the memory cache starting at address 0x2f80 and continuing to address 0x2FFF will be utilized. Specifically, data will be copied from addresses 0x2f80, 0x2f84, 0x2f88, 0x2f8c, and so on, as shown in Figure 1 for visualization.
![image](https://user-images.githubusercontent.com/108510134/231280742-685e4c9d-7a76-48dc-8542-cd0be9f91e82.png)
 
Figure 2: Memory Cache Sequence Visual

### I2C Data Example

In the previous section, Figure 2 displays a red box labeled "0x23xx i2c data", which represents the memory for reading data from I2C slave #1. The memory address for this data is 0x2300, and the red box can be replaced with any block of data, such as ADC sensor data, battery voltage level, or I2C slave #2 read data. To obtain the results shown in Figure 1, the sequence of commands outlined in Figure 2 is executed. Figure 2 provides a clear illustration of the steps involved in the process.

![image](https://user-images.githubusercontent.com/108510134/231280938-14b830b3-56a7-49a2-9c5d-0e175ef65448.png)


Figure 3: Memory Cache Sequence Visual with Commands

The commands listed in the sequence are executed during both cold and warm bootup and trigger when the device is preparing to sleep. Register 0x14c4 is used for specifying the source and destination registers for the copying process, as outlined in the register map. In this case, the destination register is 0x2f00, and the source register is 0x2f80, which is consistent with the image in Figures 1 and 2, as well as the register description.

Meanwhile, writing to register 0x14c0 specifies the number of registers to be copied and whether the copying process is ready to be performed. The final write to register 0x14c0 is set to '11' instead of 'b1' to indicate that only one register is being copied instead of eleven.

If the user wants to access the other I2C slave data, the address is offset by 16 bytes between the I2C slaves. So, I2C slave #1 stores its data starting at 0x2300, I2C slave #2 stores its data starting at 0x2316, and slave #3 stores its data at 0x2332.

### ADC Data Example

![image](https://user-images.githubusercontent.com/108510134/231280992-10f51c85-6af7-4796-a91e-9c810d8b5034.png)

Figure 4: ADC Store Data Example

In Figure 4, the sequence of commands is modified from Figure 3 to store data from ADC channel 0. To achieve this, the trigger condition from Table 2 is changed to 'b', which ensures that the data is stored after the ADC channel 0 operation is completed, thereby guaranteeing that the stored value has been updated from the last measurement. The addresses for the ADC channels are 0x61c, 0x63c, 0x65c, and 0x67c. The data for channel 0 is stored at address 0x61c, for channel 1 it is 0x63c, 0x65c for channel 2, and 0x67c for channel 3.

### On-Chip Temperature Sensor Example

If the user wants to store previous temperature readings from the on-chip temperature sensor, then the user would use the register 0x73C to shift in. 

The second to last command from Figure 4 would change to:

write: 3 9 3 14c4 2f800073C

## Transmitting Cached Data

T0 transmit cached data, the user can use the "Register Read Data" option in the Manufacturer Specific Data settings:

![image](https://user-images.githubusercontent.com/108510134/231286922-2a0213b0-bbd6-4248-8924-786f592987ff.png)

Figure 5: Transmitting Cached Data

With this option, the user can select the registers they want to transmit, the number of bytes from the register, and wether or not it will be encrypted.


