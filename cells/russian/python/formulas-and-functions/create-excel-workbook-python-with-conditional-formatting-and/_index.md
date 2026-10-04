---
category: general
date: 2026-10-04
description: Создайте Excel‑книгу на Python с использованием Aspose.Cells. Изучите
  условное форматирование в Excel на Python, изменение цвета фона ячейки на Python
  и форматирование даты в ячейках на Python в полном примере.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create Excel workbook python
- excel conditional formatting python
- cell background color python
- format cells date python
language: ru
lastmod: 2026-10-04
og_description: Создайте Excel‑книгу на Python с помощью Aspose.Cells. Этот учебник
  пошагово показывает условное форматирование Excel в Python, изменение цвета фона
  ячейки в Python и форматирование даты в ячейках в Python.
og_image_alt: Screenshot of an Excel workbook created with Python showing highlighted
  yesterday dates
og_title: Создание Excel‑книги в Python — полное руководство с условным форматированием
schemas:
- author: Aspose
  dateModified: '2026-10-04'
  description: Create Excel workbook python using Aspose.Cells. Learn excel conditional
    formatting python, cell background color python, and format cells date python
    in a full example.
  headline: Create Excel workbook python with conditional formatting and cell background
    color
  type: TechArticle
- description: Create Excel workbook python using Aspose.Cells. Learn excel conditional
    formatting python, cell background color python, and format cells date python
    in a full example.
  name: Create Excel workbook python with conditional formatting and cell background
    color
  steps:
  - name: '**create Excel workbook python** using the Aspose.Cells library.'
    text: '**create Excel workbook python** using the Aspose.Cells library.'
  - name: Apply **excel conditional formatting python** that automatically highlights
      dates that fall on “Yesterday”.
    text: Apply **excel conditional formatting python** that automatically highlights
      dates that fall on “Yesterday”.
  - name: Set the **cell background color python** to pink (or any color you prefer).
    text: Set the **cell background color python** to pink (or any color you prefer).
  - name: '**format cells date python** so the dates appear in the standard Excel
      date style.'
    text: '**format cells date python** so the dates appear in the standard Excel
      date style.'
  type: HowTo
tags:
- Aspose.Cells
- Python
- Excel automation
title: Создать Excel‑рабочую книгу в Python с условным форматированием и цветом фона
  ячеек
url: /ru/python/formulas-and-functions/create-excel-workbook-python-with-conditional-formatting-and/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создать Excel workbook python с условным форматированием и цветом фона ячейки

Если вам нужно **create Excel workbook python** быстро, это руководство покажет, как именно. Вы увидите полностью готовый, исполняемый пример, который добавляет **excel conditional formatting python**, меняет **cell background color python** и **format cells date python** для выделения «Вчера».  

Во многих сценариях отчётности визуальный индикатор в виде окрашенной ячейки делает данные мгновенно понятными. Этот учебник проведёт вас через каждую строку кода, объяснит, почему каждый шаг важен, и предоставит готовый скрипт, который вы сможете адаптировать под свои проекты.

## Что вы сможете сделать

К концу этой статьи вы сможете:

1. **create Excel workbook python** с использованием библиотеки Aspose.Cells.  
2. Применить **excel conditional formatting python**, который автоматически выделяет даты, попадающие в «Вчера».  
3. Установить **cell background color python** в розовый (или любой другой желаемый цвет).  
4. **format cells date python**, чтобы даты отображались в стандартном стиле даты Excel.  

Предварительный опыт работы с Aspose.Cells не требуется — достаточно рабочей среды Python 3 и доступа к pip.

## Требования

- Установлен Python 3.8 или новее.  
- Пакеты `aspose-cells` и `aspose-pydrawing`, установленные через `pip install aspose-cells aspose-pydrawing`.  
- Базовое знакомство с синтаксисом Python и концепциями Excel (рабочие книги, листы, ячейки).  

> **Pro tip:** Если запускать скрипт в виртуальном окружении, вы избежите конфликтов версий с другими проектами.

## Шаг 1: Настройте проект и импортируйте необходимые классы

Первый шаг при **create Excel workbook python** — импортировать классы Aspose.Cells, которые понадобятся. Эти классы дают прямой доступ к созданию рабочей книги, условному форматированию и стилям.

```python
# Import Aspose.Cells core classes
from aspose.cells import (
    Workbook, FormatConditionType, BackgroundType,
    TimePeriodType, SaveFormat
)

# Import Aspose.PyDrawing for color handling
from aspose.pydrawing import Color

# Standard library for date values
from datetime import datetime
```

*Почему это важно:* Импорт только необходимых символов поддерживает чистоту пространства имён и упрощает чтение скрипта. `Workbook` — точка входа для **create Excel workbook python**, а `FormatConditionType` и `TimePeriodType` необходимы для **excel conditional formatting python**.

## Шаг 2: Создайте новую рабочую книгу и получите первый лист

Теперь мы действительно **create Excel workbook python**. Конструктор `Workbook()` создаёт пустой файл Excel с листом по умолчанию.

```python
# Step 2: Initialize a new workbook
workbook = Workbook()

# Grab the first worksheet (index 0)
worksheet = workbook.worksheets[0]
```

*Объяснение:* Каждый файл Excel начинается как минимум с одного листа. По умолчанию Aspose.Cells называет его «Sheet1». Позже можно добавить дополнительные листы, но для этой демонстрации один лист позволяет сосредоточиться на примере.

## Шаг 3: Определите целевой диапазон для условного форматирования

Условное форматирование работает с прямоугольным диапазоном. Здесь мы выбираем диапазон `I19:K20`, который даёт нам три столбца и две строки для работы.

```python
# Define the range that will receive conditional formatting
target_range = "I19:K20"

# Retrieve (or create) the ConditionalFormatting collection for that range
conditional_formatting = worksheet.conditional_formattings.get(target_range)
```

*Зачем это делаем:* Метод `get` возвращает объект `ConditionalFormatting`, привязанный к указанному диапазону. Если в диапазоне ещё нет форматирования, Aspose.Cells автоматически создаёт новую коллекцию.

## Шаг 4: Добавьте условие TIME_PERIOD и задайте цвет фона

Это ядро **excel conditional formatting python**. Мы добавляем правило `TIME_PERIOD`, которое выделяет ячейки с датами, попадающими в «Вчера».

```python
# Add a TIME_PERIOD condition to the range
condition_index = conditional_formatting.add_condition(FormatConditionType.TIME_PERIOD)

# Access the newly created condition
condition = conditional_formatting[condition_index]

# Configure the condition to target “Yesterday”
condition.time_period = TimePeriodType.YESTERDAY

# Set the cell background color – this is the cell background color python part
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID
```

*Глубокий разбор:*  
- `FormatConditionType.TIME_PERIOD` указывает Excel оценивать даты относительно текущей даты.  
- `TimePeriodType.YESTERDAY` — встроенный enum, который автоматически обновляется каждый день, поэтому рабочая книга всегда выделяет самое последнее «Вчера».  
- Установив `background_color` в `Color.pink` и шаблон в `SOLID`, мы достигаем эффекта **cell background color python** без дополнительного кода VBA.

## Шаг 5: Заполните диапазон образцами дат и примените форматирование дат

Чтобы увидеть условное форматирование в действии, нужны реальные даты. Также необходимо **format cells date python**, чтобы Excel воспринимал их как даты, а не простые числа.

```python
# Helper function to set a cell's date style and value
def set_date(cell_name: str, date_value: datetime):
    cell = worksheet.cells.get(cell_name)
    style = cell.get_style()
    # Excel’s built‑in date format code 30 = "m/d/yy"
    style.number = 30
    cell.set_style(style)
    cell.put_value(date_value)

# Populate I19 with a date that is “yesterday” relative to the sample data
set_date("I19", datetime(2008, 7, 30))   # Example “yesterday”

# Populate K20 with another arbitrary date
set_date("K20", datetime(2008, 8, 3))    # Not “yesterday”
```

*Объяснение:*  
- Строка `style.number = 30` — это шаг **format cells date python**. Код формата 30 соответствует короткому формату даты (`m/d/yy`).  
- Вспомогательная функция делает код DRY (Don’t Repeat Yourself) и упрощает добавление новых дат в дальнейшем.

## Шаг 6: Добавьте описательную метку

Небольшая метка помогает любому, открывающему рабочую книгу, понять, почему ячейки окрашены.

```python
# Place a label next to the formatted range
worksheet.cells.get("I20").put_value("Yesterday")
```

## Шаг 7: Сохраните рабочую книгу на диск

Наконец, мы **create Excel workbook python** на диске, вызвав `save`. Константа `SaveFormat.XLSX` гарантирует, что файл будет в современном формате Office Open XML.

```python
# Define the output path – replace YOUR_DIRECTORY with a real folder
output_path = "YOUR_DIRECTORY/TimePeriodDemo.xlsx"

# Save the workbook
workbook.save(output_path, SaveFormat.XLSX)
print(f"Workbook saved to {output_path}")
```

Когда вы откроете `TimePeriodDemo.xlsx` в Excel, вы увидите:

- Ячейки `I19` и `K20` содержат даты.  
- Ячейка, соответствующая «Вчера» (в этом статическом примере — `I19`), выделена розовым.  
- Метка «Yesterday» появляется в `I20`.  

> **Tip:** Если запустить скрипт в другой день, условное форматирование всё равно выделит ячейку, дата которой ровно на один день меньше текущей системной даты — без изменения кода.

## Полный скрипт — готов к копированию и запуску

Ниже приведена полная, автономная программа, включающая все шаги выше. Скопируйте её в файл с именем `conditional_format_demo.py`, отредактируйте `YOUR_DIRECTORY` и выполните командой `python conditional_format_demo.py`.

```python
from aspose.cells import (
    Workbook, FormatConditionType, BackgroundType,
    TimePeriodType, SaveFormat
)
from aspose.pydrawing import Color
from datetime import datetime

# Step 1: Create a new workbook and get the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

# Step 2: Define the cell range that will receive the conditional format
target_range = "I19:K20"
conditional_formatting = worksheet.conditional_formattings.get(target_range)

# Step 3: Add a TIME_PERIOD condition to the range
condition_index = conditional_formatting.add_condition(FormatConditionType.TIME_PERIOD)

# Step 4: Configure the condition to highlight “Yesterday” dates
condition = conditional_formatting[condition_index]
condition.time_period = TimePeriodType.YESTERDAY
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID

# Helper to set date value and style
def set_date(cell_name: str, date_value: datetime):
    cell = worksheet.cells.get(cell_name)
    style = cell.get_style()
    style.number = 30          # Excel date format code 30 = short date
    cell.set_style(style)
    cell.put_value(date_value)

# Step 5: Populate the range with sample dates (excel conditional formatting python)
set_date("I19", datetime(2008, 7, 30))   # Example “yesterday”
set_date("K20", datetime(2008, 8, 3))    # Another sample date

# Step 6: Add a label describing the condition
worksheet.cells.get("I20").put_value("Yesterday")

# Step 7: Save the workbook
output_path = "YOUR_DIRECTORY/TimePeriodDemo.xlsx"
workbook.save(output_path, SaveFormat.XLSX)
print(f"Workbook saved to {output_path}")
```

### Ожидаемый вывод

При запуске скрипт выводит строку подтверждения:

```
Workbook saved to YOUR_DIRECTORY/TimePeriodDemo.xlsx
```

Открытие сгенерированного файла показывает розовый фон в ячейке, соответствующей правилу «Yesterday», подтверждая, что **excel conditional formatting python** и **cell background color python** работают совместно.

## Распространённые варианты и граничные случаи

| Situation | How to adapt the code |
|-----------|-----------------------|
| **Different highlight color** | Change `Color.pink` to any other `Color` constant, e.g., `Color.light_green`. |
| **Highlight “Today” instead of “Yesterday”** | Set `condition.time_period = TimePeriodType.TODAY`. |
| **Apply formatting to an entire column** | Use a range like `"A:A"` and adjust the `target_range` variable accordingly. |
| **Use a custom date format** | Replace `style.number = 30` with `style.custom = "dd-mmm-yyyy"` for a more readable format. |
| **Multiple conditions on the same range** |  |

## Что изучать дальше?


Следующие руководства охватывают тесно связанные темы, которые развивают техники, продемонстрированные в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы в собственных проектах.

- [Create Excel Workbook Python – Complete Guide with Lambda](/cells/english/python/formulas-and-functions/create-excel-workbook-python-complete-guide-with-lambda/)
- [Create and Save Excel Workbook as PDF in ASP.NET Using Aspose.Cells](/cells/english/net/workbook-operations/create-save-excel-workbook-pdf-aspnet-aspose-cells/)
- [How to Create and Save an Excel Workbook as ODS Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}