---
category: general
date: 2026-03-21
description: Экспортировать таблицу данных Excel в DataTable с заголовками, ограничить
  количество знаков после запятой и экспортировать первые 100 строк с помощью Aspose.Cells.
draft: false
keywords:
- export excel data table
- export excel to datatable
- limit decimal places excel
- export first 100 rows
- export excel with headers
language: ru
og_description: Узнайте, как экспортировать таблицу данных Excel в DataTable, сохранить
  заголовки, ограничить количество знаков после запятой и получить первые 100 строк
  в C#.
og_title: Экспорт таблицы данных Excel в C# – пошаговое руководство
tags:
- C#
- Aspose.Cells
- Excel
- DataTable
title: Экспорт таблицы данных Excel в C# – Полное руководство
url: /ru/net/excel-data-export-retrieval/export-excel-data-table-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Экспорт таблицы данных Excel – Полный пошаговый пример на C#

Нужно **export excel data table** из книги в .NET `DataTable`? Вы попали по адресу — в этом руководстве показано, как именно это сделать, сохранить заголовки столбцов, ограничить количество знаков после запятой и извлечь только первые 100 строк.  

Если вы когда‑нибудь смотрели на таблицу и думали: «Как мне получить эти данные в приложение, не потеряв форматирование?», вы не одиноки. В течение нескольких минут мы превратим эту «что‑если» ситуацию в готовое решение копировать‑вставлять, работающее с Aspose.Cells, популярной библиотекой для работы с Excel.

## Что вы узнаете

- Как **export excel to datatable** с помощью метода `ExportDataTable`.  
- Как сохранить оригинальные имена столбцов (`export excel with headers`).  
- Как **limit decimal places excel** значения, настроив `ExportTableOptions`.  
- Как безопасно получить только первые 100 строк (`export first 100 rows`).  

Никаких внешних скриптов, никаких магических строк — просто чистый C#, который можно вставить в любой .NET‑проект.

## Требования

| Требование | Почему это важно |
|-------------|----------------|
| .NET 6 или новее (или .NET Framework 4.7+) | Aspose.Cells поддерживает оба варианта, но более новые среды предоставляют асинхронные API. |
| NuGet‑пакет Aspose.Cells for .NET | Содержит `Workbook`, `ExportTableOptions` и вспомогательный `ExportDataTable`. |
| Пример файла Excel (например, `Numbers.xlsx`) | Источник данных, которые вы будете экспортировать. |
| Базовые знания C# | Вы будете следовать примерам кода, но ничего сложного не требуется. |

Если что‑то из этого вам незнакомо, установите NuGet‑пакет командой `dotnet add package Aspose.Cells` и создайте небольшой файл Excel с несколькими числами — ваш тестовый набор данных.

![пример экспорта таблицы данных Excel](excel-data-table.png "Скриншот листа Excel, который будет экспортирован в DataTable")

## Шаг 1: Загрузка книги (export excel data table)

Первое, что вам нужно, — это экземпляр `Workbook`, указывающий на ваш файл Excel. Представьте это как открытие книги перед тем, как читать главы.

```csharp
using Aspose.Cells;

// 1️⃣ Load the workbook that contains the source data
Workbook workbook = new Workbook(@"C:\Path\To\Numbers.xlsx");
```

> **Почему это важно:** Загрузка книги дает доступ к её листам, ячейкам и стилям. Если путь к файлу неверный, Aspose бросит `FileNotFoundException`, поэтому проверьте расположение.

## Шаг 2: Настройка параметров экспорта – limit decimal places excel

По умолчанию Aspose экспортирует каждое числовое значение с полной точностью. Часто достаточно лишь нескольких значимых цифр, особенно когда данные передаются в UI‑грид или API, ожидающий округлённые числа.

```csharp
using Aspose.Cells;

// 2️⃣ Configure export options – keep only 4 significant digits
ExportTableOptions exportOptions = new ExportTableOptions
{
    // This property trims the number of significant digits.
    SignificantDigits = 4
};
```

> **Полезный совет:** Если вам нужна другая стратегия округления (например, всегда округлять вверх), вы можете пост‑обработать `DataTable` после экспорта. Параметр `SignificantDigits` — самый быстрый способ **limit decimal places excel** без написания дополнительных циклов.

## Шаг 3: Экспорт нужного диапазона (export first 100 rows)

Теперь мы указываем Aspose, какой блок ячеек нужно выгрузить в `DataTable`. В этом руководстве мы берём первые 100 строк и первые 10 столбцов, но вы можете изменить эти числа под свои нужды.

```csharp
using System.Data;
using Aspose.Cells;

// 3️⃣ Export a block of cells (first 100 rows × 10 columns) to a DataTable
DataTable dataTable = workbook.Worksheets[0].Cells.ExportDataTable(
    startRow: 0,          // zero‑based index, first row
    startColumn: 0,       // first column (A)
    totalRows: 100,       // export only the first 100 rows
    totalColumns: 10,     // and the first 10 columns
    exportColumnNames: true, // keep column headers (export excel with headers)
    options: exportOptions);
```

> **Особый случай:** Если на листе меньше 100 строк, Aspose просто экспортирует существующие данные без ошибки. Тем не менее, возможно, захотите добавить проверку на неожиданно маленький диапазон:

```csharp
int rowsToExport = Math.Min(100, workbook.Worksheets[0].Cells.MaxDataRow + 1);
```

## Шаг 4: Проверка результата – быстрый вывод в консоль

Просмотр данных в отладчике приятен, но вывод нескольких строк в консоль подтверждает, что **export excel to datatable** действительно сработал и знаки после запятой обрезаны.

```csharp
static void PrintDataTable(DataTable table)
{
    foreach (DataRow row in table.Rows)
    {
        foreach (var item in row.ItemArray)
            Console.Write($"{item}\t");
        Console.WriteLine();
    }
}

// Call the helper
PrintDataTable(dataTable);
```

### Ожидаемый вывод

```
ID      Name    Score   Ratio   Date        ...
1       Alice   95.12   0.8234  2023-01-15  ...
2       Bob     88.5    0.7612  2023-01-16  ...
3       Carol   73.33   0.6721  2023-01-17  ...
...
```

Обратите внимание, что числовые столбцы теперь показывают только четыре значимых цифры, соответствующие настройке `SignificantDigits = 4`, которую мы задали ранее.

## Шаг 5: Объединяем всё — полный, готовый к запуску пример

Ниже представлен полный код программы, который можно скопировать‑вставить в консольное приложение. Он включает обработку ошибок, необязательную проверку количества строк и вспомогательный метод для вывода.

```csharp
using System;
using System.Data;
using Aspose.Cells;

class ExportExcelDemo
{
    static void Main()
    {
        try
        {
            // 👉 Load the workbook
            Workbook workbook = new Workbook(@"C:\Path\To\Numbers.xlsx");

            // 👉 Set up export options (limit decimal places excel)
            ExportTableOptions exportOptions = new ExportTableOptions
            {
                SignificantDigits = 4
            };

            // 👉 Determine safe row count (export first 100 rows)
            int maxRows = workbook.Worksheets[0].Cells.MaxDataRow + 1;
            int rowsToExport = Math.Min(100, maxRows);

            // 👉 Export to DataTable (export excel to datatable, export excel with headers)
            DataTable dt = workbook.Worksheets[0].Cells.ExportDataTable(
                startRow: 0,
                startColumn: 0,
                totalRows: rowsToExport,
                totalColumns: 10,
                exportColumnNames: true,
                options: exportOptions);

            // 👉 Show a glimpse of the data
            PrintDataTable(dt);
        }
        catch (Exception ex)
        {
            Console.WriteLine($"❌ Something went wrong: {ex.Message}");
        }
    }

    static void PrintDataTable(DataTable table)
    {
        foreach (DataRow row in table.Rows)
        {
            foreach (var item in row.ItemArray)
                Console.Write($"{item}\t");
            Console.WriteLine();
        }
    }
}
```

Запустите программу, и вы увидите первые 100 строк вашего листа, аккуратно округлённые, с сохранёнными названиями столбцов.

## Часто задаваемые вопросы и подводные камни

| Вопрос | Ответ |
|----------|--------|
| **Что делать, если на листе есть объединённые ячейки?** | `ExportDataTable` «разворачивает» объединённые ячейки, беря значение верхней‑левой. Если требуется особая обработка, сначала разъедините их или читайте сырые объекты `Cell`. |
| **Можно ли экспортировать в `DataSet` вместо `DataTable`?** | Да — используйте `ExportDataTable` |

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}