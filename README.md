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

- In WLED, set the following:

#### LED Preferences:
- Set "Length" to number of LCDs in your strip
- Set GPIO to 16, or whichever pin you plugged green into on the board 

#### Wifi Setup: 
- (Optional) set up mDNS name
- Check the "Disable WiFi Sleep" button

#### Sync Interfaces Setup: 
- Set DMX Mode to "Effect".  (Reminder: "Effect" uses 15 channels instead of 3)
- (Optional) change "DMX Start Address" to a different starting channel if using multiple sACN devices in the universe.  For example, for a second WLED device, set start address to 16
- (Optional) if you've configured multiple Segments, those addresses will also need to be accounted for in the config.  Each segment is another block of 15 channels.
- These "Optional" entries will make more sense when you get into configuring the hardware.ini file

## Configure Empty Epsilon hardware.ini file
Once your lights are working, it's time to get them to play nicely with EE.  Lighting effects are defined in the "hardware.ini" file, which lives in the root of your Empty Epsilon folder.  The EE wiki's documentation on configuring the hardware.ini file is found at https://github.com/daid/EmptyEpsilon/wiki/DMX-Configuration#hardware

I've attached my present hardware.ini to this repo, and I'll cover and try to explain what's going on in it. 
Light Setup:  I have three lights 
- a horizontal lightbar (HorizontalBar1) with 60 LEDs in a clear tube that was spray painted white.  I use this for a variety of conditional lighting effects.  It sits under my screen or on the table with players. In WLED it uses the default starting channel of 0, and has 1 segment.
- a vertical lightbar (LightBar2) with a 1m 60 LED strip inside.  This bar shows the hull strength as a variable from 1-100 using red light.  As the hull takes damage, the light ticks down like a thermometer dropping.  This bar is attached to the left side of my projector screen. In WLED it uses the DMX Start Address of 16, and has 1 segment.   
- a vertical lightbar (LightBar3) with a 1m 144 LED strip inside.  This bar separately shows front and rear shield strength as a variable from 1-100 using blue light.  As the shields takes damage, the light ticks down like a thermometer dropping. It ticks down from the top for front shields, and from the bottom for rear shields. This bar is attached to the right side of my projector screen.  In WLED it uses the DMX Start Address of 31, and has 5 segments. The segments include the two blue variable segments and three solid white segments used as dividers so that players can see where the shield levels are ticking down from.

The **[hardware]** lines of the hardware.ini just tell EE to communicate with a sACN device.  sACN broadcasts over the whole network via UDP.  You do not need to (read: cannot) specify the addresses of your devices.

The **[channels]** lines defines the channels that EE will use when sending DMX data to devices.  Because we configured WLAN to use the "Effect" mode, we need 15 channels **per segment** used.  The maximum amount of available channels is 512.  In my hardware.ini, you'll see that I had to have five separate channel lists for LightBar3 because it has 5 segments.

The rest of the data in hardware.ini defines various **[state]** and **[event]** effects which actually make the lights do what we want. 

#### Simple state
```
[state]
condition = HasShip                     
target = LightBar3Top
value = .7,0,0,0,0,0,1,1,1,0,0,0,0,0,0
```
This block specifies the condition (always on if the players have a ship), the target (one of the segments of LightBar3), and the value, which is the code being sent to the 15 channels defined in **[channels]** for that device.  The 15 channels are as follows:
```
1	Master Dimmer
2	Effect mode ID
3	Effect speed
4	Effect intensity
5	Effect palette ID
6	Effect option
7	Red Primary
8	Green Primary
9	Blue Primary
10	Red Secondary
11	Green Secondary
12	Blue Secondary
13	Red Tertiary
14	Green Tertiary
15	Blue Tertiary
```
so, in the example above, I'm using .7 to control the total brightness, the effect "0" which is known as "solid" in WLED, and my Red, Green, and Blue Primaries are all set to 1, creating white.  Effect speed and intensity are not used because effect 0/Solid doesn't do anything with those.

#### slightly less simple event
I also want my HorizontalBar1 to flash whenever the ship takes hull damage.  For this, we'll use the following code:
```
[event]
trigger = <Hull                         # When our hull is damaged generate a red flash
target = HorizontalBar1                     
runtime = .1
value =  .4, [1], [255], [255], 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0
```
Here we have a trigger telling this event to fire when the hull value foes down.  The target is HorizontalBar1, and now we specify a runtime to say how long the event should last.  In the value I'm using .4 for overall brightness, effect mode "1" which is known as "Blink" in WLED, and now I'm setting the effect speed and intensity to [255] so that they both go as fast as possible (but only for .1 second).  This gives me a single flash when hull damage is taken.

#### more complex state
Finally, let's look at the Hull Strength bar on the left.  This state utilizes EE's "variable" effect in the state definition and pairs that with WLED's "Percent" effect.
```
[state]
condition = HasShip              # Red light tracking percentage of hull left
target = LightBar2
effect = variable
input = Hull
min_input = 0
max_input = 100
min_output = .1,[98],[255],[0],0,0,1,0,0,0,0,0,0,0,0
max_output = .1,[98],[255],[100],0,0,1,0,0,0,0,0,0,0,0
```

I'm using .1 brightness because blue is really bright in a dark room, then effect mode "98" which is known as "Percent" in WLED.  I use a speed of [255] for instantaneous filling, and effect intensity is variable between [0] and [100], which corresponds to the min and max inputs. So as EE tracks the decrease from max_input to min_input as shields take damage, the corresponding percentage of output is controlled by the "Percent" effect and channel 4 (effect intensity).  




 








