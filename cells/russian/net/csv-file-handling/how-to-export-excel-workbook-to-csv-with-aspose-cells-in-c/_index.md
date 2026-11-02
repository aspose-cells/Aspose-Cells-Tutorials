---
category: general
date: 2026-09-27
description: Узнайте, как экспортировать книгу Excel в CSV с помощью Aspose.Cells.
  Это пошаговое руководство также показывает, как эффективно преобразовать файл xlsx
  в CSV.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel workbook to csv
- convert xlsx file to csv
language: ru
lastmod: 2026-09-27
og_description: Экспортируйте книгу Excel в CSV с помощью Aspose.Cells. Следуйте этому
  руководству, чтобы быстро и надёжно преобразовать файл xlsx в CSV.
og_image_alt: Screenshot of C# code that exports an Excel workbook to CSV
og_title: Экспорт книги Excel в CSV на C# – полное руководство
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Learn how to export Excel workbook to CSV using Aspose.Cells. This
    step‑by‑step guide also shows how to convert xlsx file to CSV efficiently.
  headline: How to export Excel workbook to CSV with Aspose.Cells in C#
  type: TechArticle
- description: Learn how to export Excel workbook to CSV using Aspose.Cells. This
    step‑by‑step guide also shows how to convert xlsx file to CSV efficiently.
  name: How to export Excel workbook to CSV with Aspose.Cells in C#
  steps:
  - name: Common verification steps
    text: 1. **Open in Notepad** – Confirms the file is plain text and uses the expected
      delimiter. 2. **Import into Excel** – Choose “Data → From Text/CSV” and verify
      that numbers appear correctly without extra columns. 3. **Load into a database**
      – Use a `COPY` command (PostgreSQL) or `BULK INSERT` (SQL Ser
  - name: Expected console output
    text: '``` Sample workbook created at "YOUR_DIRECTORY/input.xlsx". Workbook exported
      to CSV at "YOUR_DIRECTORY/numbers.csv". ```'
  - name: Expected CSV content
    text: '``` Sample Numbers 1234.6 0.00012346 -9876.5 3.1416 2.7183 ```'
  type: HowTo
tags:
- Excel
- CSV
- C#
- Aspose.Cells
title: Как экспортировать книгу Excel в CSV с помощью Aspose.Cells на C#
url: /ru/net/csv-file-handling/how-to-export-excel-workbook-to-csv-with-aspose-cells-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Экспорт рабочей книги Excel в CSV с помощью Aspose.Cells на C#

Если вам нужно **экспортировать рабочую книгу Excel в CSV**, это руководство покажет, как сделать это с помощью Aspose.Cells на C#. Вы также увидите, как **конвертировать файл xlsx в CSV**, контролируя десятичные разделители и значимые цифры.

Работа с CSV‑файлами распространена, когда необходимо передать данные в аналитические конвейеры, импортировать их в базы данных или делиться лёгкими таблицами. Пример ниже охватывает весь рабочий процесс — от установки библиотеки до проверки результата — поэтому вы можете сразу вставить код в любой .NET‑проект и запустить его.

## Что вы узнаете

* Установить Aspose.Cells через NuGet.  
* Загрузить существующую рабочую книгу `.xlsx` или создать её с нуля.  
* Настроить `CsvSaveOptions` для управления форматированием.  
* Сохранить рабочую книгу в файл CSV.  
* Обрабатывать особые случаи, такие как локаль‑зависимые десятичные разделители и высокая точность чисел.

Никакие внешние инструменты не требуются; всё работает внутри стандартного консольного приложения .NET.

## Требования

| Требование | Почему это важно |
|------------|------------------|
| .NET 6.0 SDK или новее | Обеспечивает среду выполнения для консольного приложения C#. |
| Visual Studio 2022 (или любой IDE) | Обеспечивает простое создание проекта и отладку. |
| Интернет‑соединение (только при первой установке) | Необходимо для загрузки пакета Aspose.Cells NuGet. |
| Исходный Excel‑файл (`input.xlsx`) | Исходная рабочая книга, которую вы хотите экспортировать. |

> **Подсказка:** Если у вас нет файла `input.xlsx`, руководство создаёт простую рабочую книгу в коде, чтобы вы могли протестировать весь процесс без внешних файлов.

## Шаг 1: Установить Aspose.Cells

Откройте терминал в папке проекта и выполните:

```bash
dotnet add package Aspose.Cells
```

Эта команда добавит последнюю стабильную версию Aspose.Cells в ваш проект, предоставив доступ к `Workbook`, `CsvSaveOptions` и другим мощным API.

## Шаг 2: Создать каркас консольного приложения

Создайте новое консольное приложение, если у вас его ещё нет:

```bash
dotnet new console -n ExcelToCsvDemo
cd ExcelToCsvDemo
```

Откройте `Program.cs` и замените его содержимое полным кодом, показанным в следующих разделах.

## Шаг 3: Загрузить или создать рабочую книгу для экспорта

Первый логический шаг — получить экземпляр `Workbook`. Вы можете либо загрузить существующий файл `.xlsx`, либо программно сгенерировать рабочую книгу.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Define the paths (adjust as needed)
        string inputPath = @"YOUR_DIRECTORY/input.xlsx";
        string outputPath = @"YOUR_DIRECTORY/numbers.csv";

        Workbook wb;

        // Try to load the existing workbook; if it doesn't exist, create a sample one.
        if (System.IO.File.Exists(inputPath))
        {
            wb = new Workbook(inputPath);
            Console.WriteLine($"Loaded workbook from \"{inputPath}\".");
        }
        else
        {
            wb = CreateSampleWorkbook();
            wb.Save(inputPath);
            Console.WriteLine($"Sample workbook created at \"{inputPath}\".");
        }

        // Continue with CSV conversion...
        ExportToCsv(wb, outputPath);
    }

    // Helper method to generate a workbook with numeric data
    private static Workbook CreateSampleWorkbook()
    {
        var workbook = new Workbook();
        var cells = workbook.Worksheets[0].Cells;

        // Populate cells with various numeric formats
        cells["A1"].PutValue(1234.56789);
        cells["A2"].PutValue(0.000123456);
        cells["A3"].PutValue(-9876.54321);
        cells["A4"].PutValue(3.1415926535);
        cells["A5"].PutValue(2.71828);

        // Add a header row
        cells["A0"].PutValue("Sample Numbers");

        return workbook;
    }
```

**Почему это важно:**  
Загрузка существующей книги позволяет сохранить формулы, стили и несколько листов. Создание примерной книги гарантирует, что руководство будет работать даже при отсутствии исходного файла.

## Шаг 4: Настроить параметры сохранения CSV

`CsvSaveOptions` позволяет точно настроить вывод CSV. Во многих локалях запятая (`','`) используется как десятичный разделитель, что может нарушить разбор чисел, когда сам CSV использует запятые как разделители полей. Установка `DecimalSeparator` в точку (`'.'`) устраняет конфликт. `SignificantDigits` обрезает лишнюю точность, уменьшая размер файла.

```csharp
    // Export method encapsulating CSV configuration
    private static void ExportToCsv(Workbook workbook, string csvPath)
    {
        // Step 4: Configure CSV save options
        var csvOptions = new CsvSaveOptions
        {
            DecimalSeparator = '.',          // Use a dot for decimal separation
            SignificantDigits = 5,           // Keep only 5 significant digits
            Encoding = System.Text.Encoding.UTF8,
            // Optional: Force all values to be quoted to preserve leading zeros
            // QuoteAllFields = true
        };

        // Step 5: Save the workbook as a CSV file using the configured options
        workbook.Save(csvPath, csvOptions);
        Console.WriteLine($"Workbook exported to CSV at \"{csvPath}\".");
    }
}
```

**Почему следует задавать эти параметры:**  

* **DecimalSeparator** — предотвращает неверное трактование чисел вроде `1,234` как двух отдельных полей.  
* **SignificantDigits** — сокращает шум плавающей запятой (например, `123.456789` становится `123.46`).  
* **Encoding** — UTF‑8 гарантирует сохранение символов, не входящих в ASCII (например, букв с диакритическими знаками).

## Шаг 5: Проверить результат CSV

После выполнения программы откройте `numbers.csv` в текстовом редакторе или табличном приложении. Вы должны увидеть примерно следующее:

```
Sample Numbers
1234.6
0.00012346
-9876.5
3.1416
2.7183
```

Обратите внимание, что каждое значение сохраняет точность в пять знаков и использует точку в качестве десятичного разделителя.

### Общие шаги проверки

1. **Открыть в Блокноте** — подтверждает, что файл является простым текстом и использует ожидаемый разделитель.  
2. **Импортировать в Excel** — выберите «Данные → Из текста/CSV» и проверьте, что числа отображаются корректно без лишних столбцов.  
3. **Загрузить в базу данных** — используйте команду `COPY` (PostgreSQL) или `BULK INSERT` (SQL Server), чтобы убедиться, что формат соответствует целевой системе.

## Особые случаи и их обработка

| Ситуация | Рекомендуемый подход |
|----------|----------------------|
| **Локаль использует запятую как десятичный разделитель** | Оставьте `DecimalSeparator = '.'` и при необходимости оберните поля в кавычки (`QuoteAllFields = true`). |
| **Большие целые числа более 15 знаков** | Установите `CsvSaveOptions.IsConvertNumericToText = true`, чтобы сохранить точные значения как текст. |
| **Несколько листов** | Пройдитесь по `workbook.Worksheets` и экспортируйте каждый лист в отдельный CSV‑файл, добавив имя листа к имени файла. |
| **Формулы, требующие вычисления** | Вызовите `workbook.CalculateFormula()` перед сохранением, чтобы формулы были рассчитаны. |
| **Специальные символы (например, разрывы строк) в ячейках** | Включите `CsvSaveOptions.EscapeMode = CsvEscapeMode.QuoteAll`, чтобы заключить проблемные ячейки в кавычки. |

## Полный, готовый к запуску пример

Ниже приведён полный файл `Program.cs`. Скопируйте его в проект `ExcelToCsvDemo` и выполните `dotnet run`.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Adjust these paths to match your environment
        string inputPath = @"YOUR_DIRECTORY/input.xlsx";
        string outputPath = @"YOUR_DIRECTORY/numbers.csv";

        Workbook wb;

        // Load an existing workbook or create a sample one
        if (System.IO.File.Exists(inputPath))
        {
            wb = new Workbook(inputPath);
            Console.WriteLine($"Loaded workbook from \"{inputPath}\".");
        }
        else
        {
            wb = CreateSampleWorkbook();
            wb.Save(inputPath);
            Console.WriteLine($"Sample workbook created at \"{inputPath}\".");
        }

        // Export to CSV with custom options
        ExportToCsv(wb, outputPath);
    }

    // Generates a simple workbook with numeric data for demonstration
    private static Workbook CreateSampleWorkbook()
    {
        var workbook = new Workbook();
        var cells = workbook.Worksheets[0].Cells;

        cells["A1"].PutValue(1234.56789);
        cells["A2"].PutValue(0.000123456);
        cells["A3"].PutValue(-9876.54321);
        cells["A4"].PutValue(3.1415926535);
        cells["A5"].PutValue(2.71828);
        cells["A0"].PutValue("Sample Numbers");

        return workbook;
    }

    // Handles CSV conversion with formatting options
    private static void ExportToCsv(Workbook workbook, string csvPath)
    {
        var csvOptions = new CsvSaveOptions
        {
            DecimalSeparator = '.',
            SignificantDigits = 5,
            Encoding = System.Text.Encoding.UTF8,
            // Uncomment the next line if you need all fields quoted
            // QuoteAllFields = true
        };

        workbook.Save(csvPath, csvOptions);
        Console.WriteLine($"Workbook exported to CSV at \"{csvPath}\".");
    }
}
```

### Ожидаемый вывод в консоли

```
Sample workbook created at "YOUR_DIRECTORY/input.xlsx".
Workbook exported to CSV at "YOUR_DIRECTORY/numbers.csv".
```

### Ожидаемое содержимое CSV

```
Sample Numbers
1234.6
0.00012346
-9876.5
3.1416
2.7183
```

## Лучшие практики и советы по производительности

* **Повторное использование `CsvSaveOptions`** — если вы экспортируете множество рабочих книг пакетно, создайте один экземпляр параметров и переиспользуйте его, чтобы сократить количество выделений памяти.  
* **Потоковый вывод** — для очень больших книг используйте `workbook.Save(Stream, csvOptions)`, чтобы избежать записи промежуточных файлов на диск.  
* **Параллельная обработка** — при конвертации  

## Что изучать дальше?

Следующие руководства охватывают тесно связанные темы, построенные на техниках, продемонстрированных в этом руководстве. Каждый ресурс включает полностью рабочие примеры кода с пошаговыми объяснениями, помогая вам освоить дополнительные возможности API и исследовать альтернативные подходы в собственных проектах.

- [Экспорт Excel в CSV с пустыми строками с помощью Aspose.Cells для .NET](/cells/english/net/workbook-operations/export-excel-csv-blank-rows-aspose-cells-net/)
- [Конвертация Excel в CSV с использованием Aspose.Cells .NET: Полное руководство](/cells/english/net/workbook-operations/load-save-excel-csv-aspose-cells-dotnet/)
- [Сохранить рабочую книгу как CSV в C# — Экспорт Excel в CSV](/cells/english/net/csv-file-handling/save-workbook-as-csv-in-c-export-excel-to-csv/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}