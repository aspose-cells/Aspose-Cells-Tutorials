---
category: general
date: 2026-05-23
description: Конвертировать Excel в PowerPoint на C# с помощью Aspose.Cells. Узнайте,
  как создать PowerPoint из файла Excel, сохранить рабочую книгу как PowerPoint и
  экспортировать таблицу в PowerPoint.
draft: false
keywords:
- convert excel to powerpoint
- create powerpoint from excel file
- save workbook as powerpoint
- export spreadsheet to powerpoint
- convert workbook to pptx
language: ru
og_description: Конвертировать Excel в PowerPoint на C#. Этот учебник показывает,
  как создать презентацию PowerPoint из файла Excel, сохранить книгу как PowerPoint
  и экспортировать таблицу в PowerPoint.
og_title: Конвертировать Excel в PowerPoint с помощью C# – Полное руководство
schemas:
- author: Aspose
  dateModified: '2026-05-23'
  description: Convert Excel to PowerPoint in C# using Aspose.Cells. Learn how to
    create PowerPoint from Excel file, save workbook as PowerPoint, and export spreadsheet
    to PowerPoint.
  headline: Convert Excel to PowerPoint with C# – Complete Guide
  type: TechArticle
tags:
- C#
- Aspose.Cells
- Excel
- PowerPoint
- Automation
title: Конвертировать Excel в PowerPoint с помощью C# – Полное руководство
url: /ru/net/converting-excel-files-to-other-formats/convert-excel-to-powerpoint-with-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Конвертация Excel в PowerPoint с C# – Полное руководство

Когда‑нибудь вам нужно было **convert Excel to PowerPoint**, но вы не знали, с чего начать? Вы не одиноки — многие разработчики сталкиваются с тем же, когда хотят превратить таблицу в набор слайдов без ручного копирования данных.  

В этом руководстве мы пройдем через **полное, сквозное решение**, которое позволяет **create PowerPoint from Excel file** с помощью C#. Вы увидите, как **save workbook as PowerPoint**, настроить параметры и даже проверить результат — всё это в нескольких строках кода.

> **What you’ll get:** готовое к запуску консольное приложение C#, которое берёт `input.xlsx` и создаёт `output.pptx` в той же папке, плюс советы по работе с изображениями, диаграммами и типичными подводными камнями.

---

## Предварительные требования

Перед тем как начать, убедитесь, что у вас есть:

- **.NET 6.0** (или любая современная версия .NET), установлен.
- **Действующая лицензия** для **Aspose.Cells for .NET** (бесплатная пробная версия подходит для тестирования).
- Excel‑файл (`input.xlsx`), который вы хотите превратить в презентацию.
- Любимая IDE — Visual Studio, VS Code, Rider — что угодно.

Никакие другие сторонние библиотеки не требуются.

---

## Шаг 1: Конвертация Excel в PowerPoint – Загрузка книги

Сначала откроем Excel‑файл, чтобы Aspose.Cells мог с ним работать. Класс `Workbook` — это шлюз ко всем листам, ячейкам и диаграммам вашей таблицы.

```csharp
using Aspose.Cells;
using Aspose.Cells.Rendering;

// Load the Excel workbook from disk
Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");

// Optional: Verify that the workbook loaded correctly
Console.WriteLine($"Loaded workbook with {workbook.Worksheets.Count} worksheet(s).");
```

> **Why this matters:** Загрузка книги дает нам представление в памяти, которое позже можно отрисовать в виде слайдов PowerPoint. Если путь к файлу неверный, конструктор `Workbook` выбросит исключение, позволяя быстро обнаружить ошибку.

---

## Шаг 2: Настройка параметров экспорта в PowerPoint

Aspose.Cells использует класс `ImageOrPrintOptions` для управления тем, как книга превращается в презентацию. Ключевое свойство — `SaveFormat`, которое мы устанавливаем в `SaveFormat.Pptx`.

```csharp
// Set up options for exporting to PowerPoint
ImageOrPrintOptions saveOptions = new ImageOrPrintOptions
{
    // This tells Aspose.Cells we want a PPTX file, not an image or PDF
    SaveFormat = SaveFormat.Pptx,

    // Optional: Adjust slide size or image quality if needed
    // ImageResolution = 300,
    // SlideSize = SlideSizeType.Widescreen
};
```

> **Pro tip:** Если нужен конкретный размер слайда (например, 16:9 widescreen), измените свойство `SlideSize`. В остальных случаях значение по умолчанию подходит для большинства сценариев.

---

## Шаг 3: Сохранение книги как PowerPoint

Теперь действительно выполняем конвертацию. Метод `Save` принимает путь к выходному файлу и только что определённые параметры.

```csharp
// Save the workbook as a PPTX file
string outputPath = @"YOUR_DIRECTORY\output.pptx";
workbook.Save(outputPath, saveOptions);

Console.WriteLine($"Successfully converted Excel to PowerPoint: {outputPath}");
```

> **What’s happening under the hood?** Aspose.Cells преобразует каждый лист в отдельный слайд, сохраняя форматирование ячеек, цвета и даже простые диаграммы. В результате получается чистый, редактируемый файл PowerPoint, который можно открыть в Microsoft PowerPoint или любом совместимом просмотрщике.

---

## Шаг 4: Проверка сгенерированного PPTX

Быстрая проверка помогает обнаружить проблемы конвертации на раннем этапе. Откройте файл программно (с помощью Aspose.Slides) или вручную в PowerPoint.

```csharp
using Aspose.Slides;

// Load the generated PPTX just to confirm it’s readable
Presentation ppt = new Presentation(outputPath);
Console.WriteLine($"PPTX contains {ppt.Slides.Count} slide(s).");

// Optionally, export the first slide as an image for visual verification
ppt.Slides[0].GetThumbnail(1f, 1f).Save(@"YOUR_DIRECTORY\first_slide.png");
```

Если количество слайдов совпадает с числом листов, всё в порядке.

---

## Шаг 5: Распространённые проблемы и как их избежать

| Симптом | Вероятная причина | Решение |
|---------|-------------------|--------|
| **Пустые слайды** | Лист содержит только формулы, которые не были вычислены. | Вызовите `workbook.CalculateFormula();` перед сохранением. |
| **Искажённые диаграммы** | Отрисовка диаграмм отключена в лицензии. | Убедитесь, что ваша лицензия Aspose.Cells включает поддержку диаграмм. |
| **Файл не найден** | Неправильный путь `YOUR_DIRECTORY` или отсутствует `input.xlsx`. | Используйте `Path.Combine(Environment.CurrentDirectory, "input.xlsx")` для относительных путей. |
| **Большой размер PPTX** | Изображения высокого разрешения или множество скрытых строк/столбцов. | Уменьшите `ImageResolution` или скройте ненужные строки/столбцы перед конвертацией. |

---

## Шаг 6: Расширение конвертации – Добавление изображений и пользовательских слайдов

Иногда требуется больше, чем простое сопоставление лист‑слайд. После конвертации можно добавить пользовательские слайды с помощью **Aspose.Slides**.

```csharp
using Aspose.Slides.Export;

// Load the PPTX we just created
Presentation presentation = new Presentation(outputPath);

// Add a title slide at the beginning
ISlide titleSlide = presentation.Slides.InsertEmptySlide(0, presentation.LayoutSlides[0]);
titleSlide.Shapes.AddAutoShape(ShapeType.Rectangle, 50, 50, 600, 100)
    .TextFrame.Text = "Quarterly Sales Overview";

// Save the extended deck
presentation.Save(@"YOUR_DIRECTORY\final_output.pptx", SaveFormat.Pptx);
Console.WriteLine("Added custom title slide.");
```

> **Why mix libraries?** Aspose.Cells берёт на себя тяжёлую работу по превращению листов в слайды, а Aspose.Slides позволяет тонко настроить презентацию — добавить логотипы, переходы или заметки докладчика.

---

## Полный рабочий пример

Ниже представлен полный код программы, который можно скопировать в новый консольный проект. В нём присутствуют все директивы `using`, обработка ошибок и комментарии.

```csharp
using System;
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Rendering;
using Aspose.Slides;
using Aspose.Slides.Export;

class ExcelToPowerPoint
{
    static void Main()
    {
        // Define paths – adjust as needed
        string inputPath = Path.Combine(Environment.CurrentDirectory, "input.xlsx");
        string outputPath = Path.Combine(Environment.CurrentDirectory, "output.pptx");

        // -------------------------------------------------
        // Step 1: Load the Excel workbook
        // -------------------------------------------------
        Workbook workbook;
        try
        {
            workbook = new Workbook(inputPath);
            Console.WriteLine($"Loaded workbook with {workbook.Worksheets.Count} sheet(s).");
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Error loading workbook: {ex.Message}");
            return;
        }

        // -------------------------------------------------
        // Step 2: Set up PowerPoint export options
        // -------------------------------------------------
        ImageOrPrintOptions saveOptions = new ImageOrPrintOptions
        {
            SaveFormat = SaveFormat.Pptx,
            // Uncomment to tweak resolution or slide size
            // ImageResolution = 200,
            // SlideSize = SlideSizeType.Widescreen
        };

        // -------------------------------------------------
        // Step 3: Save the workbook as PowerPoint
        // -------------------------------------------------
        try
        {
            workbook.Save(outputPath, saveOptions);
            Console.WriteLine($"Successfully converted Excel to PowerPoint: {outputPath}");
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Error during conversion: {ex.Message}");
            return;
        }

        // -------------------------------------------------
        // Step 4: Verify the PPTX (optional but recommended)
        // -------------------------------------------------
        try
        {
            using (Presentation ppt = new Presentation(outputPath))
            {
                Console.WriteLine($"PPTX contains {ppt.Slides.Count} slide(s).");
                // Export first slide as PNG for quick visual check
                ppt.Slides[0].GetThumbnail(1f, 1f).Save("first_slide.png");
            }
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Error verifying PPTX: {ex.Message}");
        }

        // -------------------------------------------------
        // Step 5: (Optional) Add a custom title slide
        // -------------------------------------------------
        try
        {
            using (Presentation pres = new Presentation(outputPath))
            {
                ISlide titleSlide = pres.Slides.InsertEmptySlide(0, pres.LayoutSlides[0]);
                titleSlide.Shapes.AddAutoShape(ShapeType.Rectangle, 50, 50, 600, 100)
                    .TextFrame.Text = "Quarterly Sales Overview";

                pres.Save("final_output.pptx", SaveFormat.Pptx);
                Console.WriteLine("Added custom title slide and saved final_output.pptx");
            }
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Error adding custom slide: {ex.Message}");
        }
    }
}
```

**Ожидаемый вывод при запуске программы** (при условии простого `input.xlsx` с двумя листами):

```
Loaded workbook with 2 sheet(s).
Successfully converted Excel to PowerPoint: C:\Path\output.pptx
PPTX contains 2 slide(s).
Added custom title slide and saved final_output.pptx
```

Откройте `final_output.pptx` в PowerPoint — вы должны увидеть титульный слайд, за которым следуют два слайда, отражающие листы Excel.

---

## Заключение

Теперь у вас есть **полный, готовый к продакшену рецепт конвертации Excel в PowerPoint** с помощью C#. От загрузки книги, настройки параметров экспорта, сохранения файла и до добавления пользовательских слайдов — руководство охватывает каждый необходимый шаг.  

Далее попробуйте **export spreadsheet to PowerPoint** с более богатым содержимым — внедрите диаграммы, примените темы слайдов или автоматизируйте пакетную конвертацию десятков книг. Тот же шаблон работает для **save workbook as PowerPoint** в автоматизированных конвейерах отчётности, делая ваш процесс представления данных более гладким, чем когда‑либо.

Есть вопросы о **create powerpoint from excel**

## Связанные руководства

- [Как конвертировать Excel в PowerPoint с помощью Aspose.Cells для .NET: Полное руководство](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [Конвертировать Excel в PowerPoint Aspose Cells Dotnet](/cells/german/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [Конвертировать Excel в PowerPoint Aspose Cells Dotnet](/cells/french/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}