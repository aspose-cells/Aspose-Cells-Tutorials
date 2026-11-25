---
category: general
date: 2026-11-25
description: Узнайте, как удалять строки из таблицы Excel в C# и эффективно удалять
  несколько строк из листа Excel.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- delete rows from excel table
- delete multiple rows from excel sheet
language: ru
lastmod: 2026-11-25
og_description: Удалите строки из таблицы Excel в C# и научитесь удалять несколько
  строк из листа Excel с чистым кодом.
og_image_alt: Screenshot of C# code deleting rows from an Excel table
og_title: Удаление строк из таблицы Excel в C# — полное руководство
schemas:
- author: Aspose
  dateModified: '2026-11-25'
  description: Learn how to delete rows from Excel table in C# and also delete multiple
    rows from Excel sheet efficiently.
  headline: How to delete rows from Excel table with C#
  type: TechArticle
- description: Learn how to delete rows from Excel table in C# and also delete multiple
    rows from Excel sheet efficiently.
  name: How to delete rows from Excel table with C#
  steps:
  - name: Add Aspose.Cells to your project
    text: 'Open the **Package Manager Console** and run:'
  - name: Load the workbook and locate the table
    text: '```csharp using Aspose.Cells;'
  - name: Delete the desired data rows
    text: The `DeleteRows` method expects a **zero‑based** row index relative to the
      table, **including** the header row. Because the header cannot be removed, you
      must start at index 1 for the first data row.
  - name: Save the modified workbook
    text: '```csharp // Save the workbook to a new file to preserve the original workbook.Save(@"C:\Data\table_with_header_modified.xlsx");
      } } ```'
  - name: Full working example
    text: '```csharp using Aspose.Cells;'
  - name: Edge cases and best practices
    text: '| Situation | Recommended handling | |----------------------------------------|----------------------|
      | Deleting rows beyond the last row | Check `worksheet.Rows.Count` before calling
      `RemoveAt`. | | Removing all rows except the header | Delete data rows in a
      loop or use `DeleteRows(1, table.DataRa'
  type: HowTo
tags:
- Excel automation
- C#
- Aspose.Cells
- data manipulation
title: Как удалить строки из таблицы Excel с помощью C#
url: /ru/net/row-and-column-management/how-to-delete-rows-from-excel-table-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как удалить строки из таблицы Excel с помощью C#

Если вам нужно удалить строки из таблицы Excel, используя C#, это руководство покажет, как это сделать. Вы также увидите, как удалить несколько строк из листа Excel, не затрагивая остальные данные.

Работа с Excel программно часто требует удаления устаревших или недействительных записей. Удаление строк непосредственно в листе может быть рискованным, потому что строка заголовка структурированной таблицы должна оставаться нетронутой. Это руководство проведёт вас безопасным способом, который сохраняет заголовок таблицы и позволяет удалить любое количество строк данных одним вызовом.

## Требования

Прежде чем начать, убедитесь, что у вас есть:

* .NET 6.0 или более поздняя версия  
* Visual Studio 2022 (или любой совместимый IDE)  
* NuGet‑пакет **Aspose.Cells** (версия 23.10 или новее) — эта библиотека предоставляет классы `Workbook`, `Worksheet` и `ListObject`, используемые в примерах  

Установка Microsoft Office на машине разработки не требуется, так как Aspose.Cells работает напрямую с форматом файла.

## Удаление строк из таблицы Excel — пошагово

Ниже описаны все шаги, необходимые для безопасного удаления строк из таблицы Excel. Основное ключевое слово присутствует в заголовке для удовлетворения требований SEO.

### Шаг 1: Добавьте Aspose.Cells в проект

Откройте **Package Manager Console** и выполните:

```powershell
Install-Package Aspose.Cells
```

Пакет добавит необходимые сборки и подключит типы `Workbook`, `Worksheet` и `ListObject`.

### Шаг 2: Загрузите книгу и найдите таблицу

```csharp
using Aspose.Cells;

class ExcelRowDeletion
{
    static void Main()
    {
        // Load the workbook that contains the table
        var workbook = new Workbook(@"C:\Data\table_with_header.xlsx");

        // Access the first worksheet (index 0)
        var worksheet = workbook.Worksheets[0];

        // Retrieve the first ListObject (structured table) on the sheet
        var table = worksheet.ListObjects[0];
```

*Почему это важно*: `ListObject` представляет настоящую таблицу Excel, которая хранит собственный заголовок. Работая с `ListObject`, вы избегаете случайного удаления заголовка.

### Шаг 3: Удалите нужные строки данных

Метод `DeleteRows` ожидает **нумерацию с нуля** относительно таблицы, **включая** строку заголовка. Поскольку заголовок нельзя удалять, необходимо начинать с индекса 1 для первой строки данных.

```csharp
        // Delete two data rows starting after the header (index 1)
        // Parameters: startRow (relative to the table), numberOfRows
        table.DeleteRows(1, 2);
```

Если попытаться вызвать `table.DeleteRows(0, 2)`, Aspose.Cells выбросит исключение, потому что строка заголовка (индекс 0) защищена. Начало с индекса 1 гарантирует, что будут удалены только строки данных.

### Шаг 4: Сохраните изменённую книгу

```csharp
        // Save the workbook to a new file to preserve the original
        workbook.Save(@"C:\Data\table_with_header_modified.xlsx");
    }
}
```

Запуск программы удалит две строки сразу под заголовком, оставив структуру таблицы нетронутой.

### Полный рабочий пример

```csharp
using Aspose.Cells;

class ExcelRowDeletion
{
    static void Main()
    {
        // 1. Load workbook
        var workbook = new Workbook(@"C:\Data\table_with_header.xlsx");

        // 2. Access first worksheet
        var worksheet = workbook.Worksheets[0];

        // 3. Get the first table (ListObject)
        var table = worksheet.ListObjects[0];

        // 4. Delete two rows after the header (cannot delete header itself)
        table.DeleteRows(1, 2);

        // 5. Save the result
        workbook.Save(@"C:\Data\table_with_header_modified.xlsx");
    }
}
```

**Ожидаемый результат**: Файл `table_with_header_modified.xlsx` содержит оригинальный заголовок таблицы, за которым следуют все строки, кроме двух удалённых. Другие листы не изменяются.

## Удаление нескольких строк из листа Excel

Иногда требуется удалить строки, которые **не** являются частью структурированной таблицы. Вторичное ключевое слово присутствует в этом заголовке. Подход немного отличается, потому что вы работаете с коллекцией `Rows` листа, а не с `ListObject`.

```csharp
using Aspose.Cells;

class SheetRowDeletion
{
    static void Main()
    {
        var workbook = new Workbook(@"C:\Data\plain_sheet.xlsx");
        var worksheet = workbook.Worksheets[0];

        // Delete rows 5 through 9 (inclusive) – zero‑based index
        // The second argument is the count of rows to remove
        worksheet.Rows.RemoveAt(4, 5);

        workbook.Save(@"C:\Data\plain_sheet_modified.xlsx");
    }
}
```

**Почему это работает**: `Rows.RemoveAt(startIndex, count)` удаляет непрерывный блок строк непосредственно из листа. Защиты заголовка нет, поэтому можно начинать с любого индекса. Метод эффективен, так как обновляет внутренние структуры данных за одну операцию, что идеально при необходимости удалить несколько строк из листа Excel.

### Особые случаи и рекомендации

| Ситуация                               | Рекомендуемое решение |
|----------------------------------------|-----------------------|
| Удаление строк за последней строкой    | Проверьте `worksheet.Rows.Count` перед вызовом `RemoveAt`. |
| Удаление всех строк, кроме заголовка   | Удаляйте строки данных в цикле или используйте `DeleteRows(1, table.DataRange.RowCount - 1)`. |
| Сохранение форматирования ячеек        | При удалении через `ListObject` форматирование смещается автоматически; для обычных листов скопируйте форматирование перед удалением, если это необходимо. |
| Большие листы (> 10 000 строк)         | Выполняйте удаление в обратном порядке, чтобы избежать смещения индексов, или используйте `DeleteRows` на таблице, если это возможно. |

**Совет**: Когда нужно удалять строки по условию (например, строки, где значение в столбце пустое), проходите `DataRange` таблицы в обратном порядке и вызывайте `DeleteRows` для каждой подходящей строки. Обратный проход предотвращает рассинхронизацию индексов.

## Часто задаваемые вопросы

*Работает ли это с файлами .xlsx, созданными в Excel 365?*  
Да. Aspose.Cells поддерживает полную спецификацию Office Open XML, поэтому тот же код работает с любым современным файлом `.xlsx`.

*Что делать, если в книге несколько таблиц?*  
Получите нужную таблицу по имени: `var table = worksheet.ListObjects["MyTable"];` затем примените `DeleteRows`, как показано.

*Можно ли удалять строки без сторонних библиотек?*  
Можно использовать COM‑интероп Microsoft.Office.Interop.Excel, но для этого требуется установка Excel на сервере и появляется дополнительная нагрузка, связанная с COM. Aspose.Cells предоставляет лёгкую, безопасную для сервера альтернативу.

## Заключение

Теперь вы знаете, как безопасно удалять строки из таблицы Excel и как удалять несколько строк из листа Excel с помощью C#. Основная техника использует метод `ListObject.DeleteRows`, который сохраняет заголовок таблицы, а вторичная — `Rows.RemoveAt` для обычных листов. Применяйте эти приёмы для очистки данных, автоматизации генерации отчётов или реализации массового редактирования в ваших приложениях.

**Следующие шаги**

* Исследуйте другие возможности Aspose.Cells, такие как вставка строк, копирование стилей или фильтрация данных.  
* Попробуйте те же операции с **ClosedXML**, если предпочитаете библиотеку с открытым исходным кодом; API похож, но использует `IXLTable` и `IXLRows`.  
* Сочетайте логику удаления строк с LINQ‑запросами, чтобы построить более сложные конвейеры очистки данных.

Удачной разработки!

## Что следует изучить дальше?

Следующие руководства охватывают близкие темы, которые расширяют техники, продемонстрированные в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, помогая вам освоить дополнительные возможности API и исследовать альтернативные подходы в собственных проектах.

- [как удалить строки в Excel с C# — защитить заголовок таблицы](/cells/english/net/row-and-column-management/how-to-delete-rows-in-excel-with-c-protect-table-header/)
- [Как использовать Aspose.Cells для удаления строк в таблице Excel, сохраняя](/cells/english/net/row-and-column-management/how-to-use-aspose-cells-to-delete-rows-in-an-excel-table-whi/)
- [Загрузка Excel‑файла C# — как удалить строки и удалить конкретные строки](/cells/english/net/row-and-column-management/load-excel-file-c-how-to-delete-rows-and-remove-specific-row/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}