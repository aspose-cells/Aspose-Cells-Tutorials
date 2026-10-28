---
category: general
date: 2026-08-01
description: Создайте Excel‑книгу на Python с помощью Aspose.Cells — изучите автоматическую
  подгонку ширины столбцов, форматирование ячеек по дате, установку формата даты в
  ячейке и применение условного форматирования.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- auto fit excel column
- format cells by date
- set cell date format
- aspose cells conditional formatting
language: ru
lastmod: 2026-08-01
og_description: Создайте книгу Excel на Python мгновенно. Следуйте этому руководству,
  чтобы автоматически подгонять ширину столбцов Excel, форматировать ячейки по дате,
  установить формат даты ячейки и освоить условное форматирование Aspose Cells.
og_image_alt: Screenshot showing a Python script that creates an Excel workbook using
  Aspose.Cells
og_title: Создание Excel‑книги в Python – пошаговое руководство с Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-08-01'
  description: Create Excel workbook python using Aspose.Cells – learn auto fit excel
    column, format cells by date, set cell date format and apply conditional formatting.
  headline: Create Excel Workbook Python – Full Guide with Aspose.Cells
  type: TechArticle
tags:
- Aspose Cells
- Python
- Excel automation
- Conditional Formatting
- Date handling
title: Создание Excel‑рабочей книги на Python – Полное руководство с Aspose.Cells
url: /ru/python/formatting/create-excel-workbook-python-full-guide-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание Excel Workbook в Python – Полное руководство с Aspose.Cells

Когда‑то задумывались, как **create Excel workbook python** скрипты, которые выглядят профессионально, без необходимости открывать Excel вручную? Вы не одиноки. Будь то построение дашборда отчётов или автоматизация ежедневных выгрузок данных, возможность генерировать файл Excel из Python меняет правила игры.

В этом руководстве мы пройдём через полностью готовый, исполняемый пример, который не только создаёт книгу, но и демонстрирует **auto fit excel column**, **format cells by date**, **set cell date format**, а также применение **aspose cells conditional formatting**. К концу вы получите автономный скрипт, который можно вставить в любой проект.

> **Pro tip:** Aspose.Cells for Python via .NET позволяет работать с файлами Excel без зависимости от COM, что делает его идеальным для Linux‑контейнеров или CI‑конвейеров.

## Что вам понадобится

- **Python 3.8+** (код работает на любой современной версии)  
- **Aspose.Cells for Python via .NET** – установить с помощью `pip install aspose-cells`  
- Папка, в которую можно записывать файлы (мы назовём её `YOUR_DIRECTORY`)  
- Базовое понимание функций и объектов Python (глубокие знания Excel не требуются)  

Если всё уже готово — отлично, приступаем.

## Шаг 1: Create Excel Workbook Python – Инициализация Workbook

Первое, что мы делаем, — создаём новый объект workbook. Представьте его как чистый холст, на котором каждая последующая операция рисует новый элемент.

```python
from aspose.cells import Workbook, SaveFormat, FormatConditionType, BackgroundType, TimePeriodType
from aspose.pydrawing import Color
from datetime import datetime
import os

# Create a new workbook and grab the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]
```

> **Почему это важно:** `Workbook()` создаёт представление файла `.xlsx` в памяти. Обращаясь к `worksheets[0]`, мы получаем лист по умолчанию, готовый для данных и форматирования.

## Шаг 2: Определение целевого диапазона и базового цвета – Подготовка к условному форматированию

Прежде чем добавить любую условную логику, нам нужен диапазон, который будет содержать правило. Диапазон `I19:K20` выбран произвольно, но достаточно велик, чтобы продемонстрировать несколько ячеек.

```python
# Add a conditional formatting collection to the range and set a base colour
conds = worksheet.conditional_formattings.add("I19:K20", Color.medium_sea_green)
```

Метод `add` одновременно создаёт объект форматирования и задаёт ему фон по умолчанию, чтобы позже правило выделялось.

## Шаг 3: Aspose Cells Conditional Formatting – Применение правила TIME_PERIOD для YESTERDAY

Теперь переходим к основной части демо: условию **TIME_PERIOD**, которое выделяет ячейки с датой вчерашнего дня.

```python
# Insert a TIME_PERIOD condition for YESTERDAY
condition_index = conds.add_condition(FormatConditionType.TIME_PERIOD)
condition = conds[condition_index]

# Configure the rule – yesterday, pink background, solid fill
condition.time_period = TimePeriodType.YESTERDAY
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID
```

> **Объяснение:** `FormatConditionType.TIME_PERIOD` сообщает Aspose, что правило основано на дате. Установив `time_period` в `YESTERDAY`, движок автоматически сравнивает значение каждой ячейки с предыдущим календарным днём.

## Шаг 4: Заполнение примерными датами – Установка формата даты ячейки и проверка правила

Чтобы увидеть правило в действии, нужны реальные даты. Мы также **set cell date format**, чтобы значения отображались как читаемые даты.

```python
# Cell I19 – a date that falls on “yesterday”
cell_i19 = worksheet.cells.get("I19")
cell_i19.put_value(datetime(2008, 7, 30))          # July 30, 2008 is “yesterday” for demo purposes
style_i19 = cell_i19.get_style()
style_i19.number = 30          # 30 = built‑in Excel date format (e.g., mm/dd/yyyy)
cell_i19.set_style(style_i19)

# Cell K20 – a date outside the period (no formatting applied)
cell_k20 = worksheet.cells.get("K20")
cell_k20.put_value(datetime(2008, 8, 3))
style_k20 = cell_k20.get_style()
style_k20.number = 30
cell_k20.set_style(style_k20)
```

Обратите внимание, что мы используем один и тот же номер **format cells by date** (`30`) для обеих ячеек. Это гарантирует одинаковое отображение дат независимо от локали системы.

## Шаг 5: Добавление описательной метки – Делаем лист самодокументируемым

Небольшая метка помогает каждому, кто открывает файл, понять, что означают раскрашенные ячейки.

```python
worksheet.cells.get("I20").put_value("Yesterday")
```

## Шаг 6: Auto Fit Excel Column – Автоматическая подгонка ширины столбцов

При программной генерации данных ширина столбцов часто остаётся узкой по умолчанию. Метод **auto fit excel column** расширяет их ровно настолько, насколько это необходимо для отображения содержимого.

```python
# Auto‑fit the 12th column (which corresponds to column L) so the label is fully visible
worksheet.auto_fit_column(12)
```

> **Почему столбец 12?** В нулевой индексации столбец `12` соответствует Excel‑столбцу `L`. Измените индекс, если меняете расположение.

## Шаг 7: Сохранение Workbook – Экспорт в реальный файл

Наконец, сохраняем всё на диск. Флаг `SaveFormat.XLSX` гарантирует современный, zip‑основанный формат книги.

```python
output_file = os.path.join("YOUR_DIRECTORY", "TimePeriodDemo.out.xlsx")
workbook.save(output_file, SaveFormat.XLSX)
print(f"Workbook saved to {output_file}")
```

### Ожидаемый результат

Откройте `TimePeriodDemo.out.xlsx` в Excel (или любом просмотрщике) и вы увидите:

- Ячейка **I19** выделена **розовым**, потому что её дата соответствует «вчера».  
- Ячейка **K20** остаётся без изменений, демонстрируя, что условие корректно игнорирует даты вне указанного периода.  
- Столбец **L** автоматически подогнан, поэтому метка «Yesterday» не обрезается.

![Create Excel workbook python example](/images/create_excel_workbook_python.png){: .center-image alt="Пример создания Excel workbook в Python с условным форматированием даты вчерашнего дня"}

## Распространённые варианты и граничные случаи

| Ситуация | Как изменить |
|-----------|---------------|
| **Другой диапазон дат** | Измените `condition.time_period` на `TimePeriodType.TODAY`, `TimePeriodType.LAST_7_DAYS` и т.д. |
| **Несколько условий** | Вызовите `conds.add_condition()` ещё раз и настройте новый `FormatConditionType` (например, `FORMAT_CONDITION_TYPE.EXPRESSION`). |
| **Пользовательский формат даты** | Используйте `style_i19.number = 14` для `mm-dd-yy` или задайте строку формата через `style_i19.custom = "dd-mmm-yyyy"`. |
| **Большие листы** | Оберните вызов `auto_fit_column` в блок `try/except`, чтобы избежать падения производительности на огромных файлах. |
| **Запуск в безголовом CI** | UI не требуется; Aspose полностью работает в памяти, так что файл можно генерировать в Docker‑контейнере без установленного Excel. |

## Итоги – Что мы рассмотрели

- **Create Excel workbook python** с нуля с помощью Aspose.Cells.  
- **Auto fit excel column** для аккуратного вывода.  
- **Format cells by date** и **set cell date format** для единообразного отображения.  
- Применение **aspose cells conditional formatting** с типом `TIME_PERIOD`.

Всё это укладывается в один простой скрипт, который можно адаптировать под счета, ежедневные логи или любые ситуации, где даты управляют визуальными подсказками.

## Следующие шаги

Если вы освоили основы, попробуйте изучить:

- **Data bars, color scales, and icon sets** для более богатого условного стилизования.  
- **PivotTable generation** через `worksheet.pivot_tables.add()`.  
- **Экспорт в PDF** с помощью `workbook.save("report.pdf", SaveFormat.PDF)`.  

Каждая из этих тем опирается на те же фундаментальные концепции, что и в этом руководстве, так что вы будете чувствовать себя как дома.

---

*Счастливого кодинга! Если возникнут проблемы, оставьте комментарий ниже или обратитесь к документации Aspose.Cells for Python для более глубокого изучения.*


## Что изучать дальше?


Следующие руководства охватывают тесно связанные темы, расширяющие техники, продемонстрированные в этом гиде. Каждый ресурс включает полностью рабочие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы в собственных проектах.

- [Auto-Fit Rows & Columns in Excel using Aspose.Cells Java for Seamless Workbook Management](/cells/english/java/range-management/aspose-cells-java-auto-fit-rows-columns/)
- [Create an Excel Workbook using Aspose.Cells in Java&#58; A Step-by-Step Guide](/cells/english/java/getting-started/create-excel-workbook-aspose-cells-java/)
- [Automate Excel Column Widths&#58; Auto-Fit Columns using Aspose.Cells for .NET](/cells/english/net/range-management/excel-automation-auto-fit-columns-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}