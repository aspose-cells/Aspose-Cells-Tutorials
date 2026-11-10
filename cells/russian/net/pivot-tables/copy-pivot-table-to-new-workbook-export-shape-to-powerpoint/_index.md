---
category: general
date: 2026-10-20
description: Скопируйте сводную таблицу в новую книгу с помощью Aspose.Cells и узнайте,
  как экспортировать редактируемую фигуру в PowerPoint в одном руководстве.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table to new workbook
- copy rows between worksheets
- Aspose.Cells copy rows
- export shape to PowerPoint
- editable textbox in PowerPoint
language: ru
lastmod: 2026-10-20
og_description: Скопировать сводную таблицу в новую книгу с помощью Aspose.Cells и
  экспортировать редактируемую форму в PowerPoint — пошаговый код, который вы можете
  запустить сегодня.
og_image_alt: Screenshot showing copy pivot table to new workbook using Aspose.Cells
og_title: Копировать сводную таблицу в новую книгу, экспортировать объект в PowerPoint
schemas:
- author: Aspose
  dateModified: '2026-10-20'
  description: Copy pivot table to new workbook using Aspose.Cells and learn how to
    export an editable shape to PowerPoint in a single guide.
  headline: Copy pivot table to new workbook, export shape to PowerPoint
  type: TechArticle
- description: Copy pivot table to new workbook using Aspose.Cells and learn how to
    export an editable shape to PowerPoint in a single guide.
  name: Copy pivot table to new workbook, export shape to PowerPoint
  steps:
  - name: – Load the source workbook and select the first worksheet
    text: '```csharp // Load the workbook that already contains the pivot table Workbook
      srcWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");'
  - name: – Define the cell area that includes the pivot table
    text: '```csharp // CellArea(startRow, startColumn, endRow, endColumn) // Here
      we copy rows 0‑20 and columns 0‑10, which covers the whole pivot table CellArea
      sourceArea = new CellArea(0, 0, 20, 10); ```'
  - name: – Create the destination workbook and get its first worksheet
    text: '```csharp // Create an empty workbook that will receive the copied range
      Workbook destWorkbook = new Workbook();'
  - name: – Copy the rows from the source area to the destination sheet
    text: '```csharp // CopyRows(startRow, endRow, destinationCells, destinationStartRow)
      srcWorksheet.Cells.CopyRows( sourceArea.StartRow, sourceArea.EndRow, destWorksheet.Cells,
      0); // start at row 0 in the destination sheet ```'
  - name: – Save the new workbook
    text: '```csharp destWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx"); ```'
  - name: – Create a new workbook and access its first worksheet
    text: '```csharp Workbook workbook = new Workbook(); // Empty workbook Worksheet
      worksheet = workbook.Worksheets[0]; // First (and only) sheet ```'
  - name: – Add a textbox shape to the worksheet
    text: '```csharp // AddTextBox(startRow, startColumn, width, height, text) int
      shapeIndex = worksheet.Shapes.AddTextBox(10, 10, 200, 50, "Editable text");
      ```'
  - name: – Retrieve the shape and modify its text
    text: '```csharp Shape textShape = worksheet.Shapes[shapeIndex]; textShape.Text
      = "Change me in PowerPoint"; ```'
  - name: – Save the workbook as a PowerPoint presentation
    text: '```csharp workbook.Save("YOUR_DIRECTORY/Presentation.pptx", SaveFormat.Pptx);
      ```'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Pivot Table
- PowerPoint Export
title: Скопировать сводную таблицу в новую книгу, экспортировать фигуру в PowerPoint
url: /ru/net/pivot-tables/copy-pivot-table-to-new-workbook-export-shape-to-powerpoint/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Копировать сводную таблицу в новую книгу, экспортировать форму в PowerPoint

Если вам нужно **copy pivot table to new workbook**, сохраняя её функциональность, это руководство покажет, как сделать это с помощью Aspose.Cells. Вы также увидите самый быстрый способ **export an editable shape to PowerPoint**, чтобы текстовое поле оставалось редактируемым после конвертации.

Многие разработчики полагают, что копирование диапазона, содержащего сводную таблицу, приведёт к потере логики сводной таблицы, или что формы становятся статическими изображениями при сохранении в формате PPTX. Этот учебник опровергает эти мифы и предоставляет надёжное, готовое к использованию в продакшене решение.

В следующих разделах вы:

* Загрузите исходную книгу и скопируете диапазон, включающий сводную таблицу.  
* Создадите целевую книгу, содержащую ту же сводную таблицу.  
* Добавите форму‑текстовое поле, измените её текст и сохраните книгу как презентацию PowerPoint, где текстовое поле остаётся редактируемым.  
* Поймёте, почему каждый вызов API необходим и как избежать распространённых подводных камней.

**Prerequisites**

* .NET 6.0 или новее (код также работает с .NET Framework 4.7+).  
* Aspose.Cells for .NET установлен (`Install-Package Aspose.Cells`).  
* Базовые знания C# и Visual Studio (или любой другой предпочитаемой IDE).

---

## Copy pivot table to new workbook

Этот пошаговый раздел демонстрирует, как скопировать диапазон, содержащий сводную таблицу, и сохранить определение сводной таблицы в новом файле.

### Step 1 – Load the source workbook and select the first worksheet

```csharp
// Load the workbook that already contains the pivot table
Workbook srcWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");

// The first worksheet (index 0) holds the pivot table we want to copy
Worksheet srcWorksheet = srcWorkbook.Worksheets[0];
```

*Почему?*  
`Workbook` — точка входа для любой работы с Excel в Aspose.Cells. Выбор правильного листа гарантирует, что мы работаем с точным расположением сводной таблицы.

### Step 2 – Define the cell area that includes the pivot table

```csharp
// CellArea(startRow, startColumn, endRow, endColumn)
// Here we copy rows 0‑20 and columns 0‑10, which covers the whole pivot table
CellArea sourceArea = new CellArea(0, 0, 20, 10);
```

*Почему?*  
Сводная таблица находится внутри определённого блока ячеек. Указав `CellArea`, полностью охватывающий сводную таблицу, Aspose.Cells знает, что нужно скопировать также скрытый кэш сводной таблицы.

### Step 3 – Create the destination workbook and get its first worksheet

```csharp
// Create an empty workbook that will receive the copied range
Workbook destWorkbook = new Workbook();

// Destination worksheet (also index 0)
Worksheet destWorksheet = destWorkbook.Worksheets[0];
```

*Почему?*  
Новая книга гарантирует отсутствие конфликтующих именованных диапазонов или существующих сводных таблиц, делая операцию копирования чистой.

### Step 4 – Copy the rows from the source area to the destination sheet

```csharp
// CopyRows(startRow, endRow, destinationCells, destinationStartRow)
srcWorksheet.Cells.CopyRows(
    sourceArea.StartRow,
    sourceArea.EndRow,
    destWorksheet.Cells,
    0); // start at row 0 in the destination sheet
```

*Почему?*  
`CopyRows` является частью **Aspose.Cells copy rows** API. Он копирует как значения ячеек, так и скрытый кэш сводной таблицы, поэтому после перемещения сводная таблица остаётся функциональной.

### Step 5 – Save the new workbook

```csharp
destWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx");
```

*Result*  
Откройте `CopyWithPivot.xlsx` в Excel. Сводная таблица выглядит точно так же, как в исходном файле, и её можно обновлять или изменять обычным способом.

---

## Export editable shape to PowerPoint

Теперь мы добавим форму‑текстовое поле, изменим её содержимое и сохраним книгу как файл PPTX. Форма останется полностью редактируемой при открытии в PowerPoint.

### Step 1 – Create a new workbook and access its first worksheet

```csharp
Workbook workbook = new Workbook();          // Empty workbook
Worksheet worksheet = workbook.Worksheets[0]; // First (and only) sheet
```

### Step 2 – Add a textbox shape to the worksheet

```csharp
// AddTextBox(startRow, startColumn, width, height, text)
int shapeIndex = worksheet.Shapes.AddTextBox(10, 10, 200, 50, "Editable text");
```

*Почему?*  
`AddTextBox` создаёт **editable textbox in PowerPoint**‑совместимую форму. Координаты задаются в пунктах; при необходимости скорректируйте их под ваш макет.

### Step 3 – Retrieve the shape and modify its text

```csharp
Shape textShape = worksheet.Shapes[shapeIndex];
textShape.Text = "Change me in PowerPoint";
```

*Почему?*  
Прямой доступ к объекту `Shape` позволяет менять свойства, такие как `Text`, `Font` или `Fill`. Этот шаг демонстрирует, как программно задать начальное содержимое.

### Step 4 – Save the workbook as a PowerPoint presentation

```csharp
workbook.Save("YOUR_DIRECTORY/Presentation.pptx", SaveFormat.Pptx);
```

*Result*  
Откройте `Presentation.pptx` в Microsoft PowerPoint. Текстовое поле появляется на первом слайде, и вы можете дважды щёлкнуть его, чтобы отредактировать текст так же, как любой нативный объект PowerPoint.

---

## Expected output

| File | What you’ll see |
|------|-----------------|
| `CopyWithPivot.xlsx` | Лист, содержащий оригинальную сводную таблицу, полностью функциональный (обновление работает). |
| `Presentation.pptx` | Один слайд с редактируемым текстовым полем, в котором написано «Change me in PowerPoint». |

---

## Common pitfalls and best‑practice tips

* **Pivot cache loss** – Если копировать только значения ячеек (например, используя `CopyRows` с флагом `PasteOptions` = `PasteValues`), кэш сводной таблицы будет опущен, и таблица станет статичной. Всегда используйте перегрузку `CopyRows` по умолчанию, как показано.  
* **Shape positioning** – `AddTextBox` использует единицы измерения в пунктах, а не индексы ячеек Excel. Проверьте координаты на тестовом файле, чтобы избежать размещения вне слайда.  
* **File format mismatch** – Сохранение книги как PPTX с помощью `SaveFormat.Pptx` автоматически конвертирует все поддерживаемые формы. Попытка сохранить как `Pdf` растеризует форму, делая её не редактируемой.

---

## Conclusion

Теперь вы знаете, как **copy pivot table to new workbook** и как **export an editable shape to PowerPoint** с помощью Aspose.Cells for .NET. Полные, исполняемые примеры кода охватывают каждый необходимый вызов API, объясняют, почему каждый шаг важен, и показывают ожидаемые результаты.

Далее вы можете изучить:

* **Working with charts** – копировать диаграммы вместе со сводными таблицами (`Aspose.Cells copy rows between worksheets`).  
* 

## What Should You Learn Next?

Следующие учебники охватывают тесно связанные темы, построенные на техниках, продемонстрированных в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, помогающими освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [Create New Workbook – How to Copy a Worksheet with a Pivot Table](/cells/english/net/excel-copy-worksheet/create-new-workbook-how-to-copy-a-worksheet-with-a-pivot-tab/)
- [Copy pivot table and export Excel to PPTX with Aspose.Cells](/cells/english/net/converting-excel-files-to-other-formats/copy-pivot-table-and-export-excel-to-pptx-with-aspose-cells/)
- [Create New Workbook in C# – Copy Pivot Table](/cells/english/net/pivot-tables/create-new-workbook-in-c-copy-pivot-table/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}