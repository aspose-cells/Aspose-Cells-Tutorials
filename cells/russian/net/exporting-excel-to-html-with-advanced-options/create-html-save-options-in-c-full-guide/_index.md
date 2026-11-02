---
category: general
date: 2026-06-08
description: Создайте параметры сохранения HTML в C# для встраивания всех шрифтов
  и сохранения книги в формате HTML. Узнайте, как экспортировать книгу Excel в HTML
  с простым полным примером.
draft: false
keywords:
- create html save options
- save workbook as html
- export excel workbook to html
- embed all fonts in html
language: ru
og_description: Создайте параметры сохранения HTML в C#, чтобы встроить все шрифты
  и экспортировать книгу Excel в HTML. Это руководство проведёт вас через полное готовое
  к запуску решение.
og_title: Создание параметров сохранения HTML в C# – Полный учебник
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Create HTML save options in C# to embed all fonts and save workbook
    as HTML. Learn how to export Excel workbook to HTML with a simple, complete example.
  headline: Create HTML Save Options in C# – Full Guide
  type: TechArticle
- description: Create HTML save options in C# to embed all fonts and save workbook
    as HTML. Learn how to export Excel workbook to HTML with a simple, complete example.
  name: Create HTML Save Options in C# – Full Guide
  steps:
  - name: Expected Output
    text: Running the program produces `EmbeddedWorkbook.html` in the execution folder.
      Open it in any modern browser and you’ll see the text **“Hello, Aspose.Cells!”**
      rendered in **Comic Sans MS**, even if your system doesn’t have that font installed.
      Inspect the HTML source and you’ll notice a `<style>` bl
  - name: What if the workbook contains many different fonts?
    text: Embedding *all* fonts can inflate the HTML size dramatically (each font
      is Base64‑encoded). If file size becomes a concern, consider setting `EmbedAllFonts
      = false` and manually embedding only the critical fonts via `htmlOptions.FontEmbeddingMode
      = FontEmbeddingMode.Custom;`.
  - name: Does this work with older Excel files (`.xls`)?
    text: Absolutely. Aspose.Cells abstracts the source format, so whether you load
      an `.xlsx`, `.xls`, or even a CSV, the **export excel workbook to html** step
      behaves the same.
  - name: Can I control the output folder dynamically?
    text: 'Sure thing—just replace the hard‑coded `outputPath` with something like:'
  - name: What about images or charts inside the workbook?
    text: '`HtmlSaveOptions` also handles images, charts, and even formulas. By default
      they’re rendered as PNGs embedded in the HTML. If you prefer external files,
      toggle `htmlOptions.ExportImagesAsBase64 = false`.'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel Export
- HTML Export
title: Создание параметров сохранения HTML в C# – Полное руководство
url: /ru/net/exporting-excel-to-html-with-advanced-options/create-html-save-options-in-c-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание параметров сохранения HTML в C# – Полный учебник

Вы когда‑нибудь задумывались, как **создать параметры сохранения HTML**, которые сохраняют каждый шрифт точно таким же, как в Excel? Вы не одиноки. Многие разработчики сталкиваются с проблемой, когда экспортированный HTML теряет пользовательские шрифты, делая страницу скучной. Хорошая новость? Пара строк кода на C# позволяют **встроить все шрифты в HTML** и **сохранить книгу как HTML** без проблем.

В этом руководстве мы пройдем весь процесс **экспорта книги Excel в HTML** с использованием Aspose.Cells. К концу вы получите автономную, готовую к запуску программу, которая не только создаёт нужные параметры, но и объясняет *почему* каждую настройку важно учитывать. Никаких недостающих частей, никаких «см. документацию» отклонений — только чёткое решение от начала до конца.

## Требования

Перед тем как начать, убедитесь, что у вас есть:

* .NET 6.0 SDK (или любая современная версия .NET) — код работает как на .NET Core, так и на .NET Framework.  
* Пакет NuGet **Aspose.Cells** — `dotnet add package Aspose.Cells`.  
* Базовое понимание синтаксиса C# — если вы умеете писать `Console.WriteLine`, вы готовы к работе.  

Это всё. Никаких дополнительных инструментов, никаких скрытых файлов конфигурации.

## Шаг 1: Настройка проекта и загрузка книги

Сначала нам нужен консольный проект и книга, с которой будем работать. Если у вас уже есть файл Excel, отлично — иначе пример создаст его «на лету».

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create a new workbook or load an existing one
        Workbook wb = new Workbook(); // starts with a default sheet

        // Populate the sheet with some styled text so we can see font embedding in action
        var sheet = wb.Worksheets[0];
        var cell = sheet.Cells["A1"];
        cell.PutValue("Hello, Aspose.Cells!");
        var style = cell.GetStyle();
        style.Font.Name = "Comic Sans MS";   // a non‑system font to test embedding
        style.Font.Size = 14;
        cell.SetStyle(style);

        // Continue with HTML export...
```

**Почему мы делаем это:** загрузка книги даёт нам объект для экспорта. Добавление пользовательского шрифта (`Comic Sans MS`) делает настройку *embed all fonts* видимой в сгенерированном HTML.

## Шаг 2: **Создание параметров сохранения HTML** – Суть задачи

Теперь переходим к сердцу задачи: настройке `HtmlSaveOptions`. Этот объект точно указывает Aspose.Cells, как должен быть записан HTML.

```csharp
        // Step 2: Create HTML save options and embed all fonts in the output
        HtmlSaveOptions htmlOptions = new HtmlSaveOptions
        {
            // Setting this to true forces every used font to be base‑64 encoded
            // and placed directly inside the HTML file. No external .ttf files.
            EmbedAllFonts = true,

            // Optional but handy: keep the original Excel formatting
            ExportColumnHeaders = true,
            ExportRowHeaders = true
        };
```

**Почему `EmbedAllFonts = true` важно:** когда вы открываете полученный HTML в браузере, пользовательские шрифты уже встроены в файл. Это значит, что страница выглядит идентично исходному Excel, даже на машинах, где шрифт не установлен.

## Шаг 3: **Сохранить книгу как HTML** используя настроенные параметры

С нашими параметрами готовыми, мы наконец‑то можем **сохранить книгу как HTML**. Сигнатура метода принимает путь к файлу, желаемый формат и объект параметров, который мы только что создали.

```csharp
        // Step 3: Save the workbook as an HTML file using the configured options
        string outputPath = "EmbeddedWorkbook.html";
        wb.Save(outputPath, SaveFormat.Html, htmlOptions);

        Console.WriteLine($"Workbook successfully exported to {outputPath}");
    }
}
```

**Что происходит «под капотом»?** Aspose.Cells рендерит каждую ячейку, преобразует определения шрифтов в Base64 и внедряет их в блок `<style>`. Полученный `EmbeddedWorkbook.html` — единственный, автономный файл — без отдельных `.css` или файлов шрифтов.

## Полный рабочий пример

Объединив всё вместе, представляем полностью готовую программу, которую можно скопировать в `Program.cs` и запустить:

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create or load a workbook
        Workbook wb = new Workbook();
        var sheet = wb.Worksheets[0];
        var cell = sheet.Cells["A1"];
        cell.PutValue("Hello, Aspose.Cells!");
        var style = cell.GetStyle();
        style.Font.Name = "Comic Sans MS"; // non‑standard font for testing
        style.Font.Size = 14;
        cell.SetStyle(style);

        // 2️⃣ Create HTML save options – embed all fonts
        HtmlSaveOptions htmlOptions = new HtmlSaveOptions
        {
            EmbedAllFonts = true,
            ExportColumnHeaders = true,
            ExportRowHeaders = true
        };

        // 3️⃣ Save workbook as HTML
        string outputPath = "EmbeddedWorkbook.html";
        wb.Save(outputPath, SaveFormat.Html, htmlOptions);

        Console.WriteLine($"Workbook successfully exported to {outputPath}");
    }
}
```

### Ожидаемый результат

Запуск программы создаёт `EmbeddedWorkbook.html` в папке выполнения. Откройте его в любом современном браузере, и вы увидите текст **«Hello, Aspose.Cells!»**, отрисованный **Comic Sans MS**, даже если в системе этот шрифт не установлен. Просмотрите исходный HTML — вы заметите блок `<style>` с правилом `@font-face`, содержащим огромную строку Base64 — это встроенный шрифт.

![Create HTML Save Options diagram](image.png "Диаграмма, показывающая процесс экспорта HTML"){: alt="Схема создания параметров сохранения HTML"}

*Текст alt включает основной ключевой запрос для SEO.*

## Часто задаваемые вопросы и особые случаи

### Что делать, если книга содержит много разных шрифтов?

Встраивание *всех* шрифтов может резко увеличить размер HTML (каждый шрифт кодируется в Base64). Если размер файла становится проблемой, рассмотрите возможность установки `EmbedAllFonts = false` и вручную встраивайте только критически важные шрифты через `htmlOptions.FontEmbeddingMode = FontEmbeddingMode.Custom;`.

### Работает ли это со старыми файлами Excel (`.xls`)?

Абсолютно. Aspose.Cells абстрагирует исходный формат, поэтому независимо от того, загружаете вы `.xlsx`, `.xls` или даже CSV, шаг **экспорта книги Excel в HTML** ведёт себя одинаково.

### Можно ли управлять папкой вывода динамически?

Конечно — просто замените жёстко заданный `outputPath` на что‑то вроде:

```csharp
string outputPath = Path.Combine(Environment.CurrentDirectory, "Reports", "MyExport.html");
Directory.CreateDirectory(Path.GetDirectoryName(outputPath));
```

Таким образом вы сможете **сохранить книгу как HTML** в любой нужной вам папке.

### Что насчёт изображений или диаграмм внутри книги?

`HtmlSaveOptions` также обрабатывает изображения, диаграммы и даже формулы. По умолчанию они рендерятся как PNG, встроенные в HTML. Если вы предпочитаете внешние файлы, переключите `htmlOptions.ExportImagesAsBase64 = false`.

## Профессиональные советы

* **Совет по производительности:** переиспользуйте один экземпляр `HtmlSaveOptions`, если экспортируете множество книг в цикле — будет меньше «мусора».  
* **Совет по тестированию:** используйте безголовый браузер (например, Puppeteer) для автоматической проверки корректного отображения встроенных шрифтов.  
* **Проверка версии:** флаг `EmbedAllFonts` был введён в Aspose.Cells 20.9. Убедитесь, что ваш пакет NuGet обновлён до последней версии.

## Заключение

Теперь вы точно знаете, как **создать параметры сохранения HTML** в C#, которые **встраивают все шрифты в HTML**, и видели практический способ **сохранить книгу как HTML** для любого файла Excel. Этот полный, готовый к запуску пример охватывает *что*, *почему* и *как* **экспорта книги Excel в HTML**, предоставляя надёжную основу для более сложных сценариев, таких как пакетная обработка или пользовательское стилизование.

Готовы к следующему шагу? Попробуйте экспортировать книгу, содержащую диаграммы, или поэкспериментируйте с различными свойствами `HtmlSaveOptions`, например `ExportImagesAsBase64` или `CssClassPrefix`. Тот же шаблон применяется — создаёте параметры, меняете флаги и вызываете `wb.Save`. Приятного кодинга, и пусть ваши HTML‑экспорты всегда выглядят точно так же, как оригинальные листы Excel!

## Что изучать дальше?

Следующие учебники охватывают тесно связанные темы, построенные на техниках, продемонстрированных в этом руководстве. Каждый ресурс включает полные работающие примеры кода с пошаговыми объяснениями, помогая вам освоить дополнительные возможности API и исследовать альтернативные подходы в ваших проектах.

- [Добавление префикса к стилям элементов таблицы с помощью параметров сохранения HTML](/cells/english/net/exporting-excel-to-html-with-advanced-options/prefixing-table-elements-styles/)
- [Установка шрифта по умолчанию при конвертации Excel в HTML с Aspose.Cells для .NET \| Руководство по операциям с книгой](/cells/english/net/workbook-operations/excel-html-conversion-default-font-aspose-cells-net/)
- [Экспорт свойств книги и листа Excel в HTML с помощью Aspose.Cells для .NET](/cells/english/net/workbook-operations/export-excel-properties-to-html-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}