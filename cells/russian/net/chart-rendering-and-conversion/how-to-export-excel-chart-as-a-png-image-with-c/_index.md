---
category: general
date: 2026-11-19
description: Как экспортировать диаграмму Excel в виде PNG‑изображения с помощью Aspose.Cells.
  Узнайте, как сохранить изображение диаграммы Excel и установить формат PNG всего
  за несколько шагов.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to export excel chart
- save excel chart image
- set image format png
- save excel picture file
language: ru
lastmod: 2026-11-19
og_description: Как экспортировать диаграмму Excel в PNG‑изображение с помощью Aspose.Cells.
  Следуйте этому пошаговому руководству, чтобы сохранить изображение диаграммы Excel
  и эффективно установить формат PNG.
og_image_alt: How to export Excel chart as a PNG image
og_title: Как экспортировать график Excel в PNG‑изображение – быстрый гид по C#
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: How to export Excel chart as a PNG image using Aspose.Cells. Learn
    to save Excel chart image and set image format PNG in just a few steps.
  headline: How to export Excel chart as a PNG image with C#
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
- Chart export
title: Как экспортировать диаграмму Excel в PNG‑изображение с помощью C#
url: /ru/net/chart-rendering-and-conversion/how-to-export-excel-chart-as-a-png-image-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как экспортировать диаграмму Excel в PNG‑изображение с помощью C#

Если вам нужно **как экспортировать диаграмму Excel** в переносимый формат изображения, это руководство покажет готовое решение, готовое к запуску. С помощью Aspose.Cells вы можете **сохранить изображение диаграммы Excel** в формате PNG всего в три строки кода, а также в руководстве объясняется, как **установить формат изображения png** и **безопасно сохранить файл изображения Excel**.

В конце статьи вы получите исполняемую программу, которая загружает книгу, рендерит первую диаграмму и записывает файл `pivot.png` на диск. Никаких дополнительных инструментов, никаких ручных копирований — только чистый C#‑код, который можно вставить в любой проект .NET.

## Требования

Прежде чем начать, убедитесь, что у вас есть:

* .NET 6.0 SDK или новее (код также работает с .NET Framework 4.6+)
* Visual Studio 2022 или любой редактор C#
* Лицензия Aspose.Cells for .NET (или временный оценочный ключ)
* Файл Excel (`pivot.xlsx`), содержащий хотя бы одну диаграмму на первом листе

Эти элементы — единственные внешние зависимости; руководство не требует установки Office на машине.

## Шаг 1: Установить Aspose.Cells

Откройте терминал в папке проекта и выполните:

```bash
dotnet add package Aspose.Cells
```

Пакет добавляет пространство имён `Aspose.Cells`, которое предоставляет классы `Workbook`, `ImageOrPrintOptions` и другие, необходимые для **сохранения изображения диаграммы Excel**.

## Шаг 2: Создать минимальное консольное приложение

Создайте новое консольное приложение (`dotnet new console -n ExportChartDemo`) и замените автоматически сгенерированный `Program.cs` следующим кодом. Программа демонстрирует **как экспортировать диаграмму Excel** и содержит комментарии, поясняющие каждое решение.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;   // Required for ImageOrPrintOptions
using System.Drawing.Imaging;  // Provides ImageFormat enum

namespace ExportChartDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // 1️⃣ Load the workbook that contains the pivot chart
            // -----------------------------------------------------------------
            // Replace the path with the actual location of your Excel file.
            string workbookPath = @"YOUR_DIRECTORY\pivot.xlsx";
            Workbook workbook = new Workbook(workbookPath);

            // -----------------------------------------------------------------
            // 2️⃣ Set up image export options (PNG format)
            // -----------------------------------------------------------------
            // This is where we **set image format png** for the exported picture.
            ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
            {
                ImageFormat = ImageFormat.Png,
                // Optional: control the resolution (DPI) of the output image.
                // Higher DPI yields larger files but sharper charts.
                HorizontalResolution = 300,
                VerticalResolution = 300
            };

            // -----------------------------------------------------------------
            // 3️⃣ Render the first picture (the chart) on the first worksheet
            // -----------------------------------------------------------------
            // Aspose.Cells stores charts as Picture objects inside the worksheet.
            // The index [0] refers to the first chart; adjust if you have multiple.
            Worksheet sheet = workbook.Worksheets[0];
            if (sheet.Pictures.Count == 0)
            {
                Console.WriteLine("No pictures found on the first worksheet.");
                return;
            }

            // Render the picture to a PNG file.
            string outputPath = @"YOUR_DIRECTORY\pivot.png";
            sheet.Pictures[0].RenderToImage(imageOptions, outputPath);

            Console.WriteLine($"Chart exported successfully to: {outputPath}");
        }
    }
}
```

### Почему важна каждая часть

* **Загрузка книги** — `Workbook` разбирает файл `.xlsx` без необходимости установки Microsoft Excel.
* **ImageOrPrintOptions** — Этот объект управляет форматом вывода. Установка `ImageFormat = ImageFormat.Png` **устанавливает формат изображения png**, который является без потерь и широко поддерживается.
* **RenderToImage** — Метод `RenderToImage` преобразует диаграмму (объект `Picture`) в файл изображения. Метод также автоматически обрабатывает масштабирование, DPI и прозрачность.
* **Обработка ошибок** — Проверка `sheet.Pictures.Count == 0` предотвращает исключение во время выполнения, если на листе нет диаграмм, что часто происходит, когда пользователь указывает неверный лист.

## Шаг 3: Запустить программу и проверить результат

1. Соберите проект: `dotnet build`.
2. Запустите его: `dotnet run --project ExportChartDemo`.

Если всё настроено правильно, вы увидите:

```
Chart exported successfully to: YOUR_DIRECTORY\pivot.png
```

Откройте `pivot.png` в любой программе просмотра изображений. Вы должны увидеть точное визуальное представление диаграммы Excel, подтверждая, что вы успешно **сохранили файл изображения Excel**.

### Ожидаемый вывод

Ниже приведён пример того, как может выглядеть экспортированный PNG (конкретная диаграмма зависит от вашего исходного файла).

![Экспортированная диаграмма Excel, сохранённая как PNG‑изображение](images/exported-chart.png){: .center alt="Как экспортировать диаграмму Excel в PNG‑изображение"}

## Шаг 4: Расширенные параметры — экспорт нескольких диаграмм

Если в вашей книге более одной диаграммы, вы можете пройтись по коллекции `Pictures` в цикле:

```csharp
for (int i = 0; i < sheet.Pictures.Count; i++)
{
    string chartPath = $@"YOUR_DIRECTORY\chart_{i + 1}.png";
    sheet.Pictures[i].RenderToImage(imageOptions, chartPath);
    Console.WriteLine($"Chart {i + 1} saved to {chartPath}");
}
```

Этот шаблон позволяет **сохранить изображение диаграммы Excel** для каждой диаграммы на листе, что удобно для конвейеров отчётности.

## Распространённые проблемы и способы их избежать

| Симптом | Вероятная причина | Решение |
|---------|-------------------|---------|
| `ArgumentOutOfRangeException` на `Pictures[0]` | На листе нет диаграммы или диаграмма находится на другом листе. | Проверьте индекс листа (`Worksheets[0]`) и убедитесь, что диаграмма существует. При необходимости используйте `Worksheets["SheetName"]`. |
| Экспортированное изображение размыто | DPI установлен слишком низко (по умолчанию 96). | Увеличьте `HorizontalResolution` и `VerticalResolution` в `ImageOrPrintOptions`. |
| PNG‑файл пустой или повреждённый | Отсутствует лицензия, вызывающая ограничения оценки. | Примените действующую лицензию Aspose.Cells перед загрузкой книги (`License license = new License(); license.SetLicense("Aspose.Total.lic");`). |
| Ошибки пути к файлу (`FileNotFoundException`) | Неправильный заполнитель `YOUR_DIRECTORY`. | Используйте абсолютные пути или `Path.Combine(Environment.CurrentDirectory, "pivot.xlsx")`. |

Устранение этих проблем обеспечивает плавный опыт **сохранения файла изображения Excel**.

## Профессиональный совет: экспортировать напрямую в поток памяти

Иногда требуется получить изображение в памяти (например, для загрузки в веб‑API), а не записывать его на диск:

```csharp
using (var ms = new MemoryStream())
{
    sheet.Pictures[0].RenderToImage(imageOptions, ms);
    // ms now contains the PNG bytes – you can send them over HTTP, store in DB, etc.
}
```

Та же логика **установки формата изображения png** применяется; просто замените путь к файлу на поток.

## Заключение

Теперь вы знаете **как экспортировать диаграмму Excel** в PNG‑файл с помощью Aspose.Cells для .NET. В руководстве рассмотрено:

* Установка библиотеки
* Загрузка книги
* **Установка формата изображения png**
* **Сохранение изображения диаграммы Excel** на диск
* Обработка нескольких диаграмм и типичных ошибок

С этой базой вы можете интегрировать экспорт диаграмм в автоматизированные отчёты, веб‑службы или настольные утилиты. Далее изучайте связанные темы, такие как **сохранение файла изображения Excel** в JPEG (`ImageFormat.Jpeg`) или преобразование диаграмм в PDF для печатных отчётов.

Удачной разработки!


## Что изучать дальше?


В следующих руководствах рассматриваются тесно связанные темы, которые расширяют техники, продемонстрированные в этом руководстве. Каждый ресурс содержит полностью работающие примеры кода с пошаговыми объяснениями, помогающими освоить дополнительные возможности API и исследовать альтернативные подходы в ваших проектах.

- [Convert Excel Pie Chart to Image Using Aspose.Cells .NET&#58; A Step-by-Step Guide](/cells/english/net/charts-graphs/convert-excel-pie-chart-image-aspose-cells-net/)
- [Export Chart as PNG – Complete Guide to Convert Excel to HTML with Aspose.Cells](/cells/english/net/chart-rendering-and-conversion/export-chart-as-png-complete-guide-to-convert-excel-to-html/)
- [Export Excel Cells to Image Using Aspose.Cells .NET&#58; A Step-by-Step Guide](/cells/english/net/import-export/export-excel-cells-to-image-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}