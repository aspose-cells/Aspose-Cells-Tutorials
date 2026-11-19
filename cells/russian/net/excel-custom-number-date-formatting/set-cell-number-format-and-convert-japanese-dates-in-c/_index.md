---
category: general
date: 2026-11-19
description: Задайте числовой формат ячейки в C# и узнайте, как применить формат даты
  Excel для дат японской эры, обеспечивая надёжное преобразование дат Excel в C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set cell number format
- apply excel date format
- c# excel date conversion
- japanese era date excel
- aspose.cells date handling
language: ru
lastmod: 2026-11-19
og_description: Установите числовой формат ячейки в C# и примените формат даты Excel
  к датам японской эры. Следуйте этому полному руководству для точного преобразования
  дат Excel в C#.
og_image_alt: Screenshot showing a C# code editor with set cell number format applied
  to an Excel cell
og_title: Установите числовой формат ячейки и преобразуйте японские даты в C# – пошаговое
  руководство
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: Set cell number format in C# and learn how to apply Excel date format
    for Japanese era dates, enabling reliable C# Excel date conversion.
  headline: Set cell number format and convert Japanese dates in C#
  type: TechArticle
- description: Set cell number format in C# and learn how to apply Excel date format
    for Japanese era dates, enabling reliable C# Excel date conversion.
  name: Set cell number format and convert Japanese dates in C#
  steps:
  - name: Why this works
    text: '* `Style.Number = 14` maps to Excel’s *Short Date* format (`mm/dd/yyyy`
      by default). * When the cell contains a Japanese era string like `R3/04/01`,
      Aspose.Cells’ internal parser recognises the era and converts it to the corresponding
      Gregorian serial number during `CalculateFormula()`. * After the '
  - name: When to use a custom format
    text: '* Reports intended for Japanese audiences. * When you need to preserve
      the original era information for legal documents. * In dashboards where both
      Gregorian and era dates are shown side‑by‑side.'
  - name: Full end‑to‑end example
    text: Below is a self‑contained program that demonstrates both the Gregorian and
      era outputs in one run.
  - name: Edge cases & common pitfalls
    text: '| Situation | What to watch for | Fix / Recommendation | |----------------------------------------|------------------------------------------------------|----------------------------------------------------------|
      | Empty or malformed era string | `PutValue` stores the literal text; conversion
      fails'
  - name: Automation tip
    text: 'If you need to process a large range of era dates (e.g., column A contains
      many Japanese dates), wrap the conversion logic in a loop:'
  type: HowTo
tags:
- C#
- Excel
- Aspose.Cells
- Date conversion
title: Установить числовой формат ячейки и преобразовать японские даты в C#
url: /ru/net/excel-custom-number-date-formatting/set-cell-number-format-and-convert-japanese-dates-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Установить числовой формат ячейки и преобразовать японские даты в C#

Если вам необходимо **установить числовой формат ячейки** в проекте автоматизации Excel на C#, это руководство покажет, как **применить формат даты Excel** и выполнить **преобразование даты Excel в C#** для дат японских эпох. Вы получите полностью готовый пример, который преобразует строку эпохи Рэйва (например, `R3/04/01`) в григорианскую дату `2021‑04‑01`.

## Что вы узнаете

* Как создать рабочую книгу и получить доступ к её первому листу.  
* Как **установить числовой формат ячейки**, чтобы Excel воспринимал значение как дату.  
* Как **применить формат даты Excel**, который распознаёт строки японских эпох.  
* Как инициировать **преобразование даты Excel в C#**, пересчитывая формулы.  
* Ожидаемый вывод и советы по устранению неполадок в граничных случаях.  

**Требования**

* .NET 6 или новее (код также работает с .NET Framework 4.6+).  
* Aspose.Cells для .NET 2024 или новее — установить через NuGet: `dotnet add package Aspose.Cells`.  
* Базовое знакомство с C# и работой с датами в Excel.  

> **Совет:** Aspose.Cells работает без установленного Microsoft Office, что делает его идеальным для серверной автоматизации.

## Установить числовой формат ячейки с помощью Aspose.Cells в C#

Первый шаг — сообщить Excel, что ячейка содержит дату. Excel хранит даты как последовательные числа, поэтому нам нужно применить встроенный числовой формат даты (ID 14) к целевой ячейке.

```csharp
using System;
using Aspose.Cells;

class JapaneseEraDateDemo
{
    static void Main()
    {
        // 1️⃣ Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // 2️⃣ Insert a Japanese era date string (Reiwa 3) into cell A1
        sheet.Cells["A1"].PutValue("R3/04/01");

        // 3️⃣ **Set cell number format** – use built‑in date format ID 14
        //    This tells Excel to treat the string as a date value.
        sheet.Cells["A1"].Style.Number = 14;

        // 4️⃣ Recalculate formulas so the internal date engine converts the era.
        workbook.CalculateFormula();

        // 5️⃣ Output the converted Gregorian date.
        Console.WriteLine(sheet.Cells["A1"].StringValue); // → 2021-04-01
    }
}
```

### Почему это работает

* `Style.Number = 14` соответствует формату *Краткая дата* в Excel (`mm/dd/yyyy` по умолчанию).  
* Когда ячейка содержит строку японской эпохи, например `R3/04/01`, внутренний парсер Aspose.Cells распознаёт эпоху и преобразует её в соответствующий григорианский последовательный номер во время `CalculateFormula()`.  
* После вычисления `StringValue` возвращает отформатированную григорианскую дату.  

## Применить формат даты Excel для японских дат эпох

Если вы хотите, чтобы ячейка отображала японскую эпоху вместо григорианской даты, можно использовать пользовательский числовой формат, включающий код эпохи. Это демонстрирует возможность **применения формата даты Excel**.

```csharp
// Apply a custom format that forces the Japanese era display
sheet.Cells["A1"].Style.Custom = "[$-ja-JP]ggge\"年\"m\"月\"d\"日\"";

// Recalculate to apply the custom format
workbook.CalculateFormula();

// Output the era‑styled string
Console.WriteLine(sheet.Cells["A1"].StringValue); // → R3年04月01日
```

* `[$-ja-JP]` принудительно задаёт японскую локаль.  
* `ggg` представляет название эпохи (например, `R` для Рэйва).  
* Добавление буквальных символов (`年`, `月`, `日`) создаёт привычный японский формат даты.  

### Когда использовать пользовательский формат

* Отчёты, предназначенные для японской аудитории.  
* Когда необходимо сохранить оригинальную информацию об эпохе для юридических документов.  
* В панелях мониторинга, где григорианские и эпохальные даты отображаются рядом.  

## Преобразование даты Excel в C# — работа с японскими эпохами

Процесс **преобразования даты Excel в C#** можно разбить на три логические части:

1. **Разбор строки эпохи** — Aspose.Cells автоматически распознаёт `R` (Рэйва), `H` (Хэйсэй), `S` (Сёва) и т.д.  
2. **Преобразование в последовательный номер** — Excel хранит даты как количество дней, прошедших с 1899‑12‑30.  
3. **Форматирование последовательного номера** — либо встроенным форматом (ID 14), либо пользовательским японским форматом.  

### Полный пример от начала до конца

Ниже представлена автономная программа, демонстрирующая как григорианский, так и эпохальный вывод за один запуск.

```csharp
using System;
using Aspose.Cells;

class JapaneseEraConversion
{
    static void Main()
    {
        // Create workbook and worksheet
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];

        // Input: Reiwa 3 (2021) – can be any era string
        ws.Cells["A1"].PutValue("R3/04/01");

        // ---- Part 1: Gregorian output ----
        ws.Cells["A1"].Style.Number = 14;      // built‑in short date
        wb.CalculateFormula();                // forces conversion
        string gregorian = ws.Cells["A1"].StringValue;
        Console.WriteLine($"Gregorian: {gregorian}"); // 2021-04-01

        // ---- Part 2: Japanese era output ----
        ws.Cells["B1"].PutValue("R3/04/01");   // repeat input for clarity
        ws.Cells["B1"].Style.Custom = "[$-ja-JP]ggge\"年\"m\"月\"d\"日\"";
        wb.CalculateFormula();
        string era = ws.Cells["B1"].StringValue;
        Console.WriteLine($"Japanese era: {era}"); // R3年04月01日
    }
}
```

**Ожидаемый вывод в консоль**

```
Gregorian: 2021-04-01
Japanese era: R3年04月01日
```

### Пограничные случаи и распространённые подводные камни

| Ситуация                              | На что обратить внимание                                   | Исправление / Рекомендация                                   |
|---------------------------------------|------------------------------------------------------------|--------------------------------------------------------------|
| Пустая или некорректная строка эпохи  | `PutValue` сохраняет буквальный текст; преобразование не удаётся | Проверить ввод с помощью регулярного выражения перед записью в ячейку. |
| Несоответствие локали                 | Пользовательский формат отображает западные цифры вместо японских символов | Убедитесь, что пользовательский формат включает `[$-ja-JP]` или задайте `Workbook.Settings.CultureInfo` в `ja-JP`. |
| Рабочая книга содержит формулы, ссылающиеся на ячейку даты | Пересчёт может перезаписать результаты формул | Вызовите `CalculateFormula` **после** всех шагов форматирования, либо используйте `Workbook.CalculateFormula(FormulaCalculationOptions.IgnoreError)`, если необходимо пропустить ошибки. |
| Использование более старых версий Aspose.Cells | Поддержка японских эпох была добавлена в 2022 Q3          | Обновите до последней версии пакета NuGet.                     |

## Тестирование решения

1. **Запустите программу** из Visual Studio или `dotnet run`.  
2. Убедитесь, что консоль выводит григорианскую дату `2021‑04‑01` и строку эпохи `R3年04月01日`.  
3. Откройте сгенерированную рабочую книгу (если вы добавите `wb.Save("Demo.xlsx");`) в Microsoft Excel, чтобы увидеть тот же формат, применённый к ячейкам.  

### Совет по автоматизации

Если необходимо обработать большой диапазон дат эпох (например, столбец A содержит множество японских дат), оберните логику преобразования в цикл:

```csharp
for (int row = 0; row < ws.Cells.MaxDataRow + 1; row++)
{
    var cell = ws.Cells[row, 0]; // column A
    cell.Style.Number = 14;
}
wb.CalculateFormula();
```

Такой подход сохраняет операцию **установки числового формата ячейки** быстрой и экономичной по памяти.  

## Заключение

Теперь вы знаете, как **установить числовой формат ячейки** в C# с помощью Aspose.Cells, как **применить формат даты Excel** для строк японских эпох и как выполнить надёжное **преобразование даты Excel в C#** из эпохи в григорианскую дату. Полный, исполняемый код демонстрирует оба вывода и подчёркивает распространённые граничные случаи.  

**Следующие шаги**

* Изучите другие встроенные идентификаторы форматов  

## Что вам следует изучить дальше?

Следующие руководства охватывают тесно связанные темы, которые развивают техники, продемонстрированные в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и изучить альтернативные подходы к реализации в ваших проектах.

- [установить формат даты Excel в C# – Полное пошаговое руководство](/cells/english/net/excel-custom-number-date-formatting/set-excel-date-format-in-c-complete-step-by-step-guide/)
- [Как применить числовой формат в Excel с помощью Aspose.Cells](/cells/english/net/excel-custom-number-date-formatting/how-to-apply-number-format-excel-with-aspose-cells/)
- [Как применить пользовательский числовой формат в Excel на C#](/cells/english/net/excel-custom-number-date-formatting/how-to-apply-a-custom-number-format-excel-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}