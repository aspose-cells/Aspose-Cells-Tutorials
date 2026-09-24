---
category: general
date: 2026-09-24
description: Создайте Excel‑книгу программно, научитесь создавать несколько листов‑деталей,
  а затем сохраните книгу в файл xlsx с наглядным примером на C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook programmatically
- how to create multiple detail sheets
- save workbook as xlsx file
language: ru
lastmod: 2026-09-24
og_description: Создайте книгу Excel программно, посмотрите, как создать несколько
  листов‑деталей и сохранить книгу в файл xlsx в одном, готовом к запуску примере.
og_image_alt: Screenshot of an Excel workbook created programmatically in C#
og_title: Создание Excel‑книги программно — полное руководство по C#
schemas:
- author: Aspose
  dateModified: '2026-09-24'
  description: Create Excel workbook programmatically and learn how to create multiple
    detail sheets, then save workbook as xlsx file with a clear C# example.
  headline: Create Excel workbook programmatically using Smart Markers
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
title: Создать рабочую книгу Excel программно с помощью Smart Markers
url: /ru/net/smart-markers-dynamic-data/create-excel-workbook-programmatically-using-smart-markers/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание рабочей книги Excel программно с использованием Smart Markers

Если вам нужно **создать рабочую книгу Excel программно**, это руководство покажет, как сделать это с помощью Aspose.Cells .NET. Вы также узнаете, **как создать несколько листов‑деталей** из единого источника данных и, наконец, **сохранить рабочую книгу в файл xlsx** без каких‑либо ручных действий.  

Решение полностью автономно: мы пройдёмся по каждой строке кода, объясним, почему каждое настройка важна, и рассмотрим распространённые подводные камни, такие как дублирование имён листов. К концу вы получите готовое к запуску консольное приложение, которое создаёт рабочую книгу с главным листом и набором листов‑деталей.

## Что понадобится

| Требование | Причина |
|------------|---------|
| .NET 6.0 SDK или новее | Обеспечивает среду выполнения для консольного приложения C# |
| Aspose.Cells for .NET (пакет NuGet `Aspose.Cells`) | Предоставляет классы `Workbook`, `SmartMarkerProcessor` и `SmartMarkerOptions` |
| Простой источник данных (например, `DataTable` или список объектов) | Предоставляет значения, которые будут расширены Smart Markers |
| Visual Studio 2022 или любой редактор, поддерживающий .NET | Обеспечивает простоту компиляции и запуска кода |

> **Pro tip:** Установите пакет Aspose.Cells через CLI перед началом работы:  
> `dotnet add package Aspose.Cells`

## Шаг 1: Настройка проекта и импорт пространств имён

Создайте новый консольный проект и подключите необходимые пространства имён.

```csharp
using System;
using System.Data;               // For DataTable (sample data source)
using Aspose.Cells;              // Core Excel API
using Aspose.Cells.SmartMarkers; // Smart Marker processing
```

*Почему это важно*: `Aspose.Cells` управляет жизненным циклом рабочей книги, а `Aspose.Cells.SmartMarkers` предоставляет мощный движок Smart Marker, способный генерировать множество листов из одного шаблона.

## Шаг 2: Программное создание рабочей книги Excel

Первое конкретное действие — создать экземпляр `Workbook`. Этот объект представляет весь файл Excel в памяти.

```csharp
// Step 2: Create a new workbook (or load an existing template)
Workbook workbook = new Workbook(); // an empty workbook with one default sheet
```

Если вы предпочитаете начать с шаблона, который уже содержит строки заголовков или форматирование, замените `new Workbook()` на `new Workbook("Template.xlsx")`. Остальная часть процесса работает идентично.

## Шаг 3: Подготовка шаблона Smart Marker

Smart Markers работают с содержимым ячеек, содержащих заполнители вроде `&=Employees.Name`. Для этого руководства мы добавим простой шаблон напрямую через код, но вы также можете отредактировать лист вручную в Excel.

```csharp
// Access the first worksheet (index 0)
Worksheet sheet = workbook.Worksheets[0];

// Write a header row
sheet.Cells["A1"].PutValue("Employee Report");

// Insert a Smart Marker that will generate a detail sheet for each employee
sheet.Cells["A3"].PutValue("&=Employees.Name");

// Optional: add column titles for the detail sheet
sheet.Cells["A4"].PutValue("Name");
sheet.Cells["B4"].PutValue("Department");
sheet.Cells["C4"].PutValue("Salary");
```

*Почему это важно*: Заполнитель `&=Employees.Name` указывает процессору Smart Marker проходить по коллекции `Employees`. Каждый проход создаст новый лист, потому что мы настроим процессор создавать **лист‑деталь** для каждой строки.

## Шаг 4: Создание источника данных, содержащего несколько строк

Мы используем `DataTable` как быстрый способ смоделировать коллекцию записей сотрудников.

```csharp
// Step 4: Create a DataTable with sample employee data
DataTable employees = new DataTable("Employees");
employees.Columns.Add("Name", typeof(string));
employees.Columns.Add("Department", typeof(string));
employees.Columns.Add("Salary", typeof(decimal));

employees.Rows.Add("Alice Johnson", "Finance", 72000);
employees.Rows.Add("Bob Smith", "Engineering", 95000);
employees.Rows.Add("Carol Lee", "Marketing", 63000);
```

Вы можете заменить это любой `IEnumerable` (например, `List<Employee>`) — Smart Markers принимают любой источник данных, реализующий `IEnumerable`.

## Шаг 5: Настройка параметров Smart Marker – как создать несколько листов‑деталей

По умолчанию Smart Markers записывают данные обратно в тот же лист. Чтобы генерировать **несколько листов‑деталей**, необходимо установить свойство `DetailSheetNewName`. Это также демонстрирует **как создать несколько листов‑деталей** без конфликтов имён.

```csharp
// Step 5: Configure Smart Marker options
SmartMarkerOptions smOptions = new SmartMarkerOptions
{
    // Each iteration will create a new sheet named "Detail"
    DetailSheetNewName = "Detail"
};
```

Если источник данных содержит дублирующиеся имена, процессор автоматически добавит числовой суффикс (например, `Detail_1`, `Detail_2`). Это предотвращает ошибки выполнения и гарантирует сохранение всех листов‑деталей.

## Шаг 6: Обработка Smart Markers

Теперь вызываем процессор, передавая источник данных и только что определённые параметры.

```csharp
// Step 6: Process Smart Markers
workbook.Worksheets[0].SmartMarkerProcessor.Process(employees, smOptions);
```

*Почему это важно*: Процессор читает заполнитель `&=Employees.Name`, проходит по каждой строке `employees`, создаёт новый лист под названием “Detail” и записывает данные строки в этот лист. Исходный лист остаётся как сводный или главный лист.

## Шаг 7: Сохранение рабочей книги в файл xlsx

Наконец, сохраняем рабочую книгу на диск, используя шаблон **save workbook as xlsx file**.

```csharp
// Step 7: Save the resulting workbook
string outputPath = @"./output/detail.xlsx";
workbook.Save(outputPath, SaveFormat.Xlsx);
Console.WriteLine($"Workbook saved to {outputPath}");
```

Перечисление `SaveFormat.Xlsx` гарантирует, что файл будет сохранён в современном формате Office Open XML, совместимом с Excel 2007+ и большинством облачных сервисов.

## Полный, исполняемый пример

Скопируйте следующий код в `Program.cs` проекта .NET console и запустите его. Программа сгенерирует `detail.xlsx` в папке `output`, содержащий один главный лист и три листа‑детали (по одному на каждого сотрудника).

```csharp
using System;
using System.Data;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

namespace ExcelSmartMarkerDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create an empty workbook
            Workbook workbook = new Workbook();

            // 2️⃣ Build a simple template with a Smart Marker
            Worksheet sheet = workbook.Worksheets[0];
            sheet.Cells["A1"].PutValue("Employee Report");
            sheet.Cells["A3"].PutValue("&=Employees.Name");
            sheet.Cells["A4"].PutValue("Name");
            sheet.Cells["B4"].PutValue("Department");
            sheet.Cells["C4"].PutValue("Salary");

            // 3️⃣ Prepare the data source
            DataTable employees = new DataTable("Employees");
            employees.Columns.Add("Name", typeof(string));
            employees.Columns.Add("Department", typeof(string));
            employees.Columns.Add("Salary", typeof(decimal));

            employees.Rows.Add("Alice Johnson", "Finance", 72000);
            employees.Rows.Add("Bob Smith", "Engineering", 95000);
            employees.Rows.Add("Carol Lee", "Marketing", 63000);

            // 4️⃣ Configure Smart Marker options (how to create multiple detail sheets)
            SmartMarkerOptions smOptions = new SmartMarkerOptions
            {
                DetailSheetNewName = "Detail"
            };

            // 5️⃣ Process the markers
            workbook.Worksheets[0].SmartMarkerProcessor.Process(employees, smOptions);

            // 6️⃣ Save workbook as xlsx file
            string outPath = "./output/detail.xlsx";
            workbook.Save(outPath, SaveFormat.Xlsx);
            Console.WriteLine($"Workbook saved to {outPath}");
        }
    }
}
```

**Ожидаемый результат**

- `output/detail.xlsx` содержит:
  - **Sheet1** – оригинальный шаблон с заголовком “Employee Report”.
  - **Detail** – первый лист‑деталь с записью Alice.
  - **Detail_1** – второй лист‑деталь с записью Bob.
  - **Detail_2** – третий лист‑деталь с записью Carol.

Откройте файл в Excel, и вы увидите каждого сотрудника на отдельном листе, что доказывает, что мы успешно **создали несколько листов‑деталей** и **сохранили рабочую книгу в файл xlsx**.

## Часто задаваемые вопросы и обработка граничных случаев

| Question | Answer |
|----------|--------|
| *Что если мне нужно пользовательское имя для каждого листа‑детали?* | Установите `DetailSheetNewName = "Employee_"` и включите столбец с именем `SheetName` в источник данных. Процессор добавит значение `SheetName` к базовому имени. |
| *Можно ли оставить оригинальный лист как сводку всех деталей?* | Да. Главный лист остаётся нетронутым; вы можете добавить формулы, ссылающиеся на сгенерированные листы‑детали. |
| *Что происходит, если источник данных пуст?* | Листы‑детали не создаются, но рабочая книга всё равно сохраняется. При необходимости особой обработки проверьте `employees.Rows.Count` перед обработкой. |
| *Можно ли использовать существующий файл шаблона?* | Замените `new Workbook()` на `new Workbook("Template.xlsx")`. Вся логика Smart Marker будет работать одинаково. |

## Заключение

Теперь вы знаете **как создать рабочую книгу Excel программно**, как **создать несколько листов‑деталей** с помощью Smart Markers и как **сохранить рабочую книгу в файл xlsx** с помощью Aspose.Cells. Полный пример можно адаптировать для счетов‑фактур, отчётов или любой ситуации, где требуется вывод Excel в формате мастер‑деталь.

### Следующие шаги

- Изучите другие возможности Smart Marker, такие как **group markers** и **conditional formatting**.  
- Замените `DataTable` реальным запросом к базе данных для генерации масштабных отчётов.  
- Используйте `Workbook.Save("output.pdf", SaveFormat.Pdf)`, чтобы экспортировать те же данные в PDF для распространения.

Не стесняйтесь экспериментировать с различными схемами именования, стилями или дополнительными листами — ваши новые навыки программного создания Excel готовы к использованию в продакшене. Happy coding!

## Что стоит изучить дальше?

Следующие руководства охватывают тесно связанные темы, которые развивают техники, продемонстрированные в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, помогающими освоить дополнительные возможности API и исследовать альтернативные подходы в ваших проектах.

- [Создать рабочую книгу Excel C# – Добавить комментарий и сохранить как XLSX](/cells/english/net/excel-comment-annotation/create-excel-workbook-c-add-comment-save-as-xlsx/)
- [Создать новую рабочую книгу в C# – Добавить формулу и сохранить файл Excel](/cells/english/net/excel-workbook/create-new-workbook-in-c-add-formula-and-save-excel-file/)
- [Создать рабочую книгу Excel C# – Вставить JSON и сохранить как XLSX](/cells/english/net/excel-data-import-export/create-excel-workbook-c-insert-json-and-save-as-xlsx/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}