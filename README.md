# EE-WLED-Lighting
Notes and code for using WLED-controlled LED light strips in Empty Epsilon

![image](https://github.com/MrDionysus/EE-WLED-Lighting/assets/26928293/66115c23-b336-424a-af48-23c20545893c)

![image](https://github.com/MrDionysus/EE-WLED-Lighting/assets/26928293/8c971bc6-63a7-4dec-bea3-1bff3368dfca)

## Overview
I used the following steps to create three light bars/strips for my Empty Epsilon bridge.  The strips are powerful but inexpensive to make, and really add to the immersion of an in-person bridge setup.
DISCLAIMER: These steps involve stripping wires and connecting them to a power source.  Use at your own risk.  I'm not responsible if you set something on fire. Educate yourself at https://learn.adafruit.com/adafruit-neopixel-uberguide/powering-neopixels regarding power requirements and how to connect the power source.

## Additional Reading
I pieced this process together using the following resources:
- Neopixel Uberguide https://learn.adafruit.com/adafruit-neopixel-uberguide
- How To Install WLED on an ESP32 Board and Connect / Control Addressable LEDs https://www.youtube.com/watch?v=TOEnFKLm9Sw
- The WLED Project https://kno.wled.ge/ and [Getting Started - WLED Project ](https://kno.wled.ge/basics/getting-started/)
- https://www.youtube.com/watch?v=Er_NqsJUQ0o
- A lot of guidance from the Empty Epsilon channels on the United Stellar Navy discord https://discord.gg/KHBQeEU

## Components
### Tools needed
- Wire strippers
- Electrical tape
- Optional: Soldering iron/solder, depending on how you connect your wires
- Optional: Drill for drilling out plastic electrical boxes, if used

### Materials needed
- LED strips: You're looking for 5V individually addressable 5050SMD strips.  For my tube I used a 60 LED/m roll https://a.co/d/ibcPaj2 ($20/5m), for my aluminum channels I used 144 LED/m strips https://a.co/d/7KyVqO5 ($14/1m)
- ESP32 controller: You need 1 controller per strip, they won't work without it.  I used this 3-pack https://a.co/d/iQdDK9a for $15 (~$5/controller)
- 1 spool 22AWG cable cord https://a.co/d/iMc7nA2 ($12/10m)
- Gray #22-#16 AWG wire nuts https://a.co/d/3w4WqYA ($16/1000ct), or just get some from Harbor Freight
- Female breadboard jumper wires. I bought this pack and just use the female connectors https://a.co/d/aOdb7O8 ($7)
- 5v power supply. I used a 3A https://a.co/d/cucyJoM ($8/1ct).  Your amperage needs vary based on length and LED count, educate yourself at https://learn.adafruit.com/adafruit-neopixel-uberguide/powering-neopixels to decide what power supply you'll need.  The one in the amazon link has a DC terminal connector, but you could also cut and strip the wires inside a different power supply.  

### Optional materials 
- 3-pin LED strip connector https://a.co/d/aBcHtsK ($10/20ct). Saves you some soldering. NOTE - does not work for the 144 LED strip listed above, I had to solder those.
- 1/2 double-sided clear tape https://a.co/d/i4VjUmj ($6/roll). Better double-sided tape to hold your strips in place.  The 144 LED strips don't have any tape and need this.
- Plastic electrical boxes https://a.co/d/bOVcQNI ($7/5ct). Just the right size to hold your wires and the ESP32 board.  You'll need to drill out holes for the wires and power connector.  Also need to drill out four little risers at the bottom of the plastic boxes.

### LED container materials (as desired)
- Aluminum channels for light strips https://a.co/d/iDYbw1J ($20/6x 1m channels). Channels meant for LED strips.  NOTE: 60 LED strips look mediocre in these, you can see each LED light.  The 144 LED strips are *mostly* diffused by the cover.
- Clear plastic tubes https://www.lowes.com/pd/Lithonia-Lighting-12-Pack-FLUORESCENT-BULB-GUARD-Clear-Bulb-Guard/1000398805. I spray painted one white, cut it to ~1m, and put two plumbing elbows on the ends.  Inspired by this video shared by gwaland on the USN Discord: https://www.youtube.com/watch?v=Er_NqsJUQ0o, watch it for more ideas.

## Setup
- Flash your ESP32 with WLED by following the instructions at https://kno.wled.ge/basics/install-binary/
- Follow the on-screen prompts to connect to the device and join it to your WiFi network
- Run your led strip, counting the number of LEDs.
- Clamp or solder three wires to the strip (red = 5v, green = DIN/Data, white=GND) ![image](https://github.com/MrDionysus/EE-WLED-Lighting/assets/26928293/f6204b30-84d5-4d8a-831a-20ae21bedb6f)
- Attach wires to ESP32 board – white to GND, Red to 5V, Green to P16 ![image](https://github.com/MrDionysus/EE-WLED-Lighting/assets/26928293/529e88b1-d549-444c-9f65-7b4c127be72e)
- Attach wires to power source – white to GND, Red to 5V ![image](https://github.com/MrDionysus/EE-WLED-Lighting/assets/26928293/da6b4c20-cd11-490f-bfb5-bf4922099de4)
- Join all same-colored wires together.  I used Grey #22 wire nuts. ![image](https://github.com/MrDionysus/EE-WLED-Lighting/assets/26928293/06e3bc25-e242-4a03-8f52-d19d6551d579)

## WLED Setup
- Connect to WLED over WiFi with your browser
- In LED, set the following

#### LED Preferences:
- Set "Length" to number of LCDs in your strip
- Set GPIO to 16, or whichever pin you plugged green into on the board 






 








