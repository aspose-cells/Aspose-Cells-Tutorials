---
category: general
date: 2026-11-16
description: Как скопировать сводную таблицу из одного файла Excel в новую книгу с
  помощью C#. Узнайте, как загрузить книгу, скопировать диапазон и сохранить сводные
  таблицы.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot table
- copy range to new workbook
- load excel workbook c#
- Aspose.Cells copy pivot
- preserve pivot table C#
- Excel automation C#
language: ru
lastmod: 2026-11-16
og_description: Как скопировать сводную таблицу из существующей книги в новую книгу
  с помощью C#. Следуйте этому полному руководству, чтобы загрузить книгу Excel, скопировать
  диапазон и сохранить сводную таблицу неизменной.
og_image_alt: how to copy pivot table example in C#
og_title: Как скопировать сводную таблицу в новую книгу Excel на C# – пошаговое руководство
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: How to copy pivot table from one Excel file to a new workbook using
    C#. Learn to load workbook, copy range, and preserve pivot tables.
  headline: How to copy a pivot table to a new workbook in C#
  type: TechArticle
- description: How to copy pivot table from one Excel file to a new workbook using
    C#. Learn to load workbook, copy range, and preserve pivot tables.
  name: How to copy a pivot table to a new workbook in C#
  steps:
  - name: Expected output
    text: 'Running the program produces `CopyWithPivot.xlsx`. Opening the file in
      Excel shows:'
  - name: Copying multiple pivot tables
    text: If your source sheet contains several pivots, expand the `CellArea` to cover
      the union of all ranges, or repeat the copy step for each distinct area.
  - name: Preserving styles and conditional formatting
    text: '`CopyRows` copies cell styles automatically. If you need to preserve workbook‑wide
      named styles or custom number formats, call `destWorkbook.Worksheets[0].CopyStyle`
      before saving.'
  - name: Working with large workbooks
    text: For files larger than 100 MB, consider using `Workbook.LoadOptions` with
      the `MemorySetting` set to `MemorySetting.MemoryPreference` to reduce memory
      pressure.
  - name: Next steps
    text: '* Explore **Aspose.Cells** features such as refreshing pivots programmatically.
      * Combine this approach with **ExcelPackage** (EPPlus) if you need an open‑source
      alternative. * Automate copying across multiple sheets by looping through `srcWorkbook.Worksheets`.'
  type: HowTo
- questions:
  - answer: Aspose.Cells can read macro‑enabled files (`.xlsm`), but the macro code
      isn’t copied. The pivot table itself is preserved because it’s part of the worksheet
      XML.
    question: Does this work with macros or VBA‑enabled workbooks?
  - answer: The copy operation includes the cached data only. If the destination workbook
      needs to refresh from the original source, you’ll have to re‑configure the data
      connection manually.
    question: What if the pivot uses an external data source?
  - answer: 'No. A pivot table needs its cache. The most reliable way is to copy the
      rows that contain the cache, as demonstrated. You can later hide those rows
      if you don’t want them visible. ## Conclusion You now know **how to copy pivot
      table** from one Excel file to another using C#. The tutorial covered **l'
    question: Can I copy the pivot without the underlying data rows?
  type: FAQPage
tags:
- C#
- Excel
- Aspose.Cells
- Automation
title: Как скопировать сводную таблицу в новую рабочую книгу в C#
url: /ru/net/pivot-tables/how-to-copy-a-pivot-table-to-a-new-workbook-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как скопировать сводную таблицу в новую книгу Excel на C#

Если вам нужно **how to copy pivot table** из одного файла Excel в новую книгу, это руководство покажет точные шаги. Вы узнаете, как **load excel workbook c#**, определить исходный диапазон и **copy range to new workbook**, сохраняя сводную таблицу нетронутой.

Копирование сводной таблицы — распространённая задача, когда требуется переиспользовать шаблон отчёта, перенести данные между проектами или создать лёгкий файл для распространения. Пример кода ниже использует Aspose.Cells — полностью управляемую .NET‑библиотеку, работающую без установленного Microsoft Office. К концу этого урока у вас будет готовая к запуску программа, создающая новую книгу, содержащую оригинальную сводную таблицу, готовую к дальнейшей обработке или распространению.

## Предварительные требования

Перед началом убедитесь, что у вас есть:

* .NET 6.0 SDK или новее (пример работает с .NET Core и .NET Framework)
* Visual Studio 2022 или любой другой редактор C#
* Лицензия Aspose.Cells for .NET (бесплатная trial‑версия подходит для оценки)
* Исходный файл Excel (`Source.xlsx`), содержащий хотя бы одну сводную таблицу

> **Pro tip:** Если вы используете бесплатную trial‑версию, установите лицензию в коде, чтобы избавиться от водяных знаков оценки.

## Шаг 1: Загрузить исходную книгу (load excel workbook c#)

Первое действие — открыть книгу, в которой находится сводная таблица. Aspose.Cells считывает файл в память, предоставляя полный доступ к листам, ячейкам и объектам сводных таблиц.

```csharp
using Aspose.Cells;

class PivotCopyDemo
{
    static void Main()
    {
        // Load the source workbook that contains the pivot table
        Workbook srcWorkbook = new Workbook(@"YOUR_DIRECTORY\Source.xlsx");
```

*Почему это важно*: Загрузка книги является фундаментом любой автоматизации Excel. Без корректного объекта `Workbook` вы не сможете исследовать сводную таблицу или копировать её данные.

## Шаг 2: Определить область ячеек, охватывающую сводную таблицу (copy range to new workbook)

Сводная таблица располагается внутри прямоугольного блока ячеек. Необходимо указать этот блок, чтобы операция копирования знала, что перемещать. Конструктор `CellArea` использует индексы, начинающиеся с нуля: `StartRow, StartColumn, EndRow, EndColumn`.

```csharp
        // Define the cell range that encloses the pivot table, e.g., A1:K21
        // Row and column indexes start at 0, so A1 = (0,0)
        CellArea sourceRange = new CellArea(0, 0, 20, 10); // A1:K21
```

*Почему это важно*: Явно задавая диапазон, вы избегаете копирования лишних данных и гарантируете включение кэша сводной таблицы. Диапазон можно вычислять динамически, если размеры сводных таблиц различаются.

## Шаг 3: Создать новую книгу и получить её первый лист

Теперь создаём целевую книгу, в которую будут скопированы строки. Aspose.Cells автоматически добавляет лист по умолчанию, которым мы будем пользоваться в качестве целевого.

```csharp
        // Create a new workbook that will receive the copied range
        Workbook destWorkbook = new Workbook();
        Worksheet destWorksheet = destWorkbook.Worksheets[0];
```

*Почему это важно*: Начало с чистой книги гарантирует, что в файл попадёт только сводная таблица (и поддерживающие её строки), что делает результат лёгким.

## Шаг 4: Скопировать строки из исходного диапазона на целевой лист (how to copy pivot table)

Метод `CopyRows` копирует целые строки, сохраняя формулы, форматирование и, что особенно важно, сводные таблицы. Параметры метода: начальная строка, конечная строка, коллекция целевых ячеек и индекс строки в целевом листе, с которой начинается копирование (здесь `0`, то есть первая строка).

```csharp
        // Copy the rows that contain the pivot table.
        // Pivot tables inside the range are preserved automatically.
        destWorksheet.Cells.CopyRows(
            sourceRange.StartRow,
            sourceRange.EndRow,
            destWorksheet.Cells,
            0);
```

*Почему это важно*: Использование `CopyRows` вместо копирования отдельных ячеек обеспечивает сохранение связи кэша сводной таблицы с скопированными данными. Aspose.Cells обрабатывает внутренние XML‑структуры, поэтому вам не нужно вручную восстанавливать сводную таблицу.

## Шаг 5: Сохранить полученную книгу (copy range to new workbook)

Наконец, записываем новый файл на диск. Целевая книга теперь содержит идентичную сводную таблицу, работающую независимо от исходного файла.

```csharp
        // Save the new workbook with the copied pivot table
        destWorkbook.Save(@"YOUR_DIRECTORY\CopyWithPivot.xlsx");

        // Optional: inform the user
        System.Console.WriteLine("Pivot table copied successfully!");
    }
}
```

### Ожидаемый результат

Запуск программы создаёт `CopyWithPivot.xlsx`. При открытии файла в Excel вы увидите:

* Тот же макет сводной таблицы, что и в `Source.xlsx`
* Все строки исходных данных, входящие в кэш сводной таблицы
* Отсутствие ссылок на оригинальную книгу (сводная таблица работает автономно)

## Обработка типовых вариантов

### Копирование нескольких сводных таблиц

Если на листе‑источнике несколько сводных таблиц, расширьте `CellArea`, чтобы охватить объединённый диапазон всех таблиц, либо повторите шаг копирования для каждой отдельной области.

```csharp
// Example: copy two separate ranges
CellArea firstPivot = new CellArea(0, 0, 20, 10);
CellArea secondPivot = new CellArea(25, 0, 45, 10);

destWorksheet.Cells.CopyRows(firstPivot.StartRow, firstPivot.EndRow, destWorksheet.Cells, 0);
destWorksheet.Cells.CopyRows(secondPivot.StartRow, secondPivot.EndRow, destWorksheet.Cells, 21); // start after first block
```

### Сохранение стилей и условного форматирования

`CopyRows` автоматически копирует стили ячеек. Если необходимо сохранить стили, объявленные на уровне книги, или пользовательские форматы чисел, вызовите `destWorkbook.Worksheets[0].CopyStyle` перед сохранением.

### Работа с большими книгами

Для файлов размером более 100 МБ рекомендуется использовать `Workbook.LoadOptions` с параметром `MemorySetting`, установленным в `MemorySetting.MemoryPreference`, чтобы снизить нагрузку на память.

```csharp
LoadOptions loadOptions = new LoadOptions(LoadFormat.Xlsx)
{
    MemorySetting = MemorySetting.MemoryPreference
};
Workbook largeSrc = new Workbook(@"bigfile.xlsx", loadOptions);
```

## Полный исходный код (готов к запуску)

Ниже представлен полностью готовая программа, включая директивы `using` и комментарии. Скопируйте её в новый консольный проект и замените `YOUR_DIRECTORY` на реальный путь к папке.

```csharp
using System;
using Aspose.Cells;

class PivotCopyDemo
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Load the source workbook (load excel workbook c#)
        // -------------------------------------------------
        Workbook srcWorkbook = new Workbook(@"YOUR_DIRECTORY\Source.xlsx");

        // -------------------------------------------------
        // Step 2: Define the area that contains the pivot table
        // -------------------------------------------------
        // Adjust the indices if your pivot occupies a different range.
        CellArea sourceRange = new CellArea(0, 0, 20, 10); // A1:K21

        // -------------------------------------------------
        // Step 3: Create the destination workbook
        // -------------------------------------------------
        Workbook destWorkbook = new Workbook();
        Worksheet destWorksheet = destWorkbook.Worksheets[0];

        // -------------------------------------------------
        // Step 4: Copy rows (how to copy pivot table)
        // -------------------------------------------------
        destWorksheet.Cells.CopyRows(
            sourceRange.StartRow,
            sourceRange.EndRow,
            destWorksheet.Cells,
            0);

        // -------------------------------------------------
        // Step 5: Save the new file (copy range to new workbook)
        // -------------------------------------------------
        destWorkbook.Save(@"YOUR_DIRECTORY\CopyWithPivot.xlsx");

        Console.WriteLine("Pivot table copied successfully!");
    }
}
```

Запустите программу (`dotnet run` или `Ctrl+F5` в Visual Studio). После выполнения откройте `CopyWithPivot.xlsx`, чтобы убедиться, что сводная таблица ведёт себя точно так же, как оригинальная.

## Часто задаваемые вопросы

**Q: Работает ли это с макросами или книгами, содержащими VBA?**  
A: Aspose.Cells может читать файлы с макросами (`.xlsm`), но код макросов не копируется. Сама сводная таблица сохраняется, так как является частью XML‑листов.

**Q: Что если сводная таблица использует внешний источник данных?**  
A: Операция копирования включает только кэшированные данные. Если целевой файл должен обновляться из оригинального источника, соединение данных придётся настроить вручную.

**Q: Можно ли скопировать сводную таблицу без строк данных, лежащих в её кэше?**  
A: Нет. Сводная таблица требует кэш данных. Самый надёжный способ — скопировать строки, содержащие кэш, как показано выше. При желании эти строки можно скрыть после копирования.

## Заключение

Теперь вы знаете, **how to copy pivot table** из одного файла Excel в другой с помощью C#. В руководстве рассмотрены **load excel workbook c#**, определён **copy range to new workbook**, и использован метод `CopyRows` библиотеки Aspose.Cells для сохранения сводной таблицы. С готовым, исполняемым примером вы можете внедрять эту схему в конвейеры отчётности, автоматические инструменты экспорта или любые сценарии, где требуется перенос сводных таблиц между книгами.

### Следующие шаги

* Изучите возможности **Aspose.Cells**, такие как программное обновление сводных таблиц.  
* Сочетайте этот подход с **ExcelPackage** (EPPlus), если нужен открытый альтернативный вариант.  
* Автоматизируйте копирование между несколькими листами, перебирая `srcWorkbook.Worksheets`.  

Экспериментируйте с различными диапазонами, добавляйте собственные стили или внедряйте логику в более крупный сервис обработки данных. Приятного кодинга!

## Что изучать дальше?

Следующие руководства охватывают смежные темы, построенные на техниках, продемонстрированных в этом материале. Каждый ресурс содержит полностью рабочие примеры кода с пошаговыми объяснениями, помогающими освоить дополнительные возможности API и исследовать альтернативные подходы в ваших проектах.

- [Create New Workbook in C# – Copy Pivot Table](/cells/english/net/pivot-tables/create-new-workbook-in-c-copy-pivot-table/)
- [How to copy pivot table in Excel with C# and Aspose.Cells](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-excel-with-c-and-aspose-cells/)
- [Copy pivot table to new workbook, export shape to PowerPoint](/cells/english/net/pivot-tables/copy-pivot-table-to-new-workbook-export-shape-to-powerpoint/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}