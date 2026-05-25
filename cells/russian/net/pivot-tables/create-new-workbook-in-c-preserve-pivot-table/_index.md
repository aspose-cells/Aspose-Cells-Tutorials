---
category: general
date: 2026-02-15
description: Создайте новую книгу в C# и скопируйте сводную таблицу, не теряя её определения.
  Узнайте, как копировать строки, сохранять сводную таблицу и легко дублировать её.
draft: false
keywords:
- create new workbook
- copy pivot table
- preserve pivot table
- how to copy rows
- duplicate pivot table
language: ru
og_description: Создайте новую книгу в C# и скопируйте сводную таблицу, сохранив её
  определение. Пошаговое руководство для разработчиков.
og_title: Создать новую книгу в C# – Сохранить сводную таблицу
tags:
- Aspose.Cells
- C#
- Excel automation
title: Создать новую книгу в C# — Сохранить сводную таблицу
url: /ru/net/pivot-tables/create-new-workbook-in-c-preserve-pivot-table/
---

top-button >}}

Make sure to keep shortcodes at end.

Now produce final content with translation. Ensure all markdown formatting preserved.

Let's craft final answer.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание новой книги Excel в C# – Сохранение сводной таблицы

Когда‑нибудь вам нужно было **create new workbook** в C#, содержащий точную копию сводной таблицы из другого файла? Вы не одиноки. Во многих конвейерах отчетности сводная таблица является сердцем анализа, и потеря её определения при перемещении данных — настоящий кошмар.

Хорошие новости? С помощью нескольких строк кода Aspose.Cells вы можете копировать строки — включая сводную таблицу — в новую книгу и сохранить всё в целости. Ниже вы увидите **how to copy rows**, **preserve pivot table** настройки, и даже **duplicate pivot table** между файлами без нарушения формул или кэша.

## Что охватывает этот учебник

В этом руководстве мы пройдем:

1. Загрузка исходной книги, в которой уже есть сводная таблица.  
2. **Create new workbook** объекты для назначения.  
3. Использование `CopyRows` для передачи диапазона, содержащего сводную таблицу.  
4. Сохранение результата с гарантией того, что сводная таблица остаётся рабочей.  

Никакой внешней документации не требуется — только код, объяснение «почему» и несколько практических советов, которые вы можете сразу вставить в свой проект.

> **Профессиональный совет:** Aspose.Cells работает с .NET Core, .NET Framework и даже Xamarin, поэтому один и тот же фрагмент кода работает везде, где он вам нужен.

---

![Create new workbook with copied pivot table](/images/create-new-workbook-pivot.png "create new workbook with copied pivot table")

## Шаг 1 – Создание новой книги и загрузка исходного файла

Первое, что мы делаем, — **create new workbook** объекты. Один содержит оригинальные данные, другой получит скопированный диапазон.

```csharp
using Aspose.Cells;

// Load the source workbook that already contains a pivot table
var sourceWorkbook = new Workbook(@"C:\Data\source.xlsx");

// Create an empty workbook that will become the destination
var destinationWorkbook = new Workbook();
```

*Почему это важно:*  
`Workbook` — это точка входа для любой работы с Excel в Aspose.Cells. Создавая новую книгу, мы гарантируем чистый лист — без скрытых стилей или лишних листов, которые могут помешать позже.

## Шаг 2 – Как копировать строки, включая сводную таблицу

Теперь переходим к основной части задачи: **how to copy rows**, которые охватывают сводную таблицу, не уплощая её. Метод `CopyRows` делает именно это.

```csharp
// Copy the first 20 rows (adjust as needed) from the source to the destination
// Parameters: startRow, totalRows, targetCells, targetStartRow
sourceWorkbook.Worksheets[0].Cells.CopyRows(
    startRow: 0,
    totalRows: 20,
    targetCells: destinationWorkbook.Worksheets[0].Cells,
    targetStartRow: 0);
```

Несколько моментов, на которые стоит обратить внимание:

* `startRow` и `totalRows` определяют блок, содержащий сводную таблицу.  
* Метод копирует **both** исходные данные и кэш сводной таблицы, поэтому целевая книга знает, как воссоздать сводную таблицу «на лету».  
* Если ваша сводная таблица начинается глубже в листе, просто измените индексы — нет необходимости вызывать другой API.

> **Распространённый вопрос:** *Потеряет ли скопированная сводная таблица ссылку на исходные данные?*  
> Нет. Aspose.Cells встраивает кэш непосредственно в лист, поэтому сводная таблица становится автономной в новом файле.

## Шаг 3 – Сохранение сводной таблицы при сохранении назначения

После копирования строк сводная таблица находится в целевой книге точно так же, как в исходной. Сохранить файл просто.

```csharp
// Save the destination workbook; the pivot table remains functional
destinationWorkbook.Save(@"C:\Data\destination.xlsx");
```

Когда вы откроете `destination.xlsx` в Excel, вы увидите сводную таблицу, готовую к обновлению. Поведение **preserve pivot table** происходит автоматически, потому что кэш переехал вместе со строками.

### Проверка результата

Откройте файл и:

1. Щёлкните по сводной таблице.  
2. Обратите внимание, что появился список полей — это значит, что кэш цел.  
3. Попробуйте обновить; данные обновятся без ошибок.

Если вы столкнётесь с ошибкой *#REF!*, дважды проверьте, что скопированный диапазон включает скрытые строки кэша (обычно сразу после видимых данных).

## Шаг 4 – Дублирование сводной таблицы в несколько книг (опционально)

Иногда один и тот же свод нужен в нескольких отчётах. Использованный нами шаблон масштабируется без проблем — просто повторите копирование для каждой новой книги.

```csharp
string[] targets = {
    @"C:\Reports\Q1.xlsx",
    @"C:\Reports\Q2.xlsx",
    @"C:\Reports\Q3.xlsx"
};

foreach (var path in targets)
{
    var wb = new Workbook(); // fresh workbook each loop
    sourceWorkbook.Worksheets[0].Cells.CopyRows(0, 20, wb.Worksheets[0].Cells, 0);
    wb.Save(path);
}
```

Этот фрагмент **duplicates pivot table** трижды в одном цикле. Отрегулируйте массив `targets`, чтобы он соответствовал вашему графику отчётности.

### Особые случаи, которые следует учитывать

| Situation | What to Watch For | Fix |
|-----------|-------------------|-----|
| Pivot uses external data source | Cache may reference a connection that doesn’t exist on the new machine | Embed the data source or recreate the connection in the destination workbook |
| Very large pivot ( > 100 k rows ) | `CopyRows` can be memory‑intensive | Use `CopyRows` in chunks or consider `Copy` with `PasteOptions` to limit memory usage |
| Worksheet has hidden rows/columns | Hidden cache rows might be skipped if you copy only visible rows | Always copy the exact row range that contains the cache, not just the visible area |

## Полный рабочий пример

Объединив всё вместе, получаем автономную программу, которую можно вставить в консольное приложение.

```csharp
using System;
using Aspose.Cells;

namespace PivotCopyDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load source workbook (contains the original pivot)
            var sourcePath = @"C:\Data\source.xlsx";
            var sourceWorkbook = new Workbook(sourcePath);

            // 2️⃣ Prepare destination workbook
            var destinationWorkbook = new Workbook();

            // 3️⃣ Copy rows that include the pivot (adjust range as needed)
            sourceWorkbook.Worksheets[0].Cells.CopyRows(
                startRow: 0,
                totalRows: 20,
                targetCells: destinationWorkbook.Worksheets[0].Cells,
                targetStartRow: 0);

            // 4️⃣ Save – the pivot table is preserved
            var destPath = @"C:\Data\destination.xlsx";
            destinationWorkbook.Save(destPath);

            Console.WriteLine("Pivot table successfully copied!");
        }
    }
}
```

Запустите программу, откройте `destination.xlsx`, и вы увидите ту же сводную таблицу, готовую к анализу ваших данных. Ручное воссоздание не требуется.

---

## Заключение

Мы только что показали, как **create new workbook** в C# и **copy pivot table**, сохранив все настройки. Используя `CopyRows`, вы получаете надёжный способ **preserve pivot table** функциональности, отвечаете на извечный вопрос «**how to copy rows**», и даже **duplicate pivot table** в нескольких отчётах с минимальным объёмом кода.

Следующие шаги? Попробуйте изменить скопированный диапазон, чтобы включить диаграммы, ссылающиеся на ту же сводную таблицу, или поэкспериментировать с `PasteOptions`, чтобы точно сохранить форматирование. Тот же шаблон работает и с другими объектами Aspose.Cells, такими как таблицы и именованные диапазоны, так что смело расширяйте его.

Есть сложный случай — возможно, сводная таблица берёт данные из внешней БД или книга хранится в облаке? Оставьте комментарий ниже, и мы разберёмся вместе. Счастливого кодинга!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}