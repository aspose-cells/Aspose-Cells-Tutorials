---
category: general
date: 2026-03-25
description: Как экспортировать диаграммы из Word с помощью Aspose.Words C# – узнайте,
  как включать диаграммы и экспортировать их из Word за считанные минуты.
draft: false
keywords:
- how to export charts
- how to include charts
- export charts from word
- Aspose.Words export
- C# document automation
language: ru
og_description: Как экспортировать диаграммы из Word с помощью Aspose.Words C#. Это
  руководство покажет, как быстро включать диаграммы и экспортировать их из Word.
og_title: Как экспортировать диаграммы из Word – Полное руководство по C#
tags:
- C#
- Aspose.Words
- Word Automation
- Charts
title: Как экспортировать диаграммы из Word – Полное руководство по C#
url: /ru/net/chart-rendering-and-conversion/how-to-export-charts-from-word-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как экспортировать диаграммы из Word – Полное руководство на C#

Когда‑то вам нужно было **как экспортировать диаграммы** из документа Word, но вы не знали, с чего начать? Вы не одиноки; многие разработчики сталкиваются с этой проблемой при автоматизации отчетов. В этом руководстве мы пройдем практическое решение от начала до конца, которое не только покажет, **как экспортировать диаграммы**, но и объяснит, **как включать диаграммы** в экспортируемый файл. К концу вы сможете экспортировать диаграммы из Word всего несколькими строками C#.

Мы будем использовать популярную библиотеку **Aspose.Words for .NET**, потому что она нативно работает с объектами диаграмм и поддерживает .docx, .doc и даже более старые форматы. Никаких заморочек с Office Interop, без COM‑кошмаров. Нижеописанные шаги предполагают, что у вас есть базовый проект C# и установлен пакет Aspose.Words через NuGet. Если вы новичок в этой библиотеке, не переживайте — мы быстро пройдемся по требованиям.

## Требования

- .NET 6.0 или новее (код также работает на .NET Framework 4.7+)
- Visual Studio 2022 или любая другая IDE по вашему выбору
- Aspose.Words for .NET (установите через `dotnet add package Aspose.Words`)

> **Pro tip:** Держите вашу версию Aspose.Words актуальной; последняя версия (по состоянию на март 2026) добавляет улучшенную работу с диаграммами и повышает производительность.

## Шаг 1: Загрузка исходного документа Word

Первое, что нужно сделать — открыть файл `.docx`, содержащий диаграммы, которые вы хотите извлечь. Aspose.Words делает это в одну строку.

```csharp
using Aspose.Words;

// Load the source document (replace with your actual path)
Document document = new Document(@"C:\Docs\input.docx");
```

*Почему это важно:* При загрузке документа создаётся представление в памяти каждого элемента — абзацев, таблиц и, что особенно важно, объектов диаграмм. Без этого шага вы не сможете получить доступ к диаграммам и манипулировать ими.

## Шаг 2: Настройка параметров сохранения для сохранения диаграмм

По умолчанию простой вызов `document.Save("output.docx")` сохраняет всё, но если вы когда‑нибудь переключаете `ExportImages` или похожие флаги, встроенные диаграммы могут потеряться. Чтобы быть явным — и ответить на часть вопроса «**как включать диаграммы**» — мы задаём `DocxSaveOptions` с `ExportCharts = true`.

```csharp
// Create save options that ensure charts are included
DocxSaveOptions saveOptions = new DocxSaveOptions
{
    ExportCharts = true          // Guarantees charts are part of the saved file
};
```

*Объяснение:* `ExportCharts` указывает движку сериализовать каждую диаграмму как нативный элемент Office Open XML. Это необходимо, когда позже открывать файл в Word или других редакторах; диаграммы будут выглядеть точно так же, как в исходном документе.

## Шаг 3: Сохранение документа с настроенными параметрами

Теперь записываем документ обратно на диск, используя только что определённые параметры. Выходной файл будет содержать весь оригинальный контент **и** диаграммы.

```csharp
// Save the document with charts preserved
document.Save(@"C:\Docs\charts.docx", saveOptions);
```

На этом этапе у вас есть новый файл Word (`charts.docx`), который является точной копией оригинала, включая все графики диаграмм. Откройте его в Microsoft Word, чтобы проверить — ваши диаграммы должны быть полностью функциональными, редактируемыми и выглядеть точно так же, как и прежде.

## Полный рабочий пример

Ниже представлена полная, готовая к запуску программа. Скопируйте её в консольное приложение, поправьте пути и нажмите **F5**.

```csharp
using System;
using Aspose.Words;
using Aspose.Words.Saving;

namespace ExportChartsDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the source document containing charts
            string inputPath = @"C:\Docs\input.docx";
            Document document = new Document(inputPath);
            Console.WriteLine($"Loaded document: {inputPath}");

            // 2️⃣ Set save options to explicitly include charts
            DocxSaveOptions saveOptions = new DocxSaveOptions
            {
                ExportCharts = true   // This ensures charts are not stripped out
            };
            Console.WriteLine("Configured DocxSaveOptions to export charts.");

            // 3️⃣ Save the new file
            string outputPath = @"C:\Docs\charts.docx";
            document.Save(outputPath, saveOptions);
            Console.WriteLine($"Document saved with charts at: {outputPath}");

            // Verification hint
            Console.WriteLine("Open the output file in Word to confirm charts are present.");
        }
    }
}
```

**Ожидаемый результат:** При открытии `charts.docx` в Microsoft Word каждая диаграмма из `input.docx` будет отображаться без изменений. Нет отсутствующих изображений, нет битых ссылок.

## Обработка распространённых граничных случаев

| Ситуация | На что обратить внимание | Рекомендованное решение |
|-----------|--------------------------|--------------------------|
| **Документ содержит встроенные листы Excel** | Диаграммы могут быть связаны с внешними данными Excel. | Используйте `DocxSaveOptions.ExportEmbeddedExcelData = true` (доступно в новых версиях), чтобы сохранить данные. |
| **Большие документы (> 100 МБ)** | Потребление памяти резко возрастает при загрузке. | Установите `LoadOptions.LoadFormat = LoadFormat.Docx` и рассмотрите потоковую обработку с помощью `DocumentBuilder` для поэтапного процесса. |
| **Нужны только определённые диаграммы** | Экспорт всего файла избыточен. | Переберите `document.GetChildNodes(NodeType.Shape, true)` и отфильтруйте по `Shape.IsChart`. Затем клонируйте эти формы в новый `Document` перед сохранением. |
| **Целевой формат — PDF** | Диаграммы могут отрисовываться иначе. | Используйте `PdfSaveOptions` с `ExportCharts = true` (флаг работает и для PDF). |

Эти варианты отвечают на запрос «**export charts from word**» в разных контекстах, гарантируя, что вы покрыты как при сохранении обратно в DOCX, так и при конвертации в другие форматы.

## Часто задаваемые вопросы

**В: Работает ли это со старыми файлами `.doc`?**  
О: Да. Aspose.Words автоматически преобразует устаревший бинарный формат в современную структуру Open XML в памяти, поэтому `ExportCharts` по‑прежнему применяется.

**В: Что если я хочу экспортировать только изображения диаграмм, а не весь документ?**  
О: Вы можете извлечь каждую диаграмму как изображение с помощью `ChartRenderer`. Пример: `chartRenderer.Save("chart.png", ImageFormat.Png);` Это решает более узкую задачу «how to export charts».

**В: Есть ли проблемы с лицензированием?**  
О: Aspose.Words — коммерческая библиотека. Для оценки вы можете использовать временную лицензию; для продакшн‑использования потребуется полноценная лицензия, чтобы избавиться от водяного знака оценки.

## Визуальный обзор

Ниже представлена быстрая схема процесса — обратите внимание на ключевое слово в альтернативном тексте.

![How to export charts example – diagram showing load → configure → save steps](https://example.com/images/export-charts-diagram.png)

*Alt text:* **how to export charts diagram illustrating load, configure, and save steps**

## Итоги

Мы только что рассмотрели, **как экспортировать диаграммы** из документа Word с помощью Aspose.Words, продемонстрировали, **как включать диаграммы** при сохранении, и коснулись нескольких сценариев для **export charts from word** в разных форматах. Трёхшаговый шаблон — загрузка, настройка, сохранение — прост, надёжен и масштабируется от небольших отчётов до массивных корпоративных документов.

Что дальше? Попробуйте извлекать только выбранные диаграммы, конвертировать их в PNG для веб‑использования или автоматизировать пакетный процесс, который проходит по папке Word‑файлов и экспортирует их диаграммы за один раз. Каждый из этих вариантов опирается на базовую технику, которую вы только что освоили.

Не стесняйтесь оставить комментарий, если столкнётесь с проблемами, или поделиться тем, как вы адаптировали этот шаблон под свои проекты. Счастливого кодинга, и пусть ваши диаграммы всегда отображаются безупречно!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}