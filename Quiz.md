# C# Programming Notes - Comprehensive Guide

## Table of Contents
1. [Why Programming](#why-programming)
2. [.NET Framework Architecture](#net-framework-architecture)
3. [Types in C#](#types-in-c)
4. [Value Types](#value-types)
5. [Reference Types](#reference-types)
6. [Constants](#constants)
7. [Properties](#properties)
8. [Control Structures](#control-structures)
9. [Conditional Statements](#conditional-statements)
10. [Loops](#loops)
11. [Break and Continue Statements](#break-and-continue-statements)
12. [Exception Handling](#exception-handling)
13. [Methods and Functions](#methods-and-functions)
14. [Object-Oriented Programming (OOP) - The Four Principles](#object-oriented-programming-oop---the-four-principles)

## Why Programming - Short Q&A

### Definition
Programming is the process of creating instructions for computers to solve problems, automate tasks, and build software applications using programming languages.

**Q: Why learn programming?**  
A: Programming teaches problem-solving, logical thinking, and enables you to create software solutions for real-world problems. It develops:
- Analytical thinking skills
- Logic and reasoning abilities
- Creativity in solution design
- Problem decomposition techniques
- Mathematical and computational thinking

**Q: Why choose C#?**  
A: C# (pronounced "C-Sharp") is a modern, type-safe, object-oriented programming language developed by Microsoft. It's versatile and widely used for:
- **Desktop Applications**: Windows Forms, WPF applications
- **Web Development**: ASP.NET Core web applications and APIs
- **Game Development**: Unity game engine development
- **Mobile Development**: Xamarin cross-platform apps
- **Enterprise Software**: Large-scale business applications
- **Cloud Applications**: Azure cloud services
- **Machine Learning**: ML.NET framework

### Key Advantages of C#:
- **Type Safety**: Prevents common programming errors at compile time
- **Memory Management**: Automatic garbage collection
- **Rich Ecosystem**: Extensive .NET library and NuGet packages
- **Cross-Platform**: Runs on Windows, macOS, and Linux
- **Strong Community**: Large developer community and support

## .NET Framework Architecture

### Definition
The .NET Framework is a comprehensive development platform that provides a runtime environment and programming model for building and running applications on Windows. It consists of several key components working together.

### Key Components:

1. **CLR (Common Language Runtime)**: 
   - The execution environment that handles running applications
   - Provides memory management, garbage collection, exception handling
   - Enables cross-language interoperability
   - Converts Intermediate Language (IL) to native machine code

2. **Base Class Library (BCL)**: 
   - Collection of reusable types and functions
   - Provides fundamental programming functionality
   - Includes collections, I/O, threading, security, etc.

3. **Framework Class Library (FCL)**:
   - Higher-level services built on BCL
   - Includes ASP.NET, Windows Forms, WPF, etc.

4. **Common Type System (CTS)**:
   - Defines how types are declared, used, and managed
   - Ensures type safety across different .NET languages

5. **Common Language Specification (CLS)**:
   - Subset of CTS that defines language interoperability rules

### .NET Compilation Process:
1. Source code (.cs) → Compiler (csc.exe) → Intermediate Language (IL)
2. IL + Metadata → Just-In-Time (JIT) Compiler → Native Machine Code
3. Native code executes under CLR supervision

```csharp
// Example showing .NET class library usage
using System;           // Basic system functionality
using System.Collections.Generic;  // Generic collections
using System.IO;        // Input/output operations

namespace MyApplication 
{
    class Program 
    {
        static void Main(string[] args) 
        {
            // Using Console class from System namespace
            Console.WriteLine("Hello .NET Framework!");
            
            // Using generic collections from System.Collections.Generic
            List<string> fruits = new List<string> { "Apple", "Banana", "Orange" };
            
            // Using File class from System.IO
            string filePath = "sample.txt";
            File.WriteAllText(filePath, "Hello from .NET!");
            
            Console.WriteLine($"File created: {File.Exists(filePath)}");
        }
    }
}
```

## Types in C# - Value vs Reference

### Definition
C# has a rich type system that categorizes all data types into two main categories based on how they store data and behave during assignment operations.

### Memory Allocation:
- **Stack**: Fast, automatic memory management, limited size, stores value types
- **Heap**: Larger memory space, managed by garbage collector, stores reference types

### Value Types (Stack Allocation)
**Definition**: Value types directly contain their data. When you assign a value type to another variable, a copy of the data is created.

**Characteristics**:
- Stored directly on the stack (or inline in reference types)
- Assignment creates a copy of the data
- Cannot be null (unless nullable)
- Automatically initialized to default values
- Passed by value to methods (unless using ref/out)
- Memory automatically reclaimed when scope ends

**Examples**: 
- Built-in types: int, double, bool, char, decimal
- User-defined: struct, enum
- Special: nullable types, tuples

### Reference Types (Heap Allocation)
**Definition**: Reference types contain a reference (pointer) to the memory location where the actual data is stored on the heap.

**Characteristics**:
- Reference stored on stack, object data stored on heap
- Assignment copies the reference, not the data
- Can be null
- Default value is null
- Passed by reference to methods
- Memory managed by garbage collector
- Multiple variables can reference the same object

**Examples**:
- Built-in types: string, array, object
- User-defined: class, interface, delegate
- Special: anonymous types, dynamic types

```csharp
// Demonstrating value vs reference type behavior
class ValueVsReferenceDemo 
{
    public static void Main() 
    {
        // Value type behavior
        int a = 10;
        int b = a;      // Copy of value
        b = 20;
        Console.WriteLine($"a = {a}, b = {b}"); // a = 10, b = 20
        
        // Reference type behavior
        int[] array1 = { 1, 2, 3 };
        int[] array2 = array1;  // Copy of reference
        array2[0] = 100;
        Console.WriteLine($"array1[0] = {array1[0]}"); // array1[0] = 100
    }
}
```

## Value Types

### Simple Types (Built-in Primitives)

**Definition**: Simple types are the fundamental building blocks of C# programming. They represent basic data values and are directly supported by the language with specific keywords.

#### Integral Types
- **Purpose**: Store whole numbers without decimal points
- **Memory**: Various sizes from 8-bit to 64-bit
- **Range**: Different ranges based on signed/unsigned nature

```csharp
// Integral types with ranges and examples
byte b = 255;           // 8-bit unsigned: 0 to 255
sbyte sb = -128;        // 8-bit signed: -128 to 127
short s = -32768;       // 16-bit signed: -32,768 to 32,767
ushort us = 65535;      // 16-bit unsigned: 0 to 65,535
int i = -2147483648;    // 32-bit signed: -2,147,483,648 to 2,147,483,647
uint ui = 4294967295U;  // 32-bit unsigned: 0 to 4,294,967,295
long l = -9223372036854775808L;  // 64-bit signed
ulong ul = 18446744073709551615UL; // 64-bit unsigned

// Hexadecimal and binary notation
int hex = 0xFF;         // Hexadecimal (255 in decimal)
int binary = 0b1111;    // Binary notation (15 in decimal)

// Digit separators for readability
int million = 1_000_000;
long bigNumber = 9_223_372_036_854_775_807L;
```

#### Floating-Point Types
- **Purpose**: Store numbers with decimal points
- **Precision**: Different levels of precision and range

```csharp
// Floating-point types
float f = 3.14159F;     // 32-bit, ~7 digits precision
double d = 3.141592653589793;  // 64-bit, ~15-17 digits precision
decimal m = 3.14159265358979323846M; // 128-bit, 28-29 digits precision

// Scientific notation
double scientific = 1.23e-4;  // 0.000123
float negative = -2.5e3F;     // -2500

// Special floating-point values
double positiveInfinity = double.PositiveInfinity;
double negativeInfinity = double.NegativeInfinity;
double notANumber = double.NaN;

// Checking for special values
if (double.IsInfinity(positiveInfinity)) 
{
    Console.WriteLine("It's infinity!");
}
```

#### Character and Boolean Types
```csharp
// Character type - single Unicode character
char letter = 'A';                // Letter
char digit = '9';                 // Digit character
char symbol = '$';                // Symbol
char unicode = '\u0041';          // Unicode escape (A)
char newline = '\n';              // Escape sequence

// Boolean type - true or false
bool isTrue = true;
bool isFalse = false;
bool result = (10 > 5);           // Expression result: true

// Logical operations
bool and = true && false;         // false
bool or = true || false;          // true
bool not = !true;                 // false
```

### Struct (User-Defined Value Type)

**Definition**: A struct is a value type that can encapsulate data and related functionality. It's similar to a class but with value semantics, making it ideal for small, simple objects that represent single values.

**Characteristics**:
- Value type (stored on stack or inline)
- Cannot inherit from other structs or classes (except interfaces)
- Cannot be inherited by other types
- Automatically gets a parameterless constructor
- All fields must be initialized before use
- Supports constructors, methods, properties, and indexers
- Ideal for immutable data structures

**When to Use Structs**:
- Small, simple data structures
- Immutable types
- Types that don't require reference semantics
- Performance-critical scenarios where avoiding heap allocation is important

```csharp
// Basic struct definition
public struct Point 
{
    // Fields
    public int X;
    public int Y;
    
    // Constructor (must initialize all fields)
    public Point(int x, int y) 
    {
        X = x;
        Y = y;
    }
    
    // Method
    public void Display() 
    {
        Console.WriteLine($"Point: ({X}, {Y})");
    }
    
    // Property
    public double DistanceFromOrigin => Math.Sqrt(X * X + Y * Y);
    
    // Override ToString for better display
    public override string ToString() 
    {
        return $"({X}, {Y})";
    }
}

// Advanced struct example - representing a complex number
public readonly struct Complex 
{
    public readonly double Real;
    public readonly double Imaginary;
    
    public Complex(double real, double imaginary) 
    {
        Real = real;
        Imaginary = imaginary;
    }
    
    // Computed property
    public double Magnitude => Math.Sqrt(Real * Real + Imaginary * Imaginary);
    
    // Operator overloading
    public static Complex operator +(Complex a, Complex b) 
    {
        return new Complex(a.Real + b.Real, a.Imaginary + b.Imaginary);
    }
    
    public override string ToString() 
    {
        return $"{Real} + {Imaginary}i";
    }
}

// Usage examples
class StructDemo 
{
    public static void Main() 
    {
        // Creating struct instances
        Point p1 = new Point();     // Default constructor: (0, 0)
        Point p2 = new Point(3, 4); // Custom constructor
        Point p3;                   // Uninitialized
        p3.X = 1;
        p3.Y = 2;
        
        // Using methods and properties
        p2.Display();              // Output: Point: (3, 4)
        Console.WriteLine($"Distance: {p2.DistanceFromOrigin:F2}"); // 5.00
        
        // Value semantics - copying
        Point p4 = p2;  // Creates a copy
        p4.X = 10;      // Doesn't affect p2
        Console.WriteLine($"p2: {p2}, p4: {p4}"); // p2: (3, 4), p4: (10, 4)
        
        // Complex number example
        Complex c1 = new Complex(3, 4);
        Complex c2 = new Complex(1, 2);
        Complex sum = c1 + c2;
        Console.WriteLine($"{c1} + {c2} = {sum}"); // 3 + 4i + 1 + 2i = 4 + 6i
    }
}
```

### Enum (Named Constants)

**Definition**: An enum (enumeration) is a value type that defines a set of named constants. It provides a way to assign meaningful names to integral constant values, making code more readable and maintainable.

**Characteristics**:
- Based on integral types (default is int)
- Provides type safety for constants
- Can be used in switch statements
- Supports bitwise operations (with [Flags] attribute)
- Can have explicit values assigned
- Underlying values start from 0 by default

**Benefits**:
- Code readability and maintainability
- Type safety (prevents invalid values)
- IntelliSense support
- Easy to refactor

```csharp
// Basic enum definition
public enum DayOfWeek 
{
    Sunday,     // 0 (default)
    Monday,     // 1
    Tuesday,    // 2
    Wednesday,  // 3
    Thursday,   // 4
    Friday,     // 5
    Saturday    // 6
}

// Enum with explicit values
public enum HttpStatusCode 
{
    OK = 200,
    NotFound = 404,
    InternalServerError = 500,
    BadRequest = 400
}

// Enum with different underlying type
public enum FileAccess : byte 
{
    Read = 1,
    Write = 2,
    ReadWrite = Read | Write  // 3
}

// Flags enum for bitwise operations
[Flags]
public enum Permissions 
{
    None = 0,           // 0000
    Read = 1,           // 0001
    Write = 2,          // 0010
    Execute = 4,        // 0100
    Delete = 8,         // 1000
    All = Read | Write | Execute | Delete  // 1111
}

// Enum usage examples
class EnumDemo 
{
    public static void Main() 
    {
        // Basic usage
        DayOfWeek today = DayOfWeek.Friday;
        Console.WriteLine($"Today is {today}");
        Console.WriteLine($"Numeric value: {(int)today}"); // 5
        
        // Converting from string
        DayOfWeek parsed = (DayOfWeek)Enum.Parse(typeof(DayOfWeek), "Monday");
        Console.WriteLine($"Parsed: {parsed}");
        
        // Enum.TryParse (safer)
        if (Enum.TryParse<DayOfWeek>("Wednesday", out DayOfWeek day)) 
        {
            Console.WriteLine($"Successfully parsed: {day}");
        }
        
        // Getting all enum values
        foreach (DayOfWeek d in Enum.GetValues<DayOfWeek>()) 
        {
            Console.WriteLine($"{d} = {(int)d}");
        }
        
        // Flags enum usage
        Permissions userPermissions = Permissions.Read | Permissions.Write;
        Console.WriteLine($"User permissions: {userPermissions}");
        
        // Checking if flag is set
        bool canRead = userPermissions.HasFlag(Permissions.Read);
        Console.WriteLine($"Can read: {canRead}"); // True
        
        // Adding permission
        userPermissions |= Permissions.Execute;
        Console.WriteLine($"Updated permissions: {userPermissions}");
        
        // Removing permission
        userPermissions &= ~Permissions.Write;
        Console.WriteLine($"After removing write: {userPermissions}");
    }
}
```

### Nullable Types

**Definition**: Nullable types allow value types to represent their normal range of values plus an additional null value. This is particularly useful when working with databases or APIs where a value might be absent or undefined.

**Syntax**: 
- `T?` is shorthand for `Nullable<T>`
- Only works with value types
- Reference types are already nullable

**Common Scenarios**:
- Database fields that can be NULL
- Optional parameters
- Representing "no value" or "unknown" states
- API responses with optional fields

```csharp
// Nullable type declarations
int? nullableInt = null;        // Can be null or any int value
DateTime? nullableDate = null;  // Can be null or any DateTime
bool? nullableBool = true;      // Can be null, true, or false

// Checking for null
if (nullableInt.HasValue) 
{
    Console.WriteLine($"Value: {nullableInt.Value}");
} 
else 
{
    Console.WriteLine("No value (null)");
}

// Null coalescing operator
int defaultValue = nullableInt ?? 0;  // Use 0 if null
Console.WriteLine($"Default value: {defaultValue}");

// Null coalescing assignment (C# 8.0+)
nullableInt ??= 42;  // Assign 42 if nullableInt is null

// Nullable reference types (C# 8.0+)
#nullable enable
string? nullableString = null;  // Explicitly nullable
string nonNullableString = "Hello"; // Cannot be null

// Working with nullable types in methods
public static void ProcessNullableValue(int? value) 
{
    switch (value) 
    {
        case null:
            Console.WriteLine("Value is null");
            break;
        case 0:
            Console.WriteLine("Value is zero");
            break;
        default:
            Console.WriteLine($"Value is {value}");
            break;
    }
}
```

### Tuple (Lightweight Data Structure)

**Definition**: A tuple is a lightweight data structure that holds multiple values of different types. It provides a convenient way to group related values without creating a custom class or struct.

**Types of Tuples**:
1. **System.Tuple** (legacy, reference type)
2. **ValueTuple** (modern, value type, preferred)

**Benefits**:
- Quick data grouping without custom types
- Multiple return values from methods
- Temporary data structures
- Named or unnamed elements

```csharp
// Tuple literal syntax (ValueTuple)
(string, int) person = ("Rijoan", 30);
Console.WriteLine($"Name: {person.Item1}, Age: {person.Item2}");

// Named tuple elements
var personNamed = (Name: "Khairul", Age: 25, City: "New York");
Console.WriteLine($"Name: {personNamed.Name}");
Console.WriteLine($"Age: {personNamed.Age}");
Console.WriteLine($"City: {personNamed.City}");

// Tuple deconstruction
(string name, int age) = person;
Console.WriteLine($"Deconstructed - Name: {name}, Age: {age}");

// Discarding unwanted values
(string personName, _) = person;  // Ignore age
Console.WriteLine($"Only name: {personName}");

// Method returning tuple
public static (int min, int max, double average) AnalyzeNumbers(int[] numbers) 
{
    int min = numbers.Min();
    int max = numbers.Max();
    double avg = numbers.Average();
    return (min, max, avg);
}

// Using the tuple-returning method
int[] data = { 1, 5, 3, 9, 2, 8 };
var (minimum, maximum, average) = AnalyzeNumbers(data);
Console.WriteLine($"Min: {minimum}, Max: {maximum}, Avg: {average:F2}");

// Nested tuples
var nested = (Person: (Name: "Raisul", Age: 35), Address: (Street: "123 Main St", City: "Boston"));
Console.WriteLine($"Person: {nested.Person.Name}, City: {nested.Address.City}");

// Tuple comparison
var tuple1 = (1, "apple");
var tuple2 = (1, "apple");
var tuple3 = (2, "apple");

Console.WriteLine(tuple1 == tuple2); // True
Console.WriteLine(tuple1 == tuple3); // False
```
## Reference Types

### Class (Object-Oriented Blueprint)

**Definition**: A class is a reference type that serves as a blueprint for creating objects. It encapsulates data (fields/properties) and behavior (methods) into a single unit, supporting the principles of object-oriented programming.

**Key Concepts**:
- **Encapsulation**: Bundling data and methods together
- **Inheritance**: Creating new classes based on existing ones
- **Polymorphism**: Objects of different types responding to the same interface
- **Abstraction**: Hiding implementation details

**Class Members**:
- **Fields**: Store data
- **Properties**: Controlled access to data
- **Methods**: Define behavior
- **Constructors**: Initialize objects
- **Events**: Enable notifications
- **Indexers**: Array-like access

```csharp
// Comprehensive class example
public class Person 
{
    // Private fields (encapsulation)
    private string _firstName;
    private string _lastName;
    private DateTime _birthDate;
    
    // Static field (shared among all instances)
    private static int _totalPersons = 0;
    
    // Constructor
    public Person(string firstName, string lastName, DateTime birthDate) 
    {
        _firstName = firstName ?? throw new ArgumentNullException(nameof(firstName));
        _lastName = lastName ?? throw new ArgumentNullException(nameof(lastName));
        _birthDate = birthDate;
        _totalPersons++;
    }
    
    // Properties with validation
    public string FirstName 
    {
        get => _firstName;
        set => _firstName = !string.IsNullOrWhiteSpace(value) ? value : 
               throw new ArgumentException("First name cannot be empty");
    }
    
    public string LastName 
    {
        get => _lastName;
        set => _lastName = !string.IsNullOrWhiteSpace(value) ? value : 
               throw new ArgumentException("Last name cannot be empty");
    }
    
    // Read-only property
    public string FullName => $"{_firstName} {_lastName}";
    
    // Computed property
    public int Age 
    {
        get 
        {
            var today = DateTime.Today;
            var age = today.Year - _birthDate.Year;
            if (_birthDate.Date > today.AddYears(-age)) age--;
            return age;
        }
    }
    
    // Static property
    public static int TotalPersons => _totalPersons;
    
    // Methods
    public void Introduce() 
    {
        Console.WriteLine($"Hi, I'm {FullName} and I'm {Age} years old.");
    }
    
    public virtual void Work() 
    {
        Console.WriteLine($"{FullName} is working.");
    }
    
    // Method overloading
    public void SendMessage(string message) 
    {
        Console.WriteLine($"Sending message to {FullName}: {message}");
    }
    
    public void SendMessage(string message, string method) 
    {
        Console.WriteLine($"Sending message to {FullName} via {method}: {message}");
    }
    
    // Override Object methods
    public override string ToString() 
    {
        return $"Person: {FullName}, Age: {Age}";
    }
    
    public override bool Equals(object obj) 
    {
        if (obj is Person other)
            return _firstName == other._firstName && 
                   _lastName == other._lastName && 
                   _birthDate == other._birthDate;
        return false;
    }
    
    public override int GetHashCode() 
    {
        return HashCode.Combine(_firstName, _lastName, _birthDate);
    }
}

// Inheritance example
public class Employee : Person 
{
    public string EmployeeId { get; set; }
    public decimal Salary { get; set; }
    public string Department { get; set; }
    
    public Employee(string firstName, string lastName, DateTime birthDate, 
                   string employeeId, decimal salary, string department) 
        : base(firstName, lastName, birthDate) 
    {
        EmployeeId = employeeId;
        Salary = salary;
        Department = department;
    }
    
    // Override virtual method
    public override void Work() 
    {
        Console.WriteLine($"{FullName} is working in {Department} department.");
    }
    
    // New method specific to Employee
    public void GetPaid() 
    {
        Console.WriteLine($"{FullName} received salary: ${Salary:N2}");
    }
}

// Usage example
class ClassDemo 
{
    public static void Main() 
    {
        // Creating objects
        var person = new Person("Rijoan", "Mahmud", new DateTime(1990, 5, 15));
        var employee = new Employee("Khairul", "Islam", new DateTime(1985, 3, 22), 
                                   "EMP001", 75000m, "IT");
        
        // Using objects
        person.Introduce();
        employee.Introduce();
        
        // Polymorphism
        Person worker = employee;  // Employee IS-A Person
        worker.Work();  // Calls Employee's overridden Work method
        
        // Static member access
        Console.WriteLine($"Total persons created: {Person.TotalPersons}");
    }
}
```

### Array (Collection of Elements)

**Definition**: An array is a reference type that represents a collection of elements of the same type stored in contiguous memory locations. Arrays provide indexed access to elements and have a fixed size once created.

**Characteristics**:
- **Fixed Size**: Cannot be resized after creation
- **Type Safety**: All elements must be of the same type
- **Zero-Based Indexing**: First element is at index 0
- **Reference Type**: Array variable stores reference to heap memory
- **Automatic Initialization**: Elements initialized to default values

**Types of Arrays**:
1. **Single-Dimensional Arrays**: Linear sequence of elements
2. **Multidimensional Arrays**: Rectangular arrays (2D, 3D, etc.)
3. **Jagged Arrays**: Arrays of arrays (irregular)

```csharp
// Single-dimensional array examples
class ArrayDemo 
{
    public static void Main() 
    {
        // Array declaration and initialization
        int[] numbers = new int[5];                    // Default values: [0,0,0,0,0]
        string[] names = new string[3];                // Default values: [null,null,null]
        
        // Array initialization with values
        int[] scores = { 85, 92, 78, 96, 88 };         // Array literal
        string[] colors = new string[] { "Red", "Green", "Blue" };
        
        // Alternative initialization syntax
        int[] grades = new int[4] { 90, 85, 88, 92 };
        
        // Accessing elements
        Console.WriteLine($"First score: {scores[0]}");     // 85
        Console.WriteLine($"Last score: {scores[4]}");      // 88
        
        // Modifying elements
        scores[0] = 95;
        Console.WriteLine($"Updated first score: {scores[0]}"); // 95
        
        // Array properties
        Console.WriteLine($"Array length: {scores.Length}");    // 5
        Console.WriteLine($"Array rank: {scores.Rank}");        // 1 (single-dimensional)
        
        // Iterating with for loop
        Console.WriteLine("Scores:");
        for (int i = 0; i < scores.Length; i++) 
        {
            Console.WriteLine($"scores[{i}] = {scores[i]}");
        }
        
        // Iterating with foreach loop
        Console.WriteLine("Colors:");
        foreach (string color in colors) 
        {
            Console.WriteLine($"Color: {color}");
        }
        
        // Array methods (from System.Array)
        Array.Sort(scores);                             // Sort in ascending order
        Console.WriteLine($"Sorted scores: [{string.Join(", ", scores)}]");
        
        Array.Reverse(scores);                          // Reverse order
        Console.WriteLine($"Reversed: [{string.Join(", ", scores)}]");
        
        int index = Array.IndexOf(scores, 92);          // Find index of value
        Console.WriteLine($"Index of 92: {index}");
        
        // Multidimensional array (rectangular)
        int[,] matrix = new int[3, 3] 
        {
            { 1, 2, 3 },
            { 4, 5, 6 },
            { 7, 8, 9 }
        };
        
        Console.WriteLine($"Matrix element [1,2]: {matrix[1, 2]}"); // 6
        Console.WriteLine($"Matrix dimensions: {matrix.GetLength(0)} x {matrix.GetLength(1)}");
        
        // Iterating through 2D array
        Console.WriteLine("Matrix:");
        for (int row = 0; row < matrix.GetLength(0); row++) 
        {
            for (int col = 0; col < matrix.GetLength(1); col++) 
            {
                Console.Write($"{matrix[row, col]} ");
            }
            Console.WriteLine();
        }
        
        // Jagged array (array of arrays)
        int[][] jaggedArray = new int[3][];
        jaggedArray[0] = new int[4] { 1, 2, 3, 4 };     // 4 elements
        jaggedArray[1] = new int[2] { 5, 6 };           // 2 elements
        jaggedArray[2] = new int[3] { 7, 8, 9 };        // 3 elements
        
        Console.WriteLine("Jagged Array:");
        for (int i = 0; i < jaggedArray.Length; i++) 
        {
            Console.Write($"Row {i}: ");
            for (int j = 0; j < jaggedArray[i].Length; j++) 
            {
                Console.Write($"{jaggedArray[i][j]} ");
            }
            Console.WriteLine();
        }
    }
}
```

### String (Immutable Character Sequence)

**Definition**: String is a reference type that represents a sequence of Unicode characters. In C#, strings are immutable, meaning once created, their content cannot be changed. Any operation that appears to modify a string actually creates a new string object.

**Key Characteristics**:
- **Immutable**: Cannot be modified after creation
- **Reference Type**: Stored on the heap
- **Unicode Support**: Full Unicode character support
- **String Interning**: Identical string literals share memory
- **Null Terminated**: Internally null-terminated for C interop

```csharp
class StringDemo 
{
    public static void Main() 
    {
        // String creation
        string name = "Rijoan Mahmud";                       // String literal
        string message = new string('A', 5);            // "AAAAA"
        string empty = string.Empty;                    // Empty string
        string nullString = null;                       // Null reference
        
        // String properties
        Console.WriteLine($"Length: {name.Length}");         // 8
        Console.WriteLine($"Is empty: {string.IsNullOrEmpty(empty)}"); // True
        Console.WriteLine($"Is null or whitespace: {string.IsNullOrWhiteSpace("   ")}"); // True
        
        // String indexing and character access
        Console.WriteLine($"First character: {name[0]}");    // 'J'
        Console.WriteLine($"Last character: {name[name.Length - 1]}"); // 'e'
        
        // String methods (return new strings due to immutability)
        string upperCase = name.ToUpper();              // "RIJOAN MAHMUD"
        string lowerCase = name.ToLower();              // "rijoan mahmud"
        string trimmed = "  Hello World  ".Trim();      // "Hello World"
        string replaced = name.Replace("Rijoan", "Khairul"); // "Khairul Mahmud"
        string substring = name.Substring(0, 6);        // "Rijoan"
        
        Console.WriteLine($"Original: {name}");         // Original unchanged
        Console.WriteLine($"Upper: {upperCase}");
        
        // String comparison
        string str1 = "Hello";
        string str2 = "hello";
        string str3 = "Hello";
        
        Console.WriteLine($"str1 == str3: {str1 == str3}");                    // True
        Console.WriteLine($"str1 == str2: {str1 == str2}");                    // False (case sensitive)
        Console.WriteLine($"Ignore case: {str1.Equals(str2, StringComparison.OrdinalIgnoreCase)}"); // True
        
        // String concatenation
        string firstName = "Rijoan";
        string lastName = "Mahmud";
        string fullName1 = firstName + " " + lastName;           // Simple concatenation
        string fullName2 = string.Concat(firstName, " ", lastName); // Using Concat method
        string fullName3 = $"{firstName} {lastName}";            // String interpolation (preferred)
        string fullName4 = string.Format("{0} {1}", firstName, lastName); // Format method
        
        // String splitting and joining
        string csv = "apple,banana,orange,grape";
        string[] fruits = csv.Split(',');                       // Split into array
        string rejoined = string.Join(" | ", fruits);          // Join with separator
        Console.WriteLine($"Fruits: {rejoined}");              // "apple | banana | orange | grape"
        
        // String searching
        string text = "The quick brown fox jumps over the lazy dog";
        bool contains = text.Contains("fox");                   // True
        int index = text.IndexOf("fox");                        // 16
        int lastIndex = text.LastIndexOf("the");               // 31
        bool startsWith = text.StartsWith("The");              // True
        bool endsWith = text.EndsWith("dog");                  // True
        
        // StringBuilder for multiple string operations (mutable)
        var sb = new System.Text.StringBuilder();
        sb.Append("Hello");
        sb.Append(" ");
        sb.Append("World");
        sb.AppendLine("!");
        sb.Insert(6, "Beautiful ");
        string result = sb.ToString();                          // "Hello Beautiful World!\n"
        Console.WriteLine($"StringBuilder result: {result}");
        
        // String interpolation with formatting
        double price = 19.99;
        int quantity = 3;
        string receipt = $"Items: {quantity}, Total: {price * quantity:C}";
        Console.WriteLine(receipt);                             // "Items: 3, Total: $59.97"
        
        // Verbatim strings
        string path = @"C:\Users\Rijoan\Documents\file.txt";      // No need to escape backslashes
        string multiline = @"Line 1
Line 2
Line 3";
        
        // Raw string literals (C# 11+)
        string json = """
        {
            "name": "Rijoan",
            "age": 30,
            "city": "New York"
        }
        """;
    }
}
```


## Constants - const vs readonly

### Definition
Constants are values that cannot be changed during program execution. C# provides two ways to create constants: `const` and `readonly`, each with different characteristics and use cases.

### const Keyword

**Definition**: `const` creates compile-time constants that are replaced with their actual values during compilation.

**Characteristics**:
- **Compile-time**: Value must be known at compile time
- **Immutable**: Cannot be changed after declaration
- **Static**: Implicitly static, accessed through type name
- **Types**: Limited to compile-time constants (primitives, null, string literals)
- **Performance**: No memory allocation at runtime (inlined)
- **Scope**: Can be declared at class or local level

```csharp
public class ConstantsExample 
{
    // Compile-time constants
    public const double PI = 3.14159265359;
    public const string APPLICATION_NAME = "MyApp";
    public const int MAX_USERS = 1000;
    public const bool DEBUG_MODE = true;
    
    // const with expressions (must be compile-time evaluable)
    public const int SECONDS_IN_HOUR = 60 * 60;  // 3600
    public const string VERSION = "1.0.0";
    
    public void DemonstrateConst() 
    {
        // Local constants
        const int localConst = 42;
        const string greeting = "Hello";
        
        // Usage - no instance needed for class-level constants
        Console.WriteLine($"PI value: {PI}");
        Console.WriteLine($"App: {APPLICATION_NAME}");
        Console.WriteLine($"Local: {localConst}");
    }
}

// Usage
Console.WriteLine(ConstantsExample.PI);  // Access without creating instance
```

### readonly Keyword

**Definition**: `readonly` creates runtime constants that can be initialized either at declaration or in constructors, but cannot be modified afterward.

**Characteristics**:
- **Runtime**: Value determined at runtime
- **Initialization**: At declaration or in constructor only
- **Instance/Static**: Can be instance-level or static
- **Types**: Any type allowed
- **Memory**: Actual memory allocation (not inlined)
- **Flexibility**: Can have different values for different instances

```csharp
public class ReadonlyExample 
{
    // Static readonly - shared among all instances
    public static readonly DateTime ApplicationStartTime = DateTime.Now;
    public static readonly string[] SupportedFormats = { "JSON", "XML", "CSV" };
    
    // Instance readonly - can have different values per instance
    public readonly string InstanceId;
    public readonly DateTime CreationTime;
    public readonly int ProcessId;
    
    // readonly field that can be set in constructor
    private readonly ILogger _logger;
    
    // Constructor - can initialize readonly fields
    public ReadonlyExample(ILogger logger) 
    {
        InstanceId = Guid.NewGuid().ToString();
        CreationTime = DateTime.Now;
        ProcessId = Environment.ProcessId;
        _logger = logger ?? throw new ArgumentNullException(nameof(logger));
    }
    
    // Static constructor - can initialize static readonly fields
    static ReadonlyExample() 
    {
        // Additional initialization if needed
        Console.WriteLine($"Static constructor called at {ApplicationStartTime}");
    }
    
    public void ShowValues() 
    {
        Console.WriteLine($"Instance ID: {InstanceId}");
        Console.WriteLine($"Created: {CreationTime}");
        Console.WriteLine($"Process: {ProcessId}");
        Console.WriteLine($"App started: {ApplicationStartTime}");
    }
}

// Usage
var example1 = new ReadonlyExample(new ConsoleLogger());
var example2 = new ReadonlyExample(new FileLogger());
// Each instance has different readonly values
```

### Comparison and Best Practices

```csharp
public class ConstVsReadonlyComparison 
{
    // Use const for true constants that will never change
    public const string COMPANY_NAME = "TechCorp";          // Good: Never changes
    public const double GRAVITY = 9.81;                    // Good: Physical constant
    
    // Use readonly for values that are constant per instance/execution
    public readonly DateTime StartupTime = DateTime.Now;    // Good: Varies per run
    public static readonly Version AppVersion = new Version(1, 0, 0); // Good: Complex type
    
    // DON'T do this with const (will cause issues if changed later)
    // public const string API_URL = "https://api.example.com"; // Bad: Might change
    
    // DO use readonly for configuration values
    public static readonly string ApiUrl = ConfigurationManager.AppSettings["ApiUrl"];
    
    // Performance comparison
    public void PerformanceDemo() 
    {
        // const - inlined, no memory access
        double area1 = PI * 5 * 5;  // Becomes: 3.14159... * 5 * 5
        
        // readonly - memory access required
        double area2 = ReadonlyPI * 5 * 5;  // Memory lookup for ReadonlyPI
    }
    
    public const double PI = 3.14159;
    public static readonly double ReadonlyPI = 3.14159;
}
```

| Aspect          | const                    | readonly                |
|-----------------|--------------------------|-------------------------|
| Initialization  | At declaration only      | Declaration or constructor |
| Compile/Runtime | Compile-time constant    | Runtime constant        |
| Memory          | No allocation (inlined)  | Memory allocation       |
| Types           | Primitives, string, null | Any type                |
| Scope           | Implicitly static        | Instance or static      |
| Performance     | Faster (inlined)         | Slightly slower         |
| Flexibility     | Less flexible            | More flexible           |
| Use case        | True constants           | Per-instance constants  |



## Properties

### Definition
Properties are members that provide a flexible mechanism to read, write, or compute values of private fields. They act like public fields but are actually special methods called accessors (getters and setters).

**Benefits of Properties**:
- **Encapsulation**: Control access to internal data
- **Validation**: Validate data before setting
- **Computed Values**: Calculate values on-the-fly
- **Lazy Loading**: Load data only when needed
- **Change Notification**: Notify when values change
- **Backwards Compatibility**: Can change implementation without breaking code

### Types of Properties

```csharp
public class PropertyExamples 
{
    // Private fields (backing fields)
    private string _name;
    private int _age;
    private decimal _salary;
    private DateTime _birthDate;
    
    // 1. Traditional Property with Backing Field
    public string Name 
    {
        get 
        { 
            Console.WriteLine("Getting name");
            return _name; 
        }
        set 
        { 
            Console.WriteLine($"Setting name to: {value}");
            if (string.IsNullOrWhiteSpace(value))
                throw new ArgumentException("Name cannot be empty");
            _name = value.Trim();
        }
    }
    
    // 2. Auto-Implemented Property (compiler creates backing field)
    public string Email { get; set; }  // Full access
    public string Phone { get; private set; }  // Public get, private set
    
    // 3. Read-Only Property (get only)
    public string FullName => $"{FirstName} {LastName}";  // Expression-bodied
    
    // Traditional read-only property
    public int Age 
    {
        get 
        {
            var today = DateTime.Today;
            var age = today.Year - _birthDate.Year;
            if (_birthDate.Date > today.AddYears(-age)) age--;
            return age;
        }
    }
    
    // 4. Write-Only Property (rare, set only)
    public string Password 
    {
        set 
        {
            if (value?.Length < 8)
                throw new ArgumentException("Password must be at least 8 characters");
            // Hash and store password
            _hashedPassword = HashPassword(value);
        }
    }
    private string _hashedPassword;
    
    // 5. Property with Validation and Business Logic
    public decimal Salary 
    {
        get => _salary;
        set 
        {
            if (value < 0)
                throw new ArgumentException("Salary cannot be negative");
            if (value > 1_000_000)
                throw new ArgumentException("Salary exceeds maximum allowed");
            
            var oldSalary = _salary;
            _salary = value;
            
            // Raise event when salary changes
            OnSalaryChanged(oldSalary, value);
        }
    }
    
    // 6. Computed Property (no backing field)
    public string TaxBracket 
    {
        get 
        {
            return _salary switch 
            {
                < 50000 => "Low",
                < 100000 => "Medium",
                < 200000 => "High",
                _ => "Very High"
            };
        }
    }
    
    // 7. Lazy-Loaded Property
    private List<string> _projects;
    public List<string> Projects 
    {
        get 
        {
            if (_projects == null) 
            {
                Console.WriteLine("Loading projects from database...");
                _projects = LoadProjectsFromDatabase();
            }
            return _projects;
        }
    }
    
    // 8. Property with Different Access Levels
    public DateTime LastLoginTime { get; protected set; }  // Protected setter
    
    // 9. Static Property
    public static int TotalEmployees { get; private set; }
    
    // 10. Init-Only Property (C# 9.0+) - can only be set during initialization
    public string EmployeeId { get; init; }
    
    // 11. Required Property (C# 11+) - must be set during initialization
    public required string FirstName { get; set; }
    public required string LastName { get; set; }
    
    // Constructor
    public PropertyExamples() 
    {
        TotalEmployees++;
        LastLoginTime = DateTime.Now;
    }
    
    // Event for property change notification
    public event Action<decimal, decimal> SalaryChanged;
    
    protected virtual void OnSalaryChanged(decimal oldValue, decimal newValue) 
    {
        SalaryChanged?.Invoke(oldValue, newValue);
    }
    
    private List<string> LoadProjectsFromDatabase() 
    {
        // Simulate database call
        Thread.Sleep(100);
        return new List<string> { "Project A", "Project B", "Project C" };
    }
    
    private string HashPassword(string password) 
    {
        // Simulate password hashing
        return Convert.ToBase64String(System.Text.Encoding.UTF8.GetBytes(password));
    }
}

// Usage examples
class PropertyDemo 
{
    public static void Main() 
    {
        // Using properties
        var employee = new PropertyExamples 
        {
            FirstName = "Rijoan",      // Required property
            LastName = "Mahmud",        // Required property
            EmployeeId = "EMP001",   // Init-only property
            Email = "rijoan.mahmud@company.com"
        };
        
        // Property access
        employee.Name = "Rijoan Mahmud";  // Calls setter with validation
        Console.WriteLine(employee.Name);  // Calls getter
        
        // Computed properties
        Console.WriteLine($"Full Name: {employee.FullName}");
        
        // Property with business logic
        employee.SalaryChanged += (old, newVal) => 
            Console.WriteLine($"Salary changed from {old:C} to {newVal:C}");
        
        employee.Salary = 75000;  // Triggers validation and event
        Console.WriteLine($"Tax Bracket: {employee.TaxBracket}");
        
        // Lazy loading
        Console.WriteLine("Accessing projects for first time:");
        var projects = employee.Projects;  // Loads from "database"
        Console.WriteLine("Accessing projects again:");
        projects = employee.Projects;      // Returns cached value
        
        // Auto-implemented properties
        employee.Email = "rijoan.mahmud@newcompany.com";
        Console.WriteLine($"Email: {employee.Email}");
        
        // Static property
        Console.WriteLine($"Total employees: {PropertyExamples.TotalEmployees}");
    }
}
```
## Control Structures

### Definition
Control structures are programming constructs that control the flow of execution in a program. They determine which statements are executed, how many times, and under what conditions.

### Types of Control Structures:
1. **Sequential**: Statements executed in order (default)
2. **Selection**: Choose between alternatives (if-else, switch)
3. **Iteration**: Repeat statements (loops)
4. **Jump**: Transfer control to another part of program (break, continue, return)

## Conditional Statements

### if-else Statement

**Definition**: The if-else statement allows conditional execution of code blocks based on boolean expressions. It enables decision-making in programs.

**Syntax Variations**:
- Simple if
- if-else
- if-else if-else (nested conditions)
- Ternary operator (conditional operator)

```csharp
class ConditionalDemo 
{
    public static void Main() 
    {
        // Simple if statement
        int temperature = 25;
        if (temperature > 20) 
        {
            Console.WriteLine("It's a warm day!");
        }
        
        // if-else statement
        int age = 17;
        if (age >= 18) 
        {
            Console.WriteLine("You can vote!");
        } 
        else 
        {
            Console.WriteLine("You cannot vote yet.");
        }
        
        // if-else if-else chain
        int score = 85;
        string grade;
        
        if (score >= 90) 
        {
            grade = "A";
        } 
        else if (score >= 80) 
        {
            grade = "B";
        } 
        else if (score >= 70) 
        {
            grade = "C";
        } 
        else if (score >= 60) 
        {
            grade = "D";
        } 
        else 
        {
            grade = "F";
        }
        
        Console.WriteLine($"Your grade is: {grade}");
        
        // Nested if statements
        bool isWeekend = true;
        bool isRaining = false;
        
        if (isWeekend) 
        {
            if (!isRaining) 
            {
                Console.WriteLine("Great day for outdoor activities!");
            } 
            else 
            {
                Console.WriteLine("Perfect day to stay inside and read.");
            }
        } 
        else 
        {
            Console.WriteLine("Time to work!");
        }
        
        // Ternary operator (conditional operator)
        string message = (age >= 18) ? "Adult" : "Minor";
        Console.WriteLine($"Status: {message}");
        
        // Complex boolean expressions
        int hour = DateTime.Now.Hour;
        bool isBusinessHours = (hour >= 9 && hour <= 17);
        bool isWeekday = (DateTime.Now.DayOfWeek != DayOfWeek.Saturday && 
                         DateTime.Now.DayOfWeek != DayOfWeek.Sunday);
        
        if (isBusinessHours && isWeekday) 
        {
            Console.WriteLine("Office is open");
        } 
        else 
        {
            Console.WriteLine("Office is closed");
        }
        
        // Null checking
        string name = null;
        if (name != null && name.Length > 0) 
        {
            Console.WriteLine($"Hello, {name}!");
        } 
        else 
        {
            Console.WriteLine("Name is not provided");
        }
        
        // Using null-conditional operator (safer)
        if (!string.IsNullOrEmpty(name)) 
        {
            Console.WriteLine($"Hello, {name}!");
        }
    }
}
```

### switch Statement and Expression

**Definition**: The switch statement provides a multi-way branch based on the value of an expression. It's often more readable than multiple if-else statements when checking a single variable against many values.

**Traditional Switch Statement**:
- Uses case labels
- Requires break statements
- Supports fall-through behavior
- Limited pattern matching

**Switch Expression (C# 8.0+)**:
- More concise syntax
- Expression-based (returns a value)
- No break statements needed
- Enhanced pattern matching

```csharp
class SwitchDemo 
{
    public static void Main() 
    {
        // Traditional switch statement
        DayOfWeek today = DateTime.Now.DayOfWeek;
        
        switch (today) 
        {
            case DayOfWeek.Monday:
                Console.WriteLine("Start of the work week");
                break;
            case DayOfWeek.Tuesday:
            case DayOfWeek.Wednesday:
            case DayOfWeek.Thursday:
                Console.WriteLine("Midweek grind");
                break;
            case DayOfWeek.Friday:
                Console.WriteLine("TGIF!");
                break;
            case DayOfWeek.Saturday:
            case DayOfWeek.Sunday:
                Console.WriteLine("Weekend relaxation");
                break;
            default:
                Console.WriteLine("Unknown day");
                break;
        }
        
        // Switch expression (C# 8.0+)
        string dayType = today switch 
        {
            DayOfWeek.Monday => "Manic Monday",
            DayOfWeek.Tuesday or DayOfWeek.Wednesday or DayOfWeek.Thursday => "Midweek",
            DayOfWeek.Friday => "Thank God It's Friday",
            DayOfWeek.Saturday or DayOfWeek.Sunday => "Weekend",
            _ => "Unknown day"  // Default case
        };
        
        Console.WriteLine($"Day type: {dayType}");
        
        // Switch with different types
        object value = 42;
        string result = value switch 
        {
            int i when i > 0 => $"Positive integer: {i}",
            int i when i < 0 => $"Negative integer: {i}",
            int i when i == 0 => "Zero",
            string s when !string.IsNullOrEmpty(s) => $"Non-empty string: {s}",
            string s => "Empty or null string",
            bool b => $"Boolean: {b}",
            null => "Null value",
            _ => $"Unknown type: {value.GetType().Name}"
        };
        
        Console.WriteLine(result);
        
        // Switch with tuples (pattern matching)
        var point = (X: 0, Y: 0);
        string location = point switch 
        {
            (0, 0) => "Origin",
            (0, _) => "On Y-axis",
            (_, 0) => "On X-axis",
            (_, _) when point.X == point.Y => "On diagonal",
            (_, _) => "Somewhere in the plane"
        };
        
        Console.WriteLine($"Point location: {location}");
        
        // Method using switch expression for calculations
        double CalculateArea(string shape, double dimension1, double dimension2 = 0) 
        {
            return shape.ToLower() switch 
            {
                "circle" => Math.PI * dimension1 * dimension1,
                "square" => dimension1 * dimension1,
                "rectangle" => dimension1 * dimension2,
                "triangle" => 0.5 * dimension1 * dimension2,
                _ => throw new ArgumentException($"Unknown shape: {shape}")
            };
        }
        
        // Usage of calculation method
        try 
        {
            Console.WriteLine($"Circle area: {CalculateArea("circle", 5):F2}");
            Console.WriteLine($"Rectangle area: {CalculateArea("rectangle", 4, 6):F2}");
        } 
        catch (ArgumentException ex) 
        {
            Console.WriteLine($"Error: {ex.Message}");
        }
        
        // Switch with when guards
        int ProcessNumber(int number) 
        {
            return number switch 
            {
                int n when n < 0 => Math.Abs(n),           // Make positive
                int n when n == 0 => 1,                    // Zero becomes one
                int n when n > 100 => 100,                 // Cap at 100
                int n when n % 2 == 0 => n / 2,           // Halve even numbers
                int n => n * 2                            // Double odd numbers
            };
        }
        
        int[] testNumbers = { -5, 0, 25, 50, 150, 7 };
        foreach (int num in testNumbers) 
        {
            Console.WriteLine($"{num} -> {ProcessNumber(num)}");
        }
    }
}
```

## Loops

### Definition
Loops are control structures that allow repeated execution of a block of code. They are essential for automating repetitive tasks and processing collections of data.

### Types of Loops:
1. **for**: When you know the exact number of iterations
2. **while**: When you have a condition to check before each iteration
3. **do-while**: When you need at least one execution, then check condition
4. **foreach**: When iterating over collections or arrays

### for Loop

**Definition**: The for loop is used when you know in advance how many times you want to execute a statement or block of statements. It's particularly useful for counting and array/collection processing.

**Components**:
1. **Initialization**: Executed once at the beginning
2. **Condition**: Checked before each iteration
3. **Update**: Executed after each iteration

```csharp
class ForLoopDemo 
{
    public static void Main() 
    {
        // Basic for loop
        Console.WriteLine("Counting from 1 to 5:");
        for (int i = 1; i <= 5; i++) 
        {
            Console.WriteLine($"Count: {i}");
        }
        
        // Counting backwards
        Console.WriteLine("\nCountdown:");
        for (int i = 10; i >= 1; i--) 
        {
            Console.WriteLine($"T-minus {i}");
        }
        Console.WriteLine("Blast off!");
        
        // Different increment values
        Console.WriteLine("\nEven numbers from 0 to 20:");
        for (int i = 0; i <= 20; i += 2) 
        {
            Console.WriteLine(i);
        }
        
        // Multiple variables in for loop
        Console.WriteLine("\nMultiple variables:");
        for (int i = 0, j = 10; i < 5; i++, j--) 
        {
            Console.WriteLine($"i: {i}, j: {j}");
        }
        
        // Nested for loops (multiplication table)
        Console.WriteLine("\nMultiplication Table (1-5):");
        for (int i = 1; i <= 5; i++) 
        {
            for (int j = 1; j <= 5; j++) 
            {
                Console.Write($"{i * j:D2} ");
            }
            Console.WriteLine();  // New line after each row
        }
        
        // For loop with arrays
        string[] fruits = { "Apple", "Banana", "Orange", "Grape", "Mango" };
        Console.WriteLine("\nFruits with index:");
        for (int i = 0; i < fruits.Length; i++) 
        {
            Console.WriteLine($"[{i}] {fruits[i]}");
        }
        
        // For loop with complex conditions
        Console.WriteLine("\nFibonacci sequence (first 10 numbers):");
        int a = 0, b = 1;
        for (int i = 0; i < 10; i++) 
        {
            Console.Write($"{a} ");
            int temp = a + b;
            a = b;
            b = temp;
        }
        Console.WriteLine();
        
        // Infinite for loop (be careful!)
        // for (;;) { /* This runs forever unless broken */ }
        
        // For loop with early termination
        Console.WriteLine("\nSearching for number 7:");
        int[] numbers = { 1, 3, 5, 7, 9, 11, 13 };
        for (int i = 0; i < numbers.Length; i++) 
        {
            if (numbers[i] == 7) 
            {
                Console.WriteLine($"Found 7 at index {i}");
                break;  // Exit loop early
            }
            Console.WriteLine($"Checking index {i}: {numbers[i]}");
        }
    }
}
```

### while Loop

**Definition**: The while loop executes a block of code repeatedly as long as a specified condition remains true. The condition is checked before each iteration, so the loop body may not execute at all if the condition is initially false.

**Use Cases**:
- Unknown number of iterations
- Condition-dependent repetition
- Reading data until end-of-file
- User input validation
- Processing until a specific state is reached

```csharp
class WhileLoopDemo 
{
    public static void Main() 
    {
        // Basic while loop
        int count = 1;
        Console.WriteLine("Basic while loop:");
        while (count <= 5) 
        {
            Console.WriteLine($"Iteration: {count}");
            count++;  // Important: modify the condition variable
        }
        
        // While loop with user input
        Console.WriteLine("\nGuessing game (guess the number 1-10):");
        Random random = new Random();
        int secretNumber = random.Next(1, 11);
        int guess = 0;
        int attempts = 0;
        
        while (guess != secretNumber) 
        {
            Console.Write("Enter your guess: ");
            string input = Console.ReadLine();
            
            if (int.TryParse(input, out guess)) 
            {
                attempts++;
                if (guess < secretNumber) 
                {
                    Console.WriteLine("Too low!");
                } 
                else if (guess > secretNumber) 
                {
                    Console.WriteLine("Too high!");
                } 
                else 
                {
                    Console.WriteLine($"Correct! You guessed it in {attempts} attempts.");
                }
            } 
            else 
            {
                Console.WriteLine("Please enter a valid number.");
            }
        }
        
        // While loop for data processing
        Console.WriteLine("\nProcessing array until negative number:");
        int[] data = { 5, 10, 15, 20, -1, 25, 30 };
        int index = 0;
        int sum = 0;
        
        while (index < data.Length && data[index] >= 0) 
        {
            sum += data[index];
            Console.WriteLine($"Added {data[index]}, running sum: {sum}");
            index++;
        }
        
        Console.WriteLine($"Final sum before negative number: {sum}");
        
        // While loop with complex condition
        Console.WriteLine("\nSimulating a simple ATM withdrawal:");
        decimal balance = 1000m;
        bool continueBanking = true;
        
        while (continueBanking && balance > 0) 
        {
            Console.WriteLine($"Current balance: ${balance:F2}");
            Console.Write("Enter withdrawal amount (0 to quit): $");
            
            if (decimal.TryParse(Console.ReadLine(), out decimal withdrawal)) 
            {
                if (withdrawal == 0) 
                {
                    continueBanking = false;
                } 
                else if (withdrawal > balance) 
                {
                    Console.WriteLine("Insufficient funds!");
                } 
                else if (withdrawal < 0) 
                {
                    Console.WriteLine("Invalid amount!");
                } 
                else 
                {
                    balance -= withdrawal;
                    Console.WriteLine($"Withdrew ${withdrawal:F2}");
                }
            } 
            else 
            {
                Console.WriteLine("Invalid input!");
            }
            
            Console.WriteLine();  // Empty line for readability
        }
        
        Console.WriteLine("Thank you for banking with us!");
        
        // Potential infinite loop warning
        // while (true) 
        // {
        //     // This runs forever unless you use break or return
        //     // Always ensure there's a way to exit!
        // }
    }
}
```

### do-while Loop

**Definition**: The do-while loop is similar to the while loop, but it checks the condition after executing the loop body. This guarantees that the loop body executes at least once, regardless of the condition.

**Key Difference**: 
- **while**: Check condition, then execute (0 or more times)
- **do-while**: Execute, then check condition (1 or more times)

```csharp
class DoWhileLoopDemo 
{
    public static void Main() 
    {
        // Basic do-while loop
        int number = 1;
        Console.WriteLine("Basic do-while loop:");
        do 
        {
            Console.WriteLine($"Number: {number}");
            number++;
        } 
        while (number <= 3);
        
        // Menu-driven program (classic do-while use case)
        int choice;
        do 
        {
            Console.WriteLine("\n=== CALCULATOR MENU ===");
            Console.WriteLine("1. Addition");
            Console.WriteLine("2. Subtraction");
            Console.WriteLine("3. Multiplication");
            Console.WriteLine("4. Division");
            Console.WriteLine("0. Exit");
            Console.Write("Enter your choice: ");
            
            if (int.TryParse(Console.ReadLine(), out choice)) 
            {
                switch (choice) 
                {
                    case 1:
                        PerformAddition();
                        break;
                    case 2:
                        PerformSubtraction();
                        break;
                    case 3:
                        PerformMultiplication();
                        break;
                    case 4:
                        PerformDivision();
                        break;
                    case 0:
                        Console.WriteLine("Goodbye!");
                        break;
                    default:
                        Console.WriteLine("Invalid choice! Please try again.");
                        break;
                }
            } 
            else 
            {
                Console.WriteLine("Please enter a valid number.");
                choice = -1;  // Force continue
            }
        } 
        while (choice != 0);
        
        // Input validation with do-while
        int validatedAge;
        do 
        {
            Console.Write("Enter your age (1-120): ");
            string input = Console.ReadLine();
            
            if (!int.TryParse(input, out validatedAge)) 
            {
                Console.WriteLine("Please enter a valid number.");
            } 
            else if (validatedAge < 1 || validatedAge > 120) 
            {
                Console.WriteLine("Age must be between 1 and 120.");
                validatedAge = 0;  // Force invalid to continue loop
            }
        } 
        while (validatedAge < 1 || validatedAge > 120);
        
        Console.WriteLine($"Thank you! Your age is {validatedAge}.");
        
        // Random number generation until condition met
        Console.WriteLine("\nGenerating random numbers until we get one > 90:");
        Random random = new Random();
        int randomNum;
        int attempts = 0;
        
        do 
        {
            randomNum = random.Next(1, 101);  // 1-100
            attempts++;
            Console.WriteLine($"Attempt {attempts}: Generated {randomNum}");
        } 
        while (randomNum <= 90);
        
        Console.WriteLine($"Success! Got {randomNum} after {attempts} attempts.");
    }
    
    // Helper methods for calculator
    static void PerformAddition() 
    {
        Console.Write("Enter first number: ");
        if (double.TryParse(Console.ReadLine(), out double num1)) 
        {
            Console.Write("Enter second number: ");
            if (double.TryParse(Console.ReadLine(), out double num2)) 
            {
                Console.WriteLine($"Result: {num1} + {num2} = {num1 + num2}");
            }
        }
    }
    
    static void PerformSubtraction() 
    {
        Console.Write("Enter first number: ");
        if (double.TryParse(Console.ReadLine(), out double num1)) 
        {
            Console.Write("Enter second number: ");
            if (double.TryParse(Console.ReadLine(), out double num2)) 
            {
                Console.WriteLine($"Result: {num1} - {num2} = {num1 - num2}");
            }
        }
    }
    
    static void PerformMultiplication() 
    {
        Console.Write("Enter first number: ");
        if (double.TryParse(Console.ReadLine(), out double num1)) 
        {
            Console.Write("Enter second number: ");
            if (double.TryParse(Console.ReadLine(), out double num2)) 
            {
                Console.WriteLine($"Result: {num1} × {num2} = {num1 * num2}");
            }
        }
    }
    
    static void PerformDivision() 
    {
        Console.Write("Enter first number: ");
        if (double.TryParse(Console.ReadLine(), out double num1)) 
        {
            Console.Write("Enter second number: ");
            if (double.TryParse(Console.ReadLine(), out double num2)) 
            {
                if (num2 != 0) 
                {
                    Console.WriteLine($"Result: {num1} ÷ {num2} = {num1 / num2}");
                } 
                else 
                {
                    Console.WriteLine("Error: Division by zero!");
                }
            }
        }
    }
}
```

### foreach Loop

**Definition**: The foreach loop is used to iterate over collections, arrays, and any object that implements IEnumerable. It provides a clean, readable way to access each element in a collection without dealing with indices or iterators.

**Advantages**:
- **Simplicity**: No need to manage indices
- **Safety**: No risk of index out-of-bounds errors
- **Readability**: Intent is clear
- **Performance**: Often optimized by compiler
- **Type Safety**: Automatic type inference

```csharp
class ForeachLoopDemo 
{
    public static void Main() 
    {
        // Basic foreach with array
        string[] fruits = { "Apple", "Banana", "Orange", "Grape", "Mango" };
        
        Console.WriteLine("Fruits in the basket:");
        foreach (string fruit in fruits) 
        {
            Console.WriteLine($"- {fruit}");
        }
        
        // Foreach with var keyword (type inference)
        var numbers = new int[] { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 };
        
        Console.WriteLine("\nEven numbers:");
        foreach (var number in numbers) 
        {
            if (number % 2 == 0) 
            {
                Console.Write($"{number} ");
            }
        }
        Console.WriteLine();
        
        // Foreach with List<T>
        List<string> cities = new List<string> 
        {
            "New York", "London", "Tokyo", "Paris", "Sydney"
        };
        
        Console.WriteLine("\nWorld cities:");
        foreach (string city in cities) 
        {
            Console.WriteLine($"City: {city}");
        }
        
        // Foreach with Dictionary
        Dictionary<string, int> ageMap = new Dictionary<string, int> 
        {
            { "Rijoan", 25 },
            { "Khairul", 30 },
            { "Raisul", 35 },
            { "Saif", 28 }
        };
        
        Console.WriteLine("\nAge information:");
        foreach (KeyValuePair<string, int> person in ageMap) 
        {
            Console.WriteLine($"{person.Key} is {person.Value} years old");
        }
        
        // Simplified Dictionary iteration
        Console.WriteLine("\nSimplified dictionary iteration:");
        foreach (var person in ageMap) 
        {
            Console.WriteLine($"{person.Key}: {person.Value}");
        }
        
        // Foreach with 2D array
        int[,] matrix = 
        {
            { 1, 2, 3 },
            { 4, 5, 6 },
            { 7, 8, 9 }
        };
        
        Console.WriteLine("\nMatrix elements:");
        foreach (int element in matrix) 
        {
            Console.Write($"{element} ");
        }
        Console.WriteLine();
        
        // Foreach with jagged array
        int[][] jaggedArray = 
        {
            new int[] { 1, 2 },
            new int[] { 3, 4, 5 },
            new int[] { 6, 7, 8, 9 }
        };
        
        Console.WriteLine("\nJagged array:");
        foreach (int[] row in jaggedArray) 
        {
            Console.Write("Row: ");
            foreach (int element in row) 
            {
                Console.Write($"{element} ");
            }
            Console.WriteLine();
        }
        
        // Foreach with custom objects
        List<Employee> employees = new List<Employee> 
        {
            new Employee { Name = "Rijoan", Department = "IT", Salary = 75000 },
            new Employee { Name = "Khairul", Department = "HR", Salary = 65000 },
            new Employee { Name = "Mike", Department = "Finance", Salary = 80000 }
        };
        
        Console.WriteLine("\nEmployee information:");
        foreach (Employee emp in employees) 
        {
            Console.WriteLine($"{emp.Name} - {emp.Department} - ${emp.Salary:N0}");
        }
        
        // Foreach with LINQ-style operations
        Console.WriteLine("\nHigh-salary employees (>70K):");
        foreach (var emp in employees.Where(e => e.Salary > 70000)) 
        {
            Console.WriteLine($"{emp.Name}: ${emp.Salary:N0}");
        }
        
        // Foreach with string (string implements IEnumerable<char>)
        string message = "Hello, World!";
        Console.WriteLine("\nCharacter analysis:");
        foreach (char c in message) 
        {
            if (char.IsLetter(c)) 
            {
                Console.WriteLine($"'{c}' is a letter");
            } 
            else if (char.IsDigit(c)) 
            {
                Console.WriteLine($"'{c}' is a digit");
            } 
            else 
            {
                Console.WriteLine($"'{c}' is a special character");
            }
        }
        
        // Nested foreach loops
        Console.WriteLine("\nNested foreach - Departments and Employees:");
        var departments = new Dictionary<string, List<string>> 
        {
            { "IT", new List<string> { "Rijoan", "Khairul", "Raisul" } },
            { "HR", new List<string> { "Saif", "Zahin" } },
            { "Finance", new List<string> { "Maruf", "Karim", "Nasir" } }
        };
        
        foreach (var dept in departments) 
        {
            Console.WriteLine($"\n{dept.Key} Department:");
            foreach (string employee in dept.Value) 
            {
                Console.WriteLine($"  - {employee}");
            }
        }
    }
}
```

```csharp
// Helper class for employee example
class Employee 
{
    public string Name { get; set; }
    public string Department { get; set; }
    public decimal Salary { get; set; }
}
```
## Break and Continue Statements

### Definition
Break and continue are jump statements that alter the normal flow of loop execution. They provide fine-grained control over loop behavior and help optimize program logic.

### break Statement

**Definition**: The break statement immediately terminates the nearest enclosing loop or switch statement and transfers control to the statement following the terminated statement.

**Use Cases**:
- Exit a loop when a specific condition is met
- Early termination to improve performance
- Exit from infinite loops
- Break out of nested loops (only the innermost)

```csharp
class BreakStatementDemo 
{
    public static void Main() 
    {
        // Basic break in for loop
        Console.WriteLine("Finding first even number:");
        for (int i = 1; i <= 10; i++) 
        {
            if (i % 2 == 0) 
            {
                Console.WriteLine($"First even number found: {i}");
                break;  // Exit loop immediately
            }
            Console.WriteLine($"Checking: {i} (odd)");
        }
        
        // Break in while loop - search example
        Console.WriteLine("\nSearching in array:");
        int[] numbers = { 5, 12, 8, 3, 17, 9, 22 };
        int target = 17;
        int index = -1;
        int i = 0;
        
        while (i < numbers.Length) 
        {
            if (numbers[i] == target) 
            {
                index = i;
                break;  // Found it, no need to continue
            }
            i++;
        }
        
        if (index != -1) 
        {
            Console.WriteLine($"Found {target} at index {index}");
        } 
        else 
        {
            Console.WriteLine($"{target} not found");
        }
        
        // Break in nested loops (only breaks innermost loop)
        Console.WriteLine("\nBreak in nested loops:");
        for (int row = 1; row <= 3; row++) 
        {
            Console.WriteLine($"Row {row}:");
            for (int col = 1; col <= 5; col++) 
            {
                if (col == 3) 
                {
                    Console.WriteLine("  Breaking inner loop at col 3");
                    break;  // Only breaks inner loop
                }
                Console.WriteLine($"  Col {col}");
            }
            Console.WriteLine($"Finished row {row}\n");
        }
        
        // Using labeled break to break outer loop (using goto alternative)
        Console.WriteLine("Breaking out of nested loops completely:");
        bool found = false;
        for (int outer = 1; outer <= 3 && !found; outer++) 
        {
            for (int inner = 1; inner <= 3; inner++) 
            {
                Console.WriteLine($"Outer: {outer}, Inner: {inner}");
                if (outer == 2 && inner == 2) 
                {
                    Console.WriteLine("Target found! Exiting both loops.");
                    found = true;
                    break;
                }
            }
        }
        
        // Break in do-while loop
        Console.WriteLine("\nPassword validation with break:");
        int attempts = 0;
        string correctPassword = "secret123";
        
        do 
        {
            attempts++;
            Console.Write($"Attempt {attempts} - Enter password: ");
            string password = Console.ReadLine();
            
            if (password == correctPassword) 
            {
                Console.WriteLine("Access granted!");
                break;  // Exit the loop on success
            }
            
            if (attempts >= 3) 
            {
                Console.WriteLine("Too many failed attempts. Access denied!");
                break;  // Exit after 3 attempts
            }
            
            Console.WriteLine("Incorrect password. Try again.");
        } 
        while (true);  // Would be infinite without break statements
    }
}
```

### continue Statement

**Definition**: The continue statement skips the remaining statements in the current iteration of a loop and moves to the next iteration. It doesn't exit the loop entirely, just skips to the next cycle.

**Use Cases**:
- Skip certain elements in data processing
- Filter out unwanted values
- Optimize loop performance by avoiding unnecessary processing
- Handle special cases within loops

```csharp
class ContinueStatementDemo 
{
    public static void Main() 
    {
        // Basic continue in for loop
        Console.WriteLine("Printing odd numbers from 1 to 10:");
        for (int i = 1; i <= 10; i++) 
        {
            if (i % 2 == 0) 
            {
                continue;  // Skip even numbers
            }
            Console.WriteLine($"Odd number: {i}");
        }
        
        // Continue with data processing
        Console.WriteLine("\nProcessing temperatures (skipping invalid readings):");
        double[] temperatures = { 25.5, -999, 30.2, -999, 28.7, 31.1, -999, 29.3 };
        double sum = 0;
        int validCount = 0;
        
        for (int i = 0; i < temperatures.Length; i++) 
        {
            if (temperatures[i] == -999) 
            {
                Console.WriteLine($"Skipping invalid reading at index {i}");
                continue;  // Skip invalid temperature readings
            }
            
            sum += temperatures[i];
            validCount++;
            Console.WriteLine($"Valid temperature: {temperatures[i]}°C");
        }
        
        double average = validCount > 0 ? sum / validCount : 0;
        Console.WriteLine($"Average temperature: {average:F1}°C");
        
        // Continue in while loop
        Console.WriteLine("\nProcessing user inputs (type 'quit' to exit):");
        int inputCount = 0;
        
        while (inputCount < 5)  // Limit to 5 inputs for demo
        {
            Console.Write("Enter a positive number (or 'quit'): ");
            string input = Console.ReadLine();
            inputCount++;
            
            if (input?.ToLower() == "quit") 
            {
                Console.WriteLine("Quitting...");
                break;
            }
            
            if (!double.TryParse(input, out double number)) 
            {
                Console.WriteLine("Invalid input. Please enter a number.");
                continue;  // Skip to next iteration
            }
            
            if (number <= 0) 
            {
                Console.WriteLine("Number must be positive. Skipping...");
                continue;  // Skip negative or zero numbers
            }
            
            Console.WriteLine($"Processing: {number}");
            Console.WriteLine($"Square root: {Math.Sqrt(number):F2}");
        }
        
        // Continue in foreach loop
        Console.WriteLine("\nProcessing employee data:");
        List<Employee> employees = new List<Employee> 
        {
            new Employee { Name = "Rijoan", Age = 25, Department = "IT" },
            new Employee { Name = "", Age = 30, Department = "HR" },  // Invalid name
            new Employee { Name = "Khairul", Age = -5, Department = "Finance" },  // Invalid age
            new Employee { Name = "Raisul", Age = 35, Department = "" },  // Invalid department
            new Employee { Name = "Saif", Age = 28, Department = "IT" }
        };
        
        Console.WriteLine("Valid employees:");
        foreach (Employee emp in employees) 
        {
            // Skip employees with invalid data
            if (string.IsNullOrWhiteSpace(emp.Name)) 
            {
                Console.WriteLine("Skipping employee with empty name");
                continue;
            }
            
            if (emp.Age <= 0 || emp.Age > 100) 
            {
                Console.WriteLine($"Skipping {emp.Name} with invalid age: {emp.Age}");
                continue;
            }
            
            if (string.IsNullOrWhiteSpace(emp.Department)) 
            {
                Console.WriteLine($"Skipping {emp.Name} with empty department");
                continue;
            }
            
            // Process valid employee
            Console.WriteLine($"✓ {emp.Name}, Age: {emp.Age}, Dept: {emp.Department}");
        }
        
        // Continue in nested loops
        Console.WriteLine("\nPrinting multiplication table (skipping multiples of 3):");
        for (int i = 1; i <= 4; i++) 
        {
            Console.WriteLine($"\nTable for {i}:");
            for (int j = 1; j <= 10; j++) 
            {
                int product = i * j;
                if (product % 3 == 0) 
                {
                    continue;  // Skip multiples of 3
                }
                Console.WriteLine($"{i} × {j} = {product}");
            }
        }
        
        // Practical example: File processing simulation
        Console.WriteLine("\nSimulating file processing:");
        string[] files = 
        {
            "document.txt", "image.jpg", "backup.tmp", 
            "data.csv", "temp.log", "report.pdf", 
            "cache.tmp", "config.xml"
        };
        
        Console.WriteLine("Processing files (skipping temporary files):");
        foreach (string file in files) 
        {
            if (file.EndsWith(".tmp") || file.EndsWith(".log")) 
            {
                Console.WriteLine($"Skipping temporary file: {file}");
                continue;
            }
            
            Console.WriteLine($"Processing: {file}");
            // Simulate processing...
        }
    }
}

// Helper class for employee example
class Employee 
{
    public string Name { get; set; }
    public int Age { get; set; }
    public string Department { get; set; }
}
```

## Exception Handling

### Definition
Exception handling is a programming construct that allows you to handle runtime errors gracefully. It provides a structured way to catch, handle, and recover from unexpected situations that may occur during program execution.

**Key Concepts**:
- **Exception**: An error condition that occurs during program execution
- **Throwing**: The process of signaling that an error has occurred
- **Catching**: The process of handling the thrown exception
- **Finally**: Code that always executes, regardless of whether an exception occurred

### try-catch-finally Statement

```csharp
class ExceptionHandlingDemo 
{
    public static void Main() 
    {
        // Basic try-catch
        Console.WriteLine("Basic exception handling:");
        try 
        {
            int[] numbers = { 1, 2, 3 };
            Console.WriteLine(numbers[5]);  // This will throw IndexOutOfRangeException
        } 
        catch (IndexOutOfRangeException ex) 
        {
            Console.WriteLine($"Array index error: {ex.Message}");
        }
        
        // Multiple catch blocks
        Console.WriteLine("\nMultiple exception types:");
        try 
        {
            Console.Write("Enter a number: ");
            string input = Console.ReadLine();
            int number = int.Parse(input);
            int result = 100 / number;
            Console.WriteLine($"100 / {number} = {result}");
        } 
        catch (FormatException ex) 
        {
            Console.WriteLine($"Invalid format: {ex.Message}");
        } 
        catch (DivideByZeroException ex) 
        {
            Console.WriteLine($"Cannot divide by zero: {ex.Message}");
        } 
        catch (Exception ex)  // General exception (should be last)
        {
            Console.WriteLine($"Unexpected error: {ex.Message}");
        }
        
        // try-catch-finally
        Console.WriteLine("\nUsing finally block:");
        FileStream file = null;
        try 
        {
            file = new FileStream("test.txt", FileMode.Open);
            // Process file...
            Console.WriteLine("File processed successfully");
        } 
        catch (FileNotFoundException) 
        {
            Console.WriteLine("File not found - creating new file");
            file = new FileStream("test.txt", FileMode.Create);
        } 
        catch (IOException ex) 
        {
            Console.WriteLine($"I/O error: {ex.Message}");
        } 
        finally 
        {
            // This always executes
            file?.Close();
            Console.WriteLine("File closed in finally block");
        }
        
        // Using statement (automatic disposal)
        Console.WriteLine("\nUsing 'using' statement for automatic cleanup:");
        try 
        {
            using (FileStream fs = new FileStream("data.txt", FileMode.OpenOrCreate)) 
            {
                // File automatically closed when exiting using block
                Console.WriteLine("Working with file...");
            }  // fs.Dispose() called automatically here
        } 
        catch (Exception ex) 
        {
            Console.WriteLine($"File error: {ex.Message}");
        }
        
        // Custom exceptions
        Console.WriteLine("\nCustom exceptions:");
        try 
        {
            ValidateAge(150);
        } 
        catch (InvalidAgeException ex) 
        {
            Console.WriteLine($"Age validation error: {ex.Message}");
        }
        
        // Exception properties
        Console.WriteLine("\nException properties:");
        try 
        {
            ThrowDetailedException();
        } 
        catch (Exception ex) 
        {
            Console.WriteLine($"Message: {ex.Message}");
            Console.WriteLine($"Source: {ex.Source}");
            Console.WriteLine($"Stack Trace: {ex.StackTrace}");
            if (ex.InnerException != null) 
            {
                Console.WriteLine($"Inner Exception: {ex.InnerException.Message}");
            }
        }
    }
    
    // Method that throws custom exception
    static void ValidateAge(int age) 
    {
        if (age < 0 || age > 120) 
        {
            throw new InvalidAgeException($"Age {age} is not valid. Must be between 0 and 120.");
        }
    }
    
    // Method that demonstrates exception wrapping
    static void ThrowDetailedException() 
    {
        try 
        {
            // Simulate an inner exception
            throw new InvalidOperationException("Inner operation failed");
        } 
        catch (Exception innerEx) 
        {
            throw new ApplicationException("Outer operation failed", innerEx);
        }
    }
}

// Custom exception class
public class InvalidAgeException : Exception 
{
    public InvalidAgeException() : base() { }
    public InvalidAgeException(string message) : base(message) { }
    public InvalidAgeException(string message, Exception innerException) : base(message, innerException) { }
}
```

## Methods and Functions

### Definition
Methods (also called functions in other languages) are reusable blocks of code that perform specific tasks. They help organize code, promote reusability, and make programs more maintainable by breaking complex problems into smaller, manageable pieces.

**Benefits**:
- **Reusability**: Write once, use many times
- **Modularity**: Break complex problems into smaller parts
- **Maintainability**: Easier to update and debug
- **Readability**: Code becomes more organized and understandable
- **Testing**: Individual methods can be tested separately

### Method Components

```csharp
class MethodsDemo 
{
    // Basic method structure
    // [access modifier] [static] [return type] [method name]([parameters])
    
    // Simple method with no parameters and no return value
    public static void SayHello() 
    {
        Console.WriteLine("Hello, World!");
    }
    
    // Method with parameters
    public static void GreetPerson(string name) 
    {
        Console.WriteLine($"Hello, {name}!");
    }
    
    // Method with return value
    public static int Add(int a, int b) 
    {
        return a + b;
    }
    
    // Method with multiple parameters and return value
    public static double CalculateCircleArea(double radius) 
    {
        if (radius < 0) 
        {
            throw new ArgumentException("Radius cannot be negative");
        }
        return Math.PI * radius * radius;
    }
    
    // Method overloading (same name, different parameters)
    public static int Multiply(int a, int b) 
    {
        return a * b;
    }
    
    public static double Multiply(double a, double b) 
    {
        return a * b;
    }
    
    public static int Multiply(int a, int b, int c) 
    {
        return a * b * c;
    }
    
    // Method with optional parameters (default values)
    public static string FormatName(string firstName, string lastName, string title = "Mr./Ms.") 
    {
        return $"{title} {firstName} {lastName}";
    }
    
    // Method with params keyword (variable number of arguments)
    public static int Sum(params int[] numbers) 
    {
        int total = 0;
        foreach (int number in numbers) 
        {
            total += number;
        }
        return total;
    }
    
    // Method with ref parameter (pass by reference)
    public static void SwapNumbers(ref int a, ref int b) 
    {
        int temp = a;
        a = b;
        b = temp;
    }
    
    // Method with out parameter (must assign value before returning)
    public static bool TryDivide(int dividend, int divisor, out double result) 
    {
        if (divisor == 0) 
        {
            result = 0;
            return false;
        }
        result = (double)dividend / divisor;
        return true;
    }
    
    // Method with in parameter (readonly reference)
    public static void PrintPersonInfo(in Person person) 
    {
        // person cannot be modified inside this method
        Console.WriteLine($"Name: {person.Name}, Age: {person.Age}");
    }
    
    // Recursive method
    public static int Factorial(int n) 
    {
        if (n <= 1) 
            return 1;
        return n * Factorial(n - 1);
    }
    
    // Method returning multiple values using tuples
    public static (int min, int max, double average) AnalyzeNumbers(int[] numbers) 
    {
        if (numbers == null || numbers.Length == 0) 
        {
            return (0, 0, 0);
        }
        
        int min = numbers[0];
        int max = numbers[0];
        int sum = 0;
        
        foreach (int number in numbers) 
        {
            if (number < min) min = number;
            if (number > max) max = number;
            sum += number;
        }
        
        double average = (double)sum / numbers.Length;
        return (min, max, average);
    }
    
    // Expression-bodied method (C# 6.0+)
    public static double ConvertCelsiusToFahrenheit(double celsius) => celsius * 9 / 5 + 32;
    
    // Local function (nested method)
    public static void ProcessData() 
    {
        Console.WriteLine("Processing data...");
        
        // Local function - only visible within ProcessData
        bool IsValidData(string data) 
        {
            return !string.IsNullOrWhiteSpace(data) && data.Length > 0;
        }
        
        string[] dataItems = { "Item1", "", "Item3", null, "Item5" };
        
        foreach (string item in dataItems) 
        {
            if (IsValidData(item)) 
            {
                Console.WriteLine($"Valid: {item}");
            } 
            else 
            {
                Console.WriteLine("Invalid data found");
            }
        }
    }
    
    public static void Main() 
    {
        // Calling methods
        SayHello();
        GreetPerson("Rijoan");
        
        int sum = Add(5, 3);
        Console.WriteLine($"5 + 3 = {sum}");
        
        double area = CalculateCircleArea(5.0);
        Console.WriteLine($"Circle area: {area:F2}");
        
        // Method overloading
        Console.WriteLine($"Int multiply: {Multiply(3, 4)}");
        Console.WriteLine($"Double multiply: {Multiply(3.5, 2.5)}");
        Console.WriteLine($"Triple multiply: {Multiply(2, 3, 4)}");
        
        // Optional parameters
        Console.WriteLine(FormatName("Rijoan", "Mahmud"));  // Uses default title
        Console.WriteLine(FormatName("Khairul", "Islam", "Dr."));  // Custom title
        
        // Variable arguments
        Console.WriteLine($"Sum of 1,2,3: {Sum(1, 2, 3)}");
        Console.WriteLine($"Sum of 1,2,3,4,5: {Sum(1, 2, 3, 4, 5)}");
        
        // ref parameter
        int x = 10, y = 20;
        Console.WriteLine($"Before swap: x={x}, y={y}");
        SwapNumbers(ref x, ref y);
        Console.WriteLine($"After swap: x={x}, y={y}");
        
        // out parameter
        if (TryDivide(10, 3, out double divisionResult)) 
        {
            Console.WriteLine($"Division result: {divisionResult:F2}");
        } 
        else 
        {
            Console.WriteLine("Division failed");
        }
        
        // Recursive method
        Console.WriteLine($"Factorial of 5: {Factorial(5)}");
        
        // Multiple return values
        int[] testNumbers = { 1, 5, 3, 9, 2, 8, 4 };
        var (min, max, avg) = AnalyzeNumbers(testNumbers);
        Console.WriteLine($"Min: {min}, Max: {max}, Average: {avg:F2}");
        
        // Expression-bodied method
        double fahrenheit = ConvertCelsiusToFahrenheit(25);
        Console.WriteLine($"25°C = {fahrenheit}°F");
        
        // Local function demo
        ProcessData();
    }
}

// Helper class for in parameter example
public class Person 
{
    public string Name { get; set; }
    public int Age { get; set; }
}
```
## Object-Oriented Programming (OOP) - The Four Principles

### Definition
Object-Oriented Programming (OOP) is a programming paradigm based on the concept of "objects" that contain data (attributes) and code (methods). OOP is built on four fundamental principles that help create maintainable, scalable, and reusable code.

### Why OOP?
- **Code Reusability**: Write once, use multiple times
- **Modularity**: Break complex problems into smaller, manageable pieces
- **Maintainability**: Easier to update and modify existing code
- **Scalability**: Easy to extend functionality
- **Real-world Modeling**: Maps closely to how we think about real-world entities

## 1. Encapsulation

### Definition
Encapsulation is the bundling of data (fields) and methods that operate on that data within a single unit (class), while restricting direct access to some of the object's components. It's about hiding the internal implementation details and exposing only what's necessary through a well-defined interface.

### Key Concepts:
- **Data Hiding**: Hide internal data from outside access
- **Access Modifiers**: Control visibility of class members
- **Properties**: Provide controlled access to private fields
- **Information Hiding**: Hide implementation complexity

### Access Modifiers in C#:
- **public**: Accessible from anywhere
- **private**: Accessible only within the same class
- **protected**: Accessible within the class and its derived classes
- **internal**: Accessible within the same assembly
- **protected internal**: Accessible within the same assembly or derived classes
- **private protected**: Accessible within the same class or derived classes in the same assembly

```csharp
// Example demonstrating Encapsulation
public class BankAccount 
{
    // Private fields - data hiding
    private string _accountNumber;
    private decimal _balance;
    private string _accountHolderName;
    private List<string> _transactionHistory;
    
    // Constructor
    public BankAccount(string accountNumber, string accountHolderName, decimal initialBalance = 0) 
    {
        _accountNumber = accountNumber ?? throw new ArgumentNullException(nameof(accountNumber));
        _accountHolderName = accountHolderName ?? throw new ArgumentNullException(nameof(accountHolderName));
        _balance = initialBalance >= 0 ? initialBalance : throw new ArgumentException("Initial balance cannot be negative");
        _transactionHistory = new List<string>();
        
        if (initialBalance > 0) 
        {
            _transactionHistory.Add($"Account opened with initial deposit: ${initialBalance:F2}");
        }
    }
    
    // Public properties - controlled access to private data
    public string AccountNumber => _accountNumber;  // Read-only
    public string AccountHolderName => _accountHolderName;  // Read-only
    
    // Read-only property with logic
    public decimal Balance 
    {
        get 
        {
            Console.WriteLine("Balance accessed");
            return _balance;
        }
    }
    
    // Read-only property returning copy of private collection
    public IReadOnlyList<string> TransactionHistory => _transactionHistory.AsReadOnly();
    
    // Public methods - controlled operations on private data
    public bool Deposit(decimal amount) 
    {
        if (amount <= 0) 
        {
            Console.WriteLine("Deposit amount must be positive");
            return false;
        }
        
        _balance += amount;
        _transactionHistory.Add($"Deposited: ${amount:F2} | New Balance: ${_balance:F2}");
        Console.WriteLine($"Successfully deposited ${amount:F2}");
        return true;
    }
    
    public bool Withdraw(decimal amount) 
    {
        if (amount <= 0) 
        {
            Console.WriteLine("Withdrawal amount must be positive");
            return false;
        }
        
        if (amount > _balance) 
        {
            Console.WriteLine("Insufficient funds");
            return false;
        }
        
        _balance -= amount;
        _transactionHistory.Add($"Withdrawn: ${amount:F2} | New Balance: ${_balance:F2}");
        Console.WriteLine($"Successfully withdrawn ${amount:F2}");
        return true;
    }
    
    // Private method - internal implementation detail
    private bool ValidateTransaction(decimal amount) 
    {
        return amount > 0 && amount <= 10000; // Max transaction limit
    }
    
    // Public method using private validation
    public bool Transfer(BankAccount targetAccount, decimal amount) 
    {
        if (targetAccount == null) 
        {
            Console.WriteLine("Target account cannot be null");
            return false;
        }
        
        if (!ValidateTransaction(amount)) 
        {
            Console.WriteLine("Invalid transaction amount");
            return false;
        }
        
        if (Withdraw(amount)) 
        {
            if (targetAccount.Deposit(amount)) 
            {
                _transactionHistory.Add($"Transferred ${amount:F2} to account {targetAccount.AccountNumber}");
                return true;
            } 
            else 
            {
                // Rollback if deposit fails
                Deposit(amount);
                Console.WriteLine("Transfer failed - deposit to target account failed");
                return false;
            }
        }
        
        return false;
    }
    
    public void PrintStatement() 
    {
        Console.WriteLine($"\n--- Account Statement ---");
        Console.WriteLine($"Account: {_accountNumber}");
        Console.WriteLine($"Holder: {_accountHolderName}");
        Console.WriteLine($"Current Balance: ${_balance:F2}");
        Console.WriteLine("\nTransaction History:");
        
        foreach (string transaction in _transactionHistory) 
        {
            Console.WriteLine($"  {transaction}");
        }
        Console.WriteLine("--- End Statement ---\n");
    }
}

// Usage demonstrating encapsulation
class EncapsulationDemo 
{
    public static void Main() 
    {
        var account1 = new BankAccount("ACC001", "Rijoan Mahmud", 1000);
        var account2 = new BankAccount("ACC002", "Khairul Islam", 500);
        
        // Accessing public interface
        Console.WriteLine($"Account 1 Balance: ${account1.Balance}");
        
        // Using public methods
        account1.Deposit(200);
        account1.Withdraw(150);
        account1.Transfer(account2, 300);
        
        // Cannot access private fields directly
        // account1._balance = 99999;  // Compilation error!
        // account1._accountNumber = "HACKED";  // Compilation error!
        
        // Viewing transaction history through public interface
        account1.PrintStatement();
        account2.PrintStatement();
    }
}
```

### Benefits of Encapsulation:
- **Data Integrity**: Prevents invalid states through validation
- **Security**: Controls access to sensitive data
- **Flexibility**: Can change internal implementation without affecting external code
- **Maintainability**: Easier to debug and modify
- **Abstraction**: Users don't need to understand internal complexity

---
<div align="center">

# --- This is Till Quiz ---

</div>

---

## 2. Inheritance

### Definition
Inheritance is a mechanism that allows a class (derived/child class) to inherit properties, methods, and behaviors from another class (base/parent class). It enables code reuse and establishes an "is-a" relationship between classes.

### Key Concepts:
- **Base Class (Parent)**: The class being inherited from
- **Derived Class (Child)**: The class that inherits from the base class
- **IS-A Relationship**: Derived class "is a" type of base class
- **Method Overriding**: Derived class can provide specific implementation
- **Method Overloading**: Multiple methods with same name but different parameters

### Types of Inheritance:
- **Single Inheritance**: One base class, one derived class
- **Multilevel Inheritance**: Chain of inheritance (A → B → C)
- **Hierarchical Inheritance**: Multiple classes inherit from one base class

Note: C# doesn't support multiple inheritance from classes (but supports multiple interfaces)

```csharp
// Base class demonstrating inheritance
public class Animal 
{
    // Protected members - accessible to derived classes
    protected string _name;
    protected int _age;
    protected string _species;
    
    // Public constructor
    public Animal(string name, int age, string species) 
    {
        _name = name ?? throw new ArgumentNullException(nameof(name));
        _age = age >= 0 ? age : throw new ArgumentException("Age cannot be negative");
        _species = species ?? throw new ArgumentNullException(nameof(species));
        
        Console.WriteLine($"Animal created: {_name}");
    }
    
    // Virtual method - can be overridden in derived classes
    public virtual void MakeSound() 
    {
        Console.WriteLine($"{_name} makes a generic animal sound");
    }
    
    // Virtual method with implementation
    public virtual void Sleep() 
    {
        Console.WriteLine($"{_name} is sleeping peacefully");
    }
    
    // Non-virtual method - cannot be overridden (but can be hidden)
    public void Breathe() 
    {
        Console.WriteLine($"{_name} is breathing");
    }
    
    // Virtual method
    public virtual void Move() 
    {
        Console.WriteLine($"{_name} is moving");
    }
    
    // Protected method - available to derived classes
    protected void UpdateAge(int newAge) 
    {
        if (newAge >= _age) 
        {
            _age = newAge;
            Console.WriteLine($"{_name}'s age updated to {_age}");
        }
    }
    
    // Public properties
    public string Name => _name;
    public int Age => _age;
    public string Species => _species;
    
    // Virtual method for string representation
    public override string ToString() 
    {
        return $"{_name} ({_species}), Age: {_age}";
    }
}

// Derived class - Single Inheritance
public class Dog : Animal 
{
    private string _breed;
    private bool _isTrained;
    
    // Constructor calls base constructor
    public Dog(string name, int age, string breed, bool isTrained = false) 
        : base(name, age, "Canine")  // Call base class constructor
    {
        _breed = breed ?? "Mixed";
        _isTrained = isTrained;
        Console.WriteLine($"Dog created: {_name} is a {_breed}");
    }
    
    // Override virtual method - provide specific implementation
    public override void MakeSound() 
    {
        Console.WriteLine($"{_name} barks: Woof! Woof!");
    }
    
    // Override Move method
    public override void Move() 
    {
        Console.WriteLine($"{_name} runs on four legs, wagging tail");
    }
    
    // New method specific to Dog
    public void Fetch() 
    {
        if (_isTrained) 
        {
            Console.WriteLine($"{_name} fetches the ball happily!");
        } 
        else 
        {
            Console.WriteLine($"{_name} looks confused about fetching");
        }
    }
    
    // New method
    public void Train() 
    {
        if (!_isTrained) 
        {
            _isTrained = true;
            Console.WriteLine($"{_name} has been trained!");
        } 
        else 
        {
            Console.WriteLine($"{_name} is already trained");
        }
    }
    
    // Method to demonstrate protected access
    public void HaveBirthday() 
    {
        UpdateAge(_age + 1);  // Using protected method from base class
        Console.WriteLine($"Happy birthday, {_name}!");
    }
    
    // Property specific to Dog
    public string Breed => _breed;
    public bool IsTrained => _isTrained;
    
    // Override ToString
    public override string ToString() 
    {
        return $"{base.ToString()}, Breed: {_breed}, Trained: {_isTrained}";
    }
}

// Another derived class
public class Cat : Animal 
{
    private bool _isIndoor;
    private int _livesRemaining;
    
    public Cat(string name, int age, bool isIndoor = true) 
        : base(name, age, "Feline") 
    {
        _isIndoor = isIndoor;
        _livesRemaining = 9;  // Cats have 9 lives!
        Console.WriteLine($"Cat created: {_name}, Indoor: {_isIndoor}");
    }
    
    // Override methods
    public override void MakeSound() 
    {
        Console.WriteLine($"{_name} meows: Meow! Purr...");
    }
    
    public override void Move() 
    {
        Console.WriteLine($"{_name} moves gracefully and silently");
    }
    
    // Cat-specific methods
    public void Climb() 
    {
        Console.WriteLine($"{_name} climbs up high with agility");
    }
    
    public void UseLitterBox() 
    {
        if (_isIndoor) 
        {
            Console.WriteLine($"{_name} uses the litter box");
        } 
        else 
        {
            Console.WriteLine($"{_name} goes outside");
        }
    }
    
    // Properties
    public bool IsIndoor => _isIndoor;
    public int LivesRemaining => _livesRemaining;
    
    public override string ToString() 
    {
        return $"{base.ToString()}, Indoor: {_isIndoor}, Lives: {_livesRemaining}";
    }
}

// Multilevel Inheritance - Puppy inherits from Dog, which inherits from Animal
public class Puppy : Dog 
{
    private int _energyLevel;
    
    public Puppy(string name, int age, string breed) 
        : base(name, age, breed, false)  // Puppies are typically not trained initially
    {
        _energyLevel = 100;  // Puppies have high energy!
        Console.WriteLine($"Puppy created: {_name} is full of energy!");
    }
    
    // Override method from Dog
    public override void MakeSound() 
    {
        Console.WriteLine($"{_name} makes puppy sounds: Yip! Yip! *whimper*");
    }
    
    // New puppy-specific methods
    public void Play() 
    {
        if (_energyLevel > 20) 
        {
            _energyLevel -= 20;
            Console.WriteLine($"{_name} plays energetically! Energy: {_energyLevel}%");
        } 
        else 
        {
            Console.WriteLine($"{_name} is too tired to play");
        }
    }
    
    public void Nap() 
    {
        _energyLevel = Math.Min(100, _energyLevel + 50);
        Console.WriteLine($"{_name} takes a nap and recovers energy: {_energyLevel}%");
    }
    
    // Override Sleep method
    public override void Sleep() 
    {
        _energyLevel = 100;
        Console.WriteLine($"{_name} sleeps deeply and wakes up with full energy!");
    }
    
    public int EnergyLevel => _energyLevel;
}

// Inheritance demonstration
class InheritanceDemo 
{
    public static void Main() 
    {
        Console.WriteLine("=== Inheritance Demo ===\n");
        
        // Creating objects of different classes
        Animal genericAnimal = new Animal("Generic", 5, "Unknown");
        Dog myDog = new Dog("Rocky", 3, "Golden Retriever", true);
        Cat myCat = new Cat("Fluffy", 2, true);
        Puppy myPuppy = new Puppy("Bruno", 1, "Labrador");
        
        Console.WriteLine("\n--- Basic Information ---");
        Console.WriteLine(genericAnimal);
        Console.WriteLine(myDog);
        Console.WriteLine(myCat);
        Console.WriteLine(myPuppy);
        
        Console.WriteLine("\n--- Making Sounds (Polymorphism) ---");
        genericAnimal.MakeSound();  // Generic sound
        myDog.MakeSound();          // Dog bark
        myCat.MakeSound();          // Cat meow
        myPuppy.MakeSound();        // Puppy sounds
        
        Console.WriteLine("\n--- Movement ---");
        genericAnimal.Move();
        myDog.Move();
        myCat.Move();
        myPuppy.Move();
        
        Console.WriteLine("\n--- Inherited Methods ---");
        genericAnimal.Breathe();  // All animals can breathe
        myDog.Breathe();
        myCat.Breathe();
        myPuppy.Breathe();
        
        Console.WriteLine("\n--- Class-Specific Methods ---");
        myDog.Fetch();
        myDog.Train();
        
        myCat.Climb();
        myCat.UseLitterBox();
        
        myPuppy.Play();
        myPuppy.Play();
        myPuppy.Nap();
        
        Console.WriteLine("\n--- Demonstrating IS-A Relationship ---");
        // A Dog IS-A Animal
        Animal animalReference = myDog;
        animalReference.MakeSound();  // Still calls Dog's implementation due to polymorphism
        
        // A Puppy IS-A Dog and IS-A Animal
        Animal puppyAsAnimal = myPuppy;
        Dog puppyAsDog = myPuppy;
        
        puppyAsAnimal.MakeSound();  // Puppy's sound
        puppyAsDog.Fetch();         // Inherited from Dog
        
        Console.WriteLine("\n--- Birthday Celebration ---");
        myDog.HaveBirthday();  // Using protected method from base class
    }
}
```

### Benefits of Inheritance:
- **Code Reusability**: Avoid duplicating common functionality
- **Extensibility**: Easy to add new features to existing classes
- **Maintainability**: Changes in base class automatically propagate
- **Polymorphism**: Treat objects of different classes uniformly
- **Logical Organization**: Models real-world relationships

## 3. Polymorphism

### Definition
Polymorphism allows objects of different types to be treated as instances of the same type through a common interface. The word "polymorphism" comes from Greek, meaning "many forms." It enables a single interface to represent different underlying forms (data types).

### Types of Polymorphism:

#### 1. Compile-Time Polymorphism (Static)
- **Method Overloading**: Multiple methods with same name but different parameters
- **Operator Overloading**: Custom behavior for operators

#### 2. Runtime Polymorphism (Dynamic)
- **Method Overriding**: Derived classes provide specific implementations
- **Virtual Methods**: Methods that can be overridden
- **Abstract Methods**: Must be implemented by derived classes
- **Interface Implementation**: Classes implementing common interfaces

```csharp
// Base class for demonstrating polymorphism
public abstract class Shape 
{
    protected string _name;
    protected string _color;
    
    public Shape(string name, string color = "Black") 
    {
        _name = name;
        _color = color;
    }
    
    // Abstract method - must be implemented by derived classes
    public abstract double CalculateArea();
    public abstract double CalculatePerimeter();
    
    // Virtual method - can be overridden
    public virtual void DisplayInfo() 
    {
        Console.WriteLine($"Shape: {_name}");
        Console.WriteLine($"Color: {_color}");
        Console.WriteLine($"Area: {CalculateArea():F2}");
        Console.WriteLine($"Perimeter: {CalculatePerimeter():F2}");
    }
    
    // Virtual method
    public virtual void Draw() 
    {
        Console.WriteLine($"Drawing a {_color} {_name}");
    }
    
    // Non-virtual method (common to all shapes)
    public void ChangeColor(string newColor) 
    {
        _color = newColor;
        Console.WriteLine($"{_name} color changed to {_color}");
    }
    
    // Properties
    public string Name => _name;
    public string Color => _color;
}

// Derived class - Circle
public class Circle : Shape 
{
    private double _radius;
    
    public Circle(double radius, string color = "Red") : base("Circle", color) 
    {
        _radius = radius > 0 ? radius : throw new ArgumentException("Radius must be positive");
    }
    
    // Implement abstract methods
    public override double CalculateArea() 
    {
        return Math.PI * _radius * _radius;
    }
    
    public override double CalculatePerimeter() 
    {
        return 2 * Math.PI * _radius;
    }
    
    // Override virtual method
    public override void Draw() 
    {
        Console.WriteLine($"Drawing a {_color} circle with radius {_radius}");
        Console.WriteLine("    ⭘");
    }
    
    // Circle-specific method
    public double GetDiameter() => _radius * 2;
    
    public double Radius => _radius;
}

// Derived class - Rectangle
public class Rectangle : Shape 
{
    private double _width;
    private double _height;
    
    public Rectangle(double width, double height, string color = "Blue") : base("Rectangle", color) 
    {
        _width = width > 0 ? width : throw new ArgumentException("Width must be positive");
        _height = height > 0 ? height : throw new ArgumentException("Height must be positive");
    }
    
    // Implement abstract methods
    public override double CalculateArea() 
    {
        return _width * _height;
    }
    
    public override double CalculatePerimeter() 
    {
        return 2 * (_width + _height);
    }
    
    // Override virtual method
    public override void Draw() 
    {
        Console.WriteLine($"Drawing a {_color} rectangle ({_width} x {_height})");
        Console.WriteLine("    ▬▬▬▬");
        Console.WriteLine("    ▬▬▬▬");
    }
    
    // Override DisplayInfo to add specific information
    public override void DisplayInfo() 
    {
        base.DisplayInfo();  // Call parent implementation
        Console.WriteLine($"Dimensions: {_width} x {_height}");
    }
    
    // Rectangle-specific methods
    public bool IsSquare() => Math.Abs(_width - _height) < 0.001;
    
    public double Width => _width;
    public double Height => _height;
}

// Another derived class - Triangle
public class Triangle : Shape 
{
    private double _base;
    private double _height;
    private double _side1, _side2, _side3;
    
    public Triangle(double baseLength, double height, double side1, double side2, double side3, string color = "Green") 
        : base("Triangle", color) 
    {
        _base = baseLength > 0 ? baseLength : throw new ArgumentException("Base must be positive");
        _height = height > 0 ? height : throw new ArgumentException("Height must be positive");
        _side1 = side1 > 0 ? side1 : throw new ArgumentException("Side1 must be positive");
        _side2 = side2 > 0 ? side2 : throw new ArgumentException("Side2 must be positive");
        _side3 = side3 > 0 ? side3 : throw new ArgumentException("Side3 must be positive");
    }
    
    // Implement abstract methods
    public override double CalculateArea() 
    {
        return 0.5 * _base * _height;
    }
    
    public override double CalculatePerimeter() 
    {
        return _side1 + _side2 + _side3;
    }
    
    // Override virtual method
    public override void Draw() 
    {
        Console.WriteLine($"Drawing a {_color} triangle");
        Console.WriteLine("      ▲");
        Console.WriteLine("     ▲ ▲");
        Console.WriteLine("    ▲▲▲▲▲");
    }
    
    // Triangle-specific methods
    public string GetTriangleType() 
    {
        if (Math.Abs(_side1 - _side2) < 0.001 && Math.Abs(_side2 - _side3) < 0.001) 
            return "Equilateral";
        else if (Math.Abs(_side1 - _side2) < 0.001 || Math.Abs(_side2 - _side3) < 0.001 || Math.Abs(_side1 - _side3) < 0.001) 
            return "Isosceles";
        else 
            return "Scalene";
    }
    
    public double Base => _base;
    public double Height => _height;
}

// Interface for demonstrating interface polymorphism
public interface IDrawable 
{
    void Draw();
    void SetColor(string color);
}

public interface IResizable 
{
    void Scale(double factor);
    double GetSize();
}

// Class implementing multiple interfaces
public class Square : Shape, IDrawable, IResizable 
{
    private double _side;
    
    public Square(double side, string color = "Yellow") : base("Square", color) 
    {
        _side = side > 0 ? side : throw new ArgumentException("Side must be positive");
    }
    
    // Implement abstract methods from Shape
    public override double CalculateArea() => _side * _side;
    public override double CalculatePerimeter() => 4 * _side;
    
    // Override Draw from Shape (also satisfies IDrawable)
    public override void Draw() 
    {
        Console.WriteLine($"Drawing a {_color} square with side {_side}");
        Console.WriteLine("    ■■■■");
        Console.WriteLine("    ■■■■");
        Console.WriteLine("    ■■■■");
        Console.WriteLine("    ■■■■");
    }
    
    // Implement IDrawable explicitly
    void IDrawable.SetColor(string color) 
    {
        ChangeColor(color);
    }
    
    // Implement IResizable
    public void Scale(double factor) 
    {
        if (factor > 0) 
        {
            _side *= factor;
            Console.WriteLine($"Square scaled by {factor}. New side: {_side:F2}");
        }
    }
    
    public double GetSize() => _side;
    
    public double Side => _side;
}

// Polymorphism demonstration
class PolymorphismDemo 
{
    public static void Main() 
    {
        Console.WriteLine("=== Polymorphism Demo ===\n");
        
        // Array of Shape references - polymorphic collection
        Shape[] shapes = 
        {
            new Circle(5.0, "Red"),
            new Rectangle(4.0, 6.0, "Blue"),
            new Triangle(3.0, 4.0, 3.0, 4.0, 5.0, "Green"),
            new Square(3.0, "Yellow")
        };
        
        Console.WriteLine("--- Processing Shapes Polymorphically ---");
        foreach (Shape shape in shapes) 
        {
            // Polymorphic method calls - actual implementation depends on object type
            shape.DisplayInfo();
            shape.Draw();
            Console.WriteLine($"Area: {shape.CalculateArea():F2}");
            Console.WriteLine($"Perimeter: {shape.CalculatePerimeter():F2}");
            Console.WriteLine();
        }
        
        Console.WriteLine("--- Runtime Type Checking ---");
        foreach (Shape shape in shapes) 
        {
            Console.WriteLine($"Processing {shape.Name}:");
            
            // Type checking and casting
            if (shape is Circle circle) 
            {
                Console.WriteLine($"  Circle-specific: Diameter = {circle.GetDiameter():F2}");
            }
            else if (shape is Rectangle rectangle) 
            {
                Console.WriteLine($"  Rectangle-specific: Is Square? {rectangle.IsSquare()}");
            }
            else if (shape is Triangle triangle) 
            {
                Console.WriteLine($"  Triangle-specific: Type = {triangle.GetTriangleType()}");
            }
            else if (shape is Square square) 
            {
                Console.WriteLine($"  Square-specific: Side = {square.Side:F2}");
            }
        }
        
        Console.WriteLine("\n--- Interface Polymorphism ---");
        
        // Interface polymorphism
        IDrawable[] drawables = 
        {
            new Square(2.0, "Purple"),
            new Circle(3.0, "Orange")
        };
        
        foreach (IDrawable drawable in drawables) 
        {
            drawable.Draw();
            drawable.SetColor("Pink");
        }
        
        Console.WriteLine("\n--- Method Overloading (Compile-time Polymorphism) ---");
        Calculator calc = new Calculator();
        
        // Same method name, different parameters
        Console.WriteLine($"Add integers: {calc.Add(5, 3)}");
        Console.WriteLine($"Add doubles: {calc.Add(5.5, 3.2)}");
        Console.WriteLine($"Add three numbers: {calc.Add(1, 2, 3)}");
        Console.WriteLine($"Add array: {calc.Add(new int[] { 1, 2, 3, 4, 5 })}");
        
        Console.WriteLine("\n--- Polymorphic Method Parameters ---");
        ProcessShape(new Circle(4.0));
        ProcessShape(new Rectangle(3.0, 5.0));
        ProcessShape(new Square(2.5));
        
        Console.WriteLine("\n--- Collection of Different Types ---");
        var shapeList = new List<Shape> 
        {
            new Circle(2.0),
            new Rectangle(3.0, 4.0),
            new Square(2.0)
        };
        
        double totalArea = CalculateTotalArea(shapeList);
        Console.WriteLine($"Total area of all shapes: {totalArea:F2}");
    }
    
    // Method that accepts any Shape (polymorphic parameter)
    static void ProcessShape(Shape shape) 
    {
        Console.WriteLine($"Processing a {shape.Name}:");
        Console.WriteLine($"  Area: {shape.CalculateArea():F2}");
        Console.WriteLine($"  Perimeter: {shape.CalculatePerimeter():F2}");
        shape.Draw();
    }
    
    // Method demonstrating polymorphic collection processing
    static double CalculateTotalArea(IEnumerable<Shape> shapes) 
    {
        double total = 0;
        foreach (Shape shape in shapes) 
        {
            total += shape.CalculateArea();  // Polymorphic method call
        }
        return total;
    }
}

// Class demonstrating method overloading (compile-time polymorphism)
public class Calculator 
{
    // Method overloading - same name, different parameters
    public int Add(int a, int b) 
    {
        Console.WriteLine("Adding two integers");
        return a + b;
    }
    
    public double Add(double a, double b) 
    {
        Console.WriteLine("Adding two doubles");
        return a + b;
    }
    
    public int Add(int a, int b, int c) 
    {
        Console.WriteLine("Adding three integers");
        return a + b + c;
    }
    
    public int Add(params int[] numbers) 
    {
        Console.WriteLine($"Adding array of {numbers.Length} numbers");
        return numbers.Sum();
    }
    
    // Operator overloading example
    public static Calculator operator +(Calculator c1, Calculator c2) 
    {
        Console.WriteLine("Using overloaded + operator for Calculator");
        return new Calculator();
    }
}
```

### Benefits of Polymorphism:
- **Flexibility**: Write code that works with multiple types
- **Extensibility**: Add new types without changing existing code
- **Maintainability**: Single interface for multiple implementations
- **Code Reusability**: Same code works with different object types
- **Dynamic Behavior**: Behavior determined at runtime

## 4. Abstraction

### Definition
Abstraction is the process of hiding complex implementation details while exposing only the essential features and functionality to the user. It focuses on what an object does rather than how it does it. Abstraction helps manage complexity by providing a simplified interface to complex systems.

### Types of Abstraction:

#### 1. Data Abstraction
- Hide internal data representation
- Expose only necessary operations

#### 2. Process Abstraction
- Hide complex algorithms and processes
- Provide simple methods to achieve results

### Implementation in C#:
- **Abstract Classes**: Cannot be instantiated, may contain abstract methods
- **Interfaces**: Define contracts that classes must implement
- **Access Modifiers**: Control what's visible to external classes
- **Properties**: Abstract away field access with controlled logic

```csharp
// Abstract class demonstrating abstraction
public abstract class Vehicle 
{
    // Protected fields - hidden from external access but available to derived classes
    protected string _make;
    protected string _model;
    protected int _year;
    protected double _fuelLevel;
    protected double _maxFuelCapacity;
    protected bool _isEngineRunning;
    
    // Constructor
    public Vehicle(string make, string model, int year, double maxFuelCapacity) 
    {
        _make = make ?? throw new ArgumentNullException(nameof(make));
        _model = model ?? throw new ArgumentNullException(nameof(model));
        _year = year > 1900 ? year : throw new ArgumentException("Invalid year");
        _maxFuelCapacity = maxFuelCapacity > 0 ? maxFuelCapacity : throw new ArgumentException("Invalid fuel capacity");
        _fuelLevel = 0;
        _isEngineRunning = false;
    }
    
    // Abstract methods - must be implemented by derived classes
    public abstract void StartEngine();
    public abstract void StopEngine();
    public abstract double CalculateFuelEfficiency();
    public abstract void PerformMaintenance();
    
    // Virtual methods - can be overridden but have default implementation
    public virtual void Refuel(double amount) 
    {
        if (amount <= 0) 
        {
            Console.WriteLine("Fuel amount must be positive");
            return;
        }
        
        double previousLevel = _fuelLevel;
        _fuelLevel = Math.Min(_maxFuelCapacity, _fuelLevel + amount);
        double actualAmount = _fuelLevel - previousLevel;
        
        Console.WriteLine($"Refueled {actualAmount:F2} liters. Fuel level: {_fuelLevel:F2}/{_maxFuelCapacity:F2}");
    }
    
    // Concrete method - common implementation for all vehicles
    public void DisplayBasicInfo() 
    {
        Console.WriteLine($"Vehicle: {_year} {_make} {_model}");
        Console.WriteLine($"Fuel: {_fuelLevel:F2}/{_maxFuelCapacity:F2} liters");
        Console.WriteLine($"Engine: {(_isEngineRunning ? "Running" : "Off")}");
    }
    
    // Protected method - abstracted helper method
    protected bool HasSufficientFuel(double requiredFuel) 
    {
        return _fuelLevel >= requiredFuel;
    }
    
    // Properties - abstracted access to internal data
    public string Make => _make;
    public string Model => _model;
    public int Year => _year;
    public double FuelLevel => _fuelLevel;
    public bool IsEngineRunning => _isEngineRunning;
    public double FuelPercentage => (_fuelLevel / _maxFuelCapacity) * 100;
}

// Concrete implementation - Car
public class Car : Vehicle 
{
    private int _numberOfDoors;
    private string _transmissionType;
    private double _currentSpeed;
    private const double FUEL_CONSUMPTION_RATE = 0.08; // liters per km
    
    public Car(string make, string model, int year, int numberOfDoors, string transmissionType) 
        : base(make, model, year, 60.0) // 60 liter fuel tank
    {
        _numberOfDoors = numberOfDoors;
        _transmissionType = transmissionType;
        _currentSpeed = 0;
    }
    
    // Implement abstract methods
    public override void StartEngine() 
    {
        if (_isEngineRunning) 
        {
            Console.WriteLine($"{_make} {_model} engine is already running");
            return;
        }
        
        if (_fuelLevel < 1.0) 
        {
            Console.WriteLine($"Cannot start {_make} {_model} - insufficient fuel");
            return;
        }
        
        _isEngineRunning = true;
        Console.WriteLine($"{_make} {_model} engine started successfully");
        Console.WriteLine("*Vroom vroom* - Car engine purring");
    }
    
    public override void StopEngine() 
    {
        if (!_isEngineRunning) 
        {
            Console.WriteLine($"{_make} {_model} engine is already off");
            return;
        }
        
        _currentSpeed = 0;
        _isEngineRunning = false;
        Console.WriteLine($"{_make} {_model} engine stopped");
    }
    
    public override double CalculateFuelEfficiency() 
    {
        // Car-specific fuel efficiency calculation
        double baseEfficiency = 12.5; // km per liter
        
        // Adjust for transmission type
        if (_transmissionType.ToLower() == "manual") 
        {
            baseEfficiency += 1.5;
        }
        
        // Adjust for age
        double agePenalty = (_year < 2010) ? 2.0 : 0;
        
        return Math.Max(8.0, baseEfficiency - agePenalty);
    }
    
    public override void PerformMaintenance() 
    {
        Console.WriteLine($"Performing car maintenance on {_make} {_model}:");
        Console.WriteLine("- Checking engine oil");
        Console.WriteLine("- Inspecting brakes");
        Console.WriteLine("- Checking tire pressure");
        Console.WriteLine("- Testing lights and signals");
        Console.WriteLine("- Maintenance completed");
    }
    
    // Car-specific methods
    public void Drive(double distance) 
    {
        if (!_isEngineRunning) 
        {
            Console.WriteLine("Cannot drive - engine is not running");
            return;
        }
        
        double fuelNeeded = distance * FUEL_CONSUMPTION_RATE;
        if (!HasSufficientFuel(fuelNeeded)) 
        {
            Console.WriteLine($"Insufficient fuel to drive {distance} km");
            return;
        }
        
        _fuelLevel -= fuelNeeded;
        Console.WriteLine($"Drove {distance} km. Fuel remaining: {_fuelLevel:F2} liters");
    }
    
    public void Accelerate(double speedIncrease) 
    {
        if (!_isEngineRunning) 
        {
            Console.WriteLine("Cannot accelerate - engine is not running");
            return;
        }
        
        _currentSpeed = Math.Min(200, _currentSpeed + speedIncrease); // Max speed 200 km/h
        Console.WriteLine($"Accelerated to {_currentSpeed} km/h");
    }
    
    public void Brake(double speedDecrease) 
    {
        _currentSpeed = Math.Max(0, _currentSpeed - speedDecrease);
        Console.WriteLine($"Slowed down to {_currentSpeed} km/h");
    }
    
    // Properties
    public int NumberOfDoors => _numberOfDoors;
    public string TransmissionType => _transmissionType;
    public double CurrentSpeed => _currentSpeed;
}

// Another concrete implementation - Motorcycle
public class Motorcycle : Vehicle 
{
    private string _engineType;
    private bool _hasSidecar;
    private const double FUEL_CONSUMPTION_RATE = 0.04; // liters per km (more efficient)
    
    public Motorcycle(string make, string model, int year, string engineType, bool hasSidecar = false) 
        : base(make, model, year, 20.0) // 20 liter fuel tank
    {
        _engineType = engineType;
        _hasSidecar = hasSidecar;
    }
    
    // Implement abstract methods
    public override void StartEngine() 
    {
        if (_isEngineRunning) 
        {
            Console.WriteLine($"{_make} {_model} is already running");
            return;
        }
        
        if (_fuelLevel < 0.5) 
        {
            Console.WriteLine($"Cannot start {_make} {_model} - insufficient fuel");
            return;
        }
        
        _isEngineRunning = true;
        Console.WriteLine($"{_make} {_model} started");
        Console.WriteLine($"*Roar* - {_engineType} engine rumbling");
    }
    
    public override void StopEngine() 
    {
        _isEngineRunning = false;
        Console.WriteLine($"{_make} {_model} engine stopped");
    }
    
    public override double CalculateFuelEfficiency() 
    {
        double baseEfficiency = 25.0; // km per liter
        
        // Sidecar reduces efficiency
        if (_hasSidecar) 
        {
            baseEfficiency -= 5.0;
        }
        
        // Engine type affects efficiency
        if (_engineType.ToLower().Contains("sport")) 
        {
            baseEfficiency -= 3.0;
        }
        
        return Math.Max(15.0, baseEfficiency);
    }
    
    public override void PerformMaintenance() 
    {
        Console.WriteLine($"Performing motorcycle maintenance on {_make} {_model}:");
        Console.WriteLine("- Checking chain and sprockets");
        Console.WriteLine("- Inspecting brake pads");
        Console.WriteLine("- Checking tire tread");
        Console.WriteLine("- Testing lights");
        Console.WriteLine("- Maintenance completed");
    }
    
    // Motorcycle-specific methods
    public void Ride(double distance) 
    {
        if (!_isEngineRunning) 
        {
            Console.WriteLine("Cannot ride - engine is not running");
            return;
        }
        
        double fuelNeeded = distance * FUEL_CONSUMPTION_RATE;
        if (!HasSufficientFuel(fuelNeeded)) 
        {
            Console.WriteLine($"Insufficient fuel to ride {distance} km");
            return;
        }
        
        _fuelLevel -= fuelNeeded;
        Console.WriteLine($"Rode {distance} km on the motorcycle. Fuel remaining: {_fuelLevel:F2} liters");
    }
    
    // Properties
    public string EngineType => _engineType;
    public bool HasSidecar => _hasSidecar;
}

// Interface demonstrating abstraction through contracts
public interface IElectricVehicle 
{
    double BatteryLevel { get; }
    double MaxBatteryCapacity { get; }
    void ChargeBattery(double amount);
    double CalculateRange();
    void DisplayBatteryInfo();
}

// Electric car implementing both abstract class and interface
public class ElectricCar : Vehicle, IElectricVehicle 
{
    private double _batteryLevel;
    private double _maxBatteryCapacity;
    private double _energyEfficiency; // km per kWh
    
    public ElectricCar(string make, string model, int year, double batteryCapacity) 
        : base(make, model, year, 0) // No fuel tank
    {
        _maxBatteryCapacity = batteryCapacity;
        _batteryLevel = 0;
        _energyEfficiency = 5.0; // 5 km per kWh
    }
    
    // Implement abstract methods from Vehicle
    public override void StartEngine() 
    {
        if (_isEngineRunning) 
        {
            Console.WriteLine($"{_make} {_model} is already on");
            return;
        }
        
        if (_batteryLevel < 5.0) 
        {
            Console.WriteLine($"Cannot start {_make} {_model} - battery too low");
            return;
        }
        
        _isEngineRunning = true;
        Console.WriteLine($"{_make} {_model} powered on silently");
    }
    
    public override void StopEngine() 
    {
        _isEngineRunning = false;
        Console.WriteLine($"{_make} {_model} powered off");
    }
    
    public override double CalculateFuelEfficiency() 
    {
        // For electric cars, return equivalent efficiency
        return _energyEfficiency * 33.7; // kWh to gasoline equivalent
    }
    
    public override void PerformMaintenance() 
    {
        Console.WriteLine($"Performing electric car maintenance on {_make} {_model}:");
        Console.WriteLine("- Checking battery health");
        Console.WriteLine("- Inspecting electric motor");
        Console.WriteLine("- Testing regenerative braking");
        Console.WriteLine("- Updating software");
        Console.WriteLine("- Maintenance completed");
    }
    
    // Override refuel method (not applicable for electric)
    public override void Refuel(double amount) 
    {
        Console.WriteLine("Electric vehicles don't use fuel. Use ChargeBattery() instead.");
    }
    
    // Implement IElectricVehicle interface
    public double BatteryLevel => _batteryLevel;
    public double MaxBatteryCapacity => _maxBatteryCapacity;
    
    public void ChargeBattery(double amount) 
    {
        if (amount <= 0) 
        {
            Console.WriteLine("Charge amount must be positive");
            return;
        }
        
        double previousLevel = _batteryLevel;
        _batteryLevel = Math.Min(_maxBatteryCapacity, _batteryLevel + amount);
        double actualAmount = _batteryLevel - previousLevel;
        
        Console.WriteLine($"Charged {actualAmount:F2} kWh. Battery: {_batteryLevel:F2}/{_maxBatteryCapacity:F2} kWh");
    }
    
    public double CalculateRange() 
    {
        return _batteryLevel * _energyEfficiency;
    }
    
    public void DisplayBatteryInfo() 
    {
        double percentage = (_batteryLevel / _maxBatteryCapacity) * 100;
        Console.WriteLine($"Battery: {_batteryLevel:F2}/{_maxBatteryCapacity:F2} kWh ({percentage:F1}%)");
        Console.WriteLine($"Estimated range: {CalculateRange():F1} km");
    }
    
    // Electric car specific method
    public void Drive(double distance) 
    {
        if (!_isEngineRunning) 
        {
            Console.WriteLine("Cannot drive - car is not powered on");
            return;
        }
        
        double energyNeeded = distance / _energyEfficiency;
        if (_batteryLevel < energyNeeded) 
        {
            Console.WriteLine($"Insufficient battery to drive {distance} km");
            return;
        }
        
        _batteryLevel -= energyNeeded;
        Console.WriteLine($"Drove {distance} km silently. Battery remaining: {_batteryLevel:F2} kWh");
    }
}

// Abstraction demonstration
class AbstractionDemo 
{
    public static void Main() 
    {
        Console.WriteLine("=== Abstraction Demo ===\n");
        
        // Cannot instantiate abstract class
        // Vehicle vehicle = new Vehicle(); // Compilation error!
        
        // Create concrete implementations
        Car myCar = new Car("Toyota", "Camry", 2020, 4, "Automatic");
        Motorcycle myBike = new Motorcycle("Harley-Davidson", "Street 750", 2019, "V-Twin", false);
        ElectricCar myElectricCar = new ElectricCar("Tesla", "Model 3", 2022, 75.0);
        
        Console.WriteLine("--- Vehicle Information (Abstracted View) ---");
        // Using abstraction - we don't need to know internal details
        Vehicle[] vehicles = { myCar, myBike, myElectricCar };
        
        foreach (Vehicle vehicle in vehicles) 
        {
            vehicle.DisplayBasicInfo();
            Console.WriteLine($"Fuel Efficiency: {vehicle.CalculateFuelEfficiency():F2}");
            Console.WriteLine();
        }
        
        Console.WriteLine("--- Starting Engines (Abstract Method Implementation) ---");
        foreach (Vehicle vehicle in vehicles) 
        {
            vehicle.StartEngine(); // Each vehicle implements this differently
        }
        
        Console.WriteLine("\n--- Refueling/Charging (Abstracted Operations) ---");
        myCar.Refuel(40.0);
        myBike.Refuel(15.0);
        myElectricCar.ChargeBattery(50.0); // Different implementation for electric
        
        Console.WriteLine("\n--- Using Specific Features (Through Abstraction) ---");
        
        // Car-specific operations
        Console.WriteLine("Car Operations:");
        myCar.Drive(100);
        myCar.Accelerate(60);
        myCar.Brake(20);
        
        // Motorcycle-specific operations
        Console.WriteLine("\nMotorcycle Operations:");
        myBike.Ride(50);
        
        // Electric car operations
        Console.WriteLine("\nElectric Car Operations:");
        myElectricCar.DisplayBatteryInfo();
        myElectricCar.Drive(80);
        
        Console.WriteLine("\n--- Interface Abstraction ---");
        // Using interface abstraction
        if (myElectricCar is IElectricVehicle electricVehicle) 
        {
            Console.WriteLine("Electric vehicle specific operations:");
            electricVehicle.DisplayBatteryInfo();
            Console.WriteLine($"Range: {electricVehicle.CalculateRange():F1} km");
        }
        
        Console.WriteLine("\n--- Maintenance (Abstract Process) ---");
        foreach (Vehicle vehicle in vehicles) 
        {
            vehicle.PerformMaintenance(); // Each vehicle has different maintenance
            Console.WriteLine();
        }
        
        Console.WriteLine("--- Abstraction Benefits ---");
        Console.WriteLine("1. We can work with vehicles without knowing internal details");
        Console.WriteLine("2. Each vehicle type implements methods according to its nature");
        Console.WriteLine("3. Common interface allows polymorphic behavior");
        Console.WriteLine("4. Complex operations are hidden behind simple method calls");
        Console.WriteLine("5. Easy to add new vehicle types without changing existing code");
    }
}
```

### Benefits of Abstraction:
- **Simplicity**: Complex systems become easier to use
- **Maintainability**: Internal changes don't affect external usage
- **Security**: Implementation details are hidden
- **Flexibility**: Different implementations can be swapped easily
- **Reusability**: Abstract interfaces can be reused across different implementations
- **Focus**: Users focus on what to do, not how it's done

### Summary of OOP Principles:

| Principle | Purpose | Implementation | Benefits |
|-----------|---------|----------------|----------|
| **Encapsulation** | Bundle data and methods, hide implementation | private fields, public properties/methods | Data protection, controlled access |
| **Inheritance** | Reuse code, establish relationships | class derivation, IS-A relationship | Code reuse, hierarchical organization |
| **Polymorphism** | One interface, many forms | virtual methods, interfaces, overloading | Flexibility, extensibility |
| **Abstraction** | Hide complexity, show essentials | abstract classes, interfaces | Simplicity, maintainability |

These four principles work together to create robust, maintainable, and scalable object-oriented applications. They help manage complexity, promote code reuse, and make software systems more flexible and easier to understand.