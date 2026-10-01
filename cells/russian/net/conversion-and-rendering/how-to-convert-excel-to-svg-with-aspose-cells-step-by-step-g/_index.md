---
category: general
date: 2026-10-01
description: Узнайте, как преобразовать Excel в SVG и сохранить файл Excel в формате
  SVG с помощью Aspose.Cells. Следуйте этому полному руководству, чтобы экспортировать
  листы Excel в виде SVG‑изображений.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert excel to svg
- save excel file as svg
- how to export excel to svg
- export excel worksheet as svg
language: ru
lastmod: 2026-10-01
og_description: Преобразуйте Excel в SVG с помощью Aspose.Cells. Этот учебник объясняет,
  как экспортировать листы Excel в виде SVG‑изображений, охватывая настройку, код
  и особые случаи.
og_image_alt: Diagram illustrating the convert excel to svg workflow
og_title: Конвертировать Excel в SVG с помощью Aspose.Cells – полное руководство по
  программированию
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Learn how to convert Excel to SVG and save Excel file as SVG using
    Aspose.Cells. Follow this complete tutorial to export Excel worksheets as SVG
    images.
  headline: How to convert Excel to SVG with Aspose.Cells – step‑by‑step guide
  type: TechArticle
- description: Learn how to convert Excel to SVG and save Excel file as SVG using
    Aspose.Cells. Follow this complete tutorial to export Excel worksheets as SVG
    images.
  name: How to convert Excel to SVG with Aspose.Cells – step‑by‑step guide
  steps:
  - name: Exporting multiple worksheets at once
    text: 'When a workbook contains several sheets, you can let Aspose.Cells generate
      a separate SVG for each sheet automatically:'
  - name: Controlling SVG dimensions
    text: 'SVG files are vector‑based, but you can still influence the viewport size:'
  - name: Handling formulas and calculated values
    text: 'By default, Aspose.Cells evaluates formulas before rendering. If you want
      to export raw formulas as text, set:'
  - name: Performance tips
    text: '- **Reuse `ImageOrPrintOptions`**: Create the options once and reuse them
      for multiple workbooks to avoid unnecessary allocations. - **Stream output**:
      If you are building a web API, write the SVG directly to a `MemoryStream` and
      return it as a file result instead of saving to disk.'
  type: HowTo
tags:
- Aspose.Cells
- C#
- SVG export
title: Как конвертировать Excel в SVG с помощью Aspose.Cells – пошаговое руководство
url: /ru/net/conversion-and-rendering/how-to-convert-excel-to-svg-with-aspose-cells-step-by-step-g/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как конвертировать Excel в SVG с помощью Aspose.Cells – пошаговое руководство

Если вам нужно **convert Excel to SVG**, это руководство покажет, как экспортировать лист Excel в виде изображения SVG с помощью Aspose.Cells. Вы увидите полностью рабочий пример, который сохраняет файл Excel как SVG, и узнаете, почему важна каждая настройка.

Экспорт таблиц в виде масштабируемой векторной графики полезен, когда требуется чёткое отображение на веб‑страницах, в отчётах или документации без потери качества. Ниже представлены все шаги от установки библиотеки до работы с несколькими листами и типичными подводными камнями.

## Требования

Перед началом убедитесь, что у вас есть:

- .NET 6.0 или новее (код также работает с .NET Framework 4.7.2+)
- Действительная лицензия Aspose.Cells или бесплатный ключ оценки
- Файл Excel (`input.xlsx`), который нужно конвертировать
- Visual Studio 2022 или любой другой редактор C# по вашему выбору

Дополнительные пакеты NuGet не требуются, кроме `Aspose.Cells`.

## Шаг 1: Установить Aspose.Cells

Стандартный способ – добавить пакет Aspose.Cells через NuGet. Откройте терминал в папке проекта и выполните:

```bash
dotnet add package Aspose.Cells --version 24.10
```

Эта команда загружает последнюю стабильную версию (24.10 на момент написания) и обновляет ваш файл проекта. Использование последней версии гарантирует совместимость с новейшими функциями Excel и улучшениями SVG.

## Шаг 2: Загрузить книгу Excel

Загрузка книги – первая конкретная операция в конвейере **convert excel to svg**. Класс `Workbook` представляет весь файл Excel и даёт доступ к листам, формулам и форматированию.

```csharp
using Aspose.Cells;
using Aspose.Cells.Rendering;

// Load the source workbook
var workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");

// Optional: verify that the workbook loaded correctly
Console.WriteLine($"Loaded workbook with {workbook.Worksheets.Count} worksheet(s).");
```

**Почему это важно:**  
Если файл не может быть открыт (например, неверный путь или неподдерживаемый формат), Aspose.Cells бросает информативное исключение, которое можно перехватить и записать в лог. Раннее проверка количества листов помогает решить, экспортировать один лист или всю книгу целиком.

## Шаг 3: Настроить параметры рендеринга SVG

Чтобы **save excel file as svg**, необходимо создать экземпляр `ImageOrPrintOptions` и установить его `SaveFormat` в `SaveFormat.Svg`. Также можно тонко настроить качество изображения, масштаб и встраивание шрифтов.

```csharp
// Set up rendering options for SVG output
var imageOptions = new ImageOrPrintOptions
{
    // Export format must be SVG
    SaveFormat = SaveFormat.Svg,

    // Preserve the original aspect ratio
    OnePagePerSheet = true,

    // Optional: increase resolution for sharper vectors
    // (SVG is resolution‑independent, but this affects rasterized elements)
    HorizontalResolution = 300,
    VerticalResolution = 300
};
```

**Объяснение:**  
`OnePagePerSheet = true` заставляет каждый лист помещаться на одну страницу SVG, что обычно требуется для веб‑встраивания. Изменение разрешения влияет на то, как встроенные растровые изображения (например, картинки в ячейках) отображаются внутри SVG.

## Шаг 4: Сохранить книгу как изображение SVG

Теперь вы можете **export excel worksheet as svg**, вызвав `Workbook.Save` с целевым путём и только что настроенными параметрами.

```csharp
// Define the output path
string outputPath = @"YOUR_DIRECTORY\output.svg";

// Save the workbook (or a specific worksheet) as SVG
workbook.Save(outputPath, imageOptions);

Console.WriteLine($"Workbook exported to SVG at: {outputPath}");
```

Если нужно экспортировать только один лист, а не всю книгу, получите лист и используйте `SheetRender`:

```csharp
// Export only the first worksheet
var sheet = workbook.Worksheets[0];
var sheetRender = new SheetRender(sheet, imageOptions);
sheetRender.ToImage(0, outputPath); // 0 = first page
```

**Почему это работает:**  
`Workbook.Save` перебирает все листы, когда `OnePagePerSheet` включён, генерируя отдельный SVG‑файл для каждого листа, если путь вывода содержит плейсхолдер (например, `output_{0}.svg`). Использование `SheetRender` даёт точный контроль над тем, какие листы экспортировать.

## Шаг 5: Проверить результат SVG

После завершения конвертации откройте полученный файл `.svg` в браузере или SVG‑редакторе (например, Inkscape). Вы должны увидеть текст, границы ячеек и любые встроенные изображения в виде масштабируемых векторов.

```bash
# On macOS or Linux you can open the file directly:
open YOUR_DIRECTORY/output.svg
```

Если SVG выглядит пустым или без форматирования, проверьте следующее:

1. Книга действительно содержит данные в целевом листе.  
2. Скрытые строки/столбцы не маскируют содержимое (используйте `sheet.IsVisible`).  
3. Шрифты, используемые в книге, установлены на машине; иначе Aspose.Cells заменит их, что может изменить внешний вид.

## Расширенные соображения

### Экспорт нескольких листов одновременно

Когда книга содержит несколько листов, можно позволить Aspose.Cells автоматически генерировать отдельный SVG для каждого листа:

```csharp
// Use a placeholder {0} for sheet index
string multiOutput = @"YOUR_DIRECTORY\output_{0}.svg";
workbook.Save(multiOutput, imageOptions);
```

Библиотека заменяет `{0}` индексом листа (начиная с 0). Это удобно для пакетной обработки больших отчётов.

### Управление размерами SVG

Файлы SVG векторные, но вы всё равно можете влиять на размер области просмотра:

```csharp
imageOptions.PageWidth = 800;   // width in pixels (converted to SVG points)
imageOptions.PageHeight = 600;  // height in pixels
```

Указание явных размеров обеспечивает согласованную раскладку при встраивании SVG в HTML‑контейнеры.

### Обработка формул и вычисленных значений

По умолчанию Aspose.Cells вычисляет формулы перед рендерингом. Если нужно экспортировать сырые формулы как текст, установите:

```csharp
imageOptions.ExportFormulasAsString = true;
```

Эта опция полезна для документации, где необходимо показать фактическую формулу Excel, а не её вычисленный результат.

### Советы по производительности

- **Reuse `ImageOrPrintOptions`**: Создайте параметры один раз и переиспользуйте их для нескольких книг, чтобы избежать лишних выделений памяти.  
- **Stream output**: Если вы создаёте веб‑API, запишите SVG напрямую в `MemoryStream` и верните его как файл, вместо сохранения на диск.

```csharp
using (var stream = new MemoryStream())
{
    workbook.Save(stream, imageOptions);
    // Reset position before reading
    stream.Position = 0;
    // Return stream to caller (e.g., ASP.NET Core FileResult)
}
```

## Распространённые проблемы и как их избежать

| Симптом | Причина | Решение |
|--------|---------|---------|
| Пустой SVG‑файл | В книге скрыты строки/столбцы или лист имеет нулевой размер | Отобразите строки/столбцы или установите `sheet.IsVisible = true` |
| Отсутствие шрифтов | Шрифт не установлен на сервере | Установите требуемый шрифт или встроите его с помощью `imageOptions.EmbeddedFonts = true` |
| Несколько SVG‑файлов с неожиданными именами | В пути вывода нет плейсхолдера `{0}` | Используйте `output_{0}.svg` для генерации файлов по листам |
| Медленная конвертация больших книг | Рендеринг каждого листа отдельно без `OnePagePerSheet` | Включите `OnePagePerSheet` или обрабатывайте листы параллельно с `Task.Run` |

## Полный, готовый к запуску пример

Ниже представлено автономное консольное приложение, демонстрирующее **how to export Excel to SVG** от начала до конца. Замените `YOUR_DIRECTORY` реальной папкой на вашем компьютере.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;

namespace ExcelToSvgDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the workbook
            var workbookPath = @"YOUR_DIRECTORY\input.xlsx";
            var workbook = new Workbook(workbookPath);
            Console.WriteLine($"Loaded {workbook.Worksheets.Count} worksheet(s).");

            // 2️⃣ Configure SVG options
            var svgOptions = new ImageOrPrintOptions
            {
                SaveFormat = SaveFormat.Svg,
                OnePagePerSheet = true,
                HorizontalResolution = 300,
                VerticalResolution = 300,
                // Optional: set explicit dimensions
                // PageWidth = 800,
                // PageHeight = 600
            };

            // 3️⃣ Export each sheet as a separate SVG file
            string outputPattern = @"YOUR_DIRECTORY\output_{0}.svg";
            workbook.Save(outputPattern, svgOptions);
            Console.WriteLine("Export completed. SVG files created:");

            for (int i = 0; i < workbook.Worksheets.Count; i++)
            {
                Console.WriteLine($"\t{string.Format(outputPattern, i)}");
            }
        }
    }
}
```

**Ожидаемый вывод** (консоль):

```
Loaded 2 worksheet(s).
Export completed. SVG files created:
    YOUR_DIRECTORY\output_0.svg
    YOUR_DIRECTORY\output_1.svg
```

Откройте любой из сгенерированных файлов `.svg` в браузере, чтобы убедиться, что конвертация прошла успешно.

## Заключение

Теперь вы знаете, как **convert Excel to SVG** с помощью Aspose.Cells, от установки библиотеки до работы с несколькими листами и тонкой настройки параметров рендеринга. В руководстве рассмотрен полный процесс **save excel file as svg**, объяснено, почему важна каждая настройка, и выделены особые случаи, такие как скрытые строки, встраивание шрифтов и вопросы производительности.

Далее вы можете изучить:

- **How to export Excel to SVG** в веб‑API (стриминг SVG напрямую клиенту)  
- Конвертацию Excel в другие векторные форматы, такие как PDF или EMF  
- Использование Aspose.Slides для встраивания сгенерированного SVG в презентации PowerPoint  

Не стесняйтесь экспериментировать с масштабированием, пользовательскими стилями или комбинировать вывод SVG с HTML/CSS для интерактивных отчётов. Приятного кодинга!

## Что вам стоит изучить дальше?

Следующие руководства охватывают тесно связанные темы, построенные на техниках, продемонстрированных в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, помогающими освоить дополнительные возможности API и исследовать альтернативные подходы в ваших проектах.

- [Конвертировать листы Excel в SVG с помощью Aspose.Cells Java: Полное руководство](/cells/english/java/workbook-operations/convert-excel-to-svg-aspose-cells-java/)
- [Конвертировать Excel в SVG с помощью Aspose.Cells для .NET: Пошаговое руководство](/cells/english/net/workbook-operations/convert-excel-to-svg-aspose-cells-net/)
- [Как конвертировать диаграммы Excel в SVG с помощью Aspose.Cells в Java](/cells/english/java/charts-graphs/convert-excel-charts-svg-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}