---
layout: post
title:  "Rails ActionView Form Helper Methods – form_tag and form_for"
date:   2017-06-29 17:03:54 +0000
---


As I have progressed through Rails lessons, I’ve noticed that there are lots of methods that are being used to do various things such as generating HTML for forms. Form helpers like form_tag and form_for help with building different forms. Sometimes I just start to use methods like this in the labs without completely understanding what they do, so I decided to review the information about them.  The form_tag method allows for building a form without the need for a model or database table. The form_tag is for when you need a search field or a form that doesn’t save or update to the database.

```
<%= form_tag (sessions_path) do %>

	<%= label_tag 'email', 'Email' %>
	<%= text_field_tag 'email' %>

	<%= label_tag 'password', 'Password' %>
	<%= password_field_tag 'password' %>

	<%= submit_tag "Sign In"%>
<% end %>
```

The form_for is a little more abstract than the form_tag method and knows things automatically. It makes assumptions about what you want based on the instance of the model that is passed into it and automatically knows what route using RESTful conventions.

```
<%= form_for(@post) do |f| %>
	<label>Post title:</label><br>
	<%= f.text_field :title %><br>
	 
	<label>Post description</label><br>
	<%= f.text_area :description %><br>
  
  	<%= f.submit %>
<% end %>
```

When deciding between these two, the form_for method is better when when you need the form to be connected to a model. An example would be a user profile edit form used to edit a users profile in the database. In order for the form_for to work, there has to be a table in the database and a model. There also needs to be proper routes in the config/routes.rb file and in the proper controller for the model. As in the above example, @post would need to be defined in the PostsController.

Here are a few references that were helpful in understanding these two helper methods.

https://indyarock.wordpress.com/2013/09/08/difference-between-form_for-and-form_tag-with-example-in-rails/

https://agilewarrior.wordpress.com/2011/09/10/difference-between-form_for-and-form_tag-helper-tags-in-rails/

http://travisje.github.io/blog/2015/07/13/form_for/
