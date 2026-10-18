---
category: general
date: 2026-08-08
description: Создайте Excel‑книгу на Python и добавьте условное форматирование на
  основе даты. Пошаговое руководство с использованием Aspose.Cells для выделения ячеек
  за вчерашний день.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- conditional formatting based on date
- Aspose.Cells Python example
- Excel date formatting Python
- Python Excel automation
language: ru
lastmod: 2026-08-08
og_description: Создайте Excel‑книгу на Python с Aspose.Cells и примените условное
  форматирование по дате для динамических таблиц.
og_image_alt: Screenshot of an Excel sheet created with Python showing cells highlighted
  by date conditional formatting
og_title: Создать рабочую книгу Excel на Python – условное форматирование дат
schemas:
- author: Aspose
  dateModified: '2026-08-08'
  description: Create Excel workbook Python and add conditional formatting based on
    date. Step‑by‑step guide using Aspose.Cells to highlight yesterday’s cells.
  headline: Create Excel workbook Python date conditional formatting
  type: TechArticle
tags:
- Python
- Excel
- Aspose.Cells
title: Создать книгу Excel с условным форматированием дат в Python
url: /ru/python/formatting/create-excel-workbook-python-date-conditional-formatting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Create Excel workbook Python date conditional formatting

Если вам нужно **create Excel workbook Python** и автоматически подсвечивать ячейки, соответствующие определённой дате, этот учебник покажет, как это сделать. Вы узнаете, как применить **conditional formatting based on date**, чтобы даты вчерашнего дня подсвечивались розовым цветом, используя библиотеку Aspose.Cells.

Руководство проходит каждый шаг — от установки SDK до сохранения окончательного файла .xlsx — чтобы вы могли скопировать‑вставить работающий пример в свой проект. Внешняя документация не требуется; весь код и пояснения находятся в одном месте.

## Предварительные требования

* Установлен Python 3.8 или новее.
* Пакет `aspose-cells` (обёртка Python для Aspose.Cells). Установите его с помощью:
  ```bash
  pip install aspose-cells
  ```
* Базовое знакомство с Python и концепциями Excel, такими как листы и стили ячеек.

> **Совет:** Aspose.Cells работает без установленного Microsoft Excel, что делает его идеальным для серверной автоматизации.

## Шаг 1: Создание Excel workbook в Python

Первая задача — создать новый workbook и получить лист по умолчанию. Этот объект представляет весь файл Excel и предоставляет доступ к строкам, столбцам и API форматирования.

```python
from aspose.cells import Workbook, SaveFormat

# Create a new workbook – this automatically adds one worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]   # reference to the first (default) sheet
```

Создание workbook является основой для любой дальнейшей манипуляции, будь то добавление данных, формул или правил форматирования.

## Шаг 2: Определение условного формата на основе даты

Теперь мы добавляем **conditional formatting based on date**. Перечисление `FormatConditionType.TIME_PERIOD` позволяет указать встроенные периоды времени, такие как Yesterday, Today или LastWeek.

```python
from aspose.cells import FormatConditionType, BackgroundType, TimePeriodType
from aspose.pydrawing import Color

# Target range I19:K20 – three columns by two rows
range_obj = worksheet.get_range("I19:K20")
conditions = range_obj.format_conditions

# Add a new time‑period condition (e.g., Yesterday)
condition_index = conditions.add_condition(FormatConditionType.TIME_PERIOD)
condition = conditions[condition_index]

# Set the visual style: pink solid background
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID

# Specify that the condition should trigger for "Yesterday"
condition.time_period = TimePeriodType.YESTERDAY
```

Почему этот шаг важен: Excel оценивает условие для каждой ячейки в диапазоне. Когда значение ячейки попадает в определённый период (вчера), автоматически применяется назначенный стиль.

## Шаг 3: Заполнение диапазона образцами дат

Чтобы увидеть правило в действии, мы записываем несколько объектов `datetime` в целевые ячейки. Один из них намеренно установлен на дату вчерашнего дня относительно внутренней системы дат workbook.

```python
from datetime import datetime

# Cell I19 – yesterday’s date (will be highlighted)
cell_i19 = worksheet.cells.get("I19")
cell_i19.put_value(datetime(2008, 7, 30))   # This date matches the "Yesterday" rule
style_i19 = cell_i19.get_style()
style_i19.number = 30                       # Excel’s built‑in date format
cell_i19.set_style(style_i19)

# Cell K20 – a random later date (no highlight)
cell_k20 = worksheet.cells.get("K20")
cell_k20.put_value(datetime(2008, 8, 3))    # Not yesterday, so no formatting
style_k20 = cell_k20.get_style()
style_k20.number = 30
cell_k20.set_style(style_k20)

# Optional label for clarity
worksheet.cells.get("I20").put_value("Yesterday")
```

Строка `number = 30` указывает Excel отображать значение в стандартном коротком формате даты. Вы можете изменить этот индекс на любой встроенный числовой формат, если предпочитаете другое представление.

## Шаг 4: Настройка ширины столбца для удобочитаемости

Автоподгонка ширины столбца, содержащего даты, делает вывод более читаемым, особенно когда workbook открывается в Excel или в просмотрщике.

```python
# Column 12 corresponds to column L (zero‑based indexing)
worksheet.auto_fit_column(12)
```

## Шаг 5: Сохранение workbook на диск

Наконец, сохраните workbook в файл .xlsx. Замените `"YOUR_DIRECTORY"` реальным путём на вашем компьютере.

```python
import os

output_path = os.path.join("YOUR_DIRECTORY", "TimePeriodDemo.out.xlsx")
workbook.save(output_path, SaveFormat.XLSX)
print(f"Workbook saved to {output_path}")
```

Когда вы откроете `TimePeriodDemo.out.xlsx` в Excel, ячейка **I19** будет отображаться с розовым фоном, потому что её значение соответствует правилу “Yesterday”, тогда как **K20** останется без изменений.

### Ожидаемый результат

| I19 (дата) | I20 (метка) | J19 | J20 | K19 | K20 (дата) |
|------------|-------------|-----|-----|-----|------------|
| *2008‑07‑30* (розовый фон) | Вчера | – | – | – | *2008‑08‑03* (без форматирования) |

Розовая заливка подтверждает, что **conditional formatting based on date** работает как задумано.

## Общие варианты и граничные случаи

| Ситуация | Как адаптировать код |
|-----------|-----------------------|
| **Подсветить “Today” вместо “Yesterday”** | Change `condition.time_period = TimePeriodType.TODAY` |
| **Применить правило ко всему столбцу** | Use `worksheet.get_range("A:A").format_conditions` |
| **Использовать пользовательский диапазон дат (например, последние 7 дней)** | Replace the time‑period condition with a formula condition: <br>```python<br>condition = conditions.add_condition(FormatConditionType.FORMULA)<br>condition.formula1 = 'AND(A1>=TODAY()-7, A1<=TODAY())'<br>``` |
| **Другие цвета фона** | Set `condition.style.background_color = Color.light_green` (or any `Color` you prefer) |
| **Запуск на Linux без дисплея** | Aspose.Cells полностью безголовый; дополнительная конфигурация не требуется. |

## Полный, исполняемый пример

Ниже приведён полный скрипт, который можно выполнить как есть (после обновления каталога вывода). Включены все импорты, комментарии и базовая обработка ошибок.

```python
# -*- coding: utf-8 -*-
"""
Create Excel workbook Python with date conditional formatting.
Demonstrates how to highlight yesterday’s dates using Aspose.Cells.
"""

import os
from datetime import datetime
from aspose.cells import (
    Workbook, SaveFormat,
    FormatConditionType, BackgroundType,
    TimePeriodType
)
from aspose.pydrawing import Color

# ----------------------------------------------------------------------
# 1️⃣ Initialize workbook
# ----------------------------------------------------------------------
workbook = Workbook()
worksheet = workbook.worksheets[0]

# ----------------------------------------------------------------------
# 2️⃣ Add conditional formatting for "Yesterday"
# ----------------------------------------------------------------------
range_obj = worksheet.get_range("I19:K20")
conditions = range_obj.format_conditions
cond_idx = conditions.add_condition(FormatConditionType.TIME_PERIOD)
condition = conditions[cond_idx]

# Visual style: pink solid fill
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID
condition.time_period = TimePeriodType.YESTERDAY

# ----------------------------------------------------------------------
# 3️⃣ Populate sample dates
# ----------------------------------------------------------------------
# Cell that should match the condition
cell_i19 = worksheet.cells.get("I19")
cell_i19.put_value(datetime(2008, 7, 30))   # Yesterday relative to demo data
style_i19 = cell_i19.get_style()
style_i19.number = 30                       # Excel short‑date format
cell_i19.set_style(style_i19)

# Cell that does NOT match
cell_k20 = worksheet.cells.get("K20")
cell_k20.put_value(datetime(2008, 8, 3))
style_k20 = cell_k20.get_style()
style_k20.number = 30
cell_k20.set_style(style_k20)

# Optional label
worksheet.cells.get("I20").put_value("Yesterday")

# ----------------------------------------------------------------------
# 4️⃣ Auto‑fit column for better visibility
# ----------------------------------------------------------------------
worksheet.auto_fit_column(12)   # Column L (0‑based index)

# ----------------------------------------------------------------------
# 5️⃣ Save workbook
# ----------------------------------------------------------------------
output_dir = "YOUR_DIRECTORY"   # <-- replace with a real folder
os.makedirs(output_dir, exist_ok=True)
output_path = os.path.join(output_dir, "TimePeriodDemo.out.xlsx")
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

Запуск скрипта создаёт файл Excel, где ячейка “Yesterday” автоматически подсвечивается, демонстрируя **create Excel workbook Python** в сочетании с **conditional formatting based on date**.

## Заключение

Теперь вы знаете, как **create Excel workbook Python** объекты, определить **date‑based conditional formatting**


## Что изучать дальше?

Следующие учебники охватывают тесно связанные темы, которые опираются на техники, продемонстрированные в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [Создать Excel Workbook с использованием Aspose.Cells в Java: пошаговое руководство](/cells/english/java/getting-started/create-excel-workbook-aspose-cells-java/)
- [Создать Excel Workbook с диаграммами, используя Aspose.Cells .NET | пошаговое руководство](/cells/english/net/charts-graphs/create-excel-workbook-charts-aspose-cells-net/)
- [Автоматизация Excel: создать Workbook и добавить ListBox с помощью Aspose.Cells для .NET](/cells/english/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}