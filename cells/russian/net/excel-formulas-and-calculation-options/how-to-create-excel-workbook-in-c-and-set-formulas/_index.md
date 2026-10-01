---
category: general
date: 2026-10-01
description: Быстро создайте книгу Excel на C#, научитесь задавать формулу, вычислять
  котангенс и использовать функцию PI в Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook c#
- how to calculate cot
- set formula in cell
- write formula to cell
- how to use pi function
language: ru
lastmod: 2026-10-01
og_description: Создайте Excel‑книгу в C# с помощью Aspose.Cells. Узнайте, как задать
  формулу, использовать функцию PI и вычислять котангенс за несколько простых шагов.
og_image_alt: Diagram showing an Excel workbook created in C# with a formula in cell
  A1
og_title: Создать рабочую книгу Excel в C# — задать формулы и вычислить котангенс
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Create Excel workbook in C# quickly, learn how to set a formula, calculate
    cotangent, and use the PI function in Aspose.Cells.
  headline: How to create Excel workbook in C# and set formulas
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: Как создать книгу Excel в C# и задать формулы
url: /ru/net/excel-formulas-and-calculation-options/how-to-create-excel-workbook-in-c-and-set-formulas/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как создать рабочую книгу Excel в C# и задать формулы

Если вам нужно **create Excel workbook C#** код, который записывает формулу в ячейку, это руководство покажет, как это сделать. Вы увидите, как задать формулу в листе, использовать встроенную функцию PI и вычислить котангенс угла — всё с помощью Aspose.Cells.

В руководстве рассматривается всё: от инициализации рабочей книги до получения вычисленного результата, так что вы можете скопировать полный пример в свой проект без каких‑либо пропусков.

## Требования

Перед началом убедитесь, что у вас есть:

* .NET 6.0 или более поздняя версия установлен  
* Действующая лицензия Aspose.Cells (или временный оценочный ключ)  
* Visual Studio 2022 или любой предпочитаемый вами IDE для C#  

Дополнительные пакеты NuGet не требуются, кроме `Aspose.Cells`.

## Создание рабочей книги Excel в C#

Первый шаг — создать новый объект `Workbook`. Этот объект представляет весь файл Excel в памяти и даёт доступ к его листам.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook and get the first worksheet
        var workbook = new Workbook();                 // creates an empty .xlsx file
        var worksheet = workbook.Worksheets[0];        // the default first sheet

        // Continue with the rest of the steps...
```

Создание рабочей книги таким образом гарантирует, что файл готов к дальнейшему манипулированию, например, добавлению данных, стилизации ячеек или записи формул.

## Задать формулу в ячейке с использованием функции PI

Теперь вы **write formula to cell** A1. Формула использует функцию `PI()` для получения константы π и функцию `COT` для вычисления её котангенса.

```csharp
        // Step 2: Set a formula in cell A1 (row 0, column 0)
        // The formula calculates the cotangent of π/4, which equals 1
        worksheet.Cells[0, 0].Formula = "=COT(PI()/4)";

        // Continue with calculation...
```

*Почему это важно*: `PI()` — встроенная функция Excel, возвращающая значение π. Деля её на 4, получаем 45°, а `COT` возвращает котангенс этого угла. Это демонстрирует **how to use pi function** внутри формулы Excel из C#.

## Как вычислить котангенс с помощью Aspose.Cells

Если вам интересно **how to calculate cot** без ручного преобразования углов, функция `COT` делает всю тяжелую работу. Она принимает угол в радианах, поэтому его можно комбинировать с `PI()` для типовых углов.

```csharp
        // Step 3: Recalculate the workbook so the formula is evaluated
        workbook.Calculate();

        // Step 4: Retrieve and display the calculated result
        double result = worksheet.Cells[0, 0].DoubleValue;
        Console.WriteLine($"Cotangent of PI/4 = {result}");
    }
}
```

Запуск программы выводит:

```
Cotangent of PI/4 = 1
```

Поскольку `COT(π/4)` равно 1, вывод подтверждает, что формула была правильно **set formula in cell** и вычислена.

## Записать формулу в ячейку — дополнительные советы

* **Multiple formulas**: Вы можете назначить формулу любой ячейке, используя свойство `Formula`, например `worksheet.Cells["B2"].Formula = "=SIN(PI()/2)";`.
* **International settings**: Aspose.Cells учитывает локаль рабочей книги, поэтому имена функций остаются на английском (`PI`, `COT`) независимо от региональных настроек пользователя.
* **Performance**: Если вам нужно задать тысячи формул, сгруппируйте их и вызовите `workbook.Calculate()` один раз в конце, чтобы избежать повторных пересчетов.

## Полный исполняемый пример

Ниже представлен полный код программы, который можно скопировать и вставить в консольный проект. В нём включены все необходимые директивы `using` и показан полный процесс от создания рабочей книги до вывода результата.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // Create a new workbook and obtain the first worksheet
        var workbook = new Workbook();
        var worksheet = workbook.Worksheets[0];

        // Write a formula that uses the PI function and calculates cotangent
        worksheet.Cells[0, 0].Formula = "=COT(PI()/4)";

        // Force calculation so the formula value is materialized
        workbook.Calculate();

        // Read the calculated value and display it
        double cotValue = worksheet.Cells[0, 0].DoubleValue;
        Console.WriteLine($"Cotangent of PI/4 = {cotValue}");

        // Optional: save the workbook to verify the formula visually
        workbook.Save("CotExample.xlsx");
    }
}
```

**Ожидаемый вывод** при запуске программы:

```
Cotangent of PI/4 = 1
```

Сгенерированный файл `CotExample.xlsx` содержит формулу в ячейке A1, что позволяет открыть его в Excel и увидеть тот же результат.

## Заключение

Теперь вы знаете, как **create Excel workbook C#** код, который записывает формулу, использует функцию `PI` и **calculates cot** с помощью Aspose.Cells. Пример охватывает весь жизненный цикл: создание рабочей книги, **set formula in cell**, пересчёт и получение результата.

Дальнейшие шаги, которые вы можете изучить:

* Применить **write formula to cell** для более сложных вычислений, например финансовых моделей.  
* Использовать **set formula in cell** совместно с условным форматированием для выделения результатов.  
* Скомбинировать **how to use pi function** с тригонометрическими диаграммами для научных отчётов.

Не стесняйтесь экспериментировать с разными углами, функциями и макетами листов. Овладение работой с формулами в C# открывает путь к полностью автоматизированным конвейерам отчётности в Excel. Приятного кодинга!

## Что изучить дальше?

Следующие руководства охватывают тесно связанные темы, которые развивают техники, продемонстрированные в этом руководстве. Каждый ресурс содержит полностью работающие примеры кода с пошаговыми объяснениями, помогающими освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [Как вычислить котангенс в Excel с C# – создать рабочую книгу, использовать EXPAND](/cells/english/net/formulas-functions/how-to-calculate-cotangent-in-excel-with-c-create-workbook-u/)
- [Как использовать WRAPCOLS в C# – создать рабочую книгу Excel с функциями Wrap](/cells/english/net/formulas-functions/how-to-use-wrapcols-in-c-create-excel-workbook-with-wrap-fun/)
- [Как создать именованные диапазоны, ограниченные рабочей книгой, в Excel с помощью Aspose.Cells .NET](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}