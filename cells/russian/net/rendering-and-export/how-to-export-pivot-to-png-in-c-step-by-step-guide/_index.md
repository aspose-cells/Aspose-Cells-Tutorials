---
category: general
date: 2026-02-14
description: Как экспортировать сводную таблицу из книги Excel в PNG с помощью Aspose.Cells.
  Узнайте, как загрузить книгу Excel, отобразить сводную таблицу в виде изображения
  и без усилий сохранить её.
draft: false
keywords:
- how to export pivot
- export excel pivot
- load excel workbook
- pivot table to png
- save pivot image
language: ru
og_description: Как экспортировать сводную таблицу из Excel в PNG в C#. Это руководство
  показывает, как загрузить книгу Excel, отобразить сводную таблицу в PNG и сохранить
  изображение сводной таблицы.
og_title: как экспортировать pivot в png в C# – полный учебник
tags:
- Aspose.Cells
- C#
- Excel automation
title: Как экспортировать Pivot в PNG в C# — пошаговое руководство
url: /ru/net/rendering-and-export/how-to-export-pivot-to-png-in-c-step-by-step-guide/
---

produce final content with all translations.

Check for any missed bold terms: In title we removed bold. That's fine.

Make sure we didn't translate code block placeholders.

Check list formatting: keep dash and spaces.

Now produce final answer.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# как экспортировать сводную таблицу в PNG в C# – Полный учебник

Когда‑нибудь задавались вопросом, **как экспортировать сводную таблицу** из листа Excel в чёткий PNG‑файл? Вы не одиноки — разработчикам часто нужен быстрый визуальный образ сводной таблицы для отчётов, панелей мониторинга или вложений в электронную почту. Хорошая новость? С помощью Aspose.Cells вы можете загрузить книгу Excel, получить первую сводную таблицу, превратить её в изображение и **сохранить изображение сводной таблицы** всего за несколько строк кода C#.

В этом учебнике мы пройдём всё, что вам нужно: от основ **load excel workbook**, до рендеринга **pivot table to png**, и, наконец, сохранения файла на диск. К концу вы получите автономную, исполняемую программу, которую можно добавить в любой проект .NET.

---

## Что вам понадобится

- **.NET 6 или новее** (код также работает на .NET Framework 4.7+)
- **Aspose.Cells for .NET** пакет NuGet (версия 23.12 на момент написания)
- Файл Excel (`input.xlsx`), содержащий хотя бы одну сводную таблицу
- Среда Visual Studio или VS Code, с которой вам удобно работать

Никаких дополнительных библиотек, без COM‑interop и без необходимости установки Excel — Aspose.Cells обрабатывает всё в памяти.

---

## Шаг 1 – Загрузка книги Excel

Первое, что нужно сделать, — загрузить книгу в память. Здесь ключевое слово **load excel workbook** проявляет себя.

```csharp
using System.Drawing;
using Aspose.Cells;

class PivotExport
{
    static void Main()
    {
        // Step 1: Load the workbook from disk
        // Adjust the path to where your input.xlsx lives
        var workbookPath = @"YOUR_DIRECTORY\input.xlsx";
        Workbook workbook = new Workbook(workbookPath);

        // Grab the first worksheet (you can also select by name)
        Worksheet worksheet = workbook.Worksheets[0];
```

> **Почему это важно:**  
> Загрузка книги один раз делает операцию быстрой и предотвращает блокировку исходного файла. Aspose.Cells читает файл в управляемый поток, поэтому позже вы можете загружать его из массива байтов или сетевого расположения.

---

## Шаг 2 – Рендеринг сводной таблицы в изображение

Теперь, когда книга находится в памяти, мы можем получить доступ к её сводным таблицам. API предоставляет удобный метод `ToImage()`, который возвращает `System.Drawing.Image`.

```csharp
        // Step 2: Find the first pivot table on the worksheet
        if (worksheet.PivotTables.Count == 0)
        {
            System.Console.WriteLine("No pivot tables found on the first worksheet.");
            return;
        }

        // Export the first pivot table as an image
        Image pivotImage = worksheet.PivotTables[0].ToImage();

        // Optional: tweak image quality or size here
        // pivotImage.SetResolution(300, 300);
```

> **Полезный совет:** Если ваша книга содержит несколько сводных таблиц, просто пройдитесь в цикле по `worksheet.PivotTables` и экспортируйте каждую. Вызов `ToImage()` учитывает текущий вид (фильтры, срезы и т.д.), поэтому вы получаете именно то, что видит пользователь.

---

## Шаг 3 – Сохранение сгенерированного PNG‑файла

Наконец, мы сохраняем bitmap на диск. Перегрузка `Save` автоматически выбирает формат на основе расширения файла.

```csharp
        // Step 3: Save the image as PNG
        var outputPath = @"YOUR_DIRECTORY\pivot.png";
        pivotImage.Save(outputPath, System.Drawing.Imaging.ImageFormat.Png);

        System.Console.WriteLine($"Pivot table exported successfully to {outputPath}");
    }
}
```

> При запуске программы создаётся `pivot.png`, который выглядит точно так же, как сводная таблица в Excel. Откройте его в любом просмотрщике изображений, и вы увидите строки, столбцы и итоги, отрисованные пиксель‑в‑пиксель.

---

## Обработка распространённых граничных случаев

### Несколько листов или сводных таблиц

Если ваша книга хранит сводную таблицу на другом листе, измените индекс листа или используйте имя листа:

```csharp
Worksheet ws = workbook.Worksheets["SalesData"];
```

Затем цикл:

```csharp
foreach (PivotTable pt in ws.PivotTables)
{
    Image img = pt.ToImage();
    img.Save($"pivot_{pt.Name}.png", ImageFormat.Png);
}
```

### Большие сводные таблицы

Для очень больших сводных таблиц размер изображения по умолчанию может быть огромным. Вы можете контролировать размер рендеринга, изменив коэффициент масштабирования листа перед вызовом `ToImage()`:

```csharp
worksheet.PageSetup.Zoom = 75; // renders at 75 % of original size
```

### Управление памятью

`System.Drawing.Image` реализует `IDisposable`. В production‑коде оберните изображение в блок `using`, чтобы своевременно освобождать нативные ресурсы:

```csharp
using (Image pivotImage = worksheet.PivotTables[0].ToImage())
{
    pivotImage.Save(outputPath, ImageFormat.Png);
}
```

---

## Полный рабочий пример

Ниже приведена полная, готовая к запуску программа. Вставьте её в новый консольный проект, скорректируйте пути к файлам и нажмите **F5**.

```csharp
using System;
using System.Drawing;
using System.Drawing.Imaging;
using Aspose.Cells;

namespace PivotExportDemo
{
    class Program
    {
        static void Main()
        {
            // -----------------------------------------------------------------
            // 1️⃣ Load the Excel workbook (load excel workbook)
            // -----------------------------------------------------------------
            string inputFile = @"YOUR_DIRECTORY\input.xlsx";
            Workbook wb = new Workbook(inputFile);
            Worksheet ws = wb.Worksheets[0]; // first worksheet

            // -----------------------------------------------------------------
            // 2️⃣ Ensure a pivot table exists and export it (how to export pivot)
            // -----------------------------------------------------------------
            if (ws.PivotTables.Count == 0)
            {
                Console.WriteLine("No pivot tables found. Exiting.");
                return;
            }

            // Export the first pivot table as a PNG image (pivot table to png)
            using (Image img = ws.PivotTables[0].ToImage())
            {
                // -----------------------------------------------------------------
                // 3️⃣ Save the pivot image to disk (save pivot image)
                // -----------------------------------------------------------------
                string outputFile = @"YOUR_DIRECTORY\pivot.png";
                img.Save(outputFile, ImageFormat.Png);
                Console.WriteLine($"Pivot exported successfully → {outputFile}");
            }
        }
    }
}
```

**Ожидаемый вывод:**  
```
Pivot exported successfully → YOUR_DIRECTORY\pivot.png
```

И файл `pivot.png` будет содержать визуальную реплику оригинальной сводной таблицы.

---

## Часто задаваемые вопросы

- **Работает ли это с файлами .xlsx, содержащими диаграммы?**  
  Да. Метод `ToImage()` учитывает только макет сводной таблицы; диаграммы не затрагиваются.

- **Можно ли экспортировать в JPEG или BMP вместо PNG?**  
  Конечно — просто измените аргумент `ImageFormat` в `Save`. PNG без потерь, поэтому мы рекомендуем его для чётких данных.

- **Что делать, если книга защищена паролем?**  
  Загрузите её, используя перегрузку с паролем:  
  `Workbook wb = new Workbook(inputFile, new LoadOptions { Password = "mySecret" });`

---

## Подведение итогов

Мы только что рассмотрели **как экспортировать сводную таблицу** из файла Excel в PNG‑изображение с помощью Aspose.Cells. Шаги — **load excel workbook**, найти **pivot table to png** и **save pivot image** — просты, но достаточно мощны для реальных конвейеров отчётности.

Далее вы можете исследовать:

- Автоматизация экспорта всех сводных таблиц в папке (export excel pivot in bulk)  
- Встраивание PNG в PDF или HTML‑письмо (combine with iTextSharp or Razor)  
- Добавление водяных знаков или пользовательского стиля к экспортированному изображению  

Попробуйте их и позвольте изображениям говорить за вас в следующей панели мониторинга.

---

![пример вывода экспорта сводной таблицы](assets/pivot-export-example.png "пример вывода экспорта сводной таблицы")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}