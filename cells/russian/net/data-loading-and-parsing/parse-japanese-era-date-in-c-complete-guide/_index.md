---
category: general
date: 2026-06-27
description: Узнайте, как разобрать дату в японском календаре в C# и затем отформатировать
  datetime в виде yyyy‑mm‑dd для ISO‑вывода. Пошаговый код, граничные случаи и советы.
draft: false
keywords:
- parse japanese era date
- format datetime yyyy-mm-dd
- C# JapaneseCalendar
- CultureInfo date parsing
- .NET DateTime era handling
language: ru
og_description: Разбор даты японской эры в C# и простое форматирование datetime в
  yyyy‑mm‑dd. Полный пример с объяснениями и подводными камнями.
og_title: Разбор даты японской эры в C# – Полный программный разбор
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: Learn how to parse Japanese era date in C# and then format datetime
    yyyy-mm-dd for ISO output. Step‑by‑step code, edge cases, and tips.
  headline: Parse Japanese era date in C# – Complete Guide
  type: TechArticle
- description: Learn how to parse Japanese era date in C# and then format datetime
    yyyy-mm-dd for ISO output. Step‑by‑step code, edge cases, and tips.
  name: Parse Japanese era date in C# – Complete Guide
  steps:
  - name: Multiple Eras
    text: Japan has gone through several eras (Meiji, Taishō, Shōwa, Heisei, Reiwa).
      The `JapaneseCalendar` automatically maps them, so `"H30-12-31"` (Heisei 30)
      becomes `2018-12-31`. Just keep the same parsing logic; the calendar does the
      heavy lifting.
  - name: Invalid Input
    text: 'If a string doesn’t match the expected pattern, `Parse` throws. Use `TryParseExact`
      as shown earlier, or pre‑validate with a regular expression:'
  - name: Time Zones
    text: '`DateTime` objects are “kind‑agnostic” by default. If you need a UTC timestamp,
      call:'
  type: HowTo
tags:
- C#
- .NET
- DateTime
- Localization
title: Разбор дат японской эры в C# — полное руководство
url: /ru/net/data-loading-and-parsing/parse-japanese-era-date-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Разбор даты японской эры в C# – Полное руководство

Когда‑то вам нужно было **разобрать дату японской эры** в приложении .NET и вы заметили, что результат выглядит неверно? Вы не одиноки. Во многих устаревших системах даты приходят в виде «R3‑04‑01», и их нужно превратить в чистую строку **format datetime yyyy-mm-dd** для API или баз данных.  

В этом руководстве мы пройдём по точным шагам, объясним, почему каждый из них важен, и покажем, как справиться с коварными граничными случаями, которые часто подводят разработчиков.

> **Примечание:** Весь код готов к копированию‑вставке в консольное приложение, нацеленное на .NET 6 или новее.

## Что понадобится

- .NET 6 SDK (или любая более свежая версия)
- Базовое знакомство с C# и пространством имён `System.Globalization`
- IDE или редактор – Visual Studio, VS Code, Rider или любой другой, который вам нравится

Никаких внешних пакетов NuGet не требуется; всё находится в BCL.

## Шаг 1: Настройка японской культуры с императорским календарём

Сначала нам нужен `CultureInfo`, который знает об императорском календаре Японии. По умолчанию `ja-JP` использует григорианский календарь, поэтому заменяем его `DateTimeFormat.Calendar` на экземпляр `JapaneseCalendar`.

```csharp
using System;
using System.Globalization;

class Program
{
    static void Main()
    {
        // Step 1: Create a Japanese culture and switch to the Japanese imperial calendar
        CultureInfo japaneseCulture = new CultureInfo("ja-JP");
        japaneseCulture.DateTimeFormat.Calendar = new JapaneseCalendar();

        // (The rest of the code follows...)
```

> **Почему это важно:** `JapaneseCalendar` переводит символы эпох (например, «R» для Reiwa) в правильный григорианский год. Без него `DateTime.Parse` выбросит `FormatException`.

## Шаг 2: Разбор строки даты, основанной на эпохе

Теперь мы можем передать строку вроде `"R3-04-01"` в `DateTime.Parse`. Настроенная культура подскажет парсеру, как интерпретировать часть «R3».

```csharp
        // Step 2: Parse a date string that uses the Japanese era format (e.g., "R3-04-01")
        string eraDate = "R3-04-01";
        DateTime parsedDate = DateTime.Parse(eraDate, japaneseCulture);
```

Если вы предпочитаете более безопасный подход, который избегает исключений при плохом вводе, замените `Parse` на `TryParseExact`:

```csharp
        // Safer alternative with TryParseExact
        if (DateTime.TryParseExact(
                eraDate,
                "ggy-MM-dd",               // ggy = era+year, MM = month, dd = day
                japaneseCulture,
                DateTimeStyles.None,
                out DateTime safeDate))
        {
            parsedDate = safeDate;
        }
        else
        {
            Console.WriteLine("Unable to parse the Japanese era date.");
            return;
        }
```

> **Совет профессионала:** Пользовательская строка формата `"ggy-MM-dd"` точно указывает парсеру, чего ожидать. «gg» – обозначение эпохи, «y» – год внутри этой эпохи.

## Шаг 3: Преобразование результата в ISO 8601 (`format datetime yyyy-mm-dd`)

Наконец, выводим `DateTime` в стандартном ISO‑формате. Спецификатор формата `"yyyy-MM-dd"` делает именно это.

```csharp
        // Step 3: Display the parsed date in a standard ISO format
        string isoDate = parsedDate.ToString("yyyy-MM-dd", CultureInfo.InvariantCulture);
        Console.WriteLine(isoDate); // Expected output: 2021-04-01
    }
}
```

Запуск программы выводит:

```
2021-04-01
```

Это **format datetime yyyy-mm-dd**, который вам нужен, готовый для JSON‑полей, SQL‑вставок или любой downstream‑системы.

![пример разбора даты японской эры](placeholder.png){alt="пример разбора даты японской эры"}

## Обработка других эпох и граничных случаев

### Несколько эпох

В Японии было несколько эпох (Meiji, Taishō, Shōwa, Heisei, Reiwa). `JapaneseCalendar` автоматически сопоставляет их, так что `"H30-12-31"` (Heisei 30) становится `2018-12-31`. Достаточно оставить ту же логику разбора; календарь выполнит всю тяжёлую работу.

### Неправильный ввод

Если строка не соответствует ожидаемому шаблону, `Parse` бросит исключение. Используйте `TryParseExact`, как показано выше, или предварительно проверьте строку регулярным выражением:

```csharp
bool IsValidEraDate(string input) =>
    System.Text.RegularExpressions.Regex.IsMatch(
        input, @"^[RHS][0-9]+-\d{2}-\d{2}$", System.Text.RegularExpressions.RegexOptions.IgnoreCase);
```

### Часовые пояса

Объекты `DateTime` по умолчанию «без типа» (`kind‑agnostic`). Если нужен UTC‑таймстамп, вызовите:

```csharp
DateTime utc = DateTime.SpecifyKind(parsedDate, DateTimeKind.Utc);
```

Или используйте `DateTimeOffset` для полной осведомлённости о зоне.

## Полный рабочий пример

Вот весь фрагмент, который можно вставить в новый консольный проект:

```csharp
using System;
using System.Globalization;

class Program
{
    static void Main()
    {
        // Initialize Japanese culture with the imperial calendar
        CultureInfo japaneseCulture = new CultureInfo("ja-JP");
        japaneseCulture.DateTimeFormat.Calendar = new JapaneseCalendar();

        // The era‑based date you want to convert
        string eraDate = "R3-04-01";

        // Try parsing – safer than Parse when input may be malformed
        if (!DateTime.TryParseExact(
                eraDate,
                "ggy-MM-dd",
                japaneseCulture,
                DateTimeStyles.None,
                out DateTime parsedDate))
        {
            Console.WriteLine("Failed to parse the Japanese era date.");
            return;
        }

        // Convert to ISO 8601 (format datetime yyyy-mm-dd)
        string isoDate = parsedDate.ToString("yyyy-MM-dd", CultureInfo.InvariantCulture);
        Console.WriteLine($"Original era date: {eraDate}");
        Console.WriteLine($"Converted ISO date: {isoDate}");
    }
}
```

**Ожидаемый вывод в консоли**

```
Original era date: R3-04-01
Converted ISO date: 2021-04-01
```

## Итоги

Мы рассмотрели, как **разобрать строки даты японской эры**:

1. Создаём `CultureInfo` для `ja-JP` и заменяем календарь на `JapaneseCalendar`.
2. Используем `DateTime.Parse` или более надёжный `TryParseExact` с пользовательским форматом.
3. Форматируем полученный `DateTime` с помощью `"yyyy-MM-dd"`, получая желаемый **format datetime yyyy-mm-dd**.

Это всё, что нужно, чтобы соединить устаревшие японские данные с современными ISO‑совместимыми системами.

## Что дальше?

- **Пакетная обработка:** Пройдитесь по CSV с датами эпох и запишите ISO‑строки в базу данных.
- **Локализация:** Преобразуйте ISO‑даты обратно в формат эпохи для отображения в UI (`ToString("ggyy年MM月dd日", japaneseCulture)`).
- **Пользовательские календари:** Исследуйте `TaiwanCalendar` или `HijriCalendar` для других региональных потребностей.

Экспериментируйте – меняйте строку эпохи, проверяйте граничные случаи или интегрируйте эту логику в эндпоинты ASP.NET Core. Если возникнут вопросы, оставляйте комментарий ниже; счастливого кодинга!

## Что стоит изучить дальше?

Следующие руководства охватывают тесно связанные темы, которые развивают техники, продемонстрированные в этом пособии. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы в собственных проектах.

- [How to Implement Date Validation in .NET Using Aspose.Cells: A Comprehensive Guide](/cells/english/net/data-validation/implement-date-validation-net-aspose-cells/)
- [Change Excel Date System to 1904 using Aspose.Cells .NET](/cells/english/net/calculation-engine/change-excel-date-system-aspose-cells-net/)
- [How to Implement and Format Excel Comments Using Aspose.Cells for .NET: A Step‑By‑Step Guide](/cells/english/net/comments-annotations/implement-format-excel-comments-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}