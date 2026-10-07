---
category: general
date: 2026-06-08
description: Удаление строк в таблице Word с помощью Aspose.Words. Узнайте, как удалять
  строки, удалять несколько строк в Word, и освоить редактирование таблиц за несколько
  минут.
draft: false
keywords:
- delete rows word table
- how to delete rows
- delete multiple rows word
language: ru
og_description: Удаление строк в таблице Word с помощью Aspose.Words. Этот учебник
  показывает, как удалять строки, удалять несколько строк в Word и поддерживать порядок
  в ваших таблицах.
og_title: Удаление строк в таблице Word – Полное руководство по C#
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Delete rows word table using Aspose.Words. Learn how to delete rows,
    delete multiple rows word, and master table editing in minutes.
  headline: Delete rows word table – Complete C# Guide
  type: TechArticle
- description: Delete rows word table using Aspose.Words. Learn how to delete rows,
    delete multiple rows word, and master table editing in minutes.
  name: Delete rows word table – Complete C# Guide
  steps:
  - name: 3.1 How to delete rows (single row)
    text: 'To remove a single row, call `DeleteRows(startIndex, count)` where `startIndex`
      is zero‑based. Skipping the header row (index 0) is common:'
  - name: 3.2 Delete multiple rows word – batch removal
    text: 'When you need to drop a range—say rows 2‑6—you pass the start index and
      the number of rows to erase. This is the **delete multiple rows word** pattern:'
  - name: Expected output
    text: '- `output.docx` contains the original table **without** rows 2‑6. - All
      remaining rows shift up, preserving cell formatting and column widths. - The
      header row stays intact, keeping your column titles visible.'
  type: HowTo
- questions:
  - answer: Absolutely. Loop through `table.Rows`, inspect `row.Cells[i].GetText()`,
      and collect matching indices. Then call `DeleteRows` with the smallest index
      and total count, or delete rows in reverse order to avoid re‑indexing.
    question: Can I delete rows based on cell content instead of index?
  - answer: Yes. Aspose.Words supports both `.doc` and `.docx`. Just change the file
      extension in the `Document` constructor and `Save` call.
    question: Does this work with .doc files?
  - answer: 'Retrieve it via `doc.FirstSection.HeadersFooters` collection, then apply
      the same `DeleteRows` logic. ## Conclusion You now have a solid, end‑to‑end
      solution for **delete rows word table** using C#. The example shows *how to
      delete rows* individually and how to **delete multiple rows word** in a sin'
    question: What if the table is inside a header/footer?
  type: FAQPage
tags:
- C#
- Aspose.Words
- Word automation
title: Удаление строк таблицы Word – Полное руководство по C#
url: /ru/net/tables-and-lists/delete-rows-word-table-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Удаление строк в таблице Word – Полное руководство по C#

Когда‑нибудь вам нужно было **delete rows word table**, но вы не знали, с чего начать? Вы не одиноки; многие разработчики сталкиваются с этой проблемой при очистке сгенерированных отчетов или обрезке таблиц, основанных на данных. Хорошая новость? С несколькими строками C# и Aspose.Words вы можете легко удалить ненужные строки, будь то одна строка или их пакет. В этом руководстве мы пройдемся по *how to delete rows* и даже рассмотрим более сложный случай **delete multiple rows word** за один раз.

Мы охватим всё, что вам нужно знать: точный код, почему каждый шаг важен, типичные подводные камни и готовый к запуску пример. К концу вы сможете удалять строки из любой таблицы Word, не нарушая структуру документа. Без лишних слов, только практические, проверенные в бою техники.

## Требования

Перед тем как начать, убедитесь, что у вас есть:

- **Aspose.Words for .NET** (версия 23.12 или новее). Вы можете установить её из NuGet: `Install-Package Aspose.Words`.
- Среда разработки .NET (Visual Studio, Rider или VS Code с расширением C#).
- Входной файл Word (`input.docx`), содержащий хотя бы одну таблицу с заголовочной строкой.

И всё — никаких дополнительных библиотек, без COM‑interop, только чистый управляемый код.

## Шаг 1: Загрузка документа Word

Первое, что нужно сделать, — открыть документ. Aspose.Words рассматривает файл Word как объект `Document`, который даёт полный доступ к разделам, телам, таблицам и прочему.

```csharp
using Aspose.Words;

class TableCleaner
{
    static void Main()
    {
        // Load the source .docx file
        Document doc = new Document(@"YOUR_DIRECTORY\input.docx");
        // Continue with table manipulation…
```

*Почему это важно:* Загрузка документа создаёт представление в памяти, поэтому любые изменения происходят быстро и не затрагивают файловую систему, пока вы явно не сохраните файл.

## Шаг 2: Получение целевой таблицы

В большинстве случаев вы знаете, какую таблицу нужно редактировать — обычно первую. Aspose.Words делает её получение тривиальным через свойство `FirstSection`.

```csharp
        // Access the first table in the first section
        Table table = doc.FirstSection.Body.Tables[0];
```

Если в документе несколько таблиц, вы можете пройтись по `doc.GetChildNodes(NodeType.Table, true)` и выбрать нужную по индексу или пользовательскому маркеру.

## Шаг 3: Удаление строк — одна или несколько

### 3.1 Как удалить строку (одна строка)

Чтобы удалить одну строку, вызовите `DeleteRows(startIndex, count)`, где `startIndex` — ноль‑базовый индекс. Часто пропускают заголовочную строку (индекс 0):

```csharp
        // Delete just the second row (index 1)
        table.DeleteRows(1, 1);
```

### 3.2 Delete multiple rows word — пакетное удаление

Когда нужно удалить диапазон, например строки 2‑6, передайте начальный индекс и количество строк для удаления. Это и есть шаблон **delete multiple rows word**:

```csharp
        // Delete rows 2‑6 (skip header at index 0)
        // startIndex = 1 (second row), count = 5 rows
        table.DeleteRows(1, 5);
```

*Зачем использовать один вызов?* Удаление строк по одной заставляет таблицу переиндексировать после каждого удаления, что может привести к ошибкам и замедлить процесс. Пакетный метод сохраняет внутреннюю структуру таблицы согласованной.

#### Пограничный случай: удаление за пределами таблицы

Если `startIndex + count` превышает фактическое количество строк, Aspose.Words бросит `ArgumentOutOfRangeException`. Защитный guard выглядит так:

```csharp
        int rowsToDelete = Math.Min(5, table.Rows.Count - 1); // never delete the header
        if (rowsToDelete > 0)
            table.DeleteRows(1, rowsToDelete);
```

Этот фрагмент гарантирует, что вы никогда не попытаетесь удалить больше строк, чем существует.

## Шаг 4: Сохранение изменённого документа

После того как строки удалены, сохранить изменения можно одной строкой:

```csharp
        // Save the cleaned document
        doc.Save(@"YOUR_DIRECTORY\output.docx");
    }
}
```

Метод `Save` автоматически выбирает формат по расширению файла, поэтому вы можете вывести документ в PDF, HTML или даже ODT, изменив суффикс.

## Полный рабочий пример

Собрав всё вместе, получаем полностью готовую к запуску программу:

```csharp
using System;
using Aspose.Words;

class TableCleaner
{
    static void Main()
    {
        // 1️⃣ Load the Word document
        Document doc = new Document(@"YOUR_DIRECTORY\input.docx");

        // 2️⃣ Access the first table (adjust index if needed)
        Table table = doc.FirstSection.Body.Tables[0];

        // 3️⃣ Delete rows 2‑6 (skip header row at index 0)
        //    This demonstrates delete multiple rows word in one call.
        if (table.Rows.Count > 1) // ensure there is at least a header + one data row
        {
            int rowsToDelete = Math.Min(5, table.Rows.Count - 1);
            table.DeleteRows(1, rowsToDelete);
        }

        // 4️⃣ Save the modified document
        doc.Save(@"YOUR_DIRECTORY\output.docx");

        Console.WriteLine("Rows removed successfully. Output saved to output.docx");
    }
}
```

### Ожидаемый результат

- `output.docx` содержит исходную таблицу **без** строк 2‑6.
- Все оставшиеся строки смещаются вверх, сохраняя форматирование ячеек и ширину столбцов.
- Заголовочная строка остаётся нетронутой, поэтому названия столбцов видны.

## Почему этот подход лучше альтернатив

| Подход | Преимущества | Недостатки |
|----------|------|------|
| **Aspose.Words `DeleteRows`** | Однострочное пакетное удаление, сохраняет стили, без COM‑зависимостей | Требует коммерческой библиотеки (доступна бесплатная пробная версия) |
| Office Interop | Работает с нативным Word | Требует установленный Word на сервере, медленно, проблемы с очисткой COM |
| Open XML SDK | Бесплатно, открытый исходный код | Ручная работа с XML; безопасное удаление строк громоздко |

Если вы уже используете Aspose.Words для других задач с документами, оставаться на `DeleteRows` позволит поддерживать кодовую базу чистой и согласованной.

## Советы профессионалов и типичные подводные камни

- **Совет:** Всегда оставляйте заголовочную строку (индекс 0) нетронутой, если только вы действительно не хотите её удалить. Удаление заголовка может сломать последующую обработку, ожидающую имена столбцов.
- **Остерегайтесь объединённых ячеек.** Если строка содержит вертикально объединённую ячейку, которая охватывает удаляемую строку, Aspose.Words автоматически скорректирует диапазон объединения, но визуально проверьте результат.
- **Замечание о производительности:** Удаление большого количества строк из массивной таблицы (тысячи строк) всё равно быстро, однако при обработке сотен документов в цикле стоит переиспользовать объект `Document`, где это возможно, чтобы снизить нагрузку на выделение памяти.

## Часто задаваемые вопросы

**В: Можно ли удалять строки на основе содержимого ячейки, а не индекса?**  
О: Конечно. Пройдите по `table.Rows`, проверьте `row.Cells[i].GetText()` и соберите подходящие индексы. Затем вызовите `DeleteRows` с минимальным индексом и общим количеством, либо удаляйте строки в обратном порядке, чтобы избежать переиндексации.

**В: Работает ли это с файлами .doc?**  
О: Да. Aspose.Words поддерживает как `.doc`, так и `.docx`. Просто измените расширение в конструкторе `Document` и вызове `Save`.

**В: Что делать, если таблица находится в колонтитуле/нижнем колонтитуле?**  
О: Получите её через коллекцию `doc.FirstSection.HeadersFooters`, затем примените ту же логику `DeleteRows`.

## Заключение

Теперь у вас есть надёжное сквозное решение для **delete rows word table** с использованием C#. Пример показывает *how to delete rows* по отдельности и как **delete multiple rows word** выполнить одним эффективным вызовом. С Aspose.Words вы получаете чистый API, без COM‑проблем и полный контроль над документами Word.

Готовы к следующему вызову? Попробуйте добавить новую строку с вычисленными итогами или экспортировать обрезанную таблицу в CSV с помощью `Table.ToTxt`. Возможности безграничны, когда вы владеете манипуляцией таблицами.

Счастливого кодинга, и пусть ваши таблицы Word остаются аккуратными!

## Что изучать дальше?

Следующие руководства охватывают тесно связанные темы, расширяющие техники, продемонстрированные в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы в собственных проектах.

- [How to Delete Rows in Excel Using Aspose.Cells for Java | Guide & Tutorial](/cells/english/java/worksheet-management/delete-row-excel-aspose-cells-java/)
- [How to Delete Blank Rows in Excel Using Aspose.Cells .NET for Data Cleanup](/cells/english/net/data-manipulation/delete-blank-rows-aspose-cells-net/)
- [How to Insert and Delete Rows in Excel with Aspose.Cells for .NET&#58; A Comprehensive Guide](/cells/english/net/data-manipulation/aspose-cells-net-insert-delete-excel-rows/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}