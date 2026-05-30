---
category: general
date: 2026-05-30
description: Как использовать AutoFilter в автоматизации Excel на C#. Узнайте, как
  создать рабочую книгу Excel, отфильтровать строки по значению и упростить работу
  с электронными таблицами.
draft: false
keywords:
- how to use autofilter
- create excel workbook
- filter rows by value
- filter column b
- excel automation c#
language: ru
og_description: Как использовать AutoFilter в автоматизации Excel на C#. Овладейте
  созданием рабочей книги Excel, фильтрацией строк по значению и лёгкой автоматизацией
  таблиц.
og_title: Как использовать AutoFilter в автоматизации Excel на C# – полное руководство
schemas:
- author: Aspose
  dateModified: '2026-05-30'
  description: How to use AutoFilter in C# Excel automation. Learn how to create Excel
    workbook, filter rows by value, and streamline your spreadsheet tasks.
  headline: How to Use AutoFilter in C# Excel Automation – Full Step‑by‑Step Guide
  type: TechArticle
- description: How to use AutoFilter in C# Excel automation. Learn how to create Excel
    workbook, filter rows by value, and streamline your spreadsheet tasks.
  name: How to Use AutoFilter in C# Excel Automation – Full Step‑by‑Step Guide
  steps:
  - name: '**Creating the workbook** – `new Workbook()` gives you a clean file; `Worksheets[0]`
      grabs the default sheet.'
    text: '**Creating the workbook** – `new Workbook()` gives you a clean file; `Worksheets[0]`
      grabs the default sheet.'
  - name: '**Filling sample data** – We write a tiny dataset so you can see the filter
      in action.'
    text: '**Filling sample data** – We write a tiny dataset so you can see the filter
      in action.'
  - name: '**Adding a table** – `ListObjects.Add` converts the range into an Excel
      table, which automatically supports filtering and styling.'
    text: '**Adding a table** – `ListObjects.Add` converts the range into an Excel
      table, which automatically supports filtering and styling.'
  - name: '**Applying AutoFilter** – `table.AutoFilter.Filter(1, "Apple")` tells the
      engine: “Show only rows where the second column (B) equals *Apple*.”'
    text: '**Applying AutoFilter** – `table.AutoFilter.Filter(1, "Apple")` tells the
      engine: “Show only rows where the second column (B) equals *Apple*.”'
  - name: '**Saving files** – Two files are written: one filtered, one with the filter
      removed, proving that `RemoveAutoFilter()` works as expected.'
    text: '**Saving files** – Two files are written: one filtered, one with the filter
      removed, proving that `RemoveAutoFilter()` works as expected.'
  type: HowTo
- questions:
  - answer: Yes. Aspose.Cells can save to both `.xlsx` and `.xls` by changing the
      file extension or using `SaveOptions`.
    question: Does this work with older .xls files?
  - answer: Load the file with `new Workbook("path.xlsx")`, apply the filter, then
      `Save` again.
    question: What if I need to filter *after* the workbook is already saved?
  - answer: 'Absolutely. Use `worksheet.AutoFilter.Range = "A1:C5";` and then `worksheet.AutoFilter.ApplyFilter();`.
      However, tables give you built‑in styling and easier column referencing. ---
      ## Image – Visual Confirmation ![Screenshot showing AutoFilter applied to column
      B in an Excel workbook created with C#'
    question: Can I apply a filter to a *range* that isn’t a table?
  type: FAQPage
tags:
- C#
- Excel
- Automation
title: Как использовать AutoFilter в автоматизации Excel на C# — Полное пошаговое
  руководство
url: /ru/net/excel-autofilter-validation/how-to-use-autofilter-in-c-excel-automation-full-step-by-ste/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как использовать AutoFilter в автоматизации Excel на C# – Полное руководство

Когда‑то задавались вопросом **как использовать AutoFilter**, создавая Excel‑файлы из кода C#? Вы не одиноки — многие разработчики сталкиваются с этой проблемой, когда нужно скрыть строки, не соответствующие определённому критерию.  

В этом руководстве мы пройдём через конкретный, готовый к запуску пример, который **создаёт книгу Excel**, добавляет таблицу и затем **фильтрует строки по значению** в столбце B. К концу вы получите чистый, переиспользуемый фрагмент кода, который можно вставить в любой проект C#, требующий автоматизации Excel.

## Что вы узнаете

- Как настроить проект C# с библиотекой Aspose.Cells (или Microsoft.Office.Interop).  
- **Создание книги Excel** программно и добавление стилизованной таблицы.  
- Применение **AutoFilter** для отображения только строк, где **столбец B** равен заданной строке.  
- Полное удаление фильтра, восстановление полного набора данных.  
- Советы по обработке крайних случаев, таких как отсутствие столбцов или несколько критериев фильтрации.

Опыт работы с Excel‑VBA не требуется; достаточно базовых знаний C# и NuGet‑пакетов.

---

## Требования

| Требование | Почему это важно |
|------------|------------------|
| .NET 6.0 или новее (или .NET Framework 4.7+) | Современные среды выполнения обеспечивают лучшую производительность и более удобное управление пакетами. |
| Aspose.Cells for .NET (или Microsoft.Office.Interop.Excel), установленный через NuGet | Эта библиотека предоставляет объекты `Workbook`, `Worksheet` и `Table`, используемые в коде. |
| Редактор кода (Visual Studio, VS Code, Rider и т.д.) | Вам понадобится скомпилировать и запустить пример. |
| Базовые знания C# | Руководство объясняет *почему* каждая строка существует, а не только *что* она делает. |

Установить Aspose.Cells можно так:

```bash
dotnet add package Aspose.Cells
```

---

## Как использовать AutoFilter с Aspose.Cells в C#

Ниже приведена полная, автономная программа. Сохраните её как `Program.cs` в консольном проекте и запустите — в папке вывода появится `FilteredWorkbook.xlsx`.

```csharp
using System;
using Aspose.Cells;

namespace ExcelAutoFilterDemo
{
    class Program
    {
        static void Main()
        {
            // -------------------------------------------------
            // Step 1: Create an Excel workbook and grab the first worksheet
            // -------------------------------------------------
            Workbook workbook = new Workbook();               // creates a new, empty workbook
            Worksheet sheet = workbook.Worksheets[0];         // the default sheet is named "Sheet1"

            // Populate the sheet with sample data (A‑C columns, 5 rows)
            sheet.Cells["A1"].PutValue("ID");
            sheet.Cells["B1"].PutValue("Fruit");
            sheet.Cells["C1"].PutValue("Quantity");

            sheet.Cells["A2"].PutValue(1);
            sheet.Cells["B2"].PutValue("Apple");
            sheet.Cells["C2"].PutValue(10);

            sheet.Cells["A3"].PutValue(2);
            sheet.Cells["B3"].PutValue("Banana");
            sheet.Cells["C3"].PutValue(15);

            sheet.Cells["A4"].PutValue(3);
            sheet.Cells["B4"].PutValue("Apple");
            sheet.Cells["C4"].PutValue(7);

            sheet.Cells["A5"].PutValue(4);
            sheet.Cells["B5"].PutValue("Cherry");
            sheet.Cells["C5"].PutValue(20);

            // -------------------------------------------------
            // Step 2: Convert the range into a ListObject (Excel table)
            // -------------------------------------------------
            // Parameters: firstRow, firstColumn, totalRows, totalColumns, hasHeaders
            int tableIdx = sheet.ListObjects.Add(0, 0, 5, 3, true);
            ListObject table = sheet.ListObjects[tableIdx];
            table.TableStyleType = TableStyleType.TableStyleMedium2; // nice built‑in styling

            // -------------------------------------------------
            // Step 3: Apply an AutoFilter to show only rows where column B = "Apple"
            // -------------------------------------------------
            // The AutoFilter is attached to the table’s range automatically.
            // We target column B (index 1) and set the criteria.
            table.AutoFilter.Filter(1, "Apple"); // 1 = zero‑based column index for B

            // -------------------------------------------------
            // Step 4: Save the filtered workbook to disk
            // -------------------------------------------------
            workbook.Save("FilteredWorkbook.xlsx");

            // -------------------------------------------------
            // Step 5: (Optional) Remove the AutoFilter completely
            // -------------------------------------------------
            // This demonstrates that you can revert to the full dataset without re‑loading.
            table.RemoveAutoFilter();   // clears the filter
            workbook.Save("UnfilteredWorkbook.xlsx");

            Console.WriteLine("Workbook created and filtered successfully.");
        }
    }
}
```

### Как работает код

1. **Создание книги** – `new Workbook()` создаёт чистый файл; `Worksheets[0]` берёт лист по умолчанию.  
2. **Заполнение примерными данными** – Мы записываем небольшую выборку, чтобы вы могли увидеть работу фильтра.  
3. **Добавление таблицы** – `ListObjects.Add` преобразует диапазон в таблицу Excel, которая автоматически поддерживает фильтрацию и стилизацию.  
4. **Применение AutoFilter** – `table.AutoFilter.Filter(1, "Apple")` говорит движку: «Показать только строки, где второй столбец (B) равен *Apple*».  
5. **Сохранение файлов** – Записываются два файла: один отфильтрованный, другой без фильтра, что подтверждает работу `RemoveAutoFilter()`.

> **Совет:** Если нужно фильтровать по нескольким критериям (например, “Apple” *или* “Banana”), используйте перегрузку `Filter(int columnIndex, string criteria1, string criteria2)` или передайте массив строк.

---

## Фильтрация строк по значению – типичные варианты

Хотя пример выше сосредоточен на **фильтрации столбца B**, вы можете фильтровать другие столбцы или использовать числовые критерии. Ниже быстрый шпаргалка:

| Желаемый фильтр | Фрагмент кода |
|-----------------|----------------|
| Текстовое совпадение в столбце C | `table.AutoFilter.Filter(2, "Cherry");` |
| Числа больше 10 в столбце C | `table.AutoFilter.CustomFilter(2, "10", OperatorType.GreaterThan);` |
| Несколько значений в столбце B | `table.AutoFilter.Filter(1, new[] { "Apple", "Banana" });` |

**Крайний случай:** Если заголовок столбца написан с ошибкой или индекс столбца выходит за пределы, Aspose.Cells бросит `ArgumentException`. Защититесь, проверив `table.ListColumns.Count` перед применением фильтра.

---

## Удаление AutoFilter – когда сбрасывать

Иногда требуется снова показать весь набор данных (например, после очистки поля поиска пользователем). Вызов `table.RemoveAutoFilter()` решает задачу одной строкой. Если вы используете Microsoft.Office.Interop, то следует установить `worksheet.AutoFilterMode = false;`.

---

## Полный рабочий пример (без комментариев)

Ниже ещё раз весь код программы, без комментариев, для тех, кто предпочитает лаконичный вид:

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];

        ws.Cells["A1"].PutValue("ID");
        ws.Cells["B1"].PutValue("Fruit");
        ws.Cells["C1"].PutValue("Quantity");

        ws.Cells["A2"].PutValue(1); ws.Cells["B2"].PutValue("Apple");  ws.Cells["C2"].PutValue(10);
        ws.Cells["A3"].PutValue(2); ws.Cells["B3"].PutValue("Banana"); ws.Cells["C3"].PutValue(15);
        ws.Cells["A4"].PutValue(3); ws.Cells["B4"].PutValue("Apple");  ws.Cells["C4"].PutValue(7);
        ws.Cells["A5"].PutValue(4); ws.Cells["B5"].PutValue("Cherry"); ws.Cells["C5"].PutValue(20);

        int idx = ws.ListObjects.Add(0, 0, 5, 3, true);
        ListObject tbl = ws.ListObjects[idx];
        tbl.TableStyleType = TableStyleType.TableStyleMedium2;

        tbl.AutoFilter.Filter(1, "Apple");
        wb.Save("FilteredWorkbook.xlsx");

        tbl.RemoveAutoFilter();
        wb.Save("UnfilteredWorkbook.xlsx");
    }
}
```

При запуске будет создано два файла:

- **FilteredWorkbook.xlsx** – видны только строки с *Apple*.  
- **UnfilteredWorkbook.xlsx** – исходные данные восстановлены.

---

## Часто задаваемые вопросы

**В: Работает ли это со старыми файлами .xls?**  
О: Да. Aspose.Cells может сохранять как в `.xlsx`, так и в `.xls`, меняя расширение файла или используя `SaveOptions`.

**В: Что делать, если нужно отфильтровать *после* сохранения книги?**  
О: Загрузите файл с помощью `new Workbook("path.xlsx")`, примените фильтр и снова `Save`.

**В: Можно ли применить фильтр к *диапазону*, который не является таблицей?**  
О: Конечно. Используйте `worksheet.AutoFilter.Range = "A1:C5";`, затем `worksheet.AutoFilter.ApplyFilter();`. Однако таблицы предоставляют встроенную стилизацию и более удобную ссылку на столбцы.

---

## Изображение – визуальное подтверждение

![Скриншот, показывающий применённый AutoFilter к столбцу B в книге Excel, созданной с помощью C#](/images/autofilter-column-b.png "AutoFilter на столбце B")

*(Изображение иллюстрирует отфильтрованный вид, где остаются только строки, содержащие “Apple”.)*

---

## Заключение

Мы только что рассмотрели **как использовать AutoFilter** в сценарии автоматизации Excel на C#, от **создания книги Excel** до **фильтрации строк по значению** в **столбце B**, и, наконец, **удаления фильтра**, когда он больше не нужен. Основные шаги — инициализация, добавление таблицы, применение фильтра и очистка — переиспользуемы в любом проекте, требующем **excel automation c#**.

Готовы к следующему вызову? Попробуйте:

- Добавить условное форматирование для выделения отфильтрованных строк.  
- Экспортировать отфильтрованные данные в CSV для дальнейшей обработки.  
- Скомбинировать несколько фильтров (например, “Apple” *и* количество > 8).

Экспериментируйте, ломайте, а затем исправляйте—

## Что изучать дальше?

- [Как реализовать AutoFilter в Excel с помощью Aspose.Cells для .NET (Руководство по анализу данных)](/cells/english/net/data-analysis/implement-autofilter-excel-aspose-cells-dotnet/)
- [Как использовать Autofilter Not Contains в Aspose.Cells .NET для анализа данных Excel](/cells/english/net/data-analysis/master-autofilter-not-contains-aspose-cells-net/)
- [Как реализовать Excel Autofilter 'EndsWith' с использованием Aspose.Cells для .NET](/cells/english/net/data-analysis/implement-autofilter-endswith-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}