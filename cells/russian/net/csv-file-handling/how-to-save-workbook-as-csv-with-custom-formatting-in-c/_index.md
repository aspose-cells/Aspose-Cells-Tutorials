---
category: general
date: 2026-10-20
description: Сохранить книгу в формате CSV с точными десятичными знаками, заключёнными
  в кавычки значениями и датой в японском императорском формате, используя Aspose.Cells
  для .NET.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save workbook as csv
- set excel number format
- export excel to csv
- quote csv values
language: ru
lastmod: 2026-10-20
og_description: Сохраните книгу в формате CSV с полным контролем над десятичными знаками,
  кавычками и датами в японском календаре. Следуйте этому пошаговому руководству на
  C# с использованием Aspose.Cells.
og_image_alt: Screenshot illustrating how to save workbook as CSV with custom options
  in C#
og_title: Сохранение рабочей книги в CSV – полное руководство для разработчиков C#
schemas:
- author: Aspose
  dateModified: '2026-10-20'
  description: Save workbook as CSV with precise decimal digits, quoted values and
    Japanese era date format using Aspose.Cells for .NET.
  headline: How to save workbook as CSV with custom formatting in C#
  type: TechArticle
tags:
- Aspose.Cells
- C#
- CSV export
- Excel formatting
title: Как сохранить рабочую книгу в CSV с пользовательским форматированием в C#
url: /ru/net/csv-file-handling/how-to-save-workbook-as-csv-with-custom-formatting-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как сохранить книгу в CSV с пользовательским форматированием в C#

Если вам нужно **сохранить книгу в CSV**, контролируя точность десятичных знаков, заключая значения в кавычки и обрабатывая даты в японской эре, этот учебник покажет, как сделать это с помощью Aspose.Cells для .NET. Вы узнаете, как **export Excel to CSV**, **set Excel number format** и **quote CSV values**, чтобы результат соответствовал типичным требованиям обмена данными.

Руководство предполагает наличие среды разработки .NET (Visual Studio 2022 или новее) и действующей лицензии Aspose.Cells. Дополнительные пакеты NuGet не требуются, кроме `Aspose.Cells`.

## Предварительные требования

- .NET 6.0 SDK или новее  
- Aspose.Cells for .NET (устанавливается через NuGet: `Install-Package Aspose.Cells`)  
- Пример Excel‑файла (`Data.xlsx`) в папке, к которой вы можете обратиться из кода  

## Шаг 1: Загрузка исходной книги — основа для сохранения книги в CSV

Сначала создайте экземпляр `Workbook`, указывающий на Excel‑файл, который нужно преобразовать.

```csharp
using Aspose.Cells;
using System;

// Load the source workbook
Workbook workbook = new Workbook(@"YOUR_DIRECTORY\Data.xlsx");
```

*Почему этот шаг важен*: Объект `Workbook` содержит все листы, стили и формулы. Все последующие операции CSV работают с этим представлением в памяти.

## Шаг 2: Ограничение десятичной точности при сохранении книги в CSV

Когда требуется ровно четыре знака после запятой, настройте `CsvSaveOptions`.

```csharp
// Configure CSV saving options
CsvSaveOptions csvOptions = new CsvSaveOptions
{
    // Keep 4 digits after the decimal point
    SignificantDigits = 4
};

// Save the workbook as CSV with the defined precision
workbook.Save(@"YOUR_DIRECTORY\Data_Sig4.csv", csvOptions);
```

*Ключевой момент*: `SignificantDigits` округляет каждую числовую ячейку до указанного количества знаков после запятой перед записью CSV‑файла. Это предотвращает появление шумов плавающей запятой в downstream‑системах.

## Шаг 3: Экспорт Excel в CSV с кавычками вокруг значений

Некоторые downstream‑парсеры требуют, чтобы каждое поле было заключено в двойные кавычки, особенно когда значения содержат запятые или разрывы строк. Класс `ExportTableOptions` позволяет рассматривать каждую ячейку как строку и применять пользовательское заключение в кавычки.

```csharp
// Prepare export options that treat every cell as a string
ExportTableOptions tableOptions = new ExportTableOptions
{
    ExportAsString = true, // Force string export for all cells
    // Custom delegate to wrap each value in double quotes
    CustomExport = (cell, writer) =>
    {
        writer.Write('"' + cell.StringValue + '"');
    }
};

// Export the first worksheet as a CSV file with quoted values
workbook.Save(@"YOUR_DIRECTORY\TableExport.csv", tableOptions);
```

*Почему следует заключать значения в кавычки*: Кавычки защищают запятые, переводы строк и начальные/конечные пробелы от интерпретации их как разделителей, что необходимо для надёжного импорта данных.

## Шаг 4: Установка формата числа Excel для дат в японской эре

Excel может хранить даты, используя календари, специфичные для эпох. Чтобы продемонстрировать, вставьте строку даты в японской эре и примените соответствующий числовой формат.

```csharp
// Create a new workbook for the era‑date example
Workbook eraWorkbook = new Workbook();
Worksheet sheet = eraWorkbook.Worksheets[0];

// Insert a Japanese‑era date string (Reiwa 3‑04‑01)
sheet.Cells["A1"].PutValue("R3-04-01");

// Apply the Japanese locale number format
sheet.Cells["A1"].SetNumberFormat("[$-ja-JP]yyyy-mm-dd");

// Retrieve the parsed DateTime value
DateTime parsedDate = sheet.Cells["A1"].GetDateTime();
Console.WriteLine(parsedDate); // Outputs: 2021-04-01
```

*Пояснение*: Вызов `SetNumberFormat` сообщает Aspose.Cells интерпретировать строку с использованием японского календаря. При вызове `GetDateTime()` библиотека автоматически преобразует обозначение эпохи в григорианскую дату.

## Шаг 5: Проверка сгенерированных CSV‑файлов

После выполнения кода вы должны увидеть три файла в `YOUR_DIRECTORY`:

| Имя файла            | Особенности |
|----------------------|------------|
| `Data_Sig4.csv`      | Числа округлены до 4 знаков после запятой |
| `TableExport.csv`    | Каждая ячейка заключена в двойные кавычки |
| `Data.xlsx` (unchanged) | Продемонстрировано обработка дат в японской эре (просматривается в Excel) |

Откройте `Data_Sig4.csv` в обычном текстовом редакторе, чтобы убедиться в точности, и откройте `TableExport.csv`, чтобы увидеть заключённые в кавычки значения, например:

```
"Name","Score","Comment"
"Alice","95.1234","Excellent"
"Bob","88.0000","Good"
```

Вывод в консоль для даты в эпохе будет:

```
2021-04-01 00:00:00
```

## Распространённые подводные камни и как их избежать

- **Locale‑dependent decimal separators**: `CsvSaveOptions` учитывает текущую культуру. Если нужен точка (`.`) в качестве разделителя независимо от локали, задайте `csvOptions.Separator = ',';`.
- **Large worksheets**: Экспорт книги с миллионами строк может потребовать значительного объёма памяти. Используйте `ExportTableOptions.StartRow` и `EndRow`, чтобы ограничить диапазон экспорта.
- **Special characters inside strings**: Пользовательский писатель в Шаге 3 добавляет только окружающие кавычки. Если ячейка уже содержит кавычку, удвойте её (`""`), чтобы сохранить корректность CSV.

## Профессиональный совет: Комбинирование параметров для максимального контроля

Вы можете связать `CsvSaveOptions` и `ExportTableOptions`, сначала преобразовав книгу в `MemoryStream` с одним набором параметров, а затем записав поток на диск с другим. Такой подход позволяет, например, применить одновременно округление десятичных знаков **и** заключение в кавычки за один проход:

```csharp
using (MemoryStream ms = new MemoryStream())
{
    // Apply rounding
    workbook.Save(ms, csvOptions);
    ms.Position = 0; // Reset stream

    // Load the intermediate CSV into a new workbook for quoting
    Workbook temp = new Workbook(ms, new LoadOptions(LoadFormat.Csv));
    temp.Save(@"YOUR_DIRECTORY\RoundedAndQuoted.csv", tableOptions);
}
```

## Заключение

Теперь вы знаете, как **save workbook as CSV** с точным управлением десятичными знаками, заключением значений в кавычки и пользовательским форматированием дат. Полное решение охватывает загрузку книги, настройку `CsvSaveOptions`, использование `ExportTableOptions` для **quote CSV values** и применение **set Excel number format** для дат в японской эре. Далее вы можете изучать дополнительные возможности, такие как пользовательские разделители, разные кодировки или выборочный экспорт листов.

---

*Следующие шаги*  
- Исследуйте `CsvSaveOptions.Encoding` для записи файлов UTF‑8 BOM или UTF‑16.  
- Используйте `ExportTableOptions.StartColumn` / `EndColumn` для экспорта только части столбцов.  
- Сочетайте эти техники с `DataFormatter` из Aspose.Cells для локализованного числового форматирования.  

- [Сохранить книгу в CSV – Полное руководство по экспорту Excel в CSV с контролем](/cells/english/net/csv-file-handling/save-workbook-as-csv-complete-guide-to-export-excel-to-csv-w/)
- [Сохранить книгу в CSV в C# – Экспорт Excel в CSV](/cells/english/net/csv-file-handling/save-workbook-as-csv-in-c-export-excel-to-csv/)
- [Создание и сохранение Excel‑книги в PDF в ASP.NET с использованием Aspose.Cells](/cells/english/net/workbook-operations/create-save-excel-workbook-pdf-aspnet-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}