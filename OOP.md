# Object-Oriented Programming (OOP) in C#

**COMPLETE LECTURE NOTES & STUDY GUIDE**

This comprehensive document contains everything you need to know about Object-Oriented Programming in C#, with detailed explanations, real-world examples, and key concepts for exams. No need to read lecture materials - this covers everything!

## Table of Contents
1. [Structures](#structures)
2. [Classes and Objects](#classes-and-objects)
3. [Encapsulation](#encapsulation)
4. [Inheritance](#inheritance)
5. [Polymorphism](#polymorphism)
6. [Abstraction](#abstraction)
7. [Interfaces](#interfaces)
8. [Generic Classes](#generic-classes)
9. [Delegates and Events](#delegates-and-events)
10. [Properties and Auto-Implemented Properties](#properties-and-auto-implemented-properties)
11. [Method Overloading and Overriding](#method-overloading-and-overriding)
12. [Extension Methods](#extension-methods)
13. [Composition vs Inheritance](#composition-vs-inheritance)
14. [Static Classes and Members](#static-classes-and-members)
15. [Sealed Classes](#sealed-classes)
16. [Partial Classes](#partial-classes)
17. [Exception Handling in OOP](#exception-handling-in-oop)
18. [Namespaces](#namespaces)
19. [LINQ and OOP](#linq-and-oop)
20. [Lambda Expressions](#lambda-expressions)

## Structures

Structures (or structs) are value types that are typically used to encapsulate small groups of related variables. Unlike classes which are reference types, structs are allocated on the stack rather than the heap, making them more efficient for small data structures.

### Example:

```csharp
// Structure definition
public struct Point
{
    // Fields
    public int X;
    public int Y;
    
    // Constructor
    public Point(int x, int y)
    {
        X = x;
        Y = y;
    }
    
    // Method
    public double DistanceFromOrigin()
    {
        return Math.Sqrt(X * X + Y * Y);
    }
    
    // Override ToString method
    public override string ToString()
    {
        return $"({X}, {Y})";
    }
}

// Using a structure
Point p1 = new Point(3, 4);
Console.WriteLine($"Point: {p1}"); // Output: Point: (3, 4)
Console.WriteLine($"Distance from origin: {p1.DistanceFromOrigin()}"); // Output: 5

// Structures are value types
Point p2 = p1; // Creates a copy
p2.X = 7;
Console.WriteLine($"p1: {p1}"); // Output: p1: (3, 4) - unchanged
Console.WriteLine($"p2: {p2}"); // Output: p2: (7, 4)

// Readonly struct (C# 7.2+)
public readonly struct ReadOnlyPoint
{
    public readonly int X { get; }
    public readonly int Y { get; }
    
    public ReadOnlyPoint(int x, int y)
    {
        X = x;
        Y = y;
    }
    
    // Immutable struct - can't modify its state
}

// Differences between struct and class:
// 1. Structs are value types, classes are reference types
// 2. Structs are stored on the stack, classes are stored on the heap
// 3. Structs cannot inherit from other structs or classes
// 4. Structs cannot have a parameterless constructor
// 5. Structs cannot have finalizers
// 6. Structs are passed by value, classes are passed by reference
```

## Classes and Objects

Classes are the blueprints for objects. They define properties, methods, and events that objects of that class will have.

### Example:

```csharp
// Class definition
public class Person
{
    // Fields
    private string name;
    private int age;
    
    // Constructor
    public Person(string name, int age)
    {
        this.name = name;
        this.age = age;
    }
    
    // Properties
    public string Name
    {
        get { return name; }
        set { name = value; }
    }
    
    public int Age
    {
        get { return age; }
        set { age = value; }
    }
    
    // Method
    public void Introduce()
    {
        Console.WriteLine($"Hello, my name is {name} and I am {age} years old.");
    }
}

// Creating an object
Person person = new Person("John", 30);
person.Introduce(); // Output: Hello, my name is John and I am 30 years old.
```

## Encapsulation

Encapsulation is the bundling of data and methods that operate on that data within a single unit (class) and restricting access to some of the object's components.

### Example:

```csharp
public class BankAccount
{
    // Private field - encapsulated
    private decimal balance;
    
    // Public property with validation
    public decimal Balance
    {
        get { return balance; }
        private set { balance = value; } // Only accessible within the class
    }
    
    public void Deposit(decimal amount)
    {
        if (amount <= 0)
        {
            throw new ArgumentException("Amount must be positive");
        }
        
        Balance += amount;
    }
    
    public bool Withdraw(decimal amount)
    {
        if (amount <= 0)
        {
            throw new ArgumentException("Amount must be positive");
        }
        
        if (amount > Balance)
        {
            return false; // Insufficient funds
        }
        
        Balance -= amount;
        return true;
    }
}

// Usage
var account = new BankAccount();
account.Deposit(1000);
account.Withdraw(500);
// account.Balance = 5000; // Error: Cannot access set accessor
```

## Inheritance

Inheritance enables a class to inherit fields and methods from another class, promoting code reuse and establishing a relationship between parent and child classes.

### Example:

```csharp
// Base class
public class Shape
{
    public double Width { get; set; }
    public double Height { get; set; }
    
    public Shape(double width, double height)
    {
        Width = width;
        Height = height;
    }
    
    // Virtual method can be overridden by derived classes
    public virtual double CalculateArea()
    {
        return Width * Height;
    }
}

// Derived class
public class Rectangle : Shape
{
    public Rectangle(double width, double height) : base(width, height)
    {
    }
    
    // No need to override CalculateArea as it works for rectangles
}

// Another derived class
public class Triangle : Shape
{
    public Triangle(double width, double height) : base(width, height)
    {
    }
    
    // Override the area calculation for triangles
    public override double CalculateArea()
    {
        return 0.5 * Width * Height;
    }
}

// Usage
Rectangle rect = new Rectangle(5, 10);
Console.WriteLine($"Rectangle area: {rect.CalculateArea()}"); // Output: 50

Triangle triangle = new Triangle(5, 10);
Console.WriteLine($"Triangle area: {triangle.CalculateArea()}"); // Output: 25
```

## Polymorphism

Polymorphism allows objects of different types to be treated as objects of a common type, enabling method implementations to be selected based on the actual object type.

### Example:

```csharp
public class Animal
{
    public virtual void MakeSound()
    {
        Console.WriteLine("The animal makes a sound");
    }
}

public class Dog : Animal
{
    public override void MakeSound()
    {
        Console.WriteLine("The dog barks");
    }
}

public class Cat : Animal
{
    public override void MakeSound()
    {
        Console.WriteLine("The cat meows");
    }
}

// Usage with polymorphism
Animal myAnimal = new Animal();
Animal myDog = new Dog();
Animal myCat = new Cat();

myAnimal.MakeSound(); // Output: The animal makes a sound
myDog.MakeSound();    // Output: The dog barks
myCat.MakeSound();    // Output: The cat meows

// Using polymorphism with an array
Animal[] animals = new Animal[3];
animals[0] = new Animal();
animals[1] = new Dog();
animals[2] = new Cat();

foreach (Animal animal in animals)
{
    animal.MakeSound(); // Calls the appropriate method for each type
}
```

## Abstraction

Abstraction hides complex implementation details and shows only the necessary features of an object.

### Example:

```csharp
// Abstract class
public abstract class Vehicle
{
    // Properties
    public string Model { get; set; }
    public int Year { get; set; }
    
    // Constructor
    public Vehicle(string model, int year)
    {
        Model = model;
        Year = year;
    }
    
    // Abstract method - must be implemented by derived classes
    public abstract void Start();
    
    // Regular method
    public void ShowInfo()
    {
        Console.WriteLine($"Model: {Model}, Year: {Year}");
    }
}

// Concrete class implementing the abstract class
public class Car : Vehicle
{
    public Car(string model, int year) : base(model, year)
    {
    }
    
    // Implementation of the abstract method
    public override void Start()
    {
        Console.WriteLine("Car started with key");
    }
}

public class ElectricCar : Vehicle
{
    public ElectricCar(string model, int year) : base(model, year)
    {
    }
    
    public override void Start()
    {
        Console.WriteLine("Electric car started with button");
    }
}

// Usage
// Vehicle vehicle = new Vehicle("Generic", 2022); // Error: Cannot create instance of abstract class
Car car = new Car("Toyota", 2022);
car.Start(); // Output: Car started with key
car.ShowInfo(); // Output: Model: Toyota, Year: 2022

ElectricCar electricCar = new ElectricCar("Tesla", 2023);
electricCar.Start(); // Output: Electric car started with button
```

## Interfaces

Interfaces define a contract that implementing classes must follow. They contain method signatures, properties, events, and indexers without implementation.

### Example:

```csharp
// Interface definition
public interface IPayable
{
    decimal CalculatePayment();
    void ProcessPayment();
}

// Another interface
public interface ITaxable
{
    decimal CalculateTax();
}

// Class implementing multiple interfaces
public class Employee : IPayable, ITaxable
{
    public string Name { get; set; }
    public decimal BaseSalary { get; set; }
    
    public Employee(string name, decimal baseSalary)
    {
        Name = name;
        BaseSalary = baseSalary;
    }
    
    public decimal CalculatePayment()
    {
        // Implementation for IPayable
        return BaseSalary;
    }
    
    public void ProcessPayment()
    {
        // Implementation for IPayable
        Console.WriteLine($"Processing payment for {Name}");
    }
    
    public decimal CalculateTax()
    {
        // Implementation for ITaxable
        return BaseSalary * 0.2m; // 20% tax
    }
}

// Another class implementing IPayable
public class Invoice : IPayable
{
    public string InvoiceNumber { get; set; }
    public decimal Amount { get; set; }
    
    public decimal CalculatePayment()
    {
        return Amount;
    }
    
    public void ProcessPayment()
    {
        Console.WriteLine($"Processing payment for invoice {InvoiceNumber}");
    }
}

// Using interfaces for polymorphism
public void ProcessPayments(IPayable[] payableItems)
{
    foreach (var item in payableItems)
    {
        decimal amount = item.CalculatePayment();
        Console.WriteLine($"Payment amount: {amount}");
        item.ProcessPayment();
    }
}

// Usage
Employee employee = new Employee("John", 5000);
Invoice invoice = new Invoice { InvoiceNumber = "INV001", Amount = 1500 };

IPayable[] payableItems = { employee, invoice };
ProcessPayments(payableItems);
```

## Generic Classes

Generics enable you to design classes and methods that defer the specification of data types until the class or method is declared and instantiated.

### Example:

```csharp
// Generic class
public class GenericList<T>
{
    private T[] items;
    private int count;
    
    public GenericList(int capacity)
    {
        items = new T[capacity];
        count = 0;
    }
    
    public void Add(T item)
    {
        if (count < items.Length)
        {
            items[count] = item;
            count++;
        }
        else
        {
            throw new IndexOutOfRangeException("List is full");
        }
    }
    
    public T GetItem(int index)
    {
        if (index < 0 || index >= count)
        {
            throw new IndexOutOfRangeException();
        }
        return items[index];
    }
    
    public int Count
    {
        get { return count; }
    }
}

// Usage
GenericList<string> stringList = new GenericList<string>(5);
stringList.Add("Hello");
stringList.Add("World");
Console.WriteLine(stringList.GetItem(0)); // Output: Hello

GenericList<int> intList = new GenericList<int>(10);
intList.Add(10);
intList.Add(20);
Console.WriteLine(intList.GetItem(1)); // Output: 20
```

## Delegates and Events

Delegates are type-safe function pointers that can reference methods with a compatible signature. Events are a way for a class to notify other classes when something of interest happens.

### Example:

```csharp
// Delegate definition
public delegate void MessageHandler(string message);

// Class with event
public class Publisher
{
    // Event based on delegate
    public event MessageHandler MessageReceived;
    
    // Method to trigger the event
    public void SendMessage(string message)
    {
        Console.WriteLine($"Publisher sending message: {message}");
        
        // Check if there are any subscribers
        if (MessageReceived != null)
        {
            // Invoke the event
            MessageReceived(message);
        }
    }
}

// Subscriber class
public class Subscriber
{
    private string name;
    
    public Subscriber(string name)
    {
        this.name = name;
    }
    
    // Method that matches the delegate signature
    public void OnMessageReceived(string message)
    {
        Console.WriteLine($"{name} received: {message}");
    }
}

// Usage
Publisher publisher = new Publisher();

Subscriber sub1 = new Subscriber("Subscriber 1");
Subscriber sub2 = new Subscriber("Subscriber 2");

// Subscribe to the event
publisher.MessageReceived += sub1.OnMessageReceived;
publisher.MessageReceived += sub2.OnMessageReceived;

// Trigger the event
publisher.SendMessage("Hello World!");

// Unsubscribe from the event
publisher.MessageReceived -= sub1.OnMessageReceived;

// Only sub2 will receive this message
publisher.SendMessage("Second message");
```

## Properties and Auto-Implemented Properties

Properties provide a way to protect a field by reading and writing to it through special accessor methods. Auto-implemented properties simplify property declarations when no additional logic is needed.

### Example:

```csharp
public class Student
{
    // Full property with backing field
    private string _name;
    public string Name
    {
        get { return _name; }
        set { _name = value; }
    }
    
    // Auto-implemented property (compiler creates the backing field automatically)
    public int Age { get; set; }
    
    // Read-only auto-implemented property
    public string StudentId { get; private set; }
    
    // Auto-property with default value (C# 6.0+)
    public bool IsActive { get; set; } = true;
    
    public Student(string name, int age, string studentId)
    {
        Name = name;
        Age = age;
        StudentId = studentId;
    }
}

// Usage
Student student = new Student("Alice", 20, "S12345");
Console.WriteLine($"Name: {student.Name}, Age: {student.Age}, ID: {student.StudentId}");
student.Name = "Alice Smith";
// student.StudentId = "S67890"; // Error: Cannot access set accessor
```

## Method Overloading and Overriding

Method overloading allows multiple methods with the same name but different parameters. Method overriding is redefining a method in a derived class that already exists in the base class.

### Example:

```csharp
public class Calculator
{
    // Method overloading - same method name, different parameters
    public int Add(int a, int b)
    {
        return a + b;
    }
    
    public double Add(double a, double b)
    {
        return a + b;
    }
    
    public int Add(int a, int b, int c)
    {
        return a + b + c;
    }
    
    // Virtual method that can be overridden
    public virtual string Describe()
    {
        return "Basic Calculator";
    }
}

public class ScientificCalculator : Calculator
{
    // Method overriding - same signature, different implementation
    public override string Describe()
    {
        return "Scientific Calculator";
    }
    
    // Method hiding - using 'new' keyword
    public new int Add(int a, int b)
    {
        Console.WriteLine("Using scientific calculator's Add method");
        return base.Add(a, b);
    }
}

// Usage
Calculator calc = new Calculator();
Console.WriteLine(calc.Add(5, 10));           // Output: 15
Console.WriteLine(calc.Add(5.5, 10.5));       // Output: 16.0
Console.WriteLine(calc.Add(5, 10, 15));       // Output: 30

ScientificCalculator sciCalc = new ScientificCalculator();
Console.WriteLine(sciCalc.Describe());        // Output: Scientific Calculator

Calculator baseCalc = sciCalc;
Console.WriteLine(baseCalc.Describe());       // Output: Scientific Calculator (polymorphism)
```

## Extension Methods

Extension methods allow adding methods to existing types without modifying them.

### Example:

```csharp
// Must be in a static class
public static class StringExtensions
{
    // Extension method for string type
    public static bool IsValidEmail(this string str)
    {
        // Simple validation - contains @ and period
        return str != null && str.Contains("@") && str.Contains(".");
    }
    
    public static string Reverse(this string str)
    {
        if (string.IsNullOrEmpty(str))
            return str;
            
        char[] chars = str.ToCharArray();
        Array.Reverse(chars);
        return new string(chars);
    }
}

// Usage
string email = "user@example.com";
bool isValid = email.IsValidEmail(); // Extension method called as if it were a regular method
Console.WriteLine($"Is valid email: {isValid}"); // Output: True

string text = "Hello, World!";
string reversed = text.Reverse();
Console.WriteLine(reversed); // Output: !dlroW ,olleH
```

## Composition vs Inheritance

Composition creates a "has-a" relationship, while inheritance creates an "is-a" relationship. Composition is often preferred over inheritance for flexibility.

### Example:

```csharp
// Composition example - "has-a" relationship
public class Engine
{
    public void Start()
    {
        Console.WriteLine("Engine started");
    }
    
    public void Stop()
    {
        Console.WriteLine("Engine stopped");
    }
}

public class Car
{
    // Car "has-a" Engine - composition
    private Engine engine;
    
    public Car()
    {
        engine = new Engine();
    }
    
    public void Start()
    {
        Console.WriteLine("Car starting...");
        engine.Start();
        Console.WriteLine("Car started");
    }
    
    public void Stop()
    {
        Console.WriteLine("Car stopping...");
        engine.Stop();
        Console.WriteLine("Car stopped");
    }
}

// Inheritance example - "is-a" relationship
public class Vehicle
{
    public virtual void Move()
    {
        Console.WriteLine("Vehicle is moving");
    }
}

public class Bicycle : Vehicle  // Bicycle "is-a" Vehicle - inheritance
{
    public override void Move()
    {
        Console.WriteLine("Bicycle is moving by pedaling");
    }
}

// Usage
Car car = new Car();
car.Start();
car.Stop();

Bicycle bicycle = new Bicycle();
bicycle.Move();
```

## Static Classes and Members

Static classes cannot be instantiated and can only contain static members. Static members belong to the type itself, not to instances.

### Example:

```csharp
// Static class
public static class MathHelper
{
    // Static property
    public static double PI { get; } = 3.14159;
    
    // Static method
    public static double CalculateCircleArea(double radius)
    {
        return PI * radius * radius;
    }
    
    public static double CalculateCircleCircumference(double radius)
    {
        return 2 * PI * radius;
    }
}

// Class with static and instance members
public class Counter
{
    // Static field - shared by all instances
    private static int instanceCount = 0;
    
    // Instance field - unique to each instance
    private int currentCount;
    
    // Constructor
    public Counter()
    {
        instanceCount++;
        currentCount = 0;
    }
    
    // Static property
    public static int InstanceCount
    {
        get { return instanceCount; }
    }
    
    // Instance method
    public void Increment()
    {
        currentCount++;
    }
    
    // Instance property
    public int CurrentCount
    {
        get { return currentCount; }
    }
}

// Usage
double area = MathHelper.CalculateCircleArea(5);
Console.WriteLine($"Circle area: {area}");

// Create instances and demonstrate static vs instance members
Counter c1 = new Counter();
Counter c2 = new Counter();
c1.Increment();
c2.Increment();
c2.Increment();

Console.WriteLine($"c1 count: {c1.CurrentCount}");      // Output: 1
Console.WriteLine($"c2 count: {c2.CurrentCount}");      // Output: 2
Console.WriteLine($"Total instances: {Counter.InstanceCount}"); // Output: 2
```

## Sealed Classes

Sealed classes cannot be inherited from. This can be used to prevent further derivation and to optimize performance.

### Example:

```csharp
public class Base
{
    public virtual void Method1()
    {
        Console.WriteLine("Base.Method1()");
    }
}

public sealed class Derived : Base
{
    public override void Method1()
    {
        Console.WriteLine("Derived.Method1()");
    }
    
    public void Method2()
    {
        Console.WriteLine("Derived.Method2()");
    }
}

// The following would cause a compiler error:
// public class AnotherDerived : Derived { }  // Error: Cannot derive from sealed type 'Derived'

// Method sealing - prevent override in derived classes
public class BaseWithSealedMethod
{
    public virtual void Method()
    {
        Console.WriteLine("Base.Method()");
    }
}

public class DerivedWithSealedMethod : BaseWithSealedMethod
{
    // Sealed method cannot be overridden in derived classes
    public sealed override void Method()
    {
        Console.WriteLine("Derived.Method() - sealed");
    }
}

public class ThirdLevel : DerivedWithSealedMethod
{
    // This would cause a compiler error:
    // public override void Method() { } // Error: Cannot override sealed method
}
```

## Partial Classes

Partial classes allow splitting a class definition across multiple files.

### Example:

```csharp
// File1.cs
public partial class Customer
{
    // Properties
    public int Id { get; set; }
    public string Name { get; set; }
    
    // Constructor
    public Customer(int id, string name)
    {
        Id = id;
        Name = name;
    }
}

// File2.cs
public partial class Customer
{
    // Methods
    public void DisplayInfo()
    {
        Console.WriteLine($"Customer ID: {Id}, Name: {Name}");
    }
    
    public bool IsValid()
    {
        return Id > 0 && !string.IsNullOrEmpty(Name);
    }
}

// Usage
Customer customer = new Customer(1, "John Doe");
customer.DisplayInfo();
Console.WriteLine($"Is valid: {customer.IsValid()}");
```

## Exception Handling in OOP

Exception handling is a key part of object-oriented programming, allowing for robust error detection and recovery.

### Example:

```csharp
public class BankAccount
{
    private decimal balance;
    private readonly string accountNumber;
    
    // Custom exception class
    public class InsufficientFundsException : Exception
    {
        public decimal AttemptedAmount { get; }
        public decimal CurrentBalance { get; }
        
        public InsufficientFundsException(string message, decimal attemptedAmount, decimal currentBalance)
            : base(message)
        {
            AttemptedAmount = attemptedAmount;
            CurrentBalance = currentBalance;
        }
    }
    
    public BankAccount(string accountNumber, decimal initialBalance)
    {
        if (initialBalance < 0)
        {
            throw new ArgumentException("Initial balance cannot be negative", nameof(initialBalance));
        }
        
        this.accountNumber = accountNumber;
        this.balance = initialBalance;
    }
    
    public void Withdraw(decimal amount)
    {
        if (amount <= 0)
        {
            throw new ArgumentException("Amount must be positive", nameof(amount));
        }
        
        if (amount > balance)
        {
            throw new InsufficientFundsException(
                "Insufficient funds for this withdrawal", 
                amount, 
                balance);
        }
        
        balance -= amount;
    }
    
    public decimal Balance
    {
        get { return balance; }
    }
}

// Usage
try
{
    BankAccount account = new BankAccount("123456", 1000);
    Console.WriteLine($"Initial balance: {account.Balance}");
    
    account.Withdraw(500);
    Console.WriteLine($"Balance after withdrawal: {account.Balance}");
    
    // This will throw an exception
    account.Withdraw(700);
}
catch (BankAccount.InsufficientFundsException ex)
{
    Console.WriteLine($"Error: {ex.Message}");
    Console.WriteLine($"Attempted to withdraw {ex.AttemptedAmount} but current balance is {ex.CurrentBalance}");
}
catch (ArgumentException ex)
{
    Console.WriteLine($"Invalid argument: {ex.Message}");
}
catch (Exception ex)
{
    Console.WriteLine($"Unexpected error: {ex.Message}");
}
finally
{
    Console.WriteLine("Transaction completed");
}
```

## Namespaces

Namespaces help organize code and avoid naming collisions.

### Example:

```csharp
// Define a namespace
namespace Finance
{
    public class BankAccount
    {
        public decimal Balance { get; private set; }
        
        public void Deposit(decimal amount)
        {
            Balance += amount;
        }
    }
}

namespace HR
{
    public class Employee
    {
        public string Name { get; set; }
        public decimal Salary { get; set; }
    }
}

// Using namespaces
using Finance;
using HR;

// Without the 'using' directive
Finance.BankAccount account = new Finance.BankAccount();
HR.Employee employee = new HR.Employee();

// With the 'using' directive
BankAccount account2 = new BankAccount();
Employee employee2 = new Employee();

// Nested namespaces
namespace Company.Project.Module
{
    public class Service
    {
        public void Run()
        {
            Console.WriteLine("Service running");
        }
    }
}

// Using nested namespace
Company.Project.Module.Service service = new Company.Project.Module.Service();
```

## LINQ and OOP

Language Integrated Query (LINQ) seamlessly integrates query capabilities into C# and works well with OOP concepts.

### Example:

```csharp
public class Product
{
    public int Id { get; set; }
    public string Name { get; set; }
    public decimal Price { get; set; }
    public string Category { get; set; }
}

public class ProductRepository
{
    private List<Product> products;
    
    public ProductRepository()
    {
        products = new List<Product>
        {
            new Product { Id = 1, Name = "Laptop", Price = 1200, Category = "Electronics" },
            new Product { Id = 2, Name = "Phone", Price = 800, Category = "Electronics" },
            new Product { Id = 3, Name = "Book", Price = 25, Category = "Books" },
            new Product { Id = 4, Name = "Headphones", Price = 150, Category = "Electronics" },
            new Product { Id = 5, Name = "Desk", Price = 300, Category = "Furniture" }
        };
    }
    
    public List<Product> GetExpensiveElectronics(decimal minPrice)
    {
        // LINQ query syntax
        var query = from p in products
                    where p.Category == "Electronics" && p.Price > minPrice
                    orderby p.Price descending
                    select p;
                    
        return query.ToList();
    }
    
    public List<string> GetProductNames()
    {
        // LINQ method syntax
        return products
            .OrderBy(p => p.Name)
            .Select(p => p.Name)
            .ToList();
    }
    
    public IEnumerable<IGrouping<string, Product>> GroupByCategory()
    {
        return products.GroupBy(p => p.Category);
    }
    
    public decimal GetAveragePrice()
    {
        return products.Average(p => p.Price);
    }
}

// Usage
var repo = new ProductRepository();

var expensiveElectronics = repo.GetExpensiveElectronics(500);
foreach (var product in expensiveElectronics)
{
    Console.WriteLine($"{product.Name}: ${product.Price}");
}

var productNames = repo.GetProductNames();
Console.WriteLine($"Products: {string.Join(", ", productNames)}");

var groupedProducts = repo.GroupByCategory();
foreach (var group in groupedProducts)
{
    Console.WriteLine($"Category: {group.Key}");
    foreach (var product in group)
    {
        Console.WriteLine($"  - {product.Name}: ${product.Price}");
    }
}

Console.WriteLine($"Average price: ${repo.GetAveragePrice()}");
```

## Lambda Expressions

Lambda expressions provide a concise way to represent anonymous methods and are commonly used with delegates.

### Example:

```csharp
public class LambdaDemo
{
    public void Run()
    {
        // Simple lambda expression with Func delegate
        Func<int, int> square = x => x * x;
        Console.WriteLine(square(5)); // Output: 25
        
        // Lambda with multiple parameters
        Func<int, int, int> add = (x, y) => x + y;
        Console.WriteLine(add(3, 7)); // Output: 10
        
        // Lambda with statement block
        Func<int, int> factorial = n =>
        {
            int result = 1;
            for (int i = 1; i <= n; i++)
            {
                result *= i;
            }
            return result;
        };
        Console.WriteLine(factorial(5)); // Output: 120
        
        // Lambda with LINQ
        List<int> numbers = new List<int> { 1, 5, 3, 9, 7, 4 };
        
        var evenNumbers = numbers.Where(n => n % 2 == 0);
        Console.WriteLine(string.Join(", ", evenNumbers)); // Output: 4
        
        var squaredNumbers = numbers.Select(n => n * n);
        Console.WriteLine(string.Join(", ", squaredNumbers)); // Output: 1, 25, 9, 81, 49, 16
        
        // Using Action delegate with lambda
        Action<string> greet = name => Console.WriteLine($"Hello, {name}!");
        greet("Alice"); // Output: Hello, Alice!
        
        // Lambda capturing variables
        for (int i = 1; i <= 3; i++)
        {
            int counter = i; // Capture in a local variable to avoid closure issues
            
            // Creating a delayed action that captures the counter value
            Action action = () => Console.WriteLine($"Counter value: {counter}");
            action(); // Output: Counter value: 1, 2, 3
        }
    }
    
    // Using lambda as event handler
    public void SetupButton()
    {
        // In a real application, this would be a UI button
        var button = new { Text = "Click Me" };
        
        // Event handler using lambda
        // button.Click += (sender, e) => Console.WriteLine("Button was clicked!");
    }
    
    // Using lambda for sorting
    public void SortExample()
    {
        var people = new List<Person>
        {
            new Person { Name = "Alice", Age = 25 },
            new Person { Name = "Bob", Age = 30 },
            new Person { Name = "Charlie", Age = 20 }
        };
        
        // Sort by age
        people.Sort((p1, p2) => p1.Age.CompareTo(p2.Age));
        
        foreach (var person in people)
        {
            Console.WriteLine($"{person.Name}: {person.Age}");
        }
        // Output:
        // Charlie: 20
        // Alice: 25
        // Bob: 30
    }
    
    public class Person
    {
        public string Name { get; set; }
        public int Age { get; set; }
    }
}

## Summary Diagrams and Exam Tips

### OOP Principles Quick Reference

**Encapsulation:**
- Hide implementation details 
- Control access using access modifiers (private, protected, public)
- Use properties to expose controlled access to data

**Inheritance:**
- "Is-a" relationship
- Base class (parent) → Derived class (child)
- Use `virtual` and `override` for polymorphism
- C# only supports single inheritance for classes

**Polymorphism:**
- Static: Method overloading (compile-time)
- Dynamic: Method overriding (runtime)
- Using base class references to call derived class methods

**Abstraction:**
- Focus on what an object does, not how it works
- Use `abstract` classes and methods
- Cannot instantiate abstract classes

### Common Exam Questions

1. **Difference between abstract class and interface?**
   - Abstract class: Can have implementation, constructors, fields; single inheritance
   - Interface: No implementation (before C# 8), no fields, multiple inheritance

2. **When to use struct vs class?**
   - Struct: Small, value type, immutable, stack-based (faster for small data)
   - Class: Reference type, inheritance, heap-based, mutable

3. **Method hiding vs overriding?**
   - Hiding: `new` keyword, base reference calls base method
   - Overriding: `override` keyword, base reference calls derived method

4. **Access modifiers purpose:**
   - `public`: Accessible everywhere
   - `private`: Only within containing class
   - `protected`: Within class and derived classes
   - `internal`: Within same assembly
   - `protected internal`: Within same assembly or derived classes

5. **C# naming conventions:**
   - PascalCase: Classes, methods, properties
   - camelCase: Variables, parameters
   - _camelCase: Private fields

### Performance Considerations

**Memory Efficiency:**
- Use structs for small data (≤16 bytes)
- Consider using readonly properties for immutable objects
- Implement IDisposable for resource cleanup

**Runtime Performance:**
- Virtual method calls have slight overhead
- Sealed classes can be optimized by compiler
- Generics offer better performance than object boxing/unboxing

### OOP Best Practices

1. Follow Single Responsibility Principle (SRP)
2. Prefer composition over inheritance
3. Code to interfaces, not implementations
4. Keep inheritance hierarchies shallow
5. Use dependency injection for better testability
6. Make classes immutable where possible
7. Override ToString() for better debugging
8. Use properties instead of public fields

### Memory Diagram: Value vs Reference Types

```
Stack Memory         Heap Memory
+------------+       +------------+
| struct p1  |       | class c1   |
| X: 5       |       | Name: "John"|
| Y: 10      |       +------------+
+------------+           ↑
                         |
| struct p2  |       +--|----------+
| X: 5       |       | reference  |
| Y: 10      |       +------------+
+------------+
```

### Key Differences Between OOP Languages

| Feature           | C#                | Java               | C++                |
|-------------------|-------------------|--------------------|--------------------|
| Multiple Inherit. | Interfaces only   | Interfaces only    | Full support       |
| Properties        | Built-in          | Manual get/set     | Manual get/set     |
| Operator Overload | Supported         | Not supported      | Supported          | 
| Memory Management | Garbage Collection| Garbage Collection | Manual + RAII      |
| Generics          | Runtime+Compile   | Erasure (Runtime)  | Templates (Compile)|

Remember these concepts for your exams, and you'll be well prepared to tackle any OOP question!
