---
category: general
date: 2026-10-26
description: Установите область печати и экспортируйте лист Excel в PNG на C#. Узнайте
  о параметрах экспорта изображений, как экспортировать PNG и получить печатное изображение
  из рабочей книги.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set print area
- excel sheet to png
- how to export png
- export excel image
- image export options
language: ru
lastmod: 2026-10-26
og_description: Установите область печати и экспортируйте лист Excel в PNG на C#.
  Этот пошаговый учебник охватывает параметры экспорта изображений и показывает, как
  экспортировать PNG из рабочей книги.
og_image_alt: Screenshot showing an Excel worksheet with the print area set and exported
  as a PNG image
og_title: Установите область печати и экспортируйте лист Excel в PNG – руководство
  по C#
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Set print area and export an Excel sheet to PNG in C#. Learn image
    export options, how to export PNG, and get a printable image from a workbook.
  headline: Set print area and export Excel sheet to PNG in C#
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: Установить область печати и экспортировать лист Excel в PNG в C#
url: /ru/net/rendering-and-export/set-print-area-and-export-excel-sheet-to-png-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Установить область печати и экспортировать лист Excel в PNG на C#

Если вам нужно **установить область печати** перед экспортом листа Excel в PNG, это руководство покажет, как это сделать. Вы увидите полный пример на C#, который настраивает параметры экспорта изображения, корректирует область печати листа и сохраняет результат как изображение.

Экспорт листа Excel в PNG — распространённая задача, когда необходимо вставить снимок листа в отчёт, письмо или веб‑страницу. Приведённый ниже код работает с любой книгой, содержащей сводную таблицу, но техника применима и к обычным диапазонам данных. Внешние инструменты не требуются — достаточно библиотеки Aspose.Cells for .NET.

## Требования

- .NET 6.0 или новее (пример ориентирован на .NET 6, но любой современный .NET будет работать)
- Aspose.Cells for .NET (установите через NuGet: `Install-Package Aspose.Cells`)
- Базовое знакомство с C# и концепциями Excel, такими как листы и области печати

## Шаг 1: Настройка параметров экспорта изображения

Первое, что нужно сделать, — создать экземпляр `ImageOrPrintOptions`. Этот объект сообщает Aspose.Cells, как отрисовывать лист в виде изображения.

```csharp
using Aspose.Cells;
using Aspose.Cells.Rendering;
using System.Drawing.Imaging;

// Define image export options (PNG format)
ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
{
    // Export quality settings can be adjusted here
    ImageFormat = ImageFormat.Png,
    // Optional: set resolution (DPI) for higher‑quality PNGs
    HorizontalResolution = 300,
    VerticalResolution = 300
};
```

**Почему это важно:** `ImageOrPrintOptions` управляет форматом вывода, разрешением и другими деталями рендеринга. Использование PNG обеспечивает без потерь качество, что идеально для отчётов, требующих чёткого текста и графики.

## Шаг 2: Загрузка книги и доступ к целевому листу

```csharp
// Load an existing workbook (replace with your file path)
Workbook wb = new Workbook(@"C:\Temp\SampleWorkbook.xlsx");

// Access the first worksheet in the workbook
Worksheet worksheet = wb.Worksheets[0];
```

**Почему это важно:** Необходимо работать с конкретным объектом `Worksheet`, поскольку область печати задаётся на уровне листа.

## Шаг 3: Определение диапазона, который нужно печатать

Во многих сценариях нужные данные находятся внутри сводной таблицы. Следующий код извлекает диапазон данных первой сводной таблицы на листе.

```csharp
// Get the data range of the first pivot table on the worksheet
CellArea pivotDataRange = worksheet.PivotTables[0].PivotDataRange;
```

Если ваш лист не содержит сводную таблицу, вы можете заменить `pivotDataRange` любой `CellArea`, которую создадите вручную, например:

```csharp
CellArea customRange = new CellArea(0, 0, 20, 10); // A1:K21
```

## Шаг 4: **Установить область печати** в соответствии с выбранным диапазоном

```csharp
// Set the worksheet's print area to match the pivot table's data range
worksheet.PageSetup.PrintArea = pivotDataRange.RefersTo;
```

**Почему это важно:** Область печати указывает Excel (и Aspose.Cells), какие ячейки включать при рендеринге листа в изображение. Выравнивая область печати с диапазоном данных сводной таблицы, вы избегаете пустых полей и гарантируете, что экспортированный PNG содержит только релевантные данные.

## Шаг 5: Экспорт листа в PNG‑изображение

```csharp
// Export the worksheet to an image using the defined options
// and assign the resulting image to the first picture shape on the sheet
worksheet.Pictures[0].Image = worksheet.ToImage(imageOptions);

// Optionally, save the image to a file for external use
worksheet.Pictures[0].Image.Save(@"C:\Temp\WorksheetExport.png", ImageFormat.Png);
```

**Почему это важно:** `worksheet.ToImage` учитывает ранее установленную область печати, поэтому PNG‑файл содержит ровно те ячейки, которые вы определили. Присвоение изображения объекту `PictureShape` позволяет при необходимости вставить его обратно в книгу, а сохранение на диск даёт отдельный файл.

## Полный рабочий пример

Объединив все шаги, получаем автономную программу, которую можно запустить сразу.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;
using System.Drawing.Imaging;

class ExportExcelToPng
{
    static void Main()
    {
        // 1️⃣ Configure image export options (PNG format)
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
        {
            ImageFormat = ImageFormat.Png,
            HorizontalResolution = 300,
            VerticalResolution = 300
        };

        // 2️⃣ Load the workbook
        Workbook wb = new Workbook(@"C:\Temp\SampleWorkbook.xlsx");

        // 3️⃣ Access the first worksheet
        Worksheet worksheet = wb.Worksheets[0];

        // 4️⃣ Get the data range of the first pivot table (or define your own)
        CellArea dataRange = worksheet.PivotTables[0].PivotDataRange;

        // 5️⃣ **Set print area** to the data range
        worksheet.PageSetup.PrintArea = dataRange.RefersTo;

        // 6️⃣ Export the worksheet as PNG
        worksheet.Pictures[0].Image = worksheet.ToImage(imageOptions);
        worksheet.Pictures[0].Image.Save(@"C:\Temp\WorksheetExport.png", ImageFormat.Png);

        Console.WriteLine("Export complete: WorksheetExport.png created.");
    }
}
```

### Ожидаемый результат

Запуск программы создаёт `C:\Temp\WorksheetExport.png`. Открытие файла показывает чёткое PNG‑изображение, содержащее только ячейки, определённые **установленной областью печати** (в данном примере — данные сводной таблицы). Изображение можно вставлять в документы Word, слайды PowerPoint или веб‑страницы без дополнительных шагов конвертации.

## Обработка нескольких листов или сводных таблиц

- **Несколько листов:** Переберите `wb.Worksheets` и повторите шаги 3‑5 для каждого листа, который нужно экспортировать.
- **Несколько сводных таблиц:** Выберите нужный `PivotTables[index]` или пройдитесь по `worksheet.PivotTables`, чтобы экспортировать каждую таблицу отдельно.
- **Отсутствие сводной таблицы:** Создайте `CellArea` вручную (см. комментарий в Шаге 3) и назначьте его в `PrintArea`.

## Практические советы (E‑E‑A‑T)

- **Совет:** Установите `HorizontalResolution` и `VerticalResolution` в 300 DPI для PNG, готовых к печати; более низкие значения уменьшают размер файла для веб‑использования.
- **Осторожно с пустыми объектами изображения:** Если на листе нет объектов изображения, добавьте один перед назначением изображения:

```csharp
if (worksheet.Pictures.Count == 0)
{
    worksheet.Pictures.Add(0, 0, 0, 0);
}
```

- **Производительность:** Повторное использование одного экземпляра `ImageOrPrintOptions` для нескольких листов избегает лишних выделений памяти.
- **Совместимость:** Aspose.Cells 23.9+ полностью поддерживает .NET 6 и новее; более ранние версии могут потребовать корректировок имён API.

## Заключение

Теперь вы знаете, как **установить область печати** и экспортировать Excel

## Что следует изучить дальше?

Следующие руководства охватывают близко связанные темы, построенные на техниках, продемонстрированных в этом руководстве. Каждый ресурс включает полные рабочие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в собственных проектах.

- [Как экспортировать Excel в PNG – полное пошаговое руководство](/cells/english/net/image-and-chart-operations/how-to-export-excel-to-png-full-step-by-step-guide/)
- [Как экспортировать диапазон Excel как изображение с C# и Aspose.Cells](/cells/english/net/image-and-chart-operations/how-to-export-excel-range-as-image-with-c-and-aspose-cells/)
- [Лист Excel в PNG – экспортировать сводную таблицу как PNG на C#](/cells/english/net/conversion-and-rendering/excel-sheet-to-png-export-a-pivot-table-as-png-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}