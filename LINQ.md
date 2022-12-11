---
Tags: completed ead lec12
---
Links: [[EAD|HomePage]] [SampleQueries](https://www.tutorialsteacher.com/linq/sample-linq-queries)
# LINQ (**L**anguage **I**ntegrated **Q**ueries) 

`Language-Integrated Query `(*LINQ*) is a set of features introduced in Visual Studio 2008 that extends powerful query capabilities to the language syntax of C# and Visual Basic. LINQ introduces standard, easily-learned patterns for querying and updating data, and the technology can be extended to support potentially any kind of data store. 
LINQ queries uses extension methods for classes that implement `IEnumerable` or `IQueryable` interface. The  `Enumerable`  and  `Queryable`   are  two static classes that contain extension methods to write LINQ queries.

![[Excalidraw/LINQ]]

##### NameSpace
`System.Linq`

#### <u>Writing a **LINQ** query is typically a four-step process:</u>

1. Identify the data source. 
2. Identify the type of data you want to retrieve from the data source. 
3. Write the query. 
4. Execute the query.

#### <u>There are many benefits of **LINQ**, some of which are listed below:</u>

1. **LINQ** simplifies the process of querying data from various data sources.
2. **LINQ** is more efficient and concise as compared to traditional querying techniques.
3. **LINQ** makes it easier to maintain and update application code.
4. **LINQ** offers better performance by optimizing the query execution process.

#### <u>There are a few potential drawbacks to using **LINQ**:</u>

1. **LINQ** syntax can be confusing and difficult to read, especially for complex queries.
2. **LINQ** queries can be slow, especially when compared to traditional SQL queries.
3. **LINQ** can be difficult to debug, since the query syntax is not always obvious.
4. **LINQ** is not always supported by all data sources.

#### <u>There are three ways in which you can write a **LINQ** query in C#:</u>
1.  Use query syntax.
2.  Use method syntax.
3.  Use a combination of query syntax and method syntax.
```ad-note
- Some query operations, such as `Count` or `Max`, have no equivalent query expression clause and must therefore be expressed as a *method call*.
- `ToList()` extension method executes the query immediately and returns the result.
```

#### Method Syntax
Method syntax (also known as fluent syntax) uses extension methods included in the `Enumerable` or `Queryable` static class, similar to how you would call the extension method of any class.


```cs
using System;
using System.Linq;

class MyProgram
{
    static void Main()
    {
        // 1. Define the Data Source
        var cities = new String[] {"Lahore", "Islamabad", "Kasur", "Peshawar", "Sialkot", "karachi", "Istanbol"};

        // 2. Define the Query
        var query = cities.Where((str)=>str.Length>6).Where((str)=>str[0]=='I').Select(n=>n.Substring(0,4));

        // 3. Process Query
        foreach (var c in query)
            Console.WriteLine(c);
    }
}



```
**Output:** `Islamabad`

#### Query Syntax
Query syntax is similar to SQL for the database.

```ad-info
title: LINQ Query Syntax
```cs
from <range variable> in <IEnumerable<T> or IQueryable<T> Collection>

<Standard Query Operators> <lambda expression>

<select or groupBy operator> <result formation>
```

The LINQ query syntax starts with `from` keyword and ends with `select` keyword.

```cs
using System;
using System.Linq;
using System.Collections;
using System.Collections.Generic;

class MyProgram
{

    class EmailAddress
    {
        public string Name {get; set;}

        public string Adress {get; set; }
    }


    static void Main()
    {
        // 1. Define the Data Source
        var adresses = new EmailAddress[] {
            new EmailAddress {Name="Ahmad", Adress="abc"},
            new EmailAddress {Name="Ali", Adress="abc"},
            new EmailAddress {Name="Raheem", Adress="abc"},
        };

        // 2. Define the Query, We need to return object (anonymous classes are used) 
        var query2 = from c in adresses
                     select new {Name = c.Name, Adress = c.Adress};

        // 3. Process Query
        foreach (var c in query2)
            Console.WriteLine(c);

		// More Examples
		List<int> numbers = new() { 5, 4, 1, 3, 9, 8, 6, 7, 2, 0 };

        // Query #1.
        var filteringQuery =
            from num in numbers
            where num < 3 || num > 7
            select num;

        foreach (var element in filteringQuery)
            Console.Write(element + " ");
        Console.WriteLine();

        // Query #2.
        var orderingQuery =
            from num in numbers
            where num < 3 || num > 7
            orderby num ascending
            select num;

        foreach (var element in orderingQuery)
            Console.Write(element + " ");
        Console.WriteLine();

        // Query #3.
        string[] groupingQuery = { "carrots", "cabbage", "broccoli", "beans", "barley" };
        var queryFoodGroups =
            from item in groupingQuery
            group item by item[0];

        foreach (var element in queryFoodGroups)
        {
            foreach (var x in element)
                Console.Write(x + " ");
            Console.WriteLine();
        }
		
    }
}
```

#### Standard Query Operators
Standard Query Operators in LINQ are actually extension methods for the `IEnumerable<T> and IQueryable<T>` types. They are defined in the `System.Linq.Enumerable` and `System.Linq.Queryable` classes. There are over 50 standard query operators available in LINQ that provide different functionalities like filtering, sorting, grouping, aggregation, concatenation, etc.
```ad-note
- Standard query operators in *query syntax* is converted into extension methods at *compile time.* So both are same.
```


**<u>The following table lists all the classification of Standard Query Operators:</u>**

| Classification | Standard Query Operators                                                                           |
| -------------- | -------------------------------------------------------------------------------------------------- |
| Filtering      | Where, OfType                                                                                      |
| Sorting        | OrderBy, OrderByDescending, ThenBy, ThenByDescending, Reverse                                      |
| Grouping       | GroupBy, ToLookup                                                                                  |
| Join           | GroupJoin, Join                                                                                    |
| Projection     | Select, SelectMany                                                                                 |
| Aggregation    | Aggregate, Average, Count, LongCount, Max, Min, Sum                                                |
| Quantifiers    | All, Any, Contains                                                                                 |
| Elements       | ElementAt, ElementAtOrDefault, First, FirstOrDefault, Last, LastOrDefault, Single, SingleOrDefault |
| Set            | Distinct, Except, Intersect, Union                                                                 |
| Partitioning   | Skip, SkipWhile, Take, TakeWhile                                                                   |
| Concatenation  | Concat                                                                                             |
| Equality       | SequenceEqual                                                                                      |
| Generation     | DefaultEmpty, Empty, Range, Repeat                                                                 |
| Conversion     | AsEnumerable, AsQueryable, Cast, ToArray, ToDictionary, ToList                                     |

---
Created: 2022-11-29