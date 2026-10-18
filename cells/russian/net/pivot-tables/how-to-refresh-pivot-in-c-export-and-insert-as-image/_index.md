---
category: general
date: 2026-05-04
description: Как обновить сводную таблицу в C# и экспортировать её в PNG, затем вставить
  изображение в лист. Следуйте этому пошаговому руководству с полным кодом.
draft: false
keywords:
- how to refresh pivot
- how to export pivot
- insert image into worksheet
- refresh pivot table code
- load excel workbook c#
language: ru
og_description: Как обновить сводную таблицу в C#? Узнайте, как экспортировать сводную
  таблицу в виде изображения и вставить её в лист с полными примерами кода.
og_title: Как обновить Pivot в C# – экспортировать и вставить как изображение
tags:
- C#
- Aspose.Cells
- Excel Automation
title: Как обновить Pivot в C# — экспортировать и вставить как изображение
url: /ru/net/pivot-tables/how-to-refresh-pivot-in-c-export-and-insert-as-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как обновить сводную таблицу в C# – экспортировать и вставить как изображение

Как обновить сводную таблицу в C# – частая проблема при автоматизации отчетов Excel. В этом руководстве вы увидите точно **как обновить сводную таблицу**, экспортировать её в PNG и поместить это изображение в заполнитель листа — всё в одной, готовой к запуску программе.

Если вам также интересно *как экспортировать сводную таблицу* или нужно **вставить изображение в лист**, вы попали по адресу. Мы пройдемся по каждой строке кода, объясним, почему это важно, и даже рассмотрим несколько граничных случаев, с которыми можно столкнуться в реальных проектах.

---

## Что понадобится

Прежде чем начать, убедитесь, что у вас есть:

- **Aspose.Cells for .NET** (библиотека, предоставляющая `Workbook`, `Worksheet`, `ImageOrPrintOptions` и т.д.). Получить её можно через NuGet: `Install-Package Aspose.Cells`.
- .NET 6 или новее (приведённый код нацелен на .NET 6, но подойдёт любая современная версия).
- Базовые знания C# и работы с файлами — ничего сложного.

И всё. Никаких дополнительных DLL, без COM‑interop, просто чистое консольное приложение C#.

---

## Шаг 1 – Загрузка Excel‑книги в стиле C#

Сначала откроем исходный файл. Здесь реализуется часть **load excel workbook c#**.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Load the workbook from disk
        string inputPath = @"YOUR_DIRECTORY\input.xlsx";
        Workbook workbook = new Workbook(inputPath);

        // Grab the first worksheet (index 0)
        Worksheet worksheet = workbook.Worksheets[0];
```

> **Зачем?**  
> Загрузка книги даёт доступ к её листам, сводным таблицам и заполнителям изображений. Если файл не найден, Aspose бросит понятное `FileNotFoundException`, которое можно перехватить для более дружелюбного UI.

---

## Шаг 2 – Подготовка параметров изображения для экспорта сводной таблицы

Теперь указываем Aspose, как должно выглядеть экспортируемое изображение. Это ядро **how to export pivot**.

```csharp
        // Step 2: Set up image export options – PNG is lossless and widely supported
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
        {
            SaveFormat = SaveFormat.Png,
            // Optional: tweak resolution for sharper images
            HorizontalResolution = 300,
            VerticalResolution = 300
        };
```

> **Совет:**  
> Если нужен JPEG для меньшего размера файла, замените `SaveFormat.Png` на `SaveFormat.Jpeg` и скорректируйте `Quality` соответственно.

---

## Шаг 3 – Код обновления сводной таблицы

Устаревшая сводная таблица показывает старые данные. Обновление гарантирует, что изображение отражает актуальные цифры.

```csharp
        // Step 3: Refresh the first pivot table in the worksheet
        if (worksheet.PivotTables.Count > 0)
        {
            worksheet.PivotTables[0].Refresh();
        }
        else
        {
            Console.WriteLine("No pivot tables found on the first worksheet.");
            return;
        }
```

> **Почему обновлять?**  
> Сводные таблицы кэшируют исходные данные при создании. Если базовый лист изменяется (например, добавляются новые строки), кэш становится устаревшим. Вызов `Refresh()` заставляет Aspose заново запросить диапазон источника, обеспечивая, что экспортируемое изображение не застрянет со старыми итогами.

---

## Шаг 4 – Преобразование обновлённой сводной таблицы в изображение

Вот магическая строка, которая действительно **export pivot** в массив байтов.

```csharp
        // Step 4: Export the refreshed pivot table as an image
        byte[] pivotImage = worksheet.PivotTables[0].ToImage(imageOptions);
```

> **Что вы получаете:**  
> `pivotImage` теперь содержит PNG‑закодированное изображение сводной таблицы, готовое к записи на диск или встраиванию в другое место.

---

## Шаг 5 – Вставка изображения в лист

Здесь мы **insert image into worksheet**. Поместим изображение в первый заполнитель картинки (если он существует).

```csharp
        // Step 5: Insert the image into the first picture placeholder
        if (worksheet.Pictures.Count > 0)
        {
            worksheet.Pictures[0].ImageBytes = pivotImage;
        }
        else
        {
            // If no placeholder exists, add a new picture at cell A1
            int pictureIndex = worksheet.Pictures.Add(0, 0, pivotImage).Index;
            Console.WriteLine($"Added new picture at index {pictureIndex}.");
        }
```

> **Зачем использовать заполнитель?**  
> Многие шаблоны Excel поставляются с предварительно отформатированной фигурой‑картинкой (размер, граница, позиция). Обращаясь к `Pictures[0]`, мы сохраняем макет. Если в шаблоне нет заполнителя, резервный вариант создаст новую картинку, привязанную к ячейке A1.

---

## Шаг 6 – Сохранение книги (по желанию)

Наконец, фиксируем изменения. Можно перезаписать оригинал или записать в новый файл.

```csharp
        // Step 6: Save the updated workbook
        string outputPath = @"YOUR_DIRECTORY\output.xlsx";
        workbook.Save(outputPath);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

> **Ожидаемый результат:**  
> Откройте `output.xlsx` — вы увидите обновлённую сводную таблицу, экспортированную в чёткий PNG, и отображённую в первом слоте картинки. Остальная часть книги остаётся нетронутой.

---

## Полный рабочий пример (готов к копированию)

Ниже полный блок кода, который можно вставить в новый консольный проект. Ничего не пропущено.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Load the workbook
        string inputPath = @"YOUR_DIRECTORY\input.xlsx";
        Workbook workbook = new Workbook(inputPath);
        Worksheet worksheet = workbook.Worksheets[0];

        // Configure image export options (PNG, 300 DPI)
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
        {
            SaveFormat = SaveFormat.Png,
            HorizontalResolution = 300,
            VerticalResolution = 300
        };

        // Refresh the first pivot table
        if (worksheet.PivotTables.Count == 0)
        {
            Console.WriteLine("No pivot tables found.");
            return;
        }
        worksheet.PivotTables[0].Refresh();

        // Export pivot to PNG byte array
        byte[] pivotImage = worksheet.PivotTables[0].ToImage(imageOptions);

        // Insert the image into a picture placeholder or add a new picture
        if (worksheet.Pictures.Count > 0)
        {
            worksheet.Pictures[0].ImageBytes = pivotImage;
        }
        else
        {
            worksheet.Pictures.Add(0, 0, pivotImage);
        }

        // Save the workbook
        string outputPath = @"YOUR_DIRECTORY\output.xlsx";
        workbook.Save(outputPath);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

Запустите программу, откройте полученный файл и убедитесь, что сводная таблица отражает последние данные и отображается как изображение высокого разрешения.

---

## Часто задаваемые вопросы и граничные случаи

| Question | Answer |
|----------|--------|
| **What if the workbook has multiple worksheets?** | Adjust `workbook.Worksheets[0]` to the appropriate index or name (`workbook.Worksheets["Sheet2"]`). |
| **Can I export multiple pivot tables?** | Loop through `worksheet.PivotTables` and repeat steps 3‑4 for each. Store each image in a separate placeholder or combine them into one sheet. |
| **What about large pivot tables causing memory pressure?** | Use `ImageOrPrintOptions` with a lower DPI or export to JPEG to reduce byte‑array size. |
| **Do I need to dispose of anything?** | Aspose objects are managed; the `using` statement isn’t required, but you can wrap `Workbook` in a `using` block if you prefer deterministic cleanup. |
| **Is this compatible with .NET Core?** | Yes. Aspose.Cells supports .NET Core, .NET 5/6, and .NET Framework. Just reference the appropriate NuGet package. |

---

## Советы и лучшие практики

- **Validate paths**: Use `Path.Combine` and `Environment.GetFolderPath` to avoid hard‑coded separators.
- **Error handling**: Wrap the whole `Main` body in a `try/catch` and log `Exception.Message` for production scripts.
- **Template design**: Place a transparent picture shape where you want the pivot image; this preserves column widths and row heights.
- **Performance**: If you only need the image, you can skip saving the workbook entirely and write `pivotImage` to a separate PNG file.

---

## Заключение

Теперь вы знаете **how to refresh pivot** в C#, как экспортировать обновлённый вид в изображение и **insert image into worksheet** без проблем. Полное решение — загрузка книги, настройка параметров экспорта, обновление сводной таблицы, преобразование в PNG и сохранение файла — покрывает весь требуемый рабочий процесс.

Готовы к следующему вызову? Попробуйте сочетать **how to export pivot** с пакетной обработкой нескольких файлов или изучите **refresh pivot table code** для динамических источников данных, таких как базы данных или CSV‑фиды. Принцип тот же: load, refresh, export, insert, save.

Счастливого кодинга, и пусть ваши автоматизации Excel остаются свежими и картинко‑идеальными!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}