---
category: general
date: 2026-10-10
description: Узнайте, как сохранять Excel в виде текста на C# с помощью Aspose.Cells.
  Это руководство охватывает преобразование Excel в txt, экспорт XLSX в txt и создание
  txt из Excel с полным кодом.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save excel as text
- convert excel to txt
- export xlsx to txt
- create txt from excel
language: ru
lastmod: 2026-10-10
og_description: Сохраните Excel в виде текста с помощью Aspose.Cells для .NET. Следуйте
  этому руководству, чтобы преобразовать Excel в txt, экспортировать XLSX в txt и
  создать txt из Excel с примером кода.
og_image_alt: Screenshot of C# code that saves an Excel workbook as a plain‑text file
og_title: Сохранить Excel как текст в C# – полный учебник по Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Learn how to save Excel as text in C# using Aspose.Cells. This guide
    covers convert Excel to txt, export XLSX to txt, and create txt from Excel with
    full code.
  headline: How to save Excel as text with Aspose.Cells – step‑by‑step guide
  type: TechArticle
- description: Learn how to save Excel as text in C# using Aspose.Cells. This guide
    covers convert Excel to txt, export XLSX to txt, and create txt from Excel with
    full code.
  name: How to save Excel as text with Aspose.Cells – step‑by‑step guide
  steps:
  - name: Prerequisites
    text: '* .NET 6.0 or later (the code also works with .NET Framework 4.7.2+). *
      Basic familiarity with C# and Visual Studio (or any .NET IDE). * An active Aspose.Cells
      for .NET license or a free evaluation key. * The Excel file you want to convert
      (`input.xlsx` in the examples).'
  - name: Full runnable program
    text: 'Putting the pieces together, here is a complete, self‑contained console
      application:'
  - name: Verify programmatically
    text: 'You can read the generated file back into memory to confirm that the export
      succeeded:'
  - name: Common edge cases
    text: '| Situation | What to watch for | Recommended fix | |----------------------------------------|---------------------------------------------------|-----------------|
      | Cells contain formulas | The exported value is the **calculated result**,
      not the formula text. | Ensure the workbook is fully calcul'
  - name: What’s next?
    text: '* Try exporting to CSV (`CsvSaveOptions`) for Excel‑compatible comma‑separated
      files. * Explore the `PdfSaveOptions` class to **export Excel to PDF** in a
      single line. * Combine multiple worksheets into one text file by iterating over
      `workbook.Worksheets`.'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
- Text export
title: Как сохранить Excel в виде текста с помощью Aspose.Cells – пошаговое руководство
url: /ru/net/converting-excel-files-to-other-formats/how-to-save-excel-as-text-with-aspose-cells-step-by-step-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как сохранить Excel как текст с помощью Aspose.Cells – пошаговое руководство

Если вам нужно **быстро сохранить Excel как текст**, это руководство покажет, как сделать это в C# с помощью Aspose.Cells. Вы увидите, как **конвертировать Excel в txt**, управлять точностью чисел и обрабатывать типичные граничные случаи — все в одном исполняемом примере.

В последующих разделах вы изучите полный рабочий процесс, от установки библиотеки до проверки полученного файла. Внешняя документация не требуется; всё необходимое включено здесь.

## Что вы получите

К концу этого руководства вы сможете:

* Загружать любую книгу `.xlsx` с диска.  
* Настраивать `TxtSaveOptions` для ограничения количества значимых цифр.  
* **Экспортировать XLSX в txt** одним вызовом `Save`.  
* Понимать, как устранять проблемы форматирования при **создании txt из Excel**.

### Предварительные требования

* .NET 6.0 или новее (код также работает с .NET Framework 4.7.2+).  
* Базовые знания C# и Visual Studio (или любой другой .NET IDE).  
* Действующая лицензия Aspose.Cells for .NET или бесплатный оценочный ключ.  
* Файл Excel, который вы хотите конвертировать (`input.xlsx` в примерах).

> **Pro tip:** Если планируете запускать это на сервере, храните файл лицензии в безопасном месте и загружайте его один раз при старте приложения.

## Шаг 1: Настройка среды разработки

1. Создайте новый консольный проект:

   ```bash
   dotnet new console -n ExcelToTxtDemo
   cd ExcelToTxtDemo
   ```

2. Добавьте пакет Aspose.Cells через NuGet:

   ```bash
   dotnet add package Aspose.Cells
   ```

   Это загрузит последнюю стабильную версию (на 2026‑10‑10 это 23.9).

3. (Опционально) Если у вас есть файл лицензии, поместите `Aspose.Cells.lic` в корень проекта и добавьте следующий код в начало `Program.cs`:

   ```csharp
   // Load Aspose.Cells license (required for production use)
   var license = new Aspose.Cells.License();
   license.SetLicense("Aspose.Cells.lic");
   ```

   Загрузка лицензии удаляет водяные знаки оценки и отключает ограничения по размеру.

## Шаг 2: Загрузка книги Excel

Первая рабочая строка создаёт экземпляр `Workbook`, представляющий весь файл Excel.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 2: Load the workbook you want to convert
        var workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");
        // Continue with export logic...
    }
}
```

**Почему это важно:** `Workbook` абстрагирует листы, ячейки, формулы и форматирование. Загрузив файл один раз, вы сохраняете быструю и экономную по памяти конверсию.

## Шаг 3: Настройка TxtSaveOptions для точного контроля цифр

При **конвертации Excel в txt** числовые значения могут содержать много знаков после запятой. `TxtSaveOptions` позволяет ограничить вывод определённым количеством значимых цифр, что часто требуется для downstream‑систем, ожидающих фиксированную ширину текста.

```csharp
// Step 3: Create and configure TxtSaveOptions
var txtOptions = new TxtSaveOptions
{
    // Keep only 5 significant digits (e.g., 123.45678 → 123.46)
    SignificantDigits = 5,

    // Optional: Use tab as the delimiter for column separation
    Separator = "\t",

    // Optional: Export only the first worksheet
    ExportActiveWorksheetOnly = true
};
```

**Пояснение:**  
* `SignificantDigits` обрезает шум плавающей запятой, сохраняя достаточную точность для большинства бизнес‑расчётов.  
* `Separator` по умолчанию — пробел; установка значения `\t` (табуляция) делает полученный файл удобнее для импорта в базы данных или электронные таблицы.  
* `ExportActiveWorksheetOnly` предотвращает случайный экспорт скрытых листов, которые иначе могут раздувать текстовый файл.

## Шаг 4: Экспорт XLSX в txt с настроенными параметрами

Теперь у вас есть всё необходимое для **сохранения Excel как текст**. Метод `Save` записывает текстовое представление в указанный путь.

```csharp
// Step 4: Save the workbook as a plain‑text file
workbook.Save(@"YOUR_DIRECTORY\output.txt", txtOptions);
Console.WriteLine("Export completed: output.txt");
```

Сгенерированный `output.txt` будет содержать строки с табуляцией между значениями, каждую ячейку представив в виде простого текста согласно заданным параметрам.

### Полный исполняемый пример

Объединив все части, получаем полностью автономное консольное приложение:

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Load license if you have one (remove comments if not needed)
        // var license = new License();
        // license.SetLicense("Aspose.Cells.lic");

        // 1️⃣ Load the Excel workbook
        var workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");

        // 2️⃣ Configure TxtSaveOptions
        var txtOptions = new TxtSaveOptions
        {
            SignificantDigits = 5,
            Separator = "\t",
            ExportActiveWorksheetOnly = true
        };

        // 3️⃣ Export XLSX to TXT
        workbook.Save(@"YOUR_DIRECTORY\output.txt", txtOptions);

        Console.WriteLine("✅ Excel workbook successfully saved as text at: output.txt");
    }
}
```

**Ожидаемый вывод** (консоль):

```
✅ Excel workbook successfully saved as text at: output.txt
```

**Пример полученного `output.txt`** (первые три строки):

```
Name    Age     Salary
Alice   30      55000
Bob     27      47000
```

Числа округлены до пяти значимых цифр, столбцы разделены табуляцией.

## Шаг 5: Проверка результата и обработка граничных случаев

### Программная проверка

Можно считать сгенерированный файл обратно в память, чтобы убедиться, что экспорт прошёл успешно:

```csharp
string[] lines = File.ReadAllLines(@"YOUR_DIRECTORY\output.txt");
if (lines.Length > 0)
{
    Console.WriteLine("First line of the txt file:");
    Console.WriteLine(lines[0]);
}
```

### Типичные граничные случаи

| Ситуация                               | На что обратить внимание                                 | Рекомендуемое решение |
|----------------------------------------|----------------------------------------------------------|------------------------|
| Ячейки содержат формулы                | Экспортируется **рассчитанное значение**, а не текст формулы. | Убедитесь, что книга полностью вычислена (`workbook.CalculateFormula();`) перед сохранением. |
| Даты отображаются как серийные числа   | Excel хранит даты как числа; они могут выглядеть как `44745`. | Установите `txtOptions.ConvertDateTime = true;`, чтобы получить человекочитаемый формат даты. |
| Большие листы (>10 000 строк)          | Потребление памяти может резко возрасти.                | Используйте `txtOptions.ExportAllSheets = false;` и обрабатывайте листы по отдельности. |
| Юникод‑символы (например, эмодзи)      | По умолчанию кодировка — UTF‑8; старые системы могут ожидать ANSI. | При необходимости задайте `txtOptions.Encoding = Encoding.GetEncoding("windows-1252");`. |

Предвидя эти сценарии, вы сможете **создавать txt из Excel** надёжно для разных наборов данных.

## Заключение

Теперь вы знаете, как **сохранить Excel как текст** с помощью Aspose.Cells для .NET: от загрузки книги до настройки `TxtSaveOptions` и финального **экспорта XLSX в txt**. Пример демонстрирует полный путь кода, объясняет логику каждой настройки и охватывает типичные подводные камни при **конвертации Excel в txt**.

### Что дальше?

* Попробуйте экспорт в CSV (`CsvSaveOptions`) для файлов, совместимых с Excel, разделённых запятыми.  
* Исследуйте класс `PdfSaveOptions`, чтобы **экспортировать Excel в PDF** одной строкой кода.  
* Объедините несколько листов в один текстовый файл, перебирая `workbook.Worksheets`.  

Не бойтесь экспериментировать с параметрами — изменяйте разделитель, точность или выбор листов, чтобы подстроить процесс под ваш конкретный workflow.

Счастливого кодинга!


## Что вам стоит изучить дальше?


Следующие руководства охватывают тесно связанные темы, расширяющие техники, продемонстрированные в этом руководстве. Каждый ресурс содержит полностью рабочие примеры кода с пошаговыми объяснениями, помогающими освоить дополнительные возможности API и исследовать альтернативные подходы в ваших проектах.

- [Save Excel as Text File with Custom Separator using Aspose.Cells](/cells/english/net/workbook-operations/save-excel-text-custom-separator-aspose-cells-net/)
- [Save Excel as txt – Complete C# Guide to Export Numbers with Significant Digits](/cells/english/net/converting-excel-files-to-other-formats/save-excel-as-txt-complete-c-guide-to-export-numbers-with-si/)
- [How to Save Excel Files in Multiple Formats Using Aspose.Cells .NET (2023 Guide)](/cells/english/net/workbook-operations/aspose-cells-net-save-excel-formats/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}