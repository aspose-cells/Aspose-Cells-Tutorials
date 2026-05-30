---
category: general
date: 2026-05-30
description: Измените размер шрифта текстового поля в Excel с помощью C#. Узнайте,
  как быстро изменить шрифт текстового поля в Excel с пошаговым кодом.
draft: false
keywords:
- change textbox font size
- modify excel textbox font
language: ru
og_description: Измените размер шрифта текстового поля в Excel с помощью C#. Это руководство
  показывает, как безопасно и эффективно изменить шрифт текстового поля в Excel.
og_title: Изменение размера шрифта текстового поля в Excel с помощью C# – Полный учебник
schemas:
- author: Aspose
  dateModified: '2026-05-30'
  description: Change textbox font size in Excel using C#. Learn how to modify excel
    textbox font quickly with step‑by‑step code.
  headline: Change Textbox Font Size in Excel with C# – Complete Guide
  type: TechArticle
- description: Change textbox font size in Excel using C#. Learn how to modify excel
    textbox font quickly with step‑by‑step code.
  name: Change Textbox Font Size in Excel with C# – Complete Guide
  steps:
  - name: Why this matters
    text: Opening the workbook via COM gives us a live object model—meaning any change
      we make reflects instantly in the file. Setting `Visible = false` speeds things
      up and avoids popping windows during automation.
  - name: Why we use `TextFrame2`
    text: '`TextFrame2` is the newer object model introduced with Office 2007. It
      supports advanced typographic features and is generally more reliable than the
      older `TextFrame`. Using it ensures our **change textbox font size** operation
      works across modern Excel versions.'
  - name: 1. Change *all* textboxes on a sheet
    text: '```csharp foreach (Excel.Shape s in xlWorksheet.Shapes) { if (s.Type.HasFlag(Excel.MsoShapeType.msoTextBox))
      { var tr = s.TextFrame2.TextRange; tr.Font.Name = fontName; tr.Font.Size = newSize;
      } } ```'
  - name: 2. Identify a textbox by its **Name** instead of index
    text: 'If you gave your textbox a meaningful name (e.g., “TitleBox”), you can
      fetch it directly:'
  type: HowTo
tags:
- Excel Interop
- C#
- Office Automation
title: Изменение размера шрифта текстового поля в Excel с помощью C# – Полное руководство
url: /ru/net/excel-shape-text-modifications/change-textbox-font-size-in-excel-with-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Изменение размера шрифта текстового поля в Excel с помощью C# – Полное руководство

Нужно **изменить размер шрифта текстового поля** в листе Excel с помощью C#? Вы попали по адресу. Независимо от того, генерируете ли вы отчёты, создаёте панель мониторинга или просто подправляете шаблон, настройка внешнего вида текстового поля может сделать вашу таблицу гораздо более профессиональной.

В этом руководстве мы также **изменим шрифт текстового поля в Excel** не только размером — речь идёт о семействе шрифтов, полужирном начертании и даже работе с несколькими фигурами. К концу вы получите готовый к запуску фрагмент кода, охватывающий каждый этап процесса, от открытия книги до очистки COM‑объектов. Без лишних слов, только практический код, который вы можете сразу добавить в свой проект.

## Необходимые условия — Что понадобится

Прежде чем приступать, убедитесь, что на вашем компьютере установлено следующее:

| Требование | Зачем это нужно |
|-------------|----------------|
| **.NET 6+** (or .NET Framework 4.7.2+) | Обеспечивает компилятор C# и среду выполнения. |
| **Microsoft.Office.Interop.Excel** NuGet package | Предоставляет типы COM‑interop, необходимые для взаимодействия с Excel. |
| **Excel установлен** (any recent version) | Слой Interop работает только при наличии приложения Office. |
| **Базовые знания C#** | Вы сможете легко следовать, но мы объясним каждую строку. |

Если чего‑то не хватает, остановитесь и установите это сейчас; остальная часть руководства предполагает, что всё уже готово.

## Шаг 1: Настройка проекта и импорт пространств имён

Для начала создайте новое консольное приложение (или интегрируйте код в существующее) и подключите пространство имён interop.

```csharp
using System;
using Excel = Microsoft.Office.Interop.Excel;

namespace ExcelTextboxDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll call the helper method that does the heavy lifting.
            ChangeTextboxFontSize(@"C:\Temp\Sample.xlsx", "Sheet1", 0, 14, "Calibri");
        }
    }
}
```

> **Совет:** Если вы нацелены на .NET 6+, добавьте пакет `Microsoft.Office.Interop.Excel` с помощью `dotnet add package Microsoft.Office.Interop.Excel`. Это гарантирует правильное разрешение псевдонима `Excel`.

## Шаг 2: Открытие книги и получение целевого листа

Теперь нам нужно запустить Excel, открыть файл и перейти к листу, содержащему текстовое поле. Оборачивание этого кода в блок `try/finally` гарантирует освобождение COM‑объектов даже в случае ошибки.

```csharp
static void ChangeTextboxFontSize(string workbookPath,
                                  string sheetName,
                                  int textboxIndex,
                                  double newSize,
                                  string fontName)
{
    Excel.Application xlApp = null;
    Excel.Workbook xlWorkbook = null;
    Excel.Worksheet xlWorksheet = null;

    try
    {
        xlApp = new Excel.Application
        {
            // Keep Excel hidden; set to true if you want to watch the changes.
            Visible = false,
            DisplayAlerts = false
        };

        xlWorkbook = xlApp.Workbooks.Open(workbookPath);
        xlWorksheet = xlWorkbook.Worksheets[sheetName] as Excel.Worksheet;
        if (xlWorksheet == null)
            throw new ArgumentException($"Worksheet '{sheetName}' not found.");
```

### Почему это важно

Открытие книги через COM предоставляет живую объектную модель — любые изменения сразу отражаются в файле. Установка `Visible = false` ускоряет процесс и предотвращает появление окон во время автоматизации.

## Шаг 3: Получение формы текстового поля

Excel рассматривает текстовые поля как объекты `Shape` в коллекции `Shapes`, а не как отдельную коллекцию `TextBox`. Поэтому код ниже выглядит немного иначе, чем фрагмент, который вы могли увидеть в интернете.

```csharp
        // Excel stores all drawing objects (including textboxes) in the Shapes collection.
        Excel.Shapes shapes = xlWorksheet.Shapes;

        // Guard against an out‑of‑range index.
        if (textboxIndex < 0 || textboxIndex >= shapes.Count)
            throw new IndexOutOfRangeException("Textbox index is out of range.");

        // Grab the specific shape; we assume it’s a textbox.
        Excel.Shape textboxShape = shapes.Item(textboxIndex + 1); // COM collections are 1‑based.
        if (!textboxShape.Type.HasFlag(Excel.MsoShapeType.msoTextBox))
            throw new InvalidOperationException("Selected shape is not a textbox.");
```

> **Внимание:** Коллекция `Shapes` индексируется с 1, поэтому мы добавляем `+1` к нулевому индексу `textboxIndex`, который вы передаёте. Пропуск этого приводит к ошибкам «индекс вне диапазона», которые сложно отлаживать.

## Шаг 4: Изменение размера шрифта (и имени) текстового поля

Здесь мы наконец **изменяем размер шрифта текстового поля**. Свойство `TextFrame2` предоставляет доступ к параметрам форматирования rich‑text, включая `Font.Name` и `Font.Size`.

```csharp
        // Access the text range inside the textbox.
        Excel.TextRange2 textRange = textboxShape.TextFrame2.TextRange;

        // Change the font name – this also “modifies excel textbox font”.
        textRange.Font.Name = fontName;

        // Change the font size – the core of our tutorial.
        textRange.Font.Size = newSize;

        // Optional: make the text bold for extra emphasis.
        // textRange.Font.Bold = Microsoft.Office.Core.MsoTriState.msoTrue;
```

### Почему мы используем `TextFrame2`

`TextFrame2` — более новая модель объектов, появившаяся в Office 2007. Она поддерживает расширенные типографические возможности и, как правило, надёжнее старого `TextFrame`. Использование её гарантирует, что операция **изменения размера шрифта текстового поля** будет работать в современных версиях Excel.

## Шаг 5: Сохранение, очистка и проверка

После изменения шрифта необходимо сохранить изменения и освободить все ссылки COM. Пропуск очистки может оставить «осиротевшие» процессы Excel, работающие в фоне.

```csharp
        // Save the workbook – you can also use SaveAs to create a copy.
        xlWorkbook.Save();

        Console.WriteLine($"Successfully changed textbox font size to {newSize} pt and font to '{fontName}'.");
    }
    catch (Exception ex)
    {
        Console.Error.WriteLine($"Error: {ex.Message}");
    }
    finally
    {
        // Release COM objects in reverse order of creation.
        if (xlWorksheet != null) System.Runtime.InteropServices.Marshal.ReleaseComObject(xlWorksheet);
        if (xlWorkbook != null)
        {
            xlWorkbook.Close(false);
            System.Runtime.InteropServices.Marshal.ReleaseComObject(xlWorkbook);
        }
        if (xlApp != null)
        {
            xlApp.Quit();
            System.Runtime.InteropServices.Marshal.ReleaseComObject(xlApp);
        }

        // Force garbage collection to clean up any remaining RCWs.
        GC.Collect();
        GC.WaitForPendingFinalizers();
    }
}
```

> **Совет:** Если вам нужно **изменять шрифт текстового поля в Excel** на многих листах, оберните внутреннюю логику в цикл, проходящий по `Workbook.Worksheets`. Только не забудьте сбрасывать `textboxIndex` для каждого листа.

## Обработка особых случаев — Несколько текстовых полей и отсутствие фигур

В реальных таблицах редко встречается только одно текстовое поле. Ниже представлены две быстрые стратегии, которые можно применить без переписывания всего метода.

### 1. Изменить *все* текстовые поля на листе

```csharp
foreach (Excel.Shape s in xlWorksheet.Shapes)
{
    if (s.Type.HasFlag(Excel.MsoShapeType.msoTextBox))
    {
        var tr = s.TextFrame2.TextRange;
        tr.Font.Name = fontName;
        tr.Font.Size = newSize;
    }
}
```

### 2. Определить текстовое поле по его **Name** вместо индекса

Если вы задали текстовому полю осмысленное имя (например, “TitleBox”), его можно получить напрямую:

```csharp
Excel.Shape namedBox = xlWorksheet.Shapes.Item("TitleBox");
namedBox.TextFrame2.TextRange.Font.Size = newSize;
```

Оба подхода позволяют **изменять шрифт текстового поля в Excel** с точностью, независимо от структуры книги.

## Визуальный обзор (по желанию)

Если вы предпочитаете быстрый визуальный ориентир, представьте следующую схему:

![Скриншот листа Excel с выделенным текстовым полем – демонстрирует, как изменить размер шрифта текстового поля](change-textbox-font-size.png)

*Alt text:* *изменить размер шрифта текстового поля в Excel – выделенное текстовое поле готово к изменению шрифта.*

## Полный рабочий пример

Объединив всё вместе, представляем один файл, который вы можете скопировать‑вставить в консольный проект и запустить сразу (только обновите путь к файлу и имя листа).

```csharp
using System;
using Excel = Microsoft.Office.Interop.Excel;

namespace ExcelTextboxDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Adjust these parameters for your environment.
            string workbookPath = @"C:\Temp\Sample.xlsx";
            string sheetName = "Sheet1";
            int textboxIndex = 0;          // First textbox on the sheet.
            double newFontSize = 14;       // Desired font size.
            string newFontName = "Calibri";

            ChangeTextboxFontSize(workbookPath, sheetName, textboxIndex, newFontSize, newFontName);
        }

        static void ChangeTextboxFontSize(string workbookPath,
                                          string sheetName,
                                          int textboxIndex,
                                          double newSize,
                                          string fontName)
        {
            Excel.Application xlApp = null;
            Excel.Workbook xlWorkbook = null;
            Excel.Worksheet xlWorksheet = null;

            try
            {
                xlApp = new Excel.Application { Visible = false, DisplayAlerts = false };
                xlWorkbook = xlApp.Workbooks.Open(workbookPath);
                xlWorksheet = xlWorkbook.Worksheets[sheetName] as Excel.Worksheet;

                if (xlWorksheet == null)


## Что изучать дальше?

- [Изменение размера шрифта в Excel](/cells/english/net/working-with-fonts-in-excel/changing-font-size/)
- [Как настроить размер шрифта в ячейках Excel с помощью Aspose.Cells .NET | Полное руководство](/cells/english/net/formatting/customize-font-size-excel-aspose-cells-dotnet/)
- [Как задать стили шрифта в Excel с помощью Aspose.Cells для .NET (Пошаговое руководство)](/cells/english/net/formatting/aspose-cells-dotnet-set-font-styles-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}