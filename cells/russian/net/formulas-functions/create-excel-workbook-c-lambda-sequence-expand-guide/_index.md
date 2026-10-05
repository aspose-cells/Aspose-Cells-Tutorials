---
category: general
date: 2026-03-30
description: Создайте Excel‑книгу в C# с использованием Aspose.Cells. Узнайте, как
  применять лямбда‑функцию в Excel, функцию последовательности в Excel, расширять
  массив в Excel и сохранять книгу в формате xlsx.
draft: false
keywords:
- create excel workbook c#
- lambda function excel
- save workbook as xlsx
- sequence function excel
- expand array excel
language: ru
og_description: Быстро создайте книгу Excel на C#. Это руководство показывает, как
  использовать лямбда‑функцию Excel, функцию последовательности Excel, расширение
  массива Excel и сохранить книгу в формате xlsx.
og_title: Создание рабочей книги Excel на C# – Руководство по Lambda, SEQUENCE и EXPAND
tags:
- Aspose.Cells
- C#
- Excel automation
title: Создание книги Excel на C# – Руководство по Lambda, SEQUENCE и EXPAND
url: /ru/net/formulas-functions/create-excel-workbook-c-lambda-sequence-expand-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание Excel Workbook C# – Lambda, SEQUENCE & EXPAND руководство

Когда‑нибудь вам нужно было **создать Excel workbook C#** для автоматизированного отчёта, но вы не знали, какие вызовы API использовать? Вы не одиноки — многие разработчики сталкиваются с тем же самым, когда впервые погружаются в программную генерацию Excel. В этом руководстве вы увидите полностью готовый, исполняемый пример, который охватывает всё от новой **SEQUENCE function Excel** до мощной **LAMBDA function Excel**, а также как **expand array Excel** результаты.

Мы также покажем точные шаги, как **save workbook as xlsx**, чтобы вы могли передать файл любому пользователю Excel. К концу этого урока у вас будет надёжный, готовый к продакшену фрагмент кода, который можно вставить в любой .NET‑проект. Никаких расплывчатых ссылок «см. документацию» — только работающий код.

## Что вам понадобится

- **.NET 6.0 или новее** — пример ориентирован на .NET 6, но подойдёт любая современная версия.  
- **Aspose.Cells for .NET** — установить через NuGet (`Install-Package Aspose.Cells`).  
- Базовое понимание синтаксиса C# (переменные, объекты и lambda‑выражения).  
- IDE, с которым вам удобно работать (Visual Studio, Rider или VS Code).  

Вот и всё. Никакого дополнительного COM‑interop, без установки Office на сервер — Aspose.Cells обрабатывает всё в памяти.

## Создание Excel Workbook C# – пошаговая реализация

Ниже мы разбиваем процесс на небольшие шаги. Каждый шаг имеет чёткий заголовок, короткий фрагмент кода и объяснение **почему** мы это делаем. Смело копируйте полный блок в конце и запускайте как консольное приложение.

### Шаг 1 – Инициализация нового Workbook

Сначала нам нужен пустой объект workbook, представляющий файл Excel в памяти.

```csharp
using Aspose.Cells;

// Step 1: Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();               // empty workbook
Worksheet sheet = workbook.Worksheets[0];         // default first sheet
```

*Почему это важно:* `Workbook` — точка входа для всех операций Aspose.Cells. Получив первый `Worksheet`, мы получаем холст, где можем записывать формулы, значения или форматирование.  

> **Pro tip:** Если нужны несколько листов, просто вызовите `workbook.Worksheets.Add()` и сохраните ссылку на каждый.

### Шаг 2 – Использование функции SEQUENCE Excel для генерации данных

**sequence function excel** создаёт динамический массив чисел без VBA. Мы разместим её в ячейке `A1` и позволим Excel автоматически расширить диапазон.

```csharp
// Step 2: Generate a 5‑row, 1‑column array from a SEQUENCE
sheet["A1"].Formula = "EXPAND(SEQUENCE(3),5,1)"; // 1..3 padded with blanks
```

*Почему это важно:* `SEQUENCE(3)` возвращает `[1,2,3]`. Обернув её в `EXPAND`, мы принудительно получаем диапазон из 5 строк, заполняя лишние строки пустыми значениями. Это демонстрирует одновременно **sequence function excel** и **expand array excel**.

### Шаг 3 – Агрегация чисел с помощью функции LAMBDA Excel

Теперь продемонстрируем возможности **lambda function excel**. Мы сложим числа от 1 до 5, используя новую функцию `REDUCE`, которая внутри опирается на lambda.

```csharp
// Step 3: Aggregate a sequence (sum 1..5) using REDUCE/LAMBDA
sheet["B1"].Formula = "REDUCE(0, SEQUENCE(5), LAMBDA(a,b, a+b))"; // result = 15
```

*Почему это важно:* `REDUCE` проходит по массиву, полученному из `SEQUENCE(5)`, передавая каждый элемент (`b`) в lambda вместе с аккумулятором (`a`). Lambda `a+b` складывает их, в результате в `B1` будет `15`. Это чистый, только‑формульный способ выполнять редукцию без циклов в C#.

### Шаг 4 – Применение тригонометрических функций непосредственно в ячейках

Встроенные математические функции Excel удобны для быстрых вычислений. Мы разместим котангенс и гиперболический котангенс в соседних ячейках.

```csharp
// Step 4: Trigonometric functions directly in Excel cells
sheet["C1"].Formula = "COT(PI()/4)";   // evaluates to 1
sheet["D1"].Formula = "COTH(1)";      // hyperbolic cotangent of 1
```

*Почему это важно:* Показано, что можно сочетать классические математические функции с новыми динамическими массивными формулами. Нет необходимости вычислять эти значения в C#, если только у вас нет особых требований к производительности.

### Шаг 5 – Вычисление всех формул

Aspose.Cells не вычисляет формулы автоматически при их установке. Нужно явно вызвать вычисление.

```csharp
// Step 5: Force calculation so that cells store the results
workbook.CalculateFormula();
```

*Почему это важно:* После этого вызова свойство `Value` каждой ячейки содержит вычисленный результат, готовый к сохранению или чтению обратно.

### Шаг 6 – Сохранение Workbook в формате Xlsx

Наконец, сохраняем workbook на диск, используя шаблон **save workbook as xlsx**.

```csharp
// Step 6: Save the workbook to an Excel file (XLSX format)
string outputPath = Path.Combine(
    Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
    "NewFunctions.xlsx");

workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to: {outputPath}");
```

*Почему это важно:* Метод `Save` автоматически определяет расширение файла. Указывая “.xlsx”, мы гарантируем совместимость с современными версиями Excel. Путь указывает на рабочий стол для удобного доступа во время тестирования.

### Полный рабочий пример

Ниже полный код программы, который можно вставить в новый консольный проект. Он включает все перечисленные шаги, а также небольшой блок проверки, выводящий вычисленные значения в консоль.

```csharp
using System;
using System.IO;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Initialize workbook
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // SEQUENCE + EXPAND
        sheet["A1"].Formula = "EXPAND(SEQUENCE(3),5,1)";

        // REDUCE with LAMBDA
        sheet["B1"].Formula = "REDUCE(0, SEQUENCE(5), LAMBDA(a,b, a+b))";

        // Trig functions
        sheet["C1"].Formula = "COT(PI()/4)";
        sheet["D1"].Formula = "COTH(1)";

        // Calculate formulas
        workbook.CalculateFormula();

        // Verify results (optional)
        Console.WriteLine("A1‑A5 (expanded SEQUENCE):");
        for (int i = 0; i < 5; i++)
        {
            Console.WriteLine($"  Row {i + 1}: {sheet.Cells[i, 0].Value ?? "blank"}");
        }
        Console.WriteLine($"B1 (sum 1‑5): {sheet["B1"].Value}");
        Console.WriteLine($"C1 (cot(π/4)): {sheet["C1"].Value}");
        Console.WriteLine($"D1 (coth(1)): {sheet["D1"].Value}");

        // Save workbook
        string outputPath = Path.Combine(
            Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
            "NewFunctions.xlsx");
        workbook.Save(outputPath);
        Console.WriteLine($"Workbook saved to: {outputPath}");
    }
}
```

**Ожидаемый вывод в консоли**

```
A1‑A5 (expanded SEQUENCE):
  Row 1: 1
  Row 2: 2
  Row 3: 3
  Row 4: blank
  Row 5: blank
B1 (sum 1‑5): 15
C1 (cot(π/4)): 1
D1 (coth(1)): 1.31303528549933
Workbook saved to: C:\Users\YourName\Desktop\NewFunctions.xlsx
```

И когда вы откроете *NewFunctions.xlsx*, вы увидите те же числа, расположенные в первых четырёх столбцах.

![create excel workbook c# screenshot of the resulting spreadsheet](/images/create-excel-workbook-csharp.png)

## Пограничные случаи, советы и часто задаваемые вопросы

- **Что делать, если нужен более чем один лист?**  
  Просто вызовите `workbook.Worksheets.Add()` и повторите назначение формул для каждого нового объекта `Worksheet`.  

- **Можно ли использовать более старые версии Excel?**  
  Динамические массивные функции (`SEQUENCE`, `EXPAND`, `REDUCE`) требуют Excel 365 или Excel 2021+. Если вы нацелены на более старые версии, используйте классические формулы или вычисляйте значения в C# перед записью.  

- **Беспокойства по поводу производительности?**  
  Для тысяч строк установка формул на диапазон и последующий вызов `CalculateFormula` обычно быстрее, чем цикл с поэлементным присваиванием значений.  

- **Сохранение в поток вместо файла?**  
  `work

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}