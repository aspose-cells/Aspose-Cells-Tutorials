---
category: general
date: 2026-09-15
description: Узнайте, как копировать сводную таблицу, копировать лист с сводной таблицей
  и сохранять книгу в формате pptx с помощью Aspose.Cells в C#. Полное пошаговое руководство.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot table
- copy worksheet with pivot
- save workbook as pptx
language: ru
lastmod: 2026-09-15
og_description: Как копировать сводную таблицу, копировать лист со сводной таблицей
  и сохранять книгу в формате pptx с помощью Aspose.Cells. Следуйте полным, исполняемым
  примерам на C#.
og_image_alt: Screenshot showing how to copy pivot table in a C# code editor
og_title: Как скопировать сводную таблицу и экспортировать листы — полное руководство
  по C#
schemas:
- author: Aspose
  dateModified: '2026-09-15'
  description: Learn how to copy pivot table, copy worksheet with pivot, and save
    workbook as pptx using Aspose.Cells in C#. Complete step‑by‑step guide.
  headline: How to copy pivot table while preserving worksheets
  type: TechArticle
- description: Learn how to copy pivot table, copy worksheet with pivot, and save
    workbook as pptx using Aspose.Cells in C#. Complete step‑by‑step guide.
  name: How to copy pivot table while preserving worksheets
  steps:
  - name: – Load the source workbook that holds the pivot table
    text: '```csharp // Load the workbook that contains the pivot table you want to
      copy Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx"); ```'
  - name: – Create an empty destination workbook
    text: '```csharp // Create a new, empty workbook that will receive the copied
      data Workbook destinationWorkbook = new Workbook(); ```'
  - name: – Copy the rows that include the pivot table
    text: '```csharp // Copy rows 0‑19 (A1:G20) from the first worksheet of the source
      sourceWorkbook.Worksheets[0].Cells.CopyRows(0, 0, 20); ```'
  - name: – Copy the columns that contain the pivot table
    text: '```csharp // Copy columns 0‑6 (A‑G) from the same worksheet sourceWorkbook.Worksheets[0].Cells.CopyColumns(0,
      0, 7); ```'
  - name: – Transfer the prepared sheet into the destination workbook
    text: '```csharp // Move the fully prepared worksheet into the destination workbook
      sourceWorkbook.Worksheets[0].Copy(destinationWorkbook.Worksheets[0]); ```'
  - name: – Save the result – the pivot table remains intact
    text: '```csharp // Save the destination workbook; the pivot table works exactly
      like the original destinationWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx");
      ```'
  - name: – Load the workbook that includes the textbox
    text: '```csharp // Load the Excel file that contains an editable textbox shape
      Workbook workbookWithTextbox = new Workbook("YOUR_DIRECTORY/DocWithTextbox.xlsx");
      ```'
  - name: – Configure PPTX save options
    text: '```csharp // Create PPTX save options and enable the editable textbox feature
      (available from v25.11) PptxSaveOptions pptxOptions = new PptxSaveOptions {
      ExportEditableTextBox = true }; ```'
  - name: – Save the workbook as PPTX
    text: '```csharp // Export the workbook to a PPTX file; the textbox stays editable
      in PowerPoint workbookWithTextbox.Save("YOUR_DIRECTORY/Result.pptx", pptxOptions);
      ```'
  - name: – Prepare the SmartMarkerProcessor
    text: '```csharp // Initialise the processor that will fill Smart Markers SmartMarkerProcessor
      smartMarkerProcessor = new SmartMarkerProcessor(); ```'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Как скопировать сводную таблицу, сохраняя рабочие листы
url: /ru/net/pivot-tables/how-to-copy-pivot-table-while-preserving-worksheets/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как скопировать сводную таблицу, сохраняя листы

Если вам нужно **how to copy pivot table** из одной книги в другую, не теряя базовый кэш сводной таблицы, это руководство предоставляет готовое решение. Вы также увидите, как **copy worksheet with pivot** и как **save workbook as pptx**, сохраняя редактируемые текстовые поля. Все примеры используют последнюю версию Aspose.Cells for .NET, так что вы можете вставить код в любой проект C# и увидеть мгновенный результат.

Работа с файлами Excel программно часто включает перемещение данных между книгами, экспорт в презентации или вставку сложных Smart Markers. Ниже приведённые три фрагмента кода охватывают эти распространённые сценарии и объясняют, почему каждый шаг важен.

## Требования

Перед началом убедитесь, что у вас есть:

* .NET 6.0 или новее установлен  
* Aspose.Cells for .NET (version 25.11 или новее) подключён в проекте  
* Папка с именем `YOUR_DIRECTORY`, где будут читаться и записываться образцы файлов  

Дополнительные пакеты NuGet не требуются.

---

## Как скопировать сводную таблицу с помощью Aspose.Cells

Копирование диапазона, содержащего сводную таблицу, при сохранении кэша сводной таблицы — частая необходимость. Ниже показана точная последовательность действий, которую вам нужно выполнить.

### Шаг 1 – Загрузить исходную книгу, содержащую сводную таблицу

```csharp
// Load the workbook that contains the pivot table you want to copy
Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");
```

*Why*: Aspose.Cells читает книгу в память, предоставляя доступ к листам, ячейкам и сводным таблицам.

### Шаг 2 – Создать пустую целевую книгу

```csharp
// Create a new, empty workbook that will receive the copied data
Workbook destinationWorkbook = new Workbook();
```

*Why*: Начало с пустой книги гарантирует, что скрытые стили или именованные диапазоны не помешают операции копирования.

### Шаг 3 – Скопировать строки, включающие сводную таблицу

```csharp
// Copy rows 0‑19 (A1:G20) from the first worksheet of the source
sourceWorkbook.Worksheets[0].Cells.CopyRows(0, 0, 20);
```

*Why*: `CopyRows` копирует сырые значения ячеек, форматы и ссылки на базовый кэш сводной таблицы. Диапазон должен охватывать всю область сводной таблицы.

### Шаг 4 – Скопировать столбцы, содержащие сводную таблицу

```csharp
// Copy columns 0‑6 (A‑G) from the same worksheet
sourceWorkbook.Worksheets[0].Cells.CopyColumns(0, 0, 7);
```

*Why*: Сводные таблицы охватывают как строки, так и столбцы; копирование столбцов гарантирует сохранение полной раскладки таблицы.

### Шаг 5 – Перенести подготовленный лист в целевую книгу

```csharp
// Move the fully prepared worksheet into the destination workbook
sourceWorkbook.Worksheets[0].Copy(destinationWorkbook.Worksheets[0]);
```

*Why*: Метод `Copy` клонирует лист, включая кэш сводной таблицы, поэтому целевая книга отображает идентичную сводную таблицу.

### Шаг 6 – Сохранить результат – сводная таблица остаётся нетронутой

```csharp
// Save the destination workbook; the pivot table works exactly like the original
destinationWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx");
```

*Why*: Сохранение книги записывает все внутренние структуры, гарантируя возможность последующего обновления сводной таблицы.

**Pro tip**: После копирования вы можете вызвать `destinationWorkbook.Worksheets[0].PivotTables[0].Refresh()`, чтобы обновить данные, если исходные данные изменились.

---

## Копировать лист со сводной таблицей – краткая альтернатива

Если вам просто нужно дублировать весь лист, уже содержащий сводную таблицу, вы можете пропустить шаги копирования строк/столбцов и воспользоваться методом `Copy` уровня листа напрямую.

```csharp
// Load source workbook
Workbook src = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");

// Create destination workbook
Workbook dst = new Workbook();

// Copy the first worksheet (including its pivot table) to the destination
src.Worksheets[0].Copy(dst.Worksheets[0]);

// Save the new file
dst.Save("YOUR_DIRECTORY/WorksheetCopy.xlsx");
```

Этот подход полезен, когда лист не содержит дополнительных данных за пределами области сводной таблицы. Операция **copy worksheet with pivot** автоматически сохраняет всё форматирование, именованные диапазоны и кэши сводных таблиц.

---

## Сохранить книгу как PPTX с редактируемыми текстовыми полями

Экспорт листа Excel, содержащего редактируемый текстовый блок, в PowerPoint может потребоваться для панелей отчётности. Ниже показан код, демонстрирующий **save workbook as pptx**, сохраняя возможность редактирования текстового блока.

### Шаг 1 – Загрузить книгу, включающую текстовый блок

```csharp
// Load the Excel file that contains an editable textbox shape
Workbook workbookWithTextbox = new Workbook("YOUR_DIRECTORY/DocWithTextbox.xlsx");
```

### Шаг 2 – Настроить параметры сохранения PPTX

```csharp
// Create PPTX save options and enable the editable textbox feature (available from v25.11)
PptxSaveOptions pptxOptions = new PptxSaveOptions
{
    ExportEditableTextBox = true
};
```

*Why*: Установка `ExportEditableTextBox` указывает Aspose.Cells преобразовать текстовый блок Excel в форму PowerPoint, которая остаётся редактируемой после экспорта.

### Шаг 3 – Сохранить книгу как PPTX

```csharp
// Export the workbook to a PPTX file; the textbox stays editable in PowerPoint
workbookWithTextbox.Save("YOUR_DIRECTORY/Result.pptx", pptxOptions);
```

**Expected result**: Откройте `Result.pptx` в PowerPoint, выберите текстовый блок и отредактируйте его содержимое так же, как любой встроенный объект.

**Common question**: *Что делать, если нужно зафиксировать текстовый блок?*  
Установите `pptxOptions.ExportEditableTextBox = false`; форма будет преобразована в статическое изображение.

---

## Экспорт Smart Marker, содержащего массив JSON, как значение одной ячейки

Smart Markers позволяют заполнять шаблоны Excel сложными структурами данных. Ниже полное пример, демонстрирующий обработку данных в стиле **how to copy pivot table**, одновременно вставляя массив JSON в одну ячейку.

### Шаг 1 – Подготовить SmartMarkerProcessor

```csharp
// Initialise the processor that will fill Smart Markers
SmartMarkerProcessor smartMarkerProcessor = new SmartMarkerProcessor();
```

### Шаг 2 – Вставить Smart Marker в ячейку A1

```csharp
// The marker ${Orders:ArrayAsSingle} tells the processor to write the whole array into one cell
Workbook workbook = new Workbook();
workbook.Worksheets[0].Cells["A1"].PutValue("${Orders:ArrayAsSingle}");
```

### Шаг 3 – Определить источник данных с массивом в стиле JSON

```csharp
// Anonymous object that mimics a JSON array
var dataModel = new { Orders = new[] { "A", "B", "C" } };
```

### Шаг 4 – Обработать книгу

```csharp
// Fill the Smart Marker with the array data; the array becomes a comma‑separated string
smartMarkerProcessor.Process(workbook, dataModel);
```

### Шаг 5 – Сохранить полученную книгу

```csharp
// Persist the workbook; cell A1 now contains "A,B,C"
workbook.Save("YOUR_DIRECTORY/JsonSingleCell.xlsx");
```

**Result verification**: Откройте `JsonSingleCell.xlsx` и убедитесь, что ячейка A1 содержит `A,B,C`. Это демонстрирует, как рассматривать коллекцию как значение одной ячейки — шаблон, часто необходимый при экспорте данных для downstream‑систем.

---

## Полный рабочий пример

Ниже представлен единый пример программы, объединяющий три сценария. Скопируйте код в консольное приложение, скорректируйте пути к файлам и запустите его, чтобы увидеть все три результата.

```csharp
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1. How to copy pivot table (preserve pivot cache)
        // -------------------------------------------------
        Workbook srcPivot = new Workbook("YOUR_DIRECTORY/Source.xlsx");
        Workbook dstPivot = new Workbook();
        srcPivot.Worksheets[0].Cells.CopyRows(0, 0, 20);
        srcPivot.Worksheets[0].Cells.CopyColumns(0, 0, 7);
        srcPivot.Worksheets[0].Copy(dstPivot.Worksheets[0]);
        dstPivot.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx");

        // -------------------------------------------------
        // 2. Save workbook as PPTX with editable textbox
        // -------------------------------------------------
        Workbook txtWorkbook = new Workbook("YOUR_DIRECTORY/DocWithTextbox.xlsx");
        PptxSaveOptions pptxOpts = new PptxSaveOptions { ExportEditableTextBox = true };
        txtWorkbook.Save("YOUR_DIRECTORY/Result.pptx", pptxOpts);

        // -------------------------------------------------
        // 3. Export Smart Marker containing a JSON array
        // -------------------------------------------------
        SmartMarkerProcessor smProcessor = new SmartMarkerProcessor();
        Workbook smWorkbook = new Workbook();
        smWorkbook.Worksheets[0].Cells["A1"].PutValue("${Orders:ArrayAsSingle}");
        var model = new { Orders = new[] { "A", "B", "C" } };
        smProcessor.Process(smWorkbook, model);
        smWorkbook.Save("YOUR_DIRECTORY/JsonSingleCell.xlsx");
    }
}
```

Запуск этой программы выдаёт:

* `CopyWithPivot.xlsx` – точная копия оригинальной сводной таблицы.  
* `Result.pptx` – слайд PowerPoint с редактируемым текстовым блоком.  
* `JsonSingleCell.xlsx` – лист, где массив JSON отображается в одной ячейке.

---

## Заключение

Теперь вы знаете, как безопасно **how to copy pivot table**, как **copy worksheet with pivot** одним вызовом и как **save workbook as pptx**, сохраняя редактируемые текстовые поля. Эти шаблоны охватывают наиболее распространённые рабочие процессы Excel‑to‑PowerPoint и Excel‑to‑JSON, с которыми вы столкнётесь в проектах корпоративной автоматизации.

Далее рекомендуется изучить:

* Обновление скопированных сводных таблиц программно (`PivotTable.Refresh()`)  
* Экспорт в другие форматы, такие как PDF или HTML (`PdfSaveOptions`, `HtmlSaveOptions`)  
* Использование расширенных опций Smart Marker, например пользовательские функции или условное форматирование  

Экспериментируйте с различными диапазонами, несколькими листами или более крупными структурами JSON. API Aspose.Cells предоставляет тонкий контроль, позволяя адаптировать эти примеры к любой реальной задаче. Приятного кодинга!

## Что изучать дальше?

Следующие руководства охватывают тесно связанные темы, расширяющие техники, продемонстрированные в этом руководстве. Каждый ресурс включает полные рабочие примеры кода с пошаговыми объяснениями, помогающими освоить дополнительные возможности API и исследовать альтернативные подходы в ваших проектах.

- [Создание новой книги – Как скопировать лист со сводной таблицей](/cells/english/net/excel-copy-worksheet/create-new-workbook-how-to-copy-a-worksheet-with-a-pivot-tab/)
- [Как скопировать сводную таблицу в C# – Конвертация Excel в PPTX, копирование диапазона и создание текстового блока](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/)
- [Копирование листов внутри книги с помощью Aspose.Cells for .NET – Пошаговое руководство](/cells/english/net/worksheet-management/copy-sheets-within-workbook-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}