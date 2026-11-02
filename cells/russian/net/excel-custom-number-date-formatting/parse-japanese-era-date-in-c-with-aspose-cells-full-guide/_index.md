---
category: general
date: 2026-06-08
description: Разберите дату в японской эре в C# с помощью Aspose.Cells. Узнайте, как
  CultureInfo ja-JP и формат японской эры обеспечивают точное преобразование дат Excel.
draft: false
keywords:
- parse japanese era date
- Aspose.Cells
- CultureInfo ja-JP
- Japanese era format
- Excel date conversion
- C# DateTime parsing
language: ru
og_description: Быстро разбирайте даты японской эры в C#. В этом руководстве показано,
  как CultureInfo ja-JP и Aspose.Cells преобразуют строки эпох в корректные объекты
  DateTime.
og_title: Разбор даты японской эры в C# – руководство Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Parse Japanese era date in C# using Aspose.Cells. Learn how CultureInfo
    ja-JP and Japanese era format enable accurate Excel date conversion.
  headline: Parse Japanese Era Date in C# with Aspose.Cells – Full Guide
  type: TechArticle
- description: Parse Japanese era date in C# using Aspose.Cells. Learn how CultureInfo
    ja-JP and Japanese era format enable accurate Excel date conversion.
  name: Parse Japanese Era Date in C# with Aspose.Cells – Full Guide
  steps:
  - name: 5.1 Invalid or Empty Strings
    text: '```csharp string maybeDate = workbook.Worksheets[0].Cells["B1"].GetString();
      // could be empty if (string.IsNullOrWhiteSpace(maybeDate)) { Console.WriteLine("Cell
      B1 is empty – skipping."); } else { // Attempt to parse; catch format exceptions
      try { DateTime dt = DateTime.Parse(maybeDate, new Cultur'
  - name: 5.2 Older Eras (Showa, Taisho)
    text: 'The same `CultureInfo ja-JP` works for older eras automatically:'
  - name: 5.3 Using `DateTime.ParseExact` for Strict Validation
    text: 'If you want to enforce the exact Japanese era pattern, use a custom format
      string:'
  type: HowTo
- questions:
  - answer: Yes. As long as the workbook’s `Settings.CultureInfo` is set to `ja-JP`
      *before* you call `GetDateTime()`, Aspose.Cells will interpret the existing
      strings correctly.
    question: Does this work with .xlsx files that already contain era dates?
  - answer: The parsing returns a `DateTime` with `Kind = Unspecified`. If you need
      UTC or local time, apply `DateTime.SpecifyKind` or convert after parsing.
    question: What about time zones?
  - answer: Absolutely. Loop through the desired range and call `GetDateTime()` on
      each cell—just remember to handle exceptions for malformed entries.
    question: Can I parse multiple cells at once?
  type: FAQPage
tags:
- C#
- Excel
- DateTime
- Localization
title: Разбор даты японской эпохи в C# с Aspose.Cells – Полное руководство
url: /ru/net/excel-custom-number-date-formatting/parse-japanese-era-date-in-c-with-aspose-cells-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Разбор дат японской эры в C# с Aspose.Cells – Полное руководство

Когда‑нибудь вам нужно было **parse japanese era date** строки напрямую из Excel? Возможно, вы извлекаете данные из устаревшей системы, которая всё ещё использует «令和3年5月12日», и вам нужен чистый `DateTime` для построения отчётов. В этом руководстве мы пройдём полный, готовый к запуску пример, который преобразует такие строки в правильные даты C# — без догадок.

Мы будем использовать **Aspose.Cells**, мощную .NET‑библиотеку для работы с Excel, вместе с настройкой **CultureInfo ja-JP**, которая умеет читать японские эпохи. К концу вы получите переиспользуемый фрагмент кода, который обрабатывает «令和», «平成» и даже более старые эпохи без усилий.

## Требования

- .NET 6.0 или новее (код также работает на .NET Framework 4.6+)  
- Aspose.Cells для .NET (можно взять бесплатный пробный пакет NuGet: `Install-Package Aspose.Cells`)  
- Базовое знакомство с C# — ничего сложного, достаточно консольного приложения  
- Любая IDE по вашему выбору (Visual Studio, Rider, VS Code и т.д.)

Вот и всё. Никаких дополнительных сервисов, никаких obscure third‑party парсеров.

## Шаг 1: Настройка проекта и добавление Aspose.Cells

Сначала создайте новый консольный проект:

```bash
dotnet new console -n JapaneseEraParser
cd JapaneseEraParser
dotnet add package Aspose.Cells
```

Затем откройте **Program.cs** и добавьте необходимые пространства имён:

```csharp
using System;
using System.Globalization;
using Aspose.Cells;
```

> **Pro tip:** Если вы используете Visual Studio, IDE предложит автоматически добавить инструкции `using` после ввода имён классов.

## Шаг 2: Создание Workbook и применение японской культуры

Ключ к правильному **parse japanese era date** — указать Aspose.Cells, какую культуру использовать. Установка `CultureInfo` в `ja-JP` активирует парсинг с учётом эпох.

```csharp
// Step 2: Initialize a new workbook and set Japanese culture
Workbook workbook = new Workbook();
workbook.Settings.CultureInfo = new CultureInfo("ja-JP");
```

Почему это важно? Японский календарь имеет несколько эпох (например, *Reiwa* (令和), *Heisei* (平成)). Объект `CultureInfo` содержит `JapaneseCalendar`, который знает даты начала каждой эпохи, поэтому любая строка, соответствующая формату японской эпохи, может быть правильно интерпретирована.

## Шаг 3: Запись строки даты японской эпохи в ячейку

Запишем пример даты эпохи в ячейку **A1**. При желании измените строку, чтобы протестировать разные эпохи.

```csharp
// Step 3: Put a Japanese era date string into A1
string japaneseDate = "令和3年5月12日"; // Reiwa 3, May 12, 2021
workbook.Worksheets[0].Cells["A1"].PutValue(japaneseDate);
```

Если вы предпочитаете работать с существующей книгой, её можно загрузить с помощью `new Workbook("path/to/file.xlsx")` и пропустить шаг создания.

## Шаг 4: Получение значения как объекта C# DateTime

Теперь происходит магия. При вызове `GetDateTime()` Aspose.Cells читает ячейку, используя ранее установленный `CultureInfo`, и возвращает корректный `DateTime`.

```csharp
// Step 4: Parse the cell value into a DateTime
DateTime parsedDate = workbook.Worksheets[0].Cells["A1"].GetDateTime();
Console.WriteLine($"Parsed DateTime: {parsedDate:yyyy-MM-dd}");
```

**Expected output**

```
Parsed DateTime: 2021-05-12
```

Это весь процесс **parse japanese era date** — четыре лаконичные строки кода.

## Шаг 5: Обработка граничных случаев и альтернативных эпох

В реальных данных не всегда всё чисто. Ниже несколько сценариев, с которыми вы можете столкнуться, и способы их обработки.

### 5.1 Неверные или пустые строки

```csharp
string maybeDate = workbook.Worksheets[0].Cells["B1"].GetString(); // could be empty
if (string.IsNullOrWhiteSpace(maybeDate))
{
    Console.WriteLine("Cell B1 is empty – skipping.");
}
else
{
    // Attempt to parse; catch format exceptions
    try
    {
        DateTime dt = DateTime.Parse(maybeDate, new CultureInfo("ja-JP"));
        Console.WriteLine($"B1 parsed as {dt:yyyy-MM-dd}");
    }
    catch (FormatException)
    {
        Console.WriteLine($"Unable to parse '{maybeDate}' as a Japanese era date.");
    }
}
```

### 5.2 Старые эпохи (Showa, Taisho)

Тот же `CultureInfo ja-JP` автоматически работает и для старых эпох:

```csharp
string showaDate = "昭和45年12月31日"; // Showa 45 = 1970-12-31
DateTime showaParsed = DateTime.Parse(showaDate, new CultureInfo("ja-JP"));
Console.WriteLine(showaParsed.ToString("yyyy-MM-dd")); // 1970-12-31
```

### 5.3 Использование `DateTime.ParseExact` для строгой валидации

Если вы хотите принудительно задать точный шаблон японской эпохи, используйте пользовательскую строку формата:

```csharp
string pattern = "ggggy年M月d日"; // gggg = era name, y = year in era
DateTime strictDate = DateTime.ParseExact(japaneseDate, pattern, new CultureInfo("ja-JP"));
Console.WriteLine(strictDate); // 2021-05-12 00:00:00
```

Этот подход бросает `FormatException`, если строка отклоняется от шаблона, что может быть полезно для проверки качества данных.

## Полный рабочий пример

Ниже полный код программы, который можно скопировать в **Program.cs** и запустить.

```csharp
using System;
using System.Globalization;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create workbook and set Japanese culture
        Workbook workbook = new Workbook();
        workbook.Settings.CultureInfo = new CultureInfo("ja-JP");

        // 2️⃣ Insert a Japanese era date string
        string japaneseDate = "令和3年5月12日";
        workbook.Worksheets[0].Cells["A1"].PutValue(japaneseDate);

        // 3️⃣ Parse the cell value into DateTime
        DateTime parsedDate = workbook.Worksheets[0].Cells["A1"].GetDateTime();
        Console.WriteLine($"Parsed DateTime: {parsedDate:yyyy-MM-dd}");

        // 4️⃣ Demonstrate handling an older era
        string showaDate = "昭和45年12月31日";
        DateTime showaParsed = DateTime.Parse(showaDate, new CultureInfo("ja-JP"));
        Console.WriteLine($"Showa parsed: {showaParsed:yyyy-MM-dd}");

        // 5️⃣ Strict parsing with ParseExact
        string pattern = "gggy年M月d日";
        try
        {
            DateTime strict = DateTime.ParseExact(japaneseDate, pattern, new CultureInfo("ja-JP"));
            Console.WriteLine($"Strict parse: {strict:yyyy-MM-dd}");
        }
        catch (FormatException ex)
        {
            Console.WriteLine($"Strict parse failed: {ex.Message}");
        }
    }
}
```

Запустите его с помощью `dotnet run`, и вы увидите:

```
Parsed DateTime: 2021-05-12
Showa parsed: 1970-12-31
Strict parse: 2021-05-12
```

Бум — **parse japanese era date** выполнено, и у вас есть шаблон для любой эпохи, с которой вы можете столкнуться.

![Рабочий процесс разбора дат японской эры — показывает создание workbook, настройку культуры, запись в ячейку и вызов GetDateTime call](parse-japanese-era-date.png "Диаграмма, иллюстрирующая процесс разбора дат японской эры с помощью Aspose.Cells и CultureInfo ja-JP")

## Часто задаваемые вопросы

- **Работает ли это с файлами .xlsx, которые уже содержат даты эпох?**  
  Да. Пока в `Settings.CultureInfo` workbook установлен в `ja-JP` *до* вызова `GetDateTime()`, Aspose.Cells корректно интерпретирует существующие строки.

- **А как насчёт часовых поясов?**  
  Парсинг возвращает `DateTime` с `Kind = Unspecified`. Если нужен UTC или локальное время, используйте `DateTime.SpecifyKind` или выполните преобразование после парсинга.

- **Можно ли разобрать несколько ячеек одновременно?**  
  Конечно. Пройдитесь в цикле по нужному диапазону и вызывайте `GetDateTime()` для каждой ячейки — не забудьте обрабатывать исключения для некорректных записей.

## Заключение

Мы рассмотрели всё, что нужно для **parse japanese era date** строк в C# с использованием Aspose.Cells и встроенного `CultureInfo ja-JP`. От настройки workbook, записи строк в формате эпох, получения чистого `DateTime`, до обработки граничных случаев, таких как старые эпохи и строгая валидация — это руководство предоставляет готовое к продакшн решение.

Далее вы можете изучить **Excel date conversion** для числовых серийных дат или погрузиться в **C# DateTime parsing** с пользовательскими календарями для других локалей. Та же схема работает для тайского буддийского календаря, еврейского календаря и других — просто замените `CultureInfo`.

Есть сложный случай, с которым вы боретесь? Оставьте комментарий, и мы разберёмся вместе. Счастливого кодинга!

## Что стоит изучить дальше?

Следующие руководства охватывают тесно связанные темы, построенные на техниках, продемонстрированных в этом руководстве. Каждый ресурс включает полные рабочие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в собственных проектах.

- [Как реализовать проверку дат в .NET с помощью Aspose.Cells: Полное руководство](/cells/english/net/data-validation/implement-date-validation-net-aspose-cells/)
- [Изменить систему дат Excel на 1904 с помощью Aspose.Cells .NET](/cells/english/net/calculation-engine/change-excel-date-system-aspose-cells-net/)
- [Эффективно конвертировать Excel в PDF с пользовательскими форматами дат, используя Aspose.Cells для Java](/cells/english/java/workbook-operations/render-excel-custom-date-formats-pdf-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}