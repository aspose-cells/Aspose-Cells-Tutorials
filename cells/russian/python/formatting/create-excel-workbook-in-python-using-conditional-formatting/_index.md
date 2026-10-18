---
category: general
date: 2026-09-21
description: Узнайте, как создать рабочую книгу Excel в Python, установить цвет фона
  ячейки и применить условное форматирование на основе даты с помощью Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- set cell background color
- format cells by date
- excel conditional formatting python
- date based conditional formatting
language: ru
lastmod: 2026-09-21
og_description: Создайте рабочую книгу Excel в Python, задайте цвет фона ячейки и
  примените условное форматирование по дате с помощью Aspose.Cells. Следуйте пошаговому
  руководству.
og_image_alt: Screenshot of an Excel sheet showing a yellow‑green cell background
  for yesterday's dates
og_title: Создайте книгу Excel в Python с условным форматированием
schemas:
- author: Aspose
  dateModified: '2026-09-21'
  description: Learn how to create Excel workbook in Python, set cell background color,
    and apply date based conditional formatting with Aspose.Cells.
  headline: Create Excel workbook in Python using conditional formatting
  type: TechArticle
tags:
- Python
- Excel
- Aspose.Cells
title: Создание рабочей книги Excel в Python с использованием условного форматирования
url: /ru/python/formatting/create-excel-workbook-in-python-using-conditional-formatting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание Excel‑книги в Python с использованием условного форматирования

Если вам нужно **создавать Excel‑книги python** скриптами, которые автоматически подсвечивают даты, это руководство покажет, как это сделать. Вы увидите, как **установить цвет фона ячейки**, добавить правило «Вчера», и сохранить файл — все с помощью Aspose.Cells for Python.

Работа с Excel‑файлами программно часто подразумевает повторение одной и той же логики форматирования на многих листах. К концу этого урока у вас будет переиспользуемый шаблон для **excel conditional formatting python**, который можно внедрить в любой проект.

## Требования

- Python 3.8+ установлен  
- пакет `aspose-cells` (`pip install aspose-cells`)  
- базовое знакомство с функциями Python и модулем `datetime`  

Дополнительные библиотеки не требуются; Aspose.Cells обрабатывает все операции с Excel.

## Шаг 1: Создать книгу и получить первый лист

Первый шаг — **создать excel workbook python** объект и взять дефолтный лист. Это даст вам чистый холст для дальнейшего стилизования.

```python
# Import required Aspose.Cells classes
from aspose.cells import (
    Workbook, FormatConditionType, TimePeriodType,
    BackgroundType, Color, SaveFormat
)
from datetime import datetime
import os

# Create a new workbook; the first worksheet is at index 0
workbook = Workbook()
worksheet = workbook.worksheets[0]
```

*Почему это важно:* `Workbook()` создаёт Excel‑файл в памяти. Обращение к `worksheets[0]` избавляет от жёсткой привязки к именам листов и работает даже если имя по умолчанию изменится.

## Шаг 2: Вспомогательная функция для добавления условного формата TIME_PERIOD

Чтобы код оставался аккуратным, мы оборачиваем создание условного формата во вспомогательную функцию. Она принимает диапазон ячеек, цвет фона и требуемое правило периода времени.

```python
def add_time_period(sheet, cell_range, bg_color, period_type):
    """
    Adds a TIME_PERIOD conditional formatting rule to `cell_range`.
    The rule paints the cells with `bg_color` when the date matches `period_type`.
    """
    # Retrieve (or create) the ConditionalFormatting collection for the range
    cf = sheet.conditional_formattings.get(cell_range)
    if cf is None:
        cf = sheet.conditional_formattings.add(cell_range)

    # Insert a TIME_PERIOD condition and configure its style
    idx = cf.add_condition(FormatConditionType.TIME_PERIOD)
    condition = cf[idx]
    condition.style.background_color = bg_color          # set cell background color
    condition.style.pattern = BackgroundType.SOLID
    condition.time_period = period_type                # e.g., TimePeriodType.YESTERDAY
```

*Почему это важно:* Вспомогательная функция абстрагирует повторяющиеся шаги создания условного формата, делая его лёгким для переиспользования в других правилах, основанных на датах, таких как «Сегодня» или «Последняя неделя».

## Шаг 3: Применить правило «Вчера» к диапазону

Теперь используем вспомогательную функцию, чтобы подсветить ячейки, содержащие дату вчерашнего дня. Диапазон `I19:K20` станет **medium sea green**, когда условие выполнится.

```python
add_time_period(
    worksheet,
    "I19:K20",                # range to format
    Color.medium_sea_green,  # set cell background color
    TimePeriodType.YESTERDAY # date based conditional formatting
)
```

*Почему это важно:* `TimePeriodType.YESTERDAY` входит в встроенный перечислитель Aspose.Cells, поэтому нет необходимости вручную вычислять даты. Библиотека оценивает правило каждый раз при открытии книги.

## Шаг 4: Заполнить диапазон примерными датами

Чтобы увидеть правило в действии, запишем две даты — одну, соответствующую «Вчера», и одну, не соответствующую. Стиль `number` со значением `30` соответствует встроенному формату даты.

```python
# Cell I19 gets a date that is exactly yesterday (relative to the sample data)
cell = worksheet.cells.get("I19")
cell.put_value(datetime(2008, 7, 30))   # 30 July 2008
cell.style.number = 30                # date format

# Cell K20 gets a date that is outside the rule
cell = worksheet.cells.get("K20")
cell.put_value(datetime(2008, 8, 3))    # 3 August 2008
cell.style.number = 30
```

*Почему это важно:* Вставив конкретные даты, вы можете проверить работу условного форматирования без необходимости открывать файл в определённый день.

## Шаг 5: Добавить описательную метку и авто‑подгонку столбца

Небольшая метка поясняет назначение отформатированного диапазона, а `auto_fit_column` делает лист удобочитаемым.

```python
# Add a label under the formatted range
worksheet.cells.get("I20").put_value("Yesterday")

# Adjust column width for better visibility (column 12 = L)
worksheet.auto_fit_column(12)
```

## Шаг 6: Сохранить книгу

Наконец, записываем книгу на диск. Вызов `os.makedirs` гарантирует, что целевая папка существует.

```python
output_path = os.path.join("YOUR_DIRECTORY", "TimePeriodDemo.xlsx")
os.makedirs(os.path.dirname(output_path), exist_ok=True)

# Save as XLSX – the most widely supported Excel format
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

При открытии *TimePeriodDemo.xlsx* вы увидите:

- Ячейка **I19** закрашена **medium sea green**, потому что её значение соответствует правилу «Вчера».  
- Ячейка **K20** сохраняет фон по умолчанию, так как её дата не удовлетворяет условию.  

Это демонстрирует **format cells by date** с помощью одной строки кода на Python.

## Полный, исполняемый пример

Объединив все части, получаем полный скрипт, который можно скопировать и запустить:

```python
from aspose.cells import (
    Workbook, FormatConditionType, TimePeriodType,
    BackgroundType, Color, SaveFormat
)
from datetime import datetime
import os

# 1️⃣ Create workbook and get first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

# 2️⃣ Helper to add TIME_PERIOD conditional formatting
def add_time_period(sheet, cell_range, bg_color, period_type):
    cf = sheet.conditional_formattings.get(cell_range)
    if cf is None:
        cf = sheet.conditional_formattings.add(cell_range)
    idx = cf.add_condition(FormatConditionType.TIME_PERIOD)
    condition = cf[idx]
    condition.style.background_color = bg_color
    condition.style.pattern = BackgroundType.SOLID
    condition.time_period = period_type

# 3️⃣ Apply “Yesterday” rule (set cell background color)
add_time_period(
    worksheet,
    "I19:K20",
    Color.medium_sea_green,
    TimePeriodType.YESTERDAY
)

# 4️⃣ Fill sample dates (format cells by date)
cell = worksheet.cells.get("I19")
cell.put_value(datetime(2008, 7, 30))
cell.style.number = 30

cell = worksheet.cells.get("K20")
cell.put_value(datetime(2008, 8, 3))
cell.style.number = 30

# 5️⃣ Add label and auto‑fit column
worksheet.cells.get("I20").put_value("Yesterday")
worksheet.auto_fit_column(12)

# 6️⃣ Save the workbook
output_path = os.path.join("YOUR_DIRECTORY", "TimePeriodDemo.xlsx")
os.makedirs(os.path.dirname(output_path), exist_ok=True)
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

Запустите скрипт, откройте полученный файл, и вы увидите условное форматирование в действии.

## Общие варианты и граничные случаи

| Вариант | Как реализовать | Когда использовать |
|-----------|------------------|-------------|
| **Подсветить “Today”** | Заменить `TimePeriodType.YESTERDAY` на `TimePeriodType.TODAY` | Дашборды в реальном времени |
| **Несколько диапазонов** | Вызывать `add_time_period` для каждого диапазона, передавая разные цвета | Сложные отчёты |
| **Динамический диапазон дат** | Использовать `TimePeriodType.LAST_7_DAYS` или `TimePeriodType.NEXT_MONTH` | Скользящие отчёты |
| **Пользовательский цвет** | Использовать `Color.from_argb(255, r, g, b)` для создания любого оттенка | Стиль, соответствующий бренду |

**Pro tip:** Всегда задавайте `condition.style.pattern = BackgroundType.SOLID`, когда нужен сплошной залив, иначе Excel может отобразить градиент, выглядящий непоследовательно в разных версиях.

## Заключение

Теперь вы знаете, как **создавать Excel‑книги python** скриптами, которые **устанавливают цвет фона ячейки**, применяют **excel conditional formatting python** и **format cells by date** с помощью Aspose.Cells. Пример охватывает сценарий **date based conditional formatting**, но тот же шаблон работает для любого правила периода времени.

Дальше вы можете изучить:

- Добавление полос данных или наборов значков (`FormatConditionType.DATA_BAR`)  
- Комбинирование нескольких условных правил для одного диапазона  
- Экспорт книги в PDF (`SaveFormat.PDF`) для отчётности  

Не бойтесь экспериментировать с разными цветами, диапазонами и типами периодов, чтобы подстроить решение под ваши конкретные потребности в отчётности. Приятного кодинга!

## Что вам следует изучить дальше?

Следующие руководства охватывают тесно связанные темы, расширяющие техники, продемонстрированные в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, помогающими освоить дополнительные возможности API и исследовать альтернативные подходы в ваших проектах.

- [Master Excel Cell Formatting and Workbook Management with Aspose.Cells for .NET](/cells/english/net/formatting/excel-formatting-aspose-cells-net/)
- [Excel Automation with Aspose.Cells .NET&#58; Create Workbook & Set External Links](/cells/english/net/automation-batch-processing/excel-automation-aspose-cells-net/)
- [How to Create Workbook Scoped Named Ranges in Excel Using Aspose.Cells .NET](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}