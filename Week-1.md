# Week 1 Goals
* Test-drive a simple program using objects and methods
* Pair using the driver-navigator style
* Follow an effective debugging process
* Describe some basic OO principles like encapsulation, SRP
<br>

***

<br>

# Daily Goals

## Tuesday 18th February 2020
### MORNING GOAL
Learn some Debugging Techniques

**Plan:** 
Attend Debugging workshop and work through the challenges.

**Process:**
Debug a program by finding and fixing three bugs
- One was a reasonably simple typo in the file (t1tle instead of title)
- The second was again a typo, calling a wrong method this time (.includes? instead of .include?) 
- The third one threw a NameError message (undefined variable) and it was coming from one of the project gems (one of the methods was returning nil).

**What I've Learnt:**
>Mantra for Debugging: 
>- Tighten the loop (find the _exact line_ the bug is coming from)
>- Get visibility (use `p` to inspect everything to help you home in on the exact line)
>- Once you know the one thing that is wrong, try to fix it.

_(Hint: Start from the first line of the error and check the paths, as it may not be caused in the main file but in a secondary one, a gem...)_

<br>

### AFTERNOON GOAL
Practice Pairing and Test-Drive

**Plan:** 
Pair with Karla and start working through the afternoon challenge for the week "Boris Bikes".

**Process:**
1. Set up a project in which we could both collaborate via GitHub
2. Work with _User Stories_ and transform them into _Domain Models_.
3. Move from _Domain Models_ to a _Feature Test_ and investigate on the error.
4. Use Rspec to make an _Unit Test_ out of the _Feature Test_.
5. Pass your first test with the help of the _Stack Trace_.
6. Go back to feature and implement it. (_Add a Variable to the existent Class_)
7. Update the Unit test for the new feature. (_Add an "it" to the "describe"_)

**What I've Learnt:**
>**User Stories:** describe each thing the program is expected to do from the perspective of an user. 

>**Domain Models:** diagram that shows how objects within a system use messages to communicate with one another. (_Process: write down all the nouns and verbes in the user story and organize them into Objects and Messages in a table_)

>**Feature Test:** taking the information from the Domain Model for a feature you need to figure out how this Objects and Messages will work together in the code (_Process: test it in IRB_).

>**Stack Trace:** all the lines that get printed when an error is thrown. Gives information about the type of error and all the paths to the different places of the code where it has happened.

<br>

## Wednesday 19th February 2020
### MORNING GOAL
Practice some debugging effective techniques.

**Plan:**
Work through the material on Debugging Approaches.

**Process:**
Work on error caused in two different programs:
```rb
def factorial(n)
  product = 1
  while n > 0
    n -= 1
    product *= n
  end
  product
end
```
Giving visibility to every step of the process showed that the product was always smaller than expected. Realized that within the while loop `n -= 1` should be placed after `product *= n` so that in the first loop n could be used as given.

```rb
def encode(plaintext, key)
  cipher = key.chars.uniq + (('a'...'z').to_a - key.chars)
  ciphertext_chars = plaintext.chars.map do |char|
    (65 + cipher.find_index(char)).chr
  end
  ciphertext_chars.join
end

def decode(ciphertext, key)
  cipher = key.chars.uniq + (('a'...'z').to_a - key.chars)
  plaintext_chars = ciphertext.chars.map do |char|
    cipher[65 - char.ord]
  end
  plaintext_chars.join
end

encode("theswiftfoxjumpedoverthelazydog", "secretkey")
"EMBAXNKEKSYOVQTBJSWBDEMBPHZGJSL"
```
This second was way more tricky. There were errors thrown in both methods but once I found the first one it was much more easier to solve the second.
The encode method returned `TypeError: nil cant be coerced into Integer` when passing the given argument, but it would work with almost anything else. I started giving visibility and it was by printing `char` inside the map iterations that I saw it was actually breaking at letter 'z'. Automatically realized that cipher was using an excluding range, bug fixed!

The bugs in the decode method was, firstly in the range, same as in the encode, and then saw that `cipher[65 - char.ord]` made no sense and should be done in the opposite way `cipher[char.ord - 65]` to mirror the one in the encode method.

**What I've Learnt:**
>**Don't fall in the Panic Zone:** I managed to feel much more calm than yesterday through all the process although the bugs were harder to fix. And I also got a deeper understanding of the ways of giving visibility and tighten the loop to find the error.

<br>

### AFTERNOON GOAL
Practice TDD and Git Collaboration.

**Plan:**
Pair with Nima, read the material for Git Collaboration and keep working on the Boris Bikes Project.

**Process:**
1. We had our DockingStation releasing bikes from yesterday, update it with a method `#working?` to check if it works. In order to pass the tests we had to create a new file with a Bike class and the method in it and require it in the docking_station file. (_Did all this process with Feature-Test, Unit-Test, Pass the Test_)
2. Our method `release_bike` returns nil so we modified it to return `Bike.new`, an instance of the Bike class, so it will also respong to `#working?`.



**What I've Learnt:**
>**Rspec Built-in Matchers:** The most interesting was the possibility of using `.and` in between two conditions of the test to make it pass only if both are true. (`.or` would pass if one or the other are true, like the `||` comparisor operator) `expect(subject.release_bike).to be_an_instance_of(Bike).and respond_to(:working?)` 

<br>

## Thursday 20th February 2020
### MORNING GOAL
1. Configure name and email in Git.
2. Practice TDD.
3. Attend 'TDD a simple program' Workshop.

**Plan:**
1. Go through Git Collaboration material and GitHub Guides and configure it to display my name and emails in the commits.
```rb
$ git config --global user.name "Jara Santamaria"
$ git config --global user.email "jarasmar@gmail.com"
```
2. Go through material and excercises provided for TDD.

**Process:**
2. For practicing TDD I went through different stages:
- Firstly I read an article about the Three Laws of TDD. 
- I read a blogpost about Four-Phase Testing.
3. Discussed over the steps of TDD and why is a good technique and then apply the process to a Class. <br/>
Process:
- Read and understand one specification/user story (or create it if it's our own program)
- Domain Model (diagram that shows you the objects and messages from the spec)
- Feature test (express user needs in code - IRB)
- Unit test (rspec)
- Run it and fail.
- Write the minimum amount of code to make the test pass.
- Refactor your code until the test is green.
- Do as many unit tests as needed to pass completely the feature test.
- Go for a new User Story

**What I've Learnt:**
>**The Three Laws of TDD:** <br/> 1. You are not allowed to write any production code unless it is to make a failing unit test pass. <br/> 2. You are not allowed to write any more of a unit test than is sufficient to fail; and compilation failures are failures. <br/> 3. You are not allowed to write any more production code than is sufficient to pass the one failing unit test. <br/>
_By practicing TDD we save a lot of future Debugging time. For a good practice we should keep the system executing at all times. The time between executing tests is within seconds or minutes._

>**Four-Phase Test:** <br/> 1. Setup <br/> 2. Excercise (the system under test is executed) <br/> 3. Verify (the result of the exercise is verified against the developer’s expectations) <br/> 4. Teardown (the system under test is reset to its pre-setup state, usually implicitly)

```rb
it 'encrypts the password' do
  user = User.new(password: 'password') # setup

  user.save # excercise

  user.encrypted_password.should_not be_nil # verify
end
```

>**Feature Test vs. Unit Test:** <br/>
A unit test is only for one specific function or individual component of a program, that doesn't depend in any other thing of this program. A feature test is for the whole app, showing how this thing we are testing will work with the whole, from the point of view of the user. <br/>
1 user story -> 1 or more feature tests -> at least one unit test for each of the feature tests <br/>
_In other words, a feature test reproduces what the user does. When doing repl apps the user will interact with ruby language, so we test it in IRB. Command Line Apps interact with input/output and Web Apps interact with clics._

<br>

### AFTERNOON GOAL
Practice TDD

**Plan:**
Pair with Peter and Patrick and keep going with the Boris Bikes Projects.

**Process:**
1. We compared our previous code and made sure we all start at the same level and our code that far works the same way even if was different.
2. Implement our code with user story "I want to dock my bike at the docking station" creating a dock method for our DockingStation class that takes bike as an argument.
```rb
it "responds to #dock" do
  bike = Bike.new
  expect{subject.dock(bike)}.not_to raise_error
end
```
3. Implement our code with user story "I want to see a bike that has been docked". This one was more tricky as we wanted the bike that has been docked get stored in the station variable. <br/>
This will be the test:
```
it "docks bike" do
    bike = Bike.new
    subject.dock(bike)
    expect(subject.station).to eq bike
end
```
And on the ruby file we created an Instance Variable `@station` with an `attr_reader :station`.

**What I've Learnt:**
>**Instance Variable:** An instance variable is used as part of Object-Oriented Programming (OOP) to give objects their own private space to store data in a Class. We define them starting with @. We can create it on their own but if we want to assign them an initial value they have to be created inside the method `initialize`, that will make the value available through all methods in the Class.

>**Encapsulation:** you can't access instance variables from outside the class, that's what we call encapsulation, an object's data is protected from the outside.

>**attr_reader:** returns the value of an instance variable and makes it accessible to others. (_`attr_accesor` gives permission to both write and read an instance variable, `_attr_reader_` is only for reading and `_attr_writer_` only for writing_).

>**Require vs. require_relative:** The general rule is `require` should be used for external files, like gems, while `require_relative` should be used for referring to files within your directory. `Require_relative`'s scope is wider and is aware of the entire directory where the program resides.


<br>

## Friday 21st February 2020
### MORNING GOAL
Practice TDD

**Plan:**
Start working on the birthdays project.

**Process:**
- Store all of my friends’ birthdays so I can keep track of them
- See them all at once with their names and birthdays each on a line in a tidy format
- Check whose birthday it is today - the program can check through the birthdays I have stored and check each one to see if it’s someone’s birthday, and tells me something like "It's Mary Poppin's birthday today! They are 124 years old!" - otherwise it won't say anything.

**What I've Learnt:**
>**Time Class:** 
```rb
time = Time.new
time.strftime("%d/%m/%Y")        # "05/12/2015"
```

<br>

### AFTERNOON GOAL
Practice TDD

**Plan:**
Pair with Daria and keep working on the Boris Bikes project.

**Process:**
1. I don't want a station to release a bike when it is not available: Create a test that will raise an exception.
2. Limit the capacity of an station: Raise exception when the station is full.
3. Stations will have a default value of 20 bikes: initialize a constant variable `@capacity` to equal 20.
4. Refactor your code so it follows the _Single Responsability Principle_ using private methods.
5. Use a constant to set the default capacity of the station instead of using the number 20 all over the code (improves readibility).
6. Give the possibility to give a station a bigger capacity when needed, but keeping the default value if not specified.
```rb
class DockingStation
attr_reader :station, :capacity
DEFAULT_CAPACITY = 20
  def initialize(capacity=DEFAULT_CAPACITY)
    @station = []
    @capacity = capacity
  end
```

**What I've Learnt:**
>**Private Methods:** they are not accessible from outside the object and they are only used internally. An important aspect of good object-oriented design is that the consumer of an object should not have to know how that object is implemented.

<br>

***

<br>

## Weekend Challenge
**Airport Challenge:** See the full project [here](https://github.com/jarasmar/airport_challenge)

We have a request from a client to write the software to control the flow of planes at an airport. The weather is normally sunny but sometimes there can also be a storm. These are the user stories:
- I want to instruct a plane to land at an airport
- I want to instruct a plane to take off from an airport and confirm that it is no longer in the airport
- I want to prevent landing when the airport is full
- I would like a default airport capacity that can be overridden as appropriate
- I want to prevent takeoff and landing when weather is stormy

**What I've Learnt:**
>**Rspec Mocks:** help to control the context in a code example by letting you set known return values, fake implementations of methods, and even set expectations that specific messages are received by an object. (_For example this will help you override the random weather to ensure consistent test behaviour._)

>**Method Stubs:** instruction to an object (real or test double) to return a known value in response to a message: <br/> 
```rb
allow(subject).to receive(:storm?) { false } # overrides storm true
```
_To override a rand and return the expected value in the test:_

```rb
expect(subject).to receive(:rand).and_return(7)
```

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
* I added stretching to my morning routine and did it every day!!

<br>
