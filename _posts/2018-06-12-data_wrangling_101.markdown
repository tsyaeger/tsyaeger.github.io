---
layout: post
title:      "legislation wrangling 101"
date:       2018-06-12 23:42:45 -0400
permalink:  data_wrangling_101
---


Even if you're one of the small minority who knows their state representatives, it's very unlikely that you know what they’ve been up to. Do you know what bills they’ve authored or how they’ve voted on certain bills—bills that you might care about if you even knew that they existed? Do you know what bills have upcoming votes and how to voice your opinion to your representative? Me neither.

This is nothing to blame ourselves for.  All of this information is buried in disparate places and is pretty difficult to understand when you get your hands on it. That’s one of the reasons that I decided to create this little program for my cli data gem project. I think that we should be able to decrease the amount of energy that it takes a typical person to participate in the political process, and I think that we developers can be part of that solution. 

This program allows you to find your reps by district/party/house and to view the bills they’ve authored along with brief descriptions. The user can also choose to route to a representative’s contact page or to a bill’s detailed info page. It’s just a start, but it was very cool to see the info become more manageable as I moved forward bit by bit.

My first step in building this program was to learn a bit about California state government, which was essential, not just because I’m new to the state, but because the jargon and constant use of abbreviations (without keys) made the info nearly illegible. After that I scraped the legislation website gathering basic info on each bill as well as links to each individual bill. Next came the senate and assembly rosters with contact links to each representative. Scraping completed! 

At that point I created domain objects for bills, representatives, and parties and connected them all. I then created the command line interface allowing the user to access the information in a variety of ways by looping over a basic menu. Finally, I spent loads of time refactoring and breaking and fixing and refactoring. It could have gone on forever. It's tough knowing the right time to just put it down and press submit.
