---
category: general
date: 2026-07-13
description: Сдвигайте ячейки вверх в Excel с помощью C#. Узнайте, как удалить первые
  строки, удалить несколько строк и удалить строки из таблицы в одной безопасной операции.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- shift cells up
- remove first rows
- remove rows from table
- delete multiple rows
- how to delete rows
language: ru
lastmod: 2026-07-13
og_description: Сдвиньте ячейки вверх в листе Excel с помощью C#. Этот учебник показывает,
  как удалить первые строки, удалить несколько строк и безопасно удалить строки из
  таблицы.
og_image_alt: Screenshot of C# code that shifts cells up after deleting rows in an
  Excel worksheet
og_title: Сдвиг ячеек вверх в Excel с помощью C# – Полное пошаговое руководство
schemas:
- author: Aspose
  dateModified: '2026-07-13'
  description: Shift cells up in Excel using C#. Learn how to remove first rows, delete
    multiple rows, and remove rows from table in a single, safe operation.
  headline: Shift Cells Up in Excel with C# – Complete Guide
  type: TechArticle
- questions:
  - answer: Absolutely. Loop through `sheet.Cells.Rows` and call `DeleteRows(rowIndex,
      1, true)` whenever the condition matches. Just remember to iterate backwards
      to avoid index shifting.
    question: Can I delete rows based on a condition instead of a fixed index?
  - answer: Yes. Aspose.Cells supports both `.xlsx` and legacy `.xls` formats. The
      same API applies.
    question: Does this work with `.xls` files?
  - answer: 'Target the specific table by name: `Table myTable = sheet.Tables["MyTable"];`
      then use `myTable.Range.StartRow` to calculate the rows to delete. --- ## Full
      Working Example Below is the complete, ready‑to‑run program that incorporates
      everything we discussed. Copy‑paste it into a console app, adjust'
    question: What if my workbook contains multiple tables and I only want to affect
      one?
  type: FAQPage
tags:
- Aspose.Cells
- C#
- Excel automation
title: Сдвиг ячеек вверх в Excel с помощью C# – Полное руководство
url: /ru/net/row-and-column-management/shift-cells-up-in-excel-with-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Сдвиг ячеек вверх в Excel с помощью C# – Полное руководство

Когда‑нибудь задумывались, как **сдвинуть ячейки вверх** после удаления строк в файле Excel? Вы не одиноки. Будь то очистка импортированных данных или сокращение огромного отчёта, умение удалять первые строки без нарушения таблицы — обязательный навык для любого разработчика C#.

В этом руководстве мы пошагово рассмотрим практическое решение от начала до конца, которое показывает **как удалить строки**, сохранить заголовок и автоматически сдвинуть оставшиеся ячейки вверх. К концу вы сможете **удалять строки из таблицы**, **удалять несколько строк** и **удалять первые строки** всего в несколько строк кода.

---

## Что вам понадобится

- .NET 6+ (или .NET Framework 4.7.2 и выше)  
- Библиотека **Aspose.Cells for .NET** (бесплатная пробная версия или лицензия)  
- Базовые знания C# и Visual Studio (или любой другой IDE, который вам нравится)  

Никаких других зависимостей — только пакет NuGet и файл Excel для экспериментов.

---

## Шаг 1: Установите Aspose.Cells

Для начала добавьте пакет Aspose.Cells в ваш проект:

```bash
dotnet add package Aspose.Cells
```

Эта однострочная команда подтянет всё, что нужно для работы с рабочими книгами, листами и таблицами. Если вы используете Visual Studio, можно также щёлкнуть правой кнопкой по проекту → **Manage NuGet Packages** → поиск *Aspose.Cells* и нажать **Install**.

*Pro tip:* Используйте последнюю стабильную версию; на июль 2026 это **23.9.0**, которая поддерживает новейшие форматы файлов Excel.

---

## Шаг 2: Загрузите рабочую книгу, содержащую таблицу

Теперь откроем файл Excel, в котором находятся данные, требующие очистки. Замените `YOUR_DIRECTORY` реальным путём на вашем компьютере.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Load the workbook that contains the table
        Workbook workbook = new Workbook(@"C:\Data\table.xlsx");
        
        // Grab the first worksheet (index 0)
        Worksheet sheet = workbook.Worksheets[0];
        
        // Optional: get a reference to the first table for context
        Table table = sheet.Tables[0];
```

На данном этапе у нас есть объект `Worksheet`, готовый к манипуляциям. Обратите внимание, что таблица пока не тронута — сохранение заголовка критично, когда позже будем **сдвигать ячейки вверх**.

---

## Шаг 3: Удалите первые две строки, сдвигая ячейки вверх

Вот суть задачи: удалять строки *и* заставлять ячейки ниже автоматически подниматься. Aspose.Cells предоставляет метод `DeleteRows`, который делает именно это, если передать `true` для параметра `shiftCellsUp`.

```csharp
        // Delete the first two rows (row index starts at 0)
        // The third argument ‑‑> true tells Aspose.Cells to shift cells up.
        sheet.Cells.DeleteRows(0, 2, true);
```

### Почему важен флаг `true`

Если опустить `true`, строки удалятся, но их место останется пустым, образуя пробелы в данных. Установка **true** сообщает библиотеке свернуть диапазон, эффективно **сдвигая ячейки вверх**, так что строка 3 становится новой строкой 1. Это самый чистый способ **удалить первые строки** без нарушения формул или структуры таблицы.

> **Важно:** Удаление строк, включающих заголовок таблицы, вызовет исключение. Сохраните строку‑заголовок (обычно строка 0) нетронутой, либо удалите её отдельно после восстановления заголовка таблицы.

---

## Шаг 4: Проверьте, что таблица выглядит корректно

После удаления стоит убедиться, что ссылка таблицы всё ещё указывает на правильный диапазон. Можно вывести адрес таблицы или обновить его:

```csharp
        // Refresh the table range to reflect the new data area
        table.Refresh();

        // Output the new range for debugging
        Console.WriteLine($"Table now spans: {table.Ref}");
```

Запуск программы должен показать что‑то вроде `Table1!A1:D8` вместо исходного `A1:D10`, подтверждая, что строки удалены и ячейки сдвинуты вверх.

---

## Шаг 5: Сохраните изменённую рабочую книгу

Наконец, запишите изменения обратно на диск. Можно перезаписать оригинальный файл или создать новую копию — на ваш выбор.

```csharp
        // Save the workbook with the changes
        workbook.Save(@"C:\Data\modified_table.xlsx");
    }
}
```

Откройте `modified_table.xlsx` в Excel, и вы увидите, что первые две строки исчезли, остальные строки поднялись, а таблица осталась целой. Операция эффективно **удалила несколько строк**, сохранив целостность данных.

---

## Пограничные случаи и распространённые подводные камни

| Ситуация | Что происходит | Как решить |
|-----------|----------------|-------------|
| **Строка‑заголовок входит в диапазон удаления** | Aspose.Cells бросает `InvalidOperationException`, потому что таблица не может потерять заголовок. | Удаляйте только строки данных, либо воссоздайте заголовок после удаления с помощью `sheet.Cells["A1"].PutValue("Header")`. |
| **Таблица охватывает несколько листов** | Удаление строк на одном листе не влияет на остальные. | Пройдитесь по каждому листу и его таблицам, если нужен глобальный чистка. |
| **Большие файлы (>100 МБ)** | Потребление памяти резко возрастает. | Используйте `LoadOptions` с `MemoryPreference` = `MemoryPreference.MemoryOnly`, чтобы уменьшить нагрузку на ОЗУ. |
| **Необходимо сохранить формулы, ссылающиеся на удалённые строки** | Формулы могут стать `#REF!`. | Вызовите `sheet.Cells.DeleteRows(startRow, count, true, true)` — четвёртый аргумент заставит Aspose.Cells обновить формулы. |

---

## Часто задаваемые вопросы

**В: Можно ли удалять строки по условию, а не по фиксированному индексу?**  
О: Конечно. Пройдитесь по `sheet.Cells.Rows` и вызывайте `DeleteRows(rowIndex, 1, true)`, когда условие выполнено. Не забудьте итерировать в обратном порядке, чтобы избежать смещения индексов.

**В: Работает ли это с файлами `.xls`?**  
О: Да. Aspose.Cells поддерживает как `.xlsx`, так и устаревший формат `.xls`. API одинаково.

**В: Что если в рабочей книге несколько таблиц, а я хочу изменить только одну?**  
О: Обратитесь к конкретной таблице по имени: `Table myTable = sheet.Tables["MyTable"];` затем используйте `myTable.Range.StartRow` для вычисления строк, которые нужно удалить.

---

## Полный рабочий пример

Ниже представлен полностью готовый к запуску код, включающий всё, о чём мы говорили. Скопируйте‑вставьте его в консольное приложение, поправьте пути к файлам и нажмите **F5**.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the workbook
        Workbook workbook = new Workbook(@"C:\Data\table.xlsx");
        Worksheet sheet = workbook.Worksheets[0];

        // 2️⃣ (Optional) Reference the first table for context
        Table table = sheet.Tables[0];

        // 3️⃣ Delete the first two rows and shift cells up
        //    Row index starts at 0, delete 2 rows, shift up = true
        sheet.Cells.DeleteRows(0, 2, true);

        // 4️⃣ Refresh the table range so it reflects the new data area
        table.Refresh();

        // 5️⃣ Show the new table reference (useful for debugging)
        Console.WriteLine($"Table now spans: {table.Ref}");

        // 6️⃣ Save the modified workbook
        workbook.Save(@"C:\Data\modified_table.xlsx");

        Console.WriteLine("Rows removed and cells shifted up successfully!");
    }
}
```

**Ожидаемый результат:**  
- Строки 1‑2 исчезают с листа.  
- Строка 3 становится новой строкой 1, строка 4 — строкой 2 и т.д.  
- Диапазон таблицы автоматически обновляется, подтверждая, что **сдвиг ячеек вверх** выполнен корректно.

---

## Заключение

Мы только что рассмотрели, как **сдвигать ячейки вверх** в листе Excel с помощью C#. Используя метод `DeleteRows` библиотеки Aspose.Cells с флагом `true`, вы можете безопасно **удалять первые строки**, **удалять несколько строк** и **удалять строки из таблицы**, не нарушая модель данных. Подход быстрый, надёжный и работает со всеми современными форматами Excel.

Готовы к следующему шагу? Попробуйте сочетать эту технику с условным фильтром, чтобы удалять строки, содержащие пустые значения или дубликаты. Или изучите API стилизации Aspose.Cells, чтобы заново применить форматирование после сдвига. Возможности безграничны, когда вы владеете манипуляцией строк в Excel.

Есть вопросы или интересный кейс, которым хотите поделиться? Оставляйте комментарий ниже, и happy coding!

## Что изучать дальше?

Следующие руководства охватывают тесно связанные темы, расширяющие техники, продемонстрированные в этом гайде. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы в собственных проектах.

- [Delete Multiple Rows in Excel with Aspose.Cells .NET&#58; A Comprehensive Guide for Data Manipulation](/cells/english/net/data-manipulation/delete-rows-excel-aspose-cells-net/)
- [How to Insert and Delete Rows in Excel with Aspose.Cells for .NET&#58; A Comprehensive Guide](/cells/english/net/data-manipulation/aspose-cells-net-insert-delete-excel-rows/)
- [How to Delete Blank Rows in Excel Using Aspose.Cells .NET for Data Cleanup](/cells/english/net/data-manipulation/delete-blank-rows-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}