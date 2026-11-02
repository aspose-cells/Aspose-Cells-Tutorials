---
category: general
date: 2026-09-15
description: Узнайте, как применить условное форматирование по периоду времени и сохранить
  рабочую книгу в формате XLSX с помощью Aspose.Cells в Python. Включает пошаговый
  код.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- time period conditional formatting
- save workbook as xlsx
- how to create excel workbook python
- how to highlight yesterday in excel
- add conditional formatting python
language: ru
lastmod: 2026-09-15
og_description: Примените условное форматирование по периоду времени в Excel с помощью
  Python и сохраните книгу в формате XLSX. Следуйте этому полному руководству по Aspose.Cells.
og_image_alt: Screenshot of an Excel sheet where the cells for yesterday are highlighted
  in pink
og_title: Применить условное форматирование по периоду времени в Excel с помощью Python
schemas:
- author: Aspose
  dateModified: '2026-09-15'
  description: Learn how to apply time period conditional formatting and save workbook
    as XLSX with Aspose.Cells in Python. Includes step‑by‑step code.
  headline: How to apply time period conditional formatting in Excel using Python
  type: TechArticle
- description: Learn how to apply time period conditional formatting and save workbook
    as XLSX with Aspose.Cells in Python. Includes step‑by‑step code.
  name: How to apply time period conditional formatting in Excel using Python
  steps:
  - name: '**Creating the workbook** gives you an in‑memory Excel file you can manipulate
      without opening Excel.'
    text: '**Creating the workbook** gives you an in‑memory Excel file you can manipulate
      without opening Excel.'
  - name: '**Defining the range** (`I19:K20`) tells Aspose.Cells where the rule applies,
      keeping the logic isolated.'
    text: '**Defining the range** (`I19:K20`) tells Aspose.Cells where the rule applies,
      keeping the logic isolated.'
  - name: '**Adding a TIME_PERIOD condition** uses Aspose’s built‑in enumeration `TimePeriodType.YESTERDAY`.
      This avoids manual date calculations and automatically updates when the file
      is opened on a different day.'
    text: '**Adding a TIME_PERIOD condition** uses Aspose’s built‑in enumeration `TimePeriodType.YESTERDAY`.
      This avoids manual date calculations and automatically updates when the file
      is opened on a different day.'
  - name: '**Setting the style** (`background_color` and `pattern`) determines how
      the highlighted cells appear. Using `Color.pink` makes the rule easy to spot.'
    text: '**Setting the style** (`background_color` and `pattern`) determines how
      the highlighted cells appear. Using `Color.pink` makes the rule easy to spot.'
  - name: '**Writing sample dates** with number format 30 ensures Excel displays them
      as short dates rather than serial numbers.'
    text: '**Writing sample dates** with number format 30 ensures Excel displays them
      as short dates rather than serial numbers.'
  - name: '**Auto‑fitting the column** improves readability for anyone opening the
      file later.'
    text: '**Auto‑fitting the column** improves readability for anyone opening the
      file later.'
  - name: '**Saving as XLSX** produces a widely compatible file that can be opened
      in Excel, Google Sheets, or any modern spreadsheet program.'
    text: '**Saving as XLSX** produces a widely compatible file that can be opened
      in Excel, Google Sheets, or any modern spreadsheet program.'
  - name: Cells `I19` and `K20` contain the dates `30‑07‑2008` and `03‑08‑2008`.
    text: Cells `I19` and `K20` contain the dates `30‑07‑2008` and `03‑08‑2008`.
  - name: The cell `I20` shows the text “Yesterday”.
    text: The cell `I20` shows the text “Yesterday”.
  - name: If you change your system date to **July 30 2008** and reopen the file,
      the cells with matching dates are automatically filled with pink.
    text: If you change your system date to **July 30 2008** and reopen the file,
      the cells with matching dates are automatically filled with pink.
  type: HowTo
tags:
- Aspose.Cells
- Python
- Excel automation
title: Как применить условное форматирование по периоду времени в Excel с помощью
  Python
url: /ru/python/formatting/how-to-apply-time-period-conditional-formatting-in-excel-usi/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как применить условное форматирование по периоду времени в Excel с помощью Python

Если вам требуется **условное форматирование по периоду времени** в файле Excel, этот учебник покажет, как сделать это с помощью Python. Вы увидите полностью готовый, исполняемый пример, который создаёт рабочую книгу, выделяет даты «вчера», и **сохраняет рабочую книгу как XLSX** всего в несколько строк кода.

Условное форматирование — мощный способ привлечь внимание к данным, соответствующим определённому правилу. В этом руководстве мы сосредоточимся на периоде «Вчера», но тот же подход работает и для других встроенных периодов, таких как Today, LastWeek и NextMonth. К концу урока вы сможете **создавать скрипты python‑style для создания Excel‑рабочих книг**, готовые к использованию в продакшене.

## Предварительные требования

- Установлен Python 3.8+  
- Пакеты `aspose-cells` и `aspose-pydrawing` (`pip install aspose-cells aspose-pydrawing`)  
- Базовое знакомство с синтаксисом Python  

Дополнительная установка Office не требуется, так как Aspose.Cells генерирует файл самостоятельно.

## Условное форматирование по периоду времени с Aspose.Cells в Python

В этом разделе рассматривается каждая строка кода, необходимая для основной задачи. Блок кода ниже — полный скрипт; комментарии объясняют назначение каждого шага.

```python
# -*- coding: utf-8 -*-
"""
Apply time period conditional formatting to highlight yesterday's dates
and save the workbook as XLSX using Aspose.Cells for Python.
"""

from aspose.cells import (
    Workbook, FormatConditionType, BackgroundType,
    TimePeriodType, SaveFormat
)
from aspose.pydrawing import Color
from datetime import datetime

# Step 1: Create a new workbook and select the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

# Step 2: Define the range that will receive the conditional formatting rule
cell_range = "I19:K20"
cond_format = worksheet.conditional_formattings.add(cell_range)

# Step 3: Add a TIME_PERIOD condition for “Yesterday” and style it
condition_index = cond_format.add_condition(FormatConditionType.TIME_PERIOD)
condition = cond_format[condition_index]
condition.style.background_color = Color.pink          # Highlight colour
condition.style.pattern = BackgroundType.SOLID        # Solid fill
condition.time_period = TimePeriodType.YESTERDAY      # Built‑in “Yesterday” period

# Step 4: Populate the range with sample dates (Excel number format 30 = short date)
date_cells = ["I19", "K20"]                           # Cells that will contain dates
sample_dates = [datetime(2008, 7, 30), datetime(2008, 8, 3)]
for cell_ref, date_val in zip(date_cells, sample_dates):
    cell = worksheet.cells.get(cell_ref)
    cell.put_value(date_val)                         # Write the Python datetime
    style = cell.get_style()
    style.number = 30                                 # Excel short date format
    cell.set_style(style)

# Step 5: Add a label so the user knows what the rule represents
worksheet.cells.get("I20").put_value("Yesterday")

# Step 6: Auto‑fit the column for better readability (column L is index 12)
worksheet.auto_fit_column(12)

# Step 7: Save the workbook – this demonstrates “save workbook as xlsx”
output_path = "TimePeriodExample.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

### Почему каждый шаг важен

1. **Создание рабочей книги** даёт вам Excel‑файл в памяти, которым можно манипулировать без открытия Excel.  
2. **Определение диапазона** (`I19:K20`) указывает Aspose.Cells, где применять правило, изолируя логику.  
3. **Добавление условия TIME_PERIOD** использует встроенную перечисление Aspose `TimePeriodType.YESTERDAY`. Это избавляет от ручных вычислений дат и автоматически обновляется при открытии файла в другой день.  
4. **Установка стиля** (`background_color` и `pattern`) определяет, как будут выглядеть выделенные ячейки. Использование `Color.pink` делает правило легко заметным.  
5. **Запись образцовых дат** с числовым форматом 30 гарантирует, что Excel отобразит их как короткие даты, а не как серийные номера.  
6. **Автоподгонка столбца** улучшает читаемость для любого, кто откроет файл позже.  
7. **Сохранение как XLSX** создаёт широко совместимый файл, который можно открыть в Excel, Google Sheets или любой современной таблице.

## Как создать Excel‑рабочую книгу в стиле Python с Aspose.Cells

Приведённый выше скрипт уже демонстрирует минимальные шаги для **создания Excel‑рабочей книги в Python**. На практике вы можете захотеть:

- Добавить несколько листов (`workbook.worksheets.add("Report")`).  
- Заполнить большие таблицы данными с помощью циклов или pandas DataFrame (`worksheet.cells.import_data_table`).  
- Применить дополнительное форматирование (шрифты, границы) через `cell.get_style()`.

Все эти действия следуют одной схеме: получить объект, изменить его свойства и вызвать `set_style` или `save`.

## Добавление условного форматирования в Python – другие полезные шаблоны

Помимо примера «Вчера», Aspose.Cells поддерживает несколько типов условного форматирования:

| FormatConditionType | Типичный сценарий использования |
|---------------------|-----------------------------------|
| `FORMAT_CONDITION_TYPE_EXPRESSION` | Пользовательские формулы (`=A1>100`) |
| `FORMAT_CONDITION_TYPE_CELL_VALUE` | Простые сравнения (`>`, `<`, `=`) |
| `FORMAT_CONDITION_TYPE_COLOR_SCALE` | Градиентные шкалы цветов |
| `FORMAT_CONDITION_TYPE_DATA_BAR`   | Внутри‑ячеечные бар‑визуализации |

Чтобы **добавить условное форматирование в Python** для числового порога, замените `FormatConditionType.TIME_PERIOD` на `FormatConditionType.CELL_VALUE` и задайте `condition.operator_type` и `condition.formula1`.

```python
# Example: highlight values greater than 500
idx = cond_format.add_condition(FormatConditionType.CELL_VALUE)
cond = cond_format[idx]
cond.operator_type = ConditionOperatorType.GREATER_THAN
cond.formula1 = "500"
cond.style.background_color = Color.light_green
```

## Сохранение рабочей книги как XLSX – лучшие практики

Когда вы **сохраняете рабочую книгу как xlsx**, учитывайте:

- **Указание правильного `SaveFormat`** (`SaveFormat.XLSX`) во избежание устаревших форматов.  
- **Использование детерминированного имени файла**, если скрипт запускается в цикле (`f"report_{datetime.now():%Y%m%d}.xlsx"`).  
- **Закрытие ресурсов** (`workbook.dispose()`) в длительно работающих сервисах для освобождения нативной памяти.

В примере уже используется `SaveFormat.XLSX`, который создаёт современную, zip‑основанную рабочую книгу, сохраняющую все правила условного форматирования.

## Выделение «вчера» в Excel – шаги проверки

После выполнения скрипта откройте `TimePeriodExample.xlsx`:

1. Ячейки `I19` и `K20` содержат даты `30‑07‑2008` и `03‑08‑2008`.  
2. Ячейка `I20` показывает текст «Yesterday».  
3. Если изменить системную дату на **30 июля 2008 г.** и снова открыть файл, ячейки с совпадающими датами автоматически заполнятся розовым цветом.  
4. Изменение системной даты на любой другой день убирает розовое заполнение, подтверждая, что правило реагирует на **условное форматирование по периоду времени**.

## Распространённые ошибки и как их избежать

- **Отсутствует `aspose-pydrawing`** — класс `Color` находится в этом пакете; забыв установить его, вы получите `ImportError`.  
- **Неправильный числовой формат** — использование формата General по умолчанию показывает серийные номера (например, 39822). Всегда задавайте `style.number = 30` для коротких дат.  
- **Несоответствие диапазона** — диапазон условного форматирования должен включать ячейки, которые вы хотите выделить; иначе правило не будет работать.

## Профессиональный совет: переиспользуйте процедуру форматирования

Если вам нужен тот же правило «Вчера» в нескольких рабочих книгах, вынесите логику в вспомогательную функцию:

```python
def apply_yesterday_highlight(worksheet, address):
    cf = worksheet.conditional_formattings.add(address)
    idx = cf.add_condition(FormatConditionType.TIME_PERIOD)
    cond = cf[idx]
    cond.style.background_color = Color.pink
    cond.style.pattern = BackgroundType.SOLID
    cond.time_period = TimePeriodType.YESTERDAY
```

Вызовите `apply_yesterday_highlight(worksheet, "A1:A10")` в любом месте, где это необходимо.

## Заключение

В этом руководстве мы показали, как реализовать **условное форматирование по периоду времени** в Excel с помощью Python, как **сохранить рабочую книгу как XLSX** и как **выделить вчерашний день в Excel** одним переиспользуемым скриптом. Теперь у вас есть надёжная база для **добавления условного форматирования в Python** в любой проект автоматизации, будь то ежедневные отчёты, построение панелей мониторинга или подготовка экспортов данных.

**Следующие шаги**

- Исследуйте другие значения `TimePeriodType`, такие как `TODAY` или `LAST_WEEK`.  
- Сочетайте несколько условных правил в одном диапазоне для более богатых визуальных подсказок.  
- Интегрируйте генерацию рабочей книги в веб‑сервис или запланированную задачу.

Счастливого кодинга и наслаждайтесь визуальной ясностью, которую приносит условное форматирование в вашу автоматизацию Excel!

## Что изучать дальше?

Следующие учебники охватывают тесно связанные темы, расширяющие техники, продемонстрированные в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы в собственных проектах.

- [Мастерство условного форматирования в Excel с использованием Aspose.Cells .NET : Полное руководство](/cells/english/net/formatting/mastering-aspose-cells-net-conditional-formatting/)
- [Мастер Aspose.Cells .NET : Применение условного форматирования к чередующимся строкам в Excel](/cells/english/net/formatting/aspose-cells-net-conditional-formatting-alternate-rows/)
- [Мастерство условного форматирования с пользовательскими шрифтами в Excel с использованием Aspose.Cells для .NET и C#](/cells/english/net/formatting/conditional-formatting-custom-fonts-aspose-csharp/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}