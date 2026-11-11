---
category: general
date: 2026-10-26
description: отключить автофильтр в Excel с помощью C#. Этот учебник показывает, как
  программно удалить автофильтр из таблицы Excel и содержит полностью рабочий пример.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- disable autofilter in excel
- remove autofilter from excel table
- Excel automation C#
- Aspose.Cells filter handling
- programmatic Excel editing
language: ru
lastmod: 2026-10-26
og_description: быстро отключить автофильтр в Excel. Следуйте этому руководству, чтобы
  удалить автофильтр из таблицы Excel с помощью C# и Aspose.Cells.
og_image_alt: Screenshot of an Excel worksheet where the autofilter has been disabled
og_title: Отключить автофильтр в Excel с помощью C# — пошаговое руководство
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: disable autofilter in Excel using C#. This tutorial shows how to remove
    autofilter from Excel table programmatically and includes a full working example.
  headline: How to disable autofilter in Excel with C# – complete guide
  type: TechArticle
- description: disable autofilter in Excel using C#. This tutorial shows how to remove
    autofilter from Excel table programmatically and includes a full working example.
  name: How to disable autofilter in Excel with C# – complete guide
  steps:
  - name: Open the saved file (`Sample_NoFilter.xlsx`) in Microsoft Excel.
    text: Open the saved file (`Sample_NoFilter.xlsx`) in Microsoft Excel.
  - name: Click any column header – you should **not** see the drop‑down filter arrow.
    text: Click any column header – you should **not** see the drop‑down filter arrow.
  - name: 'If you still see arrows, double‑check that the table you targeted is indeed
      the one with the filter. You can list all tables with:'
    text: 'If you still see arrows, double‑check that the table you targeted is indeed
      the one with the filter. You can list all tables with:'
  type: HowTo
tags:
- Excel
- C#
- Aspose.Cells
title: Как отключить автофильтр в Excel с помощью C# — полное руководство
url: /ru/net/excel-autofilter-validation/how-to-disable-autofilter-in-excel-with-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как отключить автофильтр в Excel с помощью C# – полное руководство

Если вам нужно **отключить автофильтр в Excel**, это руководство покажет, как сделать это из C#. Независимо от того, очищаете ли вы отчет перед публикацией или автоматизируете конвейер экспорта данных, удаление фильтра гарантирует, что лист отображает все строки. Вы также узнаете, как **удалить автофильтр из таблицы Excel** одним надёжным вызовом.

Мы будем использовать популярную библиотеку **Aspose.Cells for .NET**, потому что она работает без необходимости установки Excel на сервере. К концу этого руководства у вас будет автономное консольное приложение, которое загружает книгу, находит первую таблицу и отключает её автофильтр. Решение работает с файлами .xlsx, созданными в Excel 2007 или новее.

## Что понадобится

| Prerequisite | Why it matters |
|--------------|----------------|
| .NET 6.0 или новее | Обеспечивает среду выполнения для кода C#. |
| Aspose.Cells for .NET (NuGet package `Aspose.Cells`) | Обеспечивает программный доступ к листам, таблицам и автофильтрам. |
| Пример файла Excel (`Sample.xlsx`), содержащий как минимум одну таблицу с применённым автофильтром | Код работает с первой таблицей; наличие таблицы позволяет продемонстрировать отключение фильтра. |
| Visual Studio 2022 (или любой IDE для C#) | Обеспечивает простую сборку и отладку консольного приложения. |

> **Pro tip:** Если вы предпочитаете бесплатную альтернативу, вы можете адаптировать код для использования **ClosedXML** или **EPPlus**; основная идея — установить свойство `AutoFilter` таблицы в `null` — остаётся той же.

## Шаг 1: Создать новый консольный проект

Откройте терминал или командную строку Visual Studio и выполните:

```bash
dotnet new console -n ExcelFilterDemo
cd ExcelFilterDemo
dotnet add package Aspose.Cells
```

Это создаёт новый проект с именем `ExcelFilterDemo` и подключает библиотеку Aspose.Cells.

## Шаг 2: Загрузить книгу и найти первый лист

Первой логической операцией является открытие файла книги. Aspose.Cells читает файл в объект `Workbook`, который предоставляет прямой доступ к листам и таблицам.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Path to the Excel file you want to modify
        const string inputPath = "Sample.xlsx";

        // Load the workbook into memory
        Workbook wb = new Workbook(inputPath);

        // Access the first worksheet (index 0)
        Worksheet worksheet = wb.Worksheets[0];
```

> **Почему этот шаг?** Загрузка книги необходима перед тем, как вы сможете манипулировать объектами Excel. Использование первого листа (`Worksheets[0]`) отражает типичный сценарий, когда основные данные находятся на первом листе.

## Шаг 3: Получить первую таблицу, определённую на листе

Таблицы Excel (также называемые ListObjects) являются контейнерами, содержащими структурированные данные. Каждая таблица может иметь собственный автофильтр. Чтобы удалить фильтр, нам сначала нужна ссылка на объект таблицы.

```csharp
        // Get the first table on the worksheet.
        // If the worksheet has no tables, this will throw an IndexOutOfRangeException.
        Table table = worksheet.Tables[0];
```

> **Пограничный случай:** Если книга может содержать листы без таблиц, оберните доступ в проверку `if (worksheet.Tables.Count > 0)`. Это предотвращает ошибки выполнения и делает решение надёжным.

## Шаг 4: Отключить автофильтр для таблицы

Само отключение происходит в одну строку: присвойте `null` свойству `AutoFilter` объекта `Table`. Это очищает любые критерии фильтра и удаляет выпадающие стрелки из строки заголовка.

```csharp
        // Disable the autofilter – this clears any applied filter.
        table.AutoFilter = null;
```

После выполнения этой строки таблица ведёт себя как обычный диапазон без пользовательского интерфейса фильтра.

## Шаг 5: Сохранить изменённую книгу

Наконец, запишите изменения обратно на диск. Вы можете перезаписать оригинальный файл или создать новый, чтобы сохранить исходный нетронутым.

```csharp
        // Save the workbook. Use a new file name to avoid overwriting the original.
        const string outputPath = "Sample_NoFilter.xlsx";
        wb.Save(outputPath);

        System.Console.WriteLine($"Autofilter disabled. Saved to {outputPath}");
    }
}
```

### Полный исходный код

Объединив все части, получаем полную программу, выглядящую так:

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Path to the original Excel file
        const string inputPath = "Sample.xlsx";

        // Load the workbook
        Workbook wb = new Workbook(inputPath);

        // Access the first worksheet
        Worksheet worksheet = wb.Worksheets[0];

        // Ensure the worksheet contains at least one table
        if (worksheet.Tables.Count == 0)
        {
            System.Console.WriteLine("No tables found on the first worksheet.");
            return;
        }

        // Get the first table
        Table table = worksheet.Tables[0];

        // Disable the autofilter – clears any applied filter
        table.AutoFilter = null;

        // Save the modified workbook
        const string outputPath = "Sample_NoFilter.xlsx";
        wb.Save(outputPath);

        System.Console.WriteLine($"Autofilter disabled. Saved to {outputPath}");
    }
}
```

Запустите программу командой `dotnet run`. После выполнения откройте `Sample_NoFilter.xlsx` в Excel; вы увидите, что стрелки фильтра исчезли и все строки видимы.

## Проверьте, что автофильтр действительно исчез

1. Откройте сохранённый файл (`Sample_NoFilter.xlsx`) в Microsoft Excel.  
2. Щёлкните любой заголовок столбца — вы **не должны** видеть выпадающую стрелку фильтра.  
3. Если стрелки всё ещё видны, проверьте, что выбранная вами таблица действительно та, в которой установлен фильтр. Вы можете вывести список всех таблиц с помощью:

```csharp
foreach (var tbl in worksheet.Tables)
{
    System.Console.WriteLine($"Table name: {tbl.Name}, Has AutoFilter: {tbl.AutoFilter != null}");
}
```

Вывод консоли должен показывать `Has AutoFilter: False` для таблицы, которую вы изменили.

## Распространённые подводные камни и как их избежать

| Symptom | Likely cause | Fix |
|---------|--------------|-----|
| `IndexOutOfRangeException` at `worksheet.Tables[0]` | На листе нет таблиц. | Добавьте проверку `if (worksheet.Tables.Count == 0)` перед доступом. |
| Saved file still shows filters | Вы отредактировали неправильный лист или таблицу. | Используйте `wb.Worksheets["SheetName"]` или пройдитесь по `wb.Worksheets`, чтобы найти нужную таблицу. |
| The program crashes on older .NET versions | Aspose.Cells требует .NET 6.0+ для последней версии пакета. | Обновите целевую платформу в файле `.csproj`. |
| NullReferenceException when `table.AutoFilter` is already null | Вы вызвали код дважды для одного и того же файла без повторной загрузки. | Перезагрузите книгу или проверьте `if (table.AutoFilter != null)` перед присваиванием. |

## Расширение решения

Теперь, когда вы знаете, как **отключить автофильтр в Excel**, вы можете захотеть:

* **Remove autofilter from Excel table** только когда выполнено определённое условие (например, установлен флаг пользователя). Добавьте оператор `if` вокруг `table.AutoFilter = null;`.
* **Применить новый фильтр** программно после очистки старого, используя `table.AutoFilter.Range` и `table.AutoFilter.AddFilterColumn(...)`.
* **Обрабатывать несколько таблиц** в одной книге, проходя в цикле `worksheet.Tables` и отключая каждый фильтр.

Эти расширения следуют той же схеме, продемонстрированной выше, и сохраняют кодовую базу чистой.

## Заключение

Теперь у вас есть краткий, готовый к продакшену метод **отключить автофильтр в Excel** с помощью C#. Загрузив книгу, получив первую таблицу и установив `table.AutoFilter = null`, вы эффективно **удаляете автофильтр из таблицы Excel** без ручного вмешательства. Полный пример компилируется, запускается и создаёт чистый файл, готовый к дальнейшей автоматизации или распространению.

Не стесняйтесь экспериментировать с дополнительными таблицами, условной логикой или альтернативными библиотеками. Если вы столкнётесь с какими‑либо пограничными случаями, обратитесь к разделу устранения неполадок или изучите обширную документацию Aspose.Cells для продвинутой работы с фильтрами. Счастливого кодинга!

## Что изучать дальше?

Следующие руководства охватывают тесно связанные темы, которые развивают техники, продемонстрированные в этом руководстве. Каждый ресурс включает полностью рабочие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [How to remove autofilter from Excel tables using C#](/cells/english/net/excel-autofilter-validation/how-to-remove-autofilter-from-excel-tables-using-c/)
- [Clear filter UI in Excel with C# – Remove AutoFilter Button](/cells/english/net/excel-autofilter-validation/clear-filter-ui-in-excel-with-c-remove-autofilter-button/)
- [How to Use AutoFilter in C# Excel Automation – Full Step‑by‑Step Guide](/cells/english/net/excel-autofilter-validation/how-to-use-autofilter-in-c-excel-automation-full-step-by-ste/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}