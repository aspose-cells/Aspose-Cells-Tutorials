---
category: general
date: 2026-03-30
description: Как копировать лист в C# с помощью Aspose.Cells — пошаговое руководство,
  охватывающее копирование диапазона ячеек, копирование столбцов между листами, копирование
  сводной таблицы листа и добавление кода нового листа.
draft: false
keywords:
- how to copy worksheet
- copy cell range
- copy columns between sheets
- copy worksheet pivot table
- add new worksheet code
language: ru
og_description: Узнайте, как копировать лист в C# с помощью Aspose.Cells. Это руководство
  показывает, как копировать диапазон ячеек, сохранять сводные таблицы, копировать
  столбцы между листами и добавлять код нового листа.
og_title: Как скопировать лист в C# – Полный учебник Aspose.Cells
tags:
- Aspose.Cells
- C#
- Excel Automation
title: Как скопировать лист в C# с помощью Aspose.Cells – Полное руководство
url: /ru/net/excel-copy-worksheet/how-to-copy-worksheet-in-c-with-aspose-cells-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как скопировать лист в C# с помощью Aspose.Cells – Полное руководство

Когда‑нибудь задумывались **how to copy worksheet** в C# без потери единой сводной таблицы или формулы? Вы не одиноки — многие разработчики сталкиваются с проблемой, когда нужно дублировать лист, сохранив все детали. В этом руководстве мы пройдем практическое, сквозное решение, которое не только копирует данные, но и сохраняет **copy worksheet pivot table**, обрабатывает **copy cell range** и показывает **add new worksheet code**, который вам понадобится.

Мы охватим всё от загрузки исходной книги до сохранения файла назначения, чтобы вы могли copy columns between sheets, сохранять объекты и поддерживать чистоту кода. Без расплывчатых ссылок, только полноценный, исполняемый пример, который вы можете сразу добавить в свой проект.

## Что покрывает этот учебник

- Загрузка существующего Excel‑файла с помощью Aspose.Cells  
- Использование **add new worksheet code** для создания целевого листа  
- Определение **copy cell range**, включающего сводную таблицу  
- Настройка **CopyOptions** для сохранения диаграмм, формул и сводных таблиц без изменений  
- Выполнение **copy columns between sheets** с точностью по строкам  
- Сохранение результата и проверка корректности копирования листа  

К концу этого руководства вы сможете уверенно ответить на вопрос «how to copy worksheet», независимо от того, автоматизируете ли вы отчёты или создаёте пользовательский интерфейс, управляемый электронными таблицами.

## Как скопировать лист – Обзор

Прежде чем погрузиться в код, давайте очертим общий процесс. Представьте его как рецепт:

1. **Load** исходную книгу (`Source.xlsx`).  
2. **Add** новый лист для размещения копии (`add new worksheet code`).  
3. **Define** область, которую нужно дублировать (`copy cell range`).  
4. **Configure** параметры копирования, чтобы сводная таблица сохранилась (`copy worksheet pivot table`).  
5. **Copy** строки и столбцы (`copy columns between sheets`).  
6. **Save** новую книгу (`Destination.xlsx`).  

Вот и всё — шесть шагов, без магии. Каждый шаг объясняется ниже с фрагментами кода и обоснованием.

## Шаг 1 – Загрузка исходной книги

Первое и главное: вам нужен экземпляр `Workbook`, указывающий на файл, который вы хотите дублировать. Этот шаг важен, потому что Aspose.Cells работает напрямую с файловой системой, а не с пользовательским интерфейсом Office.

```csharp
using Aspose.Cells;

// Path to the original file
string sourcePath = "YOUR_DIRECTORY/Source.xlsx";
string destinationPath = "YOUR_DIRECTORY/Destination.xlsx";

// Load the workbook – this is the starting point for how to copy worksheet
Workbook workbook = new Workbook(sourcePath);
```

*Why this matters:* Загрузка файла создаёт в‑памяти представление каждого листа, ячейки и объекта. Без этого нечего копировать, и любая попытка выполнить `add new worksheet code` позже завершится неудачей, поскольку исходные данные отсутствуют.

## Шаг 2 – Добавление нового листа (add new worksheet code)

Теперь нам нужно место для вставки скопированных данных. Здесь проявляется сила **add new worksheet code**. Вы можете назвать лист как угодно; в данном примере мы назвали его `"Copy"`.

```csharp
// Grab the first worksheet (the one we want to copy)
Worksheet sourceSheet = workbook.Worksheets[0];

// Add a fresh worksheet to receive the copy
Worksheet copySheet = workbook.Worksheets.Add("Copy");
```

*Pro tip:* Если вы планируете копировать несколько листов, вызывайте `Worksheets.Add` внутри цикла и присваивайте каждому листу уникальное имя. Так вы избежите конфликтов имён и поддержите порядок в книге.

## Шаг 3 – Определение диапазона копируемых ячеек

**copy cell range** указывает Aspose.Cells точно, какие строки и столбцы дублировать. Во многих реальных сценариях диапазон включает сводную таблицу, поэтому необходимо быть точным.

```csharp
// Define the area that contains the pivot table (A1:G20)
CellArea sourceRange = new CellArea
{
    StartRow = 0,      // Row 1 (zero‑based)
    StartColumn = 0,   // Column A
    EndRow = 19,       // Row 20
    EndColumn = 6      // Column G
};

// Destination range – we start at the same top‑left corner
CellArea destinationRange = new CellArea
{
    StartRow = 0,
    StartColumn = 0,
    EndRow = 19,
    EndColumn = 6
};
```

*Why we need this:* Явно указывая диапазон, вы избегаете копирования всего листа (что может быть неэкономично) и гарантируете, что сводная таблица находится внутри копируемой области. Это суть **how to copy worksheet**, когда нужен только часть листа.

## Шаг 4 – Настройка параметров копирования (preserve copy worksheet pivot table)

Aspose.Cells предоставляет объект `CopyOptions`, который управляет тем, что будет вставлено. Чтобы сохранить сводную таблицу, диаграммы и формулы, мы устанавливаем `PasteType.All` и включаем `PasteSpecial`.

```csharp
CopyOptions copyOptions = new CopyOptions
{
    PasteType = PasteType.All,   // Copy everything: values, formats, objects
    PasteSpecial = true          // Enable special paste to retain pivot tables
};
```

*Explanation:* `PasteType.All` — самый всеобъемлющий вариант, а `PasteSpecial` указывает движку правильно обрабатывать сложные объекты, такие как сводные таблицы. Пропуск этого шага — распространённая ошибка; скопированный лист потеряет интерактивные функции.

## Шаг 5 – Копирование строк и столбцов (copy columns between sheets)

Теперь начинается самая сложная часть: фактическое перемещение данных. Мы будем использовать `CopyRows` и `CopyColumns` для обработки **copy columns between sheets**. Выполнение обоих действий гарантирует сохранение объединённых ячеек и ширины столбцов.

```csharp
// Copy rows from the source to the destination sheet
sourceSheet.Cells.CopyRows(
    sourceRange.StartRow,
    sourceRange.EndRow,
    copySheet.Cells,
    destinationRange.StartRow,
    copyOptions);

// Copy columns from the source to the destination sheet
sourceSheet.Cells.CopyColumns(
    sourceRange.StartColumn,
    sourceRange.EndColumn,
    copySheet.Cells,
    destinationRange.StartColumn,
    copyOptions);
```

*What’s happening:* `CopyRows` перемещает данные построчно, а `CopyColumns` — постолбцово. Выполнение обоих гарантирует дублирование всего прямоугольного блока, что необходимо, когда нужно **copy columns between sheets** с разной шириной столбцов или скрытыми столбцами.

## Шаг 6 – Сохранение книги

Наконец, запишите изменения обратно на диск. Этот шаг завершает процесс **how to copy worksheet**.

```csharp
// Save the workbook with the newly copied sheet
workbook.Save(destinationPath);
```

*Verification tip:* Откройте `Destination.xlsx` и проверьте, что лист `"Copy"` выглядит идентично оригиналу, сводные таблицы работают, а ширина столбцов совпадает. Если что‑то выглядит неправильно, пересмотрите настройки `CopyOptions`.

## Особые случаи и распространённые варианты

### Копирование нескольких листов

Если нужно дублировать несколько листов, оберните вышеописанную логику в цикл `foreach`:

```csharp
foreach (Worksheet ws in workbook.Worksheets)
{
    Worksheet newWs = workbook.Worksheets.Add(ws.Name + "_Copy");
    // Re‑use sourceRange/destinationRange or calculate per sheet
    // Then call CopyRows/CopyColumns as shown earlier
}
```

### Сохранение формул между разными книгами

Если у исходной и целевой книг разные именованные диапазоны, установите `copyOptions` в `PasteType.Formulas` в дополнение к `All`:

```csharp
copyOptions.PasteType = PasteType.All | PasteType.Formulas;
```

### Большие диапазоны и производительность

Для огромных наборов данных (сотни тысяч строк) рассмотрите возможность использовать только `CopyRows` и пропустить `CopyColumns`, если ширина столбцов не критична. Это может сэкономить несколько секунд.

## Полный рабочий пример

Ниже приведена полная, готовая к запуску программа, воплощающая всё, о чём мы говорили. Вставьте её в консольное приложение, скорректируйте пути к файлам и нажмите **F5**.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // ---------- Step 1: Load the source workbook ----------
        string sourcePath = "YOUR_DIRECTORY/Source.xlsx";
        string destinationPath = "YOUR_DIRECTORY/Destination.xlsx";
        Workbook workbook = new Workbook(sourcePath);

        // ---------- Step 2: Add a new worksheet (add new worksheet code) ----------
        Worksheet sourceSheet = workbook.Worksheets[0];
        Worksheet copySheet = workbook.Worksheets.Add("Copy");

        // ---------- Step 3: Define the copy cell range ----------
        CellArea sourceRange = new CellArea
        {
            StartRow = 0,
            StartColumn = 0,
            EndRow = 19,
            EndColumn = 6
        };
        CellArea destinationRange = new CellArea
        {
            StartRow = 0,
            StartColumn = 0,
            EndRow = 19,
            EndColumn = 6
        };

        // ---------- Step 4: Set copy options (preserve copy worksheet pivot table) ----------
        CopyOptions copyOptions = new CopyOptions
        {
            PasteType = PasteType.All,
            PasteSpecial = true
        };

        // ---------- Step 5: Copy rows and columns (copy columns between sheets) ----------
        sourceSheet.Cells.CopyRows(
            sourceRange.StartRow,
            sourceRange.EndRow,
            copySheet.Cells,
            destinationRange.StartRow,
            copyOptions);

        sourceSheet.Cells.CopyColumns(
            sourceRange.StartColumn,
            sourceRange.EndColumn,
            copySheet.Cells,
            destinationRange.StartColumn,
            copyOptions);

        // ---------- Step 6: Save the workbook ----------
        workbook.Save(destinationPath);
    }
}
```

**Expected result:** При открытии `Destination.xlsx` отображается лист с именем **Copy**, который полностью копирует первый лист `Source.xlsx` — включая любые сводные таблицы, форматирование и ширину столбцов. Исходный файл остаётся нетронутым.

## Часто задаваемые вопросы

**В:** Работает ли это с файлами .xlsx, созданными в Excel 2019?  
**О:** Абсолютно. Aspose.Cells поддерживает все современные форматы Excel, поэтому тот же код работает с `.xlsx`, `.xlsm` и даже более старыми файлами `.xls`.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}