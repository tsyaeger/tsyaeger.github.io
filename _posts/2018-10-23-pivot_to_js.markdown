---
layout: post
title:      "Pivot to JS"
date:       2018-10-23 22:07:34 -0400
permalink:  pivot_to_js
---


Being that the javascript/Rails project was my first attempt at building anything js top to bottom, there were plenty of lessons that I learned, big and small. 

The project was slow-moving at first and I quickly realized that I needed to supplement the coursework, so I spent a significant amount of time on js/jquery/ajax tutorials. These were most helpful to me:

Js in the browser and asynchronous js sections:   https://www.udemy.com/modern-javascript/

Rails/JS playlist:  https://www.youtube.com/playlist?list=PLm8ctt9NhMNV5X3s8n3x3uNyqh7bk9L8s

Once I was up and running it became clear that I needed to focus on my coding process. I tended to work too much in my text editor, which I’m sure is not uncommon for people adding js to their repertoires. But once I started habituating myself to spending time in the browser and I added a few console tricks, my process became far more efficient.

All in all, here are some of the most valuable lessons I learned:

Mistake:  I overused js because I was so excited to practice using it. I used it to format and render basic elements of pages that I had no intention of making dynamic. I ended up having to revamp and it was a pain.
* Lesson:  Don’t just dive in, unless you don’t mind spending a lot of time undoing things. Identify areas where your js is appropriate.


Mistake:  At times I had difficulty understanding what was being returned by my code. I used debugger but wasn’t exactly sure what was going wrong.
* Lesson:  For on the fly testing use console.assert(test condition, ‘your msg’)  to specify the return values that you’re looking for.


Mistake:  I didn’t have a handle on my JSON data.
* Lesson:  Use the JSON viewer extension and console.table(data, [‘col1’, ‘col2’]), which shows a sortable table of your data.


Mistake:  I used a few global variables.
* Lesson: Don’t ever use global variables—just wrap them in anonymous functions. No big deal. (And make sure to declare variables so that they don’t become global.)


Mistake:  Wasting my life searching line-by-line through html elements.
* Lesson:  To find an element use 'inspect' in the console:   inspect ($(‘#myId’))


Mistake:  I spent way too much time endlessly going back and forth from console/elements/page/text editor because I didn’t know…

* You can edit js code in ‘sources’ by clicking the js file in the js folder and then you can save the edited code.

* You can edit a document on the page by using:  document.body.contentEditable=true  in the console and the code, itself, will change along with it.

* You can select an element, return to console and write $0 to grab that element, or $1, $2 and so on, to get the element(s) selected previously.  E.g., 1) select some element on the page, 2) var x = $0,  3)  x === that random thing on the page you selected

* You can move elements by dragging!

* You can see all listeners attached to an element with:  getEventListeners(‘#myId’)

Oh, and if you haven't already, you should checkout Chrome’s devtools debugging tutorial: [https://developers.google.com/web/tools/chrome-devtools/javascript/]

