---
category: general
date: 2026-08-11
description: Экспорт Excel в txt на C# с пошаговым руководством. Узнайте, как преобразовать
  xlsx в обычный текст с помощью Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to txt
- convert xlsx to plain text
- how to export excel worksheet as text
- export worksheet as text file
language: ru
lastmod: 2026-08-11
og_description: Быстрый экспорт Excel в txt на C#. Этот учебник показывает, как преобразовать
  xlsx в обычный текст, настроить форматы и работать с большими листами.
og_image_alt: Code snippet that exports an Excel worksheet to a plain text file using
  C#
og_title: Экспорт Excel в TXT в C# – пошаговое руководство для разработчиков
schemas:
- author: Aspose
  dateModified: '2026-08-11'
  description: Export excel to txt in C# with a step-by-step guide. Learn how to convert
    xlsx to plain text using Aspose.Cells.
  headline: Export excel to txt in C# – complete programming guide
  type: TechArticle
- description: Export excel to txt in C# with a step-by-step guide. Learn how to convert
    xlsx to plain text using Aspose.Cells.
  name: Export excel to txt in C# – complete programming guide
  steps:
  - name: – load the workbook
    text: '```csharp using Aspose.Cells;'
  - name: – get the first worksheet
    text: '```csharp Worksheet sheet = workbook.Worksheets[0]; ```'
  - name: – define export options for text conversion
    text: '```csharp ExportTableOptions exportOptions = new ExportTableOptions { ExportAsString
      = true, // Export all values as text DateTimeFormat = "yyyy-MM-dd", // Desired
      date format NumberFormat = "#,##0.00" // Desired numeric format }; ```'
  - name: – export worksheet as text file
    text: '```csharp // Apply the options to the worksheet sheet.ExportTableOptions
      = exportOptions;'
  type: HowTo
tags:
- excel
- csharp
- text export
- aspose.cells
title: Экспорт Excel в TXT в C# – полное руководство по программированию
url: /ru/net/converting-excel-files-to-other-formats/export-excel-to-txt-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Экспорт Excel в TXT на C# – полное руководство по программированию

Если вам нужно **экспортировать Excel в TXT**, вы можете достичь результата несколькими строками кода C#. Это руководство показывает, как преобразовать книгу `.xlsx` в обычный текстовый файл, сохраняя заданный вами формат данных.

Экспорт листов как текстовых файлов часто требуется, когда downstream‑системы принимают только разделённые данные или когда необходимо проанализировать сырые значения ячеек. В следующих разделах вы узнаете, как настроить форматы дат и чисел, работать с большими листами и избегать типичных подводных камней.

## Предварительные требования для преобразования xlsx в обычный текст

Перед началом убедитесь, что у вас есть:

* .NET 6.0 (или новее) установлен – код нацелен на .NET Standard 2.0, поэтому работает и с .NET Framework 4.6+.
* Лицензия на **Aspose.Cells** (бесплатная оценочная версия подходит для тестирования).
* IDE, например Visual Studio 2022 или Visual Studio Code.
* Файл Excel с именем `input.xlsx`, размещённый в папке, к которой ваш проект может обратиться.

Эти элементы являются единственными внешними требованиями; руководство не зависит от дополнительных пакетов NuGet.

## Как экспортировать Excel в TXT с помощью Aspose.Cells

Aspose.Cells предоставляет класс `ExportTableOptions`, который позволяет управлять тем, как значения ячеек преобразуются в строки. Установив `ExportAsString` в `true`, вы заставляете каждую ячейку записываться как текст, что необходимо для детерминированного текстового вывода.

### Шаг 1 – загрузить книгу

```csharp
using Aspose.Cells;

string inputPath = @"YOUR_DIRECTORY\input.xlsx";
Workbook workbook = new Workbook(inputPath);
```

*Конструктор `Workbook` читает файл Excel в память. Если файл не существует, генерируется исключение, поэтому в продакшн‑коде рекомендуется обернуть вызов в блок try‑catch.*

### Шаг 2 – получить первый лист

```csharp
Worksheet sheet = workbook.Worksheets[0];
```

*Листы нумеруются с нуля, поэтому индекс 0 относится к первой вкладке. При необходимости можно заменить индекс именем листа (`workbook.Worksheets["Sheet1"]`).*

### Шаг 3 – определить параметры экспорта для текстового преобразования

```csharp
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true,               // Export all values as text
    DateTimeFormat = "yyyy-MM-dd",       // Desired date format
    NumberFormat   = "#,##0.00"          // Desired numeric format
};
```

*`ExportAsString` гарантирует, что каждая ячейка, независимо от исходного типа, станет строкой в выходном файле. Свойства `DateTimeFormat` и `NumberFormat` позволяют контролировать отображение дат и чисел, что критично при **преобразовании xlsx в обычный текст** для систем, ожидающих определённый шаблон.*

### Шаг 4 – экспортировать лист как текстовый файл

```csharp
// Apply the options to the worksheet
sheet.ExportTableOptions = exportOptions;

// Export the data to a tab‑delimited text file
string outputPath = @"YOUR_DIRECTORY\Exported.txt";
sheet.ExportDataTable(outputPath);
```

*`ExportDataTable` записывает содержимое листа в обычный текстовый файл, используя указанные параметры. Делимитер по умолчанию – символ табуляции (`\t`). Если нужен иной делимитер, используйте перегрузку, принимающую экземпляр `ExportTableOptions`, и укажите `ExportTableOptions.Separator`. Полученный файл можно открыть в любом текстовом редакторе или импортировать в базу данных.*

#### Ожидаемый результат

Предположим, `input.xlsx` содержит:

| A            | B       | C            |
|--------------|---------|--------------|
| 2023‑05‑01   | 1234.5  | Пример текста|

С указанными выше параметрами файл `Exported.txt` будет содержать:

```
2023-05-01	1,234.50	Sample text
```

Каждый столбец разделён табуляцией, даты имеют формат `yyyy‑MM‑dd`, а числа используют запятую как разделитель тысяч и два знака после запятой.

## Распространённые подводные камни при экспорте листа как текстового файла

| Проблема | Почему происходит | Как избежать |
|----------|-------------------|--------------|
| Зависимое от локали форматирование чисел | По умолчанию формат учитывает культуру ОС, что может приводить к непоследовательному использованию запятых или точек. | Явно задайте `NumberFormat` в `ExportTableOptions`. |
| Скрытые строки или столбцы появляются в выводе | Aspose.Cells экспортирует весь используемый диапазон, включая скрытые строки. | Установите `ExportTableOptions.ExportHiddenRows = false` и `ExportHiddenColumns = false`, если хотите их пропустить. |
| Большие листы вызывают нагрузку на память | Вся книга загружается в память перед экспортом. | Используйте `Workbook.LoadOptions` с `LoadDataOnly = true` для снижения использования памяти или обрабатывайте файл частями. |
| Ячейки с датами хранятся как текст в исходном файле | Если ячейка уже содержит отформатированную строку, экспортер рассматривает её как текст и игнорирует `DateTimeFormat`. | Убедитесь, что исходная книга хранит даты как корректные типы Excel. |

Устранение этих проблем делает процесс **как экспортировать лист Excel как текст** надёжным в разных средах.

## Расширение решения – пользовательские разделители и потоковый экспорт

Если нужен файл CSV (значения, разделённые запятыми) вместо табуляции, измените параметры:

```csharp
exportOptions.Separator = ',';
exportOptions.ExportHiddenRows = false;   // optional
exportOptions.ExportHiddenColumns = false; // optional
sheet.ExportTableOptions = exportOptions;
sheet.ExportDataTable(@"YOUR_DIRECTORY\Exported.csv");
```

Для файлов размером более 500 МБ потоковая запись вывода предотвращает исчерпание ОЗУ:

```csharp
using (FileStream stream = new FileStream(@"YOUR_DIRECTORY\LargeExport.txt",
                                          FileMode.Create,
                                          FileAccess.Write,
                                          FileShare.None,
                                          bufferSize: 81920,
                                          useAsync: true))
{
    sheet.ExportDataTable(stream, exportOptions);
}
```

Перегрузка, принимающая `Stream`, записывает строки по‑инкрементно, что идеально подходит для пакетных задач или веб‑сервисов, возвращающих текстовый файл напрямую клиенту.

## Проверка результата программно

После завершения экспорта вы можете прочитать первую строку обратно в память, чтобы подтвердить формат:

```csharp
string firstLine = File.ReadLines(outputPath).First();
Console.WriteLine($"First line: {firstLine}");
```

Запуск этого фрагмента кода должен вывести ту же строку, что показана в разделе *Ожидаемый результат*, давая уверенность в успешном преобразовании.

## Итоги полного кода

Собрав все части вместе, получаем автономную программу, которую можно скопировать в консольное приложение:

```csharp
using System;
using System.IO;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Paths – adjust to your environment
        string inputPath  = @"YOUR_DIRECTORY\input.xlsx";
        string outputPath = @"YOUR_DIRECTORY\Exported.txt";

        // Load workbook
        Workbook workbook = new Workbook(inputPath);
        Worksheet sheet = workbook.Worksheets[0];

        // Configure export options
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            DateTimeFormat = "yyyy-MM-dd",
            NumberFormat   = "#,##0.00",
            Separator      = '\t' // tab delimiter
        };

        // Apply options and export
        sheet.ExportTableOptions = exportOptions;
        sheet.ExportDataTable(outputPath);

        // Simple verification
        string firstLine = File.ReadLines(outputPath).First();
        Console.WriteLine($"Export completed. First line: {firstLine}");
    }
}
```

Скомпилируйте и запустите программу; файл `Exported.txt` появится в той же директории, что и исходная книга.

## Следующие шаги и смежные темы

* **Экспорт листа как текстовый файл** – экспериментируйте с различными разделителями, кодировками (UTF‑8 vs. ASCII) и стилями окончания строк для кроссплатформенной совместимости.
* **Массовое преобразование** – перебирайте `workbook.Worksheets`, чтобы создать отдельный текстовый файл для каждой вкладки.
* **Интеграция с базами данных** – передавайте сгенерированный текст напрямую в операцию bulk‑insert для SQL Server или PostgreSQL.
* 

## Что вам стоит изучить дальше?

Следующие руководства охватывают тесно связанные темы, построенные на техниках, продемонстрированных в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, помогающими освоить дополнительные возможности API и исследовать альтернативные подходы в ваших проектах.

- [Как экспортировать файлы Excel в .NET с помощью Aspose.Cells: Полное руководство](/cells/english/net/workbook-operations/export-excel-files-net-aspose-cells-guide/)
- [Как экспортировать видимые строки Excel с помощью Aspose.Cells для .NET: Пошаговое руководство](/cells/english/net/workbook-operations/export-visible-rows-aspose-cells-dotnet/)
- [Как экспортировать диаграммы Excel в PDF с помощью Aspose.Cells для .NET: Пошаговое руководство](/cells/english/net/workbook-operations/export-excel-charts-pdf-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}