# Week 5 Goals
* Test drive a simple front-end web app with Javascript
* Follow an effective process for learning a new language

<br>

***

<br>

# Daily Goals

## Monday 16th March 2020
### MORNING GOAL

Get a main idea about what is Javascript.

**Plan:**
- Pair review the weekend challenge
- Attend Kick-off workshop with Eoin
- Get started with JS.

**Process:**

I decided to invest the time I had left in the morning to have a quick look at all the resources available for the week and chose to begin with the 'Introduction to Javascript (and Jasmine)' learning pill, as I had no idea of what JS was about.

The challenge is about setting up Jasmine and Javascript and translating our old project 'FizzBuzz' into this new language.

- Jasmine is the testing framework for JS, I downloaded [here](https://github.com/jasmine/jasmine/releases) and installed the last version in my computer.
- To use Jasmine in your own project create a new directory with the appropriate name, e.g. FizzBuzz and transfer over the lib directory intact.
```
cp -r ~/Downloads/jasmine-standalone-3.5.0/lib .
```
- Now we need to create a test file, and a file for our code: `spec/FizzbuzzSpec.js` and `src/Fizzbuzz.js`
- To finish Jasmine setup create a file at your root directory `SpecRunner.html` with the following code:
```html
<!-- include source files here... -->
  <script type="text/javascript" src="src/Fizzbuzz.js"></script>

  <!-- include spec files here... -->
  <script type="text/javascript" src="spec/FizzbuzzSpec.js"></script>
```
- We are now ready to start testing!
- This is the main structure for testing in Jasmine/JS: Function {} acts like Ruby's do/end
```javascript
describe('', function() {

//method statements go here

});
```
- Our first test should look something like this:
```javascript
describe('FizzBuzz', function() {

  var fizzbuzz;
  
  beforeEach(function() {
    fizzbuzz = new FizzBuzz();
  });

  describe('multiples of 3', function() {
    it('fizzes for 3', function() {
      expect(fizzbuzz.play(3)).toEqual('Fizz');
    });

  });

});
```
- Let's split it up:
  - We give our described method a name 'FizzBuzz' (like the file we created, something like a class name in ruby)
  - Declare a variable inside the function block. It will be a local variable and it's only available withing the nearest {}. _If not declared it will look in every parent function and if still can't find any it will create it for you in the top level, but it will be a global variable, which is not a good practice_.
```javascript
var fizzbuzz;
```
  - Jasmine has no context blocks but we can open a new `describe` function with an `it`.
  - We then need an instance of FizzBuzz to test against so we create it inside out it block: _when we are instantiating our version of the class - we MUST add the `();`_
  ```javascript
   fizzbuzz = new FizzBuzz();
  ```
  - Now we just need an expectation withing our it block:
  ```javascript
  expect(fizzbuzz.play(3)).toEqual('Fizz');
  ```
- Our test is ready, but notice the methods are named with CamelCase in Javascript convention.
- Let's move into the code to make it pass: _this is the whole code for the program. It creates a first function `FizzBuzz` (in ruby this would be the class) and then two other functions depending on it (methods in ruby)._

```javascript
function FizzBuzz() {
}

FizzBuzz.prototype.play = function(number) {
  if (this._isDivisibleBy(15, number)) {
    return 'FizzBuzz';
  } else if (this._isDivisibleBy(5, number)) {
    return 'Buzz';
  } else if (this._isDivisibleBy(3, number)) {
    return 'Fizz';
  } else {
    return number;
  }
}

FizzBuzz.prototype._isDivisibleBy = function(divisor, number) {
  return number % divisor === 0;
}
```

<br>

### AFTERNOON

**Plan:**

Pair with Stephan and Georige and get started with the afternoon challenge 'Thermostat'.

**Process:**
- First steps of the proyect were translating FizzBuzz and Airport challenges to get a grip on Javascript and Jasmine syntax. We did fizzbuzz together and then have a quick look at the airport but decided to do it as solo work during the week.
- We started with the first user story for Thermostat: `Thermostat starts at 20 degrees`
- First we write the test:

```javascript
// spec/thermostatSpec.js

'use strict';

describe('Thermostat', function() {

  var thermostat;

  beforeEach(function() {
    thermostat = new Thermostat();
  });

  it('starts at 20 degrees', function() {
    expect(thermostat.temperature).toEqual(20);
  });
});
```

- And then the code:
```javascript
// src/thermostat.js

'use strict';

function Thermostat() {
  this.temperature = 20;
}
```

**What I've Learnt:**
>**Strict Mode** blabla

<br>

## Tuesday 17th March 2020
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

## Wednesday 18th March 2020
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

## Thursday 19th March 2020
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

## Friday 20th March 2020
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
