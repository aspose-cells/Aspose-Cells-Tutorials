---
category: general
date: 2026-03-18
description: Извлекать дату из Excel и выводить её в формате yyyy‑mm‑dd по ISO. Узнайте,
  как читать даты японских эпох, преобразовывать их и отображать даты ISO в C#.
draft: false
keywords:
- extract date from excel
- output date yyyy-mm-dd
- display date iso format
language: ru
og_description: Извлеките дату из Excel и выведите её в формате yyyy‑mm‑dd (ISO).
  Пошаговое руководство по C# с полным кодом и объяснениями.
og_title: Извлечение даты из Excel – вывод даты в формате yyyy‑mm‑dd в C#
tags:
- C#
- Excel
- DateTime
- Aspose.Cells
title: Извлечение даты из Excel и вывод даты в формате yyyy‑mm‑dd – Полное руководство
  по C#
url: /ru/net/data-loading-and-parsing/extract-date-from-excel-and-output-date-yyyy-mm-dd-complete/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Извлечение даты из Excel – Как вывести дату yyyy‑mm‑dd в формате ISO

Когда‑нибудь вам нужно было **извлечь дату из Excel**, но вы не знали, как работать с датами в японской эре или получить чистую строку `yyyy‑mm‑dd`? Вы не одиноки. Во многих проектах миграции данных исходная рабочая книга хранит даты, используя календарь японского императора, а система получателя ожидает дату в формате ISO, например `2024-04-01`.  

В этом руководстве мы пройдем полный, готовый к запуску пример, который читает ячейку, интерпретирует японскую эру и **выводит дату yyyy‑mm‑dd**. К концу вы точно будете знать, как **отобразить дату в формате ISO** в любом приложении .NET, и у вас будет переиспользуемый фрагмент кода, который можно вставить в свой проект.

## Что понадобится

- **.NET 6+** (or .NET Framework 4.7.2+).  
- **Aspose.Cells for .NET** – библиотека, позволяющая задать пользовательский календарь при загрузке рабочей книги.  
- Excel‑файл (`japan-date.xlsx`), содержащий дату, записанную в ячейке с японской эрой (например, `令和3年4月1日`).  
- Любимая IDE — Visual Studio, Rider или даже VS Code подойдёт.

Дополнительные пакеты NuGet не требуются, помимо Aspose.Cells, и код работает на Windows, Linux или macOS.

## Шаг 1: Настройте проект и установите Aspose.Cells

```bash
dotnet new console -n ExcelDateDemo
cd ExcelDateDemo
dotnet add package Aspose.Cells
```

> **Pro tip:** Если вы работаете на CI‑сервере, зафиксируйте версию пакета (`Aspose.Cells 23.12`), чтобы обеспечить воспроизводимые сборки.

## Шаг 2: Загрузите рабочую книгу с календарём японского императора

Ключ к **извлечению даты из Excel**, когда источник использует не‑григорианский календарь, — указать Aspose.Cells, какой календарь применять при загрузке. Мы делаем это с помощью `LoadOptions.Calendar`.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 2: Create load options and set the Japanese Emperor calendar
        LoadOptions loadOptions = new LoadOptions
        {
            // This tells Aspose.Cells to interpret era dates correctly
            Calendar = new JapaneseEmperorCalendar()
        };

        // Step 3: Open the workbook that contains Japanese era dates
        // Replace the path with the actual location of your Excel file
        string filePath = @"YOUR_DIRECTORY\japan-date.xlsx";
        Workbook workbook = new Workbook(filePath, loadOptions);
```

**Почему это важно:** Без пользовательского календаря Aspose.Cells будет рассматривать ячейку как обычную строку, и информация об эпохе будет потеряна. При присвоении `JapaneseEmperorCalendar` библиотека автоматически преобразует `令和3年4月1日` в `2021‑04‑01` за кулисами.

## Шаг 3: Получите дату из конкретной ячейки

Теперь, когда рабочая книга знает, как интерпретировать эпоху, мы можем прочитать ячейку как `DateTime`. Предположим, что дата находится в первом листе, ячейка **A1** (строка 0, столбец 0).

```csharp
        // Step 4: Retrieve the date value from the first worksheet, first cell
        Worksheet sheet = workbook.Worksheets[0];
        Cell dateCell = sheet.Cells[0, 0]; // A1

        // GetDateTime() returns a System.DateTime object
        DateTime extractedDate = dateCell.GetDateTime();
```

Если ячейка пуста или содержит значение, не являющееся датой, `GetDateTime()` бросит исключение. Защитный подход выглядит так:

```csharp
        if (dateCell.Type != CellValueType.IsDateTime)
        {
            Console.WriteLine("The target cell does not contain a valid date.");
            return;
        }

        DateTime extractedDate = dateCell.GetDateTime();
```

**Особый случай:** Некоторые старые файлы Excel хранят даты в виде чисел (серийные даты). Aspose.Cells обрабатывает их автоматически, но всё равно следует проверять тип ячейки, если ожидается смешанное содержимое.

## Шаг 4: Выведите дату yyyy‑mm‑dd (ISO) и проверьте

Имея `DateTime`, форматировать её как **output date yyyy‑mm‑dd** — это однострочник:

```csharp
        // Step 5: Output the date in ISO format (yyyy‑mm‑dd)
        string isoDate = extractedDate.ToString("yyyy-MM-dd");
        Console.WriteLine($"Extracted date (ISO): {isoDate}");
    }
}
```

Запуск программы с файлом, содержащим `令和3年4月1日`, выведет:

```
Extracted date (ISO): 2021-04-01
```

Это точный **display date iso format**, требуемый многими API.

## Полный рабочий пример

Собрав все части вместе, представляем полностью готовую к копированию программу:

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Load the workbook with Japanese era support
        LoadOptions loadOptions = new LoadOptions
        {
            Calendar = new JapaneseEmperorCalendar()
        };

        string filePath = @"YOUR_DIRECTORY\japan-date.xlsx";
        Workbook workbook = new Workbook(filePath, loadOptions);

        // Access the cell that holds the date (A1)
        Worksheet sheet = workbook.Worksheets[0];
        Cell dateCell = sheet.Cells[0, 0];

        // Validate the cell contains a date
        if (dateCell.Type != CellValueType.IsDateTime)
        {
            Console.WriteLine("The target cell does not contain a valid date.");
            return;
        }

        // Extract the DateTime value
        DateTime extractedDate = dateCell.GetDateTime();

        // Convert to ISO format (yyyy‑mm‑dd)
        string isoDate = extractedDate.ToString("yyyy-MM-dd");
        Console.WriteLine($"Extracted date (ISO): {isoDate}");
    }
}
```

> **Note:** Замените `YOUR_DIRECTORY` на реальную папку, содержащую `japan-date.xlsx`. Код работает с любым листом и любой ячейкой — просто скорректируйте индексы.

## Обработка других календарей (необязательно)

Если вам когда‑нибудь понадобится **извлечь дату из Excel**, использующую тайский буддийский календарь или еврейский календарь, просто замените экземпляр календаря:

```csharp
loadOptions.Calendar = new ThaiBuddhistCalendar();   // for Thai dates
// or
loadOptions.Calendar = new HebrewCalendar();         // for Hebrew dates
```

Остальная часть логики остаётся неизменной, что демонстрирует гибкость подхода.

## Распространённые подводные камни и как их избежать

| Проблема | Почему происходит | Решение |
|----------|-------------------|---------|
| `GetDateTime()` throws `InvalidCastException` | Ячейка не является датой (возможно, строка) | Проверьте `Cell.Type` перед вызовом или используйте `DateTime.TryParse` для `Cell.StringValue`. |
| Неправильный год после преобразования | Рабочая книга загружена без установки `Calendar` | Всегда создавайте `LoadOptions` с нужным календарём **до** открытия файла. |
| ISO‑вывод показывает часть времени (`2021-04-01 00:00:00`) | Использован `ToString()` без строки формата | Используйте спецификатор формата `"yyyy-MM-dd"` чтобы принудительно вывести **output date yyyy‑mm‑dd**. |
| Файл не найден | Относительный путь указывает на неправильную папку | Используйте `Path.Combine(Environment.CurrentDirectory, "japan-date.xlsx")` или укажите абсолютный путь. |

## Pro‑советы для кода, готового к продакшн

1. **Кешируйте рабочую книгу**, если нужно читать много дат из одного файла — открытие книги относительно дорого.  
2. **Оберните логику извлечения** в переиспользуемый метод:

   ```csharp
   static string ExtractIsoDate(string file, int sheetIdx, int row, int col)
   {
       var opts = new LoadOptions { Calendar = new JapaneseEmperorCalendar() };
       var wb = new Workbook(file, opts);
       var cell = wb.Worksheets[sheetIdx].Cells[row, col];
       if (cell.Type != CellValueType.IsDateTime) return null;
       return cell.GetDateTime().ToString("yyyy-MM-dd");
   }
   ```

3. **Записывайте оригинальную строку эпохи** (`cell.StringValue`) вместе с ISO‑выводом для аудита.  
4. **Проводите unit‑тесты** метода с несколькими жёстко закодированными Excel‑файлами, охватывающими разные эпохи (Heisei, Reiwa), чтобы гарантировать корректность.

## Визуальный обзор

Ниже представлена быстрая диаграмма, иллюстрирующая поток данных — от ячейки Excel к ISO‑строке.  

![Пример извлечения даты из Excel, показывающий Excel → LoadOptions → DateTime → ISO строку]  

*Alt text: «extract date from excel» диаграмма, отображающая конвейер преобразования.*

## Заключение

Мы рассмотрели всё, что нужно, чтобы **извлечь дату из Excel**, обработать значения японской эры и **вывести дату yyyy‑mm‑dd**, чтобы она соответствовала **display date iso format**, который любят современные API. Решение автономно, работает с любой версией .NET, поддерживающей Aspose.Cells, и может быть расширено на другие календари одной заменой строки.

Есть другой календарь в виду? Или вы извлекаете даты из нескольких столбцов? Не стесняйтесь изменить вспомогательный метод `ExtractIsoDate` или оставить комментарий ниже. Приятного кодинга, и пусть ваши даты всегда находятся в идеальном синхроне с ISO!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}