---
category: general
date: 2026-10-10
description: Создайте книгу Excel на C# и задайте значение ячейки датой в японском
  календаре, затем примените пользовательский формат и прочитайте ячейку даты с помощью
  Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- set cell value
- apply custom format
- read date cell
- excel date parsing
language: ru
lastmod: 2026-10-10
og_description: Создайте рабочую книгу Excel на C# и разбирайте даты в японских эпохах.
  Узнайте, как задать значение ячейки, применить пользовательский формат и прочитать
  ячейку с датой с помощью Aspose.Cells.
og_image_alt: Screenshot showing a C# program that creates an Excel workbook and parses
  a Japanese era date
og_title: Создание Excel‑книги в C# – полное руководство по разбору дат
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Create Excel workbook in C# and set cell value with a Japanese era
    date, then apply custom format and read date cell using Aspose.Cells.
  headline: How to create Excel workbook and parse Japanese dates in C#
  type: TechArticle
tags:
- C#
- Aspose.Cells
- Excel automation
title: Как создать рабочую книгу Excel и разобрать японские даты в C#
url: /ru/net/excel-custom-number-date-formatting/how-to-create-excel-workbook-and-parse-japanese-dates-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как создать книгу Excel и разобрать японские даты в C#

Если вам нужно **создать книгу Excel** с нуля, это руководство покажет, как это сделать. Вы узнаете, как **установить значение ячейки** строкой даты в японской эре, **применить пользовательский формат**, который понимает эру, и, наконец, **прочитать ячейку с датой**, чтобы получить .NET `DateTime`. Полный пример работает с последней версией Aspose.Cells для .NET, поэтому вы можете скопировать‑вставить код в любой проект C#.

Работа с датами, включающими японские эры, может быть сложной, потому что стандартный парсер Excel не распознаёт символы эпох. Используя пользовательский числовой формат (`[ja-JP-Era]`), вы указываете Excel, как интерпретировать строку, обеспечивая надёжный **excel date parsing**. Ниже представлены все шаги, от создания книги до извлечения даты.

## Prerequisites

- .NET 6.0 или новее (код также работает на .NET Framework 4.7+)
- Aspose.Cells for .NET (NuGet‑пакет `Aspose.Cells`)
- Базовые знания C# и Visual Studio или любой другой IDE по вашему выбору

## Step 1: Create Excel workbook and add a worksheet

Первая операция — **создать книгу Excel** в памяти. Aspose.Cells автоматически создаёт лист по умолчанию, но при необходимости вы можете добавить дополнительные.

```csharp
using Aspose.Cells;
using System;

class JapaneseDateExample
{
    static void Main()
    {
        // Step 1: Create a new workbook instance
        Workbook workbook = new Workbook();

        // Optional: rename the default worksheet for clarity
        workbook.Worksheets[0].Name = "Dates";
```

Создание книги выделяет внутренние структуры, которые позже будут хранить ячейки, стили и формулы. На этом этапе файл не записывается на диск, что делает операцию быстрой и удобной для тестирования.

## Step 2: Set cell value with a Japanese era date string

Далее **устанавливаем значение ячейки** строкой даты в японской эре `"R5-04-01"` (Reiwa 5, 1 апреля). Строка следует шаблону `EraYear-MM-DD`.

```csharp
        // Step 2: Reference cell A1 on the first worksheet
        Cell dateCell = workbook.Worksheets[0].Cells["A1"];

        // Put the Japanese era date string into the cell
        dateCell.PutValue("R5-04-01");
```

Метод `PutValue` сохраняет необработанный текст. Excel будет рассматривать его как строку, пока числовой формат не укажет иначе. Такой подход работает для любого пользовательского представления календаря, а не только для японских эр.

## Step 3: Apply a custom number format that understands the Japanese era

Теперь **применяем пользовательский формат**, чтобы Excel мог преобразовать строку эпохи в реальную последовательную дату. Формат `[ja-JP-Era]yyyy/MM/dd` сообщает движку интерпретировать ведущий символ эпохи (`R` для Reiwa) и вычислять григорианскую дату.

```csharp
        // Step 3: Apply a custom number format for Japanese era parsing
        dateCell.Style.Custom = "[ja-JP-Era]yyyy/MM/dd";
```

Пользовательский формат сохраняется в объекте стиля ячейки. Aspose.Cells учитывает этот формат как при рендеринге, так и при преобразовании значения, обеспечивая надёжный **excel date parsing** на последующих этапах.

## Step 4: Retrieve the parsed DateTime value from the cell

Наконец, **читаем ячейку с датой**, чтобы получить .NET `DateTime`. Свойство `DateTimeValue` возвращает преобразованное значение на основе ранее применённого пользовательского формата.

```csharp
        // Step 4: Retrieve the parsed DateTime value
        DateTime parsedDate = dateCell.DateTimeValue;

        // Output the result to the console for verification
        Console.WriteLine($"Parsed Gregorian date: {parsedDate:yyyy-MM-dd}");
```

При запуске программы в консоли будет выведено:

```
Parsed Gregorian date: 2023-04-01
```

Вывод подтверждает, что строка японской эпохи `"R5-04-01"` была корректно интерпретирована как 1 апреля 2023 года.

## Full, runnable example

Собрав все части вместе, получаем самостоятельную программу, которую можно сразу же скомпилировать и запустить.

```csharp
using Aspose.Cells;
using System;

class JapaneseDateExample
{
    static void Main()
    {
        // Create a new workbook
        Workbook workbook = new Workbook();

        // Reference cell A1
        Cell dateCell = workbook.Worksheets[0].Cells["A1"];

        // Insert Japanese era date string
        dateCell.PutValue("R5-04-01");

        // Apply custom format for Japanese era parsing
        dateCell.Style.Custom = "[ja-JP-Era]yyyy/MM/dd";

        // Retrieve the parsed DateTime
        DateTime parsedDate = dateCell.DateTimeValue;

        // Show the result
        Console.WriteLine($"Parsed Gregorian date: {parsedDate:yyyy-MM-dd}");

        // (Optional) Save the workbook to verify the visual format
        workbook.Save("JapaneseEraDate.xlsx");
    }
}
```

Запуск программы создаёт файл `JapaneseEraDate.xlsx` с ячейкой A1, отображающей `2023/04/01`, а консоль выводит ту же григорианскую дату. Файл можно открыть в Excel, чтобы увидеть отформатированное значение.

## Why this approach works

- **create excel workbook** – Создание экземпляра `Workbook` формирует полную структуру файла Excel в памяти без обращения к диску.
- **set cell value** – `PutValue` сохраняет необработанный текст, что необходимо перед применением культуры‑специфичного формата.
- **apply custom format** – Токен `[ja-JP-Era]` соединяет нотацию эпохи с внутренней системой последовательных дат Excel.
- **read date cell** – `DateTimeValue` автоматически использует стиль ячейки для выполнения преобразования, возвращая нативный `DateTime`.
- **excel date parsing** – Делегируя разбор стилю ячейки, вы избегаете ручной обработки строк, снижая количество ошибок и улучшая поддержку локалей.

## Edge cases and practical tips

- **Different eras** – Используйте `S` для Showa, `H` для Heisei, `R` для Reiwa. Одна и та же строка формата работает для всех эпох.
- **Invalid strings** – Если ячейка содержит некорректную дату эпохи, `DateTimeValue` возвращает `DateTime.MinValue`. Проверьте `dateCell.IsDate` перед чтением.
- **Multiple cells** – Применяйте пользовательский формат к целому диапазону (`range.ApplyStyle(style)`), когда нужно разобрать множество дат.
- **Performance** – Установка стиля один раз для столбца быстрее, чем для каждой отдельной ячейки в больших листах.
- **Saving options** – Aspose.Cells может сохранять в XLSX, XLS, CSV или PDF. Выберите формат, соответствующий дальнейшей обработке.

## Frequently asked questions

**Can I use the built‑in .NET culture instead of a custom format?**  
Класс .NET `CultureInfo` не понимает символы японских эпох так же, как Excel. Использование пользовательского числового формата — самый надёжный метод для **excel date parsing** строк эпох.

**What if I need to write the date back to Excel in era format?**  
Установите значение ячейки как `DateTime` и примените тот же пользовательский формат. Excel автоматически отобразит эпоху.

**Does this work on older versions of Excel?**  
Токен `[ja-JP-Era]` поддерживается в Excel 2010 и новее. Aspose.Cells эмулирует это поведение, поэтому книга отображается корректно даже в более старых версиях Excel, где нет нативной поддержки эпох.

## Conclusion

Теперь вы знаете, как **создать книгу Excel**, **установить значение ячейки** строкой даты в японской эпохе, **применить пользовательский формат** и **прочитать ячейку с датой**, чтобы получить `DateTime`. Этот подход обеспечивает надёжный **excel date parsing** без ручной обработки строк, делая ваш C#‑код автоматизации лаконичным и надёжным.

Далее изучайте связанные темы, такие как **форматирование нескольких столбцов дат**, **работа с другими культурными календарями** или **экспорт книги в PDF**. Каждый из этих вариантов опирается на те же принципы, описанные в этом руководстве, позволяя адаптировать решение под широкий спектр сценариев локализации. Приятного кодинга!

## What Should You Learn Next?

The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Create Excel Workbook in C# – Apply Custom Number Format](/cells/english/net/excel-custom-number-date-formatting/create-excel-workbook-in-c-apply-custom-number-format/)
- [Create Excel Workbook with Custom Format – C# Guide](/cells/english/net/excel-custom-number-date-formatting/create-excel-workbook-with-custom-format-c-guide/)
- [Excel Automation with Aspose.Cells .NET: Create Workbook & Set External Links](/cells/english/net/automation-batch-processing/excel-automation-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}