---
category: general
date: 2026-03-25
description: Копировать сводную таблицу с помощью C# и Aspose.Cells. Узнайте, как
  копировать сводную таблицу, экспортировать файл сводной таблицы и сохранять данные
  за считанные минуты.
draft: false
keywords:
- copy pivot table
- how to copy pivot
- export pivot table file
- Aspose.Cells pivot
- C# Excel automation
language: ru
og_description: Копировать сводную таблицу в C# с помощью Aspose.Cells. Это руководство
  показывает, как копировать сводную таблицу, экспортировать файл сводной таблицы
  и сохранить все настройки без изменений.
og_title: Copy Pivot Table in C# – Full Programming Tutorial
tags:
- C#
- Excel
- Aspose.Cells
- Data Export
title: Копирование сводной таблицы в C# — Полное пошаговое руководство
url: /ru/net/pivot-tables/copy-pivot-table-in-c-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Копирование сводной таблицы в C# – Полное пошаговое руководство

Когда‑нибудь вам нужно было **скопировать сводную таблицу** из одной книги в другую и вы задавались вопросом, сохраняется ли логика сводной при перемещении? Вы не одиноки. Во многих конвейерах отчетности мы генерируем мастер‑книгу, а затем отправляем облегчённую копию, которая всё равно позволяет конечным пользователям фильтровать данные. Хорошая новость? С несколькими строками кода на C# и Aspose.Cells вы можете сделать именно это — без ручных манипуляций.

В этом руководстве мы пройдем весь процесс: загрузку исходного файла, выбор диапазона, содержащего сводную таблицу, вставку его в новую книгу с сохранением определения сводной, и, наконец, **экспорт файла со сводной таблицей** для дальнейшего использования. К концу вы будете знать, *как программно копировать сводную*, и получите готовый к запуску пример, который можно вставить в ваш проект.

## Требования

- .NET 6+ (или .NET Framework 4.6+) установлен  
- NuGet‑пакет Aspose.Cells для .NET (`Install-Package Aspose.Cells`)  
- Исходный файл Excel (`source.xlsx`), уже содержащий сводную таблицу (подходит любой размер)  
- Базовые знания C#; глубокие внутренности Excel не требуются  

Если чего‑то не хватает, просто добавьте NuGet‑пакет и откройте Visual Studio — и всё.

## Что делает код (Обзор)

1. **Load** рабочую книгу, содержащую оригинальную сводную таблицу.  
2. **Define** `Range`, охватывающий всю сводную (включая её кэш).  
3. **Create** совершенно новую рабочую книгу, которая станет назначением.  
4. **Paste** диапазон с `CopyPivotTable = true`, чтобы копировать определение сводной, а не только значения.  
5. **Save** файл назначения, получая **export pivot table file**, которым можно поделиться.  

Это весь рабочий процесс в пяти лаконичных шагах. Давайте разберём каждый из них.

## Шаг 1 – Загрузка исходной рабочей книги, содержащей сводную таблицу

Сначала нам нужно загрузить исходный файл в память. Aspose.Cells делает это в одну строку.

```csharp
using Aspose.Cells;

// Load the source workbook (replace the path with your actual file)
Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");

// Grab the first worksheet – adjust the index if your pivot lives elsewhere
Worksheet sourceSheet = sourceWorkbook.Worksheets[0];
```

*Почему это важно:* Загрузка рабочей книги даёт доступ к базовому кэшу сводной. Если копировать только значения ячеек, сводная теряет возможность использовать слайсеры. Сохраняя объект рабочей книги в памяти, мы сохраняем полные метаданные сводной.

## Шаг 2 – Определение диапазона, включающего сводную таблицу

Сводная — это не просто блок ячеек; у неё также есть скрытые данные кэша. Самый безопасный способ — выбрать прямоугольник, полностью охватывающий видимую область. В большинстве случаев подходит `A1:E20`, но вы можете программно определить точные границы, используя свойства `PivotTable`.

```csharp
// Example range – adjust to match your pivot's size
Range sourceRange = sourceSheet.Cells.CreateRange("A1:E20");

// (Optional) Dynamically get the used range of the pivot:
PivotTable pivot = sourceSheet.PivotTables[0];
int firstRow = pivot.Row - 1;      // include header row
int firstCol = pivot.Column - 1;   // include field list
int lastRow  = pivot.Row + pivot.RowCount;
int lastCol  = pivot.Column + pivot.ColumnCount;
Range dynamicRange = sourceSheet.Cells.CreateRange(firstRow, firstCol,
                                                    lastRow - firstRow + 1,
                                                    lastCol - firstCol + 1);
```

*Почему выбираем диапазон:* Метод `Paste` работает с объектом `Range`. Указывая точную область, мы гарантируем, что и макет сводной, и её кэш перемещаются вместе.

## Шаг 3 – Создание новой целевой рабочей книги

Теперь мы создаём пустую рабочую книгу, которая получит скопированную сводную. Никаких изысков, просто чистый лист.

```csharp
// Initialize an empty workbook – it comes with one default worksheet
Workbook destinationWorkbook = new Workbook();
Worksheet destinationSheet = destinationWorkbook.Worksheets[0];
```

*Подсказка:* Если нужно сохранить существующие листы (например, шаблон), вы можете добавить новую книгу как клон шаблонного файла вместо использования пустого конструктора.

## Шаг 4 – Вставка диапазона с сохранением сводной таблицы

Это ядро операции. Установка `CopyPivotTable = true` сообщает Aspose.Cells перенести определение сводной, а не только отображаемые значения.

```csharp
destinationSheet.Cells.Paste(
    sourceRange,
    new PasteOptions
    {
        PasteType = PasteType.All,      // copy everything: formulas, formats, etc.
        CopyPivotTable = true           // crucial – keeps the pivot functional
    });
```

*Что происходит за кулисами?* Aspose.Cells воссоздаёт кэш сводной в целевой книге, перенастраивает источник данных сводной и сохраняет слайсеры, фильтры и вычисляемые поля. В результате получаем полностью интерактивную сводную — именно то, что вы бы ожидали при ручном дублировании листа в Excel.

## Шаг 5 – Сохранение полученной рабочей книги (Экспорт файла со сводной таблицей)

Наконец мы записываем целевую рабочую книгу на диск. Полученный файл — ваш **export pivot table file**, готовый к распространению.

```csharp
destinationWorkbook.Save("YOUR_DIRECTORY/copy-pivot.xlsx");
```

Откройте `copy-pivot.xlsx` в Excel, и вы увидите сводную таблицу в целости, готовую к обновлению или фильтрации.

## Полный рабочий пример (Все шаги вместе)

Ниже приведена полная программа, которую можно скопировать‑вставить в консольное приложение. Она включает обработку ошибок и комментарии для ясности.

```csharp
using System;
using Aspose.Cells;

namespace PivotCopyDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            try
            {
                // 1️⃣ Load source workbook with the pivot table
                Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
                Worksheet sourceSheet = sourceWorkbook.Worksheets[0];

                // 2️⃣ Define the range that fully encloses the pivot
                // Adjust "A1:E20" as needed, or use dynamic detection shown earlier
                Range sourceRange = sourceSheet.Cells.CreateRange("A1:E20");

                // 3️⃣ Create a fresh destination workbook
                Workbook destinationWorkbook = new Workbook();
                Worksheet destinationSheet = destinationWorkbook.Worksheets[0];

                // 4️⃣ Paste the range and keep the pivot definition
                destinationSheet.Cells.Paste(
                    sourceRange,
                    new PasteOptions
                    {
                        PasteType = PasteType.All,
                        CopyPivotTable = true
                    });

                // 5️⃣ Save the new file – this is your exported pivot table file
                destinationWorkbook.Save("YOUR_DIRECTORY/copy-pivot.xlsx");

                Console.WriteLine("✅ Pivot table copied successfully! File saved as copy-pivot.xlsx");
            }
            catch (Exception ex)
            {
                Console.WriteLine($"❌ An error occurred: {ex.Message}");
            }
        }
    }
}
```

**Ожидаемый результат:** При открытии `copy-pivot.xlsx` сводная таблица будет выглядеть точно так же, как в `source.xlsx`. Вы можете обновлять её, менять фильтры или даже добавлять новые источники данных, не теряя функциональности.

## Часто задаваемые вопросы и особые случаи

### Что делать, если в исходной книге несколько сводных?

Пройдитесь по `sourceSheet.PivotTables` и повторите копирование‑вставку для каждой. Только убедитесь, что диапазоны назначения не перекрываются.

```csharp
int destRow = 0;
foreach (PivotTable pt in sourceSheet.PivotTables)
{
    // Calculate a non‑overlapping destination range for each pivot
    Range src = sourceSheet.Cells.CreateRange(pt.Row, pt.Column,
                                              pt.RowCount + 5, pt.ColumnCount + 5);
    destinationSheet.Cells.Paste(src, new PasteOptions { PasteType = PasteType.All, CopyPivotTable = true });
    destRow += pt.RowCount + 10; // move down for the next pivot
}
```

### Работает ли это с внешними источниками данных (например, SQL)?

Если оригинальная сводная использует внешнее соединение, строка подключения также копируется. Однако целевая книга должна иметь доступ к тому же источнику данных. Возможно, потребуется скорректировать учётные данные или использовать `WorkbookSettings` для разрешения внешних соединений.

### Можно ли скопировать только макет сводной (без данных)?

Установите `PasteOptions.PasteType = PasteType.Formulas` и оставьте `CopyPivotTable = true`. Это копирует структуру, оставляя кэш данных пустым, что заставит выполнить обновление при первом открытии.

### Что насчёт защиты листа?

Если исходный лист защищён, снимите защиту перед копированием или передайте соответствующий `Password` в `Worksheet.Unprotect`. После вставки вы можете вновь применить защиту к листу назначения.

## Профессиональные советы и подводные камни

- **Pro tip:** Всегда используйте последнюю версию Aspose.Cells; в более старых релизах была ошибка, когда `CopyPivotTable` игнорировал слайсеры.  
- **Watch out for:** Большие кэши сводных могут раздувать целевой файл. Если важен размер, рассмотрите очистку неиспользуемых полей перед копированием.  
- **Performance tip:** При копировании множества листов временно отключите `WorkbookSettings.EnableThreadedCalculation` для ускорения операции.  
- **Naming clash:** Если в целевой книге уже есть сводная с тем же именем, Aspose переименует импортируемую (`PivotTable1_1`). Переименуйте вручную, если нужен конкретный идентификатор.

## Визуальное резюме

![Копирование сводной таблицы в C# – схема, показывающая исходную книгу → выбор диапазона → вставку с сохранением сводной → файл назначения](copy-pivot-diagram.png "Иллюстрация рабочего процесса копирования сводной таблицы")

*Alt text:* Диаграмма рабочего процесса **Copy pivot table**, иллюстрирующая источник, диапазон, параметры вставки и экспортированный файл.

## Заключение

Мы рассмотрели всё, что необходимо для **copy pivot table** с использованием C# и Aspose.Cells: загрузку источника, выбор правильного диапазона, сохранение определения сводной при вставке и, наконец, экспорт результата в виде отдельного файла. Приведённый выше фрагмент готов к использованию в продакшене; просто укажите свои пути, и всё готово.

Теперь, когда вы знаете, *how to copy pivot* программно, вы можете автоматизировать распределение отчетов, создавать генераторы шаблонов или интегрировать аналитику Excel в более крупные сервисы .NET. Далее вы можете изучить **export pivot table file** в другие форматы (PDF, CSV) или внедрить рабочую книгу в веб‑API для аналитики «на лету».

Есть интересный вариант, которым хотите поделиться — возможно, копирование сводных между разными версиями Excel или работа с моделями PowerPivot? Оставьте комментарий, и давайте продолжать обсуждение. Счастливого кодинга!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}