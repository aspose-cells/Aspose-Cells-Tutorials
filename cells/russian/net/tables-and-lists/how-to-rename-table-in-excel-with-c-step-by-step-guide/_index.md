---
category: general
date: 2026-08-11
description: Как переименовать таблицу в Excel с помощью C# и Aspose.Cells. Узнайте,
  как создать рабочую книгу Excel, добавить именованный диапазон и избежать конфликтов
  при переименовании.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to rename table
- create excel workbook
- add named range
- how to add range
- rename excel table
language: ru
lastmod: 2026-08-11
og_description: Как переименовать таблицу в Excel с помощью C# и Aspose.Cells. Это
  руководство покажет, как создать рабочую книгу Excel, добавить именованный диапазон
  и безопасно переименовать таблицу Excel.
og_image_alt: Screenshot of C# code that renames an Excel table
og_title: Как переименовать таблицу в Excel с помощью C# — полный учебник по программированию
schemas:
- author: Aspose
  dateModified: '2026-08-11'
  description: How to rename table in Excel with C# using Aspose.Cells. Learn to create
    Excel workbook, add named range, and avoid rename conflicts.
  headline: How to rename table in Excel with C# – step‑by‑step guide
  type: TechArticle
- description: How to rename table in Excel with C# using Aspose.Cells. Learn to create
    Excel workbook, add named range, and avoid rename conflicts.
  name: How to rename table in Excel with C# – step‑by‑step guide
  steps:
  - name: '**Create Excel workbook** – instantiate a `Workbook` and add some sample
      data.'
    text: '**Create Excel workbook** – instantiate a `Workbook` and add some sample
      data.'
  - name: '**Add a named range** – use `Worksheets.Names.Add` to create a range called
      `MyRange`.'
    text: '**Add a named range** – use `Worksheets.Names.Add` to create a range called
      `MyRange`.'
  - name: '**Create an Excel table (ListObject)** – convert the data into a table
      so we have something to rename.'
    text: '**Create an Excel table (ListObject)** – convert the data into a table
      so we have something to rename.'
  - name: '**Rename the table** – attempt to set the table’s `Name` property to the
      same identifier as the named range.'
    text: '**Rename the table** – attempt to set the table’s `Name` property to the
      same identifier as the named range.'
  - name: '**Handle name conflicts** – catch the exception, explain why it occurs,
      and show a safe rename strategy.'
    text: '**Handle name conflicts** – catch the exception, explain why it occurs,
      and show a safe rename strategy.'
  type: HowTo
tags:
- Excel
- C#
- Aspose.Cells
- Automation
title: Как переименовать таблицу в Excel с помощью C# – пошаговое руководство
url: /ru/net/tables-and-lists/how-to-rename-table-in-excel-with-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как переименовать таблицу в Excel с помощью C# – пошаговое руководство

Если вам нужно **как переименовать таблицу** в файле Excel программно, это руководство покажет точный подход с использованием Aspose.Cells для .NET. Вы увидите, как **создать Excel workbook**, определить **named range** и переименовать существующую таблицу Excel без возникновения конфликта имен.

Решение работает для любого проекта .NET, нацеленного на .NET 6 или новее, и требует только пакета Aspose.Cells NuGet. К концу руководства вы сможете безопасно переименовать таблицу Excel и понять, почему конфликт может возникнуть, когда имя таблицы совпадает с определённым диапазоном.

## Требования

- .NET 6 SDK или новее, установленный  
- Visual Studio 2022 (или любая IDE для C#)  
- Пакет Aspose.Cells for .NET (`dotnet add package Aspose.Cells`)  

Дополнительные сборки Excel interop не требуются, поскольку Aspose.Cells работает полностью в памяти.

## Обзор решения

1. **Создать Excel workbook** – создать объект `Workbook` и добавить примерные данные.  
2. **Добавить named range** – использовать `Worksheets.Names.Add` для создания диапазона с именем `MyRange`.  
3. **Создать таблицу Excel (ListObject)** – преобразовать данные в таблицу, чтобы её можно было переименовать.  
4. **Переименовать таблицу** – попытаться установить свойство `Name` таблицы в то же имя, что и у named range.  
5. **Обработать конфликты имён** – перехватить исключение, объяснить его причину и показать безопасную стратегию переименования.

Каждый шаг подробно объяснён ниже.

## Шаг 1: Как создать Excel workbook и заполнить данными

Создание workbook — фундамент для любой автоматизации Excel. Класс `Workbook` представляет весь файл в памяти.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new workbook
        Workbook workbook = new Workbook();

        // Access the first worksheet (index 0)
        Worksheet sheet = workbook.Worksheets[0];

        // Fill some sample data in cells A1:C4
        sheet.Cells["A1"].PutValue("ID");
        sheet.Cells["B1"].PutValue("Name");
        sheet.Cells["C1"].PutValue("Score");

        sheet.Cells["A2"].PutValue(1);
        sheet.Cells["B2"].PutValue("Alice");
        sheet.Cells["C2"].PutValue(85);

        sheet.Cells["A3"].PutValue(2);
        sheet.Cells["B3"].PutValue("Bob");
        sheet.Cells["C3"].PutValue(92);

        sheet.Cells["A4"].PutValue(3);
        sheet.Cells["B4"].PutValue("Carol");
        sheet.Cells["C4"].PutValue(78);
```

**Почему это важно:** Workbook должен содержать данные, прежде чем вы сможете создать таблицу. Aspose.Cells хранит данные в нулевой‑базовой коллекции, поэтому `Worksheets[0]` всегда указывает на первый лист.

## Шаг 2: Как добавить named range на лист

**named range** позволяет обращаться к конкретной ячейке или диапазону по удобному идентификатору. Добавление диапазона простое:

```csharp
        // 2️⃣ Define a named range called "MyRange" that points to cell A1
        // The range string follows Excel notation: SheetName!$A$1
        workbook.Worksheets.Names.Add("MyRange", "Sheet1!$A$1");
```

**Почему это важно:** Named ranges хранятся в глобальной коллекции имён workbook. Если позже таблица получит то же имя, Aspose.Cells выбросит `CellException`, потому что Excel не допускает дублирование имён.

## Шаг 3: Как добавить таблицу Excel (ListObject)

Таблица обеспечивает структурированную работу с данными, фильтрацию и стилизацию. В Aspose.Cells она называется **ListObject**.

```csharp
        // 3️⃣ Convert the data range A1:C4 into an Excel table
        // The range string includes the header row.
        int firstRow = 0;   // zero‑based index for row 1
        int firstCol = 0;   // column A
        int totalRows = 4;  // rows 1‑4
        int totalCols = 3;  // columns A‑C

        // Create the ListObject (table) and give it an initial name
        ListObject table = sheet.ListObjects[sheet.ListObjects.Add(firstRow, firstCol, totalRows, totalCols, true)];
        table.Name = "InitialTable";
```

**Почему это важно:** Таблица теперь существует с именем `InitialTable`. Переименование её демонстрирует процесс **как переименовать таблицу**.

## Шаг 4: Как переименовать таблицу Excel и обработать конфликты

Попытка переименовать таблицу в `MyRange` конфликтует с ранее созданным named range. Ниже показан правильный шаблон для обнаружения и разрешения конфликта.

```csharp
        // 4️⃣ Try to rename the table to "MyRange"
        try
        {
            table.Name = "MyRange";   // This will raise an exception
            Console.WriteLine("Table renamed successfully.");
        }
        catch (Exception ex)
        {
            // 5️⃣ Handle the name conflict gracefully
            Console.WriteLine("Name conflict detected: " + ex.Message);

            // Resolve by choosing a unique name
            string safeName = GetUniqueTableName(workbook, "MyRange");
            table.Name = safeName;
            Console.WriteLine($"Table renamed to safe identifier: {safeName}");
        }

        // Save the workbook to verify the result
        workbook.Save("RenamedTable.xlsx");
    }

    /// <summary>
    /// Generates a unique table name that does not exist as a named range or another table.
    /// </summary>
    static string GetUniqueTableName(Workbook wb, string baseName)
    {
        int counter = 1;
        string candidate = baseName + "_" + counter;

        // Check against workbook names and existing table names
        while (NameExists(wb, candidate))
        {
            counter++;
            candidate = baseName + "_" + counter;
        }
        return candidate;
    }

    /// <summary>
    /// Returns true if the identifier is already used as a named range or table name.
    /// </summary>
    static bool NameExists(Workbook wb, string name)
    {
        // Check named ranges
        foreach (Name n in wb.Worksheets.Names)
        {
            if (string.Equals(n.TextToRefer, name, StringComparison.OrdinalIgnoreCase))
                return true;
        }

        // Check existing tables
        foreach (Worksheet ws in wb.Worksheets)
        {
            foreach (ListObject lo in ws.ListObjects)
            {
                if (string.Equals(lo.Name, name, StringComparison.OrdinalIgnoreCase))
                    return true;
            }
        }
        return false;
    }
}
```

### Что делает код

| Шаг | Действие | Причина |
|------|----------|----------|
| **Попытка переименования** | `table.Name = "MyRange"` | Демонстрирует сценарий конфликта. |
| **Перехват исключения** | Выводит сообщение о конфликте. | Даёт мгновенную обратную связь о проблеме. |
| **Генерация безопасного имени** | `GetUniqueTableName` добавляет числовой суффикс, пока имя не будет свободным. | Гарантирует, что новое имя таблицы **не** будет конфликтовать с существующим named range или другой таблицей. |
| **Сохранить workbook** | `workbook.Save("RenamedTable.xlsx")` | Сохраняет изменения, чтобы вы могли открыть файл в Excel и проверить результат. |

**Ожидаемый вывод** при запуске программы:

```
Name conflict detected: A name with the same text already exists.
Table renamed to safe identifier: MyRange_1
```

Открытие `RenamedTable.xlsx` показывает таблицу с именем `MyRange_1` и отдельный named range `MyRange`, указывающий на ячейку A1.

## Почему возникает конфликт и лучшие практики переименования таблицы Excel

- Excel хранит **named ranges** и **имена таблиц** в одном пространстве имён.  
- При попытке присвоить таблице имя, которое уже существует как диапазон, Aspose.Cells бросает `CellException`.  
- Рекомендуемый подход — **сначала проверять существующие имена** (как показано в `NameExists`) или использовать соглашение об именовании, гарантирующее уникальность (например, префикс `tbl_` для таблиц).  

Применение этого шаблона предотвращает ошибки во время выполнения и делает вашу автоматизацию надёжной.

## Дополнительные советы по работе с Aspose.Cells

- **Pro tip:** Используйте `Workbook.Worksheets.Names.Remove("MyRange")`, если хотите намеренно заменить диапазон именем таблицы.  
- **Осторожно с регистром:** Excel воспринимает имена без учёта регистра; вспомогательные методы используют `OrdinalIgnoreCase`, чтобы имитировать поведение Excel.  
- **Производительность:** При обработке большого количества листов кэшируйте коллекцию имён вместо повторных итераций.

## Полный пример в одном блоке

Ниже приведена полная программа, которую можно скопировать и вставить в консольный проект. Она включает все шаги от создания workbook до безопасного переименования таблицы.

```csharp
using System;
using Aspose.Cells;

class RenameTableDemo
{
    static void Main()
    {
        // Create workbook and populate data
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        sheet.Cells["A1"].PutValue("ID");
        sheet.Cells["B1"].PutValue("Name");
        sheet.Cells["C1"].PutValue("Score");

        sheet.Cells["A2"].PutValue(1);
        sheet.Cells["B2"].PutValue("Alice");
        sheet.Cells["C2"].PutValue(85);

        sheet.Cells["A3"].PutValue(2);
        sheet.Cells["B3"].PutValue("Bob");
        sheet.Cells["C3"].PutValue(92);

        sheet.Cells["A4"].PutValue(3);
        sheet.Cells["B4"].PutValue("Carol");
        sheet.Cells["C4"].PutValue(78);

        // Add named range "MyRange" pointing to A1
        workbook.Worksheets.Names.Add("MyRange", "Sheet1!$A$1");

        // Convert the data range into a table named "InitialTable"
        ListObject table = sheet.ListObjects[sheet.ListObjects.Add(0, 0, 4, 3, true)];
        table.Name = "InitialTable";

        // Attempt to rename the table to "MyRange" – this will conflict
        try
        {
            table.Name = "MyRange";
            Console


## Что следует изучить дальше?


Следующие руководства охватывают близко связанные темы, расширяющие техники, продемонстрированные в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы в собственных проектах.

- [How to Create Workbook Scoped Named Ranges in Excel Using Aspose.Cells .NET](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)
- [How to Implement Named Range Formulas in .NET using Aspose.Cells for Excel Automation](/cells/english/net/formulas-functions/implement-named-range-formulas-net-aspose-cells/)
- [How to Add Slicers to Excel Tables Using Aspose.Cells for .NET: A Comprehensive Guide](/cells/english/net/advanced-features/add-slicers-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}