---
layout: post
title:  "Sinatra Portfolio Project Chopsticks"
date:   2017-01-12 23:01:49 +0000
---


Chopsticks is the first iteration of a meal tracking website. The goal was to get the core functionality to later build upon for later potfolio projects. 

The projects allows users to create an account and login with error checking
![](http://i.imgur.com/d7hd7Oe.png)

One of the more useable features I created was the ability to remember last visited page. So you haven't logged in yet and you navigate directly to /meals but that page requires you to be logged in. So it remembers you are trying to go to /meals then sends  you to the login form to sign in. Upon successfully signing in, you are automatically redirected back to /meals without having to retype the url. 

Our models our as follows:

Fooditem : has many meals, has many serving_types, belongs_to user

Meal : has many fooditems, has many users

User : has many meals, has many fooditems


route /fooditems/new

![](http://i.imgur.com/U9b4Lwy.png)

The serving sizes (g/ml) are pulled down from the database and autopopulated into a select->option tag so we are free to add/remove more like cups/100g or so on later down the road. 

when you successfully create a fooditem you are directed to /fooditems index page where you can view your newly created food which is a link to see its individual nutritional values

![](http://i.imgur.com/PXcg6tP.png)
![](http://i.imgur.com/z4hZP5P.png)

/meals is very similar but a meal is a collection of fooditems. We needed a way to store adding a given fooditem into a meal before the meal was saved into the db. In comes sessions. I originally stored the fooditem object directly into a session variable but this exceeds the 4k cookie size limit. So I reconfigured to only store the ids of the fooditems in array then recreate the fooditems from those ids later. 

You can add foods to your given meal by going to /meals index page and there are link next to each food to add to a meal. This will direct you through /meals/add/:fooditemid where it will append that fooditem id to the meal array if it finds the food in the db. Then you are directed back to /meals/new where it shows you new fooditem added to the list. It also calculated the totals of fat/carbs/protein for all fooditems in your given meal.

![](http://i.imgur.com/noPAhJs.png)

The /meals and /fooditems are not really intended to be public facing as you really want only admins able to add/edit/delete foods/meals from your database. So I gave users a way to link them eating a meal at a given time and date for tracking purposes. 

user_meals

user_id, meal_id, date_eaten, time_eaten, data(serialized data)

this allows us to say a given user eats x combination of foods on a given day, at a given time and can have multiples. Later we can build out a dash board where you can add meals for your current day/today and have it track how many calories you have left or how much of a macronutrient your target is and could possible suggest foods that fit those requirements. 

But that is for another time when i spend a lot more time making it look pretty and as sinatra is a great framework its not really suited for something of that scope that would have millions of foods and meals and users. Till next time in rails land!








