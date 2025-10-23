## What is Polymorphism?
Polymorphism is one of the four pillars of object-oriented programming.
The word polymorphism means "many forms".
It allows a single interface to represent different implementations.
Constructor overloading is a form of compile-time polymorphism (also called static polymorphism).
Example
```c#
  class Message
  {
      public void greet()
      {
          Console.WriteLine("Hello");
      }
  
      public void greet(string name)
      {
          Console.WriteLine("Hello " + name);
      }
  
      static void Main(string[] args)
      {
          Message p1 = new Message();
  
          p1.greet();
          p1.greet("Nixie!");
      }
  }
```
Output
```apl
  Hello
  Hello Nixie!
```
## Two Types of Polymorphism in C#
| Type | Description | When it Happens | Example |
|---|---|---|---|
| Compile-time (Static) | Method Overloading | During compilation | Same method name, different parameters |
| Runtime (Dynamic) | Method Overriding | During execution | Derived class modifies base behavior |
### A. Compile Time Polymorphism
It is achieved by method overloading. The method to be executed is determined at compile time.
### **Method Overloading**
Multiple methods in the same class share the same name but differ in the number or type of parameters. The correct method is selected by the compiler based on the arguments provided.
Method overloading can be done by changing:
Changing the number of Parameters
Changing data types of the parameters.
Changing the Order of the parameters.
```c#
	  using System;
	  
	  class Calculator {
	      public int Add(int a, int b) {
	          return a + b;
	      }
	  
	      public double Add(double a, double b) {
	          return a + b;
	      }
	  }
	  
	  class Program {
	      static void Main() {
	          Calculator calc = new Calculator();
	          Console.WriteLine(calc.Add(5, 10));     // Calls int version
	          Console.WriteLine(calc.Add(2.5, 3.5));  // Calls double version
	      }
	  }
```
```apl
	  15
	  6
```
The decision about which method to call (Add(int, int) or Add(double, double)) is made by the compiler at compile time based on the arguments passed.
**Shortcut**
```c#
	  class Calculator {
	      public int Add(int a, int b) => a + b;
	      public double Add(double a, double b) => a + b;
	  }
```
**Practice 01**
Create a class to calculate the area of different shapes using a single method name, **calculateArea**.
square = side * side; return type: int
circle = 3.1416 * radius; return type: double
rectangle = length * width; return type: int
### B. Runtime Polymorphism (Method Overriding)
Runtime polymorphism (dynamic polymorphism) in C# is achieved through method overriding. It occurs when a derived class provides a specific implementation of a method already defined in the base class, using the same signature. This allows the derived class to modify or extend the behavior of the inherited method.
**Virtual Method**: The base class method must be declared as virtual to allow overriding.
	  **Override Keyword**: The derived class method must use the override keyword to provide a new implementation.  
```c#
	  using System;
	  
	  // Base class
	  class Animal{
	      
	    	// set as virtual method to allow overriding
	      public virtual void MakeSound(){
	          Console.WriteLine("Animal makes a sound");
	      }
	    
	  }
	  
	  // Derived class
	  class Dog : Animal
	  {
	      // use override keyword to override the base class method
	      public override void MakeSound()
	      {
	          Console.WriteLine("Dog barks");
	      }
	  }
	  
	  // Derived class
	  class Cat : Animal
	  {
	      // use override keyword to override the base class method
	      public override void MakeSound()
	      {
	          Console.WriteLine("Cat meows");
	      }
	  }
	  
	  class Program
	  {
	      static void Main(string[] args)
	      {
	          Animal myAnimal = new Animal();
	          Animal myDog = new Dog();
	          Animal myCat = new Cat();
	  
	          myAnimal.MakeSound(); 
	          myDog.MakeSound();    
	          myCat.MakeSound();   
	      }
	  }
	  
```
```apl
	  Animal makes a sound
	  Dog barks
	  Cat meows
```
### Method Overriding Example Flow
![Methodoverriding](https://media.geeksforgeeks.org/wp-content/uploads/20250915104642966204/Methodoverriding.webp)
## Keywords for Method Overriding
In C#, three keywords are used for Method Overriding which are listed below:
### **1. virtual Keyword**
This keyword is used in the base class to define a method that can be overridden in a derived class.
**Example** 1**:** Method overriding using virtual keyword.
```c#
  using System;
  
  class Animal
  {
      // Base class method marked as virtual
      public virtual void Move()
      {
          Console.WriteLine("Animal is moving.");
      }
  }
  
  class Dog : Animal
  {
      // Overriding the base class method using 'override'
      public override void Move()
      {
          Console.WriteLine("Dog is running.");
      }
  }
  
  class Geeks
  {
      static void Main()
      {   
          // Creating an object of the Dog class
          Dog dog = new Dog();  
          dog.Move();  
      }
  }
```
Output:
```apl
  Dog is running.
```
### 2. override keyword
This keyword is used in the derived class to provide a specific implementation of a method defined in the base class.
**Example: **Method overriding using override keyword.
```c#
  using System;
  
  class Animal{
    
      // Base class method marked as virtual
      public virtual void Move(){
          Console.WriteLine("Animal is moving.");
      }
  }
  
  class Dog : Animal {
    
      // Overriding the base class method using 'override'
      public override void Move(){
          Console.WriteLine("Dog is running.");
      }
  }
  
  class Geeks {
      static void Main(){
  
          // Creating an object of the Dog class
          Dog dog = new Dog();
          dog.Move();
      }
  }
```
Output:
```apl
  Dog is running.
```
### **3. Base Keyword**
This method is used to access members(methods, properties or constructors) of the base class from within a derived class.
**Use of Base Keyword:**
Call methods or functions of base class from derived class.
Call constructor internally of base class at the time of inheritance.
**Example** 1**:** Method overriding using Base keyword.
```c#
  using System;
  
  class Animal {
      // Base class method marked as virtual
      public virtual void Move(){
          Console.WriteLine("Animal is moving.");
      }
  }
  
  class Dog : Animal {  
      // Derived class method that calls the base class method using 'base'
      public override void Move(){
          // Calls the Move() method from the Animal class
          base.Move();
          Console.WriteLine("Dog is running.");
      }
  }
  
  class Geeks {
      static void Main(){
          Dog dog = new Dog();
          dog.Move();
      }
  }
```
Output:
```apl
  Animal is moving.
  Dog is running.
```
**Practice 2**
Define a base Employee class with calculateBonus() method, and then create subclasses (e.g. Manager, Developer). The Manager and Developer subclasses would override the calculateBonus() method to implement their specific bonus logic.
Default bonus = baseSalary * 0.05
Manager = 5000 + (baseSalary * 0.10);
Developer = baseSalary * 0.08
