---
category: general
date: 2026-02-26
description: Быстро применяйте числовой формат в Excel и узнайте, как отформатировать
  столбец как валюту, задать числовой формат столбца и установить цвет шрифта столбца
  всего за несколько строк кода C#.
draft: false
keywords:
- apply number format excel
- format column as currency
- set column number format
- format currency column
- set column font color
language: ru
og_description: Примените числовой формат Excel в C# с помощью простых шагов. Узнайте,
  как отформатировать столбец как валюту, установить числовой формат столбца и задать
  цвет шрифта столбца для профессиональных таблиц.
og_title: Применение числового формата в Excel — Полное руководство по стилизации
  столбцов
tags:
- C#
- Excel
- Aspose.Cells
- DataTable
- Styling
title: Применение числового формата в Excel – пошаговое руководство по форматированию
  столбцов
url: /ru/net/number-and-display-formats-in-excel/apply-number-format-excel-step-by-step-guide-to-formatting-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Применить числовой формат Excel – Как стилизовать столбцы Excel в C#

Когда‑нибудь задавались вопросом, как **apply number format excel** во время обхода `DataTable`? Вы не одиноки. Большинство разработчиков сталкиваются с проблемой, когда нужен заголовок синего шрифта *и* столбец, отформатированный как валюта, в одной операции импорта. Хорошая новость? С несколькими строками C# и правильными объектами стиля вы можете сделать это без пост‑обработки листа.

В этом руководстве мы пройдем полный, готовый к запуску пример, показывающий, как **format column as currency**, **set column number format** для любого другого столбца и даже **set column font color** для заголовков. К концу вы получите переиспользуемый шаблон, который можно вставить в любой проект Aspose.Cells (или аналогичный).

## Что вы узнаете

- Как получить `DataTable` и сопоставить каждый столбец с конкретным `Style`.
- Точные шаги для **apply number format excel** с помощью `Worksheet.Cells.ImportDataTable`.
- Почему создание стилей заранее эффективнее, чем форматирование ячеек по одной.
- Обработка граничных случаев, когда исходная таблица содержит больше столбцов, чем вы стилизовали.
- Полный, готовый к копированию и вставке код, который вы можете запустить уже сегодня.

> **Prerequisite:** This guide assumes you have Aspose.Cells for .NET (or any library exposing `Workbook`, `Worksheet`, `Style` APIs) referenced in your project. If you’re using a different library, the concepts translate directly—just replace the type names.

---

## Шаг 1: Получить исходные данные как DataTable

Прежде чем можно будет применять стили, нужны сырые данные. В большинстве реальных сценариев данные находятся в базе, CSV‑файле или через API. Для наглядности мы смоделируем простой `DataTable` с двумя столбцами: *Product* (string) и *Price* (decimal).

```csharp
using System;
using System.Data;
using Aspose.Cells;
using System.Drawing;

public static DataTable GetData()
{
    var dt = new DataTable();
    dt.Columns.Add("Product", typeof(string));
    dt.Columns.Add("Price", typeof(decimal));

    dt.Rows.Add("Apple", 1.25m);
    dt.Rows.Add("Banana", 0.75m);
    dt.Rows.Add("Cherry", 2.10m);

    return dt;
}
```

> **Why this matters:** Pulling the data into a `DataTable` gives you a tabular, in‑memory representation that `ImportDataTable` can consume directly, eliminating the need for manual cell‑by‑cell insertion.

## Шаг 2: Создать массив стилей – по одному на каждый столбец

Перегрузка `ImportDataTable`, которую мы будем использовать, принимает массив объектов `Style`. Каждый элемент соответствует индексу столбца. Если оставить элемент `null`, столбец наследует стиль книги по умолчанию.

```csharp
// Initialize the workbook (Aspose.Cells)
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.Worksheets[0];

// Prepare the style array based on the number of columns
DataTable dataTable = GetData();
Style[] columnStyles = new Style[dataTable.Columns.Count];
```

> **Pro tip:** Declaring the array *after* you have the `DataTable` ensures the size matches exactly, preventing `IndexOutOfRangeException` later.

## Шаг 3: Установить цвет шрифта (синий) для первого столбца

Часто требуется выделить заголовки или ключевые столбцы отдельным цветом шрифта. Здесь мы делаем текст первого столбца синим.

```csharp
// Style for the first column – blue font
columnStyles[0] = workbook.CreateStyle();
columnStyles[0].Font.Color = Color.Blue;
```

> **Why use a style object?** Styles are reusable and applied in bulk, which is far faster than iterating over every cell after import. The workbook caches the style once, then reuses it for every cell in that column.

## Шаг 4: Форматировать второй столбец как валюту

Встроенные числовые форматы Excel идентифицируются индексом. `14` соответствует формату валюты по умолчанию (например, `$1,234.00`). Если нужен пользовательский формат, вместо этого можно задать строку формата.

```csharp
// Style for the second column – built‑in currency format (ID 14)
columnStyles[1] = workbook.CreateStyle();
columnStyles[1].Number = 14; // 14 = built‑in currency format
```

> **Edge case:** If your workbook uses a locale where the currency symbol isn’t `$`, the same index will adapt automatically (e.g., `€` for German locales).

## Шаг 5: Импортировать DataTable с определёнными стилями

Теперь собираем всё вместе. Метод `ImportDataTable` вставит данные, начиная с ячейки `A1` (строка 0, столбец 0) и применит подготовленные стили.

```csharp
// Import the DataTable into the worksheet, applying the column styles
worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);
```

- Второй параметр `true` указывает Aspose.Cells рассматривать первую строку `DataTable` как заголовки столбцов.
- Координаты `0, 0` задают левый‑верхний угол начала импорта.
- `columnStyles` сопоставляет каждый столбец с его стилем.

## Шаг 6: Сохранить книгу (по желанию, но удобно для проверки)

Если хотите увидеть результат в Excel, просто сохраните книгу на диск. Этот шаг не обязателен для логики стилизации, но полезен для отладки.

```csharp
// Save the workbook to a file
workbook.Save("StyledReport.xlsx", SaveFormat.Xlsx);
Console.WriteLine("Workbook saved as StyledReport.xlsx");
```

### Ожидаемый результат

| **Product** (синий шрифт) | **Price** (валюта) |
|---------------------------|--------------------|
| Apple                     | $1.25              |
| Banana                    | $0.75              |
| Cherry                    | $2.10              |

- Столбец *Product* отображается синим, что делает его заметным.
- Столбец *Price* показывает значения с символом валюты по умолчанию и двумя знаками после запятой.

---

## Часто задаваемые вопросы и варианты

### Как **set column number format** для более чем двух столбцов?

Просто расширьте массив `columnStyles`. Например, чтобы отобразить процент в третьем столбце:

```csharp
columnStyles[2] = workbook.CreateStyle();
columnStyles[2].Number = 10; // 10 = built‑in percentage format
```

### Что делать, если нужен *custom* формат валюты, например “USD 1,234.00”?

Замените свойство `Number` строкой формата:

```csharp
columnStyles[1].Custom = "\"USD\" #,##0.00";
```

### Можно ли применить **set column font color** к числовому столбцу, не затрагивая его числовой формат?

Абсолютно. Стили комбинируются. Вы можете задать одновременно `Font.Color` и `Number` в одном экземпляре `Style`:

```csharp
columnStyles[3] = workbook.CreateStyle();
columnStyles[3].Font.Color = Color.Green;
columnStyles[3].Number = 2; // 2 = built‑in date format (just an example)
```

### Что происходит, если в `DataTable` больше столбцов, чем стилей?

Любой столбец без явного стиля (`null` элемент) унаследует стиль книги по умолчанию. Чтобы избежать случайных `null`, можно сначала инициализировать весь массив базовым стилем:

```csharp
Style defaultStyle = workbook.CreateStyle();
defaultStyle.Font.Size = 11;
for (int i = 0; i < columnStyles.Length; i++)
    columnStyles[i] = defaultStyle;
```

Затем переопределить только нужные столбцы.

### Работает ли такой подход с большими наборами данных (10 k+ строк)?

Да. Поскольку стили применяются *один раз на столбец* до импорта, операция остаётся O(N) по отношению к строкам, а потребление памяти остаётся низким. Избегайте перебора каждой ячейки после импорта — именно там падает производительность.

---

## Полный рабочий пример (готов к копированию)

```csharp
using System;
using System.Data;
using System.Drawing;
using Aspose.Cells;

class ExcelStyler
{
    static void Main()
    {
        // 1️⃣ Retrieve data
        DataTable dataTable = GetData();

        // 2️⃣ Create workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 3️⃣ Prepare style array (one per column)
        Style[] columnStyles = new Style[dataTable.Columns.Count];

        // 4️⃣ Style first column – blue font
        columnStyles[0] = workbook.CreateStyle();
        columnStyles[0].Font.Color = Color.Blue;

        // 5️⃣ Style second column – built‑in currency format (ID 14)
        columnStyles[1] = workbook.CreateStyle();
        columnStyles[1].Number = 14;

        // 6️⃣ (Optional) Add more styles here – e.g., percentage, custom formats

        // 7️⃣ Import the DataTable with styles
        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);

        // 8️⃣ Save to file for verification
        workbook.Save("StyledReport.xlsx", SaveFormat.Xlsx);
        Console.WriteLine("Excel file created: StyledReport.xlsx");
    }

    // Helper method to mock data
    public static DataTable GetData()
    {
        var dt = new DataTable();
        dt.Columns.Add("Product", typeof(string));
        dt.Columns.Add("Price", typeof(decimal));

        dt.Rows.Add("Apple", 1.25m);
        dt.Rows.Add("Banana", 0.75m);
        dt.Rows.Add("Cherry", 2.10m);
        return dt;
    }
}
```

Запустите программу, откройте `StyledReport.xlsx`, и вы сразу увидите результат **apply number format excel**.

---

## Заключение

Мы продемонстрировали чистый и эффективный способ **apply number format excel** при импорте `DataTable`. Подготовив массив `Style[]` заранее, вы можете **format column as currency**, **set column number format** и **set column font color** одним вызовом — без пост‑обработки.

Не стесняйтесь расширять шаблон: добавлять условное форматирование, объединять ячейки для заголовков или даже внедрять формулы. Те же принципы сохранят ваш код аккуратным, а таблицы — профессиональными.

---

### Что дальше?

- Изучите **conditional formatting**, чтобы выделять значения, превышающие порог.
- Скомбинируйте эту технику с **pivot table generation** для динамической отчётности.
- Попробуйте **set column number format** для дат, процентов или пользовательской научной нотации.

Есть свой вариант? Делитесь в комментариях — давайте поддерживать

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}