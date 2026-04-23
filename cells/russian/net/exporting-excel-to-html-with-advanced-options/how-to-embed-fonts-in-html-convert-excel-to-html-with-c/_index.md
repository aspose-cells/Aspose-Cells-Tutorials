---
category: general
date: 2026-03-01
description: Узнайте, как внедрять шрифты в HTML при конвертации Excel в HTML с помощью
  Aspose.Cells. Это пошаговое руководство также показывает, как сохранять Excel в
  формате HTML.
draft: false
keywords:
- how to embed fonts
- embed fonts in html
- convert excel to html
- create html from excel
- save excel as html
language: ru
og_description: Как внедрить шрифты в HTML при экспорте Excel в HTML. Следуйте этому
  полному руководству, чтобы сохранить типографику во всех браузерах.
og_title: Как внедрить шрифты в HTML – Быстрое руководство по C#
tags:
- Aspose.Cells
- C#
- HTML export
title: Как встраивать шрифты в HTML – Конвертировать Excel в HTML с помощью C#
url: /ru/net/exporting-excel-to-html-with-advanced-options/how-to-embed-fonts-in-html-convert-excel-to-html-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как внедрить шрифты в HTML – Конвертировать Excel в HTML с помощью C#

Когда‑нибудь задавались вопросом **как внедрить шрифты в HTML**, чтобы ваша конверсия Excel‑в‑HTML выглядела пиксель‑идеально? Вы не одиноки. При экспорте рабочей книги в HTML по умолчанию используются системные шрифты, что может нарушить макет на компьютерах, где эти шрифты не установлены.  

Включив внедрение шрифтов, вы гарантируете, что вывод сохраняет оригинальную типографику, независимо от того, где он просматривается. В этом руководстве мы пройдём по точным шагам **внедрения шрифтов в HTML** с помощью Aspose.Cells for .NET, а также коснёмся связанных задач, таких как **конвертировать Excel в HTML**, **создать HTML из Excel** и **сохранить Excel как HTML**.

## Что вы узнаете

- Почему внедрение шрифтов важно для кросс‑браузерной согласованности.  
- Точный код C#, необходимый для включения **embed fonts in html** при сохранении рабочей книги.  
- Как обрабатывать распространённые крайние случаи, такие как большие файлы шрифтов или ограничения лицензирования.  
- Быстрые шаги проверки, чтобы убедиться, что шрифты действительно внедрены.

### Предварительные требования

- .NET 6.0 или новее (код также работает с .NET Framework 4.6+).  
- Установленный NuGet‑пакет Aspose.Cells for .NET (`Install-Package Aspose.Cells`).  
- Базовое понимание C# и работы с файлами Excel.  
- По крайней мере один пользовательский TrueType/OpenType шрифт, используемый в вашей рабочей книге.

> **Pro tip:** Если вы используете Visual Studio, включите “Nullable reference types”, чтобы заранее отлавливать потенциальные проблемы с null.

---

## Шаг 1: Настройте проект и загрузите рабочую книгу

Сначала создайте новое консольное приложение (или интегрируйте код в существующее решение). Затем добавьте пространство имён Aspose.Cells.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Load an existing Excel file that uses custom fonts
        string sourcePath = @"C:\Temp\Report.xlsx";
        Workbook wb = new Workbook(sourcePath);
```

*Почему это важно:* Загрузка рабочей книги даёт библиотеке доступ к стилям ячеек, включая информацию о шрифте, которую мы позже захотим внедрить.

---

## Шаг 2: Создайте **HtmlSaveOptions** и включите внедрение шрифтов

Класс `HtmlSaveOptions` управляет каждым аспектом экспорта в HTML. Установка `EmbedFonts = true` сообщает Aspose.Cells внедрять необходимые файлы шрифтов непосредственно в HTML (в виде Base64‑закодированных data‑URL).

```csharp
        // Step 2: Create HTML save options
        HtmlSaveOptions htmlOptions = new HtmlSaveOptions();

        // Enable embedding of fonts in the saved HTML
        htmlOptions.EmbedFonts = true;

        // Optional: Reduce the size of embedded fonts by subsetting
        htmlOptions.SubsetEmbeddedFonts = true;
```

*Почему мы включаем `SubsetEmbeddedFonts`*: Он удаляет неиспользуемые глифы, уменьшая конечный HTML‑файл — особенно полезно при работе с большими семействами шрифтов.

---

## Шаг 3: Выберите папку вывода и сохраните HTML

Теперь решите, куда должен попасть файл HTML. Aspose.Cells также создаст папку для вспомогательных ресурсов (изображения, CSS и т.д.).  

```csharp
        // Define output location
        string outputFolder = @"C:\Temp\ExportedHtml";
        string outputFile = System.IO.Path.Combine(outputFolder, "Report.html");

        // Ensure the folder exists
        System.IO.Directory.CreateDirectory(outputFolder);

        // Step 3: Save the workbook as HTML with the configured options
        wb.Save(outputFile, htmlOptions);

        Console.WriteLine($"HTML file with embedded fonts saved to: {outputFile}");
    }
}
```

*Что вы увидите:* Откройте полученный `Report.html` в любом браузере. Пользовательские шрифты должны отображаться корректно, даже если шрифт не установлен на машине.

---

## Шаг 4: Проверьте, действительно ли шрифты внедрены

Быстрый способ подтвердить внедрение — просмотреть сгенерированный HTML‑файл. Ищите блоки `<style>`, содержащие правила `@font-face` с `src: url(data:font/ttf;base64,…)`.  

```html
/* Example snippet from the output */
@font-face {
    font-family: 'MyCustomFont';
    src: url(data:font/ttf;base64,AAEAAAARAQAABAA...);
    font-weight: normal;
    font-style: normal;
}
```

Если вы видите URI `data:`, шрифт внедрён. Не должно быть ссылок на внешние файлы `.ttf` или `.woff`.

---

## Часто задаваемые вопросы и крайние случаи

| Вопрос | Ответ |
|----------|--------|
| **Что делать, если моя рабочая книга использует много разных шрифтов?** | Внедрение всех шрифтов может сильно увеличить размер HTML. Используйте `htmlOptions.SubsetEmbeddedFonts = true`, чтобы оставить только нужные глифы, или вручную ограничьте набор шрифтов через `htmlOptions.FontsToEmbed`. |
| **Нужно ли беспокоиться о лицензировании шрифтов?** | Обязательно. Внедрение шрифта в HTML создаёт его копию, распространяемую вместе с вашим контентом. Убедитесь, что у вас есть право распространять шрифт (например, открытые шрифты вроде Google Fonts безопасны). |
| **Будет ли это работать в старых браузерах, таких как IE9?** | Подход с Base64 data‑URI поддерживается начиная с IE8, но имеет ограничение по размеру (~32 KB). Для очень больших шрифтов рассмотрите возможность использования внешних файлов шрифтов, обслуживаемых по HTTP. |
| **Можно ли внедрять шрифты при конвертации Excel в PDF вместо HTML?** | Да — Aspose.Cells также поддерживает `PdfSaveOptions.EmbedStandardFonts` и `PdfSaveOptions.FontEmbeddingMode`. Принцип тот же, только другой API. |
| **Что если мне нужно **create HTML from Excel** на сервере без UI?** | Тот же код работает в ASP.NET Core, Azure Functions или любой безголовой среде — только убедитесь, что процесс имеет права чтения файлов шрифтов. |

---

## Советы по производительности

1. **Кешируйте HTML**, если экспортируете одну и ту же рабочую книгу многократно; шаг внедрения может быть ресурсоёмким.  
2. **Сжимайте папку вывода** (zip) перед передачей по сети; шрифты уже Base64‑закодированы, поэтому zip всё равно сократит несколько килобайт.  
3. **Избегайте внедрения системных шрифтов** (Arial, Times New Roman), если вам не нужна их кастомная версия; браузеры уже имеют их.

---

## Полный рабочий пример (готовый к копированию)

```csharp
using System;
using Aspose.Cells;

class EmbedFontsDemo
{
    static void Main()
    {
        // 1️⃣ Load the workbook (your Excel file must contain custom fonts)
        string excelPath = @"C:\Temp\Sample.xlsx";
        Workbook workbook = new Workbook(excelPath);

        // 2️⃣ Prepare HTML options with font embedding enabled
        HtmlSaveOptions options = new HtmlSaveOptions
        {
            EmbedFonts = true,               // ✅ This is the key line for embedding fonts
            SubsetEmbeddedFonts = true,      // ✅ Reduces file size by keeping only used glyphs
            ExportActiveWorksheetOnly = true // Optional: export just the active sheet
        };

        // 3️⃣ Define where the HTML will be saved
        string outputDir = @"C:\Temp\HtmlExport";
        System.IO.Directory.CreateDirectory(outputDir);
        string htmlPath = System.IO.Path.Combine(outputDir, "Sample.html");

        // 4️⃣ Save the workbook as HTML
        workbook.Save(htmlPath, options);

        Console.WriteLine($"✅ HTML with embedded fonts saved at: {htmlPath}");
    }
}
```

Запуск этой программы создаёт файл `Sample.html`, который **embed fonts in html** и может быть открыт на любом устройстве без потери оригинального вида.

---

## Заключение

Мы рассмотрели **как внедрить шрифты в HTML** при **конвертации Excel в HTML**, обеспечивая визуальную точность вашей рабочей книги после перехода в веб. Включив `HtmlSaveOptions.EmbedFonts` (и при желании `SubsetEmbeddedFonts`), вы получаете автономный HTML‑файл, работающий во всех браузерах, даже на машинах без оригинальных шрифтов.  

Далее вы можете исследовать **create HTML from Excel** для нескольких листов или углубиться в **save Excel as HTML** с пользовательскими CSS‑темами. Оба сценария используют тот же объект `HtmlSaveOptions` — просто настройте свойства, такие как `ExportActiveWorksheetOnly` или `CssStyleSheetType`.

Попробуйте, поиграйте с параметрами, и позвольте внедрённым шрифтам выполнить тяжёлую работу. Если возникнут проблемы, оставляйте комментарий — приятного кодинга!  

![Как внедрить шрифты в HTML пример](https://example.com/images/embed-fonts.png "Как внедрить шрифты в HTML пример")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}