# Week 10 Goals

- Feel more confident in your ability to complete a tech test.
- Develop a structured process to approaching complex problems, utilising TDD and good OO design skills.
- Solve a challenging technical problem by writing well crafted code (well tested, easy to read and easy to change).

This week, you'll work solo to complete different technical challenges. A self assessment form will help you reflect on the quality of your code, and coaches will review your code once you believe you have achieved professional quality.

<br>

***

<br>

## Bank Tech Test

See the whole project [here](https://github.com/jarasmar/Bank_Tech_Test)

#### Requirements
- You should be able to interact with your code via a REPL like IRB or the JavaScript console. (You don't need to implement a command line interface that takes input from STDIN.)
- Deposits, withdrawal.
- Account statement (date, amount, balance) printing.
- Data can be kept in memory (it doesn't need to be stored to a database or anything)

#### Acceptance criteria

**Given** a client makes a deposit of 1000 on 10-01-2012  
**And** a deposit of 2000 on 13-01-2012  
**And** a withdrawal of 500 on 14-01-2012  
**When** she prints her bank statement  
**Then** she would see

```
date       || credit  || debit  || balance
14/01/2012 ||         || 500.00 || 2500.00
13/01/2012 || 2000.00 ||        || 3000.00
10/01/2012 || 1000.00 ||        || 1000.00
```

#### Approach

I am going to start working in a single class 'Account' that will take the main functionality.
It will evolve into a second class Transaction and then Statement.
Finally, if our app will need to manage several accounts, I will build a class Bank that manages all processes from every account.



## Gilded Rose Refactoring

See the whole project [here](https://github.com/jarasmar/Gilded_Rose_Refactor_Ruby)

#### Specifications

- Item SellIn value: number of days we have to sell the item.
- Item Quality value: how valuable the item is (always between 0 and 50)
- At the end of each day our system lowers both values for every item.
- Once the sell by date has passed, Quality degrades twice as fast.


#### Exceptions

- "Sulfuras": never has to be sold or decreases in Quality
- "Aged Brie": increases in Quality the older it gets
	- Quality increases by 1  before sell_in date
	- Quality increases by 2  after sell_in date
- "Backstage passes": increases in Quality the older it gets:
	- Quality increases by 2 when there are 10 days or less
	- Quality increases by 3 when there are 5 days or less
	- Quality drops to 0 after the concert


#### Implementation

- "Conjured Items": degrade in Quality twice as fast as normal items.
	- Quality decreases by 2 before sell_in date has passed
	- Quality decreases by 4 after sell_in date has passed


#### My approach

- Set up the project, rspec, simplecov and rubocop
- Do test coverage for all the code
- Separate the classes into two different files
- Refactor the code
	- Update_quality method checks the item name and updates the sell_in date.
	- It delegates the update quality functionality into private methods according to the item name
- Implement the new feature 'conjured items'


***

<br>


# Weekend Reflections

### Did you meet all of your goals you set at the start of the week?
* I feel I was very productive this week and I got good feedback from the tech tests I submitted.

### What things do you still need to work through?
* Javascript

### What would you change/improve moving forward?
##### Technical: 
* Put apart some time to read some theoreticals.

##### Personal:
* Go back to an organized meal plan

### A pat on the back
* I went out for a walk in the park everyday.
<br>
