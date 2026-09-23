---
category: general
date: 2026-03-25
description: Создайте книгу Excel из JSON и сохраните её в формате xlsx. Узнайте,
  как экспортировать JSON в xlsx, генерировать Excel из JSON и заполнять Excel из
  JSON за считанные минуты.
draft: false
keywords:
- create excel workbook
- export json to xlsx
- generate excel from json
- populate excel from json
- save workbook as xlsx
language: ru
og_description: Создайте книгу Excel из JSON мгновенно. Это руководство показывает,
  как экспортировать JSON в XLSX, генерировать Excel из JSON и заполнять Excel из
  JSON с помощью Aspose.Cells.
og_title: Создание Excel‑книги из JSON – Полный учебник по C#
tags:
- Aspose.Cells
- C#
- JSON
- Excel automation
title: Создание Excel‑книги из JSON – пошаговое руководство
url: /ru/net/excel-data-import-export/create-excel-workbook-from-json-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание Excel Workbook из JSON – Полный учебник C#

Когда‑нибудь вам нужно было **create excel workbook** из JSON‑payload, но вы не знали, с чего начать? Вы не одиноки; многие разработчики сталкиваются с этой проблемой, пытаясь превратить данные API в аккуратную таблицу. Хорошая новость? Всего несколькими строками C# и Aspose.Cells вы можете **export json to xlsx**, **generate excel from json** и **populate excel from json** без использования сторонних конвертеров.

В этом руководстве мы пройдем весь процесс — начиная с сырой строки JSON, помещая её в SmartMarker и, наконец, **save workbook as xlsx** на диск. В конце у вас будет готовый к использованию Excel‑файл, выглядящий так:

| Name | Score |
|------|-------|
| John | 90    |
| Anna | 85    |

> **Pro tip:** Если вы уже используете Aspose.Cells в другом месте вашего проекта, вы можете переиспользовать тот же экземпляр `Workbook` для нескольких импортов JSON — это удобно для пакетной обработки.

---

## Что вам понадобится

- **.NET 6+** (или любой современный .NET Framework, поддерживающий C# 10)
- **Aspose.Cells for .NET** — установить через NuGet: `dotnet add package Aspose.Cells`
- Базовое понимание синтаксиса C# (глубокие знания Excel не требуются)

И всё. Никаких внешних сервисов, без COM‑interop, только чистый управляемый код.

---

## Шаг 1: Инициализировать новый Excel Workbook

Первое, что мы делаем, — создаём новый объект workbook. Представьте это как открытие пустого Excel‑файла, в который мы позже вставим наши данные.

```csharp
using Aspose.Cells;

// Step 1: Create a new workbook and grab the first worksheet
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.Worksheets[0];
```

Зачем начинать с нового workbook? Это гарантирует чистый лист, предотвращает оставшиеся стили от предыдущих запусков и сохраняет размер файла минимальным — идеально для автоматизированных конвейеров.

---

## Шаг 2: Подготовить JSON‑данные для импорта

Для демонстрации мы используем небольшой массив JSON, но вы можете заменить его любым корректным JSON, полученным от веб‑сервиса, из файла или результата запроса к базе данных.

```csharp
// Step 2: JSON string representing a simple collection of records
string jsonData = "[{\"Name\":\"John\",\"Score\":90},{\"Name\":\"Anna\",\"Score\":85}]";
```

Обратите внимание на двойные экранированные кавычки (`\"`) — это просто синтаксис строкового литерала C#. В реальном сценарии вы, скорее всего, будете читать это из файла:

```csharp
// string jsonData = File.ReadAllText("data.json");
```

---

## Шаг 3: Сообщить SmartMarker рассматривать весь массив как одну запись

Движок SmartMarker в Aspose.Cells может автоматически итерировать коллекции. Включив **ArrayAsSingle**, мы рассматриваем весь массив JSON как одну запись, что именно нужно для плоской таблицы.

```csharp
// Step 3: Configure SmartMarker options – array‑as‑single mode
SmartMarkerOptions options = new SmartMarkerOptions
{
    ArrayAsSingle = true   // This makes the whole JSON array behave like one record
};
```

Если забыть этот флаг, SmartMarker попытается создать отдельный лист для каждого элемента — это точно не то, что вам нужно при генерации простой таблицы.

---

## Шаг 4: Поместить токен SmartMarker в лист

Токены SmartMarker выглядят как `${jsonArray}`. Когда процессор запускается, он заменяет токен данными из JSON‑источника. Мы разместим токен в ячейке **A1**, чтобы вывод начался в левом верхнем углу.

```csharp
// Step 4: Insert the SmartMarker token into cell A1
worksheet.Cells["A1"].PutValue("${jsonArray}");
```

Вы также можете предварительно отформатировать строку заголовка перед обработкой. Например, установить полужирный шрифт для первой строки:

```csharp
Cell headerCell = worksheet.Cells["A1"];
headerCell.Style.Font.IsBold = true;
```

---

## Шаг 5: Запустить процессор SmartMarker

Теперь происходит магия. Процессор читает JSON, сопоставляет каждое свойство с колонкой и записывает строки под токеном.

```csharp
// Step 5: Process the SmartMarker with our JSON data and options
worksheet.SmartMarkerProcessor.Process(jsonData, options);
```

За кулисами Aspose.Cells:

1. Парсит JSON в объект .NET.
2. Сопоставляет имена свойств (`Name`, `Score`) заголовкам колонок.
3. Записывает каждый элемент массива как новую строку.

Если ваш JSON содержит вложенные объекты, вы можете ссылаться на них через точечную нотацию (`${parent.child}`) — удобно для более сложных отчётов.

---

## Шаг 6: Сохранить Workbook как файл XLSX

Наконец, сохраняем workbook на диск. Расширение файла `.xlsx` сообщает Excel (и большинству других табличных приложений), что это рабочая книга OpenXML.

```csharp
// Step 6: Save the workbook to a file
string outputPath = Path.Combine(Environment.CurrentDirectory, "json-single.xlsx");
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

Конечно, вы можете напрямую передать workbook в HTTP‑ответ, если создаёте веб‑API:

```csharp
// Example for ASP.NET Core
using (var stream = new MemoryStream())
{
    workbook.Save(stream, SaveFormat.Xlsx);
    stream.Position = 0;
    return File(stream, "application/vnd.openxmlformats-officedocument.spreadsheetml.sheet", "data.xlsx");
}
```

---

## Полный рабочий пример

Ниже приведена полностью готовая к запуску программа, включающая каждый из описанных шагов. Скопируйте её в новый консольный проект и нажмите **F5**.

```csharp
using System;
using System.IO;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ JSON data to be merged into the sheet
        string jsonData = "[{\"Name\":\"John\",\"Score\":90},{\"Name\":\"Anna\",\"Score\":85}]";

        // 3️⃣ Enable array‑as‑single mode so the whole array is one record
        SmartMarkerOptions options = new SmartMarkerOptions
        {
            ArrayAsSingle = true
        };

        // 4️⃣ Put a SmartMarker token in A1 that points to the JSON array
        worksheet.Cells["A1"].PutValue("${jsonArray}");

        // Optional: make the header bold for better readability
        worksheet.Cells["A1"].Style.Font.IsBold = true;

        // 5️⃣ Process the SmartMarker with the JSON payload
        worksheet.SmartMarkerProcessor.Process(jsonData, options);

        // 6️⃣ Save the result as an XLSX file
        string outputPath = Path.Combine(Environment.CurrentDirectory, "json-single.xlsx");
        workbook.Save(outputPath);

        Console.WriteLine($"✅ Workbook created and saved to: {outputPath}");
    }
}
```

**Ожидаемый результат:** При открытии `json-single.xlsx` вы увидите две строки под жирным заголовком — `John` со счётом `90` и `Anna` со счётом `85`. Имена колонок автоматически выводятся из имён свойств JSON.

---

## Часто задаваемые вопросы и особые случаи

### Что делать, если ключи JSON содержат пробелы или специальные символы?

SmartMarker ожидает корректные имена идентификаторов. Замените пробелы на подчёркивания или используйте пользовательское сопоставление:

```csharp
// Example JSON: {"First Name":"John"}
string jsonData = "[{\"First_Name\":\"John\",\"Score\":90}]";
// Token stays the same – Aspose.Cells will map "First_Name" to column header "First_Name"
```

### Как экспортировать большой массив JSON (тысячи строк)?

Процессор потоково обрабатывает данные, поэтому потребление памяти остаётся умеренным. Тем не менее, вы можете:

- Увеличить лимит `MaxRows` листа (`worksheet.Cells.MaxRow = 1_048_576;` — максимум Excel).
- Отключить сетку для повышения производительности (`worksheet.IsGridlinesVisible = false;`).

### Можно ли добавить несколько JSON‑таблиц в один workbook?

Конечно. Просто разместите разные токены SmartMarker в отдельных диапазонах (например, `${orders}` в `A10`, `${customers}` в `D1`) и вызовите `Process` один раз для каждого токена или один раз для составного JSON‑объекта, содержащего оба массива.

---

## Бонус: Добавление простого графика (опционально)

Если хотите визуализировать оценки, добавьте быстрый столбчатый график после заполнения данных:

```csharp
// Insert a column chart starting at cell E1
int chartIndex = worksheet.Charts.Add(ChartType.Column, 0, 4, 15, 10);
Chart chart = worksheet.Charts[chartIndex];
chart.NSeries.Add("B2:B3", true);
chart.NSeries[0].Name = "Score";
chart.Title.Text = "Scores by Name";
```

График автоматически привяжется к только что добавленным строкам, предоставив вам готовый отчёт в один клик.

---

## Заключение

Теперь вы знаете, **how to create excel workbook** из строки JSON, **export json to xlsx**, **generate excel from json** и **populate excel from json** с помощью функции SmartMarker в Aspose.Cells. Полное решение — инициализация workbook, настройка SmartMarker, обработка JSON и сохранение файла — вмещается в несколько строк кода, но масштабируется до огромных наборов данных.

Что дальше? Попробуйте заменить статический JSON вызовом API, добавить условное форматирование в зависимости от оценок или генерировать несколько листов для разных доменов данных. Та же схема работает с CSV, XML или даже результатами запросов к базе данных — просто измените строку‑источник и подкорректируйте токен SmartMarker.

Счастливого кодинга, и пусть ваши таблицы всегда остаются аккуратными!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}