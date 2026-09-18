---
category: general
date: 2026-09-18
description: Узнайте, как расширять массив в Excel с помощью функции EXPAND, заполнять
  шаблон Excel и создавать лист Excel с динамическим диапазоном с использованием C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to expand array
- populate excel template
- dynamic range excel
- use expand function
- expand array formula
language: ru
lastmod: 2026-09-18
og_description: Как расширить массив в Excel с помощью функции EXPAND, заполнить шаблон
  Excel и создать решение с динамическим диапазоном в Excel, используя код C#.
og_image_alt: Excel worksheet showing expanded 5x5 array and Smart Markers result
og_title: Как расширить массив в Excel и заполнить шаблон
schemas:
- author: Aspose
  dateModified: '2026-09-18'
  description: Learn how to expand array in Excel using the EXPAND function, populate
    an Excel template, and create a dynamic range Excel worksheet with C#.
  headline: How to expand array in Excel and populate a template
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
title: Как расширить массив в Excel и заполнить шаблон
url: /ru/net/templates-reporting/how-to-expand-array-in-excel-and-populate-a-template/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как расширить массив в Excel и заполнить шаблон

Если вам нужно **расширить массив** в Excel при заполнении заранее подготовленного шаблона, это руководство покажет полное решение от начала до конца. С помощью функции `EXPAND` вместе с Smart Markers от Aspose.Cells вы можете превратить одну ссылку на ячейку в диапазон 5 × 5 и автоматически заменить маркеры, такие как `{IsActive}`, на актуальные данные.

Вы увидите, как **заполнить шаблон Excel**, создать **динамический диапазон Excel** и правильно **использовать функцию EXPAND** в проекте C#. К концу руководства у вас будет исполняемая программа, которая загружает файл `.xlsx`, расширяет формулу массива, применяет Smart Markers и сохраняет результат.

## Требования

* .NET 6.0 или новее (код также работает с .NET Core 3.1+)
* Aspose.Cells for .NET (NuGet‑пакет `Aspose.Cells`)
* Excel‑книга, содержащая ячейку‑заполнитель формулы (например, `B2`) и Smart Marker, такой как `{IsActive}`
* Базовые знания C# и формул Excel

> **Pro tip:** Функция `EXPAND` доступна только в Excel для Microsoft 365 и Excel 2021+. В более старых версиях будет возвращена ошибка `#NAME?`.

## Шаг 1: Как расширить массив с помощью функции EXPAND

Первый шаг — загрузить книгу и записать формулу `EXPAND`, которая превращает одну исходную ячейку в более крупную матрицу.  

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Load the workbook that contains the template layout
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Access the first worksheet (index 0)
        Worksheet ws = workbook.Worksheets[0];

        // Apply the EXPAND function to cell B2.
        // =EXPAND(A2,5,5) expands the array that starts at A2 into a 5‑row by 5‑column range.
        ws.Cells["B2"].Formula = "=EXPAND(A2,5,5)";
```

Почему это важно: `EXPAND` устраняет необходимость вручную копировать формулы по строкам и столбцам. Когда исходная ячейка (`A2`) меняется, весь блок 5 × 5 обновляется автоматически, предоставляя вам **динамический диапазон Excel**, который реагирует на изменения данных.

## Шаг 2: Заполнение шаблона Excel с помощью Smart Markers

Smart Markers позволяют встраивать заполнители в шаблон, которые заменяются значениями из объекта C#. Это самый удобный способ **заполнить шаблон Excel** без написания кода построчно.

```csharp
        // Prepare an anonymous object that matches the marker names in the template.
        var data = new { IsActive = true };

        // Apply Smart Markers. The marker {IsActive} inside a formula like
        // =IF({IsActive}, "Active", "Inactive") will be replaced with the value from the object.
        workbook.Worksheets[0].SmartMarkersProcessor().Apply(data);
```

Вызов `SmartMarkersProcessor().Apply` сканирует весь лист, находит `{IsActive}` и вставляет булево значение. Формула затем автоматически вычисляется как `"Active"` или `"Inactive"`.

## Шаг 3: Проверка расширенного диапазона и заполненного результата

После применения как формулы `EXPAND`, так и Smart Markers, вы можете программно прочитать несколько ячеек, чтобы убедиться, что всё работает как ожидается.

```csharp
        // Optional: read a cell from the expanded block to confirm the value.
        var sampleValue = ws.Cells["B2"].Value; // top‑left cell of the expanded range
        Console.WriteLine($"Top‑left of expanded range: {sampleValue}");

        // Read the marker result cell (assume it is C2)
        var status = ws.Cells["C2"].StringValue;
        Console.WriteLine($"Status from Smart Marker: {status}");
```

Запуск программы должен вывести исходное значение из `A2` (или результат массива) и либо **Active**, либо **Inactive** в зависимости от флага `IsActive`.

## Шаг 4: Сохранение книги — окончательный результат

Наконец, запишите изменённую книгу на диск. Этот шаг демонстрирует полный процесс от загрузки, расширения, заполнения до сохранения файла.

```csharp
        // Save the workbook with the expanded array and populated markers.
        workbook.Save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

Сохранённый `output.xlsx` теперь содержит матрицу 5 × 5, сгенерированную формулой `EXPAND`, и ячейку, отражающую значение `{IsActive}`. Откройте файл в Excel, чтобы увидеть динамический диапазон в действии.

## Пограничные случаи и лучшие практики

| Ситуация | Рекомендация |
|----------|--------------|
| Версия Excel не поддерживает `EXPAND` | Вернуться к классическим формулам `=OFFSET` или `=INDEX`, либо обновить до Office 365. |
| Необходимо расширить до переменного размера | Использовать `ROWS(source)` и `COLUMNS(source)` внутри `EXPAND` для истинной динамичности. |
| Несколько Smart Markers на одном листе | Вызвать `SmartMarkersProcessor().Apply` один раз с составным объектом данных. |
| Большие книги ( > 10 000 строк) | Отключить вычисления при записи формул (`workbook.Settings.CheckFormula = false`). |

## Полный рабочий пример

Ниже приведена полная, автономная программа, которую вы можете скопировать и вставить в новый консольный проект.

```csharp
using System;
using Aspose.Cells;

class ExpandArrayDemo
{
    static void Main()
    {
        // 1️⃣ Load the workbook that serves as the template.
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
        Worksheet ws = workbook.Worksheets[0];

        // 2️⃣ Write the EXPAND formula to create a 5x5 dynamic range.
        ws.Cells["B2"].Formula = "=EXPAND(A2,5,5)";

        // 3️⃣ Prepare data for Smart Markers.
        var data = new { IsActive = true };

        // 4️⃣ Apply Smart Markers – replaces {IsActive} in any formula or text.
        workbook.Worksheets[0].SmartMarkersProcessor().Apply(data);

        // 5️⃣ (Optional) Verify a couple of cells.
        Console.WriteLine($"Expanded top‑left: {ws.Cells["B2"].Value}");
        Console.WriteLine($"Marker result: {ws.Cells["C2"].StringValue}");

        // 6️⃣ Save the final workbook.
        workbook.Save("YOUR_DIRECTORY/output.xlsx");
        Console.WriteLine("Workbook saved successfully.");
    }
}
```

**Ожидаемый вывод при запуске программы** (при условии, что `A2` содержит число `42`):

```
Expanded top‑left: 42
Marker result: Active
Workbook saved successfully.
```

Открытие `output.xlsx` показывает блок 5 × 5, заполненный значениями, полученными из `A2`, и ячейку, содержащую **Active**.

## Заключение

Теперь вы знаете, **как расширить массив** в Excel с помощью функции `EXPAND`, как **заполнить шаблон Excel** с помощью Smart Markers и как создать **динамический диапазон Excel**, который автоматически адаптируется к исходным данным. Пример также демонстрирует правильный способ **использовать функцию EXPAND** и **формулу expand array** в реальном сценарии автоматизации на C#.

Далее рассмотрите расширение решения:

* Замените фиксированные размеры `5,5` на `ROWS(A2:A10), COLUMNS(A2:E2)` для действительно переменных диапазонов.
* Объедините несколько Smart Markers для генерации полных отчётов (например, списков сотрудников, таблиц продаж).
* Изучите API стилизации Aspose.Cells для автоматического форматирования расширенного блока.

Не стесняйтесь экспериментировать с различными исходными массивами, именами маркеров и макетами книг. Приятного кодинга!

## Что стоит изучить дальше?

Следующие руководства охватывают тесно связанные темы, которые развивают техники, продемонстрированные в этом руководстве. Каждый ресурс включает полные рабочие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [Экспорт данных в Excel: Заполнение шаблона из массива в C#](/cells/english/net/smart-markers-dynamic-data/export-data-to-excel-populate-a-template-from-an-array-in-c/)
- [Как создать массив в Excel с помощью C# — пошаговое руководство](/cells/english/net/data-manipulation/how-to-create-array-in-excel-with-c-step-by-step-guide/)
- [Обработка данных с использованием функции массива в Excel](/cells/english/net/excel-formulas-and-calculation-options/processing-data-using-array-function/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}