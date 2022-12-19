---
Tags: ead notes completed
---
Links: [[EAD|HomePage]]

# C# Compilation Process
 **[[CS Compilation Process|Read Here]]**
 
## Simple Program
```CS
using System;

class MyProgram
{
	static void Main(String[] args)
	{
		Console.WriteLine("Halo From here");
	}
}
//MyProgram.c
```
`$ csc MyProgram.c && MyProgram.exe` -> `Halo From here`

<u>There are two ways to get user input:</u>
1. Using command line arguments e.g. executable.exe 4 6
2. Using `Console.ReadLine()` or `Console.ReadKey()`

## Command Line Arguments
```cs
using System;

class MyProgram
{
	static void Main(String[] args)
	{
		Console.Write(args[0]);
		Console.Write(args[1]);
		...
	}
}
//MyProgram.cs
```
`$ csc MyProgram.c && MyProgram.exe Ahm ad` -> `Ahmad`

## Using Command
```cs
using System; 

class MyProgram
{
	static void Main(String[] args)
	{
		Console.Write("Enter name: ");
		String name = Console.ReadLine();
		Console.Write("Enter Roll no: ");
		String roll = Console.ReadLine();
		Console.Write("Enter CGPA: ");
		String cgpa = Console.ReadLine();
		Console.WriteLine("Name: " + name);
		Console.WriteLine("Roll: " + roll);
		Console.WriteLine("Cgpa: " + cgpa);
	}
}
//MyProgram.cs
```

## Console.ReadKey Method
Obtains the next character or function key pressed by the user.
#### Overloads
| Signature | Functionality                                                                                                       |
| --------- | ------------------------------------------------------------------------------------------------------------------- |
| `ReadKey()` | Obtains the next character or function key pressed by the user. The pressed key is *displayed* in the console window. |
| `ReadKey(Boolean)` | Obtains the next character or function key pressed by the user. The pressed key is *optionally displayed* in the console window. `true` to not display the pressed key; otherwise, `false`.                                                                           |

#### Returns
`ConsoleKeyInfo`

An object that describes the `ConsoleKey` constant and Unicode character, if any, that correspond to the pressed console key. The `ConsoleKeyInfo` object also describes, in a bitwise combination of `ConsoleModifiers` values, whether **one or more** Shift, Alt, or Ctrl modifier keys was pressed *simultaneously with the console key.*


#### Example
One of the most common uses of the `ReadKey()` method is to halt program execution until the user presses a key and the app either terminates or displays an additional window of information. *The following example uses the `ReadKey()` method to display information about which key the user pressed.*
```cs
using System;

class Example
{
   public static void Main()
   {
      ConsoleKeyInfo cki;
      // Prevent example from ending if CTL+C is pressed.
      Console.TreatControlCAsInput = true;

      Console.WriteLine("Press any combination of CTL, ALT, and SHIFT, and a console key.");
      Console.WriteLine("Press the Escape (Esc) key to quit: \n");
      do
      {
         cki = Console.ReadKey();
         Console.Write(" --- You pressed ");
         if((cki.Modifiers & ConsoleModifiers.Alt) != 0) Console.Write("ALT+");
         if((cki.Modifiers & ConsoleModifiers.Shift) != 0) Console.Write("SHIFT+");
         if((cki.Modifiers & ConsoleModifiers.Control) != 0) Console.Write("CTL+");
         Console.WriteLine(cki.Key.ToString());
       } while (cki.Key != ConsoleKey.Escape);
    }
}
// This example displays output similar to the following:
//       Press any combination of CTL, ALT, and SHIFT, and a console key.
//       Press the Escape (Esc) key to quit:
//
//       a --- You pressed A
//       k --- You pressed ALT+K
//       ► --- You pressed CTL+P
//         --- You pressed RightArrow
//       R --- You pressed SHIFT+R
//                --- You pressed CTL+I
//       j --- You pressed ALT+J
//       O --- You pressed SHIFT+O
//       § --- You pressed CTL+U
```


## Creating a .dll file
By default access modifier of a class is `internal` meaning that  it is only visible with in it's assembly. We need to ensure that class of a library(.dll) is public. You will need to do it little different in Visual Studio *(Not fun).* [Add Reference]
```cs
Public class MyLibrary
{
	public int add(int a, int b)
	{
		return a + b;
	}
}
//MyLibrary.cs
```
`$ csc /target:library MyLibrary.cs` -> `MyLibrary.dll`

## Using .dll in a .exe
```CS
using System;

class MyProgram
{
	static void Main(String[] args)
	{
		MyLibrary obj = new MyLibrary();
		int result = obj.add(33, 36);
		Console.WriteLine(result);
	}
}
//MyProgram.cs
```
`$ csc /reference:MyLibrary.dll MyProgram.c && MyProgram.exe` -> `69`

## Arguments
In C#, arguments are generally passed by *value* by default. This means that when a method is called with an argument, a copy of the value of the argument is made and passed to the method. The method operates on the copy, and any changes made to the argument within the method do not affect the original value.

However, it is also possible to pass arguments by reference in C# by using the `ref` or `out` keywords. When an argument is passed by reference, a reference to the memory location of the argument is passed to the method, rather than a copy of the value. This means that the method can modify the original value of the argument directly, and the changes will be reflected in the calling code.

```cs
void Increment(ref int x)
{
    x++;
}

// To call this method and pass an argument by reference, you would use the ref keyword like this:

int y = 5;
Increment(ref y);

// After this code runs, the value of `y` will be 6.
```
It is important to be careful when using the `ref` and `out` keywords, as passing arguments by reference can make the code more difficult to understand and can increase the risk of *unintended side effects.* It is generally best to use these keywords only when they are necessary to achieve the desired behavior in the code.


## Circular Reference
A circular reference is when an object contains a *reference to itself.* This can happen in C# when an object contains a reference to another object which contains a reference back to the first object. This can cause problems because it can create a loop that is never broken and can cause the program to crash.

## Type Casting
```cs
using System;

class MyProgram
{
	static void Main(String[] args)
	{
		int cgpa = int.Parse(Console.ReadLine());
		int marks = System.Convert.int32(Console.ReadLine());
	}
}
//MyProgram.cs
```


## Object Intializer
In C#, object initializers allow you to create and initialize an object in a single statement. They provide a *concise syntax* for creating and initializing objects without having to explicitly call a constructor and set the object's properties individually.

```cs
class Point
{
    public int X { get; set; }
    public int Y { get; set; }
}

Point point = new Point { X = 10, Y = 20 };

```
## parmas keywords
By using the `params` keyword, you can specify a *method parameter* that takes a variable number of arguments. The parameter type must be a single-dimensional array.

No additional parameters are permitted after the `params` keyword in a method declaration, and only one `params` keyword is permitted in a method declaration.

When you call a method with a `params` parameter, you can pass in:

-   A comma-separated list of arguments of the type of the array elements.
-   An array of arguments of the specified type.
-   No arguments. If you send no arguments, the length of the `params` list is zero.

```cs
public void PrintNumbers(params int[] numbers)
{
    foreach (int number in numbers)
    {
        Console.WriteLine(number);
    }
}

PrintNumbers(1, 2, 3, 4, 5);

int[] numbers = { 1, 2, 3, 4, 5 };
PrintNumbers(numbers);
// the array of integers is automatically expanded and passed as individual arguments to the method.
```


# To Dos
- [x] Set up VS and stuff
<br>
```chartsview
#-----------------#
#- chart type    -#
#-----------------#
type: WordCloud

#-----------------#
#- chart data    -#
#-----------------#
data: "wordcount:Compilation Process"

#-----------------#
#- chart options -#
#-----------------#
options:
  wordField: "word"
  weightField: "count"
  colorField: "count"
  wordStyle:
    rotation: 30
```
<br>

Created: 2022-10-20