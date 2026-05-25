---
category: general
date: 2026-02-14
description: Создайте объект мастер‑данных в C# и без труда генерируйте лист деталей.
  Изучите полный процесс SmartMarker с практическими примерами кода.
draft: false
keywords:
- create master data object
- generate detail sheet
- smartmarker processing
- worksheet automation
- c# data binding
language: ru
og_description: Создайте объект мастер‑данных в C# и сгенерируйте лист деталей с помощью
  SmartMarker. Следуйте нашему подробному руководству для готового к запуску решения.
og_title: Создание объекта мастер‑данных — Полное руководство
tags:
- C#
- SmartMarker
- Excel Automation
title: Создание объекта мастер‑данных — пошаговое руководство по созданию листа деталей
url: /ru/net/smart-markers-dynamic-data/create-master-data-object-step-by-step-guide-to-generate-det/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание объекта главных данных – Полный учебник

Когда‑нибудь вам нужно было **create master data object** для листа Excel, но вы не знали, как привязать его к листу деталей SmartMarker? Вы не одиноки. Во многих сценариях отчётности главный объект управляет динамическим листом деталей, и правильная настройка может ощущаться как сборка пазла без картинки.  

В этом руководстве мы пройдем весь процесс — построим объект главных данных, настроим параметры SmartMarker для **generate detail sheet**, и наконец запустим процессор. К концу у вас будет исполняемый фрагмент кода, который можно вставить в любой проект .NET, использующий библиотеку GrapeCity Documents for Excel (GcExcel) library.

## Что понадобится

- .NET 6+ (или .NET Framework 4.7.2) с ссылкой на `GcExcel.dll`
- Базовые знания C# (переменные, анонимные типы, инициализаторы объектов)
- Excel‑книга, уже содержащая теги SmartMarker, такие как `{{OrderId}}`, и таблицу для строк товаров
- Visual Studio, Rider или любой предпочитаемый редактор

Это всё — никаких дополнительных пакетов NuGet, кроме основной поставки GcExcel distribution.

## Шаг 1: Создание объекта главных данных

Первое, что нужно сделать, — **create master data object**, который отражает структуру, ожидаемую тегами SmartMarker. Считайте его небольшим моделью отчёта в памяти.

```csharp
// Step 1: Build the master data object that feeds the SmartMarkers.
// It contains an OrderId and a collection of line items.
var orderData = new
{
    OrderId = 1,
    Items = new[]
    {
        new { Product = "A", Quantity = 2 },
        new { Product = "B", Quantity = 5 }
    }
};
```

Зачем здесь использовать анонимный тип? Потому что он позволяет определить лёгкий контейнер без объявления полноценного класса — идеально для быстрых демонстраций или когда структура вряд ли изменится. Если позже понадобится переиспользуемая модель, просто замените `var` на правильный POCO.

> **Pro tip:** Сохраняйте имена свойств (`OrderId`, `Product`, `Quantity`) точно такими же, как заполнители в вашем листе; SmartMarker сопоставляет их без учёта регистра.

## Шаг 2: Настройка параметров SmartMarker для генерации листа деталей

Теперь мы указываем SmartMarker, что хотим отдельный лист для таблицы строк. Здесь в действие вступает ключевое слово **generate detail sheet**.

```csharp
// Step 2: Set up SmartMarker options.
// Enabling DetailSheet creates a new sheet for each master record.
var smartMarkerOptions = new SmartMarkerOptions
{
    DetailSheet = true,
    // The new sheet will be named using the OrderId value.
    DetailSheetNewName = "Order_{OrderId}"
};
```

Шаблон `DetailSheetNewName` использует заполнители в фигурных скобках, которые заменяются во время выполнения. В нашем примере лист будет назван `Order_1`. Если позже вы будете проходить несколько заказов, каждый получит свою вкладку — именно то, что ожидают большинство бухгалтеров.

## Шаг 3: Запуск процессора SmartMarker

Когда данные и параметры готовы, последний шаг — вызвать процессор для целевого листа.

```csharp
// Step 3: Execute SmartMarker processing on the worksheet.
// 'worksheet' is an IWorksheet instance that points to the template sheet.
worksheet.SmartMarkerProcessor.StartSmartMarkerProcessing(orderData, smartMarkerOptions);
```

Внутри SmartMarker сканирует лист в поисках тегов, внедряет значения `orderData`, и поскольку `DetailSheet` равно `true`, он клонирует шаблон в новый лист с именем `Order_1`. Все строки появляются в области деталей, сохраняя любое форматирование, применённое в шаблоне.

### Полный рабочий пример

Ниже приведена автономная консольная программа, которая открывает шаблонную книгу (`Template.xlsx`), выполняет три шага и сохраняет результат как `Result.xlsx`. Вы можете скопировать‑вставить её в новый консольный проект и нажать **F5**.

```csharp
using System;
using GrapeCity.Documents.Excel;

class Program
{
    static void Main()
    {
        // Load the Excel template that contains SmartMarker tags.
        var workbook = new Workbook();
        workbook.Open("Template.xlsx");

        // -------------------------------------------------
        // Step 1: Create the master data object.
        // -------------------------------------------------
        var orderData = new
        {
            OrderId = 1,
            Items = new[]
            {
                new { Product = "A", Quantity = 2 },
                new { Product = "B", Quantity = 5 }
            }
        };

        // -------------------------------------------------
        // Step 2: Configure SmartMarker options to generate detail sheet.
        // -------------------------------------------------
        var smartMarkerOptions = new SmartMarkerOptions
        {
            DetailSheet = true,
            DetailSheetNewName = "Order_{OrderId}"
        };

        // -------------------------------------------------
        // Step 3: Process the worksheet.
        // -------------------------------------------------
        // Assume the first sheet holds the master template.
        var worksheet = workbook.Worksheets[0];
        worksheet.SmartMarkerProcessor.StartSmartMarkerProcessing(orderData, smartMarkerOptions);

        // Save the populated workbook.
        workbook.Save("Result.xlsx");
        Console.WriteLine("Done! Check Result.xlsx – a new sheet named Order_1 should exist.");
    }
}
```

#### Ожидаемый результат

- **Result.xlsx** содержит лист с именем `Order_1`.
- Ячейка `A1` (или где бы вы ни разместили `{{OrderId}}`) теперь показывает `1`.
- Таблица, начинающаяся с блока SmartMarker, содержит две строки:
  | Product | Quantity |
  |---------|----------|
  | A       | 2        |
  | B       | 5        |

Если открыть файл, вы увидите, что форматирование из шаблона сохранено — границы, шрифты, условное форматирование — всё осталось нетронутым.

## Часто задаваемые вопросы и особые случаи

### Что делать, если у меня несколько заказов?

Оберните объект главных данных в коллекцию, и SmartMarker будет автоматически итеративно обрабатывать её:

```csharp
var orders = new[]
{
    new {
        OrderId = 1,
        Items = new[] { new { Product = "A", Quantity = 2 } }
    },
    new {
        OrderId = 2,
        Items = new[] { new { Product = "C", Quantity = 3 } }
    }
};

worksheet.SmartMarkerProcessor.StartSmartMarkerProcessing(orders, smartMarkerOptions);
```

Каждый заказ создаёт собственный лист (`Order_1`, `Order_2`, …). Процессор рассматривает внешний массив как главную коллекцию.

### Как управлять позицией листа?

Установите `smartMarkerOptions.DetailSheetInsertIndex = 2;`, чтобы разместить новый лист после второй вкладки, или используйте `DetailSheetInsertAfter = "Summary"`, чтобы вставить после листа с именем.

### Можно ли отключить лист деталей для конкретного запуска?

Просто переключите `DetailSheet = false;`. Тогда SmartMarker запишет строки в тот же лист, где находятся главные теги.

### Что делать с большими наборами данных?

SmartMarker эффективно потоково передаёт данные, но если превысить несколько сотен тысяч строк, вы можете столкнуться с ограничением Excel в 1 048 576 строк. В этом случае разбейте данные на несколько главных записей или рассмотрите экспорт в CSV.

## Визуальный обзор

![Diagram illustrating how to create master data object and generate detail sheet using SmartMarker](/images/smartmarker-flow.png)

*Иллюстрация показывает поток от C# master object → SmartMarker options → обработка листа → новый лист деталей.*

## Заключение

Теперь вы знаете, как **create master data object** в C# и настроить SmartMarker для автоматического **generate detail sheet**. Трёхшаговый шаблон — данные, параметры, процессор — покрывает большинство сценариев автоматизации Excel с GcExcel.  

Отсюда вы можете исследовать:

- Добавление данных заголовка/подвала на каждый лист деталей
- Использование условного форматирования в зависимости от статуса заказа
- Экспорт сгенерированной книги в PDF с помощью `workbook.SaveAsPdf(...)`

Не стесняйтесь экспериментировать, ломать вещи, а затем собирать их обратно. Это самый быстрый путь к освоению автоматизации листов. Счастливого кодинга!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}