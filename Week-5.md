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

**What I've Learnt:**
>**Functions:** they appear roughly equivalent to three concepts in Ruby: classes, blocks and methods, but it's not exactly like that, a function creates an object that can be called (invoked). 
- There are no classes in JavaScript, but we do use functions as a convenient way to instantiate objects that share behaviour.
```javascript
function Dog(name) {
  this.name = name;
}

var barney = new Dog('Barney');
```
- Anonymous functions work similar as blocks: _This is normally called a callback_
```javascript
var callback = function(arg) {
  console.log(arg);
};

['one', 'two', 'three'].forEach(callback);
```
- Function to define methods:
```javascript
function Dog(name) {
  this.name = name
}

Dog.prototype.bark = function() {
  console.log(this.name + ' says Woof!')
};

# We can call bark in any instance of Dog

fido = new Dog('fido');
fido.bark();
```
_It's easy to think of bark as being a method of Dog. But it isn't. Objects in JavaScript are just bags of properties. So fido is just a bag of properties, some of which it inherits from the prototype of Dog. And bark is just a property that happens to contain a Function object. It behaves like a method because of the way it is invoked_

<br>

### AFTERNOON

**Plan:**

Pair with Stephan and George and get started with the afternoon challenge 'Thermostat'.

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
>**Strict Mode** it makes us write higher standard JS as converts mistakes (that could be passed by without strict mode) into errors, so we can fix them in the moment instead of risking them causing problems in a future when it would be more difficult to find them. For example, it is impossible to create global variables by mistake in strict mode (if you mistype a variable in sloppy mode JS will just create that new object and keep working, but functionality might be affected).

>**Prototype Keyword:** It's important to understand that unlike Ruby where your instances inherit from a class, when it comes to JavaScript, your instances inherit from another object. When the JavaScript interpreter cannot find a property or method defined on the current instance it looks to the next object in the inheritance chain for the missing information.

<br>

## Tuesday 17th March 2020
### MORNING GOAL
Basisc of Javascript and Jasmine

**Plan:**
- Start translating airport challenge from Ruby to Javascript.

**Process:**

- For the first user story I decided to go straight away to the walkthrough to have an example of how classes were related to each other and how to use doubles. 
```
As an air traffic controller
To get passengers to a destination
I want to instruct a plane to land at an airport and confirm that it has landed.
```

- For the second user story I was trying to do every little step on my own, using the previous one as an example and then doublechecking or correcting from the walkthrough.
```
As an air traffic controller
To get passengers to a destination
I want to instruct a plane to take off from an airport and confirm that it is no longer in the airport
```

**What I've Learnt:**
>**Jasmine Spies:** Jasmine has test double functions called spies. A spy can stub any function and tracks calls to it and all arguments. A spy only exists in the describe or it block in which it is defined, and will be removed after each spec. There are special matchers for interacting with spies: `toHaveBeenCalled`, `and.callThrough`, `and.returnValue`, `and.throwError`...

>**Create Spy Object** we use this function in Jasmine when we want to test dependencies that are not available within the actual context, like for creating doubles of other classes. _In the example, while testing Plane we make a 'double' of Airport that takes a function (method) 'clearForLanding' and 'clearForTakeoff._
```javascript
describe('Plane',function(){
  var plane;
  var airport;
  beforeEach(function(){
    plane = new Plane();
    airport = jasmine.createSpyObj('airport',['clearForLanding','clearForTakeOff']);
  });
```


<br>

### AFTERNOON GOAL

**Plan:**
Pair with Artemis and work together on the Thermostat challenge.

**Process:**
- Implement user story: `You can increase the temp with an up function
```javascript
Thermostat.prototype.up = function() {
  this.temperature += 1;
}
```

- Implement user story: `You can decrease the temp with a down function`

- Implement user story: `The minimum temperature is 10 degrees`
  - Now given that our thermostat has a default temperature of 20, and we want to test that we can't go more than 10 degrees below that default, here we employ a loop to handle the cumbersome test setup of calling thermostat.down eleven times.
  
```javascript
// spec/thermostatSpec.js

it('has a minimum of 10 degrees', function() {
  for (var i = 0; i < 11; i++) {
    thermostat.down();
  }
  expect(thermostat.getCurrentTemperature()).toEqual(10);
});
```
  - We add another property to our object constructor function:
  
```javascript
function Thermostat() {
  this.MINIMUM_TEMPERATURE = 10;
  this.temperature = 20;
}
```
  - Create a method to return a boolean check on whether or not the temperature is currently set to the MINIMUM_TEMPERATURE:
  
```javascript
// src/thermostat.js
Thermostat.prototype.isMinimumTemperature = function() {
  return this.temperature === this.MINIMUM_TEMPERATURE;
}
```
  - Add the condition to the down method:
  
```javascript
// src/thermostat.js

Thermostat.prototype.down = function() {
  if (this.isMinimumTemperature()) {
    return;
  }
  this.temperature -= 1;
}
```

**What I've Learnt:**
>**Equality comparisons:** double equals (==) will perform a type conversion when comparing two things, and will handle NaN, -0, and +0. Triple equals (===) will do the same comparison as double equals but without type conversion; if the types differ, false is returned.

>**This Keyword:** blabalaka

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
