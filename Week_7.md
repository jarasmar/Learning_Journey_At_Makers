# Week  Goals

By the end of the week all developers can:

- Build a front-end app in Javascript
- Work competently in Javascript 
- Reason about asynchronous behaviour in Javascript

This week is analogous to week 2 in that developers will be wrestling with some underlying language concepts that are not well understood (by Makers).

Most of the work and interventions we have run historically are meant to 'de-magic' Javascript and force developers to confront the pieces they are glossing over in an attempt to get work done.


<br>

***

<br>

# Daily Goals

## Monday 30th March 2020
### MORNING GOAL

Make a working plan for the week and start it.

**Plan:**

- First Half Morning: JS syntax in FreeCodeCamp
- Rest of the morning: Practicals
    - Asynchronous JS
    - Makers Pills:
      - Arrays
      - jQuery events 
      - Mocking
      - Front end single page app
    - JS Closures
    - Semicolons use

**Process:**

**Semicolons in JavaScript:**
- Required: when two statements are on the same line.
  ```javascript
  var i = 0; i++         // <-- semicolon obligatory
                        //     (but optional before newline)
  var i = 0            // <-- semicolon optional
  i++                 // <-- semicolon optional
  ```
- Optional: after statements (a piece of code that tells the computer to do something). It can be omitted if the statement is followed by a line break, like the example above.
- Avoid: after curly braces (except in a function definition)
  ```javascript
  // NO semicolons after }:
  if  (...) {...} else {...}
  for (...) {...}
  while (...) {...}

  // BUT:
  do {...} while (...);

  // function statement: 
  function (arg) { /*do this*/ } // NO semicolon after }
  ```
  
- Avoid: after the round bracket in an if, for, while or switch statement.
  ```javascript
  // After the ) changes the action completely:
  if (0 === 1); { alert("hi") }

  // equivalent to:

  if (0 === 1) /*do nothing*/ ;
  alert ("hi");
  ```
**JQuery Events:**
- To set up an event handler we'll use a jQuery method called on. We'll usually pass one argument to on the name of the event we want to react to (a click for example) and a function to know what action to take when the event occurs. In the example we will be dynamically adding an element to a list on the page.
```javascript
// #add is the button's ID in HTML

$('#add').on('click', function() {
  var $newItem = $('<li>New item</li>')
  $newItem.appendTo('.items');
});
```
- When we create an element dynamically it has a problem: the click handler is loaded with the whole document, so all preexistent elements know how to behave, but those created dynamically doesnt (as the document is not being reloaded). 
    - We need to nominate a responsible parent up the DOM tree. Body is always an option as it includes all the code, but you can also use some container that is closer, like the list in this case (we give it a class `items`).
    - Make very new element created dynamically be appended to its parent (class item)
    ```javascript
    $(document).ready(function() {
        $('#add').on('click', function() {
            var $newItem = $('<li>New item</li>')
            $newItem.appendTo('.items');
        });
    
        $('.items').on('click', 'li', function() {
            $(this).remove();
        });
    });
    ```

<br>

### AFTERNOON GOAL

**Plan:**
Pair with Karla and start the Note App Project.

**Process:**
**Writing tests without a Testing Library:**
- We can create a JavaScript file with functions that will act as tests for our model functions.
- Use a script tag to add our test file in index.html
- Run it in the browser and in the console you will see the fails.
```javascript
// circle-tests.js

(function(exports) {
  function testCircleRadiusDefaultsTo10() {
    var circle = new Circle();

    if (circle.radius !== 10) {
      throw new Error("Circle size is not 10");
    }
  };

  testCircleRadiusDefaultsTo10();
})(this);
```
- This can be refactored to have a template function 'assert'
```javascript
// assert.js

var assert = {
  isTrue: function(assertionToCheck) {
    if (!assertionToCheck) {
      throw new Error("Assertion failed: " + assertionToCheck + " is not truthy");
    }
  };
};

// circle-tests.js

function testCircleRadiusDefaultsTo10() {
  var circle = new Circle();
  assert.isTrue(circle.radius === 10);
};

testCircleRadiusDefaultsTo10();
```

**Module Pattern:**
- A design pattern to encapsulate JavaScript code.
- An Immediately-invoked Function Expression (IIFE) is a way to execute functions immediately, as soon as they are created.
- They are very useful because they don’t pollute the global object, and they are a simple way to isolate or hide variables or function declarations. 
```javascript
// This is the syntax that defines a IIFE

(function() {
  /* */
})()
```
- The code in an IFFE is 'hidden', none of the rest of the code can access any variables or functions inside the IIFE.
- The module pattern is basically just an IIFE. But it uses a bit of extra code to export (or expose, or make available to the outside, or show) functions and variables that are part of the public interface of the module.
```javascript
(function(exports) {
  var EXCLAMATION_MARK_COUNT = 5

  function exclaim(string) {
    return string + "!".repeat(EXCLAMATION_MARK_COUNT);
  };

  exports.exclaim = exclaim;
})(this);
```
_`this` and `exports` are the global object. This means that adding exclaim onto exports is effectively making exclaim globally available._

**Back to the Project**
- Testing without a test library and wrapping all the code in the module pattern, use the contructor and prototype pattern to define a note model object that can be instantiated.
- The note takes a text property upon instantiation (hardcoded for now).
- Build a method that returns the text.
- Create a new object that stores a list of notes (`noteList`) in an array.
- Build a method that returns the contents of the array
- Build a method that creates and stores a new note. It takes a string as an argument that would be the text for the new note. 
- In order to display our notes we need to convert them into HTML.
- Create a new object (`noteListView`) that instantiates with a `noteList`.
- Build a method that returns a HTML string that represents the noteList.
    - The noteList array doesnt contain only strings, so first we create a new array that only has the text of every note.
    - Then we interpolate every string into the HTML pattern.
```javascript
NoteListView.prototype.generateView = function() {
    var textArray = [];
    for (var i = 0; i < this.noteList.noteList.length; i++) {
      textArray.push(this.noteList.noteList[i].text);
    }

    return('<ul><li><div>' + textArray.join('</div></li><li><div>') + '</div></li></ul>');

  }
```

<br>

## Tuesday 31st March 2020
### MORNING GOAL
Validate my approach for learning a new language.

**Plan:**

Read through some of the resources on my list and talk to a coach about my approach.

**Frontend Single Page App**
- The essence of a frontend, single page app is that the browser never refreshes the page. 
- Once the page loads, all changes happen by inserting HTML into the existing page.
- When we do one action (like a click) the change is inserted into the page dynamically, not sent from a server after a request/response cycle and a page refresh.
- We use `clickEvent.preventDefault()` to prevent the link action to refresh the page (which does by default).
- It can also have a navigation architecture (a web of different pages):
    - We make the link redirect to a new page that will display the action. The new URL will include a `#`
    - Navigating to the new URL doesn't refresh the page so data is retained while navigating the different pages.

**What I've Learnt:**
>**ESlint** tool that can be plugged to your text editor and analyzes the code to quickly find problems and keep it consistent.

<br>

### AFTERNOON GOAL

**Plan:**
Plan with Nima and keep working on the afternoon challenge.

**Process:**
- Spike to create and serve an index.html page for your app:
    - Create an index.html file containing the minimal HTML structure and add a div that has an id attribute set to app and contains the text hello.
- Install Node JS
- Install http-server from [NPM](https://www.npmjs.com/package/http-server). It is a small library that runs a local server to serve static assets like HTML, CSS and JavaScript. It's useful for serving a frontend website locally. Run it:
```
$ cd root/of/your-project/
$ npm install http-server --save
$ node node_modules/http-server/bin/http-server
```
- Go to [http://localhost:8080/](Go to http://localhost:8080/) in a browser to view your index.html page. It should say hello.

- Spike code that inserts some HTML into the index.html page.
    - Create a note-controller.js file and use a script tag to load it in your index.html file.
    - Add code that gets hold of the app div element in your index.html page. console.log the element to be sure you've got it.
    - Add code that can change the app greeting from 'hello' to 'howdy'.
    - Visit http://localhost:8080 and check you can see 'howdy'.
- Spike and then TDD code that shows a note in the index.html page
- Create a file called note-controller.js and wrap all your code in module pattern.
- Use constructor/prototype pattern to define a note controller that:
    - Takes a note list model as a parameter.
    - Adds a note that says 'Favourite drink: seltzer'.
    - Creates a note list view, passing the note list model (generate HTML string).
    - Make a method that gets the HTML from the note list view and inserts it into the app element.
    ```javascript
    document.getElementById('app').innerHTML = this.noteListView.generateView();
    ```
    

**What I've Learnt:**

>**Spike:** is a product-testing method originating from Extreme Programming that uses the simplest possible program to explore potential solutions. It is used to determine how much work will be required to solve or work around a software issue.

>**Node JS:** it allows you to "build fast, scalable network applications" using Javascript on the server side. This means that if you choose the path of Javascript, you can become full-stack with a single language.

>**NPM:** node based package manager, that will help you to organise and version control Node Packages on your machine and in your projects. Is the equivalent of Bundler from Ruby, as Node packages function in a similar way as Ruby gems.

<br>

## Wednesday 1st April 2020
### MORNING GOAL

**Plan:**
- Attend workshop on Module Pattern with Eoin.
- Create a Diagram of the afternoon project

![Diagram](images/NotesAppDiagram-Wednesday.png)

<br>

### AFTERNOON GOAL

**Plan:**
Pair with George and work on the Notes App.

**Process:**
- TDD a single note view: (so it can be displayed in its own individual page)
    - In a new file `single-note-view.js` TDD a SingleNote object that initializes with a note.
    - Give it a method that takes that note and converts it to HTML (similar than the one that returns the whole list but for an individual note).
    ```javascript
    SingleNoteView.prototype.displayNote = function() {
        return '<div>' + this.note.text + '</div>'
    }
    ```
- Update your code so the main list of notes only shows the first 20 characters of each one.
    - Modify the `generateView` method so that when it creates the HTML string joining all the note's texts into a table cuts them to 20 characters.
    ```javascript
    NoteListView.prototype.generateView = function() {

    return('<ul><li><div>' + 
    this.noteList.notes.map(note => note.text.slice(0, 20)).join('</div></li><li><div>') + 
    '</div></li></ul>');

    }
    ```


<br>

## Thursday 2nd April 2020
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

## Friday 3rd April 2020
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
