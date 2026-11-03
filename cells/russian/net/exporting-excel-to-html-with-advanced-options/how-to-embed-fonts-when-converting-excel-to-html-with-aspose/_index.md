---
category: general
date: 2026-10-01
description: Узнайте, как встраивать шрифты в HTML при конвертации Excel в HTML с
  помощью Aspose.Cells. Экспортируйте Excel в HTML с встроенными шрифтами за несколько
  шагов.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to embed fonts
- convert excel to html
- embed fonts in html
- how to export excel
- export excel as html
language: ru
lastmod: 2026-10-01
og_description: Как внедрять шрифты в HTML при экспорте файлов Excel. Следуйте этому
  пошаговому руководству, чтобы преобразовать Excel в HTML с внедрёнными шрифтами.
og_image_alt: Screenshot of Aspose.Cells code embedding fonts in exported HTML
og_title: Как встроить шрифты в HTML из Excel – руководство Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Learn how to embed fonts in HTML while converting Excel to HTML using
    Aspose.Cells. Export Excel as HTML with embedded fonts in a few steps.
  headline: How to embed fonts when converting Excel to HTML with Aspose.Cells
  type: TechArticle
- description: Learn how to embed fonts in HTML while converting Excel to HTML using
    Aspose.Cells. Export Excel as HTML with embedded fonts in a few steps.
  name: How to embed fonts when converting Excel to HTML with Aspose.Cells
  steps:
  - name: 'Edge case: unsupported fonts'
    text: If the workbook uses a font that is not installed on the server, Aspose.Cells
      falls back to a default system font. To avoid this, install the required fonts
      on the server or embed them manually after export.
  - name: Converting multiple worksheets
    text: If you need to **convert Excel to HTML** for all worksheets, set `ExportActiveWorksheetOnly
      = false` (the default). Aspose.Cells will create a separate HTML file for each
      sheet.
  - name: Controlling CSS output
    text: 'You can reduce the HTML size by disabling inline CSS:'
  - name: Using a stream instead of a file
    text: 'When integrating into a web API, write the HTML to a `MemoryStream` and
      return it directly:'
  type: HowTo
tags:
- Aspose.Cells
- .NET
- Excel conversion
title: Как встроить шрифты при конвертации Excel в HTML с помощью Aspose.Cells
url: /ru/net/exporting-excel-to-html-with-advanced-options/how-to-embed-fonts-when-converting-excel-to-html-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как внедрять шрифты при конвертации Excel в HTML с помощью Aspose.Cells

Внедрение шрифтов в HTML при конвертации книги Excel является важным для сохранения оригинального вида в разных браузерах. Если вам нужно конвертировать Excel в HTML, сохранив пользовательские шрифты, это руководство покажет полный процесс. Вы также увидите, как экспортировать Excel как HTML и почему внедрение шрифтов в HTML имеет значение для согласованного отображения.

В этом учебнике рассматривается всё, что вам необходимо знать: требуемые библиотеки, настройка кода и проверка сгенерированного HTML‑файла. К концу вы сможете экспортировать Excel как HTML с внедрёнными шрифтами всего в несколько строк C#.

## Что вам понадобится

Прежде чем начать, убедитесь, что у вас есть:

* **.NET 6.0 или новее** – код ориентирован на .NET 6, но любой .NET‑версии, поддерживающей Aspose.Cells, достаточно.
* **Aspose.Cells for .NET** – получите лицензию или используйте бесплатную оценочную версию с сайта Aspose.
* **C#‑среда разработки** (Visual Studio, Rider или VS Code) – любой IDE, способный компилировать .NET‑проекты.
* Книга Excel (`Styled.xlsx`), использующая пользовательские шрифты, которые вы хотите сохранить.

## Шаг 1: Настройте Aspose.Cells в вашем .NET проекте

Сначала добавьте пакет Aspose.Cells через NuGet в ваш проект:

```bash
dotnet add package Aspose.Cells
```

Затем подключите пространство имён в начале вашего C#‑файла:

```csharp
using Aspose.Cells;
```

Добавление пакета делает доступными классы `Workbook`, `HtmlSaveOptions` и связанные с ними.

## Шаг 2: Загрузите книгу Excel

Загрузка книги — первый конкретный шаг в **как экспортировать данные Excel**. Конструктор `Workbook` читает файл с диска:

```csharp
// Step 1: Load the Excel workbook
var workbook = new Workbook("YOUR_DIRECTORY/Styled.xlsx");
```

*Почему это важно:* Aspose.Cells разбирает книгу, включая стили ячеек, формулы и информацию о шрифтах. Если файл не найден, будет выброшено исключение, поэтому убедитесь, что путь указан правильно.

## Шаг 3: Настройте параметры сохранения HTML для внедрения шрифтов

Ядром **внедрения шрифтов в html** является класс `HtmlSaveOptions`. Установите `EmbedFonts` в `true`, чтобы каждый шрифт, использованный в книге, был записан в HTML‑вывод как правило `@font-face`, закодированное в Base64.

```csharp
// Step 2: Set HTML save options to embed fonts in the output
var htmlOptions = new HtmlSaveOptions
{
    EmbedFonts = true,
    // Optional: keep the original worksheet name as the HTML file name
    ExportActiveWorksheetOnly = true
};
```

*Почему это важно:* По умолчанию Aspose.Cells ссылается на внешние файлы шрифтов, которые могут отсутствовать на клиентском компьютере. Включение `EmbedFonts` гарантирует, что отрендеренный HTML выглядит идентично оригинальному листу Excel, независимо от установленных шрифтов у пользователя.

### Пограничный случай: неподдерживаемые шрифты

Если книга использует шрифт, не установленный на сервере, Aspose.Cells переключится на шрифт системы по умолчанию. Чтобы этого избежать, установите необходимые шрифты на сервере или внедрите их вручную после экспорта.

## Шаг 4: Сохраните книгу как HTML, используя настроенные параметры

Теперь можно записать HTML‑файл. Метод `Save` принимает путь вывода и экземпляр `HtmlSaveOptions`:

```csharp
// Step 3: Save the workbook as an HTML file using the configured options
workbook.Save("YOUR_DIRECTORY/Styled.html", htmlOptions);
```

После выполнения `Styled.html` будет содержать данные таблицы и блок `<style>` с Base64‑закодированными определениями `@font-face` для каждого пользовательского шрифта.

## Шаг 5: Проверьте внедрённые шрифты

Откройте `Styled.html` в браузере. Проверьте раздел `<head>` — вы должны увидеть что‑то вроде:

```html
<style>
@font-face {
    font-family: 'Calibri';
    src: url(data:font/ttf;base64,AAEAAAARAQAABAA...);
}
...
</style>
```

Если шрифты отображаются корректно в отрисованной таблице, внедрение прошло успешно. Если заметны отсутствующие глифы, ещё раз проверьте, что исходные файлы шрифтов установлены на машине, где происходит конверсия.

## Общие варианты и дополнительные параметры

### Конвертация нескольких листов

Если нужно **конвертировать Excel в HTML** для всех листов, установите `ExportActiveWorksheetOnly = false` (значение по умолчанию). Aspose.Cells создаст отдельный HTML‑файл для каждого листа.

```csharp
htmlOptions.ExportActiveWorksheetOnly = false;
workbook.Save("YOUR_DIRECTORY/AllSheets.html", htmlOptions);
```

### Управление выводом CSS

Можно уменьшить размер HTML, отключив встроенный CSS:

```csharp
htmlOptions.ExportCssSeparately = true; // Generates a .css file alongside the .html
```

### Использование потока вместо файла

При интеграции в веб‑API запишите HTML в `MemoryStream` и верните его напрямую:

```csharp
using var stream = new MemoryStream();
workbook.Save(stream, htmlOptions);
stream.Position = 0; // Reset for reading
// Return stream as a file download in ASP.NET Core
```

## Совет профессионала: лицензируйте продукт, чтобы убрать водяные знаки оценки

Если вы используете оценочную версию, сгенерированный HTML может содержать комментарий‑водяной знак. Примените вашу лицензию Aspose.Cells перед загрузкой книги, чтобы получить чистый вывод:

```csharp
var license = new License();
license.SetLicense("Aspose.Total.lic");
```

## Полный рабочий пример

Ниже приведена полностью готовая к запуску программа, демонстрирующая **как внедрять шрифты**, **конвертировать excel в html** и **экспортировать excel как html** в одном процессе:

```csharp
using System;
using Aspose.Cells;

class ExcelToHtmlWithEmbeddedFonts
{
    static void Main()
    {
        // Apply license if you have one (optional)
        // var license = new License();
        // license.SetLicense("Aspose.Total.lic");

        // 1️⃣ Load the Excel workbook
        var workbookPath = @"YOUR_DIRECTORY/Styled.xlsx";
        var workbook = new Workbook(workbookPath);

        // 2️⃣ Configure HTML save options to embed fonts
        var htmlOptions = new HtmlSaveOptions
        {
            EmbedFonts = true,
            ExportActiveWorksheetOnly = true, // Export only the first sheet
            ExportCssSeparately = false        // Keep CSS inline for a single file
        };

        // 3️⃣ Save as HTML
        var htmlPath = @"YOUR_DIRECTORY/Styled.html";
        workbook.Save(htmlPath, htmlOptions);

        Console.WriteLine($"Excel workbook '{workbookPath}' has been exported to HTML with embedded fonts at '{htmlPath}'.");
    }
}
```

**Ожидаемый результат:** После запуска программы `Styled.html` появится в `YOUR_DIRECTORY`. Открытие файла в любом современном браузере покажет таблицу с теми же шрифтами, что и в оригинальном файле Excel, даже на компьютерах, где этих шрифтов нет.

## Заключение

Теперь вы знаете **как внедрять шрифты** при **конвертации Excel в HTML** с помощью Aspose.Cells, и видели полный процесс от загрузки книги до проверки внедрённых шрифтов. Такой подход гарантирует сохранение визуального соответствия ваших Excel‑файлов в сгенерированном HTML, что идеально подходит для веб‑отчётов, email‑рассылок или любых сценариев, где необходимо **экспортировать Excel как HTML** с пользовательской типографикой.

Далее изучайте связанные темы, такие как **экспорт Excel в PDF**, **стилизация HTML‑вывода пользовательским CSS** или **пакетная обработка нескольких книг**. Все они опираются на тот же шаблон `HtmlSaveOptions`, поэтому вы сможете адаптировать код с минимальными изменениями.

Happy coding!

## Что вам следует изучить дальше?

Следующие учебники охватывают тесно связанные темы, построенные на техниках, продемонстрированных в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы в ваших проектах.

- [How to Export Excel to HTML – Step‑by‑Step Guide](/cells/english/net/exporting-excel-to-html-with-advanced-options/how-to-export-excel-to-html-step-by-step-guide/)
- [How to Embed Fonts in HTML – Complete C# Guide](/cells/english/net/exporting-excel-to-html-with-advanced-options/how-to-embed-fonts-in-html-complete-c-guide/)
- [How to embed fonts when converting Excel to PDF – Step‑by‑Step Guide](/cells/english/net/conversion-to-pdf/how-to-embed-fonts-when-converting-excel-to-pdf-step-by-step/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}