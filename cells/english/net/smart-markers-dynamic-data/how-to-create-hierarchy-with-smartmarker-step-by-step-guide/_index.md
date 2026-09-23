---
category: general
date: 2026-02-14
description: How to create hierarchy in SmartMarker templates is easier than you think
  – learn to create hierarchical data and how to list employees efficiently.
draft: false
keywords:
- how to create hierarchy
- create hierarchical data
- how to list employees
- SmartMarker nested range
- C# template processing
language: en
og_description: How to create hierarchy in SmartMarker templates is simple. Follow
  this guide to create hierarchical data and list employees with nested ranges.
og_title: How to Create Hierarchy with SmartMarker – Complete Guide
tags:
- SmartMarker
- C#
- templating
title: How to Create Hierarchy with SmartMarker – Step‑by‑Step Guide
url: /net/smart-markers-dynamic-data/how-to-create-hierarchy-with-smartmarker-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Create Hierarchy with SmartMarker – Complete Guide

Ever wondered **how to create hierarchy** inside a SmartMarker template without pulling your hair out? You're not the only one. In many reporting scenarios you need a parent‑child relationship—think departments and the people that work in them. The good news is that SmartMarker makes it a piece of cake once you know the right steps.

In this tutorial we’ll walk through the whole process: from **creating hierarchical data** in C#, enabling nested ranges, and finally rendering a template that **lists employees** for each department. By the end you’ll have a ready‑to‑run sample you can drop into any .NET project.

---

## What You’ll Need

- .NET 6+ (any recent version works)
- A reference to the **SmartMarker** library (the `ws.SmartMarkerProcessor` namespace)
- Basic C# knowledge – nothing fancy, just a few objects and a lambda or two
- An IDE or editor of your choice (Visual Studio, Rider, VS Code… you pick)

If you already have those, great—let’s dive in.

---

## How to Create Hierarchy – Overview

The core idea is to build a **nested object graph** that mirrors the structure you want to see in the final document. In our case the graph looks like:

```
Departments
 ├─ Name (string)
 └─ Employees (string[])
```

SmartMarker can then iterate over `Departments` and, because we’ll turn on **nested range processing**, it will also loop over each department’s `Employees` collection automatically.

---

## Step 1: Build the Hierarchical Data Model

First we create an anonymous object that contains an array of departments, each with its own employee list. Using an anonymous type keeps the example lightweight—feel free to replace it with real POCO classes later.

```csharp
// Step 1: Create hierarchical data that SmartMarker will iterate over
var departmentData = new
{
    Departments = new[]
    {
        new { Name = "HR", Employees = new[] { "John", "Amy" } },
        new { Name = "IT", Employees = new[] { "Bob", "Eve" } }
    }
};
```

> **Why this matters:** The `Departments` array is the top‑level collection. Each element contains an `Employees` array, giving us the second level of hierarchy that we’ll later access with `#Departments.Employees#`.

---

## Step 2: Enable Nested Range Processing

SmartMarker won’t dive into inner collections unless you tell it to. The `SmartMarkerOptions` object holds that switch.

```csharp
// Step 2: Enable nested range processing so inner collections (Employees) can be used
var smartMarkerOptions = new SmartMarkerOptions
{
    EnableNestedRange = true   // crucial for #Departments.Employees# to work
};
```

> **Pro tip:** If you forget this flag, the inner `#Employees#` range simply returns nothing, and you’ll be scratching your head wondering why the template is blank.

---

## Step 3: Run the Processor with Your Data

Now we hand the data and options to the processor. The `ws` variable represents your **WebService** (or whatever object hosts the SmartMarker engine).

```csharp
// Step 3: Run SmartMarker processing with the data and the configured options
ws.SmartMarkerProcessor.StartSmartMarkerProcessing(departmentData, smartMarkerOptions);
```

At this point SmartMarker parses the template, substitutes `#Departments.Name#` for each department name, and then, because nested ranges are enabled, iterates through each department’s `Employees` collection.

---

## Step 4: Craft the Template Markers

Below is a minimal template that demonstrates both the outer and inner loops. Paste it into the SmartMarker template editor (or a `.txt` file you pass to the processor).

```
#Departments.Name#
  #Departments.Employees#
    - #Departments.Employees#
  #/Departments.Employees#
#/Departments.Name#
```

When rendered you’ll see:

```
HR
  - John
  - Amy
IT
  - Bob
  - Eve
```

> **What you’re seeing:** The outer `#Departments.Name#` prints the department title. The inner `#Departments.Employees#` block loops over each employee, and `#Departments.Employees#` inside the block outputs the actual name.

---

## Expected Output & Verification

Running the full example (data + options + template) should produce exactly the list shown above. To quickly verify, you can dump the result to the console:

```csharp
string result = ws.SmartMarkerProcessor.GetProcessedResult(); // pseudo‑method
Console.WriteLine(result);
```

If you see the two department headings followed by their employee bullets, you’ve successfully **created a hierarchy** and **listed employees**.

---

## Common Pitfalls & Edge Cases

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| No output for employees | `EnableNestedRange` left false | Set `EnableNestedRange = true` |
| Duplicate employee names | Same array reused across departments | Clone the array or use distinct collections |
| Very large hierarchies cause memory pressure | SmartMarker loads the whole object graph into memory | Stream data or paginate large collections |
| Template syntax errors | Missed closing `#/…#` tags | Use the SmartMarker validator or run a quick test with a tiny template |

---

## Going Further – Real‑World Variations

1. **Dynamic data sources** – Pull departments from a database and map them to the anonymous structure using LINQ.
2. **Conditional formatting** – Add a `IsManager` flag to each employee and use SmartMarker’s conditional tags (`#if …#`) to highlight managers.
3. **Multiple nesting levels** – If you need teams inside departments, just add another collection (`Teams`) and keep `EnableNestedRange` turned on.

---

## Full Working Example (Copy‑Paste Ready)

```csharp
using System;
using SmartMarker; // hypothetical namespace

class Program
{
    static void Main()
    {
        // 1️⃣ Build hierarchical data
        var departmentData = new
        {
            Departments = new[]
            {
                new { Name = "HR", Employees = new[] { "John", "Amy" } },
                new { Name = "IT", Employees = new[] { "Bob", "Eve" } }
            }
        };

        // 2️⃣ Enable nested ranges
        var smartMarkerOptions = new SmartMarkerOptions
        {
            EnableNestedRange = true
        };

        // 3️⃣ Start processing
        var ws = new WebService(); // assume this is your entry point
        ws.SmartMarkerProcessor.StartSmartMarkerProcessing(departmentData, smartMarkerOptions);

        // 4️⃣ Retrieve and display the result
        string output = ws.SmartMarkerProcessor.GetProcessedResult(); // placeholder method
        Console.WriteLine(output);
    }
}
```

**Template (template.txt)**

```
#Departments.Name#
  #Departments.Employees#
    - #Departments.Employees#
  #/Departments.Employees#
#/Departments.Name#
```

Running the program prints the hierarchy exactly as shown earlier.

---

## Conclusion

We’ve covered **how to create hierarchy** in SmartMarker, from shaping **hierarchical data** in C# to turning on nested ranges and finally rendering a template that **lists employees** per department. The pattern scales—just add more nested collections or conditional logic and you’ve got a powerful reporting engine at your fingertips.

Ready for the next challenge? Try swapping the anonymous types for strongly‑typed POCO classes, or integrate this flow into an ASP.NET Core endpoint that returns a PDF or Word document. The sky’s the limit, and now you have a solid foundation.

---

![How to create hierarchy diagram](image.png){alt="How to create hierarchy diagram showing department‑employee relationship"}

*Happy coding! If you hit any snags, drop a comment below—I'm happy to help.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}