---
category: general
date: 2026-09-15
description: Создайте книгу Excel на C# и узнайте, как сохранить её в PDF, разливая
  динамические массивы с помощью функции EXPAND.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- save workbook as pdf
- spill dynamic array
- use expand function
- how to create dynamic array in excel
language: ru
lastmod: 2026-09-15
og_description: Создайте книгу Excel на C# и быстро сохраните её в PDF, используя
  функцию EXPAND для вывода динамического массива.
og_image_alt: Create Excel workbook screenshot showing dynamic array and PDF output
og_title: Создайте книгу Excel и сохраните её в PDF с динамическими массивами
schemas:
- author: Aspose
  dateModified: '2026-09-15'
  description: Create Excel workbook in C# and learn how to save workbook as PDF while
    spilling dynamic arrays using the EXPAND function.
  headline: Create Excel workbook and save as PDF with dynamic arrays
  type: TechArticle
tags:
- excel
- csharp
- aspose-cells
- pdf
- dynamic-array
title: Создать книгу Excel и сохранить её в PDF с динамическими массивами
url: /ru/net/conversion-to-pdf/create-excel-workbook-and-save-as-pdf-with-dynamic-arrays/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание рабочей книги Excel и сохранение её в PDF с динамическими массивами

Если вам нужно **программно создать рабочую книгу Excel** и затем **сохранить её как PDF**, это руководство покажет полное решение от начала до конца на C#. Вы также увидите, как **разлить результаты динамического массива** с помощью **функции EXPAND**, которая является современным способом создания массивов без VBA.  

Независимо от того, создаёте ли вы сервис отчётности, функцию экспорта для ERP‑системы или аналитическую панель, нижеописанные шаги позволят вам сгенерировать книгу, заполнить её данными Smart‑Marker и получить PDF, сохраняющий расширенные возможности шрифтов.

## Требования

Прежде чем начать, убедитесь, что у вас есть:

* .NET 6.0 или новее (код также работает с .NET Framework 4.8)
* Последняя версия **Aspose.Cells for .NET** (v25.8 или новее) — предоставляет `Workbook`, `PdfSaveOptions` и `SmartMarkerProcessor`.
* IDE, например Visual Studio 2022 (подойдёт любой редактор, способный компилировать C#).

Добавьте пакет NuGet в ваш проект:

```bash
dotnet add package Aspose.Cells --version 25.8
```

## Шаг 1: Создать рабочую книгу Excel и настроить первый лист

Первая задача — **создать рабочую книгу Excel** и получить ссылку на лист по умолчанию. Этот лист будет содержать динамический массив и шаблон Smart Marker.

```csharp
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;
using System;

class Program
{
    static void Main()
    {
        // Create a new workbook in memory
        Workbook wb = new Workbook();

        // Get the first (default) worksheet
        Worksheet ws = wb.Worksheets[0];
```

*Почему это важно*: Создание экземпляра `Workbook` выделяет внутреннюю структуру книги, а обращение к `Worksheets[0]` даёт готовый к использованию лист без необходимости добавлять его вручную.

## Шаг 2: Разлить динамический массив с помощью функции EXPAND

**Функция EXPAND** в Excel может превратить статический массив‑литерал в диапазон‑разлив любого размера. Здесь мы просим Excel разлить `{1,2,3}` в диапазон 5 строк × 1 столбца, начиная с `A1`.

```csharp
        // Write the EXPAND formula into A1
        ws.Cells["A1"].Formula = "=EXPAND({1,2,3},5,1)";

        // Force calculation so the spill occurs immediately
        ws.Calculate();
```

*Почему это важно*: Использование `EXPAND` избавляет от ручных циклов в C#. Движок вычисляет диапазон‑разлив и сохраняет значения непосредственно в лист, которые позже отобразятся в PDF.

## Шаг 3: Сохранить рабочую книгу как PDF с сохранением селекторов вариаций шрифта

Когда необходимо **сохранить рабочую книгу как PDF**, вы также можете включить расширенные типографские возможности, такие как селекторы вариаций шрифта (доступны, начиная с Aspose.Cells v25.8). Это гарантирует корректный рендеринг сложных скриптов в PDF.

```csharp
        // Configure PDF options
        PdfSaveOptions pdfOpts = new PdfSaveOptions
        {
            FontVariationSelectors = true   // keeps variation selectors for OpenType fonts
        };

        // Save the current workbook (with the spilled array) as PDF
        wb.Save(@"YOUR_DIRECTORY\VarSelector.pdf", pdfOpts);
```

*Почему это важно*: Установка `FontVariationSelectors` в `true` необходима для языков, использующих глиф‑вариации (например, китайский, японский, эмодзи). Полученный PDF точно повторяет отображение в Excel.

## Шаг 4: Вставить шаблон Smart Marker, ссылающийся на вложенный источник данных

Smart Markers позволяют встраивать заполнители непосредственно в лист. Шаблон ниже сгенерирует список заказов и их позиций.

```csharp
        // Define a Smart Marker template in cell A1
        string template = "${Orders.OrderId}\n${Orders.Items:ItemName}\n";
        ws.Cells["A1"].PutValue(template);
```

*Почему это важно*: Размещая шаблон в `A1`, вы указываете Aspose.Cells, где начинать разлив данных. Синтаксис `:` (`Items:ItemName`) сообщает процессору итерировать вложенную коллекцию.

## Шаг 5: Определить вложенный источник данных (заказы с позициями)

Мы создаём анонимный массив заказов, каждый из которых содержит собственную коллекцию объектов‑товаров. Это типичный сценарий «мастер‑деталь».

```csharp
        // Sample nested data source
        var orders = new[]
        {
            new
            {
                OrderId = 1,
                Items = new[]
                {
                    new { ItemName = "Apple" },
                    new { ItemName = "Banana" }
                }
            },
            new
            {
                OrderId = 2,
                Items = new[]
                {
                    new { ItemName = "Carrot" }
                }
            }
        };
```

*Почему это важно*: Вложенная структура демонстрирует **как создать динамический массив в Excel** через Smart Markers без написания VBA или ручных циклов по ячейкам.

## Шаг 6: Обработать Smart Markers и сохранить окончательный файл Excel

Теперь передаём рабочую книгу и источник данных в `SmartMarkerProcessor`. После обработки заполнители заменяются реальными строками, и мы сохраняем результат как обычный файл `.xlsx`.

```csharp
        // Process the Smart Markers
        SmartMarkerProcessor processor = new SmartMarkerProcessor();
        processor.Process(wb, orders);

        // Save the populated workbook
        wb.Save(@"YOUR_DIRECTORY\NestedSmartMarker.xlsx");
    }
}
```

*Почему это важно*: `SmartMarkerProcessor` автоматически разливает шаблон, создаёт необходимые строки и заполняет их данными. Финальную книгу можно открыть в Excel, чтобы убедиться, что каждый заказ и его позиции отображаются корректно.

## Ожидаемый результат

* **VarSelector.pdf** — PDF‑файл, в котором числа 1‑3 разливаются вниз на пять строк, отображаясь с любыми включёнными вариациями OpenType‑шрифта.
* **NestedSmartMarker.xlsx** — файл Excel со следующими строками (начиная с `A1`):

| OrderId | ItemName |
|---------|----------|
| 1       | Apple    |
| 1       | Banana   |
| 2       | Carrot   |

PDF‑версия сохраняет тот же разлив чисел, потому что состояние листа было сохранено до обработки Smart Marker; при необходимости можно выполнить сохранение PDF после обработки, чтобы получить финальные данные в PDF.

## Полезные советы и распространённые подводные камни

| Совет | Пояснение |
|-----|-------------|
| **Повторно используйте один объект `PdfSaveOptions`** | Создание объекта параметров один раз и его повторное использование избавляет от тонких различий в рендеринге (например, отсутствие селекторов вариаций). |
| **Вызовите `ws.Calculate()` после установки формул** | Без явного расчёта диапазон‑разлив может остаться пустым при программном просмотре книги. |
| **Размещайте шаблоны Smart Marker на чистом листе** | Смешивание шаблонов с существующими данными может вызвать неожиданную вставку строк. По возможности используйте отдельный лист. |
| **Следите за путями к файлам** | Используйте `Path.Combine(Environment.CurrentDirectory, "output.pdf")`, чтобы избежать жёстко заданных каталогов на разных машинах. |
| **Проверка версии** | `FontVariationSelectors` доступен только, начиная с версии 25.8; более старые версии просто игнорируют свойство без исключения. |

## Следующие шаги

Теперь, когда вы знаете, как **создать рабочую книгу Excel**, **разлить динамический массив** и **сохранить книгу как PDF**, вы можете исследовать:

* Добавление диаграмм или изображений перед конвертацией в PDF.
* Экспорт той же книги в другие форматы (например, HTML, CSV) с помощью перегрузок `Save`.
* Использование **выражений Smart Marker** (`${Orders.Total:SUM(Items.Price)}`) для вычисления агрегатов «на лету».
* Интеграцию этого кода в ASP.NET Core API, чтобы пользователи могли напрямую скачивать сгенерированный PDF через веб‑конечную точку.

---

**Итоги** – В этом руководстве вы узнали, как **создать рабочую книгу Excel**, использовать **функцию EXPAND** для **разлива динамического массива**, внедрить **Smart Marker**, работающий с вложенным источником данных, и, наконец, **сохранить книгу как PDF**, сохраняя расширенные возможности шрифтов. Полный, готовый к запуску пример можно скопировать в любой C#‑проект и адаптировать под свои структуры данных. Приятного кодинга!


## Что изучать дальше?


Следующие руководства охватывают тесно связанные темы, расширяющие техники, продемонстрированные в этом пособии. Каждый ресурс содержит полностью работающие примеры кода с пошаговыми объяснениями, помогающие освоить дополнительные возможности API и исследовать альтернативные подходы в ваших проектах.

- [Create and Save Excel Workbook as PDF in ASP.NET Using Aspose.Cells](/cells/english/net/workbook-operations/create-save-excel-workbook-pdf-aspnet-aspose-cells/)
- [How to Create and Save an Excel Workbook as ODS Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [How to Create and Save an Excel Workbook as SVG using Aspose.Cells for Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}