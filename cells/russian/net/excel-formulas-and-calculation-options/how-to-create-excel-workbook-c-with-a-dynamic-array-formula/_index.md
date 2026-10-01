---
category: general
date: 2026-10-01
description: Быстро создайте Excel‑книгу в C# и изучите пример формулы динамического
  массива для записи формул Excel на C# в Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook c#
- dynamic array formula example
- write excel formula c#
language: ru
lastmod: 2026-10-01
og_description: Быстро создайте Excel‑книгу в C# и посмотрите пример динамической
  формулы массива, демонстрирующий, как писать формулы Excel в C# с помощью Aspose.Cells.
  Следуйте пошаговому руководству, чтобы сгенерировать, вычислить и сохранить файл.
og_image_alt: Screenshot of C# code creating an Excel workbook and applying a SORT
  dynamic array formula
og_title: Создать рабочую книгу Excel на C# с формулой динамического массива
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Create Excel workbook C# quickly and learn a dynamic array formula
    example to write Excel formula C# in Aspose.Cells.
  headline: How to create Excel workbook C# with a dynamic array formula
  type: TechArticle
- description: Create Excel workbook C# quickly and learn a dynamic array formula
    example to write Excel formula C# in Aspose.Cells.
  name: How to create Excel workbook C# with a dynamic array formula
  steps:
  - name: Verifying the result (expected output)
    text: 'You can print the spilled values to the console to confirm the calculation
      succeeded:'
  - name: What if I need to use a different dynamic array function?
    text: 'Replace the formula string with any other dynamic array function, such
      as `=FILTER(A2:A10, B2:B10>10)` or `=UNIQUE(A2:A10)`. The same **write Excel
      formula C#** pattern applies:'
  - name: How do I handle formulas that reference other worksheets?
    text: 'Reference another sheet by its name:'
  - name: Can I suppress automatic calculation and calculate later?
    text: 'Yes. Set the workbook’s calculation mode to manual:'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Как создать книгу Excel в C# с динамической формулой массива
url: /ru/net/excel-formulas-and-calculation-options/how-to-create-excel-workbook-c-with-a-dynamic-array-formula/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как создать книгу Excel на C# с динамической формулой массива

Если вам нужно **создать книгу Excel на C#** программно, это руководство покажет, как сделать это с помощью Aspose.Cells. Вы также получите **пример динамической формулы массива**, демонстрирующий лучший способ **записать формулу Excel на C#** для современных функций Excel, таких как `SORT`.

Раньше создание файла Excel из C# требовало COM‑interop или ручной генерации XML, что было хрупким и трудно поддерживаемым. К концу этого урока у вас будет полностью рабочая книга, автоматически вычисляющая динамический массив, и вы поймёте, почему такой подход надёжен для автоматизации в продакшн‑среде.

## Требования

Прежде чем начать, убедитесь, что у вас есть:

- .NET 6.0 или новее (код работает и с .NET Core, и с .NET Framework)
- Действительная лицензия Aspose.Cells или бесплатный ключ оценки
- Visual Studio 2022 (или любой IDE, поддерживающий C#)
- Базовые знания синтаксиса C# и формул Excel

Дополнительные пакеты NuGet не требуются, кроме `Aspose.Cells`, который можно добавить с помощью:

```bash
dotnet add package Aspose.Cells
```

## Шаг 1: Создайте проект C# и подключите Aspose.Cells

Создайте новое консольное приложение и добавьте ссылку на Aspose.Cells. Этот шаг важен, потому что библиотека предоставляет `Workbook`, `Worksheet` и движок вычислений, необходимые для **записи формулы Excel на C#**.

```csharp
// Program.cs
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // The rest of the tutorial code lives inside this method.
    }
}
```

> **Почему это важно:** Aspose.Cells абстрагирует детали низкоуровневого OpenXML, позволяя сосредоточиться на бизнес‑логике, а не на особенностях формата файла.

## Шаг 2: Создайте книгу Excel и получите первый лист

Теперь мы **создаём книгу Excel на C#**, создавая объект `Workbook`. По умолчанию книга содержит один лист, который мы получаем для дальнейших операций.

```csharp
// Step 2: Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();               // creates a blank .xlsx file in memory
Worksheet worksheet = workbook.Worksheets[0];    // first (and only) sheet by default
```

> **Совет:** Если нужны несколько листов, вызовите `workbook.Worksheets.Add()` перед их использованием.

## Шаг 3: Заполните исходные данные для динамического массива

Функциям динамического массива, таким как `SORT`, нужен исходный диапазон. Заполним ячейки *A2:A10* несортированными числами, чтобы формула `SORT` могла продемонстрировать своё поведение.

```csharp
// Step 3: Fill A2:A10 with sample data
int[] numbers = { 42, 7, 19, 33, 5, 27, 14, 8, 21 };
for (int i = 0; i < numbers.Length; i++)
{
    worksheet.Cells[i + 1, 0].PutValue(numbers[i]); // Row i+2, Column A (0‑based index)
}
```

> **Зачем это делаем:** Наличие конкретных данных позволяет увидеть **пример динамической формулы массива** в действии без необходимости внешних файлов ввода.

## Шаг 4: Запишите динамическую формулу массива в ячейку A1

Это ядро части **записи формулы Excel на C#**. Мы присваиваем формулу `SORT` ячейке *A1*. Поскольку `SORT` — функция динамического массива, Excel автоматически «разольёт» отсортированные результаты в ячейки ниже.

```csharp
// Step 4: Insert a dynamic array formula (SORT) into cell A1
worksheet.Cells[0, 0].Formula = "=SORT(A2:A10)";
```

> **Пояснение:**  
> - `worksheet.Cells[0, 0]` указывает на ячейку **A1** (строка 0, столбец 0).  
> - Строка `=SORT(A2:A10)` — обычная формула Excel. Aspose.Cells разбирает её так же, как Excel, обеспечивая полную поддержку современных функций динамических массивов.

## Шаг 5: Пересчитайте книгу, чтобы формула заполнила данные автоматически

Aspose.Cells не пересчитывает формулы автоматически при записи. Необходимо явно вызвать вычисление, чтобы увидеть разлитые результаты.

```csharp
// Step 5: Recalculate the workbook so the formula evaluates
workbook.Calculate();   // runs the calculation engine once
```

После этого вызова ячейки **A1:A9** будут содержать отсортированный список: 5, 7, 8, 14, 19, 21, 27, 33, 42.

### Проверка результата (ожидаемый вывод)

Вы можете вывести разлитые значения в консоль, чтобы убедиться, что вычисление прошло успешно:

```csharp
Console.WriteLine("Sorted values from A1 down:");
for (int row = 0; row < 9; row++)
{
    Console.WriteLine(worksheet.Cells[row, 0].StringValue);
}
```

**Ожидаемый вывод в консоли**

```
Sorted values from A1 down:
5
7
8
14
19
21
27
33
42
```

> **Примечание о граничных случаях:** Если исходный диапазон содержит нечисловые данные, `SORT` отсортирует их лексикографически. Всегда проверяйте типы данных перед применением функций, работающих только с числами.

## Шаг 6: Сохраните книгу на диск (по желанию)

Сохранение файла позволяет открыть его в Excel и визуально увидеть динамический массив. Этот шаг не обязателен для самого вычисления, но полезен для отладки и распространения.

```csharp
// Step 6: Save the workbook as an .xlsx file
string outputPath = "SortedNumbers.xlsx";
workbook.Save(outputPath, SaveFormat.Xlsx);
Console.WriteLine($"Workbook saved to {outputPath}");
```

Когда вы откроете *SortedNumbers.xlsx* в Excel 365 или новее, увидите, как отсортированный список автоматически «разливается» из **A1** вниз — именно то, что создал **пример динамической формулы массива** из C#.

## Полный рабочий пример

Объединив все части, получаем полностью готовую программу:

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1. Create workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 2. Fill source data (A2:A10)
        int[] numbers = { 42, 7, 19, 33, 5, 27, 14, 8, 21 };
        for (int i = 0; i < numbers.Length; i++)
        {
            worksheet.Cells[i + 1, 0].PutValue(numbers[i]); // A2:A10
        }

        // 3. Write dynamic array formula (SORT) into A1
        worksheet.Cells[0, 0].Formula = "=SORT(A2:A10)";

        // 4. Force calculation so the array spills
        workbook.Calculate();

        // 5. Display the spilled values in the console
        Console.WriteLine("Sorted values from A1 down:");
        for (int row = 0; row < 9; row++)
        {
            Console.WriteLine(worksheet.Cells[row, 0].StringValue);
        }

        // 6. Save the workbook (optional)
        string outputPath = "SortedNumbers.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);
        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

Запустите программу (`dotnet run`), и вы увидите отсортированные числа в консоли, а также подтверждение, что файл был сохранён.

## Часто задаваемые вопросы и варианты

### Что делать, если нужно использовать другую функцию динамического массива?

Замените строку формулы любой другой функцией динамического массива, например `=FILTER(A2:A10, B2:B10>10)` или `=UNIQUE(A2:A10)`. То же самое применимо к паттерну **записи формулы Excel на C#**:

```csharp
worksheet.Cells[0, 0].Formula = "=UNIQUE(A2:A10)";
```

### Как работать с формулами, ссылающимися на другие листы?

Ссылайтесь на другой лист по его имени:

```csharp
worksheet.Cells[0, 0].Formula = "=SORT('Sheet2'!A2:A10)";
```

Aspose.Cells автоматически разрешает ссылки между листами во время `workbook.Calculate()`.

### Можно ли отключить автоматический расчёт и выполнить его позже?

Да. Установите режим расчёта книги в ручной:

```csharp
workbook.Settings.CalcMode = CalcMode.Manual;
// ... make many changes ...
workbook.Calculate(); // call once when ready
```

Это повышает производительность, когда вы обновляете тысячи ячеек перед окончательным вычислением.

## Заключение

Теперь вы знаете, как **создать книгу Excel на C#** с помощью Aspose.Cells, вставить **пример динамической формулы массива** и **записать формулу Excel на C#**, которая автоматически «разливается». Полное решение охватывает настройку проекта, подготовку данных, вставку формулы, принудительный расчёт, проверку и опциональное сохранение файла.

Далее вы можете изучать более продвинутые сценарии: цепочку нескольких функций динамического массива, пользовательские числовые форматы или интеграцию генерации книги в веб‑API. Не забывайте всегда проверять входные данные перед применением формул и использовать мощный движок расчётов Aspose.Cells для надёжной серверной обработки Excel. Приятного кодинга!

## Что изучать дальше?

Следующие руководства охватывают тесно связанные темы, расширяющие техники, продемонстрированные в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, помогающими освоить дополнительные возможности API и исследовать альтернативные подходы в ваших проектах.

- [Create New Workbook in C# – Add Formula and Save Excel File](/cells/english/net/excel-workbook/create-new-workbook-in-c-add-formula-and-save-excel-file/)
- [Excel Automation with Aspose.Cells .NET: Mastering Workbook & Formula Calculations](/cells/english/net/formulas-functions/excel-automation-aspose-cells-net-workbook-formulas/)
- [Create Excel Workbook C# – Complete Guide with Aspose.Cells](/cells/english/net/excel-workbook/create-excel-workbook-c-complete-guide-with-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}