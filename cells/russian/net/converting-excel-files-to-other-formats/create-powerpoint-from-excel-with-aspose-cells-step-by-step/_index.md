---
category: general
date: 2026-10-01
description: Создайте PowerPoint из Excel с помощью Aspose.Cells на C#. Экспортируйте
  Excel в PowerPoint и быстро преобразуйте XLSX в PPTX с полным примером кода.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create PowerPoint from Excel
- export Excel to PowerPoint
- convert Excel to PPTX
- convert XLSX to PPTX
- generate PowerPoint from Excel
language: ru
lastmod: 2026-10-01
og_description: Создайте PowerPoint из Excel с помощью Aspose.Cells на C#. Узнайте,
  как экспортировать Excel в PowerPoint и конвертировать XLSX в PPTX за несколько
  строк кода.
og_image_alt: Screenshot of a PowerPoint slide generated from Excel using Aspose.Cells
og_title: Создание PowerPoint из Excel с помощью Aspose.Cells – быстрое руководство
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Create PowerPoint from Excel using Aspose.Cells in C#. Export Excel
    to PowerPoint and convert XLSX to PPTX quickly with a complete code example.
  headline: Create PowerPoint from Excel with Aspose.Cells – step‑by‑step guide
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Office automation
title: Создание PowerPoint из Excel с помощью Aspose.Cells – пошаговое руководство
url: /ru/net/converting-excel-files-to-other-formats/create-powerpoint-from-excel-with-aspose-cells-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание PowerPoint из Excel с помощью Aspose.Cells – пошаговое руководство

Если вам нужно **создать PowerPoint из Excel**, это руководство покажет, как сделать это с помощью Aspose.Cells для .NET. Вы научитесь **экспортировать Excel в PowerPoint**, конвертировать рабочую книгу XLSX в презентацию PPTX и настраивать полученные слайды, не покидая проект C#.

В руководстве рассматривается всё, что необходимо для запуска кода на .NET 6 или новее, включая настройку проекта, требуемые пакеты NuGet и полностью рабочий пример. К концу вы получите файл PowerPoint, содержащий оригинальный график Excel точно так же, как он выглядит в книге.

## Что вам понадобится

| Требование | Причина |
|---|---|
| .NET 6 SDK или новее | Обеспечивает среду выполнения для консольного приложения C# |
| Visual Studio 2022 (или любая IDE) | Обеспечивает простое создание проекта и отладку |
| NuGet‑пакет Aspose.Cells для .NET | Предоставляет класс `Workbook` и API экспорта |
| Файл Excel (`.xlsx`), содержащий хотя бы один график | Исходные данные для слайда PowerPoint |

> **Совет:** Aspose.Cells работает на Windows, Linux и macOS, поэтому вы можете запускать один и тот же код в Docker‑контейнерах или CI‑конвейерах.

## Шаг 1: Создайте новый консольный проект и добавьте Aspose.Cells

Откройте терминал (или консоль менеджера пакетов Visual Studio) и выполните:

```bash
dotnet new console -n ExcelToPptxDemo
cd ExcelToPptxDemo
dotnet add package Aspose.Cells
```

Команда `dotnet add package` загружает последнюю стабильную версию **Aspose.Cells**, которая включает метод `ExportPptx`, используемый далее.

## Шаг 2: Добавьте исходную книгу Excel

Поместите файл Excel, который хотите конвертировать, в папку проекта. В этом руководстве используется `ChartOle.xlsx`, содержащий один график на первом листе.

```
/ExcelToPptxDemo
│   Program.cs
│   ChartOle.xlsx   ← your source workbook
```

## Шаг 3: Напишите код, который **создаёт PowerPoint из Excel**

Откройте `Program.cs` и замените его содержимое следующим кодом. Пример демонстрирует **основную операцию экспорта** и также показывает, как обрабатывать типичные граничные случаи, такие как отсутствие файлов и неподдерживаемые типы графиков.

```csharp
using System;
using System.IO;
using Aspose.Cells;

namespace ExcelToPptxDemo
{
    class Program
    {
        static void Main()
        {
            // Define input and output paths
            string inputPath = Path.Combine(AppContext.BaseDirectory, "ChartOle.xlsx");
            string outputPath = Path.Combine(AppContext.BaseDirectory, "Exported.pptx");

            // Verify that the source workbook exists
            if (!File.Exists(inputPath))
            {
                Console.WriteLine($"Error: The file '{inputPath}' was not found.");
                return;
            }

            try
            {
                // Load the Excel workbook that contains the chart
                var workbook = new Workbook(inputPath);

                // Export the first worksheet as a PowerPoint presentation
                // This call performs the **convert Excel to PPTX** operation.
                workbook.Worksheets[0].ExportPptx(outputPath);

                Console.WriteLine($"Success: PowerPoint file created at '{outputPath}'.");
            }
            catch (Exception ex)
            {
                // Catch any errors thrown by Aspose.Cells (e.g., unsupported chart)
                Console.WriteLine($"Export failed: {ex.Message}");
            }
        }
    }
}
```

### Почему это работает

* `Workbook` читает весь файл Excel, включая встроенные графики, таблицы и форматирование.  
* `ExportPptx` преобразует активный лист в набор слайдов PPTX. Метод автоматически преобразует графики Excel в формы PowerPoint, сохраняя визуальное соответствие.  
* Код оборачивает операцию в блок `try/catch`, чтобы выводить ошибки, такие как сбои **convert XLSX to PPTX**, вызванные повреждёнными файлами.

## Шаг 4: Запустите программу и проверьте результат

Выполните приложение:

```bash
dotnet run
```

Вы должны увидеть сообщение в консоли:

```
Success: PowerPoint file created at '.../Exported.pptx'.
```

Откройте `Exported.pptx` в Microsoft PowerPoint или любом совместимом просмотрщике. Первый слайд отображает график точно так же, как он выглядел в `ChartOle.xlsx`. Это подтверждает, что вы успешно **сгенерировали PowerPoint из Excel**.

## Шаг 5: Продвинутое – экспорт нескольких листов или пользовательские макеты слайдов

Базовый пример экспортирует только первый лист. В реальных сценариях вам может потребоваться:

* **Экспортировать несколько листов** в отдельные слайды.  
* **Управлять размером слайда** или добавить заполнитель заголовка.  
* **Включать скрытые листы** в конвертацию.

Ниже приведён компактный фрагмент, который перебирает все листы и добавляет каждый как отдельный слайд:

```csharp
// Export each worksheet as a separate slide
var pptxPath = Path.Combine(AppContext.BaseDirectory, "FullExport.pptx");
var presentation = new Presentation(); // Aspose.Slides.Presentation, if you have the Slides library

foreach (Worksheet ws in workbook.Worksheets)
{
    // Convert worksheet to an image first (optional for custom layout)
    var imgStream = new MemoryStream();
    ws.PageSetup.PrintArea = ws.Cells.MaxDisplayRange; // ensure full content
    ws.Pictures[0].ToImage(imgStream, ImageFormat.Png);

    // Add a new slide and insert the image
    var slide = presentation.Slides.AddEmptySlide(presentation.SlideSize.Size);
    slide.Shapes.AddPictureFrame(ShapeType.Rectangle, 0, 0, presentation.SlideSize.Size.Width, presentation.SlideSize.Size.Height, imgStream);
}

// Save the final presentation
presentation.Save(pptxPath, SaveFormat.Pptx);
```

> **Примечание:** Продвинутый фрагмент требует библиотеки **Aspose.Slides for .NET**. Если вам нужен только простой экспорт одного листа, вызов `ExportPptx`, показанный ранее, достаточен.

## Распространённые подводные камни и как их избежать

| Проблема | Причина | Решение |
|---|---|---|
| Пустой слайд после экспорта | Лист не содержит видимых объектов | Убедитесь, что перед вызовом `ExportPptx` на листе присутствует хотя бы один график, таблица или форма. |
| Отсутствуют шрифты в PowerPoint | Шрифт не установлен на машине, где открывается PPTX | Встроите необходимые шрифты в книгу Excel или установите их на целевой системе. |
| Неожиданное масштабирование | Большой график превышает размеры слайда | Отрегулируйте свойство `PageSetup.Zoom` листа перед экспортом. |
| `convert XLSX to PPTX` бросает `NotSupportedException` | Тип графика не поддерживается Aspose.Cells (например, 3‑D карты) | Замените график на поддерживаемый тип или сначала экспортируйте лист как изображение. |

Устранение этих граничных случаев обеспечивает надёжный процесс **export Excel to PowerPoint** в производственных средах.

## Заключение

Теперь вы знаете, как **создавать PowerPoint из Excel** с помощью Aspose.Cells для .NET. В руководстве рассмотрено:

* Настройка проекта и установка NuGet  
* Загрузка книги Excel и вызов `ExportPptx`  
* Запуск кода и подтверждение сгенерированного PPTX  
* Расширение решения для обработки нескольких листов и пользовательских макетов  
* Практические советы по избежанию распространённых проблем конвертации  

Обладая этими знаниями, вы можете автоматизировать генерацию отчётов, создавать конвейеры презентаций или интегрировать конвертацию Excel‑в‑PowerPoint в любое приложение C#. Экспериментируйте с разными типами графиков, добавляйте заголовки слайдов или комбинируйте экспорт с Aspose.Slides для создания полнофункциональных презентаций.

--- 

*Готовы узнать больше? Ознакомьтесь с связанными темами, такими как **convert Excel to PDF**, **embed Excel data in Word**, или **use Aspose.Slides to programmatically edit PPTX files**.*

## Что вам стоит изучить дальше?

Следующие руководства охватывают тесно связанные темы, которые развивают техники, продемонстрированные в этом пособии. Каждый ресурс содержит полностью рабочие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в собственных проектах.

- [Convert Excel To Powerpoint Aspose Cells Dotnet](/cells/german/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [Convert Excel To Powerpoint Aspose Cells Dotnet](/cells/french/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [Convert Excel To Powerpoint Aspose Cells Dotnet](/cells/spanish/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}