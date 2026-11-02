---
category: general
date: 2026-03-27
description: Создайте Excel‑книгу в C# с помощью Aspose.Cells, примените условное
  форматирование, импортируйте DataTable в Excel и сохраните книгу в формате xlsx
  — всё в одном руководстве.
draft: false
keywords:
- create excel workbook c#
- apply conditional formatting
- import datatable to excel
- save workbook as xlsx
- create excel file programmatically
language: ru
og_description: Создайте Excel‑книгу в C# с использованием Aspose.Cells, примените
  условное форматирование, импортируйте DataTable в Excel и сохраните книгу в формате xlsx
  за несколько минут.
og_title: Создание рабочей книги Excel на C# – Полное руководство с условным форматированием
tags:
- Aspose.Cells
- C#
- Excel automation
title: Создание Excel‑книги в C# – пошаговое руководство с условным форматированием
url: /ru/net/excel-conditional-formatting/create-excel-workbook-c-step-by-step-guide-with-conditional/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание Excel‑книги C# – Полный учебный курс

Когда‑нибудь нужно было **create excel workbook c#** «на лету», но не знали, с чего начать? Вы не одиноки — многие разработчики сталкиваются с этим, когда впервые автоматизируют отчёты. В этом руководстве мы покажем, как именно создать excel workbook c# с помощью Aspose.Cells, применить условное форматирование, импортировать DataTable в Excel и, наконец, сохранить книгу в формате xlsx.  

Что вы получите в результате этого урока — готовое к запуску консольное приложение, которое генерирует красочный файл Excel, а также подробное объяснение каждой строки, чтобы вы могли адаптировать его под свои проекты. Никакой внешней документации не требуется; просто скопируйте, вставьте и запустите.  

### Предварительные требования

- .NET 6+ (или .NET Framework 4.7.2+) установлен  
- Visual Studio 2022 или любой другой редактор C# по вашему выбору  
- Aspose.Cells for .NET (можно взять бесплатный пробный пакет NuGet)  

Если всё это у вас есть, приступим.

## Create Excel Workbook C# – Инициализация книги

Первое, что нужно сделать, — **create excel workbook c#** путём создания экземпляра класса `Workbook`. Этот объект представляет всю Excel‑книгу в памяти.

```csharp
using Aspose.Cells;
using Aspose.Cells.Tables;
using System.Data;
using System.Drawing;

class SmartMarkerConditionalDemo
{
    static void Main()
    {
        // Step 1: Create a new workbook and grab the first worksheet
        Workbook workbook = new Workbook();                // <-- creates the workbook
        Worksheet worksheet = workbook.Worksheets[0];      // first sheet (Sheet1)
```

> **Почему это важно:** Класс `Workbook` абстрагирует формат файла, поэтому вам не придётся работать с низкоуровневым XML или COM‑interop. Он также сразу предоставляет доступ к стилям, таблицам и smart markers.

## Применение условного форматирования

Теперь, когда книга существует, давайте **apply conditional formatting**, чтобы выделить строки, где количество превышает 100. Условное форматирование находится на уровне листа, а не отдельной ячейки, что делает его переиспользуемым.

```csharp
        // Step 4: Apply conditional formatting to highlight quantities > 100
        int cfIndex = worksheet.ConditionalFormattings.Add();               // add a new CF collection
        var conditionalFormatting = worksheet.ConditionalFormattings[cfIndex];
        var condition = conditionalFormatting.AddCondition(
            FormatConditionType.CellValue, OperatorType.Greater, "100");   // > 100

        // Define the style that will be applied when the condition is true
        condition.Style = workbook.CreateStyle();
        condition.Style.Font.Color = Color.Red;               // red font
        condition.Style.Pattern = BackgroundType.Solid;       // solid background
        condition.Style.ForegroundColor = Color.Yellow;      // yellow fill
```

> **Pro tip:** Если нужны более сложные правила (например, между двумя значениями), просто вызовите `AddCondition` ещё раз с `OperatorType.Between`.

## Запись заголовков и smart markers

Прежде чем **import datatable to excel**, нам нужны ячейки‑заполнители — smart markers, которые библиотека заменит реальными данными. Думайте о них как о тегах‑шаблонах.

```csharp
        // Step 2: Write the header row
        worksheet.Cells["A1"].PutValue("Product");
        worksheet.Cells["B1"].PutValue("Quantity");
        worksheet.Cells["C1"].PutValue("Status");

        // Step 3: Define smart markers that will be replaced by data
        worksheet.Cells["A2"].PutValue("&=Products.ProductName");
        worksheet.Cells["B2"].PutValue("&=Products.Quantity");
        worksheet.Cells["C2"].PutValue("&=Products.Quantity > 100 ? \"High\" : \"Low\"");
```

> **Почему smart markers?** Они позволяют держать макет Excel отдельно от кода. Вы один раз оформляете лист, затем просто передаёте `DataTable`, и библиотека делает всё остальное.

## Импорт DataTable в Excel

Это ядро **import datatable to excel**. Мы создаём `DataTable`, соответствующий полям smart markers, и передаём его в `ImportDataTable`.

```csharp
        // Step 5: Build a simple DataTable that matches the smart marker fields
        DataTable products = new DataTable();
        products.Columns.Add("ProductName");
        products.Columns.Add("Quantity", typeof(int));
        products.Rows.Add("Apple", 120);
        products.Rows.Add("Banana", 80);
        products.Rows.Add("Cherry", 150);

        // Step 6: Populate the worksheet with the DataTable via smart markers
        worksheet.Cells.ImportDataTable(products, true, "A2");
```

> **Edge case:** Если в вашей таблице больше столбцов, чем нужно, просто опустите лишние столбцы в smart markers — они будут проигнорированы.

## Сохранение книги в формате XLSX

Наконец, мы **save workbook as xlsx** на диск. Метод `Save` автоматически определяет формат по расширению файла.

```csharp
        // Step 7: Save the result to an Excel file
        workbook.Save("SmartMarkersConditional.xlsx");   // <-- saves as .xlsx
    }
}
```

Это вся программа. При её запуске в папке вывода появится файл `SmartMarkersConditional.xlsx`.

### Ожидаемый результат

| Продукт | Количество | Статус |
|---------|------------|--------|
| Apple   | 120        | Высокий |
| Banana  | 80         | Низкий |
| Cherry  | 150        | Высокий |

Строки с **Quantity > 100** (Apple и Cherry) будут иметь красный текст на желтом фоне благодаря добавленному ранее условному форматированию.

## Create Excel File Programmatically – Полный список исходного кода

Ниже приведён полностью готовый к копированию исходный код. В нём содержатся все обсуждённые части, а также несколько дополнительных комментариев для ясности.

```csharp
using Aspose.Cells;
using Aspose.Cells.Tables;
using System.Data;
using System.Drawing;

class SmartMarkerConditionalDemo
{
    static void Main()
    {
        // 1️⃣ Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ Write header cells
        worksheet.Cells["A1"].PutValue("Product");
        worksheet.Cells["B1"].PutValue("Quantity");
        worksheet.Cells["C1"].PutValue("Status");

        // 3️⃣ Insert smart markers – placeholders for our data
        worksheet.Cells["A2"].PutValue("&=Products.ProductName");
        worksheet.Cells["B2"].PutValue("&=Products.Quantity");
        worksheet.Cells["C2"].PutValue("&=Products.Quantity > 100 ? \"High\" : \"Low\"");

        // 4️⃣ Apply conditional formatting (highlight >100)
        int cfIdx = worksheet.ConditionalFormattings.Add();
        var cf = worksheet.ConditionalFormattings[cfIdx];
        var cond = cf.AddCondition(FormatConditionType.CellValue, OperatorType.Greater, "100");
        cond.Style = workbook.CreateStyle();
        cond.Style.Font.Color = Color.Red;
        cond.Style.Pattern = BackgroundType.Solid;
        cond.Style.ForegroundColor = Color.Yellow;

        // 5️⃣ Build a DataTable that matches the markers
        DataTable products = new DataTable();
        products.Columns.Add("ProductName");
        products.Columns.Add("Quantity", typeof(int));
        products.Rows.Add("Apple", 120);
        products.Rows.Add("Banana", 80);
        products.Rows.Add("Cherry", 150);

        // 6️⃣ Import the DataTable – this replaces the smart markers
        worksheet.Cells.ImportDataTable(products, true, "A2");

        // 7️⃣ Save the workbook – this will create an .xlsx file
        workbook.Save("SmartMarkersConditional.xlsx");
    }
}
```

> **Tip:** Если нужно создать несколько листов, просто повторите шаги 2‑6 для нового экземпляра `Worksheet`, полученного через `workbook.Worksheets.Add()`.

## Почему стоит использовать Aspose.Cells для автоматизации Excel в C#?

- **Performance:** Работает полностью в памяти, без COM‑interop, поэтому быстро даже с большими наборами данных.  
- **Feature‑rich:** Поддерживает smart markers, условное форматирование, диаграммы, сводные таблицы и многое другое.  
- **Cross‑platform:** Работает на Windows, Linux и macOS с .NET Core/5/6+.  

Если вы застряли на какой‑то функции — например, добавлении диаграммы или защите листа — просто ищите “asp​ose.cells add chart c#” и найдёте похожий пример.

## Следующие шаги и смежные темы

- **Export to PDF:** После того как вы **create excel workbook c#**, можно мгновенно экспортировать в PDF с помощью `workbook.Save("output.pdf")`.  
- **Чтение существующих Excel‑файлов:** Используйте `new Workbook("ExistingFile.xlsx")`, чтобы изменить шаблон.  
- **Массовый импорт:** Для огромных объёмов данных рассмотрите `ImportArray` или `ImportDataTable` с `ImportOptions` для повышения скорости.  

Экспериментируйте с различными правилами условного форматирования, цветами или даже добавьте строку итогов с формулами. Возможности безграничны, когда вы **create excel file programmatically**.

---

*Готовы попробовать сами? Возьмите код, запустите его и откройте сгенерированный `SmartMarkersConditional.xlsx`. Если возникнут проблемы, оставляйте комментарий ниже — happy coding!*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}