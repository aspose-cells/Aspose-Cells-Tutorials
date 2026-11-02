---
category: general
date: 2026-05-04
description: Как вычислить котангенс при создании Excel‑книги в C#. Узнайте, как использовать
  функцию EXPAND, сохранять книгу и автоматизировать вычисления.
draft: false
keywords:
- how to calculate cotangent
- create excel workbook
- how to use expand
- how to save workbook
- use expand function
language: ru
og_description: Как вычислить котангенс в Excel с помощью C#. Этот учебник показывает,
  как создать рабочую книгу Excel, использовать EXPAND и сохранить файл.
og_title: Как вычислить котангенс в Excel – Полное руководство по рабочей книге C#
tags:
- C#
- Aspose.Cells
- Excel Automation
title: Как вычислить котангенс в Excel с помощью C# — создать рабочую книгу, использовать
  EXPAND и сохранить
url: /ru/net/formulas-functions/how-to-calculate-cotangent-in-excel-with-c-create-workbook-u/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как вычислить котангенс в Excel с помощью C# – Полное руководство

Когда‑нибудь задумывались **как вычислить котангенс** непосредственно в файле Excel, созданном с помощью C#? Возможно, вы создаёте финансовую модель, научный отчёт или просто автоматизируете скучную работу с таблицами. Хорошая новость? Это можно сделать в несколько строк кода — без ручных формул, без копипаст‑акробатики.

В этом руководстве мы пройдёмся по созданию книги Excel, расширению массива с помощью функции **EXPAND**, вставке формулы **COT** для вычисления котангенса 45°, а затем сохранению файла, чтобы вы могли открыть его в Excel и увидеть результаты. По пути мы также рассмотрим **как использовать expand**, **как сохранять книгу** и несколько полезных советов, которые часто упускают из виду.

> **Быстрый ответ:** Используйте Aspose.Cells (или Microsoft Interop) для создания книги, задайте `ws.Cells["A1"].Formula = "=EXPAND({1,2,3},5,1)"`, задайте `ws.Cells["B1"].Formula = "=COT(PI()/4)"`, затем вызовите `workbook.Save("output.xlsx")`.

---

## Что вам понадобится

- **.NET 6+** (или любой современный .NET runtime).  
- **Aspose.Cells for .NET** (бесплатная пробная версия или лицензия).  
- Базовое понимание синтаксиса C#.  
- Visual Studio, Rider или любой другой редактор по вашему выбору.

Никакие дополнительные надстройки Excel не требуются; всё работает на сервере, а полученный файл открывается в любой современной версии Excel.

---

## Шаг 1: Создать книгу Excel из C#  

Создание книги — это фундамент. Представьте, что вы открываете чистый блокнот перед тем, как начать писать.

```csharp
using Aspose.Cells;

// Step 1: Initialize a new workbook object
Workbook workbook = new Workbook();               // Empty workbook
Worksheet ws = workbook.Worksheets[0];            // Grab the first sheet
```

**Почему это важно:**  
`Workbook` представляет весь пакет `.xlsx`. По умолчанию в нём один лист, к которому мы получаем доступ через `Worksheets[0]`. Если позже понадобится больше листов, их можно добавить с помощью `workbook.Worksheets.Add()`.

> **Pro tip:** Если вы целитесь в .NET Core, убедитесь, что пакет NuGet Aspose.Cells соответствует вашему runtime, чтобы избежать отсутствия нативных зависимостей.

---

## Шаг 2: Использовать функцию EXPAND для заполнения столбца  

Функция **EXPAND** — это способ Excel превратить статический массив в динамический диапазон. Она идеальна, когда нужно сгенерировать столбец значений без ручного ввода каждой ячейки.

```csharp
// Step 2: Write an EXPAND formula in cell A1
ws.Cells["A1"].Formula = "=EXPAND({1,2,3},5,1)"; // Expands to a 5‑row column
```

### Как это работает  

- `{1,2,3}` — исходный массив (три числа).  
- `5` указывает Excel создать **5 строк**.  
- `1` указывает Excel создать **1 столбец**.  

Когда вы откроете сохранённый файл, ячейки A1‑A5 будут содержать `1, 2, 3, 0, 0` (дополнительные строки заполняются нулями).  

**Пограничный случай:** Если аргумент `rows` меньше длины исходного массива, Excel обрезает массив. Поэтому `=EXPAND({1,2,3},2,1)` покажет только `1` и `2`.

---

## Шаг 3: Вставить формулу COT для вычисления котангенса  

Теперь к главному: **как вычислить котангенс** в Excel. Функция `COT` ожидает угол в радианах, поэтому передаём ей `PI()/4` (что равно 45°).

```csharp
// Step 3: Write a COT formula in cell B1
ws.Cells["B1"].Formula = "=COT(PI()/4)"; // Returns 1
```

### Почему использовать COT вместо TAN?  

Котангенс — это обратное значение тангенса (`cot = 1 / tan`). Можно написать `=1/TAN(PI()/4)`, но использование `COT` чище и избавляет от ошибок деления на ноль, когда угол равен 0° или 180°.

**Ожидаемый результат:** Открыв `output.xlsx`, вы увидите `1` в B1, потому что котангенс 45° (π/4 радиан) равен 1.

**Что если нужны градусы?**  
Тригонометрические функции Excel работают в радианах. Преобразуйте градусы с помощью `RADIANS(deg)`. Например: `=COT(RADIANS(60))`.

---

## Шаг 4: Сохранить книгу, чтобы увидеть результаты  

Сохранение — последний кусок головоломки. Вы можете записать файл в любую папку, где у вас есть права записи.

```csharp
// Step 4: Persist the workbook to disk
string outputPath = Path.Combine(
    Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
    "output.xlsx");

// Save the workbook (the default format is .xlsx)
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

### Как сохранять в разных форматах  

- **XLS** – `workbook.Save("output.xls", SaveFormat.Excel97To2003);`  
- **CSV** – `workbook.Save("output.csv", SaveFormat.CSV);`  

Если понадобится передать файл в поток (например, для веб‑API), используйте `workbook.Save(stream, SaveFormat.Xlsx)`.

---

## Полный рабочий пример  

Собрав всё вместе, получаем самостоятельную программу, которую можно скопировать в консольное приложение.

```csharp
using System;
using System.IO;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet ws = workbook.Worksheets[0];

        // 2️⃣ Expand an array {1,2,3} into a 5‑row column starting at A1
        ws.Cells["A1"].Formula = "=EXPAND({1,2,3},5,1)";

        // 3️⃣ Calculate cotangent of 45° (π/4) in B1
        ws.Cells["B1"].Formula = "=COT(PI()/4)";

        // 4️⃣ Define where to save the file (Desktop for easy access)
        string outputPath = Path.Combine(
            Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
            "output.xlsx");

        // 5️⃣ Save the workbook
        workbook.Save(outputPath);
        Console.WriteLine($"✅ Workbook saved at: {outputPath}");
    }
}
```

**Проверка результата:**  
- Откройте `output.xlsx`.  
- Столбец A должен содержать `1, 2, 3, 0, 0`.  
- Ячейка B1 должна отображать `1`.  

Если вы видите эти значения, вы успешно усвоили **как вычислять котангенс** программно и как **создавать книгу Excel**, **использовать функцию expand**, и **сохранять книгу** — всё в одном процессе.

---

## Часто задаваемые вопросы и подводные камни  

### Работает ли `COT` в старых версиях Excel?  
Да, `COT` существует с Excel 2007. Если вы нацелены на Excel 2003 (`.xls`), замените её на `1/TAN(...)`, потому что `COT` в той версии недоступен.

### Что если формула не пересчитывается автоматически?  
Aspose.Cells вычисляет формулы лениво. Вызовите `workbook.CalculateFormula()` перед сохранением, если нужны вычисленные значения, записанные в файл.

```csharp
workbook.CalculateFormula();
workbook.Save(outputPath);
```

### Можно ли записать результат сразу без формулы?  
Конечно, можно вычислить значение в C# (`Math.Cos(Math.PI / 4) / Math.Sin(Math.PI / 4)`) и присвоить его `ws.Cells["B1"].Value = result;`. В руководстве мы сосредоточились на формулах Excel, потому что они остаются динамичными — при изменении угла значение обновится автоматически.

---

## Профессиональные советы для реальных проектов  

- **Пакетные операции:** Если заполняете тысячи строк, отключите вычисления (`workbook.Settings.CalculateFormulaOnOpen = false`) во время записи, а затем включите их обратно.  
- **Именованные диапазоны:** Используйте `ws.Cells.CreateRange("MyArray", "A1:A5")` и ссылайтесь на имя в формулах для более понятных таблиц.  
- **Обработка ошибок:** Оберните `workbook.Save` в `try/catch`, чтобы отлавливать проблемы с правами доступа (`UnauthorizedAccessException`).

---

## Заключение  

Мы рассмотрели **как вычислять котангенс** в листе Excel, сгенерированном из C#, продемонстрировали **как использовать expand** для заполнения столбца и показали **как сохранять книгу** для мгновенного просмотра. Полный, готовый к запуску пример выше даст вам надёжную основу для автоматизации любой таблицы, где смешаны статические данные и тригонометрические вычисления.

Что дальше? Попробуйте заменить угол в формуле `COT` на ссылку на ячейку (`=COT(PI()*A1/180)`), чтобы пользователи могли вводить градусы. Или изучите другие математические функции, такие как `SIN`, `COS` и `ATAN2` — они работают точно так же в сгенерированной книге.

Счастливого кодинга, и пусть ваши таблицы остаются без ошибок! 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}