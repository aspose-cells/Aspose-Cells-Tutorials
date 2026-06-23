---
category: general
date: 2026-03-22
description: Как использовать лямбда‑выражения в C# для работы с формулами Excel.
  Научитесь записывать формулу в ячейку, преобразовывать диапазон в массив, выводить
  массив в консоль и вычислять котангенс в Excel.
draft: false
keywords:
- how to use lambda
- display array in console
- convert range to array
- write formula to cell
- calculate cotangent in excel
language: ru
og_description: Как использовать лямбда‑выражения в C# для работы с формулами Excel,
  преобразования диапазона в массив, записи формулы в ячейку, вывода массива в консоль
  и вычисления котангенса в Excel.
og_title: Как использовать лямбда‑выражения в C# с формулами Excel – пошагово
tags:
- C#
- Aspose.Cells
- Excel Automation
- Lambda Expressions
title: Как использовать лямбда‑выражения в C# с формулами Excel – полное руководство
url: /ru/net/formulas-functions/how-to-use-lambda-in-c-with-excel-formulas-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как использовать Lambda в C# с формулами Excel – Полное руководство

Когда‑то задавались вопросом **как использовать lambda**, когда автоматизируете Excel из C#? Вы не одиноки. Многие разработчики сталкиваются с проблемой, когда нужно объединить мощь новых динамических функций массивов Excel с возможностью `LAMBDA` в C#. Хорошая новость? На самом деле всё довольно просто, как только вы видите, как части сочетаются.

В этом руководстве мы пройдём через **запись формулы в ячейку**, **преобразование диапазона в массив**, **вывод этого массива в консоль**, а также **вычисление котангенса в Excel** — всё это показывая вам **как использовать lambda** внутри вызова `REDUCE`. К концу вы получите готовый фрагмент кода, который можно вставить в любой .NET‑проект, использующий Aspose.Cells (или аналогичную библиотеку).

---

## Что вы узнаете

- Как **записать формулу в ячейку** с помощью C#.
- Как **преобразовать диапазон в массив** с помощью функции `EXPAND`.
- Как **вывести массив в консоль** после вычисления.
- Как **вычислить котангенс в Excel** с помощью `COT` и `COTH`.
- Точный синтаксис **как использовать lambda** внутри функции `REDUCE` Excel из C#.

> **Prerequisite:** Вам нужна актуальная версия .NET (Core 6+ или .NET Framework 4.7+) и библиотека Aspose.Cells for .NET, установленная через NuGet.

---

## Шаг 1: Создать книгу и записать формулу в ячейку

Первым делом мы создаём новую книгу и получаем первый лист. Затем **записываем формулу в ячейку** – в данном случае `A1` будет содержать результат вызова `EXPAND`.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Write formula to A1 – we’ll expand B1:C2 into a 4‑by‑5 array later
        worksheet.Cells["A1"].Formula = "=EXPAND(B1:C2, 4, 5)";
```

**Почему это важно:** Запись формулы напрямую из кода позволяет генерировать сложные таблицы «на лету», не открывая Excel. Это также подготавливает основу для следующего шага, где мы **преобразуем диапазон в массив**.

---

## Шаг 2: Преобразовать диапазон в массив с помощью EXPAND

`EXPAND` – это способ Excel превратить небольшой диапазон в большую матрицу. Поместив формулу в `A1`, Excel «разольёт» блок 4 × 5, начиная с этой ячейки. С C# нам не нужно вручную копировать значения – библиотека выполнит всю тяжёлую работу при вызове `Calculate`.

```csharp
        // The EXPAND formula will spill into A1:E4 (4 rows × 5 columns)
        // No extra code needed – the workbook will handle the spill.
```

**Как использовать lambda:** Пока нет, но скоро. Сначала нам нужны данные в листе, затем мы сократим их с помощью lambda.

---

## Шаг 3: Использовать LAMBDA внутри REDUCE – ядро «Как использовать Lambda»

Excel 365 представил `REDUCE`, который принимает **начальное значение**, **диапазон** и **LAMBDA**, определяющий, как объединять каждый элемент. С C# мы просто задаём строку формулы; lambda живёт внутри формулы Excel, а не в коде C#.

```csharp
        // Reduce the spilled array by summing all its values.
        // This demonstrates how to use lambda inside REDUCE.
        worksheet.Cells["E1"].Formula = "=REDUCE(0, A1:D4, LAMBDA(acc, x, acc + x))";
```

**Объяснение:**  
- `0` – начальное значение аккумулятора (`acc`).  
- `A1:D4` – диапазон, который мы хотим обработать (первые четыре столбца «разлитого» блока).  
- `LAMBDA(acc, x, acc + x)` указывает Excel добавить каждую ячейку (`x`) к аккумулятору.  

Это и есть суть **как использовать lambda** для агрегирования в контексте таблицы.

---

## Шаг 4: Вычисление котангенса в Excel – от градусов к гиперболическому

Если нужны тригонометрические результаты, функции Excel `COT` и `COTH` работают без проблем. Мы разместим их в `G1` и `G2` соответственно.

```csharp
        // Demonstrate trigonometric functions – cotangent and hyperbolic cotangent
        worksheet.Cells["G1"].Formula = "=COT(PI()/4)";   // Expected result: 1
        worksheet.Cells["G2"].Formula = "=COTH(1)";      // Hyperbolic cotangent of 1
```

**Почему это удобно:** Знание **calculate cotangent in Excel** может избавить вас от написания собственного математического кода, особенно когда книга будет использоваться не‑разработчиками.

---

## Шаг 5: Принудительный расчёт и получение разлитого массива

Теперь мы заставляем книгу вычислить все формулы, а затем извлекаем разлитый массив из `A1`. Здесь мы **выводим массив в консоль**.

```csharp
        // Force calculation of all formulas
        workbook.Calculate();

        // Retrieve the spilled array from A1 as a 2‑D object
        var expanded = worksheet.Cells["A1"].Value;

        // Pretty‑print the 2‑D array to the console
        Console.WriteLine("Expanded array from A1 (4×5):");
        if (expanded is object[,] matrix)
        {
            for (int r = 0; r < matrix.GetLength(0); r++)
            {
                for (int c = 0; c < matrix.GetLength(1); c++)
                {
                    Console.Write($"{matrix[r, c]}\t");
                }
                Console.WriteLine();
            }
        }
        else
        {
            Console.WriteLine("Unexpected data type.");
        }

        // Show the result of the REDUCE lambda
        Console.WriteLine($"\nSum of A1:D4 (via REDUCE lambda): {worksheet.Cells["E1"].Value}");

        // Show cotangent results
        Console.WriteLine($"Cotangent of π/4: {worksheet.Cells["G1"].Value}");
        Console.WriteLine($"Hyperbolic cotangent of 1: {worksheet.Cells["G2"].Value}");
    }
}
```

**Что вы увидите:**  
- Красиво отформатированную матрицу 4 × 5, выведенную построчно.  
- Сумму, вычисленную lambda‑функцией `REDUCE`.  
- Два значения котангенса.

Это завершает процесс от **записи формулы в ячейку** до **вывода массива в консоль**.

---

## Полный рабочий пример (готов к копированию)

Ниже представлен весь код программы, который можно вставить в консольное приложение. Не забудьте сначала добавить пакет `Aspose.Cells` через NuGet (`dotnet add package Aspose.Cells`).

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Initialize workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Step 2: Write EXPAND formula (convert range to array)
        worksheet.Cells["A1"].Formula = "=EXPAND(B1:C2, 4, 5)";

        // Step 3: Use REDUCE with LAMBDA (how to use lambda)
        worksheet.Cells["E1"].Formula = "=REDUCE(0, A1:D4, LAMBDA(acc, x, acc + x))";

        // Step 4: Calculate cotangent values (calculate cotangent in excel)
        worksheet.Cells["G1"].Formula = "=COT(PI()/4)";   // Expected: 1
        worksheet.Cells["G2"].Formula = "=COTH(1)";

        // Step 5: Force calculation
        workbook.Calculate();

        // Step 6: Retrieve and display the expanded array (display array in console)
        var expanded = worksheet.Cells["A1"].Value;
        Console.WriteLine("Expanded array from A1 (4×5):");
        if (expanded is object[,] matrix)
        {
            for (int r = 0; r < matrix.GetLength(0); r++)
            {
                for (int c = 0; c < matrix.GetLength(1); c++)
                {
                    Console.Write($"{matrix[r, c]}\t");
                }
                Console.WriteLine();
            }
        }
        else
        {
            Console.WriteLine("Unexpected data type.");
        }

        // Show REDUCE result
        Console.WriteLine($"\nSum of A1:D4 (via REDUCE lambda): {worksheet.Cells["E1"].Value}");

        // Show cotangent results
        Console.WriteLine($"Cotangent of π/4: {worksheet.Cells["G1"].Value}");
        Console.WriteLine($"Hyperbolic cotangent of 1: {worksheet.Cells["G2"].Value}");
    }
}
```

**Ожидаемый вывод в консоль (значения могут отличаться в зависимости от содержимого ячеек B1:C2, которые по умолчанию равны 0):**

```
Expanded array from A1 (4×5):
0   0   0   0   0
0   0   0   0   0
0   0   0   0   0
0   0   0   0   0

Sum of A1:D4 (via REDUCE lambda): 0
Cotangent of π/4: 1
Hyperbolic cotangent of 1: 1.31303528549933
```

Не стесняйтесь заполнить `B1:C2` своими числами перед запуском – матрица отразит эти значения.

---

## Полезные советы и распространённые подводные камни

- **Pro tip:** Если нужно, чтобы разлитый диапазон начинался в другом месте, просто измените целевую ячейку (`A1`). Функция `EXPAND` учитывает эту привязку.  
- **Watch out for:** Пустые ячейки в исходном диапазоне становятся `0` в разлитом массиве, что может влиять на сумму в `REDUCE`.  
- **Edge case:** Когда в книге есть формулы, зависящие от волатильных функций (например, `NOW()`), вызывайте `workbook.Calculate()` после установки всех формул, чтобы всё было актуально.  
- **Performance note:** Для огромных разливов рекомендуется ограничить размер в вызове `EXPAND`; иначе можно выделить больше памяти, чем требуется.  
- **Compatibility:** The `

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}