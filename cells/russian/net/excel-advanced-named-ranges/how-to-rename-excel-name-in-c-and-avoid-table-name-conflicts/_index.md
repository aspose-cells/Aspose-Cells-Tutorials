---
category: general
date: 2026-11-25
description: Как переименовать имя Excel в C#, учитывая конфликты имён таблиц. Узнайте,
  как создать рабочую книгу Excel на C# и эффективно решить проблемы с именами.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to rename excel name
- create excel workbook c#
- excel table name conflict
language: ru
lastmod: 2026-11-25
og_description: Как переименовать имя Excel в C# и решить конфликты имен таблиц Excel.
  Следуйте этому пошаговому руководству, чтобы создать рабочую книгу Excel на C# и
  безопасно управлять именами.
og_image_alt: Screenshot of C# code that renames an Excel name without conflict
og_title: Как переименовать имя Excel в C# – избежать конфликтов имён таблиц
schemas:
- author: Aspose
  dateModified: '2026-11-25'
  description: How to rename Excel name in C# while handling table name conflicts.
    Learn to create Excel workbook C# and resolve naming issues efficiently.
  headline: How to rename Excel name in C# and avoid table name conflicts
  type: TechArticle
- description: How to rename Excel name in C# while handling table name conflicts.
    Learn to create Excel workbook C# and resolve naming issues efficiently.
  name: How to rename Excel name in C# and avoid table name conflicts
  steps:
  - name: Create Excel workbook in C# (secondary keyword)
    text: 'Start by adding the Aspose.Cells NuGet package to your project:'
  - name: Add a table and a conflicting defined name (secondary keyword)
    text: Next we add a ListObject (Excel table) and deliberately create a defined
      name that would clash.
  - name: Detect and resolve an Excel table name conflict (secondary keyword)
    text: Before renaming, scan the workbook’s `Names` collection and the worksheet’s
      `ListObjects` collection to ensure the target name is free.
  - name: Expected output and verification
    text: 'Running the program produces console output similar to:'
  - name: What the code does
    text: 1. **Creates** a new Excel workbook (`create excel workbook c#`). 2. **Adds**
      a table called *SalesTable* (demonstrating the conflict source). 3. **Attempts**
      to rename a defined name to *SalesTable*. 4. **Detects** the conflict with `IsNameConflict`.
      5. **Renames** the table first, then safely rena
  type: HowTo
tags:
- C#
- Excel
- Aspose.Cells
title: Как переименовать имя Excel в C# и избежать конфликтов имён таблиц
url: /ru/net/excel-advanced-named-ranges/how-to-rename-excel-name-in-c-and-avoid-table-name-conflicts/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как переименовать имя Excel в C# и избежать конфликтов имён таблиц

Если вам нужно **переименовать имя Excel** без возникновения ошибки, это руководство покажет точные шаги. Вы узнаете, почему имя таблицы может конфликтовать с именем уровня книги и как безопасно переименовать, когда вы **создаёте Excel‑книгу c#** программы.

Переименование имени Excel — распространённая задача при программном создании отчётов. Встроенный менеджер имён рассматривает таблицы листов (ListObjects) и определённые имена как часть одного пространства имён, поэтому конфликт возникает сразу же, как только вы пытаетесь задать определённому имени тот же идентификатор, что и у таблицы. Это руководство проведёт вас через полное решение, от создания книги до переименования с учётом конфликтов, используя Aspose.Cells для .NET.

## Как переименовать имя Excel в C# (primary keyword)

Когда вы пытаетесь установить `conflictingName.Name = "SalesTable"`, а таблица с именем **SalesTable** уже существует, Aspose.Cells генерирует исключение. Решение состоит в:

1. Обнаружить конфликт перед переименованием, **или**  
2. Сначала переименовать таблицу, затем присвоить желаемое имя определённому имени.

Ниже реализован первый подход — проверка коллекции имён книги перед применением нового имени.

### Шаг 1: Создать Excel‑книгу в C# (secondary keyword)

Начните с добавления пакета Aspose.Cells NuGet в ваш проект:

```bash
dotnet add package Aspose.Cells
```

Затем напишите базовый код, который создаёт книгу и лист:

```csharp
using System;
using Aspose.Cells;

namespace ExcelRenameDemo
{
    class Program
    {
        static void Main()
        {
            // Create a new workbook and get the first worksheet
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.Worksheets[0];
```

*Почему это важно:* Объект `Workbook` представляет весь файл Excel. По умолчанию он содержит один лист, который мы используем для дальнейших операций.

### Шаг 2: Добавить таблицу и конфликтующее определённое имя (secondary keyword)

Далее мы добавляем ListObject (таблицу Excel) и намеренно создаём определённое имя, которое будет конфликтовать.

```csharp
            // Add a table (ListObject) that occupies cells A1:C5
            ListObject salesTable = worksheet.ListObjects.Add(0, 0, 5, 3, TableStyleType.Light1);
            salesTable.Name = "SalesTable";

            // Define a workbook‑level name that initially does NOT conflict
            Name definedName = workbook.Worksheets[0].Names.Add("TempName");
```

*Объяснение:* Таблица получает имя **SalesTable**. Определённое имя `TempName` безвредно на данном этапе, но позже мы попытаемся переименовать его в **SalesTable**, что вызовет конфликт.

### Шаг 3: Обнаружить и решить конфликт имён таблицы Excel (secondary keyword)

Перед переименованием просмотрите коллекцию `Names` книги и коллекцию `ListObjects` листа, чтобы убедиться, что целевое имя свободно.

```csharp
            string desiredName = "SalesTable";

            bool conflict = IsNameConflict(workbook, worksheet, desiredName);

            if (conflict)
            {
                Console.WriteLine($"Cannot rename defined name to \"{desiredName}\" because a table with that name already exists.");
                // Optionally, rename the table first or choose a different name
                salesTable.Name = "SalesTable_Alt";
                Console.WriteLine($"Table renamed to \"{salesTable.Name}\". Now you can reuse \"{desiredName}\" for the defined name.");
                definedName.Name = desiredName; // This now succeeds
            }
            else
            {
                definedName.Name = desiredName; // Safe rename
                Console.WriteLine($"Defined name renamed to \"{desiredName}\" successfully.");
            }

            // Save the workbook to verify the result
            workbook.Save("RenameResult.xlsx");
        }

        /// <summary>
        /// Checks whether the desired name collides with any existing table or defined name.
        /// </summary>
        static bool IsNameConflict(Workbook wb, Worksheet ws, string name)
        {
            // Check table names (ListObjects)
            foreach (ListObject lo in ws.ListObjects)
            {
                if (string.Equals(lo.Name, name, StringComparison.OrdinalIgnoreCase))
                    return true;
            }

            // Check defined names at workbook level
            foreach (Name n in wb.Worksheets[0].Names)
            {
                if (string.Equals(n.Name, name, StringComparison.OrdinalIgnoreCase))
                    return true;
            }

            return false;
        }
    }
}
```

**Почему вспомогательная функция важна:**  
- `ListObject.Name` находится в том же пространстве имён, что и `Name.Name`.  
- `IsNameConflict` инкапсулирует проверку, делая код переиспользуемым каждый раз, когда нужно безопасно переименовать имя.  
- Переименовав таблицу сначала (`salesTable.Name = "SalesTable_Alt"`), вы освобождаете исходный идентификатор, позволяя определённому имени принять его без ошибки.

### Шаг 4: Ожидаемый вывод и проверка

Запуск программы выводит в консоль примерно следующее:

```
Cannot rename defined name to "SalesTable" because a table with that name already exists.
Table renamed to "SalesTable_Alt". Now you can reuse "SalesTable" for the defined name.
```

После выполнения сгенерированный файл `RenameResult.xlsx` содержит:

- Лист с таблицей под именем **SalesTable_Alt**, охватывающей диапазон A1:C5.  
- Определённое имя уровня книги **SalesTable**, указывающее на тот же диапазон (или любой другой диапазон, который вы зададите позже).

Откройте файл в Excel → Формулы → Менеджер имён, чтобы убедиться, что обе записи существуют без конфликта.

## Понимание конфликта имён таблицы Excel (secondary keyword)

Excel рассматривает **таблицы** (`ListObject`) и **именованные диапазоны** (`Name`) как элементы единой области имён. Когда вы создаёте таблицу с именем *SalesTable*, менеджер имён внутренне регистрирует *SalesTable* как определённое имя, указывающее на диапазон таблицы. Попытка добавить другое определённое имя с тем же идентификатором вызывает `ArgumentException`, который вы видели в оригинальном фрагменте.

Ключевые моменты, которые следует помнить:

- **Область видимости**: Имена таблиц действуют на уровне всей книги; их нельзя дублировать даже на разных листах.  
- **Регистронезависимость**: `salesTable` и `SalesTable` считаются одинаковыми.  
- **Порядок переименования имеет значение**: Сначала переименуйте таблицу (или удалите её), чтобы освободить пространство имён для определённого имени.

## Реализация переименования с обработкой исключений (primary keyword)

Если вы предпочитаете полагаться на обработку исключений вместо предварительной проверки, оберните переименование в блок `try/catch`, как показано в оригинальном коде. Однако проактивное обнаружение конфликтов (как продемонстрировано) более эффективно, поскольку избегает затрат на выброс и перехват исключения.

```csharp
try
{
    definedName.Name = "SalesTable"; // May throw if conflict exists
    Console.WriteLine("Rename succeeded.");
}
catch (Exception ex)
{
    Console.WriteLine($"Rename blocked: {ex.Message}");
    // Resolve conflict here, e.g., rename the table first
}
```

**Рекомендация:** Используйте метод `IsNameConflict` перед попыткой переименования. Этот подход следует принципу «fail‑fast» и упрощает поддержку кода.

## Полный рабочий пример (primary keyword)

Ниже представлена полная программа, которую можно скопировать и вставить в новый консольный проект .NET. Она демонстрирует **как переименовать имя Excel** безопасно, обрабатывает **конфликт имён таблицы Excel** и показывает, как **создавать Excel‑книгу c#** с нуля.

```csharp
using System;
using Aspose.Cells;

namespace ExcelRenameDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create workbook and worksheet
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.Worksheets[0];

            // 2️⃣ Add a table named "SalesTable"
            ListObject salesTable = worksheet.ListObjects.Add(0, 0, 5, 3, TableStyleType.Light1);
            salesTable.Name = "SalesTable";

            // 3️⃣ Add a temporary defined name
            Name definedName = workbook.Worksheets[0].Names.Add("TempName");

            // 4️⃣ Desired rename target
            string desiredName = "SalesTable";

            // 5️⃣ Check for conflict
            if (IsNameConflict(workbook, worksheet, desiredName))
            {
                Console.WriteLine($"Conflict detected: a table named \"{desiredName}\" already exists.");

                // Resolve by renaming the table first
                salesTable.Name = $"{desiredName}_Alt";
                Console.WriteLine($"Table renamed to \"{salesTable.Name}\".");

                // Now rename the defined name
                definedName.Name = desiredName;
                Console.WriteLine($"Defined name renamed to \"{desiredName}\".");
            }
            else
            {
                definedName.Name = desiredName;
                Console.WriteLine($"Defined name renamed to \"{desiredName}\" without conflict.");
            }

            // 6️⃣ Save the workbook
            workbook.Save("RenameResult.xlsx");
            Console.WriteLine("Workbook saved as RenameResult.xlsx");
        }

        /// <summary>
        /// Determines whether the target name collides with any existing table or defined name.
        /// </summary>
        static bool IsNameConflict(Workbook wb, Worksheet ws, string name)
        {
            foreach (ListObject lo in ws.ListObjects)
                if (string.Equals(lo.Name, name, StringComparison.OrdinalIgnoreCase))
                    return true;

            foreach (Name n in wb.Worksheets[0].Names)
                if (string.Equals(n.Name, name, StringComparison.OrdinalIgnoreCase))
                    return true;

            return false;
        }
    }
}
```

### Что делает код

1. **Создаёт** новую Excel‑книгу (`create excel workbook c#`).  
2. **Добавляет** таблицу под именем *SalesTable* (демонстрируя источник конфликта).  
3. **Пытается** переименовать определённое имя в *SalesTable*.  
4. **Обнаруживает** конфликт с помощью `IsNameConflict`.  
5. **Сначала переименовывает** таблицу, затем безопасно переименовывает определённое имя.

## Что изучать дальше?

Следующие руководства охватывают тесно связанные темы, расширяющие техники, продемонстрированные в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы в ваших проектах.

- [Assign name to Excel table and avoid naming conflicts](/cells/english/net/excel-advanced-named-ranges/assign-name-to-excel-table-and-avoid-naming-conflicts/)
- [How to Rename Table in Excel with C# – Step‑by‑Step Guide](/cells/english/net/tables-and-lists/how-to-rename-table-in-excel-with-c-step-by-step-guide/)
- [Create Excel Workbook in C# – Add Named Range & Set Table Name](/cells/english/net/excel-advanced-named-ranges/create-excel-workbook-in-c-add-named-range-set-table-name/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}