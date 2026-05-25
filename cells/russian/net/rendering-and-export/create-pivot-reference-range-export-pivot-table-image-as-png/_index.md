---
category: general
date: 2026-02-09
description: Создайте диапазон ссылок сводной таблицы в C# и экспортируйте изображение
  сводной таблицы. Узнайте, как сохранить диапазон Excel в формате PNG с помощью Aspose.Cells
  — быстрый, полный гид.
draft: false
keywords:
- create pivot reference range
- export pivot table image
- save excel range as png
- Aspose.Cells C#
- Excel automation C#
language: ru
og_description: Создайте диапазон ссылок сводной таблицы в C# и экспортируйте изображение
  сводной таблицы в PNG. Полное пошаговое руководство по сохранению диапазона Excel
  в PNG.
og_title: Создать диапазон ссылок сводной таблицы – экспортировать изображение сводной
  таблицы в PNG
tags:
- Aspose.Cells
- C#
- Excel
title: Создать диапазон ссылок сводной таблицы – экспортировать изображение сводной
  таблицы в PNG
url: /ru/net/rendering-and-export/create-pivot-reference-range-export-pivot-table-image-as-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание диапазона ссылки на сводную таблицу – Экспорт изображения сводной таблицы в PNG

Нужно **создать диапазон ссылки на сводную таблицу** в рабочей книге Excel с помощью C#? Вы также можете **экспортировать изображение сводной таблицы** и **сохранить диапазон Excel в png** всего несколькими строками кода. По моему опыту, преобразование живой сводной таблицы в статическое изображение — удобный способ внедрить аналитику в отчёты, электронные письма или панели мониторинга, не перенося всю рабочую книгу.

В этом руководстве мы пройдёмся по всему, что вам нужно знать: необходимые библиотеки, точный код, почему каждый вызов важен, и несколько подводных камней, с которыми вы можете столкнуться. К концу вы сможете уверенно генерировать PNG‑файл любой сводной таблицы и поймёте, как адаптировать шаблон для нескольких листов или пользовательских форматов изображений.

## Требования

Прежде чем начать, убедитесь, что у вас есть:

- **Aspose.Cells for .NET** (бесплатная пробная версия отлично подходит для тестирования).  
- **.NET 6.0** или новее — API, которое мы используем, полностью совместимо с .NET Standard 2.0+, поэтому более старые фреймворки также скомпилируются.  
- Базовый проект C# (Console App, WinForms или ASP.NET — что угодно, что может ссылаться на пакет NuGet).  

Если вы ещё не установили Aspose.Cells, выполните:

```bash
dotnet add package Aspose.Cells
```

И всё — без COM‑interop, без установленного Excel на сервере.

## Шаг 1: Открыть рабочую книгу и получить доступ к первому листу

Первое, что нужно сделать, — загрузить файл рабочей книги и получить лист, содержащий сводную таблицу. Мы намеренно выбираем **первый лист** (`Worksheets[0]`), потому что в большинстве демонстрационных файлов сводная таблица находится именно там, но при желании вы можете заменить индекс именем листа.

```csharp
using Aspose.Cells;
using System;

// Load an existing Excel file (replace with your own path)
Workbook wb = new Workbook("YOUR_DIRECTORY/source.xlsx");

// Access the first worksheet – this is where our pivot lives
Worksheet worksheet = wb.Worksheets[0];
```

*Почему это важно:* `Worksheet` — точка входа для любой операции, основанной на диапазоне. Если указать неправильный лист, последующий вызов `PivotTables[0]` бросит `IndexOutOfRangeException`.

## Шаг 2: Создать диапазон ссылки на сводную таблицу

Теперь мы просим саму сводную таблицу вернуть нам **диапазон ссылки**. Этот диапазон представляет собой точные ячейки, из которых состоит сводка — заголовки, строки данных и итоги. Метод `CreateReferenceRange()` выполняет всю тяжёлую работу внутри, обрабатывая объединённые ячейки и скрытые строки за вас.

```csharp
// Grab the first pivot table on the worksheet
PivotTable pivot = worksheet.PivotTables[0];

// Build a reference range that covers the whole pivot
Range pivotReferenceRange = pivot.CreateReferenceRange();
```

> **Pro tip:** Если в вашей книге несколько сводных таблиц, пройдитесь по `worksheet.PivotTables` и выберите нужную по свойству `Name`.

## Шаг 3: Преобразовать диапазон ссылки в изображение

Aspose.Cells может отрисовать любой `Range` в изображение. Возвращаемый объект поддерживает как растровые (PNG, JPEG), так и векторные (SVG) форматы. Здесь мы запрашиваем изображение по умолчанию — растровый объект, совместимый с `System.Drawing.Image`.

```csharp
// Convert the pivot reference range into an image object
ImageOrVector pivotImage = pivotReferenceRange.ToImage();
```

*Что происходит «под капотом»?* API делает снимок визуального представления диапазона, учитывая стили ячеек, шрифты и условное форматирование. По сути, это то же самое, что сделать скриншот, но программно и без пользовательского интерфейса.

## Шаг 4: Сохранить полученное изображение в файл

Наконец, сохраняем изображение. Метод `Save` автоматически выбирает PNG, если вы указываете расширение «.png». При необходимости можно передать объект `SaveOptions` для управления DPI или выбора другого формата.

```csharp
// Save the image as PNG – the extension drives the format
pivotImage.Save("YOUR_DIRECTORY/pivot.png");
```

После выполнения этой строки откройте `pivot.png` — вы увидите пиксельно‑точный снимок сводной таблицы, готовый к встраиванию куда угодно.

## Полный рабочий пример

Объединив всё вместе, получаем автономную консольную программу, которую можно скопировать и запустить:

```csharp
using Aspose.Cells;
using System;

namespace PivotExportDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load workbook
            Workbook wb = new Workbook("YOUR_DIRECTORY/source.xlsx");

            // 2️⃣ Access first worksheet
            Worksheet worksheet = wb.Worksheets[0];

            // 3️⃣ Get first pivot table
            if (worksheet.PivotTables.Count == 0)
            {
                Console.WriteLine("No pivot tables found on the first sheet.");
                return;
            }
            PivotTable pivot = worksheet.PivotTables[0];

            // 4️⃣ Create a reference range that covers the whole pivot
            Range pivotReferenceRange = pivot.CreateReferenceRange();

            // 5️⃣ Render the range to an image
            ImageOrVector pivotImage = pivotReferenceRange.ToImage();

            // 6️⃣ Save as PNG
            string outputPath = "YOUR_DIRECTORY/pivot.png";
            pivotImage.Save(outputPath);

            Console.WriteLine($"Pivot table image saved to {outputPath}");
        }
    }
}
```

**Ожидаемый результат:** файл `pivot.png` в каталоге `YOUR_DIRECTORY`. Откройте его в любом просмотрщике изображений — вы должны увидеть точную раскладку оригинальной сводной таблицы, включая заголовки столбцов, строки данных и общие итоги.

## Экспорт изображения сводной таблицы – Настройка размера и DPI

Иногда изображение по умолчанию слишком мало для слайда презентации. Разрешение можно контролировать, передав объект `ImageOrVectorSaveOptions`:

```csharp
using Aspose.Cells.Drawing;

// Define PNG options – 300 DPI for high‑quality print
ImageOrVectorSaveOptions options = new ImageOrVectorSaveOptions
{
    ImageFormat = ImageFormat.Png,
    Resolution = 300 // DPI
};

pivotImage.Save("YOUR_DIRECTORY/pivot_highres.png", options);
```

*Зачем менять DPI?* Более высокое DPI даёт более чёткие края, особенно когда PNG масштабируется в PowerPoint или PDF.

## Сохранить диапазон Excel в PNG – Работа с несколькими листами

Если нужно экспортировать сводные таблицы с нескольких листов, пройдитесь по `Workbook.Worksheets` и повторите шаги. Вот лаконичный фрагмент:

```csharp
foreach (Worksheet ws in wb.Worksheets)
{
    foreach (PivotTable pt in ws.PivotTables)
    {
        Range refRange = pt.CreateReferenceRange();
        ImageOrVector img = refRange.ToImage();
        string fileName = $"pivot_{ws.Name}_{pt.Name}.png";
        img.Save($"YOUR_DIRECTORY/{fileName}");
        Console.WriteLine($"Saved {fileName}");
    }
}
```

Этот шаблон **export pivot table image** для каждой сводной таблицы в книге, а каждый файл получает имя листа и сводной таблицы — идеально для пакетной обработки.

## Распространённые проблемы и как их избежать

| Проблема | Почему происходит | Решение |
|----------|-------------------|---------|
| `IndexOutOfRangeException` на `PivotTables[0]` | На листе нет сводных таблиц. | Проверьте `worksheet.PivotTables.Count` перед обращением. |
| Пустое изображение | Сводная таблица отфильтрована так, что скрыты все строки. | Убедитесь, что в сводной таблице есть видимые данные, или вызовите `pivot.RefreshData();` перед созданием диапазона. |
| PNG низкого разрешения | DPI по умолчанию — 96. | Используйте `ImageOrVectorSaveOptions.Resolution`, как показано выше. |
| Ошибки пути к файлу | Недопустимые символы в `YOUR_DIRECTORY`. | Применяйте `Path.Combine` и `Path.GetInvalidPathChars()` для очистки. |

## Проверка – Быстрый тест

После запуска полного примера:

1. Откройте `pivot.png` в Windows Photo Viewer.  
2. Убедитесь, что заголовки столбцов, строки данных и строки итогов совпадают с представлением в Excel.  
3. Если заметили отсутствующие строки, дважды проверьте, что метод **RefreshData** сводной таблицы был вызван до `CreateReferenceRange()`.

## Бонус: Встраивание PNG в документ Word

Поскольку изображение уже в формате PNG, его можно сразу передать в Aspose.Words:

```csharp
using Aspose.Words;
Document doc = new Document();
DocumentBuilder builder = new DocumentBuilder(doc);
builder.InsertImage("YOUR_DIRECTORY/pivot.png");
doc.Save("YOUR_DIRECTORY/report.docx");
```

Теперь у вас есть Word‑отчёт, содержащий точный снимок вашей сводной таблицы — без ручного копирования и вставки.

## Заключение

Вы только что узнали, как **create pivot reference range**, **export pivot table image** и **save Excel range as png** с помощью Aspose.Cells в C#. Ключевые выводы:

- Используйте `PivotTable.CreateReferenceRange()` для изоляции визуальной области сводной таблицы.  
- Преобразуйте этот диапазон в изображение с помощью `Range.ToImage()`.  
- Сохраняйте изображение как PNG, при необходимости регулируя DPI для печати.  

Отсюда вы можете исследовать пакетный экспорт, другие форматы изображений (SVG, JPEG) или даже встраивание PNG в PDF или Word‑документы. Возможности безграничны, как только у вас есть статическая графика сводной таблицы.

Есть вопросы или сложный сценарий? Оставьте комментарий ниже, и удачной разработки!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}