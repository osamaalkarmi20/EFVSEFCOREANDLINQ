# Report on: Entity Framework and Linq

---
**Entity Framework**: is framework to automate all these database related activities for your application.

Entity Framework is an open-source ORM framework for .NET applications supported by Microsoft. It enables developers to work with data using objects of domain specific classes without focusing on the underlying database tables and columns where this data is stored. With the Entity Framework, developers can work at a higher level of abstraction when they deal with data, and can create and maintain data-oriented applications with less code compared with traditional applications.


**CRUD** stands for **Create, Read, Update, and Delete**. These are the basic operations you can perform on data in a database. 
CRUD operations using Entity Framework Core:

1. **Create** (Insert a new record):
   ```csharp
   using (var context = new ApplicationDbContext())
   {
       var newEntity = new MyEntity { Name = "New Item" };
       context.MyEntities.Add(newEntity);
       context.SaveChanges();
   }
   ```
   - This code creates a new instance of `MyEntity`, adds it to the `MyEntities` DbSet, and saves the changes to the database.

2. **Read** (Retrieve records):
   ```csharp
   using (var context = new ApplicationDbContext())
   {
       var entities = context.MyEntities.ToList();
       foreach (var entity in entities)
       {
           Console.WriteLine(entity.Name);
       }
   }
   ```
   - This code retrieves all records from the `MyEntities` table and prints their names.

3. **Update** (Modify an existing record):
   ```csharp
   using (var context = new ApplicationDbContext())
   {
       var entity = context.MyEntities.FirstOrDefault(e => e.Id == 1);
       if (entity != null)
       {
           entity.Name = "Updated Item";
           context.SaveChanges();
       }
   }
   ```
   - This code finds the first entity with an `Id` of 1, updates its name, and saves the changes to the database.

4. **Delete** (Remove a record):
   ```csharp
   using (var context = new ApplicationDbContext())
   {
       var entity = context.MyEntities.FirstOrDefault(e => e.Id == 1);
       if (entity != null)
       {
           context.MyEntities.Remove(entity);
           context.SaveChanges();
       }
   }
   ```
   - This code finds the first entity with an `Id` of 1, removes it from the `MyEntities` DbSet, and saves the changes to the database.

These examples show the basic CRUD operations using Entity Framework Core. Each operation involves interacting with the `DbContext` to manage the data in your database. 

**Entity Framework (EF) vs. Entity Framework Core (EF Core)**

**Entity Framework (EF)**:
- **Versions**: Entity Framework was initially introduced as part of the .NET Framework, with versions up to EF 6 designed primarily for the .NET Framework.
- **Database Support**: EF 6 and earlier versions primarily support traditional relational databases such as SQL Server, MySQL, and Oracle.
- **Dependencies**: EF 6 and its predecessors are closely tied to the full .NET Framework and are typically used within applications built on top of the .NET Framework.

**Entity Framework Core (EF Core)**:
- **Cross-Platform**: EF Core is a lightweight, cross-platform version of Entity Framework, specifically designed for .NET Core and later versions (.NET 5, .NET 6, etc.). It can operate on various platforms, including Windows, Linux, and macOS.
- **Modularity**: EF Core has been rearchitected to be more modular and extensible, making it suitable for a wider range of scenarios and application types.
- **Performance**: EF Core has been optimized for performance and resource usage, addressing some of the performance issues found in earlier versions of Entity Framework.
- **New Features**: EF Core introduces new features and improvements not found in EF 6, including enhanced LINQ support, improved querying capabilities, and support for NoSQL databases in certain scenarios.

**Comparison**:
- **Entity Framework (EF)** refers to the older versions designed for the .NET Framework.
- **Entity Framework Core (EF Core)** is the modern, cross-platform ORM specifically designed for .NET Core and later versions.
- Both frameworks provide object-relational mapping capabilities, allowing developers to work with databases using object-oriented paradigms. However, EF Core is more lightweight, modular, and compatible with the cross-platform .NET Core ecosystem.
- As of .NET 5 and beyond, EF Core is the recommended ORM for new .NET applications.

---


**LINQ (Language Integrated Query)** is a powerful feature in .NET that allows you to query collections of data in a more readable and concise way. Think of it as a way to write SQL-like queries directly in your C# code. 

With LINQ, you can perform operations like filtering, sorting, and grouping on arrays, lists, and other collections. It makes your code cleaner and easier to understand. For example, instead of writing complex loops to find specific items in a list, you can use LINQ to do it in a single line.

Here's a quick example to give you an idea:

```csharp
List<int> numbers = new List<int> { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 };

// Find all even numbers
var evenNumbers = numbers.Where(n => n % 2 == 0).ToList();
```

In this example, `Where` is a LINQ method that filters the list to include only even numbers. It's simple, right?

LINQ can be used with various data sources, including databases, XML documents, and in-memory collections. It helps you write more efficient and maintainable code by abstracting the data querying process.

---

**Understanding the Skip() and Take() Methods in LINQ**

The `Take()` method extracts the first `n` elements (where `n` is a parameter to the method) from the beginning of the target sequence and returns a new sequence containing only the elements taken.

Conversely, the `Skip()` method can be thought of as the exact opposite of the `Take()` method. While the `Take()` method returns a sequence containing the first `n` elements of the target sequence, the `Skip()` method "skips" over the first `n` elements in the sequence and returns a new sequence containing the remaining elements after the first `n` elements.

To better understand these methods, you can explore a simple game (task) on the following website: [Codingame - Skip and Take](https://www.codingame.com/playgrounds/213/using-c-linq---a-practical-overview/skip-and-take).



***This is the solution for the task:***

```csharp
using System.Collections.Generic;
using System.Linq;

namespace MultipleValue1
{
    public static class SkipTake1
    {
        // Return the 3rd, 4th, and 5th items of the provided sequence.
        public static IEnumerable<string> GetThirdFourthFifthItems(IEnumerable<string> words)
        {
            var wordList = words.ToList();
            var result = wordList.Skip(2).Take(3);
            return result;
        }
    }
}
```

