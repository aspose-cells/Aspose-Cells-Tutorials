---
category: general
date: 2026-03-29
description: Узнайте, как быстро вставлять строки в GridJs. Это руководство также
  охватывает добавление строк и добавление нескольких строк в сетку с помощью пакетной
  операции.
draft: false
keywords:
- how to insert rows
- how to add rows
- add multiple rows grid
- batch row insertion
- large grid performance
language: ru
og_description: Узнайте, как быстро вставлять строки в GridJs. Это руководство показывает,
  как добавлять строки, добавлять несколько строк в сетку и обрабатывать крупные пакетные
  вставки.
og_title: Как вставлять строки в GridJs – эффективно добавлять несколько строк в таблицу
tags:
- GridJs
- C#
- data‑grid
title: Как вставлять строки в GridJs – эффективно добавлять несколько строк в таблицу
url: /ru/net/row-and-column-management/how-to-insert-rows-in-gridjs-add-multiple-rows-grid-efficien/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как вставлять строки в GridJs – Эффективное добавление нескольких строк в сетку

Когда‑нибудь задумывались **как вставлять строки** в огромную таблицу GridJs, не замораживая интерфейс? Возможно, вы столкнулись с проблемой при попытке **добавлять строки** по одной, и производительность резко падает. Хорошая новость в том, что GridJs предоставляет пакетный API, позволяющий **добавлять несколько строк в сетку** одним вызовом, сохраняя отзывчивость даже при работе с миллионами записей.

В этом руководстве мы пройдём полный, готовый к запуску пример, показывающий **как вставлять строки** с помощью `InsertRowsBatch`. Вы узнаете, почему пакетная обработка важна, как проверить результат и на что обратить внимание, когда целевой индекс огромен. К концу вы сможете без труда добавить тысячу новых записей в любой экземпляр GridJs.

## Prerequisites

Прежде чем погрузиться в детали, убедитесь, что у вас есть:

- .NET 6.0 или новее (код компилируется любой современной SDK)
- Ссылка на пакет NuGet `GridJs` (или DLL, если вы используете собственную сборку)
- Базовые знания C# – не требуется быть гуру, достаточно уверенно работать с классами и методами
- IDE или редактор по вашему выбору (Visual Studio, Rider, VS Code… всё подходит)

> **Pro tip:** Если планируете работать с действительно массивными сетками (десятки миллионов строк), включите `gridJs.EnableVirtualization = true;`, чтобы облегчить рендеринг UI.

## Step 1: Create and Configure the GridJs Instance

Первое, что нужно сделать: получить живой объект `GridJs`. Представьте его как холст, на котором вы будете «рисовать» строки.

```csharp
using System;
using GridJsLibrary;   // Assume this is the namespace for GridJs

namespace GridJsDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1 – Initialize the grid
            GridJs gridJs = new GridJs();

            // Optional: turn on virtualization for huge data sets
            gridJs.EnableVirtualization = true;

            // Populate the grid with some dummy data so we can see the effect
            SeedInitialData(gridJs);

            // Now we’re ready to insert rows in bulk
            InsertRowsInBatch(gridJs);
        }

        // Helper: add 2 000 000 rows so our batch lands at index 2 000 001
        static void SeedInitialData(GridJs grid)
        {
            for (int i = 0; i < 2_000_000; i++)
            {
                grid.InsertRow(i, new object[] { $"Row {i + 1}", DateTime.Now });
            }
            Console.WriteLine("Initial seed completed – 2 000 000 rows present.");
        }
```

> **Why this step matters:** Инициализация сетки и, при необходимости, заполнение её данными имитируют реальный сценарий, когда сетка уже содержит большой объём информации. Пакетная вставка, которую мы выполнем позже, должна учитывать нулевой базовый индекс, поэтому мы предварительно заполняем данные, чтобы продемонстрировать точку вставки.

## Step 2: Use `InsertRowsBatch` to **Add Multiple Rows Grid**

Теперь к основной части руководства – вызову, который действительно **добавляет строки** пакетно. Сигнатура метода выглядит так: `InsertRowsBatch(int startIndex, int count)`. В нашем примере мы начинаем с индекса 2 000 000 (это 2 000 001‑я строка) и добавляем десять строк.

```csharp
        // Step 2 – Insert a batch of rows
        static void InsertRowsInBatch(GridJs grid)
        {
            int startIndex = 2_000_000; // zero‑based, so this is row 2 000 001
            int rowsToAdd = 10;

            // The batch call creates placeholder rows; you can later populate them
            grid.InsertRowsBatch(startIndex, rowsToAdd);
            Console.WriteLine($"Inserted {rowsToAdd} rows starting at index {startIndex + 1}.");

            // Verify by reading back a few rows
            VerifyInsertion(grid, startIndex, rowsToAdd);
        }
```

> **How it works:** `InsertRowsBatch` выделяет требуемое количество строк внутри и сдвигает существующие строки вниз. Поскольку операция выполняется в одной транзакции, UI обновляется лишь один раз, что делает этот метод рекомендуемым способом **как добавить строки** эффективно.

## Step 3: Verify the Insertion – Did the Rows Land Where Expected?

После пакетной операции вам понадобится убедиться, что строки находятся там, где вы ожидаете. Ниже приведён вспомогательный код, который читает первую и последнюю строки только что добавленного блока и выводит их в консоль.

```csharp
        // Step 3 – Simple verification
        static void VerifyInsertion(GridJs grid, int startIdx, int count)
        {
            Console.WriteLine("Verifying inserted rows:");
            for (int i = 0; i < count; i++)
            {
                var row = grid.GetRow(startIdx + i);
                Console.WriteLine($"Row {startIdx + i + 1}: {string.Join(", ", row)}");
            }
        }
    }
}
```

**Expected output**

```
Initial seed completed – 2 000 000 rows present.
Inserted 10 rows starting at index 2000001.
Verifying inserted rows:
Row 2000001: , 
Row 2000002: , 
...
Row 2000010: , 
```

Пустые ячейки означают, что строки являются заполнителями, ожидающими данные. Теперь их можно заполнять по отдельности или выполнить ещё одну пакетную операцию обновления.

> **Edge case note:** Если `startIndex` превышает текущий счётчик строк, GridJs автоматически добавит новые строки в конец. Обратное, отрицательный индекс вызовет `ArgumentOutOfRangeException`, поэтому всегда проверяйте индексы, полученные от пользователя.

## Step 4: Populate the New Rows (Optional but Common)

Часто требуется не просто пустые строки, а заполнить их осмысленными значениями. Можно пройтись по только что созданному диапазону и вызвать `SetCell` или аналогичный API.

```csharp
        // Optional: fill the newly added rows with sample data
        static void PopulateNewRows(GridJs grid, int startIdx, int count)
        {
            for (int i = 0; i < count; i++)
            {
                int rowIdx = startIdx + i;
                grid.SetCell(rowIdx, 0, $"New Item {i + 1}");
                grid.SetCell(rowIdx, 1, DateTime.UtcNow);
            }
            Console.WriteLine("Populated the new rows with sample data.");
        }
```

Можно вызвать `PopulateNewRows(gridJs, startIndex, rowsToAdd);` сразу после пакетной вставки, если нужны строки, готовые к отображению.

## Step 5: Performance Tips for Very Large Grids

Когда речь идёт о **добавлении нескольких строк в сетку** в миллионах, учитывайте следующие приёмы:

1. **Размер пакета имеет значение** – Вставка 10 000 строк за один раз может быть быстрее, чем десять отдельных пакетов по 1 000 строк, потому что каждый пакет требует отдельного обновления UI.
2. **Отключите обновления UI** – В некоторых версиях GridJs доступны `grid.SuspendLayout()` / `grid.ResumeLayout()`. Оберните ваш пакет этими вызовами, если замечаете задержки.
3. **Используйте виртуализацию** – Как показано выше, `EnableVirtualization` значительно снижает потребление памяти и время рендеринга.
4. **Избегайте глубоких копий** – Передавайте в сетку простые типы значений или лёгкие объекты; тяжёлые объекты заставляют сетку клонировать данные, ухудшая производительность.

## Full Working Example

Объединив всё вместе, получаем полную программу, которую можно скопировать и вставить в новый консольный проект:

```csharp
using System;
using GridJsLibrary;   // Replace with the actual namespace of your GridJs library

namespace GridJsDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            GridJs gridJs = new GridJs
            {
                EnableVirtualization = true
            };

            SeedInitialData(gridJs);
            InsertRowsInBatch(gridJs);
        }

        static void SeedInitialData(GridJs grid)
        {
            for (int i = 0; i < 2_000_000; i++)
            {
                grid.InsertRow(i, new object[] { $"Row {i + 1}", DateTime.Now });
            }
            Console.WriteLine("Initial seed completed – 2 000 000 rows present.");
        }

        static void InsertRowsInBatch(GridJs grid)
        {
            int startIndex = 2_000_000; // zero‑based index for row 2 000 001
            int rowsToAdd = 10;

            grid.InsertRowsBatch(startIndex, rowsToAdd);
            Console.WriteLine($"Inserted {rowsToAdd} rows starting at index {startIndex + 1}.");

            // Optional: fill them with data
            PopulateNewRows(grid, startIndex, rowsToAdd);

            VerifyInsertion(grid, startIndex, rowsToAdd);
        }

        static void PopulateNewRows(GridJs grid, int startIdx, int count)
        {
            for (int i = 0; i < count; i++)
            {
                int rowIdx = startIdx + i;
                grid.SetCell(rowIdx, 0, $"New Item {i + 1}");
                grid.SetCell(rowIdx, 1, DateTime.UtcNow);
            }
            Console.WriteLine("Populated the new rows with sample data.");
        }

        static void VerifyInsertion(GridJs grid, int startIdx, int count)
        {
            Console.WriteLine("Verifying inserted rows:");
            for (int i = 0; i < count; i++)
            {
                var row = grid.GetRow(startIdx + i);
                Console.WriteLine($"Row {startIdx + i + 1}: {string.Join(", ", row)}");
            }
        }
    }
}
```

Запустите программу, и в консоли появится подтверждение, что десять строк были вставлены в правильное место и затем заполнены.

## Conclusion

Мы рассмотрели **как вставлять строки** в GridJs с помощью пакетного API, продемонстрировали **как добавить строки** эффективно и изучили способы **добавления нескольких строк в сетку** без «задушивания» UI. Ключевые выводы:

- Используйте `InsertRowsBatch(startIndex, count)` для любой массовой операции.
- Проверяйте индексы и учитывайте виртуализацию при работе с огромными наборами данных.
- Заполняйте строки после пакетной вставки, если нужен немедленный контент.

Далее вы можете изучить **как удалять строки**, реализовать **undo/redo** для пакетных правок или интегрировать GridJs с бек‑энд сервисом, который потоково передаёт данные. Все эти темы напрямую опираются на полученные здесь знания.

Не бойтесь экспериментировать — меняйте размер пакета, пробуйте вставлять в самое начало сетки или комбинируйте несколько пакетов в одной транзакции. Чем больше вы играете, тем увереннее будете себя чувствовать при работе с большими

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}