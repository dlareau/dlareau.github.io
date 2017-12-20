---
layout: project_page
title: Puzzlehunt CMU Webapp
category: puzzlehunt_server
---

A webapp for Puzzlehunt CMU's bi-annual puzzlehunt, that serves the dual purpose of being a general purpose webpage for the club and being a webapp that manages most of the difficult aspects of running a puzzlehunt. 

You can check out the public facing version at [http://www.puzzlehunt.club](http://www.puzzlehunt.club).

This project started when I was handed an old server, written in Go, which didn't keep any sort of history, supported roughly 1/3 of the current features, and had to be minorly re-written for every hunt. From the pain of having to re-write it for two semesters, I decided I was going to write my own server with three main goals in mind:

- The server, like the server before it, will likely outlast its creator's time at CMU, and therefore should be written in a common programming language, in a common and well tested framework, and should be able to run almost entirely without interaction with the code. I don't want this to have to be re-written when I leave because nobody could manage it without me. 
- The server should automate as much as physically possible about running a puzzlehunt and should make anything that isn't possible to automate easier to do manually.
- The server will have a history of old hunts. Any person should be able to go back and view (and even play) old puzzlehunts.

<br>

To this end, I have worked on this server for a number of years now, and it has grown to have an amazing feature-set:
- **Shibboleth Sign On:** Shibboleth supported login for CMU and Pitt affiliates, with a backup of local website accounts for non-shibboleth users.
- **Automatic Puzzle Pages:** The server automatically generates a page for each puzzle that lets you preview the puzzle, download a PDF copy, and submit answers and see feedback without refreshing.
- **Automatic Answer Response:** An automatic answer response system that supports custom responses per puzzle and a regex answer detection system for multiple correct or wrong answers. 
- **Team Support:** The ability to securely create, join, and leave teams for each puzzlehunt, with users allowed to be on only one team per puzzlehunt but many teams across puzzlehunts.
- **Customizable Puzzle Unlocking:** The ability to have a customizable puzzle unlocking structure for each puzzlehunt. Supports any structure that can be represented as a directed graph with puzzles unlocking at a certain number of active in-edges. 
- **Automatic Page Access Control:** Various parts of the site such as the current puzzlehunt pages, the staff pages, and previous hunts have built in access control that allows access based on date, time, and account level (Admin, Staff, Playtester, Normal User, Anonymous User). Access for pages in most scenarios is automatically determined based on page type. 
- **Comprehensive Admin Control Pages:** A set of pages that allow for complete control of the server, with everything from attribute editing of every server object to higher level control such as unlocking puzzles, correcting automatic answers, chatting with teams, and launching batch operations. The admin pages also allow for various high level views into how the hunt is going and how teams are doing.
- **Staff Chat:** People participating in the puzzlehunt can chat with staff through a built in chat page. The staff's chat window allows easy viewing and responding to all teams. 
- **Automatic File Management:** The webapp only requires the puzzle author to provide a link to a PDF when creating a puzzle. The server can then upon request of a staff member, securely download all linked PDFs, render them to PNGs for in-page super compatible displaying, and securely serve them in a manner such that only teams who have unlocked the corresponding puzzle can see the files. 

The site is broken into three parts:

### Public facing pages ###
{% include image.html url="/assets/images/projects/puzzlehunt_homepage.png"
description="The homepage" %}

The public facing pages are pretty much just super simple templates with some some relevant information being automatically inserted in some locations, such as the current hunt on the homepage.


### Staff pages pages ###
{% include image.html url="/assets/images/projects/puzzlehunt_progress.png"
description="The progress page" %}

{% include image.html url="/assets/images/projects/puzzlehunt_queue.png"
description="The submission queue" %}

As mentioned in the feature list above, the staff pages allow the people who run the hunt to get a good overview of how the teams are doing, how the puzzles are going, and control almost every aspect of the currently running hunt. 

### Puzzlehunt pages ###
{% include image.html url="/assets/images/projects/puzzlehunt_puzzle_page.png"
description="One of the automatically generated puzzle pages" %}

All the things a user would need to interact with during the hunt, including a main page listing all the puzzles, an automatically generated page for each puzzle, a page with all unlocked items, and a "chat with the staff" page. 