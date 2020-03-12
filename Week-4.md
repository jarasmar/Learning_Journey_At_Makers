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
|:---------------------|-------------------:|
|----------------------|--------------------|
|  RESPONSABILITIES    |   COLLABORATORS    |
|  Add student         |      Cohort        |
|  Delete student      |      Url           |
|  Retrieve student    |      Tag           |
|  Update student      |                    |


- Student DB Table: _id is a primary-key and cohort_id is a foreign key (comes from cohort table)_.

|  id  |    name   |    URL   | cohort_id |
|:-----|-----------|----------|----------:|
|  1   |  'Jara'   |  "www..."|     2     |
|  2   |  'Lukas   |  "www..."|     1     |

Cohort DB Table: _relation 1:many (one cohort for many students)_

|  id  |    cohort    |
|:-----|-------------:|
|  1   |  "Jan 2020"  |
|  2   |  "Feb 2020"  |

- Tag DB Table: _relation many:many (a tag can get several students and students can get several tags) - No need to add keys in the main student table, it uses the join table_

|  id  |     tag     |
|:-----|------------:|
|  1   |    "Yoga"   |
|  2   |   "Climb"   |

- Student-Tag Join DB Table: _records the relations many:many between classes/tables.

|  student_id  |    tag_id   |
|:-------------|------------:|
|      1       |      1      |
|      2       |      1      |
|      2       |      2      |

(Jara does yoga and Lukas does yoga and climbing)


**What I've Learnt:**
>**Normalisation:** process where we take a table structure with repetition on it and we create new structures to avoid this repetitions. This way any change is made only in one place and automatically update everywhere else.

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
