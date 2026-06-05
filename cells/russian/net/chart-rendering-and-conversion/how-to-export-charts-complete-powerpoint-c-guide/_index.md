---
category: general
date: 2026-06-05
description: Как экспортировать диаграммы из PowerPoint с помощью C#. Включает экспорт
  OLE‑объектов и делает диаграммы редактируемыми в полученном PPTX – пошагово.
draft: false
keywords:
- how to export charts
- export ole objects
- how to export ole
- make charts editable
language: ru
og_description: Как экспортировать диаграммы из PowerPoint с помощью C#. Узнайте,
  как экспортировать OLE‑объекты и сделать диаграммы редактируемыми в сохранённом
  PPTX – пошагово.
og_title: Как экспортировать диаграммы — Полное руководство по PowerPoint на C#
schemas:
- author: Aspose
  dateModified: '2026-06-05'
  description: How to export charts from PowerPoint using C#. Includes export OLE
    objects and make charts editable in the resulting PPTX – step‑by‑step.
  headline: How to Export Charts – Complete PowerPoint C# Guide
  type: TechArticle
- description: How to export charts from PowerPoint using C#. Includes export OLE
    objects and make charts editable in the resulting PPTX – step‑by‑step.
  name: How to Export Charts – Complete PowerPoint C# Guide
  steps:
  - name: Full Working Example
    text: Below is the complete, self‑contained program you can compile and run. It
      includes `using` statements, proper disposal, and comments that explain each
      line.
  - name: What if the source file has no charts?
    text: The code will still run; `ExportEditableCharts` simply has no effect because
      there’s nothing to convert. No error is thrown.
  - name: Can I export only specific charts?
    text: Yes. Instead of using the global `ExportEditableCharts` flag, you can iterate
      through `presentation.Slides` and set `Chart.IsEditable = true` on individual
      chart objects before saving. This gives you granular control.
  - name: Does enabling OLE export increase file size?
    text: A little. The binary OLE streams are stored verbatim, so the resulting PPTX
      can be a few kilobytes larger. In most business scenarios the trade‑off is worth
      it because you retain full editability.
  - name: Which PowerPoint versions can open the resulting file?
    text: Any version that supports the OOXML standard (PowerPoint 2007 and later).
      The editable chart feature relies on the native chart editor introduced in Office
      2007, so older binaries like `.ppt` won’t benefit.
  type: HowTo
tags:
- PowerPoint
- C#
- Aspose.Slides
- OLE
- Charts
title: Как экспортировать диаграммы — Полное руководство по PowerPoint на C#
url: /ru/net/chart-rendering-and-conversion/how-to-export-charts-complete-powerpoint-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как экспортировать диаграммы – Полное руководство по PowerPoint на C#

Когда‑нибудь задавались вопросом **как экспортировать диаграммы** из презентации PowerPoint, не теряя возможность их последующего редактирования? Вы не одиноки. Во многих конвейерах отчетности данные диаграмм находятся внутри PPTX, и после передачи файла получателю часто нужно подправить значение или изменить подпись. Хорошая новость в том, что с помощью нескольких строк C# вы можете сохранить возможность редактирования и даже экспортировать встроенные OLE‑объекты одновременно.

В этом руководстве мы пройдем практический, готовый к запуску пример, который показывает **как экспортировать диаграммы**, как **экспортировать OLE‑объекты**, и как **сделать диаграммы редактируемыми** в выходном файле. К концу вы получите переиспользуемый фрагмент кода, который можно вставить в любой .NET‑проект, использующий библиотеку Aspose.Slides.

> **Подсказка:** Если вы новичок в Aspose.Slides, убедитесь, что добавили NuGet‑пакет `Aspose.Slides.NET` в ваш проект — иначе код не скомпилируется.

## Что понадобится

| Requirement | Why it matters |
|-------------|----------------|
| .NET 6+ (or .NET Framework 4.7+) | Современные среды выполнения обеспечивают лучшую производительность и упрощённое управление пакетами. |
| Aspose.Slides for .NET (latest version) | Эта библиотека предоставляет классы `Presentation` и `PptxSaveOptions`, которые мы будем использовать. |
| A sample PowerPoint file with at least one chart | Пример файла PowerPoint, содержащего хотя бы одну диаграмму. Демонстрация работает с любым `.pptx`, содержащим диаграмму; после экспорта вы увидите возможность редактирования. |
| An IDE (Visual Studio, Rider, or VS Code) | Удобно для быстрого отладки и просмотра сгенерированного файла. |

Никакие дополнительные сторонние инструменты не требуются — всё обрабатывается API Aspose.

## Шаг 1 – Загрузка исходной презентации

Сначала нам нужно загрузить оригинальный PPTX в память. Считайте это открытием документа в Word перед началом редактирования.

```csharp
using Aspose.Slides;

// Step 1: Load the source presentation
Presentation presentation = new Presentation(@"C:\MyProjects\input.pptx");
```

> **Почему это важно:** Объект `Presentation` является точкой входа для всех дальнейших операций. Он разбирает файл, строит объектную модель слайдов, фигур, диаграмм и OLE‑объектов и сохраняет всё в изменяемом состоянии.

## Шаг 2 – Создание параметров сохранения и включение редактируемых диаграмм

По умолчанию при вызове `Save` библиотека преобразует диаграммы в статические изображения. Чтобы сохранить их редактируемыми, необходимо переключить флаг `ExportEditableCharts`.

```csharp
// Step 2: Create PPTX save options and enable editable charts
PptxSaveOptions saveOptions = new PptxSaveOptions
{
    // This tells Aspose to keep chart data in a format PowerPoint can edit.
    ExportEditableCharts = true
};
```

> **Как это работает:** Когда `ExportEditableCharts` равно `true`, библиотека записывает XML‑определение диаграммы (`chart.xml`) в PPTX вместо растеризации. PowerPoint затем читает этот XML и позволяет пользователю открыть редактор диаграмм.

## Шаг 3 – Включение экспорта встроенных OLE‑объектов

Во многих презентациях встраиваются листы Excel, диаграммы Visio или даже PDF‑файлы в виде OLE‑объектов. Если вы хотите, чтобы они сохранялись при передаче, включите `ExportOLEObjects`.

```csharp
// Step 3: Enable export of embedded OLE objects
saveOptions.ExportOLEObjects = true;
```

> **Что на самом деле означает “export OLE objects”:** Пакет OLE хранится как бинарный блоб внутри PPTX. Установка этого флага сохраняет оригинальный бинарный поток, позволяя получателю дважды щёлкнуть объект и открыть его в родном приложении (например, Excel). Без этого OLE‑объект будет удалён, ссылки сломаются и данные потеряются.

## Шаг 4 – Сохранение презентации с настроенными параметрами

Теперь, когда параметры подготовлены, мы просто просим Aspose записать файл.

```csharp
// Step 4: Save the presentation with the configured options
presentation.Save(@"C:\MyProjects\editable.pptx", saveOptions);
```

> **Результат:** `editable.pptx` содержит те же слайды, что и `input.pptx`, но любую диаграмму можно редактировать непосредственно в PowerPoint, а все встроенные OLE‑объекты остаются нетронутыми.

### Полный рабочий пример

Ниже приведена полная, самодостаточная программа, которую можно скомпилировать и запустить. В ней есть `using`‑директивы, корректное освобождение ресурсов и комментарии, объясняющие каждую строку.

```csharp
using System;
using Aspose.Slides;

namespace ExportChartsDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Path to the source PPTX
            string sourcePath = @"C:\MyProjects\input.pptx";
            // Path where the edited PPTX will be saved
            string destPath = @"C:\MyProjects\editable.pptx";

            // Load the presentation
            using (Presentation presentation = new Presentation(sourcePath))
            {
                // Configure save options
                PptxSaveOptions options = new PptxSaveOptions
                {
                    ExportEditableCharts = true,   // make charts editable
                    ExportOLEObjects = true        // export OLE objects such as embedded Excel sheets
                };

                // Save the new file
                presentation.Save(destPath, options);
            }

            Console.WriteLine("Presentation saved with editable charts and OLE objects.");
        }
    }
}
```

**Ожидаемый результат:** После запуска программы откройте `editable.pptx` в PowerPoint. Щёлкните правой кнопкой мыши любую диаграмму → *Edit Data* → откроется редактор диаграмм, подтверждая, что **make charts editable** выполнено успешно. Дважды щёлкните встроенный лист Excel — он откроется в Excel, доказывая, что **export OLE objects** сработал.

![диаграмма как экспортировать диаграммы](https://example.com/images/export-charts.png "как экспортировать диаграммы – PowerPoint после экспорта")

*(Текст альтернативы: как экспортировать диаграммы – скриншот PowerPoint с редактируемой диаграммой и OLE‑объектом)*

## Часто задаваемые вопросы и особые случаи

### Что если исходный файл не содержит диаграмм?

Код всё равно выполнится; `ExportEditableCharts` просто не окажет влияния, потому что нечего конвертировать. Ошибки не будет.

### Можно ли экспортировать только определённые диаграммы?

Да. Вместо глобального флага `ExportEditableCharts` можно пройтись по `presentation.Slides` и установить `Chart.IsEditable = true` для отдельных объектов диаграмм перед сохранением. Это даёт более тонкий контроль.

```csharp
foreach (ISlide slide in presentation.Slides)
{
    foreach (IChart chart in slide.Shapes.OfType<IChart>())
    {
        chart.IsEditable = true; // enable editability only for this chart
    }
}
```

### Увеличивает ли включение экспорта OLE размер файла?

Немного. Бинарные потоки OLE сохраняются в оригинальном виде, поэтому получающийся PPTX может стать на несколько килобайт больше. В большинстве бизнес‑сценариев такой компромисс оправдан, поскольку сохраняется полная редактируемость.

### Какие версии PowerPoint могут открыть полученный файл?

Любая версия, поддерживающая стандарт OOXML (PowerPoint 2007 и новее). Функция редактируемой диаграммы опирается на встроенный редактор диаграмм, появившийся в Office 2007, поэтому более старые форматы, такие как `.ppt`, не получат выгоду.

## Советы для кода, готового к продакшену

| Tip | Reason |
|-----|--------|
| Use `using` blocks (as shown) to dispose of `Presentation` objects. | Предотвращает утечки памяти, особенно при обработке большого количества файлов в пакетном режиме. |
| Validate file paths before loading. | Избегает `FileNotFoundException`, который мог бы привести к сбою фонового сервиса. |
| Log the `ExportEditableCharts` and `ExportOLEObjects` settings. | Полезно для отладки, когда пользователь сообщает о недоступных для редактирования диаграммах. |
| Catch `Aspose.Slides.Exception` separately. | Предоставляет более понятные сообщения об ошибках из библиотеки (например, неподдерживаемые типы диаграмм). |
| Consider `PptxCompressionLevel` if file size matters. | Можно сжать вывод, сохранив при этом редактируемость. |

## Итоги – Что мы достигли

Мы начали с чёткого вопроса: **как экспортировать диаграммы** из файла PowerPoint, сохранив их редактируемыми и удерживая встроенные OLE‑объекты. Загрузив презентацию, настроив `PptxSaveOptions` (`ExportEditableCharts = true` и `ExportOLEObjects = true`) и сохранив файл, мы получили PPTX, удовлетворяющий обоим требованиям. Тот же шаблон можно переиспользовать для пакетных конвертаций, CI‑конвейеров или любого автоматизированного инструмента отчётности.

## Что изучать дальше?

- **Экспортировать диаграммы как изображения** для статических отчётов (`saveOptions.ExportEditableCharts = false`).  
- **Преобразовать PPTX в PDF**, сохранив векторную графику (`PdfSaveOptions`).  
- **Программно изменять данные диаграмм** (например, обновлять значения рядов перед экспортом).  
- **Интегрировать с Azure Functions**, чтобы предоставить API экспорта диаграмм по запросу.

Экспериментируйте, делитесь найденными особенностями. Приятного кодинга, и пусть все ваши диаграммы остаются редактируемыми!

## Что вам следует изучить дальше?

Следующие руководства охватывают тесно связанные темы, построенные на техниках, продемонстрированных в этом руководстве. Каждый ресурс включает полные рабочие примеры кода с пошаговыми объяснениями, помогающими освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в собственных проектах.

- [Как экспортировать диаграммы Excel в PDF с помощью Aspose.Cells для .NET: пошаговое руководство](/cells/english/net/workbook-operations/export-excel-charts-pdf-aspose-cells-net/)
- [Как преобразовать диаграммы Excel в SVG с помощью Aspose.Cells для .NET (пошаговое руководство)](/cells/english/net/charts-graphs/convert-excel-chart-to-svg-aspose-cells-net/)
- [Как применить темы к диаграммам Excel с помощью Aspose.Cells .NET: пошаговое руководство](/cells/english/net/charts-graphs/apply-themes-charts-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}