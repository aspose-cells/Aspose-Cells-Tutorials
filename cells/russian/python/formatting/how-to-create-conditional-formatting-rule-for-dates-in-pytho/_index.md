---
category: general
date: 2026-08-24
description: Create conditional formatting rule in Python using Aspose.Cells to highlight
  dates, with auto‑fit column and background color formatting.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create conditional formatting rule
- auto fit column
- conditional formatting by date
- background color conditional format
- date based conditional format
language: ru
lastmod: 2026-08-24
og_description: Create conditional formatting rule in Python with Aspose.Cells. Learn
  how to highlight dates, set background colors, and auto‑fit columns in just a few
  lines of code.
og_image_alt: Screenshot of an Excel sheet where yesterday's date cells are highlighted
  in pink
og_title: Create a conditional formatting rule for dates in Python – step‑by‑step
  guide
schemas:
- author: Aspose
  dateModified: '2026-08-24'
  description: Create conditional formatting rule in Python using Aspose.Cells to
    highlight dates, with auto‑fit column and background color formatting.
  headline: How to create conditional formatting rule for dates in Python
  type: TechArticle
tags:
- Aspose.Cells
- Python
- Excel automation
- Conditional formatting
title: How to create conditional formatting rule for dates in Python
url: /ru/python/formatting/how-to-create-conditional-formatting-rule-for-dates-in-pytho/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как создать правило условного форматирования для дат в Python

Если вам нужно **create conditional formatting rule**, реагирующее на даты, это руководство покажет, как сделать это с помощью Aspose.Cells for Python. Независимо от того, создаёте ли вы панель отчётов или автоматизированную таблицу, вы увидите, как выделять даты вчерашнего дня, применять пользовательский цвет фона и **auto fit column** ширины столбцов, чтобы результат выглядел аккуратно.

В этом руководстве мы рассмотрим **conditional formatting by date**, продемонстрируем **background color conditional format**, и завершим сохранением рабочей книги в файл XLSX. К концу у вас будет переиспользуемый помощник, который можно адаптировать к любому **date based conditional format**, который вам нужен.

## Чего вы научитесь

* Настроить рабочую книгу и лист с помощью Aspose.Cells.
* Написать вспомогательную функцию, которая добавляет **date based conditional format** к любому диапазону ячеек.
* Заполнить ячейки примерными датами, чтобы правило могло быть оценено.
* Применить **auto fit column**, чтобы содержимое было читаемым.
* Сохранить рабочую книгу и проверить выделенные ячейки.

Единственное требование — рабочая среда Python с установленным пакетом `aspose-cells`.

## Предварительные требования

| Требование | Подробности |
|-------------|-------------|
| Python | 3.8+ |
| Aspose.Cells for Python via Java | `pip install aspose-cells` |
| Базовые знания концепций Excel | worksheets, cells, formatting |
| Необязательно: IDE (VS Code, PyCharm и др.) | любой редактор, способный запускать скрипты Python |

## Шаг 1: Создать рабочую книгу и получить первый лист

Первый шаг — подготовить объекты, готовые к **create conditional formatting rule**: `Workbook` и его стандартный `Worksheet`. Эти объекты являются точкой входа для всех последующих операций.

```python
# Step 1 – initialize workbook and worksheet
from aspose.cells import Workbook, FormatConditionType, BackgroundType, TimePeriodType, SaveFormat
from aspose.pydrawing import Color
from datetime import datetime

# Create a new, empty workbook
workbook = Workbook()

# Grab the first worksheet (index 0)
worksheet = workbook.worksheets[0]
```

*Почему это важно:* `Workbook` содержит весь файл Excel, а `Worksheet` — место, где вы применяете ячейки, стили и **conditional formatting by date**. Без этих объектов остальной код не имеет куда применяться.

## Шаг 2: Создать вспомогательную функцию для добавления условного формата TIME_PERIOD

Вместо повторения одинакового шаблона для каждого диапазона мы инкапсулируем логику во вспомогательной функции. Эта функция присваивает **background color conditional format**, который раскрашивает ячейки в зависимости от `TimePeriodType` (например, Yesterday, Today, LastWeek).

```python
def add_time_period_condition(cell_range: str, bg_color: Color, period: TimePeriodType):
    """
    Attach a TIME_PERIOD conditional format to `cell_range`.
    The rule highlights cells that fall within `period` using `bg_color`.

    Args:
        cell_range: A1‑style range string, e.g., "I19:K20".
        bg_color:   Desired background color for matching cells.
        period:     Aspose.Cells TimePeriodType enum value.
    Returns:
        The FormatConditionCollection for further customization if needed.
    """
    # 1️⃣ Attach a new ConditionalFormatting block to the specified range
    worksheet.conditional_formattings.add(cell_range)

    # 2️⃣ Grab the collection of conditions for that block
    conditions = worksheet.conditional_formattings[-1].format_conditions

    # 3️⃣ (Optional) Set a default background for the whole range
    conditions.back_color = bg_color

    # 4️⃣ Add a TIME_PERIOD condition and configure its appearance
    idx = conditions.add_condition(FormatConditionType.TIME_PERIOD)
    condition = conditions[idx]

    # Apply the visual style – pink background in this example
    condition.style.background_color = Color.pink
    condition.style.pattern = BackgroundType.SOLID

    # Define which period triggers the formatting
    condition.time_period = period

    return conditions
```

*Почему мы используем вспомогательную функцию:* Она изолирует логику **date based conditional format**, делая код более читаемым, тестируемым и переиспользуемым в разных листах или проектах.

## Шаг 3: Применить правило условного форматирования к конкретному диапазону

Теперь мы используем вспомогательную функцию, чтобы выделить ячейки, содержащие «Yesterday». Это ядро нашей операции **create conditional formatting rule**.

```python
# Step 3 – highlight cells I19:K20 that contain “Yesterday”
add_time_period_condition(
    cell_range="I19:K20",
    bg_color=Color.medium_sea_green,   # optional default background for the whole range
    period=TimePeriodType.YESTERDAY   # the date‑based trigger
)
```

Когда рабочая книга открывается, любая ячейка в диапазоне `I19:K20`, дата которой совпадает с датой вчера, будет отображаться с розовой заливкой (стиль, заданный во вспомогательной функции). Параметр `bg_color` показывает, как можно добавить фон по умолчанию позади условного цвета, если это необходимо.

## Шаг 4: Заполнить диапазон примерными датами

Правило условного форматирования становится видимым только после того, как лист содержит данные, удовлетворяющие условию. Мы вставим две даты: одну, соответствующую «Yesterday», и другую, находящуюся за пределами периода.

```python
# Step 4 – insert sample dates for demonstration

# Cell I19 will match the YESTERDAY period
yesterday_cell = worksheet.cells.get("I19")
yesterday_cell.put_value(datetime(2008, 7, 30))   # 30‑Jul‑2008 is “yesterday” relative to 31‑Jul‑2008
yesterday_cell.get_style().number = 30          # 30 = built‑in date format
yesterday_cell.set_style(yesterday_cell.get_style())

# Cell K20 will NOT match the period (it’s a later date)
outside_cell = worksheet.cells.get("K20")
outside_cell.put_value(datetime(2008, 8, 3))     # 03‑Aug‑2008 is outside “Yesterday”
outside_cell.get_style().number = 30
outside_cell.set_style(outside_cell.get_style())

# Optional label for clarity – not part of the rule
worksheet.cells.get("I20").put_value("Yesterday")
```

*Почему это важно:* Используя объекты `datetime`, мы гарантируем, что Excel воспринимает значения как настоящие даты, что необходимо для корректной работы **conditional formatting by date**. Числовой формат (`30`) обеспечивает отображение ячеек как распознаваемых дат.

## Шаг 5: Автоматически подобрать ширину столбца и сохранить рабочую книгу

После того как данные и форматирование установлены, последний штрих — **auto fit column** ширины столбцов, чтобы даты были полностью видимы. Затем мы записываем файл на диск.

```python
# Step 5 – adjust column width and save the file

# Auto‑fit column 12 (the column that contains our sample data)
worksheet.auto_fit_column(12)

# Save the workbook as an XLSX file
output_path = "YOUR_DIRECTORY/TimePeriodDemo.out.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to {output_path}")
```

Вызов `auto_fit_column` проверяет самое длинное содержимое в столбце 12 (соответствующем столбцу **L** в Excel) и соответственно расширяет ширину. Этот небольшой шаг предотвращает обрезку дат и делает **background color conditional format** явно видимым.

### Ожидаемый результат

Когда вы откроете `TimePeriodDemo.out.xlsx`:

| I19 (дата) | I20 (метка) | K20 (дата) |
|------------|------------|------------|
| 30‑Jul‑2008 (highlighted pink) | Yesterday | 03‑Aug‑2008 (no highlight) |

* Ячейка с датой вчерашнего дня показывает розовый фон, потому что **create conditional formatting rule** совпало с периодом `YESTERDAY`.
* Все остальные ячейки сохраняют фон по умолчанию (или опциональный `medium_sea_green`, который вы указали).
* Столбец L автоматически расширяется, поэтому даты полностью читаемы.

## Распространённые варианты и граничные случаи

| Ситуация | Как адаптировать код |
|-----------|-----------------------|
| **Highlight “Today” instead of “Yesterday”** | Replace `TimePeriodType.YESTERDAY` with `TimePeriodType.TODAY`. |
| **Use a different background color** | Change `condition.style.background_color = Color.pink` to any other `Color` (e.g., `Color.light_sky_blue`). |
| **Apply the rule to a non‑contiguous range** | Call `add_time_period_condition` multiple times with different `cell_range` strings (e.g., `"A1:A10", "C1:C10"`). |
| **Work with a pre‑existing workbook** | Load the file with `Workbook("myfile.xlsx")` instead of creating a new one. |
| **Multiple date‑based conditions on the same range** | After the first `add_time_period_condition` call, add another condition with `conditions.add_condition(FormatConditionType.TIME_PERIOD)` and set a different `time_period`. |

## Заключение

Теперь вы знаете, как **create conditional formatting rule**, реагирующее на даты, применить **background color conditional format** и **auto fit column** ширины столбцов с помощью Aspose.Cells for Python. Вспомогательная функция абстрагирует логику, позволяя переиспользовать тот же шаблон для любой ситуации **conditional formatting by date** — будь то «Yesterday», «LastWeek» или пользовательский диапазон.

Далее вы можете изучить:

* Добавление **icon sets** или **data bars** рядом с правилами по датам.
* Генерацию динамических отчётов, получающих даты из базы данных.
* Комбинирование нескольких правил **date based conditional format** на одном листе.

Не стесняйтесь экспериментировать с разными цветами, периодами и диапазонами, чтобы соответствовать потребностям вашего проекта. Приятного кодирования!

## Что стоит изучить дальше?

Следующие руководства охватывают тесно связанные темы, построенные на техниках, продемонстрированных в этом руководстве. Каждый ресурс включает полностью рабочие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [Master Conditional Formatting in Excel Using Aspose.Cells .NET: A Comprehensive Guide](/cells/english/net/formatting/mastering-aspose-cells-net-conditional-formatting/)
- [How to Extract Conditional Formatting Colors Using Aspose.Cells for .NET](/cells/english/net/formatting/extract-conditional-formatting-colors-aspose-cells-net/)
- [Master Conditional Formatting with Custom Fonts in Excel using Aspose.Cells for .NET and C#](/cells/english/net/formatting/conditional-formatting-custom-fonts-aspose-csharp/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}