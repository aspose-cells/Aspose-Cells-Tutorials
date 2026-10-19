---
category: general
date: 2026-10-10
description: Быстро конвертировать Excel в PNG с помощью Aspose.Cells на C#. Узнайте,
  как экспортировать диапазон Excel, сохранить файл Excel как PNG и преобразовать
  лист в изображение за несколько минут.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert excel to png
- export excel range
- save excel as png
- how to export excel
- convert worksheet to image
language: ru
lastmod: 2026-10-10
og_description: Конвертировать Excel в PNG мгновенно с помощью Aspose.Cells. Этот
  учебник показывает, как экспортировать диапазон Excel, сохранить Excel как PNG и
  преобразовать лист в изображение.
og_image_alt: Screenshot of C# code that converts an Excel worksheet to a PNG image
og_title: Конвертировать Excel в PNG с помощью C# – полное руководство по программированию
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: convert excel to png quickly using Aspose.Cells in C#. Learn to export
    excel range, save excel as png, and convert worksheet to image in minutes.
  headline: How to convert Excel to PNG with C# – step‑by‑step guide
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
- Image export
- Automation
title: Как конвертировать Excel в PNG с помощью C# – пошаговое руководство
url: /ru/net/converting-excel-files-to-other-formats/how-to-convert-excel-to-png-with-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как конвертировать Excel в PNG с помощью C# – пошаговое руководство

Если вам необходимо **конвертировать Excel в PNG** программно, это руководство покажет, как сделать это с помощью Aspose.Cells for .NET. Независимо от того, создаёте ли вы сервис отчётности или автоматизированную панель мониторинга, вы узнаете, как экспортировать диапазон Excel, сохранить результат в файл PNG и обработать типичные граничные случаи.

Вы пройдёте каждый необходимый шаг — от добавления пакета NuGet до рендеринга конкретной области листа — чтобы интегрировать решение в любой проект C# без поиска дополнительных ресурсов.

## Требования

Прежде чем начать, убедитесь, что у вас есть:

* .NET 6.0 SDK или новее (код также работает с .NET Framework 4.6+)
* Visual Studio 2022 (или любая IDE, поддерживающая C#)
* Действующая лицензия Aspose.Cells for .NET (бесплатная пробная версия подходит для оценки)
* Файл Excel с именем **Pivot.xlsx**, расположенный в папке, к которой вы можете обратиться (в руководстве используется `YOUR_DIRECTORY` как заполнитель)

> **Pro tip:** Установите пакет Aspose.Cells через консоль менеджера пакетов NuGet:  
> `Install-Package Aspose.Cells`

## Полный разбор кода для конвертации Excel в PNG

Ниже представлена полная программа, которая загружает книгу, настраивает параметры изображения и рендерит заданный диапазон ячеек в файл PNG. Все необходимые директивы `using` включены, поэтому вы можете скопировать код в новый консольный проект и сразу запустить его.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;
using System.Drawing.Imaging;

namespace ExcelToPngDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 1: Load the workbook (convert excel to png starts here)
            // -------------------------------------------------
            string workbookPath = @"YOUR_DIRECTORY\Pivot.xlsx";
            Workbook workbook = new Workbook(workbookPath);

            // -------------------------------------------------
            // Step 2: Configure image options (PNG format)
            // -------------------------------------------------
            ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
            {
                // Export format – PNG ensures lossless quality
                ImageFormat = ImageFormat.Png,

                // Optional: set resolution (default is 96 DPI)
                // HorizontalResolution = 150,
                // VerticalResolution = 150
            };

            // -------------------------------------------------
            // Step 3: Define the range you want to export
            // -------------------------------------------------
            // Example range A1:H30 – you can change this to any valid Excel range
            string range = "A1:H30";

            // -------------------------------------------------
            // Step 4: Render the range to an image file
            // -------------------------------------------------
            string outputPath = @"YOUR_DIRECTORY\Pivot.png";
            workbook.Worksheets[0].RenderRangeToImage(range, outputPath, imgOptions);

            Console.WriteLine($"Excel range {range} has been exported to PNG at: {outputPath}");
        }
    }
}
```

### Как работает код

* **Загрузка книги** — `Workbook` читает файл `.xlsx` в память, предоставляя доступ ко всем листам.
* **ImageOrPrintOptions** — Этот объект указывает Aspose.Cells генерировать PNG (`ImageFormat.Png`). При необходимости можно также задать DPI, масштабирование или цвет фона.
* **RenderRangeToImage** — Метод `RenderRangeToImage` принимает три аргумента: диапазон ячеек (`"A1:H30"`), путь к файлу назначения и параметры изображения. Это основная операция, которая **export excel range** в PNG‑изображение.
* **Результат** — После выполнения вы найдёте `Pivot.png` в указанной папке, содержащий точную визуальную репрезентацию выбранных ячеек.

## Экспорт диапазона Excel в PNG — кастомизация вывода

Если нужно **export excel range** отличный от `A1:H30`, просто измените переменную `range`. Метод принимает любой адрес в стиле Excel, включая именованные диапазоны:

```csharp
// Export a named range called "ReportArea"
string range = "ReportArea";
```

Вы также можете экспортировать весь лист, используя `"A1:Z1000"` (или более длинный адрес) или вызвав `RenderToImage` без параметра диапазона.

## Сохранение Excel как PNG с дополнительными настройками

Иногда требуется, чтобы PNG соответствовал определённому разрешению для печати или веб‑использования. Настройте `ImageOrPrintOptions` следующим образом:

```csharp
ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
{
    ImageFormat = ImageFormat.Png,
    HorizontalResolution = 300,   // 300 DPI for high‑quality print
    VerticalResolution = 300,
    Transparent = true           // Makes the background transparent
};
```

Эти параметры демонстрируют, как **save excel as png** с пользовательским DPI и прозрачностью, предоставляя полный контроль над качеством конечного изображения.

## Как экспортировать Excel — обработка нескольких листов

Пример ориентирован на первый лист (`Worksheets[0]`). Чтобы **convert worksheet to image** для другого листа, укажите его по индексу или имени:

```csharp
// By index (second sheet)
Worksheet sheet = workbook.Worksheets[1];

// By name
Worksheet sheet = workbook.Worksheets["DataSheet"];
sheet.RenderRangeToImage(range, outputPath, imgOptions);
```

Обработка каждого листа в цикле проста:

```csharp
for (int i = 0; i < workbook.Worksheets.Count; i++)
{
    string sheetPath = $@"YOUR_DIRECTORY\Sheet{i + 1}.png";
    workbook.Worksheets[i].RenderRangeToImage(range, sheetPath, imgOptions);
    Console.WriteLine($"Sheet {i + 1} exported to {sheetPath}");
}
```

## Граничные случаи и устранение неполадок

| Ситуация | Рекомендуемый подход |
|-----------|----------------------|
| **Очень большой диапазон** (например, весь рабочий лист) | Пошагово увеличивайте `HorizontalResolution`/`VerticalResolution`, чтобы избежать `OutOfMemoryException`. Рассмотрите возможность экспорта каждого листа отдельно. |
| **Объединённые ячейки** | Aspose.Cells автоматически сохраняет визуальное отображение объединённых ячеек, но проверьте результат, если вам важна точная ширина столбцов. |
| **Формулы, ссылающиеся на внешние файлы** | Убедитесь, что эти файлы доступны до загрузки книги; иначе отрендеренное изображение может содержать устаревшие значения. |
| **Отсутствующая лицензия** | Пробная версия добавляет водяной знак. Примените действующую лицензию (`License license = new License(); license.SetLicense("Aspose.Cells.lic");`) перед рендерингом, чтобы получить чистый PNG. |

## Полный рабочий пример

Ниже представлена автономная программа, которую можно собрать и запустить. Замените `YOUR_DIRECTORY` реальным путём к папке на вашем компьютере.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;
using System.Drawing.Imaging;

namespace ExcelToPngDemo
{
    class Program
    {
        static void Main()
        {
            // Load workbook
            var workbook = new Workbook(@"C:\Temp\Pivot.xlsx");

            // Set PNG options
            var options = new ImageOrPrintOptions
            {
                ImageFormat = ImageFormat.Png,
                HorizontalResolution = 150,
                VerticalResolution = 150
            };

            // Define range and output file
            string range = "A1:H30";
            string output = @"C:\Temp\Pivot.png";

            // Export the range as a PNG image
            workbook.Worksheets[0].RenderRangeToImage(range, output, options);

            Console.WriteLine($"Successfully converted Excel to PNG: {output}");
        }
    }
}
```

**Ожидаемый вывод**

```
Successfully converted Excel to PNG: C:\Temp\Pivot.png
```

Откройте `Pivot.png` в любом просмотрщике изображений — вы увидите точную визуальную раскладку ячеек A1 по H30, включая форматирование, цвета и границы.

## Заключение

Теперь у вас есть надёжный способ **convert Excel to PNG** с помощью C#. В руководстве рассмотрены способы **export excel range**, **save excel as png** и **convert worksheet to image** с настраиваемыми параметрами и рекомендациями по лучшим практикам.  

Дальше вы можете:

* Интегрировать код в веб‑API для генерации изображений по запросу.  
* Комбинировать вывод PNG с генерацией PDF для многоформатных отчётов.  
* Исследовать другие форматы изображений (`ImageFormat.Jpeg`, `ImageFormat.Bmp`), изменив свойство `ImageFormat`.

Экспериментируйте с различными диапазонами, разрешениями и выбором листов, чтобы адаптировать решение под ваш сценарий автоматизации.

---


## Что изучать дальше?


В следующих руководствах рассматриваются тесно связанные темы, расширяющие техники, продемонстрированные в этом пособии. Каждый ресурс содержит полностью рабочие примеры кода с пошаговыми объяснениями, помогающие освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [Как экспортировать лист Excel в PNG с помощью Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-to-png-aspose-cells-java/)
- [Конвертация Excel в PNG, TIFF и PDF в Java с использованием Aspose.Cells](/cells/english/java/workbook-operations/render-excel-as-png-tiff-pdf-aspose-cells-java/)
- [Мастерство Aspose.Cells Java: конвертация Excel в PNG с пользовательским поставщиком потоков](/cells/english/java/advanced-features/aspose-cells-java-custom-stream-provider/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}