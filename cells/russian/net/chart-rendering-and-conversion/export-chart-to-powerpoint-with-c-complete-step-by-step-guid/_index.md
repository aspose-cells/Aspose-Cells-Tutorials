---
category: general
date: 2026-02-26
description: Экспортировать диаграмму в PowerPoint из Excel с помощью C#. Узнайте,
  как преобразовать Excel в PowerPoint, сохранить Excel как PowerPoint и оставить
  формы редактируемыми.
draft: false
keywords:
- export chart to powerpoint
- convert excel to powerpoint
- save excel as powerpoint
- how to convert excel to ppt
- save workbook as pptx
language: ru
og_description: Экспортировать диаграмму в PowerPoint из Excel с помощью C#. Это руководство
  показывает, как преобразовать Excel в PowerPoint, сохранить книгу как PPTX и оставить
  формы редактируемыми.
og_title: Экспорт диаграммы в PowerPoint с помощью C# – Полный учебник по программированию
tags:
- Aspose.Cells
- C#
- Office Automation
title: Экспорт диаграммы в PowerPoint с помощью C# – Полное пошаговое руководство
url: /ru/net/chart-rendering-and-conversion/export-chart-to-powerpoint-with-c-complete-step-by-step-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Экспорт диаграммы в PowerPoint – Полный программный учебник

Задумывались ли вы когда‑нибудь, как **export chart to PowerPoint** без потери возможности редактирования? Во многих сценариях отчётности вам нужен живой график внутри набора слайдов, но копировать и вставлять вручную — это хлопотно. Хорошая новость: это можно сделать программно, используя несколько строк C#.

В этом руководстве мы пройдём весь процесс: от загрузки книги Excel, содержащей диаграмму с текстовым полем, настройки экспорта так, чтобы текстовые поля и фигуры оставались редактируемыми, и, наконец, сохранения результата в файл **PowerPoint**. К концу вы также узнаете, как **convert Excel to PowerPoint**, **save Excel as PowerPoint**, и даже подправить параметры для особых сценариев.

## Что понадобится

- **Aspose.Cells for .NET** (version 23.10 or later). Это библиотека, которая делает конвертацию без проблем.
- **.NET 6+** runtime – любой современный SDK подходит.
- Простой файл Excel (`ChartWithTextbox.xlsx`), содержащий как минимум одну диаграмму и текстовое поле.
- Visual Studio или ваша любимая IDE.

Дополнительные пакеты NuGet не требуются, кроме Aspose.Cells, но базовое понимание синтаксиса C# определённо поможет.

## Экспорт диаграммы в PowerPoint – Пошагово

Ниже мы разбиваем решение на отдельные, легко‑следуемые шаги. Каждый шаг включает точный код, который вам нужен, плюс короткий абзац «почему», объясняющий логику.

### Шаг 1: Загрузка книги Excel, содержащей диаграмму

Сначала нам нужно загрузить исходный файл в память. Использование `Workbook` из Aspose.Cells считывает всю таблицу, включая диаграммы, изображения и встроенные объекты.

```csharp
using Aspose.Cells;

// Step 1: Load the Excel workbook that contains the chart with a textbox
Workbook workbook = new Workbook(@"C:\Samples\ChartWithTextbox.xlsx");

// Verify that the workbook actually contains a chart
if (workbook.Worksheets[0].Charts.Count == 0)
{
    throw new InvalidOperationException("No chart found in the first worksheet.");
}
```

*Почему это важно:* Если книга открывается без правильного указания пути, вы получите `FileNotFoundException`. Быстрая проверка предотвращает экспорт пустого слайда позже.

### Шаг 2: Подготовка параметров презентации для сохранения фигур редактируемыми

Aspose.Cells позволяет решить, будут ли текстовые поля, фигуры и даже сама диаграмма оставаться **editable** после экспорта. Установка `ExportTextBoxes` и `ExportShapes` в `true` сохраняет эти объекты как нативные элементы PowerPoint, а не преобразует их в статическое изображение.

```csharp
using Aspose.Cells.Drawing;

// Step 2: Set up presentation options to keep textboxes and shapes editable in the output
PresentationOptions presentationOptions = new PresentationOptions
{
    ExportTextBoxes = true, // Preserve editable textboxes
    ExportShapes    = true  // Preserve shapes such as the chart itself
};
```

*Почему это важно:* Если оставить эти флаги со значениями по умолчанию (`false`), полученный слайд будет содержать растровое изображение диаграммы, и её серии или подпись будет невозможно отредактировать позже. Включение обеих опций даёт настоящую диаграмму PowerPoint, которая ведёт себя точно так же, как если бы вы создали её вручную.

### Шаг 3: Конвертация Excel в PowerPoint и сохранение файла

Теперь мы вызываем метод `Save`, передавая перечисление `SaveFormat.Pptx` и только что настроенные параметры. Библиотека заботится о преобразовании объекта диаграммы Excel в форму диаграммы PowerPoint.

```csharp
// Step 3: Save the workbook as a PowerPoint presentation using the configured options
workbook.Save(@"C:\Samples\Result.pptx", SaveFormat.Pptx, presentationOptions);
```

*Почему это важно:* Вызов `Save` выполняет всю тяжёлую работу — сопоставление серий Excel с сериями PowerPoint, сохранение форматирования осей и копирование всех связанных текстовых полей. После выполнения этой строки у вас будет полностью редактируемый файл `.pptx`, готовый к открытию в Microsoft PowerPoint.

### Проверка результата

Откройте `Result.pptx` в PowerPoint. Вы должны увидеть слайд, содержащий:

- Исходную диаграмму, всё ещё связанную с данными (можно двойным щелчком редактировать серии).
- Любое текстовое поле, которое было в листе Excel, теперь нативное текстовое поле PowerPoint.
- Макет слайда выбирается автоматически (обычно пустой слайд).

Если вы заметили отсутствие каких‑либо элементов, дважды проверьте, что исходная книга действительно содержит видимые объекты и что `ExportTextBoxes` / `ExportShapes` установлены в `true`.

### Конвертация Excel в PowerPoint: Работа с несколькими листами

Часто книга содержит более одного листа, каждый со своей диаграммой. По умолчанию Aspose.Cells экспортирует **all** диаграмм из **all** листов в отдельные слайды. Если вам нужен только подмножество, вы можете отфильтровать их перед сохранением:

```csharp
// Example: Export only charts from the first worksheet
Worksheet firstSheet = workbook.Worksheets[0];
foreach (Chart chart in firstSheet.Charts)
{
    chart.IsVisible = true; // Ensure visibility
}

// Hide charts from other sheets
for (int i = 1; i < workbook.Worksheets.Count; i++)
{
    foreach (Chart chart in workbook.Worksheets[i].Charts)
    {
        chart.IsVisible = false;
    }
}
```

*Совет:* Установка `chart.IsVisible = false` дешевле, чем полное удаление диаграммы, и позволяет включать/исключать её без изменения исходного файла.

### Сохранение Excel как PowerPoint – Настройка размера слайда

PowerPoint по умолчанию использует слайд размером 10 дюймов на 5,63 дюйма. Если ваша диаграмма выглядит тесно, вы можете изменить размеры слайда через объект `PresentationOptions`:

```csharp
presentationOptions.SlideSize = new SizeF(13.33f, 7.5f); // 16:9 widescreen
```

Теперь экспортированная диаграмма будет иметь больше пространства, а любые текстовые поля сохранят своё оригинальное расположение.

### Как конвертировать Excel в PPT: Работа со скрытыми объектами

Скрытые строки, столбцы или фигуры иногда попадают в экспорт. Чтобы удалить их, выполните быструю очистку перед сохранением:

```csharp
// Remove hidden rows/columns that might affect chart layout
foreach (Worksheet sheet in workbook.Worksheets)
{
    sheet.Cells.HideRows = false;
    sheet.Cells.HideColumns = false;
}
```

Этот шаг не всегда необходим, но он предотвращает неожиданные пробелы в конечной презентации.

### Сохранение книги как PPTX – Полный рабочий пример

Объединив всё вместе, представляем готовую к запуску консольную программу, демонстрирующую весь процесс:

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing; // For SizeF

class ExportChartDemo
{
    static void Main()
    {
        // Load workbook (Step 1)
        string sourcePath = @"C:\Samples\ChartWithTextbox.xlsx";
        Workbook workbook = new Workbook(sourcePath);

        // Verify chart existence
        if (workbook.Worksheets[0].Charts.Count == 0)
        {
            Console.WriteLine("No chart found. Exiting.");
            return;
        }

        // Configure presentation options (Step 2)
        PresentationOptions options = new PresentationOptions
        {
            ExportTextBoxes = true,
            ExportShapes    = true,
            SlideSize       = new SizeF(13.33f, 7.5f) // optional widescreen
        };

        // Optional: export only first worksheet charts
        for (int i = 1; i < workbook.Worksheets.Count; i++)
        {
            foreach (Chart c in workbook.Worksheets[i].Charts)
                c.IsVisible = false;
        }

        // Save as PowerPoint (Step 3)
        string targetPath = @"C:\Samples\Result.pptx";
        workbook.Save(targetPath, SaveFormat.Pptx, options);

        Console.WriteLine($"Export complete! File saved to {targetPath}");
    }
}
```

Запуск этой программы создаст `Result.pptx` с редактируемой диаграммой и текстовым полем — именно то, что вы ожидаете при ручном **save workbook as pptx**.

![Пример экспорта диаграммы в PowerPoint](/images/export-chart-to-powerpoint.png "Экспорт диаграммы в PowerPoint – редактируемый слайд")

## Часто задаваемые вопросы и особые случаи

**Что если файл Excel содержит диаграмму со связанным внешним источником данных?**  
Aspose.Cells копирует *текущие* значения данных в диаграмму PowerPoint. Он **не** сохраняет внешнюю связь, поскольку PowerPoint не может ссылаться на соединение данных Excel таким же способом. Если нужны живые обновления, рассмотрите возможность встраивания оригинального файла Excel в PPTX как OLE‑объект.

**Могу ли я экспортировать диаграмму, использующую пользовательскую тему?**  
Да. Библиотека пытается сопоставить цвета темы Excel со слотами темы PowerPoint. Для сильно кастомных палитр возможно потребуется скорректировать цвета после экспорта с помощью собственного API PowerPoint (например, Aspose.Slides).

**Есть ли ограничение на количество диаграмм?**  
Практически нет — Aspose.Cells передаёт данные потоково, поэтому даже книга с десятками диаграмм будет экспортирована, хотя размер полученного PPTX будет расти линейно.

**Нужна ли лицензия для Aspose.Cells?**  
Бесплатная оценочная версия работает, но добавляет водяной знак на первый слайд. Для использования в продакшене получите полноценную лицензию, чтобы убрать водяной знак и раскрыть полную производительность.

## Итоги

Мы рассмотрели, как **export chart to PowerPoint** с помощью C#, продемонстрировали точный код для загрузки книги Excel, настройки `PresentationOptions` для сохранения текстовых полей и фигур редактируемыми, и, наконец, сохранения результата в файл `.pptx`. Вы также узнали, как **convert Excel to PowerPoint**, **save Excel as PowerPoint**, и получили ответ на вопрос «**how to convert Excel to ppt**» с полным, готовым к запуску примером.

## Что дальше?

- **Save workbook as PPTX** с несколькими слайдами: пройдитесь по каждому листу и вызовите `Save` с `PresentationOptions` для каждого.
- Изучите **Aspose.Slides**, если нужно программно модифицировать сгенерированный PPTX (добавлять переходы, заметки докладчика и т.д.).
- Попробуйте экспортировать **pivot charts** или **3‑D charts** — те же параметры применимы, но возможно потребуется подправить форматирование осей после экспорта.

Если возникнут какие‑либо проблемы, оставьте комментарий ниже или ознакомьтесь с официальной документацией Aspose.Cells для последних изменений API. Счастливого кодинга и наслаждайтесь преобразованием диаграмм Excel в изысканные презентации PowerPoint всего лишь несколькими строками C#!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}