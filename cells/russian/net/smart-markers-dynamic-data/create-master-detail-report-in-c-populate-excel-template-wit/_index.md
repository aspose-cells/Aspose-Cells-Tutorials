---
category: general
date: 2026-02-28
description: Создайте мастер‑детальный отчёт на C# и узнайте, как заполнять шаблон
  Excel, объединять данные в Excel и загружать рабочую книгу Excel в C# всего за несколько
  шагов.
draft: false
keywords:
- create master detail report
- populate excel template
- merge data into excel
- load excel workbook c#
- how to create master detail
language: ru
og_description: Создайте мастер‑детальный отчёт в C# с использованием Aspose.Cells
  SmartMarker. Узнайте, как загрузить книгу Excel в C#, объединить данные в Excel
  и заполнить шаблон Excel.
og_title: Создать мастер‑детальный отчет в C# – заполнить шаблон Excel
tags:
- C#
- Aspose.Cells
- Excel automation
- SmartMarker
title: Создание отчёта master‑detail в C# – Заполнение шаблона Excel с помощью SmartMarker
url: /ru/net/smart-markers-dynamic-data/create-master-detail-report-in-c-populate-excel-template-wit/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание master‑detail отчёта в C# – Заполнение шаблона Excel с помощью SmartMarker

Когда‑нибудь вам нужно было **создать master detail report** в C#, но вы не знали, как поместить данные в файл Excel? Вы не одиноки. В этом руководстве мы пошагово пройдём процесс **заполнения шаблона Excel**, **слияния данных в Excel** и **загрузки книги Excel C#‑стилем**, чтобы вы получили готовый master‑detail отчёт, готовый к распространению.

Мы будем использовать Aspose.Cells SmartMarker — мощный движок, который из коробки понимает отношения master‑detail. К концу руководства у вас будет полностью готовый, исполняемый пример, который можно вставить в любой проект .NET. Никаких расплывчатых «см. документацию»‑шорткатов — только автономное решение, которое можно скопировать‑вставить и запустить.

## Что вы узнаете

- Как **создать master detail** структуры данных в C#, которые напрямую сопоставляются с шаблоном Excel.
- Точный способ **загрузки книги Excel C#** кода, который открывает файл `.xlsx` с тегами SmartMarker.
- Процесс **заполнения шаблона Excel** с помощью запуска `SmartMarkerProcessor`.
- Советы по обработке граничных случаев, таких как отсутствие тегов или большие наборы данных.
- Как проверить результат и как выглядит окончательный **master detail report**.

### Требования

- .NET 6.0 или новее (код также работает на .NET Framework 4.8).
- Aspose.Cells для .NET (можно получить бесплатный пробный пакет NuGet: `Install-Package Aspose.Cells`).
- Базовый файл Excel (`template.xlsx`), содержащий теги SmartMarker (мы покажем минимальную разметку, которая вам нужна).

Если всё готово, давайте погрузимся.

## Шаг 1 – Создание источника данных master‑detail *(how to create master detail)*

Первое, что вам нужно, — объект C#, представляющий строки‑мастера (заказы) и их дочерние строки (позиции заказа). SmartMarker автоматически прочитает эту иерархию, когда `MasterDetail` установлено в `true`.

```csharp
using System;

// Step 1: Build the master‑detail data object
var orderData = new
{
    // Master collection – each order is a row in the master table
    Orders = new[]
    {
        new
        {
            Id = 1,
            // Detail collection – items belonging to order 1
            Items = new[] { new { Sku = 101, Qty = 2 }, new { Sku = 102, Qty = 1 } }
        },
        new
        {
            Id = 2,
            Items = new[] { new { Sku = 202, Qty = 1 } }
        }
    }
};
```

**Почему это важно:**  
SmartMarker ищет свойство с именем `Orders` (мастер), а затем для каждого заказа ищет коллекцию под названием `Items`. Согласовав эти имена, вы автоматически получаете **master‑detail report** без необходимости писать какие‑либо циклы.

> **Совет:** Делайте имена свойств короткими и осмысленными; они становятся заполнителями в вашем шаблоне Excel.

## Шаг 2 – Настройка параметров SmartMarker для обработки master‑detail

Сообщите движку, что вы работаете со сценарием master‑detail, и укажите имя листа‑детали, который будет получать дочерние строки.

```csharp
using Aspose.Cells;

// Step 2: Set up SmartMarker options
SmartMarkerOptions options = new SmartMarkerOptions
{
    // Enables master‑detail processing
    MasterDetail = true,
    // The sheet in the template that holds the detail rows
    DetailSheetName = "OrderDetail"
};
```

**Почему это важно:**  
Если опустить `MasterDetail = true`, SmartMarker будет рассматривать данные как плоский список, и строки‑детали никогда не появятся. `DetailSheetName` должен точно соответствовать имени листа, созданного в шаблоне (с учётом регистра).

## Шаг 3 – Загрузка книги Excel в стиле C#

Теперь откроем шаблон, содержащий теги SmartMarker. Это шаг **загрузки книги Excel C#**, над которым многие разработчики спотыкаются, забывая указать правильный путь к файлу или корректно освободить книгу.

```csharp
using System.IO;

// Step 3: Load the workbook that holds the SmartMarker tags
string templatePath = Path.Combine(Environment.CurrentDirectory, "template.xlsx");
Workbook workbook = new Workbook(templatePath);
```

**Почему это важно:**  
Aspose.Cells читает всю книгу в память, поэтому файл может находиться на диске, быть встроенным как ресурс или даже передаваться потоком из веб‑сервиса. Просто убедитесь, что путь указывает на действительный файл `.xlsx`, содержащий теги, которые мы обсудим дальше.

## Шаг 4 – Вставка тегов SmartMarker в шаблон (заполнение шаблона Excel)

Если открыть `template.xlsx` сейчас, вы увидите два листа:

- **Orders** – лист‑мастер с строкой вида `&=Orders.Id`.
- **OrderDetail** – лист‑деталь с строками вида `&=Items.Sku` и `&=Items.Qty`.

Ниже минимальный вид разметки:

| Лист | Ячейка A1 | Ячейка B1 |
|-------|---------|---------|
| Orders | `&=Orders.Id` | *(empty)* |
| OrderDetail | `&=Items.Sku` | `&=Items.Qty` |

Код для тегов писать не требуется — они находятся в файле Excel. Шаг **заполнения шаблона Excel** просто вызывает процессор:

```csharp
// Step 4: Run SmartMarker to merge data into Excel
new SmartMarkerProcessor().Process(workbook, orderData, options);
```

**Почему это важно:**  
Процессор сканирует каждый лист, заменяет заполнители `&=` реальными значениями и расширяет строки для каждой записи мастера и детали. Поскольку `MasterDetail` включён, он автоматически создаёт новую строку для каждой позиции под соответствующим заказом.

## Шаг 5 – Сохранение master detail отчёта

Наконец, запишите заполненную книгу на диск. Это момент, когда вы получаете готовый к распространению **master detail report**.

```csharp
// Step 5: Save the populated workbook
string outputPath = Path.Combine(Environment.CurrentDirectory, "output.xlsx");
workbook.Save(outputPath);

// Optional: open the file automatically (Windows only)
System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo
{
    FileName = outputPath,
    UseShellExecute = true
});
```

**Ожидаемый результат:**  

- Лист **Orders** показывает две строки: `1` и `2` (идентификаторы заказов).  
- Лист **OrderDetail** показывает три строки:  
  - SKU 101 Qty 2  
  - SKU 102 Qty 1  
  - SKU 202 Qty 1  

Это полностью рабочий **create master detail report**, который вы можете отправить по электронной почте, распечатать или передать в другую систему.

## Граничные случаи и часто задаваемые вопросы

### Что делать, если в шаблоне отсутствует тег?

SmartMarker тихо игнорирует неизвестные теги, но вы получите пустые ячейки. Проверьте написание тегов и убедитесь, что имена свойств в вашем объекте C# точно совпадают.

### Как он обрабатывает большие наборы данных?

Процессор передаёт строки потоково, поэтому даже тысячи записей‑деталей не перегрузят память. Однако для чрезвычайно больших файлов может потребоваться увеличить `MemorySetting` в `LoadOptions`.

```csharp
var loadOptions = new LoadOptions(LoadFormat.Xlsx)
{
    MemorySetting = MemorySetting.MemoryPreference
};
Workbook largeWorkbook = new Workbook(templatePath, loadOptions);
```

### Можно ли использовать другое имя листа для мастера?

Да — просто переименуйте лист в шаблоне и при необходимости скорректируйте `DetailSheetName`, если у вас есть лист‑деталь. Имя листа‑мастера выводится из заполнителя (`&=Orders.Id`).

### Что делать, если нужно добавить строку итогов?

Добавьте обычную формулу Excel в шаблон (например, `=SUM(B2:B{#})`). SmartMarker сохранит формулу после вставки данных.

## Полный исполняемый пример

Ниже представлена полная программа, которую можно скопировать‑вставить в консольное приложение. Она включает все директивы `using`, модель данных, параметры и работу с файлами.

```csharp
using System;
using System.IO;
using Aspose.Cells;

namespace MasterDetailReportDemo
{
    class Program
    {
        static void Main()
        {
            // ---------- Step 1: Create master‑detail data ----------
            var orderData = new
            {
                Orders = new[]
                {
                    new
                    {
                        Id = 1,
                        Items = new[]
                        {
                            new { Sku = 101, Qty = 2 },
                            new { Sku = 102, Qty = 1 }
                        }
                    },
                    new
                    {
                        Id = 2,
                        Items = new[]
                        {
                            new { Sku = 202, Qty = 1 }
                        }
                    }
                }
            };

            // ---------- Step 2: SmartMarker options ----------
            SmartMarkerOptions options = new SmartMarkerOptions
            {
                MasterDetail = true,
                DetailSheetName = "OrderDetail"
            };

            // ---------- Step 3: Load the template ----------
            string templatePath = Path.Combine(Environment.CurrentDirectory, "template.xlsx");
            Workbook workbook = new Workbook(templatePath);

            // ---------- Step 4: Process the template ----------
            new SmartMarkerProcessor().Process(workbook, orderData, options);

            // ---------- Step 5: Save the result ----------
            string outputPath = Path.Combine(Environment.CurrentDirectory, "output.xlsx");
            workbook.Save(outputPath);

            Console.WriteLine($"Master detail report generated at: {outputPath}");
        }
    }
}
```

Запустите программу, откройте `output.xlsx`, и вы увидите красиво заполненные данные master‑detail.

## Визуальная ссылка

![Скриншот вывода отчёта master detail](https://example.com/images/master-detail-report.png "Пример отчёта master detail")

*На изображении показан лист Orders с идентификаторами 1 и 2, а также лист OrderDetail с тремя строками SKU‑Qty.*

## Заключение

Теперь вы знаете **как создать master detail report** в C# с использованием Aspose.Cells SmartMarker, от построения источника данных до **загрузки книги Excel C#**, **заполнения шаблона Excel**, и наконец

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}