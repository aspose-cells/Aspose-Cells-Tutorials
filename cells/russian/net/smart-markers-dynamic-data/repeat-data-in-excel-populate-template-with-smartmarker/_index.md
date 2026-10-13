---
category: general
date: 2026-02-21
description: Быстро повторяйте данные в Excel с помощью SmartMarker — узнайте, как
  заполнять шаблон Excel и без усилий дублировать строки.
draft: false
keywords:
- repeat data in excel
- populate excel template
- how to repeat rows
- repeat rows in excel
- populate excel from data
language: ru
og_description: Повторять данные в Excel с помощью SmartMarker. Узнайте, как заполнять
  шаблон Excel, повторять строки и автоматизировать ваши таблицы.
og_title: Повтор данных в Excel – заполнить шаблон с помощью SmartMarker
tags:
- excel
- csharp
- smartmarker
- automation
title: Повтор данных в Excel — заполнить шаблон с помощью SmartMarker
url: /ru/net/smart-markers-dynamic-data/repeat-data-in-excel-populate-template-with-smartmarker/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# повтор данных в excel – Заполнение шаблона с помощью SmartMarker

Когда‑то вам **нужно было повторить данные в Excel**, но вы не знали, как избежать ручного копирования‑вставки? Вы не одиноки. Во многих сценариях отчётности у вас есть список элементов, который должен автоматически расширяться в строки, а делать это вручную — рецепт ошибок.

Дело в том, что использование **SmartMarkerProcessor** из библиотеки **GemBox.Spreadsheet** позволяет **заполнить шаблон Excel** одной строкой C# и заставить строки повторяться для каждого элемента вашей коллекции. В этом руководстве мы пройдём все шаги, покажем полный код и объясним, почему каждый элемент важен, чтобы вы могли уверенно повторять строки в Excel без лишних усилий.

## Что вы узнаете

* Как определить структуру данных, управляющую операцией повторения.  
* Как привязать `SmartMarkerProcessor` к рабочей книге, содержащей скрытый лист‑шаблон.  
* Как маркер `${Repeat:Item}` автоматически разворачивается в несколько строк.  
* Советы по обработке крайних случаев, таких как пустые коллекции или пользовательское форматирование.  

К концу этого урока вы сможете **заполнять Excel данными** масштабируемым способом, который легко поддерживать и который работает в любом .NET‑проекте.

---

## Требования

* .NET 6.0 или новее (код использует современные возможности C#).  
* Пакет NuGet **GemBox.Spreadsheet** (бесплатная версия работает до 150 строк).  
* Базовый файл шаблона Excel (`Template.xlsx`) со скрытым листом под названием `HiddenTemplate`.  
* Знание объектов C# и LINQ будет полезным, но не обязательным.

---

## Шаг 1 – Определите структуру данных для повторения

Сначала нужен источник данных, по которому движок SmartMarker сможет итерировать. В реальных приложениях он обычно берётся из базы данных, API или CSV‑файла. Для простоты будем использовать анонимный тип с единственным свойством `Item`, содержащим массив строк.

```csharp
// Step 1: Define the data that will be repeated in the template
var repeatData = new { Item = new[] { "A", "B", "C" } };
```

> **Почему это важно:** Маркер `${Repeat:Item}` в шаблоне Excel ищет свойство с именем `Item`. Если вы переименуете свойство, обновите маркер соответственно. Такое тесное связывание гарантирует, что шаблон остаётся синхронным с кодом, упрощая **заполнение шаблона Excel** без угадывания имён столбцов.

### Распространённые варианты

* **Сложные объекты:** Вместо простого массива строк можно передать список объектов (`new[] { new { Name = "A", Qty = 10 } }`). Маркер повторит строки, и в листе можно будет использовать `${Item.Name}` и `${Item.Qty}`.  
* **Пустые коллекции:** Если `Item` пуст, SmartMarker просто удалит блок повторения, оставив шаблон нетронутым — это удобно для необязательных секций.

---

## Шаг 2 – Создайте SmartMarkerProcessor для скрытого листа‑шаблона

Далее загрузите рабочую книгу и создайте экземпляр `SmartMarkerProcessor`. Укажите книгу, содержащую скрытый лист‑шаблон; SmartMarker скопирует этот лист в видимый и развернёт маркеры повторения.

```csharp
using GemBox.Spreadsheet;

// Load the workbook that holds the hidden template sheet.
var wb = ExcelFile.Load("Template.xlsx");

// Step 2: Create a SmartMarkerProcessor for the workbook that holds the hidden template sheet
var processor = new SmartMarkerProcessor(wb);
```

> **Pro tip:** Если в одном файле несколько шаблонов, можно указать имя листа‑источника при вызове `processor.Process`. Это помогает, когда нужно **повторять строки в Excel** для разных разделов отчёта.

### Обработка крайних случаев

* **Отсутствующий лист‑шаблон:** Оберните загрузку в `try/catch` и запишите понятную ошибку — это предотвратит молчаливые сбои при неверном пути к файлу.  
* **Большие наборы данных:** При тысячах строк рассмотрите возможность потоковой записи результата в файл (`processor.Save`) вместо удержания всего в памяти.

---

## Шаг 3 – Примените данные и разверните маркер `${Repeat:Item}`

Теперь приходит волшебная строка, которая действительно повторяет строки. Передайте объект, созданный в Шаге 1, в `processor.Process`. SmartMarker найдёт каждый маркер `${Repeat:Item}`, продублирует строку для каждого элемента и заменит заполнители реальными значениями.

```csharp
// Step 3: Apply the data to the template, expanding the ${Repeat:Item} marker
processor.Process(repeatData);

// Save the resulting workbook.
wb.Save("Result.xlsx");
```

### Что вы должны увидеть

После открытия `Result.xlsx` скрытый лист‑шаблон будет скопирован в новый видимый лист (по умолчанию называется `Sheet1`). Строка, содержащая `${Repeat:Item}`, появится трижды, а ячейки покажут **A**, **B** и **C** соответственно.

| Item |
|------|
| A    |
| B    |
| C    |

Если добавить дополнительные столбцы, такие как `${Item.Price}`, они автоматически заполнятся из источника данных.

---

## Как повторять строки в Excel без SmartMarker (быстрое сравнение)

| Подход                | Сложность кода | Поддерживаемость | Производительность |
|-----------------------|-----------------|------------------|--------------------|
| Ручное копирование‑вставка | Высокая          | Низкая           | Плохая             |
| VBA‑макрос            | Средняя         | Средняя          | Хорошая            |
| **SmartMarkerProcessor** | Низкая          | Высокая          | Отличная           |

Как видите, использование SmartMarker для **повторения данных в Excel** обеспечивает наилучшее разделение между дизайном шаблона и бизнес‑логикой. Кроме того, подход независим от языка — аналогичные концепции существуют в библиотеках Java, Python и JavaScript.

---

## Продвинутые советы и типичные подводные камни

### 1. Форматирование повторяющихся строк

SmartMarker копирует всю строку — включая стили ячеек, границы и условное форматирование. Если нужен иной стиль для первой или последней строки, добавьте дополнительные маркеры вроде `${If:Item.IsFirst}` и используйте условные формулы внутри Excel.

### 2. Работа с большими наборами данных

При обработке более 10 000 строк отключите автоматический расчёт Excel перед запуском:

```csharp
wb.WorkbookOptions = new WorkbookOptions { RecalculateAllFormulas = false };
```

Включите его обратно после сохранения, чтобы сохранить быстродействие.

### 3. Заполнение Excel данными из реальной базы

```csharp
var orders = dbContext.Orders
    .Where(o => o.Date >= start && o.Date <= end)
    .Select(o => new { o.OrderId, o.CustomerName, o.Total })
    .ToArray();

processor.Process(new { Order = orders });
```

Затем используйте `${Repeat:Order}` в шаблоне, чтобы перечислить каждый заказ. Этот шаблон показывает, как легко **заполнять Excel данными** напрямую из Entity Framework.

### 4. Использование нескольких блоков повторения

Можно разместить несколько маркеров `${Repeat:...}` на одном листе или на разных листах. SmartMarker обрабатывает их последовательно, поэтому порядок важен только если один блок зависит от вывода другого.

---

## Полный работающий пример

Ниже приведено самостоятельное консольное приложение, которое можно скопировать в Visual Studio и сразу запустить. Оно демонстрирует все три шага и сохранение файла.

```csharp
using System;
using GemBox.Spreadsheet;

class Program
{
    static void Main()
    {
        // License free version (up to 150 rows). For production use, set your license key.
        SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

        // 1️⃣ Define the data to repeat.
        var repeatData = new { Item = new[] { "A", "B", "C" } };

        // 2️⃣ Load the template workbook (ensure Template.xlsx exists next to the exe).
        var wb = ExcelFile.Load("Template.xlsx");

        // Create processor bound to the workbook.
        var processor = new SmartMarkerProcessor(wb);

        // 3️⃣ Process the data – this expands the ${Repeat:Item} marker.
        processor.Process(repeatData);

        // Save the populated workbook.
        wb.Save("Result.xlsx");

        Console.WriteLine("Excel file generated successfully – check Result.xlsx");
    }
}
```

**Ожидаемый результат:** `Result.xlsx` содержит лист, где строка с `${Repeat:Item}` появляется три раза, показывая A, B и C. Никаких ручных правок не требуется.

---

## Заключение

Теперь вы знаете, как эффективно **повторять данные в Excel**, используя SmartMarkerProcessor. Определив простой объект данных, загрузив шаблон рабочей книги и вызвав `Process`, вы сможете **заполнять шаблон Excel**, **повторять строки в Excel** и в целом **

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}