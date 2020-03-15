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
(Notes on Tuesday Morning)

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
  
- List any existing rows in the bookmarks table.
```
SELECT * FROM bookmarks;
```
- Create four link entries in the bookmarks table, with four URLs using an INSERT statement.
```
INSERT INTO bookmarks VALUES(1, 'http://www.makersacademy.com');
```
* We don't need to put key 1, because when we created the table we told the ID to be `SERIAL PRIMARY KEY` so PostgreSQL will figure out how to increment it on its own.
- List the four entries using a SELECT statement.
```
SELECT * FROM bookmarks;
```
- Delete one of the links with a URL using a DELETE statement.
```
DELETE FROM bookmarks WHERE url = 'http://www.twitter.com';
```
- Update the http://askjeeves.com link to http://www.destroyallsoftware.com using an UPDATE statement.
```
UPDATE bookmarks SET url = 'http://www.destroyallsoftware.com' WHERE url = 'http://www.askjeeves.com';
```
- INTERACTING WITH POSTGRESQL FROM RUBY
- Install the pg gem to your project.
- Pg Documentation:
```
- The pg gem makes a PG object available in Ruby.
- We can call connect on the PG object, passing in the database name.
- This will return an object that we can send a query to, let's call that object connection.
- To retrieve bookmarks from the database, we'll call exec on the connection object, passing in a query string.
```
- IRB testing pg:
```
require 'pg'
 => true
connection = PG.connect(dbname: 'bookmark_manager')
 => #<PG::Connection:0x007fc9c79700e8>
result = connection.exec('SELECT * FROM bookmarks')
 => #<PG::Result:0x007fc9c7958628 status=PGRES_TUPLES_OK ntuples=3 nfields=2 cmd_tuples=3>
2.4.1 :005 > result.each { |bookmark| p bookmark }
{"id"=>"1", "url"=>"http://makers.tech"}
{"id"=>"2", "url"=>"http://www.destroyallsoftware.com"}
{"id"=>"3", "url"=>"http://www.google.com"}
 => #<PG::Result:0x007fc9c7830cc8 status=PGRES_TUPLES_OK ntuples=3 nfields=2 cmd_tuples=3>
 ```
 
- Test drive an update to the .all method of your Bookmark model, to do the following:
  - Use PG to connect to the PostgreSQL bookmark_manager database.
  - Retrieve all bookmark records from the bookmarks table.
  - Extract the URLs from the database response.
```
# in lib/bookmark.rb

require 'pg'

class Bookmark
def self.all
    connection = PG.connect(dbname: 'bookmark_manager')
    result = connection.exec('SELECT * FROM bookmarks')
    result.map { |bookmark| bookmark['url'] }
  end
end
```
- TABLE PLUS: GUI (Graphical User Interface) to databases
- Your database management system needs some information about your postgres server:
  - Where it is: `localhost` (i.e. your PostgreSQL server is running 'backgrounded' on your local machine, on Port 5432)
  - Required login details: Your computer's name as a username (or, you can find this out by listing databases in psql), and no password.
  - What database it should start with: `bookmark_manager` database.

- SETTING UP A TESTING ENVIRONMENT:  
- Our tests will start failing if we make changes to our databases, as they expect certain content to be in them.
- Create a test database, `bookmark_manager_test`, with a bookmarks empty table. 
- Set up an Environment Variable to tell the application to use the right database each time, so that:
  - When you run tests using rspec, bookmarks are read from the new bookmark_manager_test database.
  - When you run the application locally, bookmarks are read from the bookmark_manager database.

```rb
# in spec/spec_helper.rb

ENV['ENVIRONMENT'] = 'test'
```
- Fixing Unit Tests: this code will fill the empty test database to have the expected results.
```rb
describe '.all' do
  it 'returns a list of bookmarks' do
    connection = PG.connect(dbname: 'bookmark_manager_test')

    # Add the test data
    connection.exec("INSERT INTO bookmarks (url) VALUES ('http://www.makersacademy.com');")
    connection.exec("INSERT INTO bookmarks (url) VALUES('http://www.destroyallsoftware.com');")
    connection.exec("INSERT INTO bookmarks (url) VALUES('http://www.google.com');")

    bookmarks = Bookmark.all

    expect(bookmarks).to include('http://www.makersacademy.com')
    expect(bookmarks).to include('http://www.destroyallsoftware.com')
    expect(bookmarks).to include('http://www.google.com')
  end
end
```
- Tests should always run against an empty database so we need a script with a method that clears out the previous data before we run each test. (_We could've also used `DROP TABLE` instead of `TRUNCATE` to remove the full table_)
```rb
# in spec/setup_test_database.rb

require 'pg'

def setup_test_database
  p "Setting up test database..."

  connection = PG.connect(dbname: 'bookmark_manager_test')

  # Clear the bookmarks table
  connection.exec("TRUNCATE bookmarks;")
end
```
- To make sure this runs automatically and clears the database everytime we run a test we can call the method from spec_helper.rb.
```rb
# in spec/spec_helper.rb

require_relative './setup_test_database'

ENV['ENVIRONMENT'] = 'test'

RSpec.configure do |config|
  config.before(:each) do
    setup_test_database
  end
end

### rest of the file ###
```
- Now all our tests will run into an empty database, so make sure you fill it up in each feature and unit test.
- Update your database setup instructions to include the test database.

**What I've Learnt:**
>**Working environments:** It's normal to have multiple environments in applications. These might include:
  - A development environment that runs locally on your computer, so you can click around it and work on it. (Development database is initially empty, runs locally in our computer and we can add to it locally)
  - A production environment that runs remotely on someone else's computer, so other people on the internet can click around it. (Production database will contain the real data)
  - A test environment that runs locally on your computer whenever you run your tests. It comes into being especially for your tests, and disappears straight after your tests finish. (Test database will be empty so we set up the data we need before running our tests)

<br>

## Wednesday 11th March 2020
### MORNING GOAL

**Plan:**
Attend Database Domain Modelling using CRC cards with Josh.

**Process:**
- User stories:
```
As a coach
So I can get to know all students
I want to see a list of students' names

I want to filter the list of students by cohort name

I want each student name's name to link to the URL of a picture of the student

I want to tag a student with many named tags
```

- CRC Card (Class, Responsabilities, Collaborators).

|         Student      |     Student        |
|----------------------|--------------------|
|  RESPONSABILITIES    |   COLLABORATORS    |
|  Add student         |      Cohort        |
|  Delete student      |      Url           |
|  Retrieve student    |      Tag           |
|  Update student      |                    |


- Student DB Table: _id is a primary-key and cohort_id is a foreign key (comes from cohort table)_.

|  id  |    name   |    URL   | cohort_id |
|------|-----------|----------|-----------|
|  1   |  'Jara'   |  "www..."|     2     |
|  2   |  'Lukas   |  "www..."|     1     |

Cohort DB Table: _relation 1:many (one cohort for many students)_

|  id  |    cohort    |
|------|--------------|
|  1   |  "Jan 2020"  |
|  2   |  "Feb 2020"  |

- Tag DB Table: _relation many:many (a tag can get several students and students can get several tags) - No need to add keys in the main student table, it uses the join table_

|  id  |     tag     |
|------|-------------|
|  1   |    "Yoga"   |
|  2   |   "Climb"   |

- Student-Tag Join DB Table: _records the relations many:many between classes/tables.

|  student_id  |    tag_id   |
|--------------|-------------|
|      1       |      1      |
|      2       |      1      |
|      2       |      2      |

(Jara does yoga and Lukas does yoga and climbing)


**What I've Learnt:**
>**Normalisation:** process where we take a table structure with repetition on it and we create new structures to avoid this repetitions. This way any change is made only in one place and automatically update everywhere else.

<br>

### AFTERNOON GOAL

**Plan:**
Pair with Rafa and keep working in the Bookmark challenge

**Process:**
- User Story: I want to add new bookmarks.
- Create a feature test and make it pass updating your view (input form) and your controller: 
```rb
# in app.rb

get '/bookmarks/new' do
  erb :"/bookmarks/new"
end

post '/bookmarks' do
  url = params['url']
  connection = PG.connect(dbname: 'bookmark_manager')
  connection.exec("INSERT INTO bookmarks (url) VALUES('#{url}')")
  redirect '/bookmarks'
end
```
- Now the controller is connecting to the Db and executing SQL, which should be done by the model. We can create a new method `#create` that will do this work.
```rb
# in lib/bookmark.rb

def self.create(url:)
  if ENV['ENVIRONMENT'] == 'test'
    connection = PG.connect(dbname: 'bookmark_manager_test')
  else
    connection = PG.connect(dbname: 'bookmark_manager')
  end

  connection.exec("INSERT INTO bookmarks (url) VALUES('#{url}')")
end
```
- Now our controller looks much better:
```rb
post '/bookmarks' do
  Bookmark.create(url: params['url'])
  redirect '/bookmarks'
end
```
- We can use this new method to refactor all our long tests too.
- CONNECTION BETWEEN A DATABASE AND AN APP: 'Object-Relational Map (ORM) Pattern'.
- A normal connection between a database and an application mode works in this way:
  - Bring database data from database rows into your Ruby application.
  - Wrap each row from the table in Ruby objects, as an instance of a class.
  - Ask a model to do things (methods) with the data it wraps.
- Update the test and development databases so that bookmarks have a title, in addition to the url.
``` 
ALTER TABLE bookmarks ADD COLUMN title VARCHAR(60);
```
(Don't forget to add this line to the db/migrations folder in a different file `02_add_title_to_bookmarks.sql`)
- Update the feature tests to expect having the titles linking to the URL.
- Update the view to take title as a new input when creating a bookmark.
- Update the controller to save the new param.
```rb
post '/bookmarks' do
    title = params['title']
    url = params['url']
    Bookmark.create(title: title, url: url)
    redirect '/bookmarks'
  end
```
- Update unit tests and method `#create`.
```rb
 def self.create(url:, title:)
     if ENV['ENVIRONMENT'] == 'test'
       connection = PG.connect(dbname: 'bookmark_manager_test')
     else
       connection = PG.connect(dbname: 'bookmark_manager')
     end

     connection.exec("INSERT INTO bookmarks (title, url) VALUES('#{title}', '#{url}') RETURNING id, url, title")
  end
```
- Update the main view with a list of bookmarks so we only see the titles that link to the URLs.
```HTML
<ul>
  <% @bookmarks.each do |bookmark| %>
    <li>
      <a href="<%= bookmark.url %>">
        <%= bookmark.title %>
      </a>
    </li>
  <% end %>
</ul>
````
- The HTML indicates that we need to make sure that each bookmark is an object that responds to url and title. At the moment, each bookmark is a string. So, we need to:
  - Get the result object from the database
  - Wrap it in a Bookmark instance
  - Make sure that Bookmark instance responds to id and url.
- Change your Bookmark class to take three parameters that we retrieve from the database:
```rb
class Bookmark

  attr_reader :id, :title, :url

  def initialize(id:, title:, url:)
    @id  = id
    @title = title
    @url = url
  end

  ### rest of the class ###
end
```
- Update the `#all` method:
```rb 
def self.all
  if ENV['ENVIRONMENT'] == 'test'
    connection = PG.connect(dbname: 'bookmark_manager_test')
  else
    connection = PG.connect(dbname: 'bookmark_manager')
  end
  result = connection.exec("SELECT * FROM bookmarks")
  result.map do |bookmark|
    Bookmark.new(id: bookmark['id'], title: bookmark['title'], url: bookmark['url'])
  end
end
```
- Update `#create` to wrap the data too:
```rb
def self.create(url:, title:)
  return false unless is_url?(url)
  if ENV['ENVIRONMENT'] == 'test'
    connection = PG.connect(dbname: 'bookmark_manager_test')
  else
    connection = PG.connect(dbname: 'bookmark_manager')
  end
  result = connection.exec("INSERT INTO bookmarks (url, title) VALUES('#{url}', '#{title}') RETURNING id, title, url;")
  Bookmark.new(id: result[0]['id'], title: result[0]['title'], url: result[0]['url'])
end
```

**What I've Learnt:**
>**this** blabla

<br>

## Thursday 12th March 2020
### MORNING GOAL

**Plan:**
- Review some theoric documentation provided for the week

**Process:**
- INSTANCE METHODS VS. CLASS METHODS
- Instance Methods: provides functionality to one instance of a class.
```rb
class Foo
  def bar
    p 'This is an instance method'
  end
end

foo = Foo.new
#  => #<Foo:0x00007ffc4b073d80>
foo.bar
# => "This is an instance method" 
```

- Class Methods: provides functionality to a class itself.
```rb
class Foo
  def self.bar
    p 'This is a class method'
  end
end

Foo.bar
#  => "This is a class method" 

foo = Foo.new
#  => #<Foo:0x00007f9917849dd0>
foo.bar
# => NoMethodError (undefined method `bar' for #<Foo:0x00007f9917849dd0>)
```
- REST
- Set of conventions for writing routes. Using REST will make your routes more manageable and professional-looking.
RESTful routing exposes the true nature of your web application: as a state machine capable of being in a finite number of different states. Movements between the states are determined by user interactions, and are called state transitions:
  - Having 35 bookmarks (state)
  - Adding a bookmark (state transition)
  - Having 36 bookmarks (state)
  - Deleting a bookmark (state transition)
  - Having 35 bookmarks (state)
- For each of these, a RESTful route defines the next state of the machine, and the machine responds with the state it's now in:
  - GET /bookmarks returns a webpage with 35 bookmarks
  - POST /bookmarks transitions the machine to a new state with 36 bookmarks, and returns a webpage with 36 bookmarks.
  - DELETE /bookmarks/4 transitions the machine to a new state with 35 bookmarks and returns a webpage with 35 bookmarks.
- I was playing around with the excercises to understand and design RESTful routes [here](https://sjmog.github.io/rest) 


<br>

### AFTERNOON GOAL

**Plan:**
Pair with John and keep working on the afternoon challenge.

**Process:**
We went over step 10 and 11 again, like wednesday afternoon.

<br>

## Friday 13th March 2020
### MORNING 

We had a special workshop on working remotely, to get ready for the school shutdown starting next week. We learned how to use Zoom to make videocalls and share screens to keep pairing and doing group work and also talked about different apps that allow to share information on real time.

The rest of the time I started planning and sketching on the weekend challenge.

<br>

### AFTERNOON GOAL

**Plan:**

Pair with Neha and keep working on the Afternoon challenge.

**Process:**

- Added the User Story: I want to delete a bookmark.

<br>

***

<br>

## Weekend Challenge: Chitter

We are going to write a small Twitter clone that will allow the users to post messages to a public stream.

You can see my whole project [here](https://github.com/jarasmar/chitter-challenge)

**Features:**

I did all the basic features and planned into the log_in and log_out ones but didn't have time to do them.

```
As a Maker
So that I can let people know what I am doing  
I want to post a message (peep) to chitter

As a maker
So that I can see what others are saying  
I want to see all peeps in reverse chronological order

As a Maker
So that I can better appreciate the context of a peep
I want to see the time at which it was made

As a Maker
So that I can post messages on Chitter as me
I want to sign up for Chitter

HARDER

As a Maker
So that only I can post messages on Chitter as me
I want to log in to Chitter

As a Maker
So that I can avoid others posting messages on Chitter as me
I want to log out of Chitter

ADVANCED

As a Maker
So that I can stay constantly tapped in to the shouty box of Chitter
I want to receive an email if I am tagged in a Peep
```

**Domain Model:**

| CHITTER        | PEEP             | USER             |
| :------------- |:-----------------|:-----------------|
| -------------- |------------------|------------------|
|                | @id              | @id              |
|                | @peep            | @name            |
|                | @post_time       | @username        |
|                | @post_date       | @email           |
|                |                  | @password        |
| -------------- |------------------|------------------|
| #print_peeps   | #time            | #valid_log_in    |
| #post_peep     | #date            |                  |
| #sign_up       |                  |                  |
| #log_in        |                  |                  |
| #log_out       |                  |                  |


**Databases Plan:**

- Table Peeps:

|  id  |    peep   | post_time |  post_date | users_id  |
|------|-----------|-----------|------------|-----------|
|  1   |  'Hello'  |  13:25:00 | 2020-01-14 |     1     |
|  2   |  'World'  |  17:05:00 | 2020-03-12 |     1     |

- Table Users:

|  id  |    name   |   username  |      email      |  password  |
|------|-----------|-------------|-----------------|------------|
|  1   |  'Dino'   | SuperCactus | dino@cactus.com | itsasecret |


**Views Plan:**
```
get '/chitter'            -->  display chitter.erb (link to sign_up - link to log_in - peep list)
get '/chitter/sign_up'    -->  display sign_up.erb (sign_up form)
post '/chitter/sign_up'   -->  redirect to ./chitter/log_in (saves data to users table in DB)
  # at this point redirects to '/chitter/user'
get '/chitter/log_in'     -->  display log_in.erb (log_in form)
post '/chitter/log_in'    -->  redirect to ./chitter/user (authenticates data)
get '/chitter/user'       -->  display user.erb (link to log_out - link to post_peep - peep list)
get '/chitter/post_peep'  -->  display post_peep.erb (post_peep form)
post '/chitter/post_peep' -->  redirect to ./chitter/user (saves peep to peeps table in DB)
post '/chitter/log_out'   -->  redirect to ./chitter (clears log_in data)
```

<br>

***

<br>


# Weekend Reflections

### Did you meet all of your goals you set at the start of the week?
* Im very happy with my progress and how I am dealing with it but it has been a hard week with all the coronavirus issues and the school shutting down. I feel I have wasted a lot of energy in the process and have not been able to focus as much as other weeks. Even if I have understood everything I have been able to work through I have left quite a lot of important things behind as I didnt have enough time.

### What things do you still need to work through?
* Relations between tables in databases.
* Registration features for web apps.

### What would you change/improve moving forward?

##### Personal:
* I need to force myself to take enough breaks while working remotely.
