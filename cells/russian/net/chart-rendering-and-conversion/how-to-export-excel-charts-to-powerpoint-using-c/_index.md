---
category: general
date: 2026-10-26
description: Узнайте, как экспортировать графики Excel в PowerPoint с помощью C#.
  Сохраните редактируемость фигур и сохраняйте в формате PPTX за несколько строк кода.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel charts to powerpoint
- Aspose.Cells export
- C# Excel to PowerPoint conversion
- preserve shape editability
- SaveFormat.Pptx
- Workbook.Save method
language: ru
lastmod: 2026-10-26
og_description: Экспортируйте диаграммы Excel в PowerPoint с помощью C#. Это руководство
  показывает, как сохранить формы редактируемыми и сохранить файл в формате PPTX,
  используя Aspose.Cells.
og_image_alt: Export Excel charts to PowerPoint example showing a chart transferred
  from Excel to a slide
og_title: Экспорт графиков Excel в PowerPoint с помощью C# – пошаговое руководство
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn how to export Excel charts to PowerPoint with C#. Preserve shape
    editability and save as PPTX in a few lines of code.
  headline: How to export Excel charts to PowerPoint using C#
  type: TechArticle
- description: Learn how to export Excel charts to PowerPoint with C#. Preserve shape
    editability and save as PPTX in a few lines of code.
  name: How to export Excel charts to PowerPoint using C#
  steps:
  - name: Load the Excel workbook
    text: '```csharp using Aspose.Cells;'
  - name: (Optional) Adjust workbook settings
    text: In most cases the default settings are sufficient for a clean export. However,
      if you need to change the calculation mode, page setup, or hide certain sheets,
      you can do it here.
  - name: Save the workbook as a PowerPoint file
    text: '```csharp // Export the workbook to PPTX while keeping chart shapes editable
      workbook.Save(@"C:\Projects\Shapes.pptx", SaveFormat.Pptx); ```'
  - name: Verify the result
    text: 'Open `Shapes.pptx` in PowerPoint and:'
  - name: 'Edge case: Exporting multiple worksheets with separate charts'
    text: If your Excel file contains several worksheets, each with its own chart,
      Aspose.Cells creates a separate slide for each chart automatically. You can
      control slide order by rearranging worksheets before the save operation.
  - name: 'Performance tip: Stream the output instead of writing to disk'
    text: When generating PowerPoint files in a web API, avoid temporary files by
      writing to a `MemoryStream`.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel
- PowerPoint
title: Как экспортировать диаграммы Excel в PowerPoint с помощью C#
url: /ru/net/chart-rendering-and-conversion/how-to-export-excel-charts-to-powerpoint-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как экспортировать диаграммы Excel в PowerPoint с помощью C#

Если вам нужно **экспортировать диаграммы Excel в PowerPoint**, это руководство проведёт вас через полностью готовое решение. Независимо от того, создаёте ли вы панель отчётов или автоматизируете набор слайдов, вы увидите, как несколько строк кода C# сохраняют ваши диаграммы полностью редактируемыми после конвертации.

В этом учебнике вы узнаете, как:

* Загрузить существующую книгу Excel, содержащую диаграммы.  
* (Опционально) изменить настройки книги перед конвертацией.  
* Сохранить книгу в виде файла PowerPoint, сохранив возможность редактирования фигур.  

Всё это делается с помощью **Aspose.Cells for .NET**, библиотеки, которая осуществляет конвертацию Excel‑в‑PowerPoint без необходимости установки Microsoft Office на сервере.

## Что понадобится

| Требование | Причина |
|------------|---------|
| .NET 6.0 или новее | Современная среда выполнения с полным набором возможностей языка |
| Visual Studio 2022 (или любой IDE) | Удобный редактор и отладчик |
| **Aspose.Cells for .NET** пакет NuGet | Предоставляет класс `Workbook` и поддержку `SaveFormat.Pptx` |
| Файл Excel (`ChartAndShapes.xlsx`) с хотя бы одной диаграммой | Источник диаграмм, которые вы хотите экспортировать |

> **Pro tip:** Используйте бесплатную **Aspose.Cells Evaluation** версию для тестирования кода; лицензионный ключ удалит водяной знак оценки.

```bash
dotnet add package Aspose.Cells
```

## Экспорт диаграмм Excel в PowerPoint – полный рабочий процесс

Ниже представлен сквозной код, который выполняет экспорт с **сохранением возможности редактирования фигур**. Каждый шаг подробно объяснён.

### Шаг 1: Загрузка книги Excel

```csharp
using Aspose.Cells;

// Load the workbook that holds the charts you want to export
Workbook workbook = new Workbook(@"C:\Projects\ChartAndShapes.xlsx");
```

*Класс `Workbook` представляет всю книгу Excel. При загрузке файла читаются все листы, диаграммы и фигуры, что необходимо для дальнейших манипуляций.*

### Шаг 2: (Опционально) Настройка параметров книги

В большинстве случаев значения по умолчанию достаточны для чистого экспорта. Однако, если необходимо изменить режим расчётов, параметры страницы или скрыть определённые листы, это можно сделать здесь.

```csharp
// Example: ensure all formulas are calculated before export
workbook.CalculateFormula();

// Example: hide a sheet that you don’t want in the PowerPoint
workbook.Worksheets["SecretData"].IsVisible = false;
```

> **Почему это важно:** Настройка параметров перед конвертацией гарантирует, что сгенерированные слайды точно соответствуют желаемому состоянию, особенно когда формулы или скрытые листы могут влиять на данные диаграмм.

### Шаг 3: Сохранение книги в файл PowerPoint

```csharp
// Export the workbook to PPTX while keeping chart shapes editable
workbook.Save(@"C:\Projects\Shapes.pptx", SaveFormat.Pptx);
```

*Константа `SaveFormat.Pptx` указывает Aspose.Cells записать презентацию PowerPoint. Внутри библиотека преобразует каждую диаграмму Excel в форму PowerPoint, которая остаётся полностью редактируемой в Microsoft PowerPoint.*

### Шаг 4: Проверка результата

Откройте `Shapes.pptx` в PowerPoint и:

1. Выберите любую диаграмму на слайде.  
2. Щёлкните правой кнопкой → **Edit Data**.  
3. Убедитесь, что открылось окно с таблицей данных диаграммы и вы можете изменить значения.

Если у диаграммы открывается панель **Edit Data**, конвертация прошла успешно и **возможность редактирования фигур** сохранена.

![Export Excel charts to PowerPoint example](export-excel-charts-to-powerpoint.png){.img-fluid alt="Export Excel charts to PowerPoint example"}

## Распространённые проблемы и способы их избежать

| Проблема | Причина | Решение |
|----------|---------|----------|
| Диаграммы отображаются как статические изображения | Используется более старая версия Aspose.Cells без поддержки экспорта в PPTX | Обновите до последней версии Aspose.Cells 23.x или новее |
| Отсутствуют данные в диаграмме PowerPoint | Книга не была полностью вычислена перед экспортом | Вызовите `workbook.CalculateFormula()` перед `Save` |
| Фигуры не редактируются | Сохранение выполнено с `SaveFormat.Xlsx` вместо `SaveFormat.Pptx` | Убедитесь, что в `Workbook.Save` передаёте `SaveFormat.Pptx` |
| Исключение лицензии во время выполнения | Оценочная версия без зарегистрированной лицензии | Зарегистрируйте лицензию с помощью `License license = new License(); license.SetLicense("Aspose.Cells.lic");` |

### Пограничный случай: Экспорт нескольких листов с отдельными диаграммами

Если ваш файл Excel содержит несколько листов, каждый со своей диаграммой, Aspose.Cells автоматически создаст отдельный слайд для каждой диаграммы. Порядок слайдов можно контролировать, переставив листы перед операцией сохранения.

```csharp
// Move the worksheet that should appear first in the slide deck
workbook.Worksheets.MoveTo(2, 0); // move sheet index 2 to position 0
```

### Совет по производительности: Потоковый вывод вместо записи на диск

При генерации файлов PowerPoint в веб‑API избегайте временных файлов, записывая данные в `MemoryStream`.

```csharp
using (MemoryStream pptStream = new MemoryStream())
{
    workbook.Save(pptStream, SaveFormat.Pptx);
    // Return the stream as a file download
    FileContentResult result = new FileContentResult(pptStream.ToArray(),
        "application/vnd.openxmlformats-officedocument.presentationml.presentation")
    {
        FileDownloadName = "Charts.pptx"
    };
    return result;
}
```

## Полный, готовый к запуску пример

```csharp
using System;
using Aspose.Cells;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main()
        {
            // 1. Load the workbook containing charts
            string excelPath = @"C:\Projects\ChartAndShapes.xlsx";
            Workbook workbook = new Workbook(excelPath);

            // 2. (Optional) Ensure formulas are up‑to‑date
            workbook.CalculateFormula();

            // 3. Export to PowerPoint while preserving shape editability
            string pptxPath = @"C:\Projects\Shapes.pptx";
            workbook.Save(pptxPath, SaveFormat.Pptx);

            Console.WriteLine($"Export complete. PowerPoint saved to: {pptxPath}");
        }
    }
}
```

**Ожидаемый результат:** Консоль выводит сообщение подтверждения, а `Shapes.pptx` открывается в PowerPoint, где каждая диаграмма Excel находится на отдельном слайде. Выбор диаграммы позволяет редактировать её данные, подтверждая, что **возможность редактирования фигур** сохранена.

## Итоги и дальнейшие шаги

Теперь вы знаете, как **экспортировать диаграммы Excel в PowerPoint** с помощью C#, сохраняя их полностью редактируемыми. Ключевым элементом решения является метод `Workbook.Save` с параметром `SaveFormat.Pptx`, функция **Aspose.Cells export**, которая избавляет от необходимости вручную работать с Open XML.

Дальше вы можете изучить:

* Добавление пользовательских заголовков слайдов или заметок с помощью API **Aspose.Slides**.  
* Конвертацию других объектов Excel (таблиц, изображений) вместе с диаграммами.  
* Автоматизацию пакетной обработки нескольких книг в фоновом сервисе.

Экспериментируйте с опциональными настройками, показанными выше, и внедряйте этот шаблон в свои конвейеры отчётности для быстрой и надёжной генерации PowerPoint.

## Что изучать дальше?


В следующих учебниках рассматриваются тесно связанные темы, расширяющие техники, продемонстрированные в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, помогая вам освоить дополнительные возможности API и исследовать альтернативные подходы в собственных проектах.

- [Export Excel chart to PowerPoint with C# – complete Aspose.Cells guide](/cells/english/net/chart-rendering-and-conversion/export-excel-chart-to-powerpoint-with-c-complete-aspose-cell/)
- [How to Export Excel to PowerPoint with C# – Complete Guide](/cells/english/net/converting-excel-files-to-other-formats/how-to-export-excel-to-powerpoint-with-c-complete-guide/)
- [How to Export Shapes from Excel to PowerPoint – Complete Guide](/cells/english/net/drawing-objects/how-to-export-shapes-from-excel-to-powerpoint-complete-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}