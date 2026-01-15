---
category: general
date: 2026-01-14
description: Экспорт таблицы в CSV на C# и изучите, как задать пользовательский числовой
  формат, записать CSV в файл и включить автоматический расчёт — всё в одном руководстве.
draft: false
keywords:
- export table to csv
- set custom number format
- write csv to file
- enable automatic calculation
- how to format numbers
language: ru
og_description: Экспортировать таблицу в CSV с пользовательскими форматами чисел,
  записать CSV в файл и включить автоматический расчёт, используя Aspose.Cells в C#.
og_title: Экспорт таблицы в CSV – Полное руководство по C#
tags:
- Aspose.Cells
- C#
- CSV export
- Excel automation
title: Экспорт таблицы в CSV – полное руководство по C# с пользовательскими форматами
  чисел
url: /ru/net/csv-file-handling/export-table-to-csv-complete-c-guide-with-custom-number-form/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Экспорт таблицы в CSV – Полное руководство по C# с пользовательскими числовыми форматами

Когда‑нибудь вам нужно было **export table to CSV**, но вы не знали, как сохранить числа аккуратными? Вы не одиноки. Во многих сценариях экспорта данных вы хотите, чтобы числа были отформатированы красиво, CSV записывался на диск, а книга оставалась синхронной с формулами. Этот учебник покажет вам точно **how to export table to CSV**, как **set custom number format**, как **write CSV to file**, и как **enable automatic calculation**, чтобы всё оставалось.

Мы пройдём реальный пример с использованием Aspose.Cells for .NET. К концу этого руководства у вас будет единая, исполняемая программа C#, которая:

* Форматирует ячейку с пользовательским числовым шаблоном (часть “how to format numbers”).
* Экспортирует таблицу первого листа в строку CSV с выбранным вами разделителем.
* Сохраняет эту строку CSV в файл на диске.
* Разбирает дату в японской эре и записывает её обратно в лист.
* Включает автоматический расчёт, чтобы формулы динамического массива всегда пересчитывались.

Никаких внешних ссылок не требуется — просто скопируйте, вставьте и запустите.

![Export table to CSV illustration](export-table-to-csv.png "Диаграмма экспорта таблицы в CSV"){: alt="Диаграмма экспорта таблицы в CSV, показывающая книгу, таблицу и вывод CSV"}

---

## Что понадобится

* **Aspose.Cells for .NET** (пакет NuGet `Aspose.Cells`). Код работает с версией 23.9 или новее.
* Среда разработки .NET (Visual Studio, Rider или `dotnet CLI`).
* Базовое знакомство с синтаксисом C# — ничего сложного, только обычные операторы `using` и метод `Main`.

## Шаг 1 – Установить пользовательский числовой формат (How to Format Numbers)

Прежде чем экспортировать что‑либо, убедимся, что числа отображаются так, как нам нужно. Свойство `Custom` объекта `Style` позволяет задать шаблон, например `"0.####"`, чтобы показывать до четырёх десятичных знаков, отбрасывая конечные нули.

```csharp
using Aspose.Cells;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new workbook and grab the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ Put a raw double value into cell A1
        worksheet.Cells[0, 0].PutValue(123.456789);

        // 3️⃣ Define a custom number format – this is the “how to format numbers” piece
        Style numberStyle = workbook.CreateStyle();
        numberStyle.Custom = "0.####"; // up to 4 significant digits
        worksheet.Cells[0, 0].SetStyle(numberStyle);
```

**Почему это важно:**  
Когда вы позже экспортируете таблицу в CSV, необработанное значение double `123.456789` будет отображено как `123.456789`. С пользовательским форматом CSV будет содержать `123.4568` (округлено до четырёх знаков после запятой) — именно то, что ожидают большинство инструментов отчётности.

## Шаг 2 – Экспортировать таблицу в CSV (Основная цель)

Aspose.Cells рассматривает диапазон данных как `Table`. Даже если вы явно не создали её, первый лист всегда содержит таблицу по умолчанию с индексом 0. Экспорт этой таблицы — однострочник, как только вы настроите `ExportTableOptions`.

```csharp
        // 4️⃣ Grab the first table in the worksheet
        Table firstTable = worksheet.Tables[0];

        // 5️⃣ Configure export options – we want a CSV string, comma‑delimited
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            Delimiter = ","
        };

        // 6️⃣ Export to a CSV string
        string csvContent = firstTable.ExportToString(exportOptions);

        // Show what we got (optional debug output)
        Console.WriteLine("=== CSV CONTENT ===");
        Console.WriteLine(csvContent);
```

**Ожидаемый вывод CSV** (с учётом пользовательского формата из Шага 1):

```
123.4568
```

Обратите внимание, как число соблюдает шаблон `"0.####"`, который мы задали ранее. Это магия **export table to csv**, объединённая с пользовательским числовым стилем.

## Шаг 3 – Записать CSV в файл (Сохранить данные)

Теперь, когда у нас есть строка CSV, её нужно сохранить. Метод `File.WriteAllText` справляется с задачей, и мы можем разместить файл где угодно — просто замените `"YOUR_DIRECTORY"` на реальный путь.

```csharp
        // 7️⃣ Define where to save the CSV file
        string outputPath = Path.Combine(
            Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
            "table.csv");

        // 8️⃣ Write the CSV string to disk – this is the “write csv to file” step
        File.WriteAllText(outputPath, csvContent);
        Console.WriteLine($"CSV file written to: {outputPath}");
```

**Подсказка:** Если нужен другой разделитель (точка с запятой, табуляция, вертикальная черта), просто измените `Delimiter` в `ExportTableOptions`. Остальная часть кода остаётся прежней, что делает адаптацию тривиальной.

## Шаг 4 – Разобрать дату в японской эре (Дополнительный интересный момент)

Часто понадобится работать с датами, специфичными для локали. Aspose.Cells поставляется с `DateTimeParser`, который понимает строки японской эры, такие как `"R02/04/01"` (Reiwa 2 = 2020). Давайте поместим эту дату в следующую строку.

```csharp
        // 9️⃣ Set up a parser for Japanese‑era dates
        DateTimeParser eraParser = new DateTimeParser { Calendar = CalendarType.JapaneseEra };
        DateTime reiwaDate = eraParser.Parse("R02/04/01"); // 2020‑04‑01

        // 10️⃣ Write the parsed date into cell A2
        worksheet.Cells[1, 0].PutValue(reiwaDate);
```

Ячейка теперь содержит истинное значение `DateTime`, которое Excel (или любой просмотрщик) отобразит в соответствии с региональными настройками книги.

## Шаг 5 – Включить автоматический расчёт (Обновить формулы)

Если ваша книга содержит формулы — особенно формулы динамического массива — вам понадобится их автоматический пересчёт после изменения данных. Переключение режима расчёта — это изменение одного свойства.

```csharp
        // 11️⃣ Turn on automatic calculation so formulas stay up‑to‑date
        workbook.Settings.CalcMode = CalculationMode.Automatic;

        // 12️⃣ Force a calculation pass (optional but ensures everything is up‑to‑date now)
        workbook.CalculateFormula();

        // Cleanup: save the workbook if you want to inspect it later
        string xlsPath = Path.Combine(
            Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
            "demo.xlsx");
        workbook.Save(xlsPath);
        Console.WriteLine($"Workbook saved to: {xlsPath}");
    }
}
```

**Зачем включать автоматический расчёт?**  
Когда вы позже откроете `demo.xlsx` в Excel, любые формулы, ссылающиеся на число с пользовательским форматом или дату в японской эре, уже отразят последние значения. Это часть нашего руководства «enable automatic calculation».

## Полный рабочий пример (Все шаги вместе)

Ниже представлен полный готовый к копированию и вставке код программы. Ничего не пропущено; просто запустите её и наблюдайте вывод в консоли и появление файлов на рабочем столе.

```csharp
using Aspose.Cells;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // Create workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Set a number with a custom format (how to format numbers)
        worksheet.Cells[0, 0].PutValue(123.456789);
        Style numberStyle = workbook.CreateStyle();
        numberStyle.Custom = "0.####";
        worksheet.Cells[0, 0].SetStyle(numberStyle);

        // Export the first table to CSV (export table to csv)
        Table firstTable = worksheet.Tables[0];
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            Delimiter = ","
        };
        string csvContent = firstTable.ExportToString(exportOptions);
        Console.WriteLine("=== CSV CONTENT ===");
        Console.WriteLine(csvContent);

        // Write CSV to file (write csv to file)
        string csvPath = Path.Combine(
            Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
            "table.csv");
        File.WriteAllText(csvPath, csvContent);
        Console.WriteLine($"CSV file written to: {csvPath}");

        // Parse a Japanese‑era date and write it to the sheet
        DateTimeParser eraParser = new DateTimeParser { Calendar = CalendarType.JapaneseEra };
        DateTime reiwaDate = eraParser.Parse("R02/04/01");
        worksheet.Cells[1, 0].PutValue(reiwaDate);

        // Enable automatic calculation (enable automatic calculation)
        workbook.Settings.CalcMode = CalculationMode.Automatic;
        workbook.CalculateFormula();

        // Save the workbook for inspection
        string xlsPath = Path.Combine(
            Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
            "demo.xlsx");
        workbook.Save(xlsPath);
        Console.WriteLine($"Workbook saved to: {xlsPath}");
    }
}
```

**Контрольный список результатов**

| ✅ | Что вы должны увидеть |
|---|------------------------|
| CSV‑файл `table.csv` на рабочем столе, содержащий `123.4568` |
| Excel‑файл `demo.xlsx` на рабочем столе с числом в пользовательском формате в A1 и датой в японской эре (2020‑04‑01) в A2 |
| Вывод в консоли, подтверждающий каждый шаг |

## Часто задаваемые вопросы и особые случаи

**В: Что если в моей таблице есть заголовки?**  
**О:** `ExportTableOptions` учитывает свойство `ShowHeaders` таблицы. Установите `firstTable.ShowHeaders = true;` перед экспортом, и CSV автоматически включит строку заголовков.

**В: Можно ли экспортировать несколько таблиц одновременно?**  
**О:** Конечно. Пройдитесь в цикле по `worksheet.Tables` и объедините строки CSV, либо сохраните каждую в отдельный файл. Не забудьте скорректировать `Delimiter`, если нужен иной разделитель для каждого файла.

**В: Моим числам нужен разделитель тысяч (например, `1,234.56`).**  
**О:** Измените пользовательский формат на `"#,##0.##"`, и экспортированный CSV будет содержать запятые. Учтите, что некоторые парсеры CSV воспринимают запятые как разделители, поэтому вы можете переключиться на точку с запятой (`Delimiter = ";"`), чтобы избежать путаницы.

**В: Я нацелен на .NET 6 — есть ли проблемы совместимости?**  
**О:** Нет. Aspose.Cells 23.9+ ориентирован на .NET Standard 2.0+, поэтому отлично работает с .NET 6, .NET 7 и даже .NET Framework 4.8.

## Итоги

Мы рассмотрели, как **export table to csv**, сохраняя **custom number format**, как **write csv to file**, и как **enable automatic calculation**, чтобы ваша книга оставалась синхронной. Мы также быстро продемонстрировали разбор японской…

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}