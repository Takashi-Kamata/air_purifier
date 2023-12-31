# Air Purifer

Welcome to my DIY Air Purifier project! Here, I'm sharing my journey of making an affordable air purifier from scratch. I couldn't find budget-friendly options, so I decided to create my own.

Final result:


<img src="https://github.com/Takashi-Kamata/air_purifier/blob/main/airpurifier.png" width="300" />
<img src="https://github.com/Takashi-Kamata/air_purifier/blob/main/pmdata.png" />
<img src="https://github.com/Takashi-Kamata/air_purifier/blob/main/climatedata.png" />

## What's the story?
I wanted clean air for the grow room where I'm keeping my hydroponic farm. Things got a bit plant-smelly during the summer, and I realized I needed to filter the air to remove both the dust and the smell. But the air purifiers sold in stores were way too expensive. So, I thought, 'Why not build one myself?' I realized it's just a fan and a special filter working together. Simple, right?

## My Goals
* Upskill as an Engineer
* Affordable (NZD$100 max)
* Efficient & Effective
* IoT Enabled
* Simple!

## How do air purifiers work?
* Push or Pull polluted air using a fan 
* Force the air through a filter, idealy HEPA (for dust) & Activated Carbon (for smell) filters
* Circulate the air in the room 

## My Approach
* Find a suitable filter. Air purifiers are expensive but their replacement filters are cheap so I will utilise them
* Create a fan from scratch using 3D printed parts. Find and buy a good brushless motor
* Make a case to mount the fan to the filter
* Develop an embedded system to control the fan speed and broadcast air quality info to my home automation system

## Filter
I've decided to use Sunbeam Fresh Protect Air Purifier Filter (NZD$35) for this project! \
It uses a 3 stage filtration system (Pre-Filter Mesh, True HEPA filter, and Carbon Filter). The air purifer that uses this filter costs around NZD$300-$400.

## Fan/Motor
I've decided to use Nidec's [48F Series](https://www.nidec.com/en/product/search/category/B101/M102/S100/NCJ-48F-High-output-Type-A/).
I chose this model because Xiaomi's air purifiers seem to use Nidec's 48F series. It costed around NZD$10 from AliExpress (probably fake), but so far it's running very quietly and producing a good torque to push the air. Measured peak power consumption was around 80W.

![alt text](https://github.com/Takashi-Kamata/air_purifier/blob/main/motor.png)

## Air Quality Sensor
Sensirion's SEN55 is used to measure humidity, temperature, NOx, VOCs, PM1.0, PM2.5, PM4 and PM10. It is accurate, reliable and has mean-time-to-failure (MTTF) of 10+ years. NZD$50.

![alt text](https://github.com/Takashi-Kamata/air_purifier/blob/main/sen55.png)

## Embedded System
### Control Board - ESP32
NodeMCU ESP32 (NZD$3) is used to broadcast sensor data, host web interface to remotely control fan speed, and generate PWM for the motor. 
It connects to WiFi on startup and starts collecting sensor data after an initialisation. All the sensor data are collected on InfluxDB which I host on my home server then pulled to Home Assistance for automations.

## Hardware
### PCB
I wanted a single cable solution where I only need to plug a power cable. However, the motor is rated for 24V and ESP32 and SEN55 runs on 5V. 
I designed a custom PCB with an integrated buck converter to convert 24V to 5V to power everything (LM2596). Also, I included a logic shifter to produce PWM signal at 5V instead of 3.3V. Designed on EasyEDA STD, with electrical components from LCSC. Everything came down to roughly NZD$15 including the PCB and the components.

![alt text](https://github.com/Takashi-Kamata/air_purifier/blob/main/pcb.png)

### 3D Model
I exclusively used OnShape to design the air purifier's outer casing, fan and PCB housing. EasyEDA allows exporting PCB parts which allowed me to visualise the device on OnShape.

Here is the final cross-section of my air purifier. It will sit on top a filter.

![alt text](https://github.com/Takashi-Kamata/air_purifier/blob/main/crosssection.png)

#### 3D Printer
I used SUNLU's [Marble PLA](https://www.sunlu.com/products/pla-marble-1-75mm-filament-1kg-2-2lbs-fit-most-of-fdm-3d-printer?variant=33472258539606) filament on Ender 3 S1 Pro to print all 3D printed parts. 

## Final Cost
NZD$103, however the cost is halved if I didn't need the air quality sensor. I needed a solid air quality sensor to measure performance of the air purifier.

## What's Next?
### FreeRTOS
Since this project went through rapid-prototyping, I coded the ESP32 on Arduino. It made the project move fast but the code can be optimised better/safer. I will transfer the codebase to PlatformIO and use FreeRTOS for more reliable, fast and efficient embedded system in the future.



