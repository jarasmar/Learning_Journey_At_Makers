# Week 3 Goals
* Build a simple web app
* Follow an effective debugging process for web applications
* Explain the basics of how the web works (e.g. request/response, HTTP, HTML, CSS)
* Explain the MVC pattern

<br>

***

<br>

# Daily Goals

## Monday 2nd March 2020
### MORNING GOAL
Code review and set goals for the week

**Plan:**
- Peer code review of the weekend challenge
- Assist to the week kick off with Josh

**Process:**
- Paired with Sophia and reviewed each other code. We had a quite similar structure so not much suggestions to be done.
We both had the SMS sending function not working properly as the .env file was not getting load properly, so we fixed that together.
- In the kick off we put together all the questions from the weekend project and try to clarify them a bit.
- Josh started explaining basic Request/Response and HTTP.

```
Browser	—>		(HTTP request)			 —>		Server	

Browser 	<—   [response (HTML, CSS, JS..)		<—		Browser
```

**What I've Learnt:**
>**require 'dotenv/load':** This is the way to require the .env file so it can load the credentials to your code in a safe way.

>**Blocks vs. Arguments:** blocks `{}` test that the return is the result of what the method is doing. We use them in output and raise_error test.
```
expect{subject.method}.to output(“…”).to_stdout 		=> 	it returns the (“…”)
```
Arguments `()` tests that the return is the actual method return. 
```
expect(subject.method).to eq (“...”) 	=>	 the return of the method is eq to (“...”)
```

>**TDD Schools:** we have London style which is based in mocks and doubles all over testing and Chicado that does as little mocking as possible.
- London: tests won't fail if we make changes in other classes as they are fully independent, but we need to do feature tests (or use instance_variables) to make sure that everything works together.
- Chicago: tests fail when we do changes in different files but we automatically know that it all works together.

<br>

### AFTERNOON GOAL
Learn some basic HTTP and getting started with Sinatra

**Plan:**
Pair with Sophia and start going through the material in the afternoon challenge.

**Process: HTTP, Sinatra and Capybara**
- Install httpie (command line tool to make HTTP requests)
- `http URL` will print in the console the respond from the server
- `http -v` flag will also print the GET request
- We can send parameters (data sent from the user to the server) through the Query String (starts after the "?"). 
`http://www.example.com/home?name=Bob&age=21` is taking two parameters, name and age.

>You should now understand that clients - such as browsers, or command-line tools like HTTPie - can make requests for resources from servers. Those servers will respond with the resource, and some associated metadata. The resource itself is usually contained within the response body. The metadata is contained within the response headers. All of this communication is done via HTTP.

- **Sinatra:**<br/>
Web framework that acts like a 'server' run from our computer. You can interact with a local server in the same way you would with a remote server, receiving and responding to HTTP requests.
- Create a ruby file and `require "sinatra"` at the top of the file.
- Run in your terminal `sinatra filename.rb` to activate the web framework.
- Use a browser to visit your application at http://localhost:4567 (Nothing happens)
- Create a path
```rb
get '/path' do
  "Hello World"
end
``` 
- Shotgun gem allows you to not manually restart the server everytime you change the code. The problem is that Shotgun will lose the current session everytime you close the console, to avoid this type `set :session_secret` at the top of your file.
- You can return HTML directly with sinatra 
```rb
get '/cat' do
  'I am a string and next bit is a image'
 "<div>
  <img src='URL'>
 </div>"
```
- You can add inline CSS to style your HTML `<div style='border: 3px dashed red'>`
- Views: will separate Ruby and HTML to keep the code clean. Our Ruby file will be controlling concerns and .erb file (containing HTML) will be for presentation or view concerns.
Example: our file `add.rb` calls HTML from `index.erb`:
```rb
get '/cat'
  erb(:index)
end
```
- ERB can return simple strings but can also interpolate ruby expressions within them with `<% %>`. The following will return a random name into the string:
```
<h1>My name is <%= ["Amigo", "Oscar", "Viking"].sample %></h1>
```
- Single Responsibility Principle: view should not be cluttered with complex Ruby experessions. Limit it to light conditionals (if/else) and light iterators (each).
- Move the expression back to the controller, store it in an instance variable and interpolate it in the HTML: 
```rb
get '/random-cat' do
  @name = ["Gato", "Conejo", "Osete"].sample
  erb(:index)
end
```
```html
<h1> My name is <%=@name%> </h1>
```
- Params can send information from the client to the server in the _query string_ and you would be able to see it from the server logs. For example if we add a form to get user input and set the cat name, that input can be stored in a param in the query line.<br/>
If our input is "bigotes" the URL will be: `http://localhost:9393/named-cat?cat_name=bigotes` and if we print `params` we could see this from the server logs: `{"cat_name" => "bigotes"}`
```rb
get '/named-cat' do
  p params  # This will print the hash in the logs
  @name = params[:cat_name]
  erb(:index)
end
```
- Using `<% if %>` within your view you can set a conditional to only render the name string if you actually have a name to put in it. If no name is given, the whole string will disappear.
```html
<% if @name %>
<h1> My name is <%=@name%> </h1>
<% end %>
```
>Our form allows a user to set their cat's name. It will construct a query string and make a request to /named-cat with that string appended. Sinatra will parse the query string to a params hash and use that to render the view. Sinatra will then respond with the rendered view as an HTML string. This process forms the basis of almost all web applications.

- GET methods ask for a server resource while POST methods imply that the request is asking to modify a server resource. (Since we are setting an @name variable on the server with our request, it would seem more appropriate to use a POST request instead of a GET request.)
- If we change our form to a different file and direct its action towards `/named-cat`, we can get a new path that leads only to the form, and once we submit a name (POST) will render the `/named-cat` (that will do a GET request for the image). 
```rb
post '/named-cat' do
  @name = params[:cat_name]
  erb(:index)
end

get '/cat-form' do
  erb(:cat_form)
end
```
_Notice now `/named-cat` is a POST, it will only render after some interaction is done, like a confirmation page._

- Chrometools: When seeing the website with inspect we can see a POST request for `/named-cat` (pulled by our form submitting) and a GET request that `/named-cat` does to reach the image.

- **Capybara**<br/>
Automated browser, which can act the same as normal browsers (Chrome, Mozilla...) but with the difference that it is able to receive instructions programmatically, not just from mouse clicks or keyboard presses. We write this instructions in Ruby, using Capybara as an add-on to RSpec to compose our instructions. (It needs Mozilla Firefox to work).
- List capybara and selenium-webdriver in a Gemfile.
- Install Firefox GeckoDriver: `brew install geckodriver`
- Open up PRY and require both capybara/dsl and selenium-webdriver.
- Within the REPL, $ include Capybara::DSL.
- Set Capybara's default driver to be selenium: `Capybara.default_driver = :selenium `
- Go through [Capybara Workout](http://capybaraworkout.herokuapp.com/) and see how you can interact with a website through PRY or IRB in your command line.


<br>

## Tuesday 3rd March 2020
### MORNING GOAL
Understand mocking and request/response cycle a bit better.

**Plan:**
- Refactor some tests from the Takeaway challenge.
- Attend workshop "Modelling the request/response cycle"

**Process:**
- I managed to refactor the tests from my message and menu class to be fully independent from the other classes.
- In the workshop we did sequence diagrams (with time lines) of some basic HTML files.

<br>

### AFTERNOON

**Plan:**
Pair with Orion and keep working on the preparation material for Battle Project.

**Process:**
We went through yesterday's material again.

**What I've Learnt:**
>**Bundle:** installs all the gems listed in a project gemfile.

<br>

## Wednesday 4th March 2020
### MORNING GOAL
Validate learning on mocking

**Plan:**
- Attend Dana's workshop about empathy
- Talk to a coach

**Validate Learning: Rspec Mocking:**
I finished main refactoring on the tests of Takeaway challenge and went to talk to Josh in order to validate my learning.
- All your classes should be fully tested independently.
- Create doubles of every method or variable you need in your tests that belong to a different class.
- Feature tests are vital in order to make sure that all your classes still work together (they will pass the unit tests even if they don't).
- Domain models are also very important to make creating doubles easier (you know which classes functionalities you are going to require).
- Add features to your program one at a time, building them through the different classes (Agile).
- You can create your doubles at the top of your spec file,right after the `describe "Class" do` to make them available through all the file, or you can create a file to store all the doubles for your whole program and require it from the specs.
- Stubbing doesn't create a double, it calls a double in an unit test.
- Instance Doubles: help to verify your doubles, as the item being doubled actually needs to exist. So it gives additional confidence about things integrating, like feature tests (not necesary to do both).
- We shouldn't be testing Gems functionality, like Twilio (thats their job, we just assume it is working). To test our txt sending method we can create a double of twilio. This is the normal way of testing external code (API, DB..) We can create a manual test to run every one and then to make sure their code actually work (just in case they may have changed that feature we are using for example), but there is no need to automatize it.

<br>

### AFTERNOON

**Plan:**
Pair with Gareth and start working on the Battle Challenge.

**Process:**
- Start a new project creating a Gemfile with Sinatra, Capybara and Rspec.
- Create a controller file `app.rb` and require sinatra at the top
```rb
require 'sinatra/base'

class Battle < Sinatra::Base    # Name of the main repo 
  get '/' do
    'Hello Battle!'
  end
  
  # start the server if ruby file executed directly
  run! if app_file == $0
end
```
- Create a `config.ru` file you can use to run your app.
```
require_relative './app'
run Battle
```
- Run `rspec --init` to start writing your tests.
- Edit your `spec_helper.rb` file:
```rb
ENV['RACK_ENV'] = 'test'

# require our Sinatra app file
require File.join(File.dirname(__FILE__), '..', 'app.rb')

require 'capybara'
require 'capybara/rspec'
require 'rspec'

# tell Capybara about our app class
Capybara.app = Battle   # Name of the main repo 
```
- Create a new directory "features" and create a spec file with your first feature test and make it pass.
```rb
feature 'Testing infrastructure' do
  scenario 'Can run app and check page content' do
    visit('/')
    expect(page).to have_content 'Testing infrastructure working!'
  end
end
```
- Update the code for the user story: `We want to Start a fight by entering our names and seeing them`
- Capybara feature test that expects players to fill in their names (in a form), submit that form, and see those names on-screen:
```rb
feature 'Enter names' do
  scenario 'submitting names' do
    visit('/')
    fill_in :player_1_name, with: 'Jara'
    fill_in :player_2_name, with: 'Bigotes'
    click_button 'Submit'
    expect(page).to have_content 'Jara vs. Bigotes'
  end
end
```
- Create the HTML form in `index.erb`, call it from the `get '/'` rout in `app.rb` and point the form to a new route `post '/names'`
- `post '/names'` route uses params to render a play.erb view that displays the names.
```rb
get '/' do
  erb :index
end

post '/names' do
  @player_1_name = params[:player_1_name]
  @player_2_name = params[:player_2_name]
  erb :play
end
```


<br>

## Thursday 5th March 2020
### MORNING GOAL
Improve debugging techniques.

**Plan:**
Attend Debugging Web Apps Workshop with Josh

**Process:**<br/>
**Approach errors:**
1. See the list of error messages
2. Pick one (unit test before feature tests)
3.  Run rspec with the error path (shows only one error at a time)
4. Read the error message
5. Go to the file and line that the error is pointing (go to line command can do this with the path)
6. Get paralel views of your code and your tests to see it as a whole
7. Try to understand what the code does and what is being tested (look for the syntax that you don’t understand)
8. Try an idea and see if error changes
9. Zoom out when you do changes to see if the rest of tests for that code are still passing (your changes may break them)
10. Look also at the website, if it works or the errors it shows
11. Keep looping through steps 7-10  until the error is fixed
<br/>
**Tricks:**
1. Look for bugs expecting the most common first and  then looking for more difficult posisibilities (Typos > Syntax error > undefined method…)
2. Follow stack trace down (error may be coming from some other file)
3. Git diff will display the changes since last commit, and the error is gonna be within those things that changed (this is only useful if you commit often, everytime something gets green)
4. Give visibility


**What I've Learnt:**
>**Srand:** method for tests, removes the randomness to make tests pass everytime.

<br>

### AFTERNOON

**Plan:**
Pair with Peter and keep working on the Battle Project.

**Process:**
- Enable sessions in Sinatra: short-term information store that lives on the server. It's very small, but it allows the server to store basic pieces of information, like the name of the current user. In Sinatra, session is a Hash, and you can set values for its keys. session is most often used to store details of a logged in user.
`enable :sessions`
- In the post '/names' route, let's store the player names in the session instead of assigning them to instance variables. We will also redirect them to a new path.
```rb
post '/names' do
  session[:plyr_1_name] = params[:player_1_name]
  session[:plyr_2_name] = params[:player_2_name]
  redirect '/play'
end
```
- Now we can't access the values from our play.erb view, so we need to create a new path `/play` to store them in instance variables and render the view.
```rb
get '/play' do
  @player_1_name = session[:plyr_1_name]
  @player_2_name = session[:plyr_2_name]
  erb :play
end
```
- Feature test for next user story: "I want to see Player 2's Hit Points"
```rb
feature 'View hit points' do
  scenario 'see Player 2 hit points' do
    visit('/')
    fill_in :player_1_name, with: 'Jara'
    fill_in :player_2_name, with: 'Bigotes'
    click_button 'Submit'
    expect(page).to have_content 'Bigotes: 60HP'
  end
end
```
- Update our play.erb to display points too.
- Our feature tests are getting longer and repeating themselves. In order to keep code DRY we can create a new file `spec/features/web_helpers.rb` and require it form `spec_helper.rb`
- Define a method that will cover all the first steps:
```rb
def sign_in_and_play
  visit('/')
  fill_in :player_1_name, with: 'Jara'
  fill_in :player_2_name, with: 'Bigotes'
  click_button 'Submit'
end
```
- Substitute all this lines in your tests with a call to this method.
```rb
feature 'Enter names' do
  scenario 'submitting names' do
    sign_in_and_play
    expect(page).to have_content 'Jara vs. Bigotes'
  end
end
```
- Write a feature test for the user story: "I want to attack Player 2, and I want to get a confirmation"
```rb
feature 'Attacking' do
  scenario 'attack Player 2' do
    sign_in_and_play
    click_link 'Attack'
    expect(page).to have_content 'Jara attacked Bigotes'
  end
end
```
- Add a link to your `play.erb` view and direct it to a new path `/attack` that will render a new view `attack.rb` with the confirmation message.
```rb
# in play.erb
<form action="/attack">
  <input type="submit" value="Attack">
</form>
```

<br>

## Friday 6th March 2020
### MORNING GOAL
Practice with Web apps

**Plan:**
Work with the practical 'Build a greeter birthday app'

**Process:**
- Your challenge is to build a web app that will ask the user for a name and birthday. When the user submits the form, and depending on the current date, the app will either: wish the user happy birthday or tell them how long they'll have to wait until their next birthday.
- I created a first path rendering a form to get all the required information and send a post request redirected to a new path with an if/else conditional that would render the appropiate message depending on the date. (unfinished)


**What I've Learnt:**
>**MVC:** (Model, View, Controller) software design pattern commonly used for developing user interfaces which divides the related program logic into three interconnected elements. Controller (app.rb) gives the paths and the actions, Model (ruby files) store the code and Views (erb files are what renders in the browser).

![mvc](https://static.packt-cdn.com/products/9781783287987/graphics/7987OS_01_03.jpg)

<br>

### AFTERNOON GOAL
Practice developing web apps.

**Plan:**
Pair with Ben and keep working on Battle Project.

**Process:**
- Create a new Player class with a tested method that returns its name.
- Require the Player class in your controller file, app.rb.
- Instead of storing player names as strings in the session, store them as attributes of instances of the Player class in `$global_variables` (not a good use).
```rb
post '/names' do
  $player_1 = Player.new(params[:player_1_name])
  $player_2 = Player.new(params[:player_2_name])
  redirect '/play'
end

get '/play' do
  @player_1_name = $player_1.name
  @player_2_name = $player_2.name
  erb :play
end

get '/attack' do
  @player_1_name = $player_1.name
  @player_2_name = $player_2.name
  erb :attack
end
```
- Update your code to reference the new global variables.
- Implement user story: "I want my attack to reduce Player 2's HP"
```rb
scenario 'My attack reduces player two HP by 10' do
    sign_in_and_play
    click_button 'Attack'
    expect(page).to have_content "Bigotes: 90 HP"
  end
```
- Update your player class to have a method that deducts points aftern an attack.
```rb
class Player
  attr_reader :name, :points
  DEFAULT_HP = 100

  def initialize(name, points = DEFAULT_HP)
    @name = name
    @points = points
  end
  
   def attack(player)
    player.receive_damage
  end

  def receive_damage
    @points -= 10
  end
end
```
- Inside the `/attack` path we add the `@player_1.attack(@player_2)` and in the play view we add the variable to display the current points: `<%= @player_2.name %>: <%= @player_2.points %>HP`
- Single Responsability: create a new class game that will be responsible of the attack, while player only stores the points and names. (Move the attack method to that new class, but leave the receive_damage one).
- Skinny controllers: we want our controllers to do nothing more than small amounts of routing logic. 
- Make `Game.new` initialize with two `Player.new` and replace the players global variables with one `$game` that takes the name parameters at initalize.
```rb
class Game
  def initialize(player_1, player_2)
    @players = [player_1, player_2]
  end

  def player_1
    @players[0]
  end

  def player_2
    @players[1]
  end
```
- Update `app.rb`
```rb
  post '/names' do
    @player_1 = Player.new(params[:player1])
    @player_2 = Player.new(params[:player2])
    $game = Game.new(@player_1, @player_2)
    redirect '/play'
  end

  get '/play' do
    @current_game = $game
    erb(:play)
  end

  get '/attack' do
    @current_game = $game
    @current_game.attack(@current_game.defender)
    erb(:attack)
  end
  ```
  - Finally change the views to take the new variable `@current_game`
```rb
+<%= @current_game.player_1.name %> attacked <%= @current_game.player_2.name %>
```
- Integrate the user story: "As two players, we want to switch turns"
- Change your Game class with an instance variable @turn and @defendent that will store the names of player 1 and 2, and a method to swith them after every attack.
```rb
def initialize(player_1, player_2)
    @players = [player_1, player_2]
    @turn = player_1
    @defender = player_2
  end

  def player_1
    @players[0]
  end

  def player_2
    @players[1]
  end

  def attack(player)
    player.receive_damage
    switch_turn
  end

  def switch_turn
    @turn, @defender = @defender, @turn # changes the order of the elements in an array
  end
```
- Change your controller and your views to integrate this new changes. Call the names and points from either the @turn player or the @defendent player.
```html
# In the play view: attack button

<p> It is <%= @current_game.turn.name %>'s turn to attack </p>
<form action="/attack">
    <input type="submit" value="Attack <%= @current_game.defender.name %>" id="Attack">
</form>
```

```rb
# in app.rb
get '/attack' do
   @current_game = $game
   @current_game.attack(@current_game.defender)
   erb(:attack)
end
```
- Display a message when one player gets to 0HP "You are dead"
```html
<% if @current_game.turn.points == 0 %> <%= @current_game.turn.name %> is dead <% end %>
 ```



**What I've Learnt:**
>**This:** blabla

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
