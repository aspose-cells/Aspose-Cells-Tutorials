---
category: general
date: 2026-02-26
description: Как экспортировать Excel в табуляцией разделённый TXT‑файл с помощью
  C#. Узнайте, как экспортировать Excel как табуляцию, преобразовать Excel в TXT и
  экспортировать Excel с разделителем в три простых шага.
draft: false
keywords:
- how to export excel
- export excel as tab
- convert excel to txt
- export excel with delimiter
- export excel range
language: ru
og_description: как экспортировать Excel в таб‑разделённый txt‑файл с помощью C#.
  Этот учебник показывает экспорт Excel как таб, конвертацию Excel в txt и экспорт
  Excel с разделителем.
og_title: как экспортировать Excel — руководство по табличному тексту с разделителями
tags:
- csharp
- excel
- file-conversion
title: Как экспортировать Excel – руководство по табличному тексту с разделителями
  табуляции
url: /ru/net/converting-excel-files-to-other-formats/how-to-export-excel-tab-delimited-text-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# как экспортировать excel – Полный учебник C# Tutorial

Ever wondered **how to export excel** data into a plain‑text file without losing formatting? Maybe you need a quick TSV (tab‑separated values) for a data‑pipeline, or you’re feeding a legacy system that only reads `.txt`. Either way, you’re not alone—developers constantly hit this wall when moving data out of spreadsheets.

The good news? In just three straightforward steps you can **export excel as tab**‑delimited text, **convert excel to txt**, and even pick a custom delimiter if you change your mind later. Below you’ll see a fully runnable C# example, why each line matters, and a handful of tips to avoid the usual pitfalls.

> **Pro tip:** Этот подход работает с популярной библиотекой Aspose.Cells, но концепции применимы к любой .NET Excel API, предоставляющей метод в стиле `ExportTable`.

## Что понадобится

- **.NET 6+** (или .NET Framework 4.6+). Код компилируется на любой современной среде выполнения.
- **Aspose.Cells for .NET** (бесплатная пробная версия или лицензия). Установите через NuGet: `dotnet add package Aspose.Cells`.
- Входная рабочая книга с именем `input.xlsx`, размещённая в папке, которой вы управляете.
- Небольшая доля любопытства — глубокие внутренности Excel не требуются.

Если у вас уже всё есть, давайте сразу перейдём к решению.

## Шаг 1 – Загрузите рабочую книгу, которую хотите экспортировать

Сначала мы создаём объект `Workbook`, указывающий на исходный файл. Этот объект представляет весь файл Excel, включая все листы, именованные диапазоны и форматирование.

```csharp
using Aspose.Cells;

// Step 1: Load the workbook that contains the data to export
Workbook workbook = new Workbook(@"C:\Data\input.xlsx");
```

*Почему это важно:*  
Загрузка рабочей книги даёт доступ к коллекции листов (`workbook.Worksheets`). Без этого объекта вы не сможете обращаться к ячейкам, диапазонам или настройкам экспорта.

> **Note:** Если ваш файл находится в сетевом ресурсе, добавьте префикс `\\` или используйте UNC‑путь — Aspose.Cells справится без проблем.

## Шаг 2 – Настройте параметры экспорта (строковые значения и табуляция)

Теперь мы указываем библиотеке, как записывать данные. Установив `ExportAsString = true`, мы заставляем каждую ячейку рассматривать как обычную строку, что устраняет локализованные числовые форматы Excel. Часть `Delimiter = "\t"` является ядром **export excel as tab**.

```csharp
// Step 2: Configure the export options – export values as strings and use a tab delimiter
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true,   // ensures numbers become plain text, not scientific notation
    Delimiter = "\t"         // tab character – perfect for TSV files
};
```

*Почему это важно:*  
Если пропустить `ExportAsString`, ячейка с `12345` может превратиться в `12,345` в некоторых локалях, ломая последующие парсеры. Разделитель можно заменить на запятые, вертикальные черты или любой символ, если позже вы решите **export excel with delimiter** отличный от табуляции.

## Шаг 3 – Экспортируйте конкретный диапазон в текстовый файл

Наконец, мы выбираем интересующий нас диапазон (`A1:D10` в этом примере) и записываем его в `out.txt`. Метод `ExportTable` выполняет всю тяжёлую работу: читает ячейки, применяет параметры и записывает результат на диск.

```csharp
// Step 3: Export the range A1:D10 from the first worksheet to a text file
Worksheet sheet = workbook.Worksheets[0]; // first worksheet (index 0)
sheet.Cells.ExportTable("A1", "D10", @"C:\Data\out.txt", exportOptions);
```

После выполнения вы найдёте `out.txt` с содержимым, похожим на:

```
Name    Age    City    Score
Alice   30     NY      85
Bob     25     LA      90
...
```

Каждый столбец разделён **табуляцией**, что делает файл готовым для `awk`, `PowerShell` или любого инструмента, совместимого с CSV и поддерживающего табуляцию.

### Быстрая проверка

Откройте сгенерированный файл в простом текстовом редакторе (Notepad, VS Code) и проверьте:

1. Столбцы выравниваются, когда включён режим “Show whitespace”.
2. Нет лишних кавычек или запятых.
3. Все числовые ячейки отображаются точно так же, как в Excel (благодаря `ExportAsString`).

Если что‑то выглядит неверно, дважды проверьте, что исходная рабочая книга не скрывает строки/столбцы, и убедитесь, что вы указали правильный индекс листа.

## Общие варианты и граничные случаи

### Экспорт всего листа

Если вы хотите **export excel range**, охватывающий весь лист, можно использовать `sheet.Cells.MaxDisplayRange`:

```csharp
var maxRange = sheet.Cells.MaxDisplayRange;
sheet.Cells.ExportTable(maxRange.FirstRow, maxRange.FirstColumn,
                       maxRange.RowCount, maxRange.ColumnCount,
                       @"C:\Data\fullSheet.txt", exportOptions);
```

### Использование другого разделителя

Переключение с табуляции на вертикальную черту (`|`) так же просто, как изменить одну строку:

```csharp
exportOptions.Delimiter = "|"; // now we have a pipe‑delimited file
```

Это удовлетворяет сценарию **export excel with delimiter** без переписывания остального кода.

### Обработка больших файлов (> 100 МБ)

Для огромных книг рекомендуется потоковый экспорт, чтобы избежать загрузки всего в память:

```csharp
using (FileStream fs = new FileStream(@"C:\Data\largeOut.txt", FileMode.Create, FileAccess.Write))
{
    sheet.Cells.ExportTable("A1", "Z5000", fs, exportOptions);
}
```

### Конвертация нескольких листов за один проход

Если вам нужно **convert excel to txt** для нескольких листов, выполните цикл по ним:

```csharp
for (int i = 0; i < workbook.Worksheets.Count; i++)
{
    string outPath = $@"C:\Data\Sheet{i + 1}.txt";
    workbook.Worksheets[i].Cells.ExportTable("A1", "D10", outPath, exportOptions);
}
```

Каждый лист получает собственный TSV‑файл — удобно для пакетных задач.

## Полный рабочий пример (готов к копированию и вставке)

Ниже представлен весь код программы, готовый к компиляции. Просто замените пути к файлам на свои.

```csharp
using System;
using Aspose.Cells;

namespace ExcelToTxtDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the workbook
            string inputPath = @"C:\Data\input.xlsx";
            Workbook workbook = new Workbook(inputPath);

            // 2️⃣ Set export options – strings + tab delimiter
            ExportTableOptions exportOptions = new ExportTableOptions
            {
                ExportAsString = true,
                Delimiter = "\t"
            };

            // 3️⃣ Export range A1:D10 from the first worksheet
            Worksheet sheet = workbook.Worksheets[0];
            string outputPath = @"C:\Data\out.txt";
            sheet.Cells.ExportTable("A1", "D10", outputPath, exportOptions);

            Console.WriteLine($"Export complete! Check {outputPath}");
        }
    }
}
```

**Ожидаемый результат:** Файл с именем `out.txt`, где каждый столбец разделён символом табуляции, и значение каждой ячейки точно соответствует тому, что в Excel.

## Часто задаваемые вопросы

- **Работает ли это с файлами .xls?**  
  Да. Aspose.Cells автоматически определяет формат, поэтому вы можете передать `Workbook` старый `.xls`, и тот же код будет работать.

- **Что если мои данные содержат табуляцию?**  
  Табуляции внутри ячейки сохраняются, что может нарушить работу TSV‑парсеров. В этом случае рассмотрите возможность переключения на разделитель‑вертикальную черту (`|`), изменив `exportOptions.Delimiter`.

- **Могу ли я экспортировать формулы вместо значений?**  
  Установите `exportOptions.ExportAsString = false` и используйте перегрузку `ExportTableOptions`, включающую `ExportFormula = true`. Вывод будет содержать исходный текст формулы.

- **Можно ли пропустить скрытые строки?**  
  Да. Установите `exportOptions.ExportHiddenRows = false` (по умолчанию `true`). Скрытые строки будут исключены из итогового текстового файла.

## Заключение

Теперь у вас есть надёжный, готовый к продакшену рецепт для **how to export excel** данных в файл с табуляцией, как **export excel as tab**, и как **convert excel to txt** с полным контролем над разделителями и выбором диапазона. Используя метод `ExportTable` из Aspose.Cells, вы избегаете ручного построения CSV, сохраняете точность данных и поддерживаете чистоту кода.

Готовы к следующему вызову? Попробуйте:

- Экспортировать напрямую в `MemoryStream` для веб‑API.  
- Динамически добавлять строку заголовка на основе содержимого первой строки.  
- Интегрировать эту процедуру в Azure Function, отслеживающую хранилище на предмет новых загрузок Excel.

Запустите, поиграйте с разделителем, и пусть данные текут туда, куда вам нужно. Приятного кодинга!  

<img src="export-excel.png" alt="how to export excel example" style="max-width:100%; height:auto;" />

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}