---
category: general
date: 2026-07-03
description: Как использовать SEQUENCE в C# для генерации последовательных чисел в
  Excel. Узнайте, как создать рабочую книгу Excel на C# и ASP.NET, создав файл Excel
  несколькими строками кода.
draft: false
keywords:
- how to use sequence
- create excel workbook c#
- asp.net create excel file
- generate incremental numbers excel
language: ru
og_description: Как использовать SEQUENCE в C# для генерации последовательных чисел
  в Excel. Пошаговое руководство по созданию рабочей книги Excel на C# и ASP.NET,
  создание файла Excel.
og_title: Как использовать SEQUENCE в C# – Создание рабочей книги Excel
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: How to use SEQUENCE in C# to generate incremental numbers in Excel.
    Learn to create Excel workbook C# and ASP.NET create Excel file with a few lines
    of code.
  headline: How to Use SEQUENCE in C# – Create Excel Workbook
  type: TechArticle
- description: How to use SEQUENCE in C# to generate incremental numbers in Excel.
    Learn to create Excel workbook C# and ASP.NET create Excel file with a few lines
    of code.
  name: How to Use SEQUENCE in C# – Create Excel Workbook
  steps:
  - name: Why Use SEQUENCE Instead of a Loop?
    text: '- **Performance** – Excel does the math on its own engine, which is highly
      optimized. - **Maintainability** – The formula is self‑documenting; anyone opening
      the sheet instantly knows the intent. - **Dynamic resizing** – Change the `rows`
      argument and the spill range expands automatically.'
  - name: Pro Tip
    text: 'If you need the workbook in memory (e.g., to send it over a web API), use
      a `MemoryStream`:'
  - name: What If the Client Uses an Older Excel Version?
    text: 'Dynamic arrays (including `SEQUENCE`) were introduced in Excel 365/2019.
      If you need backward compatibility, fall back to a manual fill:'
  type: HowTo
- questions:
  - answer: No. `SEQUENCE` is a non‑iterative function; a simple `CalculateFormula()`
      call is enough.
    question: Do I need to enable iterative calculation?
  - answer: 'Change the second argument: `=SEQUENCE(1,5,10,2)` spills across B1:F1.'
    question: What if I want a horizontal spill?
  - answer: Absolutely. For example, `=INDEX(A:A, SEQUENCE(5,1,10,2))` can pull rows
      from another column.
    question: Can I combine SEQUENCE with other functions?
  - answer: The file size impact of a formula is negligible. Only when you start populating
      millions of cells manually does size become an issue.
    question: Is the workbook size a concern?
  type: FAQPage
tags:
- C#
- Excel
- Aspose.Cells
- ASP.NET
title: Как использовать SEQUENCE в C# — создать книгу Excel
url: /ru/net/formulas-functions/how-to-use-sequence-in-c-create-excel-workbook/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как использовать SEQUENCE в C# – Создание Excel‑книги

Когда‑то задавались вопросом **как использовать SEQUENCE**, чтобы вывести список чисел в лист Excel из C#? Вы не одиноки. Будь то построение панели отчётов, заполнение data‑grid или просто быстрый способ сгенерировать ID, освоение этого приёма избавит вас от написания циклов.

В этом руководстве мы **создадим Excel‑книгу в C#**, вставим динамическую формулу `SEQUENCE` в ячейку A1 и получим красивый столбец последовательных чисел. Мы также покажем, как отдать этот файл из контроллера ASP.NET — да, **ASP.NET create Excel file** тоже будет покрыт. К концу вы сможете **генерировать последовательные числа в стиле Excel** одной строкой кода.

## Что понадобится

- .NET 6+ (код также работает на .NET Framework 4.6+)  
- NuGet‑пакет **Aspose.Cells for .NET** (или любая библиотека, предоставляющая объекты `Workbook`/`Worksheet`)  
- Базовый проект ASP.NET Core или MVC, если хотите попробовать часть с загрузкой через веб  

Это всё. Никаких дополнительных COM‑интеропов, установка Office не требуется.

---

## Как использовать SEQUENCE для генерации последовательных чисел

Функция Excel `SEQUENCE(rows, [columns], [start], [step])` возвращает диапазон **spill**. В нашем случае нам нужно 5 строк, 1 столбец, начать с 10, шаг 2. Формула выглядит так:

```excel
=SEQUENCE(5,1,10,2)
```

При вычислении Excel ячейки A1:A5 будут содержать **10, 12, 14, 16, 18**. Прелесть в том, что нам не нужны циклы в C# — формула делает всю тяжёлую работу.

Ниже полный фрагмент C#, который создаёт книгу, вставляет формулу, принудительно вычисляет её и сохраняет файл.

```csharp
using Aspose.Cells;
using System.IO;

// 1️⃣ Create a new workbook
Workbook workbook = new Workbook();

// 2️⃣ Grab the first worksheet (Aspose creates one by default)
Worksheet sheet = workbook.Worksheets[0];

// 3️⃣ Insert the SEQUENCE formula – this will spill a 5‑row column starting at 10, step 2
sheet.Cells["A1"].Formula = "=SEQUENCE(5,1,10,2)";

// 4️⃣ Force calculation so the spilled range is materialized
workbook.CalculateFormula();

// 5️⃣ Save to disk (you can change the path as needed)
workbook.Save("DynamicArray.xlsx");
```

**Ожидаемый результат** — откройте *DynamicArray.xlsx* и увидите:

| A |
|---|
| 10 |
| 12 |
| 14 |
| 16 |
| 18 |

Это и есть вся история **how to use sequence** в C#. Просто, верно? Но давайте копнём чуть глубже.

### Почему использовать SEQUENCE вместо цикла?

- **Производительность** — Excel считает на собственном движке, который сильно оптимизирован.
- **Поддерживаемость** — Формула самодокументируемая; любой, открывший лист, сразу понимает намерение.
- **Динамическое изменение размера** — Изменив параметр `rows`, диапазон spill расширится автоматически.

---

## Создание Excel‑книги C# – Шаг за шагом

Если вы новичок в **create excel workbook c#**, ниже чек‑лист поможет избежать типичных ошибок.

1. **Добавьте пакет Aspose.Cells**  
   ```bash
   dotnet add package Aspose.Cells
   ```
   (Можно также использовать ClosedXML или EPPlus, но показанный API соответствует коду выше.)

2. **Установите лицензию** (опционально для trial).  
   ```csharp
   var license = new Aspose.Cells.License();
   license.SetLicense("Aspose.Total.NET.lic");
   ```

3. **Создайте экземпляр `Workbook`** — получаем чистую, пустую книгу.

4. **Получите лист** — `workbook.Worksheets[0]` — это лист по умолчанию с именем *Sheet1*.

5. **Примените формулу SEQUENCE** — как показано ранее.

6. **Вычислите** — `workbook.CalculateFormula()` принудительно создаёт spill; иначе в файле будет только формула.

7. **Сохраните** — можно записать на диск, в `MemoryStream` или напрямую в HTTP‑ответ.

### Pro Tip

Если нужен workbook в памяти (например, чтобы отправить его через веб‑API), используйте `MemoryStream`:

```csharp
using var ms = new MemoryStream();
workbook.Save(ms, SaveFormat.Xlsx);
byte[] excelBytes = ms.ToArray(); // ready to return or attach
```

---

## ASP.NET Create Excel File – Потоковая передача в браузер

Теперь, когда мы знаем **create excel workbook c#**, интегрируем это в контроллер ASP.NET Core, чтобы пользователи могли скачать файл «на лету».

```csharp
using Aspose.Cells;
using Microsoft.AspNetCore.Mvc;
using System.IO;

[Route("api/[controller]")]
public class ExcelController : ControllerBase
{
    [HttpGet("download")]
    public IActionResult Download()
    {
        // 1️⃣ Build the workbook (same steps as before)
        var workbook = new Workbook();
        var sheet = workbook.Worksheets[0];
        sheet.Cells["A1"].Formula = "=SEQUENCE(5,1,10,2)";
        workbook.CalculateFormula();

        // 2️⃣ Save to a memory stream
        using var ms = new MemoryStream();
        workbook.Save(ms, SaveFormat.Xlsx);
        ms.Position = 0; // reset stream position

        // 3️⃣ Return the file as a download
        const string fileName = "DynamicArray.xlsx";
        return File(ms, 
                    "application/vnd.openxmlformats-officedocument.spreadsheetml.sheet", 
                    fileName);
    }
}
```

Когда пользователь обращается к `/api/excel/download`, браузер предлагает загрузить *DynamicArray.xlsx*. Файл уже содержит **generated incremental numbers excel**‑столбец благодаря формуле `SEQUENCE`.

### Что если клиент использует более старую версию Excel?

Динамические массивы (включая `SEQUENCE`) появились в Excel 365/2019. Если нужна обратная совместимость, используйте обычное заполнение:

```csharp
// Alternative for older Excel: write numbers directly
for (int i = 0; i < 5; i++)
{
    sheet.Cells[i, 0].PutValue(10 + i * 2); // column 0 = A
}
```

Этот фрагмент демонстрирует классический подход **generate incremental numbers excel** без применения новой функции.

---

## Часто задаваемые вопросы и особые случаи

- **Нужно ли включать итеративные вычисления?**  
  Нет. `SEQUENCE` — неитеративная функция; достаточно простого вызова `CalculateFormula()`.

- **Как получить горизонтальный spill?**  
  Измените второй аргумент: `=SEQUENCE(1,5,10,2)` разливается по B1:F1.

- **Можно ли комбинировать SEQUENCE с другими функциями?**  
  Конечно. Например, `=INDEX(A:A, SEQUENCE(5,1,10,2))` может вытягивать строки из другого столбца.

- **Влияет ли размер книги на производительность?**  
  Влияние формулы на размер файла пренебрежимо. Значительный рост происходит только при ручном заполнении миллионов ячеек.

---

## Заключение

Мы прошли путь от **how to use sequence** в C# до **create excel workbook c#**, отдали книгу через **ASP.NET create excel file** и продемонстрировали чистый способ **generate incremental numbers excel** без написания циклов. Главный вывод: позвольте движку динамических массивов Excel выполнять подсчёт, а вашему .NET‑коду сосредотачиваться на оркестрации.

Экспериментируйте — меняйте параметры `rows`, `start` или `step`, разливайте горизонтально, комбинируйте формулу с `IF` или `FILTER` для более сложных отчётов. Когда будете готовы, попробуйте связать несколько листов или экспортировать книгу в CSV для последующей обработки.

Есть интересный приём, которым хотите поделиться? Оставляйте комментарий ниже или пишите мне на GitHub. Приятного кодинга!

## Что изучать дальше?

Следующие руководства охватывают смежные темы, расширяющие техники, продемонстрированные в этом гайде. Каждый ресурс содержит полностью рабочие примеры кода с пошаговыми объяснениями, помогающими освоить дополнительные возможности API и исследовать альтернативные подходы в ваших проектах.

- [Как создать и настроить Excel‑книги с помощью Aspose.Cells .NET: пошаговое руководство](/cells/english/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)
- [Как создать и сохранить Excel‑файлы с помощью Aspose.Cells для .NET: полное руководство](/cells/english/net/workbook-operations/create-save-excel-file-aspose-cells-dotnet/)
- [Как создавать и оформлять Excel‑книги с помощью Aspose.Cells для .NET (руководство 2023)](/cells/english/net/formatting/create-style-excel-workbooks-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}