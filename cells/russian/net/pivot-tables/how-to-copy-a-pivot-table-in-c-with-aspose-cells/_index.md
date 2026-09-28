---
category: general
date: 2026-09-27
description: Узнайте, как скопировать сводную таблицу в C# с помощью Aspose.Cells.
  Включает копирование строк с форматированием, копирование сводной таблицы на другой
  лист и экспорт сводной таблицы в новую книгу.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot table
- copy rows with formatting
- copy pivot table to another sheet
- how to copy excel rows
- export pivot table to new workbook
language: ru
lastmod: 2026-09-27
og_description: Как скопировать сводную таблицу в C# с помощью Aspose.Cells. Следуйте
  пошаговому руководству, чтобы копировать строки с форматированием, переместить сводную
  таблицу на другой лист и экспортировать её в новую книгу.
og_image_alt: Excel sheet showing a copied pivot table after using Aspose.Cells
og_title: Как скопировать сводную таблицу в C# — полное руководство по Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Learn how to copy a pivot table in C# using Aspose.Cells. Includes
    copy rows with formatting, copy pivot table to another sheet, and export pivot
    table to a new workbook.
  headline: How to copy a pivot table in C# with Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
- Pivot table
title: Как скопировать сводную таблицу в C# с помощью Aspose.Cells
url: /ru/net/pivot-tables/how-to-copy-a-pivot-table-in-c-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как скопировать сводную таблицу в C# с помощью Aspose.Cells

Если вам нужно **скопировать сводную таблицу** из одного листа в другой, изучение **как скопировать сводную таблицу** в C# с Aspose.Cells может сэкономить часы ручной работы. Этот подход также позволяет **скопировать строки с форматированием**, сохранить кэш сводной таблицы неизменным и даже **экспортировать сводную таблицу в новую книгу**, когда требуется отдельный файл.

В этом руководстве рассматривается полный рабочий процесс:

* создание книги,  
* копирование диапазона сводной таблицы с сохранением форматирования,  
* размещение скопированных данных на новом листе и  
* сохранение результата в отдельный файл.

Вы увидите, почему встроенный метод `CopyRows` является самым надёжным способом **скопировать сводную таблицу на другой лист**, и получите советы по работе с особенностями, такими как скрытые строки или внешние источники данных.

## Требования

Перед началом убедитесь, что у вас есть:

| Требование | Почему это важно |
|------------|-------------------|
| .NET 6.0 или новее | Aspose.Cells поддерживает .NET 6+ и обеспечивает лучшую производительность. |
| Visual Studio 2022 (или любой IDE для C#) | Необходим редактор, способный восстанавливать пакеты NuGet. |
| Aspose.Cells for .NET (NuGet‑пакет `Aspose.Cells`) | Эта библиотека предоставляет API `CopyRows`, используемое в примере. |
| Исходный файл Excel (`source.xlsx`), содержащий сводную таблицу в диапазоне `A1:G20` | Код копирует именно этот диапазон; при необходимости измените диапазон, если ваша сводная таблица больше. |

Установите библиотеку с помощью NuGet CLI или консоли Package Manager:

```bash
dotnet add package Aspose.Cells
```

## Шаг 1: Загрузить книгу, содержащую сводную таблицу

Первая строка создаёт объект `Workbook`, представляющий весь файл Excel. Однократная загрузка файла даёт доступ на чтение/запись ко всем листам.

```csharp
using Aspose.Cells;

// Load the source workbook
Workbook workbook = new Workbook(@"YOUR_DIRECTORY\source.xlsx");
```

> **Почему этот шаг важен** – Без загрузки книги ни один из последующих вызовов `CopyRows` не сможет обратиться к исходным данным или кэшу сводной таблицы.

## Шаг 2: Подготовить исходные и целевые листы

Нужен лист‑назначение, куда будет помещена скопированная сводная таблица. Ниже код получает первый лист (где находится оригинальная сводная таблица) и добавляет новый лист с именем **Copy**.

```csharp
// Get the source worksheet (index 0 = first sheet)
Worksheet sourceSheet = workbook.Worksheets[0];

// Add a new worksheet that will receive the copied rows
Worksheet destinationSheet = workbook.Worksheets.Add("Copy");
```

> **Pro tip:** Если лист‑назначение уже существует, сначала вызовите `Worksheets.RemoveAt(index)`, чтобы избежать дублирования имён.

## Шаг 3: Определить область ячеек, охватывающую сводную таблицу

Объект `CellArea` описывает левую‑верхнюю и правую‑нижнюю ячейки диапазона, который вы хотите переместить. В этом примере сводная таблица занимает `A1:G20`. При необходимости измените координаты для более крупных таблиц.

```csharp
// Define the range that includes the pivot table (A1:G20)
CellArea sourceArea = CellArea.CreateCellArea("A1", "G20");
```

## Шаг 4: Скопировать строки с форматированием и сохранить кэш сводной таблицы

Метод `CopyRows` копирует **строки** из листа‑источника в лист‑назначение. Передавая `CopyOptions.CopyAll`, вы гарантируете, что значения, форматирование, диаграммы и встроенные объекты — все, что входит в состав сводной таблицы — будут перенесены.

```csharp
// Copy the rows from the source area to the destination sheet
sourceSheet.CopyRows(
    sourceArea.StartRow,          // start row in the source sheet
    destinationSheet,            // target worksheet
    0,                            // start row in the destination sheet
    sourceArea.RowCount,          // number of rows to copy
    CopyOptions.CopyAll);        // copy everything (values, formats, objects, etc.)
```

### Почему `CopyRows` работает лучше, чем `Copy`, для сводных таблиц

* `CopyRows` учитывает внутренний кэш сводной таблицы, поэтому скопированная таблица остаётся рабочей.
* Он сохраняет **копирование строк с форматированием** точно так же, как они выглядят в оригинальном листе.
* В отличие от простого `Copy` диапазона, он также переносит скрытые строки и связанные срезы.

## Шаг 5: Сохранить книгу со скопированной сводной таблицей

Наконец, запишите изменённую книгу на диск. Новый файл содержит оригинальный лист и лист **Copy**, на котором находится полностью функциональная копия исходной сводной таблицы.

```csharp
// Save the workbook to a new file
workbook.Save(@"YOUR_DIRECTORY\pivot_copied.xlsx");
```

### Ожидаемый результат

При открытии `pivot_copied.xlsx`:

* Лист **Sheet1** по‑прежнему содержит исходные данные и сводную таблицу.
* Лист **Copy** отображает идентичную сводную таблицу с тем же макетом, фильтрами и форматированием.
* Все формулы и соединения данных остаются нетронутыми, поскольку кэш сводной таблицы был скопирован вместе со строками.

## Как скопировать сводную таблицу на другой лист в той же книге

Если требуется разместить сводную таблицу на уже существующем листе (например, “Report”), замените шаг создания листа‑назначения ссылкой на целевой лист:

```csharp
Worksheet destinationSheet = workbook.Worksheets["Report"]; // existing sheet
sourceSheet.CopyRows(sourceArea.StartRow, destinationSheet, 0,
                     sourceArea.RowCount, CopyOptions.CopyAll);
```

Этот фрагмент демонстрирует **копирование сводной таблицы на другой лист** без создания нового листа.

## Экспортировать сводную таблицу в новую книгу

Иногда необходимо вынести сводную таблицу в полностью отдельный файл. После операции копирования можно удалить все листы, кроме того, который содержит скопированную таблицу, и затем сохранить:

```csharp
// Keep only the copied sheet
for (int i = workbook.Worksheets.Count - 1; i >= 0; i--)
{
    if (workbook.Worksheets[i].Name != "Copy")
        workbook.Worksheets.RemoveAt(i);
}

// Save as a new workbook containing only the pivot table
workbook.Save(@"YOUR_DIRECTORY\pivot_only.xlsx");
```

Теперь `pivot_only.xlsx` содержит один лист с дублированной сводной таблицей, удовлетворяя требованию **экспортировать сводную таблицу в новую книгу**.

## Как скопировать строки Excel без потери форматирования

Тот же вызов `CopyRows` работает для любого диапазона, а не только для сводных таблиц. Если нужно **скопировать строки Excel**, включающие условное форматирование, проверку данных или объединённые ячейки, используйте тот же метод:

```csharp
// Example: copy rows 30‑40 from Sheet1 to Sheet2
sourceSheet.CopyRows(29, // zero‑based index for row 30
                     workbook.Worksheets["Sheet2"],
                     0,
                     11, // rows 30‑40 = 11 rows
                     CopyOptions.CopyAll);
```

Поскольку `CopyOptions.CopyAll` переносит всё, строки‑назначения выглядят точно так же, как строки‑источники.

## Распространённые подводные камни и как их избежать

| Подводный камень | Симптом | Решение |
|------------------|---------|----------|
| Исходный диапазон не охватывает всю сводную таблицу | Скопированная таблица обрезана. | Убедитесь, что `CellArea` покрывает все строки/столбцы сводной таблицы. |
| На листе‑назначении уже есть данные | Перезаписанные строки приводят к потере данных. | Выберите чистый лист или начинайте копировать с более высокой строки. |
| Сводная таблица использует внешний источник данных | Копия теряет соединение. | После копирования вызовите `pivotTable.RefreshData()`, чтобы восстановить связь. |
| Скрытые строки не копируются | Некоторые строки исчезают в копии. | `CopyRows` автоматически копирует скрытые строки; убедитесь, что вы не используете `CopyOptions.CopyValuesOnly`. |

## Полный, готовый к запуску пример

Ниже представлен автономный пример программы, который можно вставить в новый консольный проект. Он демонстрирует каждый шаг, описанный выше.

```csharp
using System;
using Aspose.Cells;

namespace PivotTableCopyDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the workbook that contains the pivot table
            string sourcePath = @"YOUR_DIRECTORY\source.xlsx";
            Workbook workbook = new Workbook(sourcePath);

            // 2️⃣ Get source and destination worksheets
            Worksheet sourceSheet = workbook.Worksheets[0]; // first sheet
            Worksheet destinationSheet = workbook.Worksheets.Add("Copy");

            // 3️⃣ Define the cell area that holds the pivot table (A1:G20)
            CellArea sourceArea = CellArea.CreateCellArea("A1", "G20");

            // 4️⃣ Copy rows with formatting and keep the pivot cache
            sourceSheet.CopyRows(
                sourceArea.StartRow,      // start row index (0‑based)
                destinationSheet,        // target sheet
                0,                        // start row in destination
                sourceArea.RowCount,      // number of rows to copy
                CopyOptions.CopyAll);    // copy everything

            // 5️⃣ Save the workbook with the copied pivot table
            string destPath = @"YOUR_DIRECTORY\pivot_copied.xlsx";
            workbook.Save(destPath);

            Console.WriteLine("Pivot table copied successfully to " + destPath);
        }
    }
}
```

**Запуск программы** создаёт `pivot_copied.xlsx` с дубликатом оригинальной сводной таблицы на новом листе под названием **Copy**.

## Заключение

Теперь вы знаете **как скопировать сводную таблицу** в C# используя

## Что изучать дальше?

Следующие руководства охватывают тесно связанные темы, построенные на техниках, продемонстрированных в этом пособии. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы в ваших проектах.

- [Create New Workbook – How to Copy a Worksheet with a Pivot Table](/cells/english/net/excel-copy-worksheet/create-new-workbook-how-to-copy-a-worksheet-with-a-pivot-tab/)
- [Copy Pivot Table in C# – Complete Step‑by‑Step Guide](/cells/english/net/pivot-tables/copy-pivot-table-in-c-complete-step-by-step-guide/)
- [How to copy range with pivot tables in C# – Complete Guide](/cells/english/net/pivot-tables/how-to-copy-range-with-pivot-tables-in-c-complete-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}