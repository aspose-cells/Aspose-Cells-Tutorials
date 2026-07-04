---
category: general
date: 2026-07-03
description: Как сохранить диаграммы, сохраняя их форматирование, используя Aspose.Slides
  в C#. Следуйте этому пошаговому руководству.
draft: false
keywords:
- how to preserve charts
- preserve chart formatting
language: ru
og_description: Как сохранять диаграммы и их форматирование с помощью Aspose.Slides
  в C#. Полное руководство с кодом.
og_title: как сохранить диаграммы – сохранить форматирование диаграмм в PowerPoint
  (C#)
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: how to preserve charts while keeping preserve chart formatting using
    Aspose.Slides in C#. Follow this step‑by‑step guide.
  headline: how to preserve charts – preserve chart formatting in PowerPoint C#
  type: TechArticle
- description: how to preserve charts while keeping preserve chart formatting using
    Aspose.Slides in C#. Follow this step‑by‑step guide.
  name: how to preserve charts – preserve chart formatting in PowerPoint C#
  steps:
  - name: Open `EditableCharts.pptx` in PowerPoint.
    text: Open `EditableCharts.pptx` in PowerPoint.
  - name: Click any chart → “Edit Data”.
    text: Click any chart → “Edit Data”.
  - name: The Excel‑like data sheet should appear, letting you modify series values.
    text: The Excel‑like data sheet should appear, letting you modify series values.
  type: HowTo
- questions:
  - answer: Directly no—`ExportEditableObjects` only applies to the PPTX format. Convert
      first, then export.
    question: Does this work with PowerPoint 2003 (PPT) files?
  - answer: Absolutely. The same `ExportEditableObjects` flag keeps SmartArt, tables,
      and diagrams editable.
    question: Can I preserve other objects like SmartArt?
  - answer: 'The slide size is stored in the presentation metadata and isn’t affected
      by these options. No extra code needed. --- ## Next steps – keep the momentum
      Now that you’ve nailed **how to preserve charts**, try exploring: - **preserve
      chart formatting** for specific chart types (e.g., stacked bar vs. rad'
    question: What if I need to keep the original slide size?
  type: FAQPage
tags:
- Aspose.Slides
- C#
- PowerPoint
- chart automation
title: как сохранить диаграммы — сохранить форматирование диаграмм в PowerPoint C#
url: /ru/net/setting-chart-appearance/how-to-preserve-charts-preserve-chart-formatting-in-powerpoi/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# как сохранить диаграммы – сохранить форматирование диаграмм в PowerPoint C#

Когда‑нибудь задавались вопросом **how to preserve charts**, когда нужно экспортировать или программно изменять файл PowerPoint? Возможно, вы попытались быстро сохранить, и диаграмма превратилась в статическое изображение, нарушив возможность редактирования, на которую вы рассчитывали.  

В этом руководстве мы покажем вам **how to preserve charts** **и** сохранить их **preserve chart formatting** нетронутыми, используя Aspose.Slides для .NET. К концу у вас будет готовый фрагмент кода на C#, который создаёт PPTX, где каждая диаграмма остаётся редактируемым объектом OOXML — без преобразования в плоские изображения.

## Что вы узнаете

- Точные шаги по загрузке презентации, настройке параметров экспорта и сохранению с **preserving chart formatting**.  
- Почему флаг `ExportEditableObjects` важен и как он предотвращает растеризацию диаграмм.  
- Распространённые подводные камни (например, старые форматы PPT, отсутствие шрифтов) и быстрые решения.  

Предыдущий опыт работы с Aspose не требуется; достаточно базовой настройки C# и файла PowerPoint, который вы хотите оставить пригодным для диаграмм.

## Требования

- .NET 6.0 или новее (код также работает с .NET Framework 4.7+).  
- NuGet‑пакет Aspose.Slides for .NET (`Install-Package Aspose.Slides.NET`).  
- Пример файла `input.pptx`, содержащий как минимум одну диаграмму.  
- Visual Studio, Rider или любой другой редактор по вашему выбору.

---

## Шаг 1: Установите Aspose.Slides и создайте новый консольный проект

Для начала создайте новый консольный проект и подключите библиотеку:

```bash
dotnet new console -n PreserveChartsDemo
cd PreserveChartsDemo
dotnet add package Aspose.Slides.NET
```

> **Pro tip:** Если вы работаете за корпоративным прокси, добавьте флаг `--no-restore` и выполните восстановление позже с вашими настройками прокси.

## Шаг 2: Загрузите исходную презентацию — первое место для применения **how to preserve charts**

Откройте ваш файл PPTX с помощью класса `Presentation`. Здесь действительно начинается путь к **how to preserve charts**.

```csharp
using Aspose.Slides;
using Aspose.Slides.Export;

namespace PreserveChartsDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 2: Load the source presentation
            // Replace the path with the location of your PPTX that contains charts.
            Presentation pres = new Presentation(@"YOUR_DIRECTORY\input.pptx");
```

Обратите внимание, что мы ещё не трогали объекты диаграмм — это намеренно. Загрузка файла в исходном виде гарантирует сохранение оригинальной XML‑структуры, что критически важно для **preserve chart formatting** позже.

## Шаг 3: Настройте параметры экспорта — сердце **how to preserve charts**

Aspose.Slides предоставляет класс `PresentationExportOptions`. Установка `ExportEditableObjects` в `true` указывает движку сохранять диаграммы, таблицы и SmartArt как нативные части OOXML, а не преобразовывать их в плоские изображения.

```csharp
            // Step 3: Configure export options to keep objects editable
            PresentationExportOptions exportOptions = new PresentationExportOptions
            {
                // This flag is the key to how to preserve charts.
                ExportEditableObjects = true
            };
```

Почему это работает? Когда `ExportEditableObjects` равно `false` (по умолчанию), библиотека растеризует сложные объекты для совместимости, что разрушает **preserve chart formatting**. Включив его, сохраняется оригинальный XML диаграммы, позволяя конечным пользователям открывать PPTX и по‑прежнему редактировать данные диаграммы.

## Шаг 4: Сохраните презентацию, используя настроенные параметры

Теперь мы записываем выходной файл. Перегрузка `Save`, принимающая `SaveFormat` и `exportOptions`, гарантирует, что диаграмма останется редактируемой.

```csharp
            // Step 4: Save the presentation with the configured options
            pres.Save(@"YOUR_DIRECTORY\EditableCharts.pptx", SaveFormat.Pptx, exportOptions);

            // Optional: Inform the user
            Console.WriteLine("Presentation saved with editable charts at: YOUR_DIRECTORY\\EditableCharts.pptx");
        }
    }
}
```

Запуск этой программы создаёт `EditableCharts.pptx`. Откройте его в PowerPoint, щёлкните правой кнопкой мыши по диаграмме, и вы увидите обычную опцию «Edit Data» — доказательство того, что мы успешно освоили **how to preserve charts** и **preserve chart formatting**.

## Шаг 5: Проверьте результат и устраните распространённые проблемы

### Проверка

1. Откройте `EditableCharts.pptx` в PowerPoint.  
2. Щёлкните любую диаграмму → «Edit Data».  
3. Должен появиться лист данных, похожий на Excel, позволяющий изменять значения рядов.

Если вы **видите только** статическое изображение, проверьте следующее:

- Вы используете актуальную версию Aspose.Slides (в старых сборках были баги с `ExportEditableObjects`).  
- Исходный PPTX действительно содержит объекты диаграмм (а не изображения диаграмм).  
- Никакая пользовательская тема или подмена шрифтов не приводит к рендерингу диаграммы как изображения.

### Пограничные случаи

- **Старые PPT (бинарные) файлы:** Сначала конвертируйте их в PPTX (`pres.Save("temp.pptx", SaveFormat.Pptx)`) перед применением параметров экспорта.  
- **Большие презентации:** Потребление памяти может резко возрасти; рассмотрите использование паттерна `Dispose` у `Presentation` или потоковых API для огромных файлов.  
- **Встроенные шрифты:** Если в целевой среде отсутствуют оригинальные шрифты, PowerPoint может переключиться и отобразить диаграмму как изображение. Встроите шрифты в исходный файл или поставьте их вместе с приложением.

---

## Часто задаваемые вопросы (FAQ)

**Q: Работает ли это с файлами PowerPoint 2003 (PPT)?**  
A: Напрямую нет — `ExportEditableObjects` применяется только к формату PPTX. Сначала конвертируйте, затем экспортируйте.

**Q: Могу ли я сохранить другие объекты, такие как SmartArt?**  
A: Конечно. Тот же флаг `ExportEditableObjects` сохраняет SmartArt, таблицы и диаграммы редактируемыми.

**Q: Что если мне нужно сохранить оригинальный размер слайда?**  
A: Размер слайда хранится в метаданных презентации и не зависит от этих параметров. Дополнительный код не требуется.

## Следующие шаги — поддерживайте импульс

Теперь, когда вы освоили **how to preserve charts**, попробуйте исследовать:

- **preserve chart formatting** для конкретных типов диаграмм (например, сложенные столбцы vs. радиальная).  
- Использование API `Chart` для программного изменения данных перед сохранением.  
- Экспорт в другие форматы (PDF, HTML), сохраняя при этом диаграммы редактируемыми в исходном PPTX.  

Каждый из этих пунктов основан на том же принципе: сохранять базовый OOXML нетронутым.

## Заключение

Мы прошли процесс **how to preserve charts** в файле PowerPoint, используя Aspose.Slides для .NET, и продемонстрировали точные шаги **preserve chart formatting**, необходимые для полного редактирования диаграмм. Полный фрагмент кода выше готов к вставке в любой проект C#, а объяснения раскрывают *почему* каждой строки — так что вы не просто копируете‑вставляете, а понимаете.

Попробуйте, настройте параметры экспорта, и вскоре вы будете автоматизировать обновление презентаций, не теряя возможности точно настраивать данные диаграмм. Приятного кодинга!

## Что стоит изучить дальше?

Следующие руководства охватывают тесно связанные темы, которые опираются на техники, продемонстрированные в этом руководстве. Каждый ресурс включает полностью рабочие примеры кода с пошаговыми объяснениями, помогающими освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [How to Export Excel Charts to PDF Using Aspose.Cells for .NET&#58; A Step-by-Step Guide](/cells/english/net/workbook-operations/export-excel-charts-pdf-aspose-cells-net/)
- [How to Convert Excel Charts to SVG Using Aspose.Cells for .NET (Step-by-Step Guide)](/cells/english/net/charts-graphs/convert-excel-chart-to-svg-aspose-cells-net/)
- [How to Create Charts in Excel Using Aspose.Cells for .NET&#58; A Developer's Guide](/cells/english/net/charts-graphs/create-charts-excel-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}