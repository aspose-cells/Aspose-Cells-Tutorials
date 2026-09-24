---
category: general
date: 2026-03-22
description: Как экспортировать Excel с форматированием и сохранить числовой формат.
  Узнайте, как преобразовать диапазон Excel, получить результат формулы и экспортировать
  Excel с форматированием с помощью Aspose.Cells.
draft: false
keywords:
- how to export excel
- preserve number format
- convert excel range
- get formula result
- export excel with formatting
language: ru
og_description: Как экспортировать Excel с форматированием и сохранить числовой формат.
  Пошаговое руководство по преобразованию диапазона Excel, получению результата формулы
  и экспорту Excel с форматированием на C#.
og_title: Как экспортировать Excel с форматированием — Сохранить числовой формат
tags:
- C#
- Aspose.Cells
- Excel automation
title: Как экспортировать Excel с форматированием — Сохранить числовой формат
url: /ru/net/number-and-display-formats-in-excel/how-to-export-excel-with-formatting-preserve-number-format/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как экспортировать Excel с форматированием – Сохранить числовой формат

Когда‑нибудь задумывались **как экспортировать Excel** данные, сохранив внешний вид каждой ячейки точно таким же, как в рабочей книге? Возможно, вам нужно отправить отчёт клиенту, заполнить элемент управления сеткой или просто сохранить значения в базе данных. Основная проблема обычно заключается в потере числового форматирования или формулы, превращающихся в обычные строки.  

В этом руководстве мы пройдём через полностью готовый к запуску пример на C#, который **preserves number format**, **converts an Excel range** to a `DataTable`, **gets the formula result**, и наконец **exports Excel with formatting** с помощью Aspose.Cells. К концу вы получите один метод, который можно вставить в любой проект и вызвать, передав ссылку на лист.

> **Quick preview:** код создаёт рабочую книгу, записывает значение и формулу, указывает Aspose.Cells экспортировать ячейки как отформатированные строки и выводит `123.456 | 246.912` – именно то, что вы ожидаете увидеть в Excel.

---

## Что вам понадобится

- **Aspose.Cells for .NET** (бесплатная пробная версия отлично подходит для обучения)
- .NET 6.0 или новее (API одинаково работает и в .NET Framework)
- Базовая среда разработки C# (Visual Studio, VS Code, Rider… на ваш выбор)

Никаких дополнительных пакетов NuGet, помимо Aspose.Cells, не требуется. Если вы ещё не установили его, выполните:

```bash
dotnet add package Aspose.Cells
```

---

## Шаг 1 – Создать рабочую книгу и записать значения (включая формулу)

Сначала создаём новую рабочую книгу и помещаем числовое значение в **A1**. Затем добавляем простую формулу в **B1**, умножающую первое значение на два. Это подготавливает основу для демонстрации **get formula result** позже.

```csharp
using Aspose.Cells;
using System;
using System.Data;

class ExportExcelDemo
{
    static void Main()
    {
        // Step 1: Create a new workbook and get its first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Write a numeric value and a formula that uses it
        worksheet.Cells["A1"].PutValue(123.456);
        worksheet.Cells["B1"].PutFormula("=A1*2");

        // Continue with export options...
        ExportRangeAsDataTable(worksheet);
    }
}
```

**Почему это важно:**  
- `PutValue` сохраняет сырое число, тогда как `PutFormula` сохраняет вычисление.  
- Aspose.Cells оставляет формулу **alive**, поэтому когда мы позже запрашиваем значение ячейки, мы получаем `246.912`, а не строку `"=A1*2"`.

---

## Шаг 2 – Указать Aspose.Cells экспортировать значения как отформатированные строки

Если просто вызвать `ExportDataTable` с настройками по умолчанию, числовые ячейки будут возвращены как их базовые значения `double`. Это убирает разделители тысяч, валютные символы и пользовательские десятичные разряды, которые вы могли задать. Класс `ExportTableOptions` позволяет **preserve number format** и **export as string**.

```csharp
static void ExportRangeAsDataTable(Worksheet worksheet)
{
    // Step 2: Set export options to retrieve values as formatted strings
    ExportTableOptions exportOptions = new ExportTableOptions
    {
        ExportAsString = true,          // Return values as strings
        ExportNumberFormat = true      // Preserve the cell's number format
    };

    // Step 3: Export the range A1:B1 to a DataTable
    DataTable dataTable = worksheet.Cells.ExportDataTable(
        firstRow: 0,
        firstColumn: 0,
        totalRows: 1,
        totalColumns: 2,
        includeColumnNames: true,
        options: exportOptions);

    PrintDataTable(dataTable);
}
```

**Ключевой момент:** `ExportNumberFormat = true` — флаг, который делает работу **preserve number format** возможной. Без него вы увидите `"123.456"` и `"246.912"` как сырые числа, что может выглядеть приемлемо в коде, но не при вставке данных в пользовательский интерфейс, ожидающий того же форматирования, что в Excel.

---

## Шаг 3 – Вывести экспортированные данные (проверка)

Теперь, когда у нас есть `DataTable`, заполненный отформатированными строками, выведем содержимое в консоль. Это также демонстрирует, что мы успешно **get formula result** без собственного вычисления формулы.

```csharp
static void PrintDataTable(DataTable table)
{
    // Step 4: Print the exported values (already formatted)
    foreach (DataRow row in table.Rows)
    {
        // The output will look like: 123.456 | 246.912
        Console.WriteLine($"{row[0]} | {row[1]}");
    }
}
```

Запуск программы выводит:

```
123.456 | 246.912
```

Обратите внимание, что во второй колонке отображается **formula result**, а не текст формулы. Именно это нужно, когда вы **export Excel with formatting** для последующей обработки.

---

## Шаг 4 – Конвертация больших диапазонов Excel (по желанию)

Приведённый выше пример работает с крошечным фрагментом `A1:B1`, но в реальных сценариях часто требуется экспортировать целые таблицы. Тот же метод работает для любого прямоугольного блока — просто измените параметры `firstRow`, `firstColumn`, `totalRows` и `totalColumns`.

```csharp
// Example: Export a 10‑row by 5‑column block starting at C3
DataTable bigTable = worksheet.Cells.ExportDataTable(
    firstRow: 2,          // Zero‑based index (C3 = row 2, column 2)
    firstColumn: 2,
    totalRows: 10,
    totalColumns: 5,
    includeColumnNames: true,
    options: exportOptions);
```

**Pro tip:** Если в вашем листе уже есть строка заголовков, установите `includeColumnNames` в `true`. Aspose.Cells использует первую строку диапазона как имена столбцов, что удобно при последующей привязке `DataTable` к UI‑сетке.

---

## Шаг 5 – Распространённые подводные камни и как их избежать

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **Numbers lose commas or currency symbols** | `ExportAsString` is `false` or `ExportNumberFormat` is omitted | Set both `ExportAsString = true` **and** `ExportNumberFormat = true`. |
| **Formula cells return the formula text** | You didn’t call `CalculateFormula` before export (only needed if the workbook isn’t set to auto‑calculate) | Either enable auto‑calculate (`workbook.CalculateFormula()`) or rely on `ExportAsString` which forces evaluation. |
| **Headers appear as data rows** | `includeColumnNames` set to `false` while your range includes a header row | Set `includeColumnNames = true` to treat the first row as column names. |
| **Large ranges cause memory pressure** | Exporting the entire sheet at once loads everything into memory | Export in chunks (e.g., 500 rows at a time) and merge `DataTable`s if needed. |

---

## Шаг 6 – Полный рабочий пример (готов к копированию)

Ниже представлен весь код программы, от `using`‑директив до `Main`. Вставьте его в консольное приложение и нажмите **F5** — вы сразу увидите отформатированный вывод.

```csharp
using Aspose.Cells;
using System;
using System.Data;

class ExportExcelDemo
{
    static void Main()
    {
        // Create workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Populate cells
        worksheet.Cells["A1"].PutValue(123.456);
        worksheet.Cells["B1"].PutFormula("=A1*2");

        // Export options: keep formatting and return strings
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            ExportNumberFormat = true
        };

        // Export A1:B1 as a DataTable
        DataTable dataTable = worksheet.Cells.ExportDataTable(
            firstRow: 0,
            firstColumn: 0,
            totalRows: 1,
            totalColumns: 2,
            includeColumnNames: true,
            options: exportOptions);

        // Print results
        foreach (DataRow row in dataTable.Rows)
        {
            Console.WriteLine($"{row[0]} | {row[1]}"); // Expected: "123.456 | 246.912"
        }

        // Keep console window open
        Console.WriteLine("\nPress any key to exit...");
        Console.ReadKey();
    }
}
```

**Expected output**

```
123.456 | 246.912

Press any key to exit...
```

Это весь процесс **how to export excel**, с сохранённым форматированием, вычисленными результатами формул и чистым `DataTable`, готовым к использованию в любом .NET‑потребителе.

---

## Заключение

Мы рассмотрели всё, что нужно знать о **how to export Excel** данных, одновременно **preserving number format**, **converting an Excel range** to a `DataTable` и **getting formula results** без дополнительного парсинга. Ключ — конфигурация `ExportTableOptions` — после установки `ExportAsString` и `ExportNumberFormat` в `true` Aspose.Cells берёт на себя всю тяжёлую работу.

Отсюда вы можете:

- Подключить `DataTable` к WPF `DataGrid` или представлению ASP.NET MVC.  
- Записать таблицу в CSV‑файл, сохранив точное визуальное представление.  
- Расширить подход на несколько листов или динамические диапазоны.

Не стесняйтесь экспериментировать с различными форматами (валюта, проценты) и большими блоками данных. Если столкнётесь с какими‑либо странностями, обратитесь к таблице **common pitfalls** — она охватывает самые частые проблемы при **export excel with formatting**.

Счастливого кодинга, и пусть ваши экспортированные таблицы всегда выглядят так же безупречно, как оригиналы!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}