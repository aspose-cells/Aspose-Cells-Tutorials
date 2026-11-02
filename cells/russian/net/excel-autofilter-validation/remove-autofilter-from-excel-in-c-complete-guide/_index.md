---
category: general
date: 2026-08-07
description: Быстро удалите автофильтр из Excel в C#. Узнайте, как отключить фильтр
  Excel, удалить фильтр таблицы Excel и очистить автофильтр таблицы Excel с помощью
  Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- remove autofilter from excel
- how to turn off excel filter
- delete excel table filter
- clear excel table autofilter
language: ru
lastmod: 2026-08-07
og_description: Удалите автофильтр в Excel с помощью C# и узнайте, как отключить фильтр
  Excel, удалить фильтр таблицы Excel и очистить автофильтр таблицы Excel, используя
  Aspose.Cells.
og_image_alt: Screenshot showing an Excel sheet after remove autofilter from excel
og_title: Удаление автофильтра из Excel в C# – пошаговое руководство
schemas:
- author: Aspose
  dateModified: '2026-08-07'
  description: Remove autofilter from Excel in C# quickly. Learn how to turn off Excel
    filter, delete Excel table filter, and clear Excel table autofilter with Aspose.Cells.
  headline: Remove autofilter from Excel in C# – complete guide
  type: TechArticle
- description: Remove autofilter from Excel in C# quickly. Learn how to turn off Excel
    filter, delete Excel table filter, and clear Excel table autofilter with Aspose.Cells.
  name: Remove autofilter from Excel in C# – complete guide
  steps:
  - name: Expected output
    text: 'Open `output.xlsx` in Excel:'
  - name: Multiple tables in the same worksheet
    text: 'If the worksheet contains more than one table, iterate over the collection:'
  - name: Removing filter from a specific column only
    text: 'Aspose.Cells does not expose a column‑level `AutoFilter` removal, but you
      can recreate the table without the filter:'
  - name: Working with older Excel formats (*.xls)
    text: Aspose.Cells supports the legacy binary format automatically. The same code
      works; just ensure the file extension matches the input file.
  - name: Handling large workbooks
    text: For files larger than 100 MB, enable the **LoadOptions** to use the **MemoryOptimized**
      mode, which reduces memory pressure while still allowing table manipulation.
  type: HowTo
tags:
- Excel
- C#
- Aspose.Cells
title: Удаление автофильтра из Excel в C# — полное руководство
url: /ru/net/excel-autofilter-validation/remove-autofilter-from-excel-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Удаление автофильтра из Excel в C# – полное руководство

Если вам нужно **удалить автофильтр из Excel** при программной обработке файлов, это руководство покажет, как это сделать. Вы узнаете самый быстрый способ отключить фильтр Excel, удалить фильтр таблицы Excel и очистить автофильтр таблицы Excel с помощью библиотеки Aspose.Cells.

В учебнике рассматривается всё: от настройки проекта до проверки того, что в результирующей книге больше не отображаются стрелки фильтра. Никаких ручных действий не требуется, и код работает с любым файлом .xlsx, содержащим таблицу с автофильтром.

## Предварительные требования

Прежде чем начать, убедитесь, что у вас есть:

- .NET 6.0 или более поздняя версия  
- Visual Studio 2022 (или любой IDE для C#)  
- Лицензия **Aspose.Cells for .NET** (бесплатная оценочная версия подходит для тестирования)  
- Файл Excel (`input.xlsx`), содержащий хотя бы одну таблицу с применённым автофильтром  

Также необходимо добавить пакет Aspose.Cells из NuGet в ваш проект:

```bash
dotnet add package Aspose.Cells
```

> **Совет:** Держите книгу в папке, к которой ваше приложение имеет права чтения/записи без повышения привилегий, чтобы избежать `UnauthorizedAccessException`.

![удалить автофильтр из excel](/assets/remove-autofilter.png "удалить автофильтр из excel – лист Excel без стрелок фильтра")

## Удаление автофильтра из Excel – шаг 1: загрузка книги

Первой операцией является открытие исходной книги. Загрузка файла в память даёт полный доступ к листам, таблицам и их свойствам.

```csharp
using Aspose.Cells;

// Step 1: Load the workbook containing a table with an AutoFilter
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

*Почему это важно:* `Workbook` — центральный объект в Aspose.Cells. Он разбирает пакет XLSX и строит объектную модель, отражающую внутреннюю структуру Excel, позволяя напрямую манипулировать таблицами.

## Как отключить фильтр Excel – шаг 2: доступ к целевому листу

Файлы Excel могут содержать множество листов, но в примере используется первый. При необходимости измените индекс, если ваши данные находятся на другом листе.

```csharp
// Step 2: Access the first worksheet (index 0)
Worksheet worksheet = workbook.Worksheets[0];
```

*Почему это важно:* Каждый `Worksheet` содержит собственную коллекцию таблиц. Получив правильный лист, вы гарантируете изменение нужной таблицы.

## Удаление фильтра таблицы Excel – шаг 3: поиск первой таблицы

Таблицы хранятся в коллекции `Tables` листа. Можно перебрать их, но для простоты возьмём первую таблицу.

```csharp
// Step 3: Retrieve the first table on the worksheet
Table table = worksheet.Tables[0];
```

*Почему это важно:* Объект `Table` содержит свойство `AutoFilter`, которое управляет отображением UI фильтра. Доступ к таблице необходим для последующего удаления фильтра.

## Очистка автофильтра таблицы Excel – шаг 4: удаление AutoFilter

Установка свойства `AutoFilter` в `null` полностью удаляет UI фильтра. Исходные данные остаются без изменений.

```csharp
// Step 4: Remove the AutoFilter by setting it to null
table.AutoFilter = null;
```

*Почему это важно:* Когда `AutoFilter` равен `null`, Excel больше не показывает выпадающие стрелки, а любые ранее применённые критерии фильтра очищаются. Это ключевая операция для **удаления фильтра таблицы Excel**.

## Сохранение книги – шаг 5: проверка результата

Наконец, запишите изменённую книгу на диск. Сохранённый файл откроется в Excel без стрелок фильтра.

```csharp
// Step 5: Save the workbook; the table is now a plain data table without filter UI
workbook.Save("YOUR_DIRECTORY/output.xlsx");
```

### Ожидаемый результат

Откройте `output.xlsx` в Excel:

- Таблица отображается как обычные данные — в строке заголовка нет стрелок фильтра.  
- Все строки видимы, что подтверждает очистку фильтра.  

Если стрелки всё ещё видны, проверьте, действительно ли исходный файл содержал автофильтр и что вы обратились к правильному индексу таблицы.

## Общие варианты и граничные случаи

### Несколько таблиц на одном листе

Если на листе более одной таблицы, переберите коллекцию:

```csharp
foreach (Table tbl in worksheet.Tables)
{
    tbl.AutoFilter = null; // clear filter for each table
}
```

### Удаление фильтра только из конкретного столбца

Aspose.Cells не предоставляет удаление `AutoFilter` на уровне столбца, но вы можете воссоздать таблицу без фильтра:

```csharp
// Capture existing data range
CellArea range = table.DisplayRange;

// Remove the table (including filter)
worksheet.Tables.RemoveAt(table.Index);

// Re‑add the table without AutoFilter
Table newTable = worksheet.Tables[worksheet.Tables.Add(range.StartRow, range.StartColumn, range.EndRow, range.EndColumn, true)];
```

### Работа со старыми форматами Excel (*.xls)

Aspose.Cells автоматически поддерживает устаревший бинарный формат. Тот же код работает; просто убедитесь, что расширение файла соответствует входному файлу.

### Обработка больших книг

Для файлов более 100 МБ включите **LoadOptions** с режимом **MemoryOptimized**, который снижает нагрузку на память, но по‑прежнему позволяет работать с таблицами.

```csharp
LoadOptions options = new LoadOptions(LoadFormat.Xlsx) { MemoryOptimization = true };
Workbook largeWorkbook = new Workbook("large_input.xlsx", options);
```

## Полный, готовый к запуску пример

Ниже представлена полная программа, которую можно скопировать, вставить и запустить как консольное приложение.

```csharp
using System;
using Aspose.Cells;

namespace RemoveExcelAutoFilter
{
    class Program
    {
        static void Main()
        {
            // Define file paths
            string inputPath = @"YOUR_DIRECTORY\input.xlsx";
            string outputPath = @"YOUR_DIRECTORY\output.xlsx";

            // Load the workbook
            Workbook workbook = new Workbook(inputPath);

            // Access the first worksheet
            Worksheet worksheet = workbook.Worksheets[0];

            // Ensure the worksheet contains at least one table
            if (worksheet.Tables.Count == 0)
            {
                Console.WriteLine("No tables found on the first worksheet.");
                return;
            }

            // Retrieve the first table and clear its AutoFilter
            Table table = worksheet.Tables[0];
            table.AutoFilter = null;

            // Save the modified workbook
            workbook.Save(outputPath);

            Console.WriteLine($"AutoFilter removed. Saved to {outputPath}");
        }
    }
}
```

Запустите программу, затем откройте `output.xlsx`. Вы увидите, что операция **удаления автофильтра из Excel** выполнена успешно, и лист показывает обычную таблицу данных.

## Заключение

Теперь вы знаете, как **удалить автофильтр из Excel** с помощью C#. Загрузив книгу, получив целевую таблицу и установив `AutoFilter` в `null`, вы можете **отключить фильтр Excel**, **удалить фильтр таблицы Excel** и **очистить автофильтр таблицы Excel** одним надёжным шагом.  

Далее изучайте связанные темы, такие как **форматирование таблиц Excel с Aspose.Cells**, **экспорт отфильтрованных данных в CSV** или **программное применение условного форматирования**. Все они опираются на ту же объектную модель, которую вы только что освоили.

Не бойтесь экспериментировать с несколькими таблицами, большими книгами или различными форматами файлов — ваш новый навык сделает автоматизацию Excel более плавной и предсказуемой. Приятного кодинга!

## Что вам стоит изучить дальше?

Следующие учебники охватывают тесно связанные темы, построенные на техниках, продемонстрированных в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, помогающими освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [Очистка UI фильтра в Excel с C# – Удалить кнопку AutoFilter](/cells/english/net/excel-autofilter-validation/clear-filter-ui-in-excel-with-c-remove-autofilter-button/)
- [Как реализовать AutoFilter в Excel с помощью Aspose.Cells for .NET (Руководство по анализу данных)](/cells/english/net/data-analysis/implement-autofilter-excel-aspose-cells-dotnet/)
- [Как реализовать AutoFilter Excel «EndsWith» с помощью Aspose.Cells for .NET](/cells/english/net/data-analysis/implement-autofilter-endswith-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}