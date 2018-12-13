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
look official enough for public play. Quickly settling on acrylic, I realized
there was a second issue with the current module system, with the modules
slotted in, there were visible gaps around the sides of the modules. This is
really a problem because the module front-plates were the same size as the
module boxes which were the same size as the module holes. Tolerance control
could make this better, but nothing but a design change could fix this. 

Credit to my housemate Ethan, who does part design like this for a living, for
suggesting that I just make my module front plates larger than the box and the
hole that they modules go into, hiding any imperfections in sizing. This had 2
problems: I needed to adjust the height of divider because the front plates
would not sit proud rather than flush, and that I had already printed many of
the front plates and it would add another week to production to reprint and
remake them in a larger size. Luckily, none of the modules used the outer 4mm of
space on the front plate, so I just shrunk the box and the holes by 4mm to now
have the front plates overhang the boxes. 

With all that in mind, and some quick manufacturing later (and another thanks to
Ethan for access to a good laser cutter), I had a shiny new divider and front
plate.

{% include image.html url="/assets/images/blog/ktane_new_divider.jpg"
description="Well, not so shiny with the paper on" %}

{% include image.html url="/assets/images/blog/ktane_divider_underside.jpg"
description="Took this opportunity to add some channels to route wires in" %}


### Final Modules ###

With the new front plate finished, I doubled down on finishing the remaining
modules. My plan for PAX was just enough to fill all six slots, meaning one
master module and 5 playable modules. At this point I already had basic wires,
memory, and simon says completed from back in July, and I needed to make the
master module, morse, and switches as those were the modules I already had code
for. 

Switches was quick and easy, the only real issue I ran into was that the
switches themselves were taller than the space allowed in the lid of the
briefcase when closed. That was easily fixed with some sanding and polish work
and allowed me to keep these blue switches which had a great tactile feel to
them. 

Morse was a lot harder because of all of it's aesthetic elements including the
"MHz" light up area, TX button, frequency meter, and flashing half-cylinder. 

{% include image.html url="/assets/images/blog/ktane_morse.jpg"
description="Progress picture before the frequency meter was finished." %}

Most of these elements I have Ethan to thank for their completion, he has access
to a vinyl cutter which helped make the "TX" for the button as well as the
negative covering for an orange piece of plastic for the "MHz" light up area. He
also helped make the half-cylinder that blinks out the morse code itself. While
I could have made an attempt at a number of these design elements myself, we
were working on this right up until the night before PAX and his help was what
got this project finished in time. 

### Live at PAX! ###

After working right up until and including the Thursday we left, I put the six
finished modules in the briefcase. Packed a pelican case full of repair
equipment and proceeded to spend the next 5 hours in the car to Philly.

I spent the first part of Friday just enjoying the convention and figuring out
what the best way to get the device into the convention without ending up in
handcuffs. After chatting with both my friend who was volunteering as an
enforcer for the convention and the very helpful PAX info desk, they gave me
some advice about how to bring it through the security checkpoint as well as
their phone number to call if there were any questions.

After going back out to my car, getting the game and arriving back at the
security checkpoint, everything turned out easier than expected. Making sure to
give a quick explanation to the person operating the checkpoint, showing them
that there was nothing malicious in/under each module, and ensuring that I never
used the words "bomb" or "explode" in the conversation. It would seem that I had
actually polished the game enough to the point where I guess it just looked like
a game, and the bigger issue getting the through the security checkpoint was
actually the pelican case full of repair materials and spare parts. 

Despite going through all of that, Friday ended up just being a few rounds of
playtesting with my friends, finding a few bugs, and then fixing those bugs so
that I had a presentable version the next day. This was actually the point at
which I found out about the same-address issue with the DSerial library.

I woke up sunday morning, re-programmed all the modules with the software fixes
from last night, gave each module a good testing, and then glued in some of the
modules more likely to get tugged out by users. It was game day! I again took
the morning to myself to look around the con, but just after a late lunch I went
through the same security checkpoint ritual, went into the main free-play area,
found a table and set up camp. At this point I'll let a few tweets tell the
story. 

{% include tweet.html 
url="https://twitter.com/DLareau22/status/1069002815647952896" %}

{% include tweet.html 
url="https://twitter.com/DLareau22/status/1069004203224383488" %}

{% include tweet.html 
url="https://twitter.com/DLareau22/status/1069030055098150912" %}

{% include tweet.html 
url="https://twitter.com/DLareau22/status/1069042892138840064" %}

{% include tweet.html 
url="https://twitter.com/DLareau22/status/1069063126274981893" %}

I really enjoyed being able to show it off, and the reactions I got from people
at the convention definitely made the whole effort worth it. 

### The future ###

Development continues! I've mostly been working on these blog posts and
other things since PAX, but now that I'm up to date, expect to see more work on
other modules, version 2, and design in the coming months. First up is an
attempt at moving modules to PCB's and the Password module. I'll try to post at
least once every two weeks, but no promises. 

- Dillon