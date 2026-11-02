---
category: general
date: 2026-06-17
description: Встраивание шрифтов в HTML при сохранении книги в формате HTML. Узнайте,
  как преобразовать книгу в HTML и экспортировать Excel в HTML со встроенными шрифтами
  за несколько шагов.
draft: false
keywords:
- embed fonts in html
- save workbook as html
- convert workbook to html
- how to export excel html
language: ru
og_description: Встраивайте шрифты в HTML при сохранении книги в формате HTML. Следуйте
  этому руководству, чтобы преобразовать книгу в HTML, и узнайте, как экспортировать
  Excel в HTML с полной поддержкой шрифтов.
og_title: Встраивание шрифтов в HTML — экспорт книги Excel в HTML
schemas:
- author: Aspose
  dateModified: '2026-06-17'
  description: Embed fonts in HTML while you save workbook as HTML. Learn how to convert
    workbook to HTML and export Excel HTML with embedded fonts in a few steps.
  headline: Embed Fonts in HTML – Export Excel Workbook to HTML with Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- Excel
- HTML export
title: Встраивание шрифтов в HTML – Экспорт книги Excel в HTML с помощью Aspose.Cells
url: /ru/net/exporting-excel-to-html-with-advanced-options/embed-fonts-in-html-export-excel-workbook-to-html-with-aspos/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Встраивание шрифтов в HTML – Экспорт книги Excel в HTML с помощью Aspose.Cells

Когда‑нибудь задумывались, как **встраивать шрифты в HTML** при экспорте листа Excel? Вы не одиноки. Многие разработчики сталкиваются с тем, что сгенерированный HTML показывает общий шрифт без засечек вместо оригинального оформления Excel. Хорошая новость? Пара строк кода позволяют **сохранить книгу как HTML** и сохранить каждый шрифт без изменений.

В этом руководстве мы пройдем весь процесс **конвертации книги в HTML** с использованием Aspose.Cells для .NET, объясним, почему встраивание шрифтов важно, и покажем, как именно **экспортировать Excel в HTML**, чтобы результат выглядел точно как исходная таблица. Без внешних инструментов, без ручной пост‑обработки — только чистый, исполняемый C#‑код.

## Требования

- .NET 6.0 или новее (пример работает на .NET Core, .NET Framework и .NET 5+)
- NuGet‑пакет Aspose.Cells for .NET (`Install-Package Aspose.Cells`)
- Базовые знания C# и работы с файлами Excel
- Необязательно: пользовательский файл шрифта TrueType, который вы хотите встроить (например, `MyFont.ttf`)

Всё готово? Отлично — приступим.

## Шаг 1: Настройка проекта и загрузка книги Excel

Сначала нам нужен объект workbook. Его можно создать с нуля или загрузить существующий `.xlsx`. Ниже минимальная настройка, которая также добавляет пользовательский шрифт в коллекцию стилей книги.

```csharp
using Aspose.Cells;
using System.IO;

// Load an existing workbook (replace with your own path)
Workbook wb = new Workbook("SampleData.xlsx");

// OPTIONAL: Register a custom font if your sheet uses one that isn’t standard
string fontPath = Path.Combine(Directory.GetCurrentDirectory(), "MyFont.ttf");
if (File.Exists(fontPath))
{
    // Register the font with the font manager – this ensures Aspose knows about it
    FontConfigs.AddFontFile(fontPath);
}
```

*Почему этот шаг?* Загрузка книги сначала даёт Aspose.Cells возможность проанализировать все стили ячеек. Регистрация пользовательского шрифта гарантирует, что шрифт будет найден, когда мы позже встроим его в HTML‑файл.

## Шаг 2: Настройка HtmlSaveOptions для **встраивания шрифтов в HTML**

Всё волшебство происходит в `HtmlSaveOptions`. Установка `EmbedFonts = true` сообщает библиотеке встраивать каждый используемый шрифт как правило `@font-face`, закодированное в Base64, непосредственно в сгенерированный HTML‑файл.

```csharp
// Configure HTML save options – this is where we embed fonts in HTML
HtmlSaveOptions saveOptions = new HtmlSaveOptions
{
    // Embed all referenced fonts directly into the HTML output
    EmbedFonts = true,

    // Optional: keep the original layout (useful for complex sheets)
    ExportActiveWorksheetOnly = true,

    // Optional: produce a single HTML file (no external CSS or images)
    ExportImagesAsBase64 = true
};
```

*Зачем включать `EmbedFonts`?* Без этого выходной HTML будет ссылаться на системные шрифты, и любой, кто откроет файл на машине без этих шрифтов, увидит замену. Встраивание гарантирует визуальное соответствие во всех браузерах и устройствах.

## Шаг 3: **Сохранить книгу как HTML** с настроенными параметрами

Теперь мы наконец записываем файл. Метод `Save` принимает три аргумента: путь назначения, формат (`SaveFormat.Html`) и только что сконфигурированные параметры.

```csharp
// Define the output HTML file path
string outputPath = Path.Combine(Directory.GetCurrentDirectory(), "with-fonts.html");

// Save the workbook as HTML with embedded fonts
wb.Save(outputPath, SaveFormat.Html, saveOptions);
```

Если всё прошло гладко, вы получите один файл `with-fonts.html`, содержащий полную раскладку таблицы *и* данные шрифта, закодированные прямо в разметке.

## Ожидаемый результат

Откройте `with-fonts.html` в любом современном браузере (Chrome, Edge, Firefox). Вы должны увидеть:

- Те же значения ячеек, цвета и границы, что и в оригинальном файле Excel.
- Текст, отрисованный точным шрифтом, использованным в Excel, даже если этот шрифт не установлен на вашем компьютере.
- Нет внешних `.css` или файлов изображений — всё находится внутри HTML‑файла.

Ниже небольшой фрагмент того, как может выглядеть сгенерированный блок `<style>` (строка Base64 усечена для краткости):

```html
<style type="text/css">
@font-face{
    font-family:'MyCustomFont';
    src:url(data:font/truetype;charset=utf-8;base64,AAEAAAALAIAAAwAwT1Mv... ) format('truetype');
}
...
</style>
```

## Шаг 4: Распространённые проблемы и способы их решения

| Проблема | Почему происходит | Решение |
|------|----------------|-----|
| **Отсутствует шрифт в HTML** | Файл шрифта не был зарегистрирован в `FontConfigs` перед сохранением. | Вызовите `FontConfigs.AddFontFile` *до* создания `HtmlSaveOptions`. |
| **Большой размер HTML‑файла** | Встраивание многих крупных шрифтов может сильно увеличить файл. | Встраивайте только необходимые шрифты; используйте `saveOptions.FontEmbeddingMode = FontEmbeddingMode.Subset`, чтобы включать только используемые глифы (доступно в новых версиях Aspose). |
| **Неправильные символы (например, азиатские глифы)** | Шрифт не содержит требуемых диапазонов Unicode. | Убедитесь, что исходный шрифт поддерживает нужные символы, либо встройте дополнительный запасный шрифт. |
| **Снижение производительности на больших книгах** | Встраивание шрифтов добавляет накладные расходы обработки. | Экспортируйте только активный лист (`ExportActiveWorksheetOnly = true`) или разбейте книгу на более мелкие части. |

## Шаг 5: Расширение решения — Экспорт нескольких листов

Если нужно **конвертировать книгу в HTML** для всех листов, просто отключите `ExportActiveWorksheetOnly`:

```csharp
saveOptions.ExportActiveWorksheetOnly = false; // Export every sheet
wb.Save("all-sheets.html", SaveFormat.Html, saveOptions);
```

Каждый лист появится как отдельный `<div>` в том же HTML‑файле, по‑прежнему с встроенными шрифтами.

## Совет профессионала: Комбинация с настройкой CSS

Иногда требуется более тонкий контроль над сгенерированной разметкой. `HtmlSaveOptions` предлагает свойство `CssClassPrefix`, позволяющее избежать конфликтов имён классов при объединении нескольких HTML‑экспортов:

```csharp
saveOptions.CssClassPrefix = "myExcel_";
```

Теперь каждый сгенерированный CSS‑класс будет начинаться с `myExcel_`, что упрощает последующее применение собственного стиля.

## Итоги

- **Встраивание шрифтов в HTML** осуществляется установкой `HtmlSaveOptions.EmbedFonts = true`.
- Используйте **сохранение книги как HTML** (`wb.Save(..., SaveFormat.Html, ...)`) для получения единого, автономного файла.
- Этот метод **конвертирует книгу в HTML**, сохраняя все визуальные детали, отвечая на классический вопрос **как экспортировать Excel в HTML** с полной точностью.
- Регистируйте пользовательские шрифты через `FontConfigs.AddFontFile`, чтобы они были доступны для встраивания.
- Настраивайте параметры, такие как `ExportImagesAsBase64` и `ExportActiveWorksheetOnly`, под нужды вашего проекта.

## Что дальше?

- Попробуйте экспортировать в **MHTML** (`SaveFormat.Mhtml`) для ещё более портативного пакета.
- Исследуйте **конвертацию в PDF** (`SaveFormat.Pdf`), если нужен готовый к печати формат.
- Интегрируйте экспорт HTML в веб‑API, чтобы пользователи могли мгновенно скачивать стилизованные таблицы.

Экспериментируйте — меняйте шрифты, выбирайте другие листы или комбинируйте несколько форматов экспорта. Гибкость Aspose.Cells позволяет адаптировать вывод под любой сценарий, от автоматизированных отчётных панелей до готовых к отправке по email HTML‑фрагментов.

Удачной разработки, и пусть ваш HTML всегда выглядит точно как оригинальная таблица Excel!

## Что стоит изучить дальше?

Следующие руководства охватывают тесно связанные темы, расширяющие техники, продемонстрированные в этом пособии. Каждый ресурс включает полностью рабочие примеры кода с пошаговыми объяснениями, помогающими освоить дополнительные возможности API и исследовать альтернативные подходы в ваших проектах.

- [Как создать и экспортировать Excel в HTML с помощью Aspose.Cells Java | Руководство по операциям с книгой](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)
- [Установка шрифта по умолчанию при конвертации Excel в HTML с Aspose.Cells для .NET | Руководство по операциям с книгой](/cells/english/net/workbook-operations/excel-html-conversion-default-font-aspose-cells-net/)
- [Как экспортировать Excel в HTML с линиями сетки, используя Aspose.Cells для .NET](/cells/english/net/workbook-operations/export-excel-to-html-grid-lines-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}