## **Encapsulation** (Data Hiding)
Keep data (fields) safe by hiding them inside the class and controlling access through methods/properties.
Why: Protects the internal state and prevents unintended changes.
## Access Modifiers for Fields
Public - accessible from anywhere (inside a class, subclasses, and even outside classes).
Private - accessible only within the class itself.
Protected - accessible within the class and its child (derived classes), but NOT outside.
```c#
	  using System;
	  public class Person
	  {
	      // Public: accessible everywhere
	      public string Name = "Alice";
	  
	      // Private: accessible only inside Person
	      private int age = 30;
	  
	      // Protected: accessible in Person and derived classes
	      protected string FamilySecret = "We love spaghetti.";
	  
	  }
	  
	  // Child class
	  public class Student : Person
	  {
	      public void AccessParentMembers()
	      {
	          Console.WriteLine("Accessing from Student class:");
	  
	          // ✅ Allowed: public
	          Console.WriteLine(Name);
	  
	          // ❌ Not allowed: private (age)
	          // Console.WriteLine(age);
	  
	          // ✅ Allowed: protected
	          Console.WriteLine(FamilySecret);
	  
	      }
	  }
	  
	  // Test Program
	  public class Program
	  {
	      public static void Main()
	      {
	          Student s = new Student();
	  
	          // Access public member
	          Console.WriteLine("Public: " + s.Name);
	  
	          // ❌ Private is hidden (not accessible from outside)
	          // Console.WriteLine(s.age);
	  
	          // ❌ Protected is hidden (not accessible from outside, only inside Student)
	          // Console.WriteLine(s.FamilySecret);
	  
	          Console.WriteLine("\n--- Calling Student method ---");
	          s.AccessParentMembers();
	      }
	  }
```
## Best Practices in OOP for Fields and Methods
1. Keep fields private (or at most protected) - exposing fields breaks encapsulation
If direct access is allowed, anyone can change the values without control, this makes the object fragile.
```c#
		  student.Age = -5; // nonsense value, but allowed!
```
2. Expose data through properties (getters/setters)
Properties let you add logic, validation, or read-only restrictions later without breaking existing code.
```c#
		  public class Student
		  {
		      private int age;
		  
		      // Property controls access to the private field
		      public int Age
		      {
		          get { return age; }
		          set
		          {
		              if (value >= 0)
		                  age = value;
		              else
		                  Console.WriteLine("Age cannot be negative!");
		          }
		      }
		  }
```
3. Methods are usually public (for behavior)
You expose behaviors (methods) to interact with the object, not the raw data.
4. Set fields to protected so subclasses can use them.
BUT, the safer practice is still to keep fields private and expose them via protected properties or methods.
## Bad Practice to Best Practice applying Encapsulation
Bad Practice
```C#
		  using System;
		  
		  public class Person
		  {
		      // ❌ Bad: Public fields
		      public string Name;
		      public int Age;
		  }
		  
		  public class Program
		  {
		      public static void Main()
		      {
		          Person p = new Person();
		          
		          // Direct access
		          p.Name = "Alice";
		          p.Age = -10;   // ❌ Invalid, but allowed
		  
		          Console.WriteLine($"{p.Name}, Age: {p.Age}");
		      }
		  }
```
Best Practice
```C#
		  using System;
		  
		  public class Person
		  {
		      // ✅ Private fields (hidden from outside)
		      private string name;
		      private int age;
		  
		      // ✅ Public property with no restrictions
		      public string Name
		      {
		          get { return name; }
		          set { name = value; }
		      }
		  
		      // ✅ Public property with validation
		      public int Age
		      {
		          get { return age; }
		          set
		          {
		              if (value >= 0)  // Only valid ages
		                  age = value;
		              else
		                  Console.WriteLine("Age cannot be negative!");
		          }
		      }
		  }
		  
		  public class Program
		  {
		      public static void Main()
		      {
		          Person p = new Person();
		  
		          // Safe access via properties
		          p.Name = "Alice";
		          p.Age = -10;   // ❌ Will be rejected
		          p.Age = 25;    // ✅ Accepted
		  
		          Console.WriteLine($"{p.Name}, Age: {p.Age}");
		      }
		  }
		  
```
## Refactoring
Auto-Property
```C#
	  private string name;
	  
	  public string Name
	  {
	      get { return name; }
	      set { name = value; }
	  }
	  
	  
	  
	  // Same with
	  public string Name { get; set; }
```
If you need validation logic, use the longer one.
In Auto-Property, the compiler generates hidden backing field for you.
## Activity
### Vehicle
**Instructions:**
<!--[if !supportLists]-->
1.     <!--[endif]-->Create a base class called **Vehicle**.  
Private fields: brand (string), year (int).
Public properties:
Brand (get/set, no restrictions).
Year (get/set, must not be less than 1886 — the year the first car was invented).
2. Create a derived class called **Car** that inherits from **Vehicle**.
Private field: numberOfDoors (int).
Public property:
NumberOfDoors (must be greater than 0).
Method: ShowCarInfo()
		  → displays Brand, Year, and NumberOfDoors.  
3. In the Main() method:
Ask the user to input a brand, year, and number of doors.
Create a Car object using those values.
Display its info using the method.
```c#
	  using System;
	  
	  public class Vehicle
	  {
	      // Private fields
	      private string brand;
	      private int year;
	  
	      // Public property for brand (no restrictions)
	      public string Brand
	      {
	          get { return brand; }
	          set { brand = value; }
	      }
	  
	      // Public property for year (cannot be < 1886)
	      public int Year
	      {
	          get { return year; }
	          set
	          {
	              if (value >= 1886)
	                  year = value;
	              else
	              {
	                  Console.WriteLine("Invalid year! Setting to 1886.");
	                  year = 1886;
	              }
	          }
	      }
	  }
	  
	  public class Car : Vehicle
	  {
	      // Private field
	      private int numberOfDoors;
	  
	      // Public property with validation
	      public int NumberOfDoors
	      {
	          get { return numberOfDoors; }
	          set
	          {
	              if (value > 0)
	                  numberOfDoors = value;
	              else
	              {
	                  Console.WriteLine("Invalid number of doors! Setting to 4.");
	                  numberOfDoors = 4;
	              }
	          }
	      }
	  
	      // Method to display info
	      public void ShowCarInfo()
	      {
	          Console.WriteLine("\nCar Information:");
	          Console.WriteLine($"Brand: {Brand}");
	          Console.WriteLine($"Year: {Year}");
	          Console.WriteLine($"Number of Doors: {NumberOfDoors}");
	      }
	  }
	  
	  public class Program
	  {
	      public static void Main()
	      {
	          Car myCar = new Car();
	  
	          Console.Write("Enter car brand: ");
	          myCar.Brand = Console.ReadLine();
	  
	          Console.Write("Enter year: ");
	          int inputYear = Convert.ToInt32(Console.ReadLine());
	          myCar.Year = inputYear;
	  
	          Console.Write("Enter number of doors: ");
	          int inputDoors = Convert.ToInt32(Console.ReadLine());
	          myCar.NumberOfDoors = inputDoors;
	  
	          myCar.ShowCarInfo();
	      }
	  }
	  
```
