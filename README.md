
# Background

---

I bought a Pioneer head unit a while back to bring some modernity, mainly Android Auto, to my 2006 Miata. However, I am a chronic song skipper. And while the modern touchscreen interface appeased me for a little while, I soon found the lack of a dedicated physical button for skipping to grate on me. 

Now the user manual does show an option for a remote control that is ready to use; Amazon clone units could be purchased for less than $12. 

![[Pasted image 20250531205146.png]]

But there are a few flaws that made it a no-go for me. 
- It uses a lithium coin cell battery
	- Manual advises to not let leave the remote in the car. And I don't want to tempt fate.
- Communication is via infrared light
	- Top down driving would render it useless.
- There are more buttons (ie distractions) than I need
	- I want an obvious and tactile interface as I only use 3 or 4 functions

The unit supports a wired controller but I couldn't find any specifically for a car. This is mostly intended for adapting steering wheel controls. My base model Miata doesn't come with steering wheel controls. A marinized wired Pioneer controller exists for $100 but support for the car unit isn't explicitly stated.

I considered buying the steering wheel controls since it includes cruise control, but these are at least $200 used and require an additional $60 adapter to the head unit. Just didn't seem worth it for my needs. For all these reasons, making a custom wired controller made the most sense.

## Research

There's this post about using a digital pot to generate resistance values. I used this to get the required resistance values.

https://forum.arduino.cc/t/steering-wheel-remote-audio-control/223878/4

![[pioneer_remote_connection_diagram.gif]]
![[d7e74883cce6e93dbf359f92451eba14dcfc4b05.gif]]
A potentiometer and DMM let me verify resistance values. Volume, prev/next track, mute and source/off registered with my unit. Display and band/escape didn't work. 

I only really care about volume and track control but will bake in a 5th button in case I need it.
## Design

I'm a fan of the tactile feedback that a d-pad provides and other vehicles use something similar for volume/track controls.

In order for the D-pad to function, a gap is required for the plate to push onto a button. I considered adding a spring for it to self-center but the required play didn't bother me as much as I expected once I printed it.

I went with a molex microfit connector for the board. The mating plug is terminated onto a 3.5mm headphone jack (I snipped the cord off of the free airline earbuds)

Schematic is effectively a subset of the one from the referenced forum post. The pad could be forcibly flexed to parallel two or more resistors. This has the side effect of achieving the mute function or no command is registered at all. No danger of damage and no practical issues when it comes to usage.

# Build

The following functions are supported:
- no buttons pressed: infinite resistance
- volume up: 16 kOhm
- volume down: 24 kOhm
- source/off: 1.2 kOhm
- tune up or next track: 8 kOhm
- tune down or previous track: 11.2 kOhm

I tucked the wire from the head unit into the plastic trim over the transmission area.
## Housing

Recommended print out of ABS/ASA 
Use 4x M2x5mm self tapping screws for the housing.

![[Pasted image 20250531175459.png]]
![[Pasted image 20250531175742.png]]
## PCB

Resistors are 1% 0805.
- [24k Ohm](https://www.digikey.com/en/products/detail/yageo/RC0805FR-0724KL/727756)
- [16k Ohm](https://www.digikey.com/en/products/detail/yageo/RC0805FR-0716KL/727620)
- [8.06k Ohm](https://www.digikey.com/en/products/detail/yageo/RC0805FR-078K06L/728145)
- [11.3k Ohm](https://www.digikey.com/en/products/detail/yageo/RC0805FR-0711K3L/727554)
- [1.2k Ohm](https://www.digikey.com/en/products/detail/yageo/RC0805FR-101K2L/14008301)
- [tactile switch](https://www.digikey.com/en/products/detail/e-switch/TL3301NF160QG-KR/271564)

![[2024-04-21_pioneerRemotePCB-schematic.png]]
![[2024-04-21_pioneerRemotePCB-top.png]]![[2024-04-21_pioneerRemotePCB-bottom.png]]
## Installation

I recommend placement near the shifter. It's a natural place for your hand/arm while driving. Use VHB or 3M dual lock tape. The adhesive has held on strong through the summer heat.
![[pioneerRemoteControl-02_2025-05-31.jpg]]
![[pioneerRemoteControl-01_2025-05-31.jpg]]
