---
category: general
date: 2026-03-18
description: Как экспортировать данные из Excel в DataTable в C# с кодом, который
  обрабатывает конкретные ячейки, преобразует Excel в DataTable и форматирует числа.
  Узнайте, как экспортировать определённые ячейки и многое другое.
draft: false
keywords:
- how to export excel
- convert excel to datatable
- export specific cells
- excel to datatable c#
- excel range to datatable
language: ru
og_description: Как экспортировать данные Excel в DataTable в C#. Этот учебник показывает,
  как экспортировать конкретные ячейки, преобразовать Excel в DataTable и легко форматировать
  числа.
og_title: Как экспортировать Excel в DataTable в C# – Полное руководство
tags:
- C#
- Excel
- DataTable
- Aspose.Cells
title: Как экспортировать Excel в DataTable в C# – пошаговое руководство
url: /ru/net/excel-data-import-export/how-to-export-excel-to-a-datatable-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как экспортировать Excel в DataTable на C# – пошаговое руководство

Когда‑нибудь задумывались **как экспортировать Excel**‑данные в `DataTable`, не теряя форматирование? Вы не одиноки — разработчикам постоянно нужно вытаскивать часть таблицы в память для отчётности, валидации или массовых вставок. Хорошая новость: всего несколькими строками C# можно экспортировать точный диапазон (например *A1:F11*), заставить каждую ячейку рассматриваться как строка и даже применить пользовательский числовой формат.

В этом руководстве мы охватим всё, что нужно знать: от загрузки книги, настройки **export specific cells**, преобразования диапазона в `DataTable` и обработки краевых случаев, таких как пустые строки или числа, зависящие от локали. К концу вы получите переиспользуемый метод, который работает в сценариях **excel to datatable c#** в продакшн‑коде.

> **Prerequisites** – Вам понадобится библиотека Aspose.Cells for .NET (или любой аналогичный API, предоставляющий `ExportDataTable`). Пример рассчитан на .NET 6+, но концепции применимы и к более ранним версиям.

---

## Что вы узнаете

- Как **convert Excel to DataTable** с помощью Aspose.Cells.  
- Экспорт пользовательского диапазона (`excel range to datatable`) с принудительным представлением всех значений как строк.  
- Применение числового формата с двумя знаками после запятой (`#,#00.00`) при экспорте.  
- Распространённые подводные камни (null‑строки, скрытые столбцы) и способы их обхода.  
- Готовый к копированию, полностью рабочий пример кода.

---

## Предварительные требования и настройка

Прежде чем погрузиться в код, убедитесь, что у вас есть:

1. **Aspose.Cells for .NET**, установленный через NuGet:

   ```bash
   dotnet add package Aspose.Cells
   ```

2. Файл Excel (`input.xlsx`), размещённый в папке, к которой вы можете обратиться, например `YOUR_DIRECTORY/input.xlsx`.  
3. Проект, нацеленный на .NET 6 или новее (операторы `using`, показанные ниже, работают сразу).

> **Pro tip:** Если вы используете другую библиотеку (например, EPPlus или ClosedXML), концепция остаётся той же — загрузите книгу, выберите диапазон и вызовите метод, возвращающий `DataTable`.

---

## Шаг 1: Загрузка книги и получение первого листа

Первое, что вам нужно, — объект `Workbook`, представляющий ваш файл Excel. После его создания вы можете получить доступ к любому листу по индексу или имени.

```csharp
using Aspose.Cells;
using System.Data;

namespace ExcelExportDemo
{
    class Program
    {
        static void Main()
        {
            // Load the workbook from disk
            Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");

            // Grab the first worksheet (index 0)
            Worksheet worksheet = workbook.Worksheets[0];

            // Continue with export options...
        }
    }
}
```

**Why this matters:** Загрузка книги на раннем этапе позволяет проанализировать её структуру (скрытые листы, защита) перед тем, как решать, какие ячейки экспортировать. Если файл большой, рассмотрите возможность использования `LoadOptions` для потоковой загрузки только нужных частей.

---

## Шаг 2: Настройка параметров экспорта – все значения как строки

Когда вы экспортируете данные для дальнейшей обработки (например, массовой вставки в SQL), часто требуется **consistent string representation**. Это избавляет от ошибок несоответствия типов позже.

```csharp
// Configure export behavior
ExportTableOptions exportOptions = new ExportTableOptions
{
    // Force every cell to be returned as a string, regardless of its original type
    ExportAsString = true,

    // Apply a two‑decimal‑place format to numeric cells
    NumberFormat = "#,##0.00"
};
```

**Explanation:**  
- `ExportAsString = true` заставляет Aspose.Cells игнорировать оригинальный тип ячейки и возвращать отформатированный текст.  
- `NumberFormat = "#,##0.00"` гарантирует, что числа вроде `1234.5` станут `"1,234.50"` — удобно для финансовых отчётов.

Если нужны оригинальные типы данных, просто установите `ExportAsString` в `false` и выполните преобразование самостоятельно.

---

## Шаг 3: Экспорт конкретного диапазона (A1:F11) в DataTable

Теперь переходим к основной части **export specific cells**. Метод `ExportDataTable` принимает индексы начальной/конечной строки и столбца (нумерация с нуля) и флаг включения заголовков.

```csharp
// Export cells A1:F11 (rows 0‑10, columns 0‑5) including the header row
DataTable table = worksheet.ExportDataTable(
    startRow: 0,
    startColumn: 0,
    endRow: 10,
    endColumn: 5,
    includeColumnNames: true,
    exportOptions: exportOptions);
```

**What you get:** `DataTable` с 11 строками (включая заголовок) и 6 столбцами (`A`‑`F`). Все значения — строки, отформатированные согласно `exportOptions`.

---

## Шаг 4: Проверка результата – вывод в консоль

Всегда полезно выполнить sanity‑check вывода перед передачей таблицы другому компоненту.

```csharp
// Simple console dump
foreach (DataRow row in table.Rows)
{
    foreach (var item in row.ItemArray)
    {
        Console.Write($"{item}\t");
    }
    Console.WriteLine();
}
```

Вы должны увидеть что‑то вроде:

```
Id      Name        Qty     Price   Total   Date
1       Widget A    10      2.50    25.00   2026-01-01
2       Widget B    5       3.75    18.75   2026-01-02
...
```

Обратите внимание, как числовые столбцы отображаются с двумя знаками после запятой, точно как мы задали.

---

## Полный рабочий пример (готов к копированию)

Ниже представлена полностью готовая программа, объединяющая все шаги. Скопируйте её в новый консольный проект, поправьте путь к файлу и запустите — дополнительной конфигурации не требуется.

```csharp
using Aspose.Cells;
using System;
using System.Data;

namespace ExcelExportDemo
{
    class Program
    {
        static void Main()
        {
            // -------------------------------------------------
            // 1️⃣ Load workbook and select worksheet
            // -------------------------------------------------
            string filePath = @"YOUR_DIRECTORY\input.xlsx";
            Workbook workbook = new Workbook(filePath);
            Worksheet worksheet = workbook.Worksheets[0];

            // -------------------------------------------------
            // 2️⃣ Set export options – strings + number format
            // -------------------------------------------------
            ExportTableOptions exportOptions = new ExportTableOptions
            {
                ExportAsString = true,
                NumberFormat = "#,##0.00"
            };

            // -------------------------------------------------
            // 3️⃣ Export range A1:F11 (rows 0‑10, cols 0‑5)
            // -------------------------------------------------
            DataTable table = worksheet.ExportDataTable(
                startRow: 0,
                startColumn: 0,
                endRow: 10,
                endColumn: 5,
                includeColumnNames: true,
                exportOptions: exportOptions);

            // -------------------------------------------------
            // 4️⃣ Output to console for verification
            // -------------------------------------------------
            Console.WriteLine("=== Exported DataTable ===");
            foreach (DataRow row in table.Rows)
            {
                foreach (var cell in row.ItemArray)
                {
                    Console.Write($"{cell}\t");
                }
                Console.WriteLine();
            }

            // Keep console window open
            Console.WriteLine("\nPress any key to exit...");
            Console.ReadKey();
        }
    }
}
```

**Key takeaways from the code:**  

- Объект `ExportTableOptions` переиспользуем; его можно передавать в несколько вызовов `ExportDataTable`, если нужно экспортировать несколько диапазонов.  
- Индексация начинается с **0**, поэтому `A1` соответствует `(0,0)`.  
- Установка `includeColumnNames` в `true` автоматически использует первую строку как заголовки столбцов — удобно для последующей работы с `DataTable`.

---

## Обработка краевых случаев и часто задаваемые вопросы

### Что делать, если на листе скрыты строки или столбцы?

Aspose.Cells по умолчанию учитывает видимость. Если нужно экспортировать скрытые данные, установите `exportOptions.ExportHiddenRows = true` и `ExportHiddenColumns = true`.

### Мой файл Excel содержит формулы — получу ли я вычисленные значения?

Да. По умолчанию `ExportDataTable` возвращает **displayed value** (результат формулы). Если требуется текст самой формулы, задайте `exportOptions.ExportFormulas = true`.

### Как пропустить полностью пустые строки?

После экспорта можно очистить `DataTable`:

```csharp
foreach (DataRow row in table.Rows.Cast<DataRow>()
                                   .Where(r => r.ItemArray.All(c => c == DBNull.Value || string.IsNullOrWhiteSpace(c.ToString()))).ToList())
{
    table.Rows.Remove(row);
}
```

### Можно ли экспортировать разрозненный диапазон (например, A1:B5 и D1:E5)?

Aspose.Cells не поддерживает раздельные диапазоны в одном вызове. Нужно экспортировать каждый блок отдельно, а затем вручную объединять полученные `DataTable`.

---

## Советы по производительности

- **Reuse `ExportTableOptions`** для нескольких экспортов; создание нового экземпляра каждый раз добавляет незначительные накладные расходы, но захламляет код.  
- **Stream large files** с помощью `LoadOptions`, чтобы не загружать всю книгу в память.  
- **Avoid `DataTable`**, если нужен лишь быстрый CSV‑экспорт — `ExportDataTable` удобен, но не самый экономичный по памяти при работе с огромными листами.

---

## Заключение

Мы прошли процесс **how to export Excel** в `DataTable`, контролируя форматирование, работая с конкретными диапазонами ячеек и гарантируя, что каждое значение приходит как строка. Полный пример демонстрирует чистый, готовый к продакшн подход, который можно адаптировать под **convert excel to datatable**, **export specific cells** или любой сценарий **excel range to datatable**, с которым вы столкнётесь.

Экспериментируйте: меняйте диапазон, переключайте `ExportAsString` или передавайте `DataTable` напрямую в Entity Framework для массовых вставок. Возможности безграничны, когда есть такая надёжная основа.

### Следующие шаги и смежные темы

- **Importing DataTable back into Excel** — изучите обратную операцию с помощью `ImportDataTable`.  
- **Bulk inserting a DataTable into SQL Server** — используйте `SqlBulkCopy` для молниеносных загрузок.  
- **Working with EPPlus or ClosedXML** — посмотрите, как та же задача выглядит с альтернативными библиотеками.  
- **Formatting cells on export** — изучите `ExportTableOptions` подробнее: форматы дат, пользовательские настройки культуры и многое другое.

Есть вопросы или другой сценарий использования? Оставьте комментарий, и давайте продолжать обсуждение. Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}