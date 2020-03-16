# Week 5 Goals
* Test drive a simple front-end web app with Javascript
* Follow an effective process for learning a new language

<br>

***

<br>

# Daily Goals

## Monday 16th March 2020
### MORNING GOAL

Get a main idea about what is JS

**Plan:**
- Pair review the weekend challenge
- Attend Kick-off workshop with Eoin
- Get started with JS.

**Process:**

I decided to invest the time I had left in the morning to have a quick look at all the resources available for the week and chose to begin with the 'Introduction to Javascript (and Jasmine)' learning pill, as I had no idea of what JS was about.

- Jasmine is the testing framework for JS, I downloaded [here](https://github.com/jasmine/jasmine/releases) and installed the last version in my computer.
- To use Jasmine in your own project create a new directory with the appropriate name, e.g. JavaBuzz and transfer over the lib directory intact.
```
cp -r ~/Downloads/jasmine-standalone-3.5.0/lib .
```
- Now we need to create a test file, and a file for our code: `spec/JavabuzzSpec.js` and `src/Javabuzz.js`
- To finish Jasmine setup create a file at your root directory `SpecRunner.html` with the following code:
```html
<!-- include source files here... -->
  <script type="text/javascript" src="src/Javabuzz.js"></script>

  <!-- include spec files here... -->
  <script type="text/javascript" src="spec/JavabuzzSpec.js"></script>
```
- We are now ready to start testing!
- This is the main structure for testing in Jasmine/JS: Function {} acts like Ruby's do/end
```javascript
describe('', function() {

//method statements go here

});
```
- Our final test should look something like this:
```javascript
describe('Javabuzz', function() {

  var javabuzz;

  describe('knows when a number is', function() {

    it('divisible by 3', function() {
      javabuzz = new Javabuzz();
      expect(isDivisibleByThree(3)).toBe(true);
    });

  });

});
```
- Let's split it up:
  - We give our described method a name 'JavaBuzz' (like the file we created, something like a class name in ruby)
  - Declare a variable inside the function block. It will be a local variable and it's only available withing the nearest {}. _If not declared it will look in every parent function and if still can't find any it will create it for you in the top level, but it will be a global variable, which is not a good practice_.
```javascript
var javabuzz;
```
  - Jasmine has no context blocks but we can open a new `describe` function with an `it`.
  - We then need an instance of Javabuzz to test against so we create it inside out it block: _when we are instantiating our version of the class - we MUST add the `();`_
  ```javascript
   javabuzz = new Javabuzz();
  ```
  - Now we just need an expectation withing our it block:
  ```javascript
  expect(isDivisibleByThree(3)).toBe(true);
  ```
- Our test is ready, but notice the methods are named with CamelCase in Javascript convention. Also it doesn't take `?` at the end of the method but instead puts `is` at the beggining.
  


**What I've Learnt:**
>**this** blabla

<br>

### AFTERNOON GOAL

**Plan:**

**Process:**
**What I've Learnt:**
>**this** blabla

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
