---
category: general
date: 2026-11-16
description: Узнайте, как расширять массив в Excel с помощью Aspose.Cells, функций
  динамических массивов и редуктора‑лямбда, а затем записать файл Excel из C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to expand array
- create excel workbook
- how to use lambda
- dynamic array functions
- write excel file
language: ru
lastmod: 2026-11-16
og_description: Как расширить массив в Excel с помощью Aspose.Cells, функций динамических
  массивов и редуктора‑лямбда. Следуйте полному примеру на C# для записи файла Excel.
og_image_alt: Diagram illustrating how to expand array in an Excel worksheet
og_title: Как расширить массив в Excel с помощью Aspose.Cells – пошаговое руководство
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Learn how to expand array in Excel using Aspose.Cells, dynamic array
    functions, and a lambda reducer, then write the Excel file from C#.
  headline: How to expand array in Excel with Aspose.Cells
  type: TechArticle
- questions:
  - answer: Yes. `EXPAND` pads missing columns with blank cells. The same works for
      rows.
    question: Can I expand to more columns than the source provides?
  - answer: '`EXPAND` will treat the source as a single row; you can still specify
      rows and columns to reshape it.'
    question: What if the source array is horizontal (`{1,2,3,4,5}`)?
  - answer: The lambda must return a value compatible with the accumulator type. For
      text concatenation you could use `LAMBDA(acc, val, acc & val)`.
    question: Does `REDUCE` work with non‑numeric data?
  - answer: Only when you need the computed values before saving. Excel will recalculate
      on open if you skip it.
    question: Do I need to call `CalculateFormula` for every change?
  type: FAQPage
tags:
- Aspose.Cells
- C#
- Excel automation
title: Как расширить массив в Excel с помощью Aspose.Cells
url: /ru/net/calculation-engine/how-to-expand-array-in-excel-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как расширить массив в Excel с помощью Aspose.Cells

Если вам нужно **how to expand array** в листе Excel из C#, этот учебник покажет точные шаги. Вы создадите рабочую книгу Excel, используете функции динамических массивов, такие как `EXPAND` и `REDUCE`, примените аккумулятор **lambda**, и в конце **write Excel file** на диск. Подход работает с Aspose.Cells 23.10 или новее и не требует ручной установки Excel.

К концу этого руководства у вас будет полностью рабочий файл `ExpandReduceDemo.xlsx`, демонстрирующий мощь формул динамических массивов в программном контексте.

## Что вам понадобится

- .NET 6.0 (или любая версия .NET, поддерживаемая Aspose.Cells)
- Пакет Aspose.Cells для .NET (`dotnet add package Aspose.Cells`)
- Редактор кода или IDE (Visual Studio, VS Code, Rider и т.д.)

Никакая дополнительная COM‑interop или установка Office не требуется, поскольку Aspose.Cells обрабатывает формат файла внутренне.

## Шаг 1: Создать рабочую книгу Excel

Первая задача — **create excel workbook** в памяти. Aspose.Cells предоставляет класс `Workbook`, который представляет весь файл XLSX.

```csharp
using System;
using Aspose.Cells;

class ExpandReduceDemo
{
    static void Main()
    {
        // Step 1: instantiate a new workbook and get the default worksheet
        Workbook workbook = new Workbook();              // creates an empty .xlsx structure
        Worksheet sheet = workbook.Worksheets[0];        // the first (and only) sheet by default
```

> **Why this matters:** Создание экземпляра `Workbook` дает вам чистый холст. Лист по умолчанию уже подготовлен, поэтому вам не нужно добавлять его вручную, если только вы не хотите несколько листов.

## Шаг 2: Вставить вертикальную константу массива

Движок динамических массивов Excel может работать с буквальными константами массивов. Мы разместим вертикальный массив `{1;2;3;4;5}` в ячейку **A1**.

```csharp
        // Step 2: put a vertical array constant into A1
        sheet.Cells["A1"].PutValue("{1;2;3;4;5}");
```

> **Tip:** Точка с запятой (`;`) разделяет строки в константе, а запятая (`,`) разделяла бы столбцы. Это соответствует синтаксису Excel.

## Шаг 3: Расширить массив в матрицу

Теперь мы отвечаем на основной вопрос — **how to expand array** — используя функцию `EXPAND`. Формула расширяет одностолбцовый массив до матрицы 5 строк × 2 столбца, начиная с **B1**.

```csharp
        // Step 3: use EXPAND to create a 5‑row by 2‑column matrix
        sheet.Cells["B1"].Formula = "EXPAND(A1,5,2)";
```

> **Why EXPAND?** `EXPAND(source, rows, cols)` заставляет исходный диапазон занимать указанный размер, заполняя пустыми ячейками при необходимости. Это самый читаемый способ создать большую матрицу из одного массива.

## Шаг 4: Сократить матрицу с помощью аккумулятора lambda

Функция `REDUCE` проходит по диапазону и агрегирует значения, используя выражение **lambda**. Здесь мы суммируем значения каждого столбца в один столбец, помещая результат в **D1**.

```csharp
        // Step 4: REDUCE the expanded matrix using a lambda accumulator
        sheet.Cells["D1"].Formula = "REDUCE(A1, B1:E5, LAMBDA(acc, val, acc+val))";
```

> **How to use lambda:** `LAMBDA(acc, val, acc+val)` получает текущий аккумулятор (`acc`) и следующее значение ячейки (`val`). Он возвращает новый аккумулятор, эффективно выполняя накопительный итог. Это демонстрирует **how to use lambda** в формулах Excel из кода.

## Шаг 5: Вычислить формулы, чтобы появились результаты

Aspose.Cells не вычисляет формулы автоматически при их установке. Вызов `CalculateFormula` заставляет движок вычислить каждую формулу в рабочей книге.

```csharp
        // Step 5: recalculate all formulas so the results are materialized
        workbook.CalculateFormula();
```

> **Note:** Если открыть сгенерированный файл в Excel, значения уже будут видны, поскольку они были предварительно вычислены.

## Шаг 6: Сохранить файл Excel на диск

Наконец, **write excel file** с помощью метода `Save`. Выберите папку, в которую у вас есть права на запись.

```csharp
        // Step 6: save the workbook as an .xlsx file
        string outputPath = @"YOUR_DIRECTORY\ExpandReduceDemo.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

### Ожидаемый результат

| A | B | C | D |
|---|---|---|---|
| {1;2;3;4;5} | 1 |  | 15 |
|            | 2 |  |    |
|            | 3 |  |    |
|            | 4 |  |    |
|            | 5 |  |    |

- **Column B** и **C** содержат матрицу 5 × 2, полученную с помощью `EXPAND`.
- **Cell D1** показывает `15`, сумму всех чисел, вычисленную формулой `REDUCE` + **lambda**.

## Часто задаваемые вопросы и особые случаи

- **Can I expand to more columns than the source provides?**  
  Да. `EXPAND` заполняет недостающие столбцы пустыми ячейками. То же самое работает и для строк.

- **What if the source array is horizontal (`{1,2,3,4,5}`)?**  
  `EXPAND` будет рассматривать источник как одну строку; вы всё равно можете указать количество строк и столбцов для его преобразования.

- **Does `REDUCE` work with non‑numeric data?**  
  Lambda должна возвращать значение, совместимое с типом аккумулятора. Для конкатенации текста можно использовать `LAMBDA(acc, val, acc & val)`.

- **Do I need to call `CalculateFormula` for every change?**  
  Только когда вам нужны вычисленные значения перед сохранением. Excel пересчитает их при открытии, если вы пропустите этот вызов.

## Профессиональные советы

- **Performance:** Для больших книг вызывайте `workbook.CalculateFormula` один раз после установки всех формул, а не после каждой ячейки.
- **Version safety:** `EXPAND` и `REDUCE` доступны в Excel 365 и новее. Aspose.Cells реализует их независимо от целевой версии Excel, поскольку движок вычислений встроен.
- **Debugging formulas:** Используйте `sheet.Cells["B1"].Formula`, чтобы прочитать обратно точную строку, которую вы задали; это помогает при динамическом построении формул.

## Заключение

Теперь вы знаете **how to expand array** в Excel с помощью Aspose.Cells, используете **dynamic array functions**, применяете **lambda** с `REDUCE` и **write excel file** из C#. Этот сквозной пример можно адаптировать к более сложным преобразованиям данных, таким как транспонирование матрицы, накопительные итоги или пользовательские агрегаты.

---

*Next steps:*  
- Изучите другие динамические функции, такие как `FILTER`, `SORT` и `UNIQUE`.  
- Комбинируйте несколько выражений `LAMBDA` для создания переиспользуемых пользовательских функций.  
- Интегрируйте генерацию рабочей книги в ASP.NET Core API для создания отчетов «на лету».

## Что вам следует изучить дальше?

Следующие учебники охватывают тесно связанные темы, которые опираются на техники, продемонстрированные в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [Как создать рабочую книгу Excel C# с формулой динамического массива](/cells/english/net/excel-formulas-and-calculation-options/how-to-create-excel-workbook-c-with-a-dynamic-array-formula/)
- [Как расширить массив в Excel и заполнить шаблон](/cells/english/net/templates-reporting/how-to-expand-array-in-excel-and-populate-a-template/)
- [Как расширить массив в C# с Aspose.Cells – пошаговое руководство](/cells/english/net/excel-formulas-and-calculation-options/how-to-expand-array-in-c-with-aspose-cells-step-by-step-guid/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}