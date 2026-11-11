---
category: general
date: 2026-10-26
description: Узнайте, как импортировать DataTable в лист Excel с помощью C# и Aspose.Cells,
  сохраняя стили и заголовки всего за несколько строк кода.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to import datatable
- ImportTableOptions
- ImportDataTableStyle
- Aspose.Cells
- Excel worksheet import
- C# DataTable import
language: ru
lastmod: 2026-10-26
og_description: как импортировать DataTable в лист Excel с помощью C# и Aspose.Cells.
  Следуйте этому полному руководству, чтобы сохранить стили, заголовки и форматирование.
og_image_alt: Screenshot of C# code that imports a DataTable into an Excel worksheet
  with Aspose.Cells
og_title: Как импортировать DataTable в лист Excel — пошаговое руководство по C#
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn how to import DataTable into an Excel worksheet with C# and Aspose.Cells,
    preserving styles and headers in just a few lines of code.
  headline: How to import DataTable into an Excel worksheet using C#
  type: TechArticle
tags:
- C#
- Aspose.Cells
- Excel
- DataTable
title: Как импортировать DataTable в лист Excel с помощью C#
url: /ru/net/excel-data-import-export/how-to-import-datatable-into-an-excel-worksheet-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как импортировать DataTable в лист Excel с помощью C#

Если вам нужно **как импортировать datatable** в лист Excel, это руководство покажет точные шаги на C#. Независимо от того, создаёте ли вы движок отчётности или экспортируете данные из сетки, вы увидите, как сохранить заголовки столбцов и стили ячеек с помощью Aspose.Cells. Решение работает с .NET 6+ и требует всего несколько строк кода.

Импорт DataTable — распространённая задача при работе с электронными таблицами, но разработчики часто забывают включить передачу стилей или правильно задать флаг заголовков. В этом уроке вы узнаете, как настроить **ImportTableOptions**, включить **ImportDataTableStyle** и безопасно вызвать `ImportDataTable`. К концу вы получите готовый к использованию метод, который можно вставить в любой проект C#.

## Требования

Прежде чем начать, убедитесь, что у вас есть:

* .NET 6 SDK или более поздняя версия.
* Лицензированная копия **Aspose.Cells for .NET** (бесплатная пробная версия подходит для тестирования).
* Базовое знакомство с `DataTable` и концепциями Excel.
* IDE, например Visual Studio 2022 (подойдёт любой редактор, поддерживающий C#).

Дополнительные пакеты NuGet не требуются, кроме `Aspose.Cells`.

## Шаг 1: Получить исходные данные в DataTable

Первое, что нужно сделать, отвечая на вопрос **как импортировать datatable**, — подготовить данные. В большинстве реальных сценариев `DataTable` формируется из запроса к базе данных, парсера CSV или коллекции в памяти. Ниже минимальный пример, создающий таблицу с несколькими строками:

```csharp
using System;
using System.Data;

public static DataTable GetSampleData()
{
    var table = new DataTable("Employees");
    table.Columns.Add("Id", typeof(int));
    table.Columns.Add("Name", typeof(string));
    table.Columns.Add("Department", typeof(string));

    table.Rows.Add(1, "Alice Johnson", "Finance");
    table.Rows.Add(2, "Bob Smith", "Engineering");
    table.Rows.Add(3, "Carol White", "Marketing");

    return table;
}
```

*Почему это важно*: Создавая `DataTable` заранее, вы контролируете порядок столбцов, типы данных и имена заголовков — всё это сохраняется при последующем импорте таблицы в лист Excel.

## Шаг 2: Создать `ImportTableOptions` и включить импорт стилей

Отвечая на **как импортировать datatable**, следующий вопрос — нужны ли вам визуальные стили (шрифты, цвета, границы), которые уже заданы в исходном `DataTable`. Aspose.Cells предоставляет класс `ImportTableOptions` для тонкой настройки. Установка `ImportDataTableStyle = true` копирует информацию о стиле в целевой лист.

```csharp
using Aspose.Cells;

public static ImportTableOptions CreateImportOptions()
{
    var options = new ImportTableOptions
    {
        // Preserve the style of the DataTable cells (font, background, borders)
        ImportDataTableStyle = true
    };
    return options;
}
```

*Почему это важно*: Если не включить `ImportDataTableStyle`, импортированные ячейки будут использовать стиль листа по умолчанию, и любые пользовательские форматы, применённые к `DataTable`, будут потеряны. Этот флаг необходим для профессионального экспорта.

## Шаг 3: Импортировать DataTable в лист, включая заголовки

Теперь у вас есть всё необходимое, чтобы ответить на вопрос **как импортировать datatable** в файл Excel. Вы создаёте книгу, выбираете лист и вызываете `ImportDataTable`. Второй аргумент метода (`true`) указывает Aspose.Cells записать заголовки столбцов в первую строку.

```csharp
using Aspose.Cells;
using System.IO;

public static void ExportDataTableToExcel(string filePath)
{
    // 1️⃣ Retrieve the source data
    DataTable dataTable = GetSampleData();

    // 2️⃣ Prepare import options (style preservation)
    ImportTableOptions importOptions = CreateImportOptions();

    // 3️⃣ Create a new workbook and select the first worksheet
    var workbook = new Workbook();
    Worksheet ws = workbook.Worksheets[0];
    ws.Name = "Employees";

    // 4️⃣ Import the DataTable, include headers, and apply options
    ws.Cells.ImportDataTable(dataTable, true, importOptions);

    // 5️⃣ Save the workbook to the specified path
    workbook.Save(filePath, SaveFormat.Xlsx);
}
```

Вызов `ExportDataTableToExcel("Employees.xlsx")` создаёт файл `Employees.xlsx`, где первая строка содержит **Id**, **Name** и **Department**, а каждая ячейка сохраняет стиль, определённый в оригинальном `DataTable`.

### Полный рабочий пример

Ниже представлена полностью самодостаточная консольная программа, демонстрирующая **как импортировать datatable** и сохраняющая результат в текущий каталог. Скопируйте её в новый консольный проект и запустите.

```csharp
using System;
using System.Data;
using Aspose.Cells;

namespace DataTableImportDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            string outputPath = Path.Combine(Directory.GetCurrentDirectory(), "Employees.xlsx");
            ExportDataTableToExcel(outputPath);
            Console.WriteLine($"Excel file created at: {outputPath}");
        }

        // Retrieves sample data
        private static DataTable GetSampleData()
        {
            var table = new DataTable("Employees");
            table.Columns.Add("Id", typeof(int));
            table.Columns.Add("Name", typeof(string));
            table.Columns.Add("Department", typeof(string));

            table.Rows.Add(1, "Alice Johnson", "Finance");
            table.Rows.Add(2, "Bob Smith", "Engineering");
            table.Rows.Add(3, "Carol White", "Marketing");
            return table;
        }

        // Configures import options to keep styles
        private static ImportTableOptions CreateImportOptions()
        {
            return new ImportTableOptions
            {
                ImportDataTableStyle = true
            };
        }

        // Performs the import and saves the workbook
        private static void ExportDataTableToExcel(string filePath)
        {
            DataTable dataTable = GetSampleData();
            ImportTableOptions importOptions = CreateImportOptions();

            var workbook = new Workbook();
            Worksheet ws = workbook.Worksheets[0];
            ws.Name = "Employees";

            // Here we answer the core question: how to import datatable
            ws.Cells.ImportDataTable(dataTable, true, importOptions);
            workbook.Save(filePath, SaveFormat.Xlsx);
        }
    }
}
```

**Ожидаемый результат**  
При открытии `Employees.xlsx` вы увидите:

| Id | Name          | Department |
|----|---------------|------------|
| 1  | Alice Johnson | Finance    |
| 2  | Bob Smith     | Engineering|
| 3  | Carol White   | Marketing  |

Все ячейки сохраняют стиль DataTable по умолчанию (шрифт, выравнивание). Если вы применяли пользовательские стили к `DataTable` перед импортом, эти стили появятся в листе идентично, потому что `ImportDataTableStyle` установлен в `true`.

## Распространённые ошибки и рекомендации по лучшим практикам

| Проблема | Почему происходит | Как избежать |
|----------|-------------------|--------------|
| **Отсутствуют заголовки** | Передаётся `false` во втором аргументе `ImportDataTable`, поэтому имена столбцов пропускаются. | Всегда используйте `true`, когда нужны заголовки, либо запишите их вручную перед импортом. |
| **Стиль не перенесён** | Забыт флаг `ImportDataTableStyle`. | Установите `ImportDataTableStyle = true` в `ImportTableOptions`. |
| **Большие таблицы тормозят** | Импорт миллионов строк без разбиения. | Импортируйте пакетами или используйте перегрузку `ImportDataTable` с параметром `startRow` для потоковой загрузки. |
| **Неправильная ссылка на лист** | Обращение к `workbook.Worksheets[1]`, когда существует только один лист. | Используйте `workbook.Worksheets[0]` или создайте новый лист через `workbook.Worksheets.Add()`. |
| **Истёк срок лицензии** | Пробная версия Aspose.Cells выводит водяной знак после 30 дней. | Примените действующую лицензию: `License license = new License(); license.SetLicense("Aspose.Cells.lic");`. |

**Совет профессионала**: Если после импорта нужно применить пользовательскую тему, вызовите `ws.Cells.ApplyStyle(style)`, где `style` — объект `Style`, настроенный один раз и переиспользуемый для всех строк.

## Расширение решения

Теперь, когда вы знаете **как импортировать datatable**, можете исследовать связанные сценарии:

* **Импорт нескольких таблиц** – повторите импорт на разных листах.
* **Условное форматирование** – после импорта добавьте правила через `ws.Cells.ApplyConditionalFormatting`.
* **Экспорт в CSV** – используйте `workbook.Save("file.csv", SaveFormat.Csv)`, если нужен простой текстовый формат.
* **Обратный импорт в DataTable** – примените `ws.Cells.ExportDataTable` для проверки целостности при обратном преобразовании.

Все эти расширения опираются на основной шаблон, продемонстрированный выше: получить данные, настроить параметры импорта и вызвать один метод Aspose.Cells.

## Заключение

Теперь у вас есть полноценный, готовый к продакшну ответ на вопрос **как импортировать datatable** в лист Excel с помощью C#. В руководстве рассмотрены получение исходных данных, настройка `ImportTableOptions` с `ImportDataTableStyle` и выполнение импорта через `ImportDataTable`. Следуя приведённому примеру, вы автоматически сохраняете заголовки и стили, а также можете адаптировать шаблон под большие наборы данных, несколько листов или дополнительное форматирование.

Готовы автоматизировать процесс создания отчётов? Попробуйте заменить пример `DataTable` реальным запросом к базе, поэкспериментируйте с пользовательскими стилями ячеек и интегрируйте метод в существующий слой сервисов. Приятного кодинга!

## Что изучать дальше?

Следующие учебники охватывают тесно связанные темы, построенные на техниках, продемонстрированных в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы в собственных проектах.

- [How to Import Arrays into Excel Using Aspose.Cells for .NET&#58; A Step-by-Step Guide](/cells/english/net/import-export/import-arrays-excel-aspose-cells-net/)
- [How to Import XML Data into Excel with Aspose.Cells for .NET&#58; A Step-by-Step Guide](/cells/english/net/import-export/import-xml-data-net-aspose-cells-guide/)
- [How to Import HTML-Formatted DataTables into Excel Using Aspose.Cells for .NET](/cells/english/net/import-export/aspose-cells-net-data-table-import-html-formatting/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}