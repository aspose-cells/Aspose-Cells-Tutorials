---
category: general
date: 2026-02-15
description: Как использовать WRAPCOLS для создания двухколоночного макета, добавить
  формулу и сгенерировать массив последовательности в листах C# – пошаговое руководство.
draft: false
keywords:
- how to use wrapcols
- create two column layout
- how to add formula
- how to create columns
- generate sequence array
language: ru
og_description: Как использовать WRAPCOLS для создания двухколоночного макета, добавления
  формул и генерации массива последовательности в листе C# – полное руководство.
og_title: 'Как использовать WRAPCOLS: двухколоночный макет в C#'
tags:
- CSharp
- ExcelAutomation
- WorksheetFormula
title: 'Как использовать WRAPCOLS: создайте двухколоночный макет в C#'
url: /ru/net/row-and-column-management/how-to-use-wrapcols-create-a-two-column-layout-in-c/
---

write translation.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как использовать WRAPCOLS: создать двухколоночный макет в C#

Когда‑нибудь задавались вопросом **как использовать WRAPCOLS**, когда нужен быстрый двухколоночный вид внутри листа в стиле Excel? Вы не одиноки. Многие разработчики сталкиваются с проблемой, когда пытаются разбить сгенерированный список на аккуратные столбцы без написания цикла для каждой ячейки. Хорошая новость? С функцией `WRAPCOLS` вы можете поместить одну формулу в `A1` и позволить Excel (или совместимому движку) выполнить тяжелую работу.

В этом руководстве мы пройдемся по **как добавить формулу**, которая создает **двухколоночный макет**, покажем вам **как создавать столбцы** динамически и даже **генерировать массив последовательности** на лету. К концу вы получите полностью исполняемый фрагмент C#, который можно вставить в проект, запустить и увидеть аккуратный двухколоночный блок мгновенно.

## Что вы узнаете

- Цель функции `WRAPCOLS` и почему она лучше альтернативы в виде ручных циклов.  
- Как **add a formula** в ячейку листа с помощью C#.  
- Как сгенерировать массив последовательности с помощью `SEQUENCE` и передать его в `WRAPCOLS`.  
- Советы по пересчету листа, чтобы формула вычислялась сразу.  
- Обработка граничных случаев (например, пустые листы, пользовательское количество столбцов).

Никакие внешние библиотеки, кроме стандартного пакета для работы с Excel, не требуются – мы будем использовать **ClosedXML** за его простой API, но концепции применимы к EPPlus, SpreadsheetGear или даже Google Sheets через его API.

---

## Предварительные требования

- .NET 6.0 или новее (код компилируется на .NET Core и .NET Framework).  
- Ссылка на **ClosedXML** (`dotnet add package ClosedXML`).  
- Базовые знания C# – вы должны быть уверены в использовании операторов `using` и инициализации объектов.  

Если у вас уже открыт рабочий файл, вы можете пропустить часть создания файла и перейти сразу к разделу с формулой.

---

## Шаг 1: Настройка листа (How to Create Columns)

Сначала нам нужен объект `Worksheet` для работы. В ClosedXML вы получаете его из `XLWorkbook`. Ниже приведён фрагмент, который создаёт новую книгу, добавляет лист под названием *Demo* и сохраняет ссылку под именем `worksheet` для ясности.

```csharp
using ClosedXML.Excel;

namespace WrapColsDemo
{
    class Program
    {
        static void Main()
        {
            // Create a fresh workbook and add a worksheet named "Demo"
            using var workbook = new XLWorkbook();
            var ws = workbook.Worksheets.Add("Demo");

            // Rename for clarity – this is the worksheet we’ll manipulate
            var worksheet = ws;   // <-- same object, just a clearer name

            // --------------------------------------------------------------
            // Next step: write the WRAPCOLS formula
            // --------------------------------------------------------------
```

> **Почему переименовывать?**  
> Краткое имя переменной (`worksheet`) упрощает чтение последующего кода, особенно когда вы цепляете несколько операций. Это также отражает стиль именования, который вы увидите в большинстве документаций, снижая когнитивную нагрузку.

---

## Шаг 2: Запись формулы (How to Add Formula + Generate Sequence Array)

Теперь приходит волшебная строка. Мы поместим формулу в ячейку **A1**, которая делает две вещи:

1. **Generate a sequence array** из шести чисел (`SEQUENCE(6)` → 1,2,3,4,5,6).  
2. **Wrap those numbers into two columns** (`WRAPCOLS(..., 2)`).

```csharp
            // Write the WRAPCOLS formula into A1
            worksheet.Cell("A1").FormulaA1 = "=WRAPCOLS(SEQUENCE(6), 2)";

            // --------------------------------------------------------------
            // Finally, force the engine to evaluate the formula
            // --------------------------------------------------------------
```

> **Что происходит?**  
> `SEQUENCE(6)` создаёт вертикальный массив `{1;2;3;4;5;6}`. `WRAPCOLS` затем берёт этот массив и «оборачивает» его в указанное количество столбцов — в данном случае **2**. Результат — блок 3 строки × 2 столбца, выглядящий так:

| A | B |
|---|---|
| 1 | 4 |
| 2 | 5 |
| 3 | 6 |

Если изменить второй аргумент на **3**, вы получите макет из трёх столбцов. Это и есть суть **how to create columns** «на лету» без ручных циклов.

---

## Шаг 3: Пересчёт листа (Ensuring the Formula Evaluates)

ClosedXML не будет автоматически вычислять формулы при их записи. Нужно вызвать `Calculate()` у книги (или у конкретного листа), чтобы принудительно выполнить вычисление.

```csharp
            // Recalculate so the formula is evaluated immediately
            worksheet.Calculate();

            // Optional: save the workbook to inspect the result
            workbook.SaveAs("WrapColsDemo.xlsx");
        }
    }
}
```

> **Pro tip:** При работе с большими книгами вызывайте `Calculate()` только на листах, которые действительно изменились. Это экономит память и ускоряет обработку.

Когда откроете `WrapColsDemo.xlsx`, вы увидите аккуратно заполненный двухколоночный макет в диапазоне **A1:B3**. Дополнительный код для перебора строк или столбцов не требовался – всё сделал `WRAPCOLS`.

---

## Шаг 4: Проверка результата (What to Expect)

После запуска программы откройте сгенерированный файл. Вы должны увидеть:

| A | B |
|---|---|
| 1 | 4 |
| 2 | 5 |
| 3 | 6 |

Если числа отображаются вертикально (то есть все в колонке A), проверьте, что вы вызвали `worksheet.Calculate()` **после** установки формулы. Некоторые движки также требуют `workbook.Calculate()`; приведённый выше фрагмент работает с встроенным вычислителем ClosedXML.

---

## Общие варианты и граничные случаи

### Изменение количества столбцов

Чтобы **create two column layout** с другим числом строк, просто скорректируйте размер `SEQUENCE` или второй аргумент `WRAPCOLS`:

```csharp
worksheet.Cell("A1").FormulaA1 = "=WRAPCOLS(SEQUENCE(12), 3)";
```

Это создаёт блок 4 строки × 3 столбца (12 чисел, разбитых по трём столбцам).

### Использование динамического количества столбцов

Если количество столбцов берётся из переменной, внедрите его с помощью интерполяции строк:

```csharp
int colCount = 4;
worksheet.Cell("A1").FormulaA1 = $"=WRAPCOLS(SEQUENCE(8), {colCount})";
```

Теперь у вас есть **how to add formula**, адаптирующаяся во время выполнения.

### Пустые листы

Если лист пуст, `Calculate()` всё равно работает – формула заполнит ячейки, начиная с A1. Однако, если позже удалить строки/столбцы, пересекающие диапазон вывода, вы можете увидеть ошибку `#REF!`. Чтобы избежать этого, сначала очистите целевой диапазон:

```csharp
worksheet.Range("A1:Z100").Clear(); // wipes any leftovers
```

### Совместимость

`WRAPCOLS` и `SEQUENCE` являются частью **Dynamic Array** функций Excel, появившихся в Office 365. Если вы нацелены на более старые версии Excel, этих функций не будет, и придётся использовать ручной цикл. Оценщик ClosedXML имитирует поведение последней версии Excel, поэтому он безопасен для современных окружений.

---

## Полный рабочий пример (Copy‑Paste Ready)

```csharp
using ClosedXML.Excel;

namespace WrapColsDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create workbook & worksheet
            using var workbook = new XLWorkbook();
            var ws = workbook.Worksheets.Add("Demo");
            var worksheet = ws;   // clearer name

            // 2️⃣ Write WRAPCOLS formula that generates a sequence array
            worksheet.Cell("A1").FormulaA1 = "=WRAPCOLS(SEQUENCE(6), 2)";

            // 3️⃣ Force calculation so the formula resolves immediately
            worksheet.Calculate();

            // 4️⃣ Save the file (optional, but handy for verification)
            workbook.SaveAs("WrapColsDemo.xlsx");
        }
    }
}
```

**Ожидаемый результат:** При открытии *WrapColsDemo.xlsx* вы увидите аккуратный двухколоночный макет с числами от 1 до 6, расположенными как описано выше.

---

## Заключение

Мы рассмотрели **how to use WRAPCOLS** для **create a two column layout**, продемонстрировали **how to add formula** программно и увидели, как `SEQUENCE` позволяет **generate sequence array** без цикла. Используя динамические массивные функции Excel из C#, вы можете держать код лаконичным, читаемым и поддерживаемым.

Далее вы можете изучить:

- **Creating dynamic row counts** с помощью `ROWS` или `COUNTA`.  
- **Styling the output** (границы, форматы чисел) с использованием API стилизации ClosedXML.  
- **Exporting to CSV** после построения макета, для последующей обработки.

Попробуйте, измените количество столбцов и посмотрите, как быстро можно прототипировать сложные таблицы. Счастливого кодинга!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}