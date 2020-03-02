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

**Process:**
- Review this tomorrow morning

**What I've Learnt:**
>**This:** blabla

<br>

## Tuesday 3rd March 2020
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

## Wednesday 4th March 2020
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

## Thursday 5th March 2020
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

## Friday 6th March 2020
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
