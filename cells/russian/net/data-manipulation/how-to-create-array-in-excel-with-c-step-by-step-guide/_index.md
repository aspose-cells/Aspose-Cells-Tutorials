---
category: general
date: 2026-02-09
description: Как создать массив в Excel с помощью C# за несколько минут – научитесь
  генерировать последовательные номера, использовать COT и сохранять книгу в формате
  XLSX.
draft: false
keywords:
- how to create array
- create excel workbook c#
- generate sequence numbers
- save workbook as xlsx
- how to use cot
language: ru
og_description: Как создать массив в Excel с помощью C# подробно рассматривается пошагово,
  включая генерацию последовательных номеров, использование COT и сохранение книги
  в формате XLSX.
og_title: Как создать массив в Excel с помощью C# – Краткое руководство
tags:
- C#
- Excel
- Aspose.Cells
title: Как создать массив в Excel с помощью C# – пошаговое руководство
url: /ru/net/data-manipulation/how-to-create-array-in-excel-with-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как создать массив в Excel с помощью C# – Пошаговое руководство

Когда‑нибудь задавались вопросом, **как создать массив** в Excel с помощью C# без того, чтобы тратить часы на изучение документации? Вы не одиноки. Многие разработчики сталкиваются с проблемой, когда им нужен динамический spill‑диапазон, быстрое тригонометрическое значение или просто чистый XLSX‑файл, сохранённый на диск. В этом руководстве мы сразу решим эту задачу — построив небольшую рабочую книгу, которая записывает расширяющуюся формулу массива, вставляет расчёт котангенса и сохраняет всё как XLSX‑файл.  

Мы также добавим несколько дополнительных приёмов: генерацию последовательных чисел, освоение функции `COT` и обеспечение того, чтобы файл оказался там, где вы хотите. К концу вы получите переиспользуемый фрагмент кода, который можно вставить в любой .NET‑проект. Без лишних слов, только работающий код.

> **Pro tip:** В примере используется популярная библиотека **Aspose.Cells**, но концепции применимы к другим пакетам автоматизации Excel (EPPlus, ClosedXML) с лишь незначительными изменениями.

---

## Что вам понадобится

- **.NET 6** или новее (код также компилируется на .NET Framework 4.7+)  
- **Aspose.Cells for .NET** – можно установить через NuGet (`Install-Package Aspose.Cells`)  
- Текстовый редактор или IDE (Visual Studio, Rider, VS Code…)  
- Права записи в папку, куда будет сохраняться выходной файл  

Это всё — без дополнительной конфигурации, без COM‑interop, только чистая управляемая сборка.

---

## Шаг 1: Как создать массив в Excel – Инициализация рабочей книги

Самое первое, что нужно сделать, когда вы хотите **как создать массив** в листе Excel, — это создать объект рабочей книги. Думайте о рабочей книге как о чистом холсте; лист — это место, где вы будете «рисовать» свои формулы.

```csharp
using Aspose.Cells;

public class ExcelArrayDemo
{
    public static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();               // <- fresh workbook
        Worksheet worksheet = workbook.Worksheets[0];    // first (and only) sheet

        // The rest of the steps follow...
```

Почему используется `Workbook()` без параметров? Он создаёт рабочую книгу в памяти с листом по умолчанию, что идеально подходит для быстрых программных задач. Если нужно открыть существующий файл, просто передайте путь к файлу в конструктор.

---

## Шаг 2: Генерация последовательных чисел с помощью EXPAND и SEQUENCE

Теперь, когда у нас есть лист, давайте решим часть задачи **генерация последовательных чисел**. Новые функции динамических массивов Excel (`SEQUENCE`, `EXPAND`) позволяют создать вертикальный список из 3 строк и автоматически «разлить» его в диапазон 3 × 5.

```csharp
        // Write a dynamic array formula that expands a 3‑row sequence into a 3×5 spill range
        // EXPAND pads the result to 5 columns, SEQUENCE generates numbers 1‑3 vertically
        worksheet.Cells["A1"].Formula = "=EXPAND(SEQUENCE(3,1,1,1),5,1)";
```

**Что происходит?**  
- `SEQUENCE(3,1,1,1)` → создаёт вертикальный массив `{1;2;3}`.  
- `EXPAND(...,5,1)` → берёт эту трёхстрочную колонку и растягивает её до пяти столбцов, заполняя дополнительные ячейки пустыми значениями.  

Когда вы откроете полученный `output.xlsx`, вы увидите блок 3 × 5, начинающийся с **A1**, где первый столбец содержит 1, 2, 3, а остальные четыре столбца пусты. Эта техника — основа **как создать массив**‑подобных spill‑диапазонов без ручного ввода каждой ячейки.

---

## Шаг 3: Как использовать COT – Добавление тригонометрической формулы

Если вам также интересно, **как использовать cot** внутри формулы Excel, функция `COT` удобно позволяет получить котангенс угла, заданного в радианах. Давайте вычислим `cot(π/4)`, которое должно дать **1**.

```csharp
        // Write a simple trigonometric formula that calculates cotangent of 45° (π/4)
        // COT(π/4) evaluates to 1
        worksheet.Cells["B1"].Formula = "=COT(PI()/4)";
```

Обратите внимание, что мы использовали `PI()` для получения радианного значения 180°, а затем разделили его на 4, чтобы получить 45°. Excel выполнит всю тяжёлую работу, и ячейка **B1** покажет `1`, как только рабочая книга будет открыта. Это демонстрирует **как использовать cot** для быстрых инженерных или финансовых расчётов без подключения отдельной математической библиотеки.

---

## Шаг 4: Сохранить рабочую книгу как XLSX – Сохранение файла

Весь интерес создания массива и вставки формул теряется, если файл никогда не записать на диск. Вот простой способ **save workbook as xlsx** с использованием Aspose.Cells:

```csharp
        // Save the workbook to verify the formulas (optional)
        string outputPath = @"C:\Temp\output.xlsx";   // adjust to your folder
        workbook.Save(outputPath, SaveFormat.Xlsx);

        // Let the user know we’re done
        System.Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

Почему указываем `SaveFormat.Xlsx`? Это гарантирует современный формат OpenXML, который читается везде (Excel, LibreOffice, Google Sheets). Если нужен более старый файл `.xls`, просто замените перечисление.

---

## Полный рабочий пример (все шаги вместе)

Ниже представлена полная, готовая к запуску программа. Скопируйте её в консольный проект, восстановите пакет Aspose.Cells через NuGet и нажмите **F5**.

```csharp
using Aspose.Cells;

public class ExcelArrayDemo
{
    public static void Main()
    {
        // Step 1: Initialize workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Step 2: Create a dynamic spill range (how to create array)
        worksheet.Cells["A1"].Formula = "=EXPAND(SEQUENCE(3,1,1,1),5,1)";

        // Step 3: Calculate cotangent (how to use cot)
        worksheet.Cells["B1"].Formula = "=COT(PI()/4)";

        // Step 4: Persist the file (save workbook as xlsx)
        string outputPath = @"C:\Temp\output.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);

        System.Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

**Ожидаемый результат** после открытия `output.xlsx`:

| A | B | C | D | E |
|---|---|---|---|---|
| 1 | 1 |   |   |   |
| 2 |   |   |   |   |
| 3 |   |   |   |   |

- Столбец A показывает числа 1‑3, сгенерированные функцией `SEQUENCE`.  
- Столбец B содержит значение **1** из формулы `COT`.  
- Столбцы C‑E пусты, иллюстрируя эффект заполнения функции `EXPAND`.

---

## Общие вопросы и граничные случаи

### Что если мне нужно больше строк или столбцов?

Просто измените аргументы `SEQUENCE` и `EXPAND`.  
- `SEQUENCE(10,2,5,2)` даст матрицу 10 строк × 2 столбца, начинающуюся с 5 и увеличивающуюся на 2.  
- `EXPAND(...,10,5)` дополнит результат до 10 столбцов и 5 строк.

### Работает ли это со старыми версиями Excel?

Функции динамических массивов (`SEQUENCE`, `EXPAND`) требуют Excel 365 или 2019+. Для старых файлов можно вернуться к классическим формулам или записывать значения напрямую через `Cells[row, col].PutValue(value)`.

### Могу ли я записать формулу в стиле R1C1?

Конечно. Замените `A1` на `Cells[0, 0]` и используйте свойство `FormulaR1C1`:

```csharp
worksheet.Cells[0, 0].FormulaR1C1 = "=EXPAND(SEQUENCE(3,1,1,1),5,1)";
```

### Что насчёт разделителей десятичных знаков, зависящих от культуры?

Aspose.Cells учитывает локаль рабочей книги. Если нужна конкретная культура, установите `workbook.Settings.CultureInfo = new System.Globalization.CultureInfo("en-US");` перед записью формул.

---

## Визуальное резюме

![how to create array in Excel using C#](/images/how-to-create-array-excel-csharp.png "how to create array in Excel using C#")

*Скриншот показывает окончательный диапазон spill и результат котангенса.*

---

## Заключение

Вот и всё — **как создать массив** в Excel с помощью C# с нуля, сгенерировать последовательные числа, использовать функцию `COT` и **save workbook as XLSX** в одной аккуратной программе. Ключевые выводы:

1. Используйте объекты `Workbook` и `Worksheet` для начала автоматизации Excel.  
2. Применяйте функции динамических массивов (`SEQUENCE`, `EXPAND`) для гибких spill‑диапазонов.  
3. Подключайте тригонометрические функции, такие как `COT`, для быстрых вычислений без дополнительных библиотек.  
4. Сохраняйте результат с помощью `SaveFormat.Xlsx`, чтобы получить файл, читаемый везде.

Готовы к следующему шагу? Попробуйте заменить `COT(PI()/4)`

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}