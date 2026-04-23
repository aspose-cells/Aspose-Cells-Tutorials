---
category: general
date: 2026-03-27
description: Как создать сводную таблицу в C# с помощью Aspose.Cells – научитесь добавлять
  данные, включать обновление и сохранять книгу в формате xlsx в одном руководстве.
draft: false
keywords:
- how to create pivot
- save workbook as xlsx
- how to enable refresh
- how to add data
- generate excel file c#
language: ru
og_description: Как создать сводную таблицу в C# с помощью Aspose.Cells. Это руководство
  покажет, как добавить данные, включить обновление и сохранить книгу в формате xlsx.
og_title: Как создать сводную таблицу в C# – Полный учебник по Aspose.Cells
tags:
- Aspose.Cells
- C#
- Excel automation
title: Как создать сводную таблицу в C# – полное руководство с Aspose.Cells
url: /ru/net/creating-and-configuring-pivot-tables/how-to-create-pivot-in-c-full-guide-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как создать сводную таблицу в C# – Полный учебник Aspose.Cells

Когда‑то задумывались **как создать сводную таблицу** в C# без мучений с COM‑interop? Вы не одиноки. Во многих приложениях, работающих с данными, нужен быстрый способ превратить сырые цифры продаж в аккуратный отчёт, и Aspose.Cells делает это проще простого.  

В этом руководстве мы пройдём каждый шаг: добавление данных, построение сводной таблицы, включение автоматического обновления и, наконец, **сохранение рабочей книги как xlsx**, чтобы пользователи могли сразу открыть её в Excel. К концу вы получите готовый файл `PivotRefresh.xlsx` и чёткое понимание, зачем нужна каждая строка кода.

## Требования

- .NET 6+ (или .NET Framework 4.7.2 и новее) – любой современный рантайм подойдёт.  
- Aspose.Cells for .NET – можно установить из NuGet (`Install-Package Aspose.Cells`).  
- Базовое знакомство с синтаксисом C# – глубоких знаний Excel не требуется.

> **Pro tip:** Если вы работаете на корпоративном компьютере, убедитесь, что лицензия Aspose применена; иначе в сгенерированном файле появится водяной знак.

## Шаг 1 – Как добавить данные в новую рабочую книгу

Прежде чем появится сводная таблица, нужен источник‑таблица. Мы создадим новую рабочую книгу, назовём первый лист *SalesData* и добавим несколько строк, имитирующих реальный набор продаж.

```csharp
using Aspose.Cells;
using Aspose.Cells.Pivot;

class PivotRefreshTutorial
{
    static void Main()
    {
        // 1️⃣ Create a new workbook and grab the default sheet
        var workbook = new Workbook();
        var salesDataSheet = workbook.Worksheets[0];
        salesDataSheet.Name = "SalesData";

        // 2️⃣ Write column headers
        salesDataSheet.Cells["A1"].PutValue("Region");
        salesDataSheet.Cells["B1"].PutValue("Product");
        salesDataSheet.Cells["C1"].PutValue("Units");
        salesDataSheet.Cells["D1"].PutValue("Revenue");

        // 3️⃣ Insert a sample row – add more rows as your scenario demands
        salesDataSheet.Cells["A2"].PutValue("East");
        salesDataSheet.Cells["B2"].PutValue("Widget");
        salesDataSheet.Cells["C2"].PutValue(120);
        salesDataSheet.Cells["D2"].PutValue(5400);
```

**Почему это важно:**  
- Метод `PutValue` автоматически задаёт тип ячейки, поэтому вам не придётся позже разбираться со строками и числами.  
- Определение заголовков в строке 1 даёт движку сводных таблиц то, к чему он будет обращаться при сопоставлении полей.

## Шаг 2 – Создание листа, который будет содержать сводную таблицу

Сводная таблица размещается на отдельном листе, чтобы исходные данные оставались чистыми, а отчёт – аккуратным.

```csharp
        // 4️⃣ Add a dedicated sheet for the pivot
        var pivotSheet = workbook.Worksheets.Add("PivotReport");
```

> **Что если у вас уже есть лист?** Просто обратитесь к нему по индексу (`workbook.Worksheets["MySheet"]`) вместо создания нового.

## Шаг 3 – Определение диапазона источника (Как добавить данные → Определить диапазон)

Aspose.Cells нужен `CellArea` или строка диапазона, охватывающая и заголовки, и данные. Здесь мы предполагаем максимум 100 строк; при необходимости измените значение.

```csharp
        // 5️⃣ Build the source range (A1:D100 covers headers + up to 99 data rows)
        var sourceRange = salesDataSheet.Cells.CreateRange("A1:D100");
```

**Особый случай:** Если ваш набор данных динамический, можно вычислить последнюю заполненную строку через `salesDataSheet.Cells.MaxDataRow` и построить диапазон соответственно.

## Шаг 4 – Как создать сводную таблицу – Вставка сводной таблицы

Теперь самая интересная часть: просим Aspose.Cells создать сводную, привязанную к только что определённому диапазону.

```csharp
        // 6️⃣ Insert the pivot table at cell A3 of the pivot sheet
        int pivotIndex = pivotSheet.PivotTables.Add("=SalesData!A1:D100", "A3", "SalesPivot");
        var pivotTable = pivotSheet.PivotTables[pivotIndex];
```

Обратите внимание на ссылку в стиле формулы (`=SalesData!A1:D100`). Это тот же синтаксис, который вы вводите в Excel, поэтому API выглядит интуитивно.

## Шаг 5 – Настройка строк, столбцов и полей данных (Как добавить данные → Поля)

Мы разместим *Region* в строках, *Product* в столбцах и просуммируем как *Units*, так и *Revenue*.

```csharp
        // 7️⃣ Set up row, column, and data fields
        pivotTable.RowFields.Add(0); // 0 = first column => Region
        pivotTable.ColumnFields.Add(1); // 1 = second column => Product
        pivotTable.DataFields.Add(2, "Sum of Units", PivotTableDataAggregationType.Sum);
        pivotTable.DataFields.Add(3, "Sum of Revenue", PivotTableDataAggregationType.Sum);
```

**Почему такие индексы?**  
Aspose.Cells нумерует столбцы, начиная с 0, поэтому `0` указывает на *Region*. Метод `DataFields.Add` позволяет переименовать поле (например, “Sum of Units”) и выбрать тип агрегации – `Sum` обычно используется для числовых данных.

## Шаг 6 – Как включить обновление – Сделать сводную таблицу автообновляемой при открытии

Если исходные данные изменятся позже, скорее всего, вы захотите, чтобы сводка автоматически отразила эти изменения. Здесь в помощь `RefreshDataOnOpen`.

```csharp
        // 8️⃣ Turn on automatic refresh when the file is opened
        pivotTable.RefreshDataOnOpen = true;
```

> **Примечание:** Этот флаг работает только при открытии книги в Excel; внутри Aspose.Cells он не пересчитывается, если явно не вызвать `pivotTable.RefreshData()`.

## Шаг 7 – Сохранить рабочую книгу как XLSX (Как сохранить рабочую книгу как XLSX)

Наконец, сохраняем файл на диск. Формат `.xlsx` – современный, основанный на zip‑архиве тип файлов Excel, поддерживаемый везде.

```csharp
        // 9️⃣ Save the workbook – this also satisfies the “save workbook as xlsx” requirement
        workbook.Save("PivotRefresh.xlsx");
    }
}
```

Запуск программы создаст файл **PivotRefresh.xlsx** в папке выполнения. Откройте его в Excel, и вы увидите аккуратно оформленную сводную таблицу с строками *Region*, столбцами *Product* и суммами *Units* и *Revenue*. Поскольку мы включили автообновление, любые изменения на листе *SalesData* отразятся в сводной при следующем открытии книги.

### Ожидаемый результат

| Region | Widget | Gadget | … |
|--------|--------|--------|---|
| East   | 120    | 0      |   |
| West   | 0      | 85     |   |
| **Grand Total** | **120** | **85** |   |

*(Числа будут различаться в зависимости от добавленных строк.)*

---

## Часто задаваемые вопросы и варианты

### Что если нужно несколько сводных таблиц?

Можно повторить **Шаг 4** с другим именем и другим расположением. Каждый вызов `PivotTables.Add` возвращает новый индекс, которым можно воспользоваться для получения объекта таблицы.

### Как изменить агрегацию на *Average* вместо *Sum*?

Замените `PivotTableDataAggregationType.Sum` на `PivotTableDataAggregationType.Average` в вызовах `DataFields.Add`.

### Можно ли стилизовать сводную (шрифты, цвета)?

Да. После создания сводной можно обратиться к её свойству `Style` или применить форматирование ячеек к диапазону, содержащему сводную. Например:

```csharp
pivotTable.Style = workbook.Styles[workbook.Styles.Add()];
pivotTable.Style.Font.Color = System.Drawing.Color.DarkBlue;
```

### Можно ли добавить строки после сохранения книги?

Конечно. Загрузите файл через `new Workbook("PivotRefresh.xlsx")`, добавьте строки на лист *SalesData* и вызовите `pivotTable.RefreshData()` перед повторным сохранением.

---

## Полный рабочий пример (готов к копированию)

```csharp
using Aspose.Cells;
using Aspose.Cells.Pivot;

class PivotRefreshTutorial
{
    static void Main()
    {
        // Step 1: Create workbook & add sample data
        var workbook = new Workbook();
        var salesDataSheet = workbook.Worksheets[0];
        salesDataSheet.Name = "SalesData";

        salesDataSheet.Cells["A1"].PutValue("Region");
        salesDataSheet.Cells["B1"].PutValue("Product");
        salesDataSheet.Cells["C1"].PutValue("Units");
        salesDataSheet.Cells["D1"].PutValue("Revenue");

        // Sample rows – extend as needed
        salesDataSheet.Cells["A2"].PutValue("East");
        salesDataSheet.Cells["B2"].PutValue("Widget");
        salesDataSheet.Cells["C2"].PutValue(120);
        salesDataSheet.Cells["D2"].PutValue(5400);

        salesDataSheet.Cells["A3"].PutValue("West");
        salesDataSheet.Cells["B3"].PutValue("Gadget");
        salesDataSheet.Cells["C3"].PutValue(85);
        salesDataSheet.Cells["D3"].PutValue(4250);

        // Step 2: Add sheet for the pivot
        var pivotSheet = workbook.Worksheets.Add("PivotReport");

        // Step 3: Define source range (covers up to 100 rows)
        var sourceRange = salesDataSheet.Cells.CreateRange("A1:D100");

        // Step 4: Insert pivot table
        int pivotIndex = pivotSheet.PivotTables.Add("=SalesData!A1:D100", "A3", "SalesPivot");
        var pivotTable = pivotSheet.PivotTables[pivotIndex];

        // Step 5: Configure fields
        pivotTable.RowFields.Add(0); // Region
        pivotTable.ColumnFields.Add(1); // Product
        pivotTable.DataFields.Add(2, "Sum of Units", PivotTableDataAggregationType.Sum);
        pivotTable.DataFields.Add(3, "Sum of Revenue", PivotTableDataAggregationType.Sum);

        // Step 6: Enable automatic refresh
        pivotTable.RefreshDataOnOpen = true;

        // Step 7: Save as .xlsx
        workbook.Save("PivotRefresh.xlsx");
    }
}
```

Сохраните файл, запустите его и откройте сгенерированный **PivotRefresh.xlsx** – вы только что освоили **как создать сводную таблицу** в C#.

---

## Подведение итогов

Мы рассмотрели, **как создать сводную таблицу** программно, как **добавлять данные**, как **включать автообновление**, и наконец, как **сохранить рабочую книгу как xlsx** с помощью Aspose.Cells.  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}