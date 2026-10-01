---
category: general
date: 2026-10-01
description: Научитесь удалять строки из таблицы Excel и изменять имя таблицы Excel
  с помощью C#. Пошаговое руководство с полным кодом и лучшими практиками.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- delete rows excel table
- change excel table name
- load excel workbook c#
- remove rows from excel table
- update excel table name
language: ru
lastmod: 2026-10-01
og_description: Удалите строки из таблицы Excel и измените имя таблицы Excel в C#.
  Следуйте этому полному руководству, чтобы загрузить книгу, изменить таблицу и сохранить
  результат.
og_image_alt: Screenshot showing C# code that deletes rows from an Excel table and
  updates the table name
og_title: Удаление строк из таблицы Excel и изменение её имени в C# – полное руководство
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Learn to delete rows from an Excel table and change the Excel table
    name using C#. Step‑by‑step guide with full code and best practices.
  headline: How to delete rows from an Excel table and change its name in C#
  type: TechArticle
tags:
- C#
- Aspose.Cells
- Excel automation
title: Как удалить строки из таблицы Excel и изменить её название в C#
url: /ru/net/tables-and-lists/how-to-delete-rows-from-an-excel-table-and-change-its-name-i/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как удалить строки из таблицы Excel и изменить её имя в C#

Если вам нужно **удалить строки из таблицы Excel** при работе с C#, это руководство покажет точные необходимые шаги. Вы увидите, как **загрузить книгу Excel в C#**, удалить определённые строки из таблицы и затем **обновить имя таблицы Excel**, чтобы файл оставался согласованным.

В учебнике рассматриваются все необходимые детали: требуемые пакеты NuGet, полностью готовый к запуску код и типичные подводные камни, такие как нарушения структуры таблицы. К концу статьи вы сможете программно изменять любую таблицу Excel без ручного вмешательства.

## Предварительные требования

Прежде чем начать, убедитесь, что у вас есть:

* .NET 6.0 SDK или более поздняя версия.
* Visual Studio 2022 (или любая IDE для C#), настроенная для разработки под .NET.
* Библиотека **Aspose.Cells for .NET**, добавленная через NuGet (`Install-Package Aspose.Cells`).
* Существующая книга Excel (`Table.xlsx`), содержащая как минимум один лист с таблицей.

Эти элементы обеспечивают среду, необходимую для **load Excel workbook c#** кода и надёжного выполнения операций.

## Шаг 1: Загрузка книги, содержащей таблицу

Первой операцией является открытие файла книги. Aspose.Cells читает всю книгу в память, предоставляя полный контроль над листами, таблицами и данными ячеек.

```csharp
using Aspose.Cells;

string inputPath = @"C:\Data\Table.xlsx";

// Load the workbook from disk
Workbook workbook = new Workbook(inputPath);
```

*Почему это важно*: Загрузка книги является основой для любой последующей манипуляции таблицей. Объект `Workbook` раскрывает коллекцию `Worksheets`, которую вы будете использовать для поиска целевой таблицы.

## Шаг 2: Доступ к первому листу и его первой таблице

Большинство файлов Excel хранят таблицы на первом листе, но при необходимости можно изменить индекс. Следующий код получает первый объект `Table`.

```csharp
// Access the first worksheet (index 0)
Worksheet sheet = workbook.Worksheets[0];

// Retrieve the first table on that worksheet
Table table = sheet.Tables[0];
```

Если на листе нет таблицы, `sheet.Tables.Count` будет равен нулю, и вы должны обработать этот случай. Попытка доступа к `sheet.Tables[0]`, когда таблиц нет, вызовет исключение, поэтому в производственном коде рекомендуется использовать проверку.

## Шаг 3: Удаление строк из таблицы Excel

Чтобы **удалить строки из таблицы Excel**, вызовите `DeleteRows(startRow, totalRows)`. Параметр `startRow` задаётся с нуля относительно первой строки данных таблицы (строка после заголовка).

```csharp
// Delete two rows starting from the second data row (index 1)
int startRow = 1;   // second row within the table
int rowsToDelete = 2;

table.DeleteRows(startRow, rowsToDelete);
```

### Почему использовать `DeleteRows`, а не удалять строки листа?

`DeleteRows` обновляет внутренний диапазон таблицы, сохраняя формулы, стили и определённые имена, принадлежащие таблице. Прямое удаление строк листа может нарушить структуру таблицы и вызвать исключение.

**Пограничный случай**: Если удаление оставит таблицу без строк данных, Aspose.Cells бросит `ArgumentException`. Защититесь, проверив `table.RowCount` перед удалением.

```csharp
if (table.RowCount - rowsToDelete < 1)
{
    throw new InvalidOperationException("Cannot delete all data rows from the table.");
}
```

## Шаг 4: Изменение имени таблицы Excel

После удаления строк вы, возможно, захотите задать таблице более описательное имя. Свойство `Name` задаёт определённое имя таблицы, которое используется в формулах и VBA.

```csharp
// Assign a new name to the table
string newTableName = "SalesData2026";

if (workbook.Worksheets.GetDefinedNames().Any(d => d.Text == newTableName))
{
    throw new InvalidOperationException($"The name '{newTableName}' already exists as a defined name.");
}

table.Name = newTableName;
```

*Зачем переименовывать?* Чёткое имя таблицы улучшает читаемость формул (`=SUM(SalesData2026[Amount])`) и предотвращает конфликты имён, когда несколько таблиц имеют схожие назначения.

## Шаг 5: Сохранение изменённой книги (по желанию)

Сохраните изменения, записав их в новый файл или перезаписав оригинал. Сохранение в новое место безопаснее во время разработки.

```csharp
string outputPath = @"C:\Data\ModifiedTable.xlsx";
workbook.Save(outputPath);
```

Метод `Save` записывает обновлённую книгу, включая изменённый диапазон таблицы и новое имя таблицы, на диск.

## Полный рабочий пример

Объединяя все шаги, получаем автономную программу, которую можно сразу запустить.

```csharp
using System;
using System.Linq;
using Aspose.Cells;

class ExcelTableModifier
{
    static void Main()
    {
        // ----- Step 1: Load workbook -----
        string inputPath = @"C:\Data\Table.xlsx";
        Workbook workbook = new Workbook(inputPath);

        // ----- Step 2: Access worksheet and table -----
        Worksheet sheet = workbook.Worksheets[0];
        if (sheet.Tables.Count == 0)
        {
            Console.WriteLine("No tables found on the first worksheet.");
            return;
        }

        Table table = sheet.Tables[0];

        // ----- Step 3: Delete rows -----
        int startRow = 1;      // second data row (zero‑based)
        int rowsToDelete = 2;

        if (table.RowCount - rowsToDelete < 1)
        {
            Console.WriteLine("Deletion would remove all data rows; operation aborted.");
            return;
        }

        table.DeleteRows(startRow, rowsToDelete);
        Console.WriteLine($"{rowsToDelete} rows removed starting at index {startRow}.");

        // ----- Step 4: Change table name -----
        string newTableName = "SalesData2026";

        bool nameExists = workbook.Worksheets.GetDefinedNames()
                               .Any(d => d.Text.Equals(newTableName, StringComparison.OrdinalIgnoreCase));

        if (nameExists)
        {
            Console.WriteLine($"The name '{newTableName}' already exists. Choose a different name.");
            return;
        }

        table.Name = newTableName;
        Console.WriteLine($"Table renamed to '{newTableName}'.");

        // ----- Step 5: Save workbook -----
        string outputPath = @"C:\Data\ModifiedTable.xlsx";
        workbook.Save(outputPath);
        Console.WriteLine($"Modified workbook saved to '{outputPath}'.");
    }
}
```

**Ожидаемый вывод** (при наличии файла и таблицы):

```
2 rows removed starting at index 1.
Table renamed to 'SalesData2026'.
Modified workbook saved to 'C:\Data\ModifiedTable.xlsx'.
```

Запуск программы обновит файл Excel точно так, как описано: строки будут удалены, имя таблицы изменится, а результат будет сохранён без ручного редактирования.

## Часто задаваемые вопросы и устранение неполадок

| Вопрос | Ответ |
|----------|--------|
| *Что происходит, если таблица охватывает объединённые ячейки?* | `DeleteRows` учитывает объединённые диапазоны. Если объединённая ячейка пересекает границу удаления, Aspose.Cells автоматически корректирует объединение. Проверьте результат визуально, если используете сложные объединения. |
| *Можно ли удалить строки из таблицы, которая является частью кэша сводной таблицы?* | Удаление строк из исходной таблицы, питающей сводную, **не** обновляет кэш сводной автоматически. После изменения исходной таблицы вызовите `pivotTable.RefreshData()`. |
| *Можно ли удалять строки по условию (например, значение < 0)?* | Да. Пройдитесь по `table.ListObjects` или `table.Rows`, найдите подходящие строки, соберите их индексы и вызовите `DeleteRows` для каждого диапазона. |
| *Нужно ли освобождать объект `Workbook`?* | `Workbook` реализует `IDisposable`. Оберните его в блок `using` для детерминированного освобождения ресурсов, особенно при работе с большими файлами. |
| *Чем это отличается от использования EPPlus?* | EPPlus также поддерживает работу с таблицами, но использует другой API (`ExcelTable`). Концепции загрузки книги, удаления строк и переименования таблицы аналогичны. Выбирайте библиотеку, соответствующую вашим лицензионным требованиям. |

## Лучшие практики при модификации таблиц Excel в C#

* **Проверяйте индексы** – Индексы строк таблицы начинаются с нуля; ошибки «на один» приводят к неожиданным удалениями.
* **Проверяйте конфликты имён** – Excel не допускает дублирование определённых имён; всегда проверяйте уникальность перед присвоением нового имени.
* **Создавайте резервные копии оригинальных файлов** – Автоматические скрипты могут повредить данные; храните копию исходной книги.
* **Используйте `using`** – Гарантирует своевременное освобождение файловых дескрипторов:

```csharp
using (Workbook wb = new Workbook(inputPath))
{
    // modify workbook
}
```

* **Тестируйте пограничные случаи** – Таблицы с единственной строкой данных, таблицы, охватывающие весь лист, и таблицы, связанные с диаграммами, следует проверять после внесения изменений.

## Заключение

Теперь вы знаете, как **удалять строки из таблицы Excel** и **изменять имя таблицы Excel** с помощью C#. Полное решение загружает книгу, получает целевую таблицу, удаляет нужные строки, переименовывает таблицу и сохраняет результат. Применяйте эти техники для автоматизации генерации отчётов, очистки данных или любого рабочего процесса, требующего программного управления таблицами Excel.

Далее изучайте связанные темы, такие как **обновление значений ячеек в таблице Excel**, **добавление новых строк программно** и **экспорт данных таблицы в CSV**. Освоив эти операции, вы получите полный контроль над файлами Excel из ваших C# приложений.


## Что изучать дальше?


Следующие учебники охватывают тесно связанные темы, расширяющие техники, продемонстрированные в этом руководстве. Каждый ресурс содержит полностью рабочие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы в собственных проектах.

- [How to Rename Table in Excel with C# – Step‑by‑Step Guide](/cells/english/net/tables-and-lists/how-to-rename-table-in-excel-with-c-step-by-step-guide/)
- [Create Excel Table in C# – Step‑by‑Step Guide](/cells/english/net/tables-and-lists/create-excel-table-in-c-step-by-step-guide/)
- [Get First Table from Excel Workbook in C# – Complete Guide](/cells/english/net/excel-autofilter-validation/get-first-table-from-excel-workbook-in-c-complete-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}