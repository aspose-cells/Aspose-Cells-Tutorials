---
category: general
date: 2026-10-26
description: Пользовательские ExportTableOptions при ExportAsStrin позволяют экспортировать
  данные Excel в виде строк в C#. Следуйте пошаговому руководству, чтобы настроить
  и выполнить экспорт.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- Custom ExportTableOptions when ExportAsStrin
- how to export excel as string
- ExportTableOptions C#
- Excel to DataTable string conversion
- Aspose.Cells export as string
language: ru
lastmod: 2026-10-26
og_description: Пользовательские ExportTableOptions при включённом ExportAsStrin позволяют
  выполнять экспорт Excel только в виде строк. Узнайте точные шаги настройки и запуска
  экспорта в C#.
og_image_alt: Code snippet showing ExportTableOptions configuration for string export
og_title: Пользовательские параметры ExportTableOptions при ExportAsString – экспорт
  Excel в виде строки в C#
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Custom ExportTableOptions when ExportAsStrin lets you export Excel
    data as strings in C#. Follow the step‑by‑step guide to configure and run the
    export.
  headline: Custom ExportTableOptions when ExportAsStrin for Excel
  type: TechArticle
tags:
- C#
- Aspose.Cells
- Excel
- DataTable
title: Пользовательские ExportTableOptions при ExportAsStrin для Excel
url: /ru/net/excel-data-export-retrieval/custom-exporttableoptions-when-exportasstrin-for-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Пользовательские ExportTableOptions при ExportAsStrin – экспорт Excel как строка в C#

Если вам нужны **Custom ExportTableOptions when ExportAsStrin**, чтобы получить значение каждой ячейки в виде простой строки, это руководство покажет, как это сделать. Независимо от того, создаёте ли вы конвейер импорта данных или вам нужен чистый CSV‑готовый дамп, вы увидите, почему настройка параметров таким образом избегает неожиданностей при преобразовании типов.

В этом руководстве вы узнаете **как экспортировать excel как строку** с использованием библиотеки Aspose.Cells, увидите полный, исполняемый код и поймёте логику каждой настройки. Внешняя документация не требуется — всё, что нужно, находится здесь.

## Требования

* .NET 6.0 SDK или более поздняя версия, установленная  
* Visual Studio 2022 (или любой IDE, поддерживающий .NET)  
* Пакет Aspose.Cells for .NET (установить через NuGet: `Install-Package Aspose.Cells`)  
* Excel‑файл (`sample.xlsx`), размещённый в корневой папке проекта  

Эти элементы — единственные зависимости; код работает на Windows, Linux или macOS без дополнительных библиотек.

## Шаг 1: Загрузите рабочую книгу, которую хотите экспортировать

Первое, что вы делаете, используя **Custom ExportTableOptions when ExportAsStrin**, — получаете объект `Worksheet` из загруженной рабочей книги. Этот объект предоставляет доступ к строкам, столбцам и API экспорта.

```csharp
using Aspose.Cells;
using System.Data;

// Load the workbook from disk
Workbook workbook = new Workbook("sample.xlsx");

// Get the first worksheet (index 0)
Worksheet worksheet = workbook.Worksheets[0];
```

*Почему это важно:*  
`Workbook` читает файл один раз и сохраняет всю информацию о форматировании в памяти. Выбирая конкретный `Worksheet`, вы ограничиваете область экспорта и избегаете ненужной обработки скрытых листов.

## Шаг 2: Настройте ExportTableOptions с ExportAsString = true

Суть **Custom ExportTableOptions when ExportAsStrin** заключается в объекте `ExportTableOptions`. Установка `ExportAsString` заставляет экспортер рассматривать каждую ячейку как строку, независимо от её исходного типа данных (дата, число, логическое значение и т.д.). Включение `PreserveFormatting` сохраняет визуальный стиль (например, символы валют) в результирующей строке.

```csharp
// Create and configure the export options
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true,          // Export every cell value as a string
    PreserveFormatting = true      // Keep the original cell formatting
};
```

*Почему это важно:*  
Когда вы позже вызываете `ExportDataTable`, библиотека обычно пытается определить .NET‑тип каждого столбца. При `ExportAsString = true` этот шаг определения пропускается, предотвращая неожиданные преобразования `DateTime` или `double`, которые могут нарушить работу последующих CSV‑парсеров.

## Шаг 3: Экспорт диапазона в DataTable с использованием пользовательских параметров

Теперь вы можете экспортировать прямоугольный диапазон (строки 0‑9, столбцы 0‑4) из листа. Метод возвращает `DataTable`, где каждое поле имеет тип `string`.

```csharp
// Export rows 0‑9 and columns 0‑4 (5 columns total) as a DataTable
DataTable dataTable = worksheet.ExportDataTable(
    startRow: 0,
    startColumn: 0,
    totalRows: 10,
    totalColumns: 5,
    options: exportOptions);
```

*Почему это важно:*  
`ExportDataTable` — самый удобный способ перенести данные Excel в реляционную структуру, которую уже понимают многие .NET‑API (например, Entity Framework, Dapper). Передавая **Custom ExportTableOptions when ExportAsStrin**, вы гарантируете, что каждый `DataColumn.DataType` будет `typeof(string)`.

## Шаг 4: Проверьте результат — все значения являются строками

Хорошей практикой является проверка того, что экспорт прошёл как ожидалось. Следующий цикл выводит каждую ячейку и её тип во время выполнения.

```csharp
Console.WriteLine("Exported DataTable (all values as strings):");
foreach (DataRow row in dataTable.Rows)
{
    for (int i = 0; i < dataTable.Columns.Count; i++)
    {
        object value = row[i];
        Console.Write($"{value} ({value.GetType().Name})\t");
    }
    Console.WriteLine();
}
```

**Ожидаемый вывод**

```
123 (String)    2023‑01‑15 (String)    $45.67 (String)    TRUE (String)    Sample text (String)
...
```

Каждая ячейка показывает тип `String`, подтверждая, что **Custom ExportTableOptions when ExportAsStrin** сработал корректно.

## Шаг 5: Необязательно — записать DataTable в CSV

Если ваша конечная цель — файл простого текста, вы можете легко сериализовать `DataTable` в CSV:



## Что вам стоит изучить дальше?

Следующие руководства охватывают тесно связанные темы, построенные на техниках, продемонстрированных в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [Экспорт HTML‑строк из Excel в DataTable с помощью Aspose.Cells для .NET: пошаговое руководство](/cells/english/net/import-export/export-html-strings-excel-datatable-aspose-cells-net/)
- [Экспорт пользовательских свойств Excel в PDF с Aspose Cells Net](/cells/hongkong/net/workbook-operations/export-custom-properties-excel-pdf-aspose-cells-net/)
- [Aspose Cells Java: пользовательские фильтры загрузки при экспорте Excel](/cells/hongkong/java/import-export/aspose-cells-java-custom-load-filters-excel-export/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}