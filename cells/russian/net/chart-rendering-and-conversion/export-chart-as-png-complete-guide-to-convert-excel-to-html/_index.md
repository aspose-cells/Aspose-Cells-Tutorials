---
category: general
date: 2026-06-30
description: Экспортируйте диаграмму в PNG, пока конвертируете Excel в HTML с помощью
  Aspose.Cells. Узнайте, как внедрять изображения в виде Base64 и сохранять книгу
  в формате HTML за считанные минуты.
draft: false
keywords:
- export chart as png
- convert excel to html
- embed images as base64
- save workbook as html
- export excel chart to png
language: ru
og_description: Экспортируйте диаграмму в PNG и внедряйте изображения в формате Base64
  при преобразовании Excel в HTML. Следуйте этому пошаговому руководству на C#, чтобы
  без труда сохранить рабочую книгу в виде HTML.
og_title: Экспортировать диаграмму в PNG – преобразовать Excel в HTML с помощью Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Export chart as PNG while you convert Excel to HTML using Aspose.Cells.
    Learn to embed images as Base64 and save workbook as HTML in minutes.
  headline: Export Chart as PNG – Complete Guide to Convert Excel to HTML with Aspose.Cells
  type: TechArticle
- description: Export chart as PNG while you convert Excel to HTML using Aspose.Cells.
    Learn to embed images as Base64 and save workbook as HTML in minutes.
  name: Export Chart as PNG – Complete Guide to Convert Excel to HTML with Aspose.Cells
  steps:
  - name: Open Visual Studio and create a new **Console App** (`dotnet new console`).
    text: Open Visual Studio and create a new **Console App** (`dotnet new console`).
  - name: 'Add the Aspose.Cells NuGet package:'
    text: 'Add the Aspose.Cells NuGet package:'
  - name: '(Optional) If you have a license file, place it in the project root and
      activate it at runtime:'
    text: '(Optional) If you have a license file, place it in the project root and
      activate it at runtime:'
  - name: Open the generated HTML in Chrome. Right‑click the chart image and select
      **Open image in new tab**. The URL will still start with `data:image/png;base64,`.
    text: Open the generated HTML in Chrome. Right‑click the chart image and select
      **Open image in new tab**. The URL will still start with `data:image/png;base64,`.
  - name: 'If the image appears blurry, consider increasing the chart’s resolution
      before saving:'
    text: 'If the image appears blurry, consider increasing the chart’s resolution
      before saving:'
  - name: 'For charts that rely on external data sources, make sure the workbook is
      fully refreshed before saving:'
    text: 'For charts that rely on external data sources, make sure the workbook is
      fully refreshed before saving:'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Экспорт диаграммы в PNG – Полное руководство по конвертации Excel в HTML с
  помощью Aspose.Cells
url: /ru/net/chart-rendering-and-conversion/export-chart-as-png-complete-guide-to-convert-excel-to-html/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Экспорт диаграммы в PNG – Полное руководство по конвертации Excel в HTML с помощью Aspose.Cells

Вы когда‑нибудь задумывались, как **export chart as PNG** напрямую из рабочей книги Excel, одновременно преобразовав весь лист в чистый, адаптивный HTML? Вы не одиноки. Многие разработчики сталкиваются с проблемой, когда им нужен веб‑готовый отчет, отображающий диаграммы без необходимости управлять отдельными файловыми изображениями. Хорошая новость в том, что Aspose.Cells делает это проще простого.

В этом руководстве мы пройдём по точным шагам, чтобы **convert Excel to HTML**, **embed images as Base64**, а в конце **save workbook as HTML** — при этом каждый график будет сохранён как PNG‑изображение. К концу вы получите один HTML‑файл, который можно вставить в любую веб‑страницу, и все диаграммы появятся мгновенно, без дополнительных ресурсов.

## Что вы узнаете

- Как загрузить существующую рабочую книгу, уже содержащую диаграммы.  
- Какие флаги `HtmlSaveOptions` управляют экспортом изображений, форматом диаграмм и адаптивностью.  
- Точный код, необходимый для **export chart as PNG** и встраивания этих PNG‑файлов как строк Base64.  
- Как **save workbook as HTML** одним вызовом метода.  
- Советы по устранению распространённых проблем, таких как отсутствие изображений диаграмм или слишком большие строки Base64.  

**Prerequisites:**  
- .NET 6+ (или .NET Framework 4.6+) установлен.  
- Действительная лицензия Aspose.Cells (или временный ключ оценки).  
- Базовые знания C# и Visual Studio (или вашей любимой IDE).  

Если что‑то из перечисленного вам незнакомо, сделайте паузу и подготовьте всё необходимое; остальная часть руководства предполагает, что всё готово.

---

## Шаг 1: Настройте проект и установите Aspose.Cells

Прежде чем мы сможем **export chart as PNG**, нам нужен проект C#, ссылающийся на библиотеку Aspose.Cells.

1. Откройте Visual Studio и создайте новое **Console App** (`dotnet new console`).  
2. Добавьте пакет Aspose.Cells через NuGet:

```bash
dotnet add package Aspose.Cells
```

3. (Опционально) Если у вас есть файл лицензии, поместите его в корень проекта и активируйте во время выполнения:

```csharp
// Activate license – skip this line if you’re using the trial version
Aspose.Cells.License license = new Aspose.Cells.License();
license.SetLicense("Aspose.Cells.lic");
```

> **Pro tip:** Держите файл лицензии вне системы контроля версий. Для продакшна используйте переменные окружения или безопасные хранилища секретов.

---

## Шаг 2: Загрузите рабочую книгу, содержащую диаграмму

Теперь загрузим Excel‑файл, в котором уже есть нужная нам диаграмма для **export chart as PNG**.

```csharp
using Aspose.Cells;
using System.Drawing.Imaging;   // Needed for ImageFormat enum

// Path to the source workbook – change this to your actual file location
string sourcePath = @"C:\Reports\ReportWithChart.xlsx";

// Load the workbook
Workbook workbook = new Workbook(sourcePath);
```

> **Почему это важно:** Загрузка книги на раннем этапе даёт доступ ко всем листам, диаграммам и встроенным объектам. Если загрузка не удалась, последующий шаг **export chart to PNG** никогда не выполнится.

---

## Шаг 3: Настройте параметры сохранения HTML

Сердце решения находится в `HtmlSaveOptions`. Переключив несколько свойств, мы можем:

- **ExportChartImageFormat = ImageFormat.Png** → гарантирует, что каждая диаграмма будет PNG.  
- **ExportImagesAsBase64 = true** → встраивает данные PNG напрямую в HTML, устраняя внешние файлы.  
- **IsResponsive = true** → делает сгенерированные таблицы адаптивными для мобильных экранов.  
- **ExportPrintingHeadersFooters = false** → убирает лишние метаданные печати.  

Вот полная конфигурация:

```csharp
// Create HTML save options and fine‑tune them
HtmlSaveOptions htmlOptions = new HtmlSaveOptions
{
    // 1️⃣ Embed PNG/JPEG images directly as Base64 strings
    ExportImagesAsBase64 = true,

    // 2️⃣ Force chart images to be saved as PNG files
    ExportChartImageFormat = ImageFormat.Png,

    // 3️⃣ Omit printing headers/footers for a cleaner web view
    ExportPrintingHeadersFooters = false,

    // 4️⃣ Generate responsive tables for mobile friendliness
    IsResponsive = true,

    // 5️⃣ Target modern browsers with HTML5
    HtmlVersion = HtmlVersion.Html5
};
```

### Почему именно эти настройки?

- **ExportChartImageFormat = ImageFormat.Png** — единственный способ гарантировать без потерь, веб‑безопасный формат изображения диаграммы.  
- **ExportImagesAsBase64 = true** — позволяет **embed images as Base64**, что идеально подходит для email‑отчётов или развертываний в виде одного файла.  
- **IsResponsive = true** решает частую проблему: таблицы, выходящие за пределы экрана смартфонов.  
- **ExportPrintingHeadersFooters = false** делает HTML лёгким — без скрытой информации о печати, которая никогда не используется в вебе.  

---

## Шаг 4: Сохраните рабочую книгу как HTML

С установленными параметрами последняя строка — один вызов, который одновременно **convert excel to html** и **export chart as PNG** в фоновом режиме.

```csharp
// Destination HTML file – adjust the folder as needed
string outputPath = @"C:\Reports\Report.html";

// Save the workbook using the configured options
workbook.Save(outputPath, htmlOptions);
```

После выполнения этой строки у вас появится файл `Report.html`. Откройте его в любом браузере, и вы увидите:

- Все данные листов, отрендеренные в виде чистых HTML‑таблиц.  
- Каждая диаграмма отображается как встроенное PNG‑изображение (благодаря Base64).  
- Нет дополнительных файлов изображений рядом с HTML.  

### Ожидаемый результат

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <title>Report</title>
    <style>
        /* Aspose.Cells generated responsive CSS */
    </style>
</head>
<body>
    <table class="aspose">
        <!-- Table rows here -->
    </table>

    <!-- Example of an embedded chart image -->
    <img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAA..." alt="Chart 1" />
</body>
</html>
```

Обратите внимание на атрибут `src="data:image/png;base64,..."` — это магия **embed images as base64**. Отдельные файлы `.png` на диск не создаются.

---

## Шаг 5: Проверьте экспорт PNG и при необходимости подправьте

Иногда после конвертации диаграмма может выглядеть слегка искажённой, особенно если использованы пользовательские шрифты или сложные градиенты. Как проверить:

1. Откройте сгенерированный HTML в Chrome. Щёлкните правой кнопкой по изображению диаграммы и выберите **Open image in new tab**. URL всё равно будет начинаться с `data:image/png;base64,`.  
2. Если изображение размыто, рассмотрите возможность увеличения разрешения диаграммы перед сохранением:

```csharp
htmlOptions.ImageResolution = 300; // DPI – higher values = sharper PNGs
```

3. Для диаграмм, зависящих от внешних источников данных, убедитесь, что рабочая книга полностью обновлена перед сохранением:

```csharp
workbook.CalculateFormula(); // Force recalculation
```

Эти настройки гарантируют, что шаг **export excel chart to png** даст чёткую, готовую к продакшну графику.

---

## Шаг 6: Разместите HTML где угодно

Поскольку все изображения встроены, теперь вы можете:

- Отправить HTML как единственное вложение в письме.  
- Вставить HTML в CMS, принимающую «сырой» код.  
- Разместить его на статическом сайте, не беспокоясь о потерянных PNG‑файлах.  

Если вам всё же нужны отдельные PNG‑файлы (например, для последующего PDF), можно переключить `ExportImagesAsBase64` на `false` и указать `HtmlSaveOptions` папку вывода для изображений.

```csharp
htmlOptions.ExportImagesAsBase64 = false;
htmlOptions.ImageFolder = @"C:\Reports\Images";
```

Теперь HTML будет ссылаться на внешние PNG‑файлы, всё равно обеспечивая **export chart as png**, но предоставляя отдельные изображения для других целей.

---

## Распространённые проблемы и как их избежать

| Symptom | Likely Cause | Fix |
|---------|--------------|-----|
| Диаграмма отсутствует в HTML | `ExportChartImageFormat` оставлен по умолчанию (`Jpeg`) и браузер блокирует смешанный контент. | Установите `ExportChartImageFormat = ImageFormat.Png`. |
| HTML‑файл огромный (несколько МБ) | Большие диаграммы или множество изображений высокого разрешения, встроенных как Base64. | Уменьшите `htmlOptions.ImageResolution` или сожмите диаграмму в Excel перед конвертацией. |
| Таблицы выходят за пределы экрана на мобильных | `IsResponsive` не включён. | Убедитесь, что `IsResponsive = true` в `HtmlSaveOptions`. |
| Строки Base64 содержат символы переноса строки | Старые версии .NET могут переносить длинные строки. | Обновитесь до .NET 6+ или установите `htmlOptions.ExportBase64StringInOneLine = true`. |

---

## Бонус: Оберните всё в переиспользуемый метод

Если вам придётся выполнять эту конверсию часто, вынесите логику в отдельный метод:

```csharp
public static void ConvertExcelToHtmlWithPngCharts(string excelPath, string htmlPath)
{
    // Load workbook
    Workbook wb = new Workbook(excelPath);

    // Prepare options
    HtmlSaveOptions opts = new HtmlSaveOptions
    {
        ExportImagesAsBase64 = true,
        ExportChartImageFormat = ImageFormat.Png,
        ExportPrintingHeadersFooters = false,
        IsResponsive = true,
        HtmlVersion = HtmlVersion.Html5,
        ImageResolution = 150 // reasonable default DPI
    };

    // Force recalculation for up‑to‑date charts
    wb.CalculateFormula();

    // Save as HTML
    wb.Save(htmlPath, opts);
}
```

Теперь вы можете вызвать `ConvertExcelToHtmlWithPngCharts(@"C:\Reports\MyFile.xlsx", @"C:\Reports\MyFile.html");` из любой части вашего кода.

---

## Заключение

Вы только что освоили, как **export chart as PNG** одновременно с **convert Excel to HTML**, **embed images as Base64** и **save workbook as HTML** с помощью Aspose.Cells. Главный вывод — несколько правильно выбранных параметров `HtmlSaveOptions` дают один самодостаточный HTML‑файл, работающий на любом устройстве, без лишних PNG‑файлов и беспорядочных папок.

Готовы к следующему вызову? Попробуйте сочетать этот подход с **export excel chart to PNG** для генерации PDF, либо поэкспериментируйте с пользовательским CSS для стилизации таблиц. Возможности безграничны, когда вы контролируете и данные, и их представление программно.

Не стесняйтесь оставить комментарий, если столкнётесь с трудностями, или поделиться тем, как вы адаптировали этот шаблон в своих проектах. Happy coding!

## Что стоит изучить дальше?

Следующие руководства охватывают тесно связанные темы, расширяющие техники, продемонстрированные в этом пособии. Каждый ресурс содержит полностью работающие примеры кода с пошаговыми объяснениями, помогающими вам освоить дополнительные возможности API и исследовать альтернативные подходы в собственных проектах.

- [Export Excel to HTML Using Aspose.Cells for .NET: A Complete Guide](/cells/english/net/workbook-operations/export-excel-html-aspose-cells-net/)
- [Export Excel to HTML Without Frame Scripts Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/export-excel-to-html-aspose-cells-net/)
- [How to Export an Excel Worksheet to PNG Using Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-to-png-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}