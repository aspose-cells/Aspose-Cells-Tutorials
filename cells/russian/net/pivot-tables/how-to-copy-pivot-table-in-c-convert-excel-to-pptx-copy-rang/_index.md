---
category: general
date: 2026-01-14
description: Как скопировать сводную таблицу с помощью Aspose.Cells и также узнать,
  как конвертировать Excel в PPTX, копировать диапазон в другую книгу и сделать текстовое
  поле редактируемым в PPTX в одном руководстве.
draft: false
keywords:
- how to copy pivot table
- convert excel to pptx
- copy range to another workbook
- make textbox editable pptx
- save workbook as pptx
language: ru
og_description: Как скопировать сводную таблицу, затем преобразовать Excel в PPTX,
  скопировать диапазон в другую книгу и сделать текстовое поле редактируемым в PPTX
  — всё с помощью Aspose.Cells.
og_title: Как скопировать сводную таблицу в C# – Полное руководство по работе с Excel
  и PPTX
tags:
- Aspose.Cells
- C#
- Excel automation
- PowerPoint export
title: Как скопировать сводную таблицу в C# – преобразовать Excel в PPTX, скопировать
  диапазон и сделать текстовое поле редактируемым
url: /ru/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как скопировать сводную таблицу в C# – Полное руководство по Excel в PPTX

Как скопировать сводную таблицу из одной книги в другую – частый вопрос при автоматизации отчетов на основе Excel. В этом руководстве мы рассмотрим три реальных сценария с использованием **Aspose.Cells for .NET**: копирование диапазона со сводной таблицей, экспорт листа в файл PPTX с редактируемым текстовым полем и заполнение одной ячейки массивом JSON через Smart Markers.  

Вы также увидите, как **конвертировать Excel в PPTX**, **скопировать диапазон в другую книгу**, и **сделать текстовое поле редактируемым в PPTX**, не нарушая форматирование. К концу вы получите готовый к запуску код, который можно вставить в любой .NET‑проект.

> **Pro tip:** Все примеры ориентированы на Aspose.Cells 23.12, но те же концепции применимы к более ранним версиям с небольшими изменениями API.

![Diagram showing how a pivot table is copied, a worksheet exported to PPTX, and a JSON array inserted – how to copy pivot table workflow](how-to-copy-pivot-table-diagram.png)

---

## Что понадобится

- Visual Studio 2022 (или любой IDE для C#)  
- .NET 6.0 или более поздняя версия runtime  
- NuGet‑пакет Aspose.Cells for .NET  
  ```bash
  dotnet add package Aspose.Cells
  ```  
- Два образцовых файла Excel (`source.xlsx`, `chartWithTextbox.xlsx`), размещённые в папке, которой вы управляете (замените `YOUR_DIRECTORY` на ваш реальный путь).

Никакие дополнительные библиотеки не требуются; сборка `Aspose.Cells` сама обрабатывает Excel, PPTX и Smart Markers.

---

## Как скопировать сводную таблицу и сохранить её данные

При копировании диапазона, содержащего сводную таблицу, по умолчанию вставляются только **значения**. Чтобы сохранить определение сводной таблицы, необходимо включить флаг `CopyPivotTable`.

### Пошагово

1. **Загрузите исходную книгу**, в которой находится сводная таблица.  
2. **Создайте пустую целевую книгу** – в неё будет скопирован диапазон.  
3. **Вызовите `CopyRange` с `CopyPivotTable = true`**, чтобы определение сводной таблицы перешло вместе с данными.  
4. **Сохраните целевой файл** в нужном месте.

#### Полный пример кода

```csharp
using Aspose.Cells;

class PivotCopyDemo
{
    static void Main()
    {
        // Step 1: Load the source workbook and define the range to copy
        Workbook sourceWorkbook = new Workbook(@"YOUR_DIRECTORY\source.xlsx");
        Worksheet sourceSheet = sourceWorkbook.Worksheets[0];
        // Assuming the pivot table lives inside A1:G20
        Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");

        // Step 2: Create a destination workbook (blank)
        Workbook destinationWorkbook = new Workbook();
        Worksheet destinationSheet = destinationWorkbook.Worksheets[0];

        // Step 3: Copy the range, preserving the pivot table
        destinationSheet.Cells.CopyRange(
            sourceRange,
            "B2", // paste start cell
            new CopyOptions { CopyPivotTable = true });

        // Step 4: Save the result
        destinationWorkbook.Save(@"YOUR_DIRECTORY\copyWithPivot.xlsx");
    }
}
```

**Почему это работает:**  
`CopyOptions.CopyPivotTable` указывает Aspose.Cells клонировать объект `PivotTable`, а не только его отрисованные значения. В целевой книге теперь находится полностью функциональная сводная таблица, которую можно обновлять или изменять программно.

**Особый случай:** Если исходная книга использует внешние источники данных, после копирования может потребоваться встроить данные или скорректировать строки подключения, иначе сводная таблица покажет “#REF!”.

---

## Конвертировать Excel в PPTX и сделать текстовое поле редактируемым

Экспорт листа в PowerPoint удобен для создания презентаций непосредственно из данных. По умолчанию экспортируемое текстовое поле становится статической фигурой, но установка `IsTextBoxEditable` меняет это поведение.

### Пошагово

1. **Откройте книгу**, содержащую диаграмму и текстовое поле, которое нужно экспортировать.  
2. **Настройте `ImageOrPrintOptions`** с `SaveFormat = SaveFormat.Pptx`.  
3. **Определите область печати**, включающую текстовое поле.  
4. **Включите `IsTextBoxEditable`**, чтобы текст можно было редактировать после открытия PPTX.  
5. **Сохраните файл PPTX**.

#### Полный пример кода

```csharp
using Aspose.Cells;

class ExcelToPptxDemo
{
    static void Main()
    {
        // Step 1: Load the workbook with chart and textbox
        Workbook chartWorkbook = new Workbook(@"YOUR_DIRECTORY\chartWithTextbox.xlsx");

        // Step 2: Set export options for PPTX
        ImageOrPrintOptions pptxOptions = new ImageOrPrintOptions
        {
            SaveFormat = SaveFormat.Pptx
        };

        // Step 3: Define the print area that captures the textbox (A1:D20)
        chartWorkbook.Worksheets[0].PageSetup.PrintArea = "A1:D20";

        // Step 4: Make the textbox editable in the exported PPTX
        chartWorkbook.Worksheets[0].PageSetup.IsTextBoxEditable = true;

        // Step 5: Export the worksheet to a PPTX file
        chartWorkbook.Save(@"YOUR_DIRECTORY\result.pptx", pptxOptions);
    }
}
```

**Результат:** Откройте `result.pptx` в PowerPoint – текстовое поле, размещённое в Excel, теперь будет обычным редактируемым текстовым блоком. Нет необходимости воссоздавать его вручную.

**Распространённая ошибка:** Если на листе есть объединённые ячейки, пересекающие область печати, получившийся слайд может сместиться. Скорректируйте область печати или разъедините ячейки перед экспортом.

---

## Копировать диапазон в другую книгу с помощью Smart Markers (JSON → одна ячейка)

Иногда требуется поместить массив JSON в одну ячейку Excel, например, при передаче данных в downstream‑системы, ожидающие строку JSON. Smart Markers Aspose.Cells могут сериализовать массив в одну ячейку, если установить `ArrayAsSingle = true`.

### Пошагово

1. **Загрузите шаблон книги**, содержащий маркер Smart Marker (например, `&=Items.Name`).  
2. **Подготовьте объект данных** – анонимный тип с массивом `Items`.  
3. **Создайте `SmartMarkerProcessor`** и примените данные с `ArrayAsSingle`.  
4. **Сохраните заполненную книгу**.

#### Полный пример кода

```csharp
using Aspose.Cells;
using System;

class SmartMarkerDemo
{
    static void Main()
    {
        // Step 1: Load the template workbook containing a smart marker like "&=Items.Name"
        Workbook templateWorkbook = new Workbook(@"YOUR_DIRECTORY\SmartMarkerTemplate.xlsx");

        // Step 2: Prepare the data object with an array of items
        var data = new
        {
            Items = new[]
            {
                new { Name = "A" },
                new { Name = "B" }
            }
        };

        // Step 3: Apply the SmartMarkerProcessor with ArrayAsSingle option
        SmartMarkerProcessor processor = new SmartMarkerProcessor(templateWorkbook);
        processor.Apply(data, new SmartMarkerOptions { ArrayAsSingle = true });

        // Step 4: Save the result – the JSON array will appear in a single cell
        templateWorkbook.Save(@"YOUR_DIRECTORY\jsonSingleCell.xlsx");
    }
}
```

**Пояснение:**  
Когда `ArrayAsSingle` равно true, Aspose.Cells конкатенирует каждый элемент `Items.Name` в строку в стиле JSON (`["A","B"]`) и записывает её в ячейку, где находился маркер. Это избавляет от создания отдельной строки для каждого элемента массива.

**Когда использовать:** Идеально подходит для экспорта таблиц конфигураций, полезных нагрузок API или любых сценариев, где потребитель ожидает компактную строку JSON вместо табличного представления.

---

## Дополнительные советы и обработка граничных случаев

| Сценарий | На что обратить внимание | Предлагаемое решение |
|----------|--------------------------|----------------------|
| **Большие сводные таблицы** | Пиковое потребление памяти при копировании огромных кэшей. | Установите `WorkbookSettings.MemorySetting = MemorySetting.MemoryPreference` перед загрузкой. |
| **Экспорт в PPTX с изображениями** | Изображения могут быть растровыми с низким DPI. | Задайте `pptxOptions.ImageResolution = 300` для более чётких слайдов. |
| **Форматирование JSON в Smart Marker** | Специальные символы (`"` , `\`) ломают JSON. | Экранируйте их вручную или используйте `JsonSerializer` для предварительной сериализации перед передачей в Smart Markers. |
| **Копирование диапазона между разными версиями Excel** | Старые файлы `.xls` могут потерять форматирование. | Сохраняйте цель как `.xlsx`, чтобы сохранить современные возможности. |

---

## Итоги – Как скопировать сводную таблицу и сделать гораздо больше

Мы начали с ответа на вопрос **как скопировать сводную таблицу**, сохранив её функциональность, затем показали, как **конвертировать Excel в PPTX**, **сделать текстовое поле редактируемым в PPTX**, и наконец, как **скопировать диапазон в другую книгу** с помощью Smart Markers для вставки массива JSON в одну ячейку.  

Все три фрагмента кода автономны; их можно вставить в новый консольный проект, скорректировать пути к файлам и запустить уже сегодня.

---

## Что дальше?

- **Исследуйте другие форматы экспорта** – Aspose.Cells также поддерживает PDF, XPS и HTML.  
- **Обновляйте сводные таблицы программно** с помощью `PivotTable.RefreshData()` после копирования.  
- **Комбинируйте Smart Markers с диаграммами** для создания динамических дашбордов, обновляемых автоматически.  

Если вас интересует **сохранение книги как PPTX** с пользовательскими макетами слайдов, ознакомьтесь с документацией Aspose.Cells по `SlideOptions`.  

Экспериментируйте — меняйте область печати, пробуйте разные `CopyOptions` или передавайте более сложный JSON‑payload. API достаточно гибок для большинства конвейеров отчётности.

---

### Часто задаваемые вопросы

**В: Копирует ли `CopyPivotTable` также слайсеры?**  
О: Не напрямую. Слайсеры — отдельные объекты; после копирования их нужно воссоздать или скопировать через коллекцию `Worksheet.Shapes`.

**В: Можно ли экспортировать несколько листов в одну PPTX‑презентацию?**  
О: Да. Пройдитесь в цикле по каждому листу, вызывайте `Save` с теми же `ImageOrPrintOptions` и задайте `pptxOptions.StartSlideNumber`, чтобы продолжить нумерацию.

**В: Что делать, если мой массив JSON содержит вложенные объекты?**  
О: Установите `ArrayAsSingle = false` и используйте пользовательский шаблон, который будет итерировать вложенные структуры.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}