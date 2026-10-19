---
category: general
date: 2026-10-10
description: Узнайте, как удалить целую строку в книге Excel с помощью C#. В этом
  пошаговом руководстве также рассматривается удаление строки по индексу и её удаление
  с использованием Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- delete entire row
- how to delete row
- remove row by index
- delete row excel
- delete row c#
language: ru
lastmod: 2026-10-10
og_description: Удалите всю строку в рабочей книге Excel с помощью C#. Следуйте этому
  руководству, чтобы узнать, как удалить строку по индексу, как удалить строку по
  индексу и как безопасно сохранить файл.
og_image_alt: Screenshot of an Excel worksheet before and after deleting an entire
  row with C# code
og_title: Удаление целой строки в Excel с помощью C# – полное руководство по программированию
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Learn how to delete entire row in an Excel workbook with C#. This step‑by‑step
    guide also covers how to delete row by index and remove row by index using Aspose.Cells.
  headline: How to delete entire row in an Excel file using C#
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
title: Как удалить целую строку в файле Excel с помощью C#
url: /ru/net/row-and-column-management/how-to-delete-entire-row-in-an-excel-file-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Удалить всю строку в файле Excel с помощью C#

Если вам нужно **удалить всю строку** в рабочей книге Excel, это руководство покажет, как сделать это с помощью C#. Независимо от того, очищаете ли вы импортированные данные или создаёте инструмент отчётности, нижеописанные шаги позволяют удалить строку по её индексу и сохранить результат без потери остальных данных.

Вы также увидите, как тот же подход отвечает на вопросы **how to delete row** по индексу, **remove row by index**, и почему он работает для сценариев **delete row excel** в C#.

## Prerequisites

Перед началом убедитесь, что у вас есть:

* .NET 6.0 или новее (код также работает с .NET Framework 4.6+)  
* Библиотека **Aspose.Cells for .NET** (доступна через NuGet: `Install-Package Aspose.Cells`)  
* Базовые знания C#‑консольных или десктопных проектов  

Никакие дополнительные компоненты Excel Interop или COM не требуются, что делает решение лёгким и безопасным для серверного выполнения.

## Step 1: Set up the project and import namespaces

Создайте новое консольное приложение (или добавьте код в существующий проект) и добавьте необходимые директивы `using`:

```csharp
using System;
using Aspose.Cells;

namespace ExcelRowDeletion
{
    class Program
    {
        static void Main(string[] args)
        {
            // The rest of the tutorial code lives here.
        }
    }
}
```

*Почему это важно*: Импорт `Aspose.Cells` даёт доступ к `Workbook`, `Worksheet` и методу `DeleteRows`, который выполняет фактическое удаление строки.

## Step 2: Load the workbook and select the worksheet

Необходимо загрузить исходный файл (`input.xlsx`) и получить лист, который вы хотите изменить. Первый лист доступен по индексу `0`.

```csharp
// Load the workbook from disk
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

// Get the first worksheet (you can also use workbook.Worksheets["SheetName"])
Worksheet ws = workbook.Worksheets[0];
```

> **Подсказка**: Если нужно работать с конкретным листом, замените индекс именем листа: `workbook.Worksheets["Data"]`.

## Step 3: Delete the entire row by its zero‑based index

Aspose.Cells использует нулевую базу индексации, поэтому первая строка имеет индекс `0`. Чтобы удалить строку 5 (шестую визуальную строку), вызовите `DeleteRows` с параметром `DeleteOptions.DeleteEntireRow`.

```csharp
// Delete one row starting at index 5 (zero‑based) and remove the whole row
ws.Cells[5, 0].DeleteRows(1, DeleteOptions.DeleteEntireRow);
```

*Объяснение*:

* `ws.Cells[5, 0]` указывает на первую ячейку строки, которую нужно удалить.  
* `DeleteRows(1, DeleteOptions.DeleteEntireRow)` сообщает Aspose.Cells удалить **1** строку, а флаг `DeleteEntireRow` гарантирует, что **вся строка** исчезнет, сдвигая нижележащие строки вверх.

### How to delete row by index in other scenarios

* **Delete multiple consecutive rows** – измените первый аргумент на количество строк, которые нужно стереть:

  ```csharp
  // Remove rows 5, 6 and 7 (three rows total)
  ws.Cells[5, 0].DeleteRows(3, DeleteOptions.DeleteEntireRow);
  ```

* **Delete the last row** – используйте `ws.Cells.MaxDataRow`, чтобы получить индекс самой нижней заполненной строки:

  ```csharp
  int lastRow = ws.Cells.MaxDataRow;
  ws.Cells[lastRow, 0].DeleteRows(1, DeleteOptions.DeleteEntireRow);
  ```

Эти фрагменты отвечают требованиям **remove row by index**, оставаясь при этом легко читаемыми.

## Step 4: Save the workbook with the row removed

После удаления запишите изменённую рабочую книгу обратно на диск. Можно перезаписать оригинальный файл или создать новый.

```csharp
// Save the workbook to a new file (or overwrite the original)
workbook.Save("YOUR_DIRECTORY/output.xlsx");
```

Если нужно оставить оригинальный файл без изменений, просто измените путь вывода. Метод `Save` поддерживает множество форматов (`.xls`, `.csv`, `.pdf` и т.д.) – достаточно изменить расширение файла.

## Full working example

Объединив всё вместе, получаем полностью готовую к запуску программу:

```csharp
using System;
using Aspose.Cells;

namespace ExcelRowDeletion
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the workbook
            Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

            // 2️⃣ Select the first worksheet
            Worksheet ws = workbook.Worksheets[0];

            // 3️⃣ Delete the entire row at index 5 (sixth visual row)
            ws.Cells[5, 0].DeleteRows(1, DeleteOptions.DeleteEntireRow);

            // 4️⃣ Save the result
            workbook.Save("YOUR_DIRECTORY/output.xlsx");

            Console.WriteLine("Row deleted successfully. Output saved to output.xlsx");
        }
    }
}
```

**Ожидаемый результат**: После выполнения программы файл `output.xlsx` будет содержать все исходные строки, кроме той, которая находилась на визуальной строке 6. Все данные ниже удалённой строки автоматически сдвинутся вверх, сохранив формулы и форматирование.

## Common pitfalls and how to avoid them

| Issue | Why it happens | Fix |
|-------|----------------|-----|
| **Index out of range** | Попытка удалить строку с индексом, которого нет (например, `ws.Cells[1000,0]` в листе из 200 строк) | Используйте `ws.Cells.MaxDataRow`, чтобы проверить максимальный допустимый индекс перед вызовом `DeleteRows`. |
| **Partial row deletion** | Пропуск `DeleteOptions.DeleteEntireRow` приводит к очистке только содержимого ячеек | Всегда передавайте `DeleteOptions.DeleteEntireRow`, когда требуется удалить всю строку. |
| **Unexpected formula changes** | Удаление строк, входящих в диапазон формулы, может нарушить ссылки | Пересчитайте формулы после удаления (`workbook.CalculateFormula()`), если ваша книга использует динамические диапазоны. |
| **Saving to a read‑only location** | Вызов `Save` бросает исключение, если папка защищена | Убедитесь, что целевая директория доступна для записи, либо запустите программу с необходимыми правами. |

Учёт этих моментов делает решение надёжным для продакшн‑использования и удовлетворяет запросы **delete row excel** и **delete row c#**.

## Advanced: Deleting rows based on a condition

Иногда требуется удалить строки, соответствующие определённому условию (например, строки, где столбец A пуст). Ниже показан безопасный способ пройтись снизу вверх и удалить подходящие строки:

```csharp
int lastRow = ws.Cells.MaxDataRow;
for (int row = lastRow; row >= 0; row--)
{
    // Check if column A (index 0) is empty
    if (ws.Cells[row, 0].StringValue == string.Empty)
    {
        ws.Cells[row, 0].DeleteRows(1, DeleteOptions.DeleteEntireRow);
    }
}
workbook.Save("YOUR_DIRECTORY/cleaned.xlsx");
```

Обход снизу вверх предотвращает проблему смещения индексов, возникающую при удалении строк во время прямой итерации.

## Conclusion

Теперь вы знаете, как **удалить всю строку** в рабочей книге Excel с помощью C#. Руководство охватывало:

* Загрузка рабочей книги и выбор листа  
* Использование `DeleteRows` с `DeleteOptions.DeleteEntireRow` для **how to delete row** по индексу  
* Безопасное сохранение изменённого файла  
* Обработку крайних случаев, советы по производительности и пример условного удаления  

Благодаря этим знаниям вы сможете уверенно реализовать функциональность **remove row by index**, автоматизировать очистку данных и интегрировать работу с Excel в любые C#‑приложения.  

**Следующие шаги**: изучите другие возможности Aspose.Cells, такие как вставка строк, копирование диапазонов или конвертация книги в PDF — все они базируются на тех же объектах `Workbook` и `Worksheet`, которые вы только что освоили. Приятного кодинга!

## What Should You Learn Next?

The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Delete an Excel Row Using Aspose.Cells .NET&#58; A Comprehensive Guide](/cells/english/net/worksheet-management/delete-excel-row-aspose-cells-net-tutorial/)
- [Aspose Cells Delete Rows – Protect Header Row in Excel](/cells/english/net/row-and-column-management/aspose-cells-delete-rows-protect-header-row-in-excel/)
- [Efficient Row Management in Excel using Aspose.Cells for Java&#58; Insert and Delete Rows](/cells/english/java/worksheet-management/aspose-cells-java-row-operations-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}