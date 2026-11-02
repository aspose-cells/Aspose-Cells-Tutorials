---
category: general
date: 2026-10-10
description: Конвертировать JSON в XLSX на C# с помощью SmartMarker — узнайте, как
  импортировать JSON в Excel и программно заполнять книгу.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert json to xlsx
- how to import json into excel
- populate excel from json
- create excel workbook c#
- import json into worksheet
language: ru
lastmod: 2026-10-10
og_description: Преобразуйте JSON в XLSX в C# с помощью SmartMarker. Следуйте этому
  руководству, чтобы импортировать JSON в Excel, создать рабочую книгу Excel в C#
  и заполнить её данными из JSON.
og_image_alt: Diagram showing JSON data being converted to an XLSX workbook using
  C#
og_title: Конвертировать JSON в XLSX на C# – пошаговое руководство
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Convert JSON to XLSX in C# with SmartMarker – learn how to import JSON
    into Excel and populate a workbook programmatically.
  headline: Convert JSON to XLSX in C# using SmartMarker
  type: TechArticle
- description: Convert JSON to XLSX in C# with SmartMarker – learn how to import JSON
    into Excel and populate a workbook programmatically.
  name: Convert JSON to XLSX in C# using SmartMarker
  steps:
  - name: '**Create an Excel workbook** in memory.'
    text: '**Create an Excel workbook** in memory.'
  - name: '**Load JSON data** that represents a simple list of people.'
    text: '**Load JSON data** that represents a simple list of people.'
  - name: '**Configure SmartMarker** to treat the JSON array as a single record (`ArrayAsSingle
      = true`).'
    text: '**Configure SmartMarker** to treat the JSON array as a single record (`ArrayAsSingle
      = true`).'
  - name: '**Process the worksheet**, letting SmartMarker replace markers with the
      JSON values.'
    text: '**Process the worksheet**, letting SmartMarker replace markers with the
      JSON values.'
  - name: '**Save the workbook** as an `.xlsx` file.'
    text: '**Save the workbook** as an `.xlsx` file.'
  type: HowTo
tags:
- JSON
- Excel
- C#
- Aspose.Cells
title: Преобразовать JSON в XLSX в C# с использованием SmartMarker
url: /ru/net/smart-markers-dynamic-data/convert-json-to-xlsx-in-c-using-smartmarker/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Преобразование JSON в XLSX в C# с помощью SmartMarker

Если вам нужно **преобразовать JSON в XLSX в C#**, это руководство покажет, как **импортировать JSON в Excel** и **заполнять Excel из JSON** всего несколькими строками кода. Вы увидите, как **создать рабочую книгу Excel C#**, настроить процессор SmartMarker и, наконец, **импортировать JSON в ячейки листа**.

> **Что вы получите** – полностью готовый пример, который читает массив JSON, рассматривает его как одну запись и записывает данные в файл `.xlsx`, готовый к дальнейшему отчётному использованию или анализу.

## Преобразование JSON в XLSX – обзор

SmartMarker является частью библиотеки Aspose.Cells и позволяет привязывать JSON, XML или любой объект .NET напрямую к шаблону Excel. В этом руководстве мы:

1. **Создаём рабочую книгу Excel** в памяти.  
2. **Загружаем данные JSON**, представляющие простой список людей.  
3. **Настраиваем SmartMarker** так, чтобы массив JSON рассматривался как одна запись (`ArrayAsSingle = true`).  
4. **Обрабатываем лист**, позволяя SmartMarker заменять маркеры значениями из JSON.  
5. **Сохраняем рабочую книгу** в файл `.xlsx`.

Весь процесс работает на .NET 6+ и требует только пакета `Aspose.Cells` из NuGet.

## Шаг 1: Создание рабочей книги Excel в C#

Сначала добавьте пакет Aspose.Cells в ваш проект:

```bash
dotnet add package Aspose.Cells
```

Теперь можно создать новый объект `Workbook`. Рабочая книга изначально пустая, но вы можете добавить лист и разместить теги SmartMarker там, где должны появиться данные JSON.

```csharp
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

namespace JsonToXlsxDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create a new workbook (this also creates the default first worksheet)
            Workbook workbook = new Workbook();

            // Optional: give the first sheet a friendly name
            Worksheet sheet = workbook.Worksheets[0];
            sheet.Name = "People";
```

> **Почему мы создаём рабочую книгу сначала** – SmartMarker работает с уже существующим объектом `Worksheet`; рабочая книга предоставляет контейнер для всех последующих операций.

## Шаг 2: Определение данных JSON и настройка SmartMarker

Мы используем небольшой JSON‑payload, в котором перечислены два человека. Параметр `ArrayAsSingle` указывает SmartMarker рассматривать весь массив как одну логическую запись, что удобно, когда нужен простой столбец без вложенных циклов.

```csharp
            // Step 2: Define the JSON data to populate the worksheet
            string jsonData = "[{'Name':'John','Age':30},{'Name':'Anna','Age':25}]";

            // Step 3: Initialise the SmartMarker processor
            SmartMarkerProcessor processor = new SmartMarkerProcessor();

            // Important: treat the JSON array as a single record
            processor.Options.ArrayAsSingle = true;
```

> **Подсказка:** Если опустить `ArrayAsSingle`, SmartMarker попытается создать отдельную запись для каждого элемента массива, что может привести к дублированию строк или неожиданному расположению данных.

## Шаг 3: Вставка тегов SmartMarker в лист

Теги SmartMarker – это простые текстовые заполнители, окружённые `&`. Разместите их в ячейках, где должны появиться значения из JSON. В этом примере мы записываем теги напрямую из кода, но вы также можете заранее подготовить шаблон в Excel.

```csharp
            // Step 4: Write SmartMarker tags into the first row (header) and second row (data)
            sheet.Cells["A1"].PutValue("Name");                // Header
            sheet.Cells["B1"].PutValue("Age");                 // Header
            sheet.Cells["A2"].PutValue("&=Name&");             // Data placeholder
            sheet.Cells["B2"].PutValue("&=Age&");              // Data placeholder
```

> **Объяснение:** `&=Name&` указывает SmartMarker заменить ячейку полем `Name` из JSON‑объекта, а `&=Age&` делает то же самое для `Age`.

## Шаг 4: Обработка листа – заполнение Excel из JSON

Теперь позволим SmartMarker прочитать строку JSON и подставить значения в заполнители.

```csharp
            // Step 5: Apply the JSON data to the worksheet
            processor.Process(sheet, jsonData);
```

Внутри SmartMarker парсит `jsonData`, сопоставляет каждое свойство объекта с соответствующим тегом и автоматически расширяет строки, потому что `ArrayAsSingle` установлено в `true`. После обработки лист выглядит так:

| Name | Age |
|------|-----|
| John | 30  |
| Anna | 25  |

## Шаг 5: Сохранение файла XLSX

Наконец, запишите заполненную рабочую книгу на диск.

```csharp
            // Step 6: Save the populated workbook as an .xlsx file
            string outputPath = Path.Combine(
                Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
                "SmartMarkerJson.xlsx");

            workbook.Save(outputPath, SaveFormat.Xlsx);
            Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

Запуск программы создаст `SmartMarkerJson.xlsx` на вашем рабочем столе. Открытие файла в Excel покажет чистую таблицу с корректно импортированными данными JSON.

## Распространённые ошибки при импорте JSON в лист

| Проблема | Почему происходит | Как избежать |
|----------|-------------------|--------------|
| **Отсутствуют теги SmartMarker** | SmartMarker заменяет только ячейки, содержащие `&=...&`. | Тщательно проверьте точное написание тегов и регистр. |
| **Неправильный формат JSON** | Одинарные кавычки (`'`) не являются корректным JSON для встроенного парсера. | Используйте двойные кавычки (`"`) или позвольте Aspose.Cells обработать «свободный» формат, как показано. |
| **Массив рассматривается как несколько записей** | По умолчанию `ArrayAsSingle` равно `false`. | Установите `processor.Options.ArrayAsSingle = true`, когда нужна плоская таблица. |
| **Сохранение в папку только для чтения** | `workbook.Save` бросает исключение. | Выберите записываемый каталог (например, Desktop или временную папку). |

## Расширение решения

- **Несколько листов:** Создайте дополнительные листы и вызовите `processor.Process` для каждого с разными источниками JSON.  
- **Стилизация:** После обработки применяйте стили ячеек (шрифты, границы) так же, как в любой обычной операции Aspose.Cells.  
- **Большие наборы данных:** Для тысяч строк рассмотрите потоковую запись рабочей книги, чтобы снизить потребление памяти (`WorkbookDesigner` или `SaveOptions` с `EnableMemoryOptimization`).  

## Заключение

Теперь вы знаете, как **преобразовать JSON в XLSX в C#** с помощью Aspose.Cells SmartMarker. Полный процесс — **создать рабочую книгу Excel C#**, добавить теги SmartMarker, настроить процессор, **заполнить Excel из JSON** и сохранить файл — позволяет **импортировать JSON в ячейки листа** с минимальным объёмом кода.

Экспериментируйте с более сложными структурами JSON, добавляйте формулы или генерируйте диаграммы напрямую из заполненных данных. Если вам понравилось это руководство, попробуйте следующее руководство о **импорте JSON в Excel** для построения диаграмм или о **создании рабочей книги Excel C#** с расширенным форматированием.

---


## Что изучать дальше?


Следующие учебные материалы охватывают тесно связанные темы, которые развивают техники, продемонстрированные в этом руководстве. Каждый ресурс содержит полностью работающие примеры кода с пошаговыми объяснениями, помогающими вам освоить дополнительные возможности API и исследовать альтернативные подходы в ваших проектах.

- [Преобразование JSON в Excel с C# – пошаговое руководство](/cells/english/net/smart-markers-dynamic-data/convert-json-to-excel-with-c-step-by-step-guide/)
- [Как вставить JSON в шаблон Excel – пошагово](/cells/english/net/data-loading-and-parsing/how-to-insert-json-into-excel-template-step-by-step/)
- [Создание рабочей книги Excel C# – вставка JSON и сохранение как XLSX](/cells/english/net/excel-data-import-export/create-excel-workbook-c-insert-json-and-save-as-xlsx/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}