---
category: general
date: 2026-09-24
description: Разбор DateTime с учётом японской императорской эпохи с использованием
  Aspose.Cells в C#. Включите японский календарь эпох, записывайте строки эпох и получайте
  точные значения DateTime.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- Parse DateTime with Japanese Emperor Reign
- Aspose.Cells
- C# date parsing
- Japanese era calendar
- Workbook Settings
- DateTimeValue
language: ru
lastmod: 2026-09-24
og_description: Разбор DateTime с учётом японской императорской эпохи с помощью Aspose.Cells
  в C#. В этом руководстве показано, как включить японский календарь эпох, записывать
  строки эпох и корректно считывать DateTime.
og_image_alt: Screenshot of C# code parsing a Japanese era date with Aspose.Cells
og_title: Разбор DateTime с учётом правления японского императора с использованием
  Aspose.Cells – руководство C#
schemas:
- author: Aspose
  dateModified: '2026-09-24'
  description: Parse DateTime with Japanese Emperor Reign using Aspose.Cells in C#.
    Enable the Japanese era calendar, write era strings, and retrieve accurate DateTime
    values.
  headline: Parse DateTime with Japanese Emperor Reign using Aspose.Cells
  type: TechArticle
- description: Parse DateTime with Japanese Emperor Reign using Aspose.Cells in C#.
    Enable the Japanese era calendar, write era strings, and retrieve accurate DateTime
    values.
  name: Parse DateTime with Japanese Emperor Reign using Aspose.Cells
  steps:
  - name: Multiple era formats
    text: 'Aspose.Cells recognises several era representations:'
  - name: Invalid strings
    text: 'When the string cannot be parsed (e.g., `"令和99年13月40日"`), `DateTimeValue`
      returns `DateTime.MinValue`. You can check for this condition:'
  - name: Disabling the feature
    text: 'If you later need to store raw era strings without conversion, set the
      flag back to `false`:'
  - name: Performance tip
    text: Enabling the era calendar adds a small overhead to every `PutValue` call
      that involves strings. If you only parse a handful of cells, enable the flag
      right before the operation and disable it afterward to minimise impact.
  type: HowTo
tags:
- Aspose.Cells
- C#
- DateTime
- Japanese era
- .NET
title: Разбор DateTime с учётом японского императорского правления с помощью Aspose.Cells
url: /ru/net/excel-custom-number-date-formatting/parse-datetime-with-japanese-emperor-reign-using-aspose-cell/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Разбор DateTime с японским императорским правлением с использованием Aspose.Cells

Если вам нужно **разобрать DateTime с японским императорским правлением** в .NET‑приложении, это руководство покажет, как сделать это с помощью Aspose.Cells. Включив календарь японских эпох, записав строку с эпохой и считав полученное значение `DateTime`, вы получаете надёжные, учитывающие культуру даты без ручной обработки строк.

Работа с датами японских эпох распространена в финансах, государственных учреждениях и наследуемых системах, которые всё ещё хранят даты вроде “令和3年5月10日”. В этом учебнике рассматривается полный рабочий процесс: от настройки проекта до получения объекта `DateTime`, которым можно пользоваться в вычислениях, журналировании или отображении в UI.

## Что вы узнаете

- Как добавить пакет NuGet Aspose.Cells в проект C#.  
- Как включить **японский календарь эпох** через `Workbook.Settings`.  
- Как записать строку даты в японской эпохе в ячейку и позволить Aspose.Cells автоматически её разобрать.  
- Как прочитать разобранный `DateTime` с помощью свойства `DateTimeValue`.  

**Требования**  
- .NET 6.0 или новее (код также работает с .NET Framework 4.7+).  
- Базовые знания C# и Visual Studio (или любой другой IDE).  
- Доступ в интернет для загрузки пакета Aspose.Cells.

---

## Шаг 1: Установить Aspose.Cells

Откройте папку проекта в терминале или в консоли менеджера пакетов NuGet и выполните:

```bash
dotnet add package Aspose.Cells
```

Или в Visual Studio щёлкните правой кнопкой мыши по проекту → **Manage NuGet Packages** → найдите **Aspose.Cells** и нажмите **Install**.  
Это добавит сборку `Aspose.Cells`, которая предоставляет классы `Workbook`, `Worksheet` и возможности разбора, необходимые нам.

## Шаг 2: Включить японский календарь эпох

По умолчанию Aspose.Cells отключает разбор японских эпох. Необходимо включить его через флаг `Workbook.Settings.UseJapaneseEraCalendar`.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // Create a new workbook instance
        Workbook workbook = new Workbook();

        // Enable parsing of Japanese era dates (e.g., 令和, 平成)
        workbook.Settings.UseJapaneseEraCalendar = true;
```

Установка `UseJapaneseEraCalendar` в `true` сообщает библиотеке интерпретировать строки, содержащие названия эпох (`令和`, `平成`, `昭和` и т.д.) согласно официальным правилам японского календаря.

## Шаг 3: Записать строку даты в японской эпохе в ячейку

Далее получаем первый лист и помещаем строку даты в японской эпохе в ячейку **A1**.

```csharp
        // Access the first worksheet (index 0)
        Worksheet sheet = workbook.Worksheets[0];

        // Write the era‑based date string into cell A1
        sheet.Cells["A1"].PutValue("令和3年5月10日");
```

**Почему это работает:**  
Когда `UseJapaneseEraCalendar` активен, `PutValue` анализирует строку, обнаруживает префикс эпохи (`令和`) и внутренне преобразует её в соответствующий григорианский год (2021). Библиотека затем сохраняет значение как настоящий объект `DateTime`, а не просто текст.

## Шаг 4: Получить разобранное значение `DateTime`

Теперь читаем свойство `DateTimeValue` ячейки. Aspose.Cells автоматически возвращает григорианскую дату.

```csharp
        // Retrieve the parsed DateTime from cell A1
        DateTime parsedDate = sheet.Cells["A1"].DateTimeValue;

        // Output the result to the console
        Console.WriteLine($"Parsed Gregorian date: {parsedDate:yyyy-MM-dd}");
    }
}
```

Запуск программы выводит:

```
Parsed Gregorian date: 2021-05-10
```

Вывод подтверждает, что **Parse DateTime with Japanese Emperor Reign** корректно преобразовал “令和3年5月10日” в 10 мая 2021 года.

## Шаг 5: Обработка граничных случаев и распространённых вариантов

### Несколько форматов эпох
Aspose.Cells распознаёт несколько представлений эпох:

| Эра (японская) | Диапазон годов по григорианскому календарю |
|----------------|--------------------------------------------|
| 明治 (Meiji)   | 1868‑1912                                 |
| 大正 (Taishō)  | 1912‑1926                                 |
| 昭和 (Shōwa)   | 1926‑1989                                 |
| 平成 (Heisei)  | 1989‑2019                                 |
| 令和 (Reiwa)   | 2019‑present                              |

Если ваши исходные данные содержат полноширинные символы, пробелы или используют кандзи “年”, “月”, “日”, парсер всё равно справится. Например, `"平成31年4月30日"` преобразуется в `2019-04-30`.

### Неправильные строки
Когда строку нельзя разобрать (например, `"令和99年13月40日"`), `DateTimeValue` возвращает `DateTime.MinValue`. Можно проверить это условие:

```csharp
if (parsedDate == DateTime.MinValue)
{
    Console.WriteLine("The cell does not contain a valid Japanese era date.");
}
```

### Отключение функции
Если позже понадобится сохранять исходные строки эпох без преобразования, установите флаг обратно в `false`:

```csharp
workbook.Settings.UseJapaneseEraCalendar = false;
```

### Совет по производительности
Включение календаря эпох добавляет небольшие накладные расходы к каждому вызову `PutValue`, работающему со строками. Если вы разбираете лишь несколько ячеек, включайте флаг непосредственно перед операцией и отключайте его после, чтобы минимизировать влияние.

## Полный, готовый к запуску пример

Ниже полностью готовая программа, которую можно скопировать, вставить и сразу запустить.

```csharp
using Aspose.Cells;
using System;

class ParseJapaneseEraDemo
{
    static void Main()
    {
        // 1️⃣ Create a new workbook
        Workbook workbook = new Workbook();

        // 2️⃣ Turn on Japanese era parsing
        workbook.Settings.UseJapaneseEraCalendar = true;

        // 3️⃣ Access the first worksheet
        Worksheet sheet = workbook.Worksheets[0];

        // 4️⃣ Write an era date string into A1
        sheet.Cells["A1"].PutValue("令和3年5月10日");

        // 5️⃣ Retrieve the parsed DateTime
        DateTime parsedDate = sheet.Cells["A1"].DateTimeValue;

        // Verify the result
        Console.WriteLine($"Parsed Gregorian date: {parsedDate:yyyy-MM-dd}");
        // Expected output: Parsed Gregorian date: 2021-05-10
    }
}
```

**Ожидаемый вывод**

```
Parsed Gregorian date: 2021-05-10
```

Программа демонстрирует сквозной процесс **Parse DateTime with Japanese Emperor Reign** с использованием Aspose.Cells: от создания книги до получения пригодного объекта `DateTime`.

---

## Заключение

Теперь вы знаете, как **разобрать DateTime с японским императорским правлением** в C#:

1. Установить **Aspose.Cells**.  
2. Включить **японский календарь эпох** через `Workbook.Settings`.  
3. Записать строки с эпохой в ячейки.  
4. Прочитать полученное `DateTimeValue`.  

Этот подход устраняет необходимость в ручной логике разбора, учитывает официальные границы эпох и без проблем интегрируется в существующий код .NET для работы с датами.  

**Следующие шаги**  
- Изучите другие культурно‑специфичные возможности Aspose.Cells, такие как **C# date parsing** для хиджра или тайского буддийского календарей.  
- Скомбинируйте эту технику с настройками книги, например `CalcEngine`, чтобы вычислять формулы, ссылающиеся на даты эпох.  
- Используйте разобранный `DateTime` в отчётах, хранении в базе данных или UI‑компонентах, которым нужны григорианские даты.

Экспериментируйте с различными строками эпох, обрабатывайте некорректный ввод и интегрируйте решение в более крупные конвейеры импорта данных. Приятного кодинга!

## Что вам следует изучить дальше?

Следующие учебники охватывают тесно связанные темы, которые расширяют техники, продемонстрированные в этом руководстве. Каждый ресурс содержит полностью работающие примеры кода с пошаговыми объяснениями, помогающими освоить дополнительные возможности API и исследовать альтернативные подходы в ваших проектах.

- [Разбор японских дат эпох в Excel – Полное руководство для разработчиков C#](/cells/english/net/data-loading-and-parsing/parse-japanese-era-dates-in-excel-full-guide-for-c-developer/)
- [Как разобрать японские даты в C# – Полное руководство](/cells/english/net/data-loading-and-parsing/how-to-parse-japanese-dates-in-c-complete-guide/)
- [Как реализовать проверку дат в .NET с помощью Aspose.Cells: Полное руководство](/cells/english/net/data-validation/implement-date-validation-net-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}