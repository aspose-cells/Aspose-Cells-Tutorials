---
category: general
date: 2026-08-07
description: Определите именованный диапазон в Excel с помощью C# и узнайте, как добавить
  таблицу на лист, затем программно сохранить книгу в файл.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- define named range excel
- save workbook to file
- add named range excel
- add table to worksheet
- create excel workbook programmatically
language: ru
lastmod: 2026-08-07
og_description: Определите именованный диапазон в Excel с помощью C# и посмотрите,
  как добавить таблицу, создать книгу программно и сохранить её в файл в одном процессе.
og_image_alt: Screenshot of C# code that creates an Excel workbook, adds a table,
  defines a named range, and saves the file
og_title: Определение именованного диапазона в Excel с C# — полное руководство по
  книге
schemas:
- author: Aspose
  dateModified: '2026-08-07'
  description: Define named range in Excel with C# and learn how to add a table to
    a worksheet, then save workbook to file programmatically.
  headline: Define named range in Excel with C# – create workbook
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
- named range
- programmatic Excel
title: Определить именованный диапазон в Excel с C# – создать рабочую книгу
url: /ru/net/excel-working-with-named-ranges/define-named-range-in-excel-with-c-create-workbook/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Определение именованного диапазона в Excel с C# – создание рабочей книги

Если вам нужно **define named range in Excel** из кода C#, этот учебник покажет вам точно, как это сделать. Вы также увидите, как **add a table to a worksheet**, создать рабочую книгу **programmatically**, и, наконец, **save workbook to file** без выхода из IDE.

Работа с файлами Excel программно экономит время, устраняет ручные ошибки и позволяет создавать автоматизированные конвейеры отчетности. В этом руководстве вы:

* Создать новую рабочую книгу Excel с нуля.  
* Добавить таблицу, охватывающую определённый диапазон ячеек.  
* Определить именованный диапазон и обработать конфликты имён.  
* Сохранить рабочую книгу на диск.

Все шаги используют библиотеку **Aspose.Cells for .NET**, которая работает с .NET 6+ и .NET Framework 4.6+. Дополнительный COM‑interop или установка Office не требуются.

## Предварительные требования

* .NET 6 SDK (или .NET Framework 4.6+).  
* Visual Studio 2022 или любой IDE, совместимый с C#.  
* NuGet‑пакет Aspose.Cells for .NET (`Install-Package Aspose.Cells`).  

> **Совет:** Используйте бесплатную оценочную лицензию во время тестирования; замените её на производственную лицензию перед развертыванием.

## Шаг 1: Создание рабочей книги Excel программно

Первая операция — создать объект `Workbook`. Этот объект представляет весь файл Excel в памяти.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook in memory
        Workbook workbook = new Workbook();               // create an empty workbook
        Worksheet worksheet = workbook.Worksheets[0];    // get the first (default) worksheet
```

*Почему это важно*: Создание рабочей книги в коде даёт полный контроль над листами, стилями и данными до того, как файл будет записан на диск.

## Шаг 2: Добавление таблицы на лист

Таблица (также известная как ListObject) предоставляет встроенную фильтрацию, сортировку и стилизацию. Здесь мы создаём таблицу, охватывающую ячейки **A1:B5**, и задаём ей имя **SalesData**.

```csharp
        // Step 2: Define a range and convert it into a table
        Range tableRange = worksheet.Cells.CreateRange("A1:B5", true);
        ListObject table = worksheet.Tables[worksheet.Tables.Add(tableRange, true)];
        table.Name = "SalesData";

        // Populate the table with sample data
        worksheet.Cells["A1"].PutValue("Product");
        worksheet.Cells["B1"].PutValue("Units");
        worksheet.Cells["A2"].PutValue("Apples");
        worksheet.Cells["B2"].PutValue(120);
        worksheet.Cells["A3"].PutValue("Bananas");
        worksheet.Cells["B3"].PutValue(85);
        worksheet.Cells["A4"].PutValue("Cherries");
        worksheet.Cells["B4"].PutValue(45);
        worksheet.Cells["A5"].PutValue("Dates");
        worksheet.Cells["B5"].PutValue(30);
```

*Почему это важно*: Добавление таблицы на раннем этапе позволяет позже ссылаться на данные с помощью **named range**, а структурная ссылка таблицы может использоваться в формулах.

## Шаг 3: Определение именованного диапазона в Excel – обработка конфликтов

**named range** — это идентификатор, указывающий на ячейку или диапазон, упрощающий чтение формул. Если имя уже существует (например, имя таблицы **SalesData**), Excel выдаёт конфликт. Приведённый ниже код демонстрирует, как перехватить это исключение и продолжить безопасно.

```csharp
        // Step 3: Attempt to define a named range with the same identifier as the table
        try
        {
            // This will raise an exception because "SalesData" is already used by the table
            worksheet.Names.Add("SalesData", "A1");
        }
        catch (Exception ex)
        {
            Console.WriteLine("Name conflict prevented: " + ex.Message);
        }

        // Step 4: Add a different named range – this succeeds
        worksheet.Names.Add("SalesTotal", "B6");
        worksheet.Cells["B6"].Formula = "=SUM(SalesData[Units])";
```

*Почему это важно*: Обработка конфликтов имён предотвращает сбои во время выполнения в автоматических задачах. Второй именованный диапазон **SalesTotal** демонстрирует ссылку на столбец таблицы в формуле.

## Шаг 4: Сохранение рабочей книги в файл

После всех изменений сохраняем рабочую книгу на диск. Метод `Save` поддерживает множество форматов; здесь мы используем формат по умолчанию `.xlsx`.

```csharp
        // Step 5: Save the workbook to the file system
        string outputPath = @"C:\Temp\NameConflictHandled.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved successfully to {outputPath}");
    }
}
```

*Почему это важно*: Программное использование **save workbook to file** позволяет выполнять пакетную обработку, планировать генерацию отчетов и интегрировать с веб‑API.

## Полный исходный код в одном окне

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create a new workbook
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Add a table covering A1:B5 and name it "SalesData"
        Range tableRange = worksheet.Cells.CreateRange("A1:B5", true);
        ListObject table = worksheet.Tables[worksheet.Tables.Add(tableRange, true)];
        table.Name = "SalesData";

        // Fill the table with sample data
        worksheet.Cells["A1"].PutValue("Product");
        worksheet.Cells["B1"].PutValue("Units");
        worksheet.Cells["A2"].PutValue("Apples");   worksheet.Cells["B2"].PutValue(120);
        worksheet.Cells["A3"].PutValue("Bananas");  worksheet.Cells["B3"].PutValue(85);
        worksheet.Cells["A4"].PutValue("Cherries"); worksheet.Cells["B4"].PutValue(45);
        worksheet.Cells["A5"].PutValue("Dates");    worksheet.Cells["B5"].PutValue(30);

        // Try to create a defined name with the same identifier – handle the conflict
        try
        {
            worksheet.Names.Add("SalesData", "A1");
        }
        catch (Exception ex)
        {
            Console.WriteLine("Name conflict prevented: " + ex.Message);
        }

        // Add a different defined name – this succeeds
        worksheet.Names.Add("SalesTotal", "B6");
        worksheet.Cells["B6"].Formula = "=SUM(SalesData[Units])";

        // Save the workbook
        string outputPath = @"C:\Temp\NameConflictHandled.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved successfully to {outputPath}");
    }
}
```

### Ожидаемый результат

* Файл Excel с именем **NameConflictHandled.xlsx** появляется в `C:\Temp`.  
* Лист 1 содержит отформатированную таблицу **SalesData** с строками продукта‑единицы.  
* Ячейка **B6** показывает сумму столбца **Units**, вычисленную через именованный диапазон **SalesTotal**.  
* Консоль выводит сообщение о конфликте имён (если он есть) и подтверждает расположение файла.

## Часто задаваемые вопросы и особые случаи

| Question | Answer |
|----------|--------|
| **Могу ли я определить именованный диапазон, охватывающий несколько листов?** | Да. Используйте `worksheet.Names.Add("GlobalRange", "'Sheet1'!A1:B5")` и ссылаться на него с любого листа. |
| **Что делать, если нужно перезаписать существующий файл?** | Вызовите `workbook.Save(path, SaveFormat.Xlsx, new SaveOptions { Overwrite = true })`. |
| **Как добавить именованный диапазон без конфликта, если имя уже существует?** | Используйте `worksheet.Names.Remove("ExistingName")` перед добавлением нового, либо сгенерируйте уникальный идентификатор (например, `Guid.NewGuid().ToString("N")`). |
| **Есть ли способ автоматически применить стиль к таблице?** | Установите `table.Style = workbook.Styles[BuiltInStyleId.TableStyleMedium9];` после создания таблицы. |
| **Работает ли это на .NET Core?** | Aspose.Cells поддерживает .NET Core, .NET 5/6/7 и .NET Framework. Просто подключите тот же NuGet‑пакет. |

## Заключение

Теперь вы знаете, как **define named range in Excel** с помощью C#, **add a table to a worksheet** и **save workbook to file** программно. Полный пример демонстрирует создание рабочей книги Excel с нуля, обработку конфликтов имён и генерацию готового отчёта в едином, повторяемом процессе.

Далее изучайте связанные темы, такие как **adding charts to a worksheet**, **exporting to PDF** или **reading existing workbooks**. Каждая из них опирается на те же основы, рассмотренные здесь, поэтому вы будете готовы расширять решение для более сложных сценариев автоматизации. Счастливого кодинга!

## Что следует изучить дальше?

Следующие учебники охватывают тесно связанные темы, построенные на техниках, продемонстрированных в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [Создать именованный диапазон ячеек в Excel](/cells/english/net/excel-creating-formatting-named-ranges/create-named-range-of-cells/)
- [Как реализовать формулы с именованными диапазонами в .NET с использованием Aspose.Cells для автоматизации Excel](/cells/english/net/formulas-functions/implement-named-range-formulas-net-aspose-cells/)
- [Как создать именованные диапазоны, ограниченные рабочей книгой, в Excel с использованием Aspose.Cells .NET](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}