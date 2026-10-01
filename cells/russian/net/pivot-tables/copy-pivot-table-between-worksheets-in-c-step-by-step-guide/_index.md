---
category: general
date: 2026-10-01
description: Копировать сводную таблицу в C# с использованием Aspose.Cells. Узнайте,
  как загрузить книгу Excel, определить диапазоны и скопировать диапазон на лист,
  сохраняя сводную таблицу.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- how to copy pivot
- load excel workbook c#
- copy range to worksheet
language: ru
lastmod: 2026-10-01
og_description: Копировать сводную таблицу в C# с помощью Aspose.Cells. Этот учебник
  показывает, как загрузить книгу Excel, скопировать диапазон на лист и сохранить
  сводную таблицу.
og_image_alt: Screenshot of C# code copying a pivot table between worksheets
og_title: Копировать сводную таблицу в C# — полное руководство по программированию
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Copy pivot table in C# using Aspose.Cells. Learn how to load Excel
    workbook, define ranges, and copy range to worksheet while preserving the pivot.
  headline: Copy pivot table between worksheets in C# – step‑by‑step guide
  type: TechArticle
tags:
- Excel automation
- C#
- Aspose.Cells
title: Копирование сводной таблицы между листами в C# — пошаговое руководство
url: /ru/net/pivot-tables/copy-pivot-table-between-worksheets-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Копирование сводной таблицы между листами в C# – пошаговое руководство

Если вам нужно **скопировать сводную таблицу** с одного листа на другой в файле .xlsx, это руководство покажет, как сделать это с помощью C#. Вы узнаете, как **загрузить Excel workbook C#**, определить соответствующие диапазоны и **скопировать диапазон на лист**, сохранив при этом сводную таблицу. Решение работает с Aspose.Cells .NET — библиотекой, сохраняющей определения сводных таблиц при операциях копирования.

## Загрузка Excel workbook в C#

Прежде чем работать с данными, необходимо загрузить исходный workbook в память. Aspose.Cells предоставляет класс `Workbook`, который читает файл и строит объектную модель, представляющую листы, ячейки и сводные таблицы.

```csharp
using Aspose.Cells;

class PivotCopyDemo
{
    static void Main()
    {
        // Path to the source workbook that contains the original pivot table
        const string sourcePath = @"YOUR_DIRECTORY\Input.xlsx";

        // Load the workbook – this is the step that answers “load excel workbook c#”
        Workbook workbook = new Workbook(sourcePath);
        // The workbook now holds all worksheets, including any pivot tables.
```

**Почему это важно:** Загрузка workbook один раз дает единственный источник правды. Все последующие операции работают с этим представлением в памяти, что быстрее, чем многократное открытие файла.

## Определение исходных и целевых диапазонов

Сводная таблица находится внутри прямоугольного блока ячеек. Чтобы скопировать её, создайте объект `Range`, охватывающий весь блок. Такие же размеры должны существовать на целевом листе; иначе копирование обрежет данные.

```csharp
        // Step 2: Get the first worksheet (index 0) that contains the pivot table
        Worksheet sourceSheet = workbook.Worksheets[0];

        // Step 3: Define the exact range that includes the pivot table.
        // Adjust "A1:G20" to match the actual size of your pivot.
        Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");
```

> **Подсказка:** Если вы не уверены в диапазоне, используйте `sourceSheet.PivotTables[0].DataRange.FirstCell.Name` и `LastCell.Name` для построения адреса программно.

## Добавление нового листа и подготовка целевого диапазона

Теперь создайте новый лист, который будет содержать скопированную сводную таблицу. Целевой диапазон должен иметь тот же адрес, что и исходный диапазон.

```csharp
        // Step 4: Add a new worksheet for the copy
        Worksheet destinationSheet = workbook.Worksheets.Add();

        // Create a matching range on the new sheet
        Range destinationRange = destinationSheet.Cells.CreateRange("A1:G20");
```

**Почему этот шаг необходим:** Сводные таблицы привязаны к контексту листа. Копирование диапазона без листа‑назначения вызовет исключение, потому что целевые ячейки не существуют.

## Копирование диапазона на лист с сохранением сводной таблицы

Метод `Range.Copy` библиотеки Aspose.Cells копирует не только сырые значения, но и связанные объекты, такие как сводные таблицы, диаграммы и именованные диапазоны. Это основной способ **как скопировать сводную таблицу** без потери её определения.

```csharp
        // Step 5: Perform the copy – the pivot table definition travels with the cells
        sourceRange.Copy(destinationRange);
```

> **Pro tip:** После копирования вы можете проверить наличие сводной таблицы в `destinationSheet.PivotTables`. Метод `Copy` сохраняет источник данных, фильтры и макет исходной сводной таблицы.

## Сохранение workbook с копией сводной таблицы

Наконец, запишите изменённый workbook в новый файл. Полученный файл будет содержать оригинальный лист и дублированный лист с идентичной сводной таблицей.

```csharp
        // Step 6: Save the workbook under a new name
        const string outputPath = @"YOUR_DIRECTORY\CopyWithPivot.xlsx";
        workbook.Save(outputPath);

        // Optional: Inform the user
        System.Console.WriteLine($"Pivot table copied successfully to {outputPath}");
    }
}
```

Когда вы откроете `CopyWithPivot.xlsx` в Excel, вы увидите два листа: оригинальный и новый, каждый из которых отображает одну и ту же сводную таблицу с теми же фильтрами и вычисляемыми полями.

## Распространённые подводные камни и лучшие практики

| Проблема | Почему происходит | Как избежать |
|----------|-------------------|--------------|
| **Диапазон не охватывает всю сводную таблицу** | Источник данных сводной таблицы может выходить за выбранные ячейки, из‑за чего теряются поля. | Используйте свойство `DataRange` сводной таблицы для автоматической генерации адреса. |
| **На листе‑назначении уже существует сводная таблица с тем же именем** | Aspose.Cells генерирует конфликт имён. | Переименуйте целевую сводную таблицу после копирования: `destinationSheet.PivotTables[0].Name = "PivotCopy";` |
| **Большие workbook вызывают нагрузку на память** | Загрузка всего workbook в память может быть тяжёлой. | Используйте `LoadOptions` для загрузки только необходимых листов, если весь файл не нужен. |
| **Копирование между разными версиями Excel** | Некоторые старые версии не поддерживают определённые функции сводных таблиц. | Сохраняйте результат как `.xlsx` (Office Open XML), чтобы гарантировать совместимость. |

## Расширение решения

После того как у вас появится надёжная процедура **копирования сводной таблицы**, вы сможете построить более сложные рабочие процессы:

* **Пакетное копирование:** Пройдитесь по всем листам, содержащим сводные таблицы, и дублируйте их в сводный workbook.
* **Динамическое определение диапазона:** Замените жёстко заданный `"A1:G20"` кодом, автоматически определяющим границы сводной таблицы.
* **Обновление сводной таблицы:** После копирования вызовите `destinationSheet.PivotTables[0].RefreshData();`, чтобы сводная таблица отразила изменения в источнике данных.

## Ожидаемый результат

Запуск программы с корректным `Input.xlsx` создаёт `CopyWithPivot.xlsx`. При открытии файла вы увидите:

```
Sheet1 (original)          Sheet2 (copy)
+----------------------+   +----------------------+
| Pivot Table: Sales   |   | Pivot Table: Sales   |
| – Region, Product    |   | – Region, Product    |
| – Sum of Amount      |   | – Sum of Amount      |
+----------------------+   +----------------------+
```

Оба листа показывают одинаковый макет сводной таблицы, фильтры и вычисляемые поля.

## Заключение

Теперь вы знаете, как **скопировать сводную таблицу** между листами в C# с помощью Aspose.Cells. В этом руководстве рассмотрены загрузка workbook, определение соответствующих диапазонов, выполнение копирования и сохранение результата — всё с сохранением полного определения сводной таблицы. Применяйте этот шаблон для автоматизации отчётности, создания шаблонных листов или построения инструментов миграции данных.

**Следующие шаги:**  
* Исследуйте варианты **how to copy pivot** для нескольких сводных таблиц на одном листе.  
* Скомбинируйте эту технику с автоматическими скриптами **load Excel workbook C#** для пакетной обработки файлов.  
* Поэкспериментируйте с методом **copy range to worksheet** для диаграмм, таблиц и условного форматирования, получив полное решение по клонированию workbook.  

Счастливого кодинга!

## Что вам стоит изучить дальше?

Следующие руководства охватывают тесно связанные темы, которые развивают техники, продемонстрированные в этом пособии. Каждый ресурс содержит полностью работающие примеры кода с пошаговыми объяснениями, помогающими освоить дополнительные возможности API и исследовать альтернативные подходы в ваших проектах.

- [Create New Workbook – How to Copy a Worksheet with a Pivot Table](/cells/english/net/excel-copy-worksheet/create-new-workbook-how-to-copy-a-worksheet-with-a-pivot-tab/)
- [Create New Excel Workbook – Copy & Duplicate Pivot Table](/cells/english/net/pivot-tables/create-new-excel-workbook-copy-duplicate-pivot-table/)
- [How to copy range with pivot tables in C# – Complete Guide](/cells/english/net/pivot-tables/how-to-copy-range-with-pivot-tables-in-c-complete-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}