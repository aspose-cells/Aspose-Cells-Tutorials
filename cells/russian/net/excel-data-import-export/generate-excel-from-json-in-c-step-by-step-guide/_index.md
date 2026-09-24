---
category: general
date: 2026-03-18
description: Узнайте, как генерировать Excel из JSON с помощью C#, разрешать дублирование
  имён листов, создавать лист деталей и сохранять рабочую книгу C# за считанные минуты.
draft: false
keywords:
- generate excel from json
- allow duplicate sheet names
- how to create detail sheet
- save workbook c#
- smartmarker options
- aspnet cells integration
language: ru
og_description: Создание Excel из JSON с помощью C#. В этом руководстве показано,
  как разрешить дублирование имён листов, создать лист деталей и сохранить книгу в
  C# с помощью Aspose.Cells.
og_title: Генерация Excel из JSON в C# – Полный учебник
tags:
- C#
- Excel automation
- JSON
- Aspose.Cells
title: Создание Excel из JSON в C# – пошаговое руководство
url: /ru/net/excel-data-import-export/generate-excel-from-json-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Генерация Excel из JSON в C# – Пошаговое руководство

Когда‑нибудь вам нужно было **генерировать Excel из JSON**, но вы не знали, какая библиотека справится с этой задачей? Вы не одиноки. Во многих корпоративных приложениях мы получаем данные в виде JSON и должны перенести их в красиво оформленные электронные таблицы — подумайте о отчётах по продажам, выгрузках инвентаря или журналах аудита. Хорошая новость? С помощью движка SmartMarker от Aspose.Cells вы можете превратить строку JSON в полноценный файл Excel всего в несколько строк кода.

В этом руководстве мы пройдём весь процесс: от подготовки JSON‑получателя, настройки SmartMarker для **разрешения дублирования имён листов**, создания **детального листа**, и, наконец, **сохранения рабочей книги в стиле C#**. К концу вы получите переиспользуемый фрагмент кода, который можно вставить в любой проект .NET.

> **Краткое резюме:**  
> • Основная цель — генерировать Excel из JSON.  
> • Второстепенные цели — разрешить дублирование имён листов, создать детальный лист, сохранить рабочую книгу C#.  

## Prerequisites

Перед тем как начать, убедитесь, что у вас есть:

- .NET 6.0 SDK (или любая более новая версия .NET).  
- Visual Studio 2022 или VS Code с расширением C#.  
- Действующая лицензия или бесплатная пробная версия **Aspose.Cells for .NET** (NuGet‑пакет `Aspose.Cells`).  
- Шаблон Excel‑файла (`template.xlsx`), который уже содержит теги SmartMarker, такие как `&=Name`, и заполнитель таблицы деталей.

Если что‑то из этого вам незнакомо, не паникуйте — установка NuGet‑пакета выполняется одной командой, а шаблон может быть обычной книгой с несколькими ячейками‑заполнителями.

## Overview of the Solution

На высоком уровне мы будем:

1. Определять строку JSON, отражающую данные, которые нужны в листе.  
2. Настраивать `SmartMarkerOptions`, чтобы разрешить дублирование имён листов и задать предсказуемое имя **детального листа**.  
3. Загружать шаблон Excel, содержащий теги SmartMarker.  
4. Запускать процессор SmartMarker для слияния JSON‑данных с рабочей книгой.  
5. Сохранять итоговый файл с помощью `workbook.Save(...)`.

Каждый шаг подробно объяснён ниже, с полными фрагментами кода и объяснением, почему он важен.

---

## Step 1 – Prepare the JSON payload you’ll merge

Первое, что вам понадобится — документ JSON, соответствующий тегам SmartMarker в вашем шаблоне. Считайте JSON источником правды; каждый ключ становится заполнительным полем в файле Excel.

```csharp
// Step 1: Define the JSON data that will be merged into the worksheet
string jsonData = @"{
    ""Name"": ""John"",
    ""Date"": ""2023-01-01"",
    ""Orders"": [
        { ""Item"": ""Laptop"", ""Qty"": 2, ""Price"": 1200 },
        { ""Item"": ""Mouse"",  ""Qty"": 5, ""Price"": 25 }
    ]
}";
```

**Почему это важно:**  
SmartMarker читает иерархию JSON и автоматически расширяет таблицы для коллекций, таких как `Orders`. Если структура вашего JSON не совпадает с тегами, слияние тихо создаст пустые строки — частая ловушка.

## Step 2 – Configure SmartMarker to allow duplicate sheet names and name the detail sheet

По умолчанию Aspose.Cells запрещает дублирование имён листов, что может стать препятствием, когда вы генерируете детальный лист для каждой записи‑мастера. Класс `SmartMarkerOptions` позволяет ослабить это правило и также задать шаблон имени для вновь создаваемых детальных листов.

```csharp
// Step 2: Create SmartMarker options and allow duplicate base names for detail sheets
var smartMarkerOptions = new Aspose.Cells.SmartMarker.SmartMarkerOptions
{
    // When a detail sheet is generated, it will be named "Detail", "Detail (2)", etc.
    DetailSheetNewName = "Detail",

    // This flag tells the engine that duplicate sheet names are acceptable.
    // Useful when you generate multiple detail sheets from a loop.
    AllowDuplicateSheetNames = true
};
```

**Почему это важно:**  
Если вы перебираете несколько клиентов и каждый проход создаёт новый лист, движок обычно бросит исключение. Установка `AllowDuplicateSheetNames` в `true` заставит Aspose.Cells автоматически добавлять числовой суффикс, обеспечивая плавный процесс.

## Step 3 – Load the Excel template that holds SmartMarker tags

Ваш шаблон — это полотно, на котором SmartMarker «рисует» данные. Он может содержать любое форматирование — цвета, формулы, диаграммы — так что вам не придётся воссоздавать эту логику программно.

```csharp
// Step 3: Load the workbook that contains SmartMarker tags
using var workbook = new Aspose.Cells.Workbook(@"C:\MyProjects\ExcelDemo\template.xlsx");
```

**Подсказка:**  
Храните шаблон в папке, входящей в вывод вашего проекта (например, `Content\Templates`). Так вы сможете ссылаться на него относительным путём и избежать жёстко заданных абсолютных каталогов.

## Step 4 – Run the SmartMarker processor with the JSON and options

Теперь происходит магия. `SmartMarkerProcessor` читает JSON, учитывает заданные параметры и заполняет рабочую книгу соответствующим образом.

```csharp
// Step 4: Process the SmartMarker tags using the JSON data and the configured options
workbook.SmartMarkerProcessor.Process(jsonData, smartMarkerOptions);
```

**Что происходит «под капотом»?**  
- Процессор сканирует каждую ячейку в поисках маркеров вроде `&=Name` или `&=Orders.Item`.  
- Он заменяет простые маркеры скалярными значениями (`Name`, `Date`).  
- Для коллекций (`Orders`) он создаёт новый детальный лист (именуемый «Detail») и заполняет строку таблицы для каждого элемента.  
- Поскольку мы разрешили дублирование имён листов, если в шаблоне уже существует лист под названием «Detail», движок создаст «Detail (2)».

## Step 5 – Save the merged workbook back to disk

Наконец, запишите заполненную рабочую книгу в файл. Вы можете выбрать любой формат, поддерживаемый Aspose.Cells — XLSX, CSV, PDF и т.д. Здесь мы останемся с современным XLSX.

```csharp
// Step 5: Save the workbook with the merged data
workbook.Save(@"C:\MyProjects\ExcelDemo\output.xlsx");
```

**Почему это важно:**  
Сохранение — это тот момент, когда вы действительно **save workbook C#**. Если нужно передать файл клиенту через веб, можно использовать `workbook.Save(Stream, SaveFormat.Xlsx)`.

## Full Working Example

Объединив всё вместе, получаем полностью готовое консольное приложение. Убедитесь, что вы установили NuGet‑пакет `Aspose.Cells` (`dotnet add package Aspose.Cells`) перед компиляцией.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.SmartMarker;

namespace ExcelFromJsonDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Define the JSON payload
            string jsonData = @"{
                ""Name"": ""John"",
                ""Date"": ""2023-01-01"",
                ""Orders"": [
                    { ""Item"": ""Laptop"", ""Qty"": 2, ""Price"": 1200 },
                    { ""Item"": ""Mouse"",  ""Qty"": 5, ""Price"": 25 }
                ]
            }";

            // 2️⃣ Configure SmartMarker options – allow duplicate sheet names & set detail sheet name
            var smartMarkerOptions = new SmartMarkerOptions
            {
                DetailSheetNewName = "Detail",
                AllowDuplicateSheetNames = true
            };

            // 3️⃣ Load the template workbook (ensure the path is correct)
            var workbookPath = @"C:\MyProjects\ExcelDemo\template.xlsx";
            using var workbook = new Workbook(workbookPath);

            // 4️⃣ Merge JSON data into the workbook
            workbook.SmartMarkerProcessor.Process(jsonData, smartMarkerOptions);

            // 5️⃣ Save the result
            var outputPath = @"C:\MyProjects\ExcelDemo\output.xlsx";
            workbook.Save(outputPath);

            Console.WriteLine($"✅ Excel file generated successfully at: {outputPath}");
        }
    }
}
```

### Expected Result

- **Sheet 1** (главный лист) отобразит «John» в ячейке `Name` и «2023‑01‑01» в ячейке `Date`.  
- Появится новый лист **Detail**, содержащий таблицу с двумя строками: одна для заказа Laptop, другая для заказа Mouse.  
- Если в шаблоне уже был лист с именем «Detail», новый лист будет назван «Detail (2)», благодаря флагу `AllowDuplicateSheetNames`.

![Excel output showing master sheet with name and date, plus a Detail sheet with order rows](excel-output.png "результат генерации excel из json")

*Image alt text:* **генерация excel из json – пример рабочей книги с главным и детальными листами**

## Common Questions & Edge Cases

### What if my JSON contains nested collections?

SmartMarker умеет работать с вложенными массивами, но вам понадобится добавить дополнительные детальные листы или использовать иерархические маркеры. Например, `&=Orders.SubItems.Product` автоматически создаст лист третьего уровня.

### How do I customize the naming pattern for duplicate sheets?

Вместо статического `DetailSheetNewName` вы можете назначить обратный вызов через `smartMarkerOptions.DetailSheetNameGenerator`. Это позволит включать в имя листа метки времени или уникальные идентификаторы.

```csharp
smartMarkerOptions.DetailSheetNameGenerator = (baseName, index) =>
    $"{baseName}_{DateTime.Now:yyyyMMdd}_{index}";
```

### Can I generate CSV instead of XLSX?

Конечно. Замените финальный вызов `Save` на:

```csharp
workbook.Save(outputPath, SaveFormat.Csv);
```

Остальная часть конвейера остаётся без изменений.

### Does this work in ASP.NET Core?

Да. Тот же код можно выполнить внутри действия контроллера. Просто передайте рабочую книгу в ответ:

```csharp
using var ms = new MemoryStream();
workbook.Save(ms, SaveFormat.Xlsx);
ms.Position = 0;
return File(ms, "application/vnd.openxmlformats-officedocument.spreadsheetml.sheet", "report.xlsx");
```

## Pro Tips & Pitfalls

- **Pro tip:** Храните теги SmartMarker на отдельном листе «Template». Так вы сможете защитить лист от случайных правок, но при этом процессор всё равно сможет их читать.  
- **Watch out for:** Ключи JSON, содержащие пробелы или специальные символы. Aspose.Cells ожидает валидные идентификаторы JavaScript; переименуйте их или используйте атрибут `JsonProperty`, если десериализуете из POCO.  
- **Performance tip:** При обработке тысяч строк установите `smartMarkerOptions.EnableCache = true`, чтобы переиспользовать скомпилированные маркеры.  
- **Version check:** Приведённый код рассчитан на Aspose.Cells 23.9+. Более ранние версии могут не поддерживать `AllowDuplicateSheetNames`.

## Conclusion

Теперь у вас есть полноценный, сквозной рецепт **генерировать Excel из JSON** в C#. Настроив `SmartMarkerOptions`, мы продемонстрировали, как **разрешить дублирование имён листов**, управлять именованием **детального листа** и, наконец, **save workbook C#**. Подход полностью автономный — без внешних сервисов, только один NuGet‑пакет.

Следующий шаг? Попробуйте заменить источник JSON на реальный API

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}