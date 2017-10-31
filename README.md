# Prototypal Inheritance

## Learning Objectives
- Demonstrate a use case that explains prototypal inheritance and what kind of flexibility it gives to programmers
- Use namespaces to organize application code
- Define a custom constructor method that sets one or more properties of a new object

## What is prototypal inheritance?
...
### What is inheritance?
![alt text](./images/inheritance_def.png "inheritance definitions")

### What is a prototype?

![alt text](./images/prototype_def.png "prototype definition")

### Prototyping in product design: an analogy
#### Build
Prototyping is an important part of all design. It's a process that allows for incremental testing and improvement of a product. Consider the example of designing a bicycle. First you must develop a prototype, a working model to showcase your design. You brainstorm, sketch, research, weigh the pros and cons of different frame materials, wheel-size, handlebar design, ect. You invest time and money to build your model, a prototype.

![alt text](./images/highwheel_bike.png "highwheel bike")

#### Test
So you test your prototype, you ask for opinions from others, and maybe you run it by potential investors for feedback. Everyone loves the design except they think the color is ugly and they don't like falling over the front when stopping. So what do you do? 

#### Repeat
Naturally you need to create another model, hopefully a better one. Do you start from scratch? Of course not! You reference everything you learning building your first model and you modify it. You keep the parts that are good and improve or replace the parts that aren't to build a new and improved model. This model becomes your current prototype and the cycle continues. Each new model takes qualities from the previous model and builds off them. In other words, __a new model inherits from its prototype__. 

![alt text](./images/bicycle_evolution.svg "evolution of the bicycle")

We don't have to reinvent the wheel every time we create a new bicycle. We can save time and energy focusing on what is specifically new or different rather than repeating the design process from the very beginning.

## Prototypal Inheritance in JavaScript

The concept of a prototype is critical to understanding inheritance in JavaScript and it allows us the same benefits seen in product design.
- prevents unnecessary repetition
- saves time
- helps organize code into smaller pieces

Consider we own a bike shop and we're building a website. We need to represent our inventory as objects to be displayed online.

We could define an object for each bike in the shop...

let bike1 = {
  brand: 'Cannondale',
  type: 'road',
  color: 'red',
  wheels: 2,
	roll: function() {
    console.log('they see me rollin...')
  }
}

let bike2 = {
  brand: 'Trek',
  type: 'mountain',
  color: 'blue',
  wheels: 2,
	roll: function() {
    console.log('they see me rollin...')
  }
}

What's the problem?

### Introducing Constructor functions

Constructor functions help us define new objects with less repetition.
- conventionally, constructor function names start with a capital letter
- constructor functions can be called with the 'new' keyword

First we define our constructor function.
>function Bike (brand, type, color) {
>  this.brand = brand
>  this.type = type
>  this.color = color
>  this.wheels = 2
>  this.roll = function () {
>    console.log('they see me rollin')
>  }
>} 
Then, we call it.
>bike1 = new Bike('Cannondale', 'road', 'red')
>bike2 = new Bike('Trek', 'mountain', 'blue')


function Bike () {
	this.wheels = 2
	this.roll = function () {
		console.log('they see me rollin...')
    }
}

anyBike = new Bike ()

function MountainBike () {
	this.hasSuspension = true
	this.offRoad = function () {
		console.log('bump bump bump bump')
    }
}

MountainBike.prototype = new Bike()

function TrekMtnBike (frameSize, color) {
	this.frameSize = frameSize
	this.color = color
	this.brand = 'Trek'
}

TrekMtnBike.prototype = new MountainBike()

largeBlueTrek = new TrekMtnBike('58cm', 'blue')

