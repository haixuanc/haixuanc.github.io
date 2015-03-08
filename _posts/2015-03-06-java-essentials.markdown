---
layout: post
title: "Java Essentials"
date: 2015-03-06 20:00:00
categories:
- Java
---

## Classes and Objects 

### Default Constructor

It is not necessary to supply a constructor for your class. If not defined, the compiler will supply a **no-argument constructor**. The default no-argument constructor will invoke the no-argument contructor of its parent class. If no such constructor is available in the parent class, a compiler error will be thrown. Any class directly extending the `Object` class is excempt from this concern, because `Object` class has an no-argument constructor by default.

### Arbitrary Number of Arguments

You can use a construct called **varargs** to pass an arbitrary number of values to a method. You use varargs when you don't know how many of a *particular type* of argument will be passed to the method. It is a shortcut to creating an array manually.

```java
public void drawPolygon(Point.. corners) {
	...
}
```

You will most commonly see vargars with the printing methods; e.g. the `printf` method:

```java
public PrintStream printf(String format, Object... args)
```

allows you to print an arbitrary number of objects:

```java
System.out.printf("%s: %d, %s%n", name, id, address);
```

### Covariant Return Type

When a method uses a class/interface name as its return type, the class of the type of the returned object must be either a sub-class/-interface of, or the exact class/interface of, the return type. **Covariant return type** is the technique that allows the return type of a method to vary in the same direction as the sub-class/-interface.

Now suppose we have a class hierarchy like this:

`Object` -> `Number` -> `ImaginaryNumber`

and a method declared to return a `Number`:

```java
public Number returnNumber() {
	...
}
```

you can override this method to return a subclass of `Number`:

```java
public ImaginaryNumber returnNumber() {
	...
}
```

### Explicit Constructor Invocation

From within a constructor, you can also use the `this` keyword to call another constructor in the same class. Doing so is called an **explicit constructor invocation**.

If present, the invocation of another constructor must be the first line in the constructor.

```java
public class Rectangle {
	private int x, y;
	private int width, height;

	public Rectangle() {
		this(0, 0, 1, 1); // Must be the first line in the constructor
	}

	public Rectangle(int width, int height) {
		this(0, 0, width, height); // Must be the first line in the constructor
	}

	public Rectangle(int x, int y, int width, int height) {
		this.x = x;
		this.y = y;
		this.width = width;
		this.height = height;
	}

	...
}
```

### Access Modifiers

#### Top Level

A class may be declared with the modifer:

- `public`:
	
	the class is visible to all classes everywhere.
- *package private* (no explicit modifer):

	the class is visible only within its own package.

#### Memeber Level

A class member (field or method) may be declared with the `public` or *package private* modifier just as with top-level classes, and with the same meaning. Members have two additional access modifiers:

- `private`:

	the member can only be accessed in its own class.
- `protected`:
	
	the member can only be access within its own package (as with *package private*) and, in addition, by a subclass of its class in another package.

Modifier | Class | Package | Subclass | world
---------| ----- | ------- | -------- | -----
public   | Y     | Y       | Y        | Y
protected | Y    | Y       | Y        | N
no modifier | Y  | Y       | N        | N
private  | Y     | N       | N        | N

### Constants

The `static` modifier, in combination with the `final` modifier, is used to define constants:

```java
static final double PI = 3.1415926;
```

### Initialization Blocks

#### Static Initialization Blocks

If initialization requires some logic (e.g. error handling or a `for` loop to fill a complex array), simple assignment is inadequate. Instance variables can be initialized in constructors, where error handling or other logic can be used. To provide the same capability for class variables, **static initialization blocks** are provided.  

It is not neccessary to declare class fields ar the beginning of the class definition, although this is the most common practice. It is only necessary that they be declared and initialized before they are used.

A static initialization block is a normal block of code enclosed in braces and preceded by the `static` keyword:

```java
static {
	// Whatever code is needed for initializatino goes here
}
```

A class can have any number of static initialization blocks, and they can appear anywhere in the class body. The runtime system guarantees that static initialization blocks are called in the order that thery appear in the source code.

There is an alternative to static blocks -- **private static method**:

```java
class Whatever {
	public static VarType myVar = initializeClassVariable();

	private static VarType initializeClassVariable() {
		// Initialization code goes here
	}

	...
}
```

The advantage of private static methods is that they can be reused later if you need to reinitialize the class variable.

#### Initializing Instance Variables

Normally, you would put code to initialize an instance variable in a constructor. There are two alternatives to using a constructor to initialize instance variables:

- **Initializer blocks**:
	- The Java compiler copies initializer blocks into every constructor. Therefore, this approach can be used to share a block of code between multiple constructors. 

	```java
	{
		// Whatever code is needed for initialization goes here
	}
	```

- **Final methods**:
	- Final methods cannot be overridden in a subclass.
	- This is especially useful if subclasses might want to reuse the initialization method.
	- This method is `final` because calling non-final methods during instance initialization can cause problems.

	```java
	class Whatever {
		private VarType myVar = initializeInstanceVariable();

		protected final VarType initializeInstanceVariable() {
			// Initialization code goes here
		}

		...
	}
	```

## References

- [The Java Tutorials: Classes and Objects, Oracle](http://docs.oracle.com/javase/tutorial/java/javaOO/arguments.html)
