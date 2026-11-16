---
category: general
date: 2026-11-16
description: Узнайте, как сохранять Excel в PowerPoint и программно конвертировать
  Excel в PowerPoint. Это пошаговое руководство также охватывает экспорт Excel в PPTX
  и сохранение рабочей книги в формате PPTX.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save excel as powerpoint
- convert excel to powerpoint
- export excel to pptx
- how to convert excel slide
- save workbook as pptx
language: ru
lastmod: 2026-11-16
og_description: Сохраните Excel как PowerPoint с помощью Aspose.Cells. Следуйте этому
  руководству, чтобы преобразовать Excel в PowerPoint, экспортировать Excel в PPTX
  и сохранить книгу в формате PPTX за несколько минут.
og_image_alt: Screenshot showing the result of saving Excel as PowerPoint with editable
  shapes
og_title: Сохранить Excel в PowerPoint – Полное руководство по C#
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Learn how to save Excel as PowerPoint and convert Excel to PowerPoint
    programmatically. This step‑by‑step guide also covers export Excel to PPTX and
    saving a workbook as PPTX.
  headline: How to save Excel as PowerPoint with Aspose.Cells in C#
  type: TechArticle
tags:
- Excel
- PowerPoint
- Aspose.Cells
- C#
- Export
title: Как сохранить Excel как PowerPoint с помощью Aspose.Cells в C#
url: /ru/net/converting-excel-files-to-other-formats/how-to-save-excel-as-powerpoint-with-aspose-cells-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как сохранить Excel в PowerPoint с помощью Aspose.Cells на C#

Если вам нужно **программно сохранить Excel в PowerPoint**, этот учебник предоставляет готовое решение, которое можно сразу запустить. Независимо от того, создаёте ли вы движок отчётности или автоматический генератор слайдов, нижеописанные шаги позволяют преобразовать лист Excel в редактируемый слайд PPTX всего в несколько строк кода.

Вы узнаете, как **конвертировать Excel в PowerPoint**, экспортировать лист в файл PPTX и сохранить текстовые поля и фигуры редактируемыми — без выхода из среды .NET.

## Prerequisites

Перед началом убедитесь, что у вас есть:

* .NET 6.0 или новее (код также работает с .NET Framework 4.7.2+)
* Действующая лицензия Aspose.Cells (бесплатная пробная версия подходит для оценки)
* Visual Studio 2022 (или любой другой IDE для C#)
* Рабочая книга Excel, содержащая данные и фигуры, которые вы хотите экспортировать

## Step 1: Install Aspose.Cells

Добавьте пакет Aspose.Cells NuGet в ваш проект:

```bash
dotnet add package Aspose.Cells
```

> **Pro tip:** Используйте флаг `-v`, чтобы указать конкретную версию, например, `Aspose.Cells.24.5`.

## Step 2: Load the workbook you want to export

Первая операция в процессе **save Excel as PowerPoint** — загрузка исходной рабочей книги.

```csharp
using Aspose.Cells;
using System;

// Load the workbook that contains the shapes
Workbook workbook = new Workbook(@"C:\Data\WithShapes.xlsx");
```

*Почему это важно:* Загрузка книги даёт доступ к её листам, настройкам страницы и объектам рисования, которые станут редактируемыми фигурами PowerPoint.

## Step 3: Configure export options for an editable PPTX slide

Чтобы **convert Excel to PowerPoint** с сохранением возможности редактирования, необходимо задать несколько свойств у `ImageOrPrintOptions`.

```csharp
// Prepare export options to generate an editable PPTX slide
ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
{
    SaveFormat = SaveFormat.Pptx,      // Export format
    ExportEditableText = true,        // Keep text boxes editable
    ExportEditableShapes = true       // Keep shapes editable
};
```

*Explanation:*  
* `SaveFormat = SaveFormat.Pptx` указывает Aspose.Cells генерировать файл PowerPoint.  
* `ExportEditableText` и `ExportEditableShapes` гарантируют, что полученный слайд будет вести себя как нативный слайд PowerPoint — вы сможете кликнуть по текстовому полю или фигуре и отредактировать их непосредственно в PowerPoint.

## Step 4: Define the export area and fit it to a single slide

При **export Excel to PPTX** обычно требуется, чтобы определённый диапазон появился на слайде. Установка области печати и параметров масштабирования обеспечивает чистый вывод в один слайд.

```csharp
// Define the area of the first worksheet to export
Worksheet sheet = workbook.Worksheets[0];
sheet.PageSetup.PrintArea = "A1:G30";

// Fit the exported content to a single slide
sheet.PageSetup.FitToPagesTall = 1;
sheet.PageSetup.FitToPagesWide = 1;
```

*Почему это важно:* `PrintArea` ограничивает экспорт ячейками от A1 до G30, а `FitToPagesTall` и `FitToPagesWide` сжимают всё в один слайд, предотвращая появление лишних страниц.

## Step 5: Save the worksheet as an editable PPTX file

Теперь можно наконец **save workbook as PPTX** и завершить процесс **save Excel as PowerPoint**.

```csharp
// Save the worksheet as an editable PPTX file
workbook.Save(@"C:\Output\EditableShapes.pptx", exportOptions);
Console.WriteLine("Export completed: EditableShapes.pptx");
```

После выполнения программы откройте `EditableShapes.pptx` в Microsoft PowerPoint. Вы увидите слайд, отражающий выбранный диапазон Excel, а все текстовые поля и фигуры будут полностью редактируемыми.

### Expected output

* Файл `EditableShapes.pptx`, расположенный в `C:\Output\`.
* Один слайд PowerPoint, содержащий диапазон A1:G30.
* Текстовые поля, диаграммы и фигуры, которые можно двойным щелчком редактировать непосредственно в PowerPoint.

## Full source code (ready to copy)

```csharp
using Aspose.Cells;
using System;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Load the workbook that contains the shapes
            Workbook workbook = new Workbook(@"C:\Data\WithShapes.xlsx");

            // Step 2: Prepare export options to generate an editable PPTX slide
            ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
            {
                SaveFormat = SaveFormat.Pptx,
                ExportEditableText = true,   // keep text boxes editable
                ExportEditableShapes = true  // keep shapes editable
            };

            // Step 3: Define the area of the first worksheet to export
            Worksheet sheet = workbook.Worksheets[0];
            sheet.PageSetup.PrintArea = "A1:G30";

            // Step 4: Fit the exported content to a single slide
            sheet.PageSetup.FitToPagesTall = 1;
            sheet.PageSetup.FitToPagesWide = 1;

            // Step 5: Save the worksheet as an editable PPTX file
            workbook.Save(@"C:\Output\EditableShapes.pptx", exportOptions);
            Console.WriteLine("Export completed: EditableShapes.pptx");
        }
    }
}
```

## Common questions and edge‑case handling

| Question | Answer |
|----------|--------|
| **What if I have multiple worksheets?** | Loop through `workbook.Worksheets` and repeat steps 3‑5 for each sheet, changing the output file name (e.g., `Sheet1.pptx`, `Sheet2.pptx`). |
| **Can I export the whole workbook to a single PowerPoint deck?** | Yes. Set `ExportAllSheets = true` on `ImageOrPrintOptions`. Each worksheet becomes a separate slide. |
| **My shapes appear as images, not editable objects.** | Ensure `ExportEditableShapes = true` and that you are using Aspose.Cells 24.5+ (earlier versions lack this feature). |
| **The generated PPTX is too large.** | Reduce the print area, or lower the image resolution via `exportOptions.ImageResolution`. |
| **Do I need a license for production use?** | A paid license removes the evaluation watermark and unlocks full performance. The free trial works for testing. |

## Tips for robust production code

* **Validate file paths** before calling `Workbook` or `Save` to avoid `FileNotFoundException`.  
* **Wrap the export in a try/catch** block to handle licensing errors (`Aspose.Cells.LicenseException`).  
* **Dispose of the workbook** (`workbook.Dispose()`) when done to free unmanaged resources.  
* **Use async I/O** (`FileStream` with `await`) if you are exporting many large sheets in a web service.

## Next steps

Теперь, когда вы знаете, как **save Excel as PowerPoint**, можете изучить связанные темы:

* **Export Excel to PPTX with custom slide layouts** – настройте `SlideSize` и добавьте мастер‑слайд.  
* **Convert Excel slide to PDF** – используйте `SaveFormat.Pdf` для печатной версии.  
* **Batch convert a folder of workbooks** – объедините цикл, показанный выше, с `Directory.GetFiles`.  

Экспериментируйте с различными областями печати, параметрами масштабирования и темами PowerPoint, чтобы адаптировать вывод под фирменный стиль вашей организации.

---

*Happy coding! If this guide helped you **convert Excel to PowerPoint**, feel free to share it with teammates or open an issue on the Aspose.Cells GitHub repository for further assistance.*

## What Should You Learn Next?

Следующие учебники охватывают тесно связанные темы, которые развивают техники, продемонстрированные в этом руководстве. Каждый ресурс включает полностью рабочие примеры кода с пошаговыми объяснениями, помогающими освоить дополнительные возможности API и исследовать альтернативные подходы в ваших проектах.

- [How to save Excel as PowerPoint using C# and Aspose.Cells](/cells/english/net/converting-excel-files-to-other-formats/how-to-save-excel-as-powerpoint-using-c-and-aspose-cells/)
- [How to Save PPTX from Excel – Complete Guide to Export Excel Sheet PowerPoint](/cells/english/java/integration-interoperability/how-to-save-pptx-from-excel-complete-guide-to-export-excel-s/)
- [Convert Excel to PowerPoint – Full Step‑by‑Step Guide](/cells/english/java/integration-interoperability/convert-excel-to-powerpoint-full-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}