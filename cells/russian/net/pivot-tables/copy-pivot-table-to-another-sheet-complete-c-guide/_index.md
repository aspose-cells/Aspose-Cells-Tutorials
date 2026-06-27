---
category: general
date: 2026-06-27
description: Скопировать сводную таблицу на другой лист в C# с использованием Aspose.Cells.
  Узнайте пошагово, как сохранить данные и форматирование сводной таблицы.
draft: false
keywords:
- copy pivot table to another sheet
- Aspose.Cells copy pivot
- Excel pivot duplication
- preserve pivot formatting
- copy range with pivot
language: ru
og_description: Скопировать сводную таблицу на другой лист в C# с помощью Aspose.Cells.
  Этот учебник точно показывает, как дублировать сводную таблицу, сохраняя её форматирование
  нетронутым.
og_title: Копировать сводную таблицу на другой лист – Полное руководство по C#
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: Copy pivot table to another sheet in C# using Aspose.Cells. Learn step‑by‑step
    how to preserve pivot data and formatting.
  headline: Copy Pivot Table to Another Sheet – Complete C# Guide
  type: TechArticle
tags:
- Excel automation
- C#
- Aspose.Cells
title: Копирование сводной таблицы на другой лист — Полное руководство по C#
url: /ru/net/pivot-tables/copy-pivot-table-to-another-sheet-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Копировать сводную таблицу на другой лист – Полное руководство на C#

Когда‑то вам нужно **скопировать сводную таблицу на другой лист**, но вы боитесь потерять срезы, вычисляемые поля или форматирование? Вы не одиноки. Многие разработчики сталкиваются с этой проблемой при автоматизации отчётов Excel, и раздражение вполне оправдано. В этом руководстве мы пройдём чистое, сквозное решение, которое **сохраняет сводную таблицу** точно в том виде, в каком она выглядит.

Мы будем использовать **Aspose.Cells for .NET**, мощную библиотеку, позволяющую манипулировать файлами Excel без их открытия в самом Excel. К концу этого урока у вас будет готовый фрагмент кода на C#, который копирует сводную таблицу с одного листа на другой, сохраняя все связанные соединения данных.

## Что покрывает данный учебник

- Настройка проекта .NET и добавление пакета Aspose.Cells через NuGet.  
- Загрузка существующей книги, уже содержащей сводную таблицу.  
- Определение как исходного диапазона (исходной сводки), так и диапазона назначения на другом листе.  
- Использование `CopyOptions` для **сохранения сводной таблицы** при копировании.  
- Сохранение результата и проверка, что сводка работает в новом месте.  

Никаких внешних инструментов, никакого ручного копирования‑вставки и скрытой магии — только прямой код, который можно вставить в любое консольное приложение C# или сервис.

> **Почему это важно:** Автоматизация дублирования сводных таблиц экономит часы ручной работы, особенно в ночных конвейерах отчётности, где десятки книг требуют одинаковой структуры сводных таблиц на нескольких листах.

---

## Шаг 1: Настройка проекта и добавление Aspose.Cells

Сначала создайте новый консольный проект .NET, если вы ещё этого не сделали:

```bash
dotnet new console -n PivotCopyDemo
cd PivotCopyDemo
```

Теперь добавьте пакет Aspose.Cells:

```bash
dotnet add package Aspose.Cells
```

> **Pro tip:** Используйте последнюю стабильную версию (на июнь 2026 v23.12). В ней исправлены ошибки обработки `CopyPivotTable`.

## Шаг 2: Загрузка книги и доступ к листам

Откройте книгу, содержащую исходную сводную таблицу. В большинстве реальных сценариев файл находится на общем диске, но для демонстрации будем считать, что он лежит в локальной папке `YOUR_DIRECTORY`.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Load the workbook containing the source pivot table
        Workbook workbook = new Workbook("YOUR_DIRECTORY/source.xlsx");

        // Step 2: Access the first worksheet (source sheet)
        Worksheet sourceSheet = workbook.Worksheets[0];

        // We'll also create (or reference) a destination sheet
        Worksheet destSheet = workbook.Worksheets.Add("CopyDestination");
```

Здесь мы создаём новый лист с именем **CopyDestination**, куда будет помещена копия сводки. Если у вас уже есть целевой лист, просто получите его по индексу или имени.

## Шаг 3: Определение исходного и целевого диапазонов

Сводная таблица располагается внутри прямоугольного блока ячеек. Нужно указать Aspose.Cells, какой блок копировать. В этом примере сводка занимает строки 0‑20 и столбцы 0‑10 (нумерация с нуля).

```csharp
        // Step 3: Define the source range that includes the pivot table (rows 0‑20, columns 0‑10)
        CellArea sourceRange = new CellArea(0, 0, 20, 10);

        // Step 4: Define the destination start cell (row 30, column 0) on the destination sheet
        // and calculate the target area size to match the source dimensions
        CellArea destinationRange = new CellArea(
            30,                                 // start row on destination sheet
            0,                                  // start column
            30 + sourceRange.RowCount - 1,     // end row (same height as source)
            sourceRange.ColumnCount - 1        // end column (same width as source)
        );
```

Обратите внимание, как мы динамически вычисляем конечные строку и столбец. Таким образом, даже если позже вы измените размер исходного диапазона, целевой диапазон подстроится автоматически.

## Шаг 4: Выполнение копирования с сохранением сводной таблицы

Теперь происходит «магия». Передавая объект `CopyOptions` с `CopyPivotTable = true`, Aspose.Cells знает, что нужно сохранить определение сводки.

```csharp
        // Step 5: Copy the range, preserving the pivot table
        destSheet.Cells.CopyRange(
            sourceRange,
            destinationRange,
            new CopyOptions { CopyPivotTable = true }
        );
```

Под капотом Aspose.Cells воссоздаёт кэш сводки, обновляет ссылку на источник данных и повторно применяет форматирование. Это и есть **дублирование сводной таблицы в Excel**, которое вы искали.

## Шаг 5: Сохранение и проверка результата

Наконец, запишите книгу обратно на диск. Вы можете оставить оригинальный файл нетронутым, сохранив под новым именем.

```csharp
        // Step 6: Save the workbook with the copied pivot table
        workbook.Save("YOUR_DIRECTORY/copy-pivot.xlsx");

        // Optional: open the file automatically (Windows only)
        System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo
        {
            FileName = "YOUR_DIRECTORY/copy-pivot.xlsx",
            UseShellExecute = true
        });
    }
}
```

Откройте полученный `copy-pivot.xlsx`, и вы увидите, что сводная таблица полностью воспроизведена на листе **CopyDestination**, вместе со срезами, вычисляемыми полями и форматированием. Источник данных по‑прежнему указывает на оригинальную таблицу, поэтому обновление работает точно так же.

> **Что делать, если исходная сводка охватывает динамический диапазон?**  
> Используйте `Worksheet.PivotTables[0].CacheDefinition.SourceData`, чтобы получить реальные границы, а затем построить `sourceRange` из этой информации. Это покрывает случаи, когда строки или столбцы могут расширяться со временем.

## Бонус: Сохранение форматирования сводной таблицы при копировании

Иногда при обычном копировании теряется условное форматирование или пользовательские числовые форматы. Чтобы этого избежать, расширьте `CopyOptions`:

```csharp
        var options = new CopyOptions
        {
            CopyPivotTable = true,
            CopyFormatting = true,      // copies cell styles, colors, fonts
            CopyConditionalFormatting = true
        };
        destSheet.Cells.CopyRange(sourceRange, destinationRange, options);
```

Включение `CopyFormatting` гарантирует выполнение требования **preserve pivot formatting**, обеспечивая пиксель‑точную копию.

## Ожидаемый результат

При запуске программы консоль завершится без вывода (если не добавить логирование). Открытие `copy-pivot.xlsx` должно показать:

- Лист 1: Исходные данные и сводная таблица без изменений.  
- **CopyDestination**: Точная копия сводки, начинающаяся с строки 31 (поскольку в пользовательском интерфейсе Excel нумерация строк начинается с 1).  
- Все срезы и фильтры работают; нажатие «Refresh» обновит обе сводки одновременно.

---

## Заключение

Мы только что продемонстрировали, как **скопировать сводную таблицу на другой лист** с помощью Aspose.Cells в C#. Шаги — настройка проекта, загрузка книги, определение диапазонов, копирование с `CopyPivotTable = true` и сохранение — образуют надёжный шаблон, который можно переиспользовать в любой автоматизационной цепочке.

Если хотите идти дальше, рассмотрите:

- **Excel pivot duplication** в нескольких книгах (цикл по файлам).  
- Использование опции **Aspose.Cells copy range with pivot** для перемещения сводок между разными книгами.  
- Автоматизацию обновления с помощью `PivotTable.RefreshData()` после копирования.

Экспериментируйте с разными исходными диапазонами или комбинируйте эту технику с генерацией графиков для полностью автоматизированных панелей отчётности. Есть вопросы? Оставляйте комментарий, и удачной разработки!

---

![Screenshot showing copied pivot table in new sheet](copy-pivot-screenshot.png "copy pivot table to another sheet example")


## Что изучать дальше?


Следующие учебники охватывают тесно связанные темы, которые развивают техники, продемонстрированные в этом руководстве. Каждый ресурс включает полностью рабочие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы в собственных проектах.

- [How to Change Pivot Table Source Data Using Aspose.Cells for .NET | Data Analysis Guide](/cells/english/net/data-analysis/change-pivot-table-source-aspose-cells-net/)
- [Master Pivot Table Formatting in .NET Using Aspose.Cells](/cells/english/net/formatting/format-pivot-tables-dotnet-aspose-cells/)
- [Access Pivot Table External Data Sources in .NET using Aspose.Cells](/cells/english/net/data-analysis/access-pivot-table-data-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}