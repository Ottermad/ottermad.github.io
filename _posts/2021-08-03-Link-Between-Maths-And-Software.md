---
layout: post
title: The Link Between Mathematics and Software Engineering
author: Charles Thomas
---

Mathematics and software engineering have a tumultuous relationship. Some people think you need to be a great mathematician to be a great software engineer. Others believe you don't need to know any sophisticated maths to be an amazing engineer. There is some truth to both sides to this argument and in many cases, the reason why people disagree is because of a misunderstanding about what the relevant bits of mathematics are.

People are often put off software engineering because there are parts of it that are mathematically heavy. For example, understanding cryptography does need some topics that aren't covered in high school such as group theory. Because of these areas, some people argue that you need to be good at maths to be a good software engineer. But, the truth is that most software engineers don't spend their time designing cryptographic solutions or working in other mathematically intense areas. So you don't need to know a lot of maths to be able to be a good engineer.

However, there are more general similarities between maths and software engineering. These are best illustrated by example - so let's start by talking about object-oriented programming and interfaces. 


## Object Orientated Programming
In object-oriented programming (OOP), we define classes. Classes  are made up of two things: 
* Attributes - pieces of data 
* Methods - functions that manipulate that data. 

Objects are then instances of that class. To make this a bit clearer let's look at an example. 

Imagine I want to model a car in code. I would start by defining a car class. It would have the attributes: colour, make, fuel level and speed. It would also have the method drive that increases speed and decreases fuel. 

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

I can then make instances of this car class. So I could create a red Volvo and blue Honda: 
```
car1 = Car(colour: red, make: Volvo);
car2 = Car(colour: blue; make: Honda);
```

I can now define functions that accept Cars:
```
function DriveCar(car: Car) {
	car.drive();
}
```

## Interfaces
Hopefully, you're still with me. Sometimes you'll have several classes that all have similarities. 

For example, I might have a Car class, a Motorbike class and a Bus class, all of which have a Drive method. Now sometimes I want to write a function that can work with anything that has a drive method. This way I don't have to write a DriveCar, DriveMotorbike and DriveBus functions and I can define a Drive function. Interfaces give us a way to do this.

Interfaces allow us to define what behaviour (methods) we expect from a class and then use that interface anywhere we need that behaviour. 

So we might define a Vehicle interface that  expects a drive method:
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

```
myCar = Car(colour: red, make: Volvo);
myMotorbike = Motorbike();

Drive(myCar);
Drive(myMotorbike);
```

So why have I have bothered to explain this and what is its connection to mathematics. The key part to take away is that interfaces are a way of defining something in terms of what it does instead of how it does it. 

In the example, we didn't care how our vehicles drove, only that they could drive. As this turns out this is very similar to how we define things in mathematics.


## Vectors
To see this let's take look at an example. You may have come across the concept of a vector in a high school physics class as something with a magnitude and a direction. 

For example, a force is a vector because it has a magnitude (how strong the force is) and a direction (what direction the force is pointing in). 

This is not how mathematicians define vectors. To a mathematician a vector is an object that I can do two things to [2]: 
* Vector addition - I can add it to another vector 
* Scalar multiplication - I can make my vector bigger or smaller by some factor

To make this a bit clearer let's look at a couple of examples. 

One of the easiest examples are the Real numbers. These are the numbers we're familiar with: 1, 2.5, 2.731, $$\pi$$ etc and they are vectors because I can add two of them together: 5 + 7 = 12 and I can scale them: 2x5 = 10

A more complicated example is what is called $$R^2$$ and these are the column vectors you might have seen in school. For example, $$\begin{bmatrix}2 \\ 5\end{bmatrix}$$ or $$\begin{bmatrix}3 \\ 17\end{bmatrix}$$. I can add these together by adding each component separately so $$\begin{bmatrix}1 \\ 2 \end{bmatrix} + \begin{bmatrix}3 \\ 4\end{bmatrix} = \begin{bmatrix}4 \\ 6\end{bmatrix}$$. And I can scale them by multiplying them by a single number like this: $$3\begin{bmatrix}12 \\ 10\end{bmatrix} = \begin{bmatrix}36 \\ 30 \end{bmatrix}$$


## The link
 Now in maths, we can construct some much more complicated vectors such as functions or integrals. I can also create certain types of vectors by introducing more operations such as the inner (dot) product. But the key is as long as I can prove it works for vectors that property is true for all vectors no matter how complicated they are. 

This is very similar to how we use interfaces in programming. We only care about being able to do certain operations on something and not about how it works [3].

This similarity is the key link between mathematics software. It is the ability to think abstractly about what behaviours we care about at a particular time that is a skill common to both.

## Notes:

1)  I could have talked about inheritance here but I didn't want to any add more complexity

2) To the mathematicians out there: I'm aware that there are some more axioms these operations must obey but that is not the purpose of this article

3) You could also think about type classes in a language like Haskell

