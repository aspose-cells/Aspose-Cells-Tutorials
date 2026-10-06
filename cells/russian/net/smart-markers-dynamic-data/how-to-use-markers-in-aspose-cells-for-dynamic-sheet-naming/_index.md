---
category: general
date: 2026-05-23
description: Как использовать маркеры в Aspose.Cells для динамического именования
  листов в автоматизации Excel. Узнайте о смарт‑маркерах, привязке данных JSON и создании
  листов за считанные минуты.
draft: false
keywords:
- how to use markers
- dynamic sheet naming excel
- aspose.cells smart markers
language: ru
og_description: Как использовать маркеры в Aspose.Cells для создания Excel‑файлов
  с динамическим именованием листов. Полное пошаговое руководство с полным примером
  на C#.
og_title: Как использовать маркеры – динамическое именование листов в Excel с Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-05-23'
  description: How to use markers with Aspose.Cells to achieve dynamic sheet naming
    Excel automation. Learn smart markers, JSON data binding, and sheet creation in
    minutes.
  headline: How to Use Markers in Aspose.Cells for Dynamic Sheet Naming in Excel
  type: TechArticle
- description: How to use markers with Aspose.Cells to achieve dynamic sheet naming
    Excel automation. Learn smart markers, JSON data binding, and sheet creation in
    minutes.
  name: How to Use Markers in Aspose.Cells for Dynamic Sheet Naming in Excel
  steps:
  - name: What Happens Under the Hood?
    text: 1. The processor reads the `Orders` array. 2. For each order it creates
      a **master sheet** (using `${Orders.MasterSheetName}`) and a **detail sheet**
      (using the `DetailSheetNewName` pattern). 3. Cell values are replaced with the
      corresponding JSON fields, so the master sheet’s first cell ends up con
  - name: What if I need more than two levels of hierarchy?
    text: You can nest markers inside the newly created detail sheets. Just place
      additional `${...}` tags in the template sheet before processing. The processor
      will cascade through each level automatically.
  - name: Can I use a DataTable instead of JSON?
    text: Absolutely. `SmartMarkerProcessor` has overloads for `DataSet`, `DataTable`,
      and even custom objects. The only change is the call to `ApplyJson` – you’d
      use `ApplyDataSet(myDataSet)` instead.
  - name: How do I control the order of sheet creation?
    text: The order follows the sequence of the source collection. If you need a custom
      sort, simply sort the JSON array (or DataTable) before passing it to the processor.
  - name: Is there a way to hide the template sheet after processing?
    text: Yes. Set `sm.Options.RemoveTemplateSheets = true;` before calling `ApplyJson`.
      The original sheet (index 0) will be removed from the final workbook.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Как использовать маркеры в Aspose.Cells для динамического именования листов
  в Excel
url: /ru/net/smart-markers-dynamic-data/how-to-use-markers-in-aspose-cells-for-dynamic-sheet-naming/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как использовать маркеры в Aspose.Cells для динамического именования листов в Excel

Когда‑нибудь задумывались **как использовать маркеры**, чтобы превратить статический шаблон Excel в полноценную книгу master‑detail? Вы не одиноки. Многие разработчики сталкиваются с проблемой, когда нужны возможности *dynamic sheet naming excel*, особенно когда имена листов должны отражать значения данных из JSON или базы данных.  

В этом руководстве мы пройдём полный, готовый к запуску пример на C#, который показывает **как использовать маркеры** с **Aspose.Cells** smart markers, привязывает JSON‑данные и позволяет процессору создавать листы, имена которых меняются «на лету». Без лишних слов, только точный код, который можно вставить в Visual Studio и сразу увидеть результаты.

## Что вы узнаете

- Концепцию **smart markers** и почему они идеальны для сценариев master‑detail.  
- Как встраивать теги маркеров в рабочую книгу, которые позже будут заменены на реальные имена листов.  
- Настройка **dynamic sheet naming excel** с использованием опции `DetailSheetNewName`.  
- Запуск `SmartMarkerProcessor` с JSON‑данными для автоматического создания нескольких листов.  
- Проверка результата и несколько полезных советов по избежанию распространённых ошибок.

> **Prerequisites** – Вам нужен современный .NET runtime (≥ .NET 6 подходит), библиотека Aspose.Cells for .NET (можно взять бесплатную trial‑версию на сайте Aspose) и базовое знакомство с C#.  

---

![how to use markers example in Aspose.Cells](example.png "how to use markers example in Aspose.Cells")

## Как использовать маркеры для создания динамического именования листов (Шаг 1)

Первое, что нам нужно, — пустая рабочая книга, которая будет служить шаблоном. В реальном проекте вы, вероятно, начнёте с существующего файла `.xlsx`, который уже содержит макет, форматирование и ячейки‑заполнители. Для ясности мы создадим всё программно.

```csharp
using Aspose.Cells;
using Aspose.Cells.SmartMarker;

// Step 1: Create a new workbook and get the first worksheet
Workbook wb = new Workbook();                // fresh workbook, no sheets yet
Worksheet ws = wb.Worksheets[0];             // default first sheet
```

*Why this matters*: Объект `Worksheet` — это место, куда мы помещаем наши **smart marker** теги. Представьте теги как крошечные заполнители, которые процессор позже заменит реальными значениями из JSON.  

## Вставка тегов Smart Marker (Шаг 2)

Теперь мы размещаем теги маркеров непосредственно в ячейках. Синтаксис `${...}` сообщает Aspose.Cells «это маркер». В нашем примере нужны два маркера: один для имени листа‑мастера и другой для имени листа‑детали.

```csharp
// Step 2: Insert Smart Marker tags that will be replaced with sheet names
ws.Cells[0, 0].PutValue("${Orders.MasterSheetName}");   // master sheet placeholder
ws.Cells[1, 0].PutValue("${Orders.DetailSheetName}");   // detail sheet placeholder
```

> **Pro tip** – Делайте имена маркеров короткими и осмысленными; они становятся ключами, которые вы будете использовать в JSON‑payload.  

## Подготовка JSON‑данных (Шаг 3)

Процессор работает с любым источником данных, который можно представить в виде JSON, `DataSet` или даже простого объекта. Ниже минимальная строка JSON, содержащая коллекцию master‑detail. Обратите внимание, что каждый заказ содержит как `MasterSheetName`, так и `DetailSheetName`.

```csharp
// Step 3: Prepare the JSON data that contains the master‑detail information
string jsonOrders = @"{
    ""Orders"": [
        {
            ""OrderId"": 1,
            ""MasterSheetName"": ""Master_1"",
            ""DetailSheetName"": ""Detail_1""
        },
        {
            ""OrderId"": 2,
            ""MasterSheetName"": ""Master_2"",
            ""DetailSheetName"": ""Detail_2""
        }
    ]
}";
```

*Why JSON?* Это лёгкий, человекочитаемый формат, отлично подходящий для веб‑API. Вы также можете получить эти данные из SQL‑запроса и сериализовать их с помощью `Newtonsoft.Json`.  

## Инициализация SmartMarkerProcessor (Шаг 4)

`SmartMarkerProcessor` — это движок, который сканирует книгу, ищет маркеры и выполняет привязку данных. Его создание занимает одну строку кода.

```csharp
// Step 4: Initialise the SmartMarkerProcessor with the workbook
SmartMarkerProcessor sm = new SmartMarkerProcessor(wb);
```

## Определение динамического именования листов (Шаг 5)

Здесь **dynamic sheet naming excel** действительно проявляет свою мощь. Установив `DetailSheetNewName`, мы говорим процессору создавать новый лист‑деталь для каждого заказа и именовать его на основе `OrderId`. Заполнитель `${OrderId}` будет подставлен из текущей записи во время обработки.

```csharp
// Step 5: Define how new detail sheets should be named during processing
sm.Options.DetailSheetNewName = "Detail_${OrderId}";
```

> **Watch out** – Если забыть включить синтаксис `${}`, лист будет буквально назван «Detail_${OrderId}» вместо «Detail_1», «Detail_2» и т.д.  

## Применение JSON и генерация листов (Шаг 6)

Теперь позволим процессору выполнить тяжёлую работу. Он прочитает JSON, заменит маркеры и при необходимости создаст новые листы.

```csharp
// Step 6: Apply the JSON data to populate the smart markers and generate sheets
sm.ApplyJson(jsonOrders);
```

### Что происходит «под капотом»?

1. Процессор читает массив `Orders`.  
2. Для каждого заказа он создаёт **master sheet** (используя `${Orders.MasterSheetName}`) и **detail sheet** (используя шаблон `DetailSheetNewName`).  
3. Значения ячеек заменяются соответствующими полями JSON, поэтому первая ячейка master sheet будет содержать “Master_1”, “Master_2” и т.д.  

## Сохранение и проверка результата (Опционально)

Наконец, сохраняем книгу на диск. Откройте файл в Excel, и вы увидите два листа‑мастера (`Master_1`, `Master_2`) и два динамически именованных листа‑детали (`Detail_1`, `Detail_2`).  

```csharp
// (Optional) Save the result to verify the output
wb.Save("output.xlsx");
```

**Expected output** – После открытия `output.xlsx` вы увидите:

- Лист **Master_1** с ячейкой A1 = “Master_1”.  
- Лист **Detail_1** с ячейкой A1 = “Detail_1”.  
- Лист **Master_2** с ячейкой A1 = “Master_2”.  
- Лист **Detail_2** с ячейкой A1 = “Detail_2”.  

Это полный цикл **как использовать маркеры** для достижения **dynamic sheet naming excel** с помощью **Aspose.Cells smart markers**.

---

## Часто задаваемые вопросы и особые случаи

### Что делать, если требуется более двух уровней иерархии?

Можно вкладывать маркеры в только что созданные листы‑детали. Просто разместите дополнительные теги `${...}` в шаблонном листе до обработки. Процессор автоматически пройдёт через каждый уровень.

### Можно ли использовать DataTable вместо JSON?

Конечно. `SmartMarkerProcessor` имеет перегрузки для `DataSet`, `DataTable` и даже пользовательских объектов. Единственное изменение — вызов `ApplyJson`; вместо него используйте `ApplyDataSet(myDataSet)`.

### Как контролировать порядок создания листов?

Порядок следует последовательности исходной коллекции. Если нужен пользовательский порядок, просто отсортируйте массив JSON (или DataTable) перед передачей его процессору.

### Есть ли способ скрыть шаблонный лист после обработки?

Да. Установите `sm.Options.RemoveTemplateSheets = true;` перед вызовом `ApplyJson`. Исходный лист (индекс 0) будет удалён из финальной книги.

---

## Полный рабочий пример (все шаги вместе)

Ниже полный код программы, который можно скопировать‑вставить в новый консольный проект C#. Убедитесь, что подключён пакет NuGet `Aspose.Cells`.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.SmartMarker;

namespace DynamicSheetNamingDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create a new workbook and get the first worksheet
            Workbook wb = new Workbook();
            Worksheet ws = wb.Worksheets[0];

            // Step 2: Insert Smart Marker tags that will be replaced with sheet names
            ws.Cells[0, 0].PutValue("${Orders.MasterSheetName}");
            ws.Cells[1, 0].PutValue("${Orders.DetailSheetName}");

            // Step 3: Prepare the JSON data that contains the master‑detail information
            string jsonOrders = @"{
                ""Orders"": [
                    {
                        ""OrderId"": 1,
                        ""MasterSheetName"": ""Master_1"",
                        ""DetailSheetName"": ""Detail_1""
                    },
                    {
                        ""OrderId"": 2,
                        ""MasterSheetName"": ""Master_2"",
                        ""DetailSheetName"": ""Detail_2""
                    }
                ]
            }";

            // Step 4: Initialise the SmartMarkerProcessor with the workbook
            SmartMarkerProcessor sm = new SmartMarkerProcessor(wb);

            // Step 5: Define how new detail sheets should be named during processing
            sm.Options.DetailSheetNewName = "Detail_${OrderId}";

            // (Optional) Remove the original template sheet after processing
            // sm.Options.RemoveTemplateSheets = true;

            // Step 6: Apply the JSON data to populate the smart markers and generate sheets
            sm.ApplyJson(jsonOrders);

            // Save the result
            wb.Save("output.xlsx");
            Console.WriteLine("Workbook generated successfully. Check output.xlsx.");
        }
    }
}
```

Запустите программу, откройте `output.xlsx`, и вы увидите динамические листы точно так, как описано выше.

---

## Подведение итогов

Мы только что рассмотрели **как использовать маркеры** в Aspose.Cells, чтобы превратить простую книгу в решение master‑detail с **dynamic sheet naming excel**. Ключевые выводы:

1. Разместите smart markers `${...}` там, где должны появиться данные.  
2. Передайте JSON (или любой поддерживаемый источник данных) в `SmartMarkerProcessor`.  
3. Используйте `DetailSheetNewName`, чтобы процессор называл новые листы «на лету».  

Отсюда вы можете исследовать более продвинутые сценарии — добавление таблиц, стилизация ячеек или даже внедрение диаграмм — всё управляется  

## Связанные руководства

- [Как реализовать Smart Markers Aspose.Cells в C# для динамической отчетности Excel](/cells/english/net/automation-batch-processing/implement-aspose-cells-smart-markers-with-csharp/)
- [Создание динамических Excel‑отчетов с помощью Smart Markers Aspose.Cells .NET](/cells/english/net/templates-reporting/generate-excel-reports-aspose-cells-net-smart-markers/)
- [Мастерство Aspose.Cells .NET: внедрение Smart Markers и пользовательских меток для динамических Excel‑отчетов](/cells/english/net/advanced-features/aspose-cells-net-smart-markers-custom-labels/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}