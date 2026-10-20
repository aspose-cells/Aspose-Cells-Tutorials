---
category: general
date: 2026-10-20
description: Узнайте, как использовать wrapcols в Aspose.Cells, встраивать шрифты
  в HTML и сохранять Excel в HTML с полным примером на C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use wrapcols
- embed fonts in html
- save excel as html
- convert workbook to html
- use wrapcols function
language: ru
lastmod: 2026-10-20
og_description: Как использовать wrapcols в Aspose.Cells, внедрять шрифты в HTML и
  конвертировать книгу в HTML с понятным пошаговым руководством на C# для разработчиков.
og_image_alt: Screenshot of an Excel workbook saved as HTML with embedded fonts using
  Aspose.Cells
og_title: Как использовать wrapcols и встраивать шрифты при экспорте Excel в HTML
schemas:
- author: Aspose
  dateModified: '2026-10-20'
  description: Learn how to use wrapcols in Aspose.Cells, embed fonts in HTML, and
    save Excel as HTML with a complete C# example.
  headline: How to use wrapcols and embed fonts saving Excel to HTML
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel to HTML
- Smart Markers
title: Как использовать wrapcols и встраивание шрифтов при сохранении Excel в HTML
url: /ru/net/exporting-excel-to-html-with-advanced-options/how-to-use-wrapcols-and-embed-fonts-saving-excel-to-html/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как использовать wrapcols и внедрять шрифты при сохранении Excel в HTML

Если вам нужно **how to use wrapcols** в формуле Aspose.Cells, это руководство покажет точные шаги. Вы также узнаете, как **embed fonts in HTML** и **save Excel as HTML**, чтобы вывод выглядел одинаково во всех браузерах.  

The tutorial covers three practical scenarios: using the `WRAPCOLS` function, exporting a workbook with embedded fonts, and generating a master‑detail report with Smart Markers. By the end you’ll have a single, runnable C# program that demonstrates all of these features.

## Необходимые условия

Before you start, make sure you have:

* .NET 6.0 (или новее) установлен.
* Aspose.Cells for .NET добавлен в ваш проект (`dotnet add package Aspose.Cells`).
* Basic familiarity with C# and Excel formulas.

No additional third‑party libraries are required; Aspose.Cells handles HTML conversion and font embedding internally.

## Шаг 1: Демонстрация функции **how to use wrapcols** в формуле

The `WRAPCOLS` function splits a one‑dimensional range into a two‑dimensional array, filling columns first. This is useful when you need to reshape data for reporting or charting.

```csharp
using Aspose.Cells;
using System;

class WrapColsDemo
{
    static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // Populate a vertical range A1:A3
        sheet.Cells["A1"].PutValue(1);
        sheet.Cells["A2"].PutValue(2);
        sheet.Cells["A3"].PutValue(3);

        // Apply WRAPCOLS(A1:A3, 2) – this creates a 2‑column array {1,2}
        sheet.Cells["B1"].Formula = "=WRAPCOLS(A1:A3, 2)";

        // Force calculation so the formula result is materialized
        workbook.CalculateFormula();

        // Output the result to verify the function works
        Console.WriteLine("Result of WRAPCOLS: " + sheet.Cells["B1"].Value);
        // Expected output: Result of WRAPCOLS: 1
    }
}
```

**Почему это работает:**  
`WRAPCOLS` принимает два аргумента — исходный диапазон и количество столбцов. Функция заполняет массив по столбцам, отбрасывая лишние значения (в примере `3`). Результат появляется в верхней‑левой ячейке целевого диапазона (`B1`), и при необходимости вы можете вручную расширить диапазон, чтобы увидеть весь массив.

> **Pro tip:** После установки формулы вызовите `workbook.CalculateFormula()`, чтобы гарантировать актуальность результата перед чтением значений ячеек.

## Шаг 2: **Convert workbook to HTML** и **embed fonts in html**

When you export an Excel file to HTML, fonts are often substituted by the browser’s defaults, which can break the visual layout. Aspose.Cells lets you embed the exact fonts used in the workbook directly into the HTML file.

```csharp
using Aspose.Cells;
using Aspose.Cells.Rendering;   // Required for HtmlSaveOptions
using System;

class HtmlExportDemo
{
    static void Main()
    {
        // Re‑use the workbook from the previous step
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];
        sheet.Cells["A1"].PutValue("Hello");
        sheet.Cells["A2"].PutValue("World");

        // Configure HTML save options
        HtmlSaveOptions htmlOptions = new HtmlSaveOptions
        {
            // Embedding fonts ensures the output looks the same on any device
            EmbedFonts = true,
            // Optional: specify a folder for supporting files (images, CSS)
            ExportEmbeddedImages = true
        };

        // Save the workbook as an HTML file with embedded fonts
        string outputPath = @"C:\Temp\WorkbookWithFonts.html";
        workbook.Save(outputPath, htmlOptions);

        Console.WriteLine($"Workbook saved to HTML with embedded fonts at: {outputPath}");
    }
}
```

**Почему внедрение шрифтов важно:**  
Когда `EmbedFonts` установлено в `true`, Aspose.Cells преобразует каждый используемый шрифт TrueType/OpenType в правило `@font-face`, закодированное в Base64, внутри сгенерированного HTML. Это устраняет необходимость наличия одинаковых шрифтов на клиентском компьютере, гарантируя пиксель‑точное отображение.

> **Edge case:** Если исходная книга ссылается на шрифт, который не установлен на сервере, Aspose.Cells переключится на шрифт по умолчанию и выдаст предупреждение. Убедитесь, что необходимые шрифты доступны


## Что вам следует изучить дальше?

The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Как использовать WRAPCOLS в C# – Создание Excel Workbook с функциями Wrap](/cells/english/net/formulas-functions/how-to-use-wrapcols-in-c-create-excel-workbook-with-wrap-fun/)
- [Как внедрять шрифты в HTML – Конвертация Excel в HTML с C#](/cells/english/net/exporting-excel-to-html-with-advanced-options/how-to-embed-fonts-in-html-convert-excel-to-html-with-c/)
- [Как конвертировать файлы Excel в HTML с помощью Aspose.Cells для .NET: Скрытие наложенного контента](/cells/english/net/workbook-operations/excel-to-html-hide-overlaid-content-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}