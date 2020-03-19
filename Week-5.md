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

>**This Keyword:** As we could write, “John is running fast because **he** is trying to catch the train.” We could use 'John' again instead of 'he', so in a similar way we use the keyword 'this', as a shortcut, a referent; it refers to an object; that is, the subject in context, or the subject of the executing code.

```javascript
var person = {
    firstName: "Penelope",
    lastName: "Barrymore",
    fullName: function () {
        // Notice we use "this" just as we used "he" in the example sentence earlier?:
        console.log(this.firstName + " " + this.lastName);
    // We could have also written this:
        console.log(person.firstName + " " + person.lastName);
    }
}
```

>If we use person.firstName and person.lastName, as in the last example, our code becomes ambiguous. Consider that there could be another global variable (that we might or might not be aware of) with the name “person.” Just like the pronoun “he” is used to refer to the antecedent (antecedent is the noun that a pronoun refers to), the this keyword is similarly used to refer to an object that the function (where this is used) is bound to. The this keyword not only refers to the object but it also contains the value of the object.


<br>

## Wednesday 18th March 2020
### MORNING GOAL

**Plan:**
- Attend Workshop with Eoin: 'Encapsulation with constructor and prototype pattern'

**Process:**
- Constructor Function: creates several objects of the same 'type'.
```javascript
function Person(first, last, age, eye) {
  this.firstName = first;
  this.lastName = last;
  this.age = age;
  this.eyeColor = eye;
}
```

In this case you can create as many persons as you want giving those parameters:

```javascript
var myFather = new Person("John", "Doe", 50, "blue");
var myMother = new Person("Sally", "Rally", 48, "green");
```

- Prototype function: object that can add properties to the constructor function and enables all its objects to share those properties and methods.

```javascript
Person.prototype.sayName = function() {
  console.log(this.firstName);
}

console.log(myFather.sayName()) => 'John'
```


- Then we paired and worked over some very similar code examples trying to guess which would be the output depending on the constructor-prototype patterns.


<br>

### AFTERNOON GOAL

**Plan:**
Pair with Patrick and work over the Thermostat Project

**Process:**
- User story: 'Power saving mode is on by default'
  - Add a new property to our thermostat that makes `this.PSMOn` be true or false (default is true) and a method to get it `isPSMOn`.
  - Add the posibility to switch it on and off with two new prototypes that change the property.
  ```javascript
  Thermostat.prototype.switchPSMOff = function() {
    this.PSMOn = false;
  };
  ```
- User story: 'If power saving mode is on, the maximum temperature is 25 degrees'.
  - We need a loop to test this, making it press 'up' more than 5 times and still expecting that temperature remains at 25.
  - We create a constant with the upper limit temperature with PSM on: `this.MAX_TEMP_PSM_ON = 25;`
  - And we update the 'up' prototype in our code to break if current temperature is the limit one (so up will not work).
- User story: 'If power saving mode is off, the maximum temperature is 32 degrees' (same process)
- User story: 'You can reset the temperature to 20 with a reset function'
  - It returns the property temperature to default (20).
- User story: 'You can ask about the thermostat's current energy usage: < 18 is low-usage, < 25 is medium-usage, anything else is high-usage.'
  - Create a `energyUsage` protoype that with an if/else condition returns low, medium, or high comparing `this.temperature` to the levels.
  
- INTERFACE: HTML/CSS
- Create all the elements you need to serve as controls and display data on the thermostat.
- Add your `thermostat.js` file to your document in a `<script>`

<br>

## Thursday 19th March 2020
### MORNING GOAL

**Plan:**
Attend workshop with Eoin: 'Following the flow and getting visibility'

**Process:**
- Following the flow: When debugging JavaScript we do something similar to the tightening the loop technique but with a different goal. Instead of trying to narrow in on one buggy line of code, you're just trying to understand what happens when a piece of code runs. 
  - Typing little strings that you recognize with `console.log()`. Things in JS sometimes happen in unexpected order so it's good to know which is the actual running order by seeing the order in which these little strings are being printed.
  - Using a step debugger: a program that runs your program and lets you step through your program line by line. _Run the program and go to the sources tab of the JS console_
- Getting visibility: `console.log()`
  - This: know what value `this` has in a piece of code `console.log(this);`.
  - Variables: check that it contains what you expect `console.log(airport);`.
  - Funtions: am I calling the right function? `console.log(airport.land);`.
  - Function return values: is the function returning what I expect? `console.log(airport.land());`.
  - Function parameters: does this parameter contain what I expect?
  ```javascript
  Airport.prototype.land = function(plane) {
    console.log(plane);
  }
  ```
- After explaining the basic concepts we paired up and worked debugging some FizzBuzz code that was broken.

<br>

### AFTERNOON GOAL

**Plan:**
Plan with Will and work over Thermostat Project

**Process:**
- JQUERY
- Download jQuery [here](https://jquery.com/download/), store it with your HTML file and load it with a script.
- Basic concepts:
  - `$(document).ready(function() { })`: This function wraps the rest of the code so no events happen until the whole document has been loaded.
  - jQuery selector: `$('element')` where 'element' is a CSS selector, or a tag name, classes, ids...
  - Event listener: `$('element').on('event', function() {})` where 'event' is an action you would like to listen for on the page. Popular events include clicks, scrolls, typing and generally any kind of page interaction. The most popular ones generally have convenient shortcut functions, so you can write `$('element').click(function() { })`.
  - Callbacks: anonymous function passed as last argument to the event handler. In this case, the callback is the function passed to the click function, that executes at some point in the future. The plain English translation would be "when there is a click on the element with the ID some-heading, run the function".
  ```javascript
  $('#some-heading').click(function() {
    // this function is the callback!
  })
  ```
- Back to our code, we firstly create a new instance of the thermostat object: `var thermostat = new Thermostat();` wrapped in the document loading function.
- We start implementing every action that happens within our app following this flow: <br>
**user input -> event listener -> update model -> update view to reflect change in model**
```javascript
$('#temp-up').on('click', function() { // event listener
  thermostat.increaseTemperature(); // update model
  $('#temperature').text(thermostat.temperature); // update view
})
```
- Once it all works the way we want we implement the colour changes according to the energy usage.
  - Delegate this functionality to the CSS: change the class name and let CSS assign a colour according to the class name.
  - Our energyUsage function could return low, medium or high. 
  - Give our temperature HTML id an attribute class with the value assigned to the return of that function. 
  - Create three different CSS stylings to each of those class values, et voila.


- APIs
- Use a jQuery AJAX call to get the weather information for London from a weather API and display the weather information to the user.
  - `$.get()` is shorthand for `$.ajax()`
  - This function will get an url for the given city and return the data for temperature in Celsius as unit.
```javascript
function displayWeather(city) {
    var url = 'http://api.openweathermap.org/data/2.5/weather?q=' + city;
    var token = '&appid=a3d9eb01d4de82b9b8d0849ef604dbed';
    var units = '&units=metric';
    $.get(url + token + units, function (data) {
      $('#current-temperature').text(data.main.temp);
    });
```

- Add further functionality so that the user can select their current city and the weather provided is for the selected city.
  - Create a select menu in HTML with an `id='current-city'` and the name of the city assigned as value to each option.
  - This function will assign to a variable the value of the selected item in the menu and then pass it to the `displayWeather(city);` function.
 ```javascript
 $('#current-city').change(function(){
    var city = $('#current-city').val();
    displayWeather(city);
  });
 ```

**What I've Learnt:**
>**JQuery:** is a JavaScript library that simplifies JS programming. It takes a lot of common tasks that require many lines of JavaScript code to accomplish, and wraps them into methods that you can call with a single line of code. Contains the following features: HTML/DOM manipulation, CSS manipulation, HTML event methods, Effects and animations, AJAX and Utilities.

>**APIs:** Application Programming Interface is a computing interface exposed by a particular software program, library, operating system or internet service, to allow third parties to use the functionality of that software application. The "API" referred to is not intended to extend the functionality of the source website or service, but merely to use it. 

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
