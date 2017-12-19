---
layout: project_page
title: Daily Walk Bot
category: daily_walk_bot
---

My first twitter bot!

To get the links out the way quickly: [Twitter account](https://twitter.com/DailyWalkBot) and [Github repo](https://github.com/dlareau/dailywalkbot).

I wrote most of this bot my senior year of college because I was bored and thought it would be cool to write a twitter bot (Upon further reviewing history, I apparently did it to procrastinate from homework). 

The bot was inspired by an idea my friend Owen had about a leaf blowing around and tweeting it's location. I liked the idea of the random traveler and adopted the format to be a random walker. Using a simple python twitter API, [tweepy](http://www.tweepy.org/), and the google maps API, I threw together a script that would generate a random walkable path using google maps and tweet details about it. A few iterations later, I had made it walk a random path each day made up several smaller random paths each of which was tweeted out as the destination location text, an image of the destination in google maps, and a link to the google maps pinpoint. It is important to note that it would tweet these segments out in real time. If it took 2 hours for the segment it just tweeted to be walked according to Google maps walking directions, the bot would wait 2 hours before making the next tweet. 

This worked great for a day or two, but I had it starting at my house each day and going from there, which quickly got repetitive. The initial motivation was that if I wanted to, I could actually follow these walking directions one day and it would be a nice full day walk. I quickly gave up on that idea and in a landslide [poll victory](https://twitter.com/flybye22/status/705086752797691904) the bot was changed to continue its journey wherever it left off the previous day, hopefully going on some epic journey. And boy did it go: 

{% include image.html url="/assets/images/projects/daily_walk_bot_progress.png"
description="Progress as of 12/19/2017" %}

As you might notice, there are some trends to the random path. I get to control the general direction that walkbot travels and not much more (Technically I control the weighting of all 4 cardinal directions). I've used this to make it bounce nicely around the US. 

Some interesting interactions along the way:
{% include tweet.html url="https://twitter.com/DailyWalkBot/status/711958236975472642"
description="Walkbot visits Hershey Park" %}
{% include tweet.html url="https://twitter.com/DailyWalkBot/status/719168184104939520"
description="Walkbot takes a ferry to cross the Hudson" %}
{% include tweet.html url="https://twitter.com/DailyWalkBot/status/720372267390251012"
description="Walkbot decides to visit Long Island via ferry" %}
{% include tweet.html url="https://twitter.com/flybye22/status/722849890091401216"
description="I get sick of how many ferries walkbot is taking..." %}
{% include tweet.html url="https://twitter.com/DailyWalkBot/status/722963589930340353"
description="Walkbot changes direction for the first time" %}
{% include tweet.html url="https://twitter.com/DailyWalkBot/status/750026761652543488"
description="The internet decides the next direction" %}
{% include tweet.html url="https://twitter.com/DailyWalkBot/status/778361848097824768"
description="Walkbot leaves the US for the first time" %}
{% include tweet.html url="https://twitter.com/sierracountynm/status/831617547757899778"
description="Walkbot interacts with local government after getting stuck" %}
{% include tweet.html url="https://twitter.com/DailyWalkBot/status/833700573866246144"
description="Second time leaving the US, this time with more Mexico" %}
