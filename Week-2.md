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
Practice Pair Programming and TDD

**Plan:**
1. Pair with Kuba and start working on the Oystercard Project.
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
