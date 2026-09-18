---
category: general
date: 2026-02-09
description: Очистите интерфейс фильтра в Excel с помощью C#, удалив кнопку AutoFilter.
  Узнайте, как скрыть кнопку фильтра, отобразить строку заголовка и поддерживать порядок
  в листах.
draft: false
keywords:
- clear filter UI
- remove autofilter excel
- how to remove autofilter
- show header row
- hide filter button
language: ru
og_description: Очистить интерфейс фильтра в Excel с помощью C#. Это руководство показывает,
  как скрыть кнопку фильтра, отобразить строку заголовка и поддерживать чистоту листов.
og_title: Очистка UI фильтра в Excel с C# – Удалить кнопку Автофильтра
tags:
- excel
- csharp
- epplus
- automation
title: Очистка UI фильтра в Excel с помощью C# – Удалить кнопку AutoFilter
url: /ru/net/excel-autofilter-validation/clear-filter-ui-in-excel-with-c-remove-autofilter-button/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Очистка UI фильтра в Excel с C# – Удаление кнопки AutoFilter

Когда‑нибудь вам нужно было **очистить UI фильтра** в листе Excel, но вы не знали, какая строка кода действительно скрывает эту маленькую выпадающую стрелку? Вы не одиноки. Кнопка фильтра может раздражать, когда вы отправляете отчет конечным пользователям, которым никогда не нужно менять представление.  

В этом руководстве мы пройдем полный, исполняемый пример, который **удаляет кнопку AutoFilter** из таблицы, гарантирует, что строка заголовка остаётся видимой, и даже расскажет, как *навсегда скрыть кнопку фильтра*. К концу вы точно узнаете **как удалить AutoFilter** в C# и почему каждый шаг важен.

## Что понадобится

- .NET 6+ (or .NET Framework 4.7.2+) – любой современный рантайм подходит.
- Пакет NuGet **EPPlus** (версия 6.x или новее) – он предоставляет `ExcelWorksheet`, `ExcelTable` и т.д.
- Простой файл Excel с таблицей под названием **SalesTable** (создайте её за несколько кликов).

Вот и всё. Никакого COM‑interop, никаких дополнительных DLL, только несколько операторов `using` и несколько строк кода.

## Очистка UI фильтра: удаление кнопки AutoFilter

Суть решения состоит из трёх небольших операторов. Давайте разберём их, чтобы вы поняли *почему* они нужны, а не только *что* они делают.

### Шаг 1 – Получить ссылку на таблицу

```csharp
// Step 1: Get a reference to the "SalesTable" in the first worksheet
ExcelTable salesTable = package.Workbook.Worksheets[0].Tables["SalesTable"];
```

Почему это важно: EPPlus работает с **таблицами** (`ExcelTable`), а не с обычными диапазонами. Получив объект таблицы, мы получаем доступ к свойству `AutoFilter`, которое управляет элементом UI, видимым на листе. Если пытаться изменять лист напрямую, вы затронете только значения, а не кнопку фильтра.

### Шаг 2 – Удалить строку кнопки AutoFilter

```csharp
// Step 2: Remove the AutoFilter button row (clears any applied filter UI)
salesTable.AutoFilter = null;
```

Установка `AutoFilter` в `null` сообщает EPPlus удалить соответствующую строку фильтра. Это операция *очистки UI фильтра*, которую большинство разработчиков ищут, задавая вопрос «**how to remove autofilter**». Это чистый однострочный подход, работающий с любой версией Excel, поддерживаемой EPPlus.

### Шаг 3 – Сохранить видимость строки заголовка

```csharp
// Step 3: Ensure the header row remains visible after removing the filter
salesTable.ShowHeader = true;
```

Когда вы убираете UI фильтра, Excel иногда может скрыть строку заголовка, если флаг `ShowHeader` у таблицы установлен в `false`. Явно установив его в `true`, мы гарантируем, что названия столбцов останутся на экране – тонкая, но важная деталь для аккуратного финального отчёта.

### Полный, исполняемый пример

Ниже минимальное консольное приложение, которое открывает существующую книгу, выполняет три шага и сохраняет результат. Скопируйте‑вставьте, нажмите **F5**, и наблюдайте, как кнопка фильтра исчезает.

```csharp
using System;
using System.IO;
using OfficeOpenXml;
using OfficeOpenXml.Table;

class Program
{
    static void Main()
    {
        // EPPlus requires a license context for non‑commercial use.
        ExcelPackage.LicenseContext = LicenseContext.NonCommercial;

        // 1️⃣ Load the workbook (replace with your own path)
        var filePath = Path.Combine(Environment.CurrentDirectory, "SalesReport.xlsx");
        if (!File.Exists(filePath))
        {
            Console.WriteLine($"File not found: {filePath}");
            return;
        }

        using var package = new ExcelPackage(new FileInfo(filePath));

        // 2️⃣ Get a reference to the table named "SalesTable"
        ExcelTable salesTable = package.Workbook.Worksheets[0].Tables["SalesTable"];
        if (salesTable == null)
        {
            Console.WriteLine("Table 'SalesTable' not found in the first worksheet.");
            return;
        }

        // 3️⃣ Remove the AutoFilter button (clear filter UI)
        salesTable.AutoFilter = null;

        // 4️⃣ Ensure the header row stays visible (show header row)
        salesTable.ShowHeader = true;

        // 5️⃣ Save the changes to a new file so you don’t overwrite the original
        var outputPath = Path.Combine(Environment.CurrentDirectory, "SalesReport_NoFilter.xlsx");
        package.SaveAs(new FileInfo(outputPath));

        Console.WriteLine($"Filter button removed. Saved to {outputPath}");
    }
}
```

**Ожидаемый результат:** Откройте *SalesReport_NoFilter.xlsx* – стрелки фильтра исчезли, но заголовки столбцов остались. Больше нет «клик‑для‑фильтра» визуального мусора.

> **Совет:** Если у вас **несколько таблиц** и вы хотите скрыть кнопку фильтра для всех, пройдитесь по `worksheet.Tables` и примените те же три строки внутри цикла.

## Как удалить AutoFilter в Excel с помощью C# – более подробно

Вы можете задаться вопросом: «Что если в книге уже применён фильтр? Удалит ли установка `AutoFilter = null` также отфильтрованные строки?» Ответ – **да**. EPPlus очищает как UI, так и базовые критерии фильтра, оставляя данные в исходном порядке.  

Если вы хотите лишь *скрыть* кнопку, но оставить фильтр активным, можно вместо этого установить свойство `AutoFilter` в **новый пустой фильтр**:

```csharp
salesTable.AutoFilter = new ExcelAutoFilter(); // hides button, retains filter logic
```

Этот вариант удобен, когда вы хотите *скрыть кнопку фильтра* для аккуратного вида, но всё же позволить продвинутым пользователям переключать фильтры через VBA или ленту.

### Пограничный случай: Таблицы без строки заголовка

Некоторые устаревшие отчёты используют обычные диапазоны вместо таблиц. В этом случае EPPlus не предоставит объект `ExcelTable`, поэтому приведённый выше код вызовет ошибку. Обходной путь – **преобразовать диапазон в таблицу** сначала:

```csharp
var range = worksheet.Cells["A1:D100"];
var table = worksheet.Tables.Add(range, "TempTable");
table.ShowHeader = true;    // ensure header is visible
table.AutoFilter = null;    // clear filter UI
```

Теперь вы *удалили UI autofilter excel* даже на диапазоне, который изначально не был оформлен как таблица.

## Показ строки заголовка после скрытия кнопки фильтра – почему это важно

Распространённая жалоба: после скрытия UI фильтра строка заголовка иногда исчезает, особенно если книга изначально была создана с включённым параметром «Hide Header». Явно установив `salesTable.ShowHeader = true;`, мы избегаем этого сюрприза.  

Если вам когда‑нибудь понадобится **скрыть кнопку фильтра**, но оставить заголовок скрытым (например, вы генерируете сырые данные), просто установите `salesTable.ShowHeader = false;` после очистки фильтра. Код симметричен, что упрощает переключение на основе флага конфигурации.

## Скрытие кнопки фильтра – практические советы и подводные камни

- **Version compatibility:** EPPlus 6+ работает только с файлами `.xlsx`. Если вы работаете со старым форматом `.xls`, понадобится другая библиотека (например, NPOI), потому что API *clear filter UI* недоступен.
- **Performance:** Загрузка огромной книги только для скрытия одной кнопки может быть медленной. Рассмотрите возможность использования `ExcelPackage.Load(stream, true)` для открытия в режиме **read‑only**, применения изменения, затем сохранения.
- **Testing:** Всегда проверяйте выходной файл вручную при первом запуске. Автоматизированные UI‑тесты могут убедиться, что стрелки фильтра действительно исчезли (`worksheet.Tables[0].AutoFilter == null`).
- **Licensing:** EPPlus перешёл на двойную лицензию в версии 5. Для коммерческих проектов понадобится платная лицензия или переход на альтернативную библиотеку.

## Полный исходный файл для копирования

Ниже точный файл, который вы можете добавить в новый консольный проект. Нет скрытых зависимостей, всё самодостаточно.

```csharp
// File: Program.cs
using System;
using System.IO;
using OfficeOpenXml;
using OfficeOpenXml.Table;

namespace ExcelFilterCleaner
{
    class Program
    {
        static void Main()
        {
            // License context – required for EPPlus 5+
            ExcelPackage.LicenseContext = LicenseContext.NonCommercial;

            // Path to the original workbook (adjust as needed)
            string sourcePath = Path.Combine(Environment.CurrentDirectory, "SalesReport.xlsx");
            if (!File.Exists(sourcePath))
            {
                Console.WriteLine($"Source file not found: {sourcePath}");
                return;
            }

            // Load workbook
            using var package = new ExcelPackage(new FileInfo(sourcePath));

            // Assume the first worksheet contains the table
            var worksheet = package.Workbook.Worksheets[0];
            const string tableName = "SalesTable";

            // Grab the table; abort if missing
            var salesTable = worksheet.Tables[tableName];
            if (salesTable == null)
            {
                Console.WriteLine($"Table '{tableName}' not found.");
                return;
            }

            // ---- Clear filter UI ----
            salesTable.AutoFilter = null;   // removes the filter button row
            salesTable.ShowHeader = true;   // guarantees the header row stays visible

            // Save to a new file so the original stays untouched
            string destPath = Path.Combine(Environment.CurrentDirectory, "SalesReport_NoFilter.xlsx");
            package.SaveAs(new FileInfo(destPath));

            Console.WriteLine($"Successfully cleared filter UI. Output: {destPath}");
        }
    }
}
```

Выполните `dotnet add package EPPlus --version 6.0.8` (или последнюю) перед сборкой, и у вас будет чистый лист, готовый к распространению.

## Заключение

Мы только что продемонстрировали вам **как удалить AutoFilter** и **очистить UI фильтра** в книге Excel с помощью C#. Трёхстрочная ядро (`AutoFilter = null;`, `ShowHeader = true;`) выполняет основную работу, а окружающий шаблон делает решение

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}