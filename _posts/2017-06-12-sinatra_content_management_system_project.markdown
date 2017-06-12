---
layout: post
title:  "Sinatra Content Management System Project"
date:   2017-06-12 14:27:37 -0400
---


This time around, I felt more prepared to do a project. I had just finished working on the last Sinatra labs and projects in the section, so I was much more comfortable with the idea of building a CRUD app. CRUD stands for Create, Read, Update, and Delete, which are the main functions that a CRUD app should be able to do. At first I was tempted to do something related to my favorite hobby, knitting, but I figured that was narrowing my potential user range. So I decided on a simple parts content management system which I have wanted to do for my husband’s small business. With this system, a user can sign up, or login if they’re a current user, and add parts to a simple sqlite3 database. Then, as the user needs to, they can add more parts, edit/update specifics for individual parts, and delete parts. It is built in a generic way so the parts could be for anything from auto parts to airplane parts to lawnmower parts, etc. As long as you have the name of the part, the serial number, manufacturer, and quantity that you have on hand, you can add a part to your database.

A few things that I learned during this process are:

1. You should really write out and diagram your table relationships and all of your model relationships before trying to start your migrations. Having it all there to reference will help tremendously and you will be ready for the next step easier and faster.

2. If your associations between your models are not set up/written correctly, your experimenting in Pry or Tux will not be that successful. It doesn’t “just work” like it does for Avi in the videos if the foundation isn’t laid correctly. You will have a hard time figuring out what to put into your routes and your “Views” to get the app to display what you want. The belongs_to, has_many, and has_many through can work for you, but you have to completely understand what they do for you and how they relate to your own models. 

3. If you want to add a CSS stylesheet to your project, you’ll need to add a public folder for it to go in or Sinatra will NOT acknowledge that it’s there. Or, you can specify a different location by setting it in your Application Controller. The websites below helped me understand this so I could add some color and a little bit of formatting to my layout.

https://medium.com/@kerenlerner/how-to-include-images-css-and-or-javascript-in-your-sinatra-web-application-45e2ebbfa75f

https://www.davidwparker.com/2009/11/13/sinatra-base-static-file-issue/
