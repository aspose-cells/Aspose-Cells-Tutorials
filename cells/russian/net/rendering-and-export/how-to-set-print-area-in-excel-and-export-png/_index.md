---
category: general
date: 2026-09-27
description: Установите область печати в Excel и узнайте, как экспортировать PNG‑изображения
  выбранных ячеек. В этом руководстве также рассматривается сохранение диапазона как
  изображения и добавление картинки на лист.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set print area excel
- how to export png
- save range as image
- add picture to worksheet
- export selected cells image
language: ru
lastmod: 2026-09-27
og_description: Установите область печати в Excel и экспортируйте PNG с помощью Aspose.Cells.
  Следуйте этому пошаговому руководству, чтобы сохранить диапазон как изображение
  и добавить картинку на лист.
og_image_alt: Screenshot showing set print area excel and exported PNG file
og_title: Установить область печати в Excel – экспорт PNG в C#
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Set print area in Excel and learn how to export PNG images of selected
    cells. This guide also covers saving range as image and adding picture to worksheet.
  headline: How to set print area in Excel and export PNG
  type: TechArticle
tags:
- Excel automation
- C#
- Aspose.Cells
title: Как установить область печати в Excel и экспортировать PNG
url: /ru/net/rendering-and-export/how-to-set-print-area-in-excel-and-export-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как задать область печати в Excel и экспортировать PNG

Если вам нужно **set print area excel** перед созданием изображения, это руководство покажет, как это сделать. Вы также узнаете, **how to export png** файлы из определённого диапазона, **save range as image**, и **add picture to worksheet** в едином, повторяемом рабочем процессе.

Работа с Excel программно часто подразумевает, что вам нужен только подмножество ячеек — например, сводная таблица или диаграмма — в виде изображения. Определив область печати заранее, вы гарантируете, что экспортированный PNG будет содержать ровно те ячейки, которые вам нужны, ни больше ни меньше. Это руководство проведёт вас через каждый шаг, от загрузки книги до сохранения окончательного PNG‑файла, и объяснит, почему каждую настройку важно учитывать.

## Prerequisites

Прежде чем начать, убедитесь, что у вас есть:

* .NET 6.0 или более поздняя версия  
* Visual Studio 2022 (или любой IDE для C#)  
* NuGet‑пакет **Aspose.Cells for .NET** (`Install-Package Aspose.Cells`)  
* Файл Excel (`input.xlsx`) в известном каталоге  

Эти требования гарантируют, что код будет работать без дополнительной настройки.

## Step 1: Load the workbook you want to work with

```csharp
using Aspose.Cells;
using System.Drawing.Imaging;

// Load the workbook from disk
Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");
```

Класс `Workbook` представляет весь файл Excel. Его загрузка в начале даёт доступ к листам, ячейкам и параметрам настройки страниц.

## Step 2: **Set print area excel** for the target range

```csharp
// Define the range you want to capture
string printArea = "A1:G20";

// Apply the range as the print area on the first worksheet
workbook.Worksheets[0].PageSetup.PrintArea = printArea;
```

Установка **print area** сообщает Excel (и Aspose.Cells), какие ячейки принадлежат печатной странице. При последующем экспорте листа в изображение будет отрисована только эта область, что критично для чистого **export selected cells image**.

## Step 3: Configure image export options – **how to export png**

```csharp
ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
{
    ImageFormat = ImageFormat.Png,   // PNG ensures lossless quality
    OnePagePerSheet = true           // Export the defined print area as a single page
};
```

`ImageOrPrintOptions` управляет форматом вывода. Выбирая `ImageFormat.Png`, вы получаете изображение высокого разрешения с прозрачным фоном, которое хорошо работает как в вебе, так и в настольных приложениях.

## Step 4: Create a picture from the defined range and **add picture to worksheet**

```csharp
// Create a picture object from the selected range
Picture picture = workbook.Worksheets[0].Pictures.Add(
    0,                                     // top‑left row index where the picture will be placed
    0,                                     // top‑left column index where the picture will be placed
    workbook.Worksheets[0].Cells.CreateRange(printArea));
```

Метод `Pictures.Add` вставляет новое изображение на лист. Передавая диапазон, созданный на Шаге 2, вы **save range as image** непосредственно на листе, что удобно, если позже понадобится ссылаться на картинку в других частях книги.

## Step 5: **Save the picture as an image file** – completing the **export selected cells image** workflow

```csharp
// Save the picture to disk as a PNG file
picture.Save(@"YOUR_DIRECTORY\selected_range.png", imageOptions);
```

Вызов `Save` записывает картинку в файловую систему, используя параметры, определённые на Шаге 3. Полученный файл `selected_range.png` содержит ровно те ячейки, которые заданы командой **set print area excel**.

## Full, runnable example

Собрав все части вместе, вы получаете компактную программу, которую можно вставить в любое консольное приложение:

```csharp
using System;
using Aspose.Cells;
using System.Drawing.Imaging;

class ExportExcelRangeAsPng
{
    static void Main()
    {
        // 1️⃣ Load the workbook
        Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");

        // 2️⃣ Set print area excel
        string printArea = "A1:G20";
        workbook.Worksheets[0].PageSetup.PrintArea = printArea;

        // 3️⃣ Configure how to export png
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
        {
            ImageFormat = ImageFormat.Png,
            OnePagePerSheet = true
        };

        // 4️⃣ Add picture to worksheet (save range as image)
        Picture picture = workbook.Worksheets[0].Pictures.Add(
            0,
            0,
            workbook.Worksheets[0].Cells.CreateRange(printArea));

        // 5️⃣ Export selected cells image
        picture.Save(@"YOUR_DIRECTORY\selected_range.png", imageOptions);

        Console.WriteLine("PNG exported successfully to YOUR_DIRECTORY\\selected_range.png");
    }
}
```

### Expected output

Запуск программы выводит:

```
PNG exported successfully to YOUR_DIRECTORY\selected_range.png
```

И в каталоге появится файл `selected_range.png`, показывающий только ячейки A1‑G20 из `input.xlsx`.

## Common pitfalls and how to avoid them

| Issue | Why it happens | Fix |
|-------|----------------|-----|
| The exported image contains the whole sheet | No print area was defined | Ensure you **set print area excel** before creating the picture |
| PNG is blurry | Default DPI is low | Set `imageOptions.DpiX` and `imageOptions.DpiY` to a higher value (e.g., 300) |
| File not found error | Wrong directory path | Use `Path.Combine` or double‑check the folder exists |
| Picture appears offset | Incorrect row/column indices | The first two parameters of `Pictures.Add` are the top‑left cell where the picture is placed; keep them at `0,0` for a clean export |

## Pro tip: Export multiple ranges in one run

Если нужно **export selected cells image** для нескольких областей, повторите Шаги 2‑5 внутри цикла, меняя `printArea` на каждой итерации. Не забудьте давать каждому изображению уникальное имя файла, иначе последующее сохранение перезапишет предыдущий файл.

## Conclusion

Теперь вы знаете, как **set print area excel**, настроить **how to export png**, **save range as image** и **add picture to worksheet** с помощью Aspose.Cells. Это сквозное решение позволяет превратить любой блок ячеек в PNG высокого качества всего несколькими строками кода C#.

Дальше вы можете изучить:

* Добавление границ или водяных знаков к экспортированному PNG (поиск *add picture to worksheet* со стилизацией)  
* Экспорт напрямую в PDF для печатных отчётов (*export selected cells image* → PDF workflow)  
* Автоматизацию процесса для множества книг в пакетной задаче  

Экспериментируйте с различными диапазонами, настройками DPI и форматами изображений, чтобы подобрать оптимальное решение для вашего проекта. Приятного кодинга!

## What Should You Learn Next?

Следующие учебные материалы охватывают тесно связанные темы, расширяющие техники, продемонстрированные в этом руководстве. Каждый ресурс содержит полностью работающие примеры кода с пошаговыми объяснениями, помогающими освоить дополнительные возможности API и исследовать альтернативные подходы в ваших проектах.

- [Задать область печати в Excel и экспортировать в PowerPoint – пошаговое руководство](/cells/english/net/converting-excel-files-to-other-formats/set-print-area-in-excel-and-export-to-powerpoint-step-by-ste/)
- [Экспортировать область печати Excel в HTML с Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-print-area-html-aspose-cells-java/)
- [Как задать область печати в Excel с помощью Aspose.Cells для .NET](/cells/english/net/headers-footers/set-print-area-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}