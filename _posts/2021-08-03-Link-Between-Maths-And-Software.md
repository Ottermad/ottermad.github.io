---
layout: post
title: The Link Between Mathematics and Software Engineering
author: Charles Thomas
---

Mathematics and software engineering have a tumulous relationship. Some people think you need to be a great mathematician in order to be a great software engineer, others believe you don't need to know any sophisticated maths in order to be an amazing engineer. I think there is some truth to both sides to this argument and in many cases, the reason why people disagree is because of a misunderstanding about what the relevant bits of mathematics are.

People are often put off software engineering because there are parts of it that are mathematically heavy, for example, understanding cryptography does require some topics that aren't normally covered unless you do a mathematics undergrad such as group theory (although I promise with a little bit of graft it's not that scary). And because of these areas, some people argue that you need to be good at maths in order to be a good software engineer. However, the truth is that most software engineers don't spend their time designing cryptographic solutions or working in other mathematically intense areas. So you don't need to know a lot of maths to be able to be a good engineer.

However, there are more general similarities between maths and software engineering that are best illustrated by example - so let's start by talking about object-oriented programming and interfaces. 

In object-oriented programming (OOP), we define classes that are made up of two things: attributes which are pieces of data and methods which are functions that manipulate that data. Objects are then instances of that class. To make this a bit clearer let's look at an example. Imagine I want to model a car in code, I might define a car class with the attributes: colour, make, fuel level and speed and then the method drive that increases speed and decreases fuel. 

```
class Car {
	colour: string;
	make: string;
	model: string;
	fuelLevel: float;
	speed: float;

	method Drive() {
		fuelLevel -= 1;
		speed += 1;
	}
}
```

I can then make instances of this car class. So I might create a red Volvo and blue Honda: 
```
car1 = Car(colour: red, make: Volvo);
car2 = Car(colour: blue; make: Honda);
```

I can now define functions that accept Cars. So I can create a function that changes that accepts Car objects. 
```
function DriveCar(car: Car) {
	car.drive();
}
```

Hopefully, you're still with me. So now sometimes I can have classes that all have similarities, for example, I might have a Car class, a Motorbike class and a Bus class, all of which have a Drive method. Now sometimes I want to write a function that can work with anything that has a drives method. This way I don't have to write a DriveCar, DriveMotorbike and DriveBus functions and I can just define a Drive function. Interfaces give us a way to do this.

Interfaces allow us to define what behaviour (methods) we expect from a class and then use that interface anywhere we just need that behaviour. So we might define a Vehicle interface that just expects a drive method:
```
interface Vehicle {
	drive();
}
```

and now we can write a drive function:
```
function Drive(vehicle: Vehicle) {
	vehicle.drive();
}
```

and since Car, Motorbike and Bus all have a drive method I can pass any of them into the Drive function [1].

So why have I have bothered to explain this and what is its connection to mathematics. The key part to take away from this discussion about interfaces is that they are a way of defining something in terms of what it does instead of how it does it. In the example, we didn't care how our vehicles drove, only that they could drive. As this turns out this is very similar to how we define things in mathematics.

To see this let's take look at an example. You may have come across the concept of a vector in a high school physics class as something with a magnitude and a direction. For example, a force is a vector because it has a magnitude (how strong the force is) and a direction (what direction the force is pointing in). Now, this is not how mathematicians like to define vectors. To a mathematician a vector is an object that I can do two things to [2]: 
* Vector addition - I can add it to another vector 
* Scalar multiplication - I can make my vector bigger or smaller by some factor

To make this a bit clearer let's look at a couple of examples. One of the easiest examples are the real numbers. These are just the numbers we're familiar with: 1, 2.5, 2.731, PI etc and they are vectors because I can add two of them together: 5 +7 = 12 and I can scale them: 2x5 = 10

A slightly more complicated example is what is called R^2 and these are the column vectors you might have seen in school. For example, [2, 5] or [3, 17]. Now I can add these together by adding each component separately so [1, 2] + [3, 4] = [4, 6] and I can scale them by multiplying them by a single number like this: 3[12, 10] = [36, 30]

Now in maths, we can construct some much more complicated vectors such as functions or integrals and I can create certain types of vectors by introducing more operations such as the inner (dot) product. But the key is as long as I can prove it works for vectors that property is true for all vectors no matter how complicated they are. 

Hopefully, you've begun to notice that this is very similar to how we use interfaces in programming: we only care about being able to do certain operations on something and not less about how it works [3].

To me, this similarity is the key link between mathematics software is the ability to think abstractly about what behaviours we care about at a particular time and is a skill common to both.

Notes:

1) Perhaps I should have talked about inheritance here but I didn't want to any more complexity

2) To the mathematicians out there: I'm aware that there are some more axioms these operations must obey but that is not the purpose of this article

3) You could also think about type classes in a language like Haskell

