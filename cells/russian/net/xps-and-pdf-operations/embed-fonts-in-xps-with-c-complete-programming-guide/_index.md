---
category: general
date: 2026-06-17
description: Встраивание шрифтов в XPS с помощью C# и Aspose.PDF. Узнайте о XpsSaveOptions,
  встраивании шрифтов и экспорте в XPS за считанные минуты.
draft: false
keywords:
- embed fonts in xps
- XpsSaveOptions
- Aspose.PDF for .NET
- C# XPS export
- font embedding
language: ru
og_description: Встраивание шрифтов в XPS с помощью Aspose.PDF для .NET. Этот учебник
  показывает, как настроить XpsSaveOptions, встроить шрифты и создать XPS‑файлы на
  C#.
og_title: Встраивание шрифтов в XPS с помощью C# – пошаговое руководство
schemas:
- author: Aspose
  dateModified: '2026-06-17'
  description: Embed fonts in XPS using C# and Aspose.PDF. Learn XpsSaveOptions, font
    embedding, and XPS export in minutes.
  headline: Embed Fonts in XPS with C# – Complete Programming Guide
  type: TechArticle
tags:
- C#
- XPS
- font embedding
- Aspose.PDF
title: Встраивание шрифтов в XPS с помощью C# – Полное руководство по программированию
url: /ru/net/xps-and-pdf-operations/embed-fonts-in-xps-with-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Встраивание шрифтов в XPS с помощью C# – Полное руководство по программированию

Когда‑то вам нужно **встроить шрифты в XPS**, но вы не знали, какие флаги API включить? Вы не одиноки — многие разработчики сталкиваются с этой проблемой при экспорте PDF или других документов в формат XPS. Хорошая новость: с несколькими строками C# и правильными параметрами вы можете запаковать шрифты прямо в файл XPS и гарантировать одинаковый рендеринг везде.

В этом руководстве мы пошагово рассмотрим, как настроить **XpsSaveOptions**, включить **встраивание шрифтов** и сохранить документ как XPS с помощью **Aspose.PDF for .NET**. К концу вы получите готовый фрагмент кода, который можно вставить в любой .NET‑проект.

## Что вы узнаете

- Почему встраивание шрифтов в XPS важно для кроссплатформенной точности.  
- Как создать `XpsSaveOptions` и переключить флаг `EmbedFonts`.  
- Полный C#‑код, необходимый для генерации XPS‑файла со встроенными шрифтами.  
- Распространённые подводные камни (шрифты с ограничениями лицензии, отсутствие глифов) и способы их обхода.  

**Предварительные требования**: .NET 6+ (или .NET Framework 4.6+), ссылка на пакет Aspose.PDF for .NET в NuGet и базовые знания C#. Другие внешние инструменты не нужны.

---

## Шаг 1: Установите Aspose.PDF for .NET

Прежде чем писать код, убедитесь, что библиотека Aspose.PDF доступна в вашем проекте.

```bash
dotnet add package Aspose.PDF --version 23.12
```

> **Pro tip:** Если вы работаете в Visual Studio, можно воспользоваться UI менеджером пакетов NuGet — просто найдите “Aspose.PDF”.

## Шаг 2: Создайте простой PDF‑документ

Начнём с крошечного PDF, содержащего одну строку текста. Этот документ позже будет сохранён как XPS со встроенными шрифтами.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// Create a new PDF document
Document pdfDoc = new Document();

// Add a page
Page page = pdfDoc.Pages.Add();

// Add a TextFragment with a custom font (e.g., Arial)
TextFragment tf = new TextFragment("Hello, XPS world!")
{
    // Use a TrueType font that you know is installed
    TextState = { Font = FontRepository.FindFont("Arial") }
};
page.Paragraphs.Add(tf);
```

*Почему это важно*: Использование известного TrueType‑шрифта гарантирует наличие глифов для встраивания. Если выбрать шрифт, не установленный на машине, Aspose переключится на шрифт по умолчанию, и XPS может не содержать нужный стиль.

## Шаг 3: Настройте XpsSaveOptions для встраивания шрифтов

Это сердце урока — объект `XpsSaveOptions`. Установка `EmbedFonts = true` заставляет Aspose упаковать каждый используемый шрифт непосредственно в пакет XPS.

```csharp
using Aspose.Pdf.XpsConversion;

// Configure XPS save options
XpsSaveOptions saveOptions = new XpsSaveOptions
{
    // This flag performs the actual font embedding
    EmbedFonts = true,

    // Optional: compress the XPS for smaller size
    Compression = CompressionType.Zip,

    // Optional: preserve the original PDF's layout
    PreserveFormFields = true
};
```

> **Зачем включать сжатие?** Файл XPS по сути является ZIP‑архивом XML‑файлов и ресурсов. Включив `Compression`, можно уменьшить итоговый размер до 30 % без влияния на встраивание шрифтов.

## Шаг 4: Сохраните документ как XPS со встроенными шрифтами

Теперь объединяем всё — сохраняем PDF как XPS, используя только что созданные параметры.

```csharp
// Define the output path (make sure the directory exists)
string outputPath = Path.Combine(Environment.CurrentDirectory, "EmbeddedFontExample.xps");

// Save the PDF as XPS, embedding all fonts
pdfDoc.Save(outputPath, SaveFormat.Xps, saveOptions);

Console.WriteLine($"XPS file saved to: {outputPath}");
```

При открытии `EmbeddedFontExample.xps` в Windows XPS Viewer текст должен отображаться точно так же, как в PDF, независимо от того, установлен ли Arial в системе просмотрщика.

## Шаг 5: Проверка встраивания шрифтов (необязательно, но рекомендуется)

Если хотите убедиться, что шрифты действительно встроены, распакуйте XPS‑файл (это просто ZIP‑архив) и проверьте папку `Resources/Fonts`.

```powershell
# PowerShell one‑liner to list embedded fonts
Expand-Archive -Path .\EmbeddedFontExample.xps -DestinationPath .\tempXps
Get-ChildItem .\tempXps\Resources\Fonts
```

Вы должны увидеть файлы `.ttf` или `.otf`, соответствующие использованным шрифтам. Если папка пуста, проверьте `saveOptions.EmbedFonts` и убедитесь, что исходный шрифт не ограничен лицензией.

## Распространённые особые случаи и их решения

| Ситуация | Что происходит | Как исправить |
|-----------|----------------|---------------|
| **Шрифт лицензирован как “no‑embed”** | Aspose тихо заменяет шрифт, в результате появляются пропущенные глифы. | Использовать другой шрифт или получить лицензию, позволяющую встраивание. |
| **Пользовательский шрифт не установлен** | `FontRepository.FindFont` возвращает `null` → исключение во время выполнения. | Загрузить шрифт вручную: `FontRepository.AddFont("path/to/font.ttf");` перед созданием `TextFragment`. |
| **Большие XPS‑файлы** | Встраивание множества шрифтов увеличивает размер файла. | Включить `Compression = CompressionType.Zip` или использовать подмножество шрифтов через `saveOptions.SubsetFonts = true`. |
| **Unicode‑символы не отображаются** | Отсутствуют глифы для некоторых скриптов. | Убедиться, что выбранный шрифт поддерживает нужный диапазон Unicode, либо встроить несколько резервных шрифтов. |

---

## Полный рабочий пример (готов к копированию)

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.XpsConversion;

class EmbedFontsInXpsDemo
{
    static void Main()
    {
        // 1️⃣ Create a simple PDF with custom text
        Document pdfDoc = new Document();
        Page page = pdfDoc.Pages.Add();

        // Load a TrueType font (Arial) – replace with your font if needed
        FontRepository.AddFont(@"C:\Windows\Fonts\arial.ttf");
        TextFragment tf = new TextFragment("Hello, XPS world!")
        {
            TextState = { Font = FontRepository.FindFont("Arial") }
        };
        page.Paragraphs.Add(tf);

        // 2️⃣ Set up XpsSaveOptions to embed fonts
        XpsSaveOptions saveOptions = new XpsSaveOptions
        {
            EmbedFonts = true,
            Compression = CompressionType.Zip,
            PreserveFormFields = true
        };

        // 3️⃣ Save as XPS
        string outputPath = Path.Combine(
            Environment.CurrentDirectory,
            "EmbeddedFontExample.xps");

        pdfDoc.Save(outputPath, SaveFormat.Xps, saveOptions);

        Console.WriteLine($"✅ XPS saved with embedded fonts at: {outputPath}");
    }
}
```

**Ожидаемый вывод** (консоль):

```
✅ XPS saved with embedded fonts at: C:\YourProject\EmbeddedFontExample.xps
```

Откройте сгенерированный XPS‑файл; текст должен выглядеть точно так же, как стилизованный, даже на машине без установленного Arial.

---

## Заключение

Мы только что продемонстрировали, как **встроить шрифты в XPS** с помощью C# и **Aspose.PDF for .NET**. Настроив `XpsSaveOptions` с `EmbedFonts = true`, вы гарантируете, что каждый глиф будет идти вместе с пакетом XPS, устраняя неприятные сюрпризы на клиентских машинах.  

От настройки проекта до проверки встроенных ресурсов — теперь у вас есть полное, готовое к использованию решение. Далее попробуйте заменить шрифты, добавить изображения или генерировать многостраничные XPS‑документы — каждый из них получит выгоду от той же стратегии встраивания.

Есть вопросы о лицензировании, подмножестве шрифтов или производительности? Оставляйте комментарий, и happy coding!

## Что изучать дальше?

Следующие руководства охватывают смежные темы, построенные на техниках, продемонстрированных в этом руководстве. Каждый ресурс содержит полностью рабочие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы в ваших проектах.

- [Экспорт Excel в XPS с помощью Aspose.Cells .NET](/cells/english/net/workbook-operations/export-excel-xps-aspose-cells-net/)
- [Как извлечь шрифты из файлов Excel с помощью Aspose.Cells for .NET](/cells/english/net/formatting/extract-fonts-excel-aspose-cells-dotnet-guide/)
- [Рендеринг Excel в PNG, TIFF, PDF с пользовательскими шрифтами в .NET с использованием Aspose.Cells](/cells/english/net/workbook-operations/render-excel-custom-fonts-aspose-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}