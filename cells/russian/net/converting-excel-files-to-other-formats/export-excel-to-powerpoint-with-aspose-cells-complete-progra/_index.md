---
category: general
date: 2026-08-14
description: Экспорт Excel в PowerPoint с использованием Aspose.Cells и изучите, как
  вычислять формулы Excel в коде. Пошаговый пример на C# с полным исходным кодом.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to powerpoint
- calculate excel formulas in code
- Aspose.Cells copy pivot table
- export editable objects pptx
- dynamic array EXPAND function
- C# workbook automation
language: ru
lastmod: 2026-08-14
og_description: Экспортируйте Excel в PowerPoint с помощью Aspose.Cells и вычисляйте
  формулы Excel в коде. Следуйте этому полному руководству, чтобы создавать редактируемые
  файлы PPTX из рабочих книг.
og_image_alt: Screenshot showing an Excel sheet being exported to a PowerPoint slide
  with editable textboxes
og_title: Экспорт Excel в PowerPoint с помощью Aspose.Cells – полный C#‑урок
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: Export Excel to PowerPoint using Aspose.Cells and learn how to calculate
    Excel formulas in code. Step‑by‑step C# example with full source.
  headline: Export Excel to PowerPoint with Aspose.Cells – complete programming guide
  type: TechArticle
- description: Export Excel to PowerPoint using Aspose.Cells and learn how to calculate
    Excel formulas in code. Step‑by‑step C# example with full source.
  name: Export Excel to PowerPoint with Aspose.Cells – complete programming guide
  steps:
  - name: Why this works
    text: '* **`Workbook`** loads the entire Excel file into memory, giving you full
      API access. * **`CopyRange`** with `CopyPivotTable = true` ensures the pivot
      table’s data source, cache, and layout are duplicated exactly—something older
      versions of Aspose.Cells could not do. * Adding a new worksheet (`Copy`'
  - name: Explanation
    text: '* **`WorkbookDesigner`** is a high‑level helper that prepares the workbook
      for export, handling Smart Markers, named ranges, and layout adjustments. *
      Setting `ExportEditableObjects = true` tells Aspose.Cells to translate Excel
      drawings into PowerPoint shapes rather than flattening them into images.'
  - name: Why you might use this
    text: '* **Uniform data type:** Exporting as strings avoids type‑mismatch errors
      when the consumer expects text. * **Custom formatting:** Replace `value.ToString()`
      with any custom formatter (e.g., `value.ToString("yyyy-MM-dd")` for dates).'
  - name: How the calculation engine works
    text: '* The `Formula` property stores the expression exactly as you would type
      it in Excel. * `CalculateFormula()` triggers a full workbook recalculation,
      respecting dependencies between cells. * The `EXPAND` function (available in
      Excel 365) returns a spill range based on the source cell (`B1`) and the s'
  - name: What to verify
    text: '* Open `result.xlsx` in Excel to confirm the pivot table copy, the `EXPAND`
      formula result, and any custom‑exported strings. * Open `output.pptx` in PowerPoint;
      you should see a slide that mirrors the Excel layout, and all charts/textboxes
      should be editable.'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
- PowerPoint export
- Office 365 functions
title: Экспорт Excel в PowerPoint с помощью Aspose.Cells – полное руководство по программированию
url: /ru/net/converting-excel-files-to-other-formats/export-excel-to-powerpoint-with-aspose-cells-complete-progra/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Экспорт Excel в PowerPoint с помощью Aspose.Cells – полное руководство по программированию

Если вам необходимо **программно экспортировать Excel в PowerPoint**, это руководство покажет, как сделать это с помощью Aspose.Cells для .NET. Вы также узнаете, как **вычислять формулы Excel в коде**, копировать сводные таблицы без потери определений и использовать новую функцию Office‑365 EXPAND для динамических массивов.

В следующих разделах мы пройдемся по реальному примеру на C#, объясним, почему каждая строка важна, и рассмотрим распространенные подводные камни, чтобы вы могли адаптировать решение к своим проектам.

## Что покрывает этот учебник

* Загрузка существующей книги (`input.xlsx`)  
* Копирование диапазона, содержащего сводную таблицу, с сохранением её определения  
* Экспорт книги в файл PowerPoint (`.pptx`) с редактируемыми текстовыми полями и фигурами  
* Экспорт диапазона ячеек в виде строк с использованием пользовательской логики  
* Вычисление формул Excel в коде, включая функцию Office‑365 EXPAND  
* Сохранение окончательной книги со всеми примененными изменениями  

**Требования**  
* .NET 6.0 или новее (код также работает с .NET Framework 4.7.2+)  
* Aspose.Cells для .NET v25.11 или новее (опция `CopyPivotTable` была введена в версии v25.11)  
* Базовое понимание C# и концепций Excel, таких как диапазоны, сводные таблицы и формулы  

> **Полезный совет:** Установите Aspose.Cells через NuGet (`Install-Package Aspose.Cells`), чтобы ваш проект был актуален с последними функциями.

## Экспорт Excel в PowerPoint с помощью Aspose.Cells

Первая основная задача — преобразовать книгу в презентацию PowerPoint, сохранив все визуальные элементы редактируемыми. Это необходимо, когда вы хотите автоматически генерировать наборы слайдов из финансовых отчетов или панелей мониторинга.

```csharp
using Aspose.Cells;
using Aspose.Cells.Export;      // ExportTableOptions, ExportOptions, etc.
using Aspose.Cells.Pivot;      // Pivot‑table APIs
using Aspose.Cells.Drawing;    // Shapes, textboxes, etc.

// Step 1: Load the workbook
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

// Step 2: Copy a range that contains a pivot table (preserves the definition)
Worksheet sourceSheet = workbook.Worksheets["Source"];
Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");   // includes a pivot table
Worksheet destinationSheet = workbook.Worksheets.Add("Copy");
destinationSheet.Cells.CopyRange(sourceRange, destinationSheet.Cells, new CopyOptions
{
    CopyPivotTable = true   // new option in v25.11
});
```

### Почему это работает

* **`Workbook`** загружает весь файл Excel в память, предоставляя полный доступ к API.  
* **`CopyRange`** с `CopyPivotTable = true` гарантирует точное дублирование источника данных, кэша и макета сводной таблицы — то, чего не могли делать более старые версии Aspose.Cells.  
* Добавление нового листа (`Copy`) позволяет оставить оригинальный лист нетронутым, что полезно для аудиторских следов.

## Экспорт книги в PowerPoint с редактируемыми объектами

Теперь мы преобразуем книгу в файл PowerPoint. Включив `ExportEditableObjects`, каждый график, фигура или текстовое поле становится нативным объектом PowerPoint, который пользователи могут редактировать непосредственно после экспорта.

```csharp
// Step 3: Export the workbook to PowerPoint with editable textboxes/shapes
WorkbookDesigner designer = new WorkbookDesigner(workbook);
designer.Process();   // processes Smart Markers if present
designer.ExportToPptx("YOUR_DIRECTORY/output.pptx", new ExportOptions
{
    ExportEditableObjects = true   // makes objects editable in the PPTX
});
```

### Объяснение

* **`WorkbookDesigner`** — высокоуровневый помощник, который готовит книгу к экспорту, обрабатывая Smart Markers, именованные диапазоны и корректировки макета.  
* Установка `ExportEditableObjects = true` указывает Aspose.Cells переводить рисунки Excel в фигуры PowerPoint, а не преобразовывать их в изображения. Это дает **полностью редактируемую** презентацию.

> **Особый случай:** Если ваша книга содержит сложные графики, построенные на внешних соединениях данных, убедитесь, что эти соединения разрешены до вызова `ExportToPptx`, иначе график может отображаться пустым.

## Экспорт диапазона в виде строк с использованием пользовательской логики

Иногда нужны необработанные строковые значения для дальнейшей обработки (например, передача в CSV‑парсер). Класс `ExportTableOptions` позволяет управлять тем, как преобразуется каждая ячейка.

```csharp
// Step 4: Export a range as strings using custom logic
ExportTableOptions tableOptions = new ExportTableOptions
{
    ExportAsString = true,
    CustomExport = (cell, value) => value.ToString()   // simple conversion for each cell
};
workbook.Worksheets[0].Cells.ExportTableAsString(tableOptions, "A1:D10");
```

### Почему вы могли бы использовать это

* **Единый тип данных:** Экспорт в виде строк избегает ошибок несоответствия типов, когда получатель ожидает текст.  
* **Пользовательское форматирование:** Замените `value.ToString()` любым пользовательским форматтером (например, `value.ToString("yyyy-MM-dd")` для дат).  

## Вычисление формул Excel в коде

Частая потребность — **вычислять формулы Excel в коде** без открытия Excel. Aspose.Cells предоставляет встроенный движок вычислений, который работает офлайн и поддерживает новейшие функции Office‑365, включая `EXPAND`.

```csharp
// Step 5: Use the new Office‑365 EXPAND function to create a dynamic array
Worksheet firstSheet = workbook.Worksheets[0];
firstSheet.Cells["A1"].Formula = "EXPAND(B1,5,3)";   // expands array starting at B1
workbook.CalculateFormula();   // forces recalculation of the formula
```

### Как работает движок вычислений

* Свойство `Formula` хранит выражение точно так же, как вы вводите его в Excel.  
* `CalculateFormula()` инициирует полную перерасчет книги, учитывая зависимости между ячейками.  
* Функция `EXPAND` (доступна в Excel 365) возвращает диапазон‑разлив на основе исходной ячейки (`B1`) и указанных строк (`5`) и столбцов (`3`).  

> **Совет:** Если нужно вычислить только часть книги, используйте `Worksheet.CalculateFormula()`, чтобы ограничить область и повысить производительность.

## Сохранение книги со всеми примененными изменениями

Наконец, запишите изменённую книгу обратно на диск. Вы можете сохранять в любом из поддерживаемых форматов (`.xlsx`, `.xls`, `.csv` и т.д.), изменив расширение файла.

```csharp
// Step 6: Save the workbook with all changes applied
workbook.Save("YOUR_DIRECTORY/result.xlsx");
```

### Что проверить

* Откройте `result.xlsx` в Excel, чтобы убедиться в копии сводной таблицы, результате формулы `EXPAND` и любых пользовательски экспортированных строк.  
* Откройте `output.pptx` в PowerPoint; вы должны увидеть слайд, отражающий макет Excel, и все графики/текстовые поля должны быть редактируемыми.

## Часто задаваемые вопросы и устранение неполадок

| Question | Answer |
|----------|--------|
| **Нужна ли лицензия для использования Aspose.Cells?** | Да. Пробная версия подходит для оценки, но полная лицензия удаляет водяные знаки оценки и открывает функцию `CopyPivotTable`. |
| **Что делать, если экспортированный PPTX показывает пустые фигуры?** | Убедитесь, что объекты рисунков в книге не скрыты (`Visible = true`) и что все внешние ссылки на изображения встроены перед экспортом. |
| **Могу ли я экспортировать несколько листов в отдельные слайды PPTX?** | Используйте `WorkbookDesigner.ExportToPptx` в цикле, указывая разные `ExportOptions` для каждого листа, или объедините их в одну презентацию, добавляя слайды вручную через Aspose.Slides. |
| **Является ли `CalculateFormula` потокобезопасным?** | Нет. Выполняйте вычисления в одном потоке или клонируйте книгу для каждого потока, чтобы избежать условий гонки. |

## Заключение

Теперь у вас есть **полное сквозное решение для экспорта Excel в PowerPoint** с использованием Aspose.Cells, и вы понимаете, как **вычислять формулы Excel в коде** — включая современную функцию `EXPAND`. В учебнике рассмотрены загрузка книги, копирование сводных таблиц, экспорт в редактируемый PowerPoint, пользовательский экспорт строк, вычисление формул и окончательное сохранение.

Отсюда вы можете:

* Расширить экспорт, включив несколько слайдов на лист (вторичное ключевое слово: *calculate Excel formulas in code* можно переиспользовать при генерации данных для графиков).  
* Интегрировать Aspose.Slides для добавления анимаций или макетов главных слайдов.  
* Заменить простой делегат `CustomExport` на локализованное форматирование для международных проектов.  

Не стесняйтесь экспериментировать с разными диапазонами, исследовать другие функции Office‑365 (например, `FILTER`, `SORT`) и комбинировать этот рабочий процесс с автоматической отправкой электронной почты для полностью автономных конвейеров отчетности.

---

## Что вам следует изучить дальше?

Следующие учебники охватывают тесно связанные темы, построенные на техниках, продемонстрированных в этом руководстве. Каждый ресурс включает полные работающие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [Автоматизация экспорта данных Excel с помощью Aspose.Cells для .NET: пошаговое руководство](/cells/english/net/automation-batch-processing/automate-excel-data-export-aspose-cells-net/)
- [Как экспортировать диаграммы Excel в PDF с помощью Aspose.Cells для .NET: пошаговое руководство](/cells/english/net/workbook-operations/export-excel-charts-pdf-aspose-cells-net/)
- [Экспорт ячеек Excel в изображение с помощью Aspose.Cells .NET: пошаговое руководство](/cells/english/net/import-export/export-excel-cells-to-image-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}