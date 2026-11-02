---
category: general
date: 2026-10-07
description: Узнайте, как удалить автофильтр из таблиц Excel с помощью C#. В этом
  руководстве также показано, как скрыть стрелки фильтра в Excel и отключить фильтр
  таблицы Excel.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- remove autofilter from excel
- excel table hide filter
- hide filter arrows excel
- disable excel table filter
language: ru
lastmod: 2026-10-07
og_description: Удалите автофильтр из таблиц Excel в C#, чтобы очистить свои электронные
  таблицы. Следуйте этому полному руководству, чтобы скрыть стрелки фильтра в Excel,
  отключить фильтр таблицы Excel и сохранить чистую книгу.
og_image_alt: Screenshot of an Excel worksheet after the autofilter UI has been removed
og_title: Удалить автoфильтр из таблиц Excel в C# – пошаговое руководство
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Learn how to remove autofilter from Excel tables with C#. This guide
    also shows how to hide filter arrows Excel and disable Excel table filter.
  headline: How to remove autofilter from Excel tables using C#
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
- Automation
title: Как удалить автофильтр из таблиц Excel с помощью C#
url: /ru/net/excel-autofilter-validation/how-to-remove-autofilter-from-excel-tables-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как удалить автофильтр из таблиц Excel с помощью C#

Если вам нужно **удалить автофильтр из Excel**, это руководство покажет, как сделать это программно с помощью C#. Вы узнаете, как скрыть стрелки фильтра в Excel и отключить фильтр таблицы, чтобы лист выглядел чисто.

Учебник проходит через каждый необходимый шаг — от установки библиотеки до сохранения конечной книги. В конце вы сможете открыть сохранённый файл и увидеть, что иконки выпадающих фильтров исчезли, таблица ведёт себя как обычный диапазон, и никаких элементов интерфейса, отвлекающих пользователя, не осталось. Предыдущий опыт работы с Aspose.Cells API не требуется, но базовые знания C# необходимы.

## Предварительные требования

Перед началом убедитесь, что у вас есть:

* .NET 6.0 SDK или более поздняя версия, установленная  
* Среда разработки, например Visual Studio 2022 или VS Code  
* Пакет **Aspose.Cells for .NET** NuGet (в примере кода используется эта библиотека)  
* Файл Excel, содержащий таблицу с активным фильтром (например, `TableWithFilter.xlsx`)

Вы можете установить Aspose.Cells через .NET CLI:

```bash
dotnet add package Aspose.Cells
```

> **Pro tip:** Используйте последнюю стабильную версию пакета, чтобы воспользоваться последними исправлениями ошибок и улучшениями производительности.

## Шаг 1 – удалить автофильтр из Excel: загрузить книгу

Первая операция — загрузить книгу, в которой находится таблица, которую вы хотите изменить. Загрузка файла создаёт представление в памяти, с которым можно работать.

```csharp
using Aspose.Cells;

string sourcePath = @"C:\Data\TableWithFilter.xlsx";
Workbook workbook = new Workbook(sourcePath);
```

*Почему этот шаг важен*: без загрузки книги у вас нет доступа к листу, таблице (`ListObject`) или её настройкам фильтра. Класс `Workbook` абстрагирует весь файл Excel, делая последующие действия простыми.

## Шаг 2 – найти лист, содержащий таблицу

Большинство книг имеют лист по умолчанию с именем «Sheet1». Вы также можете обратиться к листу по индексу или имени. Здесь мы используем первый лист.

```csharp
Worksheet worksheet = workbook.Worksheets[0];   // index‑based access
// Alternative: Worksheet worksheet = workbook.Worksheets["Sales"]; // by name
```

*Почему этот шаг важен*: таблицы привязаны к конкретному листу. Доступ к правильному листу гарантирует, что вы изменяете нужный `ListObject`.

## Шаг 3 – получить ListObject (таблицу Excel), которую нужно изменить

Таблица в Excel представлена объектом `ListObject`. Вы можете получить её по имени таблицы, которое видно на вкладке «Table Design» в Excel.

```csharp
// Replace "SalesTable" with the actual table name in your workbook
ListObject salesTable = worksheet.ListObjects["SalesTable"];
```

Если вы не уверены в имени таблицы, можете перечислить все таблицы на листе:

```csharp
foreach (ListObject tbl in worksheet.ListObjects)
{
    Console.WriteLine($"Found table: {tbl.Name}");
}
```

*Почему этот шаг важен*: свойство `AutoFilter` находится у `ListObject`. Выбор правильной таблицы гарантирует, что вы удалите нужный элемент интерфейса фильтра.

## Шаг 4 – скрыть стрелки фильтра в Excel, очистив UI AutoFilter

Основная операция — установить свойство `AutoFilter` в `null`. Это удалит стрелки выпадающих фильтров из строки заголовка таблицы.

```csharp
salesTable.AutoFilter = null;   // removes the filter UI
```

> **Note:** Установка `AutoFilter` в `null` эквивалентна команде «Clear Filter» в интерфейсе Excel, но также удаляет визуальные стрелки. Это удовлетворяет требованиям **excel table hide filter** и **disable Excel table filter**.

### Альтернатива: отключить фильтр для всех таблиц в книге

Если в книге несколько таблиц и вам нужен универсальный подход, пройдитесь по каждому `ListObject`:

```csharp
foreach (Worksheet ws in workbook.Worksheets)
{
    foreach (ListObject tbl in ws.ListObjects)
    {
        tbl.AutoFilter = null;
    }
}
```

## Шаг 5 – сохранить изменённую книгу

После удаления UI фильтра сохраните изменения в новый файл (или перезапишите оригинал, если хотите).

```csharp
string targetPath = @"C:\Data\TableNoFilter.xlsx";
workbook.Save(targetPath);
Console.WriteLine($"Workbook saved without autofilter at: {targetPath}");
```

*Почему этот шаг важен*: Excel отражает изменения только после сохранения файла. Новый файл откроется с чистой таблицей, в которой больше нет стрелок фильтра.

## Ожидаемый результат

Откройте `TableNoFilter.xlsx` в Excel. Вы должны увидеть:

* Строка заголовка таблицы больше не отображает стрелки выпадающих фильтров.  
* Нет применённых критериев фильтра; все строки видимы.  
* Остальная часть книги (формулы, форматирование, диаграммы) остаётся без изменений.

## Пограничные случаи и распространённые подводные камни

| Ситуация | Как решить |
|-----------|------------|
| **Имя таблицы неизвестно** | Используйте подход перечисления, показанный в Шаге 3, чтобы определить имена во время выполнения. |
| **Несколько таблиц на одном листе** | Примените цикл из альтернативы в Шаге 4, чтобы очистить фильтры для каждой таблицы. |
| **Старые форматы Excel (`.xls`)** | Aspose.Cells поддерживает как `.xlsx`, так и `.xls`. Загружайте файл тем же способом; API абстрагирует различия форматов. |
| **Файл только для чтения или заблокирован** | Убедитесь, что процесс имеет права записи и что файл не открыт в Excel во время выполнения кода. |
| **Нужно сохранить логику фильтра, но скрыть стрелки** | Вместо `AutoFilter = null` можно оставить объект фильтра и установить `ShowHideButtons = false` (доступно в более новых версиях библиотеки). |

## Полный, готовый к запуску пример

Ниже приведено полное консольное приложение, которое можно скопировать, вставить и запустить. Оно демонстрирует каждый шаг от настройки проекта до сохранения книги без фильтра.

```csharp
// Program.cs
using System;
using Aspose.Cells;

namespace ExcelFilterRemoval
{
    class Program
    {
        static void Main()
        {
            // 1. Load the workbook containing the table
            string sourcePath = @"C:\Data\TableWithFilter.xlsx";
            Workbook workbook = new Workbook(sourcePath);

            // 2. Access the first worksheet (or specify by name)
            Worksheet worksheet = workbook.Worksheets[0];

            // 3. Retrieve the table you want to modify
            //    Replace "SalesTable" with your actual table name
            ListObject salesTable = worksheet.ListObjects["SalesTable"];

            // 4. Remove the AutoFilter UI from the table
            salesTable.AutoFilter = null;

            // 5. Save the workbook – the table now has no filter UI
            string targetPath = @"C:\Data\TableNoFilter.xlsx";
            workbook.Save(targetPath);

            Console.WriteLine($"Successfully removed autofilter and saved to {targetPath}");
        }
    }
}
```

Запустите программу командой `dotnet run`. После завершения откройте выходной файл, чтобы убедиться, что стрелки фильтра исчезли.

## Заключение

Теперь вы знаете, как **удалить автофильтр из таблиц Excel** с помощью C#. Руководство охватывало загрузку книги, поиск целевой таблицы, очистку свойства `AutoFilter` и сохранение результата. Следуя этим шагам, вы также достигаете **excel table hide filter**, **hide filter arrows Excel** и **disable Excel table filter** в одном повторяемом скрипте.

### Что изучать дальше

* **Применить пользовательское стилизование** к таблице после удаления UI фильтра.  
* **Защитить лист**, чтобы пользователи не могли добавлять новые фильтры.  
* **Комбинировать с экспортом данных** (например, генерировать CSV‑файлы) для последующей обработки.  

Не стесняйтесь экспериментировать с альтернативными подходами, показанными в таблице пограничных случаев. Если вы столкнётесь со сценарием, не охваченным здесь, документация Aspose.Cells предоставляет дополнительные методы для тонкой настройки поведения таблиц. Приятного кодинга!

## Что вам стоит изучить дальше?

Следующие учебники охватывают тесно связанные темы, которые развивают техники, продемонстрированные в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы в собственных проектах.

- [hide filter arrows excel with C# – Complete Guide](/cells/english/net/excel-autofilter-validation/hide-filter-arrows-excel-with-c-complete-guide/)
- [Clear filter UI in Excel with C# – Remove AutoFilter Button](/cells/english/net/excel-autofilter-validation/clear-filter-ui-in-excel-with-c-remove-autofilter-button/)
- [How to Use AutoFilter in C# Excel Automation – Full Step‑by‑Step Guide](/cells/english/net/excel-autofilter-validation/how-to-use-autofilter-in-c-excel-automation-full-step-by-ste/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}