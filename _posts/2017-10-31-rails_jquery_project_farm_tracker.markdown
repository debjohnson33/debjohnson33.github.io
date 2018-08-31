---
layout: post
title:      "Rails/jQuery Project – Farm Tracker"
date:       2017-10-31 22:19:02 +0000
permalink:  rails_jquery_project_farm_tracker
---


This is a continuation of my Rails project, just with some jQuery added to it, so the original models, etc. are all the same. A user can have many farms, farms have many areas, and areas have many animals. A farm also has many animals through areas. The first requirement that I did was to add an “on click” handler to a farm’s page to show a list, or index, of the farm’s animals within a div so the page would not need to be refreshed. At first I used a $.ajax request to do this because I was still trying to wrap my brain around the $.get. Listing the animals also revealed a “has-many,” or at least a “has-many, through” relationship to satisfy that requirement.

This seemed way too simple to me, so I added another handler to my “Farms” link at the top of my page to render the index of farms. As I worked through the project, I became more familiar with how to use the handlers and render what I wanted on the page. Another requirement was to render at least one show page, so I did that with the farm’s areas. I was able to do this and put a next button to show the user the next area. This would be something that I would improve on in a later version with a “previous” button.

Next I tackled the idea of translating the JSON responses into Javascript Model Objects. This is actually not as complicated as it first sounded when reading it. In each js file, I wrote a constructor function for that particular model. This gave the ability to instantiate a new instance of that model (let newFarm = new Farm(attributes)) using the data retrieved from the json object so that you can take that data and format it to render it. That’s where the other part of this requirement came in. The use of a prototype method. Each prototype method allowed the use of “this” in the formatting of the data from that particular instance to be able to render it to look like your original html page.

```
 Farm.prototype.formatIndex = function() {
	let farmHtml = `
		<a href="/farms/${this.id}" data-id=${this.id} class="show_link">${this.name}</a><br>		
	`
	return farmHtml
}
```
	
A couple of things to note about these model objects. The attributes that you want to be able to use to render the page need to be listed in that model’s serializer. So when I went to render my animal show page, I had to go back to my animal serializer and make sure everything was listed instead of just a few items. This allows you to customize what you do or don’t want to render.

Last, but not least, was creating a resource and rendering the response with a refresh. This was a little different, but still similar to using $.get. Instead, I used $.post and passed in what was required. I had to read about this in the docs and do things step by step, but once I did, it worked well and I was able to create a new entry in the database. 

I definitely had to get used to using either console.log or debugger, or both to get through each part of the process and know what each variable and “this” was representing. Also, I watched through some of the videos by Avi and the Rails jQuery Office hours from May 11, 2017 on the Learn Video Lecture website: [http://instruction.learn.co/video_lectures/146] to help with review and making sure I understood. 
