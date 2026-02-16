---
category: general
date: 2026-02-15
description: Как скопировать шрифт и применить стиль ячейки в C# с простым примером.
  Узнайте, как получить стиль ячейки и использовать форматирование ячейки для установки
  размера шрифта в текстовом поле.
draft: false
keywords:
- how to copy font
- apply cell style
- get cell style
- use cell formatting
- set textbox font size
language: ru
og_description: как скопировать шрифт из ячейки листа и применить стиль ячейки к TextBox.
  Это руководство показывает, как получить стиль ячейки, использовать форматирование
  ячейки и установить размер шрифта TextBox.
og_title: Как скопировать шрифт из ячейки Excel – Полный учебник по C#
tags:
- C#
- EPPlus
- UI‑grid
- Excel‑interop
title: Как скопировать шрифт из ячейки Excel в TextBox – пошаговое руководство
url: /ru/net/working-with-fonts-in-excel/how-to-copy-font-from-an-excel-cell-to-a-textbox-step-by-ste/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# как скопировать шрифт из ячейки Excel в TextBox – Полный C# учебник

Когда‑то вам нужно **скопировать шрифт** из ячейки таблицы и сделать так, чтобы текстовое поле в UI выглядело точно так же? Вы не одиноки. Во многих инструментах отчётности или пользовательских панелях вы будете извлекать данные из Excel и пытаться сохранить визуальную точность — семейство шрифта, размер и цвет — без изменений.  

Хорошая новость: всего несколькими строками C# вы можете **получить стиль ячейки**, прочитать её свойства шрифта и **применить стиль ячейки** к любому элементу управления TextBox. В этом руководстве мы пройдём через полностью рабочий пример, показывающий, как **использовать форматирование ячеек** и даже **установить размер шрифта TextBox** программно.

---

## Что вы узнаете

- Как получить объект `TextBox` из компонента сетки (`gridJs` в нашем примере)  
- Как считать семейство шрифта, размер и цвет из конкретной ячейки Excel (`B2`)  
- Как скопировать эти атрибуты шрифта в текстовое поле, чтобы UI отражал таблицу  
- Распространённые подводные камни (например, преобразование цвета) и несколько **профессиональных советов** для надёжного кода  
- Готовый к запуску фрагмент кода, который можно вставить в консольное приложение или проект WinForms  

**Предварительные требования**  
Вам понадобится:

1. .NET 6+ (или .NET Framework 4.8) установленный  
2. Пакет NuGet EPPlus (для работы с Excel)  
3. Управление сеткой, которое предоставляет словарь `TextBoxes` (в примере используется вымышленный `gridJs`, но идея работает с любой UI‑библиотекой)

А теперь давайте приступим.

---

## Шаг 1: Настройка проекта и загрузка листа

Сначала создайте новое консольное или WinForms‑приложение и добавьте EPPlus:

```bash
dotnet add package EPPlus --version 6.*
```

Затем загрузите книгу и возьмите ячейку, стиль которой хотите скопировать.

```csharp
using OfficeOpenXml;
using OfficeOpenXml.Style;
using System.Drawing;

// ...

// Load the Excel file (make sure the file exists at the given path)
var fileInfo = new FileInfo(@"C:\Data\Sample.xlsx");
using var package = new ExcelPackage(fileInfo);
ExcelWorksheet ws = package.Workbook.Worksheets["Sheet1"]; // adjust sheet name if needed

// Retrieve the style of cell B2
ExcelStyle cellStyle = ws.Cells["B2"].Style;
```

**Почему это важно:** EPPlus даёт прямой доступ к объекту `Style`, который содержит под‑объект `Font`. Оттуда можно прочитать `Name`, `Size` и `Color`. Это и есть ядро операции **получить стиль ячейки**.

---

## Шаг 2: Получите целевой TextBox из вашей сетки

Предположим, что ваша UI‑сетка (`gridJs`) хранит текстовые поля в словаре, ключом которого является имя столбца; тогда нужный элемент можно получить так:

```csharp
// Fake grid class for illustration – replace with your actual grid component
var gridJs = new MyGrid(); // MyGrid is a placeholder for your UI control

// Step 1: Retrieve the "Notes" text box from the grid
var notesTextBox = gridJs.TextBoxes["Notes"];
```

Если вы работаете с WinForms, `notesTextBox` может быть контролом `TextBox`; для WPF — элементом `TextBox`, а для веб‑сетки — объектом JavaScript‑интеропа. Главное, чтобы у вас была ссылка, которую можно модифицировать.

---

## Шаг 3: Перенос семейства шрифта

Теперь, когда у нас есть и исходный стиль, и целевой элемент управления, копируем семейство шрифта.

```csharp
// Apply the cell's font family to the text box
notesTextBox.FontFamily = cellStyle.Font.Name;
```

**Профессиональный совет:** Не во всех UI‑фреймворках свойство `FontFamily` принимает простую строку. В WinForms вы бы писали `notesTextBox.Font = new Font(cellStyle.Font.Name, notesTextBox.Font.Size);`. Подгоняйте код под ваш фреймворк.

---

## Шаг 4: Перенос размера шрифта

Размер шрифта в EPPlus хранится как `float`. Применяем его напрямую:

```csharp
// Apply the cell's font size to the text box
notesTextBox.FontSize = cellStyle.Font.Size;
```

Если ваш контрол использует пункты (что обычно так), значение можно присвоить без преобразования. Для CSS‑основных сеток может потребоваться добавить суффикс `"pt"`.

---

## Шаг 5: Перенос цвета шрифта

Преобразование цвета — самая сложная часть, потому что EPPlus хранит цвета как целые ARGB, а многие UI‑фреймворки ожидают `System.Drawing.Color` или строку HEX для CSS.

```csharp
// Apply the cell's font colour to the text box
// EPPlus stores colour as a System.Drawing.Color when using .Color property
var excelColor = cellStyle.Font.Color?.GetColor();

// Fallback to black if the cell has no explicit colour
var safeColor = excelColor ?? Color.Black;

// Convert to the format your UI expects (example for WinForms)
notesTextBox.FontColor = safeColor;
```

> **Почему это работает:** `GetColor()` разрешает цвета, основанные на теме, и возвращает конкретный `System.Drawing.Color`. Если ячейка использует цвет по умолчанию (нет явного задания), мы по умолчанию берём чёрный, чтобы избежать исключений `null`.

---

## Полный рабочий пример

Объединив всё вместе, получаем минимальное консольное приложение, которое читает файл Excel, извлекает шрифт из **B2** и применяет его к имитационному текстовому полю.

```csharp
using OfficeOpenXml;
using OfficeOpenXml.Style;
using System;
using System.Collections.Generic;
using System.Drawing;

namespace FontCopyDemo
{
    // Mock grid control – replace with your real UI component
    public class MyGrid
    {
        public Dictionary<string, TextBoxMock> TextBoxes { get; } = new()
        {
            { "Notes", new TextBoxMock() }
        };
    }

    // Simple text box representation for demonstration
    public class TextBoxMock
    {
        public string FontFamily { get; set; }
        public float FontSize { get; set; }
        public Color FontColor { get; set; }

        public override string ToString()
        {
            return $"FontFamily: {FontFamily}, FontSize: {FontSize}, FontColor: {FontColor.Name}";
        }
    }

    class Program
    {
        static void Main()
        {
            // 1️⃣ Load Excel worksheet
            var fileInfo = new FileInfo(@"C:\Data\Sample.xlsx");
            using var package = new ExcelPackage(fileInfo);
            var ws = package.Workbook.Worksheets["Sheet1"];
            var cellStyle = ws.Cells["B2"].Style;

            // 2️⃣ Grab the target TextBox from the grid
            var gridJs = new MyGrid();
            var notesTextBox = gridJs.TextBoxes["Notes"];

            // 3️⃣ Apply font family
            notesTextBox.FontFamily = cellStyle.Font.Name;

            // 4️⃣ Apply font size
            notesTextBox.FontSize = cellStyle.Font.Size;

            // 5️⃣ Apply font colour (with safety net)
            var excelColor = cellStyle.Font.Color?.GetColor();
            notesTextBox.FontColor = excelColor ?? Color.Black;

            // Output the result for verification
            Console.WriteLine("TextBox after copying font:");
            Console.WriteLine(notesTextBox);
        }
    }
}
```

**Ожидаемый вывод (при условии, что B2 использует Arial, 12 pt, синий):**

```
TextBox after copying font:
FontFamily: Arial, FontSize: 12, FontColor: Blue
```

Запустите программу, откройте ваш UI, и вы увидите, что текстовое поле «Notes» теперь полностью повторяет стиль ячейки **B2**. Никакой ручной настройки не требуется.

---

## Часто задаваемые вопросы и особые случаи

### Что делать, если ячейка использует цвет темы вместо явного RGB‑значения?

`GetColor()` в EPPlus автоматически преобразует цвета темы в конкретный `System.Drawing.Color`. Однако, если вы используете более старую библиотеку, которая возвращает только индекс темы, вам придётся самостоятельно сопоставить этот индекс с палитрой цветов.

### Можно ли копировать другие атрибуты стиля (например, жирный, курсив)?

Конечно. Объект `ExcelStyle.Font` также предоставляет свойства `Bold`, `Italic`, `Underline` и `Strike`. Просто задайте соответствующие свойства вашего UI‑контрола:

```csharp
notesTextBox.FontBold = cellStyle.Font.Bold;
notesTextBox.FontItalic = cellStyle.Font.Italic;
```

### Что если контрол сетки не имеет свойства `FontColor`?

Большинство современных UI‑фреймворков поддерживают его, но если ваш контрол принимает только строку CSS, преобразуйте `Color` в HEX:

```csharp
string hex = $"#{notesTextBox.FontColor.R:X2}{notesTextBox.FontColor.G:X2}{notesTextBox.FontColor.B:X2}";
notesTextBox.Style["color"] = hex; // for web‑based grids
```

### Как обрабатывать несколько ячеек одновременно?

Пройдитесь в цикле по нужному диапазону, получите стиль каждой ячейки и примените его к соответствующему текстовому полю. Не забудьте кэшировать объекты стиля при обработке большого количества строк, чтобы избежать падения производительности.

---

## Профессиональные советы и распространённые подводные камни

- **Кешируйте ExcelPackage** — открывать и закрывать файл для каждой ячейки дорого. Загрузите книгу один раз и переиспользуйте объект `ExcelWorksheet`.  
- **Следите за null‑цветами** — ячейка, наследующая цвет по умолчанию, возвращает `null`. Всегда задавайте запасной вариант (чёрный или значение по умолчанию контрола).  
- **Учтите масштабирование DPI** — при работе с мониторами высокого DPI размеры шрифтов могут выглядеть больше. При необходимости скорректируйте их через `Graphics.DpiX`.  
- **Потокобезопасность** — EPPlus не является потокобезопасным. Если обрабатываете несколько листов параллельно, создавайте отдельный `ExcelPackage` для каждого потока.

---

## Заключение

Теперь вы знаете, **как скопировать шрифт** из ячейки Excel и **применить стиль ячейки** к любому контролу TextBox с помощью C#. Получив `Style` ячейки, извлекая её свойства `Font` и присваивая их UI‑элементу, вы сохраняете визуальное соответствие без ручного вмешательства.  

Полное решение — загрузка книги, получение стиля ячейки и установка семейства шрифта, размера и цвета TextBox — охватывает ядро **использования форматирования ячеек** и демонстрирует, как правильно **установить размер шрифта TextBox**.  

Дальше попробуйте расширить пример, копируя фон, границы или даже всё содержимое ячейки. Если вы работаете с библиотекой Data‑Grid, поддерживающей богатое рендеринг ячеек, теперь можете передавать ей точно такие же параметры стиля, какие вы извлекли из Excel, и ваш UI будет полностью синхронен с отчётами.

Есть вопросы? Оставляйте комментарий или изучайте связанные темы, такие как «динамическое привязывание Excel‑к‑UI» и «конверсия цвета с учётом темы». Приятного кодинга!

---

![how to copy font example](placeholder-image.jpg "how to copy font from Excel cell to TextBox")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}