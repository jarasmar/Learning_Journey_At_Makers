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
(Notes on Wednesday Morning)

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
Practice SQL 

**Plan:**
- Work on SQL Zoo

**Process:**
- Notes on Wednesday Morning.

<br>

### AFTERNOON GOAL
Practice Databases and TDD

**Plan:**
- Pair with Lila and work together in the Bookmark Manager Project.
**Process:**
- Install the postgresql via Homebrew: 
`brew install postgresql`
- Start postgres and set it to run automatically when your computer starts: 
`brew services start postgresql`
- Check your installation by running psql in the terminal:
`psql postgres`
- Create a new database with your computer username so PostgreSQL will connect to this database on startup.
`postgres=# CREATE DATABASE "your_user_name_here";`
- List all databases: `postgres=# \l`
- Quit psql: `postgres=# \q`
- When you run psql again it will automatically be in the database with your computer username.
```
Makerss-MacBook-Air:Bookmark_Manager student$ psql
psql (12.2)
Type "help" for help.

student=# 
```
- Create a new database 'bookmark_manager' from psql: 
`CREATE DATABASE bookmark_manager;`
- Use psql to connect to this new database:
`\c bookmark_manager;`
- Inspect the existing list of tables:
`\dt`
- Create a table called bookmarks in the bookmark_manager database, with two columns: id, a SERIAL PRIMARY KEY, and url, a VARCHAR with a maximum length of 60. (Note the SQL commands)
```
CREATE TABLE bookmarks(id SERIAL PRIMARY KEY, url VARCHAR(60));
```
- Record the database setup instructions for your future reference and so that anyone contributing to your project knows how to setup the database.
- Create a `/db/migrations` folder in your main repository and add a file `01_create_bookmarks_table.sql` to record the SQL queries we ran to create the table.
```
# in migrations/01_create_bookmarks_table.sql
CREATE TABLE bookmarks(id SERIAL PRIMARY KEY, url VARCHAR(60));
```
- Update your readme with the instructions too:
  - Connect to psql
  - Create the database using the psql command CREATE DATABASE bookmark_manager;
  - Connect to the database using the pqsl command \c bookmark_manager;
  - Run the query we have saved in the file 01_create_bookmarks_table.sql


**What I've Learnt:**
>**this** blabla

<br>

## Wednesday 11th March 2020
### MORNING GOAL

**Plan:**

**Process:**
- Work on SQL Zoo taking notes on basic commands.

```
# Show one value from one item:
SELECT population (category-column) FROM world (table name)
  WHERE name (category-column) = 'Germany'
```

```
# Show several values from several items:
SELECT name, population FROM world
  WHERE name IN ('Sweden', 'Norway', 'Denmark');
```

```
# Show a value from items in a range:
SELECT name, area FROM world
  WHERE area BETWEEN 200000 AND 250000
```

```
# Show values that include in their name: (Finish ‘%a’  or  Begin ‘a%’)
SELECT name, population FROM world
  WHERE name LIKE “%United%”		# NOT LIKE would exclude it
```

```
# Show population density (division of two values)
SELECT name, population/area FROM world
```

```
# Inclusive OR: Show the countries that are big by area or big by population
SELECT name, population, area FROM world
WHERE area > 3000000 OR population > 250000000
```

```
# Exclusive XOR: Show the countries that are big by area or big by population, but not both.
# Australia has a big area but a small population, it should be included.
SELECT name, population, area FROM world
WHERE area > 3000000 XOR population > 250000000
```

```
# Show population in South America in millions, round to two decimals 
SELECT name, ROUND(population/1000000, 2) FROM world
WHERE continent = 'South America'
```

```
# Show when names and capital have the same number of characters
SELECT name, capital FROM world
 WHERE LENGTH(name) LIKE LENGTH(capital)
```

```
# Show the name and the capital where the first letters of each match. 
# Don't include countries where the name and the capital are the same word.
#  You can use the function LEFT to isolate the first character.
# You can use <> as the NOT EQUALS operator.

SELECT name, capital FROM world
WHERE LEFT(name,1) = LEFT(capital,1) 
AND name <> capital
```

```
# OR connector: Show the year, subject, and name of Physics winners for 1980 together with the Chemistry winners for 1984.
SELECT yr, subject, winner FROM nobel
WHERE subject = 'Physics' AND yr = '1980'
OR subject = 'Chemistry' AND yr = '1984'
```

```
# Show the 1984 winners and subject ordered by subject and winner name; but list Chemistry and Physics last.
SELECT winner, subject FROM nobel
 WHERE yr=1984
 ORDER BY 
 CASE WHEN subject IN ('Physics','Chemistry') THEN 1 ELSE 0 END,
 subject, winner 
```

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
