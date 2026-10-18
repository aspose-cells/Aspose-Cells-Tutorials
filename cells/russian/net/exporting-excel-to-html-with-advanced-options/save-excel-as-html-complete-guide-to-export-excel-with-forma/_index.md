---
category: general
date: 2026-07-14
description: Быстро сохраняйте Excel в формате HTML и узнайте, как конвертировать
  Excel в HTML с полным форматированием. Экспортируйте Excel с сохранением форматирования
  с помощью Aspose.Cells за считанные минуты.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save excel as html
- convert excel to html
- export excel with formatting
- Aspose.Cells HTML export
- Grid.js number formatting
language: ru
lastmod: 2026-07-14
og_description: Сохраните Excel в HTML мгновенно. Это руководство показывает, как
  конвертировать Excel в HTML, сохраняя стили и включив форматирование чисел Grid.js.
og_image_alt: Screenshot of a spreadsheet saved as HTML using Aspose.Cells – save
  excel as html example
og_title: Сохранить Excel как HTML – пошаговый экспорт с полным форматированием
schemas:
- author: Aspose
  dateModified: '2026-07-14'
  description: Save Excel as HTML quickly and learn how to convert Excel to HTML with
    full formatting. Export Excel with formatting using Aspose.Cells in minutes.
  headline: Save Excel as HTML – Complete Guide to Export Excel with Formatting
  type: TechArticle
- description: Save Excel as HTML quickly and learn how to convert Excel to HTML with
    full formatting. Export Excel with formatting using Aspose.Cells in minutes.
  name: Save Excel as HTML – Complete Guide to Export Excel with Formatting
  steps:
  - name: '**Styling intact?** Compare cell background colors and borders to the original
      Excel view.'
    text: '**Styling intact?** Compare cell background colors and borders to the original
      Excel view.'
  - name: '**Number formats preserved?** Look for the `data-format` attribute on `<td>`
      elements.'
    text: '**Number formats preserved?** Look for the `data-format` attribute on `<td>`
      elements.'
  - name: '**Images displayed?** If you exported images as Base64, they should appear
      inline.'
    text: '**Images displayed?** If you exported images as Base64, they should appear
      inline.'
  - name: '**Browser console clean?** No JavaScript errors related to Grid.js.'
    text: '**Browser console clean?** No JavaScript errors related to Grid.js.'
  type: HowTo
tags:
- Excel
- HTML
- Aspose.Cells
title: Сохранить Excel в формате HTML – Полное руководство по экспорту Excel с сохранением
  форматирования
url: /ru/net/exporting-excel-to-html-with-advanced-options/save-excel-as-html-complete-guide-to-export-excel-with-forma/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Сохранить Excel как HTML – Полное руководство по экспорту Excel с форматированием

Когда‑нибудь задумывались, как **сохранить Excel как HTML** без потери цветов, границ или форматов чисел? Вы не одиноки. Во многих сценариях отчетности вам нужен готовый к вебу вид рабочей книги, и самый быстрый способ — экспортировать файл напрямую в HTML.  

В этом руководстве мы пройдем точные шаги по **конвертации Excel в HTML** с использованием Aspose.Cells, включим форматирование чисел Grid.js и убедимся, что результат выглядит точно так же, как оригинальная таблица. К концу вы получите готовый HTML‑файл, который можно разместить на любом веб‑сервере.

## Что вы узнаете

- Предварительные требования и установка пакета  
- Загрузка существующей рабочей книги (или создание её на лету)  
- Настройка `HtmlSaveOptions` для идеального визуального соответствия  
- Включение `GridJsOptions.EnableNumberFormat` для сохранения стилизации чисел  
- Сохранение файла и проверка результата  

Если вы когда‑либо пытались **экспортировать Excel с форматированием** с помощью обычного дампа CSV, вы знаете, насколько это может быть раздражающим, когда числа превращаются в обычный текст. Это руководство помогает избежать этой ловушки.

---

## Предварительные требования – Настройка среды разработки

Прежде чем погрузиться в код, убедитесь, что у вас есть:

| Требование | Почему это важно |
|-------------|----------------|
| .NET 6.0 или новее (в руководстве используется .NET 6) | Современные API и лучшая производительность |
| Visual Studio 2022 (или VS Code с расширением C#) | Удобное редактирование и отладка |
| Aspose.Cells for .NET NuGet package | Библиотека, обеспечивающая `HtmlSaveOptions` и `GridJsOptions` |
| Пример файла Excel (`sample.xlsx`) или рабочая книга, генерируемая в коде | Исходный файл, который будет конвертирован |

Установите Aspose.Cells с помощью следующей команды в консоли диспетчера пакетов:

```powershell
Install-Package Aspose.Cells
```

> **Совет:** Если вы используете CI‑конвейер, добавьте ту же строку `dotnet add package` в ваш скрипт сборки, чтобы зависимость всегда была доступна.

---

## Шаг 1: Загрузить или создать рабочую книгу

Вы можете либо загрузить существующий файл, либо создать его программно. Ниже приведён минимальный пример, который создаёт рабочую книгу с несколькими стилизованными ячейками, чтобы вы могли увидеть, как форматирование сохраняется при экспорте.

```csharp
using Aspose.Cells;
using System.Drawing;

// Create a new workbook
Workbook wb = new Workbook();
Worksheet sheet = wb.Worksheets[0];
sheet.Name = "Report";

// Populate some data
sheet.Cells["A1"].PutValue("Product");
sheet.Cells["B1"].PutValue("Price");
sheet.Cells["A2"].PutValue("Widget");
sheet.Cells["B2"].PutValue(19.99);
sheet.Cells["A3"].PutValue("Gadget");
sheet.Cells["B3"].PutValue(42.5);

// Apply basic styling
Style headerStyle = wb.CreateStyle();
headerStyle.Font.IsBold = true;
headerStyle.ForegroundColor = Color.LightGray;
headerStyle.Pattern = BackgroundType.Solid;
sheet.Cells["A1:B1"].SetStyle(headerStyle);

// Format the price column as currency
Style priceStyle = wb.CreateStyle();
priceStyle.Number = 164; // Built‑in currency format
sheet.Cells["B2:B3"].SetStyle(priceStyle);
```

> **Почему это важно:** Явно задавая форматы чисел, вы позже увидите, как `GridJsOptions.EnableNumberFormat` сохраняет эти форматы в HTML‑выводе.

---

## Шаг 2: Настроить параметры сохранения HTML

Теперь мы создаём экземпляр `HtmlSaveOptions`. Этот объект сообщает Aspose.Cells, как именно вы хотите, чтобы HTML был отрендерен.

```csharp
// Step 2: Create HTML save options
HtmlSaveOptions htmlOptions = new HtmlSaveOptions
{
    // Export the entire workbook as a single HTML page
    ExportActiveWorksheetOnly = false,

    // Keep the original cell styles (fonts, colors, borders)
    ExportGridLines = true,
    ExportColumnHeaders = true,
    ExportRowHeaders = true
};
```

### Включение форматирования чисел Grid.js

Если вы планируете внедрять HTML в страницу, использующую **Grid.js** для интерактивных таблиц, вам понадобится, чтобы числа оставались отформатированными (например, символы валют, разделители тысяч). Следующая строка делает именно это:

```csharp
// Step 3: Enable number formatting for Grid.js tables
htmlOptions.GridJsOptions = new GridJsOptions { EnableNumberFormat = true };
```

> **Что происходит под капотом?** `EnableNumberFormat` вставляет небольшой фрагмент JavaScript, который сообщает Grid.js интерпретировать атрибут `data-format` ячейки, сохраняя форматирование в стиле Excel в браузере.

---

## Шаг 3: Сохранить рабочую книгу как HTML‑файл

Когда рабочая книга готова, а параметры настроены, последняя строка записывает HTML‑файл на диск.

```csharp
// Step 4: Save the workbook as an HTML file with the configured options
string outputPath = @"C:\Temp\gridjs.html";
wb.Save(outputPath, htmlOptions);
Console.WriteLine($"Workbook successfully saved as HTML to: {outputPath}");
```

Запуск программы создаёт файл `gridjs.html`, который выглядит так (упрощённый вид):

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8" />
    <title>Report</title>
    <link rel="stylesheet" href="gridjs.css" />
    <script src="gridjs.js"></script>
</head>
<body>
    <table class="gridjs-table">
        <thead>
            <tr><th>Product</th><th>Price</th></tr>
        </thead>
        <tbody>
            <tr><td>Widget</td><td data-format="$#,##0.00">19.99</td></tr>
            <tr><td>Gadget</td><td data-format="$#,##0.00">42.5</td></tr>
        </tbody>
    </table>
</body>
</html>
```

Откройте файл в любом браузере, и вы увидите красиво оформленную таблицу с светло‑серым фоном заголовка и форматированием валют. Если разместить страницу на сайте, который уже загружает Grid.js, числа автоматически отобразятся с правильными запятыми и символами.

---

## Распространённые подводные камни при **конвертации Excel в HTML**

| Проблема | Почему происходит | Как избежать |
|-------|---------------|-----------------|
| **Потерянные формулы** | HTML статичен; формулы превращаются в обычные значения. | Если нужны живые расчёты, храните рабочую книгу на сервере и используйте JavaScript‑библиотеки, такие как SheetJS. |
| **Отсутствующие изображения** | Изображения хранятся как отдельные ресурсы. | Установите `HtmlSaveOptions.ExportImagesAsBase64 = true`, чтобы встроить их напрямую. |
| **Большие файлы** | Большие рабочие книги генерируют огромный HTML + JS. | Используйте `ExportOnlyVisibleSheets` или разбейте на несколько страниц через `HtmlSaveOptions.OnePagePerSheet`. |
| **Неправильная локаль чисел** | Excel хранит числа в нейтральной культуре, браузеры могут применять локальные настройки. | Явно задайте `htmlOptions.Encoding = Encoding.UTF8` и используйте `GridJsOptions.EnableNumberFormat`. |

---

## Продвинуто: Экспорт нескольких листов с отдельными экземплярами Grid.js

Если ваша рабочая книга содержит несколько листов и вы хотите, чтобы каждый стал отдельной таблицей Grid.js, вы можете пройтись по листам и сохранить каждый отдельно:

```csharp
for (int i = 0; i < wb.Worksheets.Count; i++)
{
    Worksheet ws = wb.Worksheets[i];
    HtmlSaveOptions opt = new HtmlSaveOptions
    {
        ExportActiveWorksheetOnly = true,
        GridJsOptions = new GridJsOptions { EnableNumberFormat = true }
    };
    string sheetPath = $@"C:\Temp\{ws.Name}.html";
    wb.Save(sheetPath, opt);
    Console.WriteLine($"Saved {ws.Name} to {sheetPath}");
}
```

Каждый файл будет содержать собственный элемент `<table class="gridjs-table">`, готовый к независимому управлению.

---

## Проверка вывода – Быстрый чек‑лист

1. **Стили сохранены?** Сравните цвета фона ячеек и границы с оригинальным видом в Excel.  
2. **Форматы чисел сохранены?** Ищите атрибут `data-format` в элементах `<td>`.  
3. **Изображения отображаются?** Если вы экспортировали изображения как Base64, они должны появиться встроенными.  
4. **Консоль браузера чиста?** Нет JavaScript‑ошибок, связанных с Grid.js.  

Если любой из этих пунктов не проходит, проверьте соответствующее свойство `HtmlSaveOptions` — большинство проблем возникает из‑за отсутствующего флага.

---

## Заключение

Теперь у вас есть надёжный, готовый к продакшену метод **сохранения Excel как HTML**, сохраняющий каждый стиль, границу и числовое представление. Настроив `HtmlSaveOptions` и включив `GridJsOptions.EnableNumberFormat`, вы превратили статическую таблицу в веб‑дружелюбную, которая без проблем работает с Grid.js.

Короче говоря, это руководство показывает, как **конвертировать Excel в HTML** и **экспортировать Excel с форматированием** с помощью Aspose.Cells. Не стесняйтесь экспериментировать: пробуйте разные темы, встраивайте диаграммы или даже обслуживайте HTML через endpoint ASP.NET для конвертации «на лету».

---

## Что дальше?

- **Изучить другие форматы экспорта**: PDF, PNG или CSV через `Workbook.Save`.  
- **Интегрировать с ASP.NET Core**: Возвращать строку HTML напрямую из действия контроллера.  
- **Сочетать с SheetJS**: Загрузить сгенерированный HTML обратно в JavaScript‑рабочую книгу для клиентского редактирования.  

Если возникнут проблемы, оставьте комментарий ниже или ознакомьтесь с документацией Aspose.Cells для более глубоких настроек. Счастливого кодинга!

---

## Что вам следует изучить дальше?

Следующие руководства охватывают тесно связанные темы, которые развивают техники, продемонстрированные в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [Как экспортировать Excel в HTML с сеткой линий, используя Aspose.Cells для .NET](/cells/english/net/workbook-operations/export-excel-to-html-grid-lines-aspose-cells-net/)
- [Экспорт Excel в HTML с сохранением стилей границ, используя Aspose.Cells для Java](/cells/english/java/workbook-operations/aspose-cells-java-export-excel-html-border-styles/)
- [Конвертация HTML в Excel с помощью Aspose.Cells .NET: Полное руководство](/cells/english/net/workbook-operations/convert-html-to-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}