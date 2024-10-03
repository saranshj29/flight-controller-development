# Flight-controller-development
## Flight Controller Project Using STM32F11CEU6 Development Board - Version1
 
 Developing a flight controller using the STM32F11CEU6 development board, alongside various sensors, and calibrating it in INAV 7 involves several steps. Below is a detailed guide how i progress  through the entire process, from hardware setup to calibration.

## Components Needed
STM32F11CEU6 Development Board-This is the main microcontroller unit (MCU) that will process sensor data and control the flight.
Inertial Measurement Unit (IMU)Sensors like the MPU6050 (gyroscope + accelerometer) or the LSM9DS1 (IMU with magnetometer) for orientation and motion detection.

PCB PROTOTYPING BOARD- Pcb prototyping board is required to make various connections from stmf32411 board to various sensors like mpu6050 bm270,compass etc

GYROSCOPE-Sensors like the MPU6050 (gyroscope + accelerometer) or the LSM9DS1 (IMU with magnetometer) for orientation and motion detection.

BAROMETER-The BMP280 is a high-precision sensor developed by Bosch Sensortec, it is used for measuring atmospheric pressure, temperature, and altitude

COMPASS-The compass sensor module (CSM) is a small, discrete electronic device that measures the orientation of an object, like an object in a room or outside in the wind. The CSM uses two sensors to measure the orientation of an object: a magnetometer and an accelerometer.

GPS MODULE-Robotbanao NEO-6M GPS Module it is used for  information for preparing accurate surveys and maps, taking precise time measurements, tracking position or location, and for navigation.

BEC-We need a constant  5V AND 3.3V suppy to development board and 3.3v to various senscors so a battery elemination circuit is required

RADIO TRANSMITTER AND RECIEVER-A transmitter is a device that converts electrical signals into radio waves and broadcasts them over the air.The receiver picks up the transmitted radio waves and converts them back into usable information. I used a flysky fs-i6 transmitter and fs-i6b reciever for pwm,ppm.sbus,ibus communication between reciever and transmitter

PDB-A PDB is a circuit board used to distribute power from a single source (typically a battery) to multiple components of a system, such as motors, ESCs (Electronic Speed Controllers), flight controllers, and other peripherals. 

ESC-electronic device used to control the speed, direction, and braking of an electric motor. I ready to sky 40a esc for this particular project

BRUSHLESS MOTORS-I used ready to sky  brushless motors 

FRAME- f450 DRONE FRAME

# SOFTWARE AND TOOLS
## Responsibility and resource
This is the unofficial target for INAV( Original source: https://github.com/iNavFlight/inav). Provides support for flight control boards that do not have official INAV support for the STM32F411CEU6 board. 
Whether or not to use this firmware is the user's responsibility and is free to do so. INAV developer link : https://github.com/iNavFlight/inav/tree/master/docs/development You can find all the details for firmware development here.

## STM32F411CEU6 INAV Firmware AND Betaflight Firmware
STM32F411CEU6 Board Firmware
First, let's connect the board and the computer.
![image](https://user-images.githubusercontent.com/19993109/139479391-49dafee0-a7da-49ae-9196-10a578d4ac55.png)

## Download INAV Configurator
https://github.com/iNavFlight/inav-configurator/releases

## Windows
Download Configurator for Windows platform (win32 or win64 is present)
Extract ZIP archive
Run INAV Configurator app from unpacked folder
Configurator is not signed, so you have to allow Windows to run untrusted application. There might be a monit for it during first run

##Install DFU Drivers (DFU mode)
### ImpulseRC Driver Fixer
https://impulserc.blob.core.windows.net/utilities/ImpulseRC_Driver_Fixer.exe
* Start ImpluseRC Driver Fixer
* Connect the FC USB to the PC While holding the boot button in. (DO NOT power on FC via external 5V or Vbat)
* The ImpulseRC Driver Fixer should then see and load the proper driver
* Start INAV configurator
* Connect the FC USB to the PC while holding the boot button in.
* INAV configurator should show it’s connected in DFU mode in the top right corner (DO NOT click the CONNECT button)
* Choose the latest hex file for your FC and then “Load Firmware local”. Once loaded, click “Flash Firmware”.
  # PIN DIAGRAM FOR STMF411CEU6
![273340518-a7bc5353-be8f-49d7-b47e-8685062d16f3](https://github.com/user-attachments/assets/2f0f6993-b4e2-429d-ac9e-2c971ec7c73d)
## PIN OUTS FOR GYRO AND BAROMETER
![327976540-ad865ced-7b75-48ea-ab6f-33a8e011db34](https://github.com/user-attachments/assets/d39c24f5-5f2c-4b8a-8d26-e53214e362a0)

### NOTE
You can connect the following modules to the board with SPI2. Board pins and module connections are given.
NOTE: There are many fakes of these modules. Therefore, first ask the seller about the module you want to buy and ask whether the chip on the module is the same. Otherwise, you may encounter fake modules.
Many fake modules have the MPU6500 chip on them. INAV automatically detects the chip you connected and shows you the chip information on the module.

## PIN OUTS FOR RECIEVER
![202130179-ef0616bc-785d-4cfc-98a4-097b3db7d4aa](https://github.com/user-attachments/assets/541389da-945d-42c1-84e2-705a8ea06c76)
![148846827-12eb543c-f4cb-4ab8-be8f-1b9b10d9a25b](https://github.com/user-attachments/assets/a46dad9d-ec88-421f-929e-b7a8787894c2)

## CIRCUIT DIADRAM OF FLIGHT CONTROLLER
![wire](https://github.com/user-attachments/assets/f3716941-469e-47e6-bdee-6fdc4e2f172e)
![ADsaDDSADSADADSADAS](https://github.com/user-attachments/assets/daa0c5f0-d4c4-4b38-beda-789702cf20bc)

# USE DC TO DC CONVERTER FOR SERVO OR POWER BOARD
![202129433-0c62a71a-41a4-4acb-99f8-6ad0d76db480](https://github.com/user-attachments/assets/e727d0fe-185d-445e-bd86-df2eb866566d)
![202128769-e25c806f-7465-484e-b5be-e26ed039809d](https://github.com/user-attachments/assets/de2d1e4f-bcf3-444f-a0ca-2c93f2aec6a6)
# CONEECTION WITH ESC 
![273340674-4eb16000-7abe-4209-af25-581cc869b4e0](https://github.com/user-attachments/assets/8495846d-281e-4258-920e-ffd0ff4c31b9)



# Calibration for ESC

Instructions for setting throttle calibration for ESC high and low signal input:
1. Connect the ESC with the motor, connect the signal lead to the board according to the pin and motor port according to the diagram. You should do this for all of the motors you are going to use.
2. Open the INAV Configurator and connect to the flight control hub.
3. Adjust the gyroscope / accelerometer and magnometer calibration settings.
4. Turn on the remote control and enable the receiver protocol in the Receiver section. 
5. Go to the Output field and set the ESC output protocol according to you. We describe the setup for the STANDARD protocol.
6.To calibrate ESCs, make sure the propellers are off, flick on the “I understand” toggle, raise Master to full value, and plug in your battery.
7. The ESCs will go through their tones.
8. When the double beeping sound is heard (the highest point of the throttle is confirmed), move the throttle to the lowest point.
9. ESC calibration is considered done when three beeps mean OK.
10. Now unplug, plug in again, and raise Master very slowly until the motors are spinning comfortably.
# NOTE-for confrigration of inav please see video on youtube
# PROTOTYPE
![WhatsApp Image 2024-10-03 at 9 28 48 AM](https://github.com/user-attachments/assets/e0ec92dc-85ba-4300-9d20-514c164fd87a)

# FINAL VERSION OF STM32F411CEU6 FLIGHTCONTROLLER

![DFGDGF](https://github.com/user-attachments/assets/a06fda05-a3f7-485d-bd3c-075e925cdda5)
![ASFDAF](https://github.com/user-attachments/assets/7b5dd90a-2638-4982-812e-2dac9fe712e3)
![aigdytsafdgu](https://github.com/user-attachments/assets/5ff2059a-1135-441b-b27d-7bcf994d6554)








