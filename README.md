# Class, Constructors, and Prototypal Inheritance

### Learning Objectives
- Define a custom constructor method that sets one or more properties of a new object
- Use namespaces to organize application code
- Demonstrate a use case that explains prototypal inheritance and what kind of flexibility it gives to programmers

Consider we own a bike shop and we're building a website. We need to represent our inventory as objects to be displayed online.

We _could_ define an object for each bike in the shop...

```javascript
let bike1 = {
  type: 'road',
  color: 'red',
  wheels: 2,
	roll: function() {
    console.log('they see me rollin...')
  }
}

let bike2 = {
  type: 'mountain',
  color: 'blue',
  wheels: 2,
	roll: function() {
    console.log('they see me rollin...')
  }
}
```
...but _should_ we?
What's the problem with this strategy?

### Introducing Class 

Classes help us define new objects with less repetition. Classes in JavaScript are syntactic sugar. They allow us to package the constructor (a method needed to create new objects) and the methods to be used by the new objects in one place.
- conventionally, class names start with a capital letter
- a class can be instantiated with the 'new' keyword

Classes serve as blueprints that give form to new objects. Class declarations contain a method called a constructor which is called automatically with the 'new' keyword. Constructor methods may take arguments which are translated to properties of the new object.


First we define our Class.
##### sugar
```javascript
class Bike {
  constructor (type, color) {
    this.type = type
    this.color = color
    this.wheels = 2
  }

  roll () {
    console.log('they see me rollin...')
  }
}
```

##### desugar
```javascript
function Bike (type, color) {
  this.type = type
  this.color = color
  this.wheels = 2
} 

Bike.prototype.roll = function () {
    console.log('they see me rollin...')
  }
```

Then, we create instances of our class.
```javascript
let bike1 = new Bike('road', 'red')
let bike2 = new Bike('mountain', 'blue')
```

Classes help solve our repetition problem. We created one class which can be reused to create any number of bikes without hard-coding individual objects.

... but we have another problem. A bike can't be fully described with a type and color alone. We probably want to include information about the brand, model, frame size, wheel size, ect.. Perhaps different types of bikes have different functions. You wouldn't use a road bike, off-road, and you wouldn't commute to work on a bmx bike.

__Objects can become large and complex__.

Prototypal inheritance helps us manage complexity.

### What is prototypal inheritance?
...
#### What is inheritance?
![alt text](./images/inheritance_def.png "inheritance definitions")

#### What is a prototype?

![alt text](./images/prototype_def.png "prototype definition")

#### Prototyping in product design: an analogy
##### Build
Prototyping is an important part of all design. It's a process that allows for incremental testing and improvement of a product. Consider the example of designing a bicycle. First you must develop a prototype, a working model to showcase your design. You start simple knowing you can revise your product later. You invest enough time and money to build your model, a prototype to showcase your idea.

![alt text](./images/draisine.jpeg "draisine bike")

##### Test
So you test your prototype, you ask for opinions from others. Everyone loves the design except but they have some suggestions for improving it. So what do you do? 

##### Repeat
Naturally you need to create another model, hopefully a better one. Do you start from scratch? Of course not! You reference everything you learning building your first model and you modify it. You keep the parts that are good and improve or replace the parts that aren't. This model becomes the new prototype and the cycle continues. Each new model takes qualities from the previous model and builds off them. In other words, __a new model inherits from its prototype__. 

![alt text](./images/bicycle_evolution.svg "evolution of the bicycle")

We don't have to reinvent the wheel every time we create a new bicycle. We can save time and energy focusing on what is specifically new or different rather than repeating the design process from the very beginning. __Prototypal inheritance allows us to build incrementally__.

### Prototypal Inheritance in JavaScript

The concept of a prototype is critical to understanding inheritance in JavaScript and it allows us the same benefits seen in product design.

Building large objects incrementally using inheritance:
- prevents unnecessary repetition
- saves time
- helps organize code into simple parts

Returning to the bike shop example, lets build more complicated objects using inheritance.

##### sugar
First we create a general class. One that will be true for all bikes in our shop.
```javascript
class Bike {
  //the constructor creates instances of Bike which will all have 2 wheels
  constructor () {
    this.wheels = 2
  }
  //all instances of Bike will have access to the roll method
  roll () {
    console.log('they see me rollin...')
  }
}
```

Great! Our first class is simple and will hold true for all bikes. We can create an instance of this class with the 'new' keyword. 

```javascript
let anyBike = new Bike()
//Bike takes no arguments because Bike's constructor method has no parameters.
```

Next, we create another _simple_ class, a subclass that will inherit from Bike. Together they can create objects that are more complicated than either can alone.

```javascript
class TrekBike extends Bike {
	constructor(type) {
		super()
		this.type = type
		this.brand = 'Trek'
    }
}
```

Our subclass has two key differences. It uses the keyword 'extends' to inherit methods from Bike. To inherit the parent classes properties we use the super function to call the parent class' constructor method.

Again, we can create an instance of our subclass with 'new'.

```javascript
trekMtnBike = new TrekBike('mountain')
//this time we pass an argument to TrekBike because TrekBike's constructor has a type parameter.
```

class TrekRoadBike extends TrekBike {
	constructor(frameSize, color) {
		super('road')
		this.frameSize = frameSize
		this.color = color
    }
	sayBrand () {
		console.log('I was made by ' + this.brand) 
    }
}
```

##### desugar
```javascript
function Bike () {
    this.wheels = 2
}
Bike.prototype.roll = function () {
	console.log('they see me rollin...')
}

function TrekBike (type) {
  Bike.call(this)
	this.type = type
	this.brand = 'Trek'
}

TrekBike.prototype = Object.create(Bike.prototype)

function TrekRoadBike (frameSize, color) {
	TrekBike.call(this, 'road')
	this.frameSize = frameSize
	this.color = color
}
TrekRoadBike.prototype = Object.create(TrekBike.prototype)

TrekRoadBike.prototype.sayBrand = function () {
	console.log('I was made by ' + this.brand)
}






