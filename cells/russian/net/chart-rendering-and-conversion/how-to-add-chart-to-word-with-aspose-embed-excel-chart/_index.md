---
category: general
date: 2026-10-01
description: Добавьте диаграмму в Word с помощью Aspose за считанные минуты. Узнайте,
  как встроить диаграмму Excel в Word, экспортировать диаграмму из Excel в Word, создать
  документ Word с Aspose и сохранить диаграмму в документе Word.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add chart to word
- embed excel chart word
- export chart excel word
- create word document aspose
- save chart word document
language: ru
lastmod: 2026-10-01
og_description: Добавьте диаграмму в Word с помощью Aspose за считанные минуты. В
  этом руководстве показано, как встроить диаграмму Excel в Word, экспортировать диаграмму
  из Excel в Word, создать документ Word с Aspose и сохранить диаграмму в документе
  Word.
og_image_alt: Screenshot illustrating how to add chart to Word using Aspose
og_title: Добавить диаграмму в Word с помощью Aspose – встроить диаграмму Excel
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Add chart to Word with Aspose in just minutes. Learn to embed Excel
    chart in Word, export chart Excel Word, create Word document Aspose, and save
    chart Word document.
  headline: How to add chart to Word with Aspose – embed Excel chart
  type: TechArticle
- description: Add chart to Word with Aspose in just minutes. Learn to embed Excel
    chart in Word, export chart Excel Word, create Word document Aspose, and save
    chart Word document.
  name: How to add chart to Word with Aspose – embed Excel chart
  steps:
  - name: '**Loading the workbook** – `Workbook` parses the Excel file and gives you
      programmatic access to its worksheets and charts.'
    text: '**Loading the workbook** – `Workbook` parses the Excel file and gives you
      programmatic access to its worksheets and charts.'
  - name: '**Creating the Word document** – `Document` is the Aspose.Words entry point
      for any Word‑processing task.'
    text: '**Creating the Word document** – `Document` is the Aspose.Words entry point
      for any Word‑processing task.'
  - name: '**DocumentBuilder** – This helper class lets you insert content (text,
      images, charts) at the current cursor position.'
    text: '**DocumentBuilder** – This helper class lets you insert content (text,
      images, charts) at the current cursor position.'
  - name: '**InsertChart** – The overload that accepts an `Aspose.Cells.Chart` object
      copies the chart’s data, formatting, and series directly into the Word file.
      No intermediate image conversion is required, preserving vector quality.'
    text: '**InsertChart** – The overload that accepts an `Aspose.Cells.Chart` object
      copies the chart’s data, formatting, and series directly into the Word file.
      No intermediate image conversion is required, preserving vector quality.'
  - name: '**Save** – `Save` writes the .docx package to disk, completing the **save
      chart word document** step.'
    text: '**Save** – `Save` writes the .docx package to disk, completing the **save
      chart word document** step.'
  type: HowTo
tags:
- Aspose
- C#
- Word automation
title: Как добавить диаграмму в Word с помощью Aspose – встроить диаграмму Excel
url: /ru/net/chart-rendering-and-conversion/how-to-add-chart-to-word-with-aspose-embed-excel-chart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как добавить диаграмму в Word с помощью Aspose – встраивание диаграммы Excel

Если вам нужно **быстро добавить диаграмму в Word**, этот учебник предоставляет полное готовое решение. Вы увидите, как встроить диаграмму Excel в файл Word, экспортировать диаграмму из Excel в Word и, наконец, **сохранить документ Word с диаграммой** всего несколькими строками C#.

Встраивание диаграмм — распространённая потребность при программной генерации отчетов, счетов или панелей мониторинга. К концу этого руководства вы сможете **создавать документы Word с Aspose**, содержащие любую диаграмму из книги Excel, без ручного копирования и вставки.

## Требования

- .NET 6.0 или новее (код также работает с .NET Framework 4.7+)
- Пакеты NuGet Aspose.Cells и Aspose.Words (установить с помощью `dotnet add package Aspose.Cells` и `dotnet add package Aspose.Words`)
- Существующий файл Excel (`Chart.xlsx`), содержащий как минимум одну диаграмму
- Среда разработки, например Visual Studio 2022 или VS Code

## Добавление диаграммы в Word с Aspose

Ниже представлен полный автономный пример программы. Скопируйте его в новый консольный проект, восстановите пакеты и запустите. Программа загружает книгу Excel, создаёт документ Word, вставляет первую диаграмму и сохраняет результат.

```csharp
using System;
using Aspose.Cells;
using Aspose.Words;
using Aspose.Words.Drawing;

namespace AddChartToWordDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Load the Excel workbook that contains the chart
            var workbookPath = @"YOUR_DIRECTORY\Chart.xlsx";
            var workbook = new Workbook(workbookPath);

            // Step 2: Create a new Word document that will receive the chart
            var wordDoc = new Document();

            // Step 3: Initialise a DocumentBuilder for the Word document
            var builder = new DocumentBuilder(wordDoc);

            // Step 4: Insert the first chart from the first worksheet into the Word document
            // This uses Aspose.Words' InsertChart overload that accepts an Aspose.Cells chart object
            builder.InsertChart(workbook.Worksheets[0].Charts[0]);

            // Step 5: Save the resulting Word document
            var outputPath = @"YOUR_DIRECTORY\Chart.docx";
            wordDoc.Save(outputPath);

            Console.WriteLine($"Chart successfully added and saved to '{outputPath}'.");
        }
    }
}
```

### Почему каждая строка важна

1. **Загрузка книги** – `Workbook` разбирает файл Excel и предоставляет программный доступ к листам и диаграммам.  
2. **Создание документа Word** – `Document` является точкой входа Aspose.Words для любой задачи обработки Word.  
3. **DocumentBuilder** – Этот вспомогательный класс позволяет вставлять содержимое (текст, изображения, диаграммы) в текущую позицию курсора.  
4. **InsertChart** – Перегрузка, принимающая объект `Aspose.Cells.Chart`, копирует данные, форматирование и серии диаграммы непосредственно в файл Word. Промежуточное преобразование в изображение не требуется, сохраняется векторное качество.  
5. **Save** – `Save` записывает пакет .docx на диск, завершая шаг **сохранить документ Word с диаграммой**.

#### Ожидаемый результат

После выполнения программы откройте `Chart.docx`. Вы увидите точную диаграмму, хранящуюся в `Chart.xlsx`, расположенную там, где был размещён builder (в начале документа). Диаграмма остаётся полностью редактируемой в Word (можно изменять размер, цвета или источник данных).

## Встраивание диаграммы Excel в Word

Если необходимо встроить более одной диаграммы, повторите вызов `InsertChart` для каждого объекта диаграммы. Например, чтобы встроить все диаграммы с первого листа:

```csharp
var sheet = workbook.Worksheets[0];
foreach (Chart chart in sheet.Charts)
{
    builder.InsertChart(chart);
    builder.Writeln(); // add a line break between charts
}
```

**Совет:** Используйте `builder.Writeln()`, чтобы вставить разрыв абзаца, гарантируя, что каждая диаграмма начинается с новой строки.

## Экспорт диаграммы Excel в Word – обработка нескольких листов

Когда диаграммы распределены по нескольким листам, пройдитесь по коллекции `Worksheets` книги:

```csharp
foreach (Worksheet ws in workbook.Worksheets)
{
    foreach (Chart chart in ws.Charts)
    {
        builder.InsertChart(chart);
        builder.Writeln();
    }
}
```

Этот подход **экспортирует диаграмму из Excel в Word** для любой структуры книги, делая решение надёжным для сложных отчётов.

## Создание документа Word с Aspose – настройка внешнего вида

Вы можете управлять размером и положением каждой вставленной диаграммы, изменяя объект `Shape`, возвращаемый `InsertChart`:

```csharp
Shape chartShape = builder.InsertChart(chart);
chartShape.Width = 500;   // width in points
chartShape.Height = 300;  // height in points
chartShape.WrapType = WrapType.Inline; // make the chart flow with text
```

Установка `WrapType` в `Inline` обеспечивает поведение диаграммы как обычного абзаца, что часто требуется при автоматической генерации документов.

## Сохранение документа Word с диаграммой – лучшие практики

- **Используйте описательное имя файла** (`Report_Q1_2026.docx`), чтобы упростить версионирование.
- **Освобождайте объекты** после использования, особенно в больших пакетных процессах:

```csharp
wordDoc.Dispose();
workbook.Dispose();
```

- **Проверяйте результат** программно, если генерируете множество файлов:

```csharp
if (System.IO.File.Exists(outputPath))
{
    Console.WriteLine("File saved successfully.");
}
else
{
    Console.Error.WriteLine("Failed to save the document.");
}
```

## Часто задаваемые вопросы и особые случаи

| Question | Answer |
|----------|--------|
| *Могу ли я вставить диаграмму, которая не первая на листе?* | Да. Обратитесь к ней по индексу: `sheet.Charts[2]` для третьей диаграммы. |
| *Что делать, если диаграмма Excel использует источник данных, отсутствующий в книге?* | Aspose.Cells встраивает данные непосредственно в объект диаграммы, поэтому диаграмма остаётся рабочей даже при удалении исходного диапазона. |
| *Нужна ли лицензия для Aspose?* | Бесплатная оценочная версия работает, но лицензированная версия удаляет водяной знак оценки и открывает полный набор функций. |
| *Будет ли диаграмма редактируемой в Word после вставки?* | Диаграмма вставляется как нативная диаграмма Word, поэтому пользователи могут редактировать серии, заголовки и стили через интерфейс Word. |
| *Как вставить диаграмму как изображение вместо нативной диаграммы?* | Используйте `builder.InsertImage(chart.ToImage())`, чтобы встроить растровое изображение. Это полезно, когда нужно сохранить точный визуальный вид без возможности редактирования на уровне Word. |

## Полный рабочий пример (копировать‑вставить)

Запуск кода создаёт файл Word (`ReportWithCharts.docx`), содержащий результаты **добавления диаграммы в Word** для каждой диаграммы в исходной книге.

```csharp
using System;
using Aspose.Cells;
using Aspose.Words;
using Aspose.Words.Drawing;

class AddChartToWord
{
    static void Main()
    {
        // Load Excel workbook
        var wb = new Workbook(@"C:\Data\Chart.xlsx");

        // Create Word document
        var doc = new Document();
        var builder = new DocumentBuilder(doc);

        // Insert every chart from every worksheet
        foreach (Worksheet ws in wb.Worksheets)
        {
            foreach (Chart ch in ws.Charts)
            {
                Shape shape = builder.InsertChart(ch);
                shape.Width = 500;
                shape.Height = 300;
                builder.Writeln(); // separate charts
            }
        }

        // Save the document
        var outPath = @"C:\Data\ReportWithCharts.docx";
        doc.Save(outPath);
        Console.WriteLine($"Document saved to {outPath}");
    }
}
```

## Заключение

Теперь вы знаете, как **добавлять диаграмму в Word** с помощью Aspose.Cells и Aspose.Words, как **встраивать диаграмму Excel в Word**, **экспортировать диаграмму из Excel в Word**, **создавать документы Word с Aspose**, и, наконец, **сохранять документ Word с диаграммой**. Этот подход работает как для сценариев с одной диаграммой, так и для сложных книг с множеством диаграмм на разных листах.

Следующие шаги, которые вы можете изучить:

- Применить пользовательское стилизование к вставленным диаграммам (цвета, шрифты) через API `Chart`.
- Скомбинировать вставку диаграмм с генерацией текста для создания полностью автоматизированных отчётов.
- Использовать Aspose.Slides, если необходимо

## Что изучать дальше?

Следующие учебники охватывают тесно связанные темы, построенные на техниках, продемонстрированных в этом руководстве. Каждый ресурс включает полные рабочие примеры кода с пошаговыми объяснениями, помогая вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [Как сохранить DOCX из Excel – Полное руководство по экспорту диаграмм в Word](/cells/english/net/converting-excel-files-to-other-formats/how-to-save-docx-from-excel-complete-guide-to-export-charts/)
- [Создание книги Excel с круговой диаграммой с помощью Aspose.Cells .NET – Подробное руководство](/cells/english/net/charts-graphs/create-excel-workbook-pie-chart-aspose-cells-net/)
- [Создание пузырьковой диаграммы в Excel с помощью Aspose.Cells .NET&#58; Пошаговое руководство](/cells/english/net/charts-graphs/create-bubble-chart-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}