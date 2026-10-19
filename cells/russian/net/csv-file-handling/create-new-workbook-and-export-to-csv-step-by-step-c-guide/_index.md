---
category: general
date: 2026-04-07
description: Создайте новую книгу в C# и узнайте, как экспортировать CSV с сохранением
  значимых цифр. Включает сохранение книги в формате CSV и советы по экспорту Excel
  в CSV.
draft: false
keywords:
- create new workbook
- save workbook as csv
- how to export csv
- save file as csv
- export excel to csv
language: ru
og_description: Создайте новую книгу в C# и экспортируйте её в CSV с полным контролем
  значимых цифр. Узнайте, как сохранить книгу как CSV и экспортировать Excel в CSV.
og_title: Создание новой рабочей книги и экспорт в CSV – Полный учебник по C#
tags:
- C#
- Aspose.Cells
- CSV export
- Excel automation
title: Создание новой рабочей книги и экспорт в CSV – пошаговое руководство по C#
url: /ru/net/csv-file-handling/create-new-workbook-and-export-to-csv-step-by-step-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание новой книги и экспорт в CSV – Полный C#‑урок

Когда‑то вам нужно **создать новую книгу** в C#, а потом задаться вопросом *как экспортировать CSV* без потери точности? Вы не одиноки. Во многих проектах конвейера данных финальный шаг – чистый CSV‑файл, и правильное форматирование может стать головной болью.  

В этом руководстве мы пройдём весь процесс: от создания новой книги, заполнения её числовым значением, настройки параметров экспорта для значимых цифр и, наконец, **сохранения книги как CSV**. К концу вы получите готовый CSV‑файл и твёрдое понимание рабочего процесса *export excel to CSV* с использованием Aspose.Cells.

## Что понадобится

- **Aspose.Cells for .NET** (пакет NuGet `Aspose.Cells` – версия 23.10 или новее).  
- Среда разработки .NET (Visual Studio, Rider или `dotnet` CLI).  
- Базовые знания C#; никаких продвинутых трюков с Excel‑interop не требуется.  

И всё — никаких дополнительных COM‑ссылок, установка Excel не нужна.

## Шаг 1: Создать экземпляр новой книги

Первым делом нам нужен полностью новый объект книги. Представьте его как пустую таблицу, живущую полностью в памяти.

```csharp
using Aspose.Cells;

// Step 1: Create a new workbook
Workbook workbook = new Workbook();
```

> **Зачем?** Класс `Workbook` – точка входа для любой работы с Excel в Aspose.Cells. Создавая её программно, вы не зависите от существующего файла, что делает шаг **save file as CSV** чистым и предсказуемым.

## Шаг 2: Получить первый лист

Каждая книга содержит как минимум один лист. Мы возьмём первый и дадим ему дружелюбное имя.

```csharp
// Step 2: Get the first worksheet (index 0)
Worksheet worksheet = workbook.Worksheets[0];
worksheet.Name = "Data";
```

> **Совет:** Переименование листов упрощает работу, когда позже открываете CSV в просмотрщике, который учитывает имена листов, хотя сам CSV их не хранит.

## Шаг 3: Записать числовое значение в ячейку A1

Теперь вставим число, у которого больше знаков после запятой, чем мы планируем оставить. Это позволит продемонстрировать функцию *significant digits*.

```csharp
// Step 3: Write a numeric value into cell A1
worksheet.Cells["A1"].PutValue(12345.6789);
```

> **Нужно больше данных?** Просто продолжайте использовать `PutValue` в других ячейках (`B2`, `C3`, …) — те же параметры экспорта будут применяться ко всему листу при **save workbook as CSV**.

## Шаг 4: Настроить параметры экспорта для значимых цифр

Aspose.Cells позволяет управлять тем, как числа выводятся в CSV. Здесь мы запрашиваем четыре значимых цифры и включаем эту функцию.

```csharp
// Step 4: Configure export options to use significant digits
ExportOptions exportOptions = new ExportOptions
{
    SignificantDigits = 4,      // keep only 4 significant digits
    UseSignificantDigits = true // enable the feature
};
```

> **Зачем использовать значимые цифры?** При работе с научными данными или финансовыми отчётами часто важна точность, а не просто количество десятичных знаков. Эта настройка гарантирует, что CSV отражает требуемую точность, что часто является проблемой при *how to export CSV* для последующего анализа.

## Шаг 5: Сохранить книгу как CSV‑файл

Наконец, записываем книгу на диск в формате CSV, используя только что определённые параметры.

```csharp
// Step 5: Save the workbook as a CSV file using the configured options
string outputPath = @"C:\Temp\out.csv";
workbook.Save(outputPath, SaveFormat.Csv, exportOptions);
```

> **Ожидаемый результат:** Файл `out.csv` будет содержать одну строку:

```
12350
```

Обратите внимание, как `12345.6789` округлилось до `12350` — это эффект сохранения четырёх значимых цифр.

### Быстрый чек‑лист для сохранения CSV

- **Путь существует:** Убедитесь, что каталог (`C:\Temp` в примере) существует, иначе `Save` бросит исключение.
- **Разрешения файлов:** Процесс должен иметь право записи; иначе вы получите `UnauthorizedAccessException`.
- **Кодировка:** Aspose.Cells по умолчанию использует UTF‑8, что подходит для большинства локалей. Если нужна другая кодовая страница, задайте `exportOptions.Encoding` перед вызовом `Save`.

## Распространённые варианты и граничные случаи

### Экспорт нескольких листов

CSV по своей природе поддерживает только один лист. Если вызвать `Save` у книги с несколькими листами, Aspose.Cells объединит их, разделяя каждый лист переводом строки. Чтобы **save file as CSV** только для конкретного листа, временно скройте остальные:

```csharp
// Hide all sheets except the one you want to export
foreach (Worksheet ws in workbook.Worksheets)
{
    ws.IsVisible = false;
}
worksheet.IsVisible = true; // the sheet we prepared earlier
workbook.Save(outputPath, SaveFormat.Csv, exportOptions);
```

### Управление разделителями

По умолчанию Aspose.Cells использует запятую (`,`) как разделитель. Если нужен точка с запятой (`;`) для европейских локалей, измените `CsvSaveOptions`:

```csharp
CsvSaveOptions csvOptions = new CsvSaveOptions
{
    Separator = ';',
    ExportOptions = exportOptions
};
workbook.Save(outputPath, csvOptions);
```

### Большие наборы данных

При экспорте миллионов строк рекомендуется использовать потоковую запись CSV, чтобы избежать высокого потребления памяти. Aspose.Cells предоставляет перегрузки `Workbook.Save`, принимающие `Stream`, позволяющие писать напрямую в файл, сетевое расположение или облачное хранилище.

## Полный рабочий пример

Ниже полностью готовая к запуску программа, объединяющая всё вышеописанное. Скопируйте её в проект консольного приложения и нажмите **F5**.

```csharp
using System;
using Aspose.Cells;

namespace CsvExportDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create a new workbook
            Workbook workbook = new Workbook();

            // 2️⃣ Get the first worksheet and give it a name
            Worksheet worksheet = workbook.Worksheets[0];
            worksheet.Name = "Data";

            // 3️⃣ Insert a numeric value (more precision than we need)
            worksheet.Cells["A1"].PutValue(12345.6789);

            // 4️⃣ Set up export options – 4 significant digits
            ExportOptions exportOptions = new ExportOptions
            {
                SignificantDigits = 4,
                UseSignificantDigits = true
            };

            // 5️⃣ Define where the CSV will be saved
            string outputPath = @"C:\Temp\out.csv";

            // 6️⃣ Save as CSV using the configured options
            workbook.Save(outputPath, SaveFormat.Csv, exportOptions);

            Console.WriteLine($"CSV file created at: {outputPath}");
        }
    }
}
```

Запустите программу, затем откройте `C:\Temp\out.csv` в Блокноте или Excel. Вы увидите округлённое значение `12350`, подтверждая, что **export excel to CSV** с учётом значимых цифр работает как ожидается.

## Итоги

Мы рассмотрели всё, что нужно для **create new workbook**, заполнения её, настройки точности экспорта и, наконец, **save workbook as CSV**. Ключевые выводы:

- Используйте `ExportOptions` для управления числовым форматом, когда вы *how to export CSV*.
- Метод `Save` с `SaveFormat.Csv` – самый простой способ **save file as CSV**.
- При необходимости меняйте разделители, видимость листов или используйте потоковый вывод для более сложных сценариев.

### Что дальше?

- **Пакетная обработка:** Пройдитесь по коллекции таблиц данных и генерируйте отдельные CSV‑файлы за один проход.
- **Пользовательское форматирование:** Комбинируйте `NumberFormat` с `ExportOptions` для валютных или датных стилей.
- **Интеграция:** Отправляйте CSV напрямую в Azure Blob Storage или S3‑бакет, используя перегрузку с потоком.

Экспериментируйте с этими идеями и оставляйте комментарии, если возникнут трудности. Приятного кодинга, и пусть ваши CSV‑экспорты всегда сохраняют нужное количество значимых цифр! 

![Иллюстрация сохранения книги C# как CSV‑файла – create new workbook](/images/create-new-workbook-csv.png "create new workbook illustration")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}