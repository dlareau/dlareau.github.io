---
layout: blogpost
title: "KTANE: Physical Edition - Road to PAX"
category: ktane
published: false
---

A computer scientist’s main challenge is not to get confused by the complexities of their own making. -Dijkstra

**A disclaimer: There is not now, nor will there ever be anything dangerous 
about this project. This is not actually a bomb, just a game replica.**

If you're reading this and don't know about this project or the game *Keep 
Talking and Nobody Explodes* you should check out either the 
[project page](/projects/KTANE_physical) or the 
[announcement post](/blog/2018/07/07/ktane).

This post is going to be long and jump around a bit, covering various aspects of
coding, manufacturing, and debugging I went through on the way to version 1 and
its showcase at PAX Unplugged.

### Debugging/Issues ###
As mentioned in the last post, in order to overcome some issues surrounding
communication between the modules I made my own protocol called DSerial that
fills in layers 3 and 4 on the OSI Layer model. It provides master/client style
communication as well as various benefits such as message retry upon failure and
identification of clients on the network. The downside to having to write your
own communication library? Having to debug your own communication library. 

In the early days of writing the library I was happy that anything was happening
over the serial port but as things progressed I needed some way to see exactly
what was happening on the line. Things were easy when everything worked because
the two arduino's I set up would send/receive messages using DSerial on a
software serial port and echo those results to the hardware serial port for
viewing on the computer. When things weren't working I tried a number of things
including trying to view the communication using a third arduino's hardware
port and using the UART decode functionality of my Rigol Scope. Eventually
though I settled on a cheap $15 logic analyzer I had gotten off of the internet.

Initially I tried to just use the built in UART decoder to read the packets, but
that quickly became really tiring. I wanted something that would actually show
the layer 3 and layer 4 traffic in human readable terms. After a quick attempt
at making a custom protocol layer in Saleae's software I gave up due to the
complexity needed just to get off the ground. Looking around at other
alternatives I noticed sigrok and in particular their easy to use protocol
framework. Less than 2 hours later I had a first version of the 
[DSerial sigrok decoder]
(https://github.com/dlareau/KTANE-physical/tree/master/sigrok/dserial_decoder). 

{% include image.html url="/assets/images/blog/ktane_sigrok.jpg"
description="Clearly labeled information."%}

Having a decoder like that not only helped me finish the library, but also
greatly reduced debugging time throughout the rest of the project whenever a
module was acting up. 

In the two weeks leading up to PAX, I discovered two more bugs in the DSerial
protocol that have yet to get true fixes. The first being that if the master
ever has to send more messages than the length of the circular queue used for
storing messages holds (even if they aren't all in the queue at the same time)
the protocol hangs. That was solved temporarily by just increasing the queue
size to be greater than the master will ever send in a single game of KTANE. 

The second bug isn't really a bug but more of a design issue with the library.
I quickly found out through lazy copy and pasting that if two clients have the
same address their conflicting traffic can somehow take down the rest of the
network. I plan to solve this eventually by having some backoff followed up by
the ability for live-address reassignment by the master module. 

### A better case ###
As the image below shows, after getting a good bit of this done back in July, I
basically sat around for 4 months getting distracted by other things like
Puzzlehunt, my actual job, and some particularly enticing videogames. Then
November hit and I was struck with the reality that if I wanted to show this off
at PAX unplugged I had to start making it much more presentable. 

{% include image.html url="/assets/images/blog/ktane-commits.png"
description="Some other things got in the way..." height="150px"%}

The first thing that had to go was the foamboard divider. I had originally
considered just giving it a black paintjob but later decided that still wouldn't
look official enough for public play. 


Foamboard not good enough for pax.
Gave up on bottom encasements, settled for bezel overlap
Ethan helped cut acrylic
Routed channels for wires
One painful cable soldering later...

### Final Modules ###
Knocked out last 3 modules in around 2 weeks
Mention ethan for morse


### Live at PAX! ###
Security
Saturday test-play and debug
Security
Sunday test-play and photos
