---
category: general
date: 2026-02-09
description: Узнайте, как встраивать шрифты в HTML при экспорте Excel в HTML с помощью
  Aspose.Cells. Этот пошаговый учебник также охватывает преобразование Excel в HTML
  и экспорт Excel со встроенными шрифтами.
draft: false
keywords:
- how to embed fonts
- embed fonts in html
- export excel to html
- convert excel to html
- how to export excel
language: ru
og_description: Как встроить шрифты в HTML при экспорте Excel. Следуйте этому полному
  руководству, чтобы преобразовать Excel в HTML с встроенными шрифтами, используя
  Aspose.Cells.
og_title: Как встроить шрифты в HTML – Руководство по экспорту Excel в HTML
tags:
- Aspose.Cells
- C#
- Excel
- HTML
title: Как встроить шрифты в HTML при экспорте из Excel – полное руководство
url: /ru/net/exporting-excel-to-html-with-advanced-options/how-to-embed-fonts-in-html-when-exporting-excel-complete-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как внедрить шрифты в HTML при экспорте Excel – Полное руководство

Вы когда‑нибудь задавались вопросом **how to embed fonts in HTML**, преобразуя книгу Excel в готовую к вебу страницу? Вы не одиноки. Многие разработчики сталкиваются с тем, что сгенерированный HTML выглядит нормально на их машине, но в браузере отображается с общими запасными шрифтами. Хорошая новость? С несколькими строками C# и правильными параметрами сохранения вы можете отправить точную типографику, которую спроектировали в Excel.

В этом руководстве мы пройдём процесс экспорта файла Excel в HTML **with embedded fonts**, используя Aspose.Cells for .NET. По пути мы также коснёмся основ *export excel to html*, покажем, как *convert excel to html* в разных сценариях, и ответим на неизбежные вопросы «**how to export excel**», которые появляются на форумах.

## Что вы получите

- Полностью рабочее консольное приложение C#, которое сохраняет книгу `.xlsx` как `embedded.html`.
- Объяснение, почему внедрение шрифтов важно для кросс‑браузерного соответствия.
- Советы по работе с лицензированием шрифтов, большими книгами и производительностью.
- Краткие рекомендации по альтернативным способам *export excel to html*, если вы не используете Aspose.Cells.

### Предварительные требования

- .NET 6.0 или новее (код также работает на .NET Framework 4.7+).
- Aspose.Cells for .NET, установленный через NuGet (`Install-Package Aspose.Cells`).
- Базовое понимание C# и модели объектов Excel.
- Шрифт TrueType (`.ttf`) или OpenType (`.otf`), на который у вас есть право внедрения.

Никакой тяжёлой настройки, без COM‑interop, только несколько пакетов NuGet и текстовый редактор.

---

## Как внедрить шрифты в HTML – Шаг 1: Подготовьте книгу

Прежде чем мы сможем сказать Aspose.Cells внедрять шрифты, нам нужна книга, которая действительно использует пользовательский шрифт. Создадим небольшую книгу в памяти, применим к ячейке нестандартный шрифт и сохраним её.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Saving;   // Needed for HtmlSaveOptions

// Step 1: Create a new workbook and access the first worksheet
Workbook workbook = new Workbook();
Worksheet sheet = workbook.Worksheets[0];

// Step 2: Insert some text and apply a custom font (e.g., "Comic Sans MS")
Style style = workbook.CreateStyle();
style.Font.Name = "Comic Sans MS";   // This font is usually not available on all browsers
style.Font.Size = 14;
style.Font.IsBold = true;

// Apply the style to cell A1
Cell cell = sheet.Cells["A1"];
cell.PutValue("Hello, embedded fonts!");
cell.SetStyle(style);

// Save the workbook as an intermediate .xlsx (optional, just for inspection)
workbook.Save("sample.xlsx");
```

**Почему это важно:** Если книга никогда не ссылается на пользовательский шрифт, у Aspose.Cells нечего внедрять. Явно задавая `style.Font.Name`, мы заставляем экспортер искать файл шрифта в системе и включать его в HTML‑вывод.

> **Pro tip:** Всегда тестируйте шрифтом, который не гарантировано присутствует на целевых машинах. Системные шрифты, такие как Arial, не продемонстрируют возможность внедрения.

## Как внедрить шрифты в HTML – Шаг 2: Настройте параметры сохранения HTML

Теперь приходит волшебная строка, отвечающая на главный вопрос: *how to embed fonts in HTML*.

```csharp
// Step 3: Create HtmlSaveOptions and enable font embedding
HtmlSaveOptions htmlOptions = new HtmlSaveOptions
{
    // Setting this flag tells Aspose.Cells to embed all referenced fonts as base‑64 data URIs
    EmbedFonts = true,

    // Optional: Reduce file size by embedding only the characters actually used
    EmbedFontSubset = true,

    // Optional: Choose a folder for external resources (images, CSS)
    ExportImagesAsBase64 = true
};
```

- `EmbedFonts = true` делает основную работу; он сканирует книгу в поисках любых ссылок на шрифты, находит соответствующие файлы `.ttf`/`.otf` и внедряет их непосредственно в сгенерированный HTML‑блок `<style>`.
- `EmbedFontSubset = true` ускоряет работу — в пакет попадают только те глифы, которые действительно используются, что делает итоговый HTML более лёгким.
- `ExportImagesAsBase64` удобно, когда у вас есть диаграммы или картинки; всё оказывается в одном файле, что идеально для электронной почты или быстрых демонстраций.

## Как внедрить шрифты в HTML – Шаг 3: Сохраните книгу

Наконец, вызываем `Save` с только что настроенными параметрами.

```csharp
// Step 4: Export the workbook to HTML with embedded fonts
string outputPath = "embedded.html";
workbook.Save(outputPath, htmlOptions);

Console.WriteLine($"Workbook exported with embedded fonts to: {outputPath}");
```

После завершения выполнения откройте `embedded.html` в любом современном браузере. Вы должны увидеть текст, отрисованный шрифтом *Comic Sans MS*, даже если шрифт не установлен локально. Браузер читает блок `<style>`, содержащий правило `@font-face` с полезной нагрузкой `data:font/ttf;base64,...` — именно то, что нам нужно.

![HTML‑output с внедрёнными шрифтами](embed-fonts-html.png "Скриншот, показывающий как внедрить шрифты в HTML")

*Текст alt изображения:* **how to embed fonts in HTML** – скриншот сгенерированной страницы с применённым пользовательским шрифтом.

---

## Export Excel to HTML – Альтернативные подходы

Если вы не привязаны к Aspose.Cells, существуют и другие способы *export excel to html*:

| Библиотека / Инструмент | Поддержка внедрения шрифтов | Краткое примечание |
|------------------------|-----------------------------|--------------------|
| **ClosedXML** | Нет встроенного внедрения шрифтов | Генерирует простой HTML; вам нужно вручную добавить `@font-face`. |
| **EPPlus** | Нет внедрения шрифтов | Хорошо подходит для таблиц данных, но теряется стилизация. |
| **Office Interop** | Может внедрять шрифты через `SaveAs` с `xlHtmlStatic` | Требует установленный Excel на сервере — обычно не рекомендуется. |
| **LibreOffice CLI** | Может внедрять шрифты с флагом `--embed-fonts` | Работает кросс‑платформенно, но добавляет тяжёлую зависимость. |

Когда нужен надёжный серверный вариант без установки Office, Aspose.Cells остаётся самым простым путём к *convert excel to html* с внедрёнными шрифтами.

## Как экспортировать Excel – Частые проблемы и их решения

1. **Отсутствие файлов шрифтов** – Если целевой шрифт не установлен на машине, где выполняется код, Aspose.Cells тихо пропускает внедрение, и HTML переходит к общему шрифту.  
   *Решение:* Установите шрифт на сервере или скопируйте файлы `.ttf`/`.otf` рядом с исполняемым файлом и задайте `FontSources` вручную:

   ```csharp
   FontSources.AddFolder(@"C:\MyFonts");
   ```

2. **Ограничения лицензии** – Некоторые коммерческие шрифты запрещают внедрение.  
   *Решение:* Проверьте EULA шрифта. Если внедрение запрещено, выберите другой шрифт или разместите файл шрифта самостоятельно с правильной лицензией.

3. **Большие книги** – Внедрение множества шрифтов может сильно увеличить размер HTML.  
   *Решение:* Используйте `EmbedFontSubset = true` (как показано выше) или ограничьте книгу только нужными листами перед экспортом.

4. **Совместимость браузеров** – Старые браузеры (IE 8 и ниже) не понимают base‑64 `@font-face`.  
   *Решение:* Добавьте запасное CSS‑правило, которое ссылается на веб‑доступную версию шрифта `.woff`.

## Convert Excel to HTML – Проверка результата

После запуска примера откройте `embedded.html` и найдите блок `<style>`, начинающийся примерно так:

```html
<style type="text/css">
@font-face {
    font-family: 'Comic Sans MS';
    src: url('data:font/ttf;base64,AAEAAAALAIAAAwAwT1MvMg8S...') format('truetype');
}
...
</style>
```

Если вы видите URL‑адрес `data:`, внедрение прошло успешно. Тело страницы будет содержать что‑то вроде:

```html
<div class="c0">Hello, embedded fonts!</div>
```

Текст должен отображаться точно так же, как в Excel, независимо от установленных у клиента шрифтов.

---

## Часто задаваемые вопросы (FAQ)

**В: Работает ли это с формулами Excel?**  
О: Абсолютно. Формулы вычисляются до генерации HTML, поэтому отображаемые значения — статические строки, как и при обычном экспорте.

**В: Можно ли внедрять шрифты при экспорте в ZIP‑пакет вместо одного HTML‑файла?**  
О: Да. Установите `htmlOptions.ExportToSingleFile = false`, и Aspose.Cells создаст папку с отдельными CSS‑ и файловыми шрифтами, что некоторым командам удобнее для контроля версий.

**В: Что если мне нужно внедрить**  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}