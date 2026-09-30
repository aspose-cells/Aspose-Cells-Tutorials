---
category: general
date: 2026-05-30
description: Как использовать SmartMarkerProcessor для переименования существующего
  листа и автоматизации задач переименования листов Excel в несколько простых шагов.
draft: false
keywords:
- how to use smartmarkerprocessor
- rename existing sheet
- automate excel sheet rename
language: ru
og_description: Как использовать SmartMarkerProcessor для переименования существующего
  листа и автоматизации задач переименования листов Excel в кратком пошаговом руководстве.
og_title: Как использовать SmartMarkerProcessor – переименовать существующий лист
  в Excel
schemas:
- author: Aspose
  dateModified: '2026-05-30'
  description: How to use SmartMarkerProcessor to rename existing sheet and automate
    Excel sheet rename tasks in a few simple steps.
  headline: How to Use SmartMarkerProcessor – Rename Existing Sheet in Excel
  type: TechArticle
- description: How to use SmartMarkerProcessor to rename existing sheet and automate
    Excel sheet rename tasks in a few simple steps.
  name: How to Use SmartMarkerProcessor – Rename Existing Sheet in Excel
  steps:
  - name: 1. Multiple Existing Detail Sheets
    text: If your template already contains **Detail**, **Detail_1**, and **Detail_2**,
      the processor will generate **Detail_3**. This behavior is deterministic, so
      you can rely on it for batch processing.
  - name: 2. Custom Prefixes or Suffixes
    text: You might want the new sheet to start with a date stamp, e.g., `"Detail_2023-09-01"`.
      Set `DetailSheetNewName = $"Detail_{DateTime.Today:yyyy-MM-dd}"`. The processor
      will still add numeric suffixes if needed.
  - name: 3. Renaming Other Sheets
    text: '`SmartMarkerOptions` also provides `HeaderSheetNewName` and `SummarySheetNewName`.
      Use them the same way to **rename existing sheet** types beyond the detail sheet.'
  - name: 4. Performance Considerations
    text: When processing large workbooks (hundreds of sheets), instantiate **one**
      `SmartMarkerProcessor` and reuse it across files. This reduces memory churn
      and speeds up the **automate excel sheet rename** workflow.
  type: HowTo
tags:
- Excel automation
- GemBox
- SmartMarker
title: Как использовать SmartMarkerProcessor – переименовать существующий лист в Excel
url: /ru/net/worksheet-management/how-to-use-smartmarkerprocessor-rename-existing-sheet-in-exc/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как использовать SmartMarkerProcessor – Переименовать существующий лист в Excel

Вы когда‑нибудь задумывались **как использовать SmartMarkerProcessor** для переименования существующего листа во время заполнения данными? Вы не одиноки. Многие разработчики сталкиваются с проблемой, когда их шаблон уже содержит лист “Detail”, а движок SmartMarker пытается создать ещё один с тем же именем. Хорошая новость? С помощью нескольких строк кода вы можете **автоматизировать переименование листов Excel** без нарушения рабочего процесса.

В этом руководстве мы пройдем полный, готовый к запуску пример, который точно показывает, как настроить процессор, переименовать существующие листы и поддерживать порядок в файлах Excel. Никаких догадок — только понятный код, объяснения *почему* каждая строка важна и советы по обработке граничных случаев, с которыми вы неизбежно столкнётесь.

---

## Требования

- **GemBox.Spreadsheet** (или любая библиотека, предоставляющая `SmartMarkerProcessor`) версии 2024‑latest, установленная через NuGet.  
- Среда разработки .NET (Visual Studio, VS Code, Rider — на ваш выбор).  
- Базовый шаблон Excel (`Template.xlsx`), который уже содержит лист с именем **Detail**.  
- Простой источник данных (например, `DataTable`, `List<T>` или анонимный объект), который вы хотите объединить с шаблоном.

Это всё. Если чего‑то не хватает, сразу скачайте пакет NuGet:

```bash
dotnet add package GemBox.Spreadsheet
```

---

![пример использования smartmarkerprocessor](/images/smartmarkerprocessor-rename.png "пример использования smartmarkerprocessor")

*Изображение выше иллюстрирует лист до и после операции переименования.*

---

## Шаг 1: Создать экземпляр SmartMarkerProcessor  

Первое, что вам нужно — объект **SmartMarkerProcessor**. Представьте его как движок, который читает ваш шаблон, ищет Smart Markers (например, `{{Name}}`) и записывает данные в соответствующие ячейки.

```csharp
using GemBox.Spreadsheet;
using GemBox.Spreadsheet.SmartMarkers;

// Initialize the component (license key is optional for the free version)
SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

// Load the workbook that contains the template sheet.
var wb = ExcelFile.Load("Template.xlsx");

// Create the processor instance.
SmartMarkerProcessor processor = new SmartMarkerProcessor();
```

> **Почему это важно:** Создание процессора **один раз** и повторное его использование в приложении уменьшает накладные расходы. Кроме того, загрузка книги заранее даёт вам доступ к коллекции листов, которая понадобится при переименовании листов.

---

## Шаг 2: Настроить параметры переименования существующего листа  

Теперь переходим к сути: указать SmartMarker, как вести себя при конфликте имён листов. Класс `SmartMarkerOptions` раскрывает свойство `DetailSheetNewName`. Если лист с именем `"Detail"` уже существует, процессор автоматически добавит суффикс (`_1`, `_2`, …), чтобы избежать конфликта.

```csharp
// Define processing options.
// The DetailSheetNewName property controls the base name for the detail sheet.
SmartMarkerOptions options = new SmartMarkerOptions
{
    // If "Detail" exists, the new sheet will become "Detail_1"
    DetailSheetNewName = "Detail"
};
```

> **Pro tip:** Если вам нужен пользовательский суффикс (например, `"Detail-Backup"`), просто задайте `DetailSheetNewName = "Detail-Backup"`. Процессор всё равно добавит номера при необходимости.  

> **Почему это важно:** Без этой настройки SmartMarker выбросит исключение или тихо перезапишет существующий лист, что приведёт к потере данных. Явное конфигурирование поведения переименования **автоматизирует переименование листов Excel** и сохраняет ваши шаблоны нетронутыми.

---

## Шаг 3: Подготовить источник данных  

SmartMarker может работать практически с любым перечислимым источником данных. Для иллюстрации используем простой список анонимных объектов, представляющих строки счета‑фактуры.

```csharp
var dataSource = new[]
{
    new { Item = "Widget A", Quantity = 5, Price = 9.99 },
    new { Item = "Widget B", Quantity = 2, Price = 19.95 },
    new { Item = "Widget C", Quantity = 1, Price = 49.50 }
};
```

Если у вас уже есть `DataTable` или `IEnumerable<T>`, просто подключите его — дополнительное преобразование не требуется.

---

## Шаг 4: Применить обработку SmartMarker к первому листу  

С процессором, параметрами и данными всё готово, пора выполнить слияние. Мы будем работать с **первым листом** (`wb.Worksheets[0]`), потому что именно там находится наш шаблон. Метод `Process` принимает три аргумента: лист, источник данных и параметры, которые мы определили ранее.

```csharp
// Apply SmartMarker processing.
// This will insert the data into the template and rename the detail sheet if needed.
processor.Process(wb.Worksheets[0], dataSource, options);
```

> **Что происходит под капотом?**  
> 1. SmartMarker сканирует лист в поисках маркеров вроде `{{Item}}`, `{{Quantity}}` и т.д.  
> 2. Он создаёт новый лист‑деталь, используя имя, заданное в `DetailSheetNewName`.  
> 3. Если лист с именем “Detail” уже существует, он автоматически становится “Detail_1”.  
> 4. Строки данных записываются на новый лист, сохраняя форматирование.

---

## Шаг 5: Сохранить результат и проверить переименование  

После обработки вам нужно сохранить книгу на диск и дважды проверить, что лист был переименован правильно.

```csharp
// Save the processed workbook.
wb.Save("Result.xlsx");

// Quick verification (optional console output)
Console.WriteLine("Worksheets in the resulting file:");
foreach (var sheet in wb.Worksheets)
    Console.WriteLine($"- {sheet.Name}");
```

Когда откроете `Result.xlsx`, вы должны увидеть лист с именем **Detail_1** (или **Detail_2**, если “Detail_1” уже существовал). Строки данных появятся под заголовочной строкой, которую вы разместили в шаблоне.

---

## Обработка распространённых граничных случаев  

### 1. Несколько существующих листов Detail  

Если ваш шаблон уже содержит **Detail**, **Detail_1** и **Detail_2**, процессор сгенерирует **Detail_3**. Такое поведение детерминировано, поэтому вы можете полагаться на него при пакетной обработке.

### 2. Пользовательские префиксы или суффиксы  

Возможно, вы захотите, чтобы новый лист начинался с даты, например, `"Detail_2023-09-01"`. Задайте `DetailSheetNewName = $"Detail_{DateTime.Today:yyyy-MM-dd}"`. При необходимости процессор всё равно добавит числовые суффиксы.

### 3. Переименование других листов  

`SmartMarkerOptions` также предоставляет `HeaderSheetNewName` и `SummarySheetNewName`. Используйте их так же, чтобы **переименовать существующий лист** других типов, помимо листа‑детали.

```csharp
options.HeaderSheetNewName = "Header";
options.SummarySheetNewName = "Summary";
```

### 4. Соображения производительности  

При обработке больших книг (сотни листов) создавайте **один** `SmartMarkerProcessor` и повторно используйте его для разных файлов. Это снижает нагрузку на память и ускоряет рабочий процесс **автоматизировать переименование листов Excel**.

---

## Полный рабочий пример  

Объединив всё вместе, получаем автономную программу, которую можно скопировать в консольное приложение и запустить сразу:

```csharp
using System;
using GemBox.Spreadsheet;
using GemBox.Spreadsheet.SmartMarkers;

class Program
{
    static void Main()
    {
        // 1. License & load template.
        SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");
        var wb = ExcelFile.Load("Template.xlsx");

        // 2. Create processor.
        SmartMarkerProcessor processor = new SmartMarkerProcessor();

        // 3. Define rename options.
        SmartMarkerOptions options = new SmartMarkerOptions
        {
            DetailSheetNewName = "Detail"
        };

        // 4. Prepare data source.
        var dataSource = new[]
        {
            new { Item = "Widget A", Quantity = 5, Price = 9.99 },
            new { Item = "Widget B", Quantity = 2, Price = 19.95 },
            new { Item = "Widget C", Quantity = 1, Price = 49.50 }
        };

        // 5. Process the first worksheet.
        processor.Process(wb.Worksheets[0], dataSource, options);

        // 6. Save the result.
        wb.Save("Result.xlsx");

        // 7. Verify sheet names.
        Console.WriteLine("Worksheets after processing:");
        foreach (var sheet in wb.Worksheets)
            Console.WriteLine($"- {sheet.Name}");
    }
}
```

**Ожидаемый вывод** (консоль):

```
Worksheets after processing:
- Sheet1
- Detail_1
```

Откройте `Result.xlsx`, и вы увидите данные аккуратно заполненными под новой вкладкой **Detail_1**.

---

## Итоги  

Мы рассмотрели **как использовать SmartMarkerProcessor** для безопасного переименования существующего листа и полной **автоматизации переименования листов Excel**. Ключевые выводы:

1. Создайте один экземпляр `SmartMarkerProcessor`.  
2. Установите `DetailSheetNewName` (или другие параметры имён листов), чтобы контролировать логику переименования.  
3. Передайте ваш источник данных и параметры в `Process`.  
4. Сохраните и проверьте, что лист был переименован как ожидалось.

Следуя этим шагам, вы сможете интегрировать SmartMarker в любой конвейер отчётности — будь то генерация счетов‑фактур, журналов аудита или ежемесячных дашбордов. Подход масштабируем, корректно обрабатывает конфликты имён и сохраняет ваши шаблоны Excel переиспользуемыми.

---

## Что дальше?  

- **Изучить другие SmartMarkerOptions**: `HeaderSheetNewName`, `SummarySheetNewName` и `InsertBlankRows` для более тонкой настройки.  
- **Комбинировать со стилизацией**: Используйте богатый API форматирования GemBox для применения цветов, границ или условного форматирования после слияния.  
- **Пакетная обработка нескольких книг**: Пройдитесь по каталогу шаблонов, повторно используя один и тот же экземпляр процессора для максимальной пропускной способности.

## Что вам стоит изучить дальше?

- [Как объединять и переименовывать листы Excel с помощью Aspose.Cells для .NET: пошаговое руководство](/cells/english/net/worksheet-management/merge-rename-excel-sheets-aspose-cells-net/)
- [Как изменить идентификаторы листов Excel в .NET с помощью Aspose.Cells: подробное руководство](/cells/english/net/worksheet-management/change-excel-sheet-id-net-aspose-cells/)
- [Как использовать Aspose.Cells для .NET для группировки строк и столбцов в Excel](/cells/english/net/data-analysis/excel-grouping-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}