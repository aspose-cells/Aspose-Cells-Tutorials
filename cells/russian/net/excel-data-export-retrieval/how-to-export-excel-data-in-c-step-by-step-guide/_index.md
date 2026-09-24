---
category: general
date: 2026-03-21
description: Как экспортировать данные Excel с именами столбцов, сохранить числовой
  формат и читать определённые строки с помощью Aspose.Cells в C#. Узнайте, как эффективно
  читать лист Excel и экспортировать выбранные строки.
draft: false
keywords:
- how to export excel
- preserve number format
- export with column names
- read excel worksheet
- export specific rows
language: ru
og_description: Как экспортировать данные Excel с именами столбцов, сохранить числовой
  формат и читать определённые строки с помощью Aspose.Cells. Полный, готовый к запуску
  пример для разработчиков C#.
og_title: Как экспортировать данные Excel в C# – Полное руководство по программированию
tags:
- C#
- Aspose.Cells
- Excel
- DataTable
title: Как экспортировать данные Excel в C# – пошаговое руководство
url: /ru/net/excel-data-export-retrieval/how-to-export-excel-data-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как экспортировать данные Excel в C# – Полное руководство по программированию

Когда‑нибудь задумывались **как экспортировать excel** данные без потери исходного форматирования? Возможно, вы пробовали быстро скопировать‑вставить и получили даты в виде «44728» или пропавшие заголовки столбцов. Это раздражает, верно? В этом руководстве вы увидите чистый, сквозной способ чтения листа Excel, сохранения числового формата, экспорта с именами столбцов и даже выбора только нужных строк.

Мы будем использовать библиотеку Aspose.Cells, потому что она предоставляет тонкий контроль над параметрами экспорта. К концу этого руководства у вас будет переиспользуемый фрагмент кода, который можно вставить в любой проект .NET, и вы поймёте, почему каждый параметр важен. Никакой внешней документации не требуется — всё, что нужно, находится здесь.

---

## Что вы узнаете

- **Чтение листа Excel** в память с помощью Aspose.Cells.
- **Экспорт конкретных строк** (например, строки 0‑49) с сохранением имён столбцов.
- **Сохранение числового формата**, чтобы валюты, даты и проценты оставались неизменными.
- Как **экспортировать с именами столбцов** и включать комментарии ячеек, если они нужны.
- Полный, готовый к запуску пример на C# плюс советы по типичным подводным камням.

### Предварительные требования

- .NET 6.0 или новее (код также работает с .NET Framework 4.6+).
- Aspose.Cells for .NET, установленный через NuGet (`Install-Package Aspose.Cells`).
- Файл Excel (`input.xlsx`), размещённый в папке, к которой вы можете обратиться.

> **Pro tip:** Если вы работаете в CI‑конвейере, рассмотрите возможность получения пакета NuGet из приватного фида, чтобы избежать неожиданностей с лицензией.

---

## Шаг 1 – Установите Aspose.Cells и добавьте пространства имён

Сначала убедитесь, что пакет Aspose.Cells добавлен в ваш проект. Откройте консоль диспетчера пакетов и выполните:

```powershell
Install-Package Aspose.Cells
```

Затем добавьте необходимые директивы `using` в начало вашего C#‑файла:

```csharp
using Aspose.Cells;
using System.Data;
using System;
```

Эти импорты дают вам доступ к `Workbook`, `Worksheet`, `ExportTableOptions` и `DataTable` — основным элементам для **чтения листа Excel** и экспорта данных.

---

## Шаг 2 – Загрузите книгу (прочитайте файл Excel)

Теперь мы действительно **читаем лист Excel**. Конструктор `Workbook` принимает путь к файлу, а Aspose.Cells обрабатывает как форматы `.xlsx`, так и более старый `.xls`.

```csharp
// Step 2: Load the workbook containing the data
string filePath = @"YOUR_DIRECTORY\input.xlsx";
Workbook workbook = new Workbook(filePath);
```

> **Почему это важно:** Загрузка книги один раз и повторное использование того же объекта `Worksheet` гораздо эффективнее, чем открывать файл каждый раз, особенно для больших таблиц.

---

## Шаг 3 – Настройте параметры экспорта (сохранение числового формата и имён столбцов)

Здесь мы указываем Aspose.Cells *как* экспортировать. Класс `ExportTableOptions` позволяет точно настроить вывод. Мы включим три флага:

1. `ExportAsString = true` – заставляет каждую ячейку стать строкой, что гарантирует сохранение визуального представления чисел.
2. `IncludeCellComments = true` – копирует любые комментарии, прикреплённые к ячейкам (удобно для документации).
3. `PreserveNumberFormat = true` – сохраняет оригинальный числовой формат (символы валют, шаблоны дат и т.д.).

```csharp
// Step 3: Configure export options to control how the table is exported
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true,          // Export all values as strings
    IncludeCellComments = true,     // Preserve any cell comments
    PreserveNumberFormat = true     // Keep the original number formatting
};
```

> **Крайний случай:** Если установить `ExportAsString` в `false`, но всё равно захотеть сохранить числовые форматы, вы можете получить «сырые» числовые значения (например, 44728 для даты). Оставив оба флага включёнными, вы избегаете такого сюрприза.

---

## Шаг 4 – Получите первый лист (чтение листа Excel)

Большинство простых файлов имеют нужные данные на первом листе, поэтому мы получим его по индексу. Если нужен другой лист, замените `0` на соответствующий нулевой индекс или используйте `workbook.Worksheets["SheetName"]`.

```csharp
// Step 4: Get the first worksheet from the workbook
Worksheet firstWorksheet = workbook.Worksheets[0];
```

> **Почему это полезно:** Прямой доступ к объекту листа даёт вам полный контроль над его коллекцией `Cells`, что необходимо для **экспорта конкретных строк** позже.

---

## Шаг 5 – Экспорт диапазона ячеек (экспорт конкретных строк)

Теперь главное в руководстве: экспорт строк 0‑49 и столбцов 0‑4 (т.е. первых 50 строк и первых пяти столбцов) в `DataTable`. Мы также попросим Aspose.Cells включить имена столбцов как первую строку `DataTable`.

```csharp
// Step 5: Export a range of cells (rows 0‑49, columns 0‑4) to a DataTable using the options
DataTable exportedTable = firstWorksheet.Cells.ExportDataTable(
    startRow: 0,
    startColumn: 0,
    totalRows: 50,
    totalColumns: 5,
    includeColumnNames: true,
    exportOptions: exportOptions);
```

### Что делает этот код

- **`startRow: 0`** – начинается с самого верха листа.
- **`totalRows: 50`** – берёт первые 50 строк (т.е. **export specific rows**).
- **`totalColumns: 5`** – ограничивает экспорт первыми пятью столбцами.
- **`includeColumnNames: true`** – гарантирует, что заголовки `DataTable` совпадают с заголовками Excel, удовлетворяя требованию **export with column names**.
- **`exportOptions`** – применяет настройки из Шага 3, поэтому ваши числовые значения остаются выглядеть как “$1,234.56”, а не “1234.56”.

---

## Шаг 6 – Проверьте экспорт (как выглядит результат)

Выведем первые несколько строк в консоль, чтобы убедиться, что форматирование сохранилось.

```csharp
// Step 6: Display a few rows to verify the export
Console.WriteLine("=== Exported DataTable Preview ===");
foreach (DataRow row in exportedTable.Rows)
{
    // Join each column with a tab for readability
    Console.WriteLine(string.Join("\t", row.ItemArray));
}
```

**Ожидаемый вывод (пример):**

```
=== Exported DataTable Preview ===
Date        Description    Amount   Tax   Total
01/02/2024  Widget A       $120.00  $12  $132.00
01/03/2024  Widget B       $200.00  $20  $220.00
...
```

Обратите внимание, как даты отображаются в формате `MM/dd/yyyy`, а валюта сохраняет символ `$` — благодаря **preserve number format**.

---

## Распространённые подводные камни и как их избежать

| Проблема | Почему происходит | Решение |
|----------|-------------------|---------|
| Даты превращаются в большие числа | `ExportAsString` оставлен `false` | Оставьте `ExportAsString = true` или преобразуйте ячейки вручную |
| Отсутствуют заголовки столбцов | `includeColumnNames` установлен в `false` | Установите `true`, когда нужен **export with column names** |
| Комментарии исчезают | `IncludeCellComments` не включён | Включите `IncludeCellComments` в `ExportTableOptions` |
| Экспортируется не тот лист | Используется `Worksheets[0]` в файле с несколькими листами | Укажите имя листа: `workbook.Worksheets["Data"]` |
| Исключение «выход за пределы диапазона» | `totalRows` превышает фактическое количество строк | Используйте `Math.Min(totalRows, worksheet.Cells.MaxDataRow + 1)` |

---

## Бонус: Экспорт всего листа с сохранением форматов

Если позже понадобится экспортировать весь лист, просто замените `totalRows` и `totalColumns` на максимальные размеры листа:

```csharp
int maxRows = firstWorksheet.Cells.MaxDataRow + 1;      // +1 because rows are zero‑based
int maxCols = firstWorksheet.Cells.MaxDataColumn + 1;

DataTable fullTable = firstWorksheet.Cells.ExportDataTable(
    startRow: 0,
    startColumn: 0,
    totalRows: maxRows,
    totalColumns: maxCols,
    includeColumnNames: true,
    exportOptions: exportOptions);
```

Теперь у вас есть процедура **read excel worksheet**, работающая с любыми размерами, при этом **preserving number format** и **exporting with column names** сохраняются.

---

## Полный рабочий пример (готов к копированию)

Ниже полностью готовая программа, которую можно вставить в консольное приложение. В ней собраны все шаги, импорты и простая проверка вывода.

```csharp
using Aspose.Cells;
using System;
using System.Data;

namespace ExcelExportDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the workbook
            string filePath = @"YOUR_DIRECTORY\input.xlsx";
            Workbook workbook = new Workbook(filePath);

            // 2️⃣ Set export options (preserve number format, include comments, export as strings)
            ExportTableOptions exportOptions = new ExportTableOptions
            {
                ExportAsString = true,
                IncludeCellComments = true,
                PreserveNumberFormat = true
            };

            // 3️⃣ Grab the first worksheet (read excel worksheet)
            Worksheet sheet = workbook.Worksheets[0];

            // 4️⃣ Export rows 0‑49, columns 0‑4 (export specific rows) with column headers
            DataTable table = sheet.Cells.ExportDataTable(
                startRow: 0,
                startColumn: 0,
                totalRows: 50,
                totalColumns: 5,
                includeColumnNames: true,
                exportOptions: exportOptions);

            // 5️⃣ Show a preview
            Console.WriteLine("=== Exported DataTable Preview ===");
            foreach (DataRow row in table.Rows)
            {
                Console.WriteLine(string.Join("\t", row.ItemArray));
            }

            // Keep console open
            Console.WriteLine("\nExport complete. Press any key to exit...");
            Console.ReadKey();
        }
    }
}
```

Сохраните файл как `Program.cs`, выполните `dotnet run`, и вы увидите отформатированный предварительный просмотр в терминале.

---

## Заключение

Мы только что прошли через **how to export excel** данные с помощью Aspose.Cells, охватив всё от загрузки книги до сохранения числового формата, экспорта с именами столбцов и ограничения экспорта конкретными строками. Код автономный, полностью исполняемый и включает практические защиты от самых распространённых краевых случаев.

Готовы к следующему вызову? Попробуйте экспортировать напрямую в CSV, всё ещё сохраняя оригинальное числовое форматирование, или передать `DataTable` в контекст Entity Framework Core для массовой вставки в базу данных. Оба сценария опираются на те же фундаментальные принципы, которые мы рассмотрели здесь.

Если вам был полезен этот гид

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}