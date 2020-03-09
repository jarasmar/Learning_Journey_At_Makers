# Week 4 Goals
* Build a simple web app with a database
* Follow an effective debugging process for database applications
* Explain the basics of how databases work (e.g. tables, SQL, basic relationships)

<br>

***

<br>

# Daily Goals

## Monday 9th March 2020
### MORNING GOAL
Set a working plan for the new week

**Plan:**
- Review weekend challenge in pair
- Set goals for the new week

**Process:**
- Review Anton code and give some appreciations/suggestions.
- Improve my own code: I refactored some of the tests that were not passing but still not fully functioning.
- Attend week kick-off with Josh: introduction to databases.
- Databases are the storage shelves of the digital world, keeping all our information.
- Every database has a DBMS (Database Management System) which structures how we organize and interact with all our stored data. Four fundamental ways of interaction with databases: (CRUD)
  - Create
  - Read
  - Update
  - Delete
- This DBMS can be:
  - Relational: organizes data in tables made of columns and rows (columns are categories and each row inside them holds a data entry). They are highly structured and have strict data types. Great for managing complex datasets. We talk to them using SQL (Structured Query Language).
  - Non-Relational: also known as noSQL (we don't use SQL to talk to them). These are more flexible systems with less strictness around data types (graphs, key-values...). They are good for getting a database up and running quickl and for deploying data across decentralised distributed networks (when data is stored across many computers that all hae to coordinate with each other).
- Most popular DMS:
1. Oracle
2. MySQL
3. Microsoft SQL
4. PostgreSQL
5. MongoDB (noSQL)
- I started working through SQL Zoo to learn some basic query language (used to manage the data held in relational DBMS)
```
# Show the population of Germany:
SELECT population (category-column) FROM world (table name)
  WHERE name (category-column) = 'Germany'
```
```
# Show the name and the population for 'Sweden', 'Norway' and 'Denmark'.
SELECT name, population FROM world
  WHERE name IN ('Sweden', 'Norway', 'Denmark');
```
```
# show the country and the area for countries with an area between 200,000 and 250,000.
SELECT name, area FROM world
  WHERE area BETWEEN 200000 AND 250000
```
```
# Name begins by 'Al'
SELECT name, population FROM world
  WHERE name LIKE "Al%"
```
```
# Show the population density of China, Australia, Nigeria and France.
SELECT name, population/area FROM world
 WHERE name IN ('China', 'Nigeria', 'France', 'Australia')
```

**What I've Learnt:**
>**SQL** (Structured Query Language) standard language used to communicate with a database. SQL statements are used to perform tasks such as update data on a database, or retrieve data from a database.

<br>

### AFTERNOON GOAL
Practice Databases

**Plan:**
Pair with Anton and start working on the afternoon project.

**Process:**
- User story: 
```
As a time-pressed user
So that I can quickly go to web sites I regularly visit
I would like to see a list of bookmarks
```
- Set up a web project
  - Create a gemfile (rspec, capybara, sinatra, rubocop and simplecov)
  - Initialize your rspec repos (spec, lib, features)
  - Update your `spec_helper.rb` file.
  - Create your controller `app.rb` (test-drive main path)
  - Create a `config.ru` file
- Write a feature test for viewing bookmarks at the /bookmarks route.
- Refactor the code to use the View and Controller.
```rb
# in app.rb

get '/bookmarks' do
  @bookmarks = [
            "http://www.makersacademy.com",
            "http://www.destroyallsoftware.com",
            "http://www.google.com"
           ]

  erb :'bookmarks/index'
end
```

```html
<!-- in views/bookmarks/index.erb -->

<ul>
  <% @bookmarks.each do |bookmark| %>
    <li><%= bookmark %></li>
  <% end %>
</ul>
```
- Test drive a refactor of the code to use a Model, that returns the list of bookmarks.
```rb
# in lib/bookmark.rb

class Bookmark
  def self.all
    [
      "http://www.makersacademy.com",
      "http://www.destroyallsoftware.com",
      "http://www.google.com"
     ]
  end
end
```
```rb
# in app.rb

get '/bookmarks' do
    @bookmarks = Bookmark.all
    erb :'bookmarks/index'
end
```


<br>

## Tuesday 10th March 2020
### MORNING GOAL

**Plan:**

**Process:**

**What I've Learnt:**
>**this** blabla

<br>

### AFTERNOON GOAL

**Plan:**

**Process:**
**What I've Learnt:**
>**this** blabla

<br>

## Wednesday 11th March 2020
### MORNING GOAL

**Plan:**

**Process:**

**What I've Learnt:**
>**this** blabla

<br>

### AFTERNOON GOAL

**Plan:**

**Process:**
**What I've Learnt:**
>**this** blabla

<br>

## Thursday 12th March 2020
### MORNING GOAL

**Plan:**

**Process:**

**What I've Learnt:**
>**this** blabla

<br>

### AFTERNOON GOAL

**Plan:**

**Process:**
**What I've Learnt:**
>**this** blabla

<br>

## Friday 13th March 2020
### MORNING GOAL

**Plan:**

**Process:**

**What I've Learnt:**
>**this** blabla

<br>

### AFTERNOON GOAL

**Plan:**

**Process:**
**What I've Learnt:**
>**this** blabla


<br>

***

<br>

## Weekend Challenge
Description

**What I've Learnt:**
>**This:** blabla

<br>

***

<br>


# Weekend Reflections

### Did you meet all of your goals you set at the start of the week?
* Answers here

### What things do you still need to work through?
* Mocking
* And this

### What would you change/improve moving forward?
##### Technical: 
* This
* And this
##### Personal:
* This
* And this

### A pat on the back
* I 
<br>
