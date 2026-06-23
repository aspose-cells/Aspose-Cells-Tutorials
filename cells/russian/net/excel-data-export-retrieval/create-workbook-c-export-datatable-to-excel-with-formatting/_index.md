---
category: general
date: 2026-02-15
description: Создайте книгу Excel на C# и экспортируйте DataTable в Excel с форматированием
  строк, задайте фон строк и автоматизируйте задачи Excel за считанные минуты.
draft: false
keywords:
- create workbook c#
- excel export formatting
- export datatable excel
- set row background
- excel automation c#
language: ru
og_description: Быстро создайте книгу Excel на C#, применяйте стили строк и автоматизируйте
  экспорт в Excel с полными примерами кода и советами по лучшим практикам.
og_title: Создание рабочей книги C# – Экспорт DataTable в Excel с форматированием
tags:
- C#
- Excel
- DataExport
title: Создать рабочую книгу C# – экспорт DataTable в Excel с форматированием
url: /ru/net/excel-data-export-retrieval/create-workbook-c-export-datatable-to-excel-with-formatting/
---

with all translations.

Check for any markdown links: none.

Check for any other text: The "Pro tip:" line we kept as is.

Check for any other bold text: "Why?" etc. We translated.

Make sure to keep the same number of headings, list items, etc.

Now produce final answer.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создать рабочую книгу C# – Экспорт DataTable в Excel с форматированием

Когда‑нибудь вам нужно было **create workbook C#** и выгрузить `DataTable` в Excel с пользовательским оформлением? Вы не одиноки. Во многих бизнес‑приложениях требуется вывести красиво отформатированную таблицу, которую нетехнический пользователь может открыть и сразу понять.  

В этом руководстве мы пройдем полностью готовое к запуску решение, которое покажет вам **how to create workbook C#**, применит **excel export formatting**, задаст **row background**, и использует **excel automation c#** для создания отшлифованного файла. Никаких расплывчатых «см. документацию» — только полный код, объяснения, почему каждая строка важна, и советы, которые вы действительно сможете использовать уже завтра.

---

## Предварительные требования

- .NET 6 (или .NET Framework 4.6+).  
- Visual Studio 2022 или любой IDE, совместимый с C#.  
- Пакет NuGet **Aspose.Cells for .NET** (или любая библиотека, предоставляющая `Workbook`, `Worksheet`, `Style`).  
- Базовое знакомство с `DataTable`.  

Если у вас ещё нет Aspose.Cells, выполните:

```bash
dotnet add package Aspose.Cells
```

> **Pro tip:** Бесплатная пробная версия работает для большинства сценариев разработки; просто не забудьте заменить лицензионный ключ перед выпуском.

![Пример создания рабочей книги C# с оформленными строками в Excel]( "Пример создания рабочей книги C# с цветными фонами строк")

---

## Шаг 1: Инициализация Workbook и Worksheet (Create Workbook C#)

Первое, что вам нужно сделать, — создать экземпляр `Workbook`. Представьте это как открытие совершенно нового файла Excel в памяти.

```csharp
using Aspose.Cells;
using System;
using System.Data;

class ExcelExporter
{
    static void Main()
    {
        // Create a new workbook – this is the core of create workbook C#
        var workbook = new Workbook();

        // Grab the first worksheet (index 0) – it's already there by default
        var worksheet = workbook.Worksheets[0];

        // The rest of the steps will fill this worksheet with data and styling
        ExportDataTableWithStyling(workbook, worksheet);
    }
}
```

**Почему?**  
`Workbook` содержит весь документ Excel, а `Worksheet` представляет отдельную вкладку. Начало с чистой рабочей книги гарантирует контроль над каждым аспектом вывода — никаких скрытых стилей по умолчанию.

---

## Шаг 2: Подготовка образца DataTable (Export DataTable Excel)

В реальном проекте вы бы получали данные из базы данных, но для демонстрации мы создадим небольшую `DataTable` «на лету».

```csharp
private static DataTable GetSampleData()
{
    var dt = new DataTable("Employees");
    dt.Columns.Add("Id", typeof(int));
    dt.Columns.Add("Name", typeof(string));
    dt.Columns.Add("Department", typeof(string));
    dt.Columns.Add("Salary", typeof(decimal));

    dt.Rows.Add(1, "Alice Johnson", "Finance", 72000);
    dt.Rows.Add(2, "Bob Smith", "IT", 68000);
    dt.Rows.Add(3, "Charlie Lee", "HR", 59000);
    dt.Rows.Add(4, "Diana Prince", "Marketing", 75000);

    return dt;
}
```

**Почему это важно:**  
Экспорт `DataTable` — самый распространённый способ перенести табличные данные из приложения в Excel. Представленный метод полностью автономен, поэтому вы можете скопировать‑вставить его в любой проект, и он будет работать.

---

## Шаг 3: Создание стиля для каждой строки (Excel Export Formatting)

Чтобы задать каждой строке свой цвет фона, мы создаём объект `Style` для каждой строки в `DataTable`. Здесь **excel export formatting** проявляет свою силу.

```csharp
private static Style[] BuildRowStyles(Workbook workbook, int rowCount)
{
    var styles = new Style[rowCount];

    // Define a palette of background colors – feel free to extend
    var colors = new[] { System.Drawing.Color.LightYellow,
                         System.Drawing.Color.LightCyan,
                         System.Drawing.Color.LightGreen,
                         System.Drawing.Color.LightPink };

    for (int i = 0; i < rowCount; i++)
    {
        // Create a fresh style instance
        var style = workbook.CreateStyle();

        // Cycle through our color array so rows get alternating shades
        style.ForegroundColor = colors[i % colors.Length];
        style.Pattern = BackgroundType.Solid;

        // Optional: make the font a little bolder for readability
        style.Font.IsBold = true;

        styles[i] = style;
    }

    return styles;
}
```

**Почему стилизация по строкам?**  
Если нужно выделить определённые записи (например, просроченные счета), вы можете заменить простой цикл цветов условной логикой — просто задайте `style.ForegroundColor` в зависимости от данных строки.

---

## Шаг 4: Импорт DataTable со стилями строк (Set Row Background)

Теперь мы объединяем всё: данные, рабочую книгу и стили.

```csharp
private static void ExportDataTableWithStyling(Workbook workbook, Worksheet worksheet)
{
    // 1️⃣ Get the data
    DataTable dt = GetSampleData();

    // 2️⃣ Build a style for each row
    Style[] rowStyles = BuildRowStyles(workbook, dt.Rows.Count);

    // 3️⃣ Import the DataTable starting at cell A1.
    //    The `true` flag tells Aspose.Cells to include column headers.
    worksheet.Cells.ImportDataTable(dt, true, "A1", rowStyles);

    // 4️⃣ Save the workbook to disk
    string outputPath = "EmployeesReport.xlsx";
    workbook.Save(outputPath);
    Console.WriteLine($"Workbook saved to {outputPath}");
}
```

**Что вы увидите:**  
При открытии `EmployeesReport.xlsx` заголовочная строка будет в формате по умолчанию, а далее четыре строки данных, каждая окрашена в светлый цвет фона. Результат выглядит как вручную созданный отчёт, а не как скучный дамп.

---

## Шаг 5: Продвинутые советы по Excel Automation C# (Excel Automation C#)

Ниже представлены несколько быстрых приёмов, которые вы можете добавить к базовому примеру:

| Совет | Фрагмент кода | Когда использовать |
|-----|--------------|-------------|
| **Авто‑подгонка столбцов** | `worksheet.AutoFitColumns();` | После импорта данных, чтобы избежать обрезки текста. |
| **Заморозить строку заголовка** | `worksheet.WindowPane.SplitRows = 1;` | Когда таблица может прокручиваться за пределы экрана. |
| **Условное форматирование** | <details><summary>Показать</summary>```csharp\nvar cf = worksheet.ConditionalFormattings[0];\ncf.AddCondition(FormatConditionType.CellValue, OperatorType.GreaterThan, "70000");\ncf.Style.ForegroundColor = System.Drawing.Color.LightSalmon;\ncf.Style.Pattern = BackgroundType.Solid;\n```</details> | Выделить зарплаты выше порога. |
| **Защитить лист** | `worksheet.Protect(ProtectionType.All, "myPassword");` | Когда нужны отчёты только для чтения. |

Эти фрагменты демонстрируют широту возможностей **excel automation c#** — вы можете продолжать расширять рабочую книгу, не переписывая основную логику импорта.

---

## Часто задаваемые вопросы и крайние случаи

**Что если DataTable содержит тысячи строк?**  
Aspose.Cells эффективно передаёт данные потоково, но вы можете отключить создание стилей для каждой строки, чтобы сэкономить память. Вместо этого примените один стиль к диапазону:

```csharp
var range = worksheet.Cells.CreateRange(1, dt.Rows.Count, 0, dt.Columns.Count);
range.SetStyle(rowStyles[0]); // reuse one style for the whole block
```

**Можно ли экспортировать в .csv вместо .xlsx?**  
Конечно — просто измените формат сохранения:

```csharp
workbook.Save("EmployeesReport.csv", SaveFormat.Csv);
```

Оформление будет потеряно (CSV не поддерживает стили), но экспорт данных останется тем же.

**Работает ли это на .NET Core?**  
Да. Aspose.Cells поддерживает .NET Standard 2.0 и более новые версии, поэтому тот же код работает на .NET 6, .NET 7 или .NET Framework.

---

## Полный рабочий пример (Готовый к копированию)

```csharp
using Aspose.Cells;
using System;
using System.Data;

class ExcelExporter
{
    static void Main()
    {
        // 1️⃣ Create a new workbook – core of create workbook C#
        var workbook = new Workbook();
        var worksheet = workbook.Worksheets[0];

        // 2️⃣ Export DataTable with styling
        ExportDataTableWithStyling(workbook, worksheet);
    }

    private static DataTable GetSampleData()
    {
        var dt = new DataTable("Employees");
        dt.Columns.Add("Id", typeof(int));
        dt.Columns.Add("Name", typeof(string));
        dt.Columns.Add("Department", typeof(string));
        dt.Columns.Add("Salary", typeof(decimal));

        dt.Rows.Add(1, "Alice Johnson", "Finance", 72000);
        dt.Rows.Add(2, "Bob Smith", "IT", 68000);
        dt.Rows.Add(3, "Charlie Lee", "HR", 59000);
        dt.Rows.Add(4, "Diana Prince", "Marketing", 75000);
        return dt;
    }

    private static Style[] BuildRowStyles(Workbook workbook, int rowCount)
    {
        var styles = new Style[rowCount];
        var colors = new[]
        {
            System.Drawing.Color.LightYellow,
            System.Drawing.Color.LightCyan,
            System.Drawing.Color.LightGreen,
            System.Drawing.Color.LightPink
        };

        for (int i = 0; i < rowCount; i++)
        {
            var style = workbook.CreateStyle();
            style.ForegroundColor = colors[i % colors.Length];
            style.Pattern = BackgroundType.Solid;
            style.Font.IsBold = true;
            styles[i] = style;
        }

        return styles;
    }

    private static void ExportDataTableWithStyling(Workbook workbook, Worksheet worksheet)
    {
        DataTable dt = GetSampleData();
        Style[] rowStyles = BuildRowStyles(workbook, dt.Rows.Count);

        // Import with row styles – sets row background (set row background)
        worksheet.Cells.ImportDataTable(dt, true, "A1", rowStyles);

        // Optional polish
        worksheet.AutoFitColumns();

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}