---
layout: post
title:      "Sinatra Healthy Habits Tracker"
date:       2019-12-18 18:45:47 -0500
permalink:  sinatra_healthy_habits_tracker
---


Flatiron School Project 2 fell swiftly upon me. As project week day 1 approached, following Thanksgiving week, I was overcome with anxiety. Finally, on the eve of Day 1 (Sunday night), after a full day of sitting with my emotions, and becoming uncomfortable with my inactivity. . . I sat down and got to work.

I had decided 2 weeks prior that I wanted to create a web application where a user can track healthy habits to help them stick to a self care routine. I decided to approach this project strategically to help manage my anxiety, and also make sure I understood the task.

To the whiteboard I went. I mapped everything out from the database, to the models, to the controllers, to the views. I was set. Once I did that I knew exactly where to start. I got started by creating my project file and connecting my GitHub repo to my environment. From there I began creating my file structure, adding my gems, and creating my database. The next day, I realized I should have started with the [Ruby Corneal Gem](https://github.com/thebrianemory/corneal) which was cerated for the purpose of building a Sinatra app. It simplifies the process by generating a Sinatra application template providing the file structure necessary to get started. So I deleted everything I had before, and started fresh using the Corneal Gem. I am so glad I did.

From there, I got my database up and running. I knew I needed a users and a habits table so I migrated those. Making sure to include the :user_id as a foreign key in my habits table, because a Habit `belongs_to` a `:user`. Then, I started thinking. . . I want my user to be able to track habits by date. I thought I needed to add a dates table. Back to the whiteboard I went. After confusing myself trying to figure out the ActiveRecord associations between users, habits, and dates (and which would be my join table) I sought outside counsel. I was advised to simplify it and just have `:date` as an attribute in my habits table (which is where I started).

As I progressed through the project I maintained that idea of keeping it simple. There were so many other things I could have added for functionality, usability, and styling, but the point of the project was to: show that I can build a Sinatra MVC app while demonstrating that I understand how to use ActiveRecord with Sinatra, and that my RESTful routes provide mapping to my controller CRUD actions.

I did that! 

If you are preparing for your Sinatra project here are a few suggestions:

* Plan, plan, plan. Write out everything you can about your application. This will make getting started so much easier.

* Use the Ruby Corneal Gem to save some time and effort getting your file structure in place.  

* Keep it simple. I cannot reiterate this enough. Start small, and if you have time go back and add things. Try your best not to break anything before your assessment!

* This project is not about styling. Styling can be fun and it makes it look nice in your portfolio, but that is not what this project is about. Again, if you finish your project early, or have free time later on (after your assessment) and you want to improve its appearance, go for it!

* Go to open office hours even if you don't need help with anything. I got a lot out of hearing other people's questions, seeing others' projects, and listening to how my cohort lead explained things. 

* Lastly, have fun!


