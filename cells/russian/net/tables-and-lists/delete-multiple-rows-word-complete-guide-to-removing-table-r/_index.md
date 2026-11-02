---
category: general
date: 2026-06-27
description: Удалить несколько строк в Word с помощью C#. Узнайте, как удалять строки
  таблицы, удалять строки таблицы и эффективно редактировать таблицы в документе Word.
draft: false
keywords:
- delete multiple rows word
- how to delete table rows
- how to remove table rows
- delete rows from word table
- word document table editing
language: ru
og_description: Мгновенно удаляйте несколько строк в Word. Этот учебник показывает,
  как удалять строки таблицы, удалять строки из таблицы Word и мастерски редактировать
  таблицы в документе Word.
og_title: Удалить несколько строк в Word – пошаговое редактирование таблицы
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: Delete multiple rows word using C#. Learn how to delete table rows,
    remove table rows and edit Word document tables efficiently.
  headline: Delete Multiple Rows Word – Complete Guide to Removing Table Rows
  type: TechArticle
tags:
- Aspose.Words
- C#
- Word Automation
title: Удаление нескольких строк в Word – Полное руководство по удалению строк таблицы
url: /ru/net/tables-and-lists/delete-multiple-rows-word-complete-guide-to-removing-table-r/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Удаление нескольких строк Word – Полное руководство по удалению строк таблицы

Когда‑нибудь вам нужно было **удалить несколько строк word** в документах, но вы не знали, какой вызов API использовать? Вы не одиноки — большинство разработчиков сталкиваются с той же проблемой, пытаясь сократить таблицу, сохранив заголовок нетронутым.  

В этом руководстве мы пройдём через краткое, сквозное решение, которое покажет *как программно удалять строки таблицы*, *как безопасно удалять строки таблицы* и почему подход работает для любого сценария **удаления строк из таблицы Word**, с которым вы можете столкнуться.

К концу вы получите переиспользуемый фрагмент кода, который можно вставить в любой проект C#, а также несколько советов для более широких задач **редактирования таблиц в Word‑документах**.

## Требования

- .NET 6.0 или новее (код также работает на .NET Framework 4.6+)
- Aspose.Words for .NET установлен (`dotnet add package Aspose.Words`)
- Базовое понимание синтаксиса C#
- Входной файл `.docx`, содержащий как минимум одну таблицу с заголовочной строкой

> **Совет:** Если у вас ещё нет лицензии, Aspose.Words предлагает бесплатный режим оценки, который идеально подходит для тестирования.

## Шаг 1: Настройка проекта и загрузка Word‑документа

Сначала создайте консольное приложение (или интегрируйте в существующий сервис) и добавьте необходимые директивы `using`. Затем загрузите исходный документ.

```csharp
using System;
using Aspose.Words;
using Aspose.Words.Tables;

class Program
{
    static void Main()
    {
        // Load the Word document (replace YOUR_DIRECTORY with your actual path)
        Document doc = new Document(@"YOUR_DIRECTORY\input.docx");
        Console.WriteLine("Document loaded successfully.");
```

**Почему это важно:**  
`Document` — точка входа для любой операции Aspose.Words. Однократная загрузка файла снижает использование памяти и даёт вам доступ ко всем последующим вызовам редактирования таблиц.

## Шаг 2: Поиск первой таблицы (или любой нужной таблицы)

Если ваш документ содержит несколько таблиц, вы можете выбрать нужную по индексу или поиском по ключевому слову. Для простоты мы возьмём первую таблицу, в которой обычно находятся данные, которые нужно обрезать.

```csharp
        // Retrieve the first table in the document
        Table firstTable = doc.GetChild(NodeType.Table, 0, true) as Table;
        if (firstTable == null)
        {
            Console.WriteLine("No table found in the document.");
            return;
        }
        Console.WriteLine($"Table with {firstTable.Rows.Count} rows found.");
```

**Объяснение:**  
`GetChild(NodeType.Table, 0, true)` проходит дерево документа в глубину и возвращает первый найденный узел `Table`. Приведение `as Table` безопасно преобразует узел, позволяя нам работать с `Rows` позже.

## Шаг 3: Удаление нескольких строк с сохранением заголовка

Теперь переходим к сути: **удалить несколько строк word** в документах. Предположим, заголовок находится в строке 0, а вы хотите удалить следующие две строки (индексы 1 и 2). Метод `DeleteRows` делает именно это.

```csharp
        // Delete two rows starting from the second row (index 1)
        // This keeps the header row untouched while removing the following rows
        firstTable?.DeleteRows(1, 2);
        Console.WriteLine("Specified rows deleted.");
```

### Как удалять строки таблицы – Вариации

- **Удалить одну строку:** `firstTable?.DeleteRows(rowIndex, 1);`
- **Удалить все строки, кроме заголовка:** `firstTable?.DeleteRows(1, firstTable.Rows.Count - 1);`
- **Удалить строки по условию:** перебрать `firstTable.Rows` и вызвать `DeleteRows`, когда ячейка соответствует вашему критерию.

Эти фрагменты отвечают на распространённый вопрос **как удалить строки таблицы** гибким способом.

## Шаг 4: Сохранение изменённого документа

После удаления строк вы просто записываете документ обратно на диск. Можно перезаписать оригинальный файл или создать новую копию.

```csharp
        // Save the modified document
        doc.Save(@"YOUR_DIRECTORY\output.docx");
        Console.WriteLine("Document saved as output.docx");
    }
}
```

**Что вы увидите:**  
Если в оригинальной таблице было, скажем, пять строк (заголовок + четыре строки данных), сохранённый `output.docx` теперь будет содержать только три строки (заголовок + оставшиеся две строки данных). Откройте файл в Word, чтобы убедиться, что нежелательные строки исчезли, не затронув остальное содержимое.

![пример удаления нескольких строк word](delete-multiple-rows-word.png)

*Текст альтернативного изображения: удаление нескольких строк word – скриншот таблицы Word до и после.*

## Полный готовый к запуску пример

Собрав всё вместе, представляем полный программный код, который можно скопировать и вставить:

```csharp
using System;
using Aspose.Words;
using Aspose.Words.Tables;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the Word document
        Document doc = new Document(@"YOUR_DIRECTORY\input.docx");
        Console.WriteLine("Document loaded.");

        // 2️⃣ Retrieve the first table
        Table firstTable = doc.GetChild(NodeType.Table, 0, true) as Table;
        if (firstTable == null)
        {
            Console.WriteLine("No table found.");
            return;
        }
        Console.WriteLine($"Found table with {firstTable.Rows.Count} rows.");

        // 3️⃣ Delete rows – this is the core of delete rows from word table
        //    Starting at index 1 (second row), delete the next two rows.
        firstTable?.DeleteRows(1, 2);
        Console.WriteLine("Rows deleted.");

        // 4️⃣ Save the result
        doc.Save(@"YOUR_DIRECTORY\output.docx");
        Console.WriteLine("Saved output.docx");
    }
}
```

Запустите программу, откройте `output.docx`, и вы увидите, что заголовок остался, а выбранные строки исчезли. Это **удаление нескольких строк word** в действии.

## Распространённые подводные камни и как их избежать

| Проблема | Почему происходит | Как исправить |
|----------|-------------------|---------------|
| **NullReferenceException** когда `firstTable` равно `null` | В документе нет таблиц или указан неверный индекс | Всегда проверяйте `firstTable != null` перед вызовом `DeleteRows`. |
| **Строки не удаляются** | Используется неверный начальный индекс (таблицы Word нумеруются с нуля) | Помните, что заголовок — строка 0; начинайте с 1, чтобы сохранить его. |
| **Сохранение поверх файла только для чтения** | Разрешения файла не позволяют перезаписать | Сохраните в другой путь или измените атрибуты файла. |
| **Неожиданные изменения макета** | Удаление строк, содержащих объединённые ячейки, может испортить таблицу | Убедитесь, что объединённые ячейки обработаны — сначала разъедините их или аккуратно удаляйте целые строки. |

## Расширение решения – Большее редактирование таблиц в Word‑документах

Если вас интересует более широкое **редактирование таблиц в Word‑документах**, рассмотрите следующие шаги:

- **Вставить новые строки**: `firstTable?.Rows.Add(new Row(doc));`
- **Обновить текст ячейки**: `firstTable.Rows[rowIndex].Cells[colIndex].Paragraphs[0].AppendText("New value");`
- **Применить стили**: Используйте `CellFormat` или `RowFormat` для установки затенения, границ или свойств шрифта.
- **Экспорт в PDF**: `doc.Save("output.pdf", SaveFormat.Pdf);`

Все эти операции основаны на той же объектной модели, которую мы использовали для удаления строк, что обеспечивает согласованность вашего кода.

## Заключение

Мы только что показали, как **удалять несколько строк word** в документах с помощью нескольких строк кода C#. Подход охватывает *как удалять строки таблицы*, *как удалять строки таблицы*, а также более широкую тему **редактирования таблиц в Word‑документах**.  

Теперь у вас есть надёжный, переиспользуемый шаблон: загрузить документ, найти таблицу, вызвать `DeleteRows` с правильными индексами и сохранить. Далее вы можете менять диапазон строк, перебрать таблицы или комбинировать с другими функциями редактирования для любой задачи автоматизации.  

Готовы пойти дальше? Попробуйте автоматизировать генерацию счетов, очистку шаблонов отчётов или создать инструмент массового обновления, который обрабатывает десятки Word‑файлов за один раз. Возможности безграничны, а API делает всё без усилий.  

Если возникнут проблемы, оставьте комментарий ниже — счастливого кодинга!

## Что изучать дальше?

Следующие руководства охватывают тесно связанные темы, построенные на техниках, продемонстрированных в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [Как вставлять и удалять строки в Excel с Aspose.Cells для .NET: Полное руководство](/cells/english/net/data-manipulation/aspose-cells-net-insert-delete-excel-rows/)
- [Удаление нескольких строк в Excel с Aspose.Cells .NET: Полное руководство по манипуляции данными](/cells/english/net/data-manipulation/delete-rows-excel-aspose-cells-net/)
- [Удаление нескольких строк в Aspose.Cells .NET](/cells/english/net/row-and-column-management/delete-multiple-rows-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}