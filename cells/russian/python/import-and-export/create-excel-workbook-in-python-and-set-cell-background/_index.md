---
category: general
date: 2026-10-07
description: Создать книгу Excel в Python, задать цвет фона ячейки, автоматически
  подобрать ширину столбцов и заполнить даты в Excel с помощью лаконичного примера
  кода.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- set cell background color
- auto fit excel columns
- populate dates in excel
- how to create excel
language: ru
lastmod: 2026-10-07
og_description: Создайте рабочую книгу Excel в Python, затем задайте цвет фона ячеек,
  автоматически подгоните ширину столбцов и заполните даты в Excel. Следуйте этому
  пошаговому руководству, чтобы создать файл TimePeriodDemo.xlsx.
og_image_alt: Screenshot of a Python‑generated Excel workbook with pink highlighted
  cells
og_title: Создайте рабочую книгу Excel в Python – установить фон и авто‑подгонку
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Create Excel workbook in Python, set cell background color, auto‑fit
    columns, and populate dates in Excel with a concise code example.
  headline: Create Excel workbook in Python and set cell background
  type: TechArticle
- description: Create Excel workbook in Python, set cell background color, auto‑fit
    columns, and populate dates in Excel with a concise code example.
  name: Create Excel workbook in Python and set cell background
  steps:
  - name: Import required namespaces and define a helper function
    text: '```python # Step 1: Import Aspose.Cells classes and supporting modules
      from aspose.cells import Workbook, FormatConditionType, TimePeriodType, BackgroundType,
      SaveFormat from aspose.pydrawing import Color from datetime import datetime
      import os ```'
  - name: Create the workbook and get the first worksheet
    text: '```python def create_workbook(): # Step 2: Instantiate a new workbook (empty
      Excel file) book = Workbook() # Aspose.Cells creates a default worksheet; we
      retrieve it for further work sheet = book.worksheets[0] return book, sheet ```'
  - name: Set cell background color with a conditional format
    text: '```python def add_yesterday_rule(sheet): # Define a conditional format
      for the range I19:K20 (Yesterday) conds = sheet.get_range("I19:K20").format_conditions
      idx = conds.add_condition(FormatConditionType.TIME_PERIOD) cond = conds[idx]'
  - name: Populate dates in Excel
    text: '```python def populate_sample_dates(sheet): # Insert a date that falls
      on yesterday relative to the demo data cell = sheet.cells.get("I19") cell.put_value(datetime(2008,
      7, 30)) # sample date cell.style.number = 30 # Excel’s date format ID cell.set_style(cell.style)'
  - name: Auto‑fit Excel columns for better visibility
    text: '```python def auto_fit_columns(sheet): # Auto‑fit column L (index 12) so
      the content is fully visible sheet.auto_fit_column(12) # <-- auto fit excel
      columns ```'
  - name: Save the workbook
    text: '```python def save_workbook(book, filename="TimePeriodDemo.xlsx"): out_path
      = os.path.join("YOUR_DIRECTORY", filename) os.makedirs(os.path.dirname(out_path),
      exist_ok=True) book.save(out_path, SaveFormat.XLSX) print(f"Workbook saved to:
      {out_path}") ```'
  - name: Full script – putting it all together
    text: '```python def main(): # Create workbook and obtain the first worksheet
      book, sheet = create_workbook()'
  type: HowTo
tags:
- Excel
- Python
- Aspose.Cells
title: Создать рабочую книгу Excel в Python и установить фон ячейки
url: /ru/python/import-and-export/create-excel-workbook-in-python-and-set-cell-background/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание рабочей книги Excel в Python и установка фона ячейки

Создайте рабочую книгу Excel в Python и примените условное форматирование всего несколькими строками кода. В этом руководстве показано, **как создавать файлы Excel** программно, задавать цвет фона ячейки, автоматически подгонять ширину столбцов Excel и заполнять даты в Excel с помощью библиотеки Aspose.Cells.

Вы узнаете, как:
* Инициализировать рабочую книгу и получить первый лист.  
* Определить условный формат, который выделяет даты «Вчера».  
* Вставить примерные даты в определённые ячейки.  
* Автоматически подгонять ширину столбцов, чтобы данные были чётко видны.  
* Сохранить рабочую книгу в выбранную папку.

Единственное требование — рабочая среда Python 3 с установленными пакетами `aspose-cells` и `aspose-pydrawing`:

```bash
pip install aspose-cells aspose-pydrawing
```

---

## Создание рабочей книги Excel в Python – пошагово

Следующие разделы разбивают процесс на управляемые шаги. Каждый шаг включает необходимый код, объяснение **почему** это важно, и совет, как избежать распространённых ошибок.

### Шаг 1: Импортировать необходимые пространства имён и определить вспомогательную функцию

```python
# Step 1: Import Aspose.Cells classes and supporting modules
from aspose.cells import Workbook, FormatConditionType, TimePeriodType, BackgroundType, SaveFormat
from aspose.pydrawing import Color
from datetime import datetime
import os
```

*Почему это важно*: Импорт правильных классов даёт доступ к созданию рабочей книги, условному форматированию и работе с цветами.  
**Совет профессионала**: Держите импорты в начале файла; это упрощает чтение скрипта и предотвращает ошибки циклического импорта.

### Шаг 2: Создать рабочую книгу и получить первый лист

```python
def create_workbook():
    # Step 2: Instantiate a new workbook (empty Excel file)
    book = Workbook()
    # Aspose.Cells creates a default worksheet; we retrieve it for further work
    sheet = book.worksheets[0]
    return book, sheet
```

Конструктор `Workbook()` создаёт пустую рабочую книгу Excel в памяти.  
**Почему**: Начало с новой книги гарантирует отсутствие оставшегося форматирования от предыдущих запусков.

### Шаг 3: Установить цвет фона ячейки с помощью условного формата

```python
def add_yesterday_rule(sheet):
    # Define a conditional format for the range I19:K20 (Yesterday)
    conds = sheet.get_range("I19:K20").format_conditions
    idx = conds.add_condition(FormatConditionType.TIME_PERIOD)
    cond = conds[idx]

    # Apply visual style – this is where we set the cell background color
    cond.style.background_color = Color.pink          # <-- set cell background color
    cond.style.pattern = BackgroundType.SOLID
    cond.time_period = TimePeriodType.YESTERDAY
```

*Почему*: Использование условия **time period** автоматически выделяет любую ячейку, содержащую дату «Вчера», устраняя необходимость ручных проверок дат.  
**Совет**: `Color.pink` — лишь пример; вы можете использовать любой объект `Color` (`Color.yellow`, `Color.light_green` и т.д.).

### Шаг 4: Заполнить даты в Excel

```python
def populate_sample_dates(sheet):
    # Insert a date that falls on yesterday relative to the demo data
    cell = sheet.cells.get("I19")
    cell.put_value(datetime(2008, 7, 30))   # sample date
    cell.style.number = 30                 # Excel’s date format ID
    cell.set_style(cell.style)

    # Insert another date outside the “Yesterday” range
    cell = sheet.cells.get("K20")
    cell.put_value(datetime(2008, 8, 3))
    cell.style.number = 30
    cell.set_style(cell.style)

    # Add a label for the rule
    sheet.cells.get("I20").put_value("Yesterday")
```

Здесь мы **заполняем даты в Excel** в ячейках `I19` и `K20`. Первая дата активирует условное форматирование, а вторая — нет.  
**Почему это важно**: Демонстрация как совпадающих, так и несовпадающих значений помогает убедиться, что правило работает как ожидается.

### Шаг 5: Автоматически подгонять ширину столбцов Excel для лучшей видимости

```python
def auto_fit_columns(sheet):
    # Auto‑fit column L (index 12) so the content is fully visible
    sheet.auto_fit_column(12)   # <-- auto fit excel columns
```

`auto_fit_column` регулирует ширину столбца в зависимости от самого длинного значения ячейки.  
**Совет**: Вызывайте эту функцию после записи всех данных; иначе ширина может быть рассчитана по неполному содержимому.

### Шаг 6: Сохранить рабочую книгу

```python
def save_workbook(book, filename="TimePeriodDemo.xlsx"):
    out_path = os.path.join("YOUR_DIRECTORY", filename)
    os.makedirs(os.path.dirname(out_path), exist_ok=True)
    book.save(out_path, SaveFormat.XLSX)
    print(f"Workbook saved to: {out_path}")
```

Сохранение файла записывает рабочую книгу из памяти на диск в современном формате XLSX.  

### Полный скрипт – собрать всё вместе

```python
def main():
    # Create workbook and obtain the first worksheet
    book, sheet = create_workbook()

    # Apply conditional formatting (set cell background color)
    add_yesterday_rule(sheet)

    # Populate the demo dates (populate dates in excel)
    populate_sample_dates(sheet)

    # Auto‑fit the relevant column (auto fit excel columns)
    auto_fit_columns(sheet)

    # Persist the file
    save_workbook(book)

if __name__ == "__main__":
    main()
```

**Ожидаемый результат**

```
Workbook saved to: YOUR_DIRECTORY/TimePeriodDemo.xlsx
```

Откройте сгенерированный файл в Excel — ячейки `I19:K20` покажут розовый фон для даты, попадающей в «Вчера», а столбец L будет достаточно широким, чтобы отобразить подпись без обрезки.

---

## Почему этот подход работает лучше всего

* **Однопроходный рабочий процесс** — Все операции выполняются над тем же экземпляром `Workbook`, избегая лишних вводов‑выводов.  
* **Условное форматирование** — Использование `FormatConditionType.TIME_PERIOD` позволяет Excel самостоятельно обрабатывать логику дат, что надёжнее, чем писать собственные проверки дат на Python.  
* **Явное стилизование** — Установка `background_color` и `pattern` гарантирует одинаковый визуальный результат во всех версиях Excel.  
* **Автоподгонка после данных** — Ширина столбцов рассчитывается после заполнения всех ячеек, обеспечивая корректный размер.

## Что вам следует изучить дальше?

Следующие руководства охватывают тесно связанные темы, которые развивают техники, продемонстрированные в этом пособии. Каждый ресурс содержит полностью работающие примеры кода с пошаговыми объяснениями, помогающими освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [Create Excel Workbook Python – Full Guide](/cells/english/python/import-and-export/create-excel-workbook-python-full-guide/)
- [Create Excel Workbook Python – Complete Step‑by‑Step Guide](/cells/english/python/import-and-export/create-excel-workbook-python-complete-step-by-step-guide/)
- [Create Excel Workbook Python – Complete Guide with Lambda](/cells/english/python/formulas-and-functions/create-excel-workbook-python-complete-guide-with-lambda/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}