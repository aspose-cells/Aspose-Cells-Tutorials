---
category: general
date: 2026-05-04
description: Как встроить шрифты при конвертации книги Excel в PDF с помощью C#. Узнайте,
  как сохранить книгу в PDF со встроенными стандартными шрифтами и избежать проблем
  с отсутствующими шрифтами.
draft: false
keywords:
- how to embed fonts
- save workbook as pdf
- convert excel to pdf
- export spreadsheet to pdf
- how to save pdf
language: ru
og_description: Как встраивать шрифты при конвертации книги Excel в PDF с помощью
  C#. Это руководство показывает полный код, объясняет, почему встраивание важно,
  и охватывает распространённые подводные камни.
og_title: Как внедрить шрифты в PDF – Сохранить рабочую книгу в PDF в C#
tags:
- C#
- Aspose.Cells
- PDF generation
title: Как встроить шрифты в PDF — Сохранить рабочую книгу в PDF на C#
url: /ru/net/conversion-to-pdf/how-to-embed-fonts-in-pdf-save-workbook-as-pdf-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как встраивать шрифты в PDF – Сохранить книгу Excel как PDF в C#

Когда‑то задавались вопросом **как встраивать шрифты**, экспортируя таблицу Excel в PDF? Вы не одиноки. Многие разработчики сталкиваются с неприятным предупреждением «отсутствует шрифт» после сохранения книги как PDF, а затем обнаруживают, что полученный файл выглядит неправильно на другом компьютере.  

Хорошая новость: исправление довольно простое с Aspose.Cells для .NET. В этом руководстве мы пройдём по точным шагам **сохранения книги как PDF** с встраиванием стандартных шрифтов, а также коснёмся **convert excel to pdf**, **export spreadsheet to pdf** и даже ответим на вопрос **how to save pdf** с правильными параметрами. К концу вы получите полностью готовый пример, который можно вставить в любой проект C#.

## Предварительные требования

Прежде чем приступить, убедитесь, что у вас есть:

* .NET 6 или новее (код также работает на .NET Framework 4.7+)  
* Действующая лицензия Aspose.Cells для .NET (бесплатная пробная версия работает, но лицензия убирает водяные знаки оценки)  
* Visual Studio 2022 или любая другая IDE по вашему выбору  
* Базовое понимание синтаксиса C# – если вы умеете писать «Hello World», то всё готово  

Если что‑то из этого вам незнакомо, сделайте паузу и подготовьте необходимые инструменты; остальная часть руководства предполагает, что всё уже готово.

## Шаг 1: Добавьте пакет Aspose.Cells через NuGet

Сначала нужна библиотека, которая действительно работает с файлами Excel. Откройте консоль NuGet вашего проекта и выполните:

```powershell
Install-Package Aspose.Cells
```

Эта единственная строка подтянет всё необходимое, включая классы `Workbook` и `PdfSaveOptions`, которые мы будем использовать позже.  

*Совет:* Если вы используете CI/CD конвейер, зафиксируйте версию пакета (например, `Aspose.Cells -Version 24.9`), чтобы избежать неожиданного ломания из‑за обновлений.

## Шаг 2: Создайте или загрузите книгу

Теперь мы либо создаём совершенно новую книгу, либо загружаем существующий `.xlsx`. Для демонстрации создадим простой лист с несколькими строками данных.

```csharp
using Aspose.Cells;

namespace PdfExportDemo
{
    class Program
    {
        static void Main()
        {
            // Step 2: Create a fresh workbook (or replace with Workbook("input.xlsx"))
            Workbook workbook = new Workbook();

            // Populate the first worksheet with sample data
            Worksheet sheet = workbook.Worksheets[0];
            sheet.Cells["A1"].PutValue("Product");
            sheet.Cells["B1"].PutValue("Quantity");
            sheet.Cells["A2"].PutValue("Apples");
            sheet.Cells["B2"].PutValue(120);
            sheet.Cells["A3"].PutValue("Oranges");
            sheet.Cells["B3"].PutValue(85);
```

Мы только что создали небольшой список инвентаря. Если у вас уже есть файл Excel, замените вызов `new Workbook()` на `new Workbook("path/to/file.xlsx")` и пропустите блок вставки данных.

## Шаг 3: Настройте параметры сохранения PDF для встраивания стандартных шрифтов

Здесь происходит магия. По умолчанию Aspose.Cells может ссылаться на системные шрифты вместо их встраивания, что приводит к проблеме «шрифт не найден» на других компьютерах. Установка `EmbedStandardFonts` в `true` заставляет PDF‑писатель встраивать самые распространённые шрифты (Arial, Times New Roman и т.д.).

```csharp
            // Step 3: Set PDF options – embed standard fonts for portability
            PdfSaveOptions pdfOptions = new PdfSaveOptions
            {
                // Ensures that fonts like Arial, Times New Roman are embedded
                EmbedStandardFonts = true,

                // Optional: keep the original layout (no scaling)
                OnePagePerSheet = false
            };
```

**Зачем встраивать шрифты?** Представьте, что вы отправляете PDF коллеге, у которого на машине только Helvetica. Без встраивания его просмотрщик заменит шрифт на другой, изменив таблицы и нарушив дизайн. Встраивание гарантирует, что PDF будет выглядеть одинаково везде.

## Шаг 4: Сохраните книгу как PDF‑файл

Наконец, вызываем `Save` и указываем папку назначения. Метод принимает путь к файлу и параметры, которые мы только что настроили.

```csharp
            // Step 4: Save the workbook as a PDF with embedded fonts
            string outputPath = @"C:\Temp\InventoryReport.pdf";
            workbook.Save(outputPath, pdfOptions);

            // Let the user know we’re done
            Console.WriteLine($"PDF saved successfully to {outputPath}");
        }
    }
}
```

Запустите программу, и вы найдёте `InventoryReport.pdf` в `C:\Temp`. Откройте его на любом компьютере — шрифты останутся на месте, таблицы будут выровнены, а макет будет соответствовать оригинальному листу Excel.

> **Ожидаемый результат:** PDF содержит двухколоночную таблицу точно так же, как в Excel, с встраиванием Arial (или шрифта системы по умолчанию). Предупреждения о недостающих шрифтах в Adobe Reader или любом другом просмотрщике не появляются.

## Шаг 5: Проверьте встраивание шрифтов (необязательно, но полезно)

Если хотите убедиться, что шрифты действительно встроены, откройте PDF в Adobe Acrobat и перейдите в **File → Properties → Fonts**. Вы должны увидеть записи вроде “ArialMT (Embedded Subset)”.

Либо можно воспользоваться бесплатным инструментом **PDF‑Info** (`pdfinfo` в Linux), который выводит встроенные шрифты из командной строки:

```bash
pdfinfo -meta InventoryReport.pdf | grep Font
```

Если рядом с каждым шрифтом стоит “Embedded”, значит всё сделано правильно.

## Распространённые граничные случаи и как их решать

| Ситуация | Что делать |
|-----------|------------|
| **Собственный корпоративный шрифт** (например, `MyCompanySans`) | Установите `PdfSaveOptions.CustomFonts = new string[] { @"C:\Fonts\MyCompanySans.ttf" };` и оставьте `EmbedStandardFonts = true`. |
| **Большая книга (много листов)** | Включите `PdfSaveOptions.OnePagePerSheet = true`, чтобы избежать огромных страниц, трудных для чтения. |
| **Лицензия не применена** | Пробная версия добавляет водяной знак. Зарегистрируйте лицензию с помощью `License license = new License(); license.SetLicense("Aspose.Cells.lic");` перед созданием книги. |
| **Проблемы с производительностью** | Переиспользуйте один экземпляр `PdfSaveOptions` для нескольких сохранений и рассмотрите `PdfSaveOptions.Compression = PdfCompressionLevel.Maximum;` для уменьшения размера файла. |

Эти настройки делают ваш конвейер **convert excel to pdf** надёжным, независимо от исходных данных.

## Часто задаваемые вопросы

**В: Встраивает ли `EmbedStandardFonts` также нестандартные шрифты?**  
О: Нет. Он встраивает только базовые 14 шрифтов PDF. Для пользовательских шрифтов их необходимо добавить через коллекцию `CustomFonts`, как показано выше.

**В: Значительно ли увеличится размер PDF?**  
О: Встраивание нескольких стандартных шрифтов добавляет лишь несколько килобайт. Если встраивать много больших пользовательских шрифтов, ожидайте умеренного роста — всё равно гораздо меньше, чем при встраивании полноразмерных изображений.

**В: Можно ли встраивать шрифты, используя другие библиотеки (например, iTextSharp)?**  
О: Конечно, но API отличается. Это руководство сосредоточено на Aspose.Cells, потому что он обрабатывает конвертацию Excel‑в‑PDF в один шаг, упрощая рабочий процесс **export spreadsheet to pdf**.

## Полный рабочий пример (готовый к копированию)

Ниже полностью готовая программа, которую можно сразу компилировать. В ней присутствуют все необходимые `using`‑директивы, заглушка лицензии (закомментирована) и подробные комментарии.

```csharp
using System;
using Aspose.Cells;

namespace PdfExportDemo
{
    class Program
    {
        static void Main()
        {
            // Uncomment and set the path if you have a license file
            // License lic = new License();
            // lic.SetLicense(@"C:\Path\To\Aspose.Cells.lic");

            // -------------------------------------------------
            // Step 1: Create or load a workbook
            // -------------------------------------------------
            Workbook workbook = new Workbook(); // Replace with new Workbook("input.xlsx") to load an existing file

            // -------------------------------------------------
            // Step 2: Populate sample data (optional)
            // -------------------------------------------------
            Worksheet sheet = workbook.Worksheets[0];
            sheet.Cells["A1"].PutValue("Product");
            sheet.Cells["B1"].PutValue("Quantity");
            sheet.Cells["A2"].PutValue("Apples");
            sheet.Cells["B2"].PutValue(120);
            sheet.Cells["A3"].PutValue("Oranges");
            sheet.Cells["B3"].PutValue(85);

            // -------------------------------------------------
            // Step 3: Configure PDF save options – embed fonts
            // -------------------------------------------------
            PdfSaveOptions pdfOptions = new PdfSaveOptions
            {
                EmbedStandardFonts = true, // <-- This is the key to how to embed fonts
                OnePagePerSheet = false,
                // Uncomment and set custom fonts if needed
                // CustomFonts = new string[] { @"C:\Fonts\MyCompanySans.ttf" }
            };

            // -------------------------------------------------
            // Step 4: Save the workbook as a PDF file
            // -------------------------------------------------
            string outputPath = @"C:\Temp\InventoryReport.pdf";
            workbook.Save(outputPath, pdfOptions);

            Console.WriteLine($"PDF saved successfully to {outputPath}");
        }
    }
}
```

Сохраните файл как `Program.cs`, соберите проект и запустите. PDF появится точно там, куда вы указали `outputPath`, а шрифты будут надёжно встроены.

## Заключение

Мы рассмотрели **как встраивать шрифты** при **сохранении книги как pdf** с помощью Aspose.Cells, прошли каждую строку кода и объяснили, почему встраивание важно для надёжного **convert excel to pdf** процесса. Теперь вы знаете, как **export spreadsheet to pdf**, проверять встраивание и справляться с типичными граничными случаями, такими как пользовательские шрифты или большие книги.  

Далее вы можете исследовать добавление заголовков/нижних колонтитулов, защиту PDF паролем или пакетную обработку нескольких книг за один запуск. Каждый

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}