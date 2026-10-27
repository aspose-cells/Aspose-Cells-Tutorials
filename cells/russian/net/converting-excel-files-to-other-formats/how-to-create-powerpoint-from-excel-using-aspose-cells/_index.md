---
category: general
date: 2026-09-18
description: Создайте PowerPoint из Excel с помощью Aspose.Cells — копируйте сводные
  таблицы, экспортируйте диапазоны и сохраняйте в формате PPTX в несколько строк кода
  C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create powerpoint from excel
- how to copy pivot table
- copy range between workbooks
- how to export excel to pptx
- save workbook as pptx
language: ru
lastmod: 2026-09-18
og_description: Быстро создавайте PowerPoint из Excel. Узнайте, как копировать сводные
  таблицы, экспортировать диапазоны и сохранять книгу в формате PPTX с помощью Aspose.Cells.
og_image_alt: Screenshot of a PowerPoint slide generated from Excel data
og_title: Создание PowerPoint из Excel с помощью Aspose.Cells – пошаговое руководство
schemas:
- author: Aspose
  dateModified: '2026-09-18'
  description: Create PowerPoint from Excel with Aspose.Cells – copy pivot tables,
    export ranges, and save as PPTX in a few lines of C# code.
  headline: How to create PowerPoint from Excel using Aspose.Cells
  type: TechArticle
- description: Create PowerPoint from Excel with Aspose.Cells – copy pivot tables,
    export ranges, and save as PPTX in a few lines of C# code.
  name: How to create PowerPoint from Excel using Aspose.Cells
  steps:
  - name: Load the source workbook and define the range
    text: You must load the workbook that holds the source data and the pivot table.
      Selecting a precise range ensures that only the needed cells are transferred,
      which keeps the resulting slide lightweight.
  - name: Prepare the destination workbook
    text: Aspose.Cells treats a PowerPoint slide as a workbook when you save it in
      PPTX format. Creating a fresh workbook gives you a clean canvas for the copied
      range.
  - name: Copy the range while preserving the pivot table
    text: The `CopyRange` method accepts a `PasteOptions` object. Setting `CopyPivotTables
      = true` tells Aspose.Cells to keep the pivot table structure intact, not just
      the rendered values.
  - name: Save the workbook as a PowerPoint file
    text: Finally, export the workbook to PPTX format. The `SaveFormat.Pptx` flag
      tells Aspose.Cells to write the worksheet as a PowerPoint slide.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel to PowerPoint
title: Как создать PowerPoint из Excel с помощью Aspose.Cells
url: /ru/net/converting-excel-files-to-other-formats/how-to-create-powerpoint-from-excel-using-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как создать PowerPoint из Excel с помощью Aspose.Cells

Если вам нужно создать PowerPoint из Excel, это руководство покажет вам краткое решение от начала до конца. Вы увидите, как скопировать сводную таблицу, экспортировать выбранный диапазон и сохранить результат в файл PPTX всего несколькими строками C#.

Создание набора слайдов напрямую из данных таблицы устраняет ручной процесс копирования‑вставки, который замедляет рабочие процессы отчетности. В руководстве рассматривается всё необходимое: от настройки проекта до финального файла PPTX, и оно работает с последней версией Aspose.Cells для .NET.

## Требования

Прежде чем начать, убедитесь, что у вас есть:

* **Aspose.Cells for .NET** (версия 23.12 или новее). Установите через NuGet: `Install-Package Aspose.Cells`.
* Среда разработки **.NET 6+** (Visual Studio 2022 или VS Code подойдут).
* Excel‑книга (`Source.xlsx`), содержащая данные и сводную таблицу, которые вы хотите переиспользовать.
* Права записи в папку вывода.

Дополнительные сторонние библиотеки не требуются.

## Создание PowerPoint из Excel – пошагово

Процесс состоит из четырёх логических шагов, которые напрямую соответствуют примеру кода, который вы увидите ниже.

### Шаг 1: Загрузите исходную книгу и определите диапазон

Необходимо загрузить книгу, в которой находятся исходные данные и сводная таблица. Точное указание диапазона гарантирует, что будут перенесены только нужные ячейки, что делает полученный слайд лёгким.

```csharp
using Aspose.Cells;
using System;

// Load the source workbook
Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");

// Select the first worksheet (index 0)
Worksheet sourceSheet = sourceWorkbook.Worksheets[0];

// Define the range that contains the pivot table and surrounding data
Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");
```

**Почему это важно:**  
`CreateRange` создаёт объект `Range`, который можно скопировать целиком. Ограничив диапазон `A1:G20`, вы избегаете переноса ненужных ячеек, которые иначе могли бы увеличить размер файла PowerPoint.

### Шаг 2: Подготовьте целевую книгу

Aspose.Cells рассматривает слайд PowerPoint как книгу, когда вы сохраняете её в формате PPTX. Создание новой книги даёт чистый холст для скопированного диапазона.

```csharp
// Create a new empty workbook that will become the PowerPoint slide
Workbook destinationWorkbook = new Workbook();

// Use the first worksheet of the new workbook
Worksheet destinationSheet = destinationWorkbook.Worksheets[0];
```

**Подсказка:** Если вам нужно несколько слайдов, вы можете добавить дополнительные листы и позже сохранить каждый из них как отдельный файл PPTX.

### Шаг 3: Скопируйте диапазон, сохранив сводную таблицу

Метод `CopyRange` принимает объект `PasteOptions`. Установка `CopyPivotTables = true` сообщает Aspose.Cells сохранять структуру сводной таблицы, а не только отрисованные значения.

```csharp
// Copy the defined range, preserving the pivot table definition
destinationSheet.Cells.CopyRange(
    sourceRange,
    new PasteOptions { CopyPivotTables = true });
```

**Как это работает:**  
Когда `CopyPivotTables` равно true, лист назначения получает как исходные данные, так и кэш сводной таблицы. Это означает, что сводная таблица остаётся полностью функциональной и её можно обновлять позже, если изменятся исходные данные.

### Шаг 4: Сохраните книгу как файл PowerPoint

Наконец, экспортируйте книгу в формат PPTX. Флаг `SaveFormat.Pptx` указывает Aspose.Cells записать лист как слайд PowerPoint.

```csharp
// Save the destination workbook as a PowerPoint presentation
destinationWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.pptx", SaveFormat.Pptx);
```

**Результат:**  
`CopyWithPivot.pptx` открывается в Microsoft PowerPoint (или любом совместимом просмотрщике) с одним слайдом, на котором отображён скопированный диапазон, включая живую сводную таблицу, с которой можно взаимодействовать в PowerPoint.

## Полный исполняемый пример

Ниже приведена полная программа, которую можно вставить в новый консольный проект и сразу запустить.

```csharp
using Aspose.Cells;
using System;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load source workbook and select the range containing the pivot table
            Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");
            Worksheet sourceSheet = sourceWorkbook.Worksheets[0];
            Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");

            // 2️⃣ Create a fresh workbook that will become the PowerPoint slide
            Workbook destinationWorkbook = new Workbook();
            Worksheet destinationSheet = destinationWorkbook.Worksheets[0];

            // 3️⃣ Copy the range, preserving the pivot table definition
            destinationSheet.Cells.CopyRange(
                sourceRange,
                new PasteOptions { CopyPivotTables = true });

            // 4️⃣ Export the workbook as a PPTX file
            destinationWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.pptx", SaveFormat.Pptx);

            Console.WriteLine("PowerPoint file created successfully.");
        }
    }
}
```

**Ожидаемый вывод:**  
При запуске программа выводит «PowerPoint file created successfully.» и создаёт файл `CopyWithPivot.pptx`. Открытие файла в PowerPoint показывает один слайд, где скопированный диапазон Excel отображается точно так же, как в исходном листе, с активной сводной таблицей, которую можно обновлять из PowerPoint.

## Распространённые варианты и граничные случаи

| Ситуация | Что изменить |
|-----------|----------------|
| **Несколько сводных таблиц** | Определите отдельные объекты `Range` для каждой таблицы и вызовите `CopyRange` для каждой, либо скопируйте весь лист, если они используют один источник данных. |
| **Большие наборы данных** | Увеличьте диапазон (например, `"A1:Z5000"`). Рассмотрите возможность включения `PasteOptions.CompressData = true` для уменьшения размера PPTX. |
| **Разные макеты слайдов** | После сохранения в PPTX откройте файл в PowerPoint и примените пользовательский макет или тему; данные останутся редактируемыми. |
| **Сохранение в поток** | Используйте `destinationWorkbook.Save(stream, SaveFormat.Pptx)`, когда нужно вернуть PPTX через веб‑API. |
| **Сохранение форматирования ячеек** | Установите `PasteOptions.PasteType = PasteType.All`, чтобы сохранить шрифты, цвета и границы. |

**Профессиональный совет:** Всегда проверяйте, существует ли целевая папка перед вызовом `Save`. Если папка отсутствует, `Save` бросит `DirectoryNotFoundException`.

## Заключение

Теперь вы знаете, как создать PowerPoint из Excel, скопировать сводную таблицу и экспортировать результат в файл PPTX с помощью Aspose.Cells. Шаги — загрузка исходной книги, определение диапазона, копирование с `CopyPivotTables` и сохранение в PPTX — охватывают весь рабочий процесс надёжным, готовым к продакшену способом.

Далее изучайте **как экспортировать Excel в PPTX** для нескольких листов или **как копировать диапазон между книгами**, когда нужно объединить данные из нескольких источников перед генерацией набора слайдов. Оба направления опираются на один и тот же API и могут быть комбинированы для автоматизации сложных конвейеров отчётности.

Удачной разработки и приятного превращения ваших таблиц в стильные презентации!

## Что изучать дальше?

Следующие учебные материалы охватывают тесно связанные темы, построенные на техниках, продемонстрированных в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы в ваших проектах.

- [How to Copy Pivot Table in C# – Convert Excel to PPTX, Copy Range & Make Textbox](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/)
- [Create New Workbook – How to Copy a Worksheet with a Pivot Table](/cells/english/net/excel-copy-worksheet/create-new-workbook-how-to-copy-a-worksheet-with-a-pivot-tab/)
- [How to Create and Save Excel Files with Aspose.Cells for .NET: A Complete Guide](/cells/english/net/workbook-operations/create-save-excel-file-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}