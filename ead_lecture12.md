---
Tags: toProcess ead
---
Links: [[EAD|HomePage]]
# LINQ (**L**anguage **I**ntegrated **Q**ueries) 

`Language-Integrated Query `(*LINQ*) is a set of features introduced in Visual Studio 2008 that extends powerful query capabilities to the language syntax of C# and Visual Basic. LINQ introduces standard, easily-learned patterns for querying and updating data, and the technology can be extended to support potentially any kind of data store.

<u>There are many benefits of *LINQ*, some of which are listed below:</u>

1. **LINQ** simplifies the process of querying data from various data sources.
2. **LINQ** is more efficient and concise as compared to traditional querying techniques.
3. **LINQ** makes it easier to maintain and update application code.
4. **LINQ** offers better performance by optimizing the query execution process.

![[LINQ]]

#### Example

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

        var query2 = from c in cities
                     where c.Length > 6
                     select c;

        // 3. Process Query
        foreach (var c in query)
            Console.WriteLine(c);
    }
}



```
**Output:** `Islamabad`

##### Example-2
```cs
using System;
using System.Linq;

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
    }
}
```
---
Created: 2022-11-29