---
category: general
date: 2026-07-13
description: Как экспортировать диапазон ячеек в виде таблицы с помощью C# и ExportTableOptions.
  Узнайте пошаговую настройку книги, форматирование и экспорт таблицы.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to export cell range as table
- ExportTableOptions usage
- Workbook and Worksheet handling
- cell value formatting C#
- scientific notation export
language: ru
lastmod: 2026-07-13
og_description: Как экспортировать диапазон ячеек в виде таблицы в C# с помощью ExportTableOptions.
  Следуйте этому руководству, чтобы форматировать ячейки, создать рабочую книгу и
  без труда экспортировать таблицу.
og_image_alt: Diagram illustrating a C# code snippet that exports a single cell range
  as a formatted table
og_title: Как экспортировать диапазон ячеек в таблицу — полное руководство на C#
schemas:
- author: Aspose
  dateModified: '2026-07-13'
  description: How to export cell range as table using C# and ExportTableOptions.
    Learn step‑by‑step workbook setup, formatting, and table export.
  headline: How to Export Cell Range as Table – Complete C# Guide
  type: TechArticle
tags:
- C#
- Aspose.Cells
- Excel automation
- data export
title: Как экспортировать диапазон ячеек в виде таблицы — полное руководство по C#
url: /ru/net/excel-data-export-retrieval/how-to-export-cell-range-as-table-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как экспортировать диапазон ячеек как таблицу – Полное руководство по C#

Когда‑то задавались вопросом **как экспортировать диапазон ячеек как таблицу** без бесконечных проблем с форматированием? Вы не одиноки. Будь то передача данных в конвейер отчетности или быстрый дамп в стиле CSV, освоение процесса экспорта может сэкономить часы ручного копирования‑вставки.

В этом руководстве мы пошагово пройдем процесс: возьмём числовую ячейку, применим научную нотацию и экспортируем её как таблицу с помощью **ExportTableOptions**. К концу вы получите готовый фрагмент кода, поймёте *почему* каждый вызов нужен, и узнаете, как настроить код для больших диапазонов или других форматов.

## Предварительные требования

- .NET 6 или новее (API работает одинаково на .NET Framework 4.7+)
- Aspose.Cells for .NET установлен (`Install-Package Aspose.Cells`)
- Базовое понимание синтаксиса C#; глубокие знания внутренностей Excel не требуются

Есть всё? Отлично — погружаемся.

## Шаг 1: Настройка параметров экспорта – Как экспортировать диапазон ячеек как таблицу

Первое, что вам нужно — это экземпляр **ExportTableOptions**, который сообщает библиотеке, как обрабатывать содержимое ячеек. Без него экспорт по умолчанию использует сырые числовые значения, что может сломать downstream‑потребителей, ожидающих текст.

```csharp
// Step 1: Define export options – export the cell value as a formatted string
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true,          // Return the cell content as text
    CustomFormat = "0.00E+00"       // Apply scientific notation format
};
```

**Почему это важно:**  
- `ExportAsString = true` заставляет библиотеку записывать отображаемый в ячейке текст, а не её внутреннее значение double.  
- `CustomFormat` позволяет задать **экспорт в научной нотации**, что полезно при работе с очень большими или очень маленькими числами.

> **Pro tip:** Если вам нужен формат даты или валюты, замените `"0.00E+00"` на `"yyyy‑MM‑dd"` или `"$#,##0.00"` соответственно.

## Шаг 2: Создание Workbook и получение первого Worksheet – Работа с Workbook и Worksheet

**Workbook** представляет весь файл Excel, а **Worksheet** — отдельную вкладку. Для простого экспорта мы будем работать с первым листом, который всегда присутствует по индексу 0.

```csharp
// Step 2: Create a new workbook and access the first worksheet
Workbook workbook = new Workbook();
Worksheet sheet = workbook.Worksheets[0];
```

**Почему это важно:**  
Создание нового `Workbook` гарантирует чистый лист — без скрытых стилей или оставшихся данных, которые могут вызвать проблемы. Обращение к `Worksheets[0]` — самый быстрый способ получить доступ к активному листу без необходимости знать его имя.

## Шаг 3: Заполнение целевой ячейки – Форматирование значения ячейки C#

Теперь вставим числовое значение в ячейку **A1** (строка 0, столбец 0). Выбранное значение намеренно имеет длинную дробную часть, чтобы вы могли увидеть работу научной нотации.

```csharp
// Step 3: Insert a numeric value into cell A1 (row 0, column 0)
sheet.Cells[0, 0].PutValue(12345.6789);
```

**Почему это важно:**  
Вызов `PutValue` автоматически определяет тип данных ячейки. Поскольку позже мы экспортируем как строку, сырый double будет преобразован с использованием ранее заданного формата, давая аккуратный вывод `"1.23E+04"`.

## Шаг 4: Экспорт определённого диапазона ячеек как таблицы – Экспорт диапазона ячеек как таблицы

Имея параметры и данные, последний шаг — попросить Aspose.Cells записать диапазон. Метод `ExportTable` ожидает начальную строку/столбец, размер диапазона и объект опций, который мы создали.

```csharp
// Step 4: Export the defined cell range as a table using the options above
// Parameters: startRow, startColumn, totalRows, totalColumns, options
sheet.ExportTable(0, 0, 1, 1, exportOptions);
```

**Почему это важно:**  
- `totalRows = 1` и `totalColumns = 1` ограничивают экспорт одной ячейкой, но вы можете увеличить эти числа, чтобы охватить более крупные блоки (например, `5, 3` для диапазона 5 строк × 3 столбца).  
- Метод записывает данные во внутреннюю табличную структуру, которую можно сохранить как CSV, HTML или даже напрямую передать клиенту.

### Сохранение результата (по желанию)

Если хотите сохранить экспортированную таблицу на диск, можно записать её в CSV‑файл:

```csharp
// Optional: Save the exported table as CSV for verification
using (var stream = new MemoryStream())
{
    sheet.ExportTableToCSV(stream, exportOptions);
    File.WriteAllBytes("ExportedTable.csv", stream.ToArray());
}
```

Выполнение вышеуказанного кода создаст файл, содержащий:

```
1.23E+04
```

## Особые случаи и распространённые варианты

| Ситуация | Что изменить | Причина |
|-----------|----------------|--------|
| **Экспорт нескольких строк** | Отрегулировать `totalRows` и при необходимости добавить цикл по строкам | Позволяет пакетный экспорт без многократного вызова `ExportTable` |
| **Сохранение формул** | Установить `ExportAsString = false` | Сохраняет оригинальную формулу вместо отображаемого значения |
| **Разные разделители** | Использовать перегрузку `ExportTableToCSV(..., ',', ...)` | Переключает вывод с запятой на табуляцию или вертикальную черту |
| **Большие листы** | Потоковый экспорт, чтобы избежать `OutOfMemoryException` | Хорошо работает при более чем 10 000 строках |

## Полный рабочий пример

Ниже полностью готовая к копированию и вставке программа. Она компилируется в любом .NET консольном проекте, где подключена библиотека Aspose.Cells.

```csharp
using System;
using System.IO;
using Aspose.Cells;

class ExportCellRangeDemo
{
    static void Main()
    {
        // 1️⃣ Define export options – how to export cell range as table
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            CustomFormat = "0.00E+00"
        };

        // 2️⃣ Create workbook and get first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // 3️⃣ Put a numeric value into A1
        sheet.Cells[0, 0].PutValue(12345.6789);

        // 4️⃣ Export the single‑cell range as a table
        sheet.ExportTable(0, 0, 1, 1, exportOptions);

        // Optional: write to CSV to see the result
        using (var ms = new MemoryStream())
        {
            sheet.ExportTableToCSV(ms, exportOptions);
            File.WriteAllBytes("ExportedTable.csv", ms.ToArray());
        }

        Console.WriteLine("Export complete! Check ExportedTable.csv");
    }
}
```

**Ожидаемый вывод:**  
Файл с именем `ExportedTable.csv`, содержащий одну строку:

```
1.23E+04
```

Если открыть CSV в текстовом редакторе, вы увидите, что научная нотация применена точно так, как задано.

## Заключение

Мы рассмотрели **как экспортировать диапазон ячеек как таблицу** от начала до конца: настройку `ExportTableOptions`, создание `Workbook`, вставку данных и окончательный вызов `ExportTable`. Поняв каждую часть, вы теперь можете масштабировать подход на большие диапазоны, другие форматы или даже интегрировать его в веб‑API, который в реальном времени обслуживает данные из Excel.

В дальнейшем стоит обратить внимание на:

- **ExportTableToHTML** для веб‑готовых превью  
- **ExportTableToDataTable** для прямой передачи в конвейеры ADO.NET  
- Расширенные **custom formats** для дат, валют и процентов  

Попробуйте эти возможности, и простой экспорт ячейки превратится в универсальный механизм доставки данных. Есть вопросы или необычный сценарий? Оставьте комментарий ниже — happy coding!

## Что изучать дальше?

Следующие руководства охватывают тесно связанные темы, расширяющие техники, продемонстрированные в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы в собственных проектах.

- [Как экспортировать видимые строки Excel с помощью Aspose.Cells for .NET: пошаговое руководство](/cells/english/net/workbook-operations/export-visible-rows-aspose-cells-dotnet/)
- [Как экспортировать файлы Excel в .NET с помощью Aspose.Cells: всестороннее руководство](/cells/english/net/workbook-operations/export-excel-files-net-aspose-cells-guide/)
- [Как получить доступ к ячейке Excel по имени с помощью Aspose.Cells for .NET: пошаговое руководство](/cells/english/net/cell-operations/access-cell-by-name-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}