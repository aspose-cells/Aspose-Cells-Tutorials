---
category: general
date: 2026-07-13
description: Создайте книгу Excel на C# и узнайте, как добавить именованный диапазон,
  присвоить имя таблице и решить конфликты имён — всё в одном наглядном примере.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- add named range
- assign name to table
- set table name
- how to add range
language: ru
lastmod: 2026-07-13
og_description: Создайте Excel‑книгу в C# с помощью Aspose.Cells. Узнайте, как добавить
  именованный диапазон, задать имя таблицы и решить конфликты имен в лаконичном, готовом
  к запуску руководстве.
og_image_alt: Screenshot showing an Excel workbook with a named range and a table
  name set using C# code
og_title: Создание Excel‑книги в C# – Добавление именованного диапазона и установка
  имени таблицы
schemas:
- author: Aspose
  dateModified: '2026-07-13'
  description: Create Excel Workbook in C# and learn how to add named range, assign
    name to table, and handle naming conflicts—all in one clear example.
  headline: Create Excel Workbook in C# – Add Named Range & Set Table Name
  type: TechArticle
- description: Create Excel Workbook in C# and learn how to add named range, assign
    name to table, and handle naming conflicts—all in one clear example.
  name: Create Excel Workbook in C# – Add Named Range & Set Table Name
  steps:
  - name: '**Use a consistent prefix** (`tbl_`, `rng_`, etc.) – it instantly tells
      you what the object is.'
    text: '**Use a consistent prefix** (`tbl_`, `rng_`, etc.) – it instantly tells
      you what the object is.'
  - name: '**Stay within 255 characters** – Excel’s limit for names.'
    text: '**Stay within 255 characters** – Excel’s limit for names.'
  - name: '**Avoid spaces and special characters** – only letters, numbers, and underscores
      are safe.'
    text: '**Avoid spaces and special characters** – only letters, numbers, and underscores
      are safe.'
  - name: '**Validate before assigning** – a quick `if (!sheet.Names.Contains(name))`
      check prevents the clash we demonstrated.'
    text: '**Validate before assigning** – a quick `if (!sheet.Names.Contains(name))`
      check prevents the clash we demonstrated.'
  type: HowTo
- questions:
  - answer: Yes, but you must qualify the address with the sheet name, e.g., `"Sheet1!A1:B5"`.
      The `Names.Add` method accepts that format.
    question: Can I add a named range that spans multiple worksheets?
  - answer: Absolutely. You can pass a formula string instead of a static address,
      such as `"=OFFSET(Sheet1!$A$1,0,0,COUNT(Sheet1!$A:$A),2)"`.
    question: Does Aspose.Cells support dynamic named ranges (like OFFSET formulas)?
  - answer: 'Just set `table.Name = " ## What Should You Learn Next?


      The following tutorials cover closely related topics that build on the techniques
      demonstrated in this guide. Each resource includes complete working code examples
      with step-by-step explanations to help you master additional API features and
      explore alternative implementation approaches in your own projects.

      - [How to Create Workbook Scoped Named Ranges in Excel Using Aspose.Cells .NET](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)
      - [How to Implement a Named Range with Workbook Scope in Aspose.Cells Java for
      Enhanced Excel Data Management](/cells/english/java/tables-structured-references/implement-named-range-workbook-scope-aspose-cells-java/)
      - [Excel Automation&#58; Create a Workbook and Add a ListBox Using Aspose.Cells
      for .NET](/cells/english/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)

      {{< /blocks/products/pf/tutorial-page-section >}} {{< /blocks/products/pf/main-container
      >}} {{< /blocks/products/pf/main-wrap-class >}} {{< blocks/products/products-backtop-button
      >}}'
    question: What if I need to rename an existing table?
  type: FAQPage
tags:
- C#
- Aspose.Cells
- Excel Automation
- .NET
title: Создание Excel‑книги в C# – Добавление именованного диапазона и установка имени
  таблицы
url: /ru/net/excel-advanced-named-ranges/create-excel-workbook-in-c-add-named-range-set-table-name/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание Excel Workbook в C# – Полное руководство по добавлению именованных диапазонов и установке имен таблиц

Когда‑нибудь вам нужно было **create Excel workbook** с нуля и вы задавались вопросом, куда поместить именованный диапазон или как дать таблице собственный идентификатор? Вы не одиноки. Во многих сценариях отчётности или экспорта данных вы будете управлять диапазонами, таблицами и иногда сталкиваться с конфликтами имён.  

В этом руководстве мы пройдем полностью исполняемый пример, который **creates an Excel workbook**, **adds a named range**, а затем **assigns a name to a table** — покажет вам точно, что делать, когда имена конфликтуют. К концу вы будете знать «как» и «почему» каждого шага, а также несколько советов, как держать код чистым.

> **Быстрая победа:** код использует библиотеку **Aspose.Cells**, которая работает с .NET 6+ и не требует установки Excel на сервере.

---

## Что вам понадобится

- **.NET 6 SDK** (или любой недавний .NET)  
- **Aspose.Cells for .NET** пакет NuGet  
- Хорошая IDE (Visual Studio, Rider или VS Code)  
- Базовые знания C# — ничего сложного, только обычные `using` инструкции

Если у вас есть всё это, мы можем сразу перейти к процессу **create excel workbook**.

---

## ## Create Excel Workbook – Обзор пошагового процесса

Ниже представлен полный готовый к копированию и вставке код программы. Он демонстрирует всё — от создания рабочей книги до обработки конфликта имён, когда вы пытаетесь **assign name to table**.

```csharp
using System;
using Aspose.Cells;

namespace ExcelNamingDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create a new workbook
            Workbook workbook = new Workbook();

            // Step 2: Add some sample data so we have a table to work with
            Worksheet sheet = workbook.Worksheets[0];
            sheet.Cells["A1"].PutValue("Product");
            sheet.Cells["B1"].PutValue("Price");
            sheet.Cells["A2"].PutValue("Apple");
            sheet.Cells["B2"].PutValue(0.99);
            sheet.Cells["A3"].PutValue("Banana");
            sheet.Cells["B3"].PutValue(0.59);
            sheet.Cells["A4"].PutValue("Cherry");
            sheet.Cells["B4"].PutValue(2.99);
            sheet.Cells["A5"].PutValue("Date");
            sheet.Cells["B5"].PutValue(3.49);

            // Step 3: Convert the data range into a table (default name Table1)
            int tableIndex = sheet.Tables.Add(sheet.Cells.CreateRange("A1:B5"), true);
            ListObject table = sheet.Tables[tableIndex];
            // At this point the table name is "Table1"

            // Step 4: Add a named range that covers the same cells
            // This is the "add named range" part of the tutorial
            sheet.Names.Add("MyRange", "A1:B5");

            // Step 5: Try to give the table the same name – this will cause a conflict
            try
            {
                table.Name = "MyRange"; // <-- assign name to table
            }
            catch (Exception ex)
            {
                // Step 6: Handle the naming conflict by outputting the error message
                Console.WriteLine("Naming conflict detected:");
                Console.WriteLine(ex.Message);
            }

            // Optional: Save the workbook to verify everything works
            workbook.Save("DemoWorkbook.xlsx");
        }
    }
}
```

**Ожидаемый вывод** при запуске программы:

```
Naming conflict detected:
A name with the same text already exists.
```

И если вы откроете *DemoWorkbook.xlsx*, вы увидите таблицу с именем **Table1** и именованный диапазон под названием **MyRange** — именно то, что мы планировали, без конфликта.

---

## ## Add Named Range – Почему это важно

**named range** по сути является псевдонимом для блока ячеек. Вместо постоянного обращения к `A1:B5` вы можете писать `MyRange` в формулах, проверках данных или даже в коде. Это повышает читаемость и уменьшает вероятность ошибок, связанных с опечатками.

В приведённом выше фрагменте мы вызываем:

```csharp
sheet.Names.Add("MyRange", "A1:B5");
```

- Первый аргумент — это **name**, который вы будете использовать позже.  
- Второй аргумент — это **address** (относительно листа).

Если вам когда‑нибудь понадобится **how to add range** динамически, вы можете собрать строку адреса с помощью `Cell.GetRefersTo()` или использовать `Range refRange = sheet.Cells.CreateRange(startRow, startCol, totalRows, totalCols)`.

---

## ## Assign Name to Table – Обработка конфликтов

Таблицы (также называемые *list objects*) уже имеют встроенное свойство имени. По умолчанию Aspose.Cells называет их `Table1`, `Table2` и т.д. Когда вы пытаетесь присвоить таблице тот же идентификатор, что и у существующего именованного диапазона, библиотека бросает исключение — так же, как делает Excel.

Почему это происходит?

- Область имён в Excel **на уровне всей рабочей книги** как для диапазонов, так и для таблиц.  
- Дублирование имён сделало бы формулы неоднозначными, поэтому движок блокирует это.

### Совет профессионала

Если вам действительно нужна таблица, которая будет делить логическое имя с диапазоном, рассмотрите **prefixing** одного из них, например:

```csharp
table.Name = "tbl_MyRange";   // safe, no conflict
```

Или сначала переименуйте диапазон:

```csharp
sheet.Names["MyRange"].Name = "DataRange";
```

Оба подхода поддерживают чистоту пространства имён и избегают ошибок времени выполнения.

---

## ## Set Table Name – Лучшие практики

Когда вы программно **set table name**, имейте в виду следующие рекомендации:

1. **Use a consistent prefix** (`tbl_`, `rng_`, etc.) – он сразу показывает, что это за объект.  
2. **Stay within 255 characters** – ограничение Excel для имён.  
3. **Avoid spaces and special characters** – безопасны только буквы, цифры и подчёркивания.  
4. **Validate before assigning** – быстрая проверка `if (!sheet.Names.Contains(name))` предотвращает конфликт, который мы продемонстрировали.

Вот вспомогательный метод, который вы можете добавить в любой проект:

```csharp
static void SafeSetTableName(Worksheet sheet, ListObject table, string desiredName)
{
    string finalName = desiredName;
    int suffix = 1;
    while (sheet.Names.Contains(finalName) || sheet.Tables.Contains(finalName))
    {
        finalName = $"{desiredName}_{suffix}";
        suffix++;
    }
    table.Name = finalName;
}
```

Вызов `SafeSetTableName(sheet, table, "MyRange")` автоматически превратит `MyRange` в `MyRange_1`, если возникнет конфликт, гарантируя, что операция **create excel workbook** никогда не будет неожиданно прервана.

---

## ## Full Working Example – Сводим всё вместе

Ниже представлена компактная версия, которую вы можете скопировать прямо в консольное приложение. Она включает процедуру безопасности и демонстрирует сквозной процесс.

```csharp
using System;
using Aspose.Cells;

namespace ExcelNamingDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create the workbook
            Workbook wb = new Workbook();
            Worksheet ws = wb.Worksheets[0];

            // Populate a simple dataset
            ws.Cells["A1"].PutValue("Item");
            ws.Cells["B1"].PutValue("Quantity");
            ws.Cells["A2"].PutValue("Pen");
            ws.Cells["B2"].PutValue(10);
            ws.Cells["A3"].PutValue("Notebook");
            ws.Cells["B3"].PutValue(5);

            // Turn data into a table
            int tblIdx = ws.Tables.Add(ws.Cells.CreateRange("A1:B3"), true);
            ListObject tbl = ws.Tables[tblIdx];

            // Add a named range covering the same cells
            ws.Names.Add("MyRange", "A1:B3");

            // Safely assign a name to the table
            SafeSetTableName(ws, tbl, "MyRange");

            // Save to verify
            wb.Save("FinalDemo.xlsx");
            Console.WriteLine($"Table name set to: {tbl.Name}");
        }

        static void SafeSetTableName(Worksheet sheet, ListObject table, string desiredName)
        {
            string candidate = desiredName;
            int i = 1;
            while (sheet.Names.Contains(candidate) || sheet.Tables.Contains(candidate))
            {
                candidate = $"{desiredName}_{i}";
                i++;
            }
            table.Name = candidate;
        }
    }
}
```

Запуск этого скрипта создаёт `FinalDemo.xlsx`, где таблица называется `MyRange_1` (или другой уникальный суффикс), а диапазон остаётся `MyRange`. Без исключений, без загадок — только чистое, детерминированное именование.

---

## ## Часто задаваемые вопросы (FAQ)

**Q: Могу ли я добавить именованный диапазон, охватывающий несколько листов?**  
A: Да, но необходимо указать имя листа в адресе, например, `"Sheet1!A1:B5"`. Метод `Names.Add` принимает такой формат.

**Q: Поддерживает ли Aspose.Cells динамические именованные диапазоны (например, формулы OFFSET)?**  
A: Абсолютно. Вы можете передать строку формулы вместо статического адреса, например `"=OFFSET(Sheet1!$A$1,0,0,COUNT(Sheet1!$A:$A),2)"`.

**Q: Что если мне нужно переименовать существующую таблицу?**  
A: Просто установите `table.Name = "

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}