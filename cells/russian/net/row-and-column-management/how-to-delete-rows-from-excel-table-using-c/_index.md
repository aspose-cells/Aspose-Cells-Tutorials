---
category: general
date: 2026-09-27
description: Узнайте, как удалять строки из таблицы Excel в C# с пошаговым руководством,
  которое также показывает, как быстро загрузить рабочую книгу Excel в C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- delete rows from Excel table
- load Excel workbook C#
language: ru
lastmod: 2026-09-27
og_description: Удалить строки из таблицы Excel в C# с понятным примером. Этот учебник
  также охватывает, как загрузить книгу Excel в C# и обработать распространённые граничные
  случаи.
og_image_alt: Screenshot illustrating delete rows from Excel table using C# code
og_title: Удаление строк из таблицы Excel в C# — полное руководство по коду
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Learn how to delete rows from Excel table in C# with a step‑by‑step
    guide that also shows how to load Excel workbook C# quickly.
  headline: How to delete rows from Excel table using C#
  type: TechArticle
- description: Learn how to delete rows from Excel table in C# with a step‑by‑step
    guide that also shows how to load Excel workbook C# quickly.
  name: How to delete rows from Excel table using C#
  steps:
  - name: What if the table has a different name or position?
    text: '* **Named table:** Use `ws.ListObjects["MyTableName"]` instead of the index.
      * **Multiple tables:** Loop through `ws.ListObjects` and pick the one that matches
      a condition (e.g., column header names). * **Dynamic row count:** You can compute
      `rowCount` at runtime by inspecting `ws.ListObjects[0].Dat'
  - name: Edge‑case handling
    text: '| Situation | Recommended code change | |----------------------------------------|--------------------------------------------------------------|
      | Table is empty or has fewer rows | Check `ws.ListObjects[0].DataRange.RowCount`
      before deleting. | | Rows to delete exceed table size | Clamp `rowCount`'
  - name: How do I delete rows from **all** tables in a workbook?
    text: '```csharp foreach (Worksheet sheet in workbook.Worksheets) { foreach (ListObject
      tbl in sheet.ListObjects) { // Example: delete the first data row of each table
      if (tbl.DataRange.RowCount > 1) tbl.DeleteRows(1, 1); } } ```'
  - name: Can I delete rows based on a **cell value**?
    text: 'Yes. Scan the `DataRange` for matching cells, collect their zero‑based
      indices, then delete in descending order:'
  - name: What if I need to **preserve formatting**?
    text: '`DeleteRows` removes the entire row from the table but retains the table’s
      style for remaining rows. If you need to keep specific formatting on a row you’re
      deleting, copy the style to another row before deletion.'
  - name: Does this work with **.xls** (Excel 97‑2003) files?
    text: Yes. Aspose.Cells automatically detects the file format, so the same code
      works with `.xls`. Just change the file extension in the `Workbook` constructor.
  - name: Next steps
    text: '* Explore **ClosedXML** or **EPPlus** if you prefer a fully open‑source
      stack. * Combine row deletion with **data validation** to clean spreadsheets
      before importing into a database. * Automate the process for a folder of workbooks
      using `Directory.GetFiles` and a loop.'
  type: HowTo
tags:
- Excel
- C#
- .NET
title: Как удалить строки из таблицы Excel с помощью C#
url: /ru/net/row-and-column-management/how-to-delete-rows-from-excel-table-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Удалить строки из таблицы Excel в C# – полное руководство по программированию

Если вам нужно **удалить строки из таблицы Excel** в файле .xlsx, этот учебник покажет, как сделать это с помощью C#. Вы увидите краткий, исполняемый пример, который загружает рабочую книгу Excel, удаляет определённые строки из первой таблицы и сохраняет результат. Подход работает с популярной библиотекой Aspose.Cells и может быть адаптирован к другим .NET API для Excel.

Удаление строк из таблицы — распространённая задача при очистке импортированных данных, сокращении разделов отчётов или автоматизации обновлений таблиц. К концу этого руководства вы сможете **загрузить рабочую книгу Excel C#**, найти таблицу (ListObject), удалить любые выбранные строки и записать изменённый файл обратно на диск.

## Требования

* .NET 6.0 или новее установлен (код также работает с .NET Framework 4.7+).
* Ссылка на пакет NuGet **Aspose.Cells** (или любую совместимую библиотеку, предоставляющую типы `Workbook`, `Worksheet` и `ListObject`).
* Входной файл с именем `input.xlsx`, размещённый в папке, к которой вы можете обратиться из проекта.
* Базовое знакомство с синтаксисом C# и Visual Studio (или вашей предпочтительной IDE).

> **Pro tip:** Если вы предпочитаете открытый альтернативный вариант, ту же логику можно применить с **ClosedXML** — просто замените специфические для Aspose классы на `XLWorkbook`, `IXLWorksheet` и `IXLTable`.

## Шаг 1: Загрузить рабочую книгу Excel в C#

Первая операция — прочитать исходный файл в память. Загрузка рабочей книги занимает мало ресурсов для типичных размеров таблиц и предоставляет полный доступ к листам, таблицам и значениям ячеек.

```csharp
using Aspose.Cells;

// Step 1: Load the workbook
// Replace YOUR_DIRECTORY with the actual folder path, e.g. @"C:\Data"
Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");
```

*Почему это важно:* `Workbook` разбирает структуру Open XML файла .xlsx, предоставляя коллекцию объектов `Worksheet`. Если файл не найден, Aspose бросает `FileNotFoundException`, поэтому убедитесь, что путь указан правильно.

## Шаг 2: Доступ к целевому листу

Большинство электронных таблиц содержат несколько листов; вам нужно выбрать тот, который содержит таблицу, которую вы хотите изменить. Здесь мы используем первый лист (`Worksheets[0]`), что является безопасным значением по умолчанию для простых файлов.

```csharp
// Step 2: Access the first worksheet
Worksheet ws = workbook.Worksheets[0];
```

*Почему это важно:* `Worksheet` является контейнером для таблиц (`ListObjects`). Доступ к правильному листу предотвращает случайные изменения несвязанных данных.

## Шаг 3: Удалить строки из таблицы Excel

Таблицы Excel представлены объектами `ListObject`. Первая таблица на листе — `ListObjects[0]`. Метод `DeleteRows(startIndex, rowCount)` удаляет строки **относительно области данных таблицы**, а не абсолютных номеров строк листа.

В этом примере мы удаляем вторую и третью строки таблицы (заголовок — строка 0, поэтому начинаем с индекса 1).

```csharp
// Step 3: Delete rows 1 and 2 from the first table (ListObject)
// The first row (index 0) is the header, so we start at index 1
ws.ListObjects[0].DeleteRows(1, 2);
```

### Что если у таблицы другое имя или позиция?

* **Именованная таблица:** используйте `ws.ListObjects["MyTableName"]` вместо индекса.
* **Несколько таблиц:** пройдитесь по `ws.ListObjects` и выберите ту, которая соответствует условию (например, названиям заголовков столбцов).
* **Динамическое количество строк:** вы можете вычислить `rowCount` во время выполнения, проверяя `ws.ListObjects[0].DataRange.RowCount`.

### Обработка граничных случаев

| Ситуация                              | Рекомендуемое изменение кода                                      |
|----------------------------------------|--------------------------------------------------------------|
| Таблица пуста или имеет меньше строк      | Проверьте `ws.ListObjects[0].DataRange.RowCount` перед удалением. |
| Количество строк для удаления превышает размер таблицы       | Ограничьте `rowCount` значением `DataRange.RowCount - startIndex`.       |
| Необходимо удалять строки по условию (например, значение в столбце C) | Пройдите `DataRange.Rows` и соберите подходящие индексы, затем удаляйте в обратном порядке, чтобы индексы оставались стабильными. |

## Шаг 4: Сохранить изменённую рабочую книгу

После удаления запишите рабочую книгу обратно в новый файл (или перезапишите оригинал, если хотите). Сохранение создаёт новый .xlsx, отражающий обновлённую таблицу.

```csharp
// Step 4: Save the modified workbook
workbook.Save(@"YOUR_DIRECTORY\output.xlsx");
```

*Почему это важно:* `Save` сериализует представление в памяти на диск. Если нужно сохранить оригинальный файл, всегда записывайте в другой путь.

## Полный, исполняемый пример

Объединение всех шагов даёт вам автономную программу, которую можно скопировать, вставить и запустить.

```csharp
using System;
using Aspose.Cells;

class ExcelRowDeletion
{
    static void Main()
    {
        // Adjust the folder path as needed
        const string folder = @"YOUR_DIRECTORY";

        // Load the workbook (load Excel workbook C#)
        Workbook workbook = new Workbook($"{folder}\\input.xlsx");

        // Access the first worksheet
        Worksheet ws = workbook.Worksheets[0];

        // Ensure the worksheet contains at least one table
        if (ws.ListObjects.Count == 0)
        {
            Console.WriteLine("No tables found on the first worksheet.");
            return;
        }

        // Delete rows 1 and 2 from the first table (skip header)
        ListObject table = ws.ListObjects[0];
        int rowsToDelete = Math.Min(2, table.DataRange.RowCount - 1); // guard against short tables
        if (rowsToDelete > 0)
        {
            table.DeleteRows(1, rowsToDelete);
            Console.WriteLine($"Deleted {rowsToDelete} row(s) from table \"{table.Name}\".");
        }
        else
        {
            Console.WriteLine("Table does not have enough rows to delete.");
        }

        // Save the result
        workbook.Save($"{folder}\\output.xlsx");
        Console.WriteLine("Workbook saved as output.xlsx");
    }
}
```

**Ожидаемый вывод** (консоль):

```
Deleted 2 row(s) from table "Table1".
Workbook saved as output.xlsx
```

Откройте `output.xlsx` — первая таблица теперь без удалённых строк, при этом строка заголовка остаётся нетронутой.

## Часто задаваемые вопросы и варианты

### Как удалить строки из **всех** таблиц в рабочей книге?

```csharp
foreach (Worksheet sheet in workbook.Worksheets)
{
    foreach (ListObject tbl in sheet.ListObjects)
    {
        // Example: delete the first data row of each table
        if (tbl.DataRange.RowCount > 1)
            tbl.DeleteRows(1, 1);
    }
}
```

### Можно ли удалить строки на основе **значения ячейки**?

Да. Просканируйте `DataRange` в поисках совпадающих ячеек, соберите их нулевые индексы, затем удаляйте в порядке убывания:

```csharp
var rowsToRemove = new List<int>();
for (int i = 0; i < table.DataRange.RowCount; i++)
{
    var cell = table.DataRange[i, 2]; // column C (zero‑based)
    if (cell.StringValue == "Obsolete")
        rowsToRemove.Add(i);
}

// Delete rows from bottom to top to keep indices valid
rowsToRemove.Sort((a, b) => b.CompareTo(a));
foreach (int rowIdx in rowsToRemove)
    table.DeleteRows(rowIdx, 1);
```

### Что если нужно **сохранить форматирование**?

`DeleteRows` удаляет всю строку из таблицы, но сохраняет стиль таблицы для оставшихся строк. Если необходимо сохранить определённое форматирование строки, которую удаляете, скопируйте стиль в другую строку перед удалением.

### Работает ли это с файлами **.xls** (Excel 97‑2003)?

Да. Aspose.Cells автоматически определяет формат файла, поэтому тот же код работает с `.xls`. Просто измените расширение файла в конструкторе `Workbook`.

## Советы по производительности

* **Пакетные удаления:** Удаление множества строк по одной может быть медленнее. По возможности используйте один вызов `DeleteRows(start, count)`.
* **Избегайте блокировки UI‑потока:** Если вы интегрируете это в настольное приложение, выполняйте манипуляцию с рабочей книгой в фоновом потоке, чтобы UI оставался отзывчивым.
* **Корректное освобождение ресурсов:** Хотя Aspose.Cells использует управляемую память, оберните `Workbook` в блок `using`, если работаете с большими файлами, чтобы своевременно освободить ресурсы.

## Заключение

Теперь у вас есть полный, готовый к продакшн пример, который **удаляет строки из таблицы Excel** с помощью C#. Руководство охватило, как **загрузить рабочую книгу Excel C#**, найти нужный `ListObject`, безопасно удалить строки и сохранить обновлённый файл. С учётом обработки граничных случаев и советов по производительности, вы можете адаптировать этот шаблон к более сложным сценариям, таким как условные удаления, несколько таблиц или альтернативные .NET библиотеки для Excel.

### Следующие шаги

* Изучите **ClosedXML** или **EPPlus**, если предпочитаете полностью открытый стек.
* Сочетайте удаление строк с **валидацией данных**, чтобы очищать таблицы перед импортом в базу данных.
* Автоматизируйте процесс для папки рабочих книг, используя `Directory.GetFiles` и цикл.

Не стесняйтесь экспериментировать с различными диапазонами строк, именами таблиц и условной логикой. Приятного кодинга!

## Что вам стоит изучить дальше?

Следующие учебники охватывают тесно связанные темы, которые развивают техники, продемонстрированные в этом руководстве. Каждый ресурс включает полные работающие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [Загрузить файл Excel C# – Как удалить строки и удалить конкретные строки](/cells/english/net/row-and-column-management/load-excel-file-c-how-to-delete-rows-and-remove-specific-row/)
- [Как вставлять и удалять строки в Excel с Aspose.Cells для .NET: Полное руководство](/cells/english/net/data-manipulation/aspose-cells-net-insert-delete-excel-rows/)
- [Как удалить пустые строки в Excel с помощью Aspose.Cells .NET для очистки данных](/cells/english/net/data-manipulation/delete-blank-rows-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}