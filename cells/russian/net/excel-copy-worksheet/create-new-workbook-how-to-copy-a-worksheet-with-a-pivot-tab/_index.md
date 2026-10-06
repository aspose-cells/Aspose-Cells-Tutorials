---
category: general
date: 2026-03-01
description: Создайте новую книгу и скопируйте лист в книгу со сводной таблицей. Узнайте,
  как экспортировать сводную таблицу, копировать лист и копировать сводную таблицу
  в C#.
draft: false
keywords:
- create new workbook
- copy worksheet to workbook
- export pivot table
- how to copy sheet
- how to copy pivot
language: ru
og_description: Создайте новую книгу в C# и скопируйте лист в книгу, сохранив сводную
  таблицу. Пошаговое руководство с полным кодом.
og_title: Создать новую книгу — копировать лист и сводную таблицу в C#
tags:
- C#
- Aspose.Cells
- Excel automation
title: Создать новую книгу – Как скопировать лист с сводной таблицей
url: /ru/net/excel-copy-worksheet/create-new-workbook-how-to-copy-a-worksheet-with-a-pivot-tab/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создать новую книгу – копировать лист и сводную таблицу в C#

Когда‑то вам нужно **создать новую книгу**, содержащую готовую сводную таблицу без её воссоздания с нуля? Вы не одиноки. Во многих сценариях отчётности у вас есть основной файл (`src.xlsx`) со сложной сводкой, и вы хотите отправить чистую копию (`dest.xlsx`) клиенту или в другую систему. Хорошая новость? Это можно сделать всего в две строки C# — и в этом руководстве мы покажем, как именно.

Мы пройдём весь процесс: загрузим исходную книгу, скопируем первый лист (на котором находится сводная таблица) и сохраним её как совершенно новую книгу. К концу вы узнаете, **как скопировать лист**, содержащий сводную таблицу, **как экспортировать данные сводной таблицы**, если это необходимо, а также несколько приёмов для особых случаев, например копирование в существующий файл.

## Требования

- .NET 6.0 или новее (подойдёт любая актуальная версия)
- Aspose.Cells for .NET (бесплатная пробная версия или лицензия) — эта библиотека предоставляет класс `Workbook`, используемый ниже.
- Исходный Excel‑файл (`src.xlsx`), уже содержащий сводную таблицу на первом листе.

Если у вас ещё нет Aspose.Cells, добавьте её через NuGet:

```bash
dotnet add package Aspose.Cells
```

Вот и всё — без дополнительного COM‑interop, без установки Excel на сервер.

## Что покрывает этот учебник

- **Создать новую книгу** из существующего листа, содержащего сводную таблицу.
- **Копировать лист в книгу**, сохраняя все определения сводных таблиц.
- **Экспортировать данные сводной таблицы** в `DataTable` (по желанию).
- Распространённые подводные камни при использовании **как скопировать сводную** в разных средах.
- Полный, готовый к запуску пример, который можно вставить в консольное приложение.

---

## Шаг 1: Загрузка исходной книги (Как скопировать лист)

Первое, что нужно сделать, — открыть книгу, содержащую сводную таблицу. Aspose.Cells делает это без проблем, потому что читает файл в память без запуска Excel.

```csharp
using Aspose.Cells;
using System;
using System.Data;

class Program
{
    static void Main()
    {
        // Path to the source workbook that holds the pivot
        string srcPath = @"YOUR_DIRECTORY\src.xlsx";

        // Load the workbook – this is where we **create new workbook** later
        Workbook sourceWorkbook = new Workbook(srcPath);
```

> **Почему это важно:** Загрузка файла проверяет наличие сводной таблицы и даёт доступ к коллекции листов. Если файл повреждён, `Workbook` бросит понятное исключение, спасая от загадочных результатов позже.

## Шаг 2: Копирование листа в новую книгу (Copy Worksheet to Workbook)

Теперь мы действительно **копируем лист в книгу**. Метод `CopyTo` из Aspose.Cells клонирует весь лист — включая формулы, форматирование и кэш сводной таблицы — в новый файл.

```csharp
        // Destination path for the new workbook
        string destPath = @"YOUR_DIRECTORY\dest.xlsx";

        // Copy the first worksheet (index 0) which contains the pivot
        sourceWorkbook.Worksheets[0].CopyTo(destPath);
```

> **Совет:** `CopyTo` создаёт совершенно новую книгу «за кулисами», поэтому не требуется создавать отдельный объект `Workbook`. Это снижает потребление памяти и гарантирует, что определение сводной таблицы останется нетронутым.

## Шаг 3: Проверка скопированной сводной (How to Copy Pivot)

После завершения копирования рекомендуется открыть новый файл и убедиться, что сводная таблица работает. Это можно сделать программно или просто открыть файл в Excel.

```csharp
        // Optional: Load the destination workbook to verify
        Workbook destWorkbook = new Workbook(destPath);
        Worksheet copiedSheet = destWorkbook.Worksheets[0];

        // Find the first pivot table on the copied sheet
        PivotTable pivot = copiedSheet.PivotTables[0];

        Console.WriteLine($"Pivot name: {pivot.Name}");
        Console.WriteLine($"Data source range: {pivot.DataSource}");
        Console.WriteLine($"Number of rows in pivot cache: {pivot.CacheDefinition.RecordCount}");
    }
}
```

Запуск программы выводит примерно следующее:

```
Pivot name: PivotTable1
Data source range: A1:D100
Number of rows in pivot cache: 100
```

Если вы видите эти значения, шаг **как скопировать сводную** выполнен успешно.

## Шаг 4: (Опционально) Экспорт данных сводной таблицы в `DataTable`

Иногда нужны «сырьё» из сводной таблицы без открытия Excel. Aspose.Cells позволяет извлечь данные сводки в `DataTable` — идеально для дальнейшей обработки или ответов API.

```csharp
        // Export pivot data to a DataTable
        DataTable pivotData = pivot.ExportDataTable(pivot.RowFields[0].Name, 
                                                   pivot.ColumnFields[0].Name,
                                                   true);

        // Display a few rows in the console
        foreach (DataRow row in pivotData.Rows)
        {
            Console.WriteLine(string.Join("\t", row.ItemArray));
        }
```

> **Зачем это может понадобиться:** Экспорт позволяет **экспортировать сводную таблицу** в базу данных, JSON‑payload или любой другой формат без ручного копирования‑вставки.

## Шаг 5: Особые случаи и типичные подводные камни

### Копирование в существующую книгу

Если нужно **скопировать лист в книгу**, в которой уже есть другие листы, используйте перегрузку, принимающую целевой объект `Workbook`:

```csharp
        Workbook targetWorkbook = new Workbook(); // empty workbook
        sourceWorkbook.Worksheets[0].CopyTo(targetWorkbook);
        targetWorkbook.Save(@"YOUR_DIRECTORY\combined.xlsx");
```

### Сохранение внешних источников данных

Сводные таблицы, получающие данные из внешних соединений (например, Power Query), могут потерять связь после копирования. В таких случаях перед сохранением установите `pivot.RefreshDataOnOpen = true`:

```csharp
        pivot.RefreshDataOnOpen = true;
```

### Большие файлы и производительность

Для файлов более 50 МБ рекомендуется включить `WorkbookSettings.MemorySetting = MemorySetting.MemoryPreference;`, чтобы снизить нагрузку на память.

---

![Пример создания новой книги](https://example.com/images/create-new-workbook.png "Создание новой книги")

*Текст alt: пример создания новой книги – копирование листа со сводной таблицей*

---

## Полный рабочий пример (Все шаги вместе)

Ниже представлен полностью готовый к запуску консольный приложение. Скопируйте‑вставьте его в новый `.csproj` и нажмите **F5**.

```csharp
using Aspose.Cells;
using System;
using System.Data;

namespace CopyPivotDemo
{
    class Program
    {
        static void Main()
        {
            // ==============================
            // 1️⃣ Load the source workbook
            // ==============================
            string srcPath = @"YOUR_DIRECTORY\src.xlsx";
            Workbook sourceWorkbook = new Workbook(srcPath);

            // ==============================
            // 2️⃣ Copy the first worksheet (pivot) to a new workbook
            // ==============================
            string destPath = @"YOUR_DIRECTORY\dest.xlsx";
            sourceWorkbook.Worksheets[0].CopyTo(destPath);

            // ==============================
            // 3️⃣ Verify the copied pivot (how to copy pivot)
            // ==============================
            Workbook destWorkbook = new Workbook(destPath);
            Worksheet copiedSheet = destWorkbook.Worksheets[0];
            PivotTable pivot = copiedSheet.PivotTables[0];

            Console.WriteLine($"Pivot name: {pivot.Name}");
            Console.WriteLine($"Data source range: {pivot.DataSource}");
            Console.WriteLine($"Cache rows: {pivot.CacheDefinition.RecordCount}");

            // ==============================
            // 4️⃣ (Optional) Export pivot data
            // ==============================
            if (pivot.RowFields.Count > 0 && pivot.ColumnFields.Count > 0)
            {
                DataTable dt = pivot.ExportDataTable(
                    pivot.RowFields[0].Name,
                    pivot.ColumnFields[0].Name,
                    true);

                Console.WriteLine("\n--- Pivot Data Preview ---");
                foreach (DataRow row in dt.Rows)
                {
                    Console.WriteLine(string.Join("\t", row.ItemArray));
                }
            }

            Console.WriteLine("\nDone! New workbook created at: " + destPath);
        }
    }
}
```

### Ожидаемый результат

- `dest.xlsx` появляется в `YOUR_DIRECTORY`.
- Первый лист выглядит точно так же, как оригинал, со сводной таблицей.
- При запуске консоли выводятся метаданные сводной и небольшой предварительный просмотр данных, подтверждая успешное копирование.

---

## Заключение

Теперь вы знаете, как **создать новую книгу**, копируя лист со сводной таблицей, как **скопировать лист в книгу**, а также как **экспортировать сводную таблицу** для последующей обработки. Независимо от того, создаёте ли вы сервис отчётности, автоматизируете распределение Excel‑файлов или просто хотите быстро дублировать сводку, описанные шаги дают надёжное, готовое к продакшену решение.

**Следующие шаги**, которые стоит изучить:

- Объединять несколько листов (использовать `CopyTo` последовательно) — идеально для упаковки полного отчёта.
- Настраивать параметры обновления кэша сводных таблиц при изменении исходных данных.
- Применять техники **как скопировать лист** для дублирования диаграмм, изображений или модулей VBA.
- Погрузиться в `WorkbookDesigner` от Aspose.Cells для генерации отчётов на основе шаблонов.

Попробуйте, измените пути и убедитесь, как легко доставлять чистые, готовые к использованию книги со сводными таблицами. Есть вопросы о особых случаях или лицензировании? Оставляйте комментарий ниже, и счастливого кодинга!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}