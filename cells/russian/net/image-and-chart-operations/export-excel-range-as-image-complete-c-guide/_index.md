---
category: general
date: 2026-06-08
description: Экспорт диапазона Excel в виде изображения с использованием C# и Aspose.Cells.
  Узнайте, как сохранить лист Excel как изображение всего за несколько простых шагов.
draft: false
keywords:
- export excel range as image
- save excel worksheet as image
- Aspose.Cells image export
- C# Excel automation
- pivot table to image
language: ru
og_description: Экспорт диапазона Excel в виде изображения с помощью C#. Этот учебник
  показывает, как быстро и надёжно сохранить лист Excel как изображение.
og_title: Экспорт диапазона Excel в изображение – Полное руководство по C#
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Export Excel range as image using C# and Aspose.Cells. Learn how to
    save Excel worksheet as image in just a few simple steps.
  headline: Export Excel Range as Image – Complete C# Guide
  type: TechArticle
- description: Export Excel range as image using C# and Aspose.Cells. Learn how to
    save Excel worksheet as image in just a few simple steps.
  name: Export Excel Range as Image – Complete C# Guide
  steps:
  - name: Prerequisites
    text: '- .NET 6.0 or later (the code also works on .NET Framework 4.7+). - Aspose.Cells
      for .NET ≥ 23.9 (you can grab a free trial from the Aspose website). - A basic
      understanding of C# and file I/O.'
  - name: What the code does
    text: '- `exportRange.ToImage` captures only the cells inside the range (pivot
      table or custom block). - `worksheet.ToImage` captures the *entire* visible
      area of the worksheet, effectively **save excel worksheet as image**.'
  - name: Multiple Pivot Tables
    text: 'If your workbook contains more than one pivot table, you can loop through
      them:'
  - name: Very Large Ranges
    text: 'Exporting a massive range (e.g., thousands of rows) can consume a lot of
      memory. Mitigate this by:'
  - name: Transparent Backgrounds
    text: 'If you need a transparent background (useful for overlaying on web pages),
      set the background color to `Color.Transparent` before export:'
  - name: File Permissions
    text: Make sure the target directory exists and your process has write permission.
      Otherwise `ToImage` throws an `IOException`.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel
- ImageExport
title: Экспорт диапазона Excel в изображение – полное руководство по C#
url: /ru/net/image-and-chart-operations/export-excel-range-as-image-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Экспорт диапазона Excel в изображение – Полное руководство C#  

Когда‑нибудь вам нужно было **export Excel range as image**, но вы не знали, какой вызов API использовать? Вы не одиноки. Независимо от того, создаёте ли вы панель отчётов или вам нужен снимок сводной таблицы для слайда PowerPoint, преобразование блока ячеек в PNG — полезный приём.  

В этом руководстве мы пройдём через полностью автономный пример, который не только **export excel range as image**, но и покажет, как **save excel worksheet as image** для всего листа. Никаких внешних скриптов, только чистый C# и Aspose.Cells, так что вы можете скопировать‑вставить код и сразу увидеть результат.  

## Что вы узнаете  

- Загрузить существующую книгу и найти конкретный диапазон (сводную таблицу или любой блок ячеек).  
- Настроить параметры экспорта изображения, такие как формат, разрешение и масштабирование.  
- Экспортировать один диапазон в PNG, JPEG или BMP.  
- Расширить ту же логику для **save excel worksheet as image** в одну строку.  
- Советы по работе с несколькими сводными таблицами, большими диапазонами и типичными подводными камнями.  

### Требования  

- .NET 6.0 или новее (код также работает на .NET Framework 4.7+).  
- Aspose.Cells for .NET ≥ 23.9 (можно получить бесплатную пробную версию на сайте Aspose).  
- Базовое понимание C# и ввода‑вывода файлов.  

Если у вас есть всё необходимое, давайте приступим.  

## Шаг 1: Настройте проект и импортируйте пространства имён  

Сначала создайте новое консольное приложение (или интегрируйте код в любой существующий проект). Добавьте пакет Aspose.Cells через NuGet:  

```bash
dotnet add package Aspose.Cells
```  

Затем импортируйте необходимые пространства имён:  

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Drawing;   // For ImageOrPrintOptions
using System.Drawing.Imaging; // For ImageFormat enum
```  

> **Pro tip:** Держите ваши директивы `using` в начале файла; так код легче просматривать — особенно когда вы позже добавляете новые возможности Aspose.  

## Шаг 2: Загрузите книгу, содержащую целевой диапазон  

Вам нужна книга на диске. Замените `YOUR_DIRECTORY/input.xlsx` реальным путём к вашему файлу.  

```csharp
// Step 2: Load the workbook containing the data you want to capture
Workbook workbook = new Workbook(@"YOUR_DIRECTORY/input.xlsx");

// Quick sanity check – make sure the file loaded correctly
if (workbook == null)
{
    Console.WriteLine("Failed to load workbook. Check the file path.");
    return;
}
```  

Почему этот шаг важен: объект `Workbook` является точкой входа для любой операции Aspose.Cells. Без него вы не сможете обращаться к листам, диапазонам или сводным таблицам.  

## Шаг 3: Определите диапазон для экспорта  

У вас есть два типичных сценария:  

1. **A specific pivot table** – код, который вы использовали, использует `PivotTables[0].PivotTableRange`.  
2. **An arbitrary cell block** – вы можете использовать `worksheet.Cells.CreateRange("B2:D10")`.  

Ниже мы обрабатываем оба случая, позволяя вам выбрать подходящий.  

```csharp
// Step 3a: Get the first worksheet (index 0)
Worksheet worksheet = workbook.Worksheets[0];

// Option A: Export the first pivot table's range
Range exportRange;
if (worksheet.PivotTables.Count > 0)
{
    exportRange = worksheet.PivotTables[0].PivotTableRange;
}
else
{
    // Option B: Fallback to a manual range (e.g., B2:D10)
    exportRange = worksheet.Cells.CreateRange("B2:D10");
}
```  

> **Why we check for pivot tables first:** Многие файлы отчётов полагаются на динамические данные сводных таблиц. Если их нет, запасной вариант гарантирует, что руководство всё равно будет работать.  

## Шаг 4: Настройте параметры экспорта изображения  

Aspose.Cells предоставляет детальный контроль над выходным изображением. Наиболее часто используемые параметры — формат, разрешение (DPI) и включение линий сетки.  

```csharp
// Step 4: Set up image export options
ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
{
    ImageFormat = ImageFormat.Png,   // PNG works well for lossless quality
    HorizontalResolution = 300,      // 300 DPI for crisp prints
    VerticalResolution = 300,
    // Optional: uncomment to hide gridlines
    // IsGridlinesVisible = false
};
```  

Вы можете переключить на `ImageFormat.Jpeg` или `ImageFormat.Bmp`, если ваша downstream‑система предпочитает эти типы. Параметр DPI важен, когда вы вставляете изображение в PDF высокого разрешения или в презентации.  

## Шаг 5: Экспортируйте диапазон (или весь лист) в виде изображения  

Теперь происходит магия. Метод `ToImage` записывает визуальное представление диапазона непосредственно на диск.  

```csharp
// Step 5a: Export the selected range to an image file
string rangeImagePath = @"YOUR_DIRECTORY/PivotRange.png";
exportRange.ToImage(rangeImagePath, imgOptions);
Console.WriteLine($"Range exported to: {rangeImagePath}");

// Step 5b: If you need to **save excel worksheet as image**, use the worksheet's ToImage overload
string sheetImagePath = @"YOUR_DIRECTORY/FullSheet.png";
worksheet.ToImage(sheetImagePath, imgOptions);
Console.WriteLine($"Worksheet exported to: {sheetImagePath}");
```  

### Что делает код  

- `exportRange.ToImage` захватывает только ячейки внутри диапазона (сводная таблица или пользовательский блок).  
- `worksheet.ToImage` захватывает *всю* видимую область листа, эффективно **save excel worksheet as image**.  

Оба вызова учитывают параметры, заданные ранее, поэтому вы получите PNG‑файлы с разрешением 300 DPI.  

## Обработка граничных случаев и часто задаваемые вопросы  

### Несколько сводных таблиц  

Если ваша книга содержит более одной сводной таблицы, вы можете пройтись по ним в цикле:  

```csharp
for (int i = 0; i < worksheet.PivotTables.Count; i++)
{
    Range ptRange = worksheet.PivotTables[i].PivotTableRange;
    string outPath = $@"YOUR_DIRECTORY/Pivot_{i}.png";
    ptRange.ToImage(outPath, imgOptions);
    Console.WriteLine($"Pivot {i} saved to {outPath}");
}
```  

### Очень большие диапазоны  

Экспортировать огромный диапазон (например, тысячи строк) может потребовать много памяти. Смягчить это можно, используя:  

- Уменьшить `HorizontalResolution` / `VerticalResolution`.  
- Экспортировать по частям (разбить диапазон на более мелкие блоки).  

### Прозрачный фон  

Если вам нужен прозрачный фон (полезно для наложения на веб‑страницы), установите цвет фона в `Color.Transparent` перед экспортом:  

```csharp
imgOptions.BackgroundColor = System.Drawing.Color.Transparent;
```  

### Права доступа к файлам  

Убедитесь, что целевая директория существует и у вашего процесса есть права на запись. Иначе `ToImage` бросит `IOException`.  

## Полный рабочий пример  

Собрав всё вместе, представляем готовую к запуску консольную программу:  

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing.Imaging;

namespace ExcelImageExportDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Adjust these paths for your environment
            string inputPath = @"YOUR_DIRECTORY/input.xlsx";
            string rangeImagePath = @"YOUR_DIRECTORY/PivotRange.png";
            string sheetImagePath = @"YOUR_DIRECTORY/FullSheet.png";

            // Load workbook
            Workbook workbook = new Workbook(inputPath);
            Worksheet worksheet = workbook.Worksheets[0];

            // Determine which range to export
            Range exportRange;
            if (worksheet.PivotTables.Count > 0)
            {
                exportRange = worksheet.PivotTables[0].PivotTableRange;
            }
            else
            {
                exportRange = worksheet.Cells.CreateRange("B2:D10");
            }

            // Configure image options
            ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
            {
                ImageFormat = ImageFormat.Png,
                HorizontalResolution = 300,
                VerticalResolution = 300
            };

            // Export range as image
            exportRange.ToImage(rangeImagePath, imgOptions);
            Console.WriteLine($"Range exported to: {rangeImagePath}");

            // Export entire worksheet as image
            worksheet.ToImage(sheetImagePath, imgOptions);
            Console.WriteLine($"Worksheet exported to: {sheetImagePath}");
        }
    }
}
```  

**Ожидаемый вывод** (консоль):  

```
Range exported to: YOUR_DIRECTORY/PivotRange.png
Worksheet exported to: YOUR_DIRECTORY/FullSheet.png
```  

Откройте сгенерированные PNG‑файлы, и вы увидите пиксель‑точный снимок выбранного диапазона и полного листа соответственно.  

## Заключение  

Мы только что рассмотрели всё, что вам нужно для **export excel range as image**, а также как **save excel worksheet as image** с помощью Aspose.Cells и C#. От загрузки книги до тонкой настройки параметров изображения и работы с несколькими сводными таблицами — шаги просты и полностью воспроизводимы.  

Далее вы можете:  

- Экспериментировать с различными значениями `ImageFormat` (JPEG, BMP).  
- Объединить изображение с PDF, используя класс `Document` для генерации отчётов.  
- Автоматизировать процесс для пакета файлов в папке.  

Не стесняйтесь адаптировать фрагмент под ваш рабочий процесс — будь то передача изображений в веб‑API, встраивание их в письма или генерация печатных отчётов. Приятного кодинга, и пусть изображения говорят за ваши данные Excel!  

## Что следует изучить дальше?  

Следующие руководства охватывают близко связанные темы, которые развивают техники, продемонстрированные в этом руководстве. Каждый ресурс включает полностью рабочие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.  

- [Export Excel Cells to Image Using Aspose.Cells .NET&#58; A Step-by-Step Guide](/cells/english/net/import-export/export-excel-cells-to-image-aspose-dotnet/)  
- [Export Excel Workbook as Image Using Aspose.Cells for Java&#58; A Step-by-Step Guide](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)  
- [Export Excel Workbook As Image Using Aspose Cells For Java](/cells/german/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}