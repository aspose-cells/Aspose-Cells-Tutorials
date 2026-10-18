---
category: general
date: 2026-02-09
description: Как назвать листы в C# с помощью SmartMarker — научитесь создавать несколько
  листов и автоматизировать их именование всего за несколько строк кода.
draft: false
keywords:
- how to name sheets
- generate multiple sheets
- automate sheet naming
- SmartMarker sheet naming
- workbook automation
language: ru
og_description: Как назвать листы в C# с помощью опций SmartMarker. Это руководство
  показывает, как генерировать несколько листов и автоматизировать их именование без
  усилий.
og_title: Как автоматически именовать листы – Краткое руководство по C#
tags:
- C#
- Aspose.Cells
- Excel automation
title: Как автоматически именовать листы – генерировать несколько листов в C#
url: /ru/net/smart-markers-dynamic-data/how-to-name-sheets-automatically-generate-multiple-sheets-in/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как автоматически именовать листы – генерировать несколько листов в C#

Когда‑то задумывались **как именовать листы** в книге Excel без ручного клика «Переименовать» каждый раз? Вы не одиноки. Во многих сценариях отчётности у вас оказывается десятки листов‑деталей, которым нужны систематические имена, а делать это вручную — кошмар.  

Хорошая новость: с несколькими строками C# вы можете **генерировать несколько листов** и **автоматизировать именование листов**, так что каждый новый лист‑деталь будет следовать предсказуемому шаблону. В этом руководстве мы пройдём полное решение, объясним, почему каждый элемент важен, и предоставим готовый к запуску пример кода.

## Что охватывает это руководство

* Настройка книги, содержащей SmartMarkers.  
* Конфигурация `SmartMarkerOptions` для управления базовым именем генерируемых листов.  
* Запуск `ProcessSmartMarkers`, чтобы библиотека автоматически создавала `Detail`, `Detail_1`, `Detail_2`, …  
* Советы по обработке крайних случаев, таких как существующие имена листов или пользовательские правила именования.  
* Полный, исполняемый пример, который можно вставить в Visual Studio и сразу увидеть результат.

Предварительный опыт работы с Aspose.Cells не требуется — достаточно базовой настройки C# и любой IDE.

## Требования

| Требование | Почему это важно |
|------------|------------------|
| .NET 6.0 или новее | Современные возможности языка и совместимость библиотеки |
| Aspose.Cells for .NET (пакет NuGet) | Предоставляет обработку `SmartMarker` и создание листов |
| Пустой консольный проект (или любое .NET‑приложение) | Дает место для выполнения кода |

Установите библиотеку с помощью:

```bash
dotnet add package Aspose.Cells
```

Теперь, когда основы покрыты, перейдём к реализации.

## Шаг 1: Создать книгу с SmartMarkers

Сначала нам нужна книга, содержащая заполнитель SmartMarker. Представьте SmartMarker как тег‑шаблон, который указывает движку, куда вставлять данные и, в нашем случае, когда создавать новый лист.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣  Create a new workbook and get the first worksheet
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];
        ws.Name = "Template";

        // 2️⃣  Insert a SmartMarker that will trigger sheet creation
        // The marker {{detail}} tells Aspose.Cells to repeat the row for each item in the "detail" collection.
        ws.Cells["A1"].PutValue("{{detail}}");
        ws.Cells["B1"].PutValue("Item Name");
        ws.Cells["C1"].PutValue("Quantity");
        ws.Cells["A2"].PutValue("&=detail.Name");
        ws.Cells["B2"].PutValue("&=detail.Quantity");

        // 3️⃣  Prepare sample data for the SmartMarker
        var data = new
        {
            detail = new[]
            {
                new { Name = "Apple",  Quantity = 10 },
                new { Name = "Banana", Quantity = 20 },
                new { Name = "Cherry", Quantity = 30 }
            }
        };
```

> **Совет:** Держите лист‑шаблон лёгким. Только строки, требующие дублирования, должны содержать SmartMarkers; всё остальное остаётся статичным.

## Шаг 2: Настроить параметры SmartMarker – ядро именования листов

Теперь начинается магия. Устанавливая `DetailSheetNewName`, мы говорим движку, какое базовое имя использовать для каждого генерируемого листа. Библиотека добавит «_1», «_2» и т.д., если базовое имя уже существует.

```csharp
        // 4️⃣  Define naming options – this is where we answer “how to name sheets”
        SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions
        {
            // Primary keyword appears here: how to name sheets
            DetailSheetNewName = "Detail"   // Base name for all generated sheets
        };
```

Если понадобится другая конвенция (например, «Report_2023»), просто измените строку. Движок автоматически обрабатывает конфликты, поэтому такой подход **автоматизирует именование листов** без дополнительного кода.

## Шаг 3: Обработать SmartMarkers и сгенерировать листы

Имея готовую книгу, данные и параметры, один вызов метода делает всю тяжёлую работу.

```csharp
        // 5️⃣  Run the SmartMarker processor – this will create Detail, Detail_1, Detail_2…
        wb.ProcessSmartMarkers(data, smartMarkerOptions);

        // 6️⃣  Save the result so you can open it in Excel
        wb.Save("GeneratedSheets.xlsx");

        // 7️⃣  Let the user know we’re done
        System.Console.WriteLine("Workbook created – check GeneratedSheets.xlsx");
    }
}
```

### Ожидаемый результат

При открытии *GeneratedSheets.xlsx* вы увидите:

| Имя листа | Содержание |
|-----------|------------|
| Template  | Исходный макет маркера (оставлен для справки) |
| Detail    | Первый набор строк (Apple, Banana, Cherry) |
| Detail_1  | Вторая копия — идентичные данные (полезно при нескольких коллекциях) |
| Detail_2  | …и так далее, в зависимости от количества различных групп SmartMarker |

Шаблон имен (`Detail`, `Detail_1`, `Detail_2`) демонстрирует **как программно именовать листы**, одновременно **генерируя несколько листов** по необходимости.

## Пограничные случаи и варианты

### 1. Существующие имена листов

Если в вашей книге уже есть лист с именем «Detail», движок начнёт с «Detail_1». Это предотвращает случайные перезаписи.

### 2. Пользовательские форматы инкремента

Хотите вместо числовых суффиксов «Detail‑A», «Detail‑B»? Можно пост‑обработать имена после `ProcessSmartMarkers`:

```csharp
for (int i = 0; i < wb.Worksheets.Count; i++)
{
    Worksheet sh = wb.Worksheets[i];
    if (sh.Name.StartsWith("Detail_"))
    {
        string suffix = ((char)('A' + i - 1)).ToString(); // A, B, C…
        sh.Name = $"Detail-{suffix}";
    }
}
```

### 3. Несколько групп SmartMarker

Если в книге более одной группы SmartMarker (например, `{{invoice}}` и `{{detail}}`), каждая группа создаст собственный набор листов на основе того же `DetailSheetNewName`. Чтобы дать каждой группе отдельный префикс, создайте отдельные экземпляры `SmartMarkerOptions` и вызовите `ProcessSmartMarkers` для каждой коллекции.

## Практические советы из практики

* **Совет:** Отключите `AllowDuplicateNames` в `WorkbookSettings`, если хотите, чтобы библиотека бросала исключение вместо тихого переименования листов. Это помогает быстро обнаружить ошибки в логике именования.  
* **Осторожно с:** Очень длинными базовыми именами. Excel ограничивает имена листов 31 символом; библиотека автоматически обрезает, но могут получиться неоднозначные имена.  
* **Примечание о производительности:** Генерация сотен листов может потреблять память. Освобождайте книгу (`wb.Dispose()`) сразу после завершения, если работаете в длительно живом сервисе.

## Визуальный обзор

![диаграмма как назвать листы](image.png "Диаграмма, показывающая поток от шаблона SmartMarker к сгенерированным листам – как назвать листы")

*Alt text включает основной ключевой запрос для SEO.*

## Полный исходный код (готовый к копированию)

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create workbook and template sheet
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];
        ws.Name = "Template";

        // SmartMarker layout
        ws.Cells["A1"].PutValue("{{detail}}");
        ws.Cells["B1"].PutValue("Item Name");
        ws.Cells["C1"].PutValue("Quantity");
        ws.Cells["A2"].PutValue("&=detail.Name");
        ws.Cells["B2"].PutValue("&=detail.Quantity");

        // Sample data
        var data = new
        {
            detail = new[]
            {
                new { Name = "Apple",  Quantity = 10 },
                new { Name = "Banana", Quantity = 20 },
                new { Name = "Cherry", Quantity = 30 }
            }
        };

        // Configure naming – this answers how to name sheets
        SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions
        {
            DetailSheetNewName = "Detail"
        };

        // Process markers → generates Detail, Detail_1, Detail_2 …
        wb.ProcessSmartMarkers(data, smartMarkerOptions);

        // Save and finish
        wb.Save("GeneratedSheets.xlsx");
        System.Console.WriteLine("Workbook created – open GeneratedSheets.xlsx to see the result.");
    }
}
```

Запустите программу, откройте сгенерированный файл, и вы увидите листы, автоматически именованные согласно заданному шаблону.

## Заключение

Теперь вы знаете **как именовать листы** в книге C#, как **генерировать несколько листов** с помощью SmartMarker и как **автоматизировать именование листов**, чтобы больше никогда не приходилось переименовывать их вручную. Подход масштабируется от нескольких страниц‑деталей до сотен, и тот же шаблон работает для любой коллекции, передаваемой в `ProcessSmartMarkers`.

Что дальше? Попробуйте заменить источник данных запросом к базе, поэкспериментировать с пользовательскими форматами суффиксов или связать несколько групп SmartMarker для полноценного движка отчётности. Возможности безграничны, когда библиотека берёт на себя рутинную работу по именованию.

Если этот гид оказался полезным, поставьте звёздочку на GitHub, поделитесь им с коллегами или оставьте комментарий ниже со своими приёмами именования. Счастливого кодинга!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}