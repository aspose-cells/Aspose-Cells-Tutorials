---
category: general
date: 2026-03-01
description: Импортируйте данные с форматированием в Excel с помощью C#. Узнайте,
  как импортировать DataTable в Excel и добавить фоновый цвет ячейкам всего за несколько
  шагов.
draft: false
keywords:
- import data with formatting
- how to import datatable into excel
- add background color to excel cells
language: ru
og_description: Импорт данных с форматированием в Excel с помощью C#. Пошаговое руководство,
  показывающее, как импортировать DataTable и добавить цвет фона ячейкам.
og_title: Импорт данных с форматированием в Excel – руководство по C#
tags:
- C#
- Excel
- DataTable
- Formatting
title: Импорт данных с форматированием в Excel с использованием C#
url: /ru/net/excel-data-import-export/import-data-with-formatting-into-excel-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Импорт данных с форматированием в Excel с помощью C#

Когда‑нибудь вам нужно было **импортировать данные с форматированием** в книгу Excel, но вы получали обычный, скучный лист? Вы не одиноки. Большинство разработчиков сталкиваются с этой проблемой, когда обнаруживают, что импорт по умолчанию удаляет все цвета и стили, которые они тщательно настроили в исходных данных.

В этом руководстве мы пройдём полный, готовый к запуску пример, который **импортирует DataTable в Excel** и **добавляет цвет фона ячейкам Excel** одновременно. Дополнительная пост‑обработка не требуется — ваша таблица будет выглядеть точно так, как вы хотите, сразу после создания.

## Что вы узнаете

- Как получить данные в `DataTable`.
- Как определить массив объектов `Style`, содержащих цвета фона.
- Как вызвать `ImportDataTable` с этими стилями, чтобы импорт сохранял форматирование.
- Полный, готовый к запуску пример, который можно вставить в консольное приложение и сразу увидеть результат.
- Советы, подводные камни и варианты для реальных проектов.

### Требования

- .NET 6.0 или новее (код также работает с .NET Framework 4.6+).
- Библиотека **GemBox.Spreadsheet** (бесплатной версии достаточно для демонстрации).
- Базовое знакомство с C# и концепциями Excel.

Если вы задаётесь вопросом *почему GemBox?* — потому что она предоставляет однострочный метод `ImportDataTable`, принимающий массивы стилей, именно то, что нам нужно для **импорта данных с форматированием** без написания цикла.

---

## Шаг 1: Настройте проект и добавьте GemBox.Spreadsheet

Чтобы начать, создайте новое консольное приложение:

```bash
dotnet new console -n ExcelImportDemo
cd ExcelImportDemo
dotnet add package GemBox.Spreadsheet
```

> **Pro tip:** Бесплатная версия ограничивает листы 150 k ячейками, чего более чем достаточно для демонстраций. Если вы достигнете лимита, перейдите на платную версию или используйте EPPlus, но API будет выглядеть немного иначе.

## Шаг 2: Получите исходные данные как `DataTable`

Первое, что нам нужно — это `DataTable`, имитирующая данные, которые обычно извлекаются из базы данных. Вот небольшой помощник, который создаёт её в памяти:

```csharp
using System;
using System.Data;
using System.Drawing;
using GemBox.Spreadsheet;

class Program
{
    static void Main()
    {
        // Register the free license (remove for paid version).
        SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

        // 1️⃣ Retrieve the source data as a DataTable.
        DataTable dataTable = GetSampleData();

        // Remaining steps will follow...
    }

    /// <summary>
    /// Generates a sample DataTable with three columns and five rows.
    /// In a real app you’d replace this with a DB call.
    /// </summary>
    static DataTable GetSampleData()
    {
        var table = new DataTable("Report");
        table.Columns.Add("ID", typeof(int));
        table.Columns.Add("Name", typeof(string));
        table.Columns.Add("Score", typeof(double));

        table.Rows.Add(1, "Alice", 93.5);
        table.Rows.Add(2, "Bob", 78.0);
        table.Rows.Add(3, "Charlie", 85.2);
        table.Rows.Add(4, "Diana", 91.3);
        table.Rows.Add(5, "Ethan", 67.8);

        return table;
    }
}
```

**Почему это важно:** Разделяя получение данных в отдельный метод, вы можете заменить любой источник — SQL, CSV, веб‑службу — без изменения логики импорта. Это делает код чистым и делает руководство **how to import datatable into excel** переиспользуемым.

## Шаг 3: Определите стили, которые нужно применить

Теперь начинается интересная часть: мы создадим массив объектов `Style`, каждый с отдельным `ForegroundColor`. GemBox позволяет задавать `BackgroundPatternColor` (заливка ячейки) и `ForegroundColor` (цвет текста). Для этой демонстрации мы окрасим первые два столбца по‑разному.

```csharp
        // 2️⃣ Define the styles to apply to the imported cells.
        Style[] importStyles = new Style[]
        {
            new Style() { BackgroundPatternColor = Color.LightBlue },   // Column 0 – Light blue fill
            new Style() { BackgroundPatternColor = Color.LightGreen }   // Column 1 – Light green fill
            // No style for column 2 – it will keep the default look.
        };
```

**Пояснение:**  
- Объекты `Style` — лёгкие контейнеры; не нужно создавать новый объект для каждой ячейки.  
- Выравнивая порядок массива с порядком столбцов, GemBox автоматически применяет соответствующий стиль во время импорта.  
- Это ключ к **import data with formatting** — форматирование переходит вместе с данными, а не после.

## Шаг 4: Импортируйте `DataTable` в лист с применением стилей

Когда данные и стили готовы, мы можем создать рабочую книгу, выбрать первый лист и вызвать `ImportDataTable`. Сигнатура метода выглядит так:

```csharp
public void ImportDataTable(
    DataTable dataTable,
    bool includeColumnNames,
    int startRow,
    int startColumn,
    Style[] columnStyles = null);
```

Вот как мы её используем:

```csharp
        // 3️⃣ Create a new workbook and import the DataTable.
        var workbook = new ExcelFile();
        var worksheet = workbook.Worksheets.Add("Report");

        // Import, include column headers, start at A1 (0,0), apply our styles.
        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, importStyles);

        // Save the file to disk.
        workbook.Save("Report.xlsx");

        Console.WriteLine("Excel file 'Report.xlsx' created with formatted data.");
```

**Что происходит «под капотом»?**  
- `true` указывает GemBox записать имена столбцов в первой строке.  
- `0, 0` позиционирует импорт в ячейку A1.  
- `importStyles` связывает каждый столбец с цветами, определёнными ранее.  

Когда вы откроете *Report.xlsx*, столбец **ID** будет подсвечен светло‑голубым, столбец **Name** — светло‑зеленым, а столбец **Score** останется без изменений. Это **import data with formatting** в одном вызове.

## Шаг 5: Проверьте результат (ожидаемый вывод)

Откройте сгенерированный `Report.xlsx`. Вы должны увидеть примерно следующее:

| ID (светло‑голубой) | Name (светло‑зеленый) | Score |
|---------------------|-----------------------|-------|
| 1                   | Alice                 | 93.5 |
| 2                   | Bob                   | 78.0 |
| 3                   | Charlie               | 85.2 |
| 4                   | Diana                 | 91.3 |
| 5                   | Ethan                 | 67.8 |

- Ячейки столбца **ID** имеют светло‑голубой фон.  
- Ячейки столбца **Name** имеют светло‑зеленый фон.  
- Столбец **Score** остаётся с фоном по умолчанию (белый).

![Лист Excel, показывающий импорт данных с форматированием – столбец ID светло‑голубой, столбец Name светло‑зеленый](excel-screenshot.png "пример импорта данных с форматированием")

*Текст alt изображения включает основной ключевой запрос для SEO.*

## Часто задаваемые вопросы и особые случаи

### Можно ли применить не только цвета фона?

Конечно. `Style` позволяет задавать шрифты, границы, числовые форматы и даже условное форматирование. Например, чтобы сделать оценки выше 90 жирными и красными:

```csharp
Style highScoreStyle = new Style()
{
    FontColor = Color.Red,
    FontBold = true
};
worksheet.Cells["C2:C6"].ConditionalFormatting.Add(
    ConditionalFormattingCondition.GreaterThan, "90", highScoreStyle);
```

### Что если в моём `DataTable` больше столбцов, чем стилей?

GemBox применит стили только к тем столбцам, для которых есть соответствующий элемент в массиве. Остальные столбцы получат стиль по умолчанию — ошибка не будет выброшена.

### Работает ли это с большими наборами данных?

Да, но следите за лимитом бесплатной версии (150 k ячеек). Для огромных отчётов рассмотрите платную лицензию или потоковую запись данных построчно с помощью `worksheet.Cells[row, col].Value = …` — хотя тогда вы потеряете удобство однострочного вызова.

### Как импортировать данные с форматированием из существующего шаблона Excel?

Сначала можно загрузить шаблон рабочей книги:

```csharp
var template = ExcelFile.Load("Template.xlsx");
var targetSheet = template.Worksheets[0];
targetSheet.Cells.ImportDataTable(dataTable, true, 5, 2, importStyles);
template.Save("FilledReport.xlsx");
```

Это позволяет сохранить логотипы в заголовках, нижние колонтитулы и любые предустановленные стили, одновременно **import data with formatting** для динамической части.

## Полный рабочий пример (готовый к копированию и вставке)

```csharp
using System;
using System.Data;
using System.Drawing;
using GemBox.Spreadsheet;

class Program
{
    static void Main()
    {
        // Register free license key.
        SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

        // 1️⃣ Get the source data.
        DataTable dataTable = GetSampleData();

        // 2️⃣ Define column styles (background colors).
        Style[] importStyles = new Style[]
        {
            new Style() { BackgroundPatternColor = Color.LightBlue },   // ID column
            new Style() { BackgroundPatternColor = Color.LightGreen }   // Name column
            // Score column gets default style.
        };

        // 3️⃣ Create workbook and import with styles.
        var workbook = new ExcelFile();
        var worksheet = workbook.Worksheets.Add("Report");

        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, importStyles);

        // Save the result.
        workbook.Save("Report.xlsx");

        Console.WriteLine("Report.xlsx created – import data with formatting complete.");
    }

    static DataTable GetSampleData()
    {
        var table = new DataTable("Report");
        table.Columns.Add("ID", typeof(int));
        table.Columns.Add("Name", typeof(string));
        table.Columns.Add("Score", typeof(double));

        table.Rows.Add(1, "Alice", 93.5);
        table.Rows.Add(2, "Bob", 78.0);
        table.Rows.Add(3, "Charlie", 85.2);
        table.Rows.Add(4, "Diana", 91.3);
        table.Rows.Add(5, "Ethan", 67.8);

        return table;
    }
}
```

Запустите программу (`dotnet run`) и откройте сгенерированный *Report.xlsx*, чтобы увидеть сразу применённые цвета.

## Заключение

Теперь у вас есть надёжный, конец

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}