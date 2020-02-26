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
```
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
>**Predicate Methods:** they end with "?" and return either true or false. 
>**Branches in Git:** process to create a new branch from your command line:
1. Pull changes so your master is up to date
2. Create the branch on your local machine and switch in this branch:
```
git checkout -b [name_of_your_new_branch]
```
3. Push the branch on github:
```
git push origin [name_of_your_new_branch]
```
4. When you want to commit something in your branch, be sure to be in your branch. You can see all the branches created by using :
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
This goal

**Plan:**
This Plan

**Process:**
This and this

**What I've Learnt:**
>**This:** blabla

<br>

### AFTERNOON GOAL
This goal

**Plan:**
This Plan

**Process:**
This and this

**What I've Learnt:**
>**This:** blabla

<br>

## Thursday 27th February 2020
### MORNING GOAL
This goal

**Plan:**
This Plan

**Process:**
This and this

**What I've Learnt:**
>**This:** blabla

<br>

### AFTERNOON GOAL
This goal

**Plan:**
This Plan

**Process:**
This and this

**What I've Learnt:**
>**This:** blabla

<br>

## Friday 28th February 2020
### MORNING GOAL
This goal

**Plan:**
This Plan

**Process:**
This and this

**What I've Learnt:**
>**This:** blabla

<br>

### AFTERNOON GOAL
This goal

**Plan:**
This Plan

**Process:**
This and this

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
* I added stretching to my morning routine and did it every day!!

<br>
