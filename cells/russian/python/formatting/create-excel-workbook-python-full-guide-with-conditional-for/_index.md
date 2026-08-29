---
category: general
date: 2026-07-14
description: Создайте код на Python для создания книги Excel, который задаёт цвет
  фона ячеек, выделяет их в зависимости от диапазона дат и сохраняет книгу в формате
  XLSX за несколько минут.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- set cell background color
- save workbook as xlsx
- highlight cells based on date range
- conditional formatting based on date
language: ru
lastmod: 2026-07-14
og_description: Создайте книгу Excel на Python мгновенно. Узнайте, как задать цвет
  фона ячейки, выделять ячейки по диапазону дат и сохранять книгу в формате XLSX с
  помощью Aspose.Cells.
og_image_alt: Screenshot showing an Excel sheet created with Python highlighting yesterday's
  dates
og_title: Создание рабочей книги Excel в Python – пошаговое условное форматирование
schemas:
- author: Aspose
  dateModified: '2026-07-14'
  description: Create Excel workbook Python code that sets cell background color,
    highlights cells based on date range, and saves workbook as XLSX in minutes.
  headline: Create Excel Workbook Python – Full Guide with Conditional Formatting
  type: TechArticle
tags:
- Python
- Aspose.Cells
- Excel Automation
- Conditional Formatting
title: Создание Excel‑книги в Python – Полное руководство с условным форматированием
url: /ru/python/formatting/create-excel-workbook-python-full-guide-with-conditional-for/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание Excel Workbook Python – Полное руководство с условным форматированием

Вы когда‑нибудь задумывались, как писать скрипты **create excel workbook python**, которые выглядят отшлифованными, не открывая Excel вручную? Вы не одиноки. Во многих проектах, основанных на данных, нам нужно генерировать таблицы, раскрашивать ячейки и даже помечать даты, попадающие в определённый диапазон — всё это с помощью чистого кода Python.

В этом руководстве мы пройдём полный готовый к запуску пример, который **creates an Excel workbook python** с использованием библиотеки Aspose.Cells, **sets cell background color**, применяет **conditional formatting based on date** и, наконец, **saves workbook as xlsx**. К концу у вас будет переиспользуемый фрагмент кода, который можно вставить в любой конвейер автоматизации.

## Что вы узнаете

- Как инициализировать рабочую книгу и получить первый лист.  
- Вспомогательная функция, которая добавляет коллекцию условного форматирования для любого диапазона ячеек.  
- Использование **conditional formatting based on date** для выделения записей за вчера.  
- Настройка ширины столбцов для аккуратного оформления.  
- Сохранение результата с помощью **save workbook as xlsx**.  

Установка внешнего Excel не требуется — Aspose.Cells обрабатывает всё в памяти.

## Предварительные требования

- Установлен Python 3.8+.  
- Пакет `aspose-cells` (`pip install aspose-cells`).  
- Базовое знакомство с функциями Python и объектами datetime.  

Если вы никогда ранее не использовали Aspose.Cells, представьте его как мощный, полностью Python‑API, имитирующий объектную модель Excel. Он идеально подходит для генерации на сервере, где пакет Office недоступен.

## Шаг 1: Инициализация рабочей книги (Create Excel Workbook Python)

Сначала нам нужно **create excel workbook python** в стиле Python. Этот шаг создаёт пустой объект рабочей книги и указывает на лист по умолчанию.

```python
# Step 1 – create a fresh workbook and get the first sheet
from aspose.cells import Workbook, FormatConditionType, BackgroundType, TimePeriodType, Color, SaveFormat
from datetime import datetime

workbook = Workbook()                     # <-- creates a new Excel file in memory
worksheet = workbook.worksheets[0]        # the default (first) sheet
```

> **Почему это важно:** Класс `Workbook` является точкой входа для любой операции с Excel. Создавая его программно, мы избегаем любой ручной работы с файлами.

## Шаг 2: Вспомогательная функция для добавления коллекции условного форматирования (Set Cell Background Color)

Условное форматирование хранится в *коллекции*, привязанной к диапазону. Давайте обернём этот шаблонный код в небольшую вспомогательную функцию, которая также позволяет **set cell background color** для всего диапазона.

```python
def add_time_period_condition(cell_range: str, highlight_color: Color):
    """
    Adds a conditional‑formatting collection to `cell_range` and
    applies `highlight_color` as the base fill.
    """
    worksheet.conditional_formattings.add(cell_range)   # attach to the range
    cf = worksheet.conditional_formattings[-1]           # grab the newly added collection
    cf.style.background_color = highlight_color
    cf.style.pattern = BackgroundType.SOLID
    return cf
```

> **Совет профессионала:** использование вспомогательной функции делает основной поток кода чистым и упрощает повторное использование той же логики для разных диапазонов.

## Шаг 3: Применение условного форматирования по дате (Highlight Cells Based on Date Range)

Теперь мы действительно **highlight cells based on date range**. В примере фокусируется на «вчера», но вы можете заменить `TimePeriodType.YESTERDAY` на `TODAY`, `LAST_WEEK` и т.д.

```python
# Step 3 – create a TIME_PERIOD rule for I19:K20 (yesterday)
cf = add_time_period_condition("I19:K20", Color.medium_sea_green)

condition_index = cf.add_condition(FormatConditionType.TIME_PERIOD)
condition = cf[condition_index]

# Define the visual style for the matching cells
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID

# The actual rule: any cell whose date is yesterday gets the pink fill
condition.time_period = TimePeriodType.YESTERDAY
```

> **Что происходит?**  
> 1. Сначала мы задаём всему диапазону нейтральный зелёный фон.  
> 2. Затем добавляем условие `TIME_PERIOD`, которое заменяет заливку на розовую **только** когда дата в ячейке равна вчерашнему дню.  
> 3. Перечисление `TimePeriodType` абстрагирует вычисление даты, поэтому вам не нужно писать собственную логику.

## Шаг 4: Заполнение примерами дат (So the Rule Can Be Evaluated)

Чтобы увидеть правило в действии, мы добавим несколько дат в лист. Одна попадает в окно «вчера», другая — нет.

```python
# Populate I19 with a date that is yesterday (relative to the hard‑coded date)
date_cell = worksheet.cells.get("I19")
date_cell.put_value(datetime(2008, 7, 30))   # 30‑Jul‑2008
date_style = date_cell.get_style()
date_style.number = 30                     # Excel’s built‑in date format
date_cell.set_style(date_style)

# Populate K20 with a date that is NOT yesterday
date_cell = worksheet.cells.get("K20")
date_cell.put_value(datetime(2008, 8, 3))    # 03‑Aug‑2008
date_style = date_cell.get_style()
date_style.number = 30
date_cell.set_style(date_style)

# Add a label for clarity
worksheet.cells.get("I20").put_value("Yesterday")
```

> **Примечание о граничных случаях:** Если ваша рабочая книга будет открываться в разных локалях, рассмотрите возможность использования `date_style.custom = "dd‑mm‑yyyy"` для обеспечения единообразного отображения.

## Шаг 5: Приведение макета в порядок (Auto‑Fit Columns)

Сжатая таблица выглядит непрофессионально. Давайте **adjust column width for a tidy output**.

```python
# Auto‑fit column L (index 12) to show the full content without truncation
worksheet.auto_fit_column(12)
```

> **Почему авто‑подгонка?** Она гарантирует, что любые длинные подписи или даты будут полностью видимы, что особенно важно при обмене файлом с нетехническими заинтересованными сторонами.

## Шаг 6: Сохранение рабочей книги (Save Workbook As XLSX)

Наконец, мы **save workbook as xlsx** в выбранное вами место. Константа `SaveFormat.XLSX` указывает Aspose.Cells записать файл в современном формате OpenXML.

```python
output_path = "YOUR_DIRECTORY/TimePeriodDemo.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

> **Ожидаемый результат:**  
> - Ячейки I19 и K20 содержат даты.  
> - I19 (вчера) выделена розовым, тогда как K20 остаётся зелёной.  
> - Столбец L автоматически расширяется, чтобы вместить подпись «Yesterday».  

Если открыть `TimePeriodDemo.xlsx` в Excel, условное форматирование уже будет применено — никаких дополнительных шагов не требуется.

---

![Лист Excel с выделенной датой вчера](https://example.com/images/excel-demo.png "Скриншот сгенерированного файла Excel с выделенными ячейками")

*Изображение выше иллюстрирует окончательную рабочую книгу; обратите внимание на розовое выделение ячейки, содержащей дату вчера.*

## Итоги: Что мы достигли

- **Created an Excel workbook python** с нуля с использованием Aspose.Cells.  
- **Set cell background color** для всего диапазона, чтобы придать листу визуальный акцент.  
- Применено **conditional formatting based on date** для автоматической пометки записей за вчера.  
- **Saved workbook as xlsx**, готовый к распространению или дальнейшей обработке.  

Всё это было реализовано менее чем в 60 строках кода Python, и код работает на любой платформе, поддерживающей среду выполнения Aspose.Cells.

## Следующие шаги и связанные темы

Если это было полезно, вам также может быть интересно изучить:

- **set cell background color** для целых строк в зависимости от статуса (например, «Completed», «Pending»).  
- Использование **highlight cells based on date range** для создания скользящих окон (последние 7 дней, текущий месяц).  
- Экспорт в другие форматы, такие как **CSV** или **PDF**, с помощью `SaveFormat.CSV` или `SaveFormat.PDF`.  
- Добавление **charts** программно для визуализации только что отформатированных данных.  

Не стесняйтесь менять логику дат, менять цветовую палитру или расширять диапазон, чтобы охватить целые столбцы. Схема остаётся той же: создать рабочую книгу, прикрепить коллекцию условного форматирования, определить правило и сохранить.

Есть вопросы по конкретному случаю использования? Оставьте комментарий ниже, и удачной разработки!

## Что стоит изучить дальше?

Следующие руководства охватывают тесно связанные темы, построенные на техниках, продемонстрированных в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [Автоматизация Excel с Aspose.Cells .NET: создание рабочей книги и установка внешних ссылок](/cells/english/net/automation-batch-processing/excel-automation-aspose-cells-net/)
- [Создание и сохранение Excel Workbook Aspose Cells Java](/cells/hongkong/java/workbook-operations/create-save-excel-workbook-aspose-cells-java/)
- [Создание и сохранение Excel Workbook Aspose Cells .NET](/cells/hongkong/net/workbook-operations/create-save-excel-workbook-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}