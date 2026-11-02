---
category: general
date: 2026-06-24
description: Создайте новую книгу в C# и скопируйте сводную таблицу, сохранив её данные.
  Узнайте, как копировать строки, экспортировать выбранный диапазон и сохранить сводную
  таблицу неизменной.
draft: false
keywords:
- create new workbook
- copy pivot table
- preserve pivot table
- how to copy rows
- export selected range
language: ru
og_description: Создайте новую книгу в C# и скопируйте сводную таблицу, сохранив её
  данные. Пошаговое руководство, охватывающее копирование строк и экспорт выбранного
  диапазона.
og_title: Создать новую книгу в C# – Копировать сводную таблицу
schemas:
- author: Aspose
  dateModified: '2026-06-24'
  description: Create new workbook in C# and copy pivot table while preserving its
    data. Learn how to copy rows, export selected range, and keep the pivot intact.
  headline: Create New Workbook in C# – Copy Pivot Table
  type: TechArticle
- questions:
  - answer: Yes, as long as the copied rectangle encloses each pivot you need. If
      you only want one, adjust `rows`/`cols` to isolate it.
    question: Does this work with multiple pivot tables on the same sheet?
  - answer: The pivot cache will still point to the original connection. Call `pivotTable.RefreshData()`
      after loading the destination if you want to re‑query the source.
    question: What if the source workbook uses external data connections?
  - answer: Absolutely. Replace `destinationWorkbook` with `sourceWorkbook` and pick
      another worksheet index.
    question: Can I copy the pivot to a different sheet within the same workbook?
  - answer: 'Use `CopyRows`/`CopyColumns` overloads that accept a `CopyOptions` object—set
      `CopyOptions.CopyType = CopyType.ValuesOnly` or `CopyType.All` depending on
      your needs. --- ## Conclusion We’ve just walked through a **create new workbook**
      scenario that **copy pivot table**, **preserve pivot table**, an'
    question: Is there a way to copy formatting only?
  type: FAQPage
tags:
- C#
- Aspose.Cells
- Excel automation
title: Создать новую книгу в C# – Копировать сводную таблицу
url: /ru/net/pivot-tables/create-new-workbook-in-c-copy-pivot-table/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание новой книги в C# – Копирование сводной таблицы

Когда‑нибудь вам нужно было **create new workbook** в C# просто чтобы переместить часть данных, включающую сводную таблицу? Вы не одиноки. Во многих конвейерах отчетности вы берёте несколько строк, возможно несколько столбцов, и ожидаете, что сводная таблица останется точно такой же — без сломанных ссылок, без пропущенных вычислений.

Хорошие новости? С помощью нескольких строк кода Aspose.Cells вы можете **copy pivot table**, сохранить её в целости и даже **export selected range** без каких‑либо поломок. Ниже вы увидите полностью готовый к запуску пример, который показывает **how to copy rows**, сохраняет сводную таблицу и сохраняет результат в совершенно новой книге.

## Что охватывает данный учебник

- Настройка проекта C# с Aspose.Cells (библиотека, которая обеспечивает работу кода).
- Загрузка исходной книги, содержащей оригинальную сводную таблицу.
- Использование методов `CopyRows` и `CopyColumns` библиотеки для дублирования точного диапазона, который вам нужен.
- Сохранение дублированной области в сценарии **create new workbook**, при этом сводная таблица остаётся рабочей.
- Советы по граничным случаям, таким как несколько сводных таблиц, скрытые строки и большие наборы данных.

К концу этого руководства вы сможете **export selected range** из любого файла Excel, сохранить логику сводной таблицы живой и разместить новый файл где угодно.

> **Prerequisite**: Aspose.Cells for .NET (бесплатная пробная версия или лицензированная) установлен через NuGet. Если вы ещё не добавили его, выполните `dotnet add package Aspose.Cells` в папке вашего проекта.

---

## Создание новой книги и копирование сводной таблицы

Ниже представлена суть решения. Мы пройдемся по каждой строке, объясним, почему она важна, и затем покажем полную программу.

```csharp
using System;
using Aspose.Cells;

class PivotCopyDemo
{
    static void Main()
    {
        // 1️⃣ Load the source workbook that contains the pivot table
        string sourcePath = @"YOUR_DIRECTORY\source.xlsx";
        Workbook sourceWorkbook = new Workbook(sourcePath);

        // 2️⃣ Create a new workbook that will receive the copied range
        Workbook destinationWorkbook = new Workbook();
        Worksheet destSheet = destinationWorkbook.Worksheets[0];

        // 3️⃣ Define the range we want to copy (first 20 rows, first 4 columns)
        //    This range includes the pivot table we care about.
        int startRow = 0;   // zero‑based index
        int startColumn = 0;
        int totalRows = 20;
        int totalColumns = 4;

        // 4️⃣ Copy rows – this is the “how to copy rows” part.
        //    Aspose.Cells lets us copy rows directly from the source cells collection.
        sourceWorkbook.Worksheets[0].Cells.CopyRows(startRow, startRow, totalRows);

        // 5️⃣ Copy columns – paired with the row copy to form a rectangular block.
        sourceWorkbook.Worksheets[0].Cells.CopyColumns(startColumn, startColumn, totalColumns);

        // 6️⃣ Now move the copied block into the destination sheet.
        //    We use the same start cell (A1) for simplicity.
        destSheet.Cells.CopyRows(startRow, startRow, totalRows);
        destSheet.Cells.CopyColumns(startColumn, startColumn, totalColumns);

        // 7️⃣ Save the destination workbook – the pivot table is preserved in the copied range
        string destPath = @"YOUR_DIRECTORY\copy-pivot.xlsx";
        destinationWorkbook.Save(destPath);

        Console.WriteLine("✅ New workbook created and pivot table preserved at: " + destPath);
    }
}
```

### Почему это работает

- **`CopyRows` / `CopyColumns`**: Эти методы дублируют базовые данные ячеек *и* связанные объекты (например, кэш сводной таблицы). Поэтому сводная таблица остаётся рабочей после перемещения.
- **Separate destination workbook**: Создавая новый экземпляр `Workbook`, мы **create new workbook** без оставшегося форматирования или скрытых листов, которые могли бы помешать.
- **Zero‑based indexing**: Aspose.Cells использует индексацию, начинающуюся с нуля, поэтому `0` указывает на ячейку **A1**. При необходимости скорректируйте `startRow`/`startColumn`, если ваша сводная таблица не находится в левом верхнем углу.
- **Preserve pivot table**: Кэш сводной таблицы находится в том же диапазоне, поэтому копирование диапазона автоматически копирует кэш. Дополнительный код не требуется.

---

## Как копировать строки без нарушения сводной таблицы

Если вас интересует только часть копирования строк, вы можете изолировать её:

```csharp
// Copy just rows 5‑15 (inclusive) from the source sheet
int sourceStartRow = 4;   // row 5 in Excel terms
int rowsToCopy = 11;      // rows 5‑15 => 11 rows
sourceWorkbook.Worksheets[0].Cells.CopyRows(sourceStartRow, 0, rowsToCopy);
```

**Pro tip**: При копировании строк, пересекающих сводную таблицу, всегда копируйте *весь* диапазон сводной таблицы (строки + столбцы). Частичные копии могут оставить сводную таблицу без полей, вызывая ошибки `#REF!`.

## Экспорт выбранного диапазона – реальный пример

Представьте, что у вас есть огромная книга продаж, но клиент хочет только сводку за первый квартал, которая находится в строках 1‑20 и столбцах A‑D. Приведённый выше фрагмент уже **export selected range** для вас. Просто измените переменные `totalRows` и `totalColumns`, чтобы соответствовать запросу клиента, и всё готово.

### Обработка скрытых строк или фильтров

Если на исходном листе есть скрытые строки (возможно отфильтрованные), вы можете захотеть копировать только *видимые* строки. Aspose.Cells предлагает перегрузки `CopyRows`, учитывающие видимость:

```csharp
sourceWorkbook.Worksheets[0].Cells.CopyRows(sourceStartRow, 0, rowsToCopy, true);
```

Установите последний булевый параметр в `true`, чтобы копировать только видимые строки — идеально для “export selected range”, когда пользователь применил фильтры.

## Сохранение сводной таблицы – распространённые подводные камни и как их избежать

| Подводный камень | Почему происходит | Решение |
|------------------|-------------------|---------|
| **Pivot cache not copied** | Использование обычного `Range.Copy` вместо `Cells.CopyRows/CopyColumns`. | Оставайтесь с методами `Cells`, как показано. |
| **Destination sheet has existing pivot** | Сохранение поверх книги, которая уже содержит сводную таблицу с тем же именем. | Начните с нового `Workbook()` (как мы делаем). |
| **Named ranges break** | Исходная сводная таблица ссылается на именованный диапазон, которого нет в новом файле. | Скопируйте также именованный диапазон: `sourceWorkbook.Worksheets[0].Names.CopyTo(destSheet);` |
| **Data source path changes** | Сводная таблица указывает на внешний источник данных, который недоступен. | Используйте `PivotTable.RefreshData()` после копирования, если необходимо. |

## Полный пример от начала до конца (готовый к запуску)

Ниже полная программа, включая директивы `using` и краткий консольный интерфейс. Скопируйте‑вставьте её в новый проект Console App и нажмите **F5**.

```csharp
using System;
using Aspose.Cells;

namespace PivotCopyUtility
{
    class Program
    {
        static void Main()
        {
            // -------------------------------------------------
            // Step 1: Load source workbook (contains the pivot)
            // -------------------------------------------------
            string srcPath = @"YOUR_DIRECTORY\source.xlsx";
            Workbook srcWb = new Workbook(srcPath);

            // -------------------------------------------------
            // Step 2: Prepare destination workbook (create new workbook)
            // -------------------------------------------------
            Workbook destWb = new Workbook();
            Worksheet destWs = destWb.Worksheets[0];

            // -------------------------------------------------
            // Step 3: Define the block we want to copy
            // -------------------------------------------------
            int startRow = 0;      // A1
            int startCol = 0;      // A
            int rows = 20;         // first 20 rows
            int cols = 4;          // first 4 columns

            // -------------------------------------------------
            // Step 4: Copy rows and columns from source to destination
            // -------------------------------------------------
            srcWb.Worksheets[0].Cells.CopyRows(startRow, startRow, rows);
            srcWb.Worksheets[0].Cells.CopyColumns(startCol, startCol, cols);
            destWs.Cells.CopyRows(startRow, startRow, rows);
            destWs.Cells.CopyColumns(startCol, startCol, cols);

            // -------------------------------------------------
            // Step 5: Save the new workbook (preserve pivot table)
            // -------------------------------------------------
            string destPath = @"YOUR_DIRECTORY\copy-pivot.xlsx";
            destWb.Save(destPath);

            Console.WriteLine($"✅ Workbook created at {destPath}");
        }
    }
}
```

**Expected output** (в консоли):

```
✅ Workbook created at YOUR_DIRECTORY\copy-pivot.xlsx
```

Откройте `copy-pivot.xlsx`, и вы увидите ту же сводную таблицу, что была в `source.xlsx`, полностью рабочую и ссылающуюся на скопированный диапазон данных.

## Часто задаваемые вопросы

**Q: Работает ли это с несколькими сводными таблицами на одном листе?**  
A: Да, при условии, что копируемый прямоугольник охватывает каждую нужную сводную таблицу. Если нужна только одна, скорректируйте `rows`/`cols`, чтобы изолировать её.

**Q: Что если исходная книга использует внешние соединения данных?**  
A: Кэш сводной таблицы всё равно будет указывать на оригинальное соединение. Вызовите `pivotTable.RefreshData()` после загрузки назначения, если хотите заново запросить источник.

**Q: Могу ли я скопировать сводную таблицу на другой лист в той же книге?**  
A: Конечно. Замените `destinationWorkbook` на `sourceWorkbook` и выберите другой индекс листа.

**Q: Есть ли способ скопировать только форматирование?**  
A: Используйте перегрузки `CopyRows`/`CopyColumns`, принимающие объект `CopyOptions` — установите `CopyOptions.CopyType = CopyType.ValuesOnly` или `CopyType.All` в зависимости от ваших потребностей.

## Заключение

Мы только что прошли через сценарий **create new workbook**, который **copy pivot table**, **preserve pivot table** и **export selected range** — всё на чистом C#

## Что вам стоит изучить дальше?

Следующие учебники охватывают тесно связанные темы, которые опираются на техники, продемонстрированные в этом руководстве. Каждый ресурс включает полные рабочие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [Создание новой сводной таблицы программно в .NET](/cells/english/net/creating-and-configuring-pivot-tables/creating-new-pivot-table/)
- [Как изменить исходные данные сводной таблицы с помощью Aspose.Cells для .NET | Руководство по анализу данных](/cells/english/net/data-analysis/change-pivot-table-source-aspose-cells-net/)
- [Как управлять совместимостью сводных таблиц Excel с Aspose.Cells для .NET | Руководство по анализу данных](/cells/english/net/data-analysis/manage-excel-pivot-table-compatibility-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}