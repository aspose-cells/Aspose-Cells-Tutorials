---
category: general
date: 2026-02-14
description: Создавать иерархию в шаблонах SmartMarker проще, чем вы думаете — узнайте,
  как создавать иерархические данные и эффективно выводить список сотрудников.
draft: false
keywords:
- how to create hierarchy
- create hierarchical data
- how to list employees
- SmartMarker nested range
- C# template processing
language: ru
og_description: 'Как создать иерархию в шаблонах SmartMarker: просто. Следуйте этому
  руководству, чтобы создать иерархические данные и вывести список сотрудников с вложенными
  диапазонами.'
og_title: Как создать иерархию с помощью SmartMarker – Полное руководство
tags:
- SmartMarker
- C#
- templating
title: Как создать иерархию с помощью SmartMarker – пошаговое руководство
url: /ru/net/smart-markers-dynamic-data/how-to-create-hierarchy-with-smartmarker-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как создать иерархию с помощью SmartMarker – Полное руководство

Ever wondered **как создать иерархию** inside a SmartMarker template without pulling your hair out? You're not the only one. In many reporting scenarios you need a parent‑child relationship—think departments and the people that work in them. The good news is that SmartMarker makes it a piece of cake once you know the right steps.

In this tutorial we’ll walk through the whole process: from **создания иерархических данных** in C#, enabling nested ranges, and finally rendering a template that **lists employees** for each department. By the end you’ll have a ready‑to‑run sample you can drop into any .NET project.

---

## Что понадобится

- .NET 6+ (любая недавняя версия подходит)
- Ссылка на библиотеку **SmartMarker** (пространство имён `ws.SmartMarkerProcessor`)
- Basic C# knowledge – nothing fancy, just a few objects and a lambda or two
- IDE or editor of your choice (Visual Studio, Rider, VS Code… you pick)

If you already have those, great—let’s dive in.

---

## Как создать иерархию — Обзор

The core idea is to build a **nested object graph** that mirrors the structure you want to see in the final document. In our case the graph looks like:

```
Departments
 ├─ Name (string)
 └─ Employees (string[])
```

SmartMarker can then iterate over `Departments` and, because we’ll turn on **nested range processing**, it will also loop over each department’s `Employees` collection automatically.

---

## Шаг 1: Построить иерархическую модель данных

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

> **Почему это важно:** Массив `Departments` — это коллекция верхнего уровня. Каждый элемент содержит массив `Employees`, предоставляя нам второй уровень иерархии, к которому мы позже обратимся с помощью `#Departments.Employees#`.

---

## Шаг 2: Включить обработку вложенных диапазонов

SmartMarker won’t dive into inner collections unless you tell it to. The `SmartMarkerOptions` object holds that switch.

```csharp
// Step 2: Enable nested range processing so inner collections (Employees) can be used
var smartMarkerOptions = new SmartMarkerOptions
{
    EnableNestedRange = true   // crucial for #Departments.Employees# to work
};
```

> **Совет:** Если вы забудете установить этот флаг, внутренний диапазон `#Employees#` просто ничего не вернёт, и вы будете терзать себя вопросом, почему шаблон пуст.

---

## Шаг 3: Запустить процессор с вашими данными

Now we hand the data and options to the processor. The `ws` variable represents your **WebService** (or whatever object hosts the SmartMarker engine).

```csharp
// Step 3: Run SmartMarker processing with the data and the configured options
ws.SmartMarkerProcessor.StartSmartMarkerProcessing(departmentData, smartMarkerOptions);
```

At this point SmartMarker parses the template, substitutes `#Departments.Name#` for each department name, and then, because nested ranges are enabled, iterates through each department’s `Employees` collection.

---

## Шаг 4: Создать маркеры шаблона

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

> **Что вы видите:** Внешний `#Departments.Name#` prints the department title. The inner `#Departments.Employees#` block loops over each employee, and `#Departments.Employees#` inside the block outputs the actual name.

---

## Ожидаемый вывод и проверка

Running the full example (data + options + template) should produce exactly the list shown above. To quickly verify, you can dump the result to the console:

```csharp
string result = ws.SmartMarkerProcessor.GetProcessedResult(); // pseudo‑method
Console.WriteLine(result);
```

If you see the two department headings followed by their employee bullets, you’ve successfully **created a hierarchy** and **listed employees**.

---

## Распространённые подводные камни и граничные случаи

| Проблема | Почему происходит | Решение |
|-------|----------------|-----|
| Нет вывода сотрудников | `EnableNestedRange` оставлен false | Установите `EnableNestedRange = true` |
| Дублирующиеся имена сотрудников | Same array reused across departments | Clone the array or use distinct collections |
| Very large hierarchies cause memory pressure | SmartMarker loads the whole object graph into memory | Stream data or paginate large collections |
| Template syntax errors | Missed closing `#/…#` tags | Use the SmartMarker validator or run a quick test with a tiny template |

---

## Дальше — реальные варианты использования

1. **Динамические источники данных** — Pull departments from a database and map them to the anonymous structure using LINQ.
2. **Условное форматирование** — Add a `IsManager` flag to each employee and use SmartMarker’s conditional tags (`#if …#`) to highlight managers.
3. **Несколько уровней вложенности** — If you need teams inside departments, just add another collection (`Teams`) and keep `EnableNestedRange` turned on.

---

## Полный рабочий пример (готов к копированию)

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

**Шаблон (template.txt)**

```
#Departments.Name#
  #Departments.Employees#
    - #Departments.Employees#
  #/Departments.Employees#
#/Departments.Name#
```

Running the program prints the hierarchy exactly as shown earlier.

---

## Заключение

We’ve covered **how to create hierarchy** in SmartMarker, from shaping **hierarchical data** in C# to turning on nested ranges and finally rendering a template that **lists employees** per department. The pattern scales—just add more nested collections or conditional logic and you’ve got a powerful reporting engine at your fingertips.

Ready for the next challenge? Try swapping the anonymous types for strongly‑typed POCO classes, or integrate this flow into an ASP.NET Core endpoint that returns a PDF or Word document. The sky’s the limit, and now you have a solid foundation.

![Как создать иерархию диаграмма](image.png){alt="Диаграмма, показывающая связь отдел‑сотрудник"}

*Счастливого кодинга! Если столкнётесь с проблемами, оставьте комментарий ниже — я с радостью помогу.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}