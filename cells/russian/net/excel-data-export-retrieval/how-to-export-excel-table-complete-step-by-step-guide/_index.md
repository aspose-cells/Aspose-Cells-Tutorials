---
category: general
date: 2026-07-03
description: Узнайте, как экспортировать таблицу Excel в файл .txt и сохранить её
  в формате .txt с помощью C#. Экспортируйте данные Excel как обычный текст с полным
  примером кода.
draft: false
keywords:
- how to export excel table
- save excel table to .txt file
- export excel data as plain text
- Aspose.Cells export table
- C# Excel to text
language: ru
og_description: Как экспортировать таблицу Excel в виде простого текста. Это руководство
  показывает, как экспортировать данные Excel в виде простого текста и сохранить таблицу
  Excel в файл .txt с помощью Aspose.Cells.
og_title: Как экспортировать таблицу Excel – Полный учебник по C#
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Learn how to export Excel table to a .txt file and save Excel table
    to .txt file using C#. Export Excel data as plain text with full code example.
  headline: How to Export Excel Table – Complete Step‑by‑Step Guide
  type: TechArticle
tags:
- C#
- Excel
- Aspose.Cells
- File I/O
title: Как экспортировать таблицу Excel – полное пошаговое руководство
url: /ru/net/excel-data-export-retrieval/how-to-export-excel-table-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как экспортировать таблицу Excel – Полное пошаговое руководство

Когда‑нибудь задавались вопросом **как экспортировать таблицу Excel** без загрузки всей книги в память? Вы не одиноки. Во многих автоматизационных задачах целевая система принимает только простой файл `.txt`, поэтому нужно **сохранить таблицу Excel в файл .txt** быстро и надёжно.  

В этом руководстве мы пройдём чистое C#‑решение, которое **экспортирует данные Excel как обычный текст** с помощью Aspose.Cells. К концу вы получите готовую к запуску программу, поймёте, зачем нужна каждая строка, и увидите, как настроить экспорт под свои особые случаи.

## Что понадобится

- **Aspose.Cells for .NET** (любая современная версия, например 23.12).  
- .NET 6 SDK или новее — код также компилируется под .NET Core.  
- Пример `input.xlsx`, содержащий хотя бы одну таблицу Excel.  
- Текстовый редактор или IDE (Visual Studio, VS Code, Rider… выбирайте сами).

Никаких дополнительных пакетов NuGet помимо Aspose.Cells не требуется, и всё работает на Windows, Linux или macOS.

## Шаг 1: Создание проекта и импорт пространств имён

Сначала создайте консольное приложение и подключите необходимые пространства имён.

```csharp
using System;
using System.IO;
using Aspose.Cells;

namespace ExcelTableExport
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll place the export logic here.
        }
    }
}
```

> **Совет:** Если вы используете .NET CLI, выполните `dotnet new console -n ExcelTableExport`, а затем `dotnet add package Aspose.Cells` перед вставкой кода выше.

## Шаг 2: Загрузка книги и получение первого листа

Объект workbook представляет всю Excel‑книгу. Однократная загрузка снижает потребление памяти.

```csharp
// Step 2: Load the workbook and get the first worksheet
Workbook wb = new Workbook("YOUR_DIRECTORY/input.xlsx");
Worksheet ws = wb.Worksheets[0];
```

Почему мы берём первый лист? Во многих автоматически генерируемых отчётах данные находятся на первом листе, но вы можете изменить индекс или использовать `wb.Worksheets["SheetName"]` для листа с именем.

## Шаг 3: Получение первой таблицы, определённой на листе

Таблицы Excel (ListObjects) дают нам структурированные данные, делая экспорт предсказуемым.

```csharp
// Step 3: Retrieve the first table defined on the worksheet
Table tbl = ws.Tables[0];
```

Если в книге несколько таблиц, просто перебирайте `ws.Tables` или выбирайте по `tbl.Name`.

## Шаг 4: Настройка параметров экспорта — экспортировать каждую ячейку как строку

Aspose.Cells позволяет управлять форматом каждой ячейки при экспорте. Установка `ExportAsString` заставляет числа, даты и формулы становиться обычным текстом.

```csharp
// Step 4: Set up export options – export every cell as a string
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true
};
```

### Добавление пользовательского действия экспорта для удаления пробелов

Часто исходные данные содержат ведущие или завершающие пробелы. Их удаление делает итоговый файл `.txt` чище.

```csharp
// Define a custom export action to trim cell values before writing
exportOptions.CustomExport = (cell, writer) =>
{
    writer.Write(cell.StringValue.Trim());
};
```

Лямбда получает объект `Cell` и `TextWriter`. Здесь же можно добавить условную логику — например, заменить запятые точками с запятой для CSV‑подобного вывода.

## Шаг 5: Экспорт таблицы, начиная с ячейки A1, в текстовый файл

Теперь действительно записываем таблицу на диск. Метод `ExportTable` проходит по таблице построчно, применяя только что определённые параметры.

```csharp
// Step 5: Export the table starting at cell A1 to a text file
using (StreamWriter writer = new StreamWriter("YOUR_DIRECTORY/Table.txt"))
{
    ws.Cells.ExportTable(tbl, "A1", exportOptions, writer);
}
```

**Что вы увидите:** Каждая строка таблицы Excel становится отдельной строкой в `Table.txt`. Столбцы разделяются символом табуляции (`\t`) по умолчанию — идеально для последующего разбора.

### Пример ожидаемого вывода

Предположим, `input.xlsx` содержит таблицу с тремя столбцами (`ID`, `Name`, `Score`) и двумя строками данных, тогда `Table.txt` будет выглядеть так:

```
1    Alice    85
2    Bob      92
```

Обратите внимание, пробелы обрезаны, и всё представлено как обычный текст — именно то, что требуется в задаче **export excel data as plain text**.

## Обработка распространённых граничных случаев

| Ситуация | Что делать | Почему |
|-----------|------------|-----|
| **В таблице есть пустые ячейки** | Лямбда пишет `cell.StringValue.Trim()`, что возвращает пустую строку для пустых ячеек. | Сохраняет выравнивание столбцов без лишних символов. |
| **Нужен пользовательский разделитель** | Замените `writer.Write(cell.StringValue.Trim());` на `writer.Write($"{cell.StringValue.Trim()},");` и удалите завершающий разделитель после каждой строки. | Некоторые системы предпочитают запятые или вертикальные черты вместо табуляций. |
| **Большие листы (> 100 k строк)** | Используйте `ExportTableOptions` с `ExportAsString = true` и потоковую запись, как показано; Aspose.Cells обрабатывает строки в режиме стриминга, избегая ошибок OOM. | Обеспечивает масштабируемость. |
| **Несколько таблиц на одном листе** | Пройдитесь по `ws.Tables` и вызовите `ExportTable` для каждой, при желании добавив разделительную строку между экспортами. | Позволяет **save Excel table to .txt file** для каждой таблицы. |

## Полный рабочий пример

Ниже представлена полная программа, которую можно скопировать в `Program.cs`. Замените `YOUR_DIRECTORY` на абсолютный или относительный путь, существующий на вашем компьютере.

```csharp
using System;
using System.IO;
using Aspose.Cells;

namespace ExcelTableExport
{
    class Program
    {
        static void Main(string[] args)
        {
            // Load workbook
            Workbook wb = new Workbook("YOUR_DIRECTORY/input.xlsx");
            Worksheet ws = wb.Worksheets[0];

            // Get first table
            if (ws.Tables.Count == 0)
            {
                Console.WriteLine("No tables found on the first worksheet.");
                return;
            }
            Table tbl = ws.Tables[0];

            // Configure export options
            ExportTableOptions exportOptions = new ExportTableOptions
            {
                ExportAsString = true,
                CustomExport = (cell, writer) =>
                {
                    // Trim whitespace and write value
                    writer.Write(cell.StringValue.Trim());
                }
            };

            // Export to text file
            string outputPath = "YOUR_DIRECTORY/Table.txt";
            using (StreamWriter writer = new StreamWriter(outputPath))
            {
                ws.Cells.ExportTable(tbl, "A1", exportOptions, writer);
            }

            Console.WriteLine($"Table exported successfully to {outputPath}");
        }
    }
}
```

Запустите программу командой `dotnet run`. Если всё настроено правильно, вы увидите сообщение‑подтверждение и свежесозданный `Table.txt` с **export excel data as plain text**.

## Бонус: Визуальное подтверждение (по желанию)

Если хотите быстро увидеть скриншот получившегося файла, откройте его в любом текстовом редакторе. Ниже — пример изображения, показывающего ожидаемую разметку.

![скриншот как экспортировать таблицу Excel](https://example.com/images/export-excel-table.png "как экспортировать таблицу Excel")

*Alt text:* **как экспортировать таблицу Excel** — показывает вывод в виде обычного текста экспортированной таблицы Excel.

## Итоги и дальнейшие шаги

Мы рассмотрели всё, что нужно знать **how to export Excel table** с помощью Aspose.Cells: от загрузки книги до обрезки значений ячеек и записи чистого файла `.txt`.  

- Теперь вы понимаете, как **save Excel table to .txt file** с пользовательской логикой.  
- Вы можете адаптировать лямбду для обработки дат, чисел или собственных разделителей.  
- Для больших проектов стоит вынести логику в переиспользуемый метод или класс.

**Что дальше?** Попробуйте экспортировать несколько таблиц или переключить формат вывода на CSV, изменив разделитель. Можно также исследовать **export excel data as plain text** напрямую в сетевой поток для интеграций в реальном времени.

Есть вопросы или возникли проблемы? Оставляйте комментарий, и удачной разработки!

## Что изучать дальше?

Следующие руководства охватывают тесно связанные темы, расширяющие техники, продемонстрированные в этом гайде. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы в собственных проектах.

- [How to Export Excel Files in .NET Using Aspose.Cells: A Comprehensive Guide](/cells/english/net/workbook-operations/export-excel-files-net-aspose-cells-guide/)
- [How to Export Visible Excel Rows Using Aspose.Cells for .NET: A Step-by-Step Guide](/cells/english/net/workbook-operations/export-visible-rows-aspose-cells-dotnet/)
- [How to Combine Excel Sheets into a Single Text File Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/combine-excel-sheets-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}