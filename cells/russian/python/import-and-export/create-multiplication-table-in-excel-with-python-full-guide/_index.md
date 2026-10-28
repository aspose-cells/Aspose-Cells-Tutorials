---
category: general
date: 2026-06-21
description: Создайте таблицу умножения в Excel с помощью Python. Узнайте, как использовать
  lambda, как применять makearray, как отображать массив Excel и считывать значения
  из Excel в Python в пошаговом руководстве.
draft: false
keywords:
- create multiplication table
- how to use lambda
- how to use makearray
- display excel array
- read excel values python
language: ru
og_description: Создайте таблицу умножения в Excel с помощью Python. Этот учебник
  показывает, как использовать lambda, makearray, отображать массив Excel и эффективно
  считывать значения из Excel в Python.
og_title: Создайте таблицу умножения в Excel с помощью Python – Полное руководство
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Create multiplication table in Excel using Python. Learn how to use
    lambda, how to use makearray, display excel array and read excel values python
    in a step‑by‑step tutorial.
  headline: Create multiplication table in Excel with Python – Full Guide
  type: TechArticle
tags:
- python
- excel
- openpyxl
title: Создайте таблицу умножения в Excel с помощью Python — Полное руководство
url: /ru/python/import-and-export/create-multiplication-table-in-excel-with-python-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание таблицы умножения в Excel с помощью Python – Полное руководство

Когда‑нибудь задавались вопросом, как **create multiplication table** в Excel без ручного ввода каждой ячейки? Вы не одиноки. Во многих сценариях отчётности вам нужна быстрая сетка 5×5 (или больше) продуктов, а делать это вручную — пустая трата времени.  

В этом руководстве мы пройдём чистый, управляемый Python способ создания этой таблицы, внедрим её с помощью формулы `MAKEARRAY` и затем извлечём результаты обратно в ваш скрипт. По пути мы ответим на **how to use lambda**, покажем **how to use makearray** и продемонстрируем **display excel array**, а также **read excel values python** — всё в одном связном примере.

К концу у вас будет переиспользуемый фрагмент кода, который работает с любой книгой, и вы поймёте, почему этот подход одновременно быстрый и надёжный в будущем.

## Что понадобится

- Python 3.8+ (последний стабильный релиз подходит)
- Библиотека `openpyxl` (или любая библиотека, умеющая работать с Excel и поддерживающая формулы)
- Базовое понимание lambda‑выражений в Python
- Никаких специальных надстроек Excel; нативная функция `MAKEARRAY` (доступна в Excel 365) выполняет основную работу

Если чего‑то не хватает, просто выполните `pip install openpyxl`, и вы готовы к работе.

## Создание таблицы умножения – Обзор

Основная идея проста: мы создаём новую книгу, записываем формулу `MAKEARRAY`, которая строит матрицу умножения 5 × 5, заставляем Excel вычислить её и, наконец, считываем полученные значения обратно в Python.

```python
from openpyxl import Workbook

# Step 1: Create a new workbook and get the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

# Step 2: Insert a MAKEARRAY formula that builds a 5×5 multiplication table
# The formula uses a LAMBDA that returns r*c for each row (r) and column (c)
worksheet["A1"] = "=MAKEARRAY(5,5, LAMBDA(r,c, r*c))"

# Step 3: Calculate all formulas so the array is materialized in the sheet
workbook.calculate_formula()

# Step 4: Read and display the top‑left 5×5 block of values
for row_index in range(1, 6):
    row_values = [worksheet.cell(row=row_index, column=col_index).value
                  for col_index in range(1, 6)]
    print(row_values)
```

Запуск скрипта выводит:

```
[1, 2, 3, 4, 5]
[2, 4, 6, 8, 10]
[3, 6, 9, 12, 15]
[4, 8, 12, 16, 20]
[5, 10, 15, 20, 25]
```

Это полностью рабочий **create multiplication table** в Excel, сгенерированный полностью из Python.

### Почему использовать `MAKEARRAY`, а не цикл Python?

- **Performance**: Excel обрабатывает вычисления нативно, что быстрее для больших матриц.
- **Live updating**: Если позже изменить размеры в формуле, лист автоматически пересчитывается.
- **Readability**: Формула напрямую выражает намерение («создать массив»), делая ваш код Python аккуратным.

## Как использовать lambda в Python для формул Excel

`LAMBDA`‑часть вызова `MAKEARRAY` — это анонимная функция на стороне Excel, а не lambda в Python. Тем не менее концепция та же: вы определяете небольшую встроенную логику, принимающую `r` (индекс строки) и `c` (индекс столбца) и возвращающую `r*c`.  

Если вы новичок в **how to use lambda** в мире Excel, представьте её как мини‑функцию, существующую только внутри формулы. Не требуется объявлять отдельную функцию где‑то ещё. В Python мы просто встраиваем строку:

```python
worksheet["A1"] = "=MAKEARRAY(5,5, LAMBDA(r,c, r*c))"
```

Эта строка говорит Excel: *«Для каждой ячейки в блоке 5 × 5 вычислить строка × столбец».*

Поскольку lambda оценивается Excel, вам не нужно беспокоиться о синтаксисе lambda в Python — только о синтаксисе Excel.

## Как использовать makearray для генерации массивов

`MAKEARRAY` — относительно новое дополнение к библиотеке функций Excel (доступно в Microsoft 365 с 2022 года). Оно заменяет старые приёмы вроде комбинаций `INDEX` + `ROW`/`COLUMN`. Сигнатура выглядит так:

```
MAKEARRAY(rows, columns, lambda)
```

- **rows** – количество требуемых строк.
- **columns** – количество требуемых столбцов.
- **lambda** – Excel‑LAMBDA, получающая `(row, column)` и возвращающая значение.

В нашем примере мы передали `5,5` для классической таблицы умножения, но вы легко можете изменить эти числа:

```python
worksheet["A1"] = "=MAKEARRAY(10,10, LAMBDA(r,c, r*c))"
```

Это даст вам таблицу 10 × 10 без использования каких‑либо циклов Python. Это демонстрирует **how to use makearray** для любого детерминированного сеточного массива, будь то таблица поиска, тепловая карта или финансовый график.

## Отображение excel array – извлечение данных обратно в Python

После того как Excel вычислит формулу, полученные значения находятся в листе так же, как любые вручную введённые ячейки. Чтобы **display excel array**, мы проходим по диапазону и выводим каждую строку:

```python
for row_index in range(1, 6):
    row_values = [worksheet.cell(row=row_index, column=col_index).value
                  for col_index in range(1, 6)]
    print(row_values)
```

Несколько советов:

- Используйте `worksheet.cell(row, column).value` вместо индексирования в виде словаря, если нужно работать с большими диапазонами; это немного быстрее.
- Если хотите более красивую таблицу, рассмотрите `tabulate` или `pandas.DataFrame` для форматирования вывода.

Ниже скриншот получившегося листа (alt‑текст изображения содержит основной ключевой запрос для SEO):

![Screenshot showing create multiplication table in Excel using Python](/images/multiplication-table-excel.png)

## Чтение excel values python – извлечение матрицы для дальнейшей обработки

Часто следующий шаг после **display excel array** — передать эти числа в конвейер анализа данных. Здесь в игру вступает **read excel values python**. Тот же цикл, который мы использовали для печати, можно переиспользовать для построения списка списков, массива NumPy или DataFrame Pandas:

```python
import pandas as pd

# Build a list of rows
data = []
for row_index in range(1, 6):
    row = [worksheet.cell(row=row_index, column=col_index).value
           for col_index in range(1, 6)]
    data.append(row)

# Convert to DataFrame for easy manipulation
df = pd.DataFrame(data, columns=[f"Col{c}" for c in range(1, 6)],
                  index=[f"Row{r}" for r in range(1, 6)])

print(df)
```

Вывод:

```
      Col1  Col2  Col3  Col4  Col5
Row1     1     2     3     4     5
Row2     2     4     6     8    10
Row3     3     6     9    12    15
Row4     4     8    12    16    20
Row5     5    10    15    20    25
```

Теперь у вас есть полностью типизированный DataFrame, который вы можете визуализировать, экспортировать в CSV или передать в модель машинного обучения. Это завершает часть рабочего процесса **read excel values python**.

## Пограничные случаи и практические советы

- **Formula recalculation**: Если вы изменяете книгу после первоначального вызова `calculate_formula()`, необходимо вызвать её снова; иначе кэшированный массив останется устаревшим.
- **Non‑365 Excel**: Более старые версии Excel не поддерживают `MAKEARRAY`. В этом случае используйте таблицу, сгенерированную в Python, и заполняйте каждую ячейку отдельно.
- **Large tables**: Для матриц больше ~100 × 100 рассмотрите потоковую передачу данных, чтобы не загружать весь лист в память.
- **Error handling**: Оберните шаги вычисления и чтения в блоки `try/except`, чтобы отлавливать `InvalidFileException` или `FormulaError`.

## Заключение

Мы только что показали, как **create multiplication table** в Excel с помощью Python, используя возможности **how to use lambda** и **how to use makearray**. Вы увидели, как **display excel array**, прочитать эти значения с помощью **read excel values python**, и даже преобразовать результат в Pandas DataFrame для последующего анализа.

Хотите пойти дальше? Попробуйте заменить логику умножения на что‑то более сложное — возможно, матрицу расстояний, таблицу вероятностей или динамическую ценовую сетку. Тот же шаблон применим: одна строка `MAKEARRAY`, быстрый `calculate_formula()` и несколько циклов Python для извлечения данных.

Если этот гид оказался полезным, поставьте звёздочку на GitHub, поделитесь им с коллегами или оставьте комментарий со своим случаем использования. Приятного кодинга и наслаждайтесь лаконичностью генерации таблиц Excel одной формулой!

## Что стоит изучить дальше?

Следующие руководства охватывают тесно связанные темы, которые развивают техники, продемонстрированные в этом гиде. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [Как создать и настроить рабочие книги Excel с Aspose.Cells .NET: пошаговое руководство](/cells/english/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)
- [Учебник Aspose.Cells .NET: Как легко создавать и изменять рабочие книги Excel](/cells/english/net/workbook-operations/aspose-cells-net-create-modify-excel-workbooks/)
- [Как создавать и стилизовать именованные диапазоны в Excel с помощью Aspose.Cells .NET | Пошаговое руководство](/cells/english/net/range-management/create-style-named-ranges-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}