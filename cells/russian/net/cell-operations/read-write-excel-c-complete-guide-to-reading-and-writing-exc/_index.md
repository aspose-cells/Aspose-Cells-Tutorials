---
category: general
date: 2026-03-01
description: Учебник по чтению и записи Excel на C# показывает, как считать значение
  ячейки Excel и записать дату и время в Excel с помощью C# и Aspose.Cells в несколько
  простых шагов.
draft: false
keywords:
- read write excel c#
- read excel cell value
- write datetime to excel
- c# excel interop
- aspnet excel automation
language: ru
og_description: Учебник по чтению и записи Excel на C# объясняет, как считывать значение
  ячейки Excel и записывать дату и время в Excel с понятными примерами кода и лучшими
  практиками.
og_title: Чтение и запись Excel в C# – пошаговое руководство
tags:
- C#
- Excel
- Aspose.Cells
title: Чтение и запись Excel C# – Полное руководство по чтению и записи ячеек Excel
url: /ru/net/cell-operations/read-write-excel-c-complete-guide-to-reading-and-writing-exc/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Чтение и запись Excel C# – Полное руководство по чтению и записи ячеек Excel

Когда‑либо пытались **read write Excel C#** и получали загадочное исключение или несоответствующую дату? Вы не одиноки. Многие разработчики сталкиваются с тем, что нужно извлечь дату в японской эре из листа и затем сохранить корректный `DateTime` обратно в ту же ячейку.  

В этом руководстве мы подробно разберём, как **read excel cell value** и **write datetime to excel** с помощью C# и мощной библиотеки Aspose.Cells. К концу вы получите автономный, готовый к запуску пример, который можно вставить в любой проект .NET.

## Что вы узнаете

- Как установить и подключить Aspose.Cells в проекте .NET 6+.  
- Точный код, необходимый для получения ячейки, содержащей строку японской эры, например `"R3/5/12"`.  
- Как разобрать эту строку в `DateTime`, используя культуру `"ja-JP"`.  
- Шаги для записи полученного `DateTime` обратно в ту же ячейку листа.  
- Советы по обработке граничных случаев, таких как пустые ячейки или неожиданные форматы эры.  

Предыдущий опыт работы с Excel interop не требуется — достаточно базовых знаний C# и .NET. Приступим.

![Скриншот операции read write Excel C# показывающий ячейку B2 до и после преобразования](read-write-excel-csharp.png "пример read write excel c#")

## Шаг 1: Настройка проекта – Основы Read Write Excel C#

Прежде чем погрузиться в код, нам нужна надёжная основа.

1. **Create a new console app** (or any .NET project) targeting .NET 6 or later:

   ```bash
   dotnet new console -n ExcelEraDemo
   cd ExcelEraDemo
   ```

2. **Add the Aspose.Cells NuGet package**. It’s a fully managed library that works without COM interop:

   ```bash
   dotnet add package Aspose.Cells
   ```

3. **Copy an Excel file** (`EraDates.xlsx`) into the project root. This workbook should contain a sheet named `"Sheet1"` with cell **B2** holding a value like `"R3/5/12"` (Reiwa 3, May 12).

Это всё, что нужно для подготовки. Остальная часть руководства сосредоточена на реальной логике **read excel cell value** и **write datetime to excel**.

## Шаг 2: Read Excel Cell Value with C#

Теперь, когда проект готов, получим строку из листа. Ниже показан точный цепочка вызовов:

```csharp
using Aspose.Cells;
using System;
using System.Globalization;

class Program
{
    static void Main()
    {
        // Load the workbook (adjust the path as needed)
        Workbook wb = new Workbook("EraDates.xlsx");
        Worksheet ws = wb.Worksheets["Sheet1"];   // assumes the sheet is named Sheet1

        // Step 2: Get the cell that holds the Japanese era date string
        // B2 contains something like "R3/5/12"
        Cell dateCell = ws.Cells["B2"];  

        // Step 3: Read the string representation from the cell
        string eraDateString = dateCell.StringValue;  

        Console.WriteLine($"Original cell value: {eraDateString}");
        // -------------------------------------------------
        // From here we’ll convert the era string to a DateTime.
        // -------------------------------------------------
    }
}
```

**Почему это работает:** `Cell.StringValue` всегда возвращает отображаемый текст, независимо от внутреннего числового формата. Это гарантирует, что мы работаем с точной строкой `"R3/5/12"`, которую видит пользователь.

### Распространённые подводные камни

- **Empty cells** – `StringValue` returns an empty string. Guard against it before parsing.  
- **Unexpected formats** – If the cell contains `"2023/05/12"` the era parser will throw; you may need a fallback.

## Шаг 3: Write DateTime to Excel with C#

Имея строку эпохи, мы теперь разбираем её с помощью `DateTime.ParseExact`. Формат `"ggyy/MM/dd"` указывает .NET ожидать японскую эру (`gg`), двухзначный год (`yy`) и компоненты месяца/дня.

```csharp
        // Step 4: Convert the era date string to a DateTime using the Japanese culture
        DateTime parsedDate;
        try
        {
            parsedDate = DateTime.ParseExact(
                eraDateString,
                "ggyy/MM/dd",
                new CultureInfo("ja-JP"));
        }
        catch (FormatException)
        {
            Console.WriteLine("The cell value does not match the expected Japanese era format.");
            return;
        }

        Console.WriteLine($"Parsed DateTime (UTC): {parsedDate:u}");

        // Step 5: Store the resulting DateTime back into the same cell
        dateCell.PutValue(parsedDate);

        // Optional: Apply a standard date format so Excel shows it nicely
        dateCell.SetStyle(new Style { Number = 14 }); // 14 = "m/d/yyyy"

        // Save the workbook to a new file so we don’t overwrite the original
        wb.Save("EraDates_Converted.xlsx");
        Console.WriteLine("Workbook saved as EraDates_Converted.xlsx");
```

**Почему мы используем `PutValue`**: Aspose.Cells автоматически определяет тип .NET и записывает соответствующий тип ячейки Excel. Передача `DateTime` приводит к настоящей дате Excel, которую можно форматировать или использовать в формулах дальше по цепочке.

### Граничные случаи и советы

- **Time zones** – `DateTime` objects are stored without zone info. If you need UTC, call `DateTime.SpecifyKind`.  
- **Culture fallback** – If you anticipate other cultures, wrap the parse in a helper that tries multiple `CultureInfo` objects.  
- **Performance** – When processing thousands of rows, reuse a single `CultureInfo` instance instead of creating a new one each loop.

## Шаг 4: Полный рабочий пример – собираем всё вместе

Ниже представлен полностью готовый к запуску код. Скопируйте его в `Program.cs`, убедитесь, что `EraDates.xlsx` находится рядом с скомпилированным бинарником, и выполните `dotnet run`.

```csharp
using Aspose.Cells;
using System;
using System.Globalization;

class Program
{
    static void Main()
    {
        // Load workbook
        Workbook wb = new Workbook("EraDates.xlsx");
        Worksheet ws = wb.Worksheets["Sheet1"];   // Change if your sheet has a different name

        // -------------------------------------------------
        // 1️⃣ Read the Japanese era string from B2
        // -------------------------------------------------
        Cell dateCell = ws.Cells["B2"];
        string eraDateString = dateCell.StringValue?.Trim();

        if (string.IsNullOrEmpty(eraDateString))
        {
            Console.WriteLine("Cell B2 is empty. Nothing to convert.");
            return;
        }

        Console.WriteLine($"Original cell value: {eraDateString}");

        // -------------------------------------------------
        // 2️⃣ Parse the era string into a DateTime
        // -------------------------------------------------
        DateTime parsedDate;
        try
        {
            parsedDate = DateTime.ParseExact(
                eraDateString,
                "ggyy/MM/dd",
                new CultureInfo("ja-JP"));
        }
        catch (FormatException)
        {
            Console.WriteLine("The value does not match the expected Japanese era format (ggyy/MM/dd).");
            return;
        }

        Console.WriteLine($"Parsed DateTime: {parsedDate:u}");

        // -------------------------------------------------
        // 3️⃣ Write the DateTime back into the same cell
        // -------------------------------------------------
        dateCell.PutValue(parsedDate);

        // Apply a friendly date format (e.g., 2023/05/12)
        Style style = wb.CreateStyle();
        style.Number = 14; // Built‑in date format
        dateCell.SetStyle(style);

        // Save the updated workbook
        wb.Save("EraDates_Converted.xlsx");
        Console.WriteLine("Conversion complete – saved as EraDates_Converted.xlsx");
    }
}
```

**Ожидаемый вывод**

```
Original cell value: R3/5/12
Parsed DateTime: 2021-05-12 00:00:00Z
Conversion complete – saved as EraDates_Converted.xlsx
```

Когда откроете `EraDates_Converted.xlsx`, ячейка **B2** теперь отображает обычную дату (например, `5/12/2021`) и может использоваться в вычислениях Excel так же, как любой другой тип даты.

## Pro Tips for Robust Read Write Excel C# Code

- **Validate before you write** – Use `Cell.IsFormula` or `Cell.Type` to avoid overwriting formulas unintentionally.  
- **Batch processing** – If you need to convert a whole column, loop through `ws.Cells.Columns[1]` (B column) and apply the same logic.  
- **Thread safety** – Aspose.Cells objects aren’t thread‑safe; create separate `Workbook` instances per thread when parallelizing.  
- **Logging** – For production scripts, replace `Console.WriteLine` with a proper logger (e.g., Serilog) to capture parsing failures.  
- **Testing** – Write unit tests that feed known era strings into a helper method and assert the resulting `DateTime` values.

## Заключение

Вы только что освоили **read write Excel C#**, научившись **read excel cell value**, разбирать строку японской эры и **write datetime to excel** с уверенностью. Полный пример демонстрирует чистый сквозной процесс, который можно адаптировать под массовые операции, разные культуры или даже конвейеры «Excel‑в‑базу данных».

Что дальше? Попробуйте расширить скрипт для обработки целого столбца дат эпох, или изучите богатые возможности форматирования Aspose.Cells для стилизации выходных ячеек. Вы также можете поэкспериментировать с другими библиотеками, такими как EPPlus или ClosedXML — большая часть логики остаётся той же, меняются лишь вызовы API.

Есть вопросы или сложный сценарий в Excel? Оставьте комментарий ниже, и счастливого кодинга!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}