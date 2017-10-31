# Prototypical Inheritance

## Learning Objectives
- Demonstrate a use case that explains prototypal inheritance and what kind of flexibility it gives to programmers
- Use namespaces to organize application code
- Define a custom constructor method that sets one or more properties of a new object

## What is prototypal inheritance?
...
### What is inheritance?
![alt text](./images/inheritance_def.png)

function Mammal () {
	this.warmBlooded = true
	this.meow = function() {
		console.log('meow')
    }
}

function Cat (name) {
	this.name = name 
}

Cat.prototype = new Mammal