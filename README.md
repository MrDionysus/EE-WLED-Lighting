## EE-WLED-Lighting
Notes and code for using WLED-controlled LED light strips in Empty Epsilon

# Overview
I used the following steps to create three light bars/strips for my Empty Epsilon bridge.  The strips are powerful but inexpensive to make, and really add to the immersion of an in-person bridge setup.
DISCLAIMER: These steps involve stripping wires and connecting them to a power source.  Use at your own risk.  I'm not responsible if you set something on fire. Educate yourself at https://learn.adafruit.com/adafruit-neopixel-uberguide/powering-neopixels regarding power requirements and how to connect the power source.

# Additional Reading
I pieced this process together using the following resources:
- Neopixel Uberguide https://learn.adafruit.com/adafruit-neopixel-uberguide
- How To Install WLED on an ESP32 Board and Connect / Control Addressable LEDs https://www.youtube.com/watch?v=TOEnFKLm9Sw
- The WLED Project https://kno.wled.ge/
- https://www.youtube.com/watch?v=Er_NqsJUQ0o
- A lot of guidance from the Empty Epsilon channels on the United Stellar Navy discord https://discord.gg/KHBQeEU

# Tools needed
- Wire strippers
- Electrical tape
- Optional: Soldering iron/solder, depending on how you connect your wires
- Optional: Drill for drilling out plastic electrical boxes, if used

# Materials needed
- LED strips: You're looking for 5V individually addressable 5050SMD strips.  For my tube I used a 60 LED/m roll https://a.co/d/ibcPaj2 ($20/5m), for my aluminum channels I used 144 LED/m strips https://a.co/d/7KyVqO5 ($14/1m)
- ESP32 controller: You need 1 controller per strip, they won't work without it.  I used this 3-pack https://a.co/d/iQdDK9a for $15 (~$5/controller)
- 1 spool 22AWG cable cord https://a.co/d/iMc7nA2 ($12/10m)
- Gray #22-#16 AWG wire nuts https://a.co/d/3w4WqYA ($16/1000ct), or just get some from Harbor Freight
- Female breadboard jumper wires. I bought this pack and just use the female connectors https://a.co/d/aOdb7O8 ($7)
- 5v power supply. I used a 3A https://a.co/d/cucyJoM ($8/1ct).  Your amperage needs vary based on length and LED count, educate yourself at https://learn.adafruit.com/adafruit-neopixel-uberguide/powering-neopixels to decide what power supply you'll need.  The one in the amazon link has a DC terminal connector, but you could also cut and strip the wires inside a different power supply.  

# Optional materials 
- 3-pin LED strip connector https://a.co/d/aBcHtsK ($10/20ct). Saves you some soldering. NOTE - does not work for the 144 LED strip listed above, I had to solder those.
- 1/2 double-sided clear tape https://a.co/d/i4VjUmj ($6/roll). Better double-sided tape to hold your strips in place.  The 144 LED strips don't have any tape and need this.
- Plastic electrical boxes https://a.co/d/bOVcQNI ($7/5ct). Just the right size to hold your wires and the ESP32 board.  You'll need to drill out holes for the wires and power connector.  Also need to drill out four little risers at the bottom of the plastic boxes.

# LED container materials (as desired)
- Aluminum channels for light strips https://a.co/d/iDYbw1J ($20/6x 1m channels). Channels meant for LED strips.  NOTE: 60 LED strips look mediocre in these, you can see each LED light.  The 144 LED strips are *mostly* diffused by the cover.
- Clear plastic tubes https://www.lowes.com/pd/Lithonia-Lighting-12-Pack-FLUORESCENT-BULB-GUARD-Clear-Bulb-Guard/1000398805. I spray painted one white, cut it to ~1m, and put two plumbing elbows on the ends.  Inspired by this video shared by gwaland on the USN Discord: https://www.youtube.com/watch?v=Er_NqsJUQ0o, watch it for more ideas.

