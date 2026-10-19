---
category: general
date: 2026-09-21
description: Настройте SmartMarkerOptions ArrayAsSingle в C#, чтобы экспортировать
  массивы JSON как одно значение ячейки в рабочей книге Excel.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- configure smartmarkeroptions arrayassingle
- Aspose.Cells smart markers
- export JSON array
- C# DataTable
- Workbook ProcessSmartMarkers
language: ru
lastmod: 2026-09-21
og_description: Настройте параметр SmartMarkerOptions ArrayAsSingle в C# для экспорта
  массивов JSON как единственного значения ячейки. Узнайте полное пошаговое решение.
og_image_alt: Screenshot of an Excel sheet showing a JSON array stored in a single
  cell after using SmartMarkerOptions
og_title: Настройка SmartMarkerOptions ArrayAsSingle в C# – полное руководство
schemas:
- author: Aspose
  dateModified: '2026-09-21'
  description: Configure SmartMarkerOptions ArrayAsSingle in C# to export JSON arrays
    as a single cell value in an Excel workbook.
  headline: Configure SmartMarkerOptions ArrayAsSingle in C# for JSON arrays
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: Настройка параметра ArrayAsSingle в SmartMarkerOptions на C# для JSON‑массивов
url: /ru/net/smart-markers-dynamic-data/configure-smartmarkeroptions-arrayassingle-in-c-for-json-arr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Настройка SmartMarkerOptions ArrayAsSingle в C# для массивов JSON

Если вам необходимо **настроить SmartMarkerOptions ArrayAsSingle** при генерации Excel‑файлов с помощью Aspose.Cells, это руководство покажет, как это сделать. Вы увидите, как сохранить массив JSON в одной ячейке, а не распределять его элементы по нескольким строкам.

Работа с JSON‑данными в таблицах часто требует выбора между «развёрнутым» представлением и компактным. Во многих отчётных сценариях — например, при хранении списка тегов или набора идентификаторов — требуется, чтобы вся строка JSON оставалась в одной ячейке. Флаг **ArrayAsSingle** в `SmartMarkerOptions` делает это возможным.

В этом учебнике вы:

* Создадите `DataTable`, содержащий массив JSON в отдельном столбце.  
* Разместите Smart Markers в листе Excel.  
* **Настроите SmartMarkerOptions ArrayAsSingle**, чтобы массив JSON рассматривался как единое значение ячейки.  
* Обработаете маркеры и сохраните книгу.  
* Проверите результат.

> **Prerequisites** – Вам понадобится библиотека Aspose.Cells for .NET (v23.12 или новее) и среда разработки .NET (рекомендовано Visual Studio 2022). Предполагаются базовые знания C# и DataTables.

---

## Шаг 1: Подготовьте источник данных с массивом JSON

Сначала создайте `DataTable`, имитирующий данные, которые вы могли бы получить из сервиса или базы данных. Столбец **Names** содержит JSON‑строку, представляющую массив имён.

```csharp
using System;
using System.Data;
using Aspose.Cells;

DataTable dataTable = new DataTable();
dataTable.Columns.Add("Id", typeof(int));
dataTable.Columns.Add("Names", typeof(string));

// Store the JSON array as a plain string
dataTable.Rows.Add(1, "[\"Alice\",\"Bob\"]");
```

*Зачем это нужно?*  
Smart Markers читают данные напрямую из объектов .NET. Поместив массив JSON в строковый столбец, вы сохраняете точный синтаксис JSON, который позже может быть записан в ячейку без изменений.

---

## Шаг 2: Вставьте Smart Markers в новую книгу

Создайте новую книгу, выберите первый лист и запишите Smart Markers, ссылающиеся на всю таблицу и конкретный столбец **Names**.

```csharp
// Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.Worksheets[0];

// Smart marker for the entire table (optional, shown for completeness)
worksheet.Cells["A1"].PutValue("&=dataTable");

// Smart marker that targets only the Names column
worksheet.Cells["A2"].PutValue("&=dataTable.Names");
```

Маркёр `&=dataTable.Names` указывает Aspose.Cells заменить ячейку значением столбца **Names** для каждой строки в `dataTable`. Поскольку у нас только одна строка, маркер будет обработан один раз.

---

## Шаг 3: **Настройте SmartMarkerOptions ArrayAsSingle**

По умолчанию Aspose.Cells разворачивает строку, похожую на массив, в отдельные строки. Установка `ArrayAsSingle` в `true` переопределяет это поведение, заставляя весь JSON‑строку оставаться в одной ячейке.

```csharp
SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions
{
    // Export the JSON array as a single cell value
    ArrayAsSingle = true
};
```

*Зачем включать `ArrayAsSingle`?*  
Когда `ArrayAsSingle` равно `false`, движок интерпретирует `["Alice","Bob"]` как два отдельных значения и записывает их в соседние строки. Установка `true` рассматривает строку как атомарное значение, что необходимо для сохранения формата JSON внутри Excel.

---

## Шаг 4: Обработайте Smart Markers с настроенными параметрами

Теперь запустите движок Smart Marker, передав объект параметров, который вы только что сконфигурировали.

```csharp
// Process smart markers using the custom options
workbook.ProcessSmartMarkers(smartMarkerOptions);
```

Во время обработки Aspose.Cells читает `dataTable`, применяет маркеры и учитывает флаг `ArrayAsSingle`, оставляя массив JSON нетронутым.

---

## Шаг 5: Сохраните книгу и проверьте результат

Наконец, запишите книгу на диск. Откройте полученный файл в Excel или любом просмотрщике таблиц, чтобы убедиться, что ячейка **A2** содержит точную JSON‑строку.

```csharp
// Save the resulting workbook
string outputPath = @"C:\Temp\SmartMarkerJson.xlsx";
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

### Ожидаемый результат

| A   |
|-----|
| **["Alice","Bob"]** |

Ячейка **A2** отображает массив JSON как единое текстовое значение, точно такое же, как хранится в `DataTable`. Дополнительные строки не создаются.

---

## Распространённые варианты и обработка граничных случаев

| Ситуация | Как адаптировать |
|-----------|--------------|
| **Несколько строк с массивами JSON** | Тот же параметр `ArrayAsSingle` работает; массив JSON каждой строки остаётся в своей ячейке. |
| **Разные структуры JSON (объекты, вложенные массивы)** | Пока JSON хранится как строка, `ArrayAsSingle` сохраняет его целиком. Для сложных объектов может потребоваться экранирование кавычек. |
| **Использование другого источника данных (например, List\<T\>)** | Замените `DataTable` любой перечисляемой коллекцией; синтаксис маркера (`&=myList.Property`) остаётся тем же. |
| **Экспорт в CSV вместо XLSX** | `ArrayAsSingle` по‑прежнему применим, но помните, что CSV не сохраняет формат ячеек; возможно, придётся обернуть JSON в кавычки. |

**Pro tip:** Всегда задавайте `ArrayAsSingle` *до* вызова `ProcessSmartMarkers`. Изменение флага после обработки не влияет на уже созданные ячейки.

---

## Полный, готовый к запуску пример

Ниже приведена полная программа, которую можно скопировать в консольное приложение. Включены все директивы `using` и комментарии для ясности.

```csharp
using System;
using System.Data;
using Aspose.Cells;

namespace SmartMarkerDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create the data source with a JSON array
            DataTable dataTable = new DataTable();
            dataTable.Columns.Add("Id", typeof(int));
            dataTable.Columns.Add("Names", typeof(string));
            dataTable.Rows.Add(1, "[\"Alice\",\"Bob\"]");

            // 2️⃣ Build a workbook and place smart markers
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.Worksheets[0];
            worksheet.Cells["A1"].PutValue("&=dataTable");          // whole table (optional)
            worksheet.Cells["A2"].PutValue("&=dataTable.Names");   // Names column

            // 3️⃣ Configure SmartMarkerOptions to treat arrays as single values
            SmartMarkerOptions options = new SmartMarkerOptions
            {
                ArrayAsSingle = true
            };

            // 4️⃣ Process the markers with the custom options
            workbook.ProcessSmartMarkers(options);

            // 5️⃣ Save the file
            string path = @"C:\Temp\SmartMarkerJson.xlsx";
            workbook.Save(path);
            Console.WriteLine($"Workbook saved to {path}");
        }
    }
}
```

Запустите программу, откройте `SmartMarkerJson.xlsx`, и вы увидите, что массив JSON сохранён в ячейке **A2**.

---

## Заключение

Теперь вы знаете, как **настроить SmartMarkerOptions ArrayAsSingle** в C# для сохранения массива JSON в одной ячейке при работе с smart markers Aspose.Cells. Шаги — подготовка `DataTable`, вставка маркеров, установка флага `ArrayAsSingle`, обработка и сохранение — образуют повторяемый шаблон, который можно применять в любой ситуации, где требуется компактное представление JSON в Excel.

Дальше вы можете изучить:

* **Aspose.Cells smart markers** для обхода коллекций.  
* Экспорт **вложенных JSON‑объектов** с настройкой формата ячеек.  
* Комбинирование **условного форматирования** со smart markers для более богатых отчётов.

Экспериментируйте с различными структурами данных и делитесь результатами. Приятного кодинга!

## Что изучать дальше?

Следующие учебники охватывают тесно связанные темы, расширяющие техники, продемонстрированные в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, помогающими освоить дополнительные возможности API и исследовать альтернативные подходы в ваших проектах.

- [Create Excel Workbook from JSON – Complete Aspose.Cells Guide](/cells/english/net/data-loading-and-parsing/create-excel-workbook-from-json-complete-aspose-cells-guide/)
- [Create Configure Excel Workbook Aspose Cells Net](/cells/hindi/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)
- [Create Configure Excel Workbook Aspose Cells Net](/cells/german/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}