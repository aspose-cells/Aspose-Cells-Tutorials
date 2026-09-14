---
category: general
date: 2026-09-11
description: Копировать сводную таблицу и экспортировать Excel в PPTX с помощью Aspose.Cells.
  Узнайте, как создавать редактируемый PPTX и сохранять книгу в формате PPTX на C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- export excel to pptx
- generate editable pptx
- save workbook as pptx
- export excel sheet pptx
language: ru
lastmod: 2026-09-11
og_description: Копировать сводную таблицу и экспортировать Excel в PPTX на C# с помощью
  Aspose.Cells. Генерировать редактируемый PPTX и сохранять книгу как PPTX с помощью
  нескольких строк кода.
og_image_alt: Screenshot of copy pivot table code and generated editable PPTX slide
og_title: Копирование сводной таблицы и экспорт Excel в PPTX – полное руководство
  по C#
schemas:
- author: Aspose
  dateModified: '2026-09-11'
  description: Copy pivot table and export Excel to PPTX using Aspose.Cells. Learn
    to generate editable PPTX and save workbook as PPTX in C#.
  headline: Copy pivot table and export Excel to PPTX with Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel
- PPTX
- Pivot Table
title: Копировать сводную таблицу и экспортировать Excel в PPTX с помощью Aspose.Cells
url: /ru/net/converting-excel-files-to-other-formats/copy-pivot-table-and-export-excel-to-pptx-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Копировать сводную таблицу и экспортировать Excel в PPTX с помощью Aspose.Cells

Если вам нужно скопировать сводную таблицу с одного листа на другой, а затем экспортировать файл Excel в презентацию PowerPoint, это руководство покажет, как это сделать. С помощью Aspose.Cells вы можете создать редактируемый PPTX и сохранить рабочую книгу как PPTX всего за несколько строк кода на C#.

В руководстве рассматривается каждый шаг, необходимый для перемещения сводной таблицы, сохранения её функциональности и создания файла PPTX, в котором диаграммы и фигуры остаются редактируемыми. Внешние инструменты не требуются — только библиотека Aspose.Cells и среда разработки .NET.

## Что вы достигнете

* **Copy pivot table** из исходного листа в лист назначения, сохраняя все соединения данных.  
* **Export Excel to PPTX** так, чтобы полученный слайд можно было редактировать в PowerPoint.  
* **Generate editable PPTX** где диаграммы, таблицы и фигуры не преобразуются в изображения.  
* **Save workbook as PPTX** используя тот же вызов API Aspose.Cells.  

### Предварительные требования

* .NET 6.0 или новее (код также работает с .NET Framework 4.6+).  
* Aspose.Cells for .NET (NuGet‑пакет `Aspose.Cells`).  
* Базовое понимание консольных приложений C#.  

> **Совет:** Установите пакет NuGet через CLI, чтобы гарантировать наличие последней версии:  
> ```bash
> dotnet add package Aspose.Cells
> ```

## Как скопировать сводную таблицу между листами

Первая операция — перемещение сводной таблицы при сохранении её определения. Aspose.Cells предоставляет метод `CopyRange` с объектом `CopyOptions`, который включает флаг `CopyPivotTable`.

```csharp
using Aspose.Cells;
using Aspose.Cells.Export;

// Load the workbook that contains the source and destination worksheets.
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

// Identify the worksheets by name.
Worksheet sourceSheet = workbook.Worksheets["Source"];
Worksheet destinationSheet = workbook.Worksheets["Destination"];

// Define the range that encloses the pivot table on the source sheet.
Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");

// Copy the range to the destination sheet, preserving the pivot table.
destinationSheet.Cells.CopyRange(
    sourceRange,
    0,                     // destination row index
    0,                     // destination column index
    new CopyOptions { CopyPivotTable = true });
```

**Почему это работает:**  
`CopyRange` копирует данные ячеек, форматирование и, когда `CopyPivotTable` установлен в `true`, кэш и метаданные сводной таблицы. Диапазон назначения начинается с ячейки `A1` (строка 0, столбец 0), но вы можете изменить смещения, чтобы разместить таблицу в другом месте.

**Типичный крайний случай:** Если лист назначения уже содержит сводную таблицу с тем же именем, Aspose.Cells автоматически переименует импортируемую таблицу, предотвращая конфликт имён.

## Экспортировать Excel в PPTX и создать редактируемый PPTX

После того как сводная таблица находится на месте, вы можете экспортировать всю рабочую книгу в файл PPTX. Класс `ImageOrPrintOptions` позволяет задать `ExportImageFormat = ImageFormat.Pptx`, что указывает Aspose.Cells рассматривать вывод как презентацию PowerPoint, а не растровое изображение.

```csharp
// Configure export options to produce an editable PPTX.
ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
{
    ExportImageFormat = ImageFormat.Pptx
};

// Save the workbook as an editable PPTX file.
workbook.Save("YOUR_DIRECTORY/output.pptx", SaveFormat.Pptx, exportOptions);
```

**Почему это работает:**  
Когда `ExportImageFormat` установлен в `Pptx`, Aspose.Cells преобразует каждый лист в отдельный слайд. Фигуры, диаграммы и сводные таблицы записываются как нативные объекты PowerPoint, поэтому вы можете дважды щёлкнуть по ним в PowerPoint и редактировать исходные данные.

**Совет для больших книг:** Если вам нужен только подмножество листов, вызовите `workbook.Worksheets.RemoveAt(index)` для листов, которые не требуется экспортировать, перед вызовом `Save`. Это уменьшит размер файла PPTX.

## Полный, исполняемый пример

Ниже приведена полная программа, объединяющая предыдущие шаги. Замените `YOUR_DIRECTORY` фактическим путём на вашем компьютере.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Export;

class Example
{
    static void Main()
    {
        // 1. Load the workbook that contains the source and destination worksheets.
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // 2. Identify the source and destination worksheets.
        Worksheet sourceSheet = workbook.Worksheets["Source"];
        Worksheet destinationSheet = workbook.Worksheets["Destination"];

        // 3. Define the range that holds the pivot table.
        Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");

        // 4. Copy the range, preserving the pivot table.
        destinationSheet.Cells.CopyRange(
            sourceRange,
            0,
            0,
            new CopyOptions { CopyPivotTable = true });

        // 5. Set up export options to generate an editable PPTX.
        ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
        {
            ExportImageFormat = ImageFormat.Pptx
        };

        // 6. Save the workbook as a PPTX document.
        workbook.Save("YOUR_DIRECTORY/output.pptx", SaveFormat.Pptx, exportOptions);

        Console.WriteLine("Pivot table copied and workbook exported to PPTX successfully.");
    }
}
```

### Ожидаемый вывод

Запуск программы выводит:

```
Pivot table copied and workbook exported to PPTX successfully.
```

Когда вы откроете `output.pptx` в Microsoft PowerPoint, вы увидите слайд, содержащий скопированную сводную таблицу в виде редактируемой диаграммы. Двойной щелчок по диаграмме открывает редактор диаграмм PowerPoint, позволяя изменять серии, оси и подписи данных без возврата в Excel.

## Обработка типичных подводных камней

| Проблема | Причина | Решение |
|----------|---------|----------|
| Сводная таблица отображается как статическое изображение | Флаг `CopyPivotTable` не указан или `ExportImageFormat` установлен в `Png` | Убедитесь, что `CopyPivotTable = true` и `ExportImageFormat = ImageFormat.Pptx`. |
| На листе назначения пустые ячейки | Диапазон источника не охватывает всю область сводной таблицы | Расширьте диапазон (например, `"A1:H30"`), чтобы включить все поля сводной таблицы. |
| Экспортированный PPTX огромный | Включены ненужные листы | Удалите лишние листы перед вызовом `Save`. |
| PowerPoint не позволяет редактировать диаграмму | Используется более старая версия Aspose.Cells без поддержки PPTX | Обновите до последней версии Aspose.Cells (см. примечания к выпуску). |

## Следующие шаги и связанные темы

* **Export Excel sheet to PPTX with custom slide layouts** – изучите `WorksheetToPdfConverter` для более тонкой настройки внешнего вида слайдов.  
* **Export Excel to PDF** – замените `ImageFormat.Pptx` на `ImageFormat.Pdf`, чтобы создать PDF вместо PPTX.  
* **Programmatically modify PPTX after export** – используйте библиотеку `Aspose.Slides` для добавления анимаций или заметок докладчика.  

Освоив **copy pivot table**, **export excel to pptx** и **generate editable pptx**, вы сможете построить сквозные конвейеры отчётности, перемещающие данные из электронных таблиц напрямую в презентационные наборы без потери возможности редактирования.

---

## Что вам следует изучить дальше?

Следующие руководства охватывают тесно связанные темы, построенные на техниках, продемонстрированных в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, помогающими вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в собственных проектах.

- [Как скопировать сводную таблицу в C# – Конвертировать Excel в PPTX, копировать диапазон и создавать текстовое поле](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/)
- [Создать новую рабочую книгу Excel – Копировать и дублировать сводную таблицу](/cells/english/net/pivot-tables/create-new-excel-workbook-copy-duplicate-pivot-table/)
- [Создать сводную таблицу в Excel с помощью Aspose.Cells for .NET](/cells/english/net/pivot-tables/create-pivot-table/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}