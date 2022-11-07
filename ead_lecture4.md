---
Tags: completed ead
---
Links: [[EAD|HomePage]]
# Properties
A `property` is a member that provides a flexible mechanism to read, write, or compute the value of a private field. Properties can be used as if they're public data members, but they're special methods called _accessors_. This feature enables data to be accessed easily and still helps promote the safety and flexibility of methods.
```ad-important
title: Encapsulation
Properties are a mean to achieve enacpsulation^[Encapsulation is a way to restrict the direct access to some components of an object, so users cannot access state values for all of the variables of a particular object.]. To achieve this, you must:
-   declare fields/variables as `private`
-   provide `public` `get` and `set` methods, through **properties**, to access and update the value of a `private` field
```
- `Properties` enable a class to expose a public way of getting and setting values, while hiding implementation or verification code.
- A `get` property accessor is used to return the property value, and a `set` property accessor is used to assign a new value. In *C# 9* and later, an `init` property accessor is used to assign a new value only during object construction. These accessors can have different access levels.
- The `value` keyword is used to define the value being assigned by the `set` or `init` accessor.
- Properties can be _read-write_ (they have both a `get` and a `set` accessor), _read-only_ (they have a `get` accessor but no `set` accessor), or _write-only_ (they have a `set` accessor, but no `get` accessor). Write-only properties are rare and are most commonly used to restrict access to sensitive data.

```cs
class Person
{
	private string name;
	private int age;
	
	public string Name 
	{
		get {return name;}	
		set {name = value;}
	}
	public int Age
	{
		get {return age;}
		set {age = value<0 ? 0 : value;}
	}
}

class Program
{
  static void Main(string[] args)
  {
    Person p = new Person();
    p.Name = "BabarxGoat";
    Console.WriteLine(p.Name);
  }
}

```

## Properties with backing fields
One basic pattern for implementing a property involves using a private backing field for setting and retrieving the property value. The `get` accessor returns the value of the private field, and the `set` accessor may perform some data *validation* before assigning a value to the private field. Both *accessors* may also perform some conversion or computation on the data before it's stored or returned.

The following example illustrates this pattern. In this example, the `TimePeriod` class represents an interval of time. Internally, the class stores the time interval in seconds in a private field named `seconds`. A *read-write* property named `Hours` allows the customer to specify the time interval in hours. Both the `get` and the `set` accessors perform the necessary conversion between hours and seconds. In addition, the set accessor validates the data and throws an `ArgumentOutOfRangeException`^[The exception that is thrown when the value of an argument is outside the allowable range of values as defined by the invoked method.] if the number of hours is invalid.
```cs
public class TimePeriod
{
    private double _seconds;

    public double Hours
    {
        get { return _seconds / 3600; }
        set
        {
            if (value < 0 || value > 24)
                throw new ArgumentOutOfRangeException(nameof(value),
                      "The valid range is between 0 and 24.");

            _seconds = value * 3600;
        }
    }
}
```

## Auto-implemented properties
In some cases, property `get` and `set` accessors just assign a value to or retrieve a value from a backing field without including any extra logic. By using auto-implemented properties, you can simplify your code while having the C# compiler transparently provide the backing field for you.
```cs
public class SaleItem
{
    public string Name
    { get; set; }

    public decimal Price
    { get; set; }
}
```

## Expression body definitions

Property accessors often consist of *single-line statements* that just assign or return the result of an expression. You can implement these properties as expression-bodied members. Expression body definitions consist of the <mark style="background: #D2B3FFA6;">=></mark> symbol followed by the expression to *assign* to or *retrieve* from the property.
```cs
class Person
{
	private int age;
	
	public string Name 
	{
		get; set;
	}
	public int Age
	{
		get => age;
		set => age = value<0 ? 0 : value;
	}
}
```




##   Required properties
Beginning with ***C# 11***, you can add the `required` member to force client code to initialize any property or field:
```cs
public class SaleItem
{
    public required string Name
    { get; set; }

    public required decimal Price
    { get; set; }
}
```
To create a `SaleItem`, you must set both the `Name` and `Price` properties using _object initializers_^[Object initializers let you assign values to any accessible fields or properties of an object at creation time without having to invoke a constructor followed by lines of assignment statements.], as shown in the following code:
```cs
var item = new SaleItem { Name = "Shoes", Price = 19.95m };
Console.WriteLine($"{item.Name}: sells for {item.Price:C2}");
```



---
**~~lecture cut short~~**
---

> Every time you smile at someone, it is an action of love, a gift to that person, a beautiful thing.
> — <cite>Mother Teresa</cite>
---


```chartsview
#-----------------#
#- chart type    -#
#-----------------#
type: WordCloud

#-----------------#
#- chart data    -#
#-----------------#
data: "wordcount:ead_lecture4"

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

Created: 2022-10-27