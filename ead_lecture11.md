---
Tags: toProcess delegate
---
Links: [[EAD Lectures]]
# Delegates

They are used to refer functions.

`delegate void Delegate();` 
Can refer to the functions with void return type and no parameters.

`delegate void Delegate(string s);` 
Can refer to the functions with void return type and take one string parameter.

```cs
using System;


class MyProgram
{
    delegate void Delegate();

    delegate void DelegateString(string s);

    delegate int DelegateInt(int a, int b);

    static void display()
    {
        Console.WriteLine("No Paramter");
    }

    static void display(string s)
    {
        Console.WriteLine("string Paramter");
    }

    static int DoStuff(int a, int b)
    {
        return a + b;
    }

    static void MagicFunc(DelegateInt fun, int a, int b)
    {
        Console.WriteLine(fun(a, b));

    }

    public static void Main()
    {
        Delegate d1 = new Delegate(display);
        d1.Invoke();

        DelegateString d2 = display;
        d2("Hey how you doing?");

        DelegateInt func = DoStuff;

        MagicFunc(func, 33, 36);

        MagicFunc((a,b)=>a-b, 99, 30);
    
        DelegateInt function = delegate (int a, int b)
        {
            return a + b;
        };

        Console.WriteLine(function(10, 10));
    }
}

```

## `Static` VS `const` vs `ReadOnly`

| `Static` | `Constant` | `ReadOnly` |
| ------ | -------- | -------- |
| The information we need to keep at *class level.* i.e Same for all instance of the class        | The `static` information that we know at **compile time** and doesn't change in the program, we use `constant`| <mark style="background: #FF5582A6;">Need to Fill in Something here</mark> |


----

Created: 2022-11-24