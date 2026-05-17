---
category: general
date: 2026-03-25
description: Узнайте, как внедрять шрифты в HTML при экспорте Excel в HTML. Этот пошаговый
  учебник покажет, как внедрять шрифты в HTML и сохранять книгу в формате HTML.
draft: false
keywords:
- how to embed fonts
- embed fonts in html
- export excel to html
- how to export excel
- save workbook as html
language: ru
og_description: Как встроить шрифты в HTML при экспорте Excel? Следуйте этому руководству,
  чтобы встроить шрифты в HTML, экспортировать Excel в HTML и сохранить книгу как
  HTML с помощью Aspose.Cells.
og_title: Как встроить шрифты в HTML из Excel – Полное руководство
tags:
- Aspose.Cells
- C#
- HTML export
- Font embedding
title: Как внедрить шрифты в HTML из Excel – Полное руководство
url: /ru/net/exporting-excel-to-html-with-advanced-options/how-to-embed-fonts-in-html-from-excel-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как внедрить шрифты в HTML из Excel – Полное руководство

Когда‑то задумывались **как внедрить шрифты** в HTML‑файл, сгенерированный из книги Excel? Вы не одиноки. Многие разработчики сталкиваются с проблемой, когда экспортированный HTML выглядит нормально на их машине, но теряет оригинальную типографику на другом устройстве. Хорошая новость? Решение довольно простое с Aspose.Cells, и вы можете «запекать» шрифты прямо в выводимый HTML.

В этом руководстве мы пройдём по точным шагам **внедрения шрифтов в html**, покажем, как **экспортировать Excel в html**, и, наконец, продемонстрируем, как **сохранить книгу как html** со всеми необходимыми настройками. К концу вы получите готовый HTML‑файл, который отображается точно так же, как исходная таблица — без пропущенных глифов и без резервных шрифтов.

## Предварительные требования

Прежде чем начать, убедитесь, что у вас есть:

- .NET 6.0 или новее (код также работает с .NET Framework)
- Aspose.Cells для .NET (бесплатная пробная версия или лицензия)
- Пример файла Excel (`sample.xlsx`), использующего хотя бы один пользовательский шрифт
- Visual Studio 2022 или любой другой редактор C#, который вам нравится

Дополнительные пакеты NuGet не требуются, кроме Aspose.Cells.

## Шаг 1: Создание проекта и загрузка книги

Первое дело — создать новое консольное приложение и добавить ссылку на Aspose.Cells.

```csharp
using System;
using Aspose.Cells;

namespace ExcelToHtmlWithFonts
{
    class Program
    {
        static void Main(string[] args)
        {
            // Load an existing Excel workbook
            string excelPath = @"C:\Temp\sample.xlsx";
            Workbook workbook = new Workbook(excelPath);
            
            // We'll configure the export options in the next step
        }
    }
}
```

**Почему это важно:** Загрузка книги — фундамент. Если книга загружена неверно, ни одна из последующих настроек внедрения шрифтов не подействует. Кроме того, Aspose.Cells автоматически считывает информацию о шрифтах, хранящуюся в файле, так что вручную указывать имена шрифтов не требуется.

## Шаг 2: Создание HtmlSaveOptions и включение внедрения шрифтов

Теперь создаём экземпляр `HtmlSaveOptions` и включаем флаг `EmbedAllFonts`. Это указывает Aspose.Cells внедрять каждый шрифт, используемый в книге, непосредственно в генерируемый HTML.

```csharp
// Step 2: Create HTML save options
HtmlSaveOptions htmlSaveOptions = new HtmlSaveOptions();

// Enable embedding of all fonts in the output HTML
htmlSaveOptions.EmbedAllFonts = true;

// Optional: Reduce the size of the generated HTML by using base64 encoding
htmlSaveOptions.ExportEmbeddedImages = true;
```

**Почему мы включаем `EmbedAllFonts`:** При экспорте Excel в HTML без этого флага HTML ссылается на шрифты по имени. Если у системы пользователя нет этих шрифтов, браузер переходит к общему шрифту, портя макет. Внедрение гарантирует, что точные глифы идут вместе с HTML‑файлом.

**Совет:** Если вам нужен только подмножество шрифтов (например, вы знаете, что книга использует лишь *Calibri* и *Arial*), вы можете задать `htmlSaveOptions.FontsList` со своей коллекцией. Это может значительно уменьшить размер конечного файла.

## Шаг 3: Сохранение книги как HTML с внедрёнными шрифтами

Наконец, вызываем `Save` у объекта `Workbook`, передавая путь и только что настроенные параметры.

```csharp
// Step 3: Save the workbook as an HTML file with embedded fonts
string htmlPath = @"C:\Temp\embedded.html";
workbook.Save(htmlPath, htmlSaveOptions);

Console.WriteLine($"HTML file with embedded fonts saved to: {htmlPath}");
```

И всё — ваш `embedded.html` теперь содержит блоки `<style>` с определениями `@font-face` и шрифтами, закодированными в base64. Откройте его в любом современном браузере, и вы увидите точно такую же типографику, как в `sample.xlsx`.

### Ожидаемый результат

При открытии `embedded.html`:

- Пользовательский шрифт отображается точно так же, как в Excel.
- Не запрашиваются внешние файлы шрифтов (проверьте вкладку Network в инструментах разработчика — ничего не должно загружаться).
- Размер страницы может быть больше, чем у обычного HTML‑экспорта, но визуальная точность на высоте.

## Экспорт Excel в HTML — Полный пример

Объединяя всё вместе, представляем полностью готовую программу:

```csharp
using System;
using Aspose.Cells;

namespace ExcelToHtmlWithFonts
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the workbook
            string excelPath = @"C:\Temp\sample.xlsx";
            Workbook workbook = new Workbook(excelPath);
            
            // 2️⃣ Configure HTML export options
            HtmlSaveOptions htmlOptions = new HtmlSaveOptions
            {
                EmbedAllFonts = true,          // ✅ Embed every used font
                ExportEmbeddedImages = true,   // ✅ Include images as base64
                ExportChartImageFormat = ImageFormat.Png,
                ExportImagesAsBase64 = true    // ✅ Keep everything in one file
            };
            
            // 3️⃣ Save as HTML
            string htmlPath = @"C:\Temp\embedded.html";
            workbook.Save(htmlPath, htmlOptions);
            
            Console.WriteLine($"✅ HTML with embedded fonts saved at: {htmlPath}");
        }
    }
}
```

**Почему это работает:** Объект `HtmlSaveOptions` — мощный контейнер. Включив `EmbedAllFonts`, вы заставляете Aspose.Cells просканировать коллекцию стилей книги, взять файлы шрифтов из ОС и внедрить их. Флаги `ExportEmbeddedImages` и `ExportImagesAsBase64` делают HTML самодостаточным, что удобно, когда нужно отправить файл по электронной почте или сохранить в базе данных.

## Распространённые подводные камни при внедрении шрифтов в HTML

Даже при правильном коде могут возникнуть небольшие проблемы. Разберём их, пока они не превратились в головную боль.

| Проблема | Почему происходит | Как исправить |
|-------|----------------|------------|
| **Отсутствует шрифт на сервере** | На сервере, где выполняется код, может не быть установлен пользовательский шрифт. | Установите необходимые шрифты на сервере или скопируйте файлы `.ttf/.otf` в известную папку и задайте `htmlSaveOptions.FontsLocation` к этому пути. |
| **Большой HTML‑файл** | Внедрение множества тяжёлых шрифтов может «раздут» HTML (иногда >5 МБ). | Используйте `htmlSaveOptions.FontsList`, чтобы внедрять только нужные шрифты, либо предварительно уменьшите их с помощью инструмента вроде FontForge. |
| **Ограничения лицензии** | Некоторые коммерческие шрифты запрещают внедрение. | Проверьте EULA шрифта. Если внедрение запрещено, используйте веб‑безопасный альтернативный шрифт или конвертируйте лист в PDF. |
| **Совместимость с браузерами** | Очень старые браузеры (IE 8) могут игнорировать `@font-face` с данными base64. | Добавьте резервное CSS‑правило или обслуживайте отдельный CSS‑файл для устаревших браузеров. |
| **Неправильный диапазон Unicode** | Внедрённый шрифт может не содержать всех используемых символов (например, азиатские глифы). | Убедитесь, что исходный шрифт поддерживает нужные блоки Unicode, либо внедрите вторичный шрифт, покрывающий недостающий диапазон. |

## Продвинутое: внедрение только выбранных шрифтов

Если вы знаете, что ваша книга использует лишь *Calibri* и *Times New Roman*, можете ограничить внедрение так:

```csharp
htmlSaveOptions.FontsList = new string[] { "Calibri", "Times New Roman" };
```

Это значительно уменьшит размер HTML, сохраняя внешний вид.

## Тестирование результата

После генерации `embedded.html` выполните быстрые проверки:

1. Откройте файл в Chrome/Edge/Firefox.  
2. Откройте Инструменты разработчика → Сеть → отфильтруйте по **font**. Вы не должны увидеть внешних запросов.  
3. Просмотрите блок `<style>`; там будут правила `@font-face` с `src: url(data:font/ttf;base64,…)`.  
4. Сравните отрисованный текст с оригинальным видом в Excel — пиксель‑совпадение означает успех.

## Итоги

В этом руководстве мы рассмотрели **как внедрять шрифты** в HTML при **экспорте Excel в HTML** с помощью Aspose.Cells. Создав объект `HtmlSaveOptions`, установив `EmbedAllFonts = true` и вызвав `Workbook.Save`, вы получаете самодостаточный HTML‑файл, точно воспроизводящий типографику исходной таблицы. Мы также обсудили типичные подводные камни, приёмы оптимизации и быстрый способ внедрять только необходимые шрифты.

---

### Что дальше?

- **Экспорт Excel в PDF с внедрёнными шрифтами** — идеально для печатных документов.  
- **Конвертация нескольких листов в один HTML‑файл** — изучите `HtmlSaveOptions.OnePagePerSheet`.  
- **Динамическая генерация HTML в ASP.NET Core** — потоковая передача HTML напрямую в браузер без записи на диск.

Экспериментируйте с параметрами, оставляйте комментарии, если столкнётесь с проблемой, и удачной разработки!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}