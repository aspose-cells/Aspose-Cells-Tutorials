---
category: general
date: 2026-03-29
description: Узнайте, как экспортировать таблицы Excel в обычный текст, записывать
  строку в файл и преобразовывать таблицу Excel в CSV или TXT с помощью C#. Включает
  полный код и рекомендации.
draft: false
keywords:
- how to export excel
- write string to file
- convert excel table
- export table as csv
- save txt file c#
language: ru
og_description: Как экспортировать таблицы Excel в текстовые файлы на C#. Получите
  полное решение, код и лучшие практики по конвертации таблиц Excel и сохранению файлов
  TXT.
og_title: Как экспортировать данные Excel – Полный учебник по C#
tags:
- C#
- Excel
- File I/O
title: Как экспортировать данные Excel — пошаговое руководство по C#
url: /ru/net/excel-data-export-retrieval/how-to-export-excel-data-step-by-step-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как экспортировать данные Excel – Полное руководство на C#

Когда‑нибудь задавались вопросом **как экспортировать Excel**‑данные без ручного открытия таблицы? Возможно, вам нужно выгрузить таблицу в простой текстовый файл для устаревшей системы, или вам нужен быстрый экспорт CSV для конвейеров анализа данных. В этом руководстве мы пройдем практическое, сквозное решение, которое **записывает строку в файл** и покажет, как **преобразовать таблицу Excel** в разделённый текстовый формат с помощью C#.

Мы рассмотрим всё: от загрузки книги, выбора нужной таблицы, настройки параметров экспорта и, наконец, сохранения результата в файл `.txt`. К концу вы сможете **экспортировать таблицу как CSV** (или любой другой разделитель) и увидите несколько полезных приёмов для **сохранения txt файла C#** проектов. Никаких внешних инструментов — только несколько пакетов NuGet и немного кода.

---

## Что понадобится

- **.NET 6.0+** (или .NET Framework 4.7.2, если предпочитаете классический вариант)
- NuGet‑пакет **Syncfusion.XlsIO** (класс `ExportTableOptions` находится здесь)
- Любая базовая IDE для C# (Visual Studio, VS Code, Rider — подойдёт любая)
- Excel‑книга, содержащая хотя бы одну таблицу (в примере будем использовать `ws.Tables[0]`)

> Подсказка: если у вас ещё нет библиотеки Syncfusion, выполните  
> `dotnet add package Syncfusion.XlsIO.Net.Core` в командной строке.

---

## Шаг 1 – Открыть книгу и получить первую таблицу  

Первым делом нужно загрузить файл Excel и получить ссылку на лист, где находится таблица. Этот шаг критичен, потому что операция **convert excel table** работает с объектом `ITable`, а не с диапазоном ячеек.

```csharp
using Syncfusion.XlsIO;
using System.IO;

class ExcelExporter
{
    static void Main()
    {
        // Load the workbook (replace with your actual file path)
        using (ExcelEngine excelEngine = new ExcelEngine())
        {
            IApplication application = excelEngine.Excel;
            application.DefaultVersion = ExcelVersion.Xlsx;

            // Open the file
            FileStream stream = new FileStream(@"C:\Data\Sample.xlsx", FileMode.Open, FileAccess.Read);
            IWorkbook workbook = application.Workbooks.Open(stream);
            IWorksheet ws = workbook.Worksheets[0];   // First worksheet
```

*Почему это важно:* Открытие книги с помощью `using` гарантирует освобождение всех неуправляемых ресурсов, предотвращая проблемы с блокировкой файла позже, когда вы попытаетесь **write string to file**.

---

## Шаг 2 – Настроить параметры экспорта (обычный текст, без заголовков, разделитель‑точка с запятой)  

Теперь указываем Syncfusion, как сериализовать таблицу. `ExportTableOptions` позволяет включать/исключать заголовки, выбирать разделитель и решать, получать строку или массив байтов.

```csharp
            // Step 2: Configure export options – plain text, omit headers, ';' delimiter
            var exportOptions = new ExportTableOptions
            {
                ExportAsString = true,      // Returns a string we can write directly
                IncludeHeaders = false,     // Skip column headers if you don’t need them
                Delimiter = ";"             // Change to ',' for classic CSV
            };
```

*Почему это важно:* Установка `IncludeHeaders = false` часто соответствует требованиям downstream‑систем, которые уже знают порядок колонок. Изменение разделителя — это способ **export table as CSV** с пользовательским разделителем.

---

## Шаг 3 – Экспортировать таблицу в строку  

С готовыми параметрами вызываем `ExportToString`. Этот метод извлекает всю таблицу (со всеми строками) и возвращает одну строку, готовую к записи в файл.

```csharp
            // Step 3: Export the first table to a string using the configured options
            ITable firstTable = ws.Tables[0];               // Access the first table
            string tableText = firstTable.ExportToString(exportOptions);
```

*Почему это важно:* Вызов `ExportToString` делает тяжёлую работу по преобразованию сетки Excel в разделённый формат. Он учитывает установленный `Delimiter`, поэтому вы получаете чистый **export table as csv**‑результат без дополнительной обработки.

---

## Шаг 4 – Записать экспортированный текст в файл  

Наконец, сохраняем строку на диск. `File.WriteAllText` — самый простой способ **save txt file C#**; он автоматически создаёт файл, если его нет, и перезаписывает его в противном случае.

```csharp
            // Step 4: Write the exported text to a file
            string outputPath = @"C:\Data\ExportedTable.txt";
            File.WriteAllText(outputPath, tableText);
            System.Console.WriteLine($"Table exported successfully to {outputPath}");
        }
    }
}
```

*Почему это важно:* Записывая строку напрямую, вы избегаете лишнего шага преобразования. Файл теперь содержит строки вида `Value1;Value2;Value3`, готовые для любого downstream‑парсера.

---

## Полный рабочий пример (все шаги в одном месте)  

Ниже представлена готовая к копированию программа, объединяющая всё обсуждённое. В ней есть обработка ошибок и комментарии для ясности.

```csharp
using Syncfusion.XlsIO;
using System;
using System.IO;

class ExcelExporter
{
    static void Main()
    {
        try
        {
            // 1️⃣ Load workbook and get first worksheet
            using (ExcelEngine excelEngine = new ExcelEngine())
            {
                IApplication app = excelEngine.Excel;
                app.DefaultVersion = ExcelVersion.Xlsx;

                string sourcePath = @"C:\Data\Sample.xlsx";
                using (FileStream fs = new FileStream(sourcePath, FileMode.Open, FileAccess.Read))
                {
                    IWorkbook wb = app.Workbooks.Open(fs);
                    IWorksheet ws = wb.Worksheets[0]; // first sheet

                    // 2️⃣ Set export options (plain text, no headers, ';' delimiter)
                    var opts = new ExportTableOptions
                    {
                        ExportAsString = true,
                        IncludeHeaders = false,
                        Delimiter = ";"
                    };

                    // 3️⃣ Export the first table to a string
                    ITable table = ws.Tables[0];
                    string csvText = table.ExportToString(opts);

                    // 4️⃣ Save the string to a .txt file
                    string destPath = @"C:\Data\ExportedTable.txt";
                    File.WriteAllText(destPath, csvText);

                    Console.WriteLine($"✅ Export complete! File saved at: {destPath}");
                }
            }
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"❌ Something went wrong: {ex.Message}");
        }
    }
}
```

**Ожидаемый вывод** (содержимое `ExportedTable.txt`):

```
John;Doe;35
Jane;Smith;28
Bob;Brown;42
```

Каждая строка соответствует строке из исходной таблицы Excel, значения разделены точкой с запятой. Если изменить `Delimiter = ","`, вы получите классический CSV‑файл.

---

## Часто задаваемые вопросы и особые случаи  

### Что делать, если в книге несколько таблиц?  
Просто замените `ws.Tables[0]` на нужный индекс или пройдитесь в цикле по `ws.Tables`:

```csharp
foreach (var tbl in ws.Tables)
{
    string txt = tbl.ExportToString(opts);
    // Save each table to a separate file or concatenate as needed
}
```

### Как включить заголовки столбцов?  
Установите `IncludeHeaders = true` в `ExportTableOptions`. Это полезно, когда downstream‑система ожидает строку заголовков.

### Можно ли экспортировать в другую папку динамически?  
Конечно. Используйте `Path.Combine` вместе с `Environment.GetFolderPath(Environment.SpecialFolder.Desktop)` или любой путь, предоставленный пользователем, чтобы сделать решение более гибким.

### Что с большими файлами?  
Для огромных таблиц рассмотрите потоковую запись вместо загрузки всей строки в память:

```csharp
using (StreamWriter writer = new StreamWriter(outputPath))
{
    writer.Write(table.ExportToString(opts));
}
```

### Работает ли это на .NET Core?  
Да — Syncfusion.XlsIO поддерживает .NET 5/6/7. Просто подключите соответствующий NuGet‑пакет, и всё готово.

---

## Советы для надёжного экспорта  

- **Проверяйте путь к файлу** перед записью. Отсутствующая директория вызовет `DirectoryNotFoundException`.  
- **Используйте `ExportAsString`** только когда таблица удобно помещается в память; иначе применяйте `ExportToStream` для огромных наборов данных.  
- **Учитывайте культуру**: если в данных есть запятые как десятичные разделители, выбирайте точку с запятой (`;`) или табуляцию (`\t`), чтобы избежать ошибок парсинга CSV.  
- **Фиксируйте версию**: Syncfusion иногда меняет сигнатуры API. Зафиксируйте версию NuGet (`<PackageReference Include="Syncfusion.XlsIO.Net.Core" Version="21.2.0.44" />`), чтобы сборка оставалась воспроизводимой.

---

## Заключение  

В этом руководстве мы продемонстрировали, **как экспортировать Excel**‑таблицы в обычные текстовые файлы с помощью C#. Загрузив книгу, настроив `ExportTableOptions`, экспортировав таблицу в строку и, наконец, **записав строку в файл**, вы получили надёжный шаблон для задач **convert excel table**, **export table as csv** и **save txt file C#**.  

Экспериментируйте — меняйте разделитель, включайте заголовки или обрабатывайте несколько таблиц. Такой же подход подходит для генерации CSV‑отчётов, передачи данных в устаревшие парсеры или простого архивирования содержимого таблиц в лёгкие текстовые файлы.

Есть другие сценарии, которые хотите решить? Может, вам нужно **write string to file** асинхронно, или вы хотите архивировать вывод «на лету». Ознакомьтесь с нашими следующими руководствами по *asynchronous file I/O in C#* и *zipping files with .NET*, чтобы продолжить развитие.

Удачной разработки! 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}