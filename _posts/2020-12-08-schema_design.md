---
layout: post
title:      "Schema Design"
date:       2020-12-08 09:58:48 +0000
---

One of the things I’ve noticed is the planning stage of designing the schema for your database is the most important thing to do before anything else. You must understand how your data is structured or could be structured and should think about the different queries that will need to be made in order to get the information you need. If you have several different tables, you need to be clear on what items they are representing and the relationships that are between them. This includes the potential for needing a join table as well as the use of foreign keys to establish relationships.

User ---> has many favorites ----> for this relationship, you could put a foreign key into the favorite table or make a join table between the user and favorite called user_favorites
Favorite ---> belongs to User

In a query, would it be helpful to have the join table for looking up a user’s favorite or is the foreign key enough? This is one of many questions that should be asked. Even if you are using Sequelize to help you abstract some of it, you still have to understand what the underlying SQL is going to look like.

The same can be said for the no-SQL database helpers like mongoose for MongoDB. You still need to understand what you’re trying to query.

For no-SQL databases, the structure of the data will be different but it still should be thought through. If a list of items belongs to a user, for instance, that list would be an array of objects representing the items in the document for MongoDB. In this case, the question should be ‘Does each item in the array need to be its own MongoDB document or a plain object?’

Using the 10-15 minutes that it takes to think these things through can save refactoring time that you might have to do later from not doing this. There are even tools online that can help you to think this through and make an entity relationship diagram. Here is a website with a list of 7 different websites you can use:

https://trevor.io/blog/top-7-entity-relationship-diagram-tools/#quickdbd
Below is an example of what can be done with about 10 minutes on one of these tools.
This was on QuickDBD and requires you to actually type out your schema which means you will have full understanding by the time you’re done.

