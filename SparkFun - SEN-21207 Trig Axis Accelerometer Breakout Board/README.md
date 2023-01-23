## Using the SEN-21207 with the IN100

The SEN-21207 is a atmospheric sensor breakout board utilizing the IN100 to report sensor data from the BMA 400 chip. The BMA 400 is an ultra-low power, 3 axes accelerometer. To learn how to setup this sensor to use with the IN100, see the directory in this GitHub called "Bosch - BMA400 Accelerometer."

### Results

The config files needed to get this example are found in the aforementioned directory "Bosch - BMA400 Accelerometer" under this same GitHub account page.

![image](https://user-images.githubusercontent.com/108510134/214163915-741449ea-2ddf-4084-a098-796b1922a3c0.png)
Figure 1: Passive Current During Advertisment on SEN-21207

![image](https://user-images.githubusercontent.com/108510134/214163933-6a76ee4c-cb11-4488-9522-f2c9b4b0fbef.png)
Figure 2: Active Current During Advertisement on SEN-21207
 
From figure 1 and figure 2, the power consumption of the SEN-21270 is efficient, with an average current of 21.36 uA. At a 1 minute advertising interval, the power consumption becomes 5.45 uA. 
