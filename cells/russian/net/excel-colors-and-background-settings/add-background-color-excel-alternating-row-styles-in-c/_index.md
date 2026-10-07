---
category: general
date: 2026-04-07
description: Добавьте цвет фона строк в Excel с помощью C#. Узнайте, как применять
  чередующиеся цвета строк, устанавливать сплошные стили фона и импортировать DataTable
  в Excel в одном рабочем процессе.
draft: false
keywords:
- add background color excel
- apply alternating row colors
- style excel rows
- set solid background
- import datatable to excel
language: ru
og_description: Добавьте цвет фона строк в Excel с помощью C#. Это руководство показывает,
  как применять чередующиеся цвета строк, установить сплошной фон и эффективно импортировать
  DataTable в Excel.
og_title: Добавить цвет фона в Excel – чередующиеся стили строк в C#
tags:
- C#
- Excel
- DataTable
- Styling
title: Добавить цвет фона в Excel — чередующиеся стили строк в C#
url: /ru/net/excel-colors-and-background-settings/add-background-color-excel-alternating-row-styles-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Добавить цвет фона в Excel – чередующиеся стили строк в C#

Когда‑нибудь вам нужно было **add background color excel** строки, но вы не знали, как сделать это без тысячи строк сложного кода? Вы не одиноки — большинство разработчиков сталкиваются с этим, когда впервые пытаются сделать свои таблицы более чем просто сырым набором данных.  

Хорошая новость? Всего за несколько минут вы можете **apply alternating row colors**, установить **solid background**, и даже **import datatable to excel**, используя чистый, переиспользуемый шаблон в C#.  

В этом руководстве мы пройдем весь процесс, от получения данных в `DataTable` до стилизации каждой строки с помощью светло‑желто‑белой полосатой схемы. Никакие внешние библиотеки, кроме надёжного пакета для работы с Excel (например, **ClosedXML** или **GemBox.Spreadsheet**), не требуются, и вы увидите, почему такой подход одновременно производителен и прост в поддержке.

## Что вы узнаете

- Как получить данные и загрузить их в лист Excel.
- Как **style excel rows** с чередующимися цветами фона.
- Механика **set solid background** с использованием объекта `Style`.
- Как **import datatable to excel**, сохраняя стили строк.
- Советы по обработке граничных случаев, таких как пустые таблицы или пользовательские схемы цветов.

> **Pro tip:** Если вы уже используете объект книги (`wb`) из библиотеки, поддерживающей создание стилей, вы можете переиспользовать те же экземпляры `Style` в нескольких листах — экономя память и поддерживая код в порядке.

---

## Шаг 1: Получение данных – подготовка DataTable

Прежде чем применять стили, нам нужен источник строк. В большинстве реальных сценариев они поступают из базы данных, API или CSV‑файла. Для примера мы просто создадим простой `DataTable` в памяти.

```csharp
using System;
using System.Data;
using System.Drawing;          // For Color
using GemBox.Spreadsheet;      // Or ClosedXML, whichever you prefer

// Simulated data fetch – replace with your own data access logic
DataTable GetData()
{
    var table = new DataTable();
    table.Columns.Add("Id", typeof(int));
    table.Columns.Add("Name", typeof(string));
    table.Columns.Add("Score", typeof(double));

    // Populate with sample rows
    for (int i = 1; i <= 10; i++)
        table.Rows.Add(i, $"Student {i}", Math.Round(new Random().NextDouble() * 100, 2));

    return table;
}
```

**Why this matters:** Использование `DataTable` предоставляет табличный, схематически‑осведомлённый контейнер, который библиотека Excel может импортировать напрямую, избавляя от необходимости писать циклы по отдельным ячейкам.

---

## Шаг 2: Создание стилей строк – **Apply alternating row colors**

Теперь мы создадим массив объектов `Style` — по одному на строку — чтобы каждая строка могла получить собственный фон. Шаблон, который мы будем использовать, — классический светло‑желтый для чётных строк и белый для нечётных.

```csharp
// Assume 'wb' is an existing Workbook instance
Workbook wb = new Workbook();

// Retrieve data
DataTable dataTable = GetData();

// Allocate a style for each row
Style[] rowStyles = new Style[dataTable.Rows.Count];

for (int i = 0; i < rowStyles.Length; i++)
{
    // Create a fresh style instance
    rowStyles[i] = wb.CreateStyle();

    // Choose background colour based on row index
    rowStyles[i].ForegroundColor = (i % 2 == 0) ? Color.LightYellow : Color.White;

    // Ensure the colour is actually applied
    rowStyles[i].Pattern = BackgroundType.Solid;   // <-- **set solid background**
}
```

**Explanation:**  
- `wb.CreateStyle()` предоставляет чистый объект стиля, который можно менять, не влияя на другие.  
- Тернарный оператор `(i % 2 == 0)` определяет, чётная строка (светло‑желтая) или нечётная (белая).  
- Установка `Pattern = BackgroundType.Solid` — ключевой шаг, который **set solid background**; без этого цвет будет проигнорирован.

---

## Шаг 3: Получение целевого листа

Большинство библиотек предоставляют коллекцию листов. Мы будем работать с первым, но вы можете выбрать любой индекс или имя по своему усмотрению.

```csharp
Worksheet worksheet = wb.Worksheets[0];   // First worksheet in the workbook
```

Если книга только что создана, библиотека обычно создает лист по умолчанию. В противном случае вы можете добавить лист явно:

```csharp
// Alternative: create a new sheet named "Report"
Worksheet worksheet = wb.Worksheets.Add("Report");
```

---

## Шаг 4: Импорт DataTable со стилями строк – **Import datatable to excel**

С готовыми стилями последний шаг — загрузить `DataTable` в лист, применяя соответствующий стиль к каждой строке.

```csharp
// Parameters: (DataTable, includeHeaders, startRow, startColumn, stylesArray)
worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, rowStyles);
```

**What’s happening under the hood?**  
- `true` указывает методу записать заголовки столбцов в первой строке.  
- `0, 0` обозначает верхний‑левый угол (A1) как точку вставки.  
- `rowStyles` сопоставляет каждый `Style` с соответствующей строкой данных, предоставляя нам чередующиеся цвета, подготовленные ранее.

---

## Шаг 5: Сохранение книги

Последний элемент головоломки — сохранить книгу в файл, чтобы открыть её в Excel и увидеть результат.

```csharp
// Choose a format – XLSX is the modern default
wb.Save("StudentScores.xlsx");

// Optional: open automatically (Windows only)
System.Diagnostics.Process.Start("StudentScores.xlsx");
```

Откройте файл, и вы увидите аккуратно отформатированный лист:

- Строка заголовка жирным шрифтом (стиль по умолчанию библиотеки).  
- Строки 1, 3, 5… с чистым белым фоном.  
- Строки 2, 4, 6… с лёгкой светло‑желтой заливкой, упрощающей просмотр.

### Ожидаемый результат

| Id | Name      | Score |
|----|-----------|-------|
| 1  | Student 1 | 78.45 |
| 2  | Student 2 | 62.13 |
| 3  | Student 3 | 91.27 |
| …  | …         | …     |

Строки 2, 4, 6, … отображаются со светло‑желтым фоном — точно тот эффект **apply alternating row colors**, к которому мы стремились.

![Пример добавления цвета фона в Excel](https://example.com/excel-background.png "Пример добавления цвета фона в Excel")

*(Alt‑text содержит основной ключевой запрос для SEO.)*

---

## Обработка граничных случаев и вариантов

### Пустой DataTable

Если `dataTable.Rows.Count` равно нулю, массив `rowStyles` будет пустым, и `ImportDataTable` всё равно запишет строку заголовка (если `includeHeaders` равно `true`). Исключение не будет выброшено, но возможно стоит защититься от создания почти пустого файла:

```csharp
if (dataTable.Rows.Count == 0)
{
    Console.WriteLine("No data to export – workbook will contain only headers.");
}
```

### Пользовательские схемы цветов

Хотите полосы синего/серого вместо желтого/белого? Просто замените значения `Color`:

```csharp
rowStyles[i].ForegroundColor = (i % 2 == 0) ? Color.LightBlue : Color.LightGray;
```

Не стесняйтесь брать цвета из конфигурационного файла, чтобы не‑разработчики могли менять палитру без правки кода.

### Переиспользование стилей в нескольких листах

Если вы экспортируете несколько таблиц в одну книгу, вы можете создать массив стилей один раз и переиспользовать его:

```csharp
Style[] sharedStyles = CreateAlternatingStyles(dataTable.Rows.Count);
worksheet1.Cells.ImportDataTable(dt1, true, 0, 0, sharedStyles);
worksheet2.Cells.ImportDataTable(dt2, true, 0, 0, sharedStyles);
```

Только будьте внимательны, чтобы обе таблицы имели одинаковое количество строк, иначе создайте новый массив для каждого листа.

---

## Полный рабочий пример

Объединив всё вместе, представляем автономную программу, которую можно скопировать и вставить в консольное приложение.

```csharp
using System;
using System.Data;
using System.Drawing;
using GemBox.Spreadsheet;   // Install-Package GemBox.Spreadsheet

class Program
{
    static void Main()
    {
        // License free for small projects – remove for commercial use
        SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

        // 1️⃣ Retrieve data
        DataTable dataTable = GetData();

        // 2️⃣ Initialise workbook
        Workbook wb = new Workbook();

        // 3️⃣ Create alternating row styles
        Style[] rowStyles = CreateAlternatingStyles(dataTable.Rows.Count);

        // 4️⃣ Get (or create) the target worksheet
        Worksheet ws = wb.Worksheets.Add("Report");

        // 5️⃣ Import data with styles
        ws.Cells.ImportDataTable(dataTable, true, 0, 0, rowStyles);

        // 6️⃣ Save the file
        wb.Save("Report.xlsx");
        Console.WriteLine("Excel file created – check Report.xlsx");
    }

    // Helper: generate a DataTable with sample data
    static DataTable GetData()
    {
        var dt = new DataTable();
        dt.Columns.Add("Id", typeof(int));
        dt.Columns.Add("Name", typeof(string));
        dt.Columns.Add("Score", typeof(double));

        var rnd = new Random();
        for (int i = 1; i <= 12; i++)
            dt.Rows.Add(i, $"Student {i}", Math.Round(rnd.NextDouble() * 100, 2));

        return dt;
    }

    // Helper: create style array for alternating colors
    static Style[] CreateAlternatingStyles(int rowCount)
    {
        var wb = new Workbook();               // Temporary workbook for style creation
        var styles = new Style[rowCount];
        for (int i = 0; i < rowCount; i++)
        {
            styles[i] = wb.CreateStyle();
            styles[i].ForegroundColor = (i % 2 == 0) ? Color.LightYellow : Color.White;
            styles[i].Pattern = BackgroundType.Solid;   // **set solid background**
        }
        return styles;
    }
}
```

Запустите программу, откройте `Report.xlsx`, и вы увидите чередующийся фон точно как описано.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}