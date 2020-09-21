# Thermal Image sensor experiment as presence detector
This was a "failed" experiment project to use an AMG8833 sensor, ESP32, MQTT and Node-Red to use as a presence detector in the door. Since PIR sensors can only tell movement, I wanted to experiment if a low definition (AGM8833 is a 8x8 pixel thermal sensor) thermal image sensor can be used to tell if somebody is the room, stays in various parts of the room etc. It is a failed project, because normal body temperature  pretty much fades into background noise after about 2 meters. It can certainly tell presence in closer distance, but it is not suitable for an entire room. The sensor is relatively expensive (cca. $50 on Banggood) so it is no viable to map a room with multiple sensors.
## What I completed in this project:
- ESP32 sketch reads the image sensor every second and sends the "image" data over MQTT
- ESP32 is also connected to a BME680 environment sensor (temperature, humidity, pressure, voletile gas compound) which is also send over MQTT every 10 seconds
- MQTT data is read by Node-Red and the thermal image is displayed on the Dashboard
- Rules can be defined that are evaluated for each image e.g. max or average temperature on the image, or part of the image.
## Usefull links
- Youtube video explaining this entire project: https://youtu.be/o97A5IZ9Piw
- Node-Red flow: xxxx
- AMG8833 sensor from Banggood: https://www.banggood.com/CJMCU-833-AMG8833-8x8-Thermal-Camera-IR-Infrared-Array-Thermal-Imaging-Sensor-Board-p-1268056.html
- BME680 sensor: https://www.aliexpress.com/item/32961369966.html
## How does it looks like in Node-Red
The below screenshot shows an example of the Node-Red flow.
![Node Red snapshot](/image/noderedsnapshot.jpg)

On the left side the actual thermal image is shown using a blue-red colour palette. That is getting auto scaled according to the measures values. The individual pixels show the exact measured values as well. On the middle the rule engine evaluates the different scenarios and provides a result based on the current image. "Am I at the desk" rule looks at the top right 4x4 pixels and checks if the average temparature is above 27C.
## Wiring
Connected pins are detailed at the top of the Arduino sketch, but you can also see an picture of my breadboard below:
![Breadboard](/image/breadboard.jpg)
## Installation and Configuration
Board configuration does not require any special settings, I just used the "ESP32 Dev Module".
- In lines 22, 23, 24 there are 3 DEFINE statements, where you can change the update interval of the various sensors. Read the comments in the code for further details
- Lines 34-42 specify settings like the Wifi credentials and also MQTT settings
