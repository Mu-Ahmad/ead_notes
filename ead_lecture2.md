---
Tags: ead notes complete
---
Links: [[EAD|HomePage]]

# C# Compilation Process
 **[[ead_lecture1|Read Here]]**
 
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

An object that describes the `ConsoleKey` constant and Unicode character, if any, that correspond to the pressed console key. The `ConsoleKeyInfo` object also describes, in a bitwise combination of `ConsoleModifiers` values, whether **one or more** *Shift*, *Alt*, or Ctrl *modifier* keys was pressed *simultaneously with the console key.*


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
By default access modifier of a class is `internal` meaning 
that  it is only visible with in it's assembly. We need to ensure that class of a library(.dll) is public. You will need to do it little different in Visual Studio (Not fun).
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
data: "wordcount:ead_lecture2"

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