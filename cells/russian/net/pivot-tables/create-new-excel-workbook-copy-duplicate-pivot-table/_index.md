---
category: general
date: 2026-02-09
description: Создайте новую книгу Excel и узнайте, как без усилий копировать сводные
  таблицы. Это руководство показывает, как дублировать сводную таблицу и сохранить
  книгу как новую.
draft: false
keywords:
- create new excel workbook
- how to copy pivot
- duplicate pivot table
- save workbook as new
- how to copy worksheet
language: ru
og_description: Создайте новую книгу Excel в C# и мгновенно скопируйте сводную таблицу.
  Узнайте, как дублировать сводную таблицу и сохранить книгу как новую, с полным примером
  кода.
og_title: Создать новую книгу Excel – пошаговое копирование сводной таблицы
tags:
- excel
- csharp
- aspose.cells
- automation
title: Создать новую книгу Excel — копировать и дублировать сводную таблицу
url: /ru/net/pivot-tables/create-new-excel-workbook-copy-duplicate-pivot-table/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создать новую книгу Excel – копировать и дублировать сводную таблицу

Когда‑нибудь вам нужно было **create new Excel workbook**, который переносит сложную сводную таблицу из существующего файла? Вы не одиноки — многие разработчики сталкиваются с этой проблемой при автоматизации конвейеров отчетности. Хорошая новость в том, что с несколькими строками C# и библиотекой Aspose.Cells вы можете быстро **how to copy pivot**, **duplicate pivot table** и **save workbook as new**, не открывая Excel вручную.

В этом руководстве мы пройдем весь процесс, от загрузки исходной книги до сохранения дублированной версии. К концу вы получите готовый к запуску фрагмент кода, который можно вставить в любой проект .NET. Без лишних слов, только практическое решение, которое вы можете протестировать уже сегодня.

## Что покрывает этот учебник

* **Prerequisites** – .NET 6+ (or .NET Framework 4.6+), Visual Studio, and the Aspose.Cells for .NET NuGet package.
* Пошаговый код, который **creates new Excel workbook**, копирует сводную таблицу и записывает результат на диск.
* Объяснения **why** каждой строки важны, а не только **what** она делает.
* Советы по обработке граничных случаев, таких как скрытые листы или большие диапазоны данных.
* Быстрый взгляд на **how to copy worksheet**, если вам когда‑нибудь понадобится весь лист, а не только сводная таблица.

Готовы? Погрузимся.

![иллюстрация создания новой книги Excel](image.png "Диаграмма, показывающая исходную книгу, копию сводной таблицы и целевую книгу")

## Шаг 1: Настройка проекта и установка Aspose.Cells

Прежде чем мы сможем **create new Excel workbook**, нам нужен проект, который ссылается на нужную библиотеку.

```csharp
// Install the Aspose.Cells package via NuGet:
//   dotnet add package Aspose.Cells
using Aspose.Cells;   // Provides Workbook, Worksheet, Range, etc.
using System;        // For basic .NET types
```

*Почему это важно:* Aspose.Cells работает полностью в памяти, поэтому вам никогда не придётся запускать Excel на сервере. Он также сохраняет информацию кэша сводной таблицы, что необходимо для настоящего **duplicate pivot table**.

> **Pro tip:** Если вы нацелены на .NET Core, убедитесь, что идентификатор среды выполнения (RID) вашего проекта соответствует платформе, на которую вы будете развертывать; иначе могут возникнуть ошибки загрузки нативных библиотек.

## Шаг 2: Загрузка исходной книги, содержащей сводную таблицу

Сейчас мы **how to copy pivot** из существующего файла. Исходная книга может находиться где угодно на диске, в потоке или даже в виде массива байтов.

```csharp
// Step 2: Load the source workbook that contains the pivot table
string sourcePath = @"C:\Reports\source.xlsx";
Workbook sourceWorkbook = new Workbook(sourcePath);

// Grab the first worksheet (adjust the index if your pivot lives elsewhere)
Worksheet sourceSheet = sourceWorkbook.Worksheets[0];

// Define the range that encloses the pivot table – A1:D20 in this example
Range sourceRange = sourceSheet.Cells.CreateRange("A1:D20");
```

*Почему мы выбираем диапазон:* Сводная таблица находится внутри обычного диапазона ячеек, но также имеет скрытые данные кэша, привязанные к листу. Копируя диапазон **including the pivot**, Aspose.Cells гарантирует, что кэш переедет вместе с ним, предоставляя вам рабочий **duplicate pivot table** в целевом файле.

## Шаг 3: Создание новой книги Excel для получения скопированных данных

Здесь мы действительно **create new Excel workbook**, который будет содержать дублированную сводную таблицу.

```csharp
// Step 3: Create a fresh workbook (empty) for the destination
Workbook destinationWorkbook = new Workbook(); // Starts with a default empty sheet
Worksheet destinationSheet = destinationWorkbook.Worksheets[0];

// Destination starts at A1 – you could offset if you need space for other data
Range destinationRange = destinationSheet.Cells.CreateRange("A1");
```

> **Why a fresh workbook?** Начало с чистого листа гарантирует, что никакое оставшееся форматирование или скрытые объекты не помешают скопированной сводной таблице. Это также делает полученный файл меньше, что удобно для автоматических вложений в электронные письма.

## Шаг 4: Копирование диапазона сводной таблицы в новую книгу

Сейчас мы выполняем реальную операцию **how to copy pivot**.

```csharp
// Step 4: Copy the range (including the pivot) from source to destination
sourceRange.Copy(destinationRange);
```

Эта единственная строка делает всю тяжёлую работу:

* Значения ячеек, формулы и форматирование передаются.
* Кэш сводной таблицы дублируется, поэтому новая сводная таблица остаётся полностью функциональной.
* Любые относительные ссылки внутри сводной таблицы автоматически корректируются под новое расположение.

### Обработка граничных случаев

* **Hidden worksheets:** Если исходный лист скрыт, сводная таблица всё равно копируется корректно, но вы можете захотеть раскрыть целевой лист для видимости пользователем:
  ```csharp
  destinationSheet.IsVisible = true;
  ```
* **Large data sets:** Для диапазонов более нескольких тысяч строк рассмотрите использование `CopyTo` с `CopyOptions` для потоковой передачи операции и снижения нагрузки на память.

## Шаг 5: Сохранение целевой книги как новый файл

Наконец, мы **save workbook as new** и проверяем результат.

```csharp
// Step 5: Save the destination workbook with the duplicated pivot table
string destPath = @"C:\Reports\copied.xlsx";
destinationWorkbook.Save(destPath, SaveFormat.Xlsx);

// Quick verification – open the file manually or read a cell value
Console.WriteLine($"Workbook saved to {destPath}");
```

Если открыть `copied.xlsx`, вы увидите точную копию оригинальной сводной таблицы, готовую к дальнейшему манипулированию или распространению.

### Опционально: Как копировать лист вместо только сводной таблицы

Иногда вам нужен весь лист, а не только сводная таблица. Тот же API делает это тривиальным:

```csharp
// Copy the whole worksheet (including all charts, tables, etc.)
sourceSheet.CopyTo(destinationWorkbook, 0); // Inserts at index 0
destinationWorkbook.Save(@"C:\Reports\full_copy.xlsx");
```

Это удовлетворяет запросу **how to copy worksheet** и может быть полезным, когда нужно сохранить дополнительные настройки уровня листа.

## Полный рабочий пример

Собрав всё вместе, представляем автономное консольное приложение, которое вы можете скомпилировать и запустить:

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // 1️⃣ Load source workbook
        string sourcePath = @"C:\Reports\source.xlsx";
        Workbook sourceWorkbook = new Workbook(sourcePath);
        Worksheet sourceSheet = sourceWorkbook.Worksheets[0];
        Range sourceRange = sourceSheet.Cells.CreateRange("A1:D20");

        // 2️⃣ Create destination workbook
        Workbook destinationWorkbook = new Workbook();
        Worksheet destinationSheet = destinationWorkbook.Worksheets[0];
        Range destinationRange = destinationSheet.Cells.CreateRange("A1");

        // 3️⃣ Copy the pivot (range)
        sourceRange.Copy(destinationRange);

        // 4️⃣ Save as new file
        string destPath = @"C:\Reports\copied.xlsx";
        destinationWorkbook.Save(destPath, SaveFormat.Xlsx);

        Console.WriteLine($"✅ Successfully created new Excel workbook with duplicated pivot table at {destPath}");
    }
}
```

**Expected output:** Консоль выводит сообщение об успехе, и `copied.xlsx` появляется в `C:\Reports` с рабочей сводной таблицей, идентичной той, что в `source.xlsx`.

## Часто задаваемые вопросы и подводные камни

* **Will formulas inside the pivot break?** Нет — потому что кэш сводной таблицы переезжает вместе с диапазоном, все вычисляемые поля остаются неизменными.
* **What if the source pivot uses external data connections?** Эти соединения *не* копируются. Вам потребуется заново установить их в целевой книге или сначала преобразовать сводную таблицу в статическую.
* **Can I copy multiple pivots at once?** Конечно — просто определите больший диапазон, охватывающий все сводные таблицы, или пройдитесь в цикле по каждому объекту `PivotTable` в `sourceSheet.PivotTables` и копируйте их по отдельности.
* **Do I need to dispose of the `Workbook` objects?** Они реализуют `IDisposable`, поэтому оборачивание их в конструкции `using` — хорошая привычка, особенно в сервисах с высокой пропускной способностью.

## Заключение

Теперь вы знаете **how to create new Excel workbook**, как копировать сводную таблицу, **duplicate pivot table** и **save workbook as new** с помощью C# и Aspose.Cells. Шаги просты: загрузить, создать, скопировать и сохранить. С опциональным фрагментом **how to copy worksheet** у вас также есть запасной вариант для полного дублирования листа.

Дальше вы можете изучить:

* Добавление пользовательского форматирования к дублированной сводной таблице.
* Программное обновление кэша сводной таблицы после изменения данных.
* Экспорт книги в PDF или CSV для последующих систем.

Попробуйте, подкорректируйте диапазон, и позвольте автоматизации снять рутинную работу из вашего процесса отчетности. Счастливого кодинга!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}