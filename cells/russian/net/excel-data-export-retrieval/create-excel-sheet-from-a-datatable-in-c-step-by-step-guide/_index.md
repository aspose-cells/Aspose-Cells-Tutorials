---
category: general
date: 2026-08-11
description: Создайте лист Excel из DataTable в C# и экспортируйте DataTable в Excel
  с автоматическим именованием листов. Узнайте, как добавить строки в DataTable и
  сохранить книгу в формате xlsx.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel sheet
- export datatable to excel
- add rows to datatable
- create multiple excel sheets
- save workbook as xlsx
language: ru
lastmod: 2026-08-11
og_description: Создайте лист Excel из DataTable в C#. Этот учебник показывает, как
  экспортировать DataTable в Excel, добавлять строки в DataTable, генерировать несколько
  листов Excel и сохранять книгу в формате xlsx.
og_image_alt: Screenshot of an Excel workbook created from a DataTable with automatically
  renamed sheets
og_title: Создание Excel‑листа из DataTable в C# – полное руководство по программированию
schemas:
- author: Aspose
  dateModified: '2026-08-11'
  description: Create excel sheet from a DataTable in C# and export datatable to excel
    with automatic sheet naming. Learn how to add rows to datatable and save workbook
    as xlsx.
  headline: Create excel sheet from a DataTable in C# – step‑by‑step guide
  type: TechArticle
tags:
- C#
- Excel automation
- Aspose.Cells
title: Создание листа Excel из DataTable в C# – пошаговое руководство
url: /ru/net/excel-data-export-retrieval/create-excel-sheet-from-a-datatable-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание листа Excel из DataTable в C# – пошаговое руководство

Если вам нужно **создать лист Excel** из `DataTable` в C#, это руководство покажет, как это сделать. Вы увидите, как **экспортировать DataTable в Excel**, добавлять строки, обрабатывать дублирующиеся имена листов и, наконец, **сохранить книгу как xlsx**.

В примере используется Aspose.Cells — широко применяемая .NET‑библиотека для автоматизации Excel. Те же концепции применимы к другим библиотекам, поддерживающим обработку в стиле SmartMarker, но код ниже работает «из коробки» с Aspose.Cells 22.12 и новее.

## Prerequisites

Прежде чем начать, убедитесь, что у вас есть:

* .NET 6.0 SDK или более новая версия, установленная  
* Ссылка на пакет **Aspose.Cells** NuGet (`Install-Package Aspose.Cells`)  
* Базовое знакомство с `DataTable` и консольными приложениями C#  

Эти требования делают руководство самостоятельным и исключают необходимость во внешних инструментах.

## Step 1: Create a DataTable that will be exported to Excel

Первый шаг — построить `DataTable`, отражающую данные, которые вы хотите видеть в листе. Здесь мы создаём таблицу с именем **Sheet1**, добавляем столбец `Id` и вставляем две строки.

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a DataTable named "Sheet1"
        DataTable dataTable = new DataTable("Sheet1");
        dataTable.Columns.Add("Id", typeof(int));

        // 2️⃣ Add rows to the DataTable
        dataTable.Rows.Add(1);
        dataTable.Rows.Add(2);

        // Subsequent steps are called from here
        ProcessAndSaveWorkbook(dataTable);
    }
```

**Почему это важно:**  
`DataTable` — удобное представление табличных данных в памяти. Название таблицы `"Sheet1"` сообщает Aspose.Cells, к какому листу обращаться при обработке SmartMarkers.

## Step 2: Add rows to the DataTable (optional expansion)

Если ваши исходные данные динамичны, часто требуется добавлять строки в цикле. Ниже приведён типичный шаблон:

```csharp
        // Example: add rows from a collection
        int[] ids = { 3, 4, 5 };
        foreach (int id in ids)
        {
            dataTable.Rows.Add(id);
        }
```

**Подсказка:** При добавлении большого количества строк рассмотрите возможность отключения ограничений (`dataTable.Constraints.Clear()`), чтобы повысить производительность.

## Step 3: Configure SmartMarker options to create multiple excel sheets automatically

Параметры SmartMarker позволяют управлять тем, как обрабатываются дублирующиеся имена листов. Установка `DetailSheetNewName` в `"Sheet1_{0}"` заставит Aspose.Cells переименовывать последующие листы в `Sheet1_1`, `Sheet1_2` и т.д.

```csharp
    private static void ProcessAndSaveWorkbook(DataTable dataTable)
    {
        // 3️⃣ Set SmartMarker options for automatic sheet renaming
        SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions
        {
            // New sheets will be named Sheet1_1, Sheet1_2, etc.
            DetailSheetNewName = "Sheet1_{0}"
        };
```

**Почему это важно:**  
Когда вы обрабатываете несколько объектов `DataTable` с одинаковым именем, Excel обычно выдаёт ошибку, потому что имена листов должны быть уникальными. Шаблон `DetailSheetNewName` автоматически устраняет этот конфликт.

## Step 4: Process the SmartMarkers and export datatable to excel

Теперь создаём новый `Workbook`, вызываем `ProcessSmartMarkers` и позволяем Aspose.Cells заполнить лист(ы) на основе `DataTable`.

```csharp
        // 4️⃣ Create a workbook and process SmartMarkers
        Workbook workbook = new Workbook();
        workbook.ProcessSmartMarkers(dataTable, smartMarkerOptions);
```

**Объяснение:**  
`ProcessSmartMarkers` сканирует книгу в поиске маркеров вроде `&=Sheet1!A1` (не показано здесь) и заменяет их данными из `dataTable`. Поскольку мы начали с пустой книги, Aspose.Cells создаёт новый лист с именем, совпадающим с именем таблицы, и заполняет его добавленными строками.

## Step 5: Save workbook as xlsx

Наконец, сохраняем книгу на диск в современном формате OpenXML (`.xlsx`). При необходимости измените путь к файлу под свою среду.

```csharp
        // 5️⃣ Save the workbook as an .xlsx file
        string outputPath = @"YOUR_DIRECTORY\DuplicateSheets.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

**Результат:**  
Запуск программы создаёт файл Excel, содержащий:

| Имя листа | Строки |
|------------|------|
| Sheet1     | 1, 2, 3, 4, 5 |
| Sheet1_1   | (если был обработан другой DataTable с тем же именем) |

Логика переименования листов обеспечивает **создание нескольких листов Excel** без ручного управления именами.

## Common variations and edge cases

| Ситуация | Как решить |
|-----------|------------------|
| **Очень большие таблицы** (≥ 100 000 строк) | Перед обработкой установить `WorkbookSettings.MemorySetting = MemorySetting.MemoryOptimized`, чтобы снизить потребление памяти. |
| **Пользовательский порядок столбцов** | Переставьте объекты `DataColumn` в `DataTable` перед вызовом `ProcessSmartMarkers`. |
| **Несколько DataTable с разными именами** | Вызывайте `ProcessSmartMarkers` для каждой таблицы; Aspose.Cells автоматически создаст отдельный лист для каждого имени. |
| **Необходима строка заголовка со стилизацией** | После обработки обратитесь к `Worksheet.Cells["A1"]` и примените свойства `Style` (шрифт, фон). |
| **Сохранение в поток вместо файла** | Замените `workbook.Save(outputPath, SaveFormat.Xlsx)` на `workbook.Save(stream, SaveFormat.Xlsx)`. |

**Pro tip:** Всегда оборачивайте операции с файловой системой в блоки `try…catch`, чтобы быстро выявлять проблемы с правами доступа.

## Full source code (ready to copy)

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create the DataTable that will be exported
        DataTable dataTable = new DataTable("Sheet1");
        dataTable.Columns.Add("Id", typeof(int));

        // Add rows – you can replace this with your own data source
        dataTable.Rows.Add(1);
        dataTable.Rows.Add(2);
        int[] extraIds = { 3, 4, 5 };
        foreach (int id in extraIds)
        {
            dataTable.Rows.Add(id);
        }

        // Process SmartMarkers and save the workbook
        ProcessAndSaveWorkbook(dataTable);
    }

    private static void ProcessAndSaveWorkbook(DataTable dataTable)
    {
        // Configure SmartMarkerOptions to rename duplicate sheets automatically
        SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions
        {
            DetailSheetNewName = "Sheet1_{0}"
        };

        // Create a new workbook and populate it from the DataTable
        Workbook workbook = new Workbook();
        workbook.ProcessSmartMarkers(dataTable, smartMarkerOptions);

        // Save the workbook as an .xlsx file
        string outputPath = @"YOUR_DIRECTORY\DuplicateSheets.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

### Expected output

Запуск программы выводит:

```
Workbook saved to YOUR_DIRECTORY\DuplicateSheets.xlsx
```

Открытие `DuplicateSheets.xlsx` показывает лист с именем **Sheet1**, где столбец `Id` содержит значения `1, 2, 3, 4, 5`. Если позже в той же книге обработать другой `DataTable` с именем `"Sheet1"`, Aspose.Cells автоматически создаст **Sheet1_1**, **Sheet1_2** и т.д.

## Conclusion

Теперь вы знаете, как **создать лист Excel** из `DataTable` в C#, **экспортировать DataTable в Excel**, **добавлять строки в DataTable**, генерировать **несколько листов Excel** с автоматическим именованием и **сохранять книгу как xlsx**. Полный, готовый к запуску пример демонстрирует весь процесс от начала до конца и предоставляет практические советы для работы с большими наборами данных и пользовательской стилизацией.

### What’s next?

* Изучите **форматирование ячеек** (шрифты, цвета, границы), получая доступ к `Worksheet.Cells` после `ProcessSmartMarkers`.  
* Используйте **циклы SmartMarker** для создания master‑detail отчётов в одной книге.  
* Перейдите к **экспорту в CSV**, заменив `SaveFormat.Csv`, если нужен текстовый вариант.  

Не стесняйтесь адаптировать код под свои источники данных — будь то запрос к базе, ответ API или коллекция в памяти. Приятного кодинга!

## What Should You Learn Next?

Следующие руководства охватывают тесно связанные темы, расширяющие техники, продемонстрированные в этом пособии. Каждый ресурс включает полностью рабочие примеры кода с пошаговыми объяснениями, помогающими освоить дополнительные возможности API и исследовать альтернативные подходы в ваших проектах.

- [How to Create and Save an Excel Workbook as ODS Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [How to Create and Save an Excel Workbook as SVG using Aspose.Cells for Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)
- [How to Create and Export Excel to HTML Using Aspose.Cells Java | Workbook Operations Guide](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}