---
category: general
date: 2026-08-11
description: Как экспортировать Excel в PNG и сохранить диапазон Excel как изображение
  с помощью Aspose.Cells. Узнайте, как сохранить изображение листа Excel и экспортировать
  изображение сводной таблицы за несколько минут.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to export excel to png
- save excel range as image
- save excel sheet picture
- export pivot table image
language: ru
lastmod: 2026-08-11
og_description: Как быстро экспортировать Excel в PNG. Этот учебник показывает, как
  сохранить диапазон Excel как изображение, сохранить картинку листа Excel и экспортировать
  изображение сводной таблицы с помощью Aspose.Cells.
og_image_alt: Screenshot of C# code exporting an Excel worksheet to a PNG file
og_title: Как экспортировать Excel в PNG – полное руководство по программированию
schemas:
- author: Aspose
  dateModified: '2026-08-11'
  description: How to export Excel to PNG and save Excel range as image using Aspose.Cells.
    Learn to save Excel sheet picture and export pivot table image in minutes.
  headline: How to export Excel to PNG – full step‑by‑step guide
  type: TechArticle
tags:
- Aspose.Cells
- Excel automation
- C#
- image export
title: Как экспортировать Excel в PNG – полное пошаговое руководство
url: /ru/net/image-and-chart-operations/how-to-export-excel-to-png-full-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как экспортировать Excel в PNG – полное пошаговое руководство

Если вам нужно **как экспортировать Excel в PNG**, это руководство проведёт вас через весь процесс с использованием Aspose.Cells for .NET. Независимо от того, хотите ли вы **сохранить диапазон Excel как изображение**, вставить картинку листа в отчёт или **экспортировать изображение сводной таблицы** для панели мониторинга, ниже приведённые шаги дадут готовое решение.

Вы узнаете, как загрузить книгу, обновить сводную таблицу, настроить параметры изображения и, наконец, записать PNG‑файл, сохраняющий стилизованный вид исходных данных. Внешние инструменты или ручные скриншоты не требуются.

## Требования

Прежде чем начать, убедитесь, что у вас есть:

* .NET 6.0 SDK или более поздняя версия  
* Visual Studio 2022 (или любой IDE для C#)  
* Лицензия Aspose.Cells for .NET или бесплатная оценочная копия – скачайте с [веб‑сайта Aspose.Cells](https://products.aspose.com/cells/net)  
* Пример Excel‑файла (`PivotTable.xlsx`), содержащего хотя бы одну сводную таблицу  

Код работает на Windows, macOS и Linux, так как Aspose.Cells платформенно‑независим.

## Шаг 1: Установить Aspose.Cells через NuGet

Откройте папку проекта в терминале и выполните:

```bash
dotnet add package Aspose.Cells
```

Это добавит последнюю стабильную версию **Aspose.Cells** в ваш `.csproj`. Библиотека предоставляет классы `Workbook`, `Worksheet`, `ImageOrPrintOptions` и другие, которые мы будем использовать для **сохранения изображения листа Excel**.

## Шаг 2: Загрузить книгу, содержащую сводную таблицу

```csharp
using Aspose.Cells;
using System;

// Load the Excel file – replace the path with your actual location
string sourcePath = @"YOUR_DIRECTORY\PivotTable.xlsx";
Workbook workbook = new Workbook(sourcePath);
```

*Почему это важно:*  
Загрузка книги даёт доступ ко всем листам, ячейкам и встроенным объектам. Класс `Workbook` абстрагирует формат файла, поэтому вы можете работать с `.xlsx`, `.xls` или даже `.csv` без дополнительного кода парсинга.

## Шаг 3: Выбрать лист и обновить сводную таблицу

```csharp
// Get the first worksheet where the pivot table resides
Worksheet sheet = workbook.Worksheets[0];

// Refresh the pivot table so it reflects the latest source data
if (sheet.PivotTables.Count > 0)
{
    sheet.PivotTables[0].Refresh();
}
else
{
    Console.WriteLine("No pivot tables found on the selected worksheet.");
}
```

*Почему это важно:*  
Сводные таблицы кэшируют исходные данные. Вызов `Refresh()` гарантирует, что визуальное представление соответствует последним изменениям, что критично при последующем **экспорте изображения сводной таблицы**.

## Шаг 4: Настроить параметры экспорта изображения (формат PNG, сохранение стилей)

```csharp
// Set up export options – PNG keeps lossless quality and supports transparency
ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
{
    SaveFormat = SaveFormat.Png,
    // Preserve the pivot table’s style (fonts, colors, borders)
    CalculatePivotTableStyle = true,
    // Optional: set image resolution (DPI) for higher quality
    HorizontalResolution = 300,
    VerticalResolution = 300
};
```

*Почему это важно:*  
`CalculatePivotTableStyle = true` заставляет Aspose.Cells отрисовать сводную таблицу точно так же, как она выглядит в Excel, включая условное форматирование. Регулировка DPI может быть полезна для печати или экранов с высоким разрешением.

## Шаг 5: Захватить используемый диапазон (включая сводную таблицу) как изображение

```csharp
// Determine the range that contains data – MaxDisplayRange covers the whole used area
CellArea usedRange = sheet.Cells.MaxDisplayRange;

// Add a picture of the used range to the worksheet (position 0,0) and save it
Picture pic = sheet.Pictures.Add(0, 0, usedRange);
pic.Save(@"YOUR_DIRECTORY\PivotImage.png", imgOptions);
```

*Почему это важно:*  
`MaxDisplayRange` автоматически расширяется до самой дальней ячейки, содержащей данные, формулы или форматирование, гарантируя, что вся сводная таблица и окружающие ячейки включены. Метод `Pictures.Add` создаёт изображение в памяти, которое мы сразу сохраняем на диск в виде PNG‑файла.

## Полный рабочий пример

Объединив всё вместе, получаем автономную консольную программу, которую можно скопировать, вставить и запустить:

```csharp
using Aspose.Cells;
using System;

namespace ExcelToPngExport
{
    class Program
    {
        static void Main()
        {
            // ---------- 1. Load workbook ----------
            string sourcePath = @"YOUR_DIRECTORY\PivotTable.xlsx";
            Workbook workbook = new Workbook(sourcePath);

            // ---------- 2. Get first worksheet ----------
            Worksheet sheet = workbook.Worksheets[0];

            // ---------- 3. Refresh pivot table ----------
            if (sheet.PivotTables.Count > 0)
            {
                sheet.PivotTables[0].Refresh();
            }
            else
            {
                Console.WriteLine("No pivot tables found on the selected worksheet.");
                return;
            }

            // ---------- 4. Set image export options ----------
            ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
            {
                SaveFormat = SaveFormat.Png,
                CalculatePivotTableStyle = true,
                HorizontalResolution = 300,
                VerticalResolution = 300
            };

            // ---------- 5. Export used range as PNG ----------
            CellArea usedRange = sheet.Cells.MaxDisplayRange;
            Picture pic = sheet.Pictures.Add(0, 0, usedRange);
            string outputPath = @"YOUR_DIRECTORY\PivotImage.png";
            pic.Save(outputPath, imgOptions);

            Console.WriteLine($"Pivot table image saved to: {outputPath}");
        }
    }
}
```

### Ожидаемый вывод

При запуске программы в консоли будет выведено:

```
Pivot table image saved to: YOUR_DIRECTORY\PivotImage.png
```

И файл `PivotImage.png` появится в целевой папке. Откройте его в любом просмотрщике изображений – вы увидите точную визуализацию листа Excel, включая стилизованную сводную таблицу, заголовки столбцов и любые соседние данные.

## Распространённые варианты и граничные случаи

| Сценарий | Корректировка |
|----------|---------------|
| **Экспортировать только определённый диапазон ячеек** (например, `A1:D20`) | Замените `sheet.Cells.MaxDisplayRange` на `new CellArea { StartRow = 0, StartColumn = 0, EndRow = 19, EndColumn = 3 }`. |
| **Несколько листов** | Пройдитесь в цикле по `workbook.Worksheets` и повторите шаги 3‑5 для каждого листа, который нужно экспортировать. |
| **Другой формат изображения** (JPEG, BMP) | Измените `SaveFormat = SaveFormat.Jpeg` (или `Bmp`). PNG рекомендуется для безпотерьного качества. |
| **Большие листы**, вызывающие нагрузку на память | Используйте `sheet.Pictures.Add` с меньшим `CellArea` или разбейте экспорт на несколько изображений. |
| **Отсутствует сводная таблица** | Защитите код условием `if (sheet.PivotTables.Count == 0)`, как показано; вы всё равно можете экспортировать обычный диапазон. |

## Профессиональные советы

* **Лицензировать заранее** – зарегистрируйте лицензию Aspose.Cells до загрузки книги, чтобы избавиться от водяного знака оценки.  
  ```csharp
  var license = new License();
  license.SetLicense(@"YOUR_DIRECTORY\Aspose.Total.NET.lic");
  ```
* **Пакетный экспорт** – для конвейеров отчётности оберните логику экспорта в метод, возвращающий `byte[]`. Это позволит отправлять PNG напрямую в веб‑API без работы с файловой системой.  
* **Прозрачный фон** – PNG уже поддерживает прозрачность. Если нужен белый фон, установите `imgOptions.Transparent = false;`.  

## Заключение

Теперь вы знаете **как экспортировать Excel в PNG** с помощью Aspose.Cells, охватывая полный цикл от загрузки книги до **сохранения диапазона Excel как изображения**, **сохранения картинки листа Excel** и **экспорта изображения сводной таблицы**. Предоставленный код полностью готов к запуску и легко адаптируется к реальным сценариям, таким как автоматизированная отчётность или генерация дашбордов.

Готовы к следующему шагу? Изучите, как **преобразовать PNG в PDF** для печатных отчётов, или интегрируйте изображение в веб‑службу, доставляющую живые визуализации Excel. Приятного кодинга!

## Что изучать дальше?

Следующие руководства охватывают тесно связанные темы, расширяющие техники, продемонстрированные в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, помогающими освоить дополнительные возможности API и исследовать альтернативные подходы в ваших проектах.

- [How to Export an Excel Worksheet to PNG Using Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-to-png-aspose-cells-java/)
- [Export Excel Workbook as Image Using Aspose.Cells for Java: A Step-by-Step Guide](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)
- [How to Export Excel Cells as Images Using Aspose.Cells for Java](/cells/english/java/import-export/export-excel-cells-as-image-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}