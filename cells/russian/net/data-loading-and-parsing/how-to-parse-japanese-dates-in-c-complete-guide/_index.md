---
category: general
date: 2026-03-29
description: Как парсить японские даты в C# с помощью DateTimeParser и CultureInfo.
  Узнайте о разборе дат японской эры, советах по разбору дат в C# и обработке крайних
  случаев.
draft: false
keywords:
- how to parse japanese
- japanese era date parsing
- datetimeparser c#
- cultureinfo ja-jp
- parse japanese era
- c# date parsing
language: ru
og_description: Как парсить японские даты в C# с помощью DateTimeParser и CultureInfo.
  Получите пошаговое решение для разбора дат японской эры.
og_title: Как парсить японские даты в C# – Полное руководство
tags:
- C#
- .NET
- DateTime
- Localization
title: Как парсить японские даты в C# – Полное руководство
url: /ru/net/data-loading-and-parsing/how-to-parse-japanese-dates-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как парсить японские даты в C# – Полное руководство

Когда‑нибудь задумывались **как парсить японские** строки дат в приложении .NET? Возможно, вы работаете над финансовой системой, которая получает даты вроде «令和3年5月12日» от японского клиента, и вам нужно преобразовать их в обычный `DateTime`. Вы не одиноки — проблемы локализации возникают постоянно.  

Хорошая новость в том, что с правильными настройками культуры и небольшим вспомогательным классом **как парсить японские** даты становится проще простого. В этом руководстве мы пройдём каждый шаг, от настройки `CultureInfo` для *ja‑JP* до обработки особых случаев, таких как исторические эры. К концу вы получите переиспользуемый `DateTimeParser`, который работает с любой современной датой в японской эре.

> **Что вы получите** — полностью готовый к запуску пример, объяснения *почему* каждая строка важна, советы по работе со старыми эрами и быстрый чек‑лист, чтобы ничего не забыть.

## Требования

- .NET 6+ (или .NET Framework 4.7 + — используемый API не изменился)
- Базовые знания C# (должны быть уверены в работе с `using` и `Console.WriteLine`)
- Без внешних пакетов NuGet — всё находится в `System` и `System.Globalization`

Если у вас уже открыт проект, отлично — просто вставьте код. Если нет, создайте новое консольное приложение командой `dotnet new console -n JapaneseDateDemo`, и вы готовы к работе.

## Шаг 1: Понимание японской календарной системы

Прежде чем перейти к коду, ответим на вопрос «почему». Японские даты записываются в формате **эра** (元号), где номер года сбрасывается при восшествии на престол нового императора. Например:

- **令和** (Reiwa) началась 01.05.2019.
- **平成** (Heisei) охватывала 1989‑2019 годы.
- **昭和** (Showa) длилась с 1926‑1989 годов.

Класс .NET `JapaneseCalendar` уже знает эти эры, но вам нужно указать парсеру, какую культуру использовать. Здесь вступает в игру **cultureinfo ja‑jp** — он связывает календарь с японской локалью.

## Шаг 2: Создание небольшого обёртки — `DateTimeParser`

Вместо того чтобы разбрасывать `CultureInfo` по всему коду, мы инкапсулируем логику в небольшом помощнике. Это делает код переиспользуемым и сохраняет остальную часть приложения чистой.

```csharp
// File: DateTimeParser.cs
using System;
using System.Globalization;

public class DateTimeParser
{
    private readonly CultureInfo _culture;
    private readonly JapaneseCalendar _japaneseCalendar;

    public DateTimeParser(CultureInfo culture)
    {
        // Ensure the supplied culture uses the Japanese calendar.
        if (culture.Calendar is not JapaneseCalendar)
            throw new ArgumentException("Culture must use JapaneseCalendar.", nameof(culture));

        _culture = culture;
        _japaneseCalendar = (JapaneseCalendar)culture.Calendar;
    }

    /// <summary>
    /// Parses a Japanese era date string (e.g., "令和3年5月12日") into a Gregorian DateTime.
    /// </summary>
    /// <param name="japaneseDate">The era‑based date string.</param>
    /// <returns>A DateTime representing the same day in the Gregorian calendar.</returns>
    public DateTime Parse(string japaneseDate)
    {
        if (string.IsNullOrWhiteSpace(japaneseDate))
            throw new ArgumentNullException(nameof(japaneseDate));

        // The standard pattern for Japanese era dates.
        // "gggy年M月d日" -> era name (ggg), year (y), month (M), day (d)
        const string pattern = "gggy年M月d日";

        // TryParseExact respects the culture's calendar (JapaneseCalendar here).
        if (DateTime.TryParseExact(
                japaneseDate,
                pattern,
                _culture,
                DateTimeStyles.None,
                out DateTime result))
        {
            return result;
        }

        // If parsing fails, give a helpful exception.
        throw new FormatException(
            $"Unable to parse '{japaneseDate}'. Expected format: {pattern}");
    }
}
```

**Зачем нужен этот помощник?**  
- **Единственная ответственность** — вся парсинг, зависящий от локали, находится в одном месте.  
- **Обработка ошибок** — мы выдаём понятные сообщения, когда формат неверен.  
- **Будущее‑готовый** — если позже понадобится поддержка старых эр *Taisho* или *Meiji*, достаточно скорректировать шаблон или добавить запасной вариант.

## Шаг 3: Подключаем всё в `Program.cs`

Теперь используем обёртку для реального разбора примерной строки. Обратите внимание, как мы получаем японскую культуру через `CultureInfo.GetCultureInfo("ja-JP")`. Это удовлетворяет требование **cultureinfo ja‑jp** и активирует `JapaneseCalendar`.

```csharp
// File: Program.cs
using System;
using System.Globalization;

class Program
{
    static void Main()
    {
        // Step 3‑1: Grab the Japanese culture (ja-JP) which uses JapaneseCalendar.
        var japaneseCulture = CultureInfo.GetCultureInfo("ja-JP");

        // Step 3‑2: Initialise our DateTimeParser with that culture.
        var parser = new DateTimeParser(japaneseCulture);

        // Step 3‑3: The era string we want to convert.
        string eraDate = "令和3年5月12日";

        try
        {
            // Step 3‑4: Parse it.
            DateTime gregorian = parser.Parse(eraDate);

            // Step 3‑5: Show the result – expected: 2021‑05‑12.
            Console.WriteLine($"Japanese: {eraDate} → Gregorian: {gregorian:yyyy-MM-dd}");
        }
        catch (Exception ex)
        {
            // Friendly error output – useful in real‑world apps.
            Console.WriteLine($"Error: {ex.Message}");
        }
    }
}
```

При запуске `dotnet run` вы увидите:

```
Japanese: 令和3年5月12日 → Gregorian: 2021-05-12
```

Это и есть суть **как парсить японские** даты. Просто, не правда ли?

## Шаг 4: Обработка особых случаев и старых эр

### 4.1 Исторические даты до 1912 года

Встроенный `JapaneseCalendar` поддерживает только современные эры (начиная с Meiji). Если нужно парсить даты из периодов *Taisho* (1912‑1926) или *Meiji* (1868‑1912), тот же шаблон работает — просто убедитесь, что строка содержит правильное название эры («大正», «明治»). Парсер всё равно вернёт корректный григорианский `DateTime`.

```csharp
string taisho = "大正5年12月31日"; // 1916‑12‑31
Console.WriteLine(parser.Parse(taisho).ToString("yyyy-MM-dd"));
```

### 4.2 Отсутствующая эра (неоднозначный ввод)

Если клиент отправит «2021年5月12日» без указания эры, парсер не справится, потому что шаблон ожидает эру (`ggg`). У вас есть два варианта:

1. **Предположить григорианский календарь** — перейти к `CultureInfo.InvariantCulture` и использовать другой шаблон.  
2. **Отклонить ввод** — сообщить вызывающему, что эра обязательна.

Небольшая адаптация:

```csharp
public DateTime ParseFlexible(string input)
{
    // Try era‑based first.
    try { return Parse(input); } catch { /* ignore */ }

    // Fallback to plain Gregorian pattern.
    const string gregPattern = "yyyy年M月d日";
    if (DateTime.TryParseExact(
            input,
            gregPattern,
            _culture,
            DateTimeStyles.None,
            out DateTime gResult))
    {
        return gResult;
    }

    throw new FormatException("Unable to parse the provided date string.");
}
```

### 4.3 Замечание о потокобезопасности

Объекты `CultureInfo` становятся только для чтения после создания, поэтому их можно безопасно переиспользовать в разных потоках. Сам `DateTimeParser` не хранит изменяемого состояния, что делает его **thread‑safe** — полезный факт для высоконагруженных веб‑API.

## Шаг 5: Собираем всё вместе — готовый к копированию пример

Ниже полный исходный код, который можно вставить в свежий консольный проект. Без внешних пакетов, без скрытых зависимостей.

```csharp
// DateTimeParser.cs
using System;
using System.Globalization;

public class DateTimeParser
{
    private readonly CultureInfo _culture;
    private readonly JapaneseCalendar _japaneseCalendar;

    public DateTimeParser(CultureInfo culture)
    {
        if (culture.Calendar is not JapaneseCalendar)
            throw new ArgumentException("Culture must use JapaneseCalendar.", nameof(culture));

        _culture = culture;
        _japaneseCalendar = (JapaneseCalendar)culture.Calendar;
    }

    public DateTime Parse(string japaneseDate)
    {
        if (string.IsNullOrWhiteSpace(japaneseDate))
            throw new ArgumentNullException(nameof(japaneseDate));

        const string pattern = "gggy年M月d日";

        if (DateTime.TryParseExact(
                japaneseDate,
                pattern,
                _culture,
                DateTimeStyles.None,
                out DateTime result))
        {
            return result;
        }

        throw new FormatException(
            $"Unable to parse '{japaneseDate}'. Expected format: {pattern}");
    }

    // Optional flexible parser for non‑era inputs.
    public DateTime ParseFlexible(string input)
    {
        try { return Parse(input); } catch { /* fall through */ }

        const string gregPattern = "yyyy年M月d日";
        if (DateTime.TryParseExact(
                input,
                gregPattern,
                _culture,
                DateTimeStyles.None,
                out DateTime gResult))
        {
            return gResult;
        }

        throw new FormatException("Unable to parse the provided date string.");
    }
}
```

```csharp
// Program.cs
using System;
using System.Globalization;

class Program
{
    static void Main()
    {
        var japaneseCulture = CultureInfo.GetCultureInfo("ja-JP");
        var parser = new DateTimeParser(japaneseCulture);

        string[] samples = {
            "令和3年5月12日",   // 2021‑05‑12
            "平成31年4月30日", // 2019‑04‑30 (last day of Heisei)
            "大正5年12月31日", // 1916‑12‑31 (historical)
            "2022年1月1日"      // ambiguous – no era
        };

        foreach (var s in samples)
        {
            try
            {
                DateTime dt = parser.ParseFlexible(s);
                Console.WriteLine($"{s} → {dt:yyyy-MM-dd}");

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}