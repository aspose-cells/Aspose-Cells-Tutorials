---
category: general
date: 2026-10-07
description: Узнайте, как Aspose.Cells удаляет строки из таблицы Excel, удаляет все
  строки, кроме заголовка, и обрабатывает удаление строк из защищённой таблицы с помощью
  чистого кода C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- aspose cells delete rows
- delete rows excel table
- excel table row deletion
- protect excel table rows
- remove rows except header
language: ru
lastmod: 2026-10-07
og_description: Aspose.Cells удаляет строки из таблицы Excel, сохраняя заголовок.
  Это руководство показывает полное решение на C#, включая работу с защищёнными таблицами
  и типичными граничными случаями.
og_image_alt: Aspose.Cells delete rows example showing code and Excel screenshot
og_title: Aspose.Cells удаление строк – удалить все строки, кроме заголовка, в C#
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Learn how Aspose.Cells delete rows from an Excel table, remove rows
    except header, and handle protected table row deletion with clean C# code.
  headline: How to use Aspose.Cells to delete rows in an Excel table while keeping
    the header
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: Как использовать Aspose.Cells для удаления строк в таблице Excel, сохраняя
  заголовок
url: /ru/net/row-and-column-management/how-to-use-aspose-cells-to-delete-rows-in-an-excel-table-whi/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как использовать Aspose.Cells для удаления строк в таблице Excel, сохраняя заголовок

Если вам нужно **aspose cells delete rows** из таблицы, но сохранить строку заголовка, это руководство показывает полное, готовое к запуску решение. Вы увидите, почему прямой вызов `ListObject.DeleteRows` не работает, когда таблица защищена, и как обойти это ограничение без ущерба целостности данных.

В руководстве рассматривается:

* Загрузка книги, содержащей защищённую таблицу.  
* Определение и временное снятие защиты таблицы.  
* Удаление всех строк данных при сохранении заголовка.  
* Восстановление исходного состояния защиты.  

К концу статьи вы сможете надёжно выполнять операции **delete rows excel table** в любом проекте Aspose.Cells.

## Prerequisites

* .NET 6.0 или новее (код также работает с .NET Framework 4.7.2+).  
* Aspose.Cells for .NET 23.9 или новее.  
* Базовое знакомство с C# и таблицами Excel (известными как ListObjects).  

Дополнительные пакеты NuGet не требуются, кроме Aspose.Cells.

## Step 1: Set up the project and import namespaces

Создайте новое консольное приложение или добавьте следующий код в существующий проект. Импортируйте пространства имён Aspose.Cells, чтобы компилятор мог распознать `Workbook`, `Worksheet` и `ListObject`.

```csharp
using System;
using Aspose.Cells;

namespace AsposeCellsTableRowDeletion
{
    class Program
    {
        static void Main()
        {
            // The full solution starts in Step 2.
        }
    }
}
```

*Почему важен этот шаг* – Импорт правильных пространств имён предотвращает ошибки неоднозначных типов и делает остальной код более понятным.

## Step 2: Load the workbook and locate the target table

Замените `"YOUR_DIRECTORY/TableProtection.xlsx"` на путь к вашему файлу Excel. В примере предполагается, что таблица, которую вы хотите изменить, называется **Orders**.

```csharp
// Load the workbook that contains the protected table
Workbook workbook = new Workbook("YOUR_DIRECTORY/TableProtection.xlsx");

// Get the first worksheet (index 0) and the ListObject named "Orders"
Worksheet worksheet = workbook.Worksheets[0];
ListObject ordersTable = worksheet.ListObjects["Orders"];
```

*Почему важен этот шаг* – Доступ к `ListObject` даёт прямой доступ к таблице, что необходимо для любой операции **excel table row deletion**.

## Step 3: Check whether the table is protected

Aspose.Cells блокирует частичное удаление строк, когда таблица защищена. Попытка вызвать `ordersTable.DeleteRows` в этом состоянии приводит к исключению. Сначала определите статус защиты.

```csharp
bool wasProtected = ordersTable.IsProtected;
Console.WriteLine($"Table protection status: {(wasProtected ? "protected" : "unprotected")}");
```

*Почему важен этот шаг* – Знание состояния защиты позволяет решить, нужно ли временно снять защиту, обеспечивая соблюдение правила **protect excel table rows** после операции.

## Step 4: Temporarily unprotect the table (if needed)

Если таблица защищена, используйте `Unprotect` с паролем (если он есть). Для таблиц без пароля просто вызовите `Unprotect()`.

```csharp
if (wasProtected)
{
    // Provide the password if the table was protected with one; otherwise, pass null.
    ordersTable.Unprotect(null);
    Console.WriteLine("Table temporarily unprotected.");
}
```

*Почему важен этот шаг* – Снятие защиты позволяет Aspose.Cells выполнить **aspose cells delete rows** без исключения, при этом вы сможете позже восстановить защиту.

## Step 5: Delete all rows except the header

Заголовок занимает первую строку таблицы (`RowCount` включает заголовок). Удаление, начиная с индекса 1, удалит все строки данных.

```csharp
int dataRows = ordersTable.RowCount - 1; // Exclude the header row
if (dataRows > 0)
{
    ordersTable.DeleteRows(1, dataRows);
    Console.WriteLine($"{dataRows} data rows removed, header preserved.");
}
else
{
    Console.WriteLine("Table contains only the header; nothing to delete.");
}
```

*Почему важен этот шаг* – Этот код реализует основную функцию **remove rows except header**, избегая исключения, которое возникает при частичном удалении в защищённых таблицах.

## Step 6: Re‑apply protection (if it was originally set)

После удаления строк восстановите исходное состояние защиты, чтобы книга вела себя точно так же, как и раньше.

```csharp
if (wasProtected)
{
    // Re‑apply protection with the same password (null if none was used)
    ordersTable.Protect(null);
    Console.WriteLine("Table protection restored.");
}
```

*Почему важен этот шаг* – Восстановление защиты соблюдает требование **protect excel table rows** и сохраняет безопасность книги для последующих пользователей.

## Step 7: Save the modified workbook

Выберите новое имя файла, чтобы не перезаписать оригинал, если только перезапись не является намеренной.

```csharp
string outputPath = "YOUR_DIRECTORY/TableProtection_Modified.xlsx";
workbook.Save(outputPath);
Console.WriteLine($"Modified workbook saved to: {outputPath}");
```

*Почему важен этот шаг* – Сохранение завершает операцию **excel table row deletion** и предоставляет конкретный результат, который можно открыть в Excel для проверки.

## Full working example

Объединяя все шаги, получаем автономную программу, которую можно скопировать, вставить и запустить.

```csharp
using System;
using Aspose.Cells;

namespace AsposeCellsTableRowDeletion
{
    class Program
    {
        static void Main()
        {
            // 1. Load workbook
            Workbook workbook = new Workbook("YOUR_DIRECTORY/TableProtection.xlsx");
            Worksheet worksheet = workbook.Worksheets[0];
            ListObject ordersTable = worksheet.ListObjects["Orders"];

            // 2. Remember protection state
            bool wasProtected = ordersTable.IsProtected;
            Console.WriteLine($"Table protection status: {(wasProtected ? "protected" : "unprotected")}");

            // 3. Unprotect if needed
            if (wasProtected)
            {
                ordersTable.Unprotect(null); // use password if applicable
                Console.WriteLine("Table temporarily unprotected.");
            }

            // 4. Delete all rows except header
            int dataRows = ordersTable.RowCount - 1;
            if (dataRows > 0)
            {
                ordersTable.DeleteRows(1, dataRows);
                Console.WriteLine($"{dataRows} data rows removed, header preserved.");
            }
            else
            {
                Console.WriteLine("Table contains only the header; nothing to delete.");
            }

            // 5. Restore protection
            if (wasProtected)
            {
                ordersTable.Protect(null); // re‑apply with original password if any
                Console.WriteLine("Table protection restored.");
            }

            // 6. Save the workbook
            string outputPath = "YOUR_DIRECTORY/TableProtection_Modified.xlsx";
            workbook.Save(outputPath);
            Console.WriteLine($"Modified workbook saved to: {outputPath}");
        }
    }
}
```

### Expected output

```
Table protection status: protected
Table temporarily unprotected.
5 data rows removed, header preserved.
Table protection restored.
Modified workbook saved to: YOUR_DIRECTORY/TableProtection_Modified.xlsx
```

Откройте `TableProtection_Modified.xlsx` в Excel. Вы увидите таблицу **Orders** только с заголовочной строкой; все строки данных будут удалены.

## Handling common variations and edge cases

| Situation | Recommended tweak | Reason |
|-----------|-------------------|--------|
| Table uses a password | Pass the password to `Unprotect` and `Protect` | Guarantees the same security level after the operation |
| Table has no data rows | Skip the `DeleteRows` call | Prevents an `ArgumentOutOfRangeException` |
| Multiple tables need cleaning | Loop through `worksheet.ListObjects` and apply the same logic | Scales the **delete rows excel table** pattern to the whole sheet |
| You want to keep the header and the first data row | Change `DeleteRows(2, dataRows‑1)` | Starts deletion after the second row, preserving the first data row |

These variations demonstrate robust **excel table row deletion** handling and reinforce why the presented approach is the recommended one.

## Pro tips

* **Batch processing** – If you need to delete rows from many workbooks, encapsulate the logic in a reusable method that accepts `Workbook` and `tableName` parameters.
* **Performance** – Deleting rows in a single call (`DeleteRows`) is faster than removing rows one by one because Aspose.Cells updates the internal data structures only once.
* **Safety** – Always work on a copy of the original file or keep a backup before applying deletions, especially when **protect excel table rows** is involved.

## Conclusion

You now have a complete, production‑ready solution for **aspose cells delete rows** while preserving the header of an Excel table. The guide covered loading the workbook, handling protected tables, performing the **remove rows except header** operation, and restoring protection. Apply the same pattern to any **excel table row deletion** scenario, and adapt the code to suit additional requirements such as password‑protected tables or batch processing.

---

*Next steps* – Explore related topics such as **delete rows excel table** with filters, merging cells after row removal, or using Aspose.Cells to copy tables between workbooks. Each of these builds on the core concepts demonstrated here and deepens your mastery of Excel automation with Aspose.Cells.

## What Should You Learn Next?

The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step‑by‑step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Aspose Cells Delete Rows – Protect Header Row in Excel](/cells/english/net/row-and-column-management/aspose-cells-delete-rows-protect-header-row-in-excel/)
- [How to Insert and Delete Rows in Excel with Aspose.Cells for .NET: A Comprehensive Guide](/cells/english/net/data-manipulation/aspose-cells-net-insert-delete-excel-rows/)
- [How to Delete Blank Rows in Excel Using Aspose.Cells .NET for Data Cleanup](/cells/english/net/data-manipulation/delete-blank-rows-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}