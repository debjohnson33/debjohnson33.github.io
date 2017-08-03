---
layout: post
title:  "Rails Project - Farm Tracker"
date:   2017-08-03 19:25:36 +0000
---

When I started my rails project I did the usual writing out what I wanted to do detailing the associations between the models/tables. This app idea comes from a need to keep track of the animals that we have on our property. We have 3 different types of animals in 4 different areas. So, for the app, I wanted a user to be able to have many farms. Each farm can have many areas and many animals through areas. To check it out on Heroku: [https://farm-tracker.herokuapp.com/](http://)

Most of this was similar to the labs and projects of the rails section except for writing a custom attributes equals method. This part led to many hours each day trying to figure out the right way to do it for my app and not have validation errors. There are many different ways to write this method, but what I did was write the “vanilla” attributes method and then separate the uses of the params in the farms controller using an if statement to check to see if the action was new/create versus edit/update. This is what it looked like:

In /models/farm.rb:

```
	def areas_attributes=(areas_attributes)
		areas_attributes.each do |i, area_attributes|
			self.areas.build(area_attributes)
		end
	end
```

In /controllers/farms_controller.rb

```
def farm_params
		if params[:action] == "new" || params[:action] == "create"
			params.require(:farm).permit(
				:name,
				:user_id, 
				:areas_attributes => [
					:id,
					:name, 
					:area_type,
					:capacity, 
					:quantity,
					:farm_id
				]
			)
		else
			params.require(:farm).permit(:name, :user_id)
		end
	end
```

Since I have different farm params for the update action, it allows you to update just the farm name. In doing this, I also changed the edit view for farm to only have fields for farm. I already had an area edit page, so this did not affect the ability to edit areas. The user just goes to the area show page of the area they want to edit and do it there.

In my searching, I also found a different custom nested attributes method. It allows you to save a farm without filling out the area fields using the delete_if, but when you go to edit/update the farm, it tries to insert the same areas into the database instead of updating them which leads to an SQL error.

```
def areas_attributes=(areas_attributes)
	areas_attributes.delete_if { |_i, h| h.any? { |_k, v| v.empty? } }
	areas_attributes.values.each { |area| areas.build(area) }
end
```

The bottom line on the attributes equals method is that you have to look at your situation and figure out what you want your app to be able to do. For me, I didn’t want a “find or create by” in my method because in real life a farm could have more than one area for the same type of animal so I wanted to be able to have 2 different goat pens if the user has them.

Something else that was a change for me was that I learned how to deploy to Heroku. This was a challenge in itself making sure that everything was edited to be compatible. Once you follow the directions on their site, it is easy to make sure it is up to date with a git command that’s similar to what we use for GitHub. You just have to do a push to both Heroku and GitHub each time you change something.

There are a lot of other things I learned in developing this app, but I don’t think there’s enough room to put it all in this blog. If anything, I’m happy that I took the extra time to learn how to add some Bootstrap styling and deploy to Heroku because now I can show my hard work to people that don’t know what forking and cloning are!  :)

To get started on Heroku: https://devcenter.heroku.com/articles/getting-started-with-ruby#introduction
Once you have an app started and have followed all the steps in the getting started:
https://www.codecademy.com/articles/deploy-rails-to-heroku

If you forgot to put your app name when typing in heroku create, you can follow these directions to change the name: https://coderwall.com/p/y5rtzq/created-a-heroku-app-but-i-want-to-change-the-name-now 
Note: Step 4 in changing the name process should be “git remote add heroku http://git.heroku.com/your-app-name-here.git It should match what it says in your Heroku app settings tab

