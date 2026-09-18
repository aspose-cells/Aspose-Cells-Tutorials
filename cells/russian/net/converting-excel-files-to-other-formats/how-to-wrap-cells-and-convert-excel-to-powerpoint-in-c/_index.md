---
category: general
date: 2026-09-18
description: Как обернуть ячейки в рабочей книге Excel и сохранить её как файл PowerPoint.
  Узнайте, как использовать WRAPCOLS, создать лист рабочей книги и экспортировать
  в PPTX.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to wrap cells
- convert excel to powerpoint
- save excel as powerpoint
- how to use wrapcols
- create workbook worksheet
language: ru
lastmod: 2026-09-18
og_description: Как переносить содержимое ячеек в Excel и экспортировать книгу в редактируемый
  файл PowerPoint с помощью C#. Следуйте пошаговому руководству, чтобы освоить WRAPCOLS
  и создание листов рабочей книги.
og_image_alt: Diagram showing how to wrap cells in Excel before exporting to PowerPoint
og_title: Как переносить содержимое ячеек и конвертировать Excel в PowerPoint на C#
schemas:
- author: Aspose
  dateModified: '2026-09-18'
  description: How to wrap cells in an Excel workbook and save it as a PowerPoint
    file. Learn to use WRAPCOLS, create workbook worksheet, and export to PPTX.
  headline: How to wrap cells and convert Excel to PowerPoint in C#
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
- PowerPoint export
title: Как переносить текст в ячейках и конвертировать Excel в PowerPoint на C#
url: /ru/net/converting-excel-files-to-other-formats/how-to-wrap-cells-and-convert-excel-to-powerpoint-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как обернуть ячейки и конвертировать Excel в PowerPoint на C#

Если вам нужно **how to wrap cells** в листе Excel, а затем превратить этот лист в презентацию PowerPoint, это руководство покажет вам полное, готовое к запуску решение. К концу первых двух предложений вы точно узнаете, какие вызовы API выполняют обёртку и какой метод сохраняет файл как PPTX.

Мы будем использовать Aspose.Cells for .NET, библиотеку, позволяющую манипулировать рабочими книгами Excel без установленного Microsoft Office. В руководстве рассматривается **convert Excel to PowerPoint**, демонстрируется **how to use WRAPCOLS**, и объясняются лучшие практики **create workbook worksheet**. Внешние инструменты не требуются — только среда разработки .NET.

## Требования

- .NET 6.0 или новее (код также работает с .NET Framework 4.6+)
- NuGet‑пакет Aspose.Cells for .NET (`Install-Package Aspose.Cells`)
- Базовое знакомство с C# и концепцией листов
- IDE, например Visual Studio или VS Code

> **Pro tip:** Используйте бесплатную оценочную лицензию Aspose.Cells во время экспериментов; замените её полной лицензией перед выпуском в продакшн.

## Шаг 1: Создать рабочую книгу и добавить лист

Первое, что вам нужно **create workbook worksheet**, — это создать объект `Workbook`. По умолчанию Aspose.Cells создает один лист (индекс 0), который мы будем использовать в демонстрации.

```csharp
using System;
using Aspose.Cells;

class WrapAndExport
{
    static void Main()
    {
        // Step 1: Initialize a new workbook (creates one worksheet automatically)
        Workbook workbook = new Workbook();

        // Reference the first worksheet for later operations
        Worksheet ws = workbook.Worksheets[0];
```

**Why this matters:** Инициализация рабочей книги предоставляет чистый холст. Лист по умолчанию уже входит в коллекцию `Worksheets`, поэтому вам не нужно вызывать `Add()`, если только вы не хотите добавить дополнительные листы.

## Шаг 2: Заполнить исходный диапазон (A2:A10)

Прежде чем мы сможем **how to wrap cells**, нам нужны данные для обёртки. Этот шаг заполняет ячейки A2‑A10 образцовым текстом.

```csharp
        // Fill cells A2:A10 with a long string to demonstrate wrapping
        for (int i = 2; i <= 10; i++)
        {
            ws.Cells[$"A{i}"].PutValue(
                "Lorem ipsum dolor sit amet, consectetur adipiscing elit. " +
                "Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.");
        }
```

**Edge case:** Если исходный диапазон пуст, `WRAPCOLS` возвращает `#VALUE!`. Всегда убеждайтесь, что диапазон содержит хотя бы одну непустую ячейку.

## Шаг 3: Применить формулу WRAPCOLS

Теперь мы отвечаем на основной вопрос **how to use WRAPCOLS**. Формула принимает вертикальный диапазон и распределяет его по указанному количеству столбцов. Мы записываем формулу в ячейку `A1`; получившийся массив автоматически заполняет соседние ячейки.

```csharp
        // Step 3: Apply WRAPCOLS to wrap A2:A10 into 3 columns, result starts at A1
        ws.Cells["A1"].Formula = "=WRAPCOLS(A2:A10,3)";
```

**What happens under the hood:** `WRAPCOLS` оценивает исходный диапазон, делит элементы поровну (или насколько это возможно) между целевыми столбцами и записывает значения в прямоугольный блок. Размер блока динамический, поэтому вам не нужно заранее определять диапазон назначения.

## Шаг 4: Сохранить рабочую книгу как редактируемый файл PowerPoint

Наконец, мы рассматриваем **convert Excel to PowerPoint** и **save Excel as PowerPoint**. Aspose.Cells может экспортировать лист напрямую в PPTX, сохраняя макет как редактируемую форму.

```csharp
        // Step 4: Export the worksheet to an editable PPTX presentation
        string outputPath = @"YOUR_DIRECTORY\ChartEditable.pptx";
        workbook.Save(outputPath, SaveFormat.Pptx);

        Console.WriteLine($"Workbook exported successfully to {outputPath}");
    }
}
```

**Why PPTX?** Сгенерированный PowerPoint содержит один слайд, на котором обёрнутые ячейки отображаются в виде таблицы. Вы можете открыть файл в Microsoft PowerPoint, редактировать текст, менять стили или добавлять дополнительные слайды — всё остаётся полностью редактируемым.

### Ожидаемый результат

- **Excel side:** Ячейка `A1` показывает массив из 3‑х столбцов оригинальных длинных строк, каждый столбец содержит примерно одинаковое количество строк.
- **PowerPoint side:** Открытие `ChartEditable.pptx` отображает слайд с таблицей, отражающей обёрнутый макет. Таблицу можно выделять, менять размер или редактировать, как любой нативный объект PowerPoint.

## Общие варианты и на что обратить внимание

| Сценарий | Корректировка |
|----------|----------------|
| **Обёртка в большее количество столбцов** | Измените второй аргумент функции `WRAPCOLS`, например, `=WRAPCOLS(A2:A10,5)`. |
| **Обёртка другого диапазона** | Обновите ссылку в формуле, например, `=WRAPCOLS(B2:B15,2)`. |
| **Экспортировать только часть листа** | Используйте `Worksheet.ExportDataTable` для извлечения `DataTable`, а затем API `Presentation` для создания пользовательского PPTX. |
| **Большие листы ( > 10 000 строк )** | Рассмотрите возможность разбивки экспорта на несколько слайдов, чтобы избежать проблем с производительностью. |

> **Watch out for:** При экспорте по умолчанию PPTX лист отображается как одно изображение, если рабочая книга содержит диаграммы. Использование `WRAPCOLS` гарантирует, что данные останутся в виде таблицы, которую можно редактировать.

## Полный исходный код для быстрого копирования

```csharp
using System;
using Aspose.Cells;

class WrapAndExport
{
    static void Main()
    {
        // Create a new workbook (contains one default worksheet)
        Workbook workbook = new Workbook();
        Worksheet ws = workbook.Worksheets[0];

        // Populate A2:A10 with sample long text
        for (int i = 2; i <= 10; i++)
        {
            ws.Cells[$"A{i}"].PutValue(
                "Lorem ipsum dolor sit amet, consectetur adipiscing elit. " +
                "Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.");
        }

        // Apply WRAPCOLS to wrap the range into 3 columns, result starts at A1
        ws.Cells["A1"].Formula = "=WRAPCOLS(A2:A10,3)";

        // Save as an editable PowerPoint presentation
        string outputPath = @"YOUR_DIRECTORY\ChartEditable.pptx";
        workbook.Save(outputPath, SaveFormat.Pptx);

        Console.WriteLine($"Workbook exported successfully to {outputPath}");
    }
}
```

Сохраните файл как `Program.cs`, восстановите пакет NuGet и запустите:

```bash
dotnet run
```

Вы должны увидеть сообщение в консоли, подтверждающее экспорт, а файл PPTX появится в указанной папке.

## Заключение

Теперь вы знаете **how to wrap cells** в листе Excel, **how to use WRAPCOLS**, и точные шаги для **convert Excel to PowerPoint** с помощью **save excel as powerpoint** используя Aspose.Cells. Полное решение демонстрирует **create workbook worksheet**, применяет формулу обёртки и создает редактируемый файл PPTX, готовый к настройкам презентации.

### Следующие шаги

- Изучите другие функции Excel (например, `TRANSPOSE`, `FILTER`) перед экспортом.
- Объедините несколько листов в многослайдовую презентацию PowerPoint, используя цикл.
- Добавьте пользовательские заголовки слайдов или брендинг, интегрируя Aspose.Slides после экспорта.

Не стесняйтесь экспериментировать с разным количеством столбцов, исходными диапазонами или даже комбинировать диаграммы и таблицы в одном PPTX. Приятного кодинга!

## Что вам стоит изучить дальше?

Следующие руководства охватывают тесно связанные темы, которые развивают техники, продемонстрированные в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [Как конвертировать Excel в PowerPoint с помощью Aspose.Cells for .NET: Полное руководство](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [Как обернуть текст в Excel с помощью Aspose.Cells for .NET | Руководство по форматированию](/cells/english/net/formatting/wrap-text-excel-aspose-cells-net/)
- [Экспортировать свойства рабочей книги и листа Excel в HTML с помощью Aspose.Cells for .NET](/cells/english/net/workbook-operations/export-excel-properties-to-html-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}