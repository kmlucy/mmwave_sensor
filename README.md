# Overview

This repository contains everything needed to build a plug-in mmWave presence sensor that works with ESPHome and Home Assistant. It plugs directly into an outlet and is position adjustable. The mmWave sensor itself is the popular model from DFRobot. The ESP32 that powers it is programmed and managed from ESPHome, and the sensor works with Home Assistant.

![PXL_20220926_134027611](https://user-images.githubusercontent.com/13952475/192294687-1cd1020a-3280-46bc-bacd-440ba9171007.jpg)

# Parts

- The mmWave sensor itself: [DFRobot SEN0395](https://www.dfrobot.com/product-2282.html)
- The ESP32: I used [this one](https://smile.amazon.com/gp/product/B08PNWB81Z), but any ESP32 D1 Mini should work. Just check the pinout and size to make sure it is the same.
- This exact [USB charger](https://smile.amazon.com/gp/product/B07P41X3L3). The entire project has been designed to fit this exact charger, so subbing in a different model would require substantial redesign.
- A short micro USB to USB A cable, the shorter the better. I used [this one](https://smile.amazon.com/gp/product/B01FSYBQ9Q).
- The housing itself is fully 3D printed. The STLs and STEP files are available in this repository, and also on [Thingiverse](https://www.thingiverse.com/thing:5533111). You will need 1X of each part.
- 3X M3-0.5 x 8mm flat head countersunk screws
- 2X ~5" pieces of wire to connect the plug to the charger board. I used 20awg, but it isn't important.

![PXL_20220926_114124538](https://user-images.githubusercontent.com/13952475/192278685-898deb84-dc93-4881-b344-dffaf04ae0bf.jpg)

# 3D Printing

1. Print 1X of each file.

![PXL_20220926_113806827](https://user-images.githubusercontent.com/13952475/192278475-aa8664be-d386-405f-b4f0-3ee8420e501e.jpg)

2. I printed them in PLA with .100mm layer height, 20% infill, and 3 walls. Ultimately, material and print settings don't matter. Choose a color and material you like and have, and print them as fine or coarse as you want. Most, but not all, parts need supports. F_001480 and F_001486 can be printed without. For the others, I would recommend setting your support angle to be ~70° to avoid supports on the exterior corners, around the ball, or in the holes.
2. After printing, remove supports and tap the two holes in F_001480 and one hole in F_001485 M3-0.5.

# USB Charger Modifications

1. You will need two parts from the USB charger: the plug and the circuit board.

![PXL_20220926_114234905](https://user-images.githubusercontent.com/13952475/192278229-41655264-f082-4b3a-a6d5-40a7087b3639.jpg)

2. Carefully cut open the housing along the line where the gray and white plastics meet. I used a vertical bandsaw, but a rotary tool or even a hacksaw would probably be better choices. You want to just barely cut through the plastic without cutting into the circuit board.

![PXL_20220926_114312025](https://user-images.githubusercontent.com/13952475/192278281-cd9cd39d-70c2-44ea-8054-dc8243f1994e.jpg)

3. Remove the front of the housing and discard. Set the circuit board aside.
4. Drill and countersink the center of the plug end of the housing to fit your M3 screws:

![PXL_20220926_114320623](https://user-images.githubusercontent.com/13952475/192277977-ec587d7a-f1b9-4737-adfb-2735a0946f53.jpg)

# Solder mmWave Sensor to ESP32

1. Position the mmWave sensor on the ESP32 with the pins included with the sensor. The mmWave sensor should be on the back of the ESP32 and face out. The pins should match up as follows (sensor - ESP32): TX - IO22, RX - IO21, IO1 - IO17, IO2 - IO16, G - GND, V - VCC. 

![PXL_20220926_114438615](https://user-images.githubusercontent.com/13952475/192280289-03ba695c-2f4a-4d89-9ebc-cb3c4d7d892e.jpg)

2. Carefully solder each pin to the sensor and to the ESP32.

![PXL_20220926_114413633](https://user-images.githubusercontent.com/13952475/192280301-4ab52aeb-5f65-415b-977a-de116815b41a.jpg)

# Program the ESP32

1. Download the [esphome_config.yaml](esphome_config.yaml) file.
2. Rename it to whatever your device will be named and place it in your ESPHome directory.
3. Replace all of the bracketed options with whatever you want to use.
4. Download the [leapmmw_sensor.h](https://github.com/hjmcnew/esphome-hs2xx3a-custom-component/blob/main/leapmmw_sensor.h) file to your ESPHome directory.
5. Plug in your ESP32 to your computer and use ESPHome to install the config. For more instructions, please see the [ESPHome Docs](https://esphome.io/).

# Add to Home Assistant

1. Go to your Integrations page in Home Assistant:

<a href="https://my.home-assistant.io/redirect/integrations/" target="_blank"><img src="https://my.home-assistant.io/badges/integrations.svg" alt="Open your Home Assistant instance and show your integrations." /></a>

2. Your new device should be discovered and available to add to Home Assistant. Add it and make sure all the entities are working properly. 
3. Unplug your device from your computer to get ready to assemble.

# Assemble the Sensor

1. Snap together the ball and socket joint.

![PXL_20220926_132025375](https://user-images.githubusercontent.com/13952475/192294055-58f37193-7bf1-49e4-8bea-03946ff82f5c.jpg)

2. Solder the two wire leads to the charger board.

![PXL_20220926_132143790](https://user-images.githubusercontent.com/13952475/192294198-fcaac741-4742-4302-a8df-f03352040d2c.jpg)

3. Route the wires through the housing lid and plug housing, splitting them around the divider in the housing.

![PXL_20220926_132422276](https://user-images.githubusercontent.com/13952475/192294247-92e39336-b97f-40fc-8083-17f65e2798d6.jpg)

4. Solder the other end of the wire leads to the plug.

![PXL_20220926_132716060](https://user-images.githubusercontent.com/13952475/192294281-b391cb2b-0466-4f58-b2ea-a7570386a983.jpg)

5. Insert the plug into the plug housing and screw it into place.

![PXL_20220926_133123354](https://user-images.githubusercontent.com/13952475/192294328-43381e11-408d-4f42-bf71-1f8b5016bb5e.jpg)

6. Plug the micro USB cable into the ESP32 and insert the sensor/ESP32 into the front housing with the sensor facing down.

![PXL_20220926_131239129](https://user-images.githubusercontent.com/13952475/192294362-77816bc1-a132-4503-8e56-6265295e6ee4.jpg)

7. Add the first spacer.

![PXL_20220926_131252137](https://user-images.githubusercontent.com/13952475/192294421-ad93701d-ddec-4024-a784-89d9cfabc06b.jpg)

8. Plug the other end of the USB cable into the charger board. Twist it around twice and insert it into the housing.

![PXL_20220926_133310967](https://user-images.githubusercontent.com/13952475/192294553-4ff0670b-5a98-4f8c-94c2-bbeb99e954af.jpg)

9. Add the second spacer.

![PXL_20220926_133356221](https://user-images.githubusercontent.com/13952475/192294583-e46a5c05-848a-43d8-a12e-93084c4cd28e.jpg)

10. Route the power wires as shown.

![PXL_20220926_133632226](https://user-images.githubusercontent.com/13952475/192294612-8975e26c-bccb-43c7-b977-82ecd3a889fa.jpg)

11. Install the housing lid and screw it into place.

![PXL_20220926_133923070](https://user-images.githubusercontent.com/13952475/192294630-91ce4258-4e1a-4cb9-b9a4-342b1019c3fc.jpg)

12. Plug it in and make sure everything is still working.
13. Done!

# Sources

https://github.com/hjmcnew/esphome-hs2xx3a-custom-component

https://community.home-assistant.io/t/mmwave-presence-detection-esphome-style/382778

https://www.youtube.com/watch?v=Viqvx7hMMJs
