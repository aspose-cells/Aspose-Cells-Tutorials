---
category: general
date: 2026-06-05
description: Включите опцию вложенного диапазона в Aspose.Cells SmartMarkerProcessor,
  чтобы без труда обрабатывать иерархические данные Excel. Узнайте о смарт‑маркерах,
  вложенных диапазонах и лучших практиках.
draft: false
keywords:
- enable nested range option
- SmartMarkerProcessor
- nested range handling
- Excel smart markers
- Aspose.Cells
language: ru
og_description: Включите опцию вложенного диапазона в Aspose.Cells SmartMarkerProcessor
  для работы с иерархическими данными. Полное руководство с кодом, советами и подводными
  камнями.
og_title: Включить опцию вложенного диапазона в Aspose.Cells SmartMarker
schemas:
- author: Aspose
  dateModified: '2026-06-05'
  description: Enable nested range option in Aspose.Cells SmartMarkerProcessor to
    handle hierarchical Excel data effortlessly. Learn smart markers, nested ranges,
    and best practices.
  headline: Enable Nested Range Option in Aspose.Cells SmartMarker
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
- Smart Markers
title: Включить опцию вложенного диапазона в Aspose.Cells SmartMarker
url: /ru/net/smart-markers-dynamic-data/enable-nested-range-option-in-aspose-cells-smartmarker/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Включение опции вложенного диапазона в Aspose.Cells SmartMarker

Когда‑нибудь задумывались, как **включить опцию вложенного диапазона** в Aspose.Cells SmartMarkerProcessor? Включение этой функции позволяет работать с иерархическими данными, такими как заказы и позиции, без проблем.  

В этом руководстве мы пройдём реальный сценарий: заполним список заказов с вложенными позициями в шаблон Excel с помощью smart‑markers. К концу вы получите полностью рабочую книгу, поймёте, что такое **SmartMarkerProcessor**, и узнаете, почему важен флаг **nested range handling**.

Мы рассмотрим:

* Подготовку анонимного объекта C#, имитирующего данные master‑detail.  
* Включение флага **nested range** в процессоре.  
* Запуск процессора над книгой и проверку результата.  

Никаких сложных фреймворков — только .NET 6+ и библиотека Aspose.Cells for .NET. Если вы когда‑либо сталкивались с повторяющимися строками внутри повторяющихся строк, это руководство для вас.

---

## Подготовка иерархических данных для Excel Smart Markers

Сначала нам нужен источник данных, отражающий отношение «родитель‑дитя». Пример ниже создаёт анонимный объект с одним заказом, содержащим две позиции.

```csharp
// Step 1: Define hierarchical data with orders and their items
var orderData = new
{
    Orders = new[]
    {
        new
        {
            Id = 1,
            Items = new[]
            {
                new { Name = "A" },
                new { Name = "B" }
            }
        }
    }
};
```

**Почему такая структура?**  
Smart markers читают имена свойств (`Orders`, `Items`) и автоматически генерируют вложенные диапазоны, когда процессор настроен правильно. Это как мини‑база данных, по которой будет проходить шаблон Excel.

> **Pro tip:** Используйте осмысленные имена свойств, совпадающие с маркерами, размещёнными в шаблоне (например, `&=Orders.Id&`, `&=Items.Name&`). Несоответствие имён — частая причина ошибок «no data».

---

## Настройка SmartMarkerProcessor и включение вложенного диапазона

Теперь создаём процессор и включаем переключатель **NestedRange**. Эта одна строка сообщает Aspose.Cells рассматривать коллекции‑дочерние как вложенные таблицы.

```csharp
// Step 2: Create a SmartMarkerProcessor and enable nested range handling
SmartMarkerProcessor processor = new SmartMarkerProcessor();
processor.Options.NestedRange = true;   // <‑‑ enable nested range option
```

**Что делает `NestedRange = true`?**  
При включении процессор создаёт отдельный диапазон для каждой дочерней коллекции и помещает его внутрь родительского диапазона. Без этого будет отрисована только верхнеуровневая коллекция (`Orders`), а строки `Items` будут проигнорированы.

> **Watch out:** Если включить вложенные диапазоны, но забыть отметить дочерний диапазон в шаблоне (с помощью `&=Items.Start&` / `&=Items.End&`), процессор бросит `SmartMarkerException`. Всегда проверяйте синтаксис маркеров.

---

## Загрузка или создание шаблона книги

Для демонстрации мы сгенерируем простую книгу «на лету», но в реальном проекте обычно начинают с существующего файла `.xlsx`, уже содержащего smart‑markers.

```csharp
// Step 3: Create a workbook with a simple template
Workbook wb = new Workbook();
Worksheet ws = wb.Worksheets[0];

// Header row
ws.Cells["A1"].PutValue("Order ID");
ws.Cells["B1"].PutValue("Item Name");

// Smart marker row for Orders (parent)
//   &amp;=Orders.Start&amp; and &amp;=Orders.End&amp; define the range for each order.
ws.Cells["A2"].PutValue("&=Orders.Start&");
ws.Cells["A2"].PutValue("&=Orders.Id&");
ws.Cells["B2"].PutValue("&=Orders.End&");

// Smart marker row for Items (child)
//   Nested inside the Orders range.
ws.Cells["A3"].PutValue("&=Items.Start&");
ws.Cells["A3"].PutValue("&=Items.Name&");
ws.Cells["B3"].PutValue("&=Items.End&");
```

Обратите внимание на маркеры `&=Orders.Start&` / `&=Orders.End&` — они указывают процессору, где начинается и заканчивается блок каждого заказа. Тот же шаблон применяется к диапазону дочерних `Items`.

---

## Обработка книги с помощью Smart Markers

Имея данные и процессор, остаётся выполнить однострочный вызов, который объединит всё.

```csharp
// Step 4: Apply the data to the workbook using smart markers
processor.Process(wb, orderData);
```

После этого вызова книга будет содержать:

| Order ID | Item Name |
|----------|-----------|
| 1        | A         |
| 1        | B         |

Сохранить результат можно на диск или отправить в виде потока клиенту:

```csharp
wb.Save("NestedRangeResult.xlsx");
```

---

## Проверка вывода и типичные подводные камни

### Ожидаемый результат

Откройте `NestedRangeResult.xlsx` — вы увидите две строки под заголовком единственного заказа, каждая строка отображает имя позиции (`A` и `B`). Идентификатор заказа повторяется для каждой дочерней строки — именно так работают вложенные диапазоны.

### Распространённые проблемы

| Symptom | Likely Cause | Fix |
|---------|--------------|-----|
| No child rows appear | `NestedRange` left as `false` | Set `processor.Options.NestedRange = true`. |
| Markers show up as plain text | Marker syntax typo (`&=Orders.Start&` vs `&=Orders.Start`) | Ensure both `&=` and trailing `&` are present. |
| Duplicate rows for each order | Missing `&=Orders.End&` marker | Add the closing marker to bound the parent range. |

---

## Полный рабочий пример (готовый к копированию)

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Define hierarchical data
        var orderData = new
        {
            Orders = new[]
            {
                new
                {
                    Id = 1,
                    Items = new[]
                    {
                        new { Name = "A" },
                        new { Name = "B" }
                    }
                }
            }
        };

        // 2️⃣ Create processor and enable nested range option
        SmartMarkerProcessor processor = new SmartMarkerProcessor();
        processor.Options.NestedRange = true;   // enable nested range option

        // 3️⃣ Build a simple workbook template with smart markers
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];

        ws.Cells["A1"].PutValue("Order ID");
        ws.Cells["B1"].PutValue("Item Name");

        // Parent range markers
        ws.Cells["A2"].PutValue("&=Orders.Start&");
        ws.Cells["A2"].PutValue("&=Orders.Id&");
        ws.Cells["B2"].PutValue("&=Orders.End&");

        // Child range markers (nested)
        ws.Cells["A3"].PutValue("&=Items.Start&");
        ws.Cells["A3"].PutValue("&=Items.Name&");
        ws.Cells["B3"].PutValue("&=Items.End&");

        // 4️⃣ Process the workbook
        processor.Process(wb, orderData);

        // 5️⃣ Save the result
        wb.Save("NestedRangeResult.xlsx");
        Console.WriteLine("Workbook generated – check NestedRangeResult.xlsx");
    }
}
```

Запустите программу, откройте сгенерированный файл — вы увидите вложенные строки, заполненные точно так же, как в таблице выше.

---

## Заключение

Вы только что узнали, как **включить опцию вложенного диапазона** в Aspose.Cells SmartMarkerProcessor, превратив плоский шаблон Excel в мощный генератор отчётов master‑detail. Установив `processor.Options.NestedRange = true`, библиотека автоматически создаёт внутренние таблицы для дочерних коллекций, избавляя вас от ручных циклов вставки строк.

Что дальше? Попробуйте добавить второй уровень вложенности (например, заказ → позиции → суб‑компоненты), поэкспериментируйте со стилизацией сгенерированных строк или переключитесь на предварительно подготовленный шаблон с диаграммами и формулами. Комбинация **Excel smart markers** и **nested range handling** — надёжная основа любой автоматизированной системы отчётности.

Есть вопросы или сложный сценарий? Оставляйте комментарий ниже, и happy coding!

## Что изучать дальше?

Следующие руководства охватывают тесно связанные темы, расширяющие техники, продемонстрированные в этом пособии. Каждый ресурс содержит полностью работающие примеры кода с пошаговыми объяснениями, помогающими освоить дополнительные возможности API и исследовать альтернативные подходы в ваших проектах.

- [Handle Nested Objects with Smart Markers Aspose.Cells](/cells/english/net/smart-markers-dynamic-data/nested-objects-smart-markers/)
- [Populate Excel with Nested Data Using Aspose.Cells for Java&#58; A Comprehensive Guide](/cells/english/java/data-manipulation/populate-excel-nested-data-aspose-cells-java/)
- [Populate Excel Nested Data Aspose Cells Java](/cells/german/java/data-manipulation/populate-excel-nested-data-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}