---
layout: post
title:      "Welcome to Wellness"
date:       2020-01-20 20:18:24 +0000
permalink:  welcome_to_wellness
---

### A walk-through of my process for creating my Flatiron School Rails project.

 I have reached the point of project 3 (Rails) for Flatiron School Software Engineering Bootcamp. For this project, I was tasked with creating a Ruby on Rails application that manages content through complex forms and RESTful routes. I was required to have user login and registration, as well as an option to signup/login using a third party(OAuth). To handle user authentication I used the RoR gem Devise, and Github for OAuth.

Personally, when beginning to think about a project I often struggle with developing an idea of what to build. The idea for this project came when I began writing in one of my new journals. I wanted to use this particular journal to keep track of areas of wellness I’m trying to improve in my life. So for each journal entry I have a list of the areas of focus, and what I did that day to work on that area. I was able to translate this into an application idea for this project. Welcome to Wellness is designed as a digital journal for tracking your wellness journey.
		 
To start, I had to think about my models and the associations. I knew I wanted there to be 3 models: User, Topic, and Entry, and I was required to have:
		 
		
		 1 has_many, 1 belongs_to and 2 has_many :through associations.
		
This is how I set my associations in my models:

```
class User < ApplicationRecord
   has_many :entries
   has_many :topics, through: :entries
end

class Topic < ApplicationRecord
    has_many :entries
    has_many :users, through: :entries
end

class Entry < ApplicationRecord
    belongs_to :user
    belongs_to :topic
end
 ```

This makes entries my JOIN table, and therefore it contains the foreign keys for user and topic.

```
create_table "entries", force: :cascade do |t|
    t.datetime "date"
    t.text "content"
    t.integer "user_id" #foreign key
    t.integer "topic_id" #foreign key
    t.datetime "created_at", precision: 6, null: false
    t.datetime "updated_at", precision: 6, null: false
    t.string "keyword"
end
```

My JOIN table had to additionally contain an attribute of its own aside from the foreign keys of the other tables. My entries attributes are `:date :content :keyword.`

Once all of that was set up, I had to figure out how I wanted everything to work in the browser, while considering which routes I wanted to be nested. The requirement: include a nested `:index or :show` route, AND a nested `:new` route with a form that relates to the parent resource. I nested my entries `:show and :new` routes inside of my topics:

```
resources :topics do
    resources :entries, only: [:new, :show]
end

URLs: http://local/host:3000/topics/1/entries/new
             http://local/host:3000/topics/1/entries/1
```

This provided me with `new_topic_entry` AND `topic_entry path` helpers to use in my controllers and views.

Of course, I had all of my other routes, controller actions, and views for the rest of my application’s usability.

Lastly, I had to add a Class level ActiveRecord scope method that when used, routes to a URL showing the scope. I decided to add a keyword search feature that allows the user to search all of their entries for a keyword, which then reroutes them to a search page that shows the entries that contain the keyword they searched for. This was more complex than I initially thought it would be. In order to make it all possible I needed to have the scope method defined in my Entry model, a custom route in my config/routes.rb file, a controller action attached to that route, and of course an associated view. You can see this all below:

```
entry.rb

scope :searched, ->(key_word) {where("keyword LIKE ?", "%#{key_word}%")}

config/routes.rb
 get 'entries/keyword_search', to: 'entries#search', as: 'keyword_search'
entries_controller.rb

def search
   if params[:search]
      @entries = current_user.entries.searched(params[:search])
   else
      @entries = current_user.entries
   end
end

views/entries/index.html.erb (where I initially search from, routes to key_word_search_path)

<h3>Looking for an entry containing a specific keyword?</h3>
   <%= form_tag keyword_search_path, :method => 'get' do %>
      <p><%= text_field_tag :search, params[:search] %>
      <%= submit_tag "Search", name: nil %></p>
   <% end %>
	 
views/entries/search.html.erb 
URL: http://localhost:3000/entries/keyword_search?search=journaling

<% @entries.each do |entry|%>
   <h2> For <%=entry.keyword%> you have the following entries:</h2>
   <h4><%=entry.date.strftime('%a, %b %e, %Y')%></h4>
   <h5><%=entry.topic.title%></h5>
   <p><%=entry.content%></p>
<%end%>
```

This concludes my walk-through. I hope some of the information provided was useful. Thank you for taking the time to read!

Well wishes,

-V.
