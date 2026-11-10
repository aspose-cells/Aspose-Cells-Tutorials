---
category: general
date: 2026-08-17
description: Сохранить Excel в PowerPoint с помощью C# — пошаговое руководство по
  конвертации файлов XLSX, редактированию текстовых полей и генерации PPTX‑файла.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save excel as powerpoint
- convert excel to powerpoint
- how to convert xlsx
- make textbox editable
- how to edit textboxes
language: ru
lastmod: 2026-08-17
og_description: Сохраните Excel как PowerPoint на C# с полным примером кода. Узнайте,
  как конвертировать XLSX, сделать текстовые поля редактируемыми и экспортировать
  в PPTX.
og_image_alt: Screenshot showing Excel data saved as a PowerPoint slide
og_title: Сохранить Excel как PowerPoint в C# – полное руководство по конвертации
schemas:
- author: Aspose
  dateModified: '2026-08-17'
  description: Save Excel as PowerPoint with C# – step‑by‑step guide to convert XLSX
    files, make textboxes editable, and generate PPTX output.
  headline: How to save Excel as PowerPoint using C# and Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel-to-PowerPoint
title: Как сохранить Excel в PowerPoint с помощью C# и Aspose.Cells
url: /ru/net/converting-excel-files-to-other-formats/how-to-save-excel-as-powerpoint-using-c-and-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как сохранить Excel в PowerPoint с помощью C# и Aspose.Cells

Если вам нужно **сохранить Excel в PowerPoint** в проекте .NET, это руководство покажет вам полное готовое к запуску решение. Вы увидите, как загрузить книгу XLSX, сделать каждый текстовый блок на листе редактируемым и экспортировать результат в файл PPTX — всё это с помощью всего нескольких строк C#.

Преобразование Excel в PowerPoint — распространённая задача для отчётных панелей, наборов слайдов или автоматической генерации презентаций. В этом руководстве также рассматривается **как программно редактировать текстовые блоки**, чтобы вы могли настроить содержимое слайда перед сохранением.

## Предварительные требования

* .NET 6.0 (или новее) SDK установлен  
* Среда разработки, например Visual Studio 2022 или VS Code  
* Лицензия Aspose.Cells для .NET (или бесплатный ключ оценки) — загрузите с [веб‑сайта Aspose](https://products.aspose.com/cells/net/)  
* Файл `input.xlsx`, который вы хотите конвертировать  

> **Совет:** Если вы используете бесплатную оценочную версию, полученный PPTX будет содержать водяной знак. Лицензированная версия удаляет его.

## Шаг 1: Установите пакет Aspose.Cells NuGet

Откройте терминал в папке проекта и выполните:

```bash
dotnet add package Aspose.Cells
```

Это добавит сборку `Aspose.Cells`, которая предоставляет классы `Workbook`, `Worksheet` и `Shape`, необходимые для конвертации.

## Шаг 2: Создайте каркас консольного приложения

Создайте новый консольный проект (если у вас его ещё нет):

```bash
dotnet new console -n ExcelToPptxDemo
cd ExcelToPptxDemo
```

Замените сгенерированный `Program.cs` кодом, показанным в следующих шагах.

## Шаг 3: Загрузите книгу и выберите первый лист

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Drawing;

class Program
{
    static void Main()
    {
        // Load the workbook from a file – adjust the path to your environment
        string inputPath = @"YOUR_DIRECTORY\input.xlsx";
        Workbook workbook = new Workbook(inputPath);

        // Get the first worksheet in the workbook
        Worksheet worksheet = workbook.Worksheets[0];
```

**Почему это важно:**  
`Workbook` читает файл Excel в память, а `Worksheet` предоставляет доступ к ячейкам листа, диаграммам и объектам. Первый лист часто является отчётом по умолчанию, который вы хотите представить.

## Шаг 4: Сделайте каждый текстовый блок на листе редактируемым

```csharp
        // Iterate through all shapes on the worksheet
        foreach (Shape shapeItem in worksheet.Shapes)
        {
            // Check if the shape is a textbox (ShapeType.TextBox)
            if (shapeItem.Type == ShapeType.TextBox)
            {
                // The IsEditable property was added in Aspose.Cells 25.11
                shapeItem.TextBox.IsEditable = true;
            }
        }
```

**Зачем это нужно:**  
По умолчанию текстовые блоки, импортированные из Excel, являются только для чтения при отображении в PowerPoint. Установка `IsEditable = true` позволяет вам (или будущим пользователям PowerPoint) изменять текст непосредственно на слайде.

## Шаг 5: Сохраните книгу как презентацию PowerPoint

```csharp
        // Define the output path for the PPTX file
        string outputPath = @"YOUR_DIRECTORY\output.pptx";

        // Save the workbook as a PowerPoint presentation
        workbook.Save(outputPath, SaveFormat.Pptx);

        Console.WriteLine($"Conversion complete. PPTX saved to: {outputPath}");
    }
}
```

**Что происходит под капотом:**  
`Workbook.Save` определяет значение перечисления `SaveFormat.Pptx` и преобразует макет листа Excel — включая строки, столбцы, диаграммы и теперь редактируемые текстовые блоки — в объекты слайдов PowerPoint.

## Полный исходный код (рабочий пример)

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Drawing;

class Program
{
    static void Main()
    {
        // Step 1: Load the workbook from a file
        string inputPath = @"YOUR_DIRECTORY\input.xlsx";
        Workbook workbook = new Workbook(inputPath);

        // Step 2: Get the first worksheet in the workbook
        Worksheet worksheet = workbook.Worksheets[0];

        // Step 3: Make every textbox on the sheet editable (property added in version 25.11)
        foreach (Shape shapeItem in worksheet.Shapes)
        {
            if (shapeItem.Type == ShapeType.TextBox)
            {
                shapeItem.TextBox.IsEditable = true;
            }
        }

        // Step 4: Save the workbook as a PowerPoint presentation
        string outputPath = @"YOUR_DIRECTORY\output.pptx";
        workbook.Save(outputPath, SaveFormat.Pptx);

        Console.WriteLine($"Conversion complete. PPTX saved to: {outputPath}");
    }
}
```

### Ожидаемый вывод

При запуске программы (`dotnet run`) вы должны увидеть:

```
Conversion complete. PPTX saved to: YOUR_DIRECTORY\output.pptx
```

Открытие `output.pptx` в Microsoft PowerPoint отобразит слайд, копирующий оригинальный лист Excel. Все текстовые блоки можно редактировать напрямую двойным щелчком.

## Часто задаваемые вопросы и особые случаи

| Вопрос | Ответ |
|----------|--------|
| **Можно ли конвертировать конкретный лист вместо первого?** | Да. Замените `workbook.Worksheets[0]` на `workbook.Worksheets["SheetName"]` или любой нужный индекс. |
| **Что делать, если книга содержит несколько листов?** | Вызовите `workbook.Save` для каждого листа, задавая отдельное имя файла PPTX, или объедините их в одну презентацию, используя объекты `Presentation` из Aspose.Slides. |
| **Будут ли сохранены диаграммы?** | Aspose.Cells автоматически преобразует диаграммы Excel в объекты диаграмм PowerPoint. Дополнительный код не требуется. |
| **Как изменить размер слайда?** | После `workbook.Save` вы можете загрузить сгенерированный PPTX с помощью Aspose.Slides и изменить `Presentation.SlideSize`. |
| **Что делать, если нужно изменить текст в текстовом блоке перед сохранением?** | Получите доступ к `shapeItem.TextBox.Text` внутри цикла, измените его, затем установите `IsEditable = true`. Пример: `shapeItem.TextBox.Text = "New title";` |

## Советы по устранению неполадок

* **“ShapeType.TextBox” не найден** — Убедитесь, что вы используете Aspose.Cells версии 25.11 или новее; более ранние версии не имеют свойства `IsEditable`.  
* **Ошибки «Файл не найден»** — Проверьте, что `YOUR_DIRECTORY` является абсолютным путём или что относительный путь указывает на правильное расположение.  
* **Лицензия не применена** — Вызовите `License license = new License(); license.SetLicense("Aspose.Total.NET.lic");` перед загрузкой книги, чтобы убрать водяные знаки оценки.

## Заключение

Теперь вы знаете, как **сохранить Excel в PowerPoint** с помощью C#, загрузив книгу XLSX, сделав каждый текстовый блок редактируемым и экспортировав в PPTX. Этот метод автоматически обрабатывает диаграммы, изображения и форматирование ячеек, предоставляя готовую к презентации набор слайдов.

Далее изучайте связанные темы, такие как **конвертация Excel в PowerPoint с помощью Aspose.Slides**, **как программно редактировать текстовые блоки после конвертации**, или **пакетная обработка нескольких книг**. Каждая из них опирается на основные шаги, описанные здесь, и может ещё больше автоматизировать ваш процесс создания отчётов.

## Что изучать дальше?

Следующие руководства охватывают тесно связанные темы, которые опираются на техники, продемонстрированные в этом руководстве. Каждый ресурс включает полные работающие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [Как конвертировать Excel в PowerPoint с помощью Aspose.Cells для .NET: Полное руководство](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [Как скопировать сводную таблицу в C# — Конвертировать Excel в PPTX, копировать диапазон и делать текстовые блоки](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/)
- [Как сохранять файлы Excel в нескольких форматах с помощью Aspose.Cells .NET (руководство 2023)](/cells/english/net/workbook-operations/aspose-cells-net-save-excel-formats/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}