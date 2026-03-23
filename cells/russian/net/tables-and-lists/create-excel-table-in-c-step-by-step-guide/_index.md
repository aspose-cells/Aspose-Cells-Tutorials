---
category: general
date: 2026-03-22
description: Быстро создайте таблицу Excel в C#. Узнайте, как добавить таблицу, задать
  её диапазон, скрыть заголовок и отключить фильтр, с полным примером кода.
draft: false
keywords:
- create excel table
- how to add table
- hide table header
- define table range
- disable table filter
language: ru
og_description: Создайте таблицу Excel в C# с понятным примером. Узнайте, как добавить
  таблицу, задать её диапазон, скрыть заголовок и отключить фильтр всего за несколько
  строк.
og_title: Создание таблицы Excel в C# – Полное руководство по программированию
tags:
- Aspose.Cells
- C#
- Excel Automation
title: Создание таблицы Excel в C# — пошаговое руководство
url: /ru/net/tables-and-lists/create-excel-table-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание Excel‑таблицы в C# – пошаговое руководство

Когда‑нибудь нужно было **создать Excel‑таблицу** программно с помощью C#? Создание Excel‑таблицы может стать простым делом, если знать правильные шаги. В этом руководстве мы пройдем полный, готовый к запуску пример, показывающий **как добавить таблицу**, **определить диапазон таблицы**, **скрыть заголовок таблицы** и даже **отключить фильтр таблицы** – всё без выхода из IDE.

Если вам когда‑нибудь мешал появляющийся UI AutoFilter, когда он не нужен, вы попали по адресу. К концу этого руководства у вас будет готовый к запуску фрагмент кода, создающий чистую книгу с именем *TableNoFilter.xlsx*, и вы поймёте, почему важна каждая строка.

## Что вы узнаете

- Как **создать Excel‑таблицу** с нуля с помощью Aspose.Cells.  
- Точный синтаксис для **определения диапазона таблицы** (A1:D5 в нашем примере).  
- Как включить строку заголовка, чтобы появился встроенный UI фильтра.  
- Приём для **скрытия заголовка таблицы** и **отключения фильтра таблицы**, когда они больше не нужны.  
- Полную готовую к копированию программу на C#, которую можно запустить уже сегодня.

### Требования

- .NET 6.0 или новее (код также работает с .NET Framework 4.7+).  
- Aspose.Cells для .NET, установленный через NuGet (`Install-Package Aspose.Cells`).  
- Базовые знания C# и Visual Studio (или любой другой предпочитаемой IDE).

---

## Шаг 1: Создание проекта и импорт пространств имён

Прежде чем **создать Excel‑таблицу**, нужен консольный проект, ссылающийся на Aspose.Cells. Откройте терминал и выполните:

```bash
dotnet new console -n ExcelTableDemo
cd ExcelTableDemo
dotnet add package Aspose.Cells
```

Теперь откройте *Program.cs* и добавьте необходимые `using`‑директивы:

```csharp
using System;
using Aspose.Cells;
```

Эти импорты дают доступ к классам `Workbook`, `Worksheet`, `CellArea` и `ListObject`, которые управляют остальной частью руководства.

## Шаг 2: Инициализация новой книги и получение первого листа

Создание новой книги – первый логичный шаг. Представьте книгу как контейнер файла Excel, а лист – отдельный лист, куда мы разместим нашу таблицу.

```csharp
// Step 2: Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();                     // Empty workbook
Worksheet worksheet = workbook.Worksheets[0];           // First (default) sheet
```

> **Почему это важно:** Новый `Workbook` создаётся с одним пустым листом. Обращаясь к `Worksheets[0]`, мы гарантируем работу с листом по умолчанию без необходимости создавать его вручную.

## Шаг 3: Определение диапазона таблицы (A1:D5)

В терминологии Excel *таблица* находится внутри прямоугольного блока ячеек. Структура `CellArea` позволяет точно указать этот блок. Здесь мы покажем, как **определить диапазон таблицы** для ячеек от A1 до D5.

```csharp
// Step 3: Define the cell range that will become the table (A1:D5)
CellArea tableRange = new CellArea(startRow: 0, startColumn: 0, endRow: 4, endColumn: 3);
// Row/column indices are zero‑based, so 0‑4 maps to rows 1‑5 and 0‑3 maps to columns A‑D.
```

> **Совет:** Если нужен динамический диапазон, можно вычислять `endRow` и `endColumn` исходя из длины данных. Нумерация начинается с нуля, что часто приводит к ошибкам «на один элемент больше/меньше», поэтому проверяйте свои числа.

## Шаг 4: Добавление таблицы и включение строки заголовка

Теперь переходим к основной части руководства: **как добавить таблицу** на лист. Коллекция `ListObjects` управляет таблицами, а установка `ShowHeaders = true` автоматически добавляет UI AutoFilter.

```csharp
// Step 4: Add a ListObject (table) to the worksheet and enable the header row
ListObject sampleTable = worksheet.ListObjects[worksheet.ListObjects.Add(tableRange, true)];
sampleTable.ShowHeaders = true;   // Shows the header row and the filter dropdowns
```

> **Объяснение:**  
> - `Add(tableRange, true)` создаёт новый `ListObject` (т.е. Excel‑таблицу) внутри указанного диапазона.  
> - Параметр `true` сообщает Aspose.Cells, что первая строка диапазона должна рассматриваться как заголовок.  
> - Установка `ShowHeaders` в `true` делает заголовок видимым и активирует встроенный UI фильтра.

На этом этапе, открыв сгенерированную книгу, вы увидите красиво отформатированную таблицу с стрелками‑фильтрами в заголовках столбцов.

## Шаг 5: Скрытие строки заголовка и отключение AutoFilter

Иногда требуется отображать данные без лишних элементов UI. Возможно, вы экспортируете чистый отчёт, где фильтры не нужны. Ниже показана техника **скрытия заголовка таблицы** и **отключения фильтра таблицы**:

```csharp
// Step 5: When the filter UI is no longer needed, hide the header row
// and clear the underlying AutoFilter object
sampleTable.ShowHeaders = false;   // Hides the header row
sampleTable.AutoFilter = null;     // Removes the filter dropdowns completely
```

> **Почему это делается:**  
> - `ShowHeaders = false` убирает визуальную строку заголовка, превращая таблицу в обычный блок данных.  
> - Установка `AutoFilter = null` удаляет скрытый объект фильтра, гарантируя отсутствие остаточных фильтров. Это и есть **отключение фильтра таблицы**.

## Шаг 6: Сохранение книги на диск

Наконец, сохраняем файл в выбранное вами место. Замените `"YOUR_DIRECTORY"` реальным путём на вашем компьютере.

```csharp
// Step 6: Save the workbook to a file
string outputPath = @"YOUR_DIRECTORY\TableNoFilter.xlsx";
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

При запуске программы вы должны увидеть:

```
Workbook saved to C:\Temp\TableNoFilter.xlsx
```

Открывая файл, вы увидите лист с блоком данных (без заголовка и без стрелок‑фильтров). Это полный цикл – от **создания Excel‑таблицы** до **отключения фильтра таблицы**.

---

## Полный рабочий пример (готов к копированию)

Ниже представлен весь код программы, готовый к компиляции. Просто замените каталог‑заполнитель на действительный путь.

```csharp
using System;
using Aspose.Cells;

namespace ExcelTableDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Create a new workbook and get the first worksheet
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.Worksheets[0];

            // Step 2: Define the cell range that will become the table (A1:D5)
            CellArea tableRange = new CellArea(0, 0, 4, 3); // A1:D5

            // Step 3: Add a ListObject (table) to the worksheet and enable the header row
            ListObject sampleTable = worksheet.ListObjects[worksheet.ListObjects.Add(tableRange, true)];
            sampleTable.ShowHeaders = true; // Shows header + AutoFilter UI

            // Step 4: When the filter UI is no longer needed, hide the header row
            // and clear the underlying AutoFilter object
            sampleTable.ShowHeaders = false; // Hide header
            sampleTable.AutoFilter = null;   // Disable filter

            // Step 5: Save the workbook to a file
            string outputPath = @"C:\Temp\TableNoFilter.xlsx"; // Change to your folder
            workbook.Save(outputPath);
            Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

**Ожидаемый результат:** Файл с именем *TableNoFilter.xlsx*, содержащий простой диапазон данных A1:D5 без видимого заголовка и без выпадающих фильтров.

---

## Часто задаваемые вопросы и особые случаи

### Что делать, если нужны несколько таблиц на одном листе?

Просто повторите **Шаг 3**, задав новый `CellArea` и создав новый `ListObject`. Каждая таблица хранит свои настройки заголовка и фильтра, поэтому одну можно скрыть, а другую оставить видимой.

### Можно ли стилизовать таблицу (полосатые строки, цвета) перед скрытием заголовка?

Конечно. У `ListObject` есть свойство `TableStyleType`. Например:

```csharp
sampleTable.TableStyleType = TableStyleType.TableStyleMedium2;
```

Стиль можно применить **до** скрытия заголовка; визуальное форматирование сохранится.

### Как оставить заголовок, но скрыть только стрелки‑фильтры?

Установите `ShowHeaders = true` (чтобы оставить строку) и затем очистите фильтр:

```csharp
sampleTable.AutoFilter = null; // Removes arrows but header stays visible
```

Это удовлетворит требование **отключить фильтр таблицы**, не теряя подписи столбцов.

### Работает ли это только с файлами .xlsx?

Aspose.Cells автоматически определяет формат по расширению, переданному в `Save`. Можно также сохранять в `.xls`, `.csv` или даже `.pdf`, указав соответствующее расширение.

---

## Заключение

Мы рассмотрели всё, что нужно для **создания Excel‑таблицы** в C# с помощью Aspose.Cells: от **определения диапазона таблицы** до **скрытия заголовка таблицы** и **отключения фильтра таблицы**. Код короткий, понятный и готов к использованию в продакшене.

Далее вы можете исследовать, как **добавлять таблицу** с динамическими данными, применять пользовательские стили или экспортировать ту же книгу в PDF. Все эти темы опираются на полученный фундамент, так что экспериментируйте и адаптируйте фрагмент под свои проекты.

Есть свои находки? Оставляйте комментарий ниже, и удачной разработки!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}