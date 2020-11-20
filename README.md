# C++ Inheritance

## Table of Contents
*Friendship is beautiful*

1. Main Idea
2. 


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

