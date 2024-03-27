## Using the SEN-15440 with the IN100

The SEN-15440 is a atmospheric sensor breakout board utilizing the IN100 to report sensor data from the BME280 chip. The BME280 is a low power, highly configurable, atmospheric sensor designed by Bosch. To learn more about this sensor working with the IN100, read the directory on this GitHub page titled "Bosch- BME280 Pressure, Temperature, and Humidity Sensor."

### Results

The config files needed to get this example are found in the aforementioned directory "Bosch- BME280 Pressure, Temperature, and Humidity Sensor" under this same GitHub account page.

![image](https://user-images.githubusercontent.com/108510134/214160457-59e6843f-f610-4f61-a75d-7841f029798b.png)

Figure 1: Passive Current During Advertisment on SEN-15440

![image](https://user-images.githubusercontent.com/108510134/214160482-aca84e30-65a9-4307-b586-48facd78ce99.png)
Figure 2: Active Current During Advertisement on SEN-15440
 
From figure 1 and figure 2, the power consumption of the SEN-15440 is efficient, with an average current of 38.58 uA. Although this may seem high, the BME280 is in forced mode, which requires the sensor to be set at every wakeup. As a result, the power consumption at faster intverals is greater. For example, at an interval of 1 advertisement per minute, the power consumption becomes 1.46 uA. 
