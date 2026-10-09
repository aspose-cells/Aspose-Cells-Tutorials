---
category: general
date: 2026-06-27
description: Экспорт таблицы в CSV с пользовательскими параметрами экспорта CSV в
  C#. Узнайте, как TableExportOptions и обработчик экспорта ячеек позволяют настроить
  вывод CSV для любой рабочей книги.
draft: false
keywords:
- export table to csv
- custom CSV export
- TableExportOptions
- cell export handler
- C# workbook to CSV
language: ru
og_description: Экспорт таблицы в CSV с пользовательскими параметрами экспорта CSV
  в C#. Это руководство проведёт вас через TableExportOptions, обработчики экспорта
  ячеек и полные примеры кода.
og_title: Экспорт таблицы в CSV в C# – Полное руководство по программированию
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: Export table to CSV with custom CSV export options in C#. Learn how
    TableExportOptions and a cell export handler let you tailor CSV output for any
    workbook.
  headline: Export table to CSV in C# – Complete Programming Guide
  type: TechArticle
- description: Export table to CSV with custom CSV export options in C#. Learn how
    TableExportOptions and a cell export handler let you tailor CSV output for any
    workbook.
  name: Export table to CSV in C# – Complete Programming Guide
  steps:
  - name: Prerequisites
    text: '- .NET 6.0 or later (the code works on .NET Framework 4.6+ as well). -
      A reference to the **GemBox.Spreadsheet** NuGet package (or any library exposing
      `TableExportOptions`). - Basic familiarity with C# and CSV concepts.'
  - name: Why `ExportAsString = true`?
    text: When you set `ExportAsString` to `true`, the library treats every cell as
      text before handing it to your handler. This guarantees that numeric cells don’t
      get auto‑formatted (e.g., scientific notation) before you have a chance to prepend
      the `$`. If you leave this flag `false`, the handler might rec
  - name: Understanding the **cell export handler**
    text: The lambda receives a `cell` object that carries metadata such as `Column`,
      `Row`, and `Value`. By checking `cell.Column == 1` we target the *Price* column
      only. The `double.TryParse` guard ensures we only format legitimate numbers—avoiding
      exceptions on empty or text cells.
  - name: Null or Empty Cells
    text: If your source data contains blanks, the handler will receive `null`. The
      guard clause `if (cell == null) return string.Empty;` prevents a `NullReferenceException`.
      You can also return a placeholder like `"N/A"` if that fits your business rules.
  - name: Large Workbooks
    text: 'When dealing with thousands of rows, consider streaming the CSV to avoid
      high memory consumption:'
  - name: Different Delimiters
    text: 'If you need a semicolon (`;`) instead of a comma, adjust the `SaveOptions`:'
  type: HowTo
tags:
- CSV
- C#
- Spreadsheet
title: Экспорт таблицы в CSV в C# – Полное руководство по программированию
url: /ru/net/csv-file-handling/export-table-to-csv-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Экспорт таблицы в CSV на C# – Полное руководство по программированию

Когда‑то вам нужно было **экспортировать таблицу в CSV**, но стандартный вывод просто не устраивал? Может, вы хотели добавить символ валюты, изменить разделитель или пропустить некоторые столбцы. В этом руководстве мы покажем, как **экспортировать таблицу в CSV** с помощью мощного класса `TableExportOptions` и пользовательского *обработчика экспорта ячеек* — без внешних скриптов.

Мы пройдём реальный сценарий: возьмём книгу в стиле электронных таблиц, изменим второй столбец, чтобы каждое значение отображалось как сумма в долларах, а затем сохраним результат в файл CSV. К концу вы получите переиспользуемый шаблон для любого **кастомного экспорта CSV**, который может понадобиться в ваших проектах на C#.

## Что вы узнаете

- Как настроить **конвертацию C# workbook в CSV** с библиотекой GemBox.Spreadsheet (или любой совместимой API).  
- Почему `TableExportOptions.ExportAsString` важен, когда нужен вывод в виде строк.  
- Как написать **обработчик экспорта ячеек**, который изменяет значения ячеек «на лету».  
- Советы по работе с граничными случаями, такими как пустые ячейки, разные типы данных и большие наборы данных.  

### Предварительные требования

- .NET 6.0 или новее (код также работает на .NET Framework 4.6+).  
- Ссылка на пакет **GemBox.Spreadsheet** в NuGet (или любая библиотека, предоставляющая `TableExportOptions`).  
- Базовое знакомство с C# и концепциями CSV.  

Если всё это у вас есть, давайте начнём.

---

## Шаг 1: Установите и подключите библиотеку Spreadsheet

Сначала добавьте пакет GemBox.Spreadsheet в ваш проект. Откройте терминал в папке решения и выполните:

```bash
dotnet add package GemBox.Spreadsheet --version 131.0
```

> **Pro tip:** GemBox предлагает бесплатный режим до 150 строк — идеально для экспериментов перед покупкой лицензии.

После восстановления пакета подключите пространство имён в начале вашего файла `.cs`:

```csharp
using GemBox.Spreadsheet;
```

> **Почему это важно:** тип `TableExportOptions` находится в этом пространстве имён; без него компилятор выдаст ошибку.

---

## Шаг 2: Создайте пример книги с данными

Соберём небольшую книгу, имитирующую типичный отчёт о продажах. Это даст нам конкретный объект для экспорта.

```csharp
// Initialize the library (free mode)
SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

// Create a new workbook and a worksheet
var wb = new ExcelFile();
var ws = wb.Worksheets.Add("Sales");

// Populate header row
ws.Cells[0, 0].Value = "Product";
ws.Cells[0, 1].Value = "Price";

// Add a few data rows
ws.Cells[1, 0].Value = "Laptop";
ws.Cells[1, 1].Value = 999.99;

ws.Cells[2, 0].Value = "Mouse";
ws.Cells[2, 1].Value = 25.5;

ws.Cells[3, 0].Value = "Keyboard";
ws.Cells[3, 1].Value = 45.0;
```

Запуск этого фрагмента сам по себе создаст обычный файл Excel. Наша цель — **экспортировать таблицу в CSV** с изюминкой: столбец цены должен иметь префикс `$`.

---

## Шаг 3: Настройте `TableExportOptions` для кастомного экспорта CSV

Здесь происходит волшебство. `TableExportOptions` позволяет управлять тем, как отображается каждая ячейка, остаются ли числа числовыми или превращаются в строки, а также какой разделитель использовать.

```csharp
// Step 3.1: Create export options for the table
var tableExportOptions = new TableExportOptions();

// Step 3.2: Export each cell's value as a string – essential for custom formatting
tableExportOptions.ExportAsString = true;

// Step 3.3: Define a custom handler to modify cell output
//         We prepend a dollar sign only for the second column (index 1)
tableExportOptions.CellExportHandler = (cell) =>
{
    // Guard against null cells – they become empty strings
    if (cell == null) return string.Empty;

    // If we are in the Price column, format as currency
    if (cell.Column == 1 && double.TryParse(cell.Value?.ToString(), out var price))
        return "$" + price.ToString("0.00");

    // Default: return the cell's string representation
    return cell.StringValue;
};
```

### Почему `ExportAsString = true`?

Когда `ExportAsString` установлен в `true`, библиотека рассматривает каждую ячейку как текст перед передачей её вашему обработчику. Это гарантирует, что числовые ячейки не будут автоматически отформатированы (например, в научную нотацию) до того, как вы успеете добавить `$`. Если оставить флаг `false`, обработчик может получить числовое значение, которое сложно превратить в отформатированную строку.

### Понимание **обработчика экспорта ячеек**

Лямбда‑выражение получает объект `cell`, содержащий метаданные, такие как `Column`, `Row` и `Value`. Проверяя `cell.Column == 1`, мы нацеливаемся только на столбец *Price*. Защита `double.TryParse` гарантирует, что форматируем только корректные числа — избегая исключений в пустых или текстовых ячейках.

---

## Шаг 4: Сохраните книгу как CSV, используя кастомные параметры

Теперь мы наконец **экспортируем таблицу в CSV** с нашей пользовательской логикой.

```csharp
// Define the output path – change this to your desired folder
string outputPath = Path.Combine(Environment.CurrentDirectory, "customSalesReport.csv");

// Save the worksheet as CSV using the options we configured
ws.Save(outputPath, SaveOptions.CsvDefault, tableExportOptions);

// Inform the user
Console.WriteLine($"CSV file created at: {outputPath}");
```

> **Ожидаемый вывод (`customSalesReport.csv`):**  
> ```
> Product,Price  
> Laptop,$999.99  
> Mouse,$25.50  
> Keyboard,$45.00  
> ```

Обратите внимание, что каждая цена теперь имеет префикс `$` — именно то, что задал наш **обработчик экспорта ячеек**.

---

## Шаг 5: Обработка граничных случаев и распространённых подводных камней

### Пустые или null‑ячейки

Если исходные данные содержат пробелы, обработчик получит `null`. Защитный оператор `if (cell == null) return string.Empty;` предотвращает `NullReferenceException`. При желании можно вернуть заполнитель, например `"N/A"`.

### Большие книги

При работе с тысячами строк рекомендуется стримить CSV, чтобы избежать высокого потребления памяти:

```csharp
using (var stream = new FileStream(outputPath, FileMode.Create, FileAccess.Write))
{
    ws.Save(stream, SaveOptions.CsvDefault, tableExportOptions);
}
```

### Другие разделители

Если нужен точка с запятой (`;`) вместо запятой, измените `SaveOptions`:

```csharp
var csvOptions = SaveOptions.CsvDefault;
csvOptions.Separator = ';';
ws.Save(outputPath, csvOptions, tableExportOptions);
```

Это быстрый пример того, насколько гибким может быть **кастомный экспорт CSV**.

---

## Шаг 6: Полный рабочий пример (готов к копированию)

Ниже представлен весь код программы. Скопируйте его в новый консольный проект и запустите — дополнительные файлы не требуются.

```csharp
using System;
using System.IO;
using GemBox.Spreadsheet;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize GemBox (free mode)
        SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

        // 2️⃣ Build a sample workbook
        var wb = new ExcelFile();
        var ws = wb.Worksheets.Add("Sales");

        ws.Cells[0, 0].Value = "Product";
        ws.Cells[0, 1].Value = "Price";

        ws.Cells[1, 0].Value = "Laptop";
        ws.Cells[1, 1].Value = 999.99;

        ws.Cells[2, 0].Value = "Mouse";
        ws.Cells[2, 1].Value = 25.5;

        ws.Cells[3, 0].Value = "Keyboard";
        ws.Cells[3, 1].Value = 45.0;

        // 3️⃣ Configure export options (custom CSV export)
        var tableExportOptions = new TableExportOptions
        {
            ExportAsString = true,
            CellExportHandler = (cell) =>
            {
                if (cell == null) return string.Empty;
                if (cell.Column == 1 && double.TryParse(cell.Value?.ToString(), out var price))
                    return "$" + price.ToString("0.00");
                return cell.StringValue;
            }
        };

        // 4️⃣ Save as CSV
        string outputPath = Path.Combine(Environment.CurrentDirectory, "customSalesReport.csv");
        ws.Save(outputPath, SaveOptions.CsvDefault, tableExportOptions);

        Console.WriteLine($"✅ CSV created at: {outputPath}");
    }
}
```

Запустите программу, откройте `customSalesReport.csv` в любом текстовом редакторе, и вы увидите красиво отформатированный вывод.

---

## Заключение

Теперь у вас есть надёжный, повторяемый шаблон для **экспорта таблицы в CSV** на C#. Используя `TableExportOptions` и **обработчик экспорта ячеек**, вы можете внедрять любую пользовательскую логику — символы валют, форматы дат, условное маскирование и т.д. Этот подход подходит как для небольших отчётов, так и для масштабных экспортов при сочетании со стримингом.

Что дальше? Попробуйте заменить `$` другими префиксами, выводить даты в ISO‑формате или генерировать несколько CSV‑файлов из разных листов одной книги. Принципы **кастомного экспорта CSV** остаются теми же.

Есть вопросы о граничных случаях, например, многокультурных данных или специальных символах? Оставляйте комментарий ниже, и happy coding!

## Что вам стоит изучить дальше?

Следующие руководства охватывают смежные темы, расширяющие техники, продемонстрированные в этом гайде. Каждый ресурс содержит полностью работающие примеры кода с пошаговыми объяснениями, чтобы вы могли освоить дополнительные возможности API и исследовать альтернативные подходы в своих проектах.

- [Load CSV & Export to JSON Using Aspose.Cells for .NET: A Comprehensive Guide](/cells/english/net/import-export/load-csv-export-json-aspose-cells-dotnet/)
- [Export Excel Csv Blank Rows Aspose Cells Net](/cells/hindi/net/workbook-operations/export-excel-csv-blank-rows-aspose-cells-net/)
- [Export Excel Csv Blank Rows Aspose Cells Net](/cells/spanish/net/workbook-operations/export-excel-csv-blank-rows-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}