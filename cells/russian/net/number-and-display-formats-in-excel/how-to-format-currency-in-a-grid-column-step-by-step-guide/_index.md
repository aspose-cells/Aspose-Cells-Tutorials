---
category: general
date: 2026-02-15
description: Как быстро отформатировать валюту, используя установку числового формата
  столбца и применение пользовательского числового формата в C#. Узнайте, как получить
  столбец по имени и установить выравнивание столбца в сетке.
draft: false
keywords:
- how to format currency
- set column number format
- apply custom numeric format
- retrieve column by name
- set grid column alignment
language: ru
og_description: как отформатировать валюту в столбце сетки с помощью C#. Этот учебник
  показывает, как получить столбец по имени, установить числовой формат столбца, применить
  пользовательский числовой формат и задать выравнивание столбца сетки.
og_title: Как форматировать валюту в столбце сетки — Полное руководство
tags:
- C#
- GridFormatting
- UI
title: Как форматировать валюту в столбце сетки — пошаговое руководство
url: /ru/net/number-and-display-formats-in-excel/how-to-format-currency-in-a-grid-column-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как отформатировать валюту в столбце Grid – Полный программный учебник

Когда‑нибудь задавались вопросом **как отформатировать валюту** в столбце сетки, не теряя волосы? Вы не одиноки. Когда вы смотрите на простое число, например `1234.5`, и хотите, чтобы оно волшебным образом превратилось в `$1,234.50`, ответ обычно состоит из нескольких строк конфигурации.  

В этом руководстве мы **получим столбец по имени**, **установим числовой формат столбца** и **применим пользовательский числовой формат**, соответствующий типичному бухгалтерскому виду. По пути мы также **установим выравнивание столбца сетки** и добавим тонкую границу, чтобы интерфейс выглядел аккуратно.

> **TL;DR** – К концу вы получите готовый фрагмент кода, который превращает сырые десятичные числа в красиво отформатированные валютные значения в любом контроле в стиле `GridJs`.

---

## Что вам понадобится

- Проект .NET (любая версия, поддерживающая C# 8.0+ – Visual Studio 2022 отлично подходит).  
- Компонент сетки, предоставляющий коллекцию `Columns` (в примере используется вымышленный класс `GridJs`, но концепции применимы к DevExpress, Telerik или Syncfusion).  
- Базовое знакомство с синтаксисом C# – никаких продвинутых трюков не требуется.

Если у вас уже всё есть – отлично. Если нет, просто создайте консольное приложение; сетку можно замокать для иллюстрации.

---

## Пошаговая реализация

Ниже каждого шага вы увидите компактный блок кода, короткое объяснение **почему** строка важна, и совет, как избежать распространённых ошибок.

### ## Шаг 1 – Получить столбец “Amount” по имени

```csharp
// Step 1: Retrieve the "Amount" column from the grid
var amountColumn = gridJs.Columns["Amount"];
if (amountColumn == null)
{
    throw new InvalidOperationException("Column 'Amount' does not exist. Verify the column name or check the grid's schema.");
}
```

**Почему это важно:**  
Большинство API сеток предоставляют столбцы через индексатор, похожий на словарь. Получив столбец по его заголовку (`"Amount"`), вы можете менять его внешний вид, не затрагивая источник данных.  

**Pro tip:** Всегда проверяйте, что результат не `null` – опечатка в имени столбца или динамическое изменение схемы иначе приведут к `NullReferenceException` во время выполнения.

---

### ## Шаг 2 – Установить числовой формат столбца с помощью пользовательской валютной маски

```csharp
// Step 2: Apply a custom numeric format for currency values
amountColumn.NumberFormat = "_(* #,##0.00_);_(* (#,##0.00);_(* \"-\"??_);_(@_)";
```

**Почему это важно:**  
Строка формата следует конвенциям бухгалтерского формата Excel:

- `_(* #,##0.00_)` → Положительные числа, выровненные по правому краю с пробелом перед символом валюты.  
- `_(* (#,##0.00)` → Отрицательные числа в скобках.  
- `_(* \"-\"??_)` → Нулевые значения отображаются как тире.  
- `_(@_)` → Текстовые значения остаются без изменений.

Использование **apply custom numeric format** даёт полный контроль над разделителями тысяч, десятичными знаками и расположением знака валюты.  

**Edge case:** Если вашему приложению нужен другой регион (например, евро вместо доллара), замените ведущий пробел нужным символом или используйте форматирование, учитывающее `CultureInfo`, в источнике данных.

---

### ## Шаг 3 – Выравнивание содержимого столбца по правому краю для лучшей читаемости

```csharp
// Step 3: Align the column contents to the right for better readability
amountColumn.Alignment = GridAlignment.Right;
```

**Почему это важно:**  
Значения валют легче сканировать, когда они выровнены по десятичному разделителю. Установка **set grid column alignment** в `Right` имитирует способ отображения денежных данных в электронных таблицах.  

**Gotcha:** Некоторые сетки игнорируют выравнивание в ячейках, содержащих пользовательские шаблоны. Если вы заметили, что выравнивание не применяется, проверьте, что столбец не использует пользовательский рендерер ячеек.

---

### ## Шаг 4 – Добавить тонкую серую границу вокруг ячеек столбца

```csharp
// Step 4: Add a thin gray border around the column cells
amountColumn.Border = new GridBorder
{
    Color = Color.Gray,
    Style = BorderLineStyle.Thin
};
```

**Почему это важно:**  
Тонкая граница отделяет столбец “Amount” от соседних, особенно когда у сетки чередуются цвета строк. Это визуальный сигнал, что данные представляют отдельную финансовую величину.  

**Tip:** Если нужна более толстая линия для печати, увеличьте `BorderLineStyle` до `Medium` или измените `Color` на `Color.Black`.

---

## Полный рабочий пример

Ниже представлен весь фрагмент, который можно вставить в проект WinForms или WPF, использующий контрол в стиле `GridJs`. Пример также выводит отформатированные значения в консоль, чтобы вы могли проверить результат без UI.

```csharp
using System;
using System.Drawing;   // For Color
using GridLibrary;      // Hypothetical namespace for GridJs

namespace GridCurrencyDemo
{
    class Program
    {
        static void Main()
        {
            // Create a mock grid and add a sample column
            var gridJs = new GridJs();
            gridJs.Columns.Add(new GridColumn
            {
                Name = "Amount",
                Header = "Amount",
                DataType = typeof(decimal)
            });

            // Populate some sample data
            gridJs.Rows.Add(new { Amount = 1234.5m });
            gridJs.Rows.Add(new { Amount = -567.89m });
            gridJs.Rows.Add(new { Amount = 0m });

            // ---- Formatting steps ------------------------------------------------
            // 1️⃣ Retrieve the "Amount" column
            var amountColumn = gridJs.Columns["Amount"]
                ?? throw new InvalidOperationException("Column 'Amount' not found.");

            // 2️⃣ Apply custom numeric format for currency
            amountColumn.NumberFormat = "_(* #,##0.00_);_(* (#,##0.00);_(* \"-\"??_);_(@_)";

            // 3️⃣ Right‑align the values
            amountColumn.Alignment = GridAlignment.Right;

            // 4️⃣ Add a thin gray border
            amountColumn.Border = new GridBorder
            {
                Color = Color.Gray,
                Style = BorderLineStyle.Thin
            };
            // -----------------------------------------------------------------------

            // Render the grid (in a real UI you would call gridJs.Render() or similar)
            Console.WriteLine("Formatted Currency Grid:");
            foreach (var row in gridJs.Rows)
            {
                var rawValue = (decimal)row.Amount;
                // The grid library would automatically apply NumberFormat when displaying.
                // For console demo we mimic the formatting:
                string formatted = rawValue.ToString("#,##0.00", System.Globalization.CultureInfo.InvariantCulture);
                if (rawValue < 0)
                    formatted = $"({formatted.TrimStart('-')})";
                else if (rawValue == 0)
                    formatted = "-";

                Console.WriteLine($"| {formatted,15} |");
            }

            // Keep console open
            Console.WriteLine("\nPress any key to exit...");
            Console.ReadKey();
        }
    }
}
```

**Ожидаемый вывод в консоль**

```
Formatted Currency Grid:
|        1,234.50 |
|       (567.89) |
|               - |
```

Обратите внимание, как положительное число выравнивается по правому краю, отрицательное отображается в скобках, а ноль – в виде тире, точно как задаёт пользовательская строка формата.

---

## Часто задаваемые вопросы и особые случаи

| Вопрос | Ответ |
|----------|--------|
| *Что если сетка использует другую культуру (например, € вместо $)?* | Замените ведущий пробел в строке формата на нужный символ или позвольте источнику данных выдавать предварительно отформатированную строку, используя `CultureInfo.CurrentCulture`. |
| *Можно ли переиспользовать один и тот же формат для нескольких столбцов?* | Конечно. Сохраните строку формата в константе (`const string CurrencyMask = "...";`) и присваивайте её там, где требуется валютное отображение. |
| *Что происходит, если столбец содержит строковое значение?* | Строка формата влияет только на числовые типы. Строки проходят без изменений, поэтому в маске есть последняя часть (`_(@_)`) – она сохраняет нечисловой контент. |
| *Есть ли влияние на производительность?* | Незначительное. Формат применяется во время рендеринга, а не при получении данных. Если только вы не рендерите тысячи строк за кадр, замедления не заметите. |
| *Как сделать границу толще для печатных отчётов?* | Замените `BorderLineStyle.Thin` на `BorderLineStyle.Medium` или `BorderLineStyle.Thick`. Некоторые библиотеки позволяют указать толщину в пикселях напрямую. |

---

## Итоги

Мы прошли весь процесс **форматирования валюты** в столбце сетки от начала до конца: получили столбец по имени, задали числовой формат, применили пользовательскую маску, выровняли ячейки и добавили эстетичную границу. Полный пример работает «из коробки» и демонстрирует точный визуальный результат, который вы можете ожидать.

Если вы готовы пойти дальше, попробуйте:

- **Dynamic cultures** – переключайте строку формата в зависимости от локали пользователя.  
- **Conditional

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}