# C++ Inheritance

## Table of Contents
*Friendship is beautiful*

1. Main Idea
2. Superclass and Child
3. Types of Inheritance
4. Making Friends
5. Nested Classes/ Dependent Types

---
---


## Main Idea
Process of making a new class from an 'old' class

* This allows for creation of a Parent>Child relationship with the child being given attributes from the parent class
* Defined through an "IS A" relationship
	- Chair "IS A" piece of furniture (parent is reference to a child)
	


## C++ Inheritance
C++ acts the same, the new class inherits the properties and method of the parent  

* Private properties and methods exist but are not accessible

### Differences
Unlike other languages there are no keywords for inheritance  
We use the ' : ' operator  

* This is a single-colon, NOT double which is scope resolution operator

`class student : public person`

## Standard Inheritance

There are multiple styles of Inheritance, thus why we defined `public`  
Public is used the most, however, we still have Protected and Private members

Protected members are inherited as protected in the new class  
Private members cannot be directly accessed, but can be accessed through public and protected members of the *base-class*

### Protected Inheritance

* Public members are inherited as protected
* Protected members are inherited as protected
* Private members remain private as in public inheritance

Due to the public interface now being protected, access to the interface is no longer available


### Private Inheritance
When using private inheritance, everything becomes private   <-- odd and controversial  

Implemented in Terms of relationship  

* Public interface of the base class, removes access of the user to the derived class

> If you make a class D privately inherit from class B, you do so beacuse you are interested in taking advantage of some features available in class B,  not because there is any conceptual relationship between the two

Private inheritance means nothing during software **design**, only during **software implementation**


## Superclass and Child

Unlike other programming language there is no super keyword

* C++ has different rules for superclasses, all for a good reason

### Inheritance and Constructors
Parent constructors can be invoked as part of the child constructor with '  :  '

```cpp
class Rectangle: public Polygon
{

	public:
		Rectangle (int a, int b): Polygon(a,b){}
		int area()
			{ return width*height; }

};
```

To invoke the methods within the child, the scope operator is used ' :: '  

```cpp
void child::print(int x)
{

	parent::print(x);

}
```


## Types of Inheritance

1.  Single Inheritance (all above)
2.  Multiple Inheritance
3.  Multilevel Inheritance
4.  Hierarchical Inheritance
5.  Hybrid Inheritance
6.  Virtual Inheritance

---

### Multiple Inheritance
Classes can be composed from multiple different parents instead of a single parent (single inheritance)  
The child class will have access to all the members of all of its parents

* Reason we don't have a super keyword

This allows for isolation and creation of discrete base classes new classes with "custom" functionality  
Not the same as Aspect Based Programming (Unity3D)... similar power

```cpp
class D: public A, public B, public 
{
};
```

### Multilevel Inheritance
This exists in most languages  
Class A is base class of Class B and Class B is a base of Class C  
Shows a true "IS A" relationship


### Hierarchical Inheritance
Logical extension of multi-level inheritance  
Greatest use of polymorphism


### Hybrid Inheritance
Pattern that is unique to languages like C++ which allows for multiple inheritance  
Combines Multiple, Multilevel and Hierarchical inheritance for a hybrid child class

This combines specializations into a single class which leads to an issue

*The Diamond Problem*  

* The hybrid class will have duplicate inherited members from the base class


### The Diamond Problem
The parents of the child are the children of the grandparent  

* They then have all the grandparent's members
* The hybrid inherits "different versions" of the same members derived from the grandparent


To solve this we use something called virtual inheritance

## Virtual Inheritance

```cpp
class Grandparent
{

	//content of grandparent class

};

class Child1 : public virtual Grandparent
{

	//content of Child1 class

};

class Child2 : public virtual Grandparent
{

	//content of Child2 class;

};

class grandson : public Child1, public Child2
{

	//content of grandson class

};
```

The compiler creates virtual pointers to access the members  
A virtual table is constructed which contains offsets used to address the members, virtual pointers refer to these offsets

## Constructors and Destructors

Generally the parent class constructors are called before child class constructors  
This cascades through the hierarchy

* Destructors work backwards starting with the child 

In multiple inheritance scenarios, parent constructors are invoke in order of their inheritance

`class derived: public class1, public class 2`


# Making Friends

Friends and C++ 

1. Private
2. Public
3. Protected

Friends can be created between classes which can break the bounds of these keywords  
When a function/class is a friend of another, they can access private and protected members of that class  

* The friend keyword give permission and power to interface with other object's members

Whole classes can also be specified as friends  
All the methods within that friend class will have access to the members of the acknowledging class

## Fair Weather Friends
Friendship is only one-direction

*  Just because a square lists Rectangle as a friend that doesn't mean that rectangle considers square as a friend


# Nested Classes/ Dependent Types

## Nesting Classes
Classes can only be accessed within the context of the class they are nested within

*  The name of the nested class is local to the enclosing class
*  They follow the same rules as other classes
	-  They don't have access to the enclosing class except through public interface
* Likewise, the enclosing class doesn't have any special access to the nested class

C++ variables assumes private and defaults to private

```cpp
{

	int x;
	
	class B {  };
	
	class C {
	
		// The compiler cannot allow the following declaration 
		// because A::B is private
		// 	B b;
		
		int y;
		void f(A* p, int i) {
			...
		
		}
	
	}

}
```

## Scope operator and Defining Subclasses
The scope operator can be used to access and define methods wihtin the class  
This allows for maintinence of the forward declaration pattern  

*  This can be used in conjunction with typedef to ease production

The nested class can inherit from the enclosing class


Forward declaration allows for public inheritance

```cpp
class Animal
{

	class Bear;
	
	class Giraffe;

};

class Animal::Bear : public Animal
{
};

class Animal::Giraffe : public Animal
{
};
```

This allows us to hide parts of our API   
If a library is created and wants to be shared which includes some sort of Data Structure we don't want it to be exposed


