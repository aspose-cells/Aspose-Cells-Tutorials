---
category: general
date: 2026-10-01
description: Преобразуйте дату японской эры в григорианскую DateTime с помощью Aspose.Cells
  в C#. Узнайте, как быстро конвертировать японский календарь.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert japanese era date
- how to convert japanese calendar
language: ru
lastmod: 2026-10-01
og_description: Преобразовать дату японской эры в григорианскую DateTime в C#. Этот
  учебник объясняет, как точно преобразовать японский календарь с помощью Aspose.Cells.
og_image_alt: Code example converting a Japanese era date string to a Gregorian DateTime
  in a C# console app
og_title: Преобразование даты японской эры в григорианскую в C# – пошаговое руководство
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: convert japanese era date to a Gregorian DateTime using Aspose.Cells
    in C#. Learn how to convert japanese calendar quickly.
  headline: How to convert Japanese era date to Gregorian in C#
  type: TechArticle
- description: convert japanese era date to a Gregorian DateTime using Aspose.Cells
    in C#. Learn how to convert japanese calendar quickly.
  name: How to convert Japanese era date to Gregorian in C#
  steps:
  - name: Why each step matters
    text: '| Step | Purpose | How it helps the conversion | |------|---------|-----------------------------|
      | **Create workbook** | Provides a container that understands Excel formulas
      and date systems. | The library’s internal date engine is activated only inside
      a workbook. | | **Insert era string** | Suppl'
  - name: Handling invalid or ambiguous strings
    text: '* **Invalid era name** – Aspose.Cells throws a `FormatException`. Wrap
      the conversion in `try/catch` to provide a friendly error message. * **Missing
      year/month/day** – The library expects a full “Era Year/Month/Day” pattern.
      If you receive partial data, prepend missing parts or reject the input ear'
  - name: Next steps
    text: '* Explore **formatting options** to write the Gregorian date back into
      the worksheet with a custom number format. * Combine this conversion with **data
      import pipelines** (e.g., reading CSV files that contain era dates). * Review
      other Aspose.Cells features such as **date arithmetic** and **regional'
  type: HowTo
tags:
- Aspose.Cells
- C#
- date conversion
title: Как преобразовать дату в японской эре в григорианскую в C#
url: /ru/net/excel-custom-number-date-formatting/how-to-convert-japanese-era-date-to-gregorian-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как конвертировать дату японской эры в григорианскую в C#

Если вам нужно **конвертировать дату японской эры** в григорианскую в C#, это руководство покажет, как это сделать. Независимо от того, обрабатываете ли вы устаревшие данные, читаете ввод пользователя или генерируете отчёты, библиотека Aspose.Cells делает преобразование простым. Кроме того, вы узнаете лучший способ **как конвертировать японский календарь** при работе с электронными таблицами.

В этом учебнике рассматривается каждый шаг — от создания рабочей книги до получения значения `DateTime` — чтобы вы могли скопировать‑вставить полностью готовую, исполняемую программу. Внешняя документация не требуется; просто следуйте коду и объяснениям ниже.

## Предварительные требования

* .NET 6.0 или новее (код также работает с .NET Framework 4.6+)
* Лицензия на **Aspose.Cells** (бесплатная пробная версия подходит для тестирования)
* Среда разработки, например Visual Studio 2022 или VS Code
* Базовые знания C# консольных приложений

## Конвертация даты японской эры с помощью Aspose.Cells

Суть преобразования реализована несколькими простыми вызовами API. Aspose.Cells автоматически интерпретирует строки японской эры (например, «Reiwa 2/04/01») и предоставляет результат в виде объекта `DateTime` после пересчёта листа.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook and get the first worksheet
        var workbook = new Workbook();                // creates an empty Excel file in memory
        var worksheet = workbook.Worksheets[0];       // the default sheet is at index 0

        // Step 2: Insert a Japanese era date string into cell A1
        // The string follows the Japanese calendar format: Era Year/Month/Day
        worksheet.Cells[0, 0].PutValue("Reiwa 2/04/01");

        // Step 3: Apply a default style to the cell (required for proper calculation)
        // Without a style, Aspose.Cells may treat the content as plain text and skip conversion.
        worksheet.Cells[0, 0].SetStyle(workbook.CreateStyle());

        // Step 4: Recalculate the worksheet so the date string is converted to a Gregorian date
        // The Calculate method parses the era string and updates the cell's internal value.
        worksheet.Calculate();

        // Step 5: Retrieve and display the converted DateTime value (2020‑04‑01)
        DateTime gregorian = worksheet.Cells[0, 0].DateTimeValue;
        Console.WriteLine($"Gregorian date: {gregorian:yyyy-MM-dd}");
    }
}
```

### Почему каждый шаг важен

| Шаг | Назначение | Как это помогает преобразованию |
|------|------------|---------------------------------|
| **Create workbook** | Предоставляет контейнер, понимающий формулы Excel и системы дат. | Внутренний движок дат библиотеки активируется только внутри рабочей книги. |
| **Insert era string** | Предоставляет исходный текст японского календаря, который нужно преобразовать. | Aspose.Cells распознаёт названия эпох, такие как *Reiwa*, *Heisei*, *Showa* и т.д. |
| **Set style** | Принуждает ячейку рассматривать как ячейку со значением, а не как литеральную строку. | Без стиля метод `Calculate` может игнорировать ячейку, оставив текст без изменений. |
| **Calculate** | Запускает разбор строки эпохи и преобразование во внутренний серийный номер даты. | Библиотека преобразует «Reiwa 2/04/01» → серийный номер → григорианский `DateTime`. |
| **Read `DateTimeValue`** | Возвращает преобразованный объект .NET `DateTime`. | Теперь у вас есть стандартный `DateTime`, который можно использовать в любом .NET API. |

## Как конвертировать японский календарь в других сценариях

Тот же подход работает для любого названия японской эры, поддерживаемого Aspose.Cells:

```csharp
// Example: converting a Heisei era date
worksheet.Cells[0, 0].PutValue("Heisei 30/12/31"); // corresponds to 2018‑12‑31
worksheet.Calculate();
Console.WriteLine(worksheet.Cells[0, 0].DateTimeValue); // 2018-12-31
```

### Обработка недопустимых или неоднозначных строк

* **Invalid era name** – Aspose.Cells бросает `FormatException`. Оберните преобразование в `try/catch`, чтобы предоставить понятное сообщение об ошибке.
* **Missing year/month/day** – Библиотека ожидает полный шаблон «Era Year/Month/Day». Если получены частичные данные, добавьте недостающие части или отклоните ввод сразу.
* **Different locale settings** – Преобразование **не** зависит от текущей культуры потока; всегда используется карта японских эпох, встроенная в Aspose.Cells. Это делает метод безопасным для серверной обработки.

```csharp
try
{
    worksheet.Cells[0, 0].PutValue(userInput);
    worksheet.Calculate();
    DateTime result = worksheet.Cells[0, 0].DateTimeValue;
    // Use result...
}
catch (FormatException ex)
{
    Console.WriteLine($"Unable to parse Japanese era date: {ex.Message}");
}
```

## Практические советы и распространённые подводные камни

* **Always call `SetStyle`** before `Calculate`. Пропуск этого шага часто приводит к ошибкам, поскольку ячейка остаётся простым текстовым контейнером.
* **Reuse the same workbook** if you need to convert many dates. Повторное использование одной рабочей книги при необходимости конвертировать множество дат уменьшает лишние затраты.
* **Batch conversion** – Заполните столбец строками эпох, вызовите `worksheet.Calculate()` один раз, затем считайте весь столбец `DateTimeValue`. Это гораздо эффективнее, чем пересчитывать каждую ячейку отдельно.
* **Version compatibility** – Логика конвертации эпох была введена в Aspose.Cells 22.9. Убедитесь, что используете эту версию или новее; более старые версии рассматривают строку как обычный текст.

## Полный рабочий пример (консольное приложение)

Ниже представлена автономная программа, которую можно сразу скомпилировать и запустить. Она демонстрирует конвертацию как Reiwa, так и Heisei, с аккуратной обработкой ошибок.

```csharp
using System;
using Aspose.Cells;

class JapaneseEraConverter
{
    static void Main()
    {
        // Initialize workbook once
        var workbook = new Workbook();
        var sheet = workbook.Worksheets[0];
        var style = workbook.CreateStyle();
        sheet.Cells[0, 0].SetStyle(style);
        sheet.Cells[1, 0].SetStyle(style);

        // Sample inputs
        string[] eraDates = { "Reiwa 2/04/01", "Heisei 30/12/31", "InvalidEra 1/01/01" };

        for (int i = 0; i < eraDates.Length; i++)
        {
            sheet.Cells[i, 0].PutValue(eraDates[i]);
        }

        // Perform conversion for all populated cells
        sheet.Calculate();

        // Output results
        for (int i = 0; i < eraDates.Length; i++)
        {
            try
            {
                DateTime dt = sheet.Cells[i, 0].DateTimeValue;
                Console.WriteLine($"{eraDates[i]} → {dt:yyyy-MM-dd}");
            }
            catch (Exception)
            {
                Console.WriteLine($"{eraDates[i]} → conversion failed");
            }
        }
    }
}
```

**Ожидаемый вывод в консоль**

```
Reiwa 2/04/01 → 2020-04-01
Heisei 30/12/31 → 2018-12-31
InvalidEra 1/01/01 → conversion failed
```

Запуск этой программы подтверждает, что библиотека корректно **конвертирует строки японской эпохи** и аккуратно сообщает о неподдерживаемых значениях.

## Заключение

Теперь вы знаете, как **конвертировать строки японской эпохи** в стандартные григорианские объекты `DateTime` с помощью Aspose.Cells в C#. Процесс сводится к вставке текста эпохи, применению стиля, пересчёту листа и чтению `DateTimeValue`. Следуя указанным шагам, вы также сможете решить более общую задачу **как конвертировать данные японского календаря** массово, обрабатывать ошибки и оптимизировать производительность.

### Следующие шаги

* Изучите **варианты форматирования**, чтобы записать григорианскую дату обратно в лист с пользовательским числовым форматом.
* Скомбинируйте это преобразование с **конвейерами импорта данных** (например, чтение CSV‑файлов, содержащих даты эпох).
* Ознакомьтесь с другими возможностями Aspose.Cells, такими как **аритметика дат** и **региональные настройки**, для более сложных календарных сценариев.

Удачной разработки, и не стесняйтесь адаптировать пример под свои рабочие процессы обработки данных!

## Что стоит изучить дальше?

Следующие учебники охватывают тесно связанные темы, опираясь на техники, продемонстрированные в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [Разбор даты японской эры в C# с Aspose.Cells – Полное руководство](/cells/english/net/excel-custom-number-date-formatting/parse-japanese-era-date-in-c-with-aspose-cells-full-guide/)
- [Включение разбора японской эры в C# с Aspose.Cells](/cells/english/net/workbook-settings/enable-japanese-era-parsing-in-c-with-aspose-cells/)
- [Как создать рабочую книгу и конвертировать строку в дату в C#](/cells/english/net/excel-custom-number-date-formatting/how-to-create-workbook-and-convert-string-to-date-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}