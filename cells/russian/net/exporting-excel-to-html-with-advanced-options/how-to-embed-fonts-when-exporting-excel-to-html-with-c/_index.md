---
category: general
date: 2026-10-10
description: Узнайте, как встраивать шрифты при экспорте Excel в HTML на C#. Это руководство
  охватывает экспорт Excel в HTML, конвертацию Excel в HTML и способы сохранения Excel
  с встроенными шрифтами.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to embed fonts
- export excel html
- convert excel html
- how to save excel
- embed fonts html
language: ru
lastmod: 2026-10-10
og_description: Как встроить шрифты при экспорте Excel в HTML на C#. Следуйте этому
  полному руководству, чтобы экспортировать Excel в HTML, конвертировать Excel HTML
  и узнать, как сохранять Excel со встроенными шрифтами.
og_image_alt: Screenshot showing exported HTML file that demonstrates how to embed
  fonts from Excel
og_title: Как внедрить шрифты при экспорте Excel в HTML – пошаговое руководство на
  C#
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Learn how to embed fonts while exporting Excel to HTML in C#. This
    guide covers export excel html, convert excel html, and how to save Excel with
    embedded fonts.
  headline: How to embed fonts when exporting Excel to HTML with C#
  type: TechArticle
tags:
- Excel
- HTML export
- Font embedding
- C#
title: Как встроить шрифты при экспорте Excel в HTML с помощью C#
url: /ru/net/exporting-excel-to-html-with-advanced-options/how-to-embed-fonts-when-exporting-excel-to-html-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как внедрить шрифты при экспорте Excel в HTML с помощью C#

Если вам нужно **how to embed fonts** в HTML‑файл, сгенерированный из рабочей книги Excel, этот учебник покажет точные шаги. Экспорт Excel в HTML часто удаляет пользовательские шрифты, что нарушает визуальное соответствие оригинальной таблицы. Настроив правильные параметры, вы можете сохранить каждый шрифт непосредственно в HTML‑выводе.

В этом руководстве вы узнаете, как **export excel html**, **convert excel html**, и **how to save Excel** с внедрёнными шрифтами, используя библиотеку Aspose.Cells для .NET. Решение работает с .NET 6+ и требует всего несколько строк кода C#.

## Что вы получите

- Полностью готовая, исполняемая программа C#, которая загружает существующий файл `.xlsx`.
- HTML‑вывод, где все используемые шрифты внедрены как Base64‑закодированные правила `@font-face`.
- Уверенность в том, что экспортированный HTML выглядит идентично исходной рабочей книге в любом браузере.

## Предварительные требования

| Requirement | Reason |
|-------------|--------|
| .NET 6 SDK or later | Обеспечивает среду выполнения для проекта C#. |
| Visual Studio 2022 (or any IDE) | Облегчает создание и запуск консольного приложения. |
| Aspose.Cells for .NET (NuGet package `Aspose.Cells`) | Предоставляет класс `HtmlSaveOptions` и функцию `EmbedFonts`. |
| An Excel file (`sample.xlsx`) that uses a custom font (e.g., *Calibri* or a downloaded TrueType font) | Показывает эффект внедрения шрифтов. |

> **Pro tip:** Если вы работаете за корпоративным прокси, настройте NuGet использовать прокси перед установкой пакета.

## Шаг 1: Установить Aspose.Cells

Откройте терминал в папке проекта и выполните:

```bash
dotnet add package Aspose.Cells
```

Эта команда добавит последнюю стабильную версию Aspose.Cells в ваш проект, делая доступными классы `Workbook` и `HtmlSaveOptions`.

## Шаг 2: Загрузить рабочую книгу Excel

Создайте новое консольное приложение (`dotnet new console`) и добавьте следующий код в `Program.cs`:

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Load an existing workbook. Replace the path with your actual file location.
        Workbook wb = new Workbook("sample.xlsx");
        // Continue with HTML export...
    }
}
```

**Почему этот шаг важен:**  
Загрузка рабочей книги дает доступ к её листам, стилям и пользовательским шрифтам, указанных в файле. Без загруженного экземпляра `Workbook` вы не сможете настроить параметры экспорта.

## Шаг 3: Настроить параметры сохранения HTML для внедрения шрифтов

Класс `HtmlSaveOptions` управляет каждым аспектом экспорта HTML. Установка `EmbedFonts = true` указывает Aspose.Cells внедрить каждый шрифт, используемый в рабочей книге, непосредственно в сгенерированный HTML‑файл.

```csharp
// Configure HTML save options to embed fonts
HtmlSaveOptions opts = new HtmlSaveOptions
{
    // When true, the exporter creates @font-face rules with Base64 data.
    EmbedFonts = true,

    // Optional: keep the original folder structure for images.
    ExportImagesAsBase64 = true,

    // Optional: generate a single HTML file (no external CSS folder).
    ExportActiveWorksheetOnly = false
};
```

**Объяснение:**  
- `EmbedFonts` — ключевой флаг, удовлетворяющий требованию **how to embed fonts**.  
- `ExportImagesAsBase64` гарантирует, что любые изображения также станут частью единого HTML‑файла, упрощая развертывание.  
- `ExportActiveWorksheetOnly`, установленный в `false`, обеспечивает включение всех листов, что полезно, когда рабочая книга содержит несколько листов.

## Шаг 4: Сохранить рабочую книгу как HTML с внедрёнными шрифтами

Теперь вызовите метод `Save`, передав желаемый путь вывода и только что настроенные параметры:

```csharp
// Save the workbook as an HTML file with embedded fonts
wb.Save("Embedded.html", opts);
```

Полученный файл `Embedded.html` содержит:

- Стандартную разметку HTML для данных таблицы.
- Один или несколько блоков `<style>` с правилами `@font-face`, внедряющими пользовательские шрифты как строки Base64.
- Все изображения, закодированные непосредственно в HTML (если есть).

## Шаг 5: Проверить, что шрифты действительно внедрены

Откройте `Embedded.html` в браузере (Chrome, Edge, Firefox). Страница должна отображаться точно так же, как оригинальная рабочая книга Excel, даже если на целевой машине пользовательские шрифты не установлены.

Чтобы двойным проверкой убедиться во внедрении:

1. Откройте исходный код страницы (`Ctrl+U` в большинстве браузеров).  
2. Найдите `@font-face`. Вы увидите блок, похожий на:

```css
@font-face {
    font-family: 'Calibri';
    src: url('data:font/ttf;base64,AAEAAAALAIAAAwAwT1Mv...') format('truetype');
    font-weight: normal;
    font-style: normal;
}
```

Если атрибут `src` содержит URL `data:`, шрифт успешно внедрён.

## Распространённые варианты и граничные случаи

| Situation | Suggested adjustment |
|-----------|----------------------|
| **Large workbook with many custom fonts** | Увеличьте `MaxFontEmbeddingSize` (если доступно) или разбейте экспорт на несколько HTML‑файлов, чтобы избежать превышения ограничений размера браузера. |
| **You need only a single worksheet** | Установите `opts.ExportActiveWorksheetOnly = true` и активируйте нужный лист перед сохранением (`wb.Worksheets[0].Activate();`). |
| **Embedding fonts is not allowed by corporate policy** | Установите `opts.EmbedFonts = false` и используйте веб‑безопасные шрифты или предоставьте файлы шрифтов рядом с HTML. |
| **Targeting older browsers that don’t support Base64 fonts** | Используйте `opts.FontEmbeddingMode = FontEmbeddingMode.FontFile;` (если версия библиотеки поддерживает) для генерации отдельных файлов `.ttf` и ссылки на них обычными URL. |

## Полный, исполняемый пример

Ниже приведена полная программа, которую вы можете скопировать и вставить в `Program.cs`. Она включает все необходимые директивы `using` и обработку ошибок для готового к продакшену скрипта.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        try
        {
            // 1️⃣ Load the workbook (replace with your file path)
            Workbook wb = new Workbook("sample.xlsx");

            // 2️⃣ Configure HTML export options to embed fonts
            HtmlSaveOptions opts = new HtmlSaveOptions
            {
                EmbedFonts = true,               // ✅ Core requirement: how to embed fonts
                ExportImagesAsBase64 = true,     // Keep everything in one file
                ExportActiveWorksheetOnly = false
            };

            // 3️⃣ Save as HTML with embedded fonts
            string outputPath = "Embedded.html";
            wb.Save(outputPath, opts);

            Console.WriteLine($"HTML file with embedded fonts saved to: {outputPath}");
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error during export: {ex.Message}");
        }
    }
}
```

**Ожидаемый вывод:**  
Запуск программы выводит строку подтверждения и создаёт `Embedded.html`. Открытие файла в любом современном браузере показывает таблицу со всеми оригинальными шрифтами, удовлетворяя цель **how to embed fonts**.

## Заключение

Теперь вы знаете, как **how to embed fonts** при выполнении операции **export excel html**, как **convert excel html**, и точные шаги **how to save excel** как HTML‑файл с внедрёнными шрифтами. Используя `HtmlSaveOptions.EmbedFonts = true`, сгенерированный HTML становится автономным, портативным и визуально идентичным исходной рабочей книге.

### Что дальше?

- Изучите свойства `HtmlSaveOptions` для управления CSS, обработкой изображений и выбором листов.  
- Скомбинируйте эту технику с серверной автоматизацией для генерации HTML‑отчётов на лету.  
- Обратите внимание на **embed fonts html** для других форматов документов (например, PDF), используя аналогичные API Aspose.

Не стесняйтесь экспериментировать с разными шрифтами, размерами рабочих книг и браузерными средами. Если возникнут проблемы, обратитесь к таблице граничных случаев выше или к документации Aspose.Cells для продвинутых сценариев внедрения шрифтов. Счастливого кодинга!

## Что вам стоит изучить дальше?

Следующие учебники охватывают тесно связанные темы, построенные на техниках, продемонстрированных в этом руководстве. Каждый ресурс включает полные работающие примеры кода с пошаговыми объяснениями, помогающие вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [Как экспортировать Excel в HTML – Полное руководство по программированию](/cells/english/net/exporting-excel-to-html-with-advanced-options/how-to-export-excel-to-html-complete-programming-guide/)
- [Как экспортировать Excel в HTML – Пошаговое руководство](/cells/english/net/exporting-excel-to-html-with-advanced-options/how-to-export-excel-to-html-step-by-step-guide/)
- [Как внедрить шрифты при конвертации Excel в PDF – Полное руководство](/cells/english/net/conversion-to-pdf/how-to-embed-fonts-when-converting-excel-to-pdf-complete-gui/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}