---
category: general
date: 2026-03-22
description: Aspose Cells удаляет строки, защищая строку заголовка. Узнайте, как получить
  первую таблицу и безопасно удалить строки таблицы Excel в C#.
draft: false
keywords:
- aspose cells delete rows
- protect header row
- delete excel table rows
- retrieve first table
language: ru
og_description: Aspose Cells удаляет строки, сохраняя строку заголовка. Узнайте, как
  получить первую таблицу и безопасно удалить строки таблицы Excel на C#.
og_title: Aspose Cells Удаление строк — Защита строки заголовка в Excel
tags:
- Aspose.Cells
- C#
- Excel automation
title: 'Aspose Cells: удаление строк – защита строки заголовка в Excel'
url: /ru/net/row-and-column-management/aspose-cells-delete-rows-protect-header-row-in-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose Cells Delete Rows – Защита заголовка строки в Excel

Когда‑либо пытались **aspose cells delete rows** из таблицы и обнаружили, что заголовок исчез? Это распространённая ошибка при программном управлении листами Excel. В этом руководстве мы пройдём полный, готовый к запуску пример, который **protects the header row**, показывает, как **retrieve first table**, и безопасно **delete Excel table rows** без нарушения структуры.

Мы рассмотрим всё: от загрузки рабочей книги до обработки исключения, которое бросает Aspose, когда вы пытаетесь оставить заголовок без таблицы. К концу вы получите надёжный шаблон, который можно вставить в любой .NET‑проект, использующий Aspose.Cells.

---

## Что понадобится

- **Aspose.Cells for .NET** (v23.12 или новее) – библиотека, позволяющая работать с файлами Excel без установленного Office.  
- Базовая среда разработки C# (Visual Studio, Rider или `dotnet` CLI).  
- Файл Excel (`TableWithHeader.xlsx`), содержащий как минимум один **ListObject** (таблица Excel) с заголовком в первой строке.

Дополнительные пакеты NuGet не требуются, кроме Aspose.Cells.

---

## Шаг 1: Загрузка рабочей книги и получение первой таблицы  

Первое, что нужно сделать, – открыть рабочую книгу и получить таблицу, которую планируется изменить. Именно здесь вступает в силу вторичное ключевое слово **retrieve first table**.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Load the workbook that contains a table with a header row
        Workbook workbook = new Workbook(@"YOUR_DIRECTORY\TableWithHeader.xlsx");

        // Access the first worksheet in the workbook
        Worksheet worksheet = workbook.Worksheets[0];

        // Retrieve the first table (ListObject) on the worksheet
        ListObject table = worksheet.ListObjects[0];

        // Continue with row deletion...
        DeleteRowsSafely(table);
    }
}
```

**Почему это важно:**  
- `Workbook` читает файл без необходимости установки Excel.  
- `worksheet.ListObjects[0]` – самый простой способ **retrieve first table**; если таблиц несколько, можно итерировать их или использовать имя таблицы.

> **Pro tip:** Если вы не уверены, содержит ли лист таблицу, сначала проверьте `worksheet.ListObjects.Count`, чтобы избежать `IndexOutOfRangeException`.

---

## Шаг 2: Защита строки заголовка при удалении строк  

Теперь к главному: **aspose cells delete rows** без удаления заголовка. Метод `DeleteRows` в Aspose принимает нулевой индекс начала и количество строк. Попытка удалить заголовок (строка 0) вызывает исключение, чего мы хотим избежать.

```csharp
static void DeleteRowsSafely(ListObject table)
{
    try
    {
        // Attempt to delete rows 2‑3 (the header is row 1 in Excel, index 0 in code)
        // Here we start at index 1 (second row) and delete 2 rows.
        table.DeleteRows(1, 2);
        Console.WriteLine("Rows deleted successfully.");
    }
    catch (Exception ex)
    {
        // The API throws an exception because the header would be removed
        Console.WriteLine("Operation blocked: " + ex.Message);
    }

    // Save the workbook to verify the result
    table.Worksheet.Workbook.Save(@"YOUR_DIRECTORY\Result.xlsx");
}
```

**Объяснение логики:**  

| Шаг | Причина |
|------|--------|
| `table.DeleteRows(1, 2);` | Индекс 1 указывает на **вторую** строку (первую строку данных). Удаление двух строк убирает строки 2‑3 в терминах Excel, оставляя заголовок (строка 1) нетронутым. |
| `catch (Exception ex)` | Aspose бросает исключение **только** когда операция оставит заголовок без таблицы. Перехват позволяет записать дружелюбное сообщение вместо падения приложения. |
| `Save` | Сохранение изменений позволяет открыть `Result.xlsx` и увидеть, что заголовок всё ещё присутствует. |

> **Что если действительно нужно удалить заголовок?**  
> Используйте `table.ShowHeaders = false;` перед удалением, либо удалите всю таблицу и создайте её заново. Но в большинстве бизнес‑сценариев вы захотите **protect header row**.

---

## Шаг 3: Проверка результата – ожидаемый вывод  

После выполнения программы откройте `Result.xlsx`. Вы должны увидеть:

- Первая строка всё ещё содержит оригинальные названия столбцов.  
- Строки 2‑3 (те, которые мы удаляли) исчезли, а оставшиеся данные сдвинулись вверх.  

Консоль выведет:

```
Rows deleted successfully.
```

Если вы по ошибке попытались удалить заголовок (например, `table.DeleteRows(0, 1);`), вывод будет:

```
Operation blocked: Cannot delete header row of the table.
```

Это сообщение подтверждает, что встроенный механизм защиты Aspose работает корректно.

---

## Шаг 4: Альтернативные способы **Delete Excel Table Rows**  

Иногда требуется более гибкое управление — удалять строки по условию или удалять разрозненные строки. Ниже два быстрых шаблона, сохраняющих заголовок в безопасности.

### 4.1 Удаление строк по фильтру данных  

```csharp
static void DeleteRowsByCondition(ListObject table, string columnName, string valueToRemove)
{
    // Find the column index by name
    int colIndex = table.ListColumns[columnName].Index;

    // Iterate backwards to avoid messing up row indices
    for (int i = table.DataRange.RowCount - 1; i >= 0; i--)
    {
        var cell = table.DataRange[i, colIndex];
        if (cell.StringValue.Equals(valueToRemove, StringComparison.OrdinalIgnoreCase))
        {
            // Delete the row (add 1 because DataRange is zero‑based inside the table)
            table.DeleteRows(i + 1, 1);
        }
    }
}
```

### 4.2 Массовое удаление с использованием диапазона  

```csharp
// Delete rows 5‑10 (still preserving the header)
table.DeleteRows(4, 6);   // 4 = 5th row in Excel, 6 = number of rows to delete
```

Оба фрагмента соблюдают правило **protect header row**, поскольку начальный индекс никогда не опускается ниже 1.

---

## Шаг 5: Распространённые ошибки и как их избежать  

| Ошибка | Почему происходит | Как исправить |
|---------|-------------------|---------------|
| Случайное удаление заголовка | Используется `0` в качестве начального индекса | Всегда начинайте с `1` для строк данных или предварительно проверьте `table.ShowHeaders`. |
| `IndexOutOfRangeException`, когда на листе нет таблиц | Предполагается наличие таблицы | Проверяйте `worksheet.ListObjects.Count > 0` перед обращением к `[0]`. |
| Изменения не сохраняются | Забыт вызов `Save` | Вызывайте `workbook.Save` после всех модификаций. |
| При удалении строк в середине индексы смещаются, что приводит к пропуску | Итерация вперёд во время удаления | Итерируйте **обратно** или сначала собирайте строки для удаления. |

---

## Шаг 6: Соберите всё вместе – полностью рабочий пример  

```csharp
using System;
using Aspose.Cells;

class AsposeDeleteRowsDemo
{
    static void Main()
    {
        // 1️⃣ Load workbook
        Workbook workbook = new Workbook(@"YOUR_DIRECTORY\TableWithHeader.xlsx");
        Worksheet sheet = workbook.Worksheets[0];

        // 2️⃣ Ensure a table exists
        if (sheet.ListObjects.Count == 0)
        {
            Console.WriteLine("No tables found on the first worksheet.");
            return;
        }

        // 3️⃣ Retrieve the first table (retrieve first table)
        ListObject table = sheet.ListObjects[0];

        // 4️⃣ Delete rows safely (aspose cells delete rows while protecting header row)
        DeleteRowsSafely(table);

        // 5️⃣ (Optional) Delete rows by condition
        // DeleteRowsByCondition(table, "Status", "Closed");

        // 6️⃣ Save the result
        workbook.Save(@"YOUR_DIRECTORY\Result.xlsx");
        Console.WriteLine("Workbook saved as Result.xlsx");
    }

    static void DeleteRowsSafely(ListObject table)
    {
        try
        {
            // Delete rows 2‑3 (header stays intact)
            table.DeleteRows(1, 2);
            Console.WriteLine("Rows deleted successfully.");
        }
        catch (Exception ex)
        {
            Console.WriteLine("Operation blocked: " + ex.Message);
        }
    }

    // Uncomment if you need conditional deletion
    /*
    static void DeleteRowsByCondition(ListObject table, string columnName, string valueToRemove)
    {
        int colIdx = table.ListColumns[columnName].Index;
        for (int i = table.DataRange.RowCount - 1; i >= 0; i--)
        {
            var cell = table.DataRange[i, colIdx];
            if (cell.StringValue.Equals(valueToRemove, StringComparison.OrdinalIgnoreCase))
            {
                table.DeleteRows(i + 1, 1);
            }
        }
    }
    */
}
```

Запустите эту программу, откройте `Result.xlsx`, и вы увидите, что заголовок остаётся нетронутым, а выбранные строки удалены. Это **полное, автономное решение** для **aspose cells delete rows** без потери заголовка.

---

## Заключение  

Мы продемонстрировали, как **aspose cells delete rows** при **protecting the header row**, как **retrieve first table**, и несколько способов безопасного **delete excel table rows**. Ключевые выводы:

- Всегда начинайте удаление с индекса 1, чтобы сохранить заголовок.  
- Используйте `try/catch` для обработки встроенного исключения защиты Aspose.  
- Проверяйте наличие таблицы перед операциями и итерируйте назад при условном удалении строк.

Готовы к следующему уровню? Попробуйте сочетать этот подход с API стилизации Aspose Cells, чтобы подсвечивать удаляемые строки перед их удалением, или автоматизировать процесс на нескольких листах. Возможности безграничны, а теперь у вас есть надёжный шаблон для дальнейшего развития.

Если этот урок оказался полезным, поставьте лайк, поделитесь им с коллегами или оставьте комментарий с вашими решениями сложных кейсов. Приятного кодинга!  

---

![Пример Aspose Cells Delete Rows – Защищённый заголовок строки](https://example.com/images/aspose-delete-rows.png "aspose cells delete rows")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}