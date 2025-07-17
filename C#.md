# C# Programming Notes

## Variables

- **Declaration:** `dataType variableName = value;`
- **Naming Rules:** Must start with letter/underscore, case-sensitive, no reserved keywords
- **Convention:** Use camelCase for variables (e.g., `firstName`)

```csharp
int age = 25;
string name = "Rijoan Maruf";
double salary = 50000.50;
bool isEmployed = true;
```

## Data Types and Sizes

| Type | Size | Range | Example |
|------|------|-------|---------|
| `byte` | 1 byte | 0 to 255 | `byte b = 255;` |
| `sbyte` | 1 byte | -128 to 127 | `sbyte sb = -128;` |
| `short` | 2 bytes | -32,768 to 32,767 | `short s = 32767;` |
| `ushort` | 2 bytes | 0 to 65,535 | `ushort us = 65535;` |
| `int` | 4 bytes | -2^31 to 2^31-1 | `int i = 2147483647;` |
| `uint` | 4 bytes | 0 to 2^32-1 | `uint ui = 4294967295;` |
| `long` | 8 bytes | -2^63 to 2^63-1 | `long l = 9223372036854775807L;` |
| `ulong` | 8 bytes | 0 to 2^64-1 | `ulong ul = 18446744073709551615UL;` |
| `float` | 4 bytes | ±1.5×10^−45 to ±3.4×10^38 | `float f = 3.14f;` |
| `double` | 8 bytes | ±5.0×10^−324 to ±1.7×10^308 | `double d = 3.14159;` |
| `decimal` | 16 bytes | ±1.0×10^−28 to ±7.9×10^28 | `decimal m = 3.14159265359m;` |
| `char` | 2 bytes | Unicode characters | `char c = 'A';` |
| `bool` | 1 byte | true/false | `bool b = true;` |

## Taking Input from User

```csharp
// Reading string input
Console.Write("Enter your name: ");
string name = Console.ReadLine();

// Reading numeric input
Console.Write("Enter your age: ");
int age = Convert.ToInt32(Console.ReadLine());
// Alternative: int age = int.Parse(Console.ReadLine());

// Reading a character
Console.Write("Enter a character: ");
char ch = Console.ReadKey().KeyChar;
```

## Typecasting

### Implicit Casting (Widening)
- No data loss, smaller to larger type
- Automatically done by C#

```csharp
int myInt = 10;
double myDouble = myInt;  // int to double conversion (10.0)
```

### Explicit Casting (Narrowing)
- Possible data loss, larger to smaller type
- Requires cast operator

```csharp
double myDouble = 9.78;
int myInt = (int)myDouble;  // double to int (9)
```

### Typecasting Using Methods

```csharp
// Using Convert class
int i = 10;
double d = Convert.ToDouble(i);    // 10.0
string s = Convert.ToString(i);    // "10"

// Using Parse methods
string numStr = "100";
int parsedInt = int.Parse(numStr);  // 100

// Using TryParse (safer)
bool success = int.TryParse("123", out int result);
if (success)
{
    Console.WriteLine($"Parsed successfully: {result}");
}
```

## Char and String

### Char
- Single Unicode character
- Enclosed in single quotes

```csharp
char grade = 'A';
char digit = '7';
char newline = '\n';

// Char to int conversion (gets ASCII/Unicode value)
int asciiValue = (int)grade;  // 65
```

### String
- Sequence of characters
- Enclosed in double quotes
- Strings are immutable (cannot be changed after creation)

```csharp
string firstName = "Rijoan";
string lastName = "Maruf";
string fullName = firstName + " " + lastName;  // Concatenation

// String interpolation
string greeting = $"Hello, {firstName}!";
```

## Escape Sequence Characters

| Escape Sequence | Description |
|-----------------|-------------|
| `\'` | Single quote |
| `\"` | Double quote |
| `\\` | Backslash |
| `\n` | New line |
| `\r` | Carriage return |
| `\t` | Tab |
| `\b` | Backspace |
| `\f` | Form feed |

```csharp
string text = "He said, \"Hello!\"";
string path = "C:\\Program Files\\dotnet";
string multiLine = "First line\nSecond line";
```

## Arithmetic Operators

| Operator | Description | Example |
|----------|-------------|---------|
| `+` | Addition | `int sum = 5 + 3;` // 8 |
| `-` | Subtraction | `int diff = 5 - 3;` // 2 |
| `*` | Multiplication | `int product = 5 * 3;` // 15 |
| `/` | Division | `int quotient = 10 / 3;` // 3 (integer division) |
| `%` | Modulus (remainder) | `int remainder = 10 % 3;` // 1 |
| `++` | Increment | `int x = 5; x++;` // x is now 6 |
| `--` | Decrement | `int y = 5; y--;` // y is now 4 |

## Assignment Operators

| Operator | Example | Equivalent |
|----------|---------|------------|
| `=` | `x = 5` | `x = 5` |
| `+=` | `x += 5` | `x = x + 5` |
| `-=` | `x -= 5` | `x = x - 5` |
| `*=` | `x *= 5` | `x = x * 5` |
| `/=` | `x /= 5` | `x = x / 5` |
| `%=` | `x %= 5` | `x = x % 5` |

## Comparison Operators

| Operator | Description | Example |
|----------|-------------|---------|
| `==` | Equal to | `if (x == y)` |
| `!=` | Not equal to | `if (x != y)` |
| `>` | Greater than | `if (x > y)` |
| `<` | Less than | `if (x < y)` |
| `>=` | Greater than or equal to | `if (x >= y)` |
| `<=` | Less than or equal to | `if (x <= y)` |

## Logical Operators

| Operator | Description | Example |
|----------|-------------|---------|
| `&&` | Logical AND | `if (x > 5 && x < 10)` |
| `||` | Logical OR | `if (x < 5 || x > 10)` |
| `!` | Logical NOT | `if (!isComplete)` |

## Math in C#

- **Math Class:** Provides mathematical constants and methods

```csharp
double result;

result = Math.Pow(2, 3);      // 8 (2³)
result = Math.Sqrt(25);       // 5 (square root)
result = Math.Abs(-10);       // 10 (absolute value)
result = Math.Round(3.7);     // 4 (rounding)
result = Math.Floor(3.7);     // 3 (largest integer less than or equal)
result = Math.Ceiling(3.2);   // 4 (smallest integer greater than or equal)

// Constants
double pi = Math.PI;          // 3.14159...
double e = Math.E;            // 2.71828...

// Min and Max
int maximum = Math.Max(5, 10);  // 10
int minimum = Math.Min(5, 10);  // 5

// Trigonometric functions (in radians)
double sine = Math.Sin(Math.PI / 2);      // 1
double cosine = Math.Cos(0);              // 1
double tangent = Math.Tan(Math.PI / 4);   // 1

// Random numbers
Random random = new Random();
int randomNumber = random.Next(1, 101);  // Random int from 1 to 100
```

## String Methods

```csharp
string text = "Hello, Rijoan Maruf!";

// Length
int length = text.Length;  // 19

// Accessing characters
char firstChar = text[0];  // 'H'

// Changing case
string upper = text.ToUpper();  // "HELLO, RIJOAN MARUF!"
string lower = text.ToLower();  // "hello, rijoan maruf!"

// Substring
string sub = text.Substring(7, 12);  // "Rijoan Maruf"

// Index methods
int index = text.IndexOf("Rijoan");  // 7
bool contains = text.Contains("Rijoan");  // true
bool startsWith = text.StartsWith("Hello");  // true
bool endsWith = text.EndsWith("!");  // true

// Replacing
string newText = text.Replace("Rijoan Maruf", "Mr. Maruf");  // "Hello, Mr. Maruf!"

// Trimming whitespace
string paddedText = "  Rijoan Maruf  ";
string trimmed = paddedText.Trim();  // "Rijoan Maruf"

// Splitting
string csv = "apple,banana,orange";
string[] fruits = csv.Split(',');  // ["apple", "banana", "orange"]

// Joining
string[] words = { "Hello", "Rijoan", "Maruf" };
string joined = string.Join(" ", words);  // "Hello Rijoan Maruf"

// Empty/null checks
bool isEmpty = string.IsNullOrEmpty(text);  // false
bool isWhiteSpace = string.IsNullOrWhiteSpace(text);  // false

// String comparison
bool areEqual = string.Equals("rijoan", "RIJOAN", StringComparison.OrdinalIgnoreCase);  // true
```

## Control Flow - If/Else

```csharp
int age = 18;

// Simple if
if (age >= 18)
{
    Console.WriteLine("You are an adult");
}

// If-else
if (age >= 18)
{
    Console.WriteLine("You are an adult");
}
else
{
    Console.WriteLine("You are a minor");
}

// If-else if-else
if (age < 13)
{
    Console.WriteLine("Child");
}
else if (age < 18)
{
    Console.WriteLine("Teenager");
}
else
{
    Console.WriteLine("Adult");
}

// Nested if
if (age >= 18)
{
    if (age < 65)
    {
        Console.WriteLine("Working age adult");
    }
    else
    {
        Console.WriteLine("Senior");
    }
}

// Ternary operator
string status = (age >= 18) ? "Adult" : "Minor";
```

## Loops

### For Loop
```csharp
// Basic for loop
for (int i = 0; i < 5; i++)
{
    Console.WriteLine(i);  // 0, 1, 2, 3, 4
}

// Nested for loop
for (int i = 0; i < 3; i++)
{
    for (int j = 0; j < 3; j++)
    {
        Console.WriteLine($"{i},{j}");
    }
}

// For loop with multiple counters
for (int i = 0, j = 10; i < j; i++, j--)
{
    Console.WriteLine($"{i} {j}");  // 0 10, 1 9, 2 8, 3 7, 4 6
}
```

### While Loop
```csharp
// Basic while loop
int count = 0;
while (count < 5)
{
    Console.WriteLine(count);  // 0, 1, 2, 3, 4
    count++;
}

// Infinite loop with break
int i = 0;
while (true)
{
    Console.WriteLine(i);
    i++;
    if (i >= 5)
        break;  // Exit loop when i is 5
}
```

### Do-While Loop
```csharp
// Basic do-while loop (executes at least once)
int num = 0;
do
{
    Console.WriteLine(num);  // 0, 1, 2, 3, 4
    num++;
} while (num < 5);

// Do-while with break
int j = 0;
do
{
    Console.WriteLine(j);
    j++;
    if (j == 3)
        break;  // Exit when j is 3
} while (j < 5);
```

### Foreach Loop
```csharp
// Iterating through an array
string[] names = { "John", "Mary", "Tom" };
foreach (string name in names)
{
    Console.WriteLine(name);
}

// Iterating through a list
List<int> numbers = new List<int> { 1, 2, 3, 4, 5 };
foreach (int number in numbers)
{
    Console.WriteLine(number);
}
```

## Methods (Functions)

### Method Declaration
```csharp
// Basic method with no parameters and no return value
void SayHello()
{
    Console.WriteLine("Hello!");
}

// Method with parameters and return value
int Add(int a, int b)
{
    return a + b;
}

// Method with default parameters
void Greet(string name, string greeting = "Hello")
{
    Console.WriteLine($"{greeting}, {name}!");
}

// Method with output parameters
bool TryDivide(int dividend, int divisor, out int result)
{
    if (divisor == 0)
    {
        result = 0;
        return false;
    }
    result = dividend / divisor;
    return true;
}

// Method with reference parameters
void Swap(ref int a, ref int b)
{
    int temp = a;
    a = b;
    b = temp;
}

// Method with variable number of parameters
int Sum(params int[] numbers)
{
    int total = 0;
    foreach (int num in numbers)
    {
        total += num;
    }
    return total;
}
```

### Method Calling
```csharp
// Calling methods
SayHello();  // Hello!
int sum = Add(5, 3);  // 8

// Calling method with named arguments
Greet(name: "Rijoan Maruf");  // Hello, Rijoan Maruf!
Greet(name: "Rijoan Maruf", greeting: "Hi");  // Hi, Rijoan Maruf!

// Using out parameter
bool success = TryDivide(10, 2, out int result);
if (success)
{
    Console.WriteLine($"Result: {result}");  // Result: 5
}

// Using ref parameter
int x = 5, y = 10;
Swap(ref x, ref y);  // x becomes 10, y becomes 5

// Using params
int total = Sum(1, 2, 3, 4, 5);  // 15
```

### Method Overloading
```csharp
// Method overloading (same name, different parameters)
int Add(int a, int b)
{
    return a + b;
}

double Add(double a, double b)
{
    return a + b;
}

int Add(int a, int b, int c)
{
    return a + b + c;
}
```
