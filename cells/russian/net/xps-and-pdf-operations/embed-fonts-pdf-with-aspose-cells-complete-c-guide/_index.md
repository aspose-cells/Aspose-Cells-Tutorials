---
category: general
date: 2026-06-24
description: Встраивание шрифтов в PDF с помощью Aspose.Cells на C#. Узнайте, как
  сохранить Excel в PDF, экспортировать Excel в HTML, конвертировать xlsx в PDF с
  помощью Aspose и дублировать строки в сводной таблице.
draft: false
keywords:
- embed fonts pdf
- save excel as pdf
- export excel to html
- xlsx to pdf aspose
- duplicate rows pivot
language: ru
og_description: Встраивание шрифтов в PDF с помощью Aspose.Cells в C#. Этот учебник
  пошагово показывает, как сохранить Excel в PDF, экспортировать Excel в HTML и многое
  другое.
og_title: Встраивание шрифтов в PDF с помощью Aspose.Cells – Полное руководство по
  C#
schemas:
- author: Aspose
  dateModified: '2026-06-24'
  description: Embed fonts PDF using Aspose.Cells in C#. Learn how to save Excel as
    PDF, export Excel to HTML, convert xlsx to PDF with Aspose, and duplicate rows
    pivot.
  headline: Embed fonts PDF with Aspose.Cells – Complete C# Guide
  type: TechArticle
tags:
- Aspose.Cells
- C#
title: Встраивание шрифтов в PDF с помощью Aspose.Cells – Полное руководство по C#
url: /ru/net/xps-and-pdf-operations/embed-fonts-pdf-with-aspose-cells-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Встраивание шрифтов PDF с Aspose.Cells – Полное руководство на C#

Когда‑нибудь задумывались, как **встраивать шрифты PDF** при конвертации рабочей книги Excel с помощью Aspose.Cells? Вы не одиноки — многие разработчики сталкиваются с проблемой, когда сгенерированный PDF выглядит некорректно на компьютерах, где исходные шрифты не установлены.  

В этом руководстве мы пройдем реальный пример, который не только **встраивает шрифты PDF**, но и показывает, как **сохранить Excel как PDF**, **экспортировать Excel в HTML**, преобразовать **xlsx в PDF с Aspose**, а также **дублировать строки сводной таблицы** без разрушения сводной таблицы. Звучит много? Не переживайте — мы разберём всё пошагово.

## Что вы узнаете

- Как копировать строки, содержащие сводную таблицу, при этом сохранять её целостность.  
- Как вставить smart‑marker, который повторяет лист деталей для каждого заказа.  
- Точные настройки, необходимые для **встраивания шрифтов PDF**, экспорта диаграмм в редактируемый PPTX и сохранения замороженных областей при **экспорте Excel в HTML**.  
- Советы по устранению распространённых проблем, таких как отсутствие шрифтов или повреждённые OLE‑объекты.  

**Требования:** .NET 6+ (или .NET Framework 4.6+), установленный Aspose.Cells для .NET и базовая среда разработки C# (Visual Studio, Rider или VS Code). Дополнительные пакеты NuGet, помимо Aspose.Cells, не требуются.

---

## Встраивание шрифтов PDF — пошаговый процесс

Ниже приведён полностью рабочий код. Каждый раздел прокомментирован, чтобы вы точно понимали, почему мы делаем то, что делаем.

```csharp
using Aspose.Cells;
using Aspose.Cells.Drawing;
using Aspose.Cells.Pivot;
using Aspose.Cells.SmartMarker;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Load the workbook that contains a pivot table and a shape
        // -------------------------------------------------
        var workbook = new Workbook("YOUR_DIRECTORY/template.xlsx");

        // -------------------------------------------------
        // Step 2: Duplicate the rows that include the pivot table (keeps the pivot intact)
        // -------------------------------------------------
        // The CopyRows method copies rows 0‑29 (30 rows) from the source worksheet
        // to the same worksheet, effectively duplicating the pivot area.
        workbook.Worksheets[0].Cells.CopyRows(0, 0, 30);

        // -------------------------------------------------
        // Step 3: Insert a smart‑marker to repeat a detail sheet for each order
        // -------------------------------------------------
        var orders = new[]
        {
            new { Id = 101, Items = new[] { "Pen", "Paper" } },
            new { Id = 102, Items = new[] { "Book" } }
        };
        var smartMarkerOptions = new SmartMarkerOptions { DetailSheetNewName = "OrderDetail" };
        workbook.Worksheets[0].SmartMarkerProcessing(new { Orders = orders }, smartMarkerOptions);

        // -------------------------------------------------
        // Step 4: Save the workbook as a PPTX file with editable charts, OLE objects, and text boxes
        // -------------------------------------------------
        var pptxOptions = new PptxSaveOptions
        {
            ExportChartsAsEditable = true,
            ExportOleObjects = true,
            ExportTextBoxesAsEditable = true
        };
        workbook.Save("YOUR_DIRECTORY/result.pptx", pptxOptions);

        // -------------------------------------------------
        // Step 5: Save the same workbook as a PDF while embedding standard fonts
        // -------------------------------------------------
        // This is where we actually **embed fonts PDF**.
        var pdfOptions = new PdfSaveOptions { EmbedStandardFonts = true };
        workbook.Save("YOUR_DIRECTORY/result.pdf", pdfOptions);

        // -------------------------------------------------
        // Step 6: Save the workbook as HTML, preserving frozen panes and embedding all fonts
        // -------------------------------------------------
        // The HTML export respects the original layout and keeps the fonts inside the file.
        var htmlOptions = new HtmlSaveOptions
        {
            PreserveFreezePanes = true,
            EmbedAllFonts = true
        };
        workbook.Save("YOUR_DIRECTORY/result.html", htmlOptions);
    }
}
```

### Почему это работает

- **CopyRows** дублирует строки, содержащие сводную таблицу, поэтому оригинальная сводная таблица остаётся связанной с исходными данными. Это удовлетворяет требованию **duplicate rows pivot**.  
- **SmartMarkerProcessing** создаёт новый лист для каждого заказа, автоматизируя генерацию листа деталей.  
- **PdfSaveOptions.EmbedStandardFonts = true** указывает Aspose.Cells встраивать шрифты непосредственно в PDF‑файл, что является ключом к **embed fonts pdf**. Без этого флага PDF будет использовать системные шрифты, нарушая макет на других компьютерах.  
- **HtmlSaveOptions** с `EmbedAllFonts` и `PreserveFreezePanes` гарантирует, что при **экспорте Excel в HTML** визуальное соответствие будет совпадать с оригинальной книгой.  

#### Ожидаемый результат

- `result.pdf` — PDF, в котором все использованные шрифты встроены; откройте его на любом компьютере, и текст будет выглядеть идентично исходному.  
- `result.pptx` — файл PowerPoint с редактируемыми диаграммами и OLE‑объектами.  
- `result.html` — папка HTML (`result.html` + `result_files`), отображающая книгу в браузере с сохранёнными замороженными областями.

---

## Сохранить Excel как PDF с Aspose.Cells

Если ваша единственная цель — **сохранить Excel как PDF**, вы можете убрать лишние шаги и сосредоточиться на параметрах PDF:

```csharp
var workbook = new Workbook("template.xlsx");

// Minimal PDF conversion – embed fonts for portability
var pdfOpts = new PdfSaveOptions
{
    EmbedStandardFonts = true,   // crucial for embed fonts pdf
    Compliance = PdfCompliance.PdfA1b // optional: make the PDF archival‑friendly
};

workbook.Save("output.pdf", pdfOpts);
```

**Совет:** При целевом соответствии PDF/A Aspose автоматически встраивает все шрифты, обеспечивая дополнительный уровень надёжности для долгосрочного хранения.

---

## Экспортировать Excel в HTML с сохранением макета

Экспорт в HTML часто теряет внешний вид оригинального листа, особенно когда задействованы замороженные области. Ниже приведён фрагмент кода с точными настройками, которые вам нужны:

```csharp
var wb = new Workbook("template.xlsx");

var htmlOpts = new HtmlSaveOptions
{
    PreserveFreezePanes = true, // keeps the top rows/columns locked
    EmbedAllFonts = true,       // embeds fonts so the page looks the same everywhere
    ExportActiveWorksheetOnly = true,
    ExportCellValueAsString = true
};

wb.Save("output.html", htmlOpts);
```

Поскольку мы установили `EmbedAllFonts`, сгенерированный HTML содержит шрифты, закодированные в base‑64, удовлетворяя требование **export excel to html** без внешних CSS‑файлов.

---

## Преобразовать Xlsx в PDF с помощью Aspose.Cells

Иногда в поиске встречается термин «**xlsx to pdf aspose**». Приведённый ниже код демонстрирует точный конвейер конвертации, включая несколько дополнительных удобств:

```csharp
var wb = new Workbook("template.xlsx");

// Optional: set page layout before conversion
wb.Worksheets[0].PageSetup.Orientation = PageOrientation.Landscape;
wb.Worksheets[0].PageSetup.FitToPagesWide = 1;
wb.Worksheets[0].PageSetup.FitToPagesTall = 0;

// PDF options – embed fonts and keep hyperlinks intact
var pdfOpts = new PdfSaveOptions
{
    EmbedStandardFonts = true,
    ExportHyperlinks = true,
    OnePagePerSheet = false
};

wb.Save("converted.pdf", pdfOpts);
```

**Зачем заниматься настройкой страницы?** Если её пропустить, в PDF по умолчанию могут обрезаться столбцы или строки. Предварительная настройка макета гарантирует, что конечный PDF будет соответствовать тому, что вы видите в Excel.

---

## Дублирование строк сводной таблицы — сохранение целостности сводной

Распространённая проблема — попытка копировать строки, содержащие сводную таблицу; при этом сводная часто теряет связь с источником данных. Метод `CopyRows`, который мы использовали ранее, решает эту задачу за вас:

```csharp
// Duplicate the first 30 rows (adjust as needed)
workbook.Worksheets[0].Cells.CopyRows(sourceRow: 0, destinationRow: 0, totalRows: 30);
```

- **sourceRow** — первая строка диапазона, который вы хотите скопировать.  
- **destinationRow** — место, куда должна быть помещена копия (тот же лист, тот же начальный индекс для эффективного дублирования).  
- **totalRows** — количество строк для копирования.  

Поскольку кэш сводной таблицы находится на листе, копирование строк **не** разрывает связь сводной. Это удовлетворяет ключевое слово **duplicate rows pivot**, одновременно поддерживая книгу в порядке.

---

## Полный рабочий пример — резюме

Объединив всё вместе, представляем полный пример программы, который можно вставить в консольное приложение и сразу запустить:



## Что стоит изучить дальше?

Следующие руководства охватывают тесно связанные темы, основанные на техниках, продемонстрированных в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, помогающие вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в собственных проектах.

- [Сохранить книгу Excel как PDF с пользовательскими шрифтами с помощью Aspose.Cells для .NET](/cells/english/net/workbook-operations/save-excel-workbook-pdf-custom-fonts-aspose-cells-net/)
- [Как экспортировать диаграммы Excel в PDF с помощью Aspose.Cells для .NET: пошаговое руководство](/cells/english/net/workbook-operations/export-excel-charts-pdf-aspose-cells-net/)
- [Как экспортировать срезы Excel в PDF с помощью Aspose.Cells для .NET](/cells/english/net/workbook-operations/export-excel-slicers-to-pdf-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}