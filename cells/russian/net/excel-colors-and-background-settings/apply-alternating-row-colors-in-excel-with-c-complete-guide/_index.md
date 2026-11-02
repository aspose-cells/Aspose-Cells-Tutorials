---
category: general
date: 2026-07-03
description: Применяйте чередующиеся цвета строк при импорте DataTable в Excel с помощью
  C#. Узнайте, как экспортировать DataTable из C# в Excel, сохранять стилизованную
  таблицу и сохранять форматирование книги.
draft: false
keywords:
- apply alternating row colors
- import datatable to excel
- export c# datatable to excel
- save styled table excel
- save workbook with formatting
language: ru
og_description: Применяйте чередующиеся цвета строк в Excel с помощью C#. Этот учебник
  показывает, как импортировать DataTable в Excel, экспортировать DataTable из C#
  в Excel и сохранять книгу с форматированием.
og_title: Применение чередования цветов строк в Excel с помощью C# – Полное руководство
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Apply alternating row colors while you import datatable to Excel using
    C#. Learn how to export C# datatable to Excel, save styled table excel, and keep
    workbook formatting.
  headline: Apply Alternating Row Colors in Excel with C# – Complete Guide
  type: TechArticle
- description: Apply alternating row colors while you import datatable to Excel using
    C#. Learn how to export C# datatable to Excel, save styled table excel, and keep
    workbook formatting.
  name: Apply Alternating Row Colors in Excel with C# – Complete Guide
  steps:
  - name: Expected Output
    text: '| ID | Name | Department | HireDate | |----|---------|------------|------------|
      | 1 | Alice | Finance | 15‑01‑2020 | | 2 | Bob | HR | 23‑06‑2019 | | 3 | Charlie
      | IT | 10‑03‑2021 | | 4 | Diana | Marketing | 05‑11‑2018 |'
  - name: What if my DataTable has thousands of rows?
    text: The `ImportDataTable` method streams data efficiently, but you might hit
      memory limits on very large tables. In such cases, consider splitting the export
      into multiple worksheets or using the `ImportDataTable` overload that lets you
      specify a start row and column.
  - name: Can I use custom colors instead of the built‑in ones?
    text: Absolutely. Just replace the `ForegroundColor` assignments in `styleWhite`
      and `styleGray` with any `System.Drawing.Color` you prefer—think pastel blues
      or corporate brand colors.
  - name: How do I ensure the alternating style works when the user adds rows later?
    text: If users edit the file manually, the original style array won’t automatically
      extend. A quick workaround is to convert the range into an Excel Table (`ListObject`)
      after import; Excel then repeats the pattern for new rows.
  type: HowTo
tags:
- C#
- Excel
- Aspose.Cells
- DataExport
title: Применение чередования цветов строк в Excel с помощью C# – Полное руководство
url: /ru/net/excel-colors-and-background-settings/apply-alternating-row-colors-in-excel-with-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Применение чередования цветов строк в Excel с C# – Полное руководство

Когда‑ли вам когда‑нибудь нужно было **применять чередование цветов строк** при экспорте `DataTable` из C# в Excel? Вы не одиноки — разработчики постоянно спрашивают, как сделать таблицы более аккуратными без ручного вмешательства в Excel после экспорта. Хорошая новость? Это можно сделать программно всего в несколько строк кода.

В этом руководстве мы пройдем через **import datatable to excel**, покажем, как **export c# datatable to excel** со стилизованной таблицей, и в конце **save styled table excel**, сохраняя форматирование. К концу вы сможете **save workbook with formatting**, выглядящий готовым к встрече с клиентом.

## Необходимые условия

- .NET 6.0 или новее (в примере используется .NET 6, но подходит любая современная версия)
- Aspose.Cells for .NET (бесплатная пробная версия или лицензия) — эта библиотека упрощает стилизацию
- Источник `DataTable` (может быть из базы данных, CSV или из‑памяти)

> **Совет:** Если у вас еще нет Aspose.Cells, вы можете получить его из NuGet с помощью `dotnet add package Aspose.Cells`.

## Шаг 1: Настройте проект и загрузите данные

Сначала создайте консольное приложение (или любой проект C#) и добавьте необходимые `using`‑директивы. Затем загрузите данные в `DataTable`. Для иллюстрации мы сгенерируем простую таблицу «на лету».

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Retrieve the source data as a DataTable
        DataTable sourceTable = GetSampleData();

        // The rest of the steps follow...
    }

    // Helper that creates a dummy DataTable
    static DataTable GetSampleData()
    {
        var table = new DataTable("Employees");
        table.Columns.Add("ID", typeof(int));
        table.Columns.Add("Name", typeof(string));
        table.Columns.Add("Department", typeof(string));
        table.Columns.Add("HireDate", typeof(DateTime));

        table.Rows.Add(1, "Alice", "Finance", new DateTime(2020, 1, 15));
        table.Rows.Add(2, "Bob", "HR", new DateTime(2019, 6, 23));
        table.Rows.Add(3, "Charlie", "IT", new DateTime(2021, 3, 10));
        table.Rows.Add(4, "Diana", "Marketing", new DateTime(2018, 11, 5));

        return table;
    }
}
```

**Почему это важно:** Наличие готового `DataTable` означает, что вы можете **import datatable to excel** одним вызовом, исключая необходимость ручного ввода ячейка за ячейкой.

## Шаг 2: Создайте Workbook и определите стили чередования строк

Теперь мы создадим новый `Workbook`. Хитрость **apply alternating row colors** заключается в `ImportTableOptions.StyleArray`. Мы используем первые два встроенных стиля (обычно белый и светло‑серый), но позже их можно настроить.

```csharp
// Step 2: Create a new workbook
Workbook workbook = new Workbook();

// Define two simple styles: white (default) and light gray
Style styleWhite = workbook.Styles[workbook.Styles.Add()];
styleWhite.ForegroundColor = System.Drawing.Color.White;
styleWhite.Pattern = BackgroundType.Solid;

Style styleGray = workbook.Styles[workbook.Styles.Add()];
styleGray.ForegroundColor = System.Drawing.Color.FromArgb(242, 242, 242); // light gray
styleGray.Pattern = BackgroundType.Solid;

// Step 3: Set up ImportTableOptions with the alternating styles
ImportTableOptions importOptions = new ImportTableOptions
{
    // The array alternates between the two styles for each row
    StyleArray = new Style[] { styleWhite, styleGray }
};
```

**Explanation:** `ImportTableOptions` сообщает Aspose.Cells, как обрабатывать каждую строку при импорте. Передавая `StyleArray` из двух элементов, библиотека автоматически окрашивает каждую нечётную строку первым стилем, а каждую чётную — вторым, что именно нужно для **apply alternating row colors**.

## Шаг 3: Перенесите DataTable на лист (включая заголовки)

С готовыми workbook и стилями мы теперь **import datatable to excel**. Метод `ImportDataTable` делает всю тяжёлую работу: записывает заголовки столбцов, учитывает массив стилей и размещает данные, начиная с ячейки A1.

```csharp
// Step 4: Import the DataTable into the first worksheet (include column headers)
Worksheet sheet = workbook.Worksheets[0];
sheet.Cells.ImportDataTable(sourceTable, true, importOptions);
```

**Почему мы передаём `true` во второй аргумент:** Это указывает методу записать имена столбцов в первую строку, что необходимо для профессионального отчёта.

## Шаг 4: Тонкая настройка таблицы (необязательно, но полезно)

Если хотите, чтобы столбцы автоматически подгонялись по ширине или добавить строку фильтра, несколько дополнительных строк сделают таблицу более удобной.

```csharp
// Auto‑fit all columns for readability
sheet.AutoFitColumns();

// Add a filter to the header row
sheet.AutoFilter.Range = $"A1:{CellsHelper.ColumnIndexToName(sourceTable.Columns.Count - 1)}1";
```

Эти правки не влияют на чередование цветов, но улучшают общее восприятие файла **save styled table excel**.

## Шаг 5: Сохраните Workbook, сохранив всё форматирование

Наконец, записываем файл на диск. Метод `Save` сохраняет каждый установленный стиль, гарантируя, что чередующиеся строки останутся неизменными.

```csharp
// Step 5: Save the workbook with the styled table
string outputPath = @"C:\Temp\StyledEmployees.xlsx";
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

Когда вы откроете `StyledEmployees.xlsx`, вы увидите чистую таблицу, где строки чередуются между белым и светло‑серым — именно тот визуальный сигнал, на который опираются многие пользователи для лучшей читаемости.

### Ожидаемый результат

| ID | Name    | Department | HireDate   |
|----|---------|------------|------------|
| 1  | Alice   | Finance    | 15‑01‑2020 |
| 2  | Bob     | HR         | 23‑06‑2019 |
| 3  | Charlie | IT         | 10‑03‑2021 |
| 4  | Diana   | Marketing  | 05‑11‑2018 |

- Строки 1, 3 … → фон белый  
- Строки 2, 4 … → фон светло‑серый  

Это весь процесс **save workbook with formatting**.

## Часто задаваемые вопросы и особенности

### Что делать, если мой DataTable содержит тысячи строк?

Метод `ImportDataTable` эффективно потоково передаёт данные, но при очень больших таблицах можно столкнуться с ограничениями памяти. В таких случаях рассмотрите разбивку экспорта на несколько листов или используйте перегрузку `ImportDataTable`, позволяющую указать начальную строку и столбец.

### Можно ли использовать собственные цвета вместо встроенных?

Конечно. Просто замените присваивания `ForegroundColor` в `styleWhite` и `styleGray` на любой `System.Drawing.Color`, который вам нужен — например, пастельные синие или фирменные цвета компании.

```csharp
styleWhite.ForegroundColor = System.Drawing.Color.LightBlue;
styleGray.ForegroundColor = System.Drawing.Color.LightCyan;
```

### Как обеспечить работу чередующегося стиля, если пользователь добавит строки позже?

Если пользователи редактируют файл вручную, исходный массив стилей не будет автоматически расширяться. Быстрый обходной путь — преобразовать диапазон в Excel Table (`ListObject`) после импорта; тогда Excel будет повторять шаблон для новых строк.

```csharp
int lastRow = sheet.Cells.MaxDataRow;
int lastCol = sheet.Cells.MaxDataColumn;
string tableRange = $"A1:{CellsHelper.ColumnIndexToName(lastCol)}{lastRow + 1}";
ListObject table = sheet.ListObjects[sheet.ListObjects.Add(tableRange, true)];
```

Теперь любая новая строка наследует чередующиеся цвета.

## Полный рабочий пример (все шаги в одном месте)

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Retrieve source data
        DataTable sourceTable = GetSampleData();

        // 2️⃣ Create workbook and define alternating styles
        Workbook workbook = new Workbook();

        Style styleWhite = workbook.Styles[workbook.Styles.Add()];
        styleWhite.ForegroundColor = System.Drawing.Color.White;
        styleWhite.Pattern = BackgroundType.Solid;

        Style styleGray = workbook.Styles[workbook.Styles.Add()];
        styleGray.ForegroundColor = System.Drawing.Color.FromArgb(242, 242, 242);
        styleGray.Pattern = BackgroundType.Solid;

        ImportTableOptions importOptions = new ImportTableOptions
        {
            StyleArray = new Style[] { styleWhite, styleGray }
        };

        // 3️⃣ Import DataTable (including headers)
        Worksheet sheet = workbook.Worksheets[0];
        sheet.Cells.ImportDataTable(sourceTable, true, importOptions);

        // 4️⃣ Optional polish
        sheet.AutoFitColumns();
        sheet.AutoFilter.Range = $"A1:{CellsHelper.ColumnIndexToName(sourceTable.Columns.Count - 1)}1";

        // 5️⃣ Save the styled workbook
        string outputPath = @"C:\Temp\StyledEmployees.xlsx";
        workbook.Save(outputPath);
        Console.WriteLine($"Workbook saved to {outputPath}");
    }

    static DataTable GetSampleData()
    {
        var table = new DataTable("Employees");
        table.Columns.Add("ID", typeof(int));
        table.Columns.Add("Name", typeof(string));
        table.Columns.Add("Department", typeof(string));
        table.Columns.Add("HireDate", typeof(DateTime));

        table.Rows.Add(1, "Alice", "Finance", new DateTime(2020, 1, 15));
        table.Rows.Add(2, "Bob", "HR", new DateTime(2019, 6, 23));
        table.Rows.Add(3, "Charlie", "IT", new DateTime(2021, 3, 10));
        table.Rows.Add(4, "Diana", "Marketing", new DateTime(2018, 11, 5));

        return table;
    }
}
```

Запустите программу, откройте сгенерированный файл, и вы сразу увидите применённые чередующиеся цвета — без необходимости ручного форматирования.

## Заключение

Мы только что продемонстрировали, как **apply alternating row colors** при **import datatable to excel** с помощью C#. Процесс охватывает всё, что нужно для **export c# datatable to excel**, **save styled table excel** и **save workbook with formatting**, выглядящего профессионально сразу «из коробки».

Что дальше? Попробуйте поменять местами два стиля для создания собственной темы или превратите диапазон в Excel Table, чтобы пользователи могли сортировать и фильтровать, сохраняя цветовой шаблон. Также можно изучить условное форматирование через `ConditionalFormattingCollection` для более динамичных визуальных подсказок.

Есть свои идеи

## Что стоит изучить дальше?

Следующие руководства охватывают тесно связанные темы, построенные на техниках, продемонстрированных в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, помогающими освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [Как импортировать DataTable в Excel с помощью Aspose.Cells для .NET (Пошаговое руководство)](/cells/english/net/import-export/import-datatable-excel-aspose-cells-net/)
- [Применение цветов и фонов в Excel с помощью Aspose.Cells для .NET](/cells/english/net/formatting/colors-and-background/)
- [Автоматизация цветов темы Excel с использованием Aspose.Cells .NET для эффективного форматирования](/cells/english/net/formatting/automate-excel-theme-colors-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}