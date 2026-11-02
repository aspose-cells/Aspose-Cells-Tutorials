---
category: general
date: 2026-07-29
description: Копировать строки из одного листа в другой и узнать, как программно загрузить
  книгу Excel с помощью Aspose.Cells в пошаговом руководстве.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy rows from one worksheet to another
- load excel workbook programmatically
- Aspose.Cells copy rows
- C# Excel automation
- worksheet data transfer
language: ru
lastmod: 2026-07-29
og_description: Копируйте строки из одного листа в другой с помощью Aspose.Cells.
  Узнайте, как программно загружать Excel‑книгу и сохранять сводные таблицы всего
  за несколько строк кода на C#.
og_image_alt: Screenshot showing C# code that copies rows from one worksheet to another
  while preserving pivot tables
og_title: Копирование строк из одного листа в другой – Руководство по автоматизации
  Excel на C#
schemas:
- author: Aspose
  dateModified: '2026-07-29'
  description: Copy rows from one worksheet to another and learn how to load Excel
    workbook programmatically using Aspose.Cells in a step‑by‑step tutorial.
  headline: Copy rows from one worksheet to another – Complete C# Guide
  type: TechArticle
- questions:
  - answer: Absolutely. Replace `destinationWorkbook.Worksheets[0]` with `destinationWorkbook.Worksheets["TargetSheet"]`
      (create the sheet first if it doesn’t exist).
    question: Can I copy to a specific worksheet instead of the first one?
  - answer: Use `CopyRows` with the overload that accepts a `CopyRowsOptions` object
      and set `PasteType` to `PasteType.Values`.
    question: What if I need to copy only values, not formulas?
  - answer: Aspose.Cells supports **streaming** via `LoadOptions` with `MemorySetting.MemoryPreference`.
      Load the source workbook with a lower memory footprint and the copy operation
      will still be efficient.
    question: How do I handle large files without exhausting memory?
  - answer: When you set the `true` flag, the pivot cache is duplicated, so the new
      workbook’s pivots reference the copied data, not the original file.
    question: Do pivot tables stay linked to the original data source?
  type: FAQPage
tags:
- C#
- Excel
- Aspose.Cells
- Automation
title: Копирование строк из одного листа в другой — Полное руководство по C#
url: /ru/net/row-and-column-management/copy-rows-from-one-worksheet-to-another-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Копирование строк из одного листа в другой — Полное руководство по C#

Когда‑то вам нужно было **скопировать строки из одного листа в другой**, но вы не знали, как сохранить формулы и сводные таблицы? Вы не одиноки. Во многих конвейерах отчётности нам приходится извлекать часть данных из основного листа и помещать её в новую книгу для дальнейшей обработки. Хорошая новость: с Aspose.Cells это можно сделать программно, и вся операция занимает всего несколько строк кода.

В этом руководстве мы пройдёмся по загрузке Excel‑книги программно, выбору диапазона и копированию этих строк в совершенно новую книгу с сохранением всех вложенных сводных таблиц. К концу вы получите переиспользуемый фрагмент кода, который можно вставить в любой C#‑проект — без ручного копирования‑вставки.

## Что вы получите

- **Загрузка Excel‑книги программно** с помощью класса `Workbook` из Aspose.Cells.  
- Определение **области ячеек**, содержащей строки, которые нужно переместить.  
- **Копирование строк из одного листа в другой** одним вызовом метода, сохраняющим сводные таблицы.  
- Сохранение результата в новый файл, готовый к распространению или дальнейшей обработке.

### Предварительные требования

- .NET 6.0 или новее (код работает как на .NET Core, так и на .NET Framework).  
- Действительная лицензия Aspose.Cells (или временный ключ оценки).  
- Две папки на диске: одна для исходной книги (`Source.xlsx`), другая для целевой (`Destination.xlsx`).  

Если всё это у вас есть, давайте начнём.

## Шаг 1: Загрузка Excel‑книги программно

Первое, что нужно сделать, — загрузить исходный файл в память. Aspose.Cells делает это проще простого:

```csharp
using Aspose.Cells;

// Load the source workbook from disk
Workbook sourceWorkbook = new Workbook(@"C:\Data\Source.xlsx");
```

> **Почему это важно:** Программная загрузка книги даёт полный контроль над содержимым файла без необходимости открывать Excel на сервере. Это также избавляет от проблем с COM‑интеропом и работает в безголовых средах, например в CI‑конвейерах.

## Шаг 2: Определение исходного диапазона, содержащего строки

Далее точно укажите, какие строки нужно перенести. Объект `CellArea` позволяет задать прямоугольный блок, используя адреса верхней‑левой и нижней‑правой ячеек:

```csharp
// Define the area A1:H20 – adjust as needed
CellArea sourceRange = CellArea.CreateCellArea("A1", "H20");
```

> **Полезный совет:** Если размер ваших данных меняется динамически, вы можете вычислять `EndRow` через `sourceWorksheet.Cells.MaxDataRow`, чтобы всегда захватывать всю таблицу.

## Шаг 3: Создание новой книги для назначения

Теперь создаём пустую книгу, которая получит скопированные строки. По умолчанию такая книга содержит один лист:

```csharp
// Create a new, empty workbook
Workbook destinationWorkbook = new Workbook();
```

> **Зачем нужна новая книга?** Чистый старт гарантирует, что вы случайно не перезапишете существующие данные, и предоставляет предсказуемую среду для тестирования.

## Шаг 4: Копирование строк из одного листа в другой (с сохранением сводных таблиц)

Это сердце руководства. Метод `CopyRows` копирует выбранные строки и, если передать `true` в качестве последнего аргумента, также копирует любые сводные таблицы, находящиеся внутри диапазона:

```csharp
// Perform the copy operation
destinationWorkbook.Worksheets[0].Cells.CopyRows(
    sourceWorkbook.Worksheets[0],      // source worksheet
    sourceRange.StartRow,              // first row to copy (0‑based)
    sourceRange.EndRow,                // last row to copy (inclusive)
    destinationWorkbook.Worksheets[0].Cells, // target worksheet
    0,                                 // target start row (top of sheet)
    true);                             // preserve pivot tables
```

### Что происходит «под капотом»?

- **Исходный лист**: `sourceWorkbook.Worksheets[0]` указывает на первый лист в исходном файле.  
- **Индексы строк**: Aspose.Cells использует нулевую базу индексации, поэтому `StartRow` и `EndRow` соответствуют строкам, заданным в `sourceRange`.  
- **Стартовая строка назначения**: Мы начинаем с строки 0 в новом листе, фактически помещая скопированный блок в самое начало.  
- **Флаг `true`**: Это волшебный переключатель, который заставляет Aspose.Cells клонировать любые сводные таблицы, найденные внутри скопированных строк, сохраняя их кэш и соединения.

> **Предупреждение о граничных случаях:** Если в исходном диапазоне есть объединённые ячейки, выходящие за пределы заданной области, эти объединения будут усечены. Чтобы сохранить их целыми, расширьте диапазон так, чтобы он полностью покрывал объединённый регион.

## Шаг 5: Сохранение целевой книги

Наконец, запишите новый файл на диск. Вы можете выбрать любую папку; просто убедитесь, что процесс имеет права на запись:

```csharp
// Save the result
destinationWorkbook.Save(@"C:\Data\Destination.xlsx");
```

Открыв `Destination.xlsx`, вы увидите строки A1‑H20 продублированными, вместе со всеми сводными таблицами, которые изначально были встроены. Остальная часть книги остаётся пустой, готовой к добавлению новых листов или данных позже.

## Полный рабочий пример

Объединив всё вместе, получаем полностью готовую к запуску программу:

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the source workbook programmatically
        Workbook sourceWorkbook = new Workbook(@"C:\Data\Source.xlsx");

        // 2️⃣ Define the source range (adjust as needed)
        CellArea sourceRange = CellArea.CreateCellArea("A1", "H20");

        // 3️⃣ Create a new destination workbook
        Workbook destinationWorkbook = new Workbook();

        // 4️⃣ Copy rows from one worksheet to another, preserving pivot tables
        destinationWorkbook.Worksheets[0].Cells.CopyRows(
            sourceWorkbook.Worksheets[0],
            sourceRange.StartRow,
            sourceRange.EndRow,
            destinationWorkbook.Worksheets[0].Cells,
            0,
            true);

        // 5️⃣ Save the result
        destinationWorkbook.Save(@"C:\Data\Destination.xlsx");

        Console.WriteLine("Rows successfully copied! Check C:\\Data\\Destination.xlsx");
    }
}
```

**Ожидаемый вывод** (консоль):

```
Rows successfully copied! Check C:\Data\Destination.xlsx
```

Откройте целевой файл и проверьте, что данные, форматирование и сводные таблицы выглядят точно так же, как в исходнике. Если обнаружите недостающие данные, дважды проверьте, что `sourceRange` полностью охватывает нужные строки.

## Часто задаваемые вопросы и советы

- **Можно ли копировать в конкретный лист, а не в первый?**  
  Конечно. Замените `destinationWorkbook.Worksheets[0]` на `destinationWorkbook.Worksheets["TargetSheet"]` (создайте лист заранее, если он не существует).

- **А если нужно копировать только значения, без формул?**  
  Используйте `CopyRows` с перегрузкой, принимающей объект `CopyRowsOptions`, и установите `PasteType` в `PasteType.Values`.

- **Как работать с большими файлами, не исчерпывая память?**  
  Aspose.Cells поддерживает **стриминг** через `LoadOptions` с параметром `MemorySetting.MemoryPreference`. Загружайте исходную книгу с меньшим потреблением памяти, а операция копирования останется эффективной.

- **Остаются ли сводные таблицы привязанными к оригинальному источнику данных?**  
  При установке флага `true` кэш сводных таблиц дублируется, поэтому сводные таблицы в новой книге ссылаются на скопированные данные, а не на оригинальный файл.

## Подведение итогов

Теперь вы знаете, как **скопировать строки из одного листа в другой**, сохраняя любые сводные таблицы, и как **загружать Excel‑книгу программно** с помощью Aspose.Cells. Этот подход служит надёжной основой для построения автоматизированных конвейеров отчётности, скриптов миграции данных или любой задачи, где требуется динамически «вырезать» данные из Excel.

Что дальше? Попробуйте расширить фрагмент кода, чтобы:

- Перебрать несколько исходных диапазонов и собрать их в одну целевую книгу.  
- Применить условное форматирование после копирования для выделения ключевых метрик.  
- Экспортировать готовую книгу в PDF или CSV для дальнейшего использования.

Экспериментируйте, а если возникнут сложности — оставляйте комментарий ниже. Приятного кодинга!

## Что изучать дальше?

Следующие руководства охватывают тесно связанные темы, развивая техники, продемонстрированные в этом пособии. Каждый ресурс содержит полностью работающие примеры кода с пошаговыми объяснениями, помогающими освоить дополнительные возможности API и исследовать альтернативные подходы в ваших проектах.

- [Как копировать строки в Excel с помощью Aspose.Cells для .NET: руководство на C#](/cells/english/net/worksheet-management/copy-rows-excel-aspose-cells-net-guide/)
- [Копирование листа из одной книги в другую с использованием Aspose.Cells](/cells/english/net/worksheet-value-operations/copy-worksheet-between-workbooks/)
- [Как экспортировать видимые строки Excel с помощью Aspose.Cells для .NET: пошаговое руководство](/cells/english/net/workbook-operations/export-visible-rows-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}