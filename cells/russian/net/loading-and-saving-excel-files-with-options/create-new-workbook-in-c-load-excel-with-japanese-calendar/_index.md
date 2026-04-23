---
category: general
date: 2026-02-26
description: Создайте новую рабочую книгу в C# и узнайте, как загружать файлы Excel,
  установить календарь на японский и без труда извлекать даты из Excel.
draft: false
keywords:
- create new workbook
- how to load excel
- how to set calendar
- extract date from excel
- read japanese dates
language: ru
og_description: Создайте новую рабочую книгу в C# и быстро научитесь загружать Excel,
  задавать японский календарь и извлекать даты из файлов Excel.
og_title: Создать новую книгу в C# — загрузить Excel с японским календарём
tags:
- C#
- Excel
- Aspose.Cells
- DateTime
title: Создать новую рабочую книгу в C# — загрузить Excel с японским календарём
url: /ru/net/loading-and-saving-excel-files-with-options/create-new-workbook-in-c-load-excel-with-japanese-calendar/
---

code blocks; there are none besides placeholders. So fine.

Now produce final answer.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание новой книги в C# – загрузка Excel с японским календарём

Когда‑нибудь вам нужно было **create new workbook** в C#, но вы не были уверены, как заставить Excel учитывать японский календарь? Вы не одиноки. Во многих корпоративных сценариях вы получаете таблицы, в которых даты хранятся в системе японских эпох, и правильное извлечение этих дат может ощущаться как расшифровка секретного языка.

Суть в том, что вы можете **create new workbook**, указать загрузчику интерпретировать даты с использованием японского календаря, а затем **extract date from excel** всего несколькими строками кода. В этом руководстве мы пройдёмся по *how to load excel*, *how to set calendar* для японских дат и, наконец, *read Japanese dates* из ячейки. Без лишних слов — только полностью готовый к запуску пример, который вы можете скопировать и вставить в свой проект.

## Требования

- .NET 6.0 или новее (код также работает на .NET Framework 4.6+)
- Библиотека **Aspose.Cells** (бесплатная пробная версия или лицензированная). Установите её через NuGet:

```bash
dotnet add package Aspose.Cells
```

- Excel‑файл (`JapanDates.xlsx`), содержащий даты в японской системе эпох в ячейке A1.

Вот и всё. Если у вас есть всё необходимое, можно сразу приступать.

---

## Создание новой книги и установка японского календаря

Первый шаг — **create new workbook** объект и настройка `LoadOptions`, чтобы парсер знал, какой календарь использовать.

```csharp
using Aspose.Cells;
using System;

class JapaneseDateReader
{
    static void Main()
    {
        // Step 1: Create a new workbook instance
        Workbook workbook = new Workbook();

        // Step 2: Set load options to interpret dates using the Japanese calendar
        workbook.LoadOptions = new LoadOptions { Calendar = CalendarType.Japanese };

        // Step 3: Load the workbook from a file
        workbook.Load("YOUR_DIRECTORY/JapanDates.xlsx");

        // Step 4: Access cell A1 – it now contains a proper DateTime value
        var cellA1 = workbook.Worksheets[0].Cells["A1"];
        DateTime dateValue = cellA1.GetDateTime();

        Console.WriteLine($"The Japanese date in A1 is: {dateValue:yyyy-MM-dd}");
    }
}
```

> **Pro tip:** Свойство `LoadOptions.Calendar` принимает несколько перечислений (`Gregorian`, `Japanese`, `Hijri` и т.д.). Выбор правильного гарантирует, что библиотека преобразует текст эпохи (например, «令和3年») в .NET `DateTime`.

![скриншот примера создания новой книги](image-url.png "Скриншот, показывающий экземпляр новой книги с настройками японского календаря"){: .align-center alt="скриншот примера создания новой книги"}

### Почему это работает

- **Workbook creation**: `new Workbook()` предоставляет чистый лист — без скрытых листов, без данных по умолчанию.
- **LoadOptions**: При назначении `CalendarType.Japanese` *до* вызова `Load` парсер рассматривает любые строки с эпохой как даты, а не как обычный текст.
- **GetDateTime()**: После загрузки `cellA1.GetDateTime()` возвращает настоящий объект `DateTime`, позволяя выполнять арифметические операции, форматирование или вставку в базу данных без дополнительных шагов преобразования.

---

## Как правильно загрузить файл Excel

Вы можете задаться вопросом: «Есть ли особый способ **how to load excel** при работе с не‑григорианскими календарями?» Ответ — да, всегда задавайте `LoadOptions` *до* вызова `Load`. Если сначала загрузить, а затем изменить календарь, даты уже будут разобраны неверно.

```csharp
// Example of a wrong order – will treat Japanese dates as plain strings
Workbook badWorkbook = new Workbook();
badWorkbook.Load("JapanDates.xlsx");          // Loads with default Gregorian calendar
badWorkbook.LoadOptions.Calendar = CalendarType.Japanese; // Too late!
```

Приведённый выше фрагмент демонстрирует распространённую ошибку. Правильный порядок (как показано в предыдущем разделе) гарантирует, что движок интерпретирует ячейки *как даты* с самого начала.

---

## Как установить календарь для японских дат

Если необходимо переключать календари «на лету» — например, обрабатывать пакет файлов, использующих разные системы эпох — вы можете переиспользовать один и тот же объект `Workbook`, создавая новые `LoadOptions` каждый раз.

```csharp
void LoadWithCalendar(string filePath, CalendarType calendar)
{
    Workbook wb = new Workbook
    {
        LoadOptions = new LoadOptions { Calendar = calendar }
    };
    wb.Load(filePath);
    // Now you can read dates according to the chosen calendar
}
```

Вызов `LoadWithCalendar("JapanDates.xlsx", CalendarType.Japanese)` даёт тот же результат, что и наш основной пример, тогда как `CalendarType.Gregorian` будет рассматривать ту же ячейку как обычную строку (или выбросит исключение, если формат не распознан).

---

## Извлечение даты из Excel — чтение японских дат

Теперь, когда книга загружена с правильным календарём, извлечение даты становится простым. Метод `Cell.GetDateTime()` возвращает `DateTime`, учитывающий преобразование эпох.

```csharp
DateTime ExtractJapaneseDate(Workbook wb, string address)
{
    var cell = wb.Worksheets[0].Cells[address];
    return cell.GetDateTime(); // Returns a .NET DateTime
}

// Usage
DateTime japaneseDate = ExtractJapaneseDate(workbook, "A1");
Console.WriteLine($"Extracted date: {japaneseDate:d}");
```

### Пограничные случаи и сценарии «что если»

| Ситуация                              | Что делать                                                                                               |
|--------------------------------------|----------------------------------------------------------------------------------------------------------|
| Ячейка содержит **текст** вместо даты | Сначала вызовите `cell.GetString()`, проверьте с помощью `DateTime.TryParse` или примените проверку данных в Excel. |
| Необходимо обработать несколько листов | Пройдитесь по `workbook.Worksheets` и примените ту же логику извлечения к каждому листу.                   |
| Даты хранятся как **числа** (серийные даты Excel) | `cell.GetDateTime()` всё равно работает, поскольку Aspose.Cells автоматически преобразует серийные числа.            |
| Файл **защищён паролем**            | Установите `LoadOptions.Password = "yourPwd"` перед вызовом `Load`.                                           |

---

## Полный рабочий пример (готовый к копированию и вставке)

Ниже приведена полная программа, которую можно вставить в консольное приложение. Она включает обработку ошибок и демонстрирует все четыре вспомогательных ключевых слова в контексте.

```csharp
using Aspose.Cells;
using System;

class JapaneseDateReader
{
    static void Main()
    {
        // --------------------------------------------------------------------
        // 1️⃣  Create new workbook and configure calendar (primary keyword)
        // --------------------------------------------------------------------
        Workbook workbook = new Workbook
        {
            LoadOptions = new LoadOptions { Calendar = CalendarType.Japanese }
        };

        // --------------------------------------------------------------------
        // 2️⃣  How to load excel – correct order matters (secondary keyword)
        // --------------------------------------------------------------------
        try
        {
            workbook.Load("YOUR_DIRECTORY/JapanDates.xlsx");
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Failed to load Excel file: {ex.Message}");
            return;
        }

        // --------------------------------------------------------------------
        // 3️⃣  How to set calendar – already done before loading (secondary)
        // --------------------------------------------------------------------
        // (If you need to change it later, see the LoadWithCalendar method above.)

        // --------------------------------------------------------------------
        // 4️⃣  Extract date from excel – read Japanese dates (secondary keywords)
        // --------------------------------------------------------------------
        try
        {
            var cell = workbook.Worksheets[0].Cells["A1"];
            DateTime japaneseDate = cell.GetDateTime(); // Proper DateTime thanks to the calendar setting
            Console.WriteLine($"Japanese date in A1 → {japaneseDate:yyyy-MM-dd}");
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Error extracting date: {ex.Message}");
        }
    }
}
```

**Ожидаемый вывод** (при условии, что A1 содержит «令和3年5月12日»):

```
Japanese date in A1 → 2021-05-12
```

Если ячейка содержит григорианскую дату, например «2021‑05‑12», тот же код всё равно работает, поскольку библиотека плавно переходит к григорианской интерпретации.

---

## Заключение

Теперь вы знаете, как **create new workbook**, правильно **how to load excel**, установить соответствующий **how to set calendar**, и наконец **extract date from excel**, одновременно **read Japanese dates**, без какого‑либо ручного парсинга. Главное — календарь должен быть задан *до* загрузки; после того как книга находится в памяти, даты уже материализованы как корректные объекты `DateTime`.

### Что дальше?

- **Batch processing**: Пройдитесь по папке с файлами, вызывая `LoadWithCalendar` для каждого.
- **Export to other formats**: Используйте `workbook.Save("output.csv")` после конвертации.
- **Localization**: Скомбинируйте `CultureInfo` с `DateTime.ToString`, чтобы отображать даты на предпочтительном языке пользователя.

Не стесняйтесь экспериментировать — замените `CalendarType.Japanese` на `CalendarType.Hijri` или `CalendarType.Gregorian` и наблюдайте, как тот же код автоматически адаптируется. Если возникнут проблемы, оставьте комментарий ниже или ознакомьтесь с документацией Aspose.Cells для более глубоких сведений об API.

Удачной разработки, и наслаждайтесь преобразованием загадочных японских дат эпох в чистые .NET `DateTime` значения!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}