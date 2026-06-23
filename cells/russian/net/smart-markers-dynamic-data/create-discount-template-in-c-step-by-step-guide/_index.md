---
category: general
date: 2026-02-14
description: Быстро создайте шаблон скидки и узнайте, как применить скидку в таблице,
  внедрить данные в шаблон и определить переменный префикс для умных маркеров.
draft: false
keywords:
- create discount template
- apply discount in spreadsheet
- inject data into template
- define variable prefix
language: ru
og_description: Создайте шаблон скидки на C#. Научитесь применять скидку в таблице,
  внедрять данные в шаблон и задавать переменный префикс для смарт‑маркировок.
og_title: Создать шаблон скидки – Полный пошаговый разбор C#
tags:
- C#
- SmartMarker
- Spreadsheet Automation
title: Создание шаблона скидки в C# – пошаговое руководство
url: /ru/net/smart-markers-dynamic-data/create-discount-template-in-c-step-by-step-guide/
---

markdown formatting, code block placeholders, etc.

Check for any URLs: none.

Check for any markdown links: none.

All good.

Now produce final output with translated content.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создать шаблон скидки – Полный разбор на C# Walkthrough

Когда‑нибудь вам нужно было **create discount template** для отчёта о продажах, но вы не знали, как автоматически загрузить цифры в таблицу? Вы не одиноки. В этом руководстве мы покажем, как именно **create discount template**, затем **apply discount in spreadsheet** ячейки, **inject data into template**, и даже **define variable prefix** для ваших smart markers — всё с чистым кодом на C#.

Мы начнём с описания проблемы, а затем сразу перейдём к рабочему решению, которое можно скопировать‑вставить. К концу у вас будет переиспользуемый шаблон, который работает как при генерации счетов, прайс‑листов, так и любой таблицы, требующей динамических скидок.

---

## Что вы узнаете

- Как спроектировать шаблон таблицы, учитывающий скидки.
- Как настроить пользовательский `VariablePrefix` / `VariableSuffix`, чтобы маркеры было легко обнаружить.
- Как передать анонимный объект (`discountData`) в `SmartMarkerProcessor`.
- Как полученная формула (`=IF(#Discount#>0, A1*(1-#Discount#), A1)`) автоматически вычисляет окончательную цену.
- Советы по обработке граничных случаев, таких как строки без скидки или несколько уровней скидок.

**Prerequisites** – recent .NET runtime (≥ .NET 6), ссылка на библиотеку `Aspose.Cells` (или аналогичную), предоставляющую `SmartMarkerProcessor`, и базовое понимание синтаксиса C#. Ничего экзотического.

## Шаг 1: Создать шаблон скидки в вашей таблице

Сначала откройте новую книгу (или используйте существующую) и разместите заполнитель там, где будет применяться скидка. Представьте шаблон как обычный файл Excel с «smart markers», которые заменит процессор.

```csharp
using Aspose.Cells;          // SmartMarkerProcessor lives here
using System;

// Step 1: Load or create a workbook
Workbook wb = new Workbook();               // creates an empty .xlsx in memory
Worksheet ws = wb.Worksheets[0];
ws.Name = "Pricing";

// Put a header
ws.Cells["A1"].PutValue("Original Price");
ws.Cells["B1"].PutValue("Discounted Price");

// Sample data row – the formula will be injected later
ws.Cells["A2"].PutValue(100);               // original price = 100
ws.Cells["B2"].Formula = "=IF(#Discount#>0, A2*(1-#Discount#), A2)";
```

**Why this matters:** Встраивая `#Discount#` в формулу, мы указываем процессору, где должно находиться значение скидки. `SmartMarkerProcessor` заменит `#Discount#` на число, которое вы укажете позже, оставив остальную часть формулы нетронутой.

## Шаг 2: Определить префикс переменной для Smart Markers

По умолчанию многие библиотеки ищут `${Variable}` или `{{Variable}}`. В нашем случае мы хотим чистый, удобочитаемый маркер, поэтому **define variable prefix** и суффикс задаются явно.

```csharp
// Step 2: Configure how markers are identified
var smartMarkerOptions = new SmartMarkerOptions
{
    VariablePrefix = "#",   // start marker
    VariableSuffix = "#"    // end marker
};
```

**Pro tip:** Использование `#` делает маркеры короткими и легко заметными в строке формул Excel. Если понадобится избежать конфликтов с существующими функциями Excel, выберите другую пару (например, `[[` и `]]`).

## Шаг 3: Вставить данные в шаблон с помощью SmartMarkerProcessor

Теперь мы передаём фактическое значение скидки. Процессор просканирует лист, найдёт каждый `#Discount#` и заменит его значением из переданного анонимного объекта.

```csharp
// Step 3: Prepare the data that will be injected
var discountData = new { Discount = 0.10, Total = 100 };

// Run the processor – it mutates the workbook in‑place
ws.SmartMarkerProcessor.StartSmartMarkerProcessing(discountData, smartMarkerOptions);
```

After this call, the formula in `B2` becomes:

```
=IF(0.1>0, A2*(1-0.1), A2)
```

When the workbook calculates, `B2` shows **90**, i.e., a 10 % discount applied to the original price of 100.

**Why it works:** `StartSmartMarkerProcessing` проходит по каждой ячейке, ищет токен `#Discount#` и подставляет числовое значение. Поскольку токен находится внутри оператора `IF`, таблица по‑прежнему обрабатывает случаи, когда скидка может быть нулевой.

## Шаг 4: Применить скидку в таблице – Проверить результат

Запустим вычисление и выведем окончательную цену в консоль. Этот шаг доказывает, что процесс **apply discount in spreadsheet** завершился успешно.

```csharp
// Step 4: Force calculation and read the result
wb.CalculateFormula();                     // ensures all formulas are up‑to‑date
double discountedPrice = ws.Cells["B2"].DoubleValue;

Console.WriteLine($"Original: {ws.Cells["A2"].DoubleValue}");
Console.WriteLine($"Discounted (10%): {discountedPrice}");
```

**Expected output**

```
Original: 100
Discounted (10%): 90
```

Если изменить `discountData.Discount` на `0.25` и повторно запустить процессор, вывод автоматически отразит 25 % скидку — без дополнительного кода.

## Шаг 5: Обработка граничных случаев и нескольких скидок

### Строки без скидки

Иногда товар не участвует в распродаже. Чтобы формула оставалась надёжной, ранее размещённый `IF` уже покрывает этот сценарий: когда `#Discount#` равен `0`, исходная цена проходит без изменений.

```csharp
var noDiscountData = new { Discount = 0.0 };
ws.SmartMarkerProcessor.StartSmartMarkerProcessing(noDiscountData, smartMarkerOptions);
wb.CalculateFormula();
Console.WriteLine($"No discount applied: {ws.Cells["B2"].DoubleValue}");
```

### Несколько столбцов скидок

Если нужны отдельные скидки для каждой строки, дайте каждой строке свой маркер, например `#Discount1#`, `#Discount2#`, и передайте коллекцию:

```csharp
var multiDiscountData = new[]
{
    new { Discount = 0.05 },   // row 2
    new { Discount = 0.15 }    // row 3
};

ws.SmartMarkerProcessor.StartSmartMarkerProcessing(multiDiscountData, smartMarkerOptions);
```

Процессор сопоставляет маркеры последовательно, поэтому каждая строка получает правильное значение.

## Полный рабочий пример

Ниже приведена полная, готовая к копированию программа, включающая все шаги выше. Сохраните её как `Program.cs`, добавьте ссылку на `Aspose.Cells` и запустите.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // 1️⃣ Create workbook & template
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];
        ws.Name = "Pricing";
        ws.Cells["A1"].PutValue("Original Price");
        ws.Cells["B1"].PutValue("Discounted Price");
        ws.Cells["A2"].PutValue(100);
        ws.Cells["B2"].Formula = "=IF(#Discount#>0, A2*(1-#Discount#), A2)";

        // 2️⃣ Define marker delimiters
        var smartMarkerOptions = new SmartMarkerOptions
        {
            VariablePrefix = "#",
            VariableSuffix = "#"
        };

        // 3️⃣ Inject a 10 % discount
        var discountData = new { Discount = 0.10 };
        ws.SmartMarkerProcessor.StartSmartMarkerProcessing(discountData, smartMarkerOptions);

        // 4️⃣ Calculate and display result
        wb.CalculateFormula();
        double original = ws.Cells["A2"].DoubleValue;
        double discounted = ws.Cells["B2"].DoubleValue;

        Console.WriteLine($"Original: {original}");
        Console.WriteLine($"Discounted (10%): {discounted}");

        // Optional: Save the workbook to verify manually
        wb.Save("DiscountedPricing.xlsx");
    }
}
```

Запуск этой программы выводит ожидаемые числа и создаёт файл `DiscountedPricing.xlsx`, который можно открыть в Excel, чтобы увидеть уже вычисленную формулу.

## Заключение

Теперь вы знаете, как **create discount template**, **apply discount in spreadsheet**, **inject data into template** и **define variable prefix** для smart markers — всё с помощью нескольких лаконичных строк C#. Этот шаблон масштабируем: просто измените анонимный объект или передайте коллекцию для массовых обновлений, и тот же шаблон справится с любой ситуацией скидки.

Готовы к следующему уровню? Попробуйте:

- Добавить расчёт налога вместе со скидками.
- Получать процент скидки из базы данных вместо жёсткого кодирования.
- Использовать условное форматирование для выделения строк с большими скидками.

Эти расширения сохраняют основную идею, одновременно расширяя полезность вашего шаблона скидки.

Есть вопросы или интересный пример использования? Оставьте комментарий ниже, и удачной разработки!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}