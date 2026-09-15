---
category: general
date: 2026-09-15
description: Узнайте, как сохранить книгу в формате CSV, экспортировать Excel в TXT
  и применить пользовательский числовой формат, преобразуя значения ячеек в верхний
  регистр в C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save workbook as csv
- apply custom number format
- export excel to txt
- uppercase cell values
- export worksheet as text
language: ru
lastmod: 2026-09-15
og_description: Сохранить книгу в формате CSV, экспортировать Excel в TXT и применить
  пользовательский числовой формат, преобразуя значения ячеек в верхний регистр с
  помощью Aspose.Cells на C#.
og_image_alt: Screenshot showing workbook saved as CSV using C# code
og_title: Сохранить рабочую книгу в формате CSV и экспортировать Excel в TXT с пользовательским
  форматированием в C#
schemas:
- author: Aspose
  dateModified: '2026-09-15'
  description: Learn how to save workbook as CSV, export Excel to TXT, and apply custom
    number format while converting cell values to uppercase in C#.
  headline: How to save workbook as CSV and export Excel to TXT with custom formatting
    in C#
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: Как сохранить рабочую книгу в CSV и экспортировать Excel в TXT с пользовательским
  форматированием на C#
url: /ru/net/converting-excel-files-to-other-formats/how-to-save-workbook-as-csv-and-export-excel-to-txt-with-cus/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как сохранить книгу в формате CSV и экспортировать Excel в TXT с пользовательским форматированием на C#

Если вам нужно **save workbook as CSV**, а также экспортировать лист как обычный текст и применить пользовательский числовой формат, это руководство покажет готовое решение, готовое к запуску. Вы увидите, как сохранить числовую точность, преобразовать значение каждой ячейки в верхний регистр и работать с датами японской эры — всё с помощью Aspose.Cells для .NET.

Экспорт данных из Excel часто требует работы с несколькими форматами: CSV для обмена данными, TXT для устаревших систем и пользовательские числовые форматы для локально‑специфической отчетности. Это руководство пошагово рассматривает каждое требование, чтобы вы могли скопировать код напрямую в свой проект.

В последующих разделах вы узнаете, как:

* **save workbook as csv** с заданным количеством значимых цифр  
* **export excel to txt**, принуждая **uppercase cell values**  
* **apply custom number format** для дат японской эры и прочитать отформатированный результат  

Не требуется внешних инструментов — только библиотека Aspose.Cells и среда разработки .NET.

## Требования

* .NET 6.0 или новее (код также работает с .NET Framework 4.8)  
* Aspose.Cells for .NET (пакет NuGet `Aspose.Cells`)  
* Базовое знакомство с C# и концепциями Excel  

---

## Шаг 1: Сохранить книгу в формате CSV с контролируемой точностью

Когда вы **save workbook as CSV**, числовые значения записываются с использованием стандартного строкового представления, что может привести к потере точности. Настраивая `CsvSaveOptions.SignificantDigits`, вы указываете Aspose.Cells, сколько значимых цифр сохранять.

```csharp
using Aspose.Cells;
using System;

// Create a new workbook (or load an existing one)
Workbook workbook = new Workbook();               // you can also use new Workbook("input.xlsx");

// Configure CSV options to keep up to 4 significant digits
CsvSaveOptions csvOptions = new CsvSaveOptions
{
    SignificantDigits = 4   // ensures numbers like 123.4567 stay precise
};

// Save the workbook as CSV
string csvPath = @"C:\Temp\Digits.csv";
workbook.Save(csvPath, csvOptions);

Console.WriteLine($"Workbook saved as CSV to {csvPath}");
```

**Почему это важно:**  
Установка `SignificantDigits` предотвращает ошибки округления, которые часто возникают при обмене большими наборами данных с downstream‑системами (например, хранилищами данных). Объект `CsvSaveOptions` также позволяет управлять разделителями, кодировкой и другими настройками CSV при необходимости.

---

## Шаг 2: Экспортировать лист как обычный текст с преобразованием значений в верхний регистр

Экспорт листа в простой файл `.txt` полезен для устаревших импортных процедур, ожидающих данные, разделённые пробелами. Включив `ExportTableOptions.ExportAsString` и предоставив делегат `CustomExport`, вы можете **export excel to txt** и одновременно обеспечить **uppercase cell values**.

```csharp
// Prepare export options for plain‑text output
ExportTableOptions tableOptions = new ExportTableOptions
{
    ExportAsString = true, // forces every cell to be treated as a string
    // CustomExport receives the cell and its current string value,
    // allowing you to modify it before it is written.
    CustomExport = (cell, value) =>
    {
        // Convert the cell value to an upper‑case string
        return value?.ToString().ToUpperInvariant();
    }
};

// Define the output path for the text file
string txtPath = @"C:\Temp\Table.txt";

// Export the first worksheet (index 0) as a tab‑delimited text file
workbook.Worksheets[0].ExportTable(txtPath, tableOptions);

Console.WriteLine($"Worksheet exported as text to {txtPath}");
```

**Почему это важно:**  
Многие точки интеграции (например, пакетные задания mainframe) ожидают идентификаторы в верхнем регистре. Обратный вызов `CustomExport` дает полный контроль над представлением каждой ячейки, позволяя внедрять преобразования, такие как обрезка, заполнение или локально‑специфическое форматирование, без последующей обработки файла.

---

## Шаг 3: Применить пользовательский числовой формат и прочитать отформатированный результат

Встроенные числовые форматы Excel покрывают большинство случаев, но иногда требуется отображать даты в определённой календарной системе — например, в японской эре. Приведённый ниже код демонстрирует, как **apply custom number format** к ячейке, а затем прочитать отформатированную строку, учитывающую локаль книги.

```csharp
// Create a new workbook for the era example
Workbook eraWorkbook = new Workbook();

// Access the first worksheet and target cell A1
Worksheet sheet = eraWorkbook.Worksheets[0];
Cell dateCell = sheet.Cells["A1"];

// Insert a Japanese‑era date string (Reiwa 3 = 2021)
dateCell.PutValue("Reiwa 3/04/01");

// Apply a built‑in date number format (14 = mm-dd-yy)
// You could also assign a custom format string, e.g., "[$-ja-JP]ggge年m月d日"
Style style = eraWorkbook.CreateStyle();
style.Number = 14; // standard short date format
dateCell.SetStyle(style);

// Force formula calculation (necessary if the cell contains a formula)
eraWorkbook.CalculateFormula();

// Retrieve the formatted string as it would appear in Excel
string formattedDate = dateCell.StringValue;
Console.WriteLine($"Formatted date (locale aware): {formattedDate}");
```

**Почему это важно:**  
Использование `SetStyle` с числовым форматом гарантирует, что отображение ячейки учитывает региональные настройки, что критично для отчетов, распространяемых в разных локалях. При последующем чтении `StringValue` вы получаете точную строку, которую пользователь видит в интерфейсе Excel, избавляясь от необходимости ручного разбора.

---

## Полный, исполняемый пример

Ниже представлен единый пример программы, объединяющий три шага. Вставьте его в новый проект Console App, добавьте пакет NuGet Aspose.Cells и запустите.

```csharp
using Aspose.Cells;
using System;

namespace ExcelExportDemo
{
    class Program
    {
        static void Main()
        {
            // ---------- Step 1: Save workbook as CSV ----------
            Workbook workbook = new Workbook(); // start with a fresh workbook
            // (Optionally load an existing file: new Workbook("input.xlsx"))

            // Populate some sample data
            workbook.Worksheets[0].Cells["A1"].PutValue(123.456789);
            workbook.Worksheets[0].Cells["B1"].PutValue("Sample Text");

            CsvSaveOptions csvOptions = new CsvSaveOptions
            {
                SignificantDigits = 4
            };
            string csvPath = @"C:\Temp\Digits.csv";
            workbook.Save(csvPath, csvOptions);
            Console.WriteLine($"Saved CSV to {csvPath}");

            // ---------- Step 2: Export worksheet as text with uppercase ----------
            ExportTableOptions tableOptions = new ExportTableOptions
            {
                ExportAsString = true,
                CustomExport = (cell, value) => value?.ToString().ToUpperInvariant()
            };
            string txtPath = @"C:\Temp\Table.txt";
            workbook.Worksheets[0].ExportTable(txtPath, tableOptions);
            Console.WriteLine($"Exported TXT to {txtPath}");

            // ---------- Step 3: Apply custom number format ----------
            Workbook eraWorkbook = new Workbook();
            Cell dateCell = eraWorkbook.Worksheets[0].Cells["A1"];
            dateCell.PutValue("Reiwa 3/04/01");

            Style eraStyle = eraWorkbook.CreateStyle();
            eraStyle.Number = 14; // short date format; replace with custom if needed
            dateCell.SetStyle(eraStyle);
            eraWorkbook.CalculateFormula();

            Console.WriteLine($"Japanese era date formatted: {dateCell.StringValue}");
        }
    }
}
```

**Ожидаемый вывод**

```
Saved CSV to C:\Temp\Digits.csv
Exported TXT to C:\Temp\Table.txt
Japanese era date formatted: 4/1/2021
```

(Точный формат даты может различаться в зависимости от настроек локали вашей системы.)

---

## Часто задаваемые вопросы и обработка граничных случаев

| Question | Answer |
|----------|--------|
| *Что если мне нужен другой разделитель в CSV?* | Установите `csvOptions.Separator` в `','`, `'\t'` или любой пользовательский символ перед вызовом `Save`. |
| *Можно ли сохранить оригинальную числовую точность без округления?* | Используйте `SignificantDigits = 0`, чтобы записать полное значение двойной точности, или задайте `NumberDecimalSeparator` для локально‑специфических десятичных символов. |
| *Как экспортировать только определённый диапазон, а не весь лист?* | Вызовите `ExportTable(string fileName, ExportTableOptions options, CellArea area)` и передайте `CellArea`, определяющий диапазон. |
| *Что если книга содержит формулы, ссылающиеся на другие листы?* | Убедитесь, что вызываете `workbook.CalculateFormula()` перед экспортом; иначе вы получите кэшированные значения. |
| *Можно ли сохранить оригинальное форматирование ячеек (шрифты, цвета) в TXT‑файле?* | Текстовые форматы не могут сохранять визуальное оформление. Если требуется богатое форматирование, рассмотрите экспорт в HTML (`HtmlSaveOptions`). |

---

## Заключение

Теперь вы знаете, как **save workbook as CSV** с контролируемой точностью, **export excel to TXT**, принуждая **uppercase cell values**, и **apply custom number format** для отображения дат с учётом локали. Каждый фрагмент кода автономен, работает сразу же и следует лучшим практикам как по производительности, так и по поддерживаемости.

Далее вы можете изучить:

* Использование `HtmlSaveOptions` для сохранения стилей при экспорте в веб‑дружественные форматы.  
* Применение `CsvSaveOptions.Encoding` для UTF‑8 или других наборов символов при работе с многоязычными данными.  
* Автоматизацию пакетной обработки нескольких листов с помощью цикла по `workbook.Worksheets`.

Не стесняйтесь адаптировать код под свои конвейеры данных, а гибкость Aspose.Cells возьмёт на себя тяжёлую работу.

---

## Что изучить дальше?

Следующие руководства охватывают тесно связанные темы, основанные на техниках, продемонстрированных в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в своих проектах.

- [Сохранить книгу в текстовый CSV‑формат](/cells/german/net/saving-files-in-different-formats/save-workbook-to-text-csv-format/)
- [Сохранить книгу в текстовый CSV‑формат](/cells/french/net/saving-files-in-different-formats/save-workbook-to-text-csv-format/)
- [Сохранить книгу в текстовый CSV‑формат](/cells/spanish/net/saving-files-in-different-formats/save-workbook-to-text-csv-format/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}