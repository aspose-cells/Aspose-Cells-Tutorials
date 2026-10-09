---
category: general
date: 2026-06-08
description: Как связывать листы в Excel с помощью SmartMarkerProcessor для мастер‑детальных
  отчетов. Заполните основной лист и легко создайте мастер‑детальный отчет в Excel.
draft: false
keywords:
- how to link sheets
- populate master sheet
- create master detail excel
- generate master detail report
language: ru
og_description: Как связать листы в Excel с помощью SmartMarkerProcessor. Узнайте,
  как заполнить основной лист и создать отчет мастер‑деталь за несколько минут.
og_title: Как связать листы в Excel с помощью SmartMarker – пошагово
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: How to link sheets in Excel using SmartMarkerProcessor for master‑detail
    reports. Populate master sheet and generate a master detail Excel report effortlessly.
  headline: How to Link Sheets in Excel with SmartMarker – Step‑by‑Step Guide
  type: TechArticle
- description: How to link sheets in Excel using SmartMarkerProcessor for master‑detail
    reports. Populate master sheet and generate a master detail Excel report effortlessly.
  name: How to Link Sheets in Excel with SmartMarker – Step‑by‑Step Guide
  steps:
  - name: Multiple Detail Rows per Master
    text: If a master row has several related details, SmartMarker repeats the master
      row once and then writes *all* matching detail rows beneath it. No extra code
      is needed—just ensure your `Details` collection contains every row.
  - name: Missing Details
    text: When a master entry has no matching detail rows, the detail sheet simply
      skips that section. If you need a placeholder (e.g., “No items”), you can add
      a calculated column in the template that uses an Excel formula like `=IF(COUNTA(A2:B2)=0,"No
      items","")`.
  - name: Large Datasets
    text: 'Processing tens of thousands of rows can be memory‑intensive. To keep performance
      snappy:'
  - name: Custom Column Mapping
    text: If your property names don’t line up (`MasterKey` vs `Id`), you can use
      the `SmartMarkerProcessor.Map` method to create an alias before processing.
  type: HowTo
tags:
- Excel
- SmartMarker
- C#
- master‑detail
title: Как связать листы в Excel с помощью SmartMarker – пошаговое руководство
url: /ru/net/smart-markers-dynamic-data/how-to-link-sheets-in-excel-with-smartmarker-step-by-step-gu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как связать листы в Excel с помощью SmartMarker – пошаговое руководство

Когда‑то задавались вопросом **как связать листы** в Excel без ручного копирования строк или написания бесконечных VBA‑циклов? Вы не одиноки. Большинство разработчиков сталкиваются с проблемой, когда нужен чистый мастер‑детальный отчет, который остаётся синхронным при изменении данных. Хорошая новость? SmartMarkerProcessor делает всю тяжёлую работу за вас, превращая несколько строк C# в полностью готовый мастер‑детальный workbook.

В этом руководстве мы пройдём точные шаги по **заполнению мастер‑листа**, настройке листа деталей и, наконец, **генерации мастер‑детального отчёта**, который обновляется автоматически. К концу вы получите переиспользуемый шаблон, который можно вставить в любой .NET‑проект.

> **Примечание к требованиям:** Вам нужен GrapeCity Documents for Excel (GcExcel) версии 2024 или новее, среда разработки .NET (Visual Studio 2022 отлично подходит) и базовые знания C#. Дополнительные пакеты NuGet, помимо GcExcel, не требуются.

---

## Обзор решения

Прежде чем погрузиться в код, разберём, что значит «связывать листы» в контексте SmartMarker:

1. **Мастер‑лист** – содержит одну строку на сущность (например, список клиентов).
2. **Лист деталей** – содержит строки, принадлежащие мастер‑строке (например, заказы для каждого клиента).
3. **Синтаксис SmartMarker** – небольшой язык разметки (`{MasterSheet}#master;{DetailSheet}#detail`), который указывает процессору, как привязать две таблицы данных.
4. **Опции процессора** – включение `MasterDetail` заставляет движок автоматически повторять строки мастера и вставлять связанные строки деталей под ними.

Понимание этих компонентов поможет вам позже настроить подход — возможно, вам понадобится трёхуровневая вложенность или условное форматирование. Держите эту ментальную модель под рукой, пока мы проходим реализацию.

---

## Шаг 1: Подготовьте иерархические данные для обработки мастер‑деталь

Первое, что нужно — источник данных, отражающий отношение мастер‑деталь. В большинстве реальных сценариев они берутся из базы данных, но для наглядности мы используем литерал анонимного объекта.

```csharp
// Step 1: Prepare hierarchical data for master‑detail processing
var sampleData = new
{
    // Master collection – one row per category
    Master = new[]
    {
        new { Id = 1, Name = "A" },
        new { Id = 2, Name = "B" }
    },

    // Detail collection – rows reference MasterId
    Details = new[]
    {
        new { MasterId = 1, Item = "Item1" },
        new { MasterId = 2, Item = "Item2" }
    }
};
```

**Почему это важно:** SmartMarker не угадывает отношения; он ищет совпадающие имена свойств (`MasterId` → `Id`). Структурируя данные таким образом, мы даём процессору чёткую карту, что является краеугольным камнем **как связать листы** эффективно.

> **Совет:** Если ваши данные находятся в объектах `DataTable`, просто откройте их как свойства с теми же именами — SmartMarker работает с любой перечисляемой коллекцией.

---

## Шаг 2: Создайте Workbook и загрузите шаблон

SmartMarker работает с существующим Excel‑workbook, обычно шаблоном, который уже содержит имена листов и маркеры‑заполнители. Давайте создадим workbook в памяти и добавим два пустых листа с именами *MasterSheet* и *DetailSheet*.

```csharp
using GrapeCity.Documents.Excel;

// Step 2: Create a workbook and add template sheets
IWorkbook wb = new Workbook();

// Create the master sheet and add a header row
IWorksheet masterSheet = wb.Worksheets.Add("MasterSheet");
masterSheet.Range["A1"].Value = "ID";
masterSheet.Range["B1"].Value = "Name";

// Create the detail sheet and add its header
IWorksheet detailSheet = wb.Worksheets.Add("DetailSheet");
detailSheet.Range["A1"].Value = "Master ID";
detailSheet.Range["B1"].Value = "Item";
```

Вы также можете загрузить файл `.xlsx` с диска (`wb.Open("Template.xlsx")`), если предпочитаете сначала оформить макет в Excel. Главное, чтобы имена листов совпадали с теми, которые вы будете указывать в строке SmartMarker.

---

## Шаг 3: Создайте экземпляр SmartMarkerProcessor и включите режим мастер‑деталь

Теперь подключаем движок, который будет читать маркеры и вставлять данные. `SmartMarkerProcessor` принимает workbook в качестве аргумента конструктора, а флаг `Options.MasterDetail` сообщает ему рассматривать маркеры `#master` и `#detail` как связанную пару.

```csharp
// Step 3: Create a SmartMarkerProcessor for the workbook
SmartMarkerProcessor processor = new SmartMarkerProcessor(wb);

// Enable master‑detail mode on the processor options
processor.Options.MasterDetail = true;
```

**Зачем включать `MasterDetail`?** Без этого флага процессор будет рассматривать `{MasterSheet}#master` и `{DetailSheet}#detail` как независимые операции, теряя важную связь между строками. Установка флага — единственная строка, которая заставляет **как связать листы** действительно работать.

---

## Шаг 4: Определите строку SmartMarker и запустите процессор

Строка маркеров указывает SmartMarker, какой лист является мастером, а какой деталями. Синтаксис прост: `{SheetName}#master;{SheetName}#detail`. Можно добавить дополнительные маркеры (например, `#header`), но они не нужны для базового отчёта.

```csharp
// Step 4: Execute the smart‑marker processing, linking master and detail sheets
string marker = "{MasterSheet}#master;{DetailSheet}#detail";
processor.Process(marker, sampleData);
```

При выполнении `Process` движок:

1. Записывает каждую строку мастера в *MasterSheet*, начиная с первой пустой строки после заголовка.
2. Для каждой строки мастера сканирует коллекцию `Details`, выбирает строки, где `MasterId` совпадает с `Id` мастера, и записывает их в *DetailSheet* непосредственно под соответствующей записью мастера.

---

## Шаг 5: Сохраните или экспортируйте полученный Workbook

На данном этапе у вас полностью заполненный workbook. Вы можете сохранить его на диск, передать в виде потока веб‑клиенту или даже конвертировать в PDF.

```csharp
// Save the workbook to a file (you could also stream it to a response)
wb.Save("MasterDetailReport.xlsx");
```

Откройте файл, и вы увидите два листа: *MasterSheet* перечисляет `A` и `B`, а *DetailSheet* показывает `Item1` под мастером `1` и `Item2` под мастером `2`. Это суть **заполнения мастер‑листа** и **генерации мастер‑детального отчёта** в один шаг.

---

## Визуальный обзор

![Диаграмма, иллюстрирующая как связать листы в Excel с помощью SmartMarkerProcessor](https://example.com/diagram.png "Диаграмма как связать листы")

Диаграмма (alt‑текст включает основной ключевой запрос) показывает поток данных от объектов C# → SmartMarkerProcessor → связанные листы Excel.

---

## Обработка распространённых граничных случаев

### Несколько строк деталей на один мастер

Если у мастера несколько связанных деталей, SmartMarker повторит строку мастера один раз, а затем запишет *все* подходящие строки деталей под ней. Дополнительный код не требуется — просто убедитесь, что ваша коллекция `Details` содержит все строки.

### Отсутствие деталей

Когда у записи мастера нет соответствующих строк деталей, лист деталей просто пропускает этот раздел. Если нужен заполнитель (например, «Нет элементов»), можно добавить вычисляемый столбец в шаблон, использующий формулу Excel вроде `=IF(COUNTA(A2:B2)=0,"No items","")`.

### Большие наборы данных

Обработка десятков тысяч строк может быть ресурсоёмкой. Чтобы поддерживать высокую производительность:

- Используйте `processor.Options.EnableStreaming = true` (доступно в GcExcel 2025+).
- Разбивайте данные на части и обрабатывайте каждую часть отдельно, затем объединяйте workbooks.

### Пользовательское сопоставление столбцов

Если имена ваших свойств не совпадают (`MasterKey` vs `Id`), вы можете воспользоваться методом `SmartMarkerProcessor.Map`, чтобы создать псевдоним перед обработкой.

```csharp
processor.Map("MasterId", "Id"); // tells the engine that MasterId maps to Id
```

---

## Полный рабочий пример

Объединяя всё вместе, представляем полностью готовую к копированию программу, которую можно сразу запустить.



## Что изучать дальше?

Следующие руководства охватывают тесно связанные темы, расширяющие техники, продемонстрированные в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы в собственных проектах.

- [Master External Link Formulas in Excel Using Aspose.Cells for Java](/cells/english/java/formulas-functions/aspose-cells-java-external-link-formulas-excel/)
- [Master Dynamic Excel Sheets in Java with Aspose.Cells&#58; A Comprehensive Guide](/cells/english/java/formulas-functions/dynamic-excel-sheets-aspose-cells-java-guide/)
- [Master Dynamic Excel Reports Using Aspose.Cells Java&#58; Named Ranges & Complex Formulas](/cells/english/java/templates-reporting/dynamic-excel-reports-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}