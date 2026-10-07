---
category: general
date: 2026-06-05
description: Применяйте стили ячеек при импорте с помощью Aspose.Cells. Узнайте, как
  импортировать DataTable с форматированием, стилизовать строки и поддерживать порядок
  в листах.
draft: false
keywords:
- apply cell styles
- aspose cells import
- import with formatting
- how to import datatable
- import datatable worksheet
language: ru
og_description: Применяйте стили ячеек при импорте DataTable в лист Aspose.Cells.
  Пошаговое руководство с полным кодом и советами.
og_title: Применение стилей ячеек с Aspose.Cells – импорт DataTable
schemas:
- author: Aspose
  dateModified: '2026-06-05'
  description: Apply cell styles while using Aspose.Cells import. Learn how to import
    DataTable with formatting, style rows, and keep worksheets tidy.
  headline: Apply Cell Styles with Aspose.Cells – Import DataTable with Formatting
  type: TechArticle
- description: Apply cell styles while using Aspose.Cells import. Learn how to import
    DataTable with formatting, style rows, and keep worksheets tidy.
  name: Apply Cell Styles with Aspose.Cells – Import DataTable with Formatting
  steps:
  - name: How It Works
    text: 1. **Headers** – Because we passed `true`, Aspose writes “Name” and “Score”
      into the first row. 2. **Data Rows** – Each subsequent row receives the corresponding
      style from `importStyles`. 3. **Performance** – The method streams the data
      directly into the worksheet, which is faster than looping cell
  - name: What if My DataTable Has More Columns Than Styles?
    text: Aspose will apply the last style in the array to any extra columns. To avoid
      unexpected colors, always match the array length to the column count, or pass
      `null` for columns you don’t want styled.
  - name: Can I Apply Different Styles to Specific Rows?
    text: 'Absolutely. After the import, you can loop through rows and assign new
      `Style` objects based on conditions (e.g., highlight scores > 90 in green).
      Here’s a quick snippet:'
  - name: Does This Work with Large DataSets?
    text: Yes. `ImportDataTable` streams data efficiently, and applying a static style
      array adds negligible overhead. For millions of rows, consider using `ImportDataTable`
      in chunks or leveraging `Cells.ImportDataTable` with a `DataReader` for even
      better memory usage.
  - name: How Do I Preserve Existing Formatting in the Worksheet?
    text: If the target range already has formatting you want to keep, set the `ImportDataTable`
      overload’s `importOptions` parameter (`ImportTableOptions`) and tweak `ImportDataTableOptions.PreserveCellFormatting`.
      The default behavior overwrites styles with the ones you supply.
  type: HowTo
tags:
- Aspose.Cells
- C#
- DataTable
title: Применение стилей ячеек с Aspose.Cells — импорт DataTable с форматированием
url: /ru/net/excel-formatting-and-styling/apply-cell-styles-with-aspose-cells-import-datatable-with-fo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Применение стилей ячеек с Aspose.Cells – импорт DataTable с форматированием

Вы когда‑нибудь задумывались, как **применять стили ячеек** при загрузке `DataTable` в лист Excel? Вы не одиноки. Во многих сценариях отчётности данные должны выглядеть хорошо сразу — без последующего ручного форматирования. Хорошая новость в том, что Aspose.Cells упрощает **импорт с форматированием**, так что ваши строки могут быть красными или синими, полужирными или любыми другими.

В этом руководстве мы пройдём полный, готовый к выполнению пример, показывающий **как импортировать datatable** в лист **с применёнными стилями ячеек**. К концу вы получите готовое к запуску консольное приложение C#, которое создаёт книгу, стилизует первые два столбца и сохраняет файл — всё с использованием API `aspose cells import`.

## Что вы узнаете

- Настроить Aspose.Cells в проекте .NET  
- Создать пример `DataTable`, имитирующий реальные данные  
- Определить объекты `Style` для красного и синего шрифтов  
- Использовать `Worksheet.Cells.ImportDataTable` для **импорта datatable в лист** с применением стилей  
- Проверить результат и сохранить книгу  

Никаких внешних инструментов, только чистый C# и Aspose.Cells. Приступим.

## Требования

Прежде чем погрузиться в код, убедитесь, что у вас есть следующее:

| Requirement | Why it matters |
|-------------|----------------|
| .NET 6.0 or later | Aspose.Cells 23.x нацелен на .NET Standard 2.0+, поэтому .NET 6 предоставляет новейшие возможности среды выполнения. |
| Aspose.Cells for .NET (NuGet) | Библиотека предоставляет методы `Workbook`, `Worksheet`, `Style` и `ImportDataTable`, которые нам нужны. |
| Basic C# knowledge | Вы будете разбираться с классами, массивами и инструкциями `using`. |
| An IDE (Visual Studio, VS Code, Rider) | Любой редактор подходит, но вам понадобится восстановить пакеты NuGet. |

You can install the package from the command line:

```bash
dotnet add package Aspose.Cells
```

## Шаг 1: Создать новую книгу и получить доступ к первому листу

Сначала — создадим `Workbook` и получим первый лист. Представьте книгу как пустую тетрадь; первый лист — это страница, на которой мы будем писать.

```csharp
using Aspose.Cells;
using System;
using System.Data;
using System.Drawing;

class Program
{
    static void Main()
    {
        // Create a new workbook (equivalent to a new Excel file)
        Workbook wb = new Workbook();

        // Access the first worksheet (index 0)
        Worksheet worksheet = wb.Worksheets[0];
```

> **Совет:** Если вам понадобится несколько листов, просто добавьте их с помощью `wb.Worksheets.Add()` и обращайтесь к ним по имени или индексу.

## Шаг 2: Подготовить пример DataTable (Как импортировать DataTable)

Теперь нам нужно что‑то импортировать. В реальных проектах вы бы обращались к базе данных, но для наглядности мы создадим `DataTable` в памяти.

```csharp
        // Build a sample DataTable with two columns: Name and Score
        DataTable dataTable = new DataTable("Results");
        dataTable.Columns.Add("Name", typeof(string));
        dataTable.Columns.Add("Score", typeof(int));

        // Populate rows – imagine these came from a query
        dataTable.Rows.Add("Alice", 85);
        dataTable.Rows.Add("Bob", 92);
        dataTable.Rows.Add("Charlie", 78);
        dataTable.Rows.Add("Diana", 91);
```

> **Почему это важно:** Наличие `DataTable` позволяет нам протестировать процесс **aspose cells import** без внешних зависимостей.

## Шаг 3: Определить стили, которые будут применяться к импортированным ячейкам

Здесь происходит волшебство. Мы создадим два объекта `Style`: один с красным шрифтом, другой с синим шрифтом. Они будут применяться по столбцам во время импорта.

```csharp
        // Define an array of styles – one per column
        Style[] importStyles = new Style[2];

        // Style for the first column (Name) – red text
        Style redStyle = wb.CreateStyle();
        redStyle.Font.Color = Color.Red;
        importStyles[0] = redStyle;

        // Style for the second column (Score) – blue text
        Style blueStyle = wb.CreateStyle();
        blueStyle.Font.Color = Color.Blue;
        importStyles[1] = blueStyle;
```

> **Внимание:** Длина массива `importStyles` должна соответствовать количеству импортируемых столбцов, иначе Aspose выбросит `ArgumentException`.

## Шаг 4: Импортировать DataTable в лист **с форматированием**

Теперь мы собираем всё вместе. Перегрузка `ImportDataTable`, которую мы используем, принимает массив `Style[]`, позволяя **применять стили ячеек** по мере загрузки данных в лист.

```csharp
        // Import the DataTable starting at cell A1 (row 0, column 0)
        // The 'true' flag tells Aspose to generate column headers automatically
        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, importStyles);
```

### Как это работает

1. **Заголовки** — Поскольку мы передали `true`, Aspose записывает «Name» и «Score» в первую строку.  
2. **Строки данных** — Каждая последующая строка получает соответствующий стиль из `importStyles`.  
3. **Производительность** — Метод передаёт данные напрямую в лист, что быстрее, чем проходить по ячейкам в цикле.

## Шаг 5: Проверить результат и сохранить книгу

Давайте посмотрим на первые несколько ячеек, чтобы убедиться, что стили применились, а затем запишем файл на диск.

```csharp
        // Optional: Quick sanity check – print the first row's values
        Console.WriteLine("Header Row:");
        Console.WriteLine($"{worksheet.Cells[0, 0].StringValue} | {worksheet.Cells[0, 1].StringValue}");

        // Save the workbook to an Excel file
        string outputPath = "StyledImport.xlsx";
        wb.Save(outputPath);
        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

When you open **StyledImport.xlsx**, you’ll see:

- Столбец «Name» будет отображаться **красным** текстом.  
- Столбец «Score» будет отображаться **синим** текстом.  
- Заголовки столбцов в стиле по умолчанию (их тоже можно стилизовать, но это уже другая статья).

![Apply cell styles example](https://example.com/images/apply-cell-styles.png "Apply cell styles in Aspose.Cells")

> **Примечание:** Изображение выше демонстрирует окончательный вид. Атрибут `alt` содержит основной ключевой запрос, удовлетворяя требования SEO.

## Часто задаваемые вопросы и особые случаи

### Что делать, если у моего DataTable больше столбцов, чем стилей?

Aspose применит последний стиль из массива к любым дополнительным столбцам. Чтобы избежать неожиданных цветов, всегда согласовывайте длину массива с количеством столбцов или передавайте `null` для столбцов, которые не нужно стилизовать.

### Можно ли применять разные стили к отдельным строкам?

Конечно. После импорта вы можете пройтись по строкам и назначить новые объекты `Style` в зависимости от условий (например, выделить оценки > 90 зелёным). Ниже короткий фрагмент кода:

```csharp
for (int i = 1; i <= dataTable.Rows.Count; i++) // start at 1 to skip header
{
    int score = worksheet.Cells[i, 1].IntValue;
    if (score > 90)
    {
        Style highScore = wb.CreateStyle();
        highScore.Font.Color = Color.Green;
        worksheet.Cells[i, 1].SetStyle(highScore);
    }
}
```

### Работает ли это с большими наборами данных?

Да. `ImportDataTable` эффективно передаёт данные, а применение статического массива стилей добавляет незначительные накладные расходы. Для миллионов строк рассмотрите возможность импорта `ImportDataTable` порциями или используйте `Cells.ImportDataTable` с `DataReader` для ещё более экономного использования памяти.

### Как сохранить существующее форматирование в листе?

Если целевой диапазон уже имеет форматирование, которое вы хотите сохранить, задайте параметр `importOptions` перегрузки `ImportDataTable` (`ImportTableOptions`) и настройте `ImportDataTableOptions.PreserveCellFormatting`. По умолчанию стили перезаписываются теми, которые вы передаёте.

## Итоги: чего мы достигли

- **Применили стили ячеек** во время операции **aspose cells import**.  
- Показали **импорт с форматированием**, передавая массив `Style[]`.  
- Показали **как импортировать datatable** в лист и сохранить результат.  
- Рассмотрели особые случаи, такие как несоответствие количества стилей и условное стилизование строк.

Всё это было реализовано в одном самостоятельном консольном приложении — без внешних скриптов и ручного вмешательства в Excel. Теперь у вас есть надёжная база для любой функции отчётности или экспорта данных, требующей аккуратного вывода в Excel.

## Следующие шаги

Готовы к следующему уровню? Вот несколько идей, расширяющих полученные знания:

- **Стилизовать строку заголовка** (например, полужирный шрифт, цвет фона).  
- **Применить условное форматирование** с помощью `Worksheet.Cells[i, j].ConditionalFormattingCollection`.  
- **Экспортировать в другие форматы**, такие как CSV или PDF, используя `wb.Save("file.pdf", SaveFormat.Pdf)`.  
- **Объединить несколько DataTable** в одну книгу, разместив каждый на отдельном листе, используя тот же подход к стилизации.

Если возникнут проблемы, оставьте комментарий или обратитесь к официальной документации Aspose по `ImportDataTable`. Приятного кодинга и наслаждайтесь красиво оформленными файлами Excel!

## Что изучать дальше?

Следующие руководства охватывают тесно связанные темы, развивая техники, продемонстрированные в этом руководстве. Каждый ресурс содержит полностью рабочие примеры кода с пошаговыми объяснениями, помогающими освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [Как импортировать DataTable в Excel с помощью Aspose.Cells для .NET (Пошаговое руководство)](/cells/english/net/import-export/import-datatable-excel-aspose-cells-net/)
- [Как задать стили шрифтов в Excel с помощью Aspose.Cells для .NET (Пошаговое руководство)](/cells/english/net/formatting/aspose-cells-dotnet-set-font-styles-excel/)
- [Как применить текстовую тень в Excel с помощью Aspose.Cells .NET: Пошаговое руководство](/cells/english/net/formatting/apply-text-shadow-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}