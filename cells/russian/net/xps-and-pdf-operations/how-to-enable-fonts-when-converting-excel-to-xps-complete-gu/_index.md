---
category: general
date: 2026-07-03
description: Как включить шрифты при конвертации Excel в XPS с помощью Aspose.Cells.
  Узнайте пошаговую настройку, код и советы для безупречного сохранения шрифтов.
draft: false
keywords:
- how to enable fonts
- convert excel to xps
- Aspose.Cells XPS export
- preserve font variations
- C# Excel automation
language: ru
og_description: Как включить шрифты при конвертации Excel в XPS. Следуйте этому руководству,
  чтобы получить работающий пример на C#, сохраняющий варианты шрифтов.
og_title: Как включить шрифты при конвертации Excel в XPS – Полный учебник
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: How to enable fonts while you convert Excel to XPS using Aspose.Cells.
    Learn step‑by‑step setup, code, and tips for flawless font preservation.
  headline: How to Enable Fonts When Converting Excel to XPS – Complete Guide
  type: TechArticle
- description: How to enable fonts while you convert Excel to XPS using Aspose.Cells.
    Learn step‑by‑step setup, code, and tips for flawless font preservation.
  name: How to Enable Fonts When Converting Excel to XPS – Complete Guide
  steps:
  - name: What Does `FontVariationSelectors = true` Actually Do?
    text: '- **Preserves custom weight & style variations** (e.g., a font that supports
      multiple thicknesses via OpenType features). - **Ensures the XPS viewer renders
      the exact glyphs** you see in Excel, rather than falling back to a generic font.
      - **Adds a small overhead** to the file size because the selec'
  - name: Expected Result
    text: '- The file `WithSelectors.xps` will appear in the target folder. - Open
      it in any XPS viewer (e.g., Windows XPS Viewer or Edge). - You should see the
      same font weights, italics, and any custom OpenType variations that were present
      in the original Excel file.'
  - name: Next Steps
    text: '- Experiment with other `XpsSaveOptions` properties like `Compress` or
      `EmbedStandardFonts`. - Try converting to PDF first, then to XPS, to compare
      file sizes and fidelity. - Dive into Aspose.Cells’ **image handling** (`ImageOrPrintOptions`)
      if your workbook contains charts or pictures you also need'
  type: HowTo
tags:
- Aspose.Cells
- C#
- XPS
- Excel
title: Как включить шрифты при конвертации Excel в XPS – Полное руководство
url: /ru/net/xps-and-pdf-operations/how-to-enable-fonts-when-converting-excel-to-xps-complete-gu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как включить шрифты при конвертации Excel в XPS – Полное руководство

Вы когда‑нибудь задумывались **как включить шрифты**, чтобы ваша конвертация Excel‑в‑XPS выглядела точно так же, как оригинальная рабочая книга? Вы не одиноки. Многие разработчики сталкиваются с проблемой, когда полученный XPS‑файл теряет пользовательские варианты шрифтов, делая документ тусклым.  

В этом руководстве мы пошагово рассмотрим практическое решение, которое не только показывает **как включить шрифты**, но и демонстрирует лучший способ **конвертировать Excel в XPS** с помощью Aspose.Cells. К концу вы получите готовый к запуску фрагмент C#, понятное объяснение каждой настройки и несколько профессиональных советов, чтобы ваш XPS‑вывод был пиксель‑совершенным.

## Что понадобится

Перед тем как приступить, убедитесь, что у вас есть:

- **Aspose.Cells for .NET** (последняя версия на июль 2026).  
- Среда разработки .NET (Visual Studio 2022 или VS Code с расширением C# подойдут).  
- Рабочая книга Excel (`VariationFont.xlsx`), содержащая селекторы вариаций шрифтов, которые вы хотите сохранить.  

И всё — никаких дополнительных пакетов NuGet, никаких сложных COM‑взаимодействий, просто прямой C#.

![Диаграмма, показывающая поток от рабочей книги Excel к документу XPS – как включить шрифты во время конвертации](https://example.com/images/enable-fonts-xps.png "как включить шрифты при конвертации Excel в XPS")

## Шаг 1: Настройка проекта и импорт пространств имён

Сначала создайте новое консольное приложение (или интегрируйте в существующее решение). Добавьте ссылку Aspose.Cells через NuGet:

```bash
dotnet add package Aspose.Cells
```

Затем подключите необходимые пространства имён:

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Drawing;   // optional, for advanced graphics handling
```

> **Pro tip:** Если вы нацеливаетесь на .NET 6+, можете воспользоваться неявным `global using`, чтобы файлы выглядели чище.

## Шаг 2: Загрузка рабочей книги Excel

Загрузка книги — фундамент; без корректного экземпляра `Workbook` вы не сможете изменить параметры сохранения.

```csharp
// Step 2: Load the Excel workbook you want to convert
Workbook workbook = new Workbook("YOUR_DIRECTORY/VariationFont.xlsx");

// Quick sanity check – make sure at least one worksheet is present
if (workbook.Worksheets.Count == 0)
{
    throw new InvalidOperationException("The workbook contains no worksheets.");
}
```

> **Why this matters:** Когда позже вы включаете селекторы вариаций шрифтов, Aspose.Cells нужен полностью инициализированный workbook; иначе параметр будет тихо проигнорирован.

## Шаг 3: Создание и настройка параметров сохранения XPS – Здесь вы **включаете шрифты**

Суть руководства сосредоточена в этом шаге. По умолчанию Aspose.Cells удаляет селекторы вариаций шрифтов, чтобы уменьшить размер XPS‑файла. Чтобы их сохранить, установите `FontVariationSelectors` в `true`.

```csharp
// Step 3: Create XPS save options and enable font variation selectors
XpsSaveOptions xpsOptions = new XpsSaveOptions
{
    // This flag tells Aspose.Cells to keep any OpenType font variation selectors
    FontVariationSelectors = true,

    // Optional: keep the original DPI for sharper rendering (default is 96)
    Dpi = 300
};
```

### Что делает `FontVariationSelectors = true` на самом деле?

- **Сохраняет пользовательские варианты толщины и стиля** (например, шрифт, поддерживающий несколько толщин через функции OpenType).  
- **Гарантирует, что XPS‑просмотрщик отобразит точно такие же глифы**, какие вы видите в Excel, а не заменит их на общий шрифт.  
- **Добавляет небольшое увеличение размера файла**, поскольку данные селектора сохраняются внутри пакета XPS.

Если когда‑нибудь понадобится **конвертировать Excel в XPS** без сохранения этих селекторов, просто установите свойство в `false` (или опустите его, так как `false` — значение по умолчанию).

## Шаг 4: Сохранение рабочей книги как XPS с использованием настроенных параметров

Теперь, когда параметры готовы, вызовите `Save` с перечислением `SaveFormat.Xps` и передайте объект настроек.

```csharp
// Step 4: Save the workbook as an XPS document with the font‑preserving options
string outputPath = "YOUR_DIRECTORY/WithSelectors.xps";
workbook.Save(outputPath, SaveFormat.Xps, xpsOptions);

Console.WriteLine($"Workbook successfully saved to XPS at: {outputPath}");
```

### Ожидаемый результат

- Файл `WithSelectors.xps` появится в целевой папке.  
- Откройте его в любом XPS‑просмотрщике (например, Windows XPS Viewer или Edge).  
- Вы увидите те же толщины шрифтов, курсив и любые пользовательские вариации OpenType, которые присутствовали в исходном файле Excel.

Если шрифты выглядят иначе, проверьте, действительно ли исходный Excel использует шрифт с селекторами вариаций и поддерживает ли ваш просмотрщик их.

## Распространённые ошибки и как их избежать

| Признак | Возможная причина | Решение |
|---------|-------------------|---------|
| Текст отображается общим запасным шрифтом | `FontVariationSelectors` оставлен по умолчанию (`false`) | Установите `xpsOptions.FontVariationSelectors = true`. |
| Размер XPS‑файла неожиданно растёт | Высокое значение DPI в сочетании с селекторами шрифтов | Понизьте `Dpi` до 150 или 96, если важнее размер, а не точность. |
| Исключение «File not found» при создании `Workbook` | Неправильный путь или отсутствующий файл | Используйте абсолютный путь или `Path.Combine(Environment.CurrentDirectory, "VariationFont.xlsx")`. |

## Шаг 5: Проверка конверсии (необязательный автоматический тест)

Если вы автоматизируете сборки, возможно, захотите убедиться, что XPS‑файл существует и не пуст:

```csharp
if (!System.IO.File.Exists(outputPath) || new System.IO.FileInfo(outputPath).Length == 0)
{
    throw new Exception("XPS conversion failed – file is missing or empty.");
}
```

Запуск этой проверки в CI‑конвейере гарантирует, что **как включить шрифты** работает каждый раз при отправке кода.

## Итоги: Что мы рассмотрели

- **Как включить шрифты** при конвертации Excel‑в‑XPS, переключив `FontVariationSelectors`.  
- Полный фрагмент C#, который загружает книгу, настраивает `XpsSaveOptions` и сохраняет результат.  
- Советы по устранению неполадок и проверке конечного документа.  

Теперь вы можете уверенно **конвертировать Excel в XPS**, сохраняя каждую типографскую деталь.

### Следующие шаги

- Поэкспериментируйте с другими свойствами `XpsSaveOptions`, такими как `Compress` или `EmbedStandardFonts`.  
- Попробуйте сначала конвертировать в PDF, а затем в XPS, чтобы сравнить размеры файлов и точность.  
- Изучите **обработку изображений** в Aspose.Cells (`ImageOrPrintOptions`), если ваша книга содержит диаграммы или картинки, которые тоже нужно сохранить.

Есть вопросы о более продвинутых сценариях — например, встраивании пользовательских шрифтов, не установленных на целевой машине? Оставьте комментарий ниже, и счастливого кодинга!

## Что изучать дальше?

Следующие руководства охватывают тесно связанные темы, построенные на техниках, продемонстрированных в этом гиде. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы в собственных проектах.

- [Как задать стили шрифтов в Excel с помощью Aspose.Cells for .NET (пошаговое руководство)](/cells/english/net/formatting/aspose-cells-dotnet-set-font-styles-excel/)
- [Как извлечь шрифты из файлов Excel с помощью Aspose.Cells for .NET](/cells/english/net/formatting/extract-fonts-excel-aspose-cells-dotnet-guide/)
- [Как конвертировать листы Excel в изображения с помощью Aspose.Cells .NET (пошаговое руководство)](/cells/english/net/workbook-operations/convert-excel-sheets-images-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}