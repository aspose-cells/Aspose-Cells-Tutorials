---
category: general
date: 2026-09-24
description: Экспорт диапазона Excel в виде изображения на C# с использованием Aspose.Cells
  — пошаговое руководство по сохранению области листа в формате PNG или JPEG.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel range as image
- Aspose.Cells export range
- C# Excel to PNG
- ImageOrPrintOptions usage
- export pivot table as image
language: ru
lastmod: 2026-09-24
og_description: Экспорт диапазона Excel в виде изображения на C# с Aspose.Cells. Узнайте,
  как за несколько минут преобразовать любую область листа, включая сводные таблицы,
  в PNG или JPEG.
og_image_alt: Screenshot of a C# program exporting an Excel range to a PNG image
og_title: Экспорт диапазона Excel в изображение с помощью C# — полное руководство
  по Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-09-24'
  description: Export excel range as image in C# using Aspose.Cells – step‑by‑step
    guide to save a worksheet area as PNG or JPEG.
  headline: How to export excel range as image with C# and Aspose.Cells
  type: TechArticle
- description: Export excel range as image in C# using Aspose.Cells – step‑by‑step
    guide to save a worksheet area as PNG or JPEG.
  name: How to export excel range as image with C# and Aspose.Cells
  steps:
  - name: '**Load** the workbook from disk.'
    text: '**Load** the workbook from disk.'
  - name: '**Define** the cell area that will become the image (the *print area*).'
    text: '**Define** the cell area that will become the image (the *print area*).'
  - name: '**Export** the area using `ImageOrPrintOptions` and write the file.'
    text: '**Export** the area using `ImageOrPrintOptions` and write the file.'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
- Image export
title: Как экспортировать диапазон Excel в виде изображения с помощью C# и Aspose.Cells
url: /ru/net/image-and-chart-operations/how-to-export-excel-range-as-image-with-c-and-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как экспортировать диапазон Excel в виде изображения с помощью C# и Aspose.Cells

Если вам нужно **export excel range as image** в .NET‑приложении, это руководство покажет вам полное, готовое к запуску решение. Независимо от того, публикуете ли вы панель мониторинга, встраиваете сводную таблицу в веб‑страницу или генерируете миниатюру отчёта, вы можете превратить любую область листа в PNG (или JPEG) всего несколькими строками кода C#.

В этом руководстве вы узнаете, как:

* Загрузить существующую книгу (`Workbook` class)  
* Определить точный диапазон ячеек, который нужно захватить (`PrintArea`)  
* Настроить параметры экспорта изображения (`ImageOrPrintOptions`)  
* Сохранить полученную картинку на диск  

Все предварительные требования, граничные случаи и распространённые подводные камни рассмотрены, чтобы вы могли адаптировать код к своим проектам без неожиданностей.

## Предварительные требования

| Требование | Причина |
|-------------|--------|
| **Aspose.Cells for .NET** (latest version) | Предоставляет API `Workbook`, `Worksheet` и `ImageOrPrintOptions`, используемые в примере. |
| **.NET 6.0 or later** | Пример ориентирован на .NET 6, но любой .NET Core/Framework, поддерживающий Aspose.Cells, подходит. |
| **A valid Excel file** (e.g., `input.xlsx`) | Книга, которую вы хотите конвертировать. |
| **Write permission to the output folder** | Необходима для успешного выполнения `Save`. |

You can install Aspose.Cells via NuGet:

```bash
dotnet add package Aspose.Cells
```

## Экспорт диапазона Excel в изображение – обзор процесса

Операция состоит из трёх логических фаз:

1. **Load** книгу с диска.  
2. **Define** область ячеек, которая станет изображением ( *print area*).  
3. **Export** область с помощью `ImageOrPrintOptions` и запишите файл.

Ниже каждая фаза разбита на отдельный шаг с полным исходным кодом и объяснением.

## Шаг 1: Загрузка книги

```csharp
using Aspose.Cells;
using System.Drawing.Imaging;

// Path to the source Excel file
string inputPath = @"YOUR_DIRECTORY\input.xlsx";

// Create a Workbook object – this reads the file into memory
Workbook workbook = new Workbook(inputPath);
```

**Почему это важно:**  
`Workbook` — точка входа для всех операций с Excel. Однократная загрузка файла снижает использование памяти и позволяет позже получить доступ к любому листу.

## Шаг 2: Доступ к целевому листу

```csharp
// Get the first worksheet (index 0). Change the index or use the sheet name as needed.
Worksheet sheet = workbook.Worksheets[0];
```

**Подсказка:** Если вам нужен конкретный лист по имени, замените индекс на `workbook.Worksheets["SheetName"]`. Это предотвращает ошибки при изменении структуры книги.

## Шаг 3: Определение диапазона для экспорта

```csharp
// Define the cell range that will be exported.
// Example: A1:G20 captures a typical pivot‑table area.
sheet.PageSetup.PrintArea = "A1:G20";
```

**Почему устанавливать `PrintArea`?**  
Aspose.Cells рендерит *print area* при создании изображения. Ограничивая её точным диапазоном, вы избегаете лишних пустых областей и повышаете производительность.

### Альтернатива: Экспортировать весь лист

Если вам нужен весь лист, просто опустите присваивание `PrintArea`. По умолчанию Aspose.Cells использует используемый диапазон листа.

## Шаг 4: Настройка параметров экспорта изображения

```csharp
// Create an ImageOrPrintOptions object to control the output format.
ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
{
    // Choose PNG for lossless quality; change to Jpeg for smaller files.
    ImageFormat = ImageFormat.Png,

    // Optional: set the resolution (DPI). Higher DPI yields sharper images.
    HorizontalResolution = 300,
    VerticalResolution = 300,

    // Optional: set the page orientation if the range is wide.
    PageOrientation = PageOrientationType.Landscape
};
```

**Объяснение ключевых свойств:**

* `ImageFormat` – определяет тип файла (`Png`, `Jpeg`, `Bmp` и т.д.). PNG идеален для графиков и текста, так как сохраняет чёткие границы.  
* `HorizontalResolution` / `VerticalResolution` – контролируют плотность пикселей. Для веб‑миниатюр достаточно 96 DPI; для графики, готовой к печати, рекомендуется 300 DPI.  
* `PageOrientation` – помогает, когда выбранный диапазон шире, чем выше.  

## Шаг 5: Экспорт диапазона в файл изображения

```csharp
// Define the output path for the image
string outputPath = @"YOUR_DIRECTORY\range.png";

// Save the first picture on the worksheet as an image.
// The Pictures collection is automatically populated after setting PrintArea.
sheet.Pictures[0].Save(outputPath, imgOptions);
```

**Что происходит под капотом:**  
Когда установлен `PrintArea`, Aspose.Cells генерирует временную картинку, представляющую эту область. Затем объект `Pictures[0]` сохраняется с использованием указанных вами параметров.

### Обработка листов без изображений

Если лист ещё не содержит изображения (например, совершенно новый файл), вы можете создать его «на лету»:

```csharp
// Create a picture from the defined range and add it to the sheet
Picture pic = sheet.Pictures[sheet.Pictures.Add(0, 0, sheet.PageSetup.PrintArea)];
pic.Save(outputPath, imgOptions);
```

## Полный, исполняемый пример

Объединив всё вместе, представляем автономное консольное приложение, которое вы можете скопировать, вставить и запустить:

```csharp
using Aspose.Cells;
using System.Drawing.Imaging;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the workbook
        string inputPath = @"YOUR_DIRECTORY\input.xlsx";
        Workbook workbook = new Workbook(inputPath);

        // 2️⃣ Access the first worksheet
        Worksheet sheet = workbook.Worksheets[0];

        // 3️⃣ Define the range to export (e.g., a pivot table)
        sheet.PageSetup.PrintArea = "A1:G20";

        // 4️⃣ Set image export options (PNG, 300 DPI, landscape)
        ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
        {
            ImageFormat = ImageFormat.Png,
            HorizontalResolution = 300,
            VerticalResolution = 300,
            PageOrientation = PageOrientationType.Landscape
        };

        // 5️⃣ Save the picture as an image file
        string outputPath = @"YOUR_DIRECTORY\range.png";

        // Ensure a picture exists; create one if necessary
        Picture pic;
        if (sheet.Pictures.Count == 0)
        {
            pic = sheet.Pictures[sheet.Pictures.Add(0, 0, sheet.PageSetup.PrintArea)];
        }
        else
        {
            pic = sheet.Pictures[0];
        }

        pic.Save(outputPath, imgOptions);

        System.Console.WriteLine($"Export completed: {outputPath}");
    }
}
```

**Ожидаемый результат:**  
Файл с именем `range.png` появляется в `YOUR_DIRECTORY`. При открытии он показывает точные ячейки от **A1 до G20**, отрисованные как чёткое PNG‑изображение.

## Распространённые варианты и обработка граничных случаев

| Сценарий | Корректировка |
|----------|------------|
| **Export to JPEG** | Измените `ImageFormat = ImageFormat.Jpeg` и при желании задайте `Quality = 90` (диапазон 0‑100). |
| **Multiple ranges** | Вызовите `sheet.Pictures.Add` для каждого диапазона и сохраняйте каждое изображение под отдельным именем файла. |
| **Large worksheets** | Увеличьте `HorizontalResolution`/`VerticalResolution` только для необходимого диапазона, чтобы избежать всплесков памяти. |
| **No picture generated** | Убедитесь, что `PrintArea` правильно отформатирован (`"A1:G20"`). Неверный адрес приводит к пустой коллекции `Pictures`. |
| **Saving to a stream** | Используйте `pic.Save(Stream, imgOptions)`, когда требуется изображение в памяти (например, для ответа ASP.NET). |

## Профессиональные советы для надёжного экспорта изображений

* **Validate the print area** – используйте разбор `CellArea` (`CellArea area = CellArea.CreateCellArea("A1", "G20")`) для программного построения диапазонов и избежания опечаток.  
* **Dispose of resources** – оберните `Workbook` в блок `using`, если обрабатываете много файлов, чтобы быстро освобождать нативные ресурсы.  
* **Batch processing** – при экспорте десятков диапазонов переиспользуйте один экземпляр `ImageOrPrintOptions`, чтобы снизить накладные расходы на создание объектов.  
* **Thread safety** – объекты Aspose.Cells **не** являются потокобезопасными. Создавайте отдельный `Workbook` для каждого потока или синхронизируйте доступ.  

## Заключение

Теперь у вас есть полный, готовый к продакшну метод **export excel range as image** с использованием C# и Aspose.Cells. Шаги — загрузка книги, установка области печати, настройка `ImageOrPrintOptions` и сохранение изображения — охватывают как «как», так и «почему», позволяя адаптировать код к сводным таблицам, диаграммам или любому пользовательскому блоку ячеек.

Далее вы можете изучить:

* **Export excel range as image** в других форматах (SVG, BMP) — ещё один вторичный запрос для попытки.  
* **Embedding the PNG in a PDF** с помощью Aspose.PDF для сквозной генерации отчётов.  
* **Automating batch exports** across multiple workbooks with a simple console loop.

Не стесняйтесь экспериментировать с различными разрешениями, ориентациями и каталогами вывода. Приятного кодинга!

## Что изучать дальше?

Следующие руководства охватывают тесно связанные темы, построенные на техниках, продемонстрированных в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [Export Excel Cells to Image Using Aspose.Cells .NET: A Step‑By‑Step Guide](/cells/english/net/import-export/export-excel-cells-to-image-aspose-dotnet/)
- [Export Excel Workbook as Image Using Aspose.Cells for Java](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)
- [How to Export an Excel Worksheet to PNG Using Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-to-png-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}