---
category: general
date: 2026-11-16
description: Создайте условное форматирование в Excel с помощью Python. Узнайте, как
  добавить диапазон условного форматирования, выделить даты и программно создать книгу.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create conditional formatting
- create excel workbook python
- how to highlight dates
- add conditional formatting range
- add conditional formatting python
language: ru
lastmod: 2026-11-16
og_description: Создайте условное форматирование в Excel с помощью Python. Этот учебник
  показывает, как добавить диапазон условного форматирования, выделить даты и создать
  рабочую книгу.
og_image_alt: Screenshot of Excel sheet with conditional formatting applied using
  Python
og_title: Создайте условное форматирование в Excel с помощью Python — пошаговое руководство
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Create conditional formatting in Excel using Python. Learn to add a
    conditional formatting range, highlight dates, and build a workbook programmatically.
  headline: How to create conditional formatting in Excel with Python
  type: TechArticle
tags:
- Excel
- Python
- Aspose.Cells
- Conditional Formatting
title: Как создать условное форматирование в Excel с помощью Python
url: /ru/python/formatting/how-to-create-conditional-formatting-in-excel-with-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как создать условное форматирование в Excel с помощью Python

Если вам нужно **создать условное форматирование** в файле Excel, работая в Python, это руководство покажет, как это сделать. Вы научитесь **создавать excel workbook python**‑стиль, определять диапазон форматирования и выделять даты, не покидая IDE.

Условное форматирование позволяет визуально помечать ячейки, соответствующие определённым критериям — идеально для панелей мониторинга, отчётов или листов проверки данных. К концу этого урока у вас будет полностью функционирующая рабочая книга, которая окрашивает ячейки с датой «Вчера» в розовый, а остальные диапазоны оставит зелёными.

## Что вы получите

* Создадите новую рабочую книгу с нуля.  
* Добавите коллекцию условного форматирования для конкретного блока ячеек.  
* Примените правило **TIME_PERIOD**, которое выделяет даты (сценарий «как выделить даты»).  
* Сохраните файл как рабочую книгу XLSX, готовую к дальнейшей обработке.

**Требования**  
* Python 3.8+  
* Пакет `aspose-cells` для Python (`pip install aspose-cells`)  
* Базовое знакомство с модулем Python `datetime`  

---

## Как создать условное форматирование в Python

Первый шаг — настроить рабочую книгу и лист, которые будут содержать правила форматирования.

```python
# Step 1: Import required classes and create a new workbook
from aspose.cells import Workbook, FormatConditionType, BackgroundType, TimePeriodType, SaveFormat
from aspose.pydrawing import Color
from datetime import datetime

# Instantiate a blank workbook and grab the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

# Optional: auto‑fit column 12 (L) to make the output readable
worksheet.auto_fit_column(12)
```

**Почему это важно** — `Workbook` является точкой входа для всех операций с Excel. Программное создание рабочей книги заменяет ручной шаг «Файл → Новый», позволяя автоматизировать конвейеры отчётов.

---

## Подготовка коллекции условного форматирования — добавление диапазона

Далее мы определяем блок ячеек, который получит правило. В этом примере диапазон **I19:K20**.

```python
# Step 2: Create a conditional‑format collection for the target range
conds = worksheet.conditional_formattings.add("I19:K20")

# Apply a base style (green background) that will show when no rule matches
conds[0].style.background_color = Color.medium_sea_green
conds[0].style.pattern = BackgroundType.SOLID
```

**Пояснение** — `conditional_formattings.add` регистрирует новую коллекцию, привязанную к строке адреса. Первое условие (`conds[0]`) работает как «стиль по умолчанию»; последующее правило переопределит его, когда выполнится его критерий.

---

## Добавление условия TIME_PERIOD — как выделить даты

Теперь добавляем реальную логику, которая определяет даты «Вчера» и закрашивает их в розовый.

```python
# Step 3: Add a TIME_PERIOD condition that highlights cells dated “Yesterday”
idx = conds.add_condition(FormatConditionType.TIME_PERIOD)   # returns the new index
condition = conds[idx]

# Define the visual style for cells that satisfy the condition
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID

# Set the rule to the built‑in YESTERDAY period
condition.time_period = TimePeriodType.YESTERDAY
```

**Зачем использовать TIME_PERIOD?** — Aspose.Cells предоставляет встроенные перечисления, такие как `YESTERDAY`, `TODAY` и `LAST_WEEK`. Они сравнивают значение даты в ячейке с текущей системной датой, избавляя от необходимости писать пользовательские формулы.

---

## Заполнение примерными данными — демонстрация правила

Чтобы увидеть форматирование в действии, вставляем дату, соответствующую правилу, и другую, не соответствующую.

```python
# Step 4: Populate sample dates so the rule can be seen

# Cell I19 gets a date that is “yesterday” relative to 2008‑07‑31
cell_i19 = worksheet.cells.get("I19")
cell_i19.put_value(datetime(2008, 7, 30))  # yesterday for the example
style = cell_i19.get_style()
style.number = 30                         # full date format (e.g., 7/30/2008)
cell_i19.set_style(style)

# Cell K20 gets a later date – it should stay green
cell_k20 = worksheet.cells.get("K20")
cell_k20.put_value(datetime(2008, 8, 3))   # a future date
style = cell_k20.get_style()
style.number = 30
cell_k20.set_style(style)

# Optional label for clarity
worksheet.cells.get("I20").put_value("Yesterday")
```

**Примечание о граничных случаях** — Правило `TIME_PERIOD` работает только с *реальными* датами. Если ячейка содержит текст (например, «N/A»), правило игнорируется, предотвращая неожиданные изменения цвета.

---

## Сохранение рабочей книги — add conditional formatting python

Наконец, записываем рабочую книгу на диск. Файл можно открыть в любой программе для работы с таблицами, чтобы проверить цвета.

```python
# Step 5: Save the workbook
output_path = "TimePeriodExample.out.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to {output_path}")
```

**Ожидаемый результат**  

| I19 (green → pink) | J19 (green) | K19 (green) |
|--------------------|------------|------------|
| 7/30/2008 (yesterday) | – | – |
| **I20**: “Yesterday” label | – | – |
| I21‑K21 (green)    | – | – |

Ячейка **I19** отображается с розовым фоном, потому что её дата соответствует периоду «Вчера», тогда как **K20** остаётся зелёной.

---

## Часто задаваемые вопросы и практические советы

* **Можно ли использовать пользовательский диапазон дат вместо встроенного периода?**  
  Да. Замените `condition.time_period` на `condition.formula1 = "TODAY()-1"` и установите `condition.type = FormatConditionType.FORMULA`.

* **Что делать, если моя рабочая книга уже содержит данные?**  
  Используйте `worksheet.cells.import_data` для массовой загрузки данных перед добавлением коллекции условного форматирования.

* **Производительность при работе с большими листами?**  
  Добавление большого количества условий может замедлить рендеринг. Группируйте ячейки с одинаковым правилом в один диапазон (например, “A1:C1000”), чтобы уменьшить количество условий.

* **Кроссплатформенная совместимость?**  
  Сгенерированный файл XLSX соответствует стандарту Office Open XML, поэтому работает в приложениях для Windows, macOS и Linux.

---

## Заключение

Теперь вы знаете, как **создать условное форматирование** в рабочей книге Excel с помощью Python. В руководстве рассмотрены создание книги, определение **add conditional formatting range**, применение правила **how to highlight dates** и сохранение файла — всё это с использованием подхода **add conditional formatting python**, предоставляемого Aspose.Cells.

Дальше вы можете:

* Расширить набор правил другими значениями `TimePeriodType` (например, `TODAY`, `LAST_MONTH`).  
* Скомбинировать несколько условий для одного диапазона, чтобы получить более богатые визуальные подсказки.  
* Интегрировать этот процесс в автоматические конвейеры отчётности или веб‑сервисы.

Приятного кодинга, экспериментируйте с разными цветами, диапазонами и логикой дат, чтобы адаптировать их под ваши отчётные задачи!

## Что изучать дальше?


Следующие руководства охватывают тесно связанные темы, которые развивают техники, продемонстрированные в этом пособии. Каждый ресурс включает полностью рабочие примеры кода с пошаговыми объяснениями, помогающими освоить дополнительные возможности API и изучить альтернативные подходы реализации в ваших проектах.

- [Create Excel workbook Python date conditional formatting](/cells/english/python/formatting/create-excel-workbook-python-date-conditional-formatting/)
- [How to apply time period conditional formatting in Excel using Python](/cells/english/python/formatting/how-to-apply-time-period-conditional-formatting-in-excel-usi/)
- [Create Excel Workbook Python – Full Guide to Styling & Conditional Formatting](/cells/english/python/formatting/create-excel-workbook-python-full-guide-to-styling-condition/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}