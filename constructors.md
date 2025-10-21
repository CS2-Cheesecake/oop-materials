## 🎯  **Intended Learning Outcomes**
By the end of the lesson, students will be able to:
Define what a constructor is and explain its role in object initialization.
Differentiate between default and parameterized constructors.
Explain the purpose of constructor overloading.
Implement and apply constructors in C# classes.
Demonstrate constructors through a simple real-world example.
## 🧠  **Introduction to Constructors**
### 📘 Definition:
A **constructor** is a **special method** in a class that is **automatically called when an object is created**.
Its main role is to **initialize object data members**.
### 🪄 Syntax:
```C#
  class ClassName
  {
    // Constructor
    public ClassName()
    {
        // Initialization code
    }
  }
```
### ⚙️ Key Points:
Has the **same name as the class**.
**No return type** (not even `void`).
Automatically executes when you create an instance.
## 🧩  **A. Default Constructor**
### 📘 Definition:
A **default constructor** is one **without parameters**.
It initializes object members with **default values** or **predefined logic**.
### 🧾 Example:
```c#
  class Student
  {
      public string Name { get; set; }
      public int Age { get; set; }
      
      public Student()
      {
          Name = "Unknown";
          Age = 18;
      }
  }
```
### ▶️ Usage:
```
  Student s1 = new Student();
  Console.WriteLine($"Name: {s1.Name}, Age: {s1.Age}");
```
## ⚙️  **B. Parameterized Constructor**
### 📘 Definition:
A **parameterized constructor** takes **arguments** to initialize data members with specific values when an object is created.
### 🧾 Example:
```c#
  class Student
  {
      public string Name { get; set; }
      public int Age { get; set; }
  
      public Student(string name, int age)
      {
          Name = name;
          Age = age;
      }
    
  }
```
### ▶️ Usage:
```
  Student s1 = new Student("Reid", 21);
  Console.WriteLine($"Name: {s1.Name}, Age: {s1.Age}");
```
## Combine Default and Parameterized Constructor in one class
```c#
  class Student
  {
  
      public string Name { get; set; }
      public int Age { get; set; }
  
  
      public Student()
      {
          Name = "Unknown";
          Age = 18;
      }
  
      public Student(string name, int age)
      {
          Name = name;
          Age = age;
      }
  }
  
  class Program
  {
      static void Main()
      {
          
          Student s1 = new Student();
          Student s2 = new Student("Reid", 21);
  
          Console.WriteLine("Student Records:");
          Console.WriteLine($"Name: {s1.Name}, Age: {s1.Age}");
          Console.WriteLine($"Name: {s2.Name}, Age: {s2.Age}");
      }
  }
```
## 🔁  **Constructor Overloading**
### 📘 Concept:
Constructor **overloading** means having **multiple constructors** in a class, each with **different parameter lists**.
**Constructor overloading** happens when **a class has two or more constructors** with the **same name** (the class name) but **different parameter lists**.
It allows **flexibility** in how you initialize an object.
### 🧾 Example:
```c#
  class Product
  {
      public string Name { get; set; }
      public double Price { get; set; }
  
  
      public Product()
      {
          Name = "Unnamed";
          Price = 0.0;
      }
  
      public Product(string name)
      {
          Name = name;
          Price = 0.0;
      }
  
      public Product(string name, double price)
      {
          Name = name;
          Price = price;
      }
  }
```
### ▶️ Usage:
```
  Product p1 = new Product();
  Product p2 = new Product("Laptop");
  Product p3 = new Product("Smartphone", 399.99);
  
  Console.WriteLine($"{p1.Name} - {p1.Price}");
  Console.WriteLine($"{p2.Name} - {p2.Price}");
  Console.WriteLine($"{p3.Name} - {p3.Price}");
```
## 🌍  **Example: Bank Account**
### 🧾 Example Program:
```c#
  using System;
  
  class BankAccount
  {
      public string AccountName { get; set; }
      public double Balance { get; set; }
  
      // Default constructor
      public BankAccount()
      {
          AccountName = "Default Account";
          Balance = 0.0;
      }
  
      // Parameterized constructor
      public BankAccount(string accountName, double initialDeposit)
      {
          AccountName = accountName;
          Balance = initialDeposit;
      }
  
      public void DisplayInfo()
      {
          Console.WriteLine($"Account: {AccountName}, Balance: {Balance}");
      }
  }
  
  class Program
  {
      static void Main()
      {
          BankAccount acc1 = new BankAccount();                // Calls default constructor
          BankAccount acc2 = new BankAccount("Reid", 5000);    // Calls parameterized constructor
  
          acc1.DisplayInfo();
          acc2.DisplayInfo();
      }
  }
  
```
## 💡  **Key Takeaways**
| Concept | Description | Example |
|---|---|---|
| **Constructor** | Special method to initialize an object | `public ClassName() { }` |
| **Default Constructor** | No parameters, sets default values | `public Student() { }` |
| **Parameterized Constructor** | Accepts arguments | `public Student(string n, int a)` |
| **Overloaded Constructors** | Multiple constructors with different parameters | Combine all above |
## 🧩  **Class Activity**
### 💻 Lab Task:
- Create a class named `Book` with the following:
- Fields: `Title`, `Author`, `Price`
  
Constructors:
- Default (sets default values)
- Parameterized (sets title and author)
- Overloaded (sets title, author, and price)
  
Method: `DisplayBookDetails()`  
Then, in `Main()`, create multiple `Book` objects using all constructors and display their information.
### 💻  **Lab Task:**
Create a class named `Car` with the following specifications:
**Properties:**
- `Brand`
- `Model`
- `Price`  
**Constructors:**
- **Default constructor** – sets brand to `"Unknown"`, model to `"Generic"`, and price to `0.0`  
- **Parameterized constructor (2 parameters)** – sets brand and model  
- **Overloaded constructor (3 parameters)** – sets brand, model, and price
  
**Method:**
`DisplayCarInfo()` – displays the brand, model, and price of the car.

**In the `Main()` method:**
- Create one object using the **default constructor**
- Create one object using the **2-parameter constructor**
- Create one object using the **3-parameter constructor**
- Call `DisplayCarInfo()` for each object.
