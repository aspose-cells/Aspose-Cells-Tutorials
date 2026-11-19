---
category: general
date: 2026-11-19
description: Установить формат валюты в Excel с помощью C# – узнайте, как задать числовой
  формат и стиль столбцов Excel при импорте листа Excel.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set currency format
- how to set number format
- assign number format
- excel worksheet import
- style excel columns
language: ru
lastmod: 2026-11-19
og_description: Установите валютный формат в Excel с помощью C# и узнайте, как задать
  числовой формат, присвоить его и оформить столбцы Excel при импорте листа.
og_image_alt: Screenshot showing Excel cells formatted as currency after import
og_title: Установить формат валюты в Excel с помощью C# – полное пошаговое руководство
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: Set currency format in Excel with C# – learn how to set number format
    and style excel columns during an excel worksheet import.
  headline: Set currency format while importing data into Excel using C#
  type: TechArticle
- description: Set currency format in Excel with C# – learn how to set number format
    and style excel columns during an excel worksheet import.
  name: Set currency format while importing data into Excel using C#
  steps:
  - name: Expected result
    text: 'When you open **FinancialReport.xlsx**, you’ll see:'
  - name: Assign number format to date columns
    text: '```csharp // Suppose column 2 contains dates and you want "dd-MMM-yyyy"
      columnStyles[2].Number = 14; // 14 = built‑in short date ```'
  - name: Use custom number formats for percentages
    text: '```csharp columnStyles[3].Custom = "0.00%"; // Shows 0.75 as 75.00% ```'
  - name: Styling beyond number formats
    text: 'You can also set font, background color, or alignment on the same `Style`
      object:'
  type: HowTo
tags:
- C#
- Excel
- DataTable
- Aspose.Cells
- Formatting
title: Установить формат валюты при импорте данных в Excel с помощью C#
url: /ru/net/excel-custom-number-date-formatting/set-currency-format-while-importing-data-into-excel-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Установить формат валюты при импорте данных в Excel с помощью C#

Если вам нужно **установить формат валюты** в листе Excel, это руководство покажет, как **задать числовой формат** и оформить столбцы во время **импорта листа Excel**. Вы увидите полностью готовый, исполняемый пример, который присваивает правильный числовой формат каждому столбцу `DataTable` и импортирует данные с требуемым оформлением.

Работа с Excel из C# часто требует не только выгрузки сырых значений — необходимо также контролировать, как числа отображаются. Будь то генерация счетов, финансовых отчётов или дашбордов, правильное форматирование валют, процентов или дат делает вывод сразу читаемым.

## Требования

Прежде чем начать, убедитесь, что у вас есть:

* .NET 6.0 (или новее) установлен.
* Ссылка на **Aspose.Cells for .NET** (или любую библиотеку, предоставляющую класс `Style` с свойством `Number`).  
  *NuGet*: `Install-Package Aspose.Cells`.
* Базовое знакомство с `DataTable` и коллекциями C#.
* IDE, например Visual Studio 2022 или VS Code.

## Шаг 1: Получить данные, которые будут записаны в лист

Сначала получите `DataTable`, содержащий исходные данные, которые нужно экспортировать. В реальных проектах они могут поступать из запроса к базе данных, вызова API или парсера CSV.

```csharp
using System.Data;

/// <summary>
/// Returns a sample DataTable with three columns:
/// Id (int), Amount (decimal), and Description (string).
/// </summary>
DataTable GetData()
{
    var table = new DataTable();
    table.Columns.Add("Id", typeof(int));
    table.Columns.Add("Amount", typeof(decimal));
    table.Columns.Add("Description", typeof(string));

    // Sample rows
    table.Rows.Add(1, 1234.56m, "Office supplies");
    table.Rows.Add(2, 98765.43m, "Consulting fees");
    table.Rows.Add(3, 0.99m, "Miscellaneous");

    return table;
}

// Retrieve the data
DataTable dataTable = GetData();
```

> **Почему это важно:** Импорт полностью заполненного `DataTable` позволяет отделить логику получения данных от логики генерации Excel, что повышает тестируемость и поддерживаемость.

## Шаг 2: Создать массив стилей — по одной записи на каждый столбец в DataTable

Aspose.Cells ожидает массив `Style[]`, длина которого соответствует количеству столбцов, которые вы планируете импортировать. Каждый элемент может хранить конкретный числовой формат.

```csharp
// Allocate a Style object for each column
Style[] columnStyles = new Style[dataTable.Columns.Count];

// Initialize each Style instance (required before assigning properties)
for (int i = 0; i < columnStyles.Length; i++)
{
    columnStyles[i] = ws.Workbook.CreateStyle();
}
```

> **Совет:** Даже если форматировать нужно лишь часть столбцов, всё равно необходимо создать экземпляр `Style` для каждого столбца; иначе при импорте возникнет `NullReferenceException`.

## Шаг 3: Присвоить числовой формат нужным столбцам

Встроенные номера стилей различаются в зависимости от библиотеки. В Aspose.Cells:

* `0` → General (целое)  
* `2` → Currency (например, `$#,##0.00`)  
* `3` → Date и т.д.

Здесь мы **присваиваем числовой формат** двум столбцам: первый столбец (Id) остаётся целым, а второй столбец (Amount) получает формат валюты.

```csharp
// Column 0 → integer format (style number 0)
columnStyles[0].Number = 0;

// Column 1 → currency format (style number 2)
columnStyles[1].Number = 2;

// If you need a custom format, you can also use a format string:
// columnStyles[1].Custom = "$#,##0.00";
```

> **Как задать числовой формат:** Использование свойства `Number` — самый быстрый способ выбрать встроенный формат. Для локализованных валют рассмотрите возможность использования пользовательской строки формата с нужным символом валюты.

## Шаг 4: Импортировать DataTable в лист, применив стили столбцов

Теперь, когда массив стилей готов, импортируем данные. Метод `ImportDataTable` учитывает переданные стили.

```csharp
// Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();
Worksheet ws = workbook.Worksheets[0];

// Import the DataTable, starting at cell A1 (row 0, column 0)
// The third argument (true) tells the method to write column headers.
ws.Cells.ImportDataTable(
    dataTable,
    /* includeColumnNames */ true,
    /* startRow */ 0,
    /* startColumn */ 0,
    columnStyles);

// Save the workbook
workbook.Save("FinancialReport.xlsx", SaveFormat.Xlsx);
```

### Ожидаемый результат

При открытии **FinancialReport.xlsx** вы увидите:

| Id | Amount      | Description      |
|----|------------|------------------|
| 1  | $1,234.56  | Office supplies |
| 2  | $98,765.43 | Consulting fees |
| 3  | $0.99      | Miscellaneous    |

*Столбец **Amount** отображается с установленным форматом валюты, тогда как **Id** остаётся целым числом.*

## Как задать числовой формат для дополнительных сценариев

### Присвоить числовой формат столбцам дат

```csharp
// Suppose column 2 contains dates and you want "dd-MMM-yyyy"
columnStyles[2].Number = 14; // 14 = built‑in short date
```

### Использовать пользовательские форматы для процентов

```csharp
columnStyles[3].Custom = "0.00%"; // Shows 0.75 as 75.00%
```

### Оформление помимо числовых форматов

Вы также можете задать шрифт, цвет фона или выравнивание в том же объекте `Style`:

```csharp
columnStyles[1].Font.IsBold = true;
columnStyles[1].ForegroundColor = Color.LightYellow;
columnStyles[1].HorizontalAlignment = TextAlignmentType.Center;
```

> **Почему это работает:** Объект `Style` агрегирует все визуальные свойства ячейки. Когда вы передаёте массив в `ImportDataTable`, каждая ячейка автоматически наследует определённый стиль.

## Распространённые подводные камни и как их избежать

| Проблема | Симптом | Решение |
|----------|---------|---------|
| Не создан экземпляр каждого `Style` | `NullReferenceException` при импорте | Пройтись по массиву в цикле и вызвать `CreateStyle()` перед установкой свойств. |
| Использован неверный встроенный номер формата | Неправильный вид (например, даты отображаются как целые) | Обратиться к документации библиотеки за правильными константами `Number`. |
| Не сохранена рабочая книга | Нет выходного файла или файл пустой | Вызвать `workbook.Save(...)` после завершения импорта. |
| Несоответствие локали для символа валюты | `$` отображается даже в не‑американских локалях | Использовать пользовательскую строку формата с нужным символом (например, `"€#,##0.00"`). |

## Полный, исполняемый пример



## Что изучать дальше?

Следующие руководства охватывают тесно связанные темы, расширяющие техники, продемонстрированные в этом пособии. Каждый ресурс содержит полностью работающие примеры кода с пошаговыми объяснениями, помогающие освоить дополнительные возможности API и исследовать альтернативные подходы в ваших проектах.

- [Create excel file c# – style cells and set currency format](/cells/english/net/excel-formatting-and-styling/create-excel-file-c-style-cells-and-set-currency-format/)
- [How to Format Excel Columns in C# – Complete Guide](/cells/english/net/formatting-rows-and-columns-in-excel/how-to-format-excel-columns-in-c-complete-guide/)
- [Create Excel Workbook C# – Apply Currency Format and Import DataTable](/cells/english/net/excel-data-import-export/create-excel-workbook-c-apply-currency-format-and-import-dat/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}