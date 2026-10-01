---
category: general
date: 2026-10-01
description: Узнайте, как создать книгу Excel на C#, применить пользовательский числовой
  формат, задать количество знаков после запятой в ячейке и сохранить книгу в формате
  XLSX в полном пошаговом руководстве.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook c#
- apply custom number format
- how to format numbers excel
- set cell decimal places
- save workbook as xlsx
language: ru
lastmod: 2026-10-01
og_description: Создайте книгу Excel на C# с пользовательским числовым форматом, задайте
  количество знаков после запятой в ячейке и сохраните книгу в формате XLSX. Следуйте
  этому полному руководству для точного вывода чисел.
og_image_alt: Screenshot of an Excel sheet showing numbers rounded to four significant
  digits
og_title: Создание Excel‑книги в C# – пользовательский числовой формат и экспорт в
  XLSX
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Learn how to create Excel workbook C# and apply custom number format,
    set cell decimal places, and save workbook as XLSX in a complete step‑by‑step
    guide.
  headline: How to create Excel workbook C# with custom number formatting
  type: TechArticle
- description: Learn how to create Excel workbook C# and apply custom number format,
    set cell decimal places, and save workbook as XLSX in a complete step‑by‑step
    guide.
  name: How to create Excel workbook C# with custom number formatting
  steps:
  - name: Run the program (`dotnet run`).
    text: Run the program (`dotnet run`).
  - name: Open `SigDigits.xlsx`.
    text: Open `SigDigits.xlsx`.
  - name: Confirm that **A1** reads `123.5`.
    text: Confirm that **A1** reads `123.5`.
  - name: If you open the file’s XML (`.xlsx` is a zip archive), you’ll see the custom
      format `"0.######"` stored in the `<c>` element’s `s` attribute.
    text: If you open the file’s XML (`.xlsx` is a zip archive), you’ll see the custom
      format `"0.######"` stored in the `<c>` element’s `s` attribute.
  type: HowTo
tags:
- Excel
- C#
- Aspose.Cells
title: Как создать рабочую книгу Excel в C# с пользовательским форматированием чисел
url: /ru/net/excel-custom-number-date-formatting/how-to-create-excel-workbook-c-with-custom-number-formatting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как создать Excel workbook C# с пользовательским форматированием чисел

Если вам нужно **create excel workbook c#**, который отображает числа точно так, как вы хотите, это руководство покажет, как сделать это в нескольких простых шагах. Вы научитесь применять пользовательский числовой формат, задавать количество десятичных знаков в ячейке и, наконец, **save workbook as xlsx** для дальнейшего использования.

Работа с числовыми данными часто требует баланса между точностью и читаемостью. К концу этого руководства у вас будет переиспользуемый шаблон, который ограничивает отображаемые цифры определённым количеством значимых цифр, сохраняя при этом исходное значение в файле. Внешние скрипты не требуются — только C# и библиотека Aspose.Cells.

## Необходимые условия

* .NET 6.0 SDK или более поздняя версия, установленная  
* Visual Studio 2022 (или любая IDE для C#)  
* Пакет NuGet **Aspose.Cells for .NET** (`Install-Package Aspose.Cells`) — эта библиотека предоставляет классы `Workbook`, `Worksheet` и `ExportTableOptions`, используемые в примерах.  

Эти требования минимальны; тот же код работает в .NET Core, .NET Framework и даже в Azure Functions.

## Шаг 1: Create Excel workbook C# — инициализация файла

Первая операция — создать новый объект `Workbook`. Этот объект представляет весь Excel‑файл в памяти и автоматически содержит лист по умолчанию.

```csharp
using Aspose.Cells;

namespace ExcelDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create a new workbook and get the first worksheet
            Workbook workbook = new Workbook();               // creates an empty .xlsx container
            Worksheet sheet = workbook.Worksheets[0];         // reference to the default sheet
```

**Почему это важно:**  
Создание рабочей книги заранее предоставляет чистый холст. Лист по умолчанию (`Worksheets[0]`) готов к вводу данных, поэтому вам не нужно добавлять новый лист, если ваш сценарий не требует нескольких вкладок.

## Шаг 2: Записать числовое значение в ячейку

Теперь поместите пример числа в ячейку **A1**. Значение, которое мы используем (`123.456789`), содержит больше десятичных знаков, чем мы в конечном итоге хотим отображать, что позволяет позже продемонстрировать округление.

```csharp
            // Step 2: Write a numeric value to cell A1
            sheet.Cells[0, 0].PutValue(123.456789); // row 0, column 0 = A1
```

**Подсказка:** `PutValue` автоматически определяет тип данных, поэтому вам не нужно преобразовывать число в строку.

## Шаг 3: Применить пользовательский числовой формат — ограничить отображаемые десятичные знаки

Чтобы контролировать, как Excel отображает число, мы создаём `Style` с **custom number format**. Шаблон `"0.######"` указывает Excel отображать до шести десятичных знаков, но опускать конечные нули.

```csharp
            // Step 3: Define a custom number format (up to 6 decimal places) and apply it
            Style customStyle = workbook.CreateStyle();
            customStyle.Custom = "0.######";               // up to 6 decimals, no trailing zeros
            sheet.Cells[0, 0].SetStyle(customStyle);
```

**Как это работает:**  
Строка формата следует синтаксису пользовательских форматов Excel. `0` принудительно отображает цифру, а `#` показывает цифру только если она значимая. Комбинируя их, вы получаете гибкое отображение, которое всё ещё сохраняет исходную точность.

## Шаг 4: Задать количество десятичных знаков в ячейке — используя ExportTableOptions

Если вам нужно **set cell decimal places** для экспортируемых данных (например, при преобразовании в DataTable), Aspose.Cells позволяет указать количество **significant digits**. Этот шаг гарантирует, что экспортированный CSV или DataTable будет соблюдать те же правила округления, которые вы применили в рабочей книге.

```csharp
            // Step 4: Configure export options to limit the output to 4 significant digits
            ExportTableOptions exportOptions = new ExportTableOptions();
            exportOptions.SignificantDigits = 4;           // round to 4 significant figures
```

**Почему использовать `SignificantDigits`?**  
В отличие от фиксированного количества десятичных знаков, значимые цифры сохраняют порядок числа, ограничивая точность, что часто ожидают аналитики при суммировании данных.

## Шаг 5: Экспортировать данные листа и **save workbook as xlsx**

Наконец, экспортируйте данные (если нужен DataTable) и сохраните рабочую книгу на диск. Вызов `ExportDataTable` учитывает настроенные `ExportTableOptions`, а `workbook.Save` записывает стандартный файл XLSX.

```csharp
            // Step 5: Export the worksheet data using the configured options and save the workbook
            sheet.ExportDataTable(sheet.Cells.MaxDisplayRange, true, exportOptions);
            workbook.Save("SigDigits.xlsx");               // saves to the application’s working folder
        }
    }
}
```

**Ожидаемый результат:**  
Когда вы открываете *SigDigits.xlsx* в Excel, ячейка **A1** отображает `123.5`. Исходное значение остаётся `123.456789`, но отображаемое число соблюдает правило 4‑значных значимых цифр. Если вы экспортируете лист в DataTable, значение в таблице также будет округлено до `123.5`.

---

## Применить пользовательский числовой формат к дополнительным ячейкам

Если вам нужно отформатировать диапазон, а не одну ячейку, переиспользуйте объект `Style`:

```csharp
// Apply the same custom style to B2:C5
Range range = sheet.Cells.CreateRange("B2:C5");
range.ApplyStyle(customStyle, new StyleFlag { NumberFormat = true });
```

**Pro tip:** Переиспользование объекта стиля уменьшает нагрузку на память и гарантирует единообразное форматирование по всему листу.

## Как форматировать числа в Excel с помощью C# — общие варианты

| Сценарий | Строка формата | Результат |
|----------|----------------|-----------|
| Fixed two decimal places | `"0.00"` | `123.46` |
| Currency (US) | `"$#,##0.00"` | `$123.46` |
| Percentage with one decimal | `"0.0%"` | `12,346.0%` |
| Scientific notation | `"0.00E+00"` | `1.23E+02` |

Выберите шаблон, соответствующий требованиям вашего отчёта. Все шаблоны совместимы со свойством `Style.Custom`, продемонстрированным ранее.

## Задать количество десятичных знаков в ячейке динамически на основе ввода пользователя

Иногда требуемая точность неизвестна во время компиляции. Вы можете формировать строку формата во время выполнения:

```csharp
int decimals = 3; // could come from a UI textbox
string format = "0." + new string('#', decimals);
customStyle.Custom = format;
sheet.Cells["A2"].PutValue(987.654321);
sheet.Cells["A2"].SetStyle(customStyle);
```

**Edge case:** Если `decimals` равно нулю, формат становится `"0"` (отображение целого числа). Всегда проверяйте ввод пользователя, чтобы избежать некорректных строк формата.

## Сохранить рабочую книгу как XLSX — лучшие практики

* **Use absolute paths** при записи в известный каталог (`Path.Combine(Environment.CurrentDirectory, "output.xlsx")`).  
* **Dispose** объект `Workbook`, если вы оборачиваете его в оператор `using`, чтобы быстро освободить неуправляемые ресурсы:

```csharp
using (Workbook wb = new Workbook())
{
    // ...populate workbook...
    wb.Save(Path.Combine(@"C:\Exports", "Report.xlsx"));
}
```

* **Version compatibility:** Aspose.Cells записывает файлы, совместимые с Excel 2010‑2023, поэтому конечные пользователи не столкнутся с проблемами формата.

---

## Полный рабочий пример

Ниже приведена полная программа, которую вы можете скопировать, вставить и сразу запустить. Она включает все необходимые директивы `using`, комментарии и обработку ошибок.

```csharp
using System;
using System.IO;
using Aspose.Cells;

namespace ExcelDemo
{
    class Program
    {
        static void Main()
        {
            try
            {
                // 1️⃣ Create workbook and get the first worksheet
                Workbook workbook = new Workbook();
                Worksheet sheet = workbook.Worksheets[0];

                // 2️⃣ Write a high‑precision number to A1
                sheet.Cells[0, 0].PutValue(123.456789);

                // 3️⃣ Apply a custom number format (up to 6 decimals)
                Style customStyle = workbook.CreateStyle();
                customStyle.Custom = "0.######";
                sheet.Cells[0, 0].SetStyle(customStyle);

                // 4️⃣ Configure export options for 4 significant digits
                ExportTableOptions exportOptions = new ExportTableOptions
                {
                    SignificantDigits = 4
                };

                // 5️⃣ Export data (optional) and save the workbook as XLSX
                sheet.ExportDataTable(sheet.Cells.MaxDisplayRange, true, exportOptions);
                string outputPath = Path.Combine(Environment.CurrentDirectory, "SigDigits.xlsx");
                workbook.Save(outputPath);

                Console.WriteLine($"Workbook saved successfully at: {outputPath}");
                Console.WriteLine("Cell A1 displays: " + sheet.Cells["A1"].StringValue);
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"Error creating workbook: {ex.Message}");
            }
        }
    }
}
```

**Шаги проверки**

1. Запустите программу (`dotnet run`).  
2. Откройте `SigDigits.xlsx`.  
3. Убедитесь, что **A1** содержит `123.5`.  
4. Если открыть XML‑файл книги (`.xlsx` — это zip‑архив), вы увидите пользовательский формат `"0.######"` в атрибуте `s` элемента `<c>`.

## Заключение

В этом руководстве вы узнали, как **create excel workbook c#**, **apply custom number format**, **set cell decimal places** и **save workbook as xlsx** с помощью Aspose.Cells. Решение демонстрирует как визуальное форматирование внутри Excel, так и округление при экспорте данных через `ExportTableOptions`.

Далее вы можете:

* Расширить подход на целые диапазоны или таблицы.  
* Комбинировать несколько стилей (шрифты, границы) с помощью `StyleFlag`.  
* Автоматизировать генерацию отчётов, перебирая источники данных и применяя одинаковую логику форматирования.  

Не стесняйтесь экспериментировать с различными строками формата, количеством десятичных знаков или параметрами экспорта, чтобы соответствовать вашим конкретным требованиям к отчётности. Приятного кодирования!

## Что изучать дальше?

Следующие руководства охватывают тесно связанные темы, которые развивают техники, продемонстрированные в этом руководстве. Каждый ресурс включает полные рабочие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [Create Excel Workbook C# – Применить валютный формат и импортировать DataTable](/cells/english/net/excel-data-import-export/create-excel-workbook-c-apply-currency-format-and-import-dat/)
- [Create Excel Workbook C# – Пошаговое руководство с условным форматированием](/cells/english/net/excel-conditional-formatting/create-excel-workbook-c-step-by-step-guide-with-conditional/)
- [Create Excel Workbook C# – Добавить комментарий и сохранить как XLSX](/cells/english/net/excel-comment-annotation/create-excel-workbook-c-add-comment-save-as-xlsx/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}