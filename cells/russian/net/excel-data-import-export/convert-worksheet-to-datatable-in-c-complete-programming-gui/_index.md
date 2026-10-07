---
category: general
date: 2026-06-17
description: Быстро преобразуйте лист Excel в DataTable на C#. Узнайте, как считать
  файл Excel в DataTable на C# и экспортировать Excel в DataTable на C# с реальным
  кодом.
draft: false
keywords:
- convert worksheet to datatable
- read excel file into datatable c#
- load excel workbook c#
- export excel to datatable c#
language: ru
og_description: Быстро преобразовать лист Excel в DataTable на C#. В этом руководстве
  показано, как считать файл Excel в DataTable на C# и экспортировать Excel в DataTable
  на C# с полным примером.
og_title: Преобразование рабочего листа в DataTable в C# – Полное руководство
schemas:
- author: Aspose
  dateModified: '2026-06-17'
  description: Convert worksheet to DataTable in C# quickly. Learn how to read Excel
    file into DataTable C# and export Excel to DataTable C# with real code.
  headline: Convert Worksheet to DataTable in C# – Complete Programming Guide
  type: TechArticle
tags:
- C#
- Excel
- DataTable
title: Преобразование рабочего листа в DataTable в C# — Полное руководство по программированию
url: /ru/net/excel-data-import-export/convert-worksheet-to-datatable-in-c-complete-programming-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Преобразование листа Excel в DataTable в C# – Полное руководство по программированию

Когда‑то вам нужно было **преобразовать лист в DataTable**, но вы не знали, какой API вызвать? Вы не одиноки — многие разработчики сталкиваются с этой проблемой при автоматизации отчетов или загрузке данных Excel в базу данных. Хорошая новость: всего несколькими строками C# можно считать файл Excel в `DataTable` и быть готовым к выполнению LINQ‑запросов, массовой вставки или чему‑то ещё.

В этом руководстве мы пройдемся по загрузке книги Excel, получим первый лист и **export excel to DataTable C#** — без магии, только понятный код. К концу вы получите переиспользуемый метод, который превращает любой лист в полностью типизированный `DataTable`. (И да, мы также рассмотрим сценарий «read Excel file into DataTable C#» для тех, кто предпочитает однострочное решение.)

## Prerequisites – Что понадобится

Прежде чем начать, убедитесь, что у вас есть:

- .NET 6.0 или новее (код также работает на .NET Framework 4.6+)
- Ссылка на **Aspose.Cells** (или любую другую библиотеку, предоставляющую `ExportDataTable`; в примере используется Aspose, потому что она проста)
- Файл Excel (`.xlsx`), который вы хотите обработать
- Базовая IDE для C# (Visual Studio, Rider или VS Code)

И всё — никаких дополнительных пакетов NuGet, кроме самой библиотеки для работы с Excel. Готовы? Поехали.

## Step 1: Load Excel Workbook C# – Загрузка файла в память

Первое, что нужно сделать: **load excel workbook c#**. Представьте книгу как контейнер, в котором находятся все листы, стили и метаданные. Правильное открытие гарантирует, что файл не будет заблокирован и ресурсы не утекут.

```csharp
using Aspose.Cells;
using System.Data;

// Path to your input file – change as needed
string excelPath = @"C:\Data\input.xlsx";

// Load the workbook; the constructor reads the file into memory
Workbook workbook = new Workbook(excelPath);
```

> **Почему это важно:** Класс `Workbook` абстрагирует низкоуровневый формат файла, так что вам не придётся парсить XML вручную. Он также освобождает поток при выходе объекта из области видимости, предотвращая ошибки «файл используется».

### Pro tip
Если вы работаете с огромными таблицами, рассмотрите возможность использования `LoadOptions` для **memory‑optimized loading**:

```csharp
LoadOptions options = new LoadOptions(LoadFormat.Xlsx)
{
    MemorySetting = MemorySetting.MemoryPreference
};
Workbook workbook = new Workbook(excelPath, options);
```

## Step 2: Access the Desired Worksheet – Обычно первый лист

Большинство быстрых скриптов просто берут первый лист, но вы можете выбрать любой по имени или индексу. Ниже классический подход «первый лист», который покрывает случай **convert worksheet to DataTable** для простых файлов.

```csharp
// Grab the first worksheet (index 0)
Worksheet sheet = workbook.Worksheets[0];

// Optional: verify the sheet isn’t empty
if (sheet.Cells.MaxDataRow < 0 || sheet.Cells.MaxDataColumn < 0)
{
    throw new InvalidOperationException("The worksheet appears to be empty.");
}
```

> **Edge case:** Если в книге есть скрытые листы или нужен конкретный таб, замените `0` на `workbook.Worksheets["MySheet"]`.

## Step 3: Configure Export Options – Экспорт как строки для предсказуемых типов

При преобразовании в `DataTable` часто хочется, чтобы каждая ячейка была строкой, чтобы избежать проблем с преобразованием типов позже. Именно это делает флаг **export excel to datatable c#**.

```csharp
// Set up options so every cell is treated as a string
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true   // forces string output for all cells
};
```

Почему принудительно строки? Потому что ячейки Excel могут содержать даты, числа или формулы. Экспортируя всё как текст, вы избегаете несоответствия типов столбцов при последующей загрузке данных в таблицу SQL.

## Step 4: Perform the Export – Основная логика Convert Worksheet to DataTable

Теперь происходит магия. Мы вызываем `ExportDataTable` у объекта `Worksheet`, передавая начальную строку/столбец, общее количество строк/столбцов, флаг включения заголовков столбцов и наши параметры.

```csharp
// Determine the used range
int totalRows = sheet.Cells.MaxDataRow + 1;      // +1 because rows are zero‑based
int totalCols = sheet.Cells.MaxDataColumn + 1;   // +1 for the same reason

// Export the used range to a DataTable
DataTable dataTable = sheet.ExportDataTable(
    0,                 // start row (0‑based)
    0,                 // start column (0‑based)
    totalRows,
    totalCols,
    true,              // include column names as first row
    exportOptions);
```

### Что вы получаете
`dataTable` теперь отражает лист:

| Column1 | Column2 | Column3 |
|---------|---------|---------|
| Row1‑A  | Row1‑B  | Row1‑C  |
| Row2‑A  | Row2‑B  | Row2‑C  |
| …       | …       | …       |

Все значения — строки, что делает последующую обработку предсказуемой.

## Step 5: Verify the Result – Быстрая проверка (read excel file into datatable c#)

Простой способ убедиться, что конверсия прошла успешно, — вывести первые несколько строк в консоль. Это также демонстрирует практику **read excel file into datatable c#**.

```csharp
Console.WriteLine("First 5 rows of the imported DataTable:");
for (int i = 0; i < Math.Min(5, dataTable.Rows.Count); i++)
{
    var row = dataTable.Rows[i];
    Console.WriteLine(string.Join(" | ", row.ItemArray));
}
```

Если вы видите ожидаемые значения, разделённые символом «|», вы успешно **convert worksheet to DataTable**.

## Step 6: Wrap It Up – Переиспользуемый вспомогательный метод

В большинстве проектов такая конверсия понадобится в нескольких местах, поэтому упакуем всё в один статический метод. Это делает вызов **read excel file into datatable c#** простым, как одна строка.

```csharp
public static DataTable WorksheetToDataTable(string filePath, int sheetIndex = 0, bool exportAsString = true)
{
    // Load the workbook
    Workbook wb = new Workbook(filePath);

    // Grab the requested sheet
    Worksheet ws = wb.Worksheets[sheetIndex];

    // Prepare export options
    ExportTableOptions opts = new ExportTableOptions
    {
        ExportAsString = exportAsString
    };

    // Determine used range
    int rows = ws.Cells.MaxDataRow + 1;
    int cols = ws.Cells.MaxDataColumn + 1;

    // Export and return
    return ws.ExportDataTable(0, 0, rows, cols, true, opts);
}
```

Пример использования:

```csharp
DataTable myTable = WorksheetToDataTable(@"C:\Data\input.xlsx");
```

Вот и всё — без лишних циклов, без COM‑interop, только чистые типизированные данные.

## Common Pitfalls & How to Avoid Them

| Проблема | Почему происходит | Как исправить |
|----------|-------------------|---------------|
| **Файл заблокирован другим процессом** | Открытие книги без `LoadOptions` может оставить открытым дескриптор файла. | Используйте `LoadOptions` с `MemorySetting.MemoryPreference` или оберните `Workbook` в `using`. |
| **Отсутствуют заголовки столбцов** | Если первая строка содержит данные, а не заголовки, `ExportDataTable` воспримет её как данные. | Передайте `false` параметру `includeColumnNames` и добавьте имена столбцов вручную. |
| **Смешанные типы данных вызывают исключения** | При `ExportAsString = false` числовые ячейки становятся `double`, даты — `DateTime`. | Оставьте `ExportAsString = true`, если только не нужна строгая типизация, тогда обрабатывайте преобразования сами. |
| **Очень большие листы вызывают OutOfMemory** | Экспорт миллионов строк за один раз может переполнить кучу. | Экспортируйте частями: проходите блоками строк и объединяйте `DataTable`. |

## Bonus: Export Multiple Sheets at Once

Если нужно **export excel to datatable c#** для каждого листа, просто пройдитесь по `workbook.Worksheets`:

```csharp
var tables = new Dictionary<string, DataTable>();
foreach (Worksheet ws in workbook.Worksheets)
{
    tables[ws.Name] = ws.ExportDataTable(
        0, 0,
        ws.Cells.MaxDataRow + 1,
        ws.Cells.MaxDataColumn + 1,
        true,
        exportOptions);
}
```

Теперь `tables` содержит `DataTable` для каждого листа, ключом является имя листа — удобно для пакетного импорта.

## Conclusion

Мы провели вас от пустого файла Excel к полностью заполненному `DataTable`, используя лаконичный workflow **convert worksheet to DataTable**. Рассмотрены шаги загрузки книги, выбора листа, настройки параметров экспорта и окончательного извлечения данных в `DataTable`. С переиспользуемым вспомогательным методом вы теперь можете **read excel file into datatable c#** в любой части вашего кода, а также имеете шаблон для **export excel to datatable c#** на несколько листов.

Что дальше? Попробуйте передать полученный `DataTable` в `BulkInsert` Entity Framework, сгенерировать CSV‑отчёты или применить LINQ‑фильтры для извлечения инсайтов. Возможности безграничны, когда данные Excel живут в памяти как правильная таблица.

Есть вопросы или сложный файл Excel, который не поддаётся? Оставьте комментарий ниже, и happy coding!

## What Should You Learn Next?

Следующие руководства охватывают тесно связанные темы, расширяющие техники, продемонстрированные в этом гиде. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, помогающими освоить дополнительные возможности API и исследовать альтернативные подходы в ваших проектах.

- [Как импортировать DataTable в Excel с помощью Aspose.Cells для .NET (пошаговое руководство)](/cells/english/net/import-export/import-datatable-excel-aspose-cells-net/)
- [Экспорт данных Excel в DataTable с помощью Aspose.Cells для .NET: Полное руководство](/cells/english/net/import-export/export-excel-data-datatatable-aspose-cells-net/)
- [Экспорт HTML‑строк из Excel в DataTable с помощью Aspose.Cells для .NET: Пошаговое руководство](/cells/english/net/import-export/export-html-strings-excel-datatable-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}