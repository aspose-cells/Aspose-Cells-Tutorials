---
category: general
date: 2026-09-05
description: Создайте Excel‑книгу в Python и добавьте условное форматирование, чтобы
  выделить ячейки за вчерашний день. Узнайте полный код и почему каждый шаг важен.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- add conditional formatting excel
- highlight cells based on date
- add conditional formatting range
- how to highlight yesterday cells
language: ru
lastmod: 2026-09-05
og_description: Создайте рабочую книгу Excel в Python и добавьте условное форматирование,
  чтобы выделить ячейки за вчерашний день. Следуйте этому пошаговому руководству для
  полного решения.
og_image_alt: Screenshot of an Excel sheet where cells are highlighted after creating
  Excel workbook in Python
og_title: Создайте Excel‑книгу в Python – добавьте условное форматирование
schemas:
- author: Aspose
  dateModified: '2026-09-05'
  description: Create Excel workbook in Python and add conditional formatting to highlight
    yesterday cells. Learn the full code and why each step matters.
  headline: Create Excel workbook in Python with conditional formatting
  type: TechArticle
tags:
- Excel
- Python
- Aspose.Cells
- Conditional Formatting
title: Создать книгу Excel в Python с условным форматированием
url: /ru/python/formatting/create-excel-workbook-in-python-with-conditional-formatting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание рабочей книги Excel в Python с условным форматированием

Если вам нужно **create Excel workbook python** для задачи отчётности, это руководство покажет, как создать рабочую книгу и применить правило условного форматирования, которое выделяет даты вчерашнего дня. Вы увидите точный код, почему каждая строка существует, и как адаптировать решение для других диапазонов дат.

Условное форматирование — мощный способ привлечь внимание к данным, соответствующим определённому условию. В этом руководстве мы используем библиотеку Aspose.Cells для Python через .NET, которая предоставляет полную поддержку функций Excel без необходимости установки Microsoft Office. К концу руководства у вас будет файл, где ячейки в диапазоне *I19:K20* становятся розовыми, если они содержат дату вчерашнего дня.

## Предварительные требования

* Установлен Python 3.9+ 
* Пакет `aspose-cells` (установить с помощью `pip install aspose-cells`)
* Базовое знакомство с синтаксисом Python
* Права записи в каталог, где будет сохранена рабочая книга

Код работает на Windows, macOS и Linux, при условии, что доступна среда выполнения .NET.

## Создание рабочей книги Excel в Python

Первый шаг — создать объект `Workbook` и получить доступ к листу по умолчанию. Этот объект представляет весь файл Excel в памяти.

```python
from aspose.cells import Workbook, SaveFormat

# Create a new workbook and select the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]
```

*Почему это важно*: `Workbook()` создаёт пустую рабочую книгу с одним листом. Обращение к `worksheets[0]` даёт вам возможность позже добавлять данные, стили и форматирование.

## Добавление диапазона условного форматирования

Далее мы определяем область, которая будет оцениваться условным правилом. Диапазон `I19:K20` охватывает шесть ячеек в двух строках.

```python
# Define the range that will receive the conditional formatting rule
condition_collection = worksheet.conditional_formattings.add("I19:K20")
```

*Почему это важно*: Добавление коллекции условного форматирования к конкретному диапазону изолирует правило, предотвращая его влияние на несвязанные ячейки. Это удовлетворяет требованию **add conditional formatting range**.

## Определение правила: выделение ячеек по дате

Теперь мы создаём условие типа `TIME_PERIOD`. Это указывает Excel сравнивать значение каждой ячейки с предопределённым временным интервалом.

```python
from aspose.cells import FormatConditionType, TimePeriodType

# Add a TIME_PERIOD condition to the collection
condition_index = condition_collection.add_condition(FormatConditionType.TIME_PERIOD)
condition = condition_collection[condition_index]

# Set the time period to “Yesterday”
condition.time_period = TimePeriodType.YESTERDAY
```

*Почему это важно*: `TIME_PERIOD` — единственный встроенный тип, который напрямую поддерживает «Yesterday», «Today», «Last Week» и т.д. Установив `condition.time_period` в `YESTERDAY`, правило автоматически сравнивает значение даты в ячейке с днём, предшествующим текущей дате.

## Оформление ячеек, соответствующих условию

Условному форматированию также нужен визуальный стиль. Здесь мы выбираем сплошную розовую заливку, чтобы выделить подходящие ячейки.

```python
from aspose.pydrawing import Color as DrawingColor
from aspose.cells import BackgroundType

# Apply a pink solid background to cells that satisfy the condition
condition.style.background_color = DrawingColor.pink
condition.style.pattern = BackgroundType.SOLID
```

*Почему это важно*: Объект стиля определяет, как Excel будет отображать ячейки, соответствующие условию. Использование сплошной розовой заливки удовлетворяет требованию **highlight cells based on date** и упрощает проверку результата.

## Заполнение примерными датами для оценки

Чтобы увидеть правило в действии, мы вставляем две даты — одну, соответствующую дате вчера, и другую, не соответствующую. Формат `number` `30` соответствует встроенному формату даты `mm-dd-yy`.

```python
from datetime import datetime

# Cell I19: a date that matches “Yesterday”
cell_i19 = worksheet.cells.get("I19")
cell_i19.put_value(datetime(2008, 7, 30))   # Example date; adjust as needed
cell_i19.style.number = 30
cell_i19.set_style(cell_i19.style)

# Cell K20: a date outside the “Yesterday” period
cell_k20 = worksheet.cells.get("K20")
cell_k20.put_value(datetime(2008, 8, 3))    # Example date; adjust as needed
cell_k20.style.number = 30
cell_k20.set_style(cell_k20.style)

# Optional label for the range
worksheet.cells.get("I20").put_value("Yesterday")
```

*Почему это важно*: Предоставление как совпадающей, так и не совпадающей даты позволяет проверить корректность работы условного форматирования. При запуске скрипта скорректируйте даты на текущий месяц или замените их динамическими значениями.

## Сохранение рабочей книги

Наконец мы записываем файл на диск. Константа `SaveFormat.XLSX` гарантирует, что результат будет современным файлом Excel.

```python
output_path = "YOUR_DIRECTORY/TimePeriodExample.xlsx"
workbook.save(output_path, SaveFormat.XLSX)
print(f"Workbook saved to {output_path}")
```

*Почему это важно*: Сохранение рабочей книги позволяет открыть её в Excel, LibreOffice или любом просмотрщике, поддерживающем XLSX. Выведенный путь подтверждает, куда был записан файл.

## Полный скрипт

Объединив все части, получаем полный, исполняемый скрипт:

```python
# -*- coding: utf-8 -*-
"""
Create an Excel workbook in Python, add a conditional formatting rule,
and highlight yesterday's cells.
"""

from aspose.cells import (
    Workbook, SaveFormat, FormatConditionType,
    BackgroundType, TimePeriodType
)
from aspose.pydrawing import Color as DrawingColor
from datetime import datetime

# Step 1: Create a new workbook and access the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

# Step 2: Add a conditional formatting rule for the range I19:K20
condition_collection = worksheet.conditional_formattings.add("I19:K20")
condition_index = condition_collection.add_condition(FormatConditionType.TIME_PERIOD)
condition = condition_collection[condition_index]

# Step 3: Define the visual style for cells that meet the condition
condition.style.background_color = DrawingColor.pink
condition.style.pattern = BackgroundType.SOLID

# Step 4: Set the time‑period to “Yesterday”
condition.time_period = TimePeriodType.YESTERDAY

# Step 5: Populate sample dates for evaluation
cell_i19 = worksheet.cells.get("I19")
cell_i19.put_value(datetime(2008, 7, 30))   # yesterday relative to the example
cell_i19.style.number = 30
cell_i19.set_style(cell_i19.style)

cell_k20 = worksheet.cells.get("K20")
cell_k20.put_value(datetime(2008, 8, 3))    # outside the period
cell_k20.style.number = 30
cell_k20.set_style(cell_k20.style)

# Step 6: Add a label for the formatted range
worksheet.cells.get("I20").put_value("Yesterday")

# Step 7: Save the workbook
output_path = "YOUR_DIRECTORY/TimePeriodExample.xlsx"
workbook.save(output_path, SaveFormat.XLSX)
print(f"Workbook saved to {output_path}")
```

### Ожидаемый результат

Когда вы откроете `TimePeriodExample.xlsx`:

* Ячейка **I19** отображается с розовым фоном, потому что её значение соответствует вчерашнему дню.
* Ячейка **K20** сохраняет фон по умолчанию, так как её дата находится вне периода.
* Метка **«Yesterday»** находится в ячейке I20 для наглядности.

## Распространённые варианты и граничные случаи

| Situation | Adjustment |
|-----------|------------|
| **Выделить сегодня вместо вчера** | Изменить `condition.time_period = TimePeriodType.TODAY`. |
| **Применить правило к более крупной области** | Обновить строку диапазона в `add(\"I19:K20\")` на что‑то вроде `"A1:Z100"`. |
| **Использовать другой цвет заливки** | Заменить `DrawingColor.pink` на любой другой `DrawingColor` (например, `DrawingColor.light_green`). |
| **Работать с динамическими датами** | Вычислить `datetime.now() - timedelta(days=1)` для вчерашнего дня и записать это значение в ячейки перед применением правила. |

**Pro tip:** При программной генерации рабочей книги для многих пользователей держите определение условного форматирования отдельно от вставки данных. Так вы сможете переиспользовать один и тот же стиль на нескольких листах без дублирования кода.

## Программная проверка результата (необязательно)

Если вы хотите подтвердить форматирование без открытия Excel, вы можете проверить стиль ячейки после сохранения:



## Что изучать дальше?

Следующие руководства охватывают тесно связанные темы, основанные на техниках, продемонстрированных в этом руководстве. Каждый ресурс включает полные рабочие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [Excel Automation&#58; Создание рабочей книги и добавление ListBox с помощью Aspose.Cells для .NET](/cells/english/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)
- [Создание рабочей книги Excel и добавление меток с Aspose.Cells для Java](/cells/english/java/advanced-excel-charts/data-labeling/)
- [Excel Automation: Создание рабочей книги, добавление ListBox, Aspose Cells](/cells/german/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}