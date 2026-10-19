---
category: general
date: 2026-08-04
description: Экспортируйте диаграмму Excel в PowerPoint с помощью Aspose.Cells на
  C#. Следуйте пошаговому руководству по конвертации Excel в PowerPoint и сохраняйте
  редактируемость фигур.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel chart to powerpoint
- Aspose.Cells PPTX export
- editable shapes in PowerPoint
- Excel to PowerPoint conversion
- C# chart export
language: ru
lastmod: 2026-08-04
og_description: Экспортируйте диаграмму Excel в PowerPoint с помощью Aspose.Cells
  на C#. Узнайте, как создать редактируемый PPTX, сохранить данные диаграммы и автоматизировать
  преобразование из Excel в PowerPoint.
og_image_alt: Screenshot of an Excel chart rendered as an editable PowerPoint slide
og_title: Экспорт диаграммы Excel в PowerPoint с помощью C# – полный учебник Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Export Excel chart to PowerPoint using Aspose.Cells in C#. Follow this
    step‑by‑step Excel to PowerPoint conversion guide and keep shapes editable.
  headline: Export Excel chart to PowerPoint with C# – complete Aspose.Cells guide
  type: TechArticle
- description: Export Excel chart to PowerPoint using Aspose.Cells in C#. Follow this
    step‑by‑step Excel to PowerPoint conversion guide and keep shapes editable.
  name: Export Excel chart to PowerPoint with C# – complete Aspose.Cells guide
  steps:
  - name: Expected output
    text: '| File name | Content on slide | |--------------------------|------------------------------------------|
      | `ShapesExport.pptx` | The chart from `Shapes.xlsx` rendered as an editable
      PowerPoint chart, with axis labels, legends, and data series intact. |'
  - name: Exporting multiple worksheets
    text: If you need a slide for each worksheet, loop through `workbook.Worksheets`
      and call `Save` with a unique file name for each iteration.
  - name: Controlling slide layout
    text: Aspose.Slides lets you add a custom slide layout after the export. Create
      a new presentation, import the generated slide, and then apply a master theme.
  - name: Handling charts with external data sources
    text: If a chart references a data range outside the defined print area, extend
      the `PrintArea` to include those cells. Otherwise the chart may lose data series
      during export.
  - name: Licensing considerations
    text: 'Aspose libraries work in evaluation mode with a watermark. To remove the
      watermark, set the license before any API call:'
  type: HowTo
tags:
- Aspose.Cells
- C#
- PowerPoint
title: Экспорт диаграммы Excel в PowerPoint с помощью C# – полное руководство по Aspose.Cells
url: /ru/net/chart-rendering-and-conversion/export-excel-chart-to-powerpoint-with-c-complete-aspose-cell/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Экспорт диаграммы Excel в PowerPoint с помощью C# – полное руководство по Aspose.Cells

Если вам нужно **export Excel chart to PowerPoint**, этот учебник покажет, как сделать это с помощью Aspose.Cells и Aspose.Slides в C#. Вы получите полностью редактируемый PPTX, который сохраняет данные и формы диаграммы, делая конвертацию готовой к дальнейшей работе над дизайном.

Экспорт диаграмм из Excel в PowerPoint является распространенной задачей при построении автоматизированных конвейеров отчетности, презентаций продаж или учебных материалов. В этом руководстве вы узнаете точные шаги для выполнения **Excel to PowerPoint conversion**, при которой все элементы диаграммы остаются редактируемыми. Ручное копирование‑вставка не требуется, а код работает с .NET 6+ и классическим .NET Framework.

## Требования

- Действительная лицензия Aspose.Cells (или бесплатный оценочный ключ)  
- Aspose.Slides for .NET, добавленный в проект (библиотека обрабатывает вывод PPTX)  
- Установлен .NET 6 SDK или более поздняя версия  
- Excel‑книга, содержащая хотя бы одну диаграмму (в этом примере используется `Shapes.xlsx`)  

Вы можете установить пакеты NuGet с помощью следующих команд:

```bash
dotnet add package Aspose.Cells
dotnet add package Aspose.Slides
```

## Шаг 1: Загрузка Excel‑книги

Первой операцией является открытие книги, содержащей диаграмму, которую вы хотите экспортировать. Класс `Workbook` представляет весь файл Excel.

```csharp
using Aspose.Cells;
using Aspose.Slides;   // required for PPTX output

// Load the Excel workbook from disk
Workbook workbook = new Workbook("YOUR_DIRECTORY/Shapes.xlsx");
```

**Почему это важно:** Загрузка книги дает вам доступ к её листам, диаграммам и форматированию. Aspose.Cells читает файл без необходимости установки Microsoft Office, что делает решение легковесным и удобным для серверов.

## Шаг 2: Выбор листа и определение области печати

Лист может содержать множество диаграмм, но обычно экспортируется конкретный регион. Установка `PrintArea` сообщает Aspose.Cells, какие ячейки (включая диаграммы) следует отобразить.

```csharp
// Choose the first worksheet (index 0)
Worksheet worksheet = workbook.Worksheets[0];

// Define the area that contains the chart and any supporting data
worksheet.PageSetup.PrintArea = "A1:G30";
```

**Почему это важно:** Ограничивая экспорт определённой областью печати, вы избегаете лишних пустых слайдов и сохраняете небольшой размер файла PPTX. Область можно настроить, чтобы она точно соответствовала диапазону вашей диаграммы.

## Шаг 3: Настройка параметров экспорта для редактируемого PPTX

Aspose.Cells использует класс `ImageOrPrintOptions` для управления форматом вывода и редактируемостью. Установка `ImageFormat` в `ImageFormat.Pptx` создаёт файл PowerPoint, а `ExportEditableShapes = true` сохраняет объекты диаграммы как редактируемые формы.

```csharp
ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
{
    ImageFormat = ImageFormat.Pptx,   // Target format
    ExportEditableShapes = true       // Keep shapes/textboxes editable
};

// Attach the options to the worksheet's print settings
worksheet.PageSetup.PrintOptions = exportOptions;
```

**Почему это важно:** Флаг `ExportEditableShapes` является ключом к результату **editable shapes in PowerPoint**. Без него диаграмма будет растеризована как изображение, и вы потеряете возможность позже изменять точки данных или стиль.

## Шаг 4: Сохранение листа как презентации PowerPoint

Наконец, вызовите метод `Save` у объекта `Workbook`. Перечисление `SaveFormat.Pptx` указывает Aspose.Cells создать файл PowerPoint.

```csharp
// Export the selected worksheet to a PPTX file
workbook.Save("YOUR_DIRECTORY/ShapesExport.pptx", SaveFormat.Pptx);
```

Когда код завершится, откройте `ShapesExport.pptx` в PowerPoint. Вы увидите слайд, содержащий оригинальную диаграмму Excel как нативный объект диаграммы PowerPoint. Дважды щёлкните по диаграмме, чтобы редактировать данные, менять цвета или добавлять анимацию — так же, как если бы вы создали диаграмму непосредственно в PowerPoint.

### Ожидаемый результат

| Имя файла                | Содержимое на слайде                         |
|--------------------------|----------------------------------------------|
| `ShapesExport.pptx`      | Диаграмма из `Shapes.xlsx`, отрисованная как редактируемая диаграмма PowerPoint, с сохранёнными подписями осей, легендами и рядами данных. |

## Полный, исполняемый пример

Ниже приведена полная программа, которую вы можете скопировать, вставить и запустить. Она включает все необходимые директивы `using`, обработку ошибок и комментарии.

```csharp
using System;
using Aspose.Cells;
using Aspose.Slides;   // Required for PPTX output

class ExcelToPowerPoint
{
    static void Main()
    {
        // Path to the source Excel file – adjust as needed
        const string excelPath = "YOUR_DIRECTORY/Shapes.xlsx";
        // Path for the generated PowerPoint file
        const string pptxPath = "YOUR_DIRECTORY/ShapesExport.pptx";

        try
        {
            // Load the workbook
            Workbook workbook = new Workbook(excelPath);

            // Use the first worksheet (you can change the index or name)
            Worksheet worksheet = workbook.Worksheets[0];

            // Define the area that contains the chart
            worksheet.PageSetup.PrintArea = "A1:G30";

            // Set export options for PPTX with editable shapes
            ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
            {
                ImageFormat = ImageFormat.Pptx,
                ExportEditableShapes = true
            };
            worksheet.PageSetup.PrintOptions = exportOptions;

            // Save as PPTX
            workbook.Save(pptxPath, SaveFormat.Pptx);

            Console.WriteLine($"Export successful. PPTX saved to: {pptxPath}");
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error during export: {ex.Message}");
        }
    }
}
```

**Объяснение каждого блока**

| Block | Purpose |
|-------|---------|
| `using` directives | Подключает пространства имён Aspose.Cells и Aspose.Slides. |
| `Workbook workbook = new Workbook(excelPath);` | Загружает файл Excel без необходимости установки Office. |
| `worksheet.PageSetup.PrintArea = "A1:G30";` | Ограничивает экспорт регионом, содержащим диаграмму. |
| `ImageOrPrintOptions` | Настраивает вывод PPTX и включает **Aspose.Cells PPTX export** с редактируемыми формами. |
| `workbook.Save(pptxPath, SaveFormat.Pptx);` | Записывает файл PowerPoint на диск. |
| `try / catch` | Обеспечивает базовую обработку ошибок для отсутствующих файлов или проблем с лицензией. |

Запуск этой программы создаёт слайд PowerPoint, который вы можете открыть в Microsoft PowerPoint, Google Slides (после конвертации) или любом совместимом просмотрщике.

## Общие варианты и граничные случаи

### Экспорт нескольких листов

Если вам нужен слайд для каждого листа, пройдитесь в цикле по `workbook.Worksheets` и вызовите `Save` с уникальным именем файла для каждой итерации.

```csharp
int index = 1;
foreach (Worksheet ws in workbook.Worksheets)
{
    ws.PageSetup.PrintOptions = exportOptions;
    string fileName = $"Slide{index++}.pptx";
    workbook.Save(fileName, SaveFormat.Pptx);
}
```

### Управление макетом слайда

Aspose.Slides позволяет добавить пользовательский макет слайда после экспорта. Создайте новую презентацию, импортируйте сгенерированный слайд и затем примените мастер‑тему.

```csharp
using Aspose.Slides.Export;

// Load the PPTX created by Aspose.Cells
Presentation pres = new Presentation(pptxPath);

// Apply a built‑in layout (e.g., Title and Content)
pres.Slides[0].LayoutSlide = pres.LayoutSlides[(int)SlideLayoutType.TitleAndContent];

// Save the final presentation
pres.Save("FinalPresentation.pptx", SaveFormat.Pptx);
```

### Обработка диаграмм с внешними источниками данных

Если диаграмма ссылается на диапазон данных за пределами определённой области печати, расширьте `PrintArea`, чтобы включить эти ячейки. В противном случае диаграмма может потерять серии данных при экспорте.

### Вопросы лицензирования

Библиотеки Aspose работают в режиме оценки с водяным знаком. Чтобы удалить водяной знак, установите лицензию перед любым вызовом API:

```csharp
var license = new Aspose.Cells.License();
license.SetLicense("Aspose.Cells.lic");
```

Сделайте то же самое для Aspose.Slides, если используете его расширенные возможности.

## Профессиональные советы

- **Reuse export options:** Создайте один экземпляр `ImageOrPrintOptions` и назначьте его каждому листу, чтобы код оставался DRY.  
- **Batch processing:** Для масштабной отчётности объедините эту логику экспорта с фоновым воркером или Azure Function, чтобы генерировать файлы PPTX по запросу.  
- **Performance:** Если вам нужен только образ диаграммы (не редактируемый), установите `ExportEditableShapes = false`. Это уменьшит использование памяти и ускорит конвертацию.  
- **Testing:** Проверьте сгенерированный PPTX как в Windows, так и в macOS PowerPoint, поскольку некоторые особенности рендеринга различаются между платформами.  

## Заключение

Теперь у вас есть полное решение от начала до конца для **export Excel chart to PowerPoint** с использованием C#. В учебнике рассмотрены загрузка книги, выбор области печати, настройка **Aspose.Cells PPTX export** с **editable shapes in PowerPoint**, и сохранение результата как полностью редактируемого файла PPTX.  

Отсюда вы можете исследовать дополнительные сценарии **Excel to PowerPoint conversion**, такие как пакетный экспорт, пользовательские макеты слайдов или интеграцию процесса в веб‑API. Экспериментируйте с различными типами диаграмм, добавляйте изображения или объединяйте несколько листов в одну презентацию, чтобы адаптировать вывод к потребностям вашего бизнеса.  

Готовы автоматизировать ваш процесс отчётности? Попробуйте заменить исходный файл, скорректировать область печати и интегрировать код в ваши существующие сервисы .NET. Приятного кодинга!

## Что следует изучить дальше?

Следующие учебники охватывают тесно связанные темы, построенные на техниках, продемонстрированных в этом руководстве. Каждый ресурс включает полностью рабочие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и изучить альтернативные подходы к реализации в ваших проектах.

- [How to Convert Excel to PowerPoint Using Aspose.Cells for .NET: A Complete Guide](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [How to Export Excel Charts to PDF Using Aspose.Cells for .NET: A Step-by-Step Guide](/cells/english/net/workbook-operations/export-excel-charts-pdf-aspose-cells-net/)
- [Export Excel Cells to Image Using Aspose.Cells .NET: A Step-by-Step Guide](/cells/english/net/import-export/export-excel-cells-to-image-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}