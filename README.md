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

Prototyping is an important part of all design. It's a process that allows for incremental testing and improvement of a product. Consider the example of designing a bicycle. First you must develop a prototype, a working model to showcase your design. You brainstorm, sketch, research, weigh the pros and cons of different frame materials, wheel-size, handlebar design, ect. You invest time and money to build your first model, a prototype.

![alt text](./images/highwheel_bike.png "highwheel bike")

So you test your prototype, you ask for opinions from others, and maybe you run it by potential investors for feedback. Everyone loves the design except they think the color is ugly and they don't like falling over the front when stopping. So what do you do? Naturally you need to create another model, hopefully a better one. Do you start from scratch? Of course not! You reference everything you learning building your first model and you modify it. You keep the parts that are good and improve or replace the parts that aren't to build a new and improved model. This model becomes your current prototype and the cycle continues.

![alt text](./images/bicycle_evolution "evolution of the bicycle")





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