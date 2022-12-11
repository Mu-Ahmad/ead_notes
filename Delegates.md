---
Tags: complete delegate lec11
---
Links: [[EAD Lectures|HomePage]]
# Delegates
The `delegate` is a reference type data type that defines the method signature. You can define variables of delegate, just like other data type, that can refer to any *method with the same signature* as the delegate. Delegates in .net are the objects which represents the methods. Delegates are used to pass methods as parameters. Delegate is a type safe function pointer. 

<u>There are three steps involved while working with delegates:</u> 
1.  Declare a delegate
2.  Set a target method
3.  Invoke a delegate

A delegate can be declared using the `delegate` keyword followed by a function signature, as shown below.
```ad-note
title: Syntax
`[access modifier] delegate [return type] [delegate name]([parameters])`
```
==> `public delegate void Delegate();`  Can refer to the functions with void return type and no parameters.
==> `public delegate void Delegate(string s);`  Can refer to the functions with void return type and take one string parameter.

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

## `static` VS `const` vs `readonly`
`const`, `readonly` and `static` are keywords that are nearly the same in behavior but when we talk about their functioning they are all different.

| `static` | `const` | `readonly` |
| ------ | -------- | -------- |
| The information we need to keep at *class level.* i.e Same for all instance of the class. The static keyword can be used effectively with classes, fields, operators, events, methods and so on effectively.      | Constant fields are defined at the time of declaration in the code snippet, because once they are defined they can't be modified. By default a constant is static, so you can't define them static from your side.It is also mandatory to assign a value to them at the time of declaration otherwise it will give an error during compilation of the program. That's why it is also called a *compile-time constant.*| A Readonly field can be initialized either at the time of declaration or within the constructor of the same class. We can also change the value of a Readonly at runtime or assign a value to it at runtime (but in a non-static constructor only). For that reason a Readonly field is also called a *run-time constant.* It can be static.|

### Key points about Static keyword
1.  If the static keyword is *applied to a class*, all the members of the class must be static. 
2.  Static methods can only access static members of the same class. Static properties are used to get or set the value of static fields of a class. 
3.  A static constructor can't be parameterized. Access modifiers cannot be applied on Static constructor, it is always a *public default constructor* which is used to initialize static fields of the class.


----

Created: 2022-11-24