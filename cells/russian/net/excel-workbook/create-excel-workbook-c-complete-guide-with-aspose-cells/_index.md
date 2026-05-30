---
category: general
date: 2026-05-30
description: Создайте Excel‑книгу на C# с использованием Aspose.Cells. Научитесь писать
  формулы Excel, использовать функцию Expand, применять функцию Sequence и эффективно
  задавать формулы.
draft: false
keywords:
- create excel workbook c#
- write excel formulas
- use expand function
- aspose cells set formula
- apply sequence function
language: ru
og_description: Создайте Excel‑книгу C# с помощью Aspose.Cells. Это руководство показывает,
  как писать формулы Excel, использовать функцию Expand и применять функцию Sequence
  всего за несколько шагов.
og_title: Создание книги Excel на C# – Полный учебник по Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-05-30'
  description: Create Excel workbook C# using Aspose.Cells. Learn to write Excel formulas,
    use Expand function, apply Sequence function, and set formulas efficiently.
  headline: Create Excel Workbook C# – Complete Guide with Aspose.Cells
  type: TechArticle
- description: Create Excel workbook C# using Aspose.Cells. Learn to write Excel formulas,
    use Expand function, apply Sequence function, and set formulas efficiently.
  name: Create Excel Workbook C# – Complete Guide with Aspose.Cells
  steps:
  - name: Overwriting Existing Files
    text: 'If `output.xlsx` already exists, `Workbook.Save` will overwrite it silently.
      To avoid accidental data loss, you can check first:'
  - name: Applying Formulas to Different Sheets
    text: 'You’re not limited to the default sheet. To target a sheet named “Data”,
      create or fetch it:'
  - name: Using Dynamic Ranges
    text: 'When the size of your `SEQUENCE` output isn’t known ahead of time, combine
      it with `COUNTA` or `ROWS` to make the `EXPAND` dimensions dynamic. Example:'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel Automation
title: Создание рабочей книги Excel на C# – Полное руководство с Aspose.Cells
url: /ru/net/excel-workbook/create-excel-workbook-c-complete-guide-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание Excel‑книги C# – Полное руководство с Aspose.Cells

Когда‑нибудь нужно было **создать Excel‑книгу C#** с нуля и возникал вопрос, как добавить живые формулы, не открывая сам Excel? Вы не одиноки. Будь то построение движка отчётов, генератор счетов или просто автоматизация обработки данных, умение **писать формулы Excel** программно экономит часы ручной работы.

В этом руководстве мы пошагово разберём пример, который покажет, как **создать Excel‑книгу C#** с помощью библиотеки Aspose.Cells, **применить функцию Sequence**, **использовать функцию Expand** и правильно **установить формулу Aspose.Cells**. К концу вы получите готовое консольное приложение, которое создаёт книгу с матрицей 5 × 2 и вычисленным значением котангенса.

> **Примечание:** Код работает с Aspose.Cells 23.10 и новее и нацелен на .NET 6+, но концепции одинаковы и для более ранних версий.

## Требования

- Visual Studio 2022 (или любой другой IDE для C#)  
- Установленный .NET 6 SDK  
- Пакет NuGet **Aspose.Cells** (установим его в первом шаге)  
- Базовое знакомство с синтаксисом C# (глубоких знаний Excel не требуется)

Если что‑то из этого вам незнакомо, просто просмотрите быстрый раздел установки ниже — без проблем.

---

## Шаг 1: Установите Aspose.Cells через NuGet

Прежде чем мы сможем **создать Excel‑книгу C#**, нам нужна библиотека, работающая с файлами Excel. Откройте терминал или консоль диспетчера пакетов и выполните:

```bash
dotnet add package Aspose.Cells
```

Или, если предпочитаете графический интерфейс, щёлкните правой кнопкой по проекту → *Manage NuGet Packages* → найдите **Aspose.Cells** → нажмите **Install**.

> **Совет:** Держите библиотеку в актуальном состоянии; новые версии добавляют улучшения производительности и дополнительные функции, такие как `EXPAND`.

## Шаг 2: Инициализируйте Workbook и получите первый лист

Теперь, когда библиотека подключена, создадим новую книгу. Это основа для всех последующих шагов.

```csharp
using Aspose.Cells;

namespace ExcelAutomationDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 2: Create a new workbook and get the first worksheet
            Workbook workbook = new Workbook();               // <-- create excel workbook c#
            Worksheet ws = workbook.Worksheets[0];            // default sheet is "Sheet1"
```

Здесь `Workbook()` создаёт пустой файл Excel в памяти. Вызов `Worksheets[0]` возвращает первую вкладку, где мы будем **писать формулы Excel**.

## Шаг 3: Используйте функцию EXPAND с SEQUENCE для построения матрицы

Настоящая магия начинается, когда мы **применяем функцию Sequence** и **используем функцию Expand** вместе. Формула, которую мы установим в ячейку `A1`, выглядит так:

```
=EXPAND(SEQUENCE(4),5,2)
```

- `SEQUENCE(4)` генерирует вертикальный массив `{1;2;3;4}`.  
- `EXPAND(...,5,2)` растягивает этот массив в матрицу **5 × 2**, заполняя дополнительные ячейки пустыми значениями.

```csharp
            // Step 3: Set a formula that expands a sequence into a 5×2 matrix
            ws.Cells["A1"].Formula = "=EXPAND(SEQUENCE(4),5,2)";   // aspose cells set formula
```

Зачем так задавать формулу? Позволяя Excel выполнить расчёт, мы избегаем написания циклов в C#. Книга автоматически вычислит значения при открытии.

## Шаг 4: Добавьте простую тригонометрическую формулу

Продемонстрируем, что работает любая стандартная функция Excel. Вычислим котангенс π/4, который равен `1`.

```csharp
            // Step 4: Set a formula that calculates the cotangent of π/4 (result is 1)
            ws.Cells["B1"].Formula = "=COT(PI()/4)";               // write excel formulas
```

Эта строка показывает ещё один типичный сценарий **установки формулы Aspose.Cells**: можно вставлять любое выражение, совместимое с Excel, от арифметики до работы с текстом.

## Шаг 5: Сохраните книгу на диск

Последний шаг — записать файл, чтобы его можно было открыть в Excel или любом другом просмотрщике.

```csharp
            // Step 5: Save the workbook to view the calculated values
            string outputPath = @"YOUR_DIRECTORY\output.xlsx";
            workbook.Save(outputPath);
            System.Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

При запуске программы файл `output.xlsx` появится в указанном месте. Открыв его, вы увидите:

- Ячейки `A1:B5` заполнены матрицей 5 × 2 (первые четыре строки содержат числа 1‑4, пятая строка пустая).  
- Ячейка `B1` показывает `1`, подтверждая вычисление котангенса.

![Создание Excel‑книги C# — скриншот с сгенерированной матрицей и значением котангенса](https://example.com/placeholder-image.png "Пример создания Excel‑книги C#")

*Alt text: создание excel workbook c# – скриншот полученного файла Excel.*

---

## Шаг 6: Обработка распространённых граничных случаев

### Перезапись существующих файлов

Если `output.xlsx` уже существует, `Workbook.Save` без предупреждения перезапишет его. Чтобы избежать случайной потери данных, можно предварительно проверить:

```csharp
if (File.Exists(outputPath))
{
    Console.WriteLine("File exists – overwriting.");
}
workbook.Save(outputPath);
```

### Применение формул к другим листам

Вы не ограничены только листом по умолчанию. Чтобы обратиться к листу с именем «Data», создайте его или получите:

```csharp
Worksheet dataSheet = workbook.Worksheets["Data"] ?? workbook.Worksheets.Add("Data");
dataSheet.Cells["C3"].Formula = "=SUM(A1:A10)";
```

### Использование динамических диапазонов

Когда размер вывода `SEQUENCE` заранее неизвестен, комбинируйте его с `COUNTA` или `ROWS`, чтобы сделать размеры `EXPAND` динамичными. Пример:

```csharp
ws.Cells["D1"].Formula = "=EXPAND(SEQUENCE(COUNTA(A:A)), ROWS(A:A), 1)";
```

---

## Полный рабочий пример

Ниже представлен полностью готовый к копированию и вставке код программы. Ничего не пропущено — просто замените `YOUR_DIRECTORY` на реальный путь к папке на вашем компьютере.

```csharp
using System;
using System.IO;
using Aspose.Cells;

namespace ExcelAutomationDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Create a new workbook and get the first worksheet
            Workbook workbook = new Workbook();               // create excel workbook c#
            Worksheet ws = workbook.Worksheets[0];

            // Write excel formulas using EXPAND and SEQUENCE
            ws.Cells["A1"].Formula = "=EXPAND(SEQUENCE(4),5,2)";   // use expand function, apply sequence function
            ws.Cells["B1"].Formula = "=COT(PI()/4)";               // aspose cells set formula

            // Save the workbook
            string outputPath = @"C:\Temp\output.xlsx";   // adjust path as needed
            if (File.Exists(outputPath))
            {
                Console.WriteLine("File already exists – it will be overwritten.");
            }
            workbook.Save(outputPath);
            Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

Запустите программу (`dotnet run`) и откройте полученный файл. Вы должны увидеть следующее:

| A | B |
|---|---|
| 1 | 1 |
| 2 |   |
| 3 |   |
| 4 |   |
|   |   |

(Матрица расширяется до пяти строк; лишние ячейки пусты.)

---

## Заключение

Мы только что **создали Excel‑книгу C#** с нуля до полностью функционирующего файла, продемонстрировали, как **писать формулы Excel**, и показали практическое применение **функции Expand**, **функции Sequence** и возможностей **установки формулы Aspose.Cells**. Такой подход позволяет делегировать тяжёлые вычисления Excel, оставляя ваш C#‑код чистым и поддерживаемым.

Что дальше? Вы можете:

- Исследовать другие функции динамических массивов, такие как `FILTER` или `SORT`.  
- Генерировать диаграммы, вызывая объекты `Chart` через Aspose.Cells.  
- Автоматизировать стилизацию — шрифты, цвета, границы — чтобы вывод выглядел готовым к продакшн.

Экспериментируйте, и не стесняйтесь оставлять комментарий, если столкнётесь с проблемой. Приятного кодинга!

## Что изучать дальше?

- [Display Formulas in Excel Using Aspose.Cells .NET: A Comprehensive Guide for Efficient Workbook Management](/cells/english/net/formulas-functions/display-excel-formulas-aspose-cells-net/)
- [How to Create Workbook Scoped Named Ranges in Excel Using Aspose.Cells .NET](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)
- [Excel Automation with Aspose.Cells .NET: Create Workbook & Set External Links](/cells/english/net/automation-batch-processing/excel-automation-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}