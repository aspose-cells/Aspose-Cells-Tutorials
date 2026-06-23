---
category: general
date: 2026-06-05
description: Как округлять числа при конвертации Excel в PDF с помощью C#. Узнайте,
  как экспортировать книгу в PDF, сохранять Excel в PDF и сохранять числовую точность.
draft: false
keywords:
- how to round numbers
- convert excel to pdf
- export workbook as pdf
- save excel as pdf
- convert xlsx to pdf
language: ru
og_description: Как округлять числа при конвертации Excel в PDF с помощью C#. Следуйте
  этому руководству, чтобы экспортировать рабочую книгу в PDF, сохранить Excel в PDF
  и управлять числовым форматированием.
og_title: Как округлять числа при конвертации Excel в PDF – пошагово
schemas:
- author: Aspose
  dateModified: '2026-06-05'
  description: How to round numbers while you convert Excel to PDF using C#. Learn
    to export workbook as PDF, save Excel as PDF, and preserve numeric precision.
  headline: How to Round Numbers When Converting Excel to PDF – Complete C# Guide
  type: TechArticle
- description: How to round numbers while you convert Excel to PDF using C#. Learn
    to export workbook as PDF, save Excel as PDF, and preserve numeric precision.
  name: How to Round Numbers When Converting Excel to PDF – Complete C# Guide
  steps:
  - name: '**Load the Excel workbook** – `Workbook` reads the `.xlsx` file into memory.
      No Excel installation required, which makes this ideal for server‑side automation.'
    text: '**Load the Excel workbook** – `Workbook` reads the `.xlsx` file into memory.
      No Excel installation required, which makes this ideal for server‑side automation.'
  - name: '**Configure `PdfSaveOptions`** – The `SignificantDigits` enum controls
      numeric handling:'
    text: '**Configure `PdfSaveOptions`** – The `SignificantDigits` enum controls
      numeric handling:'
  - name: '**Export workbook as PDF** – `workbook.Save` writes the PDF to disk, applying
      the rounding rules we set.'
    text: '**Export workbook as PDF** – `workbook.Save` writes the PDF to disk, applying
      the rounding rules we set.'
  - name: '**Run the program** – Verify the console prints “PDF generated successfully…”.'
    text: '**Run the program** – Verify the console prints “PDF generated successfully…”.'
  - name: '**Open `output.pdf`** – Look at numeric columns; they should respect the
      rounding you configured.'
    text: '**Open `output.pdf`** – Look at numeric columns; they should respect the
      rounding you configured.'
  - name: '**Compare with Excel** – If numbers differ, double‑check the `SignificantDigits`
      and `Precision` settings.'
    text: '**Compare with Excel** – If numbers differ, double‑check the `SignificantDigits`
      and `Precision` settings.'
  - name: '**Automated test** – For CI pipelines, you can render the PDF to an image
      (`PdfRenderer`) and run pixel‑wise comparisons, ensuring the rounding appears
      as expected.'
    text: '**Automated test** – For CI pipelines, you can render the PDF to an image
      (`PdfRenderer`) and run pixel‑wise comparisons, ensuring the rounding appears
      as expected.'
  type: HowTo
tags:
- excel
- pdf
- csharp
- aspose.cells
title: Как округлять числа при конвертации Excel в PDF – Полное руководство по C#
url: /ru/net/conversion-to-pdf/how-to-round-numbers-when-converting-excel-to-pdf-complete-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как округлять числа при конвертации Excel в PDF – Полное руководство на C#  

Когда‑то задавались вопросом **как округлять числа** при конвертации рабочей книги Excel в PDF? Вы не одиноки — разработчикам часто нужно поддерживать финансовые показатели в порядке или делать научные данные читаемыми, а стандартная конвертация может оставить вас с огромным набором неудобных десятичных знаков.  

В этом руководстве мы пройдём практическое решение от начала до конца, которое позволяет **конвертировать Excel в PDF**, контролируя числовую точность, используя Aspose.Cells for .NET. К концу вы узнаете, как **экспортировать рабочую книгу как PDF**, **сохранить Excel как PDF**, и, что самое важное, решить, оставлять ли числа как есть, округлять их или переключать в научную нотацию.  

> **Совет:** Тот же подход работает для сценариев **convert xlsx to pdf** на любой платформе .NET — просто добавьте пакет NuGet, и всё готово.

## Требования

Прежде чем мы начнём, убедитесь, что у вас есть:

| Требование | Почему это важно |
|------------|-------------------|
| .NET 6.0 или новее (или .NET Framework 4.7+) | Aspose.Cells поддерживает оба; более новые среды выполнения дают лучшую производительность. |
| Visual Studio 2022 (или любая IDE по вашему выбору) | Удобно для отладки и просмотра сгенерированного PDF. |
| NuGet‑пакет Aspose.Cells for .NET (`Install-Package Aspose.Cells`) | Предоставляет `Workbook`, `PdfSaveOptions` и перечисления округления, которые мы будем использовать. |
| Пример файла `input.xlsx` с числовыми данными | Чтобы увидеть эффект округления в действии. |

Дополнительный COM‑interop или установка Office не требуются — Aspose.Cells полностью управляемый.

---

## Как округлять числа при конвертации Excel в PDF

Ниже представлена основная часть решения. Мы загружаем рабочую книгу, настраиваем параметры сохранения PDF, чтобы указать, как следует обрабатывать числа, и в конце записываем PDF. Ключевая строка — свойство `SignificantDigits`, которое управляет поведением округления.

```csharp
using Aspose.Cells;
using System;

class ExcelToPdfRounded
{
    static void Main()
    {
        // Step 1: Load the Excel workbook
        // Replace YOUR_DIRECTORY with the folder that holds your file.
        Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");

        // Step 2: Create PDF save options and set how numeric values are handled
        PdfSaveOptions pdfOptions = new PdfSaveOptions();

        // Choose your rounding strategy:
        // - Preserve : keep original values (default)
        // - Round    : round to the number of significant digits
        // - Scientific : force scientific notation
        pdfOptions.SignificantDigits = SignificantDigits.Round; // <-- change as needed

        // Optional: define how many digits you consider significant
        pdfOptions.Precision = 4; // rounds to 4 significant digits

        // Step 3: Save the workbook as a PDF using the configured options
        workbook.Save(@"YOUR_DIRECTORY\output.pdf", pdfOptions);

        Console.WriteLine("PDF generated successfully with rounding applied.");
    }
}
```

### Что делает код, шаг за шагом

1. **Загрузить рабочую книгу Excel** — `Workbook` читает файл `.xlsx` в память. Установка Excel не требуется, что делает это идеальным для серверной автоматизации.  
2. **Настроить `PdfSaveOptions`** — перечисление `SignificantDigits` управляет обработкой чисел:  
   * `Preserve` сохраняет каждую десятичную часть точно так, как хранит её Excel.  
   * `Round` обрезает числа до пользовательской точности (`Precision` property). Это часть *как округлять числа*, которую вы запросили.  
   * `Scientific` принудительно отображает в научном стиле, полезно для очень больших или очень маленьких значений.  
3. **Экспортировать рабочую книгу как PDF** — `workbook.Save` записывает PDF на диск, применяя заданные нами правила округления.  

Полученный `output.pdf` покажет числа, округлённые до указанной вами точности, при этом всё остальное форматирование ячеек (шрифты, цвета, границы) останется неизменным.

---

## Шаг 1: Загрузить рабочую книгу Excel (convert xlsx to pdf)

Загрузка рабочей книги проста, но есть несколько нюансов, которые стоит упомянуть:

* **Абсолютные vs. относительные пути** — использование `@"C:\\Path\\To\\File.xlsx"` избавляет от проблем с экранированием. Если вы предпочитаете относительный путь, убедитесь, что рабочий каталог установлен правильно (`Directory.SetCurrentDirectory` может помочь).  
* **Большие файлы** — для рабочих книг размером более 200 МБ рассмотрите использование `LoadOptions` с `MemorySetting` для снижения нагрузки на память.  

```csharp
Workbook workbook = new Workbook(@"C:\Data\financial_report.xlsx");
```

## Шаг 2: Настроить параметры сохранения PDF для округления (how to round numbers)

Класс `PdfSaveOptions` — это место, где происходит магия. Давайте разберём два самых полезных свойства для округления:

| Свойство | Описание | Типичные значения |
|----------|----------|-------------------|
| `SignificantDigits` | Определяет режим округления. | `Preserve`, `Round`, `Scientific` |
| `Precision` | Количество значимых цифр, когда выбран `Round`. | 2‑6 обычно используется в финансовых отчётах. |

Если требуется разное округление для разных листов, вы можете перебрать листы и применить `PdfSaveOptions` к каждому листу с помощью `PdfSaveOptions.SetWorksheetOptions`. Это удобный крайний случай, когда один лист нуждается в точных бухгалтерских числах, а другой — в научных данных.

```csharp
PdfSaveOptions options = new PdfSaveOptions
{
    SignificantDigits = SignificantDigits.Round,
    Precision = 3 // three significant digits
};
```

**Почему это важно:** Округление на этапе генерации PDF избавляет от отдельного шага очистки данных, экономя время и снижая риск несоответствия значений между Excel и конечным документом.

## Шаг 3: Экспортировать рабочую книгу как PDF (save excel as pdf)

Последний вызов `Save` учитывает все ранее установленные параметры. Если нужно создать несколько PDF из одной рабочей книги с разными правилами округления, просто клонируйте объект `PdfSaveOptions`, измените свойства и снова вызовите `Save`.

```csharp
// First PDF – rounded to 3 digits
workbook.Save(@"C:\Exports\rounded.pdf", options);

// Second PDF – preserve original values
options.SignificantDigits = SignificantDigits.Preserve;
workbook.Save(@"C:\Exports\preserved.pdf", options);
```

**Ожидаемый результат:** Откройте сгенерированный PDF в любом просмотрщике; числовые ячейки отобразятся с округлёнными значениями (например, `1234.5678` станет `1235`, если `Precision = 4` и режим округления `Round`). Всё остальное форматирование — цвета ячеек, объединённые ячейки, диаграммы — остаётся точно таким же, как в оригинальном файле Excel.

## Необязательно: Тонкая настройка округления для конкретных ячеек

Иногда нужно округлять только определённые столбцы (например, столбец “Price”), оставляя остальные без изменений. Aspose.Cells позволяет применить **пользовательский числовой формат** перед сохранением:

```csharp
Worksheet sheet = workbook.Worksheets[0];
CellRange priceRange = sheet.Cells.CreateRange("B2:B100");

// Apply a numeric format that rounds to two decimal places
priceRange.Style.Custom = "#,##0.00";
priceRange.ApplyStyle(priceRange.Style, new StyleFlag { NumberFormat = true });
```

Когда позже вызываете `workbook.Save` с `SignificantDigits.Preserve`, пользовательский формат гарантирует, что PDF покажет округлённые числа, хотя исходное значение останется точным. Эта техника отвечает на вопрос «что если мне нужно округление по столбцам?» без дополнительных веток кода.

## Тестирование вывода (convert excel to pdf)

Быстрая проверка целостности экономит часы отладки:

1. **Запустить программу** — убедитесь, что консоль выводит “PDF generated successfully…”.  
2. **Открыть `output.pdf`** — посмотрите на числовые столбцы; они должны соответствовать настроенному округлению.  
3. **Сравнить с Excel** — если числа отличаются, перепроверьте настройки `SignificantDigits` и `Precision`.  
4. **Автоматический тест** — для CI‑конвейеров вы можете отрендерить PDF в изображение (`PdfRenderer`) и выполнить побитовые сравнения, гарантируя, что округление выглядит как ожидается.

## Распространённые проблемы и как их избежать

| Симптом | Возможная причина | Решение |
|---------|-------------------|---------|
| Числа всё ещё показывают много знаков после запятой | `SignificantDigits` оставлен по умолчанию `Preserve` | Установите `pdfOptions.SignificantDigits = SignificantDigits.Round`. |
| PDF огромный (сотни МБ) | Изображения не сжаты | Используйте `pdfOptions.ImageCompression = ImageCompression.Jpeg; pdfOptions.JpegQuality = 80;`. |
| Округление не применилось к конкретному листу | Параметры применены глобально, затем лист переопределён позже | Вызовите `worksheet.PageSetup.PrintOptions.PreserveFormatting = true;` перед сохранением или используйте параметры per‑sheet. |
| Исключение: `File not found` | Неправильный разделитель пути или файл отсутствует | Используйте буквальные строковые литералы (`@"C:\\Path\\file.xlsx"`) и проверьте, что файл существует. |

## Итоги: Чему вы научились

Мы рассмотрели **как округлять числа** при **конвертации Excel в PDF**, продемонстрировали полный процесс **экспорта рабочей книги как PDF**, и показали, как **сохранить Excel как PDF** с пользовательской точностью. Теперь у вас есть переиспользуемый шаблон, который работает для задач **convert xlsx to pdf** на настольных, веб‑ и облачных сервисах.

### Следующие шаги

* Исследовать соответствие **PDF/A** (`PdfSaveOptions.Compliance = PdfCompliance.PdfA1b`) для архивных документов.  
* Скомбинировать это с **Aspose.Slides**, чтобы внедрять диаграммы как изображения перед конвертацией.  
* Автоматизировать пакетную обработку — проходить по папке с файлами `.xlsx`, применять разные правила округления к каждому файлу и сохранять PDF в хранилище отчётов.  

Не стесняйтесь экспериментировать с перечислением `SignificantDigits`, играть с `Precision` и адаптировать код под свои бизнес‑правила. Если возникнут проблемы, документация Aspose.Cells — надёжный справочник, но описанный выше шаблон покрывает 90 % реальных сценариев.

Счастливого кодинга, и пусть ваши PDF всегда отображают числа именно так, как вам нужно!

## Что вам стоит изучить дальше?

Следующие руководства охватывают тесно связанные темы, построенные на техниках, продемонстрированных в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в своих проектах.

- [Как конвертировать Excel в PDF/A с помощью Aspose.Cells for .NET (Полное руководство)](/cells/english/net/workbook-operations/convert-excel-to-pdf-a-aspose-cells-dotnet/)
- [Как экспортировать диаграммы Excel в PDF с помощью Aspose.Cells for .NET: пошаговое руководство](/cells/english/net/workbook-operations/export-excel-charts-pdf-aspose-cells-net/)
- [Как сохранить отдельные страницы файла Excel в PDF с помощью Aspose.Cells for .NET](/cells/english/net/workbook-operations/save-specific-excel-pages-pdf-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}