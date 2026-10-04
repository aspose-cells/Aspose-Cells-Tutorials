---
category: general
date: 2026-10-04
description: Узнайте, как копировать сводную таблицу из одной книги в другую с помощью
  C#. Это руководство также охватывает копирование строк, дублирование сводной таблицы
  и эффективное копирование диапазона Excel.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- how to copy pivot
- copy excel range
- how to copy rows
- duplicate pivot table
language: ru
lastmod: 2026-10-04
og_description: Копировать сводную таблицу в Excel с помощью C#. Следуйте этому полному
  руководству, чтобы дублировать сводные таблицы, копировать строки и копировать диапазон
  Excel с помощью Aspose.Cells.
og_image_alt: Screenshot showing a duplicated pivot table in an Excel worksheet after
  using C# code
og_title: Копирование сводной таблицы в Excel с помощью C# – пошаговое руководство
schemas:
- author: Aspose
  dateModified: '2026-10-04'
  description: Learn how to copy pivot table from one workbook to another using C#.
    This guide also covers how to copy rows, duplicate pivot table, and copy Excel
    range efficiently.
  headline: How to copy pivot table in Excel with C# and Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: Как скопировать сводную таблицу в Excel с помощью C# и Aspose.Cells
url: /ru/net/pivot-tables/how-to-copy-pivot-table-in-excel-with-c-and-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как скопировать сводную таблицу в Excel с помощью C# и Aspose.Cells

Если вам нужно **copy pivot table** из одной книги в другую, этот учебник покажет вам полное, готовое к выполнению решение. Вы увидите, как загрузить исходный файл, определить диапазон, содержащий сводную таблицу, скопировать строки (включая определение сводной) и сохранить результат. Независимо от того, автоматизируете ли вы конвейер отчетности или создаёте инструмент миграции, нижеуказанные шаги позволяют дублировать сводную таблицу всего несколькими строками C#.

Копирование сводной таблицы — это больше, чем копирование значений ячеек; подлежащий кэш и настройки полей должны перемещаться вместе. В примере используется библиотека **Aspose.Cells**, потому что она автоматически обрабатывает метаданные сводных таблиц, и вам не нужно вручную восстанавливать кэш. К концу этого руководства вы сможете **how to copy pivot**, **copy excel range**, и **how to copy rows** безопасно.

## Требования

- .NET 6.0 или новее установлен (код также работает с .NET Framework 4.7+).
- Действительная лицензия Aspose.Cells for .NET или временная оценочная лицензия.
- Два файла Excel: `Source.xlsx`, содержащий сводную таблицу, которую вы хотите дублировать, и пустая папка, куда будет записан `CopyWithPivot.xlsx`.
- Visual Studio 2022 (или любая IDE, поддерживающая C#).

## Шаг 1: Настройте проект и добавьте Aspose.Cells

Создайте новый консольный проект и добавьте пакет Aspose.Cells из NuGet:

```bash
dotnet new console -n PivotCopyDemo
cd PivotCopyDemo
dotnet add package Aspose.Cells
```

Пакет предоставляет классы `Workbook`, `Worksheet` и `CellArea`, используемые в коде ниже.

## Шаг 2: Загрузите исходную книгу, содержащую сводную таблицу

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // Load the source workbook that holds the pivot you want to duplicate
        Workbook srcWorkbook = new Workbook(@"YOUR_DIRECTORY/Source.xlsx");
```

> **Почему это важно:** Загрузка книги создаёт представление всех листов в памяти, включая любые скрытые кэши сводных таблиц. Без загрузки файла вы не сможете ссылаться на диапазон сводной таблицы.

## Шаг 3: Определите область ячеек, охватывающую сводную таблицу

Необходимо указать Aspose.Cells, какие строки и столбцы принадлежат сводной таблице. Структура `CellArea` позволяет задать прямоугольный блок.

```csharp
        // Define the rectangle that encloses the pivot table (adjust as needed)
        CellArea sourceRange = new CellArea
        {
            StartRow = 0,      // first row (zero‑based)
            StartColumn = 0,   // first column
            EndRow = 30,       // last row of the pivot
            EndColumn = 10     // last column of the pivot
        };
```

> **Подсказка:** Если вы не уверены в точных размерах, откройте исходный файл в Excel, выделите сводную таблицу и обратите внимание на диапазон, отображаемый в поле имени (например, `A1:K31`). Преобразуйте координаты Excel в индексы, начинающиеся с нуля, для кода.

## Шаг 4: Создайте новую целевую книгу и получите её первый лист

```csharp
        // Create an empty workbook that will receive the copied pivot
        Workbook destWorkbook = new Workbook();
        Worksheet destWorksheet = destWorkbook.Worksheets[0];
```

> **Почему этот шаг необходим:** Целевая книга должна существовать, прежде чем вы сможете копировать строки. Aspose.Cells автоматически создаёт лист по умолчанию, который мы будем использовать в качестве цели.

## Шаг 5: Скопируйте строки (включая сводную таблицу) из источника в назначение

Метод `CopyRows` копирует как значения ячеек, так и подлежащий кэш сводной таблицы.

```csharp
        // Copy rows from source to destination, preserving the pivot definition
        destWorksheet.Cells.CopyRows(
            srcWorkbook.Worksheets[0].Cells,      // source cells
            sourceRange.StartRow,                 // first row to copy
            sourceRange.EndRow - sourceRange.StartRow + 1, // number of rows
            destWorksheet.Cells,                  // target cells
            sourceRange.StartRow);                // target start row
```

> **Как это работает:**  
> - `CopyRows` принимает исходный лист, начальную строку и количество строк для копирования.  
> - Он также получает целевой лист и строку, с которой должна начаться копия.  
> - Поскольку исходный диапазон включает сводную таблицу, метод переносит кэш, список полей и макет сводной таблицы без изменений. Это суть **how to copy pivot** без потери функциональности.

### Пограничный случай: копирование сводной, охватывающей несколько листов

Если исходные данные сводной находятся на другом листе, чем сама сводная, кэш всё равно копируется, потому что Aspose.Cells хранит кэш в книге, а не на листе. Однако необходимо убедиться, что целевая книга содержит тот же диапазон исходных данных; иначе сводная покажет ошибки `#REF!`. В таких случаях сначала скопируйте диапазон исходных данных, затем строки сводной.

## Шаг 6: Сохраните книгу, теперь содержащую скопированную сводную таблицу

```csharp
        // Persist the destination workbook to disk
        destWorkbook.Save(@"YOUR_DIRECTORY/CopyWithPivot.xlsx");
        Console.WriteLine("Pivot table copied successfully.");
    }
}
```

Запуск программы создаёт `CopyWithPivot.xlsx` с точной копией оригинальной сводной таблицы, включая все слайсеры, фильтры и вычисляемые поля.

### Ожидаемый результат

При открытии `CopyWithPivot.xlsx`:

- Сводная таблица появляется в том же положении (например, A1:K31), что и в `Source.xlsx`.
- Все подписи строк и столбцов, итоги и форматирование сохранены.
- Обновление сводной показывает те же данные, что и в источнике, подтверждая правильное копирование кэша.

## Как копировать строки без сводной (copy excel range)

Если вам нужно только **copy excel range** без данных сводной, вы можете использовать тот же метод `CopyRows`, но указать диапазон, не содержащий сводную. Например:

```csharp
// Copy a simple data table from rows 5‑15, columns A‑D
destWorksheet.Cells.CopyRows(
    srcWorkbook.Worksheets[0].Cells,
    4,            // start at row 5 (zero‑based)
    11,           // copy 11 rows (5‑15 inclusive)
    destWorksheet.Cells,
    0);           // paste at the top of the destination sheet
```

## Дублирование сводной таблицы в той же книге (альтернативный подход)

Иногда требуется **duplicate pivot table** внутри той же книги, а не создавать новый файл. Это можно сделать, скопировав строки в другое место:

```csharp
// Duplicate pivot table to start at row 40 in the same worksheet
destWorksheet.Cells.CopyRows(
    srcWorkbook.Worksheets[0].Cells,
    sourceRange.StartRow,
    sourceRange.EndRow - sourceRange.StartRow + 1,
    destWorksheet.Cells,
    40); // destination start row (zero‑based)
```

## Распространённые подводные камни и как их избежать

| Подводный камень | Почему происходит | Как исправить |
|------------------|-------------------|---------------|
| Сводная показывает `#REF!` после копирования | Диапазон исходных данных отсутствует в целевой книге | Сначала скопируйте диапазон исходных данных или используйте `CopyRows` на листе исходных данных перед копированием сводной |
| Форматирование потеряно | Были скопированы только значения (например, использовался `Copy` вместо `CopyRows`) | Всегда используйте `CopyRows`, который сохраняет стиль, форматирование и метаданные сводной |
| Непредвиденный сдвиг строк | Начальная строка в целевой книге не совпадает с начальной строкой в исходной | Убедитесь, что начальная строка `destWorksheet.Cells` соответствует требуемому месту |
| Большие книги вызывают нагрузку на память | `CopyRows` загружает целые листы в память | Выполняйте копирование частями или используйте потоковые API при работе с более чем 100 000 строк |

## Полный, исполняемый пример

Ниже приведена полная программа, которую можно вставить в `Program.cs` и сразу запустить (замените `YOUR_DIRECTORY` на реальный путь на вашем компьютере).

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the source workbook containing the pivot table
        Workbook srcWorkbook = new Workbook(@"YOUR_DIRECTORY/Source.xlsx");

        // 2️⃣ Define the area that encloses the pivot (adjust to your sheet)
        CellArea sourceRange = new CellArea
        {
            StartRow = 0,
            StartColumn = 0,
            EndRow = 30,
            EndColumn = 10
        };

        // 3️⃣ Create the destination workbook (empty) and get its first sheet
        Workbook destWorkbook = new Workbook();
        Worksheet destWorksheet = destWorkbook.Worksheets[0];

        // 4️⃣ Copy rows—including the pivot cache—into the destination
        destWorksheet.Cells.CopyRows(
            srcWorkbook.Worksheets[0].Cells,
            sourceRange.StartRow,
            sourceRange.EndRow - sourceRange.StartRow + 1,
            destWorksheet.Cells,
            sourceRange.StartRow);

        // 5️⃣ Save the result
        destWorkbook.Save(@"YOUR_DIRECTORY/CopyWithPivot.xlsx");
        Console.WriteLine("Pivot table copied successfully.");
    }
}
```

Запустите программу командой `dotnet run`. После выполнения откройте `CopyWithPivot.xlsx`, чтобы убедиться, что сводная таблица выглядит точно так же, как в исходном файле.

## Заключение

Теперь вы знаете, как **copy pivot table** из одной книги Excel в другую с помощью C# и Aspose.Cells. Руководство охватило полный процесс — от загрузки исходного файла, определения области ячеек сводной, копирования строк и сохранения целевой книги. Вы также узнали **how to copy rows**, **copy excel range** и **duplicate pivot table** в одной файле, а также ознакомились с распространёнными подводными камнями и рекомендациями по лучшим практикам.

Готовы к следующему шагу? Попробуйте добавить код для программного обновления скопированной сводной, или изучите экспорт сводной в PDF с помощью Aspose.Cells. Экспериментируйте с различными исходными диапазонами, и вы быстро освоите автоматизацию Excel в .NET.

---

## Что стоит изучить дальше?

Следующие учебники охватывают тесно связанные темы, построенные на техниках, продемонстрированных в этом руководстве. Каждый ресурс включает полные работающие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в своих проектах.

- [Копировать сводную таблицу в C# — Полное пошаговое руководство](/cells/english/net/pivot-tables/copy-pivot-table-in-c-complete-step-by-step-guide/)
- [Создать новую книгу Excel — Копировать и дублировать сводную таблицу](/cells/english/net/pivot-tables/create-new-excel-workbook-copy-duplicate-pivot-table/)
- [copy rows excel — Сохранить сводную таблицу при дублировании строк](/cells/english/net/pivot-tables/copy-rows-excel-preserve-pivot-table-while-duplicating-rows/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}