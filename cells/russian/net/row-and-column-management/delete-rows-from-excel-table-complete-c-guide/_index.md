---
category: general
date: 2026-08-07
description: Удаление строк из таблицы Excel с помощью C#. Узнайте, как безопасно
  удалять строки данных в Excel, защищая при этом строку заголовка, всего за несколько
  шагов.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- delete rows from excel table
- remove data rows excel
- protect header row excel
language: ru
lastmod: 2026-08-07
og_description: Удаление строк из таблицы Excel программным способом. Это руководство
  показывает, как безопасно удалять строки данных в Excel и защищать строку заголовка
  в Excel с помощью Aspose.Cells.
og_image_alt: Screenshot of C# code that deletes rows from an Excel table while keeping
  the header intact
og_title: Удалить строки из таблицы Excel – быстрое решение на C#
schemas:
- author: Aspose
  dateModified: '2026-08-07'
  description: Delete rows from Excel table using C#. Learn how to remove data rows
    Excel safely while protecting header row Excel in just a few steps.
  headline: Delete rows from Excel table – complete C# guide
  type: TechArticle
- description: Delete rows from Excel table using C#. Learn how to remove data rows
    Excel safely while protecting header row Excel in just a few steps.
  name: Delete rows from Excel table – complete C# guide
  steps:
  - name: Run the program with a sample workbook that has at least five data rows.
    text: Run the program with a sample workbook that has at least five data rows.
  - name: Verify that the console prints “Rows deleted and workbook saved successfully.”
    text: Verify that the console prints “Rows deleted and workbook saved successfully.”
  - name: 'Open `TableHeaderProtected.xlsx` in Excel and confirm:'
    text: 'Open `TableHeaderProtected.xlsx` in Excel and confirm:'
  type: HowTo
tags:
- Excel
- C#
- Aspose.Cells
- Data manipulation
title: Удаление строк из таблицы Excel — полное руководство по C#
url: /ru/net/row-and-column-management/delete-rows-from-excel-table-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Удаление строк из таблицы Excel – полное руководство по C#

Если вам нужно **удалить строки из таблицы Excel** в проекте .NET, это руководство покажет надёжный способ сделать это. Независимо от того, очищаете ли вы импортированные данные или сокращаете отчёт, вы увидите, как удалить строки данных в Excel, при этом API автоматически **protect header row excel** от случайного удаления.

В следующих шагах вы узнаете, как загрузить книгу, безопасно удалить строки и в конце сохранить изменения. Руководство также охватывает распространённую ошибку попытки удалить строку заголовка и объясняет, почему библиотека это предотвращает. К концу вы сможете уверенно **remove data rows excel** в любом решении на основе Aspose.Cells.

## Предварительные требования

- .NET 6.0 или более поздняя версия установлен(а).
- Пакет NuGet **Aspose.Cells for .NET** (версия 23.10 или новее). Установите его с помощью:

  ```bash
  dotnet add package Aspose.Cells
  ```

- Файл Excel (`TableWithHeader.xlsx`), содержащий структурированную таблицу с строкой заголовка на первом листе.
- Базовые знания C# и Visual Studio (или любой другой предпочитаемой IDE).

## Шаг 1: Загрузка книги, содержащей таблицу со строкой заголовка

Первая операция – открыть книгу, в которой находится таблица, которую вы хотите изменить. Aspose.Cells читает файл в память без необходимости установки Excel.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // Load the workbook from disk
        Workbook workbook = new Workbook(@"YOUR_DIRECTORY\TableWithHeader.xlsx");

        // Continue with the next steps...
```

**Почему это важно:** Загрузка книги создаёт объект `Workbook`, который даёт доступ к листам, таблицам и ячейкам. Без этого объекта вы не сможете манипулировать структурой Excel.

## Шаг 2: Доступ к первому листу и его первой таблице

Большинство простых примеров хранит таблицу на первом листе и с индексом 0, но вы можете изменить индексы под свою ситуацию.

```csharp
        // Access the first worksheet (index 0)
        Worksheet worksheet = workbook.Worksheets[0];

        // Retrieve the first ListObject (Excel table) on that worksheet
        ListObject table = worksheet.Tables[0];
```

**Почему это важно:** `ListObject` представляет таблицу Excel, включающую строку заголовка, строки данных и любое форматирование. Работа с объектом таблицы гарантирует соблюдение семантики таблиц Excel, например защиту строки заголовка.

## Шаг 3: Попытка удалить строку заголовка (демонстрация защиты)

Aspose.Cells бросает исключение, если вы пытаетесь удалить строку заголовка, потому что API **protect header row excel** по‑умолчанию. Демонстрация этого поведения помогает понять, почему прямая попытка удаления не удаётся.

```csharp
        try
        {
            // Attempt to delete the header row (index 0) and the row below it
            table.DeleteRows(0, 2);
        }
        catch (Exception ex)
        {
            Console.WriteLine("Deletion prevented: " + ex.Message);
        }
```

**Ожидаемый вывод**

```
Deletion prevented: Cannot delete the header row of a table.
```

**Объяснение:** Метод `DeleteRows` принимает нулевой стартовый индекс и количество строк. Индекс 0 указывает на строку заголовка, которую библиотека защищает, чтобы сохранить структуру таблицы.

## Шаг 4: Удаление только строк данных – правильный способ **remove data rows excel**

Теперь, когда вы знаете, что заголовок защищён, удаляйте только строки данных, начинающиеся после заголовка. В большинстве таблиц первая строка данных имеет индекс 1.

```csharp
        // Delete three data rows starting after the header (index 1)
        table.DeleteRows(1, 3); // removes rows 2, 3, and 4 of the worksheet

        // Optionally, you can delete a single row:
        // table.DeleteRows(4, 1);
```

**Почему это работает:** Начав с индекса 1, вы пропускаете заголовок, поэтому операция соответствует правилу **protect header row excel**. Метод `DeleteRows` автоматически обновляет внутренний диапазон таблицы.

## Шаг 5: Сохранение изменённой книги

Сохраните изменения в новый файл, чтобы оригинал остался нетронутым.

```csharp
        // Save the workbook with the modified table
        workbook.Save(@"YOUR_DIRECTORY\TableHeaderProtected.xlsx");

        Console.WriteLine("Rows deleted and workbook saved successfully.");
    }
}
```

**Результат:** После выполнения программы `TableHeaderProtected.xlsx` содержит ту же строку заголовка, но указанные строки данных удалены. Открытие файла в Excel показывает чистую таблицу без удалённых строк.

## Распространённые подводные камни и как их избежать

| Проблема | Почему происходит | Как исправить |
|----------|-------------------|---------------|
| Попытка удалить строку заголовка | Aspose.Cells обеспечивает целостность таблицы | Всегда начинайте удаление с индекса 1 или выше |
| Удаление большего количества строк, чем существует | `DeleteRows` бросает `ArgumentOutOfRangeException` | Проверьте `table.DataRange.RowCount` перед вызовом `DeleteRows` |
| Работа с диапазоном, не являющимся таблицей | Методы `ListObject` применимы только к структурированным таблицам | Сначала преобразуйте диапазон в таблицу (`worksheet.Tables.Add`), если необходимо |

**Pro tip:** Если нужно очистить всю таблицу, но сохранить заголовок, используйте `table.DeleteRows(1, table.DataRange.RowCount - 1);`. Это удалит каждую строку данных независимо от текущего количества строк в таблице.

## Альтернатива: Удаление строк по адресу ячейки

Иногда вы можете знать точный адрес ячейки вместо индекса строки. Вы можете преобразовать адрес в индекс строки с помощью коллекции `Cells`:

```csharp
        // Example: delete rows that contain the value "Obsolete"
        for (int i = table.DataRange.FirstRow; i <= table.DataRange.LastRow; i++)
        {
            if (worksheet.Cells[i, table.DataRange.FirstColumn].StringValue == "Obsolete")
            {
                // Subtract one because DeleteRows expects a zero‑based index relative to the table
                table.DeleteRows(i - table.StartRow + 1, 1);
                i--; // Adjust loop counter after deletion
            }
        }
```

Этот подход полезен, когда строки для удаления определяются содержимым, а не фиксированным количеством.

## Тестирование вашей реализации

1. Запустите программу с примерной книгой, содержащей как минимум пять строк данных.  
2. Убедитесь, что консоль выводит «Rows deleted and workbook saved successfully».  
3. Откройте `TableHeaderProtected.xlsx` в Excel и проверьте:
   - Строка заголовка всё ещё присутствует.
   - Отсутствуют только те строки данных, которые должны быть удалены.

Если заголовок исчез, вы, вероятно, начали удаление с индекса 0 — проверьте **Шаг 4**.

## Заключение

Теперь вы знаете, как безопасно **удалять строки из таблицы Excel** с помощью C#. Руководство охватило загрузку книги, доступ к таблице, соблюдение правила **protect header row excel**, правильное **remove data rows excel** и сохранение результата. Следуя этим шагам, вы избегаете распространённых ошибок и поддерживаете таблицы Excel в хорошем состоянии.

### Следующие шаги

- Изучите возможности **Aspose.Cells**, такие как вставка строк, применение стилей или фильтрация данных.  
- Сочетайте удаление строк с **формулами Excel** для автоматической очистки на основе результатов вычислений.  
- Ознакомьтесь с сопутствующими темами, такими как **экспорт Excel в CSV** или **эффективное чтение больших книг**.

Не стесняйтесь экспериментировать с разным количеством строк, несколькими таблицами или условными удалениями. Если возникнут крайние случаи, обратитесь к обработке ошибок, показанной в **Шаг 3** — библиотека всегда будет защищать строку заголовка для вас. Приятного кодинга!

## Что следует изучить дальше?

Следующие руководства охватывают тесно связанные темы, которые развивают техники, продемонстрированные в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в собственных проектах.

- [Delete Multiple Rows in Excel with Aspose.Cells .NET: A Comprehensive Guide for Data Manipulation](/cells/english/net/data-manipulation/delete-rows-excel-aspose-cells-net/)
- [How to Insert and Delete Rows in Excel with Aspose.Cells for .NET: A Comprehensive Guide](/cells/english/net/data-manipulation/aspose-cells-net-insert-delete-excel-rows/)
- [How to Delete Blank Rows in Excel Using Aspose.Cells .NET for Data Cleanup](/cells/english/net/data-manipulation/delete-blank-rows-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}