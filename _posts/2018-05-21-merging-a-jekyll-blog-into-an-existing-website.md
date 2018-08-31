---
layout: post
title:      "Merging a Jekyll blog into an Existing Website"
date:       2018-05-21 15:29:48 +0000
---

As a Flatiron Student, I was expected to blog about different topics as I was going through the curriculum. This process helps to solidify concepts that you might be unsure about and helps others that read the posts as well. The best thing is it is set up as a seamless process. There is a blog dashboard under Learn log in that allows you to type into an editor and submit a post with very little knowledge of what’s going on behind the scenes.

Now fast-forward to post-graduation. I was challenged by my career coach to put together a website to showcase my projects. As if job searching wasn’t enough? Lol. Anyway, I got started on this with the help of a previous student and Flatiron instructor’s help. See this post from Seth Alexander: https://sethaalexander.com/portfolio-site-new-developers/. I used his guidance and found a template on https://html5up.net/ to put together information about me and my projects as well as links to the projects that are deployed on Heroku. This in itself took awhile because you have to go into the html template yourself and add the information plus do any changes to pictures and CSS you might want as well. 

Then I realized that although I will eventually get a job paying good money, I did not have one yet and wanted to only pay for one domain name. It had already hit past the year that Flatiron had paid for, so I had to pay NameCheap to keep my custom domain name. So, I figured out that I want to merge my blog posts into my already done html5up template website so I could take over my website and unlink it from Learn. 

After some searching, I found https://stackoverflow.com/questions/36011879/configure-jekyll-output-to-add-blog-to-existing-site at Stack Overflow and that seemed to be the start of this journey.  I added a new folder to my website project ‘/blog/index.html’, made a _config.yml, and cloned my blog repo from Github to retrieve my _posts folder and others that might be needed. In the _config.yml, I put: 
```
paginate: 5
paginate_path: blog/page:num
plugins: [jekyll-paginate, jekyll-feed]
```
I also added a gemfile:
```
source 'https://rubygems.org'

group :jekyll_plugins do
  gem "jekyll-paginate"
  gem "jekyll-feed"
end
```
Then I bundle installed, which added a Gemfile.lock to the project.
When I typed in ‘jekyll build’, it ran but didn’t do much. So I had to go to the Jekyll docs and try to figure out how to use it. I was supposed to use ‘jekyll serve’ during development to be able to open up ‘localhost:4000’ and see what I had so far. Next I needed to figure out why some of the pages had CSS and background pics and others did not.
The reason some pages were not receiving CSS and/or background images was a matter of file paths in the src or href. I restructured and moved the folders out of the assets folder to the root folder of the project. Then in the file paths I was able to put the ‘/’ in the front and it all worked. For example: href="/css/main.css". I ran ‘jekyll serve’ and then realized that my blog index and posts didn’t have the menu. So I found that and fixed it. I had not included the header in with the menu in the nav.html file.
Another file needed was a CNAME file (no extension on the end). This is a file listing the domain name. So for mine it was:
```
debthecoderjohnson.com
```
Once I got the CSS and images to work right, it was just a matter of pushing what I had to GitHub to my “debjohnson33.github.io” repo. Since I had already cloned a copy to my computer, I just had to take out files I no longer needed and then push to the master.
Another part of this was setting up the “Contact Me” form. I followed the directions for formspree at https://formspree.io/. Once I had pushed up my newly merged site to my repo, I had to pull up my site, fill in the form, and submit it. I received a one-time email to confirm and then it is all set. A few minutes later I also received the message in my inbox that I had filled in to set it up. 
 To see how the file structure ended up: https://github.com/debjohnson33/debjohnson33.github.io  And here is my new portfolio site complete with a blog section: https://debthecoderjohnson.com/