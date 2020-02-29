# Week 2 Goals
* Use all of week 1's skills (don't underestimate the importance of this)
* Break one class into two classes that work together, while maintaining test coverage
* Unit test classes in isolation using mocking
* Explain some basic OO principles and tie them to high level concerns (e.g. ease of change)
* Review another person's code and give them meaningful feedback

_Plan to add improvements to my Airport Challenge to make it more consistent_

<br>

***

<br>

# Daily Goals

## Monday 24th February 2020
### MORNING GOAL
Code Review and set goals for the week

**Plan:**
Peer code review of the weekend challenge.

**Process:**
1. Make an apreciation.
2. Make a suggestion.
3. Make an improvement on your own code from the review you got. <br/>
(My peer suggested to creates doubles in my tests instead of create new instances of the class Plane, and I changed all those lines of my code to let it test independently in the Airport class.)

**What I've Learnt:**
>**Test Doubles:** any object that stands in for a real object during a test (think "stunt double"). You create one using the double method. When creating a double, you can allow messages (and settheir return values) by passing a hash.
```rb
plane = double("new plane")
```

<br>

### AFTERNOON GOAL

**Plan:**
1. Pair with Kuba and practice TDD while start working on the Oystercard Project.
2. Attend Process Workshop

**Process:**<br/>
Oyster card Project
1. Create a Gemfile (_source for gems, version of ruby and add the rspec gem to ‘test’ and ’development’ groups_)
2. Create RSpec conventional files
3. Review debugging basics (_understand how to read a stack trace_)
4. Add the balance (_first test, default value of 0_)
5. Enable top up functionality (_method top up adds the value to balance_)
```rb
expect { subject.top_up 10 }.to change{ subject.balance }.by 10
```
6. Enforce maximum balance (_set a constant balance limit and raise error if top up exceeds it_) 
```rb
def top_up(value)
  fail "Top up limit of #{LIMIT} exceeded" if value > LIMIT
  @balance += value
end
```
7. Deduct the money (_method deduct substracts the amount from balance_)
<br/>

Process Workshop: 10 minutes walk<br/>
Oyster card Project<br/>

  1. Read and refine the story (in groups)<br/>
  2. Make a plan (in groups)<br/>
  In pairs, by turns:<br/>
  3. Start a TDD Process on your own (30 min)<br/>
  4. Get feedback from your colleague<br/>
  5. See your colleague go through TDD (30 min)<br/>
  6. Give feedback to your colleague<br/>

**What I've Learnt:**
>**Gemfile:** a file we create which is used for describing gem dependencies for Ruby programs. A gem is a collection of Ruby code that we can extract into a “collection” which we can call later. Gemfile should always be in the root of your project directory, this is where Bundler expects it to be.<br/>
```
source "https://rubygems.org”
ruby "2.6.3"
<br/>
group :development, :test do
  gem "rspec"
  gem "my_other_gem"
end
```
>**READ INSTRUCTIONS PROPERLY:** when we grouped for the "10 minutes walk" project, all my group started it from a completely wrong approach because none of us read the instructions carefully. We were suppossed to "_Create a function that will return true if the walk will take you exactly ten minutes and will return you to your starting point._" Instead we started creating an app that would generate the walks that would cover those parameters, which is a much longer process. We still practiced TDD which was the main point, but reading the instructions should definitely be in our top priorities.

<br>

## Tuesday 25th February 2020
### MORNING GOAL
Improve Domain Model Diagramming
Improve TDD

**Plan:**
- Attend Domain Model Workshop with Josh
- Redo "10 minute walk" project from a correct approach

**Process:**
Workshop:
- Use a _Class Diagram_ to build the _Domain Model_ for a Notebook app (in groups)

| NOTEBOOK         | NOTE         | TAG             |
| :--------------: |:------------:|:---------------:|
| note             | tag          |                 |
| create_note<br/>save_note<br/>search_tag(tag) | add_tag(tag) <br/> | create_tag(tag_name) |

- Build the structure of your code based in that model.
```rb
class Notebook

  def create_note
    # return Note.new
  end

  def save_note
    # saves Note.new to notebook
  end

  def search_tag(tag)
    # searches al notes within notebook with that tag
  end
end

class Note
  def add_tag(tag)
    # adds a tag(tag name) to a note
  end
end

class Tag
  def create_tag(tag_name)
    # creates a new tag
  end
end
```
<br/>
Redo 10 Minute Walk<br/>
I am happy with my approach to TDD in this project, I managed to build all my code on a test-firs basis and it works following all the given conditions.

**What I've Learnt:**
>**Class Diagram:** represents the relationships between objects in your model. The objects in your model are represented by boxes subdivided into up to three sections. The name of the object is placed in the top section, any instance variables go in the middle, and methods are listed in the bottom section. The boxes on the left know about the boxes on the right, hierarchy system.

| OBJECT 1           |  OBJECT 2     | OBJECT 3       |
| :----------------: | :------------:| :-------------:|
| STATE (inst_var)   |               |                |
| BEHAVIOUR (methods)|               |                |



<br>

### AFTERNOON

**Plan:**
Pair with Liam and practice TDD working on the Oystercard Project

**Process:**
- Create a new branch in the Github repository to work with a new pair without overwriting the previous work with a different collaborator.
- Give the card the possibility to touch in and touch out and define an in-journey status: we initialize an instance variable `@travelling = false` and placed it inside the `in_journey?` method to make it always return true or false. Touch_in method will change it to true and touch_out back to false.

**What I've Learnt:**
>**Predicate Methods:** they end with "?" and return either true or false.<br/>


>**Branches in Git:** process to create a new branch from your command line:
1. Pull changes so your master is up to date
2. Create the branch on your local machine and switch in this branch:
```
git checkout -b [name_of_your_new_branch]
```
3. Push the current branch and set the remote as upstream:
```
git push --set-upstream origin sri_jara
```
4. When you want to commit something in your branch, be sure to be in your branch. You can see all the branches created by using:
```
git branch -a
```
5. Add a new remote for your branch:
```
git remote add [name_of_your_remote] [name_of_your_new_branch]
```
6. Push changes from your commit into your branch:
```
git push [name_of_your_new_remote] [url]
```

<br>

## Wednesday 26th February 2020
### MORNING GOAL
- Learn how to give and receive feedback.
- Get some understanding on how classes relate to each other.

**Plan:**
- Attend Dana's workshop.
- Read OO_Relationships 1 (Forwarding).

**Process:**
- Read about Forwarding relations in OO
- Refactor some code with this premises.
```rb
class User

  def initialize(name, bio, age, password)
    @name = name
    @bio = bio
    @age = age
    @authentication = Authenticate.new(password)   # Initializes the second class with the same argument
  end

  def authenticate(candidate_password)
    @authentication.authenticate(candidate_password)   # Calls #authenticate from the second class which does the work
  end

  def profile
    print "#{@name}, born in #{birth_year}: #{@bio}"
  end

  private

  def birth_year
    Time.new.year - @age
  end
end

class Authenticate
  def initialize(password)
    @password = password
  end

  def authenticate(candidate_password)
    return true if candidate_password == @password 
    false
  end

end
```

**What I've Learnt:**
>**Feedback Types:** Appreciation (_conect, motivate, reassure, thank_), Evaluation (_rate against a set of standards_) and Coaching (_help receiver to expand Knowdledge or improve capability_).

>**Forwarding:** In object-oriented programming, forwarding means that using a member of an object (either a property or a method) results in actually using the corresponding member of a different object: the use is forwarded to another object.


<br>

### AFTERNOON GOAL
Practice Pairing and TDD

**Plan:**
Pair with Kate and keep working on the Oystercard Project.

**Process:**
- Set a minimum balance to touch_in (create a constant `MIN_FARE = 1` and fail to touch_in if balance is lower)
- Charge for the journey (at touch_out deduct MIN_FARE from balance. Set deduct as a private method)
- Save the Entry station (update #touch_in to get name_station as an argument and save it as an instance variable. Make that variable go back to nil at touch_out)
- Re-write in_journey? to depend on @entry_station (Use a double bang inside the method)
```rb
  def in_journey?
    !!@entry_station  # converts @entry_station in a boolean (will return true for any value thats not nil/false)
  end
```
- Save the Exit station
- Create a Journey History (at #touch_out push a hash with @entry_station and @exit_station into the @journey_history array)
```rb
@journey_history << {:entry_station => @entry_station, :exit_station => @exit_station}
```
- Create a station class that initializes with name and zone.

**What I've Learnt:**
>**Call a private Method from Rspec:** 
```rb
expect { subject.send(:deduct,5) }.to change{ subject.balance }.by -5
```
>**Double Bang:** When using the not-operator(!) we turn the data it’s operating on into a Boolean before negating it. A truthy value would become the Boolean false and a falsey value would become the Boolean true. <br/>
When we add the second bang (!!) it flips the resultant Boolean back to the appropriate value: it will make a truthy value into the Boolean true and a falsey to false.
```rb
"hello"   #-> this is a string; it is not in a boolean context
!"hello"  #-> this is a string that is forced into a boolean 
          #   context (true), and then negated (false)
!!"hello" #-> this is a string that is forced into a boolean 
          #   context (true), and then negated (false), and then 
          #   negated again (true)
```

<br>

## Thursday 27th February 2020
### MORNING GOAL
Understand more about relations between classes

**Plan:**
- Read OO_Relationships 1 (Polymorphism) and do the excercises.


**Process:**
- Refactor the code to a Polymorphic pattern: originally a diary that will have two different ways of scrambling the text and its corresponding unscrumbling methods.
- Create a class for each pair of scramble/unscramble techniques.
- Create a Diary class that initializes with @content, and has a method scramble that takes the chosen scramble_technique_class name as an argument and scrambles the @content with that chosen method. Unscramble will also call the chosen class to decode the @content.
```rb
class ScrambledDiary
  def initialize(contents)
    @contents = contents
  end

  def scramble(scrambler_class)   # pass it to the chosen scrambler class
    @contents = scrambler_class.new(@contents).scramble
  end

  def unscramble(unscrambler_class)
    @contents = unscrambler_class.new(@contents).unscramble
  end
end

class ScrambleByReversing
  def initialize(contents)
    @contents = contents
  end

  def scramble
    p @contents = @contents.reverse
  end

  def unscramble
  p  @contents = @contents.reverse
  end
end
```

**What I've Learnt:**
>**Polymorphism with Duck-Typing:** it refers to the ability to use functions or methods in different ways for different objects or data types. A polymorphic method will behave differently depending on the object that receives it’s message (it allows to send the same message to different objects and get different results). It greatly decreases the need for long, ugly if/else statements.<br/>
(_It would be useful for a website that can be seen in different languages. Every language will be a different class, but will be basically doing the same. We will call the same methods but in a different language._)

<br>

### AFTERNOON GOAL
Practice TDD and Pairing

**Plan:**
Pair with Sri and keep working on the Oystercard Project.

**Process:**
- Refactor all the code to implement a new Journey class that will share methods with our Oystercard class.
- Oystercard class will keep `#top_up`, `#touch_in`, `#touch_out` and `#deduct`.
- Journey will get `#start_journey`, `#finish_journey` and `#in_journey?`
- Everytime we initialize a new card it will create a new `@journey_history = []` and a `@journey = Journey.new`.

(_`#touch_in` will relate to `#start_journey` that will do its work and `#touch_out` will do the same with `#end_journey`_)

```rb
class Oystercard
  def initialize
    @balance = 0
    @journey = Journey.new
    @journey_history = []
  end
  
  def touch_in(entry_station)
    fail "Not enough money in your card" if @balance < MIN_FARE
    @journey.start_journey(entry_station)
  end
end
```

**What I've Learnt:**
>**attr_accessor:** it allows an instance variable to be read and written from a different class. (_We assigned it to our `@journey_history` array (Oystercard class) so we could push our `@current_journey` hash (Journey class) into it and then restore it back to empty everytime at `#touch_out`._)

<br>

## Friday 28th February 2020
### MORNING GOAL
- Understand more about relations between classes

**Plan:**
- Go through the Skill-Workshop OOP 3: Delegate, Delegate, Delegate

**Process:**
- This project contains two implementations of a todo list: /terrible and /great. <br/>
/terrible implements the features using a poor understanding of the delegate principle. /great implements the users stories using a good understanding of the delegate principle but it is unfinished.
- TodoList class will initialize with and `@todos = []` and have a method `#add` and `#set_complete` (delegating into Todo class) and a method `#to_string` (delegating into ListPrint class).
- Todo class will have the functionalities that create every new item and save them into the list and that allows to mark them as completed.
- ListPrint class will have the functionality to print all the items from the list as strings.<br/>

**What I've Learnt:**
>**Delegation:** one class tells another class to do something and the other class encapsulates how to do it.

>**Steve Jobs:** _Objects are like people. They’re living, breathing things that have knowledge inside them about how to do things and have memory inside them so they can remember things. And rather than interacting with them at a very low level, you interact with them at a very high level of abstraction, like we’re doing right here. 
Here’s an example: If I’m your laundry object, you can give me your dirty clothes and send me a message that says, “Can you get my clothes laundered, please.” I happen to know where the best laundry place in San Francisco is. And I speak English, and I have dollars in my pockets. So I go out and hail a taxicab and tell the driver to take me to this place in San Francisco. I go get your clothes laundered, I jump back in the cab, I get back here. I give you your clean clothes and say, “Here are your clean clothes.” 
You have no idea how I did that. You have no knowledge of the laundry place. Maybe you speak French, and you can’t even hail a taxi. You can’t pay for one, you don’t have dollars in your pocket. Yet I knew how to do all of that. And you didn’t have to know any of it. All that complexity was hidden inside of me, and we were able to interact at a very high level of abstraction. That’s what objects are. They encapsulate complexity, and the interfaces to that complexity are high level._

<br>

### AFTERNOON GOAL
Practice TDD

**Plan:**
Keep going with the Oystercard Project

**Process:**
- Refactor the tests: after moving all the code into two different classes many tests were failing. I created two spec files and distributed the tests to be executed within their own class methods.
- Add a PENALTY_FARE that would be deducted if we fail to `#touch_in` or `#touch_out`.
- I created a `#fare` method that will work for `#deduct` by checking wether `@entry_station` or `exit_station` are nil and choose the right fare for `#deduct` to apply. (_So far I managed to make it work if we fail to `#touch_in` but not if we fail to `#touch_out`_)
- I created a `#reset_journey` method that will put all the constant variables back to nil after a journey.

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
* I added stretching to my morning routine and did it every day!!

<br>
