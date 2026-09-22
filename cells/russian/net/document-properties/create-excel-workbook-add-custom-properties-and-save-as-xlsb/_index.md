---
category: general
date: 2026-03-22
description: Создать книгу Excel, добавить пользовательские свойства, установить имя
  листа и сохранить в бинарный файл XLSB с помощью C#.
draft: false
keywords:
- create excel workbook
- add custom properties
- save as xlsb
- set worksheet name
- write binary excel file
language: ru
og_description: Создать рабочую книгу Excel, добавить пользовательские свойства, задать
  имя листа и сохранить как бинарный файл XLSB с помощью C#.
og_title: Создать книгу Excel – добавить пользовательские свойства и сохранить как
  XLSB
tags:
- C#
- Aspose.Cells
- Excel automation
title: Создать книгу Excel – добавить пользовательские свойства и сохранить как XLSB
url: /ru/net/document-properties/create-excel-workbook-add-custom-properties-and-save-as-xlsb/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создать книгу Excel – Добавить пользовательские свойства и сохранить как XLSB

Когда‑нибудь вам нужно было **create Excel workbook** программно, но также сохранить некоторые метаданные? Возможно, вы создаёте движок отчётов, который помечает каждый файл идентификатором отчёта, именем автора или номером версии. В этом случае изучение того, как **add custom properties**, одновременно **set worksheet name** и в конце **save as XLSB**, сэкономит вам массу ручной пост‑обработки.

В этом руководстве мы пройдём полный, исполняемый пример, который точно показывает, как **write binary Excel file** с помощью C#. Вы увидите, почему формат XLSB — правильный выбор для передачи пользовательских свойств, как избежать самых распространённых подводных камней и что делать, если нужно поддерживать более старые версии Excel.

---

## Что понадобится

- **.NET 6+** (или .NET Framework 4.6+). Код работает на любой современной среде выполнения.
- **Aspose.Cells for .NET** (бесплатная пробная версия или лицензия). Он предоставляет классы `Workbook`, `Worksheet` и `CustomProperties`, используемые ниже.
- IDE, с которым вам удобно работать — Visual Studio, Rider или даже VS Code подойдёт.
- Права записи в папку, где будет сохранён сгенерированный файл.

Никакие другие сторонние библиотеки не требуются.

## Шаг 1: Установить Aspose.Cells

Для начала добавьте пакет Aspose.Cells NuGet в ваш проект:

```bash
dotnet add package Aspose.Cells
```

> **Pro tip:** Если вы работаете на CI‑сервере, храните лицензионный ключ в переменной окружения и загружайте его во время выполнения — это предотвращает появление водяного знака «evaluation» в вашем выводе.

---

## Шаг 2: Создать книгу Excel – Обзор

Первое реальное действие — **create Excel workbook**. Этот объект представляет весь файл в памяти и предоставляет доступ к листам, стилям и пользовательским свойствам.

```csharp
using Aspose.Cells;

namespace ExcelDemo
{
    class Program
    {
        static void Main()
        {
            // Step 2.1: Instantiate a new workbook (empty by default)
            Workbook workbook = new Workbook();

            // The rest of the steps follow...
```

Зачем создавать новый `Workbook`, а не загружать шаблон? Пустая книга гарантирует отсутствие скрытых стилей или оставшихся пользовательских свойств, что особенно важно, когда вы планируете **write binary excel file** для downstream‑систем, ожидающих чистый лист.

## Шаг 3: Установить имя листа (и почему это важно)

Листы Excel по умолчанию называются «Sheet1», «Sheet2» и т.д. Присвоение листу осмысленного имени упрощает последующую обработку — например, Power Query или макросы VBA — делая её более читаемой.

```csharp
            // Step 3.1: Grab the first worksheet (index 0) and rename it
            Worksheet worksheet = workbook.Worksheets[0];
            worksheet.Name = "Data"; // clear, concise, and self‑describing
```

Если попытаться задать дублирующее имя, Aspose.Cells выбросит `ArgumentException`. Чтобы быть уверенным, можно проверить `Worksheets.Exists("Data")` перед переименованием.

## Шаг 4: Добавить пользовательские свойства

Пользовательские свойства хранятся во внутреннем XML книги и перемещаются вместе с файлом независимо от формата. Они идеальны для внедрения таких данных, как `ReportId` или `GeneratedBy`.

```csharp
            // Step 4.1: Add a numeric property
            workbook.CustomProperties.Add("ReportId", 12345);

            // Step 4.2: Add a string property
            workbook.CustomProperties.Add("GeneratedBy", "MyApp");
```

> **Why use custom properties?**  
> • Они доступны через панель Excel «File → Info → Properties».  
> • Код, который использует книгу, может читать их без сканирования содержимого ячеек.  
> • Они сохраняются при конвертации форматов (XLSX ↔ XLSB), поскольку являются частью метаданных файла.

Можно также сохранять даты, булевы значения или даже бинарные блобы, но держите нагрузку небольшой — Excel не является базой данных.

## Шаг 5: Сохранить как XLSB (Write Binary Excel File)

Формат XLSB хранит данные в бинарной структуре, что делает файл меньше и быстрее открывается. Более важно для этого руководства, **custom properties are baked into the binary stream**, гарантируя их перенос вместе с файлом.

```csharp
            // Step 5.1: Define the output path
            string outputPath = Path.Combine(
                Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
                "WithCustomProps.xlsb");

            // Step 5.2: Save the workbook as a binary XLSB file
            workbook.Save(outputPath, SaveFormat.Xlsb);

            Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

### Ожидаемый результат

После запуска программы вы найдете `WithCustomProps.xlsb` на рабочем столе. Откройте его в Excel, перейдите в **File → Info → Properties**, и вы увидите `ReportId` и `GeneratedBy`, перечисленные в разделе *Custom*.

## Шаг 6: Пограничные случаи и часто задаваемые вопросы

### Что делать, если целевая папка только для чтения?

Обёрните вызов `Save` в блок `try/catch` и переключитесь на расположение, доступное для записи пользователем, например `%TEMP%`. Это предотвратит падение приложения из‑за ошибок доступа.

```csharp
try
{
    workbook.Save(outputPath, SaveFormat.Xlsb);
}
catch (UnauthorizedAccessException)
{
    string fallback = Path.GetTempFileName().Replace(".tmp", ".xlsb");
    workbook.Save(fallback, SaveFormat.Xlsb);
    Console.WriteLine($"Saved to fallback location: {fallback}");
}
```

### Могу ли я **save as XLSX** и всё равно сохранить пользовательские свойства?

Да — просто замените `SaveFormat.Xlsb` на `SaveFormat.Xlsx`. Свойства хранятся в той же XML‑части, поэтому они сохраняются при переключении формата. Однако файлы XLSX больше, так как они являются zip‑архивом XML, тогда как XLSB обеспечивает лучшую производительность для больших наборов данных.

### Как прочитать пользовательские свойства позже?

```csharp
Workbook loaded = new Workbook(outputPath);
foreach (CustomProperty prop in loaded.CustomProperties)
{
    Console.WriteLine($"{prop.Name} = {prop.Value}");
}
```

Этот фрагмент выводит каждое пользовательское свойство, что упрощает проверку происхождения файла downstream‑службами.

## Полный рабочий пример

Ниже приведена полная программа, которую можно скопировать и вставить в новый консольный проект. Ничего не пропущено — всё, от операторов `using` до финального `Console.WriteLine`, включено.

```csharp
using System;
using System.IO;
using Aspose.Cells;

namespace ExcelDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create a new workbook instance
            Workbook workbook = new Workbook();

            // 2️⃣ Access the first worksheet and give it a meaningful name
            Worksheet worksheet = workbook.Worksheets[0];
            worksheet.Name = "Data";

            // 3️⃣ Add custom properties (they travel with the file)
            workbook.CustomProperties.Add("ReportId", 12345);
            workbook.CustomProperties.Add("GeneratedBy", "MyApp");

            // 4️⃣ Define where to save the binary XLSB file
            string outputPath = Path.Combine(
                Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
                "WithCustomProps.xlsb");

            // 5️⃣ Save the workbook as a binary XLSB file
            try
            {
                workbook.Save(outputPath, SaveFormat.Xlsb);
                Console.WriteLine($"✅ Workbook saved to {outputPath}");
            }
            catch (Exception ex)
            {
                Console.WriteLine($"❌ Failed to save workbook: {ex.Message}");
            }
        }
    }
}
```

Запустите программу, откройте полученный файл и проверьте пользовательские свойства. Это весь процесс **create excel workbook**, **add custom properties**, **set worksheet name** и **save as xlsb** в одном аккуратном потоке.

## Заключение

Теперь вы точно знаете, как **create Excel workbook**, задать листу чёткое **set worksheet name**, внедрить полезные метаданные с помощью **add custom properties** и, наконец, **save as XLSB**, чтобы получить компактный бинарный файл Excel. Этот рабочий процесс надёжен, работает на разных версиях .NET и масштабируется как при генерации одного отчёта, так и тысячи.

Что дальше? Попробуйте добавить таблицу данных на лист «Data», поэкспериментировать с различными типами свойств (даты, булевы), или переключить вывод на **save as xlsb** для огромных наборов данных. Вы также можете изучить защиту книги паролем — Aspose.Cells делает это одной строкой кода.

Не стесняйтесь оставить комментарий, если столкнётесь с проблемами, или поделиться тем, как вы расширили этот шаблон в своих проектах. Счастливого кодинга!  

---  

![Create Excel workbook screenshot](image.png){alt="Создать книгу Excel со пользовательскими свойствами"}

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}