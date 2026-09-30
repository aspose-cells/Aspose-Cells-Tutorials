---
category: general
date: 2026-05-23
description: Создайте динамическую таблицу Excel, используя шаблон и данные JSON.
  Узнайте, как загрузить шаблон Excel, автоматизировать отчет Excel и быстро заполнить
  Excel из JSON.
draft: false
keywords:
- create dynamic excel table
- load excel template
- automate excel report
- populate excel from json
- generate excel report json
language: ru
og_description: Создайте динамическую таблицу Excel за считанные минуты с помощью
  шаблона и JSON. Этот учебник показывает, как загрузить шаблон Excel, автоматизировать
  отчет Excel и заполнить Excel из JSON.
og_title: Создайте динамическую таблицу Excel — руководство по Smart Marker
schemas:
- author: Aspose
  dateModified: '2026-05-23'
  description: Create dynamic excel table using a template and JSON data. Learn how
    to load excel template, automate excel report, and populate excel from json quickly.
  headline: Create Dynamic Excel Table – Smart Marker Guide
  type: TechArticle
tags:
- Excel
- Smart Markers
- JSON
- .NET
title: Создание динамической таблицы Excel — руководство по Smart Marker
url: /ru/net/smart-markers-dynamic-data/create-dynamic-excel-table-smart-marker-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание динамической таблицы Excel – Руководство по Smart Marker

Когда‑нибудь вам нужно было **создать динамическую таблицу Excel**, которая автоматически расширяется для каждой записи в вашем наборе данных? Вы не одиноки. Независимо от того, создаёте ли вы ежемесячную панель продаж или набор счетов для каждого клиента, возможность **заполнять Excel из JSON** без написания бесконечных циклов может сэкономить часы.

В этом руководстве мы пошагово рассмотрим полное практическое решение, показывающее, как **загрузить шаблон Excel**, внедрить Smart Marker, передать ему JSON и, наконец, **автоматизировать генерацию отчёта Excel**. К концу вы получите готовый к запуску .NET‑проект, который создаёт отшлифованную книгу Excel из единого JSON‑payload.

---

## Что понадобится

- **Aspose.Cells for .NET** (или любая библиотека, поддерживающая Smart Markers). В примере используется версия 24.5, но подойдёт любой недавний релиз.
- Visual Studio 2022 (или ваша любимая IDE для C#).
- Простой файл шаблона Excel (`template.xlsx`), размещённый в папке, которой вы управляете.
- Строка JSON, содержащая коллекцию с именем `Customers`.

Это всё — без дополнительных сервисов, без подключений к базе данных, только чистый код.

---

## Шаг 1: Создание шаблонной книги – Загрузка шаблона Excel

Первое, что мы делаем, — **загружаем шаблон Excel** в память. Представьте шаблон как холст, где специальный плейсхолдер указывает процессору, где повторять строки.

```csharp
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

// Load the template workbook (make sure the path is correct)
Workbook workbook = new Workbook(@"C:\Reports\template.xlsx");

// Grab the first worksheet – this is where our Smart Marker lives
Worksheet worksheet = workbook.Worksheets[0];
```

> **Почему это важно:** Загрузка шаблона один раз минимизирует ввод‑вывод файлов и позволяет переиспользовать один и тот же макет для множества отчётов. Кроме того, это изолирует логику Smart Marker от остального кода, обеспечивая чистое разделение ответственности.

---

## Шаг 2: Вставка Smart Marker – Создание динамической таблицы Excel

Теперь мы внедряем **Smart Marker**, который будет повторять таблицу для каждой записи в коллекции `Customers`. Синтаксис `${Customers.RepeatWorksheet}` сообщает Aspose.Cells клонировать весь лист для каждого клиента.

```csharp
// Place the Smart Marker in cell A1 (top‑left corner)
worksheet.Cells[0, 0].PutValue("${Customers.RepeatWorksheet}");
```

> **Pro tip:** Если нужно повторять только строки, а не целые листы, используйте `${Customers.Repeat}` в первой строке таблицы. Повторение на уровне листа удобно, когда каждому клиенту нужен отдельный таб.

---

## Шаг 3: Подготовка SmartMarkerProcessor – Автоматизация отчёта Excel

С установленным маркером мы создаём `SmartMarkerProcessor`. Этот объект оркестрирует привязку данных между JSON и шаблоном Excel.

```csharp
// Initialize the processor with the workbook that contains the marker
SmartMarkerProcessor processor = new SmartMarkerProcessor(workbook);
```

Процессор лёгок; при желании его можно переиспользовать для нескольких JSON‑payload.

---

## Шаг 4: Передача JSON‑данных – Заполнение Excel из JSON

Здесь происходит волшебство. Мы передаём строку JSON, содержащую массив клиентов. Каждый клиент может иметь поля `Name`, `Email` и `Total`.

```csharp
// Sample JSON data – in a real scenario you might read this from a file or API
string customersJson = @"
{
  ""Customers"": [
    { ""Name"": ""Acme Corp"", ""Email"": ""contact@acme.com"", ""Total"": 12500 },
    { ""Name"": ""Globex"", ""Email"": ""sales@globex.com"", ""Total"": 9800 },
    { ""Name"": ""Initech"", ""Email"": ""info@initech.com"", ""Total"": 15400 }
  ]
}";

// Apply the JSON to the processor – this populates the workbook
processor.ApplyJson(customersJson);
```

> **Почему JSON?** JSON независим от языка и легко генерируется из API, баз данных или даже вручную. Использование `ApplyJson` избавляет от необходимости вручную сопоставлять объекты; процессор берёт на себя тяжёлую работу.

---

## Шаг 5: Сохранение результата – Генерация отчёта Excel из JSON

Наконец, мы сохраняем заполненную книгу на диск. Выходной файл теперь содержит отдельный лист для каждого клиента, каждый из которых заполнен данными из нашего JSON.

```csharp
// Save the filled workbook – choose a path that makes sense for your app
workbook.Save(@"C:\Reports\output.xlsx");
```

### Ожидаемый результат

- **output.xlsx** будет содержать три листа с именами `Sheet1`, `Sheet2`, `Sheet3` (или любые имена, заданные в вашем шаблоне).
- На каждом листе будут отображаться значения `Name`, `Email` и `Total` для одного клиента.
- Макет, который вы разработали в `template.xlsx` (заголовки, стили, формулы), сохраняется на всех сгенерированных листах.

---

## Полный рабочий пример

Ниже представлен полностью готовый к запуску код. Скопируйте‑вставьте его в консольное приложение, скорректируйте пути к файлам и нажмите **F5**.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

namespace DynamicExcelDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the template workbook
            string templatePath = @"C:\Reports\template.xlsx";
            Workbook workbook = new Workbook(templatePath);
            Worksheet worksheet = workbook.Worksheets[0];

            // 2️⃣ Insert the Smart Marker that repeats the worksheet per customer
            worksheet.Cells[0, 0].PutValue("${Customers.RepeatWorksheet}");

            // 3️⃣ Create the SmartMarkerProcessor
            SmartMarkerProcessor processor = new SmartMarkerProcessor(workbook);

            // 4️⃣ JSON data containing a collection of customers
            string customersJson = @"
            {
                ""Customers"": [
                    { ""Name"": ""Acme Corp"", ""Email"": ""contact@acme.com"", ""Total"": 12500 },
                    { ""Name"": ""Globex"", ""Email"": ""sales@globex.com"", ""Total"": 9800 },
                    { ""Name"": ""Initech"", ""Email"": ""info@initech.com"", ""Total"": 15400 }
                ]
            }";

            // Apply the JSON – this populates the workbook dynamically
            processor.ApplyJson(customersJson);

            // 5️⃣ Save the generated report
            string outputPath = @"C:\Reports\output.xlsx";
            workbook.Save(outputPath);

            Console.WriteLine($"✅ Dynamic Excel report generated at: {outputPath}");
        }
    }
}
```

Запустите программу, откройте `output.xlsx`, и вы увидите **создание динамической таблицы Excel** в действии — каждый клиент получает свой лист, полностью отформатированный согласно вашему шаблону.

---

## Часто задаваемые вопросы и особые случаи

| Question | Answer |
|----------|--------|
| *What if my JSON has nested objects?* | Smart Markers support dot notation (`${Customers.Address.City}`) as long as the JSON hierarchy matches. |
| *Can I name the generated worksheets after the customer?* | Yes—add a marker like `${Customers.Name}` in the worksheet name cell or use `processor.ApplyJson(customersJson, "Customers")` with a naming pattern. |
| *What about large data sets (10 k+ rows)?* | The processor streams data efficiently, but keep an eye on memory. Consider splitting the report into multiple files if you hit performance limits. |
| *Do I need a license for Aspose.Cells?* | A free evaluation works for testing, but a licensed version removes evaluation watermarks and grants full features. |
| *Can I use this approach with .NET Core?* | Absolutely—Aspose.Cells supports .NET 6/7/8. Just reference the NuGet package and the code stays the same. |

---

## Советы для готовых к продакшену реализаций

- **Validate JSON** before feeding it to `ApplyJson`. A malformed payload will throw a `JsonParseException`.
- **Cache the template** if you generate many reports in a short time; loading from disk repeatedly is unnecessary I/O.
- **Lock the workbook** during processing if you run this in a multi‑threaded web service to avoid race conditions.
- **Add error handling** around `workbook.Save` to gracefully handle permission issues or locked files.
- **Customize styling** in the template (conditional formatting, formulas) to let the generated sheets retain business logic without extra code.

---

## Заключение

Теперь у вас есть надёжный сквозной шаблон того, как **создать динамическую таблицу Excel** с использованием шаблона, Smart Markers и JSON‑данных. Путём **загрузки шаблона Excel**, вставки маркера повторения и **заполнения Excel из JSON**, вы можете **автоматизировать генерацию отчёта Excel** всего несколькими строками C#.

Что дальше? Попробуйте добавить диаграммы, ссылающиеся на динамические таблицы, или экспортировать тот же JSON в PDF с помощью Aspose.Words. Вы также можете поэкспериментировать с **генерацией отчёта Excel из JSON** из запроса к базе данных, чтобы замкнуть цикл.

## Связанные руководства

- [Создание сводной таблицы в Excel с помощью Aspose.Cells for .NET](/cells/english/net/pivot-tables/create-pivot-table/)
- [Создание динамических линейных диаграмм в Excel с помощью Aspose.Cells for .NET: пошаговое руководство](/cells/english/net/charts-graphs/create-line-charts-excel-aspose-cells-dotnet/)
- [Как создать флажки в Excel с использованием Aspose.Cells for .NET | Руководство по проверке данных](/cells/english/net/data-validation/create-checkboxes-net-excel-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}