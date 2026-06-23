---
category: general
date: 2026-06-05
description: Создайте книгу Excel на C# быстро и узнайте, как задать числовой формат
  ячейки, экспортировать ячейку Excel и преобразовать значение ячейки в строку с точностью
  до двух знаков после запятой.
draft: false
keywords:
- create excel workbook
- set cell number format
- format number with two decimals
- how to export excel cell
- convert cell value to string
language: ru
og_description: Создайте книгу Excel на C# и освоите настройку числового формата ячеек,
  экспорт ячейки Excel в строку и форматирование чисел с двумя знаками после запятой.
og_title: Создание Excel‑книги в C# – Полное пошаговое руководство
schemas:
- author: Aspose
  dateModified: '2026-06-05'
  description: Create Excel workbook in C# quickly and learn how to set cell number
    format, export Excel cell, and convert cell value to string with two‑decimal precision.
  headline: Create Excel Workbook in C# – Complete Programming Guide
  type: TechArticle
- description: Create Excel workbook in C# quickly and learn how to set cell number
    format, export Excel cell, and convert cell value to string with two‑decimal precision.
  name: Create Excel Workbook in C# – Complete Programming Guide
  steps:
  - name: What if the cell already has a style?
    text: The `GetStyle` method returns a copy of the existing style, so any previous
      formatting (font, color, etc.) is retained. You only overwrite the `Custom`
      property, leaving everything else untouched.
  - name: How does culture affect the decimal separator?
    text: 'Aspose.Cells respects the thread’s `CultureInfo`. If you need a comma instead
      of a dot, set:'
  - name: Can I export a range of cells at once?
    text: Yes—use `Worksheet.ExportDataTable` or `Worksheet.ExportString` with a range
      address. The `ExportTableOptions` you defined for a single cell can be reused
      for the whole range.
  - name: What if I don’t want the value rounded but truncated?
    text: 'Change the custom format to `"0.00"` with a rounding mode, or manually
      truncate before putting the value:'
  type: HowTo
tags:
- C#
- Excel
- Aspose.Cells
title: Создание Excel‑книги в C# — Полное руководство по программированию
url: /ru/net/excel-workbook/create-excel-workbook-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание Excel Workbook в C# – Полное руководство по программированию

Когда‑нибудь задумывались, как **создать Excel workbook** в C# без борьбы с COM‑interop или грязными CSV‑трюками? Вы не одиноки. Многие разработчики нуждаются в чистом, .NET‑native способе создать файл .xlsx, поместить число в ячейку и затем экспортировать это значение в красиво отформатированную строку.  

В этом руководстве мы пройдём всё это — начнём с пустой книги, зададим числовой формат ячейки, отформатируем число с двумя знаками после запятой и, наконец, узнаем **как экспортировать данные Excel cell** в виде строки. В конце вы также увидите, как **преобразовать значение ячейки в строку** без потери точности.

> **Подсказка:** Подход ниже использует библиотеку **Aspose.Cells for .NET**, которая является проверенной в боевых условиях, коммерческой API. Если вам нужен бесплатный вариант, EPPlus или ClosedXML работают аналогично, но фрагменты кода будут немного отличаться.

## Предварительные требования

- .NET 6.0 SDK (или любая недавняя версия .NET) установлен.
- Visual Studio 2022 или VS Code с расширением C#.
- Пакет NuGet **Aspose.Cells** (`Install-Package Aspose.Cells`).

Других зависимостей не требуется — всё остальное находится внутри библиотеки.

## Шаг 1: Установите Aspose.Cells и настройте проект

Откройте терминал (или консоль диспетчера пакетов) и выполните:

```powershell
dotnet new console -n ExcelDemo
cd ExcelDemo
dotnet add package Aspose.Cells
```

Это создаст новое консольное приложение с именем `ExcelDemo` и подключит сборку `Aspose.Cells`.  

Почему этот шаг важен: без библиотеки вы не сможете **создать Excel workbook** объекты или управлять ячейками типобезопасным способом.

## Шаг 2: Создайте Workbook и получите первый Worksheet

Теперь откройте `Program.cs` и замените исходный код фрагментом ниже. Он показывает самую первую вещь, которую вы делаете, когда **создаёте Excel workbook** — создаёте экземпляр класса `Workbook` и получаете ссылку на лист по умолчанию.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 2: Create a workbook and get the first worksheet
        Workbook workbook = new Workbook();               // creates a new .xlsx in memory
        Worksheet ws = workbook.Worksheets[0];           // first (default) sheet

        // The rest of the steps will follow here...
```

> **Почему?** Объект `Workbook` — это представление Excel‑файла в памяти. По умолчанию он содержит один лист, к которому мы обращаемся через индекс, начинающийся с нуля.

## Шаг 3: Поместите числовое значение в конкретную ячейку

Давайте выберем строку 5, столбец 2 (индексы, начинающиеся с нуля) и вставим десятичное число. Это продемонстрирует **format number with two decimals** позже.

```csharp
        // Step 3: Access the cell at row 5, column 2 (zero‑based) and insert a number
        Cell cell = ws.Cells[5, 2];          // corresponds to cell C6 in Excel UI
        cell.PutValue(12345.6789);          // raw value with many decimal places
```

Метод `PutValue` сохраняет сырое значение double. На данный момент Excel будет показывать полную точность, если мы не применим формат.

## Шаг 4: Установите числовой формат ячейки (два знака после запятой)

Здесь мы **устанавливаем числовой формат ячейки**. Мы используем объект `Style` для определения пользовательского числового формата `"0.00"` — ровно два знака после запятой.

```csharp
        // Step 4: Apply a number format to show only two decimal places
        Style style = cell.GetStyle();               // clone existing style
        style.Custom = "0.00";                       // forces two digits after the dot
        cell.SetStyle(style);                        // apply the style back to the cell
```

Зачем использовать стиль вместо преобразования в строку? Сохраняя ячейку как числовой тип, мы сохраняем её вычислимость (можно суммировать, усреднять и т.д.), одновременно отображая именно то, что нужно.

## Шаг 5: Экспортируйте значение ячейки как отформатированную строку

Иногда вам нужно получить **how to export excel cell** значение в виде простого текста — возможно, записать его в лог‑файл или отправить через веб‑API. Aspose.Cells позволяет прикрепить параметры экспорта к ячейке, указывая библиотеке отобразить значение как строку с тем же числовым форматом.

```csharp
        // Step 5: Configure export options to get the formatted string
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,          // forces string output
            NumberFormat = "0.00"           // matches the style we set earlier
        };
        cell.ExportOptions = exportOptions; // attach options to the cell
```

## Шаг 6: Получите отформатированную строку (Convert Cell Value to String)

Давайте действительно выполним экспорт и посмотрим результат. Метод `ExportString` возвращает содержимое ячейки как строку, применяя любые `ExportTableOptions`, которые мы прикрепили.

```csharp
        // Step 6: Export the cell as a formatted string
        string formattedValue = cell.ExportString();
        Console.WriteLine($"Formatted cell value: {formattedValue}");
```

При запуске программы консоль выводит:

```
Formatted cell value: 12345.68
```

Обратите внимание на округление с `12345.6789` до `12345.68` — это результат **format number with two decimals**.

## Шаг 7: (Опционально) Сохраните Workbook на диск

Если вы также хотите увидеть результат в реальном файле `.xlsx`, просто вызовите `Save`:

```csharp
        // Optional: write the workbook to a file so you can open it in Excel
        workbook.Save("DemoWorkbook.xlsx");
    }
}
```

Открытие `DemoWorkbook.xlsx` показывает то же число в ячейке **C6**, отформатированное с двумя знаками после запятой.

## Пограничные случаи и часто задаваемые вопросы

### Что если у ячейки уже есть стиль?

Метод `GetStyle` возвращает копию существующего стиля, поэтому любое предыдущее форматирование (шрифт, цвет и т.д.) сохраняется. Вы перезаписываете только свойство `Custom`, оставляя всё остальное нетронутым.

### Как культура влияет на разделитель десятичных?

Aspose.Cells учитывает `CultureInfo` потока. Если вам нужна запятая вместо точки, установите:

```csharp
System.Threading.Thread.CurrentThread.CurrentCulture = new System.Globalization.CultureInfo("fr-FR");
```

Тот же формат `"0.00"` теперь отобразит `12 345,68`.

### Можно ли экспортировать диапазон ячеек сразу?

Да — используйте `Worksheet.ExportDataTable` или `Worksheet.ExportString` с адресом диапазона. `ExportTableOptions`, определённые для одной ячейки, можно переиспользовать для всего диапазона.

### Что если я не хочу округление, а усечение?

Измените пользовательский формат на `"0.00"` с режимом усечения, или вручную усеките значение перед вставкой:

```csharp
double raw = Math.Truncate(12345.6789 * 100) / 100; // yields 12345.67
cell.PutValue(raw);
```

## Полный рабочий пример (готовый к копированию и вставке)

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 2: Create a workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet ws = workbook.Worksheets[0];

        // Step 3: Access the cell at row 5, column 2 (zero‑based) and insert a number
        Cell cell = ws.Cells[5, 2];
        cell.PutValue(12345.6789);

        // Step 4: Apply a number format to show only two decimal places
        Style style = cell.GetStyle();
        style.Custom = "0.00";
        cell.SetStyle(style);

        // Step 5: Configure export options to get the formatted string
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            NumberFormat = "0.00"
        };
        cell.ExportOptions = exportOptions;

        // Step 6: Export the cell as a formatted string
        string formattedValue = cell.ExportString();
        Console.WriteLine($"Formatted cell value: {formattedValue}");

        // Optional: save the workbook for visual verification
        workbook.Save("DemoWorkbook.xlsx");
    }
}
```

**Ожидаемый вывод в консоль**

```
Formatted cell value: 12345.68
```

Откройте `DemoWorkbook.xlsx` → перейдите к ячейке **C6** → вы увидите то же число с двумя знаками после запятой.

## Заключение

Мы только что рассмотрели всё, что вам нужно, чтобы **create Excel workbook** в C#, **set cell number format**, **format number with two decimals**, понять **how to export Excel cell** данные и **convert cell value to string** для последующей обработки.  

Ключевые выводы:

1. Используйте `Workbook` и `Worksheet` для создания Excel‑файла в памяти.  
2. Примените пользовательский стиль (`"0.00"`), чтобы обеспечить отображение с двумя знаками после запятой.  
3. Прикрепите `ExportTableOptions` к ячейке, когда вам нужна строковое представление, сохраняющее тот же формат.  

Отсюда вы можете экспериментировать — добавлять новые ячейки, применять условное форматирование или даже создавать диаграммы. Если вам интересны стили шрифтов или добавление формул, ознакомьтесь с документацией Aspose.Cells по **cell styling** и **formula evaluation**.

Есть дополнительные вопросы по автоматизации Excel в C#? Оставьте комментарий, и удачной разработки!

## Что изучать дальше?

Следующие руководства охватывают тесно связанные темы, которые развивают техники, продемонстрированные в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [Мастер операций с Workbook в Aspose.Cells .NET: загрузка Excel‑файлов и отслеживание предшествующих ячеек](/cells/english/net/workbook-operations/aspose-cells-net-master-workbook-operations/)
- [Мастер форматирования ячеек Excel и управления Workbook с Aspose.Cells для .NET](/cells/english/net/formatting/excel-formatting-aspose-cells-net/)
- [Мастер Aspose.Cells для .NET: продвинутое управление Excel Workbook и ячейками](/cells/english/net/advanced-features/excel-aspose-cells-net-create-manage/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}