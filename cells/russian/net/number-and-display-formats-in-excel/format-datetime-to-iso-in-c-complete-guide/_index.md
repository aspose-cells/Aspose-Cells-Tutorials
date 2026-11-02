---
category: general
date: 2026-03-22
description: Узнайте, как форматировать дату и время в ISO при извлечении даты из
  Excel и отображать дату в формате ISO с помощью Aspose.Cells в C#.
draft: false
keywords:
- format datetime to iso
- extract date from excel
- display iso date
- Aspose.Cells date parsing
- Japanese era dates
language: ru
og_description: Форматирование даты и времени в ISO стало простым. Это руководство
  показывает, как извлечь дату из Excel и отобразить её в формате ISO с помощью Aspose.Cells.
og_title: Форматировать DateTime в ISO в C# – пошаговое руководство
tags:
- C#
- Aspose.Cells
- DateTime
- Excel
- ISO 8601
title: Форматирование DateTime в ISO в C# – Полное руководство
url: /ru/net/number-and-display-formats-in-excel/format-datetime-to-iso-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Форматирование datetime в ISO в C# – Полное руководство

Когда‑нибудь вам нужно было **format datetime to iso**, но источник находится в Excel‑файле? Возможно, ячейка содержит японскую эру, например “令和3年5月1日”, и вы ломаете голову, как превратить её в чистую строку `2021‑05‑01`. Вы не одиноки. В этом руководстве мы **extract date from excel**, разберём японскую эру и затем **display iso date** в консоли — всё с помощью нескольких строк C# и Aspose.Cells.

Мы пройдёмся по всему, что вам нужно: требуемый пакет NuGet, точный код, который можно скопировать‑вставить, почему важна каждая строка и несколько советов по краевым случаям. К концу вы получите переиспользуемый фрагмент, который **formats datetime to iso** независимо от того, насколько странным выглядит исходное значение в Excel.

## Что вам понадобится

- .NET 6.0 или новее (код также компилируется на .NET Framework 4.6+)
- Visual Studio 2022 (или любой другой предпочитаемый редактор)
- **Aspose.Cells for .NET** пакет NuGet – `Install-Package Aspose.Cells`
- Файл Excel (или новый рабочий лист), содержащий дату в формате японской эры

Это всё. Никаких дополнительных библиотек, без COM‑interop, только один хорошо задокументированный метод.

## Шаг 1: Создать рабочую книгу и записать дату в японской эре  

Сначала нам нужна рабочая книга. Если у вас уже есть файл Excel, его можно загрузить с помощью `new Workbook("path")`. В этом примере мы создадим новую рабочую книгу в памяти и поместим строку с японской эрой в ячейку **A1**.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a fresh workbook
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // 2️⃣ Write a Japanese era date (Reiwa 3 = 2021) into A1
        sheet.Cells["A1"].PutValue("令和3年5月1日");
```

> **Почему мы делаем это:** Aspose.Cells по умолчанию рассматривает значения ячеек как строки. Вставив необработанный текст эры, мы имитируем реальную ситуацию, когда японский клиент вводит даты в своей календарной системе.

## Шаг 2: Включить разбор японской эры и извлечь дату  

Aspose.Cells может автоматически преобразовывать строки с японской эрой в объекты .NET `DateTime` — при условии, что вы укажете это. Флаг `DateTimeParseOptions.EnableJapaneseEra` делает всю тяжёлую работу.

```csharp
        // 3️⃣ Retrieve the cell value while enabling Japanese era parsing
        CellValue parsed = sheet.Cells["A1"]
            .GetValue(CellValueType.DateTime, DateTimeParseOptions.EnableJapaneseEra);
```

> **Pro tip:** Если забыть опцию `EnableJapaneseEra`, библиотека вернёт исходную строку, и последующее преобразование завершится неудачей. Всегда проверяйте `parsed.Type`, если работаете со смешанным содержимым.

## Шаг 3: Преобразовать разобранный DateTime в ISO 8601  

Теперь, когда у нас есть корректный `DateTime`, превратить его в строку формата ISO — элементарно. Шаблон `"yyyy-MM-dd"` соответствует части даты ISO 8601, которую ожидают большинство API.

```csharp
        // 4️⃣ Convert to ISO 8601 (yyyy‑MM‑dd) and display it
        string isoDate = parsed.DateTimeValue.ToString("yyyy-MM-dd");
        Console.WriteLine($"ISO date: {isoDate}");
    }
}
```

> **Running the program prints:**  

```
ISO date: 2021-05-01
```

Это **display iso date**, который вы искали.

## Полный, исполняемый пример  

Ниже полностью готовый блок кода, который можно скопировать прямо в консольный проект. Никаких скрытых зависимостей, без дополнительной конфигурации.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Write a Japanese era date into cell A1
        worksheet.Cells["A1"].PutValue("令和3年5月1日");

        // Retrieve the cell value with Japanese era parsing enabled
        CellValue parsedValue = worksheet.Cells["A1"]
            .GetValue(CellValueType.DateTime, DateTimeParseOptions.EnableJapaneseEra);

        // Convert the DateTime to ISO 8601 format and output it
        string isoDate = parsedValue.DateTimeValue.ToString("yyyy-MM-dd");
        Console.WriteLine($"ISO date: {isoDate}");
    }
}
```

> **Expected output:** `ISO date: 2021-05-01`

## По‑шаговому разбору (Почему важна каждая часть)

| Шаг | Что происходит | Почему это важно |
|------|--------------|--------------------|
| **Create workbook** | Инициализирует контейнер Excel в памяти. | Даёт вам песочницу для тестов без доступа к файловой системе. |
| **PutValue** | Сохраняет необработанную строку японской эры в **A1**. | Имитирует реальный ввод данных; гарантирует, что парсер видит точный текст. |
| **GetValue with `EnableJapaneseEra`** | Преобразует строку эры в .NET `DateTime`. | Автоматически обрабатывает конвертацию календаря — без ручных таблиц соответствий. |
| **`ToString("yyyy-MM-dd")`** | Форматирует `DateTime` в ISO 8601. | Обеспечивает культурно‑независимую, сортируемую строку даты, принимаемую REST‑API, базами данных и т.д. |
| **Console.WriteLine** | Выводит окончательную ISO‑дату. | Подтверждает, что весь конвейер работает от начала до конца. |

## Обработка распространённых вариантов  

### 1. Другие расположения ячеек  

Если ваша дата находится в **B2** или в именованном диапазоне, просто замените `"A1"` на нужный адрес:

```csharp
worksheet.Cells["B2"].PutValue("令和2年12月31日");
var value = worksheet.Cells["B2"]
    .GetValue(CellValueType.DateTime, DateTimeParseOptions.EnableJapaneseEra);
```

### 2. Несколько дат в столбце  

Когда нужно **extract date from excel** для многих строк, пройдитесь по использованному диапазону в цикле:

```csharp
int lastRow = worksheet.Cells.MaxDataRow;
for (int i = 0; i <= lastRow; i++)
{
    var cell = worksheet.Cells[i, 0]; // column A
    var cv = cell.GetValue(CellValueType.DateTime, DateTimeParseOptions.EnableJapaneseEra);
    string iso = cv.DateTimeValue.ToString("yyyy-MM-dd");
    Console.WriteLine($"Row {i + 1}: {iso}");
}
```

### 3. Запасной вариант для дат без эры  

Если ячейка уже содержит стандартную строку даты, парсер всё равно сработает, но может потребоваться защита:

```csharp
CellValue cv = cell.GetValue(CellValueType.DateTime,
    DateTimeParseOptions.EnableJapaneseEra | DateTimeParseOptions.TryParse);
```

Флаг `TryParse` предотвращает исключения и возвращает исходное значение, если преобразование не удалось.

### 4. Компонент времени  

Если требуется также часть времени, используйте `"yyyy-MM-ddTHH:mm:ss"`:

```csharp
string isoDateTime = parsedValue.DateTimeValue.ToString("yyyy-MM-ddTHH:mm:ss");
```

Это даст полную метку времени ISO 8601 (`2021-05-01T00:00:00`).

## Визуальная подсказка  

![пример форматирования datetime в iso](image.png "Пример форматирования datetime в iso в C#")

*Alt text:* *пример форматирования datetime в iso, показывающий вывод консоли*

## Часто задаваемые вопросы  

- **Можно ли использовать это с файлами .xls?**  
  Да. Aspose.Cells поддерживает `.xls`, `.xlsx`, `.csv` и многие другие форматы «из коробки».

- **Что делать, если рабочая книга защищена паролем?**  
  Загрузите её с помощью `new Workbook("file.xlsx", new LoadOptions { Password = "secret" })`.

- **Зависит ли формат ISO от локали?**  
  Нет. Шаблон `"yyyy-MM-dd"` культурно‑независим, гарантируя одинаковую строку на любой машине.

- **Работает ли это на .NET Core?**  
  Абсолютно — Aspose.Cells совместим с .NET Standard 2.0.

## Итоги  

Мы рассмотрели, как **format datetime to iso** путем **extracting date from excel**, разбора строк с японской эрой и последующего **display iso date** в консоли. Основные шаги — создать рабочую книгу, записать или загрузить текст эры, включить разбор японской эры и отформатировать с помощью `ToString("yyyy-MM-dd")` — покрывают большинство сценариев.

Дальше вы можете:

- Записать ISO‑даты обратно в другой столбец для последующей обработки.  
- Экспортировать преобразованную рабочую книгу в CSV для массового импорта.  
- Скомбинировать эту логику с веб‑API, принимающим загрузки Excel и возвращающим JSON‑закодированные ISO‑даты.

Экспериментируйте с различными форматами дат, часовыми поясами или даже пользовательскими календарями. Гибкость Aspose.Cells позволяет почти всегда находить решение.

Счастливого кодинга, и пусть все ваши даты будут идеально ISO‑совместимыми!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}