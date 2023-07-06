# GPIOs and the IN100

The IN100 has several different packages, each with different GPIOs accessible. MGPIO stand for Mixed-Signal GPIO meaning they can act as both analog and digital inputs. 

### DFN8
This is the 8 pin package with 2 MGPIO's available. These are MGPIOs 4 and 5 and are reserved for the UART.
### QFN18
This is the 18 pin package with 8 GPIOS available. These are GPIOs 0, 1, 2, and 3, and MGPIOs 4, 5, 6, and 7. GPIOs 0 and 1 are reserved for the UART.
### WLCSP
This is the smallest packaging at 1.1 x 2 x .33 mm and has 4 GPIOs available. These are GPIO 0 and MGPIOs 4, 5, and 7. MGPIOs 4 and 5 are reserved for the UART.

## Configuring the (M)GPIOs in the NanoBeacon Config Tool

![image](https://github.com/NanoBeacon/config-files/assets/108510134/40301c09-5546-442d-860c-dce9c6fb9a38)
Figure 1: GPIO Tab Highlighted

The user can access the GPIO settings in the GPIO tab as highlighted in Figure 1. The (M)GPIOs have several states. These states can be selected from the left-most drop down menu for each GPIO. The states are as follows:

1. Default. The GPIO will be high as default. 
2. Analog. The GPIO is an analog input. This is for the ADC.
3. Output Low. The IN100 will drive the GPIO to be low
4. Output High. The IN100 will drive the GPIO to be high
5. Wakeup High, Sleep Low. The GPIO will be driven high when the IN100 is awake, and low during the sleep state.
6. Wakeup Low, Sleep High. The GPIO will be driven low when the IN100 is awake, and high during the sleep state

GPIO states will be automatically selected when used for I2C, ADC, GPIO Edge Count, and One Wire Sensor Controller. All other use cases should be configured manually. The default state should only be selected manually if the user does not intend to use that GPIO for any purpose. 

### Pull Up/Down Behavior

In certain states, the GPIO can be configured for pull up/down behavior. This means that the IN100 will drive the GPIO internally to be either high or low. This is useful if for use cases where the GPIO should exhibit a certain bevaior (i.e. outputting high or low) until driven externally.
Most common such cases are using the GPIO to trigger an advertisement set on a high/falling edge and having it pull up/down to avoid a floating state and accidental trigger.

### Adv. Trigger

Adv. Trigger is short for advertisement trigger. This option is availabe in the Input state for the GPIO. This is used for triggering advertisement events using a rising, falling, high level, or low level input on the selected GPIO.

### Wakeup

This option is handeled automatically by the config tool. It remains as a greyed out option as it may become available again to users in a future update of the config tool software.

### Latch

Latching will make the GPIO hold the last state it was driven at until driven otherwise. The options here include latch, and "latch in sleep, wakeup unlatch". The first option is latching as described earlier, while the second option unlatches during the wakeup time. 
In general, latching is not needed unless the GPIO is not being driven externally during sleep.

## Advanced Settings for GPIOs

Some additional behavior is possible through the Advanced tab of the config tool. 

![image](https://github.com/NanoBeacon/config-files/assets/108510134/2c0ed609-68aa-4d66-8c5c-538bf5ff6ee9)
Figure 2: Advanced Tab Highlighted

In this section, register write commands can be written and executed during the wakeup-sleep cycle of the IN100. The register write commands are explained in detail in the Host Controller API Guide under the Host Controller API section of this GitHub page. Although they seem similar to the I2C commands, that is only in structure and not in content or purpose of the commands.
These commands are stored in eFuse region 2 of the IN100, but they can also be executed using UART Commands instead. The following will cover the information relevant to the write command in the Advanced section of the config tool. 

### Commands

4 Types of the command are defined and listed in the following table.

![image](https://github.com/NanoBeacon/config-files/assets/108510134/dd1f8c12-e33c-43b7-9079-3b8f6d329351)

Table 1: Auto Programming Command

The first byte of the command always contains the information listed in the following table

![image](https://github.com/NanoBeacon/config-files/assets/108510134/87dab784-608e-4b5f-8a80-65ab90d96524)

Table 2: First Byte of the Command

#### Register Write Command 

After the 1st byte, if the command field is 2, the following several bytes indicate how to write a
value into a given register address (based on the size of the value)

![image](https://github.com/NanoBeacon/config-files/assets/108510134/5c535f97-09e7-4395-a410-4f26c64b3f59)

Table 3: List of subfields for value field in write command

Based on the size specified in the 2nd byte of the command, the total length of the command can
be:
1. 4 bytes if the size is 0 (single byte). The address is byte address and two LSB’s in the address
field indicate the byte offset in the word.
2. 5 bytes if the size is 1 (half word or 2 bytes). The address is half-word address and the 2nd LSB
in the address field indicates the half-word offset in the word. The LSB will be ignored.
3. 7 bytes if the size is 2 or 3 (1 word or 4 bytes). The address is word aligned address. The 2
LSB’s will be ignored.

#### Boot Condition

The command has to satisfy the boot condition to be executed. The condition is specified by the
boot condition field (bit 2 to 3) in the first byte of the command as shown in Table 7. The boot
condition values are specified as the following table. 

![image](https://github.com/NanoBeacon/config-files/assets/108510134/a6778223-127d-4ab9-b516-792f6067251e)

Table 4: Boot Conditions

#### Trigger Conditions

The command also has to satisfy the trigger condition to be executed. The condition is specified
by the trigger condition field (bit 4 to 7) in the first byte of the command as shown in Table 8. The
trigger condition values are specified as the following table.

![image](https://github.com/NanoBeacon/config-files/assets/108510134/d71f4e30-57b1-49d5-93c0-9def6e3ab9bd)

Table 5: Trigger Conditions

### Register Definitions for GPIOs

The GPIO registers share addresses offset by 4 bytes from one another.

![image](https://github.com/NanoBeacon/config-files/assets/108510134/aed60c89-4448-4169-b4ff-71b5e80f7cd8)

Figure 3: Register Definition for GPIO 1

In Figure 3, the register definition for GPIO 1 is provided. Likewise, GPIO 2 will start at 0xA10, GPIO3 at 0xA14, GPIO4 at 0xA18, and so on up until MGPIO 7.

![image](https://github.com/NanoBeacon/config-files/assets/108510134/18c4e240-c99d-4256-98a1-35ad2ccee241)

Figure 4: GPIO Latch Control Register

The latch control register allows direct control of when a GPIO is latching.

### Example Command Sequence

As an example, imagine a use case where a GPIO must go high to power an LED on cold boot up, but not on warm boot up. For this sequence, the latching is set to unlatch MGPIO 5, make it go high, and then do the reverse before going to sleep. That would mean unlatching, making it go low, and latching again before sleep.

![image](https://github.com/NanoBeacon/config-files/assets/108510134/c91992fd-f303-42d1-868b-8a3f79b15889)

Figure 5: Example Command Sequence










