---
category: general
date: 2026-11-16
description: Создайте Excel из JSON с помощью SmartMarker. Узнайте, как преобразовать
  JSON в Excel, встроить JSON в Excel и сохранить рабочую книгу xlsx за несколько
  минут.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel from json
- convert json to excel
- embed json in excel
- save workbook xlsx
language: ru
lastmod: 2026-11-16
og_description: Быстро создавайте Excel из JSON. Этот учебник показывает, как преобразовать
  JSON в Excel, внедрить JSON в Excel и сохранить книгу в формате xlsx с помощью Aspose.Cells.
og_image_alt: Screenshot of an Excel worksheet showing JSON data inserted into a single
  cell
og_title: Создайте Excel из JSON с помощью SmartMarker — пошаговое руководство по
  C#
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Create Excel from JSON using SmartMarker. Learn how to convert JSON
    to Excel, embed JSON in Excel, and save workbook xlsx in minutes.
  headline: Create Excel from JSON with SmartMarker in C#
  type: TechArticle
- description: Create Excel from JSON using SmartMarker. Learn how to convert JSON
    to Excel, embed JSON in Excel, and save workbook xlsx in minutes.
  name: Create Excel from JSON with SmartMarker in C#
  steps:
  - name: Build and run the console app (`dotnet run`).
    text: Build and run the console app (`dotnet run`).
  - name: Verify the console prints the full path to the generated file.
    text: Verify the console prints the full path to the generated file.
  - name: Open the file in Excel or any spreadsheet viewer.
    text: Open the file in Excel or any spreadsheet viewer.
  - name: Confirm that cell A1 holds the JSON array string exactly as shown above.
    text: Confirm that cell A1 holds the JSON array string exactly as shown above.
  type: HowTo
tags:
- SmartMarker
- Aspose.Cells
- C#
- JSON
title: Создать Excel из JSON с помощью SmartMarker в C#
url: /ru/net/smart-markers-dynamic-data/create-excel-from-json-with-smartmarker-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создать Excel из JSON с помощью SmartMarker в C#

Если вам нужно **создать Excel из JSON** в проекте .NET, это руководство показывает полное, готовое к запуску решение. С помощью процессора Smart Marker из Aspose.Cells вы можете **конвертировать JSON в Excel**, вставить строку JSON напрямую в ячейку и **сохранить книгу xlsx** без написания какого‑либо ручного кода парсинга.

Вы увидите, как зарегистрировать источник данных JSON, вставить Smart Marker, который выводит весь массив как одну строку JSON, обработать лист и, наконец, записать файл на диск. К концу руководства вы сможете сгенерировать файл Excel, содержащий исходный JSON‑payload в ячейке A1, готовый для дальнейшей обработки или отчетности.

## Требования

- .NET 6.0 или новее (код также работает с .NET Framework 4.7+)
- Aspose.Cells for .NET (пакет NuGet `Aspose.Cells`)
- Базовые знания C# и формата JSON
- IDE, например Visual Studio или VS Code

## Шаг 1: Настройка проекта и импорт пространств имён

Создайте новое консольное приложение и добавьте пакет Aspose.Cells:

```bash
dotnet new console -n JsonToExcelDemo
cd JsonToExcelDemo
dotnet add package Aspose.Cells
```

Затем включите необходимые пространства имён в начале файла `Program.cs`:

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;
```

**Почему?**  
`Aspose.Cells` предоставляет модель рабочей книги, а `Aspose.Cells.SmartMarkers` содержит класс `SmartMarkerProcessor`, который интерпретирует маркеры `&=` на листе.

## Шаг 2: Определение источника данных JSON

Поместите строку JSON в переменную. В этом примере у нас есть массив заказов:

```csharp
// Step 2: Define the JSON data source
string json = @"{
    ""Orders"": [
        { ""Id"": 1, ""Amount"": 100 },
        { ""Id"": 2, ""Amount"": 150 }
    ]
}";
```

**Почему?**  
Smart Marker работает с любым корректным JSON. Хранение JSON в строке позволяет зарегистрировать его напрямую без необходимости файла на диске.

## Шаг 3: Регистрация данных JSON в SmartMarkerProcessor

Создайте экземпляр `SmartMarkerProcessor` и свяжите строку JSON с именем, которое вы будете использовать позже на листе:

```csharp
// Step 3: Register the JSON data with the Smart Marker processor
SmartMarkerProcessor processor = new SmartMarkerProcessor();
processor.RegisterJsonDataSource("OrdersJson", json);
```

**Почему?**  
`RegisterJsonDataSource` разбирает JSON и делает его иерархию доступной для Smart Markers. Имя `"OrdersJson"` становится корневым объектом в выражениях маркеров.

## Шаг 4: Создание рабочей книги и вставка Smart Marker

Создайте новую рабочую книгу, получите её первый лист и запишите Smart Marker в ячейку A1, который выведет весь массив `Orders` как одну строку JSON:

```csharp
// Step 4: Create a workbook and get the first worksheet
Worksheet ws = new Workbook().Worksheets[0];

// Insert a Smart Marker that outputs the whole array as a single JSON string
ws.Cells["A1"].PutValue("&=OrdersJson.Orders.ArrayAsSingle");
```

**Почему?**  
Выражение `OrdersJson.Orders.ArrayAsSingle` указывает Smart Marker взять массив `Orders` и сериализовать его обратно в JSON, поместив результат в целевую ячейку. Это самый простой способ **вставить JSON в Excel**.

## Шаг 5: Обработка листа

Запустите процессор, чтобы он заменил маркер реальной строкой JSON:

```csharp
// Step 5: Process the worksheet – the marker is replaced with the JSON array string
processor.Process(ws);
```

**Почему?**  
Обработка проверяет каждую ячейку на наличие маркеров `&=`, оценивает их относительно зарегистрированных источников данных и записывает полученное значение обратно в лист.

## Шаг 6: Сохранение рабочей книги в файл .xlsx

Наконец, запишите рабочую книгу на диск. Скорректируйте путь к папке, в которую у вас есть права записи:

```csharp
// Step 6: Save the workbook
string outputPath = Path.Combine(
    Environment.CurrentDirectory,
    "JsonArraySingleCell.xlsx");

ws.Workbook.Save(outputPath, SaveFormat.Xlsx);
Console.WriteLine($"Workbook saved to: {outputPath}");
```

**Почему?**  
`SaveFormat.Xlsx` гарантирует, что файл сохраняется в современном формате Office Open XML, удовлетворяя требование **save workbook xlsx**.

## Полный исходный код

Собрав все части вместе, представляем полный, готовый к запуску пример программы:

```csharp
using System;
using System.IO;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

class Program
{
    static void Main()
    {
        // Step 2: Define the JSON data source
        string json = @"{
            ""Orders"": [
                { ""Id"": 1, ""Amount"": 100 },
                { ""Id"": 2, ""Amount"": 150 }
            ]
        }";

        // Step 3: Register the JSON data with the Smart Marker processor
        SmartMarkerProcessor processor = new SmartMarkerProcessor();
        processor.RegisterJsonDataSource("OrdersJson", json);

        // Step 4: Create a workbook and get the first worksheet
        Worksheet ws = new Workbook().Worksheets[0];

        // Insert a Smart Marker that will output the whole array as a single JSON string
        ws.Cells["A1"].PutValue("&=OrdersJson.Orders.ArrayAsSingle");

        // Step 5: Process the worksheet – the marker is replaced with the JSON array string
        processor.Process(ws);

        // Step 6: Save the workbook
        string outputPath = Path.Combine(
            Environment.CurrentDirectory,
            "JsonArraySingleCell.xlsx");
        ws.Workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved to: {outputPath}");
    }
}
```

### Ожидаемый результат в Excel

Откройте `JsonArraySingleCell.xlsx`. Ячейка A1 будет содержать:

```
[{"Id":1,"Amount":100},{"Id":2,"Amount":150}]
```

Строка JSON — это компактное представление исходного массива `Orders`, что упрощает её транспортировку или использование в дальнейших процессах на базе Excel.

## Общие варианты и граничные случаи

| Ситуация | Корректировка |
|-----------|------------|
| **Несколько объектов JSON** | Зарегистрируйте каждый объект под отдельным именем (например, `processor.RegisterJsonDataSource("CustomerJson", customerJson);`) и ссылаться на них отдельными маркерами. |
| **Отформатированный (pretty‑printed) JSON в ячейке** | Используйте опцию `ArrayAsSinglePretty`: `ws.Cells["A1"].PutValue("&=OrdersJson.Orders.ArrayAsSinglePretty");` |
| **Большие JSON‑payload'ы** | Рассмотрите запись JSON на скрытый лист или преобразование в `DataTable` для лучшей производительности. |
| **Вставка JSON в несколько ячеек** | Поместите разные маркеры в другие ячейки, например `&=OrdersJson.Orders[0].Id`, чтобы получить отдельные поля. |

**Подсказка:** При работе с очень большими JSON увеличьте буфер памяти рабочей книги (`WorkbookSettings.MemorySetting`), чтобы избежать `OutOfMemoryException`.

## Тестирование решения

1. Скомпилируйте и запустите консольное приложение (`dotnet run`).  
2. Убедитесь, что консоль выводит полный путь к сгенерированному файлу.  
3. Откройте файл в Excel или любом просмотрщике таблиц.  
4. Проверьте, что ячейка A1 содержит строку JSON‑массива точно как показано выше.

Если в ячейке находится текст маркера (`&=OrdersJson...`) вместо JSON, дважды проверьте, что процессор был вызван **после** размещения маркера и что строка JSON корректна.

## Заключение

Теперь вы знаете, как **создать Excel из JSON** с помощью Aspose.Cells Smart Markers, как **конвертировать JSON в Excel**, вставлять JSON‑payload напрямую в ячейку и **сохранять книгу xlsx** одной строкой кода. Этот подход устраняет ручной парсинг, работает с любой структурой JSON и создает чистый файл Excel, соответствующий стандартам.

### Следующие шаги

- Изучите **циклы Smart Marker** (`&=OrdersJson.Orders`) для генерации строки для каждого заказа вместо одной строки JSON.  
- Скомбинируйте эту технику с **формулами Excel** для расчёта итогов из встроенных данных.  
- Рассмотрите **чтение JSON из Excel** с помощью `Workbook.Load` и обратного использования `SmartMarkerProcessor`.

Не стесняйтесь экспериментировать с различными формами JSON, несколькими листами или экспортом в другие форматы, такие как CSV или PDF. Приятного кодинга!

## Что вам следует изучить дальше?

Следующие руководства охватывают тесно связанные темы, построенные на техниках, продемонстрированных в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, помогающими освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [Создать Excel из JSON с помощью Aspose.Cells Smart Marker](/cells/english/net/smart-markers-dynamic-data/create-excel-from-json-with-aspose-cells-smart-marker/)
- [Создать рабочую книгу Excel из JSON – Полное руководство Aspose.Cells](/cells/english/net/data-loading-and-parsing/create-excel-workbook-from-json-complete-aspose-cells-guide/)
- [Сохранить рабочую книгу Excel из JSON – Полное руководство](/cells/english/net/templates-reporting/save-excel-workbook-from-json-complete-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}