---
category: general
date: 2026-10-10
description: Конвертировать Excel в PowerPoint и задать область печати в C# с помощью
  Aspose.Cells – узнайте, как экспортировать Excel, установить область печати и создать
  файл PPTX.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert excel to powerpoint
- set print area excel
- how to export excel
- how to set print area
- convert excel to pptx
language: ru
lastmod: 2026-10-10
og_description: Конвертировать Excel в PowerPoint с помощью Aspose.Cells. Этот учебник
  показывает, как установить область печати, экспортировать Excel и создать файл PPTX
  на C#.
og_image_alt: Screenshot of code that converts Excel to PowerPoint while setting the
  print area
og_title: Конвертировать Excel в PowerPoint – полное руководство для разработчиков
  C#
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Convert Excel to PowerPoint and set print area in C# with Aspose.Cells
    – learn how to export Excel, set print area, and generate a PPTX file.
  headline: Convert Excel to PowerPoint and set print area
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
- PowerPoint export
title: Преобразовать Excel в PowerPoint и задать область печати
url: /ru/net/converting-excel-files-to-other-formats/convert-excel-to-powerpoint-and-set-print-area/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Преобразование Excel в PowerPoint и установка области печати

Если вам нужно **преобразовать Excel в PowerPoint**, это руководство покажет, как сделать это на C#. Определив область печати заранее, вы контролируете, какие ячейки появятся на каждом слайде, а итоговый файл PPTX будет соответствовать вашим ожиданиям по макету. Решение также отвечает на вопросы «как экспортировать Excel» и «как установить область печати», используя одну и ту же кодовую базу.

В этом учебнике вы:

* Загрузите существующую книгу.
* Установите область печати для листа (шаг **set print area excel**).
* Настроите параметры конвертации для вывода в PowerPoint.
* Сгенерируете файл **convert excel to pptx** одним вызовом метода.

Весь необходимый код включён, так что вы можете скопировать, вставить и сразу запустить его.

## Требования

Прежде чем начать, убедитесь, что у вас есть:

| Требование | Почему это важно |
|-------------|-------------------|
| **.NET 6.0 или новее** | Пример ориентирован на .NET 6+, но любой .NET, поддерживающий C# 10, подойдет. |
| **Aspose.Cells for .NET** | Эта библиотека предоставляет `Workbook`, `ImageOrPrintOptions` и метод `ConvertToPdf` (используется для PPTX). Установите её через NuGet: `dotnet add package Aspose.Cells` |
| **Входной файл Excel** | В руководстве используется `input.xlsx`. Поместите его в папку, к которой можно обратиться из кода. |
| **Права записи в папку вывода** | Программа записывает `output.pptx`. Убедитесь, что каталог существует и доступен для записи. |

> **Pro tip:** Если вы работаете с несколькими листами, повторите шаг установки области печати для каждого листа перед конвертацией.

## Шаг 1: Создайте новый консольный проект C#

Откройте терминал или окно PowerShell и выполните:

```bash
dotnet new console -n ExcelToPowerPointDemo
cd ExcelToPowerPointDemo
dotnet add package Aspose.Cells
```

Это создаст новый проект с именем **ExcelToPowerPointDemo** и добавит пакет Aspose.Cells, который является основной зависимостью для **how to export Excel** в другие форматы.

## Шаг 2: Напишите код конвертации

Замените содержимое `Program.cs` полным примером ниже. Код демонстрирует **convert excel to powerpoint**, показывает **how to set print area** и создаёт файл **convert excel to pptx**.

```csharp
using System;
using Aspose.Cells;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // 1️⃣ Load the workbook (how to export Excel)
            // -----------------------------------------------------------------
            string inputPath = @"YOUR_DIRECTORY\input.xlsx";
            Workbook workbook = new Workbook(inputPath);
            Console.WriteLine($"Loaded workbook with {workbook.Worksheets.Count} worksheet(s).");

            // -----------------------------------------------------------------
            // 2️⃣ Define the print area for the first worksheet (set print area excel)
            // -----------------------------------------------------------------
            // The range "A1:G30" will be the only part visible on the slide.
            // Adjust the range to match the data you want to show.
            Worksheet sheet = workbook.Worksheets[0];
            sheet.PageSetup.PrintArea = "A1:G30";
            Console.WriteLine($"Print area set to {sheet.PageSetup.PrintArea} on sheet \"{sheet.Name}\".");

            // -----------------------------------------------------------------
            // 3️⃣ Configure conversion options for PowerPoint output
            // -----------------------------------------------------------------
            ImageOrPrintOptions conversionOptions = new ImageOrPrintOptions
            {
                // SaveFormat.Pptx tells Aspose.Cells to generate a PowerPoint file.
                SaveFormat = SaveFormat.Pptx,
                // Optional: set the slide size or DPI if needed.
                // HorizontalResolution = 300,
                // VerticalResolution = 300
            };

            // -----------------------------------------------------------------
            // 4️⃣ Convert the worksheet to a PowerPoint presentation (convert excel to powerpoint)
            // -----------------------------------------------------------------
            string outputPath = @"YOUR_DIRECTORY\output.pptx";
            sheet.ConvertToPdf(conversionOptions, outputPath);
            Console.WriteLine($"Successfully created PowerPoint file at: {outputPath}");
        }
    }
}
```

### Почему важна каждая часть

* **Загрузка книги** – Первый шаг в любой сцене **how to export Excel**. `Workbook` читает файл в память, давая полный доступ к листам, ячейкам и форматированию.
* **Установка области печати** – Присваивая `PageSetup.PrintArea`, вы указываете Aspose.Cells, какие ячейки рендерить. Это суть **set print area excel**; без этого будет экспортирован весь лист, что может привести к огромным, нечитаемым слайдам.
* **Выбор `SaveFormat.Pptx`** – Объект `ImageOrPrintOptions` позволяет переключать форматы вывода. Установка `SaveFormat` в `Pptx` запускает конвейер **convert excel to pptx**.
* **Вызов `ConvertToPdf`** – Несмотря на название метода, когда `SaveFormat` установлен в `Pptx`, библиотека выводит файл PowerPoint. Это рекомендуемый способ **convert excel to powerpoint** одним вызовом.

## Шаг 3: Запустите программу

Из папки проекта выполните:

```bash
dotnet run
```

Если всё настроено правильно, вы увидите вывод в консоли, похожий на:

```
Loaded workbook with 1 worksheet(s).
Print area set to A1:G30 on sheet "Sheet1".
Successfully created PowerPoint file at: YOUR_DIRECTORY\output.pptx
```

Откройте `output.pptx` в Microsoft PowerPoint или любом совместимом просмотрщике. Каждый слайд соответствует печатной странице листа, ограниченной заданным диапазоном.

## Обработка нескольких листов

Если в книге более одного листа и вы хотите, чтобы каждый лист имел собственный набор слайдов, пройдитесь по коллекции:

```csharp
for (int i = 0; i < workbook.Worksheets.Count; i++)
{
    Worksheet ws = workbook.Worksheets[i];
    ws.PageSetup.PrintArea = "A1:G30"; // adjust per sheet if needed
    string slidePath = $@"YOUR_DIRECTORY\output_sheet{i + 1}.pptx";
    ws.ConvertToPdf(conversionOptions, slidePath);
    Console.WriteLine($"Created {slidePath}");
}
```

Этот шаблон показывает **how to export Excel** лист за листом, при этом **setting print area** выполняется индивидуально.

## Особые случаи и рекомендации по лучшим практикам

| Ситуация | Рекомендуемый подход |
|-----------|----------------------|
| **Очень большие листы** | Уменьшите область печати или увеличьте `HorizontalResolution`/`VerticalResolution`, чтобы размер PPTX оставался управляемым. |
| **Разные ориентации страниц** | Установите `sheet.PageSetup.Orientation = PageOrientationType.Landscape;` перед конвертацией. |
| **Пользовательский размер слайда** | Используйте `conversionOptions.OnePagePerSheet = false;` и настройте `conversionOptions.Width` / `conversionOptions.Height`. |
| **Отсутствует входной файл** | Оберните код загрузки в блок `try { … } catch (FileNotFoundException)` для вывода понятного сообщения об ошибке. |
| **Не‑ASCII символы** | Убедитесь, что книга сохранена с кодировкой UTF‑8; Aspose.Cells автоматически обрабатывает Unicode. |

## Полный исходный код для справки

Ниже представлен весь код программы, включая директивы `using` и комментарии. Сохраните его как `Program.cs` в проекте, созданном на **Шаге 1**.

```csharp
using System;
using Aspose.Cells;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Path to the Excel file you want to convert.
            string inputPath = @"YOUR_DIRECTORY\input.xlsx";

            // 1️⃣ Load the workbook (how to export Excel)
            Workbook workbook = new Workbook(inputPath);

            // Select the first worksheet – you can loop for multiple sheets.
            Worksheet sheet = workbook.Worksheets[0];

            // 2️⃣ Set the print area (set print area excel)
            sheet.PageSetup.PrintArea = "A1:G30";

            // 3️⃣ Prepare conversion options for PowerPoint output.
            ImageOrPrintOptions conversionOptions = new ImageOrPrintOptions
            {
                SaveFormat = SaveFormat.Pptx   // This triggers convert excel to pptx
            };

            // 4️⃣ Convert the worksheet to PowerPoint (convert excel to powerpoint)
            string outputPath = @"YOUR_DIRECTORY\output.pptx";
            sheet.ConvertToPdf(conversionOptions, outputPath);

            Console.WriteLine("Conversion complete.");
        }
    }
}
```

## Ожидаемый результат

Запуск программы создаёт файл PowerPoint (`output.pptx`), содержащий:

* По одному слайду на каждую печатную страницу листа.
* Только ячейки из диапазона **A1:G30**, видимые на каждом слайде.
* Сохранённое форматирование (шрифты, цвета, границы) как в Excel.

Откройте файл в PowerPoint, чтобы убедиться, что макет соответствует установленной области печати.

## Заключение

Теперь вы знаете, как **convert Excel to PowerPoint**, точно **set print area excel** с помощью Aspose.Cells на C#. В этом руководстве рассмотрены **how to export Excel**, продемонстрировано **how to set print area** и показан полный процесс **convert excel to pptx**.

## Что изучать дальше?

Следующие учебники охватывают тесно связанные темы, расширяющие техники, продемонстрированные в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, помогая вам освоить дополнительные возможности API и исследовать альтернативные подходы в собственных проектах.

- [Как установить область печати в Excel с помощью Aspose.Cells for .NET](/cells/english/net/headers-footers/set-print-area-excel-aspose-cells-net/)
- [Установка области печати в Excel и экспорт в PowerPoint – пошаговое руководство](/cells/english/net/converting-excel-files-to-other-formats/set-print-area-in-excel-and-export-to-powerpoint-step-by-ste/)
- [Set Print Area Excel Aspose Cells Net](/cells/german/net/headers-footers/set-print-area-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}