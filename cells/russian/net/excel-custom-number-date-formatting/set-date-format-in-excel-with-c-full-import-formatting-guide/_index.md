---
category: general
date: 2026-06-17
description: Установите формат даты в Excel с помощью C#, а также задайте фон ячейки,
  примените цвет текста и раскрасьте столбец Excel при импорте. Учитесь шаг за шагом.
draft: false
keywords:
- set date format
- set cell background
- apply foreground color
- color excel column
- excel import formatting
language: ru
og_description: Установите формат даты в Excel с помощью C#, одновременно задавая
  фон ячейки, применяя цвет текста и раскрашивая столбец Excel при импорте. Полный
  учебник.
og_title: Установите формат даты в Excel с помощью C# – Полное руководство
schemas:
- author: Aspose
  dateModified: '2026-06-17'
  description: Set date format in Excel using C# and also set cell background, apply
    foreground color, and color Excel column during import. Learn step‑by‑step.
  headline: Set date format in Excel with C# – Full Import Formatting Guide
  type: TechArticle
- description: Set date format in Excel using C# and also set cell background, apply
    foreground color, and color Excel column during import. Learn step‑by‑step.
  name: Set date format in Excel with C# – Full Import Formatting Guide
  steps:
  - name: 2.1 Set Date Format for the First Column
    text: The first column (`OrderDate`) should display as “MM/dd/yyyy”. Aspose uses
      the built‑in number format index 14 for the short date, but you can also supply
      a custom format string if you prefer.
  - name: 2.2 Set Cell Background for the Second Column
    text: Let’s give the `CustomerName` column a light blue background. This is where
      **set cell background** comes into play.
  - name: 2.3 Apply Foreground (Text) Color – Optional Extra
    text: 'If you also want the text itself to be a contrasting color, you can tweak
      the same style:'
  - name: 3.1 Save the Workbook
    text: '```csharp // Save to a file – change path as needed wb.Save("FormattedReport.xlsx",
      SaveFormat.Xlsx); Console.WriteLine("Excel file created with date format and
      colors."); ```'
  - name: What if I have more than two columns?
    text: Just expand the `columnStyles` array and assign a `Style` to each index
      you care about. Unassigned indexes will fall back to the default style, which
      is perfectly fine.
  - name: How do I format a column as currency?
    text: '```csharp columnStyles[3] = wb.CreateStyle(); columnStyles[3].Number =
      164; // Built‑in currency format (e.g., $#,##0.00) ```'
  - name: Can I change the header row style separately?
    text: 'Yes. After the import, you can grab the first row and apply a distinct
      style:'
  - name: What if the DataTable contains null dates?
    text: 'Aspose will leave those cells blank. If you prefer a placeholder like “N/A”,
      you can preprocess the table:'
  type: HowTo
tags:
- excel
- csharp
- aspnet
- data-import
title: Установите формат даты в Excel с помощью C# – Полное руководство по форматированию
  импорта
url: /ru/net/excel-custom-number-date-formatting/set-date-format-in-excel-with-c-full-import-formatting-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Установить формат даты в Excel с C# – Полное руководство по форматированию импорта

Когда‑нибудь вам нужно было **установить формат даты** в листе Excel, сгенерированном из кода C#, но при этом вы хотели задать пользовательский фон или цвет текста для столбца? Вы не одиноки. Во многих сценариях отчётности вы извлекаете `DataTable` из базы данных, помещаете её в лист и потом пытаетесь привести даты к нужному виду и сделать столбцы яркими с правильными цветами.  

В этом руководстве мы пройдём чистое, сквозное решение, которое **устанавливает формат даты**, **задаёт фон ячейки**, **применяет цвет переднего плана**, и даже **окрашивает столбец Excel** при импорте данных. К концу вы получите переиспользуемый шаблон, который обрабатывает **excel import formatting** без обычных проб и ошибок.

> **Что вам понадобится**  
> * .NET 6+ (или .NET Framework 4.7+)  
> * Aspose.Cells for .NET (бесплатная пробная версия подходит для тестирования)  
> * Источник `DataTable` – любой запрос ADO.NET подойдет  
> * Visual Studio или ваша любимая IDE  

Давайте начнём.

---

## Обзор решения

Мы разобьём задачу на три логических части:

1. **Получить исходные данные** – `DataTable` со строками, которые вы хотите экспортировать.  
2. **Создать стили, специфичные для столбцов** – один стиль для столбца даты, другой для текстового столбца, плюс любые дополнительные стили, которые вам нужны.  
3. **Импортировать таблицу со стилями** – используйте `Worksheet.Cells.ImportDataTable`, чтобы каждый столбец наследовал подготовленный стиль.  

Почему такой подход? Потому что Aspose.Cells позволяет прикрепить массив `Style` непосредственно к вызову `ImportDataTable`, что означает отсутствие необходимости во втором проходе для повторного применения форматирования. Это быстрее, менее подвержено ошибкам и делает ваш код аккуратным.

---

## Шаг 1: Получить данные для экспорта

Сначала — вам нужен `DataTable`. В реальном проекте вы, вероятно, вызовете хранимую процедуру или используете Entity Framework для её заполнения, но для иллюстрации мы смоделируем простую таблицу с датой и текстовым столбцом.

```csharp
using System;
using System.Data;
using Aspose.Cells;

DataTable GetData()
{
    var table = new DataTable();
    table.Columns.Add("OrderDate", typeof(DateTime));
    table.Columns.Add("CustomerName", typeof(string));

    // Sample rows – replace with your DB call
    table.Rows.Add(DateTime.Today.AddDays(-2), "Acme Corp");
    table.Rows.Add(DateTime.Today.AddDays(-1), "Globex Inc");
    table.Rows.Add(DateTime.Today, "Soylent Co");

    return table;
}
```

> **Pro tip:** Если ваш источник использует nullable даты, убедитесь, что тип столбца `typeof(DateTime?)` – Aspose всё равно будет учитывать назначенный позже формат.

---

## Шаг 2: Подготовить массив стилей – по одному на каждый столбец

Теперь мы создаём `Style[]`, длина которого соответствует количеству столбцов в `DataTable`. Каждая запись будет содержать форматирование для соответствующего столбца.

```csharp
// Create a new workbook and get the first worksheet
Workbook wb = new Workbook();
Worksheet ws = wb.Worksheets[0];

// Pull the data
DataTable dataTable = GetData();

// Allocate the style array
Style[] columnStyles = new Style[dataTable.Columns.Count];
```

### 2.1 Установить формат даты для первого столбца

Первый столбец (`OrderDate`) должен отображаться как “MM/dd/yyyy”. Aspose использует встроенный числовой формат с индексом 14 для короткой даты, но вы также можете задать собственную строку формата, если хотите.

```csharp
// Style for the date column (index 0)
columnStyles[0] = wb.CreateStyle();
columnStyles[0].Number = 14;               // Built‑in short date format
// Or a custom pattern:
// columnStyles[0].Custom = "mm/dd/yyyy";
```

**Почему это важно:** Excel хранит даты как серийные числа. Присвоив числовой формат, вы говорите Excel отображать эти числа как читаемые даты, а не как сырые числа.

### 2.2 Установить фон ячейки для второго столбца

Давайте зададим столбцу `CustomerName` светло‑голубой фон. Здесь в действие вступает **set cell background**.

```csharp
// Style for the text column (index 1)
columnStyles[1] = wb.CreateStyle();
columnStyles[1].ForegroundColor = System.Drawing.Color.LightBlue;
columnStyles[1].Pattern = BackgroundType.Solid; // Needed to show the color
```

> **Note:** Без установки `Pattern` в `Solid` цвет переднего плана не появится, потому что шаблон по умолчанию — “None”.

### 2.3 Применить цвет переднего плана (текст) – дополнительный вариант

Если вы также хотите, чтобы сам текст имел контрастный цвет, вы можете изменить тот же стиль:

```csharp
columnStyles[1].Font.Color = System.Drawing.Color.DarkBlue; // apply foreground color
```

Это удовлетворяет требованию **apply foreground color**, при этом оставляя фон столбца нетронутым.

---

## Шаг 3: Импортировать DataTable с определёнными стилями

С готовыми стилями последний шаг — одна строка, которая импортирует данные и применяет стили по столбцам.

```csharp
// Import the DataTable starting at cell A1 (row 0, column 0)
// includeColumnNames = true to add a header row
ws.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);
```

**Как это работает:** Aspose читает массив `columnStyles` и сопоставляет каждый `Style` с соответствующим индексом столбца. Строка заголовка наследует стиль по умолчанию, если вы не зададите отдельный стиль для строки 0.

### 3.1 Сохранить книгу

```csharp
// Save to a file – change path as needed
wb.Save("FormattedReport.xlsx", SaveFormat.Xlsx);
Console.WriteLine("Excel file created with date format and colors.");
```

Запустите программу, откройте *FormattedReport.xlsx*, и вы должны увидеть:

- **OrderDate** столбец отображается как даты (например, `06/15/2026`).  
- **CustomerName** столбец с светло‑голубой заливкой и тёмно‑синим текстом.  

Это весь процесс **excel import formatting** в менее чем 30 строках C#.

---

## Пошаговое резюме (с объяснением почему)

| Шаг | Что вы делаете | Почему это важно |
|------|----------------|-------------------|
| **Получить данные** | Вызов `GetData()` для заполнения `DataTable`. | Обеспечивает структурированный источник, который Aspose может напрямую обработать. |
| **Создать массив стилей** | Выделить `Style[]`, соответствующий количеству столбцов. | Позволяет стилизовать каждый столбец в одном вызове импорта. |
| **Установить формат даты** | `columnStyles[0].Number = 14;` | Обеспечивает корректное отображение дат в Excel. |
| **Установить цвет фона** | `ForegroundColor = LightBlue; Pattern = Solid;` | Выделяет столбец, удовлетворяя требованию **set cell background**. |
| **Применить цвет переднего плана** | `Font.Color = DarkBlue;` | Повышает читаемость и удовлетворяет требованию **apply foreground color**. |
| **Импортировать со стилями** | `ImportDataTable(..., columnStyles);` | Однопроходный импорт, который сохраняет всё форматирование. |
| **Сохранить книгу** | `wb.Save(...);` | Сохраняет результат для последующих пользователей. |

---

## Обработка граничных случаев и часто задаваемые вопросы

### Что если у меня больше двух столбцов?

Просто расширьте массив `columnStyles` и назначьте `Style` каждому индексу, который вам нужен. Не назначенные индексы будут использовать стиль по умолчанию, что полностью приемлемо.

```csharp
columnStyles[2] = wb.CreateStyle();
columnStyles[2].Number = 0; // General format for numeric columns
```

### Как отформатировать столбец как валюту?

```csharp
columnStyles[3] = wb.CreateStyle();
columnStyles[3].Number = 164; // Built‑in currency format (e.g., $#,##0.00)
```

### Можно ли изменить стиль строки заголовка отдельно?

Да. После импорта вы можете получить первую строку и применить отдельный стиль:

```csharp
Style headerStyle = wb.CreateStyle();
headerStyle.Font.IsBold = true;
headerStyle.ForegroundColor = System.Drawing.Color.Gold;
headerStyle.Pattern = BackgroundType.Solid;

ws.Cells.Rows[0].ApplyStyle(headerStyle, new StyleFlag { All = true });
```

### Что если DataTable содержит пустые даты?

Aspose оставит такие ячейки пустыми. Если вы предпочитаете заполнитель вроде “N/A”, вы можете предварительно обработать таблицу:

```csharp
foreach (DataRow row in dataTable.Rows)
{
    if (row.IsNull("OrderDate"))
        row["OrderDate"] = DateTime.MinValue; // or any sentinel
}
```

Затем настройте стиль, чтобы отображать пользовательский формат, показывающий “N/A” для специального значения.

---

## Полный рабочий пример

Ниже представлен полный готовый к копированию пример программы. Запустите его как консольное приложение, и вы получите красиво отформатированный файл Excel.



## Что вам стоит изучить дальше?

Следующие руководства охватывают тесно связанные темы, которые развивают техники, продемонстрированные в этом руководстве. Каждый ресурс включает полные рабочие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [Set Font Color in Excel Cells using Aspose.Cells for .NET](/cells/english/net/formatting/setting-font-color/)
- [Set Font Color in .NET Excel with Aspose.Cells](/cells/english/net/formatting/set-font-color-net-excel-aspose-cells/)
- [Set Excel Column Widths in Pixels Using Aspose.Cells for .NET | Step-by-Step Guide](/cells/english/net/formatting/set-excel-column-width-pixels-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}