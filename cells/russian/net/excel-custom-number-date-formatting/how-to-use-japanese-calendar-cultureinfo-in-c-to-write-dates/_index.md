---
category: general
date: 2026-10-26
description: Узнайте, как использовать CultureInfo японского календаря в C# при разборе
  дат эпох и вставке их в рабочий лист Excel с помощью NPOI.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- use japanese calendar cultureinfo
- japanese era date parsing
- cultureinfo with japanese calendar
- datetime parse with cultureinfo
- npoi excel cultureinfo
language: ru
lastmod: 2026-10-26
og_description: Используйте CultureInfo японского календаря в C# для разбора дат эпохи
  Рэйва и записи их в лист Excel. Полный, исполняемый код с пояснениями.
og_image_alt: Screenshot of C# code parsing a Japanese era date and inserting it into
  an Excel cell
og_title: Использовать CultureInfo японского календаря в C# — полный пример Excel
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn how to use Japanese calendar CultureInfo in C# when parsing era
    dates and inserting them into an Excel worksheet with NPOI.
  headline: How to use Japanese calendar CultureInfo in C# to write dates to Excel
  type: TechArticle
tags:
- C#
- CultureInfo
- Excel
- NPOI
- Internationalization
title: Как использовать CultureInfo японского календаря в C# для записи дат в Excel
url: /ru/net/excel-custom-number-date-formatting/how-to-use-japanese-calendar-cultureinfo-in-c-to-write-dates/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как использовать CultureInfo японского календаря в C# для записи дат в Excel

Если вам нужно **использовать CultureInfo японского календаря** при работе с датами в C#, это руководство покажет, как это сделать. Вы научитесь разбирать строку даты, содержащую название японской эры (например, *Reiwa 2/5/1*), а затем записывать полученный `DateTime` в первую ячейку листа Excel с помощью библиотеки NPOI.

Разбор дат, основанных на эре, без правильного `CultureInfo` приводит к `FormatException` или неверным значениям месяца/дня. Настроив `CultureInfo` на японский календарь, вы гарантируете, что среда выполнения .NET правильно интерпретирует эру, и что значение, сохраняемое в Excel, соответствует оригинальному японскому обозначению.

В этом руководстве вы:

* Создадите объект `CultureInfo`, использующий японский календарь.
* Разберёте строку даты с японской эрой с помощью `DateTime.Parse`.
* Вставите полученный `DateTime` в ячейку листа NPOI.
* Посмотрите полный, исполняемый пример программы и ожидаемый вывод.

> **Prerequisites** – .NET 6.0+ (или .NET Core 3.1+), пакет **NPOI** NuGet, а также базовые знания C# и работы с файлами Excel.

---

## Что вам понадобится

| Item | Reason |
|------|--------|
| **.NET SDK** (6.0 или новее) | Предоставляет среду выполнения и библиотеки для `CultureInfo`. |
| **NPOI** (`NPOI` NuGet package) | Позволяет создавать и изменять файлы Excel без установленного Office. |
| **Visual Studio Code**, **Visual Studio** или любой IDE для C# | Для компиляции и запуска примера. |
| **Строка даты с японской эрой** (например, `"Reiwa 2/5/1"`) | Демонстрирует использование японского календаря. |

---

## Шаг 1: Установить NPOI

Откройте терминал в папке проекта и выполните:

```bash
dotnet add package NPOI --version 2.6.1
```

Пакет предоставляет типы `IWorkbook`, `ISheet` и `ICell`, которые будут использованы позже.

---

## Шаг 2: Создать CultureInfo, использующий японский календарь

Японский календарь — это календарь, основанный на эпохах. Необходимо запросить *японскую* вариацию локали `ja-JP` и явно установить календарь `JapaneseCalendar`.

```csharp
using System;
using System.Globalization;

// Create a CultureInfo based on Japanese locale and switch its calendar.
CultureInfo japaneseCulture = new CultureInfo("ja-JP");
japaneseCulture.DateTimeFormat.Calendar = new JapaneseCalendar();
```

> **Why this matters** – По умолчанию культура `ja-JP` использует григорианский календарь. Переустановка свойства `Calendar` гарантирует, что такие названия эпох, как *Reiwa*, будут распознаны при разборе.

---

## Шаг 3: Разобрать строку даты с японской эрой

Теперь, когда `CultureInfo` настроен, вы можете безопасно разобрать строку, содержащую название эпохи.

```csharp
// Example Japanese era date: Reiwa 2 (2020) year, May 1st.
string eraDate = "Reiwa 2/5/1";

// Parse using the Japanese CultureInfo created earlier.
DateTime reiwaDate = DateTime.Parse(eraDate, japaneseCulture);
Console.WriteLine($"Parsed DateTime (UTC): {reiwaDate:u}");
```

**Output**

```
Parsed DateTime (UTC): 2020-05-01 00:00:00Z
```

Метод `Parse` интерпретирует *Reiwa 2* как григорианский год 2020, месяц 5, день 1.

### Edge case: handling invalid eras

Если пользователь передаёт неподдерживаемую эпоху (например, `"Heisei 31/4/30"` после завершения эпохи Хэйсэй), `DateTime.Parse` бросает `FormatException`. Оберните вызов в блок try‑catch, чтобы вывести понятное сообщение об ошибке:

```csharp
try
{
    DateTime parsed = DateTime.Parse(input, japaneseCulture);
}
catch (FormatException)
{
    Console.Error.WriteLine($"'{input}' is not a valid Japanese era date.");
}
```

---

## Шаг 4: Записать разобранный DateTime в лист Excel

С готовым объектом `DateTime` вы можете сохранить его в ячейку Excel. NPOI автоматически форматирует значения `DateTime` как даты Excel.

```csharp
using NPOI.SS.UserModel;
using NPOI.XSSF.UserModel;
using System.IO;

// Create a new workbook and a sheet.
IWorkbook workbook = new XSSFWorkbook();
ISheet sheet = workbook.CreateSheet("Japanese Dates");

// Write the DateTime into cell A1 (row 0, column 0).
IRow row = sheet.CreateRow(0);
ICell cell = row.CreateCell(0);
cell.SetCellValue(reiwaDate);

// Optionally apply a date style that shows the era (Excel does not have a built‑in era format,
// so we keep the Gregorian representation).
ICellStyle dateStyle = workbook.CreateCellStyle();
short dateFormatId = workbook.CreateDataFormat().GetFormat("yyyy-mm-dd");
dateStyle.DataFormat = dateFormatId;
cell.CellStyle = dateStyle;

// Save the workbook to a file.
using (FileStream fs = new FileStream("JapaneseEraDate.xlsx", FileMode.Create, FileAccess.Write))
{
    workbook.Write(fs);
}
Console.WriteLine("Excel file 'JapaneseEraDate.xlsx' created successfully.");
```

**Result** – При открытии *JapaneseEraDate.xlsx* в ячейке A1 будет отображаться дата **2020‑05‑01**.

### Почему использовать NPOI?

*Works on any platform* (Windows, Linux, macOS) и **не** требует Microsoft Office. Это делает решение подходящим для CI‑конвейеров, Docker‑контейнеров или серверной обработки.

---

## Шаг 5: Полная, исполняемая программа

Объединив всё вместе, получаем полностью готовое консольное приложение, демонстрирующее весь процесс:

```csharp
// File: Program.cs
using System;
using System.Globalization;
using System.IO;
using NPOI.SS.UserModel;
using NPOI.XSSF.UserModel;

class Program
{
    static void Main()
    {
        // 1️⃣ Configure CultureInfo for the Japanese calendar.
        CultureInfo japaneseCulture = new CultureInfo("ja-JP");
        japaneseCulture.DateTimeFormat.Calendar = new JapaneseCalendar();

        // 2️⃣ Parse a Japanese era date string.
        string eraDate = "Reiwa 2/5/1";
        DateTime reiwaDate;
        try
        {
            reiwaDate = DateTime.Parse(eraDate, japaneseCulture);
            Console.WriteLine($"Parsed DateTime: {reiwaDate:u}");
        }
        catch (FormatException)
        {
            Console.Error.WriteLine($"'{eraDate}' is not a valid Japanese era date.");
            return;
        }

        // 3️⃣ Create an Excel workbook and write the date.
        IWorkbook workbook = new XSSFWorkbook();
        ISheet sheet = workbook.CreateSheet("Japanese Dates");
        IRow row = sheet.CreateRow(0);
        ICell cell = row.CreateCell(0);
        cell.SetCellValue(reiwaDate);

        // Apply a simple Gregorian date format.
        ICellStyle style = workbook.CreateCellStyle();
        short fmt = workbook.CreateDataFormat().GetFormat("yyyy-mm-dd");
        style.DataFormat = fmt;
        cell.CellStyle = style;

        // 4️⃣ Save the workbook.
        const string fileName = "JapaneseEraDate.xlsx";
        using (FileStream fs = new FileStream(fileName, FileMode.Create, FileAccess.Write))
        {
            workbook.Write(fs);
        }

        Console.WriteLine($"Excel file '{fileName}' created successfully.");
    }
}
```

**How to run**

```bash
dotnet run
```

После выполнения вы найдёте `JapaneseEraDate.xlsx` в папке проекта с правильно разобранной датой.

---

## Распространённые ошибки и рекомендации по лучшим практикам

| Pitfall | Fix / Recommendation |
|---------|----------------------|
| Forgetting to set `japaneseCulture.DateTimeFormat.Calendar` | Always assign a `JapaneseCalendar` instance; otherwise the era name is not recognized. |
| Using `DateTime.TryParse` without the custom `CultureInfo` | Pass the same `japaneseCulture` to `TryParse` to keep behavior consistent. |
| Expecting Excel to display the era name | Excel’s built‑in date formats are Gregorian only. If you need the era displayed, store the original string in a separate column or create a custom text format. |
| Not disposing the `FileStream` | Use a `using` block (as shown) to ensure the file handle is released promptly. |
| Mixing `CultureInfo` objects across threads | `CultureInfo` is thread‑safe for read‑only operations, but avoid modifying its `Calendar` property after initial setup. |

---

## Заключение

Теперь вы знаете, как **использовать CultureInfo японского календаря** в C# для точного разбора дат с японскими эпохами и записи полученного `DateTime` в лист Excel с помощью NPOI. Полный пример охватывает настройку, разбор, обработку ошибок и вывод в Excel, предоставляя надёжную основу для любой интернационализированной отчётности или обмена данными.

Далее вы можете изучить:

* **Форматирование дат пользовательским текстом**, чтобы сохранить название эпохи внутри Excel.
* **Чтение дат из Excel** с помощью `cell.DateCellValue`, учитывая японский календарь.
* **Применение той же техники** к другим календарям, основанным на эпохах (например, тайскому буддийскому календарю), заменив `JapaneseCalendar` на соответствующий подкласс `Calendar`.

Не стесняйтесь экспериментировать с различными строками эпох, большими наборами данных или интегрировать эту логику в ASP.NET Core API, генерирующие Excel‑отчёты «на лету». Приятного кодинга!

## Что следует изучить дальше?

Следующие руководства охватывают тесно связанные темы, построенные на техниках, продемонстрированных в этом руководстве. Каждый ресурс включает полностью рабочие примеры кода с пошаговыми объяснениями, помогающими освоить дополнительные возможности API и исследовать альтернативные подходы в ваших проектах.

- [Создать книгу Excel с датами японского календаря – Полное руководство](/cells/english/net/excel-custom-number-date-formatting/create-excel-workbook-with-japanese-calendar-dates-full-guid/)
- [Разбор дат японских эпох в Excel – Полное руководство для разработчиков C#](/cells/english/net/data-loading-and-parsing/parse-japanese-era-dates-in-excel-full-guide-for-c-developer/)
- [Как создать книгу Excel и разобрать японские даты в C#](/cells/english/net/excel-custom-number-date-formatting/how-to-create-excel-workbook-and-parse-japanese-dates-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}