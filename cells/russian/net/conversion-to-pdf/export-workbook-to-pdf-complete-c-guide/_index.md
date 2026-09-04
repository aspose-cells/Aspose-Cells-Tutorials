---
category: general
date: 2026-02-26
description: Экспортировать книгу в PDF с внедрёнными шрифтами и также экспортировать
  диаграммы в PowerPoint на C#. Узнайте, как скопировать лист со сводной таблицей
  и сохранить книгу в формате PPTX.
draft: false
keywords:
- export workbook to pdf
- export charts to powerpoint
- copy pivot table worksheet
- embed fonts pdf export
- save workbook as pptx
language: ru
og_description: Экспортировать книгу в PDF с внедрёнными шрифтами и также экспортировать
  диаграммы в PowerPoint на C#. Следуйте пошаговому руководству, чтобы скопировать
  сводные таблицы и сохранить в формате PPTX.
og_title: Экспорт рабочей книги в PDF — Полное руководство по C#
tags:
- Aspose.Cells
- Aspose.Slides
- C#
- Reporting
title: Экспорт рабочей книги в PDF – Полное руководство по C#
url: /ru/net/conversion-to-pdf/export-workbook-to-pdf-complete-c-guide/
---

inside triple backticks; they are just placeholders. Should we keep them as is? Yes.

Also ensure we keep any markdown formatting like **bold**, *italic*, etc.

Now produce final answer.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Экспорт книги Excel в PDF – Полное руководство на C#

Экспорт книги Excel в PDF — распространённая задача, когда необходимо делиться отчётами со стейкхолдерами, у которых может не быть установлен Excel. В этом руководстве мы также покажем, как **экспортировать диаграммы в PowerPoint**, скопировать **лист с сводной таблицей** и встроить шрифты, чтобы PDF выглядел точно так же, как ваш дизайн на экране.  

Когда‑то задумывались, почему некоторые PDF‑файлы теряют оригинальное расположение элементов или почему слайды PowerPoint оказываются без некоторых фигур? Ответ обычно кроется в отсутствии нужных параметров при экспорте. К концу этого руководства у вас будет один переиспользуемый метод на C#, который решает все эти проблемы — больше никаких ручных копирований и настройки параметров экспорта.

## Что вы узнаете

- Как создать книгу, добавить выражения Smart Marker и обработать их.  
- Как **скопировать лист со сводной таблицей** без нарушения источника данных.  
- Как **экспортировать диаграммы, фигуры и текстовые блоки** в презентацию PowerPoint, сохранив их редактируемыми.  
- Как **встроить стандартные шрифты** при экспорте в PDF для одинакового отображения на любой машине.  
- Как **сохранить книгу как PPTX** с помощью подхода `save workbook as pptx`.  

Всё это работает с последними версиями библиотек Aspose.Cells и Aspose.Slides .NET (версия 23.11 на момент написания). Никаких внешних инструментов, никаких пост‑обработок — только чистый C#.

> **Pro tip:** Если вы уже используете Aspose в своём проекте, можете просто вставить приведённые фрагменты кода; в противном случае сначала добавьте NuGet‑пакеты `Aspose.Cells` и `Aspose.Slides`.

## Требования

- .NET 6.0 или новее (код также работает на .NET Framework 4.7.2).  
- Visual Studio 2022 (или любая другая IDE).  
- Aspose.Cells .NET и Aspose.Slides .NET, установленные через NuGet.  
- Базовое знакомство с C# и концепциями Excel, такими как Smart Markers и PivotTables.

---

![Диаграмма экспорта книги Excel в PDF](export-workbook-to-pdf.png "Рабочий процесс экспорта книги Excel в PDF, показывающий выводы PDF и PPTX")

## Экспорт книги Excel в PDF – пошаговая реализация

Ниже приведён полностью готовый к запуску пример. Он создаёт книгу, вставляет выражения Smart Marker, обрабатывает их, копирует диапазон со сводной таблицей и, наконец, сохраняет как PDF, так и PowerPoint‑файл.

```csharp
using System;
using Aspose.Cells;
using Aspose.Slides.Export;

namespace ReportExportDemo
{
    class Program
    {
        static void Main()
        {
            // -------------------------------------------------
            // Step 1: Build the workbook and add Smart Markers
            // -------------------------------------------------
            var reportWorkbook = new Workbook();
            Worksheet dataSheet = reportWorkbook.Worksheets[0];

            // Header with a variable department name
            dataSheet.Cells["A1"].PutValue("Report for ${$dept=Department}");

            // Conditional text based on department
            dataSheet.Cells["A2"].PutValue("${if $dept == \"Sales\"}Sales Summary${else}Other Summary${/if}");

            // Table header for orders – this will be repeated for each order
            dataSheet.Cells["A5:D5"].PutValue("${Orders.Product}|${Orders.Quantity}|${Orders.Price}");

            // -------------------------------------------------
            // Step 2: Process Smart Markers and name the detail sheet
            // -------------------------------------------------
            reportWorkbook.SmartMarkerProcessor.Options.DetailSheetNewName = "Orders_${$dept}";
            reportWorkbook.SmartMarkerProcessor.Process();

            // -------------------------------------------------
            // Step 3: Copy the range that contains the pivot table
            // -------------------------------------------------
            // Assume the pivot table lives in A1:G30 on the original sheet
            Range sourceRange = dataSheet.Cells.CreateRange("A1", "G30");
            Worksheet copySheet = reportWorkbook.Worksheets.Add("Copy");
            sourceRange.Copy(copySheet.Cells["A1"]);   // Pivot table is duplicated intact

            // -------------------------------------------------
            // Step 4: Export to PowerPoint (keep charts, shapes, text boxes)
            // -------------------------------------------------
            var pptOptions = new PresentationOptions
            {
                ExportCharts = true,
                ExportShapes = true,
                ExportTextBoxes = true
            };
            string pptPath = @"C:\Temp\FinalPresentation.pptx";
            reportWorkbook.Save(pptPath, SaveFormat.Pptx, pptOptions);

            // -------------------------------------------------
            // Step 5: Export to PDF and embed standard fonts
            // -------------------------------------------------
            var pdfOptions = new PdfSaveOptions { EmbedStandardFonts = true };
            string pdfPath = @"C:\Temp\FinalReport.pdf";
            reportWorkbook.Save(pdfPath, pdfOptions);

            Console.WriteLine("Export completed:");
            Console.WriteLine($" • PDF saved to {pdfPath}");
            Console.WriteLine($" • PowerPoint saved to {pptPath}");
        }
    }
}
```

### Почему это работает

1. **Обработка Smart Marker** позволяет заполнять книгу данными из любого источника (JSON, DataTables и т.д.) без написания циклов.  
2. **DetailSheetNewName** создаёт отдельный лист для каждого отдела, давая чистую вкладку — по‑отделу.  
3. **Копирование диапазона** (`sourceRange.Copy`) дублирует сводную таблицу *включая* её кэш, поэтому скопированный лист работает точно так же, как оригинал.  
4. **PresentationOptions** с параметрами `ExportCharts`, `ExportShapes` и `ExportTextBoxes` указывает Aspose рендерить эти объекты как нативные элементы PowerPoint, сохраняя их редактируемость.  
5. **PdfSaveOptions.EmbedStandardFonts** гарантирует, что PDF будет выглядеть одинаково на компьютерах без оригинальных шрифтов.

В результате получаются два файла — `FinalReport.pdf` и `FinalPresentation.pptx` — которые можно отправлять по электронной почте, архивировать или открывать в любом просмотрщике без потери качества.

## Экспорт диаграмм в PowerPoint (сохранить книгу как PPTX)

Если ваш отчёт содержит диаграммы, скорее всего, вы захотите, чтобы они были редактируемыми в PowerPoint. Ключевой класс — `PresentationOptions`. Ниже фокусированный фрагмент, показывающий только часть, отвечающую за экспорт диаграмм:

```csharp
// Assuming reportWorkbook already contains charts
var pptExportOptions = new PresentationOptions
{
    ExportCharts = true,      // Convert Excel charts to PowerPoint chart objects
    ExportShapes = false,    // Skip shapes if you don’t need them
    ExportTextBoxes = true   // Keep any text boxes editable
};

string pptFile = @"C:\Temp\ChartsOnly.pptx";
reportWorkbook.Save(pptFile, SaveFormat.Pptx, pptExportOptions);
```

**Что происходит «под капотом»?** Aspose переводит каждую диаграмму Excel в нативную диаграмму PowerPoint, сохраняя серии, подписи осей и форматирование. Это гораздо лучше, чем экспортировать диаграмму как статическое изображение, потому что ваша аудитория сможет позже менять отдельные точки данных.

## Копирование листа со сводной таблицей без потери данных

Сводные таблицы часто являются самой сложной частью экспорта, так как они опираются на скрытый кэш. Простой метод `Copy` работает, потому что Aspose копирует как видимый диапазон, **так и** объект кэша.

```csharp
// Copy the whole sheet (including pivot table) to a new workbook
Workbook clone = new Workbook();
reportWorkbook.Worksheets[0].CopyTo(clone.Worksheets[0]);
clone.Save(@"C:\Temp\PivotCopy.xlsx", SaveFormat.Xlsx);
```

> **Note:** Если вам нужна сводная таблица только на новом листе внутри той же книги, подход `sourceRange.Copy`, описанный выше, легче и не требует создания новой книги.

## Встраивание шрифтов при экспорте в PDF — почему это важно

Когда открываете PDF на машине, где отсутствуют оригинальные шрифты, текст может смещаться, меняются переносы строк или исчезают символы. Установка `EmbedStandardFonts = true` заставляет Aspose встраивать самые распространённые шрифты (Arial, Times New Roman и др.) непосредственно в поток PDF.

Если вы используете пользовательские шрифты, переключитесь на `PdfSaveOptions.FontEmbeddingMode = FontEmbeddingMode.EmbedAll`. Пример:

```csharp
var pdfOpts = new PdfSaveOptions
{
    EmbedStandardFonts = true,
    FontEmbeddingMode = FontEmbeddingMode.EmbedAll   // For custom fonts
};
reportWorkbook.Save(@"C:\Temp\CustomFontReport.pdf", pdfOpts);
```

Теперь каждый получатель видит точно такой же макет, какой вы создали — без сюрпризов.

## Полный рабочий пример в обзоре

Объединив всё вместе, полный код (показанный ранее) делает следующее:

1. **Создаёт** книгу с заполнителями Smart Marker.  
2. **Обрабатывает** маркеры, генерируя лист‑деталь, названный в честь отдела.  
3. **Копирует** диапазон, содержащий сводную таблицу, на новый лист, сохраняя её функциональность.  
4. **Экспортирует** книгу в PowerPoint, оставляя диаграммы, фигуры и текстовые блоки редактируемыми.  
5. **Экспортирует** ту же книгу в PDF, встраивая стандартные шрифты для надёжного отображения.

Запустите программу, откройте сгенерированные файлы, и вы увидите:

- **PDF**: Чёткие таблицы, встроенные шрифты и тот же визуальный стиль, что и в исходном Excel.  
- **PowerPoint**: Редактируемые диаграммы, которые можно щёлкнуть правой кнопкой → *Edit Data* в PowerPoint, и фигуры, остающиеся полностью управляемыми.

---

## Часто задаваемые вопросы (FAQ)

**Q: Работает ли это с .NET Core?**  
Да — Aspose.Cells и Aspose.Slides кроссплатформенны. Достаточно целиться в .NET 6 или новее, и тот же код будет работать в Windows, Linux и macOS.

**Q: Что делать, если нужно экспортировать только часть листов?**  
Используйте `Workbook.Save` с `SaveOptions`, позволяющими указать `SheetNames`. Пример: `new PresentationOptions { SheetNames = new[] { "Copy" } }`.

**Q: Можно ли зашифровать PDF?**  
Конечно. Установите `PdfSaveOptions.EncryptionDetails` с паролем перед вызовом `Save`.

**Q: Моя сводная таблица использует внешний источник данных — сломается ли ссылка при копировании?**  
Операция копирования включает кэш, но не внешнее соединение. Сводная таблица будет работать офлайн, однако не будет обновляться из оригинального источника. Если нужен живой апдейт, экспортируйте исходные данные вместе с книгой.

## Следующие шаги и смежные темы

- **Dynamic Data Sources** – Узнайте, как подавать JSON или DataTable в Smart Markers для отчётности в реальном времени.  
- **Advanced PDF Styling** – Explore `

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}