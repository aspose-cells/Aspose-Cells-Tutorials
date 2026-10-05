---
category: general
date: 2026-05-30
description: Узнайте, как добавить чередующиеся цвета строк в листах C#, установить
  фон ячейки сплошным заливом и без усилий настроить стиль ячеек листа.
draft: false
keywords:
- alternating row colors
- set cell background
- solid fill pattern
- add background color
- worksheet cell style
language: ru
og_description: Легко задавать чередующиеся цвета строк в листах C#. Узнайте, как
  установить фон ячейки, использовать сплошную заливку и освоить стиль ячеек листа.
og_title: Чередующиеся цвета строк в листах C# – Полное руководство
schemas:
- author: Aspose
  dateModified: '2026-05-30'
  description: Learn how to add alternating row colors in C# worksheets, set cell
    background with a solid fill pattern, and customize worksheet cell style effortlessly.
  headline: Alternating Row Colors in C# Worksheets – Complete Guide
  type: TechArticle
- description: Learn how to add alternating row colors in C# worksheets, set cell
    background with a solid fill pattern, and customize worksheet cell style effortlessly.
  name: Alternating Row Colors in C# Worksheets – Complete Guide
  steps:
  - name: Why Use a **Solid Fill Pattern**?
    text: The `Pattern` property tells the engine how to render the color. A `Solid`
      fill guarantees that the entire cell background is painted, eliminating any
      faint gridlines that might otherwise show through. This is the most common way
      to **set cell background** when you want a clean look.
  - name: Change the Colors
    text: 'If your brand uses different hues, just replace `Color.LightYellow` and
      `Color.LightCyan` with any `System.Drawing.Color` you prefer. For example:'
  - name: Use a Different **Background Type**
    text: While `BackgroundType.Solid` is the most common, you can experiment with
      `BackgroundType.Gray125`, `BackgroundType.Horizontal`, or any pattern that the
      library supports. This changes the visual texture while still **adding background
      color**.
  - name: Apply a **Worksheet Cell Style** to Specific Columns
    text: 'Sometimes you only want the alternating effect on data columns, leaving
      the first column (e.g., IDs) untouched. Create a separate style for that column
      and assign it after the import:'
  type: HowTo
tags:
- C#
- Excel
- Aspose.Cells
- DataTable
- Styling
title: Чередующиеся цвета строк в листах C# – Полное руководство
url: /ru/net/excel-colors-and-background-settings/alternating-row-colors-in-c-worksheets-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Чередование цветов строк в листах C# – Полное руководство

Когда‑нибудь задумывались, как сделать экспорт в Excel более эстетичным, используя **чередующиеся цвета строк**? Вы не одиноки — разработчики постоянно спрашивают, как *добавить цвет фона* строкам без написания миллионов строк кода.  

В этом руководстве мы пошагово рассмотрим простой способ **установить фон ячейки** для каждой строки, применить **сплошной шаблон заливки** и управлять **стилем ячеек листа**, чтобы результат был одновременно читаемым и визуально привлекательным.

## Что вы узнаете

- Как получить данные в `DataTable` (или любой табличный источник).  
- Как построить массив объектов `Style`, чередующих два цвета.  
- Как импортировать `DataTable` в лист, применяя эти стили.  
- Как проверить результат и при необходимости подправить цвета или шаблоны.  

Никаких внешних инструментов, кроме среды .NET и библиотеки для работы с таблицами (в примерах мы используем **Aspose.Cells**), не требуется. К концу вы получите переиспользуемый метод, который можно вставить в любой конвейер отчетности.

---

## Шаг 1: Получить исходные данные в виде `DataTable`

Первое — без данных нечего стилизовать. Ниже небольшой помощник, который создает `DataTable` с примерными строками. В реальном проекте вы замените его вызовом к базе данных или парсером CSV.

```csharp
using System;
using System.Data;

static DataTable GetData()
{
    // Create a simple table with three columns
    DataTable table = new DataTable("Report");
    table.Columns.Add("ID", typeof(int));
    table.Columns.Add("Name", typeof(string));
    table.Columns.Add("Score", typeof(double));

    // Populate with dummy rows
    for (int i = 1; i <= 10; i++)
    {
        table.Rows.Add(i, $"Item {i}", Math.Round(new Random().NextDouble() * 100, 2));
    }

    return table;
}
```

> **Почему это важно:** Наличие данных в `DataTable` позволяет движку листа *импортировать* их одним вызовом, автоматически сохраняя имена столбцов и типы данных.

## Шаг 2: Создать стили **чередующихся цветов строк**

Теперь мы сгенерируем массив объектов `Style` — по одному на каждую строку — чтобы четные строки получили светло‑желтый оттенок, а нечетные — нежный циан. Это ядро техники **чередования цветов строк**.

```csharp
using Aspose.Cells;
using System.Drawing;

// Assume workbook and worksheet are already instantiated
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.Worksheets[0];

// Retrieve data
DataTable dataTable = GetData();

// Prepare an array of styles – one for each row in the table
Style[] rowStyles = new Style[dataTable.Rows.Count];

for (int i = 0; i < rowStyles.Length; i++)
{
    // Create a fresh style for the current row
    rowStyles[i] = workbook.CreateStyle();

    // **Add background color**: LightYellow for even rows, LightCyan for odd rows
    rowStyles[i].ForegroundColor = (i % 2 == 0)
        ? Color.LightYellow
        : Color.LightCyan;

    // **Set cell background** using a **solid fill pattern**
    rowStyles[i].Pattern = BackgroundType.Solid;

    // Optional: you could also set font color, borders, etc., here
}
```

### Почему использовать **сплошной шаблон заливки**?

Свойство `Pattern` указывает движку, как отрисовывать цвет. Сплошная (`Solid`) заливка гарантирует, что весь фон ячейки будет окрашен, устраняя любые слабые линии сетки, которые могли бы просвечивать. Это самый распространенный способ **установить фон ячейки**, когда нужен чистый вид.

## Шаг 3: Импортировать `DataTable` с подготовленными стилями

С готовым массивом стилей импорт становится однострочником. Aspose.Cells автоматически применит соответствующий стиль к каждой строке.

```csharp
// Import the DataTable into the worksheet, applying the prepared styles
worksheet.Cells.ImportDataTable(
    dataTable,                     // source
    true,                          // include column names
    0,                             // start row (0‑based)
    0,                             // start column (0‑based)
    rowStyles);                    // array of styles
```

> **Что происходит «под капотом»?**  
> Библиотека проходит по каждой строке, копирует значения в ячейки и затем применяет соответствующий `Style` из `rowStyles`. Поскольку мы уже задали **сплошной шаблон заливки**, каждая ячейка в строке наследует один и тот же цвет фона, обеспечивая идеальное **чередование цветов строк**.

## Шаг 4: Сохранить книгу и проверить результат

Быстрое сохранение позволяет открыть файл в Excel (или любом совместимом просмотрщике) и увидеть эффект.

```csharp
// Save to disk – you can change the format to .xlsx, .xls, .csv, etc.
workbook.Save("AlternatingRowsReport.xlsx", SaveFormat.Xlsx);
Console.WriteLine("Workbook saved. Open 'AlternatingRowsReport.xlsx' to see the result.");
```

При открытии файла строки 1, 3, 5… будут светло‑желтыми, а строки 2, 4, 6… — светло‑циановыми. Заголовки столбцов остаются белыми, что делает данные более заметными.

![Worksheet showing alternating row colors](/images/alternating-row-colors.png "Screenshot of worksheet with alternating row colors")

*Текст alt изображения:* **чередующиеся цвета строк** — скриншот листа, где фон каждой строки чередуется между светло‑желтым и светло‑циановым.

## Шаг 5: Дальнейшая настройка (по желанию)

### Смена цветов

Если ваш бренд использует другие оттенки, просто замените `Color.LightYellow` и `Color.LightCyan` на любые `System.Drawing.Color`, которые вам нужны. Например:

```csharp
rowStyles[i].ForegroundColor = (i % 2 == 0) ? Color.FromArgb(255, 235, 205) // Peach
                                            : Color.FromArgb(205, 235, 255); // Soft blue
```

### Использовать другой **тип фона**

Хотя `BackgroundType.Solid` самый распространенный, вы можете поэкспериментировать с `BackgroundType.Gray125`, `BackgroundType.Horizontal` или любым другим шаблоном, поддерживаемым библиотекой. Это изменит визуальную текстуру, но по‑прежнему будет **добавлять цвет фона**.

### Применить **стиль ячеек листа** к отдельным столбцам

Иногда требуется оставить чередующийся эффект только для данных столбцов, а первый столбец (например, идентификаторы) оставить без изменений. Создайте отдельный стиль для этого столбца и назначьте его после импорта:

```csharp
Style idStyle = workbook.CreateStyle();
idStyle.ForegroundColor = Color.White;
idStyle.Pattern = BackgroundType.Solid;

// Apply to the first column (A)
for (int row = 0; row < dataTable.Rows.Count + 1; row++) // +1 for header
{
    worksheet.Cells[row, 0].SetStyle(idStyle);
}
```

---

## Заключение

Теперь у вас есть полное, переиспользуемое решение для **чередования цветов строк** в листах C#. Создавая массив объектов `Style`, **устанавливая фон ячейки** с помощью **сплошного шаблона заливки** и импортируя `DataTable` одним вызовом, вы можете генерировать профессиональные отчёты с минимальным объёмом кода.  

Дальше вы можете:

- **Добавить цвет фона** к строкам‑заголовкам для дополнительного акцента.  
- Скомбинировать эту технику с условным форматированием для динамических визуальных подсказок.  
- Исследовать другие свойства **стиля ячеек листа**, такие как шрифты, границы или числовые форматы.

Попробуйте в следующем экспорте — ваши пользователи оценят более чистые и удобочитаемые таблицы. Приятного кодинга!

## Что изучать дальше?

- [Установка высоты строк в листе с Aspose.Cells для .NET](/cells/english/net/size-and-spacing-customization/setting-height-of-all-rows-in-worksheet/)
- [Преобразование имен ячеек Excel в индексы строк и столбцов с помощью Aspose.Cells для .NET](/cells/english/net/cell-operations/convert-excel-cell-names-to-indices-aspose-cells-dotnet/)
- [Установка цветов вкладок листа в Excel с помощью Aspose.Cells .NET — Полное руководство](/cells/english/net/worksheet-management/set-worksheet-tab-colors-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}