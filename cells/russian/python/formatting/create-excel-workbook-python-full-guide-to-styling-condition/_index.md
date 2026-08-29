---
category: general
date: 2026-07-06
description: Создать Excel‑книгу в Python с кодом для установки фонового цвета ячейки,
  программного задания стиля ячейки и добавления условного форматирования в Python
  для выделения сегодняшней даты.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- set cell background color
- set cell style programmatically
- highlight today date excel
- add conditional formatting python
language: ru
lastmod: 2026-07-06
og_description: Создайте Excel‑книгу на Python мгновенно. Узнайте, как программно
  задать цвет фона ячейки, установить стиль ячейки и добавить условное форматирование
  в Python для выделения сегодняшней даты.
og_image_alt: Screenshot of an Excel workbook created with Python showing colored
  cells and today’s date highlighted
og_title: Создание Excel‑книги в Python – стилизация ячеек и выделение сегодняшнего
  дня
schemas:
- author: Aspose
  dateModified: '2026-07-06'
  description: Create Excel workbook Python with code to set cell background color,
    set cell style programmatically, and add conditional formatting python for highlighting
    today’s date.
  headline: Create Excel Workbook Python – Full Guide to Styling & Conditional Formatting
  type: TechArticle
- description: Create Excel workbook Python with code to set cell background color,
    set cell style programmatically, and add conditional formatting python for highlighting
    today’s date.
  name: Create Excel Workbook Python – Full Guide to Styling & Conditional Formatting
  steps:
  - name: Converting a range like `"A1:C3"` into a `CellArea`.
    text: Converting a range like `"A1:C3"` into a `CellArea`.
  - name: Filling every cell in that area with a sequential number (just for demo
      purposes).
    text: Filling every cell in that area with a sequential number (just for demo
      purposes).
  - name: Applying a solid **set cell background color**.
    text: Applying a solid **set cell background color**.
  - name: Adding a conditional rule that **highlight today date excel**.
    text: Adding a conditional rule that **highlight today date excel**.
  type: HowTo
tags:
- Python
- Aspose.Cells
- Excel Automation
- Conditional Formatting
title: Создание рабочей книги Excel на Python – Полное руководство по стилизации и
  условному форматированию
url: /ru/python/formatting/create-excel-workbook-python-full-guide-to-styling-condition/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание Excel Workbook Python – Полное руководство по стилизации и условному форматированию

Когда‑нибудь задавались вопросом, как **create Excel workbook Python** с нуля без открытия Excel? Вы не одиноки. Многие разработчики нуждаются в генерации отчетов, панелей мониторинга или даже простых журналов данных «на лету», и выполнение этого программно экономит часы ручной работы.

В этом руководстве мы пройдем весь процесс: от создания новой книги, до **set cell background color**, до **set cell style programmatically**, и наконец до **highlight today date excel** с использованием **add conditional formatting python**. К концу у вас будет готовый к запуску скрипт, который за секунды создаст отшлифованный файл .xlsx.

---

## Что вы создадите

- Свежий файл Excel с несколькими заполненными ячейками.
- Ячейки, окрашенные пользовательским фоном.
- Числовые и датированные значения, отформатированные определённым числовым стилем.
- Условное правило, которое автоматически выделяет ячейку с сегодняшней датой.

Установка внешнего Excel не требуется — Aspose.Cells for Python via .NET выполняет всю тяжелую работу.

## Необходимые условия

| Требование | Почему это важно |
|------------|-------------------|
| Python 3.8+ | Современный синтаксис и подсказки типов |
| `aspose-cells` package | Основная библиотека для работы с книгой |
| `aspose-pydrawing` (installed with Aspose.Cells) | Предоставляет класс `Color` |
| Basic familiarity with Excel concepts (cells, ranges, formatting) | Делает процесс обучения более плавным |

Установите библиотеку с помощью:

```bash
pip install aspose-cells
```

## Шаг 1: Инициализация Workbook и Worksheet

Первое, что вы делаете, когда **create excel workbook python**, — создаёте объект `Workbook` и получаете лист по умолчанию. Представьте книгу как весь файл Excel, а лист — отдельную вкладку внутри него.

```python
from aspose.cells import Workbook

# Create a new workbook – this is our empty Excel file
book = Workbook()

# Grab the first (default) worksheet
sheet = book.worksheets[0]
```

> **Совет:** Если нужны несколько листов, используйте `book.worksheets.add("MySheet")`, чтобы добавить дополнительные вкладки.

## Шаг 2: Вспомогательный класс для стилизации и условного форматирования

Ниже представлен компактный, но полный класс `ConditionalFormatting`. Он инкапсулирует повторяющиеся задачи:

1. Преобразование диапазона вроде `"A1:C3"` в объект `CellArea`.
2. Заполнение каждой ячейки в этом диапазоне последовательным номером (только для демонстрации).
3. Применение сплошного **set cell background color**.
4. Добавление условного правила, которое **highlight today date excel**.

```python
from aspose.cells import (
    CellArea, FormatConditionType, BackgroundType,
    TimePeriodType, SaveFormat, CellsHelper
)
from aspose.pydrawing import Color
from datetime import datetime

class ConditionalFormatting:
    """
    Utility class that demonstrates how to:
    • set cell background color
    • set cell style programmatically
    • add conditional formatting python
    """
    def __init__(self, worksheet):
        self._sheet = worksheet

    def get_format_condition(self, cell_range: str, color: Color):
        """
        Creates a conditional formatting object for the given range
        and fills the range with a background color.
        """
        index = self._sheet.conditional_formattings.add()
        cf = self._sheet.conditional_formattings[index]

        # Convert "A1:C3" → CellArea object
        area = self.get_cell_area_by_name(cell_range)
        cf.add_area(area)

        # Paint the whole area with the supplied color
        self.fill_cell(cell_range, color)
        return cf

    def fill_cell(self, cell_range: str, color: Color):
        """
        Populates each cell in the range with an incrementing integer
        and applies the supplied background color.
        """
        area = self.get_cell_area_by_name(cell_range)
        counter = 0
        for col in range(area.start_column, area.end_column + 1):
            for row in range(area.start_row, area.end_row + 1):
                cell = self._sheet.cells.get(row, col)

                # Apply background only if a real color is supplied
                if color != Color.empty:
                    style = cell.get_style()
                    style.foreground_color = color
                    style.pattern = BackgroundType.SOLID
                    cell.set_style(style)

                cell.put_value(counter)
                counter += 1

    @staticmethod
    def get_cell_area_by_name(name: str) -> CellArea:
        """
        Parses an Excel‑style address (e.g. "B2:D4") into a CellArea.
        """
        area = CellArea()
        parts = name.replace("$", "").split(':')

        start_row, start_col = CellsHelper.cell_name_to_index(parts[0])
        area.start_row = start_row
        area.start_column = start_col

        if len(parts) == 2:
            end_row, end_col = CellsHelper.cell_name_to_index(parts[1])
            area.end_row = end_row
            area.end_column = end_col
        else:
            area.end_row = start_row
            area.end_column = start_col
        return area

    # -----------------------------------------------------------------
    # Step 2: Add conditional formatting for TODAY
    # -----------------------------------------------------------------
    def add_time_period_1(self):
        """
        Demonstrates add conditional formatting python that highlights
        cells containing today’s date.
        """
        # 1️⃣ Create a formatting range and give it a neutral background
        cf = self.get_format_condition("I1:K2", Color.light_slate_gray)

        # 2️⃣ Add a TIME_PERIOD condition (Today)
        idx = cf.add_condition(FormatConditionType.TIME_PERIOD)
        cond = cf[idx]
        cond.time_period = TimePeriodType.TODAY
        cond.style.background_color = Color.pink
        cond.style.pattern = BackgroundType.SOLID

        # 3️⃣ Populate the cells with date values
        # Cell I1 – today’s date, formatted as a date
        cell = self._sheet.cells.get("I1")
        style = cell.get_style()
        style.number = 30               # 30 = “mm-dd-yy” style in Aspose
        cell.set_style(style)
        cell.put_value(datetime.today())

        # Cell K2 – an arbitrary past date for contrast
        self._sheet.cells.get("K2").put_value(datetime(2008, 7, 30))

        # Cell I2 – a label so the reader knows what’s being highlighted
        self._sheet.cells.get("I2").put_value("Today")
```

### Зачем нужен вспомогательный класс?

- **Reusability:** Вы можете вызвать `add_time_period_1()` для любого листа без переписывания логики.
- **Clarity:** Каждый метод делает одну задачу — признак чистого кода.
- **Extensibility:** Хотите добавить больше правил? Просто добавьте ещё один метод, следуя той же схеме.

## Шаг 3: Применить форматирование и сохранить файл

Теперь мы связываем всё вместе: создаём экземпляр вспомогательного класса, запускаем процедуру форматирования и, наконец, сохраняем книгу на диск.

```python
# Instantiate the helper with our worksheet
formatter = ConditionalFormatting(sheet)

# Fill a demo range with numbers and a light blue background
formatter.get_format_condition("A1:C3", Color.light_sky_blue)

# Add the “today” conditional rule
formatter.add_time_period_1()

# Save the workbook – choose any location you like
output_path = "styled_workbook.xlsx"
book.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to {output_path}")
```

При открытии *styled_workbook.xlsx* вы должны увидеть:

- Ячейки **A1:C3** пронумерованы от 0 до 8 с заливкой light‑sky-blue.
- Ячейка **I1** отображает сегодняшнюю дату на розовом фоне (благодаря условному правилу).
- Ячейка **K2** показывает фиксированную дату *2008‑07‑30* для сравнения.
- Ячейка **I2** содержит текст «Today».

Этот визуальный индикатор точно соответствует требованию **highlight today date excel**.

## Шаг 4: Углубляемся — настройка стилей

Если необходимо настроить шрифты, границы или числовые форматы, вы можете расширить метод `fill_cell` или создать новый вспомогательный класс:

```python
def apply_custom_style(cell, font_name="Calibri", font_size=11, bold=False):
    style = cell.get_style()
    style.font.name = font_name
    style.font.size = font_size
    style.font.bold = bold
    cell.set_style(style)
```

Затем вы можете вызвать `apply_custom_style(cell, bold=True)` внутри цикла, чтобы **set cell style programmatically** для каждой ячейки в диапазоне.

## Распространённые ошибки и как их избежать

| Симптом | Вероятная причина | Решение |
|---------|-------------------|---------|
| Ячейки остаются белыми, несмотря на `Color.light_sky_blue` | Стиль не был применён после установки `foreground_color` | Всегда вызывайте `cell.set_style(style)` после изменения объекта стиля. |
| Условное правило никогда не срабатывает | `style.number` не установлен для ячеек даты, поэтому Excel воспринимает значение как строку | Установите `style.number = 30` (или любой формат даты) перед `cell.put_value(datetime…)`. |
| Книга сохраняется как .xls, несмотря на `SaveFormat.XLSX` | Старая версия Aspose, которая по умолчанию использует устаревший формат | Обновите до последней версии пакета `aspose-cells`. |
| Диапазон вроде `"A1"` вызывает ошибку индекса | Использование `cells.get("A1")` на листе, который ещё не инициализирован | Убедитесь, что лист существует (он создаётся сразу после `Workbook()`), или используйте `cells.get(row, col)` с нулевыми индексами. |

## Полный скрипт для копирования и вставки

Ниже представлен **полный** скрипт, который вы можете поместить в файл `create_excel.py` и сразу запустить.



## Что изучать дальше?

Следующие руководства охватывают тесно связанные темы, построенные на техниках, продемонстрированных в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [Excel Automation with Aspose.Cells .NET: Create Workbook & Set External Links](/cells/english/net/automation-batch-processing/excel-automation-aspose-cells-net/)
- [Master Excel Cell Formatting and Workbook Management with Aspose.Cells for .NET](/cells/english/net/formatting/excel-formatting-aspose-cells-net/)
- [Excel Automation: Create a Workbook and Add a ListBox Using Aspose.Cells for .NET](/cells/english/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}