---
category: general
date: 2026-11-19
description: Как дублировать лист при заполнении Excel массивными данными. Узнайте,
  как создать несколько листов и заполнить лист из списка за несколько шагов.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to repeat worksheet
- populate excel with array
- generate multiple worksheets
- populate worksheet from list
language: ru
lastmod: 2026-11-19
og_description: Как повторять лист с помощью SmartMarkerProcessor. Следуйте этому
  руководству, чтобы заполнить Excel данными из массива, создать несколько листов
  и заполнить лист из списка.
og_image_alt: Screenshot showing repeated worksheets in an Excel workbook after processing
og_title: Как повторить лист в Excel — пошаговое руководство
schemas:
- author: GroupDocs
  dateModified: '2026-11-19'
  description: How to repeat worksheet while populating Excel with array data. Learn
    to generate multiple worksheets and populate worksheet from list in a few steps.
  headline: How to repeat worksheet in Excel with SmartMarkerProcessor
  type: TechArticle
- description: How to repeat worksheet while populating Excel with array data. Learn
    to generate multiple worksheets and populate worksheet from list in a few steps.
  name: How to repeat worksheet in Excel with SmartMarkerProcessor
  steps:
  - name: Expected output
    text: 'When you open the resulting workbook, you should see:'
  - name: Empty or null arrays
    text: 'If `Dept` is null or empty, the processor will not create any additional
      worksheets. To avoid a completely blank workbook, you can add a guard:'
  - name: Custom worksheet names
    text: 'The default naming scheme may not suit every reporting requirement. After
      processing, rename each sheet using a loop:'
  - name: Populating additional columns
    text: 'If you need to **populate excel with array** values beyond a single marker,
      extend the data object:'
  type: HowTo
tags:
- Excel automation
- SmartMarkerProcessor
- .NET
title: Как повторить лист в Excel с помощью SmartMarkerProcessor
url: /ru/net/smart-markers-dynamic-data/how-to-repeat-worksheet-in-excel-with-smartmarkerprocessor/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как повторить лист в Excel с помощью SmartMarkerProcessor

Если вам нужно **как повторить лист** при генерации отчетов Excel, это руководство покажет полное, готовое к запуску решение. К концу урока вы сможете **заполнять Excel массивом** данных, **генерировать несколько листов** и **заполнять лист из списка** с использованием библиотеки SmartMarkerProcessor.

Повтор листа — распространённое требование, когда каждому отделу, региону или периоду нужен свой вкладка. Пример ниже демонстрирует точные шаги, объясняет, почему каждое настройка важна, и охватывает граничные случаи, такие как пустые списки или пользовательские имена.

## Требования

Прежде чем начать, убедитесь, что у вас есть:

- .NET 6.0 или новее
- Ссылка на пакет NuGet **GroupDocs.Viewer** (или аналогичный), содержащий `SmartMarkerProcessor`
- Шаблон рабочей книги Excel (`.xlsx`) с маркером вроде `${repeat:Dept}`, размещённым в строке, которую нужно повторять
- Базовое знакомство с C# и LINQ (необязательно, но полезно)

Дополнительные сторонние библиотеки не требуются.

## Шаг 1: Создать экземпляр SmartMarkerProcessor

Процессор управляет заменой маркеров и дублированием листов. Создание его без аргументов использует параметры по умолчанию.

```csharp
// Step 1: Create a SmartMarkerProcessor instance
SmartMarkerProcessor processor = new SmartMarkerProcessor();
```

Создание процессора заранее позволяет настроить глобальные параметры до применения каких‑либо данных. Это фундамент для **как повторить лист** корректно.

## Шаг 2: Включить повтор листов

По умолчанию процессор заменяет маркеры только на текущем листе. Установка `RepeatWorksheet` в `true` сообщает движку клонировать весь лист для каждого элемента в коллекции данных.

```csharp
// Step 2: Enable worksheet repetition for the ${repeat:Dept} marker
processor.Options.RepeatWorksheet = true;
```

Включение этой опции — ключ к **генерации нескольких листов**: процессор создаст новую вкладку для каждого элемента массива `Dept` и сохранит оригинальное форматирование.

## Шаг 3: Подготовить источник данных как массив или список

SmartMarkerProcessor работает с любой перечисляемой коллекцией, но использование массива делает намерение ясным, когда нужно **заполнять лист из списка**. Здесь мы создаём анонимный объект, содержащий свойство `Dept` с массивом строк.

```csharp
// Step 3: Prepare the data source with a list of departments
var data = new { Dept = new[] { "HR", "IT", "Finance" } };
```

Если у вас уже есть `List<string>`, её можно передать напрямую; процессор обработает её так же. Важно, чтобы имя свойства (`Dept`) совпадало с маркером `${repeat:Dept}` в шаблоне.

## Шаг 4: Загрузить шаблон листа

Предположим, у вас есть `ExcelPackage` (из EPPlus) или объект `Workbook`; получите лист, который нужно повторить. Переменная `ws` представляет этот лист.

```csharp
// Example using EPPlus to load the template workbook
using var package = new OfficeOpenXml.ExcelPackage(new FileInfo("Template.xlsx"));
var ws = package.Workbook.Worksheets[0]; // first worksheet
```

Если вы предпочитаете другую библиотеку (например, ClosedXML), тот же принцип применим: получите объект листа, реализующий требуемый интерфейс.

## Шаг 5: Обработать лист с данными

Теперь применяем данные к шаблону. Процессор клонирует лист для каждого отдела, заменяет маркер `${repeat:Dept}` реальным названием отдела и оставляет остальную часть листа без изменений.

```csharp
// Step 5: Apply the data to the template worksheet (ws)
processor.Process(ws, data);
```

После завершения `Process` переменная `ws` становится первым из нескольких листов — по одному на каждый отдел. Оригинальное имя листа сохраняется, а дубликаты получают суффиксы с увеличением (например, “Sheet1 (1)”, “Sheet1 (2)”). При необходимости их можно переименовать позже.

### Ожидаемый результат

При открытии полученной книги вы увидите:

- **Sheet1** – оригинальный шаблон (обычно пустой или используемый как мастер)
- **Sheet1 (1)** – заполнен “HR”
- **Sheet1 (2)** – заполнен “IT”
- **Sheet1 (3)** – заполнен “Finance”

Каждый лист содержит одинаковую раскладку, но с подставленным названием отдела вместо `${repeat:Dept}`.

## Обработка граничных случаев

### Пустые или null массивы

Если `Dept` равно null или пусто, процессор не создаст дополнительных листов. Чтобы избежать полностью пустой книги, можно добавить проверку:

```csharp
if (data.Dept != null && data.Dept.Any())
{
    processor.Process(ws, data);
}
else
{
    // Optionally write a warning or keep the original sheet unchanged
}
```

### Пользовательские имена листов

Схема именования по умолчанию может не подходить всем требованиям отчётности. После обработки переименуйте каждый лист в цикле:

```csharp
for (int i = 1; i <= data.Dept.Length; i++)
{
    var sheet = package.Workbook.Worksheets[i]; // index 0 is the original
    sheet.Name = data.Dept[i - 1]; // use department name as tab title
}
```

### Заполнение дополнительных столбцов

Если нужно **заполнять Excel массивом** значений более одного маркера, расширьте объект данных:

```csharp
var data = new
{
    Dept = new[]
    {
        new { Name = "HR", Headcount = 12 },
        new { Name = "IT", Headcount = 25 },
        new { Name = "Finance", Headcount = 8 }
    }
};
```

Затем скорректируйте маркеры в шаблоне на `${repeat:Dept.Name}` и `${repeat:Dept.Headcount}`. Процессор повторит строку для каждого отдела и заполнит оба столбца.

## Полный рабочий пример

Ниже представлено автономное консольное приложение, демонстрирующее весь процесс от загрузки шаблона до сохранения финальной книги.

```csharp
using System;
using System.IO;
using OfficeOpenXml;               // Install-Package EPPlus
using GroupDocs.Viewer.Markup;    // SmartMarkerProcessor namespace

class Program
{
    static void Main()
    {
        // 1️⃣ Create processor
        SmartMarkerProcessor processor = new SmartMarkerProcessor();

        // 2️⃣ Enable worksheet repetition
        processor.Options.RepeatWorksheet = true;

        // 3️⃣ Define data source (array of departments)
        var data = new { Dept = new[] { "HR", "IT", "Finance" } };

        // 4️⃣ Load template workbook (ensure Template.xlsx exists)
        var fileInfo = new FileInfo("Template.xlsx");
        using var package = new ExcelPackage(fileInfo);
        var ws = package.Workbook.Worksheets[0]; // first sheet contains ${repeat:Dept}

        // 5️⃣ Process template
        processor.Process(ws, data);

        // Optional: rename generated sheets
        for (int i = 1; i <= data.Dept.Length; i++)
        {
            var sheet = package.Workbook.Worksheets[i];
            sheet.Name = data.Dept[i - 1];
        }

        // Save the result
        var output = new FileInfo("Result.xlsx");
        package.SaveAs(output);

        Console.WriteLine("Workbook generated with repeated worksheets.");
    }
}
```

**Пояснение ключевых разделов**

- **Создание процессора** – задаёт движок, который будет интерпретировать маркеры.
- **Опция RepeatWorksheet** – активирует основную функцию, отвечающую на вопрос *как повторить лист*.
- **Источник данных** – использует массив (`new[]`) для выполнения **заполнения Excel массивом**.
- **Загрузка шаблона** – демонстрирует распространённый способ получения объекта листа.
- **Обработка** – выполняет дублирование и вставку данных одним вызовом.
- **Переименование** – показывает, как превратить общие имена “(1)”, “(2)” в осмысленные заголовки, типичную задачу после **генерации нескольких листов**.

Запуск этой программы создаёт `Result.xlsx` с тремя вкладками, специфичными для отделов, каждая из которых заполнена из массива.

## Распространённые ошибки и профессиональные советы

- **Правописание маркера** – маркер должен точно соответствовать имени свойства (`${repeat:Dept}`). Ошибка в написании препятствует повторению.
- **Индекс листа** – после обработки оригинальный лист остаётся на индексе 0; сгенерированные листы идут последовательно. Неправильный индекс может привести к переименованию неверной вкладки.
- **Большие наборы данных** – генерация сотен листов может значительно увеличить размер файла. Рассмотрите возможность разбивки отчётов или использования одного листа с группированными секциями, если возникнут проблемы с производительностью.
- **Потокобезопасность** – `SmartMarkerProcessor` не является потокобезопасным. Создавайте отдельный экземпляр на каждый поток, если обрабатываете несколько книг параллельно.

## Заключение

Теперь вы знаете **как повторить лист** в Excel с помощью SmartMarkerProcessor, как **заполнять Excel массивом** данных, как **генерировать несколько листов** и как **заполнять лист из списка** эффективно. Полный пример объединяет все концепции, а дополнительный шаг переименования позволяет получить чистые, удобные для пользователя имена вкладок.

Далее вы можете изучить:

- Использование **заполнения листа из списка** с комплексными объектами (вложенные коллекции)
- Применение условного форматирования после дублирования листов
- Экспорт сгенерированной книги в PDF или CSV для дальнейшего использования

Не стесняйтесь адаптировать код под свои сценарии отчётности и наслаждайтесь автоматизацией Excel‑книг с уверенностью!

## Что стоит изучить дальше?

Следующие руководства охватывают тесно связанные темы, расширяющие техники, продемонстрированные в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, помогающими освоить дополнительные возможности API и исследовать альтернативные подходы в ваших проектах.

- [Как повторять листы — Полное руководство по автоматизации Excel](/cells/english/net/smart-markers-dynamic-data/how-to-repeat-worksheets-complete-guide-for-excel-automation/)
- [Создание листа для каждого элемента — Как повторить лист в C#](/cells/english/net/worksheet-operations/create-worksheet-per-item-how-to-repeat-worksheet-in-c/)
- [Как расширить массив в Excel и заполнить шаблон](/cells/english/net/templates-reporting/how-to-expand-array-in-excel-and-populate-a-template/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}