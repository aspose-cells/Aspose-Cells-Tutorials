---
category: general
date: 2026-03-22
description: Учебник по пользовательскому формату чисел в Excel, показывающий, как
  импортировать DataTable в Excel, установить цвет фона столбца, отформатировать столбец
  как валюту и сохранить книгу в формате xlsx.
draft: false
keywords:
- custom number format excel
- import datatable to excel
- set column background color
- format column as currency
- save workbook as xlsx
language: ru
og_description: Учебник по пользовательскому числовому формату в Excel, который пошагово
  покажет, как импортировать DataTable, установить цвет фона столбца, отформатировать
  столбец как валюту и сохранить книгу в формате xlsx.
og_title: Пользовательский числовой формат Excel в C# – пошаговое руководство
tags:
- C#
- Excel automation
- Aspose.Cells
- Data export
title: Пользовательский числовой формат Excel в C# – Полное руководство
url: /ru/net/excel-custom-number-date-formatting/custom-number-format-excel-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Пользовательский числовой формат Excel – Full‑Stack C# учебник

Задумывались ли вы когда‑нибудь, как применить стиль **custom number format excel** непосредственно из C#? Возможно, вы пробовали выгрузить DataTable в таблицу и видели только обычные числа, без цветов и без форматирования валюты. Это распространённая проблема — особенно когда нужен отшлифованный отчёт для заинтересованных сторон.

В этом руководстве мы решим эту проблему вместе: вы узнаете, как **import datatable to excel**, **set column background color**, **format column as currency**, и, наконец, **save workbook as xlsx** с пользовательским числовым форматом, который делает ваши цифры яркими. Никаких расплывчатых ссылок, только полноценное, готовое к запуску решение, которое вы можете скопировать‑вставить в свой проект.

---

## Что вы построите

К концу этого руководства у вас будет автономное C# консольное приложение, которое:

1. Получает `DataTable` (вы можете заменить заглушку своим запросом).  
2. Создаёт новую книгу Excel с использованием Aspose.Cells (или любой совместимой библиотеки).  
3. Применяет синий полужирный шрифт к первой колонке, светло‑жёлтый фон ко второй и формат валюты (`$#,##0.00`) к третьей.  
4. Сохраняет файл как `DataTableWithStyleArray.xlsx` в выбранной вами папке.

Вы увидите точно, как каждая строка влияет на конечный файл Excel, и мы обсудим, почему эти решения важны для поддерживаемости и производительности.

---

## Требования

- .NET 6.0 или новее (код также работает с .NET Framework 4.7+).  
- Aspose.Cells for .NET (бесплатная пробная версия или лицензированная). Установите через NuGet:

```bash
dotnet add package Aspose.Cells
```

- Базовое знакомство с `DataTable` и консольными приложениями C#.

---

## Шаг 1: Получить исходные данные в виде DataTable

Сначала нам нужны данные для экспорта. В реальном сценарии вы, вероятно, вызовете репозиторий или выполните SQL‑запрос. Для иллюстрации мы создадим простую таблицу в памяти.

```csharp
using System;
using System.Data;
using Aspose.Cells;

static DataTable GetSampleData()
{
    var table = new DataTable("Sales");
    table.Columns.Add("Product", typeof(string));
    table.Columns.Add("Quantity", typeof(int));
    table.Columns.Add("Revenue", typeof(decimal));

    table.Rows.Add("Widget A", 120, 3450.75m);
    table.Rows.Add("Widget B", 85, 2190.00m);
    table.Rows.Add("Widget C", 60, 1580.40m);

    return table;
}
```

> **Почему это важно:** Использование `DataTable` предоставляет табличный, схематически‑осознанный источник, который чисто отображается в строки и столбцы Excel. Это также позволяет переиспользовать одну и ту же логику экспорта для любого набора данных без переписывания кода.

---

## Шаг 2: Создать новую книгу и получить первый лист

Теперь мы создаём книгу Excel. Класс `Workbook` представляет весь файл; его `Worksheets[0]` — это лист по умолчанию, куда мы поместим наши данные.

```csharp
// Initialize a fresh workbook
Workbook workbook = new Workbook();

// Grab the first (and only) worksheet
Worksheet worksheet = workbook.Worksheets[0];
```

> **Совет:** Если вам нужны несколько листов, просто вызовите `workbook.Worksheets.Add("SheetName")` и повторите шаги стилизации для каждого.

---

## Шаг 3: Определить стили столбцов – шрифт, фон и числовой формат

Стилизация в Aspose.Cells выполняется через объекты `Style`. Мы создадим массив, где каждый элемент соответствует столбцу в DataTable.

```csharp
// Prepare an array to hold three distinct styles
Style[] columnStyles = new Style[3];

// 1️⃣ First column – blue, bold font
columnStyles[0] = workbook.CreateStyle();
columnStyles[0].Font.Color = System.Drawing.Color.Blue;
columnStyles[0].Font.IsBold = true;

// 2️⃣ Second column – light‑yellow background
columnStyles[1] = workbook.CreateStyle();
columnStyles[1].ForegroundColor = System.Drawing.Color.LightYellow;
columnStyles[1].Pattern = BackgroundType.Solid;

// 3️⃣ Third column – custom currency format (custom number format excel)
columnStyles[2] = workbook.CreateStyle();
columnStyles[2].Custom = "$#,##0.00";
```

> **Почему массив стилей?** Передача массива в `ImportDataTable` позволяет применить отдельный стиль к каждому столбцу за один вызов, что одновременно лаконично и эффективно. Это также гарантирует, что форматирование остаётся синхронным с порядком данных.

---

## Шаг 4: Импортировать DataTable с применением стилей

Вот сердце операции: мы передаём `DataTable` в лист, указываем Aspose включить строку заголовка и передаём наш массив `columnStyles`.

```csharp
// Import data starting at cell A1 (row 0, column 0)
worksheet.Cells.ImportDataTable(
    GetSampleData(),   // source DataTable
    true,              // include column names as header
    0, 0,              // start row, start column
    columnStyles);     // apply the style array
```

> **Что происходит под капотом?** Aspose проходит по каждому столбцу, записывает заголовок, затем записывает значения каждой строки. При этом он применяет соответствующий `Style` из массива, так что вы получаете синий заголовок для «Product», желтоватый «Quantity» и красиво отформатированный столбец «Revenue».

---

## Шаг 5: Сохранить книгу в файл XLSX

Наконец, мы сохраняем книгу на диск. Метод `Save` автоматически выбирает формат XLSX на основе расширения файла.

```csharp
// Choose a folder that exists on your machine
string outputPath = @"C:\Temp\DataTableWithStyleArray.xlsx";

// Ensure the directory exists (optional safety check)
System.IO.Directory.CreateDirectory(System.IO.Path.GetDirectoryName(outputPath)!);

// Save the workbook
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

> **Подсказка:** Если вам нужно передавать файл в поток (например, для веб‑API), используйте `workbook.Save(stream, SaveFormat.Xlsx)` вместо пути к файлу.

---

## Полный рабочий пример

Ниже приведена полная программа, которую вы можете вставить в новый консольный проект. Она компилируется и запускается как есть, создавая стилизованный файл Excel.

```csharp
using System;
using System.Data;
using Aspose.Cells;

namespace ExcelExportDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1 – Get data
            DataTable dataTable = GetSampleData();

            // Step 2 – Create workbook & worksheet
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.Worksheets[0];

            // Step 3 – Prepare column styles
            Style[] columnStyles = new Style[3];

            // Font style for first column (blue, bold)
            columnStyles[0] = workbook.CreateStyle();
            columnStyles[0].Font.Color = System.Drawing.Color.Blue;
            columnStyles[0].Font.IsBold = true;

            // Background style for second column (light yellow)
            columnStyles[1] = workbook.CreateStyle();
            columnStyles[1].ForegroundColor = System.Drawing.Color.LightYellow;
            columnStyles[1].Pattern = BackgroundType.Solid;

            // Currency format for third column (custom number format excel)
            columnStyles[2] = workbook.CreateStyle();
            columnStyles[2].Custom = "$#,##0.00";

            // Step 4 – Import data with styles
            worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);

            // Step 5 – Save as XLSX
            string outputPath = @"C:\Temp\DataTableWithStyleArray.xlsx";
            System.IO.Directory.CreateDirectory(System.IO.Path.GetDirectoryName(outputPath)!);
            workbook.Save(outputPath);

            Console.WriteLine($"Workbook saved to {outputPath}");
        }

        // Helper method to build a demo DataTable
        static DataTable GetSampleData()
        {
            var table = new DataTable("Sales");
            table.Columns.Add("Product", typeof(string));
            table.Columns.Add("Quantity", typeof(int));
            table.Columns.Add("Revenue", typeof(decimal));

            table.Rows.Add("Widget A", 120, 3450.75m);
            table.Rows.Add("Widget B", 85, 2190.00m);
            table.Rows.Add("Widget C", 60, 1580.40m);

            return table;
        }
    }
}
```

### Ожидаемый результат

Когда вы откроете `DataTableWithStyleArray.xlsx`, вы увидите:

| **Продукт** (синий, полужирный) | **Количество** (светло‑желтый) | **Выручка** (валюта) |
|--------------------------|-----------------------------|------------------------|
| Widget A                 | 120                         | $3,450.75              |
| Widget B                 | 85                          | $2,190.00              |
| Widget C                 | 60                          | $1,580.40              |

Указанный вами **custom number format excel** (`$#,##0.00`) гарантирует, что каждая ячейка выручки отображает знак доллара, разделитель тысяч и два знака после запятой — именно то, что ожидают финансовые команды.

---

## Часто задаваемые вопросы и особые случаи

### Можно ли использовать это с другой библиотекой Excel?

Конечно. Концепция — создание стиля для каждого столбца и применение его при импорте — переносится на EPPlus, ClosedXML или NPOI. Вызовы API различаются, но шаблон остаётся тем же.

### Что если у моего DataTable больше столбцов, чем стилей?

Aspose применит стиль по умолчанию к любому столбцу без соответствующей записи в массиве `columnStyles`. Чтобы избежать неожиданностей, либо задайте размер массива равным `dataTable.Columns.Count`, либо генерируйте стили динамически в цикле.

### Как установить пользовательский числовой формат для дат?

Просто установите `style.Custom = "dd‑mm‑yyyy"` (или любую другую допустимую строку формата Excel). Тот же подход на основе массива работает для дат, процентов или научной нотации.

### Есть ли способ автоматически подгонять ширину столбцов после импорта?

Да — вызовите `worksheet.AutoFitColumns();` после импорта. Он быстро рассчитывает ширину на основе содержимого ячеек.

### Что насчёт больших наборов данных (100k+ строк)?

`ImportDataTable` оптимизирован для массовых операций, но вы можете столкнуться с ограничениями памяти. В этом случае рассмотрите возможность потоковой передачи строк вручную с помощью `Cells[i, j].PutValue(...)` и повторного использования одного объекта `Style` для снижения нагрузки.

---

## Профессиональные советы и распространённые подводные камни

- **Избегайте жёсткого кодирования путей** в продакшн‑коде; используйте `Environment.GetFolderPath` или настройки конфигурации.  
- **Освобождайте книгу** (dispose) если вы работаете в длительно работающем сервисе — оберните её в блок `using`, чтобы освободить нативные ресурсы.  
- **Следите за разделителями, зависящими от культуры**. Пользовательский формат `$#,##0.00` принудительно использует точку как десятичный разделитель независимо от локали ОС, что обычно требуется для финансовых отчётов.  
- **Не забудьте добавить ссылку на System.Drawing** (или `System.Drawing.Common` в .NET Core) для структур цвета, используемых в стилизации.  
- **Тестируйте вывод в разных версиях Excel**; старые версии могут интерпретировать некоторые пользовательские форматы немного иначе.

---

## Заключение

Мы рассмотрели всё, что вам нужно для **custom number format excel** файлов из C#: извлечение данных из `DataTable`, **import datatable to excel**, применение **set column background color**, использование **format column as currency**, и, наконец, **save workbook as x

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}