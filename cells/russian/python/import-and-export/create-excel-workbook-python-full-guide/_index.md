---
category: general
date: 2026-06-21
description: Создайте учебник по Python в виде книги Excel, показывающий, как использовать
  функцию MAP и lambda для быстрого преобразования градусов Цельсия в Фаренгейты.
draft: false
keywords:
- create excel workbook python
- convert celsius to fahrenheit
- use map function
- how to use map
- how to use lambda
language: ru
og_description: Создайте Excel‑книгу на Python и научитесь использовать функцию MAP
  с lambda для преобразования градусов Цельсия в Фаренгейты за несколько минут.
og_title: Создание книги Excel в Python – пошаговое руководство
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Create Excel workbook Python tutorial showing how to use MAP function
    and lambda to convert Celsius to Fahrenheit quickly.
  headline: Create Excel Workbook Python – Full Guide
  type: TechArticle
- description: Create Excel workbook Python tutorial showing how to use MAP function
    and lambda to convert Celsius to Fahrenheit quickly.
  name: Create Excel Workbook Python – Full Guide
  steps:
  - name: '**How to use map** for multi‑column transformations, e.g., converting temperatures
      and rounding in one go.'
    text: '**How to use map** for multi‑column transformations, e.g., converting temperatures
      and rounding in one go.'
  - name: '**How to use lambda** to embed conditional logic: `LAMBDA(c, IF(c<0, "below
      freezing", c*9/5+32))`.'
    text: '**How to use lambda** to embed conditional logic: `LAMBDA(c, IF(c<0, "below
      freezing", c*9/5+32))`.'
  - name: 'Saving the workbook to disk: `wb.save("temperatures.xlsx")`.'
    text: 'Saving the workbook to disk: `wb.save("temperatures.xlsx")`.'
  - name: Adding styling (fonts, borders) via Aspose’s rich formatting API.
    text: Adding styling (fonts, borders) via Aspose’s rich formatting API.
  - name: Initialize a workbook.
    text: Initialize a workbook.
  - name: Write raw data.
    text: Write raw data.
  - name: Apply a MAP‑based formula.
    text: Apply a MAP‑based formula.
  - name: Force calculation.
    text: Force calculation.
  - name: Pull the results back into Python.
    text: Pull the results back into Python.
  type: HowTo
- questions:
  - answer: Just extend the range in the `put_value` call and adjust the list comprehension
      range accordingly. The MAP formula will automatically expand if you reference
      a larger range.
    question: What if I have more than four rows?
  - answer: Absolutely. Replace the lambda body with any arithmetic you need, e.g.,
      `LAMBDA(c, c*2)` for a simple doubling operation.
    question: Can I use MAP with other conversions?
  - answer: The library offers a free evaluation mode, but for production use you’ll
      want a proper license to avoid watermarks.
    question: Do I need a license for Aspose.Cells?
  - answer: No, MAP is part of the dynamic array functions introduced in Excel 365.
      If you target legacy Excel, you’d fall back to traditional copy‑down formulas.
    question: Is the MAP function available in older Excel versions?
  type: FAQPage
tags:
- python
- excel
- aspose-cells
- data conversion
title: Создание рабочей книги Excel с помощью Python – Полное руководство
url: /ru/python/import-and-export/create-excel-workbook-python-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание Excel Workbook Python – Полное руководство

Когда‑нибудь задумывались, как **create Excel workbook python**‑style без открытия самого Excel? Возможно, вам нужно мгновенно преобразовать список температур в градусах Цельсия в Фаренгейты, и вы бы предпочли не копировать‑вставлять формулы вручную. В этом руководстве мы решим именно эту задачу: вы увидите, как создать файл Excel, добавить столбец данных в Цельсиях и затем **convert celsius to fahrenheit** с помощью единой элегантной формулы, использующей **MAP function** и **lambda**.

Почему это важно? Автоматизация электронных таблиц экономит время, снижает количество ошибок и упрощает интеграцию Excel в более крупные конвейеры данных. Плюс, с Aspose.Cells for Python вы получаете полный набор возможностей Excel без тяжёлой COM‑интеграции. Готовы? Поехали.

## Что вам понадобится

- Python 3.9+ (любой современный вариант подходит)
- пакет `aspose-cells` установлен (`pip install aspose-cells`)
- Базовое понимание списков Python и функций
- Опыт работы с Excel не требуется; мы позаботимся о создании рабочей книги за вас

Если все пункты отмечены, вы готовы к работе. В противном случае сделайте паузу и установите библиотеку — поверьте, это стоит того.

![create excel workbook python example](excel_workbook.png)

*Текст альтернативного изображения: пример создания Excel workbook python, показывающий заполненную таблицу*

## Шаг 1: Создание Excel Workbook в Python

The first thing we must do is **create excel workbook python** using Aspose.Cells. Think of the workbook as a fresh notebook where each worksheet is a page you can write on.

```python
import aspose.cells as cells

# Initialize a new workbook – this is our blank Excel file
wb = cells.Workbook()

# Grab the first worksheet (index 0) to start populating data
ws = wb.worksheets[0]
```

*Почему это важно*: Инстанцирование `Workbook()` даёт вам представление файла `.xlsx` в памяти. Пока нет операций ввода‑вывода на диск, что ускоряет процесс.

## Шаг 2: Заполнение столбца A температурами в Цельсиях

Now that we have a sheet, let’s put some Celsius values into column **A**. We’ll use the `put_value` method, which accepts a Python list and writes it straight into the cell range.

```python
# Write a list of Celsius temperatures into cells A1:A4
ws.cells["A1:A4"].put_value([0, 20, 100, -10])
```

*Полезный совет*: Строка диапазона `"A1:A4"` гибка — если позже расширите список, просто скорректируйте диапазон или используйте динамический адрес.

## Шаг 3: Применить MAP с LAMBDA для преобразования каждой температуры Цельсия в Фаренгейты

Here’s where the magic happens. The **MAP function** (new in Excel 365) lets you apply a **lambda** to every element of an array. In our case, the array is `A1:A4`, and the lambda performs the classic conversion `c * 9/5 + 32`.

```python
# Set the formula in B1 that maps each Celsius value to Fahrenheit
ws.cells["B1"].formula = "=MAP(A1:A4, LAMBDA(c, c*9/5 + 32))"
```

*Как это работает*:  
- `MAP(array, LAMBDA(parameter, expression))` перебирает `array`.  
- `c` — это заполнитель для каждой температуры в Цельсиях.  
- Выражение `c*9/5 + 32` возвращает эквивалент в Фаренгейтах.

Если вы новичок в **how to use map** в Excel, представьте это как встроенную функцию Python `map()`, но в виде формулы листа. Это устраняет необходимость вручную протягивать формулы вниз.

## Шаг 4: Вычислить формулу, чтобы результаты материализовались

Aspose.Cells не вычисляет формулы автоматически, если вы явно не укажете. Вызов `calculate_formula()` заставляет движок посчитать результат MAP и сохранить значения в столбце **B**.

```python
# Force calculation – this writes the computed Fahrenheit values into the cells
wb.calculate_formula()
```

*Особый случай*: Если позже вы измените столбец с Цельсиями, потребуется снова вызвать `calculate_formula()`, либо установить `calc_mode` рабочей книги в автоматический режим.

## Шаг 5: Получить и вывести значения Фаренгейтов из столбца B

Finally, let’s pull the computed numbers back into Python and print them. This demonstrates **how to use lambda** results programmatically.

```python
# Extract the Fahrenheit values from B1:B4 into a Python list
fahrenheit = [ws.cells[f"B{i}"].value for i in range(1, 5)]
print(fahrenheit)
```

**Ожидаемый вывод**

```
[32.0, 68.0, 212.0, 14.0]
```

Если вы видите эти числа, поздравляем — вы успешно **create excel workbook python**‑style, заполнили её и использовали **use map function** вместе с **lambda** для **convert celsius to fahrenheit**.

## Часто задаваемые вопросы и подводные камни

- **Что если у меня больше четырёх строк?**  
  Просто расширьте диапазон в вызове `put_value` и скорректируйте диапазон в генераторе списка. Формула MAP автоматически расширится, если вы укажете больший диапазон.

- **Можно ли использовать MAP для других преобразований?**  
  Конечно. Замените тело lambda любой нужной вам арифметикой, например `LAMBDA(c, c*2)` для простого удвоения.

- **Нужна ли лицензия для Aspose.Cells?**  
  Библиотека предлагает бесплатный режим оценки, но для продакшн‑использования потребуется полноценная лицензия, чтобы избавиться от водяных знаков.

- **Доступна ли функция MAP в более старых версиях Excel?**  
  Нет, MAP входит в набор динамических массивных функций, появившихся в Excel 365. Если вы ориентируетесь на устаревшие версии Excel, придётся использовать традиционные формулы с копированием вниз.

## Расширение примера – дальнейшие шаги

Теперь, когда основной процесс ясен, вы можете поэкспериментировать с:

1. **How to use map** для преобразований нескольких столбцов одновременно, например, преобразование температур и их округление в одном шаге.  
2. **How to use lambda** для внедрения условной логики: `LAMBDA(c, IF(c<0, "below freezing", c*9/5+32))`.  
3. Сохранением рабочей книги на диск: `wb.save("temperatures.xlsx")`.  
4. Добавлением стилей (шрифты, границы) через богатый API форматирования Aspose.

Каждый из этих пунктов опирается на ту же основу, которую мы только что построили, позволяя держать код лаконичным и одновременно открывая мощные возможности автоматизации электронных таблиц.

## Заключение

Мы прошли весь процесс **create excel workbook python** с нуля, заполнили её данными в Цельсиях и затем **convert celsius to fahrenheit** с помощью **MAP function** и **lambda**‑выражения. Шаги были:

1. Инициализировать рабочую книгу.  
2. Записать исходные данные.  
3. Применить формулу на основе MAP.  
4. Принудительно выполнить расчёт.  
5. Получить результаты обратно в Python.

С этим рецептом в вашем арсенале автоматизация Excel‑ориентированных конвейеров данных становится простой задачей. Не стесняйтесь менять lambda, цепочкой вызывать несколько MAP, или даже внедрять рабочую книгу в веб‑сервис. Возможности безграничны.

Есть другая конверсия в уме? Оставьте комментарий, и давайте исследовать вместе. Счастливого кодинга!

## Что изучать дальше?

The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Как создать и сохранить Excel Workbook в формате SVG с помощью Aspose.Cells для Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)
- [Как создать и экспортировать Excel в HTML с использованием Aspose.Cells Java | Руководство по операциям с рабочей книгой](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)
- [Как создать и сохранить Excel Workbook в формате ODS с помощью Aspose.Cells для .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}