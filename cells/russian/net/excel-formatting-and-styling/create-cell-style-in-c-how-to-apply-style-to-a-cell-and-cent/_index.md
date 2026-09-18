---
category: general
date: 2026-02-21
description: Быстро создавайте стиль ячейки в C#. Узнайте, как применить стиль к ячейке,
  центрировать текст в ячейке, установить выравнивание ячейки и освоить форматирование
  ячеек.
draft: false
keywords:
- create cell style
- apply style to cell
- center text in cell
- set cell alignment
- how to center text
language: ru
og_description: Создайте стиль ячейки в C# и узнайте, как применить стиль к ячейке,
  центрировать текст в ячейке и установить выравнивание ячейки с помощью понятного
  пошагового руководства.
og_title: Создание стиля ячейки в C# – Применить стиль к ячейке и центрировать текст
tags:
- C#
- Aspose.Cells
- Excel automation
title: Создание стиля ячейки в C# – Как применить стиль к ячейке и центрировать текст
url: /ru/net/excel-formatting-and-styling/create-cell-style-in-c-how-to-apply-style-to-a-cell-and-cent/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание стиля ячейки в C# – Полное руководство по применению стилей и центрированию текста

Когда‑нибудь вам нужно было **create cell style** в листе Excel, но вы не знали, с чего начать? Вы не одиноки. Во многих проектах автоматизации возможность **apply style to cell** объектов является разницей между скучной таблицей и отшлифованным отчётом.  

В этом руководстве мы пройдём полный, исполняемый пример, который покажет вам **how to center text** внутри ячейки, задаст выравнивание и добавит тонкую границу — всё это в нескольких строках C#. К концу вы точно поймёте, почему каждый элемент важен и как настроить его под свои сценарии.

## Что вы получите

- Чёткое понимание рабочего процесса **create cell style** с использованием Aspose.Cells (или любой аналогичной библиотеки).
- Точный код, который вы можете скопировать‑вставить в консольное приложение для **apply style to cell**.
- Понимание **center text in cell**, **set cell alignment** и обработка особых случаев, таких как объединённые ячейки или пользовательские числовые форматы.
- Советы по расширению стиля — разные шрифты, цвета фона или условное форматирование.

> **Prerequisite:** Visual Studio 2022 (или любой C# IDE) и пакет NuGet Aspose.Cells для .NET. Другие зависимости не требуются.

---

## Шаг 1: Настройте проект и импортируйте пространства имён

Прежде чем мы сможем **create cell style**, нам нужен проект, который ссылается на библиотеку Excel.

```csharp
// Program.cs – entry point
using System;
using Aspose.Cells;   // Make sure the Aspose.Cells NuGet package is installed

class Program
{
    static void Main()
    {
        // We'll fill in the rest of the steps here.
    }
}
```

*Почему это важно:* Импорт `Aspose.Cells` даёт нам доступ к классам `Workbook`, `Worksheet`, `Style` и `Border`. Если вы используете другую библиотеку (например, EPPlus), имена классов меняются, но концепция остаётся той же.

---

## Шаг 2: Создайте рабочую книгу и получите первую ячейку

Сейчас мы **create cell style**, сначала получив ссылку на ячейку, которую хотим отформатировать.

```csharp
// Inside Main()
Workbook workbook = new Workbook();           // New, empty workbook
Worksheet ws = workbook.Worksheets[0];        // First worksheet (index 0)

// Step 1: Get a reference to the first cell (row 0, column 0) in the worksheet
Cell firstCell = ws.Cells[0, 0];               // A1 in Excel terms
firstCell.PutValue("Hello, styled world!");
```

Обратите внимание, что мы использовали `Cell` вместо общего `var` — явное указание типа делает код понятнее для новичков. Вызов `PutValue` записывает строку, чтобы позже увидеть эффект стиля.

---

## Шаг 3: Определите стиль — центрирование текста, добавление тонкой границы

Это ядро операции **create cell style**. Мы зададим горизонтальное выравнивание, тонкую границу и несколько дополнительных настроек.

```csharp
// Step 2: Define a style that centers the text and adds a thin border
Style cellStyle = workbook.CreateStyle();          // Create a fresh Style object
cellStyle.HorizontalAlignment = TextAlignmentType.Center; // Center text horizontally
cellStyle.VerticalAlignment = TextAlignmentType.Center;   // Center vertically – often forgotten
cellStyle.Borders[BorderType.TopBorder].LineStyle = CellBorderType.Thin;
cellStyle.Borders[BorderType.BottomBorder].LineStyle = CellBorderType.Thin;
cellStyle.Borders[BorderType.LeftBorder].LineStyle = CellBorderType.Thin;
cellStyle.Borders[BorderType.RightBorder].LineStyle = CellBorderType.Thin;

// Optional: set a light gray background to make the border pop
cellStyle.ForegroundColor = System.Drawing.Color.LightGray;
cellStyle.Pattern = BackgroundType.Solid;
```

*Почему мы это делаем:*  
- **HorizontalAlignment** и **VerticalAlignment** вместе отвечают на вопрос «**how to center text** в ячейке?».  
- Добавление всех четырёх границ делает ячейку похожей на обрамлённую метку, что полезно для заголовков.  
- Цвет фона не обязателен, но демонстрирует, как можно позже расширить стиль.

---

## Шаг 4: Примените определённый стиль к выбранной ячейке

Теперь, когда стиль существует, мы **apply style to cell** одним вызовом метода.

```csharp
// Step 3: Apply the defined style to the selected cell
firstCell.SetStyle(cellStyle);
```

Вот и всё — Aspose.Cells позаботится о копировании стиля во внутреннюю коллекцию стилей ячейки. Если вам нужно одинаковое форматирование для диапазона, вы можете использовать `ws.Cells.CreateRange("A1:D1").ApplyStyle(cellStyle, new StyleFlag { All = true });`.

---

## Шаг 5: Сохраните рабочую книгу и проверьте результат

Быстрое сохранение позволяет открыть файл в Excel и убедиться, что текст действительно центрирован, а граница отображается.

```csharp
// Save the workbook to disk
string outputPath = "StyledCell.xlsx";
workbook.Save(outputPath, SaveFormat.Xlsx);
Console.WriteLine($"Workbook saved to {outputPath}. Open it to see the styled cell.");
```

*Ожидаемый результат:* При открытии **StyledCell.xlsx** ячейка **A1** содержит «Hello, styled world!», центрированную по горизонтали и вертикали, окружённую тонкой серой границей и с светло‑серым фоном.

---

## Общие варианты и особые случаи

### 1. Центрирование текста в объединённом диапазоне

Если вы объединяете ячейки **A1:C1** и всё ещё хотите центрировать текст, необходимо применить стиль к ячейке в левом‑верхнем углу **после** объединения:

```csharp
ws.Cells.Merge(0, 0, 1, 3); // Merge A1:C1
firstCell.SetStyle(cellStyle); // Style still works because it’s applied to the anchor cell
```

### 2. Использование числового формата

Иногда требуется **set cell alignment** *и* отобразить числа в определённом формате:

```csharp
cellStyle.Custom = "#,##0.00"; // Two decimal places
firstCell.PutValue(12345.678);
firstCell.SetStyle(cellStyle);
```

Выравнивание остаётся центрированным, а число отображается как `12,345.68`.

### 3. Эффективное повторное использование стилей

Создание нового `Style` для каждой ячейки может ухудшить производительность. Вместо этого создайте один объект стиля и переиспользуйте его для множества ячеек или диапазонов. Класс `StyleFlag` позволяет применять только те части, которые вам нужны, экономя память.

```csharp
StyleFlag flag = new StyleFlag { HorizontalAlignment = true, Borders = true };
ws.Cells.CreateRange("B2:B10").ApplyStyle(cellStyle, flag);
```

---

## Профессиональные советы и подводные камни

- **Don’t forget vertical alignment** — центрирование только по горизонтали часто выглядит некорректно, особенно в более высоких строках.
- **Border types**: `CellBorderType.Thin` подходит для большинства отчётов, но вы можете переключить на `Medium` или `Dashed` для визуальной иерархии.
- **Color handling**: При работе с .NET Core используйте `System.Drawing.Color` из пакета `System.Drawing.Common`; иначе возникнет ошибка выполнения.
- **Saving format**: Если нужна совместимость со старыми версиями Excel, измените `SaveFormat.Xlsx` на `SaveFormat.Xls`.

![Создание стиля ячейки пример](https://example.com/images/create-cell-style.png "Создание стиля ячейки в C#")

*Alt text: скриншот, показывающий ячейку с центрированным текстом и тонкой границей, созданную в руководстве по create cell style.*

---

## Полный рабочий пример (готовый к копированию‑вставке)

```csharp
using System;
using Aspose.Cells;
using System.Drawing; // For Color

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet ws = workbook.Worksheets[0];

        // 2️⃣ Grab the first cell and put a sample value
        Cell firstCell = ws.Cells[0, 0];
        firstCell.PutValue("Hello, styled world!");

        // 3️⃣ Create the style: center text, thin border, light gray background
        Style cellStyle = workbook.CreateStyle();
        cellStyle.HorizontalAlignment = TextAlignmentType.Center;
        cellStyle.VerticalAlignment   = TextAlignmentType.Center;
        cellStyle.Borders[BorderType.TopBorder].LineStyle    = CellBorderType.Thin;
        cellStyle.Borders[BorderType.BottomBorder].LineStyle = CellBorderType.Thin;
        cellStyle.Borders[BorderType.LeftBorder].LineStyle   = CellBorderType.Thin;
        cellStyle.Borders[BorderType.RightBorder].LineStyle  = CellBorderType.Thin;
        cellStyle.ForegroundColor = Color.LightGray;
        cellStyle.Pattern = BackgroundType.Solid;

        // 4️⃣ Apply the style to the cell
        firstCell.SetStyle(cellStyle);

        // 5️⃣ Save the result
        string outputPath = "StyledCell.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);
        Console.WriteLine($"Workbook saved to {outputPath}. Open it to see the styled cell.");
    }
}
```

Запустите эту программу, откройте **StyledCell.xlsx**, и вы увидите точный результат, описанный ранее. Не стесняйтесь менять текст, стиль границы или цвет фона, чтобы соответствовать вашему бренду.

---

## Заключение

Мы только что **created cell style** с нуля, **applied style to cell**, и продемонстрировали **how to center text** как по горизонтали, так и по вертикали. Овладев этими базовыми элементами, вы теперь можете форматировать заголовки, выделять итоги или создавать целые шаблоны отчётов, не выходя из C#.  

Если вам интересны дальнейшие шаги, попробуйте:

- **Применение того же стиля к целой строке** (`ws.Cells.CreateRange("A2:E2").ApplyStyle(cellStyle, new StyleFlag { All = true });`).
- **Добавление условного форматирования** для изменения фона в зависимости от значений ячеек.
- **Экспорт в PDF** с сохранением стиля.

Помните, стилизация важна не только для эстетики, но и для читаемости. Экспериментируйте, улучшайте, и скоро ваши таблицы будут выглядеть так же профессионально, как ваш код.

*Удачной разработки!*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}