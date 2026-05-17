---
category: general
date: 2026-03-25
description: Узнайте, как быстро экспортировать Excel в DataTable на C#. Этот учебник
  охватывает экспорт Excel с именами столбцов и экспорт данных Excel в виде строк
  для надёжной обработки данных.
draft: false
keywords:
- export excel to datatable
- how to export excel to datatable
- export excel with column names
- export excel data as string
language: ru
og_description: Экспорт Excel в DataTable на C# с именами столбцов и преобразованием
  в строки. Следуйте этому лаконичному руководству для готового решения.
og_title: Экспорт Excel в DataTable в C# – Полное руководство
tags:
- C#
- Aspose.Cells
- DataTable
- Excel
title: Экспорт Excel в DataTable в C# – пошаговое руководство
url: /ru/net/excel-data-import-export/export-excel-to-datatable-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Экспорт Excel в DataTable в C# – Пошаговое руководство

Когда‑нибудь вам нужно было **export Excel to DataTable**, но вы не знали, какие флаги установить? Вы не одиноки — многие разработчики сталкиваются с тем же, когда впервые пытаются загрузить данные из таблицы в `DataTable`.  

Хорошая новость? Всего в несколько строк кода вы можете **export Excel with column names** и даже **export Excel data as string**, чтобы избежать проблем с несовпадением типов. Ниже вы найдёте полностью готовый пример и объяснение «почему» каждого параметра, чтобы вы могли адаптировать его к любому проекту без догадок.

## Что охватывает данный учебник

* Как создать рабочую книгу в памяти (без физического файла).  
* Как заполнить несколько образцовых строк, чтобы сразу увидеть результат.  
* Как настроить `ExportTableOptions`, чтобы каждая ячейка обрабатывалась как строка.  
* Как экспортировать прямоугольный диапазон в `DataTable`, сохранив первую строку как заголовки столбцов.  
* Как проверить результат и вывести первую строку в консоль.  

Никаких внешних ссылок на документацию не требуется — всё, что нужно, находится здесь. Если у вас уже есть файл Excel на диске, просто замените строку создания рабочей книги на `new Workbook("path/to/file.xlsx")`, и всё готово к работе.

---

## Шаг 1: Настройте проект и добавьте пакет Aspose.Cells NuGet

Прежде чем писать код, убедитесь, что ваш проект ссылается на **Aspose.Cells for .NET** (библиотека, реализующая класс `Workbook`). Добавить её можно через NuGet Package Manager:

```bash
dotnet add package Aspose.Cells
```

> **Pro tip:** Используйте последнюю стабильную версию (по состоянию на март 2026 года — 22.12), чтобы получить новейшие исправления ошибок и улучшения производительности.

---

## Шаг 2: Создайте рабочую книгу и заполните её образцовыми данными

Мы начнём с совершенно новой `Workbook` и запишем пару строк, чтобы вы могли увидеть экспорт в действии. Этот шаг также демонстрирует **how to export excel to datatable**, когда исходные данные находятся только в памяти.

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a fresh workbook and grab the first worksheet
        Workbook workbook = new Workbook();                 // in‑memory workbook
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ Populate a few cells – this mimics a real Excel file
        worksheet.Cells["A1"].PutValue("Name");   // column header
        worksheet.Cells["B1"].PutValue("Age");    // column header
        worksheet.Cells["A2"].PutValue("Alice");
        worksheet.Cells["B2"].PutValue(30);
        worksheet.Cells["A3"].PutValue("Bob");
        worksheet.Cells["B3"].PutValue(25);
```

*Почему это важно:* Вставив строку заголовков первой (`A1` & `B1`), мы позже сможем указать экспортеру рассматривать первую строку как имена столбцов — именно то, что означает **export excel with column names**.

---

## Шаг 3: Укажите Aspose.Cells обрабатывать каждую ячейку как строку

При экспорте числовых или датированных ячеек Aspose пытается определить тип .NET. Это может вызвать скрытые ошибки, если ваш последующий код ожидает строки. Флаг `ExportTableOptions.ExportAsString` принудительно преобразует всё в строки.

```csharp
        // 3️⃣ Configure export options – all values will be strings
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true       // <-- ensures Export Excel Data As String
        };
```

*Зачем это нужно?* Представьте столбец, в котором иногда находятся числа, а иногда текст (например, «00123» vs. «ABC»). Экспортируя всё как строки, вы избегаете потери ведущих нулей и исключений при преобразовании типов.

---

## Шаг 4: Экспортируйте нужный диапазон в DataTable

Теперь мы действительно **export excel to datatable**. Метод `ExportDataTable` принимает начальную строку/столбец, количество строк/столбцов, флаг извлечения имён столбцов и только что построенные параметры.

```csharp
        // 4️⃣ Export rows 0‑9 and columns 0‑4 (adjust as needed)
        DataTable table = worksheet.Cells.ExportDataTable(
            startRow: 0,
            startColumn: 0,
            totalRows: 10,
            totalColumns: 5,
            exportColumnNames: true,   // <-- uses the first row as headers
            exportOptions: exportOptions);
```

*Что происходит «под капотом»?*  
- `startRow: 0` указывает на первую строку Excel (строка заголовков).  
- `exportColumnNames: true` заставляет Aspose перенести «Name» и «Age» в коллекцию столбцов `DataTable`.  
- `totalRows`/`totalColumns` могут превышать фактические данные; лишние ячейки становятся пустыми строками благодаря `ExportAsString`.

---

## Шаг 5: Проверьте результат — выведите первую строку

Быстрый вывод в консоль доказывает, что преобразование прошло успешно и имена столбцов сохранены.

```csharp
        // 5️⃣ Show the first data row (if any)
        if (table.Rows.Count > 0)
        {
            Console.WriteLine($"First row: {table.Rows[0]["Name"]}, {table.Rows[0]["Age"]}");
        }
        else
        {
            Console.WriteLine("The exported DataTable is empty.");
        }
    }
}
```

**Ожидаемый вывод**

```
First row: Alice, 30
```

Если вы измените образцовые данные, консоль автоматически отразит эти изменения — дополнительный код не требуется.

---

## Часто задаваемые вопросы и особые случаи

| Question | Answer |
|----------|--------|
| **Can I export a sheet that already exists on disk?** | Да — замените `new Workbook()` на `new Workbook("myFile.xlsx")`. Остальные шаги остаются без изменений. |
| **What if my Excel file has merged cells?** | Объединённые ячейки разворачиваются; значение верхней‑левой ячейки используется для всего объединённого диапазона. |
| **Do I need to worry about culture‑specific number formats?** | Нет, когда `ExportAsString = true`; всё поступает как необработанная строка, отображаемая в Excel. |
| **How many rows can I export at once?** | Aspose.Cells может обрабатывать миллионы строк, но потребление памяти растёт вместе с размером `DataTable`. При достижении пределов рассмотрите постраничный экспорт. |
| **What about hidden columns?** | Скрытые столбцы экспортируются, если только вы не установите `ExportHiddenColumns = false` в `ExportTableOptions`. |

---

## Бонус: Экспорт в CSV вместо DataTable

Иногда удобнее получить плоский файл. Те же `ExportTableOptions` можно использовать с `ExportDataTableToCSV`:

```csharp
        string csvPath = "output.csv";
        worksheet.Cells.ExportDataTableToCSV(
            startRow: 0,
            startColumn: 0,
            totalRows: 10,
            totalColumns: 5,
            csvPath,
            exportColumnNames: true,
            exportOptions);
        Console.WriteLine($"CSV written to {csvPath}");
```

Эта однострочная команда выдаёт готовый к импорту CSV, при этом всё ещё **exporting excel data as string**.

---

## Полный рабочий пример (готов к копированию)

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Populate sample data (header + two rows)
        worksheet.Cells["A1"].PutValue("Name");
        worksheet.Cells["B1"].PutValue("Age");
        worksheet.Cells["A2"].PutValue("Alice");
        worksheet.Cells["B2"].PutValue(30);
        worksheet.Cells["A3"].PutValue("Bob");
        worksheet.Cells["B3"].PutValue(25);

        // Export everything as strings
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true
        };

        // Export range to DataTable (first row = column names)
        DataTable table = worksheet.Cells.ExportDataTable(
            startRow: 0,
            startColumn: 0,
            totalRows: 10,
            totalColumns: 5,
            exportColumnNames: true,
            exportOptions: exportOptions);

        // Display first row
        if (table.Rows.Count > 0)
        {
            Console.WriteLine($"First row: {table.Rows[0]["Name"]}, {table.Rows[0]["Age"]}");
        }
        else
        {
            Console.WriteLine("The exported DataTable is empty.");
        }
    }
}
```

Запустите программу (`dotnet run`), и вы увидите результат **export excel to datatable**, выведенный в консоль. Замените образцовые данные, измените `totalRows`/`totalColumns` или укажите реальный файл — всё масштабируется.

---

## Заключение

Теперь у вас есть **complete, self‑contained solution for exporting Excel to DataTable** в C#. Настроив `ExportTableOptions.ExportAsString`, вы гарантируете **export excel data as string**, а установив `exportColumnNames: true`, получаете привычные заголовки столбцов, ожидаемые при **export excel with column names**.  

Отсюда вы можете:

* Передать `DataTable` в Entity Framework или Dapper для массовой вставки.  
* Отправить её в движок отчётности, такой как **FastReport** или **RDLC**.  
* Преобразовать её в JSON для ответа API (`JsonConvert.SerializeObject(table)`).

Не стесняйтесь экспериментировать — попробуйте экспортировать более крупный лист или комбинировать это с **how to export excel to datatable** из сетевого ресурса. Паттерн остаётся тем же, а код готов к продакшну.

![Схема потока преобразования Excel → DataTable – export excel to datatable](https://example.com/placeholder.png "диаграмма export excel to datatable")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}