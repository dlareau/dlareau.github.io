---
layout: project_page
title: Keep Talking and Nobody Explodes - Physical Edition
category: ktane
---

**A disclaimer: There is not now, nor will there ever be anything dangerous about this 
project. This is not actually a bomb, just a game replica.**


Released in July of 2015, *Keep Talking and Nobody Explodes* focuses on the
disarming of a virtual bomb where one player plays the "Defuser" and any number
of players play the "Experts". There are a number of different "modules" that
each need disarming to win. Each module has some component of information that
is only clear to the experts. The catch is that the experts are physically
separated from the defuser and cannot see the modules, making communication
important. Shortly after release, my friends and I became obsessed with the
game, drilling the modules until we could tackle even the hardest of bombs,
racking up hundreds of plays.

Jumping forward to 2018, in a story you can follow more in the blog posts below,
I decided to start making a physical version of the game. The goals for this
project are:
- It must be fully playable.
- It must be fully modular.
- Whenever possible, it must replicate the look/play of the game accurately.

Starting some time in June, and with a few delays, the first playable
version was finished at the end of November, just in time for me to bring it to 
PAX Unplugged to show it off.

<div style="text-align: center;">
	<div><i> Gallery: </i></div>
	<blockquote class="imgur-embed-pub" lang="en" data-id="a/J6HdM0v"><a href="//imgur.com/J6HdM0v">Keep Talking and Nobody Explodes - Physical Edition</a></blockquote><script async src="//s.imgur.com/min/embed.js" charset="utf-8"></script>
</div>

{% include tweet.html 
url="https://twitter.com/DLareau22/status/1069002815647952896" description="" %}

Development on this project continues, which you can follow through both the
blog posts at the bottom of this page and the 
[github page](https://github.com/dlareau/KTANE-physical) for this project.

### FAQ ###
**Why did you do this?**  
Making things like these is my hobby, this project is/was just something I do
for fun in my spare time. 

**Are you going to make more than one? / Are you going to sell these?**  
No. Unless contacted by Steel Crate Games to expressly do so, this project will
remain one of a kind and a purely non-commercial effort. I do not own the 
copyright for Keep Talking and Nobody Explodes and I don't feel like getting
sued.

**Has anyone else done this before?**  
There have been a number of projects with similar goals, but all of the ones I
can find either:
- Did not attempt to directly replicate the game because they wanted to sell
their product.
- Fell off in development before finishing any significant number of modules.
- Did not attempt any appreciable level of playability polish (i.e. never made 
it off breadboards)

I could have missed something though, so if you know about another similar 
project, let me know!

**Did you have any help making this?**  
I could not have made some of the physical elements of this project without the
amazing help of my friend [Ethan Gladding](http://www.egladding.com/). He
helped with design and manufacturing of many small aesthetic touches such as the
acrylic backpanel and the morse module diffuser.

**Are you going to make more modules?**  
Yes, you can check out the 
[github page](https://github.com/dlareau/KTANE-physical) to see which modules
I am planning to build. 

**Why aren't you making [Insert module here] module?**  
If you don't see an original game module listed, I probably thought it
infeasible to replicate physically. One that comes to mind is wire sequences
where panels of wires magically appear from inside the device. While there are 
ways to make almost any module just using a screen, I feel that defeats the
point of the "physical" version.

**I don't want to read github, give me a technical summary!**  
Each module (including the controller module) is controlled by an Atmega328p
Arduino Nano clone. Due to design constraints, the modules talk over a 
multidrop serial bus using a custom protocol developed for this project called
DSerial. Configuration of stuff like the serial number and time remaining is
handled through a web interface run by an ESP8266 connected to the controller
module.

---
Disclaimer:  
I am not endorsed by, directly affiliated with, 
maintained, authorized, or sponsored by Steel Crate Games.

---