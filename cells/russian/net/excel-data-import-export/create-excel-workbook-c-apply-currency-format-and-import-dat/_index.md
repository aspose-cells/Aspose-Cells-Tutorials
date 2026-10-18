---
category: general
date: 2026-03-30
description: Создайте Excel‑книгу в C# с форматированием валюты. Узнайте, как импортировать
  DataTable, добавить числовой формат в Excel и применить валютный формат к столбцу
  за несколько минут.
draft: false
keywords:
- create excel workbook c#
- format cells currency
- import datatable to excel
- add number format excel
- apply currency format column
language: ru
og_description: Создайте рабочую книгу Excel на C# и мгновенно отформатируйте ячейки
  как валюту. Этот пошаговый учебник показывает, как импортировать DataTable в Excel
  и добавить числовой формат для столбца.
og_title: Создание книги Excel на C# – Руководство по форматированию валют
tags:
- Aspose.Cells
- C#
- Excel automation
title: Создание книги Excel на C# – применение валютного формата и импорт DataTable
url: /ru/net/excel-data-import-export/create-excel-workbook-c-apply-currency-format-and-import-dat/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание Excel‑книги C# – Применение формата валюты и импорт DataTable

Когда‑нибудь нужно **создать Excel‑книгу C#**, которая сразу выглядит как готовый отчёт? Может быть, вы вытягиваете данные о продажах из базы и хотите, чтобы столбец цены отображался в долларах без ручных правок в Excel. Знакомо? Вы не одиноки — большинство разработчиков сталкиваются с этой проблемой, когда впервые автоматизируют экспорт в Excel.

В этом руководстве мы пройдём полный, готовый к запуску пример, который **создаёт Excel‑книгу C#**, импортирует `DataTable` и **форматирует столбец Price как валюту**. В конце у вас будет файл `StyledTable.xlsx`, который можно открыть и увидеть красиво отформатированные числа. Дополнительная пост‑обработка не требуется.

> **Что вы узнаете**
> - Как настроить Aspose.Cells в проекте .NET  
> - Как **import datatable to excel** с массивом стилей  
> - Как **add number format excel** для конкретного столбца  
> - Советы по работе с большим количеством столбцов или разными локалями  

> **Требования**
> - .NET 6+ (или .NET Framework 4.6+) установлен
> - NuGet‑пакет Aspose.Cells for .NET (`Install-Package Aspose.Cells`)
> - Базовые знания C# и DataTable  

---

## Шаг 1: Подготовьте DataTable (import datatable to excel)

Сначала нам нужны некоторые примерные данные. В реальном приложении вы, скорее всего, заполняете эту таблицу запросом к БД, но жёстко закодированный пример упрощает задачу.

```csharp
using System.Data;

// Create a DataTable with two columns: Product (string) and Price (double)
DataTable dataTable = new DataTable();
dataTable.Columns.Add("Product", typeof(string));
dataTable.Columns.Add("Price", typeof(double));

// Add a few rows – you can add as many as you like
dataTable.Rows.Add("Apple", 1.23);
dataTable.Rows.Add("Banana", 0.78);
dataTable.Rows.Add("Cherry", 2.50);
```

*Почему это важно*: `DataTable` служит мостом между вашими бизнес‑данными и файлом Excel. Aspose.Cells может импортировать её напрямую, сохраняя имена столбцов и типы данных.

---

## Шаг 2: Создайте новую книгу (create excel workbook c#)

Теперь создаём объект Excel‑файла. Представьте его как чистый холст, на котором вы будете рисовать.

```csharp
using Aspose.Cells;

// Instantiate a fresh workbook – this is the core of create excel workbook c#
Workbook workbook = new Workbook();

// Grab the first worksheet (index 0). You could also add more sheets later.
Worksheet worksheet = workbook.Worksheets[0];
```

> **Pro tip:** Если нужны несколько листов, вызовите `workbook.Worksheets.Add()` и задайте каждому осмысленное имя.

---

## Шаг 3: Определите стиль валюты (format cells currency)

Aspose.Cells позволяет создать объект `Style`, описывающий внешний вид ячеек. Для валюты используем встроенный номер формата 164 (`"$#,##0.00"`).

```csharp
// Create a new style object for the price column
Style priceStyle = workbook.CreateStyle();
priceStyle.Number = 164; // Built‑in currency format "$#,##0.00"
```

*Почему не просто задать строку формата?* Использование встроенного ID гарантирует совместимость между версиями Excel и избавляет от проблем, связанных с локалью.

---

## Шаг 4: Сформируйте массив стилей (apply currency format column)

При импорте `DataTable` можно передать массив объектов `Style` — один на каждый столбец. `null` означает «использовать стиль по умолчанию». Здесь мы применяем `priceStyle` только ко второму столбцу.

```csharp
// Column 0 (Product) gets the default style, Column 1 (Price) gets the currency style
Style[] columnStyles = { null, priceStyle };
```

Если позже добавятся новые столбцы, просто расширьте массив. Длина `columnStyles` должна совпадать с количеством импортируемых столбцов, иначе Aspose бросит исключение.

---

## Шаг 5: Импортируйте DataTable со стилями (import datatable to excel)

Теперь происходит магия — наш `DataTable` попадает на лист, и столбец цены сразу отображается как валюта.

```csharp
// Parameters:
//  - dataTable: source data
//  - true: include column headers
//  - startRow: 0 (top of sheet)
//  - startColumn: 0 (first column)
//  - columnStyles: style array defined above
worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);
```

*Что делать, если столбцов больше двух?* Просто расширьте `columnStyles`, чтобы каждый столбец получил нужный стиль (или `null` для стиля по умолчанию). Это самый чистый способ **add number format excel** выборочно.

---

## Шаг 6: Сохраните книгу (create excel workbook c#)

Наконец, записываем файл на диск. Выберите любую папку, в которую у вас есть права записи.

```csharp
// Save the workbook as an XLSX file
workbook.Save("YOUR_DIRECTORY/StyledTable.xlsx");
```

Откройте `StyledTable.xlsx` в Excel, и вы увидите:

| Product | Price |
|---------|-------|
| Apple   | $1.23 |
| Banana  | $0.78 |
| Cherry  | $2.50 |

Столбец **Price** уже отформатирован как валюта — никаких дополнительных шагов не требуется.

---

## Особые случаи и варианты

### Больше столбцов, разные форматы

Если нужно **format cells currency** для нескольких столбцов (например, Cost, Tax, Total), создайте отдельный `Style` для каждого и заполните `columnStyles` соответственно:

```csharp
Style costStyle = workbook.CreateStyle();
costStyle.Number = 164; // currency

Style taxStyle = workbook.CreateStyle();
taxStyle.Number = 164;

// Assuming columns: Product, Cost, Tax, Total
Style[] styles = { null, costStyle, taxStyle, priceStyle };
worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, styles);
```

### Валюта, зависящая от локали

Для евро или британского фунта используйте другие встроенные ID (например, 165 для `€#,##0.00`). Либо задайте пользовательскую строку формата:

```csharp
priceStyle.Custom = "€#,##0.00";
```

### Большие наборы данных

Aspose.Cells справляется с миллионами строк, но потребление памяти растёт вместе с объектами стилей. Переиспользуйте один экземпляр `Style` для всех валютных столбцов, чтобы снизить нагрузку.

### Отсутствующие стили

Если `columnStyles` короче, чем количество столбцов, Aspose применит стиль по умолчанию к оставшимся столбцам. Это удобно, когда интересуют только отдельные столбцы.

---

## Полный рабочий пример (все шаги вместе)

Ниже представлена полная программа, которую можно скопировать в консольное приложение. В ней собраны все обсуждённые части и несколько полезных комментариев.

```csharp
using Aspose.Cells;
using System;
using System.Data;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Build sample DataTable (import datatable to excel)
        // -------------------------------------------------
        DataTable dataTable = new DataTable();
        dataTable.Columns.Add("Product", typeof(string));
        dataTable.Columns.Add("Price", typeof(double));
        dataTable.Rows.Add("Apple", 1.23);
        dataTable.Rows.Add("Banana", 0.78);
        dataTable.Rows.Add("Cherry", 2.50);
        // You can add as many rows as you like here.

        // -------------------------------------------------
        // Step 2: Create a new workbook (create excel workbook c#)
        // -------------------------------------------------
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // -------------------------------------------------
        // Step 3: Define a currency style (format cells currency)
        // -------------------------------------------------
        Style priceStyle = workbook.CreateStyle();
        priceStyle.Number = 164; // "$#,##0.00" – built‑in currency format

        // -------------------------------------------------
        // Step 4: Build the style array (apply currency format column)
        // -------------------------------------------------
        // First column gets default style (null), second column uses priceStyle.
        Style[] columnStyles = { null, priceStyle };

        // -------------------------------------------------
        // Step 5: Import the DataTable with the style array
        // -------------------------------------------------
        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);

        // -------------------------------------------------
        // Step 6: Save the workbook to disk
        // -------------------------------------------------
        string outputPath = @"YOUR_DIRECTORY\StyledTable.xlsx";
        workbook.Save(outputPath);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

**Ожидаемый результат:** При открытии `StyledTable.xlsx` столбец `Price` будет отображаться с долларовым знаком и двумя знаками после запятой, точно как требует инструкция **format cells currency**.

---

## Часто задаваемые вопросы

**В: Работает ли это с .NET Core?**  
О: Абсолютно. Aspose.Cells совместим с .NET‑standard, поэтому можно целиться в .NET 5, .NET 6 и выше без изменений.

**В: Что если в моём DataTable 10 столбцов, а форматировать нужно только столбец 5?**  
О: Создайте `Style[]` длиной 10, заполните позиции 0‑4 и 6‑9 `null`, а в индекс 4 (нумерация с нуля) поместите ваш кастомный стиль. Aspose учтёт каждое значение.

**В: Можно ли скрыть строку заголовков?**  
О: После импорта задайте `worksheet.Cells.Rows[0].Hidden = true;` или просто передайте `false` в параметр `includeColumnNames` метода `ImportDataTable`.

---

## Заключение

Мы только что **создали Excel‑книгу C#**, импортировали `DataTable` и **применили формат валюты к столбцу** с помощью Aspose.Cells. Основные шаги — подготовка данных, определение стиля, построение массива стилей, импорт через `ImportDataTable` и сохранение — покрывают ядро большинства задач автоматизации Excel.

Дальше вы можете исследовать:

- **add number format excel** для дат или процентов  
- Экспорт нескольких листов в один файл  
- Использование **format cells currency** с символами разных локалей  
- Автоматизацию создания диаграмм на основе тех же данных  

Попробуйте, и вы быстро станете «гуру» по Excel‑отчётности в своей команде. Есть свои находки? Оставляйте комментарий ниже — happy coding!  

![create excel workbook c# screenshot](image.png "create excel workbook c#")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}