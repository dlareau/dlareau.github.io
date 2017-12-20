---
layout: blogpost
title: "The History of Cluster Counter"
category: cluster_counter
published: false
---

Humans complicate everything...

I've been populating my website's ["Projects"](/projects) section, and when it came time to make a page for Cluster Counter, I basically started typing out the story below. Realizing that most of it was actually very far from the technical details of the project, which is what I wanted on that page, I decided to make the story this post instead. 

A bit of background information. Carnegie Mellon offers a number of computing facilities to students, one of which is a number of computer labs where students can go to get work done. Some have their stigmas and to an extent their social cliques, but none more than the Gates Hall 3000 cluster. The Gates Hall 3000 cluster or "G3K" or "cluster" as many of the inhabitants called it, was special for a few reasons, not the least of which being that almost all of the walls in the cluster were whiteboards. The most prominent thing about this cluster though, was that it was a self dubbed "social cluster", a place to hang out, chat, rest, discuss interesting thoughts/problems, and maybe if you are lucky, get work done. This social culture was a far cry from the normal library-esque feeling of most other computer clusters on campus, and this allowed many many silly things to come to pass in this cluster. 

{% include image.html url="/assets/images/blog/cluster_overall.jpg"
description="It isn't nearly that spacious in real life." %}

{% include image.html url="/assets/images/blog/cluster_art.jpeg"
description="An example of what the walls usually looked like." %}

One of the silly things that came to pass started when I brought a small mechanical counter that I had salvaged from an old piece of machinery into cluster. 

{% include image.html url="/assets/images/blog/cluster_counter_manual_new.jpeg"
description="V0.1: What it would have looked like when new." %}

How it worked was simple, depress and release the lever on the right and it would increment the display by one. If you turned the knob on the left it would reset by first setting the numbers to 11111, then 22222, all the way up to 99999 where it would wrap to 00000. I first brought it into cluster as sort of a fidget toy for myself, the mechanical action and click of the lever each time it incremented was a nice mental distraction. Soon though, someone noticed the small device and wanted to see what it was and try it for themselves. After it got passed around most of the group that was in cluster at that point, someone said "I wonder how high we could get it as a group". Thinking that was a good idea, but not wanting the relatively small device to get thrown away, I screwed it to a block of wood and made its purpose obvious. Cluster counter was born:

{% include image.html url="/assets/images/blog/cluster_counter_manual.jpeg"
description="V1.0: Not the prettiest thing." %} 

Like the lead-in says though, humans complicate everything. The local anarchists of cluster quickly got to spinning the reset knob to either clear the progress or set it to something like 11111 then click it a few times to make it look like we had achieved 11148. Feeling that was against the spirit of the challenge, I came up with a quick fix.

{% include image.html url="/assets/images/blog/cluster_counter_manual_2.jpeg"
description="V1.1: 'Security patch'" %} 

People could still somewhat reach in the end of the nut and twist the knob as evidenced by the value in the photo, but it stopped most activity of the reseting variety. As with a few things that come into cluster, the counter got a bit of a makeover and it also received some additional tamper-proofing.

{% include image.html url="/assets/images/blog/cluster_counter_fancy.jpeg"
description="V1.2: 'UI update'" %} 

And that is how it pretty much stayed for about a month until it went missing during some renovation and failed to return. Jump forward two months, students were returning from winter break, and some people were missing the counter. I was itching for a small electronics project at this point, so of course I made an electronic version. Lacking a nice pushbutton for a physical interface, this version would be web based. See the [project page](/projects/cluster_counter) for more details, but it was basically a number of seven segment displays hooked up to an Intel Edison that would poll a file on the internet every second or so and update the number on the display. Along with some helpful text telling people where to go, and a tiny web script, the counter was reborn.

{% include image.html url="/assets/images/blog/cluster_counter_wall.jpg"
description="V2.0: Now with more electrons!" %} 

I can't believe I thought 