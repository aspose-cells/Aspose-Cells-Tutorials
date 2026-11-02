---
category: general
date: 2026-10-04
description: Узнайте, как создать книгу Excel на C#, использовать функцию EXPAND,
  принудительно выполнять вычисление формул и сохранять книгу в формате XLSX, заполняя
  столбец числами.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- how to use expand
- force formula calculation
- save workbook as xlsx
- populate column with numbers
language: ru
lastmod: 2026-10-04
og_description: Создайте рабочую книгу Excel на C# с использованием Aspose.Cells.
  В этом руководстве показано, как использовать EXPAND, принудительно вычислять формулы
  и сохранять книгу в формате XLSX, заполняя столбец числами.
og_image_alt: Screenshot of a C# program that creates an Excel workbook and applies
  the EXPAND function
og_title: Создание Excel‑книги в C# — полное руководство с EXPAND и сохранением в
  XLSX
schemas:
- author: Aspose
  dateModified: '2026-10-04'
  description: Learn how to create Excel workbook in C# and use EXPAND, force formula
    calculation, and save workbook as XLSX while populating a column with numbers.
  headline: How to create Excel workbook in C# with the EXPAND function
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
- Automation
title: Как создать рабочую книгу Excel в C# с функцией EXPAND
url: /ru/net/excel-formulas-and-calculation-options/how-to-create-excel-workbook-in-c-with-the-expand-function/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как создать Excel‑книгу в C# с функцией EXPAND

Если вам нужно **создать Excel‑книгу** программно, это руководство покажет готовое решение, готовое к запуску. Вы увидите, как **заполнить столбец числами**, применить функцию **EXPAND** для горизонтального «разливания» данных, **принудительно вычислить формулы** и, наконец, **сохранить книгу в формате XLSX**.  

В этом учебнике описаны все необходимые шаги — от инициализации книги до проверки результата. Внешняя документация не требуется — просто скопируйте код, запустите его, и у вас будет полностью рабочий файл Excel.

## Требования

- .NET 6.0 или новее (код также работает с .NET Framework 4.6+)
- NuGet‑пакет Aspose.Cells for .NET (`Install-Package Aspose.Cells`)
- Базовое знакомство с синтаксисом C#
- IDE, например Visual Studio или VS Code

## Шаг 1: Создать Excel‑книгу и получить доступ к первому листу

Первое действие — **создать Excel‑книгу** и получить ссылку на её лист по умолчанию. Aspose.Cells автоматически добавляет лист с индексом 0, поэтому сразу можно с ним работать.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();          // create Excel workbook
        Worksheet sheet = workbook.Worksheets[0];   // first (default) worksheet
```

*Почему это важно:* Создание экземпляра `Workbook` выделяет внутреннюю структуру файла, а обращение к `Worksheets[0]` даёт конкретный объект `Worksheet` для работы со строками, столбцами и ячейками.

## Шаг 2: Заполнить столбец числами

Далее заполняем вертикальный список в столбце A. Это демонстрирует **заполнение столбца числами** и предоставляет исходный диапазон для функции EXPAND.

```csharp
        // Step 2: Fill a vertical list of values in column A
        sheet.Cells["A1"].PutValue(1);
        sheet.Cells["A2"].PutValue(2);
        sheet.Cells["A3"].PutValue(3);
```

*Совет:* Используйте `PutValue` для чистых чисел, строк, дат или любых примитивов .NET. Метод автоматически определяет тип ячейки.

## Шаг 3: Как использовать EXPAND – «разлить» список по горизонтали

Часть **как использовать expand** является ядром этого руководства. Функция `EXPAND` расширяет исходный диапазон до новой формы. Здесь мы расширяем вертикальный диапазон `A1:A3` в одну строку, охватывающую три столбца, начиная с `B1`.

```csharp
        // Step 3: Apply the EXPAND function to spill the list horizontally starting at B1
        // The formula expands the range A1:A3 into 1 row and 3 columns (B1:D1)
        sheet.Cells["B1"].Formula = "=EXPAND(A1:A3, 1, 3)";
```

*Пояснение:*  
- Первый аргумент (`A1:A3`) — исходный диапазон.  
- Второй аргумент (`1`) принуждает результат иметь **1** строку.  
- Третий аргумент (`3`) принуждает результат иметь **3** столбца.  

При пересчёте книги ячейки `B1`, `C1` и `D1` будут содержать соответственно `1`, `2` и `3`.

## Шаг 4: Принудительный расчёт формул

Aspose.Cells не вычисляет формулы автоматически после их установки, поэтому необходимо **принудительно вычислить формулы** перед сохранением. Это гарантирует, что результат функции EXPAND будет записан в файл.

```csharp
        // Step 4: Force calculation of all formulas in the workbook
        workbook.CalculateFormula();   // triggers calculation engine
```

*Зачем это нужно:* Без вызова `CalculateFormula` сохранённый файл будет содержать только строку формулы, а Excel пересчитает её только при открытии. Для автоматизированных конвейеров обычно требуется, чтобы значения были записаны сразу.

## Шаг 5: Сохранить книгу в формате XLSX

Теперь, когда книга полностью готова, **сохраните её в формате XLSX** в выбранное место. Расширение файла определяет формат вывода; `.xlsx` создаёт книгу Office Open XML.

```csharp
        // Step 5: Save the workbook to a file
        string outputPath = @"C:\Temp\ExpandFunction.xlsx";
        workbook.Save(outputPath);   // save workbook as XLSX
        System.Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

*Подсказка:* Если нужен другой формат (CSV, PDF и т.д.), просто измените расширение файла или используйте `workbook.Save(outputPath, SaveFormat.Xls)` для более старых версий Excel.

## Полный, готовый к запуску пример

Собрав все части вместе, получаем автономную программу, которая **создаёт Excel‑книгу**, заполняет столбец, использует **EXPAND**, принудительно вычисляет формулы и **сохраняет книгу в формате XLSX**.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1. Create Excel workbook
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // 2. Populate column with numbers
        sheet.Cells["A1"].PutValue(1);
        sheet.Cells["A2"].PutValue(2);
        sheet.Cells["A3"].PutValue(3);

        // 3. How to use EXPAND – spill horizontally
        sheet.Cells["B1"].Formula = "=EXPAND(A1:A3, 1, 3)";

        // 4. Force formula calculation
        workbook.CalculateFormula();

        // 5. Save workbook as XLSX
        string path = @"C:\Temp\ExpandFunction.xlsx";
        workbook.Save(path);
        System.Console.WriteLine($"Workbook saved to {path}");
    }
}
```

### Ожидаемый результат

После запуска программы откройте `ExpandFunction.xlsx` в Excel. Вы увидите:

| A | B | C | D |
|---|---|---|---|
| 1 | 1 | 2 | 3 |
| 2 |   |   |   |
| 3 |   |   |   |

Значения `1`, `2`, `3` в ячейках `B1:D1` подтверждают, что функция **EXPAND** отработала, а шаг **принудительного расчёта формул** успешно материализовал результаты.

## Общие варианты и граничные случаи

| Сценарий | Корректировка |
|----------|----------------|
| **Динамический исходный диапазон** | Используйте `=EXPAND(A1:INDEX(A:A, COUNTA(A:A)), 1, 0)`, чтобы расширять столько строк, сколько заполнено. |
| **Другие размеры вывода** | Измените второй и третий аргументы функции `EXPAND` для управления количеством строк и столбцов. |
| **Несколько листов** | Пройдитесь в цикле по `workbook.Worksheets` и примените ту же логику к каждому листу. |
| **Большие наборы данных** | Вызовите `workbook.CalculateFormula()` один раз после установки всех формул, чтобы избежать повторных пересчётов. |
| **Сохранение в поток памяти** | Замените `workbook.Save(path)` на `workbook.Save(stream, SaveFormat.Xlsx)`, когда файл нужен в ответе веб‑API. |

## Список проверок для устранения неполадок

- **Формула не расширяется:** Убедитесь, что `CalculateFormula()` вызывается *после* установки формулы.  
- **Файл не найден при сохранении:** Проверьте, что целевая директория существует и процесс имеет права записи.  
- **Неправильный тип данных:** Используйте `PutValue` для чисел; для дат — `PutValue(DateTime.Now)` или `PutDateTime`.  
- **Несоответствие версий:** Функция EXPAND требует движка расчётов, совместимого с Excel 365; Aspose.Cells 23.9+ её поддерживает.

## Заключение

Теперь вы знаете, как **создать Excel‑книгу** в C#, **заполнить столбец числами**, применить функцию **EXPAND**, **принудительно вычислить формулы** и **сохранить книгу в формате XLSX**. Этот сквозной пример можно адаптировать для отчётности, трансформации данных или любой автоматизации, требующей динамического вывода в Excel.

### Следующие шаги

- Изучите другие функции динамических массивов, такие как `FILTER`, `SORT` и `UNIQUE`.  
- Интегрируйте генерацию книги в ASP.NET Core API для выдачи Excel‑файлов по запросу.  
- Замените жёстко заданные числа данными из базы данных или CSV‑файла для реальных отчётов.

Экспериментируйте с различными диапазонами, именами листов и форматами вывода. Приятного кодинга!

## Что изучать дальше?

Следующие учебники охватывают тесно связанные темы, расширяющие техники, продемонстрированные в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы в своих проектах.

- [How to Calculate Cotangent in Excel with C# – Create Workbook, Use EXPAND,](/cells/english/net/formulas-functions/how-to-calculate-cotangent-in-excel-with-c-create-workbook-u/)
- [How to Use WRAPCOLS in C# – Create Excel Workbook with Wrap Functions](/cells/english/net/formulas-functions/how-to-use-wrapcols-in-c-create-excel-workbook-with-wrap-fun/)
- [How to Create and Save an Excel Workbook as ODS Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}