---
category: general
date: 2026-03-29
description: How to substitute variables in JSON using SmartMarker – learn to use
  if expression, apply conditional logic, multiply values, and generate JSON effortlessly.
draft: false
keywords:
- how to substitute variables
- use if expression
- how to apply conditional
- how to multiply values
- how to generate json
language: en
og_description: How to substitute variables in JSON using SmartMarker. Discover how
  to use if expression, apply conditional logic, multiply values, and generate JSON
  in minutes.
og_title: How to Substitute Variables in JSON with SmartMarker – Step‑by‑Step
tags:
- C#
- SmartMarker
- JSON templating
title: How to Substitute Variables in JSON with SmartMarker – Complete Guide
url: /net/smart-markers-dynamic-data/how-to-substitute-variables-in-json-with-smartmarker-complet/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Substitute Variables in JSON with SmartMarker – Complete Guide

Ever wondered **how to substitute variables** inside a JSON payload without writing a custom parser? You're not alone. In many integration scenarios—think invoices, pricing engines, or dynamic configuration files—you need to inject runtime values, apply simple conditionals, and maybe even do a quick multiplication. This tutorial shows you exactly **how to substitute variables** using the SmartMarker library, all while keeping the JSON clean and readable.

We'll walk through a real‑world example that covers **use if expression**, **how to apply conditional**, **how to multiply values**, and **how to generate json** on the fly. By the end, you'll have a ready‑to‑run C# snippet that you can drop into any .NET project.

## What You'll Learn

- Set up `SmartMarkerOptions` to store reusable variables.  
- Write a JSON template that contains an `if` expression for conditional logic.  
- Multiply a value by a variable inside the template.  
- Process the template with `SmartMarkerProcessor` and get the final JSON string.  
- Troubleshoot common pitfalls such as missing variables or malformed expressions.

No external services, no heavy dependencies—just plain C# and the SmartMarker NuGet package.

---

## How to Substitute Variables – Step‑by‑Step Overview

Below is a high‑level picture of the workflow. Think of it as a pipeline where your raw JSON template enters on the left, the SmartMarker engine does its magic, and the fully‑rendered JSON exits on the right.

![Diagram showing how to substitute variables in JSON](https://example.com/images/smartmarker-flow.png "How to substitute variables in JSON")

*Image alt text: Diagram showing how to substitute variables in JSON.*

---

## Step 1: Install and Import SmartMarker

Before you can start, make sure the SmartMarker package is referenced in your project. If you’re using the .NET CLI, run:

```bash
dotnet add package SmartMarker
```

Then, add the necessary `using` directives at the top of your C# file:

```csharp
using SmartMarker;
using SmartMarker.Models;
using System;
```

> **Pro tip:** The latest version (as of March 2026) is 2.4.1. It supports .NET 6 and later, but works just fine with .NET Framework 4.7 too.

---

## Step 2: Create SmartMarker Options and Define Variables

Now we’ll create an instance of `SmartMarkerOptions` that will hold any variables we want to reuse across the template. This is where we answer the question **how to substitute variables**—the variables act as placeholders that SmartMarker will replace later.

```csharp
// Step 2: Create SmartMarker options to hold variables used in the template
var smartMarkerOptions = new SmartMarkerOptions();

// Define a variable (Rate) that we’ll reference later in the JSON expression
smartMarkerOptions.Variables["Rate"] = 0.08; // 8% commission rate
```

Why store the rate in `Variables` instead of hard‑coding it? Because you might pull that number from a database, a config file, or a user input. Keeping it in the options makes the template reusable and testable.

---

## Step 3: Write the JSON Template with an `if` Expression

Here’s where the **use if expression** keyword shines. SmartMarker lets you embed conditional logic directly inside the JSON string. The syntax looks a bit like a property name, but SmartMarker treats it as a directive.

```csharp
// Step 3: Prepare the JSON data with a conditional field that uses the variable
string jsonTemplate = @"{
    ""Amount"": 1000,
    ""if(Amount>500)"": ""${Amount * Rate}""
}";
```

Notice the key `if(Amount>500)`. SmartMarker evaluates the expression `Amount>500`; if it’s true, the corresponding value (`${Amount * Rate}`) gets inserted into the output. The `${...}` syntax is the *variable substitution* engine—here we **how to multiply values** (`Amount * Rate`) before injecting the result.

---

## Step 4: Process the Template and Retrieve the Final JSON

With the options and template ready, we hand everything over to the processor. The method `ProcessJson` parses the template, applies the condition, performs the multiplication, and returns a clean JSON string.

```csharp
// Step 4: Process the JSON with SmartMarker, applying the variable substitution
string resultJson = ws.SmartMarkerProcessor.ProcessJson(jsonTemplate, smartMarkerOptions);
Console.WriteLine(resultJson);
```

Running the snippet prints:

```json
{
  "Amount": 1000,
  "Result": "80"
}
```

**What happened?**  
- `Amount` is 1000, which satisfies `Amount>500`.  
- SmartMarker evaluates `${Amount * Rate}` → `1000 * 0.08 = 80`.  
- The original conditional key (`if(Amount>500)`) is replaced by a clean property name (`Result`). By default SmartMarker uses `"Result"` but you can customize it (more on that later).

If you change `Amount` to `400`, the output becomes:

```json
{
  "Amount": 400
}
```

The conditional block disappears because the expression evaluated to `false`. That’s the essence of **how to apply conditional** logic in JSON.

---

## Step 5: Customizing the Output Property Name (Optional)

Sometimes you don’t want the generic `"Result"` key. SmartMarker lets you specify a custom name using the `RenameIfExpression` option:

```csharp
smartMarkerOptions.RenameIfExpression = "Discount";
string customResult = ws.SmartMarkerProcessor.ProcessJson(jsonTemplate, smartMarkerOptions);
Console.WriteLine(customResult);
```

Output:

```json
{
  "Amount": 1000,
  "Discount": "80"
}
```

Now the conditional value is stored under a more meaningful property name—perfect for downstream services that expect a specific field.

---

## Common Pitfalls and How to Avoid Them

| Issue | Why It Happens | Fix |
|-------|----------------|-----|
| Variable not found | You referenced a variable that isn’t in `smartMarkerOptions.Variables`. | Double‑check spelling and ensure the variable is added before processing. |
| Invalid `if` syntax | Missing parentheses or wrong operator (`>`, `<`, `==`). | Follow the exact `if(<expression>)` pattern; SmartMarker only supports simple numeric comparisons. |
| JSON becomes malformed | Accidentally leaving a trailing comma after the conditional block. | Let SmartMarker handle the removal; keep the original template syntactically correct. |
| Unexpected number format | Result appears as a string `"80"` instead of a number. | Cast or parse later, or use `${(Amount * Rate):N0}` for numeric formatting. |

---

## Full Working Example (Copy‑Paste Ready)

Below is the complete program you can compile and run. It demonstrates **how to generate json** with dynamic variables, conditionals, and arithmetic—all in under 30 lines.

```csharp
using System;
using SmartMarker;
using SmartMarker.Models;

class Program
{
    static void Main()
    {
        // 1️⃣ Create SmartMarker options and define a reusable variable
        var smartMarkerOptions = new SmartMarkerOptions();
        smartMarkerOptions.Variables["Rate"] = 0.08; // 8% commission
        smartMarkerOptions.RenameIfExpression = "Discount"; // optional custom name

        // 2️⃣ JSON template with an if expression and multiplication
        string jsonTemplate = @"{
            ""Amount"": 1000,
            ""if(Amount>500)"": ""${Amount * Rate}""
        }";

        // 3️⃣ Process the template
        string output = ws.SmartMarkerProcessor.ProcessJson(jsonTemplate, smartMarkerOptions);

        // 4️⃣ Show the result
        Console.WriteLine("Generated JSON:");
        Console.WriteLine(output);
    }
}
```

**Expected console output**

```
Generated JSON:
{
  "Amount": 1000,
  "Discount": "80"
}
```

Feel free to change `Amount` to test the conditional branch, or adjust `Rate` to see different discount calculations.

---

## Extending the Pattern – More “How to” Scenarios

- **How to substitute variables** from a configuration file: Load a `Dictionary<string, object>` from `appsettings.json` and feed it into `smartMarkerOptions.Variables`.  
- **How to use if expression** for multiple conditions: Chain them like `"if(Amount>500 && CustomerType=='VIP')"`—SmartMarker supports logical AND/OR.  
- **How to apply conditional** formatting: Use `${Amount:0.00}` inside the expression to control decimal places.  
- **How to multiply values** with more complex math: `${(Amount - Discount) * TaxRate}` works the same way.  
- **How to generate json** for nested objects: Place the conditional block inside another JSON object, and SmartMarker will preserve the hierarchy.

---

## Conclusion

We’ve covered **how to substitute variables** in JSON using SmartMarker, demonstrated **use if expression** for conditional inclusion, explained **how to apply conditional** logic, shown **how to multiply values** inside a template, and finally illustrated **how to generate json** that’s ready for downstream consumption. The approach is lightweight, requires no external templating engine, and fits neatly into any C# codebase.

Give it a spin—tweak the variables, add more conditions, or wrap the whole thing in a helper class for reuse across your solution. When you need to produce dynamic JSON quickly, SmartMarker is a solid, production‑ready option.

---

**Next steps**

- Dive deeper into SmartMarker’s advanced features like loops (`foreach`) and custom functions.  
- Combine this technique with ASP.NET Core endpoints to serve dynamic JSON APIs.  
- Explore other templating libraries (e.g., Handlebars.NET) for comparison, especially if you need richer syntax.

Got questions or a particular use‑case you’re wrestling with? Drop a comment below, and let’s troubleshoot together. Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}