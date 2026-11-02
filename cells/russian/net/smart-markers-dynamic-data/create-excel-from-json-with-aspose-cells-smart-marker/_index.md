---
category: general
date: 2026-08-07
description: Создайте Excel из JSON с помощью Aspose.Cells Smart Marker — узнайте,
  как заполнить шаблон Excel, применить динамическое именование листов и создать несколько
  листов.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel from json
- populate excel template
- dynamic sheet naming
- generate multiple worksheets
- aspose.cells smart marker
language: ru
lastmod: 2026-08-07
og_description: Создайте Excel из JSON с помощью Aspose.Cells Smart Marker, быстро
  заполняйте шаблоны, используйте динамическое именование листов и генерируйте несколько
  листов.
og_image_alt: Screenshot of generated Excel workbook with multiple dynamically named
  sheets
og_title: Создание Excel из JSON – руководство по Smart Marker в Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-08-07'
  description: Create Excel from JSON using Aspose.Cells Smart Marker – learn how
    to populate an Excel template, apply dynamic sheet naming, and generate multiple
    worksheets.
  headline: Create Excel from JSON with Aspose.Cells Smart Marker
  type: TechArticle
- description: Create Excel from JSON using Aspose.Cells Smart Marker – learn how
    to populate an Excel template, apply dynamic sheet naming, and generate multiple
    worksheets.
  name: Create Excel from JSON with Aspose.Cells Smart Marker
  steps:
  - name: Define the JSON‑compatible source data
    text: '```csharp // Step 1: Define the source data that will be merged into the
      workbook var ordersData = new { Orders = new[] { new { Id = 1, Items = new[]
      { "Apple", "Banana" } }, new { Id = 2, Items = new[] { "Orange" } } } }; ```'
  - name: Prepare the workbook template and insert a Smart Marker
    text: '```csharp // Step 2: Create a new workbook and place a Smart Marker that
      references the data collection var workbook = new Workbook(); // creates an
      empty workbook workbook.Worksheets[0].Cells["A1"].PutValue("{{Orders}}"); ```'
  - name: Configure dynamic sheet naming
    text: '```csharp // Step 3: Configure how duplicated detail sheets should be named
      during processing var smartMarkerOptions = new SmartMarkerOptions { // {0} will
      be replaced by an incremental index (DetailSheet_1, DetailSheet_2, …) DetailSheetNewName
      = "DetailSheet_{0}" }; ```'
  - name: Process the template with the data and naming options
    text: '```csharp // Step 4: Process the workbook with the data and the naming
      options var smartMarkerProcessor = new SmartMarkerProcessor(workbook, smartMarkerOptions);
      smartMarkerProcessor.Process(ordersData); ```'
  - name: Save the resulting workbook
    text: '```csharp // Step 5: Save the resulting workbook – the detail sheets are
      created automatically workbook.Save("YOUR_DIRECTORY/SmartMarkerDupSheets.xlsx");
      ```'
  - name: Populate Excel template with additional fields
    text: 'If your JSON includes more properties (e.g., `CustomerName`, `TotalAmount`),
      add corresponding markers to the template:'
  - name: Generate multiple worksheets from nested collections
    text: 'You can create a second level of duplication by placing a marker inside
      the detail sheet that references a nested collection, such as `Items`:'
  - name: Custom naming with data from the record
    text: '```csharp var smartMarkerOptions = new SmartMarkerOptions { DetailSheetNewName
      = "Order_{Id}" }; ```'
  - name: Next steps
    text: '* Explore **conditional formatting** inside the detail sheet to highlight
      high‑value orders. * Replace the anonymous object with a strongly typed model
      deserialized via `System.Text.Json`. * Combine Smart Markers with **PivotTable**
      generation for advanced reporting.'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Создать Excel из JSON с помощью Aspose.Cells Smart Marker
url: /ru/net/smart-markers-dynamic-data/create-excel-from-json-with-aspose-cells-smart-marker/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание Excel из JSON с помощью Aspose.Cells Smart Marker

Если вам нужно **создать Excel из JSON**, этот учебник покажет полное, готовое к продакшну решение. Вы увидите, как **заполнить шаблон Excel**, настроить **динамическое именование листов** и **автоматически генерировать несколько листов** с помощью движка **Aspose.Cells Smart Marker**.

Руководство проведёт вас через каждый необходимый шаг, от определения объекта‑источника, похожего на JSON, до сохранения окончательной книги. Внешние скрипты не требуются, код работает на .NET 6 и выше.

## Что вы достигнете

* Загрузите объект данных в стиле JSON в память.  
* Вставьте заполнитель Smart Marker в шаблон книги.  
* Примените шаблон именования, чтобы каждый дублированный лист деталей получил уникальное имя.  
* Обработайте шаблон, создав отдельный лист для каждого заказа в коллекции.  
* Сохраните результат в файл `.xlsx`, готовый к дальнейшему использованию.

Требования: Visual Studio 2022 (или любой IDE для C#), .NET 6+, и пакет **Aspose.Cells** из NuGet. Пример использует C#; те же концепции применимы к VB.NET или другим .NET‑языкам.

## Создание Excel из JSON – общий рабочий процесс

Следующие разделы разбивают процесс на пять логических шагов. Каждый шаг включает точный код, объяснение его важности и советы по масштабированию решения.

### Шаг 1: Определите совместимые с JSON исходные данные

```csharp
// Step 1: Define the source data that will be merged into the workbook
var ordersData = new
{
    Orders = new[]
    {
        new { Id = 1, Items = new[] { "Apple", "Banana" } },
        new { Id = 2, Items = new[] { "Orange" } }
    }
};
```

**Почему это важно** – Объект `ordersData` отражает структуру, которую вы бы получили от реального JSON‑API. Aspose.Cells Smart Marker читает публичные свойства, поэтому анонимный тип работает, пока имена свойств совпадают с тегами маркеров (`{{Orders}}`). Когда вы замените анонимный тип десериализованным объектом JSON, код менять не придётся.

### Шаг 2: Подготовьте шаблон книги и вставьте Smart Marker

```csharp
// Step 2: Create a new workbook and place a Smart Marker that references the data collection
var workbook = new Workbook();                     // creates an empty workbook
workbook.Worksheets[0].Cells["A1"].PutValue("{{Orders}}");
```

**Почему это важно** – Маркер `{{Orders}}` указывает процессору проходить по коллекции `Orders`. Размещение маркера в ячейке `A1` первого листа делает этот лист *главным* листом. Процессор будет клонировать его для каждого заказа, сохраняя любое форматирование, которое вы добавите позже.

> **Подсказка:** Если у вас есть заранее подготовленный шаблон (например, с заголовками, формулами или стилями), загрузите его через `new Workbook("Template.xlsx")` вместо создания пустой книги.

### Шаг 3: Настройте динамическое именование листов

```csharp
// Step 3: Configure how duplicated detail sheets should be named during processing
var smartMarkerOptions = new SmartMarkerOptions
{
    // {0} will be replaced by an incremental index (DetailSheet_1, DetailSheet_2, …)
    DetailSheetNewName = "DetailSheet_{0}"
};
```

**Почему это важно** – По умолчанию Aspose.Cells именует дублированные листы `Sheet1`, `Sheet2` и т.д. Шаблон `DetailSheetNewName` вставляет инкрементный индекс (`{0}`), так что каждый лист получает осмысленное имя. Вы можете добавить дополнительные плейсхолдеры (например, `{Id}`), чтобы включить данные текущей записи.

> **Pro tip:** Используйте `DetailSheetNewName = "Order_{Id}"`, чтобы именовать листы по идентификатору заказа — это упрощает навигацию в больших книгах.

### Шаг 4: Обработайте шаблон с данными и параметрами именования

```csharp
// Step 4: Process the workbook with the data and the naming options
var smartMarkerProcessor = new SmartMarkerProcessor(workbook, smartMarkerOptions);
smartMarkerProcessor.Process(ordersData);
```

**Почему это важно** – `SmartMarkerProcessor` объединяет `ordersData` с книгой, создаёт новый лист для каждого элемента в `Orders` и применяет ранее заданный шаблон именования. Процессор также разворачивает любые вложенные коллекции (например, `Items`), если вы добавите дополнительные маркеры внутри листа деталей.

### Шаг 5: Сохраните полученную книгу

```csharp
// Step 5: Save the resulting workbook – the detail sheets are created automatically
workbook.Save("YOUR_DIRECTORY/SmartMarkerDupSheets.xlsx");
```

**Почему это важно** – Метод `Save` записывает полностью заполненную книгу на диск. Файл теперь содержит главный лист (который можно скрыть или удалить) и серию листов деталей с именами `DetailSheet_1`, `DetailSheet_2`, …, каждый из которых содержит данные одного заказа.

#### Ожидаемый результат

| Имя листа        | Содержание (упрощённо)                     |
|-------------------|------------------------------------------|
| DetailSheet_1     | Order Id = 1, Items: Apple, Banana       |
| DetailSheet_2     | Order Id = 2, Items: Orange              |

Все листы сохраняют любое форматирование, применённое к главному листу до обработки.

## Расширенные варианты

### Заполнение шаблона Excel дополнительными полями

Если ваш JSON содержит больше свойств (например, `CustomerName`, `TotalAmount`), добавьте соответствующие маркеры в шаблон:

```csharp
workbook.Worksheets[0].Cells["B1"].PutValue("{{CustomerName}}");
workbook.Worksheets[0].Cells["C1"].PutValue("{{TotalAmount}}");
```

Процессор заменит каждый маркер на значение соответствующего свойства.

### Генерация нескольких листов из вложенных коллекций

Вы можете создать второй уровень дублирования, разместив маркер внутри листа деталей, ссылающийся на вложенную коллекцию, такую как `Items`:

```csharp
// Inside the detail sheet (e.g., cell A2)
workbook.Worksheets[0].Cells["A2"].PutValue("{{Items}}");

// Inside the same sheet, cell B2 will list each item
workbook.Worksheets[0].Cells["B2"].PutValue("{{Items}}");
```

Во время обработки Aspose.Cells создаст строку для каждого элемента массива `Items`, позволяя формировать детализированные списки по каждому заказу.

### Пользовательское именование с данными из записи

```csharp
var smartMarkerOptions = new SmartMarkerOptions
{
    DetailSheetNewName = "Order_{Id}"
};
```

Теперь листы именуются `Order_1`, `Order_2`, что согласует имя листа с бизнес‑идентификатором.

## Типичные подводные камни и как их избежать

| Проблема                              | Решение |
|--------------------------------------|----------|
| Текст маркера не совпадает с именем свойства (чувствительно к регистру) | Убедитесь, что маркер (`{{Orders}}`) точно соответствует имени свойства, включая регистр. |
| Шаблон содержит объединённые ячейки, охватывающие область маркера | Разъедините ячейки или разместите маркер в одной, не объединённой ячейке, чтобы избежать непредвидённых изменений макета. |
| Большие JSON‑коллекции вызывают нагрузку на память | Обрабатывайте данные партиями или потоково загружайте JSON в `DataTable` и используйте `SmartMarkerProcessor` с `DataSource`. |
| Путь сохранения файла недействителен | Используйте `Path.Combine(Environment.CurrentDirectory, "output.xlsx")` или проверьте права записи. |

## Полный рабочий пример

```csharp
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

class Program
{
    static void Main()
    {
        // 1️⃣ Define JSON‑compatible data
        var ordersData = new
        {
            Orders = new[]
            {
                new { Id = 1, Items = new[] { "Apple", "Banana" } },
                new { Id = 2, Items = new[] { "Orange" } }
            }
        };

        // 2️⃣ Create workbook and add master Smart Marker
        var workbook = new Workbook();
        workbook.Worksheets[0].Cells["A1"].PutValue("{{Orders}}");

        // 3️⃣ Set up dynamic sheet naming
        var smartMarkerOptions = new SmartMarkerOptions
        {
            DetailSheetNewName = "DetailSheet_{0}"
        };

        // 4️⃣ Process template with data
        var processor = new SmartMarkerProcessor(workbook, smartMarkerOptions);
        processor.Process(ordersData);

        // 5️⃣ Save the result
        string outputPath = Path.Combine(
            Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
            "SmartMarkerDupSheets.xlsx");
        workbook.Save(outputPath);
    }
}
```

Запуск программы создаёт файл Excel на рабочем столе, содержащий два листа деталей (`DetailSheet_1` и `DetailSheet_2`). Каждый лист отражает соответствующую запись заказа.

## Заключение

Теперь вы знаете, как **создавать Excel из JSON** с помощью **Aspose.Cells Smart Marker**, как **заполнять шаблон Excel**, применять **динамическое именование листов** и **автоматически генерировать несколько листов**. Та же схема масштабируется до десятков и тысяч записей, поддерживает вложенные коллекции и без проблем интегрируется с любой .NET‑библиотекой десериализации JSON.

### Следующие шаги

* Исследуйте **условное форматирование** внутри листа деталей для выделения заказов с высокой стоимостью.  
* Замените анонимный объект на строго типизированную модель, десериализованную через `System.Text.Json`.  
* Сочетайте Smart Markers с генерацией **PivotTable** для продвинутой отчётности.  

Экспериментируйте с шаблоном именования, добавляйте новые маркеры и интегрируйте этот рабочий процесс в существующие конвейеры экспорта данных. Приятного кодинга!

## Что изучать дальше?

Следующие учебники охватывают тесно связанные темы, расширяющие техники, продемонстрированные в этом руководстве. Каждый ресурс включает полностью рабочие примеры кода с пошаговыми объяснениями, помогая вам освоить дополнительные возможности API и исследовать альтернативные подходы в собственных проектах.

- [Создание динамических Excel‑отчетов с использованием Aspose.Cells .NET Smart Markers](/cells/english/net/templates-reporting/generate-excel-reports-aspose-cells-net-smart-markers/)
- [Заполнение Excel данными с помощью Aspose.Cells и Smart Markers](/cells/english/java/cell-operations/populate-excel-aspose-cells-smart-markers/)
- [Как создать и объединить книги Excel с помощью Aspose.Cells для Java | Полное руководство](/cells/english/java/workbook-operations/create-merge-excel-workbooks-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}