---
category: general
date: 2026-10-13
description: Узнайте, как сохранять Excel в формате TXT с помощью Aspose.Cells. Это
  руководство охватывает экспорт Excel в TXT, запись значения в ячейку и установку
  значимых цифр всего за несколько шагов.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save excel as txt
- export excel to txt
- write value to cell
- set significant digits
- export spreadsheet as txt
language: ru
lastmod: 2026-10-13
og_description: Сохраните Excel в TXT с помощью Aspose.Cells. Узнайте, как экспортировать
  Excel в TXT, записать значение в ячейку и установить значимые цифры всего за несколько
  строк кода C#.
og_image_alt: Screenshot showing a workbook saved as a TXT file using save excel as
  txt
og_title: Сохранение Excel в TXT – пошаговое руководство для разработчиков .NET
schemas:
- author: Aspose
  dateModified: '2026-10-13'
  description: Learn how to save Excel as TXT with Aspose.Cells. This guide covers
    export Excel to TXT, write value to cell, and set significant digits in just a
    few steps.
  headline: How to save Excel as TXT using Aspose.Cells in C#
  type: TechArticle
- questions:
  - answer: It rounds to the nearest value based on the specified number of significant
      digits, ensuring the output is mathematically accurate to that precision.
    question: Does `SignificantDigits` round or truncate?
  - answer: 'Yes. Replace the file path with a `MemoryStream` instance: `workbook.Save(stream,
      txtOptions);`. This is handy for web APIs that need to return the TXT content
      without touching the file system.'
    question: Can I export directly to a memory stream?
  - answer: 'Use `txtOptions.ExportFormattedValues = true`. This forces Aspose.Cells
      to write the cell’s displayed text rather than the raw value. ## Conclusion
      You now know how to **save Excel as TXT** with full control over precision,
      formatting, and output location. By following the four steps—create a workbo'
    question: What if I need to keep the original formatting (e.g., dates)?
  type: FAQPage
tags:
- Excel
- TXT
- Aspose.Cells
- .NET
title: Как сохранить Excel в TXT с использованием Aspose.Cells в C#
url: /ru/net/converting-excel-files-to-other-formats/how-to-save-excel-as-txt-using-aspose-cells-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как сохранить Excel в TXT с помощью Aspose.Cells на C#

Если вам нужно **сохранить Excel в TXT** быстро, этот учебник покажет полный процесс за менее чем пять минут. Вы увидите, как экспортировать Excel в TXT, записать значение в ячейку и задать значимые цифры, чтобы текстовый файл содержал именно те данные, которые вы ожидаете.

Экспорт таблицы в формате TXT полезен, когда downstream‑системы принимают только plain‑text ввод, когда необходимо генерировать логи или когда нужен человекочитаемый дамп вычислений. Пример ниже работает с Aspose.Cells v25.10 или новее и запускается на любой среде выполнения .NET 6+.

## Предварительные требования

Перед началом убедитесь, что у вас есть:

* Лицензированная копия **Aspose.Cells for .NET** (бесплатная trial‑версия подходит для тестирования).
* Установленный .NET 6 SDK или более новая версия.
* IDE, например Visual Studio 2022, VS Code или Rider.
* Базовые знания C# — продвинутый опыт автоматизации Excel не требуется.

Вы можете установить пакет Aspose.Cells через NuGet с помощью:

```bash
dotnet add package Aspose.Cells
```

## Шаг 1: Создать рабочую книгу и получить доступ к первому листу (save excel as txt)

Первое, что нужно сделать, когда вы хотите **save Excel as TXT**, — создать объект `Workbook`. Этот объект представляет весь файл Excel в памяти.

```csharp
using Aspose.Cells;

// Create a new workbook (an empty Excel file)
Workbook workbook = new Workbook();

// Access the first worksheet (index 0)
Worksheet worksheet = workbook.Worksheets[0];
```

> **Why this matters:** Класс `Workbook` является точкой входа для всех операций с таблицами. Начав с новой рабочей книги, вы избегаете скрытого форматирования, которое могло бы повлиять на вывод в plain‑text.

## Шаг 2: Записать число высокой точности в ячейку (write value to cell)

Теперь необходимо **write value to cell** A1. Метод `PutValue` автоматически определяет тип данных и сохраняет его как числовое значение.

```csharp
// Write a high‑precision number into cell A1
worksheet.Cells["A1"].PutValue(12345.6789012345);
```

> **Tip:** Если позже понадобится записать строки, даты или формулы, тот же метод `PutValue` работает — просто передайте соответствующий тип .NET.

## Шаг 3: Настроить параметры экспорта, чтобы оставить только необходимую точность (set significant digits)

При экспорте в файл TXT часто требуется ограничить количество цифр, чтобы уменьшить размер файла или соответствовать спецификации downstream‑системы. Класс `TxtSaveOptions` предоставляет свойство `SignificantDigits` для этой цели.

```csharp
// Configure TXT save options to retain only 6 significant digits
TxtSaveOptions txtSaveOptions = new TxtSaveOptions(SaveFormat.Txt)
{
    SignificantDigits = 6   // New option in v25.10
};
```

> **Why you should set significant digits:** Без этой настройки Aspose.Cells записывает полное значение двойной точности, что может привести к длинным строкам вроде `12345.6789012345`. Установка `SignificantDigits = 6` обрезает вывод до `12345.7`, что соответствует большинству требований к отчетности.

## Шаг 4: Экспортировать рабочую книгу в файл TXT (export excel to txt)

Наконец, вы **export Excel to TXT**, вызывая `Workbook.Save` с ранее настроенными параметрами.

```csharp
// Save the workbook as a TXT file using the configured options
string outputPath = @"C:\Temp\LimitedDigits.txt";
workbook.Save(outputPath, txtSaveOptions);
```

Когда код завершится, файл `LimitedDigits.txt` будет содержать:

```
12345.7
```

> **Result verification:** Откройте файл в любом текстовом редакторе (Notepad, VS Code), чтобы убедиться, что присутствуют только шесть значимых цифр и что нет лишних запятых или табуляций.

## Полный, готовый к запуску пример

Ниже представлено автономное консольное приложение, которое можно скопировать, вставить и сразу запустить.

```csharp
using System;
using Aspose.Cells;

namespace ExcelToTxtDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create workbook and get the first worksheet
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.Worksheets[0];

            // 2️⃣ Write a high‑precision number to cell A1
            worksheet.Cells["A1"].PutValue(12345.6789012345);

            // 3️⃣ Set up TXT save options with 6 significant digits
            TxtSaveOptions txtOptions = new TxtSaveOptions(SaveFormat.Txt)
            {
                SignificantDigits = 6
            };

            // 4️⃣ Save as TXT
            string path = @"C:\Temp\LimitedDigits.txt";
            workbook.Save(path, txtOptions);

            Console.WriteLine($"Workbook exported to TXT at: {path}");
        }
    }
}
```

**Explanation of each block**

| Block | Purpose |
|-------|---------|
| `using Aspose.Cells;` | Импортирует пространство имен Aspose.Cells, необходимое для `Workbook`, `Worksheet` и `TxtSaveOptions`. |
| `Workbook workbook = new Workbook();` | Создаёт пустую рабочую книгу Excel в памяти. |
| `worksheet.Cells["A1"].PutValue(...);` | **write value to cell** A1 с числом двойной точности. |
| `TxtSaveOptions` | Конфигурирует поведение **set significant digits** для экспорта в TXT. |
| `workbook.Save(..., txtOptions);` | Выполняет операцию **export excel to txt**, создавая файл plain‑text. |

## Особые случаи и дополнительные советы

| Scenario | How to handle |
|----------|---------------|
| **Large worksheets** (many rows/columns) | Используйте `txtOptions.Encoding = Encoding.UTF8`, если нужна поддержка Unicode, и рассмотрите возможность потоковой записи с `Workbook.Save(Stream, txtOptions)`, чтобы избежать высокого потребления памяти. |
| **Custom delimiters** (comma‑separated values) | `TxtSaveOptions` также предоставляет свойство `Separator` — установите его в `','`, чтобы получить CSV‑подобный вывод, оставаясь в формате TXT. |
| **Preserving formulas** | Установите `txtOptions.ExportFormulas = true`, чтобы записать текст формулы вместо вычисленного значения. |
| **Locale‑specific decimal separators** | Настройте `txtOptions.DecimalSeparator` в `','` для европейских локалей. |
| **Multiple worksheets** | Пройдитесь по `workbook.Worksheets` в цикле и вызывайте `Save` для каждой, добавляя имя листа к имени файла. |

## Часто задаваемые вопросы

**Q: Округляет ли `SignificantDigits` или просто отбрасывает лишнее?**  
A: Он округляет до ближайшего значения на основе указанного количества значимых цифр, обеспечивая математическую точность до этой точности.

**Q: Можно ли экспортировать напрямую в поток памяти?**  
A: Да. Замените путь к файлу экземпляром `MemoryStream`: `workbook.Save(stream, txtOptions);`. Это удобно для веб‑API, которым нужно вернуть содержимое TXT без обращения к файловой системе.

**Q: Что делать, если нужно сохранить оригинальное форматирование (например, даты)?**  
A: Используйте `txtOptions.ExportFormattedValues = true`. Это заставит Aspose.Cells записать отображаемый текст ячейки вместо её сырого значения.

## Заключение

Теперь вы знаете, как **save Excel as TXT** с полным контролем над точностью, форматированием и местом сохранения. Следуя четырём шагам — создать рабочую книгу, **write value to cell**, **set significant digits** и **export Excel to TXT** — вы сможете интегрировать экспорт в plain‑text в любое .NET‑приложение.

Далее изучайте связанные темы, такие как **export spreadsheet as TXT with custom delimiters**, **convert Excel to CSV** или **use Aspose.Cells to generate JSON reports**. Все они опираются на те же базовые концепции, продемонстрированные здесь, предоставляя универсальный набор инструментов для обмена данными между платформами.

Удачной разработки!

## Что вам стоит изучить дальше?

Следующие учебники охватывают тесно связанные темы, построенные на техниках, продемонстрированных в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы в собственных проектах.

- [Сохранить Excel как текст — Полное руководство C# по экспорту Excel в TXT](/cells/english/net/converting-excel-files-to-other-formats/save-excel-as-text-complete-c-guide-to-export-excel-to-txt/)
- [Создать новую рабочую книгу и экспортировать Excel в TXT с точностью](/cells/english/net/excel-data-export-retrieval/create-new-workbook-and-export-excel-to-txt-with-precision/)
- [Создать новую рабочую книгу — Экспортировать Excel в TXT с полной точностью](/cells/english/net/converting-excel-files-to-other-formats/create-new-workbook-export-excel-to-txt-with-full-precision/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}