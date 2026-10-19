---
category: general
date: 2026-06-27
description: Как экспортировать Excel с помощью C# — узнайте, как преобразовать Excel
  в PowerPoint, создать PowerPoint из Excel и загрузить книгу Excel в C# за считанные
  минуты.
draft: false
keywords:
- how to export excel
- convert excel to powerpoint
- create powerpoint from excel
- load excel workbook c#
- export excel chart powerpoint
language: ru
og_description: Как экспортировать Excel с помощью C# — просто. Следуйте этому пошаговому
  руководству, чтобы преобразовать Excel в PowerPoint, создать PowerPoint из Excel
  и загрузить рабочую книгу Excel в C#.
og_title: Как экспортировать Excel в PowerPoint — полное руководство по C#
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: How to export Excel using C#—learn to convert Excel to PowerPoint,
    create PowerPoint from Excel, and load Excel workbook C# in minutes.
  headline: How to Export Excel to PowerPoint – Complete C# Guide
  type: TechArticle
- description: How to export Excel using C#—learn to convert Excel to PowerPoint,
    create PowerPoint from Excel, and load Excel workbook C# in minutes.
  name: How to Export Excel to PowerPoint – Complete C# Guide
  steps:
  - name: '**Load Excel workbook** – We read the `.xlsx` file into memory.'
    text: '**Load Excel workbook** – We read the `.xlsx` file into memory.'
  - name: '**Convert workbook to a PowerPoint presentation** – Aspose converts each
      worksheet (or selected chart) into a slide.'
    text: '**Convert workbook to a PowerPoint presentation** – Aspose converts each
      worksheet (or selected chart) into a slide.'
  - name: '**Save the generated presentation** – The final PPTX can be opened in PowerPoint,
      edited, or sent to stakeholders.'
    text: '**Save the generated presentation** – The final PPTX can be opened in PowerPoint,
      edited, or sent to stakeholders.'
  type: HowTo
- questions:
  - answer: Yes. Use `Workbook.Worksheets["Sheet1"]` to isolate a sheet, then call
      `SaveToPresentation` on that worksheet alone.
    question: Can I export only a single worksheet instead of the whole workbook?
  - answer: Macros are not transferred to PowerPoint—only visual objects (charts,
      tables) are exported. If you need macro functionality, consider generating the
      slides first, then adding VBA manually.
    question: What about preserving macros?
  - answer: Absolutely. Aspose.Cells supports legacy formats; just change the file
      extension in `excelPath`.
    question: Does this work with `.xls` files?
  - answer: 'After creating the `Presentation` object, set: ```csharp presentation.SlideSize.Size
      = SlideSizeType.Widescreen; ```'
    question: How do I change the slide size to widescreen (16:9)?
  - answer: 'Open‑source libraries like EPPlus can read Excel, but they don’t provide
      direct Excel‑to‑PowerPoint conversion. You’d need to manually render charts
      to images and insert them, which is far more code. ## Tips & Best Practices
      - **Batch processing:** If you have dozens of workbooks, wrap the conversio'
    question: Is there a free alternative?
  type: FAQPage
tags:
- C#
- Excel
- PowerPoint
- Aspose
title: Как экспортировать Excel в PowerPoint — полное руководство по C#
url: /ru/net/converting-excel-files-to-other-formats/how-to-export-excel-to-powerpoint-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как экспортировать Excel в PowerPoint – Полное руководство на C#

Когда‑нибудь задавались вопросом, **как экспортировать Excel** данные напрямую в презентацию PowerPoint без потери форматирования? Вы не одиноки. Во многих конвейерах отчетности узким местом является перенос графиков и таблиц из рабочей книги Excel в стильную презентацию. Хорошие новости? Всего лишь несколькими строками C# вы можете **convert Excel to PowerPoint**, создать полностью редактируемый PPTX и даже сохранить точность графиков.

В этом руководстве мы пройдем процесс загрузки рабочей книги Excel в C#, преобразования её содержимого в презентацию PowerPoint и сохранения результата. К концу вы сможете **create PowerPoint from Excel** автоматически — без ручного копирования‑вставки. Никаких сложных UI‑трюков, только чистый код.

> **Что вам понадобится**  
> * .NET 6+ (or .NET Framework 4.7.2+)  
> * Пакеты NuGet Aspose.Cells и Aspose.Slides (они выполняют основную работу)  
> * Пример файла Excel с как минимум одним графиком (мы назовём его `chartOle.xlsx`)  

![Диаграмма, показывающая, как экспортировать Excel в PowerPoint с помощью C#](https://example.com/images/export-excel-to-pptx.png "Диаграмма «Как экспортировать Excel в PowerPoint»")

## Как экспортировать Excel в PowerPoint с помощью C# – Обзор

Прежде чем приступить к кодированию, полезно понять трехшаговый процесс:

1. **Load Excel workbook** – Мы читаем файл `.xlsx` в память.  
2. **Convert workbook to a PowerPoint presentation** – Aspose преобразует каждый лист (или выбранный график) в слайд.  
3. **Save the generated presentation** – Финальный PPTX можно открыть в PowerPoint, отредактировать или отправить заинтересованным сторонам.  

Каждый шаг намеренно изолирован, чтобы позже можно было заменить его пользовательской логикой (например, выбрать определённые листы, применить темы слайдов и т.д.). Теперь разберём детали.

## Шаг 1 – Загрузка рабочей книги Excel в стиле C#

Первое, что вам нужно сделать, — загрузить файл Excel в приложение. С использованием Aspose.Cells код прост:

```csharp
using Aspose.Cells;   // Handles Excel files
using Aspose.Slides;  // Handles PowerPoint files
using System;

// Step 1: Load the Excel workbook
string excelPath = @"YOUR_DIRECTORY\chartOle.xlsx";

if (!System.IO.File.Exists(excelPath))
{
    throw new FileNotFoundException($"Excel file not found at {excelPath}");
}

// The Workbook class reads the .xlsx file into memory
Workbook workbook = new Workbook(excelPath);
```

**Почему это важно:**  
`Workbook` абстрагирует всю таблицу, предоставляя доступ к листам, ячейкам и — что особенно важно — встроенным графикам. Если пропустить проверку существования файла, позже вы получите неопределённый `FileNotFoundException`, который может стать кошмаром для отладки в продакшене.

**Совет:** Если вам нужен только конкретный лист, вы можете передать объект `LoadOptions`, чтобы ограничить использование памяти:

```csharp
LoadOptions options = new LoadOptions(LoadFormat.Xlsx) { LoadDataOnly = true };
Workbook workbook = new Workbook(excelPath, options);
```

Эта небольшая настройка значительно ускоряет работу с большими рабочими книгами.

## Шаг 2 – Преобразование Excel в PowerPoint (Экспорт графика Excel в PowerPoint)

Теперь начинается магия: преобразование рабочей книги в PPTX. Aspose.Slides предоставляет один метод, который делает всю тяжелую работу:

```csharp
// Step 2: Convert the workbook to a PowerPoint presentation (PPTX format)
Presentation presentation = workbook.SaveToPresentation(ExportToPresentationFormat.Pptx);
```

**Что происходит под капотом?**  
`SaveToPresentation` проходит по каждому листу, извлекает объекты графиков и создает слайд для каждого графика. Метод сохраняет оригинальное оформление графика, поэтому цвета, шрифты и подписи данных остаются неизменными. Если в вашей рабочей книге есть простые таблицы, они будут отображаться как текстовые блоки на слайде.

**Особый случай – несколько графиков:**  
Если на листе более одного графика, Aspose размещает их вертикально на одном слайде. Чтобы разместить их на отдельных слайдах, можно вручную перебрать графики в цикле:

```csharp
Presentation presentation = new Presentation();

foreach (Worksheet sheet in workbook.Worksheets)
{
    foreach (Chart chart in sheet.Charts)
    {
        // Export each chart as an individual slide
        ISlide slide = presentation.Slides.AddEmptySlide(presentation.SlideSize.Size);
        chart.ExportToSlide(presentation, slide);
    }
}
```

Этот фрагмент дает вам точный контроль — идеально для отшлифованной презентации.

## Шаг 3 – Сохранение сгенерированной презентации (Создание PowerPoint из Excel)

Последний шаг — сохранить файл PPTX на диск. Это так же просто, как:

```csharp
// Step 3: Save the generated presentation to a file
string pptxPath = @"YOUR_DIRECTORY\editable.pptx";
presentation.Save(pptxPath, Aspose.Slides.Export.SaveFormat.Pptx);

Console.WriteLine($"Presentation saved successfully to {pptxPath}");
```

**Почему стоит проверять результат:**  
После сохранения откройте `editable.pptx` в PowerPoint. Вы должны увидеть один слайд на каждый график, каждый полностью редактируемый (можно менять цвета, перемещать объекты и т.д.). Если график выглядит некорректно, дважды проверьте, что оригинальный график Excel использует стандартные шрифты — некоторые пользовательские шрифты могут не встраиваться корректно.

**Распространённая ошибка:**  
Сохранение на сетевой ресурс без соответствующих прав вызывает `UnauthorizedAccessException`. Убедитесь, что у учетной записи, под которой запущено приложение, есть права записи в `YOUR_DIRECTORY`.

## Полный рабочий пример – Все шаги вместе

Ниже представлен полный, готовый к запуску код. Вставьте его в новый проект Console App, восстановите пакеты NuGet и нажмите **F5**.

```csharp
using System;
using Aspose.Cells;
using Aspose.Slides;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main()
        {
            // Paths – adjust to your environment
            string excelPath = @"YOUR_DIRECTORY\chartOle.xlsx";
            string pptxPath = @"YOUR_DIRECTORY\editable.pptx";

            // -------------------------------------------------
            // Step 1: Load the Excel workbook (load excel workbook c#)
            // -------------------------------------------------
            if (!System.IO.File.Exists(excelPath))
            {
                Console.WriteLine($"Error: File not found -> {excelPath}");
                return;
            }

            Workbook workbook = new Workbook(excelPath);
            Console.WriteLine("Excel workbook loaded successfully.");

            // -------------------------------------------------
            // Step 2: Convert Excel to PowerPoint (export excel chart powerpoint)
            // -------------------------------------------------
            Presentation presentation = workbook.SaveToPresentation(ExportToPresentationFormat.Pptx);
            Console.WriteLine("Workbook converted to PowerPoint.");

            // -------------------------------------------------
            // Step 3: Save the generated presentation (create powerpoint from excel)
            // -------------------------------------------------
            presentation.Save(pptxPath, Aspose.Slides.Export.SaveFormat.Pptx);
            Console.WriteLine($"Presentation saved at: {pptxPath}");
        }
    }
}
```

**Ожидаемый вывод (консоль):**

```
Excel workbook loaded successfully.
Workbook converted to PowerPoint.
Presentation saved at: YOUR_DIRECTORY\editable.pptx
```

Откройте `editable.pptx`, и вы увидите слайд для каждого графика, готовый к дальнейшей доработке.

## Часто задаваемые вопросы (FAQ)

**В: Можно ли экспортировать только один лист, а не всю рабочую книгу?**  
О: Да. Используйте `Workbook.Worksheets["Sheet1"]`, чтобы изолировать лист, затем вызовите `SaveToPresentation` только для этого листа.

**В: Что насчёт сохранения макросов?**  
О: Макросы не переносятся в PowerPoint — экспортируются только визуальные объекты (графики, таблицы). Если нужна функциональность макросов, сначала сгенерируйте слайды, а затем добавьте VBA вручную.

**В: Работает ли это с файлами `.xls`?**  
О: Да. Aspose.Cells поддерживает устаревшие форматы; просто измените расширение файла в `excelPath`.

**В: Как изменить размер слайда на широкоформатный (16:9)?**  
О: После создания объекта `Presentation` установите:

```csharp
presentation.SlideSize.Size = SlideSizeType.Widescreen;
```

**В: Есть ли бесплатная альтернатива?**  
О: Библиотеки с открытым исходным кодом, такие как EPPlus, могут читать Excel, но они не предоставляют прямого преобразования Excel в PowerPoint. Вам придётся вручную рендерить графики в изображения и вставлять их, что требует гораздо больше кода.

## Советы и лучшие практики

- **Batch processing:** Если у вас есть десятки рабочих книг, оберните конвертацию в цикл `Parallel.ForEach` — только будьте осторожны с небезопасными для потоков объектами Aspose.  
- **Memory management:** Вызывайте `presentation.Dispose()` и `workbook.Dispose()` при работе с большими файлами, чтобы своевременно освобождать нативные ресурсы.  
- **Styling slides:** После конвертации вы можете применить тему мастер‑слайда с помощью `presentation.SlideMaster`, чтобы все слайды выглядели одинаково.  
- **Testing:** Автоматизируйте простой модульный тест, который загружает известную рабочую книгу, выполняет конвертацию и проверяет, что полученный PPTX содержит ожидаемое количество слайдов.

## Заключение

Мы только что показали, **как экспортировать Excel** данные в презентацию PowerPoint с помощью C#. Загрузив рабочую книгу, преобразовав её с помощью Aspose и сохранив PPTX, вы получаете повторяемый программный способ **convert Excel to PowerPoint**, **create PowerPoint from Excel** и **load Excel workbook C#**‑style без ручных действий. Код автономный, работает с любой современной средой .NET и может быть расширен для сложных конвейеров отчетности.

Готовы к следующему вызову? Попробуйте вставлять несколько графиков на один слайд, применять пользовательские макеты слайдов или даже автоматически генерировать заметки докладчика. Возможности безграничны, когда вы объединяете автоматизацию Excel с генерацией PowerPoint.

Есть вопросы или интересный пример использования? Оставьте комментарий ниже, и удачной разработки!

## Что стоит изучить дальше?

Следующие руководства охватывают тесно связанные темы, построенные на техниках, продемонстрированных в этом руководстве. Каждый ресурс включает полные рабочие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [Как конвертировать Excel в PowerPoint с помощью Aspose.Cells для .NET&#58; Полное руководство](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [Как экспортировать графики Excel в PDF с помощью Aspose.Cells для .NET&#58; Пошаговое руководство](/cells/english/net/workbook-operations/export-excel-charts-pdf-aspose-cells-net/)
- [Как экспортировать Excel в HTML с сеткой ячеек с помощью Aspose.Cells для .NET](/cells/english/net/workbook-operations/export-excel-to-html-grid-lines-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}