---
category: general
date: 2026-09-15
description: Узнайте, как внедрять шрифты в SVG и экспортировать диаграмму Excel в
  PowerPoint, включая преобразование XLSX в SVG и преобразование XLSX в PPTX с полными
  примерами кода.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- embed fonts in SVG
- export excel chart to powerpoint
- convert xlsx to svg
- convert xlsx to pptx
- save workbook as svg
language: ru
lastmod: 2026-09-15
og_description: Встраивание шрифтов в SVG и экспорт диаграммы Excel в PowerPoint с
  пошаговым кодом C#. Быстро и надёжно преобразуйте XLSX в SVG и XLSX в PPTX.
og_image_alt: Screenshot showing an Excel chart exported to PowerPoint with embedded
  fonts in the resulting SVG file
og_title: Встраивание шрифтов в SVG и экспорт диаграммы Excel в PowerPoint — полное
  руководство
schemas:
- author: Aspose
  dateModified: '2026-09-15'
  description: Learn how to embed fonts in SVG and export Excel chart to PowerPoint,
    covering convert XLSX to SVG and convert XLSX to PPTX with full code examples.
  headline: How to embed fonts in SVG when converting Excel files to SVG and PowerPoint
  type: TechArticle
- description: Learn how to embed fonts in SVG and export Excel chart to PowerPoint,
    covering convert XLSX to SVG and convert XLSX to PPTX with full code examples.
  name: How to embed fonts in SVG when converting Excel files to SVG and PowerPoint
  steps:
  - name: Open `EditableChart.pptx` in PowerPoint.
    text: Open `EditableChart.pptx` in PowerPoint.
  - name: Locate the slide containing the chart.
    text: Locate the slide containing the chart.
  - name: Choose **Chart Tools → Design → Edit Data**.
    text: Choose **Chart Tools → Design → Edit Data**.
  - name: Confirm that the Excel‑style data grid appears and that you can change values.
    text: Confirm that the Excel‑style data grid appears and that you can change values.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Как встроить шрифты в SVG при конвертации файлов Excel в SVG и PowerPoint
url: /ru/net/converting-excel-files-to-other-formats/how-to-embed-fonts-in-svg-when-converting-excel-files-to-svg/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как встраивать шрифты в SVG при конвертации файлов Excel в SVG и PowerPoint  

Если вам нужно **встраивать шрифты в SVG** при конвертации рабочей книги Excel, это руководство покажет, как это сделать. Вы также узнаете, как **экспортировать диаграмму Excel в PowerPoint**, а также как **конвертировать XLSX в SVG** и **конвертировать XLSX в PPTX** с редактируемыми диаграммами.  

Работа с данными Excel программно часто требует переноса одного и того же визуального контента между разными форматами файлов. Ручное воссоздание диаграммы в PowerPoint или повторное применение шрифтов в SVG подвержено ошибкам и отнимает много времени. К концу этого руководства у вас будет один переиспользуемый фрагмент C#, который:

* Сохраняет рабочую книгу в файл SVG с встроенными шрифтами и селекторами вариаций шрифтов.  
* Экспортирует ту же рабочую книгу в файл PPTX, где диаграмма остаётся редактируемой.  

Единственное требование — наличие недавней версии **Aspose.Cells for .NET** (2024‑x или новее) и среды разработки .NET, такой как Visual Studio 2022.

---

## Что вам понадобится  

* .NET 6.0 или новее (код также работает на .NET Framework 4.8).  
* NuGet‑пакет Aspose.Cells for .NET (`Install-Package Aspose.Cells`).  
* Файл Excel (`input.xlsx`), содержащий как минимум одну диаграмму.  
* Права записи в каталог вывода.  

---

## Встраивание шрифтов в SVG при конвертации XLSX в SVG  

Встраивание шрифтов гарантирует, что SVG будет отображаться корректно на любом устройстве, даже если целевая система не имеет оригинальных шрифтов. Класс `SvgSaveOptions` предоставляет два флага, позволяющих это сделать: `EmbedFonts` и `FontVariationSelectors`.

```csharp
using Aspose.Cells;
using Aspose.Cells.Rendering;

// Load the workbook
Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");

// OPTIONAL: Use WRAPCOLS to reshape data before export (demonstrates a formula)
Worksheet sheet = workbook.Worksheets[0];
sheet.Cells["A1"].Formula = "=WRAPCOLS({1,2,3,4,5},2)"; // 2 columns per wrap
sheet.Calculate(); // Force calculation so the formula result appears

// Configure SVG options to embed fonts
SvgSaveOptions svgOptions = new SvgSaveOptions
{
    EmbedFonts = true,                // embed fonts in the SVG
    FontVariationSelectors = true    // include variation selectors for better Unicode handling
};

// Save the workbook as an SVG file
string svgPath = @"YOUR_DIRECTORY\WithFonts.svg";
workbook.Save(svgPath, svgOptions);
```

**Почему это работает:**  
* `EmbedFonts = true` копирует файлы шрифтов в раздел `<defs>` SVG, устраняя внешние зависимости.  
* `FontVariationSelectors = true` добавляет необходимые селекторы для шрифтов, поддерживающих функции OpenType, сохраняя варианты глифов, такие как лигатуры.  

**Ожидаемый результат:** Откройте `WithFonts.svg` в любом современном браузере; текст внутри диаграммы или ячеек будет отображаться тем же шрифтом, что использовался в Excel, даже на компьютерах, где этот шрифт не установлен.

---

## Экспорт диаграммы Excel в PowerPoint с редактируемыми диаграммами  

Когда необходимо встроить диаграмму в слайд PowerPoint, но при этом дать получателю возможность редактировать данные диаграммы, `PptxSaveOptions` из Aspose.Cells предоставляет флаг `ExportEditableChart`.

```csharp
// Configure PPTX options to keep charts editable after export
PptxSaveOptions pptxOptions = new PptxSaveOptions
{
    ExportEditableChart = true   // allow chart editing in PowerPoint
};

// Save the same workbook as a PPTX file
string pptxPath = @"YOUR_DIRECTORY\EditableChart.pptx";
workbook.Save(pptxPath, pptxOptions);
```

**Почему это важно:**  
Установка `ExportEditableChart` в `true` сохраняет диаграмму как объект Office Open XML, а не как статическое изображение. Когда вы открываете `EditableChart.pptx` в PowerPoint, можно щелкнуть правой кнопкой мыши по диаграмме → **Edit Data** и изменить серии так же, как в нативной диаграмме PowerPoint.

**Шаги проверки:**  

1. Откройте `EditableChart.pptx` в PowerPoint.  
2. Найдите слайд, содержащий диаграмму.  
3. Выберите **Chart Tools → Design → Edit Data**.  
4. Убедитесь, что появляется сетка данных в стиле Excel и что вы можете менять значения.

---

## Конвертация XLSX в SVG – полный обзор рабочего процесса  

Ниже представлена компактная версия, объединяющая загрузку, необязательную манипуляцию данными и сохранение в SVG. Используйте её, когда нужен только вывод в SVG.

```csharp
public void ConvertXlsxToSvg(string inputPath, string outputPath)
{
    Workbook wb = new Workbook(inputPath);

    // Example: apply a formula to demonstrate cell calculations
    Worksheet ws = wb.Worksheets[0];
    ws.Cells["A1"].Formula = "=WRAPCOLS({1,2,3,4,5},2)";
    ws.Calculate();

    SvgSaveOptions opts = new SvgSaveOptions
    {
        EmbedFonts = true,
        FontVariationSelectors = true
    };

    wb.Save(outputPath, opts);
}
```

Вызовите метод следующим образом:

```csharp
ConvertXlsxToSvg(@"YOUR_DIRECTORY\input.xlsx", @"YOUR_DIRECTORY\Result.svg");
```

**Подсказка для крайних случаев:** Если ваша рабочая книга содержит пользовательские шрифты, не установленные на сервере, встраивайте их вручную перед вызовом `Save`. Используйте `FontInfoCollection` для добавления файлов шрифтов в `SvgSaveOptions` через свойство `CustomFonts` (доступно в более новых версиях Aspose.Cells).

---

## Конвертация XLSX в PPTX – сохранение редактируемости диаграмм  

Следующий вспомогательный метод демонстрирует путь **convert XLSX to PPTX**, обеспечивая сохранение редактируемости диаграммы.

```csharp
public void ConvertXlsxToPptx(string inputPath, string outputPath)
{
    Workbook wb = new Workbook(inputPath);

    // Ensure any chart you want to keep editable is on the first worksheet
    // (Aspose.Cells exports only the first worksheet by default for PPTX)
    PptxSaveOptions opts = new PptxSaveOptions
    {
        ExportEditableChart = true
    };

    wb.Save(outputPath, opts);
}
```

Использование:

```csharp
ConvertXlsxToPptx(@"YOUR_DIRECTORY\input.xlsx", @"YOUR_DIRECTORY\Result.pptx");
```

**Распространённый вопрос:** *Что если моя рабочая книга содержит несколько листов с диаграммами?*  
**Ответ:** По умолчанию Aspose.Cells экспортирует первый лист. Чтобы включить дополнительные листы, пройдитесь по `workbook.Worksheets`, скопируйте каждую диаграмму на новый слайд и сохраните каждый слайд отдельно, используя объекты `Presentation` из Aspose.Slides. Этот продвинутый сценарий выходит за рамки базового процесса «сохранить рабочую книгу как SVG» и «экспортировать диаграмму Excel в PowerPoint», но основные флаги остаются теми же.

---

## Практические советы и подводные камни  

* **Performance:** Встраивание шрифтов увеличивает размер файла SVG. Если размер критичен, установите `EmbedFonts = false` и используйте веб‑безопасные шрифты.  
* **Font licensing:** Убедитесь, что у вас есть право встраивать используемые шрифты; некоторые коммерческие шрифты ограничивают встраивание.  
* **Chart compatibility:** Редактируемые диаграммы сохраняются как части `chart.xml` внутри PPTX. Очень сложные диаграммы (например, 3‑D или комбинированные) могут потерять часть оформления при редактировании в PowerPoint. Протестируйте наиболее часто используемые типы диаграмм.  
* **Version mismatches:** Флаг `ExportEditableChart` требует Aspose.Cells 20.10 или новее. При использовании более старой версии будет тихо переключено на растровое изображение.  
* **Thread safety:** Объекты Workbook не являются потокобезопасными. Создавайте новый экземпляр `Workbook` для каждого запроса в сценарии веб‑службы.  

---

## Полный пример от начала до конца  

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;

class ExcelExportDemo
{
    static void Main()
    {
        // Paths – adjust to your environment
        string inputFile = @"YOUR_DIRECTORY\input.xlsx";
        string svgFile   = @"YOUR_DIRECTORY\WithFonts.svg";
        string pptxFile  = @"YOUR_DIRECTORY\EditableChart.pptx";

        // 1. Load workbook
        Workbook workbook = new Workbook(inputFile);

        // 2. Optional: reshape data using WRAPCOLS
        Worksheet sheet = workbook.Worksheets[0];
        sheet.Cells["A1"].Formula = "=WRAPCOLS({1,2,3,4,5},2)";
        sheet.Calculate();

        // 3. Save as SVG with embedded fonts
        SvgSaveOptions svgOpts = new SvgSaveOptions
        {
            EmbedFonts = true,
            FontVariationSelectors = true
        };
        workbook.Save(svgFile, svgOpts);
        Console.WriteLine($"SVG saved with embedded fonts to: {svgFile}");

        // 4. Save as PPTX with editable chart
        PptxSaveOptions pptxOpts = new PptxSaveOptions
        {
            ExportEditableChart = true
        };
        workbook.Save(pptxFile, pptxOpts);
        Console.WriteLine($"PPTX saved with editable chart to: {pptxFile}");
    }
}
```

Запуск этой программы создаёт два файла:

* **WithFonts.svg** – SVG, который отображается точно так же, как в Excel, со встроенными шрифтами.  
* **EditableChart.pptx** – презентация PowerPoint, в которой диаграмму можно редактировать напрямую.

---

## Заключение  

Теперь вы знаете, как **встраивать шрифты в SVG** при **конвертации XLSX в SVG**, а также как **экспортировать диаграмму Excel в PowerPoint**, сохраняя её редактируемой. Тот же код демонстрирует простой способ **сохранить рабочую книгу как SVG** и **конвертировать XLSX в PPTX** с минимальными усилиями.  

Отсюда вы можете изучать дальнейшие темы, такие как:

* Программное добавление пользовательских шрифтов (`svgOptions.CustomFonts`).  
* Пакетная обработка нескольких рабочих книг в фоновом сервисе.  
* Использование Aspose.Slides для создания много‑слайдовых файлов PPTX, комбинирующих несколько диаграмм Excel.  

Экспериментируйте с параметрами, адаптируйте фрагменты к вашему проекту и наслаждайтесь надёжными конверсиями Excel‑в‑SVG/PPTX без ручной пост‑обработки. Приятного кодинга!

## Что вам следует изучить дальше?

Следующие руководства охватывают тесно связанные темы, построенные на техниках, продемонстрированных в этом руководстве. Каждый ресурс включает полностью рабочие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [Как конвертировать диаграммы Excel в SVG с помощью Aspose.Cells for .NET (Пошаговое руководство)](/cells/english/net/charts-graphs/convert-excel-chart-to-svg-aspose-cells-net/)
- [Конвертировать диаграмму Excel в SVG Aspose Cells Net](/cells/german/net/charts-graphs/convert-excel-chart-to-svg-aspose-cells-net/)
- [Конвертировать диаграмму Excel в SVG Aspose Cells Net](/cells/french/net/charts-graphs/convert-excel-chart-to-svg-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}