---
category: general
date: 2026-11-25
description: Узнайте, как создавать несколько листов в файле Excel с помощью C#. В
  этом руководстве рассматривается сохранение рабочей книги в формате XLSX и обработка
  дублирующихся имён листов.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create multiple sheets
- create excel file c#
- duplicate sheet names
- save workbook xlsx
language: ru
lastmod: 2026-11-25
og_description: Создайте несколько листов в файле Excel с помощью C#. Следуйте этому
  полному руководству, чтобы сохранить рабочую книгу в формате XLSX и управлять дублирующимися
  именами листов.
og_image_alt: Code editor showing C# sample that generates an Excel workbook with
  several detail sheets
og_title: Создайте несколько листов в файле Excel с помощью C# – пошаговое руководство
schemas:
- author: Aspose
  dateModified: '2026-11-25'
  description: Learn how to create multiple sheets in an Excel file using C#. This
    guide covers saving the workbook as XLSX and handling duplicate sheet names.
  headline: How to create multiple sheets in an Excel file using C#
  type: TechArticle
- description: Learn how to create multiple sheets in an Excel file using C#. This
    guide covers saving the workbook as XLSX and handling duplicate sheet names.
  name: How to create multiple sheets in an Excel file using C#
  steps:
  - name: '**Create a new workbook** and name the first worksheet *Master*.'
    text: '**Create a new workbook** and name the first worksheet *Master*.'
  - name: '**Insert a smart marker** that tells Aspose.Cells how to name the detail
      worksheets.'
    text: '**Insert a smart marker** that tells Aspose.Cells how to name the detail
      worksheets.'
  - name: '**Process the smart marker** with a data source that may contain duplicate
      names.'
    text: '**Process the smart marker** with a data source that may contain duplicate
      names.'
  - name: '**Save the workbook** as an XLSX file.'
    text: '**Save the workbook** as an XLSX file.'
  type: HowTo
tags:
- C#
- Excel
- Aspose.Cells
- Automation
title: Как создать несколько листов в файле Excel с помощью C#
url: /ru/net/worksheet-management/how-to-create-multiple-sheets-in-an-excel-file-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как создать несколько листов в файле Excel с помощью C#

Если вам нужно **create multiple sheets** в книге Excel из C#, этот учебник предоставляет готовое к запуску решение. К концу руководства у вас будет программа, которая генерирует главный лист, создает листы деталей с помощью smart markers и сохраняет результат в файл **XLSX** — при этом безопасно обрабатывая **duplicate sheet names**.

Вы также увидите, как **create excel file c#** проекты с библиотекой Aspose.Cells, популярным выбором для серверной автоматизации электронных таблиц.

## Предварительные требования

* .NET 6.0 SDK или более поздняя версия, установленная  
* Visual Studio 2022 (или любая IDE, поддерживающая .NET)  
* Пакет NuGet **Aspose.Cells for .NET** (`Aspose.Cells`) — он предоставляет классы `Workbook`, `Worksheet` и `SmartMarkersFactory`, используемые в коде.  

Вы можете добавить пакет с помощью следующей команды CLI:

```bash
dotnet add package Aspose.Cells
```

> **Совет:** Используйте приватный NuGet‑фид или бесплатную community‑edition, если вам нужны только базовые возможности.

## Обзор решения

Подход состоит из четырёх логических шагов:

1. **Создать новую книгу** и назовите первый лист *Master*.  
2. **Вставить smart marker** который указывает Aspose.Cells, как именовать листы деталей.  
3. **Обработать smart marker** с источником данных, который может содержать дублирующиеся имена.  
4. **Сохранить книгу** как файл XLSX.  

Каждый шаг подробно объясняется ниже, а полный исходный файл предоставлен в конце статьи.

## Шаг 1: Создать новую книгу и добавить главный лист

Класс `Workbook` представляет весь файл Excel. При создании экземпляра без параметров Aspose.Cells создает книгу по умолчанию, которая уже содержит один лист. Переименование этого листа в *Master* делает его назначение очевидным.

```csharp
using Aspose.Cells;
using System;
using System.Data;   // For DataTable used as a data source

// 1️⃣ Create a new workbook
Workbook workbook = new Workbook();

// 1️⃣ Retrieve the first worksheet (index 0) and give it a friendly name
Worksheet masterSheet = workbook.Worksheets[0];
masterSheet.Name = "Master";
```

**Почему это важно:**  
Начало работы с чистой книгой избегает оставшегося форматирования или скрытых листов от предыдущих запусков. Именование листа *Master* помогает позже найти smart marker и делает файл читаемым для нетехнических пользователей.

## Шаг 2: Вставить smart marker, определяющий имена листов деталей

Smart markers — это заполнители, которые Aspose.Cells заменяет данными во время выполнения. Синтаксис `&=DetailSheetNewName=Detail` сообщает движку создать новый лист для каждой строки в источнике данных, используя значение столбца `Detail` в качестве имени листа.

```csharp
// 2️⃣ Place a smart marker in cell A1 of the master sheet
masterSheet.Cells["A1"].PutValue("&=DetailSheetNewName=Detail");
```

**Почему это важно:**  
Smart marker устраняет необходимость писать цикл, который вручную добавляет листы. Он также автоматически копирует макет главного листа на каждый вновь созданный лист, обеспечивая согласованный стиль.

## Шаг 3: Обработать smart marker с источником данных, который может содержать дубликаты

Ниже мы создаём `DataTable`, имитирующую источник данных. Обратите внимание, что столбец *Detail* содержит дублирующиеся значения (`"Report"` встречается дважды). Метод `SmartMarkersFactory.Process` учитывает настройку `AllowDuplicateSheetNames`, которая по умолчанию **true** в этом примере.

```csharp
// 3️⃣ Build a sample data source (DataTable) with duplicate sheet names
DataTable dataSource = new DataTable();
dataSource.Columns.Add("Detail", typeof(string));
dataSource.Columns.Add("Value", typeof(double));

// Add rows – "Report" appears twice to demonstrate duplicate handling
dataSource.Rows.Add("Report", 123.45);
dataSource.Rows.Add("Summary", 67.89);
dataSource.Rows.Add("Report", 101.12);   // Duplicate sheet name

// Register the data source in the workbook's data collection
workbook.Worksheets[0].SmartMarkersFactory.Process(new[] { "dataSource" });
```

> **Важно:** Если необходимо гарантировать уникальные имена листов, установите `workbook.Settings.CheckDuplicateSheetNames = true;` перед обработкой. Поведение по умолчанию создаёт листы с одинаковыми именами, что Excel позволяет, но может сбивать с толку при навигации по файлу.

## Шаг 4: Сохранить книгу в файл XLSX

Наконец, сохраняем сгенерированную книгу на диск. Метод `Save` автоматически выбирает подходящий писатель на основе расширения файла.

```csharp
// 4️⃣ Save the workbook – the file will contain the master sheet and two "Report" sheets plus a "Summary" sheet
string outputPath = @"C:\Temp\duplicate_detail_sheets.xlsx";
workbook.Save(outputPath, SaveFormat.Xlsx);

Console.WriteLine($"Workbook saved to {outputPath}");
```

**Ожидаемый результат**

Когда вы откроете `duplicate_detail_sheets.xlsx`, вы увидите:

| Имя листа | Содержимое (первая строка) |
|------------|---------------------------|
| Master     | Заполнитель smart marker (нет данных) |
| Report     | Строка данных 1 (`123.45`) |
| Summary    | Строка данных 2 (`67.89`) |
| Report (2) | Строка данных 3 (`101.12`) |

Второй лист *Report* автоматически переименован в *Report (2)* Aspose.Cells, чтобы избежать жёсткой ошибки, сохранив при этом исходный дублирующий смысл.

## Полный исходный код

Скопируйте следующий файл в консольный проект (`dotnet new console`) и запустите его. Программа демонстрирует полный рабочий процесс для **create multiple sheets** и **save workbook xlsx**, обрабатывая **duplicate sheet names**.

```csharp
// Program.cs
using Aspose.Cells;
using System;
using System.Data;

namespace ExcelMultipleSheetsDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create a new workbook and name the first sheet "Master"
            Workbook workbook = new Workbook();
            Worksheet masterSheet = workbook.Worksheets[0];
            masterSheet.Name = "Master";

            // Step 2: Add a smart marker that will generate detail sheets
            masterSheet.Cells["A1"].PutValue("&=DetailSheetNewName=Detail");

            // Step 3: Prepare a data source with duplicate sheet names
            DataTable dataSource = new DataTable();
            dataSource.Columns.Add("Detail", typeof(string));
            dataSource.Columns.Add("Value", typeof(double));

            dataSource.Rows.Add("Report", 123.45);
            dataSource.Rows.Add("Summary", 67.89);
            dataSource.Rows.Add("Report", 101.12); // duplicate name

            // Bind the data source to the workbook
            workbook.Worksheets[0].SmartMarkersFactory.Process(new[] { "dataSource" });

            // Step 4: Save the workbook as an XLSX file
            string outputPath = @"C:\Temp\duplicate_detail_sheets.xlsx";
            workbook.Save(outputPath, SaveFormat.Xlsx);

            Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

Запустите `dotnet run` из папки проекта. После выполнения откройте сгенерированный файл, чтобы убедиться, что созданы три листа деталей, два из которых имеют базовое имя **Report**.

## Обработка граничных случаев и лучшие практики

| Ситуация | Рекомендуемый подход |
|-----------|----------------------|
| **Очень большие наборы данных** ( > 10 000 строк) | Используйте `WorkbookSettings.MemorySetting = MemorySetting.MemoryPreference;` чтобы снизить нагрузку на память. |
| **Пользовательские правила именования листов** | Предобработайте столбец `Detail`, заменив недопустимые символы (`/ \ ? * [ ] :`) перед вызовом `Process`. |
| **Необходимы действительно уникальные имена** | Установите `workbook.Settings.CheckDuplicateSheetNames = true;` и задайте резервную схему именования (например, добавить GUID). |
| **Генерация PDF вместо XLSX** | После сохранения вызовите `workbook.Save("output.pdf", SaveFormat.Pdf);` — Aspose.Cells может экспортировать напрямую в PDF. |
| **Запуск в веб‑сервисе** | Запишите книгу в `MemoryStream` и верните её как загрузку файла, чтобы избежать операций ввода‑вывода на диск. |

### Совет: переиспользовать один экземпляр `Workbook` для нескольких экспортов

Если ваше приложение создаёт несколько отчётов за запрос, храните один объект `Workbook` в памяти, очистите его листы (`workbook.Worksheets.Clear();`) и повторите шаги. Это избавляет от накладных расходов при повторной загрузке среды Aspose.Cells.

## Заключение

Теперь вы знаете, как **create multiple sheets** в книге Excel с помощью C#, как **create excel file c#** с Aspose.Cells, как управлять **duplicate sheet names** и как надёжно **save workbook xlsx**. Полный пример демонстрирует чистый, поддерживаемый шаблон, масштабируемый от быстрых скриптов до сервисов производственного уровня.

### Что дальше?

* Исследуйте **conditional formatting** на сгенерированных листах, чтобы выделять ключевые значения.  
* Используйте **Smart Markers** для автоматического заполнения таблиц, диаграмм или сводных таблиц.  
* Интегрируйте код в ASP.NET Core API и возвращайте файл XLSX как поток загрузки.

## Что вам стоит изучить дальше?

Следующие учебники охватывают тесно связанные темы, построенные на техниках, продемонстрированных в этом руководстве. Каждый ресурс включает полные работающие примеры кода с пошаговыми объяснениями, помогая вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в собственных проектах.

- [Создать Excel Workbook C# – Пошаговое руководство по записи дат и сохранению как XLSX](/cells/english/net/excel-workbook/create-excel-workbook-c-step-by-step-guide-to-write-dates-sa/)
- [Создать новую книгу в C# – Добавить формулу и сохранить файл Excel](/cells/english/net/excel-workbook/create-new-workbook-in-c-add-formula-and-save-excel-file/)
- [Создать Excel workbook и сохранить его в файл в C#](/cells/english/net/excel-workbook/create-excel-workbook-and-save-it-to-file-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}