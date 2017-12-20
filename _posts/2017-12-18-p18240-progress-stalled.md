---
layout: blogpost
title: "The 74XX P18240: Progress Stalled"
category: p18240
---

Turns out this is harder than I initially thought.

As part of this blog's revival, I feel that I owe an update on the project that was a lot of this blog's initial content. The short version of this update is that this project is on hold until I get a good bit of time to make a few major design decisions and source some parts. 

There were a few things that made me stall this project:
#### Fan out ####
I realized that for things like the ALU, the output would be driving around a dozen other circuits. After looking at the current draw of most 7400 series chips and the max output current of the 74245 chip I was looking at, I realized I had a problem on my hands. There are a few ways I could fix this, but I haven't had the time to figure out a solution that is easy and true to the original design.

#### Part sourcing ####
After planning out the ALU, I started to see if I could source parts for it, and it turns out nobody is selling a surface mount version of the 74181 ALU chip. I looked for a while and the best I could find was a very large version of the 74181 in a DIP footprint. This made me wonder if I should just give up and use the through hole part, if I should try to make my own ALU out of SMD parts, or if I should make my own 74181 SMD chip by having a microcontroller of a similar footprint programmed to act the same way. As with the other issues here, I haven't really had the time to sort out my feelings on the matter, leaving the ALU kind of stalled. 

#### Bus connection issues ####
I touched a bit on this in the [3rd register post]({{"/blog/2017/05/28/p18240-register3.html" | absolute_url }}), but I ran into some issues when considering how various parts connect. A one of the unsolved issues I have right now is that with flat ribbon cable, having the cable make a right angle via folding flips the connectors. I also have the issue of how to split the bus off to various parts. I had initially thought that having a small board with 3 connectors on it to make a "T" junction would be easy, but it turns out at the small pitch of the FFC parts and the manufacturing limits of the PCB shops, I couldn't route everything properly without making the boards larger than I wanted. These issues pushed me to wonder if I should just do the whole design as one big board, eliminating all of these issues, but like the rest of the things listed here, I haven't really had the time to think this one through properly.

<br>

So there you have it, I need to solve a few things before I start this project again. I don't really feel like it would be appropriate to write the ALU post at this point in time, given how much it might change with the second issue above, but just so there is some cool content in this blog post, have a picture of the very nice looking ALU schematic:

{% include image.html url="/assets/images/blog/p18240-ALU-sch-v2.png"
description="This is actually already version 3."%}

I hope that someday I will come back to this project, maybe I'll make it one of my goals for 2018. 

\- Dillon