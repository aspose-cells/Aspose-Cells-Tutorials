---
category: general
date: 2026-03-29
description: Узнайте, как копировать диапазон, копировать сводные таблицы, как сохранять
  рабочую книгу и как загружать её в C#. Легко перемещайте сводные таблицы с пошаговым
  кодом.
draft: false
keywords:
- how to copy range
- copy pivot tables
- how to save workbook
- how to load workbook
- move pivot table
language: ru
og_description: Как копировать диапазон, копировать сводные таблицы, как сохранять
  книгу и как загружать книгу в C#. Перемещайте сводные таблицы без усилий с помощью
  понятного кода.
og_title: Как копировать диапазон с помощью сводных таблиц в C# — Полное руководство
tags:
- C#
- Aspose.Cells
- Excel automation
title: Как скопировать диапазон с сводными таблицами в C# – Полное руководство
url: /ru/net/pivot-tables/how-to-copy-range-with-pivot-tables-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как копировать диапазон с сводными таблицами в C# – Полное руководство

Когда‑нибудь задавались вопросом **how to copy range**, содержащий сводную таблицу, не разрывая связь с исходными данными? Вы не одиноки. Во многих реальных проектах я сталкивался с этой проблемой — файлы Excel приходят со сложными сводными таблицами, и требуется переместить их или дублировать данные в другое место.  

Хорошие новости? Решение довольно простое, как только вы знаете **how to load workbook**, делаете копию и затем **how to save workbook** снова. В этом руководстве мы пройдем весь процесс, включая как **copy pivot tables**, а также быстрый совет по **move pivot table**, если вам нужно разместить её в другом месте того же листа.

К концу этого руководства у вас будет полностью рабочий фрагмент C#, который:

1. Загружает существующий файл Excel.  
2. Копирует диапазон (включая сводную таблицу) в новое место.  
3. Сохраняет изменённую книгу в новый файл.

Без внешних скриптов, без ручных манипуляций — только чистый, повторяемый код.

---

## Необходимые условия

- **.NET 6+** (любая современная версия подходит).  
- **Aspose.Cells for .NET** — библиотека, предоставляющая `Workbook`, `WorksheetCopyOptions` и т.д. Вы можете установить её через NuGet:

```bash
dotnet add package Aspose.Cells
```

- Входная книга (`input.xlsx`), уже содержащая сводную таблицу в диапазоне `A1:G20`.  
- Базовое знакомство с C# и Visual Studio (или вашей любимой IDE).

> **Подсказка профессионала:** Если вы используете другую библиотеку Excel (например, EPPlus), концепции одинаковы — просто замените вызовы API.

---

## Шаг 1 – How to load workbook (Основная настройка)

Прежде чем мы сможем что‑либо копировать, нам нужно загрузить файл Excel в память.

```csharp
using Aspose.Cells;

// Step 1: Load the source workbook
var sourceWorkbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");

// Grab the first worksheet – this is where our pivot lives
var sourceWorksheet = sourceWorkbook.Worksheets[0];
```

**Почему это важно:**  
Загрузка книги предоставляет объектную модель, которой можно управлять. Без правильного `how to load workbook` любая последующая операция копирования вызовет исключение *FileNotFound* или *InvalidOperation*.

> **Осторожно:** Если файл большой, рассмотрите возможность использования `LoadOptions` с `MemorySetting` для контроля использования памяти.

---

## Шаг 2 – How to copy range (включая сводную таблицу)

Теперь наступает звезда шоу: копирование диапазона, содержащего сводную таблицу. Метод `CopyRange` в сочетании с `WorksheetCopyOptions` выполняет основную работу.

```csharp
// Step 2: Copy a range that includes a pivot table to a new location
sourceWorksheet.CopyRange(
    "A1:G20",                                   // Source range
    new WorksheetCopyOptions { CopyPivotTables = true }, // Ensure pivot tables travel with the data
    sourceWorksheet,                           // Destination worksheet (same sheet in this case)
    "A25");                                     // Upper‑left corner of the destination
```

**Почему мы устанавливаем `CopyPivotTables = true`:**  
По умолчанию копирование диапазона перемещает только сырые ячейки. Кеш сводной таблицы остаётся, и скопированная сводка становится статической таблицей. Установка `CopyPivotTables` сохраняет живое соединение, поэтому дублированная сводка всё ещё обновляется при изменении исходных данных.

**Пограничный случай:** Если диапазон назначения перекрывается с исходным, Aspose.Cells выбросит `ArgumentException`. Всегда выбирайте неперекрывающийся диапазон или сначала создайте новый лист.

---

## Шаг 3 – How to save workbook (Сохранение изменений)

После копирования вам понадобится записать изменения обратно на диск. Здесь в дело вступает **how to save workbook**.

```csharp
// Step 3: Save the modified workbook to a new file
sourceWorkbook.Save(@"YOUR_DIRECTORY\output.xlsx");
```

**Что происходит под капотом:**  
`Save` сериализует книгу в памяти, включая только что скопированную сводную таблицу, в стандартный пакет `.xlsx`. Если нужен другой формат (CSV, PDF и т.д.), просто измените расширение файла или используйте перегрузку, принимающую `SaveFormat`.

> **Совет:** Используйте `Workbook.Save(string, SaveOptions)`, если нужно защитить файл паролем или задать другие параметры экспорта.

---

## Полный рабочий пример

Putting it all together, here’s the complete, ready‑to‑run program:

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ How to load workbook
        var sourceWorkbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");
        var sourceWorksheet = sourceWorkbook.Worksheets[0];

        // 2️⃣ How to copy range (including pivot tables)
        sourceWorksheet.CopyRange(
            "A1:G20",
            new WorksheetCopyOptions { CopyPivotTables = true },
            sourceWorksheet,
            "A25");

        // 3️⃣ How to save workbook
        sourceWorkbook.Save(@"YOUR_DIRECTORY\output.xlsx");

        Console.WriteLine("✅ Range copied and workbook saved successfully!");
    }
}
```

**Ожидаемый результат:**  
Откройте `output.xlsx`. Вы увидите оригинальную сводную таблицу всё ещё в `A1:G20` и идентичную полностью функциональную копию, начинающуюся с `A25`. Обе сводки указывают на одни и те же исходные данные, поэтому обновление одной обновит другую.

---

## Часто задаваемые вопросы и варианты

### Могу ли я **move pivot table** вместо копирования её?

Конечно. После копирования просто очистите исходный диапазон (или используйте `sourceWorksheet.Cells.ClearRange(0, 0, 19, 6)`) и при необходимости переименуйте диапазон назначения. Это фактически «перемещает» сводную таблицу.

### Что если сводная таблица использует внешний источник данных?

`CopyPivotTables = true` копирует только определение сводной таблицы, а не внешнее соединение. Убедитесь, что целевая книга имеет доступ к тому же источнику данных, или воссоздайте соединение после копирования.

### Как скопировать на **different worksheet**?

Просто передайте объект листа назначения вместо `sourceWorksheet`:

```csharp
var destWorksheet = sourceWorkbook.Worksheets.Add("CopiedPivot");
sourceWorksheet.CopyRange("A1:G20", new WorksheetCopyOptions { CopyPivotTables = true }, destWorksheet, "A1");
```

### Есть ли способ скопировать **multiple ranges** за один раз?

Вы можете вызывать `CopyRange` многократно или использовать `CopyRows`/`CopyColumns` для больших блоков. Перебор списка строк адресов — чистый подход.

---

## Распространённые подводные камни и профессиональные советы

- **Размер кеша сводной таблицы:** Большие кеши могут значительно увеличить размер книги. Если нужны только отображаемые данные, рассмотрите `CopyPivotTables = false`, а затем используйте `PivotTable.RefreshData()` в месте назначения.  
- **Пути к файлам:** Используйте `Path.Combine`, чтобы избежать жёстко заданных разделителей, особенно в кроссплатформенном .NET.  
- **Производительность:** Для огромных книг оберните копирование в `using (var stream = new MemoryStream())` и сначала сохраните в поток, затем запишите на диск. Это уменьшает нагрузку ввода‑вывода.

---

## Заключение

Теперь вы знаете **how to copy range**, содержащий сводную таблицу, как **copy pivot tables**, и точные шаги для **how to load workbook** и **how to save workbook** после операции. Независимо от того, нужно ли вам **move pivot table** в пределах того же листа или на другой лист, схема остаётся той же — загрузить, скопировать с правильными параметрами и сохранить.

Попробуйте это с вашими файлами, измените адрес назначения и поэкспериментируйте с различными конфигурациями сводных таблиц. Чем больше вы будете экспериментировать, тем увереннее станете в автоматизации задач Excel на C#.

---

![Диаграмма, показывающая, как диапазон A1:G20 копируется в A25 на том же листе – how to copy range with pivot tables](/images/how-to-copy-range-diagram.png "how to copy range with pivot tables")

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}