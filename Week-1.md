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
```
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

```
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

## Friday 21st February 2020
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
