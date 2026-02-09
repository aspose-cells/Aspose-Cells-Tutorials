---
category: general
date: 2026-02-09
description: Как создать рабочую книгу в C# со светло‑голубым фоном и импортировать
  данные с заголовками. Узнайте, как добавить светло‑голубой фон, использовать стиль
  Excel по умолчанию и импортировать DataTable.
draft: false
keywords:
- how to create workbook
- add light blue background
- import data with headers
- excel import datatable c#
- use default style excel
language: ru
og_description: Как создать книгу Excel в C# со светло-голубым фоном, импортировать
  данные с заголовками и применить стиль Excel по умолчанию — всё в одном кратком
  руководстве.
og_title: Как создать рабочую книгу – светло‑голубой фон, импорт данных
tags:
- C#
- Excel
- Aspose.Cells
title: Как создать рабочую книгу — светло‑голубой фон, импорт данных
url: /ru/net/excel-data-import-export/how-to-create-workbook-light-blue-background-data-import/
---

Date" maybe keep as is because it's a column name. But we can translate "ID", "Name", "HireDate", "Salary" maybe keep English as they are column names. The instruction says keep technical terms in English, but these are not technical terms, they are data labels. Could translate to Russian equivalents: "ID", "Имя", "Дата найма", "Зарплата". However the example shows "Name (light‑blue)" etc. Might be okay to translate. But to be safe, translate visible text, keep code terms unchanged. So translate table headers.

Also bullet points after table.

- Edge Cases headings.

- All other text.

Make sure we keep markdown formatting.

Let's craft translation.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как создать книгу Excel – светло‑голубой фон, импорт данных

Когда‑нибудь задумывались **как создать книгу Excel** в C#, которая выглядела бы чуть красивее «из коробки»? Возможно, вы получили `DataTable` из базы данных и устали от скучных, по‑умолчанию белых ячеек. В этом руководстве мы пройдёмся по созданию новой книги, добавлению светло‑голубого фона к столбцу и импорту данных с заголовками — всё это с использованием стандартного стиля, который предоставляет Excel.

Мы также добавим несколько сценариев «что‑если», например обработку `null`‑значений или стилизацию более чем одного столбца. К концу вы получите полностью оформленный файл Excel, готовый к отправке заинтересованным сторонам без дополнительной пост‑обработки.

## Предварительные требования

Прежде чем начать, убедитесь, что у вас есть:

* **.NET 6+** (код также работает на .NET Framework 4.6+)  
* **Aspose.Cells for .NET** – библиотека, обеспечивающая работу классов `Workbook`, `Style` и метода `ImportDataTable`. Установите её через NuGet:  

  ```bash
  dotnet add package Aspose.Cells
  ```

* Источник `DataTable` – в примере мы создадим его искусственно, но вы можете заменить его любой ADO.NET‑запросом.

Все готово? Отлично, приступим.

## Шаг 1: Инициализировать новую книгу (Primary Keyword)

Первое, что нужно сделать, – **how to create workbook** – буквально. Класс `Workbook` представляет весь файл Excel, а его конструктор даёт чистый лист.

```csharp
using Aspose.Cells;
using System;
using System.Data;
using System.Drawing;

namespace ExcelStylingDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create a new workbook (or obtain an existing one)
            Workbook workbook = new Workbook();   // <-- this is how to create workbook
```

> **Почему это важно:** Создание новой `Workbook` с нуля гарантирует, что вы контролируете каждый стиль с самого начала. Если открыть существующий файл, вы унаследуете все стили, оставленные предыдущим автором, что может привести к несогласованному форматированию.

## Шаг 2: Подготовить `DataTable`, который будете импортировать

Для иллюстрации создадим простой `DataTable`. В реальных проектах вы, скорее всего, будете вызывать хранимую процедуру или метод ORM.

```csharp
            // Step 2: Retrieve the data you want to import (e.g., from a database)
            DataTable dataTable = GetSampleData(); // replace with your own GetData()
```

```csharp
        // Helper method that returns a dummy DataTable
        static DataTable GetSampleData()
        {
            DataTable table = new DataTable("Employees");
            table.Columns.Add("ID", typeof(int));
            table.Columns.Add("Name", typeof(string));
            table.Columns.Add("HireDate", typeof(DateTime));
            table.Columns.Add("Salary", typeof(decimal));

            table.Rows.Add(1, "Alice Johnson", new DateTime(2020, 5, 12), 72000);
            table.Rows.Add(2, "Bob Smith", new DateTime(2019, 3, 4), 68000);
            table.Rows.Add(3, "Carol White", DBNull.Value, 75000); // demonstrates a null value
            return table;
        }
```

> **Подсказка:** Если необходимо точно сохранить порядок столбцов, как он задан в базе данных, установите параметр `importColumnNames` метода `ImportDataTable` в `true`. Это заставит Aspose.Cells записать заголовки столбцов за вас.

## Шаг 3: Определить стили столбцов – по умолчанию + светло‑голубой фон

Теперь решаем задачу **add light blue background**. Aspose.Cells позволяет передать массив объектов `Style`, соответствующий каждому импортируемому столбцу. Первый элемент — стиль для столбца 0, второй — для столбца 1 и т.д. Если стилей меньше, чем столбцов, оставшиеся столбцы используют стиль по умолчанию.

```csharp
            // Step 3: Define column styles – the default style and a custom style with a light‑blue foreground
            Style defaultStyle = workbook.DefaultStyle; // this is the use default style excel
            Style lightBlueStyle = workbook.CreateStyle();
            lightBlueStyle.ForegroundColor = Color.LightBlue;
            lightBlueStyle.Pattern = BackgroundType.Solid; // make sure the color shows

            // Apply default style to the first column, light blue to the second column
            Style[] columnStyles = { defaultStyle, lightBlueStyle };
```

> **Почему только два стиля?** В нашем примере четыре столбца, но мы хотим выделить только второй столбец (Name). Длина массива не обязана совпадать с количеством столбцов; любые отсутствующие элементы автоматически наследуют стиль книги по умолчанию.

## Шаг 4: Импортировать `DataTable` с заголовками и стилями

Здесь мы объединяем **excel import datatable c#** и **import data with headers**. Метод `ImportDataTable` делает всю тяжёлую работу: записывает имена столбцов, строки и применяет массив стилей, который мы только что создали.

```csharp
            // Step 4: Import the DataTable into the first worksheet starting at cell A1, applying the styles
            Worksheet sheet = workbook.Worksheets[0];
            sheet.Cells.ImportDataTable(dataTable, // the source DataTable
                                        true,       // import column names as headers
                                        0,          // start row (0‑based)
                                        0,          // start column (0‑based)
                                        columnStyles);
```

### Ожидаемый результат

После выполнения программы объект `workbook` будет содержать один лист, выглядящий так:

| **ID** | **Имя** (светло‑голубой) | **Дата найма** | **Зарплата** |
|-------|--------------------------|----------------|--------------|
| 1     | Alice Johnson            | 5/12/2020      | 72000        |
| 2     | Bob Smith                | 3/4/2019       | 68000        |
| 3     | Carol White              | *(пусто)*      | 75000        |

* Столбец **Имя** имеет светло‑голубой фон, что подтверждает работу массива стилей.
* Заголовки столбцов созданы автоматически, потому что мы передали `true` для `importColumnNames`.
* `null`‑значения отображаются как пустые ячейки — это поведение по умолчанию в Aspose.Cells.

## Шаг 5: Сохранить книгу (необязательно, но полезно)

Вероятно, вы захотите записать файл на диск или отправить его клиенту через поток. Сохранение простое:

```csharp
            // Step 5: Save the workbook to a file
            string outputPath = "StyledEmployees.xlsx";
            workbook.Save(outputPath, SaveFormat.Xlsx);
            Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

> **Профессиональный совет:** Если вы ориентируетесь на более старые версии Excel, замените `SaveFormat.Xlsx` на `SaveFormat.Xls`. API выполнит конвертацию за вас.

## Пограничные случаи и варианты

### Несколько стилизованных столбцов

Если требуется стилизовать более одного столбца, просто расширьте массив `columnStyles`:

```csharp
Style[] columnStyles = { defaultStyle, lightBlueStyle, defaultStyle, lightBlueStyle };
```

Теперь и **Имя**, и **Зарплата** будут светло‑голубыми.

### Условное форматирование вместо фиксированных стилей

Иногда нужно, чтобы столбец становился красным, когда значение превышает порог. Здесь на помощь приходит **use default style excel** в сочетании с условным форматированием:

```csharp
int salaryColIdx = 3; // zero‑based index for Salary column
FormatCondition condition = sheet.ConditionalFormattings[0]
    .AddCondition(FormatConditionType.CellValue, OperatorType.GreaterThan, "70000");
condition.Style.ForegroundColor = Color.LightCoral;
condition.Style.Pattern = BackgroundType.Solid;
```

### Импорт без заголовков

Если ваша downstream‑система уже поставляет собственные заголовки, передайте `false` в аргумент `importColumnNames`. Данные начнутся с `A1`, а заголовки можно добавить вручную позже.

```csharp
sheet.Cells.ImportDataTable(dataTable, false, 1, 0); // start at row 2 (index 1)
```

## Полный рабочий пример (All

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}