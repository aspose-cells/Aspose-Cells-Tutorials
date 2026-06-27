---
category: general
date: 2026-06-27
description: как использовать wrapcols и wrap rows в Excel на C#. Узнайте, как создать
  книгу Excel на C# и пересчитать формулы Excel с пошаговым примером.
draft: false
keywords:
- how to use wrapcols
- wrap rows excel
- wrap columns excel
- recalculate excel formulas
- create excel workbook c#
language: ru
og_description: как использовать wrapcols и wrap rows в Excel с помощью C#. Это руководство
  показывает, как создать рабочую книгу Excel на C# и пересчитать формулы Excel за
  считанные минуты.
og_title: Как использовать wrapcols в C# – Полный учебник по обёртке в Excel
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: how to use wrapcols and wrap rows excel in C#. Learn to create excel
    workbook c# and recalculate excel formulas with a step‑by‑step example.
  headline: how to use wrapcols in C# – Full Guide with Excel WRAPROWS & Recalculate
    Formulas
  type: TechArticle
- description: how to use wrapcols and wrap rows excel in C#. Learn to create excel
    workbook c# and recalculate excel formulas with a step‑by‑step example.
  name: how to use wrapcols in C# – Full Guide with Excel WRAPROWS & Recalculate Formulas
  steps:
  - name: Expected Result
    text: '| A | B | C | |---|---|---| | 1 | A | 2 | | 2 | B | 3 | | 3 | C | 4 | |
      4 | D | 5 | | 5 | E | 6 | | 6 | F | 7 | | 7 | G | 8 | | 8 | H | 9 | | 9 | I
      | |'
  - name: What if the source range is empty?
    text: Both `WRAPCOLS` and `WRAPROWS` will simply return an empty array, resulting
      in a blank cell. It’s safe to call the functions even when you’re not sure about
      data presence.
  - name: Can I wrap more than one range at a time?
    text: Yes—just place additional formulas in other cells. Each formula works independently,
      so you could have `WRAPCOLS` in D1, `WRAPROWS` in E1, etc.
  - name: How does this differ from a simple copy‑paste transpose?
    text: '`WRAPCOLS`/`WRAPROWS` handle *pagination* automatically. If you have 20
      items and ask for 3 columns, the function creates the necessary number of rows
      (7 in this case) without you calculating the dimensions manually.'
  - name: Does the library support dynamic array formulas (Excel 365)?
    text: Aspose.Cells fully supports dynamic array functions, including `WRAPCOLS`
      and `WRAPROWS`. The calculation engine will spill the results just like native
      Excel.
  - name: What about performance on large datasets?
    text: For millions of rows, consider batching the calculation (`workbook.CalculateFormula(FormulaCalculationOptions)`)
      or disabling automatic calculation while you insert formulas, then re‑enable
      it before saving.
  type: HowTo
tags:
- Excel
- C#
- Aspose.Cells
title: Как использовать wrapcols в C# – полное руководство с Excel WRAPROWS и пересчётом
  формул
url: /ru/net/row-and-column-management/how-to-use-wrapcols-in-c-full-guide-with-excel-wraprows-reca/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# как использовать wrapcols в C# – Полное руководство с Excel WRAPROWS и пересчетом формул

Когда‑нибудь задавались вопросом **how to use wrapcols**, когда нужно преобразовать длинный список в аккуратную сетку? Возможно, вы пробовали ручной способ копирования‑вставки, но он медленный, подвержен ошибкам и, откровенно говоря, доставляет неудобства. Хорошая новость? `WRAPCOLS` в Excel (и его «брат» `WRAPROWS`) могут выполнить всю тяжелую работу за вас — *и* вы можете управлять ими из кода C#.

В этом руководстве мы пройдем процесс создания Excel‑книги в C#, применения `WRAPCOLS` и `WRAPROWS`, и, наконец, **recalculate excel formulas**, чтобы обернутые данные отображались мгновенно. К концу у вас будет готовый к запуску фрагмент кода, который можно вставить в любой проект .NET.

## Что вы узнаете

- Как **create excel workbook c#** с использованием библиотеки Aspose.Cells (без необходимости COM‑interop).  
- Точный синтаксис функции `WRAPCOLS` и то, как он отличается от `WRAPROWS`.  
- Почему необходимо **recalculate excel formulas** после вставки функций и как сделать это эффективно.  
- Полный, исполняемый пример, который вы можете скопировать‑вставить и увидеть результат в файле `.xlsx`.  

**Prerequisites** – Вам нужен .NET 6+ (или .NET Framework 4.7+), Visual Studio 2022 или любой другой IDE, а также пакет NuGet Aspose.Cells для .NET. Если вы новичок в Aspose.Cells, не волнуйтесь; шаги просты и полностью объяснены.

---

## Шаг 1: Настройка проекта и установка Aspose.Cells

Для начала создайте новый консольный проект:

```bash
dotnet new console -n WrapDemo
cd WrapDemo
dotnet add package Aspose.Cells
```

> **Pro tip:** Если вы используете Visual Studio, просто щёлкните правой кнопкой мыши по проекту → *Manage NuGet Packages* → найдите **Aspose.Cells** и установите его.

Библиотека предоставляет нам классы `Workbook`, `Worksheet` и `Cell`, которые понадобятся нам в дальнейшем руководстве.

## Шаг 2: Создание Excel‑книги и заполнение образцовыми данными

Теперь мы создадим книгу, получим первый лист и заполним столбцы **A** и **B** образцовыми числами. Эти данные позже будут преобразованы в столбцы и строки.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // Step 2‑1: Create a new workbook
        Workbook workbook = new Workbook();

        // Step 2‑2: Access the first worksheet (index 0)
        Worksheet worksheet = workbook.Worksheets[0];

        // Populate A2:A10 with numbers 1‑9
        for (int i = 2; i <= 10; i++)
        {
            worksheet.Cells[$"A{i}"].PutValue(i - 1);
        }

        // Populate B2:B10 with letters A‑I (just for variety)
        char letter = 'A';
        for (int i = 2; i <= 10; i++, letter++)
        {
            worksheet.Cells[$"B{i}"].PutValue(letter.ToString());
        }

        // The rest of the steps follow…
```

> **Why this matters:** Наличие детерминированных данных позволяет убедиться, что `WRAPCOLS` и `WRAPROWS` делают именно то, что вы ожидаете.

## Шаг 3: Применение функции `WRAPCOLS` – **how to use wrapcols**

`WRAPCOLS` принимает одно‑мерный диапазон и распределяет его по заданному количеству столбцов, автоматически добавляя новые строки по мере необходимости. Ниже точная формула, которую мы вставим в ячейку **A1**:

```csharp
        // Step 3: Insert WRAPCOLS formula – wrap A2:A10 into 3 columns per row
        worksheet.Cells["A1"].Formula = "=WRAPCOLS(A2:A10, 3)";
```

> **Explanation:** Второй аргумент (`3`) указывает Excel создать три столбца в каждой строке. Таким образом, первые три значения (1, 2, 3) попадают в A1:C1, следующие три (4, 5, 6) — в A2:C2, а оставшиеся заполняют следующую строку.

## Шаг 4: Применение функции `WRAPROWS` – wrap rows excel

`WRAPROWS` делает противоположное: берёт вертикальный диапазон и распределяет его по заданному количеству строк в каждом столбце. Мы разместим эту формулу в **B1**:

```csharp
        // Step 4: Insert WRAPROWS formula – wrap B2:B10 into 2 rows per column
        worksheet.Cells["B1"].Formula = "=WRAPROWS(B2:B10, 2)";
```

> **Explanation:** При `2` строках на столбец значения «A, B» попадают в B1:B2, «C, D» — в C1:C2 и т.д. Функция автоматически расширяет лист по горизонтали.

## Шаг 5: Пересчёт всех формул – **recalculate excel formulas**

Когда вы задаёте формулу программно, Excel не вычислит результат, пока книга не будет открыта или вы явно не попросите библиотеку выполнить вычисление. Здесь и пригодится **recalculate excel formulas**:

```csharp
        // Step 5: Force calculation so the wrapped data appears immediately
        workbook.CalculateFormula();
```

> **Why you need this:** Без вызова `CalculateFormula()` ячейки будут отображать необработанный текст `=WRAPCOLS(...)` при открытии файла, что противоречит цели руководства.

## Шаг 6: Сохранение книги и проверка результата

Наконец, запишите книгу на диск. Вы можете открыть полученный файл в Excel, чтобы увидеть обёрнутую раскладку.

```csharp
        // Step 6: Save the workbook (adjust the path as needed)
        string outputPath = "output.xlsx";
        workbook.Save(outputPath);
        Console.WriteLine($"Workbook saved to {outputPath}. Open it to see wrapcols and wraprows in action.");
    }
}
```

### Ожидаемый результат

| A | B | C |
|---|---|---|
| 1 | A | 2 |
| 2 | B | 3 |
| 3 | C | 4 |
| 4 | D | 5 |
| 5 | E | 6 |
| 6 | F | 7 |
| 7 | G | 8 |
| 8 | H | 9 |
| 9 | I |   |

- **Столбцы A‑C** заполняются вызовом `WRAPCOLS` (три столбца на строку).  
- **Строки B‑I** заполняются вызовом `WRAPROWS` (две строки на столбец).  

Откройте `output.xlsx`, и вы увидите точную раскладку, показанную выше. Если числа не совпадают, дважды проверьте строки формул и убедитесь, что был вызван `CalculateFormula()`.

---

## Часто задаваемые вопросы и особые случаи

### Что если исходный диапазон пуст?
Обе функции `WRAPCOLS` и `WRAPROWS` просто вернут пустой массив, что приведёт к пустой ячейке. Вы можете вызывать их, даже если не уверены в наличии данных.

### Можно ли обернуть более одного диапазона одновременно?
Да — просто разместите дополнительные формулы в других ячейках. Каждая формула работает независимо, так что вы можете иметь `WRAPCOLS` в D1, `WRAPROWS` в E1 и т.д.

### Чем это отличается от простого копирования‑вставки с транспонированием?
`WRAPCOLS`/`WRAPROWS` автоматически обрабатывают *пагинацию*. Если у вас 20 элементов и вы задаёте 3 столбца, функция создаст необходимое количество строк (7 в данном случае) без необходимости вручную рассчитывать размеры.

### Поддерживает ли библиотека динамические массивные формулы (Excel 365)?
Aspose.Cells полностью поддерживает функции динамических массивов, включая `WRAPCOLS` и `WRAPROWS`. Движок вычислений разольёт результаты так же, как нативный Excel.

### Какова производительность при работе с большими наборами данных?
Для миллионов строк рассмотрите пакетный расчёт (`workbook.CalculateFormula(FormulaCalculationOptions)`) или отключите автоматический расчёт во время вставки формул, а затем включите его перед сохранением.

---

## Полный исходный код (готов к запуску)

Ниже представлен полный код программы — скопируйте его в `Program.cs` и нажмите **F5**.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Populate column A (A2:A10) with numbers 1‑9
        for (int i = 2; i <= 10; i++)
        {
            worksheet.Cells[$"A{i}"].PutValue(i - 1);
        }

        // Populate column B (B2:B10) with letters A‑I
        char letter = 'A';
        for (int i = 2; i <= 10; i++, letter++)
        {
            worksheet.Cells[$"B{i}"].PutValue(letter.ToString());
        }

        // Apply WRAPCOLS – wrap A2:A10 into 3 columns per row
        worksheet.Cells["A1"].Formula = "=WRAPCOLS(A2:A10, 3)";

        // Apply WRAPROWS – wrap B2:B10 into 2 rows per column
        worksheet.Cells["B1"].Formula = "=WRAPROWS(B2:B10, 2)";

        // Recalculate all formulas so the wrapped data appears
        workbook.CalculateFormula();

        // Save the workbook (adjust the folder if needed)
        string outputPath = "output.xlsx";
        workbook.Save(outputPath);
        Console.WriteLine($"Workbook saved to {outputPath}. Open it to see the wrapped results.");
    }
}
```

---

## Заключение

Теперь вы знаете **how to use wrapcols** (и его аналог `WRAPROWS`) из C# для преобразования данных в листе Excel, и понимаете, почему **recalculate excel formulas** является обязательным шагом. Этот шаблон — *create excel workbook c# → insert WRAP functions → recalculate* — является надёжной основой для любой задачи отчётности или представления данных, требующей динамических раскладок столбцов или строк.

Что дальше? Попробуйте поэкспериментировать с:

- Различным количеством столбцов/строк (`WRAPCOLS(..., 5)` или `WRAPROWS(..., 4)`).  
- Комбинированием `WRAPCOLs` с другими функциями динамических массивов, такими как `FILTER` или `SORT`.  
- Экспортом книги в PDF с помощью `workbook.Save("report.pdf", SaveFormat.Pdf)`.

Не стесняйтесь изменять пример, добавлять стили или интегрировать его в более крупный конвейер автоматизации. Если возникнут проблемы, оставьте комментарий ниже — приятного кодинга!

![Диаграмма, показывающая как wrapcols и wraprows преобразуют один столбец в сетку – пример how to use wrapcols](wrapcols-wraprows-diagram.png "пример how to use wrapcols")

## Что стоит изучить дальше?

Следующие руководства охватывают тесно связанные темы, которые развивают техники, продемонстрированные в этом руководстве. Каждый ресурс включает полные рабочие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в своих проектах.

- [Как использовать Aspose.Cells для .NET для группировки строк и столбцов в Excel](/cells/english/net/data-analysis/excel-grouping-aspose-cells-net/)
- [Как скрыть строки и столбцы в Excel с помощью Aspose.Cells .NET: Полное руководство](/cells/english/net/range-management/aspose-cells-net-hide-rows-columns-excel/)
- [Как создавать и настраивать Excel‑книги с Aspose.Cells .NET: Пошаговое руководство](/cells/english/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}