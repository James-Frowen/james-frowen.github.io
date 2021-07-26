---
layout: unity_tip
permalink: /unity_tips/networking_definitions/
title: Game Networking Definitions
description: A version of FixedUpdate that will run after all others
date: 2021-07-26
---

Definitions for reducing bandwidth for game networking


# Delta Compression

Sends delta of previous and current values.

### Example

float changes from `10.2` to `10.3` you can represent the change as `+0.1` and then the value can be sent using less byte


# Bit Packing

Bit Packing is writing values to a bit level instead of byte level. For example, Normally bools use a whole byte, but with bit packing they only take up a single bit.


# Float Compression 

Float values can be converted quantised and sent as less bytes depending on the range and resolution needed. 

If using Delta Compression you can reduce the bounds allowing the value to be sent using even less bits

### Example

if your world bounds are only +-64 and you need ~0.015 resolution you can compress a float value to 8,192 discrete values, which will only take up 13 bits.

# Variable Size int

...work in progress...

# Quaternion Smallest 3

Quaternion are made up of 4 float values, so if sent normally they will take up 16 bytes. Because of the rules that Quaternion follow they you can instead send the smallest 3 of these values, and also use Float Compression to bring the size of each of those values down.

### Quaternion Rules
- a quaternions is always normalized (x^2+y^2+z^2+w^2 = 1)
- each value is between 1 and 0
- max value for 2nd largest is 1/sqrt(2) or ~0.707
    - derived from 2a^2= 1

