---
layout: post
title:      "Rails v Sinatra"
date:       2018-08-23 05:47:33 +0000
permalink:  rails_v_sinatra
---


For my rails projects I decided to return to the same app that I built for my Sinatra project, a gif library/messaging service. This process was useful in a couple of ways. 

First, I was able to correct many of the mistakes I made on the Sinatra version. The primary lesson I learned in this regard was that before building anything—any little tiny thing—I first need to clearly envision what I want the final product to look like and how I want it to behave. I too often dive in with a vague idea of what I want, but that leads to a lot of backtracking. 

For example, I redesigned my database schema by first writing out exactly what I wanted to be able to call in regards to associated objects. I wanted to be able to call user.received_messages, user.sent_messages, user.gifs, user.contacts, etc. — and from there I went on to design and build the db. Previously, I started with the diagram, but not the functionality. It may sound simple but it was a game changer for me.  

Second, I learned more about Sinatra and Rails by comparing them side by side. On one hand, the flexibility of Sinatra is exciting in that it’s a blank canvas. You can write whatever routes you want and connect them to whatever erbs you want, you write your own helpers, etc. However, at times I felt like a bull in a china shop. When I look back on my code I regret each and every route name I used. They were all very unclear.

To move from that to the very opinionated/bossy/helpful Rails was beneficial in that I felt that the guidance and strictures kept me more disciplined and guided me through the process. When I look at my Rails code, it is far more readable and easier to jump into after time away. There were fewer occasions to lose my way. Obviously, Rails is very helpful with the forms, links, validations, rending partials, and resource routing, but these methods are also instructive by demonstrating principles and strategies that I can use in whatever code I write in the future.
