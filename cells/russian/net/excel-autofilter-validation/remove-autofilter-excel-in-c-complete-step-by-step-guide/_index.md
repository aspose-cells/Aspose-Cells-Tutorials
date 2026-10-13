---
category: general
date: 2026-02-23
description: Узнайте, как удалить автофильтр в Excel с помощью C#. В этом руководстве
  также рассматривается, как удалить автофильтр, очистить фильтр Excel, очистить фильтр
  таблицы Excel и загрузить книгу Excel на C#.
draft: false
keywords:
- remove autofilter excel
- how to remove autofilter
- clear excel filter
- clear excel table filter
- load excel workbook c#
language: ru
og_description: Удалить автофильтр Excel в C# объяснено в первом предложении. Следуйте
  шагам, чтобы очистить фильтр Excel, очистить фильтр таблицы Excel и загрузить книгу
  Excel в C#.
og_title: Удаление автофильтра в Excel на C# – Полное руководство
tags:
- Aspose.Cells
- C#
- Excel Automation
title: Удаление автoфильтра в Excel с помощью C# – Полное пошаговое руководство
url: /ru/net/excel-autofilter-validation/remove-autofilter-excel-in-c-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# удалить автофильтр excel в C# – Полное пошаговое руководство

Когда‑то вам нужно было **удалить автофильтр excel** из таблицы, но вы не знали, какой вызов API использовать? Вы не одиноки — многие разработчики сталкиваются с этой проблемой при автоматизации отчётов. Хорошая новость в том, что несколькими строками C# можно очистить фильтр, сбросить представление и поддерживать рабочую книгу в порядке.

В этом руководстве мы пройдёмся по **удалению автофильтра**, а также покажем, как **очистить excel‑фильтр**, **очистить фильтр таблицы excel** и **загрузить excel‑рабочую книгу c#** с помощью популярной библиотеки Aspose.Cells. К концу вы получите готовый к запуску фрагмент кода, поймёте, почему каждый шаг важен, и узнаете, как обрабатывать типичные граничные случаи.

## Требования

Прежде чем приступить, убедитесь, что у вас есть:

* .NET 6 (или любая современная версия .NET) — код работает как на .NET Core, так и на .NET Framework.  
* Пакет NuGet Aspose.Cells for .NET (`Install-Package Aspose.Cells`).  
* Файл Excel (`input.xlsx`), содержащий таблицу с именем **MyTable** и применённым AutoFilter.  

Если чего‑то не хватает, установите это вначале — иначе код не скомпилируется.

![удалить автофильтр excel](/images/remove-autofilter-excel.png "Скриншот, показывающий лист Excel с применённым автофильтром – удалить автофильтр excel")

## Шаг 1 — Загрузка Excel‑рабочей книги с помощью C#

Первое, что нужно сделать, — открыть книгу. Aspose.Cells абстрагирует низкоуровневую работу с файлами, позволяя сосредоточиться на бизнес‑логике.

```csharp
using Aspose.Cells;

// Load the workbook (replace with your actual path)
Workbook workbook = new Workbook(@"C:\MyProjects\ExcelDemo\input.xlsx");
```

*Почему это важно:* загрузка книги даёт доступ к листам, таблицам и фильтрам. Пропустив этот шаг, вы не сможете ничего изменить.

## Шаг 2 — Получить целевой лист

В большинстве книг несколько листов, но в примере предполагается, что таблица находится на первом. При необходимости измените индекс или используйте имя листа.

```csharp
// Access the first worksheet (index 0)
Worksheet worksheet = workbook.Worksheets[0];
```

> **Совет:** если вы не уверены, на каком листе находится таблица, пройдитесь по `workbook.Worksheets` и проверьте `worksheet.Name`, пока не найдёте нужный.

## Шаг 3 — Получить таблицу (ListObject) с именем «MyTable»

Aspose.Cells представляет таблицы Excel как `ListObject`. Выбор правильной таблицы важен, потому что AutoFilter привязан к таблице, а не к всему листу.

```csharp
// Retrieve the table named "MyTable"
ListObject table = worksheet.ListObjects["MyTable"];
if (table == null)
{
    throw new InvalidOperationException("Table 'MyTable' not found in the worksheet.");
}
```

*Почему проверяем на null:* попытка очистить фильтр у несуществующей таблицы вызовет исключение во время выполнения. Защитный код выдаёт понятное сообщение об ошибке — гораздо лучше, чем непонятный стек‑трейс.

## Шаг 4 — Очистить AutoFilter у таблицы

Теперь переходим к основной части руководства: фактическому удалению фильтра. Установка свойства `AutoFilter` в `null` сообщает Aspose.Cells удалить любые применённые критерии фильтрации.

```csharp
// Remove any applied AutoFilter from the table
table.AutoFilter = null;
```

Эта строка делает две вещи:

1. **Очищает UI фильтра** — стрелки‑выпадающие исчезают, как при нажатии «Clear Filter» в Excel.  
2. **Сбрасывает представление данных** — все строки снова становятся видимыми, что часто требуется перед дальнейшей обработкой.

### Что делать, если нужно очистить фильтр только в одном столбце?

Если вы хотите оставить UI фильтра таблицы, но убрать фильтр из конкретного столбца, можно обратиться к фильтру столбца:

```csharp
// Example: clear filter on the first column only
if (table.AutoFilter != null && table.AutoFilter.ColumnFilters.Count > 0)
{
    table.AutoFilter.ColumnFilters[0].Clear();
}
```

Это вариант **clear excel table filter**, о котором спрашивают многие разработчики.

## Шаг 5 — Сохранить книгу (по желанию)

Если изменения должны сохраняться, запишите книгу обратно на диск. Можно перезаписать исходный файл или создать новую копию.

```csharp
// Save the workbook – choose a new file name to keep the original intact
workbook.Save(@"C:\MyProjects\ExcelDemo\output.xlsx");
```

*Почему можно пропустить этот шаг:* когда книга используется только в памяти (например, отправляется как вложение письма), запись на диск не требуется.

## Полный рабочий пример

Объединив всё вместе, получаем автономную программу, которую можно вставить в консольное приложение и сразу запустить:

```csharp
using System;
using Aspose.Cells;

namespace ExcelAutoFilterDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the workbook
            string inputPath = @"C:\MyProjects\ExcelDemo\input.xlsx";
            Workbook workbook = new Workbook(inputPath);

            // 2️⃣ Access the first worksheet
            Worksheet worksheet = workbook.Worksheets[0];

            // 3️⃣ Retrieve the table named "MyTable"
            ListObject table = worksheet.ListObjects["MyTable"];
            if (table == null)
            {
                Console.WriteLine("Error: Table 'MyTable' not found.");
                return;
            }

            // 4️⃣ Remove any applied AutoFilter from the table
            table.AutoFilter = null; // <-- this clears the filter

            // Optional: Save to a new file
            string outputPath = @"C:\MyProjects\ExcelDemo\output.xlsx";
            workbook.Save(outputPath);

            Console.WriteLine("AutoFilter removed and workbook saved to: " + outputPath);
        }
    }
}
```

**Ожидаемый результат:** откройте `output.xlsx` — стрелки фильтра исчезнут, и все строки будут видимы. Больше скрытых данных, таблица ведёт себя как обычный диапазон.

## Часто задаваемые вопросы и граничные случаи

### Что если рабочая книга использует старый формат `.xls`?

Aspose.Cells поддерживает как `.xlsx`, так и `.xls`. Достаточно изменить расширение в пути; тот же код будет работать, так как библиотека абстрагирует формат.

### Работает ли это с защищёнными листами?

Если лист защищён, его нужно сначала снять защиту:

```csharp
worksheet.Unprotect("yourPassword"); // remove protection
table.AutoFilter = null;              // clear filter
worksheet.Protect("yourPassword");    // re‑apply protection if needed
```

### Как очистить *все* фильтры во всей книге?

Пройдитесь по каждому листу и каждой таблице:

```csharp
foreach (Worksheet ws in workbook.Worksheets)
{
    foreach (ListObject lo in ws.ListObjects)
    {
        lo.AutoFilter = null;
    }
}
```

Это покрывает более общий сценарий **clear excel filter**.

### Можно ли использовать этот подход с Microsoft.Office.Interop.Excel вместо Aspose.Cells?

Да, но API отличается. С Interop вы бы работали с `Worksheet.AutoFilterMode` и вызывали `Worksheet.ShowAllData()`. Метод Aspose.Cells, показанный здесь, обычно быстрее и не требует установки Excel на сервере.

## Итоги

Мы рассмотрели всё, что нужно для **удаления автофильтра excel** с помощью C#:

1. **Загрузить книгу** (`load excel workbook c#`).  
2. **Найти лист** и **ListObject** (`MyTable`).  
3. **Очистить AutoFilter** (`remove autofilter`, `clear excel filter`).  
4. **Сохранить** изменения, если требуется их сохранить.

Теперь вы можете внедрять эту логику в более крупные конвейеры обработки данных, генерировать чистые отчёты или просто предоставлять пользователям свежий вид их данных.

## Что дальше?

* **Применить условное форматирование** после очистки фильтров — сделает данные более читаемыми.  
* **Экспортировать отфильтрованный (или неотфильтрованный) вид** в CSV с помощью `Table.ExportDataTableAsString()` для последующей обработки.  
* **Скомбинировать с EPPlus**, если нужен бесплатный альтернативный пакет — большинство концепций перенесутся без изменений.

Экспериментируйте: пробуйте очищать фильтры в нескольких таблицах, работать с файлами, защищёнными паролем, или даже переключать фильтры «на лету» в зависимости от ввода пользователя. Паттерн остаётся тем же, а результат — более плавная и предсказуемая автоматизация Excel.

Счастливого кодинга, и пусть ваши таблицы Excel остаются без фильтров, когда это необходимо!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}