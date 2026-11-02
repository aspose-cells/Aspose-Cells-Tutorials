---
category: general
date: 2026-05-23
description: Встраивание шрифтов в HTML при экспорте Excel в HTML с помощью Aspose.Cells.
  Пошаговое руководство по преобразованию таблицы в HTML с встроенными шрифтами.
draft: false
keywords:
- embed fonts in html
- export excel to html
- convert spreadsheet to html
- save workbook as html
- how to embed fonts html
language: ru
og_description: Встраивание шрифтов в HTML при экспорте Excel в HTML. Узнайте, как
  преобразовать таблицу в HTML с встроенными шрифтами за несколько простых шагов.
og_title: Встраивание шрифтов в HTML – Экспорт Excel в HTML с помощью C#
schemas:
- author: Aspose
  dateModified: '2026-05-23'
  description: Embed fonts in HTML when you export Excel to HTML using Aspose.Cells.
    Step‑by‑step guide to convert spreadsheet to HTML with embedded fonts.
  headline: Embed fonts in HTML – Export Excel to HTML with C#
  type: TechArticle
- description: Embed fonts in HTML when you export Excel to HTML using Aspose.Cells.
    Step‑by‑step guide to convert spreadsheet to HTML with embedded fonts.
  name: Embed fonts in HTML – Export Excel to HTML with C#
  steps:
  - name: 1️⃣ **What if my workbook uses a custom font that isn’t installed on the
      server?**
    text: Aspose.Cells can only embed fonts that are available to the runtime. Install
      the `.ttf` or `.otf` file on the machine running the conversion, or copy it
      into the project directory and register it via `System.Drawing.Text.PrivateFontCollection`
      before invoking the save operation.
  - name: 2️⃣ **Will embedding increase the file size dramatically?**
    text: Yes, each embedded font is Base64‑encoded, which adds roughly 33 % overhead.
      If the workbook uses many large fonts, consider enabling `EmbedOnlyUsedFonts
      = true` to limit the payload to fonts actually referenced in the sheet.
  - name: 3️⃣ **Can I still export images separately?**
    text: Setting `ExportImagesAsBase64 = true` (as shown above) inlines images, making
      the HTML truly self‑contained. If you prefer external image files, set this
      property to `false` and specify `ExportImagesFolder` to control the output folder.
  - name: 4️⃣ **Is this approach compatible with older browsers?**
    text: Most modern browsers (Chrome, Edge, Firefox, Safari) support Base64‑encoded
      `@font-face`. Internet Explorer 11 also works, but you might need to ensure
      the MIME type is correct. For legacy support, consider providing a fallback
      font stack in your CSS.
  - name: 5️⃣ **How does this differ from a simple “export excel to html” without
      embedding?**
    text: A plain export writes the text using generic web fonts (`Arial`, `Helvetica`,
      etc.). The visual layout may shift, especially for corporate reports that rely
      on a brand‑specific typeface. Embedding removes that uncertainty.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Встраивание шрифтов в HTML – Экспорт Excel в HTML с помощью C#
url: /ru/net/exporting-excel-to-html-with-advanced-options/embed-fonts-in-html-export-excel-to-html-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Встраивание шрифтов в HTML – Экспорт Excel в HTML с C#

Задумывались ли вы когда‑нибудь, как **встроить шрифты в HTML** при экспорте книги Excel? Вы не одиноки. Когда вы делитесь таблицей в виде веб‑страницы, отсутствие шрифтов может превратить аккуратный отчёт в неразборчивый беспорядок — особенно если у зрителя не установлен оригинальный шрифт.

В этом руководстве мы пройдём полный, готовый к запуску пример, который покажет вам точно **как встраивать шрифты в HTML** с помощью Aspose.Cells для .NET. К концу вы сможете **экспортировать Excel в HTML**, **преобразовать таблицу в HTML** и **сохранить книгу как HTML** с шрифтами, встроенными непосредственно в файл.

---

## Что вы узнаете

- Почему встроенные шрифты важны для экспорта Excel в веб‑формате.  
- Как настроить `HtmlSaveOptions`, чтобы включить флаг `EmbedFonts`.  
- Полная программа на C#, которая загружает книгу, применяет настройки и записывает HTML‑файл.  
- Советы по работе с пользовательскими шрифтами, совместимости версий и устранению распространённых проблем.  

Предыдущий опыт работы с Aspose.Cells не требуется, но у вас должно быть базовое понимание C# и разработки на .NET.

---

## Требования

| Требование | Почему это важно |
|-------------|----------------|
| **.NET 6.0 or later** | Современная среда выполнения; более старые фреймворки могут не поддерживать новейшие возможности Aspose.Cells. |
| **Aspose.Cells for .NET** (NuGet package `Aspose.Cells`) | Предоставляет необходимый класс `HtmlSaveOptions`. |
| **A TrueType or OpenType font** you want to embed (e.g., `Arial.ttf`) | Только эти форматы шрифтов могут быть встроены в HTML‑файл. |
| **An IDE** (Visual Studio, Rider, VS Code) | Обеспечивает простоту запуска и отладки примера. |

Если вы ещё не установили пакет NuGet, выполните:

```bash
dotnet add package Aspose.Cells
```

---

## Шаг 1: Загрузите книгу, которую хотите преобразовать

Сначала нам нужен экземпляр `Workbook`. Вы можете загрузить существующий файл `.xlsx`, создать его с нуля или даже получить данные из базы данных. Ниже минимальный пример, который открывает файл `Sample.xlsx` из папки проекта:

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Load the source Excel file
        var workbook = new Workbook("Sample.xlsx");
        // Continue with HTML conversion...
```

> **Зачем этот шаг?**  
> `Workbook` — это точка входа для всех операций Aspose.Cells. Без него вы не сможете получить доступ к листам, стилям или данным, которые в конечном итоге будут преобразованы в HTML.

---

## Шаг 2: Настройте параметры сохранения HTML для **встраивания шрифтов в HTML**

Теперь приходит волшебная строка, отвечающая на вопрос «как встроить шрифты в html». Мы создаём экземпляр `HtmlSaveOptions` и устанавливаем `EmbedFonts` в `true`. Это заставляет библиотеку внедрять данные шрифта как CSS‑правила `@font-face`, закодированные в Base64.

```csharp
        // Step 2: Set up HTML save options with embedded fonts
        var htmlOptions = new HtmlSaveOptions
        {
            // This flag ensures fonts are written directly into the HTML file
            EmbedFonts = true,

            // Optional: you can control whether to embed only used fonts
            // EmbedOnlyUsedFonts = true,

            // Optional: control the output folder for external resources
            ExportImagesAsBase64 = true
        };
```

> **Зачем включать `EmbedFonts`?**  
> Когда полученный HTML открывается на машине без оригинального шрифта, браузер переключается на общий шрифт. Встраивание гарантирует визуальную точность на всех платформах.

---

## Шаг 3: Сохраните книгу как HTML

После подготовки параметров мы вызываем `Workbook.Save`, передавая желаемое имя файла и объект `HtmlSaveOptions`. Библиотека выполняет всю тяжёлую работу — преобразует ячейки, формулы и стили в разметку HTML, а затем помещает данные шрифта в теги `<style>`.

```csharp
        // Step 3: Export the workbook to HTML with embedded fonts
        workbook.Save("output.html", htmlOptions);

        // Inform the user
        Console.WriteLine("Workbook successfully saved as HTML with embedded fonts.");
    }
}
```

> **Что вы увидите:**  
> Откройте `output.html` в любом современном браузере, и вы заметите точно такую же типографику, как в оригинальном файле Excel, даже если у зрителя шрифт не установлен локально.

---

## Полный рабочий пример

Объединив всё вместе, представляем полный код программы, который можно скопировать и вставить в консольный проект:

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the source workbook
        var workbook = new Workbook("Sample.xlsx");

        // 2️⃣ Configure HTML save options to embed fonts
        var htmlOptions = new HtmlSaveOptions
        {
            EmbedFonts = true,
            ExportImagesAsBase64 = true,
            // You can also set ExportActiveWorksheetOnly = true if you only need one sheet
        };

        // 3️⃣ Save the workbook as HTML
        workbook.Save("output.html", htmlOptions);

        Console.WriteLine("✅ Workbook saved as HTML with embedded fonts.");
    }
}
```

Запустите программу (`dotnet run`), затем откройте `output.html`. Вы должны увидеть точную копию оригинальной таблицы, включая использованные шрифты.

![Пример вывода HTML с встроенными шрифтами](embed-fonts-html.png "Скриншот, показывающий HTML‑файл со встроенными шрифтами")

*Текст alt изображения: embed fonts in html – скриншот сгенерированной HTML‑страницы, сохраняющей оригинальные шрифты таблицы.*

---

## Часто задаваемые вопросы и особые случаи

### 1️⃣ **Что если моя книга использует пользовательский шрифт, который не установлен на сервере?**  
Aspose.Cells может встраивать только те шрифты, которые доступны среде выполнения. Установите файл `.ttf` или `.otf` на машину, где выполняется конверсия, либо скопируйте его в каталог проекта и зарегистрируйте через `System.Drawing.Text.PrivateFontCollection` перед вызовом операции сохранения.

### 2️⃣ **Увеличит ли встраивание размер файла существенно?**  
Да, каждый встроенный шрифт кодируется в Base64, что добавляет примерно 33 % накладных расходов. Если книга использует много крупных шрифтов, рассмотрите возможность включения `EmbedOnlyUsedFonts = true`, чтобы ограничить нагрузку только шрифтами, действительно используемыми на листе.

### 3️⃣ **Могу ли я всё ещё экспортировать изображения отдельно?**  
Установка `ExportImagesAsBase64 = true` (как показано выше) встраивает изображения, делая HTML полностью автономным. Если вы предпочитаете внешние файлы изображений, установите это свойство в `false` и задайте `ExportImagesFolder` для указания папки вывода.

### 4️⃣ **Совместим ли этот подход со старыми браузерами?**  
Большинство современных браузеров (Chrome, Edge, Firefox, Safari) поддерживают `@font-face`, закодированный в Base64. Internet Explorer 11 также работает, но может потребоваться убедиться, что MIME‑тип правильный. Для поддержки устаревших браузеров рассмотрите возможность предоставления запасного стека шрифтов в вашем CSS.

### 5️⃣ **Чем это отличается от простого «экспорта Excel в HTML» без встраивания?**  
Простой экспорт записывает текст с использованием общих веб‑шрифтов (`Arial`, `Helvetica` и др.). Визуальное оформление может измениться, особенно в корпоративных отчётах, где используется фирменный шрифт. Встраивание устраняет эту неопределённость.

---

## Профессиональные советы и лучшие практики

- **Кешируйте HTML**, если вы генерируете один и тот же отчёт многократно. Процесс конвертации, хотя и быстрый, всё равно потребляет ресурсы процессора.  
- **Проверяйте вывод** с помощью HTML‑валидатора (например, W3C validator), чтобы обнаружить случайные ошибки разметки, которые могут нарушить работу почтовых клиентов.  
- **Комбинируйте с минификацией CSS**, если планируете обслуживать HTML через веб. Встроенные данные шрифтов уже сжаты, но окружающий CSS можно уменьшить.  
- **Обратите внимание на лицензирование**: Aspose.Cells требует действующей лицензии для продакшн‑использования; иначе в выводе HTML появится водяной знак.  
- **Тестируйте на разных устройствах** — особенно на мобильных браузерах — чтобы убедиться, что встроенные шрифты корректно отображаются на разных плотностях экрана.

---

## Заключение

Теперь у вас есть готовое решение для **встраивания шрифтов в HTML**, когда вы **экспортируете Excel в HTML**, **преобразуете таблицу в HTML** или просто **сохраняете книгу как HTML** с полной типографической точностью. Переключив флаг `EmbedFonts` в `HtmlSaveOptions`, вы устраняете проблему «отсутствующего шрифта» и предоставляете любой аудитории аккуратную, автономную веб‑страницу.

Готовы к следующему вызову? Попробуйте добавить **интерактивные диаграммы** в экспорт HTML или поэкспериментировать с **конвертацией в PDF**, чтобы увидеть, как работают встроенные шрифты в другом формате. Тот же шаблон `HtmlSaveOptions` применим — просто измените тип вывода.

Удачной разработки, и пусть ваши таблицы всегда выглядят точно так, как вы задумали — независимо от того, где их просматривают!

## Связанные руководства

- [Преобразование Excel в HTML на Java с использованием Aspose.Cells: пошаговое руководство](/cells/english/java/workbook-operations/convert-excel-html-aspose-cells-java/)
- [Экспорт Excel в HTML с помощью Aspose.Cells Java: пошаговое руководство](/cells/english/java/workbook-operations/export-excel-html-aspose-cells-java/)
- [Преобразование Excel в HTML с подсказками с использованием Aspose.Cells Java: полное руководство](/cells/english/java/workbook-operations/excel-to-html-conversion-with-tooltips-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}