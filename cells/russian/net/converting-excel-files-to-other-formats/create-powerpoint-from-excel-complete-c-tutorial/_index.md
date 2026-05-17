---
category: general
date: 2026-02-21
description: Быстро создавайте PowerPoint из Excel. Узнайте, как экспортировать Excel
  в PowerPoint с редактируемым текстом и диаграммами, используя Aspose.Cells, всего
  в несколько строк кода C#.
draft: false
keywords:
- create powerpoint from excel
- export excel to powerpoint
- export editable text
- export excel chart powerpoint
- convert excel chart powerpoint
language: ru
og_description: Создайте презентацию PowerPoint из Excel с редактируемым текстом и
  диаграммами. Следуйте этому подробному руководству, чтобы экспортировать Excel в
  PowerPoint с помощью Aspose.Cells.
og_title: Создание PowerPoint из Excel – пошаговое руководство на C#
tags:
- C#
- Aspose.Cells
- PowerPoint
- Excel Automation
title: Создание PowerPoint из Excel – Полный учебник по C#
url: /ru/net/converting-excel-files-to-other-formats/create-powerpoint-from-excel-complete-c-tutorial/
---

final output with all translations.

Be careful to preserve markdown formatting, code block placeholders unchanged.

Let's craft translation.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание PowerPoint из Excel – Полный учебник C#

Когда‑нибудь вам нужно было **create PowerPoint from Excel**, но вы не знали, какой API использовать? Вы не одиноки. Многие разработчики сталкиваются с проблемой, когда хотят превратить насыщенный данными лист в отшлифованную презентацию, особенно если им нужны текстовые поля, остающиеся редактируемыми после конвертации.  

В этом руководстве мы покажем, как **export Excel to PowerPoint**, сохраняя редактируемый текст, точность графиков и макет — всё это с помощью нескольких строк кода C#. К концу вы получите готовый файл PPTX, который можно доработать в PowerPoint так же, как любой вручную созданный слайд.

## Что вы узнаете

- Как загрузить книгу Excel, содержащую графики и фигуры.  
- Как настроить `PresentationExportOptions`, чтобы текстовые поля оставались редактируемыми (`export editable text`).  
- Как действительно **export Excel chart PowerPoint** и получить чистую презентацию.  
- Небольшие вариации, которые можно применить, когда нужно **convert Excel chart PowerPoint** для разных настроек страницы или нескольких листов.  

### Требования

- Среда разработки .NET (Visual Studio 2022 или новее).  
- Aspose.Cells for .NET (бесплатная пробная версия или лицензия).  
- Файл Excel (`ChartWithShape.xlsx`), содержащий как минимум один график и фигуру, которую вы хотите оставить редактируемой.  

Если всё это у вас есть, давайте приступать — без лишних слов, только практическое, готовое к запуску решение.

## Создание PowerPoint из Excel – Пошагово

Ниже под каждым шагом мы разместим короткий фрагмент кода, объясним **почему** мы делаем именно так и укажем типичные подводные камни. Не стесняйтесь скопировать‑вставить полный пример в конце страницы.

### Шаг 1: Загрузка книги Excel

Сначала нужно загрузить исходную книгу в память. Aspose.Cells читает файл и формирует богатую объектную модель, которой мы можем управлять.

```csharp
// Step 1: Load the Excel workbook that contains the chart and shape
Workbook workbook = new Workbook("YOUR_DIRECTORY/ChartWithShape.xlsx");

// Quick sanity check – make sure the workbook actually loaded
if (workbook.Worksheets.Count == 0)
    throw new InvalidOperationException("The workbook appears to be empty.");
```

**Почему это важно:**  
Загрузка книги — фундамент. Если путь к файлу неверен или книга повреждена, все последующие шаги `export excel to powerpoint` завершатся ошибкой. Проверка на этапе загрузки дает раннюю обратную связь вместо неясного «файл не найден» позже.

### Шаг 2: Подготовка параметров экспорта

Aspose.Cells предоставляет объект `PresentationExportOptions`, который управляет внешним видом PPTX. Здесь вы решаете, хотите ли вы, чтобы текст оставался редактируемым.

```csharp
// Step 2: Create export options for PowerPoint conversion
PresentationExportOptions exportOptions = new PresentationExportOptions();

// Optional: tweak the slide size (default is 10in x 7.5in)
exportOptions.SlideSize = new SizeF(10, 7.5f);
```

**Почему это важно:**  
Если не настроить `PresentationExportOptions`, библиотека использует значения по умолчанию, которые могут не соответствовать вашему корпоративному шаблону слайдов. Задав размер слайда заранее, вы избавитесь от необходимости ручного изменения размеров позже.

### Шаг 3: Включение редактируемых текстовых полей

Волшебный флаг `ExportEditableTextBoxes` сообщает Aspose.Cells сохранять любые текстовые фигуры как текстовые поля PowerPoint, а не как статические изображения.

```csharp
// Step 3: Enable editability of text boxes in the resulting presentation
exportOptions.ExportEditableTextBoxes = true;
```

**Почему это важно:**  
Если пропустить эту строку, полученный PPTX будет содержать растровый текст — его нельзя будет отредактировать в PowerPoint. Установка `export editable text` — ключ к действительно переиспользуемой презентации.

### Шаг 4: Экспорт листа в PPTX

Теперь мы действительно записываем файл PPTX. Можно выбрать любой лист; в примере используется первый (`Worksheets[0]`).

```csharp
// Step 4: Export the first worksheet's page setup to a PPTX file
workbook.Worksheets[0].PageSetup.SaveToPptx("YOUR_DIRECTORY/Result.pptx", exportOptions);
```

**Почему это важно:**  
`SaveToPptx` учитывает настройки страницы (поля, ориентацию), заданные в Excel, поэтому слайд точно повторяет ваш макет. Это ядро процесса **export excel chart powerpoint**.

### Шаг 5: Проверка результата (необязательно, но рекомендуется)

После конвертации откройте сгенерированный `Result.pptx` в PowerPoint и проверьте:

1. Графики выглядят чётко и сохраняют серии данных.  
2. Текстовые поля можно выделять и редактировать.  
3. Размер слайда соответствует вашим ожиданиям.

Если что‑то выглядит неправильно, вернитесь к `exportOptions` — например, может потребоваться установить `exportOptions.IncludePrintArea = true`, чтобы учесть именованную область печати.

```csharp
// Optional: open the PPTX automatically (requires System.Diagnostics)
System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo
{
    FileName = "YOUR_DIRECTORY/Result.pptx",
    UseShellExecute = true
});
```

### Шаг 6: Расширенные варианты (экспорт нескольких листов)

Часто требуется **convert excel chart powerpoint** для нескольких листов одновременно. Пройдитесь по коллекции и дайте каждому слайду уникальное имя:

```csharp
for (int i = 0; i < workbook.Worksheets.Count; i++)
{
    string outputPath = $"YOUR_DIRECTORY/Result_Sheet{i + 1}.pptx";
    workbook.Worksheets[i].PageSetup.SaveToPptx(outputPath, exportOptions);
}
```

**Pro tip:** Если вам нужны все листы в *одном* PPTX, создайте новый объект `Presentation`, импортируйте каждый слайд и сохраните один раз. Это немного сложнее, но избавит от необходимости управлять множеством файлов.

## Полный рабочий пример

Вот полностью готовая программа, которую можно вставить в консольное приложение и сразу запустить.

```csharp
using System;
using System.Drawing;
using Aspose.Cells;
using Aspose.Cells.Export;

class Program
{
    static void Main()
    {
        // 1️⃣ Load workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/ChartWithShape.xlsx");
        if (workbook.Worksheets.Count == 0)
        {
            Console.WriteLine("Workbook is empty – aborting.");
            return;
        }

        // 2️⃣ Set up export options
        PresentationExportOptions exportOptions = new PresentationExportOptions
        {
            SlideSize = new SizeF(10, 7.5f),          // optional custom size
            ExportEditableTextBoxes = true           // <‑‑ keep text boxes editable
        };

        // 3️⃣ Export first worksheet
        string outputPath = "YOUR_DIRECTORY/Result.pptx";
        workbook.Worksheets[0].PageSetup.SaveToPptx(outputPath, exportOptions);
        Console.WriteLine($"PowerPoint created at: {outputPath}");

        // 4️⃣ Open the result automatically (Windows only)
        try
        {
            System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo
            {
                FileName = outputPath,
                UseShellExecute = true
            });
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Could not open PPTX automatically: {ex.Message}");
        }
    }
}
```

**Ожидаемый результат:**  
При открытии `Result.pptx` вы увидите слайд, точно повторяющий макет листа Excel. Любой график, размещённый в Excel, будет представлен как нативный график PowerPoint, а подпись, добавленная как фигура, превратится в полностью редактируемое текстовое поле.

## Часто задаваемые вопросы и особые случаи

- **Does this work with macro‑enabled workbooks (`.xlsm`)?**  
  Да. Aspose.Cells читает макросы, но не исполняет их. Процесс конвертации игнорирует VBA, поэтому вы всё равно получите визуальное содержимое.

- **What if my worksheet contains multiple charts?**  
  Все видимые графики переносятся на один слайд. Если нужен отдельный слайд для каждого графика, разбейте лист или используйте цикл, показанный в Шаге 6.

- **Can I preserve custom PowerPoint themes?**  
  Не напрямую во время экспорта. После конвертации вы можете применить тему в PowerPoint или программно через Aspose.Slides.

- **Is there a way to export only a selected range?**  
  Установите именованную область печати в Excel (`Page Layout → Print Area`) и включите `exportOptions.IncludePrintArea = true`.

## Заключение

Теперь вы знаете, как **create PowerPoint from Excel** с помощью Aspose.Cells, полностью контролируя редактируемый текст, точность графиков и размер слайдов. Краткий фрагмент кода, который мы предоставили, покрывает наиболее распространённый сценарий, а дополнительные советы дают гибкость, когда нужно **export excel to powerpoint** для нескольких листов или пользовательских макетов.  

Готовы к следующему вызову? Попробуйте комбинировать этот подход с **Aspose.Slides**, чтобы программно добавлять переходы, заметки докладчика или даже внедрять сгенерированные слайды в более крупную презентацию. Или поэкспериментируйте с конвертацией всей книги в много‑слайдовую презентацию — идеально для автоматизированных конвейеров отчётности.

Есть вопросы или нашли умный трюк? Оставьте комментарий ниже, и счастливого кодинга!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}