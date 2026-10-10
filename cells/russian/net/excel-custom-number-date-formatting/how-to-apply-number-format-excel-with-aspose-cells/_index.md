---
category: general
date: 2026-10-10
description: Быстро примените числовой формат в Excel, импортируя DataTable, задавая
  форматы даты и валюты и сохраняя строку заголовка, всё в один шаг.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- apply number format excel
- set date format excel
- format excel cells date
- set currency format excel
- preserve header row excel
language: ru
lastmod: 2026-10-10
og_description: Примените числовой формат в Excel с помощью C# и Aspose.Cells. Узнайте,
  как установить формат даты в Excel, формат валюты в Excel и сохранить строку заголовка
  в Excel при импорте DataTable.
og_image_alt: Excel worksheet showing currency and date columns formatted after import
og_title: Применение числового формата Excel в C# – пошаговое руководство
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: apply number format excel quickly by importing a DataTable, setting
    date and currency formats, and preserving header row excel in a single step.
  headline: How to apply number format excel with Aspose.Cells
  type: TechArticle
tags:
- excel
- aspnet
- csharp
- excel-formatting
title: Как применить числовой формат в Excel с Aspose.Cells
url: /ru/net/excel-custom-number-date-formatting/how-to-apply-number-format-excel-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как применить числовой формат Excel с Aspose.Cells

Если вам нужно **apply number format excel** при загрузке данных из `DataTable`, это руководство покажет, как это сделать. Вы также узнаете, как **set date format excel**, **set currency format excel** и **preserve header row excel** во время импорта, чтобы полученный лист выглядел профессионально без дополнительной пост‑обработки.

Мы рассмотрим всё: от установки библиотеки до написания полного, исполняемого фрагмента кода. К концу вы сможете импортировать любой `DataTable` в книгу Excel, автоматически форматировать числовые столбцы и сохранять строку заголовка нетронутой — всё это в нескольких строках C#.

## Требования

* .NET 6.0 или новее (код также работает с .NET Framework 4.6+)
* Visual Studio 2022 (или любой предпочитаемый вами IDE для C#)
* **Aspose.Cells for .NET** – установить через NuGet:

```bash
dotnet add package Aspose.Cells
```

* Источник `DataTable` — в примере используется вспомогательный метод `GetTable()`, который возвращает примерные данные.

> **Совет:** Aspose.Cells — коммерческая библиотека, но она предоставляет бесплатный режим оценки, который отключает водяной знак на срок до 30 дней.

## Шаг 1: Создать книгу и получить доступ к первому листу

Объект workbook является точкой входа для всех операций с Excel. Создание новой книги предоставляет лист по умолчанию с индексом 0.

```csharp
using Aspose.Cells;
using System;
using System.Data;

class Program
{
    static void Main()
    {
        // Create a new workbook
        Workbook wb = new Workbook();

        // Obtain reference to the first worksheet
        Worksheet sheet = wb.Worksheets[0];
```

*Почему этот шаг?*  
`Workbook` управляет форматом файла, движком вычислений и репозиторием стилей. Ранний доступ к `Worksheet` позволяет позже передать целевой лист в метод импорта.

## Шаг 2: Получить исходные данные в виде DataTable

В реальных проектах данные часто поступают из запроса к базе данных, парсера CSV или ответа API. Для иллюстрации мы создаём простой `DataTable` с тремя столбцами: **Product**, **Price** и **ReleaseDate**.

```csharp
        // Step 2: Retrieve the source data as a DataTable
        DataTable sourceTable = GetTable();
```

```csharp
        // Helper method that builds a sample DataTable
        static DataTable GetTable()
        {
            DataTable dt = new DataTable();
            dt.Columns.Add("Product", typeof(string));
            dt.Columns.Add("Price", typeof(decimal));
            dt.Columns.Add("ReleaseDate", typeof(DateTime));

            dt.Rows.Add("Widget A", 12.99m, new DateTime(2023, 5, 1));
            dt.Rows.Add("Widget B", 23.50m, new DateTime(2023, 6, 15));
            dt.Rows.Add("Widget C", 7.75m, new DateTime(2023, 7, 30));
            return dt;
        }
```

*Почему этот шаг?*  
`DataTable` предоставляет табличное представление в памяти, которое Aspose.Cells может импортировать напрямую, сохраняя порядок столбцов и типы данных.

## Шаг 3: Подготовить массив `Style` — один стиль на столбец

Aspose.Cells позволяет применять отдельный стиль к каждому столбцу во время импорта, передавая массив объектов `Style`. Длина массива должна соответствовать количеству столбцов в исходной таблице.

```csharp
        // Step 3: Prepare an array of Style objects – one for each column
        Style[] columnStyles = new Style[sourceTable.Columns.Count];
        for (int i = 0; i < columnStyles.Length; i++)
        {
            // Each entry must be instantiated before we can set properties
            columnStyles[i] = wb.CreateStyle();
        }
```

*Почему этот шаг?*  
Если пропустить явное создание (`CreateStyle()`), попытка установить `Number` вызовет `NullReferenceException`. Инициализация каждого `Style` гарантирует успешное последующее присвоение.

## Шаг 4: Назначить числовые форматы — валюта и дата

Excel определяет встроенные числовые форматы по ID.

* **14** – Валюта (например, `$1,234.00`)  
* **22** – Краткая дата (`mm/dd/yyyy`)

```csharp
        // Step 4: Assign number formats to the desired columns
        // Column 0 – Product name (no format needed)
        // Column 1 – Currency format (Number format ID 14)
        columnStyles[1].Number = 14;   // set currency format excel

        // Column 2 – Date format (Number format ID 22)
        columnStyles[2].Number = 22;   // set date format excel
```

> **Примечание:** Если нужен пользовательский формат (например, `"¥#,##0.00"`), используйте `Style.Custom = "¥#,##0.00"` вместо встроенного ID.

*Почему этот шаг?*  
Применение правильного **number format** во время импорта устраняет необходимость второго прохода, проходящего по ячейкам для изменения форматирования. Это также гарантирует, что **format excel cells date** и **set currency format excel** будут согласованы во всех строках.

## Шаг 5: Импортировать DataTable, сохранив строку заголовка

Метод `ImportDataTable` может копировать данные, сохранять первую строку как заголовок и применять подготовленные стили столбцов.

```csharp
        // Step 5: Import the DataTable into the worksheet
        // Parameters:
        //   sourceTable – the DataTable to import
        //   true        – preserve the header row (preserve header row excel)
        //   "A1"        – start cell
        //   columnStyles – array of styles for each column
        sheet.Cells.ImportDataTable(sourceTable, true, "A1", columnStyles);
```

```csharp
        // Save the workbook to disk
        wb.Save("FormattedReport.xlsx");
        Console.WriteLine("Workbook created successfully.");
    }
}
```

**Ожидаемый результат** — откройте `FormattedReport.xlsx`, и вы увидите:

| Продукт | Цена (валюта) | Дата выпуска (дата) |
|---------|------------------|--------------------|
| Widget A| $12.99           | 05/01/2023         |
| Widget B| $23.50           | 06/15/2023         |
| Widget C| $7.75            | 07/30/2023         |

Строка заголовка сохранена, столбец **Price** отображает символ валюты, а столбец **ReleaseDate** показывает короткий формат даты — всё без дополнительного кода стилизации.

### Обработка распространённых граничных случаев

| Ситуация                               | Решение |
|----------------------------------------|----------|
| **Больше столбцов, чем стилей**           | Убедитесь, что `columnStyles.Length` равно `sourceTable.Columns.Count`. Отсутствующие элементы используют стиль по умолчанию книги. |
| **Null‑значения в числовых столбцах**     | Excel рассматривает `null` как пустую ячейку; числовой формат всё равно применяется, когда позже вводится значение. |
| **Пользовательская валюта, зависящая от локали**    | Используйте `columnStyles[i].Custom = "\"€\"#,##0.00"` и установите `columnStyles[i].Number = -1`, чтобы отключить встроенный ID. |
| **Большие таблицы ( > 100 000 строк )**    | Рассмотрите возможность использования перегрузки `ImportDataTable` с `ImportTableOptions` для потоковой передачи данных и снижения нагрузки на память. |
| **Применение одного и того же стиля к нескольким столбцам** | Повторно используйте один и тот же экземпляр `Style` в массиве (например, `columnStyles[1] = columnStyles[2] = dateStyle;`). |

## Бонус: Использование пользовательской строки формата

Если встроенные ID не подходят, вы можете определить пользовательский числовой формат:

```csharp
// Example: display Euro currency with no decimal places
Style euroStyle = wb.CreateStyle();
euroStyle.Custom = "\"€\"#,##0";
columnStyles[1] = euroStyle;   // replace the built‑in currency style
```

Этот подход даёт вам полный контроль над **format excel cells date** и **set currency format excel** за пределами предопределённых ID.

## Заключение

Теперь вы знаете, как эффективно **apply number format excel** при импорте `DataTable` с помощью Aspose.Cells. Создавая массив `Style` для каждого столбца, назначая встроенные или пользовательские числовые ID и используя перегрузку `ImportDataTable`, которая **preserve header row excel**, вы можете генерировать готовые к публикации листы в одной операции.

### Что дальше?

* Исследуйте **set date format excel** с пользовательскими шаблонами, например `"dddd, mmmm dd, yyyy"`.
* Сочетайте эту технику с **conditional formatting**, чтобы выделять значения вне диапазона.
* Используйте **format excel cells date** в сводных таблицах или диаграммах для динамической отчётности.

Не стесняйтесь экспериментировать с различными числовыми ID или пользовательскими строками, чтобы соответствовать руководству по стилю вашей организации. Приятного кодирования!

## Что вам стоит изучить дальше?

Следующие учебные материалы охватывают тесно связанные темы, основанные на техниках, продемонстрированных в этом руководстве. Каждый ресурс содержит полностью работающие примеры кода с пошаговыми объяснениями, помогающими освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [apply number format excel – Пошаговое руководство по форматированию столбцов](/cells/english/net/number-and-display-formats-in-excel/apply-number-format-excel-step-by-step-guide-to-formatting-c/)
- [Create Excel Workbook C# – Применить валютный формат и импортировать DataTable](/cells/english/net/excel-data-import-export/create-excel-workbook-c-apply-currency-format-and-import-dat/)
- [Set date format in Excel with C# – Полное руководство по форматированию при импорте](/cells/english/net/excel-custom-number-date-formatting/set-date-format-in-excel-with-c-full-import-formatting-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}