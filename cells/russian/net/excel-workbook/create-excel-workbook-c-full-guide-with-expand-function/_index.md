---
category: general
date: 2026-06-08
description: Создайте Excel‑книгу на C# шаг за шагом и изучите, как использовать функцию EXPAND
  в Excel для динамических диапазонов. Идеально для разработчиков .NET.
draft: false
keywords:
- create excel workbook c#
- use expand function in excel
language: ru
og_description: Создайте книгу Excel на C# с понятным примером и узнайте, как использовать
  функцию EXPAND в Excel для создания динамических массивов.
og_title: Создание рабочей книги Excel на C# – Полное руководство по программированию
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Create Excel workbook C# step‑by‑step and learn how to use expand function
    in Excel for dynamic ranges. Perfect for .NET developers.
  headline: Create Excel Workbook C# – Full Guide with Expand Function
  type: TechArticle
- description: Create Excel workbook C# step‑by‑step and learn how to use expand function
    in Excel for dynamic ranges. Perfect for .NET developers.
  name: Create Excel Workbook C# – Full Guide with Expand Function
  steps:
  - name: '`SEQUENCE(3)` produces a vertical array `{1;2;3}`.'
    text: '`SEQUENCE(3)` produces a vertical array `{1;2;3}`.'
  - name: '`EXPAND(...,5,5)` tells Excel to grow that array to 5 rows and 5 columns.'
    text: '`EXPAND(...,5,5)` tells Excel to grow that array to 5 rows and 5 columns.'
  - name: The result is a 5 × 5 grid where the first three rows contain the numbers
      1‑3 repeated across columns, and the remaining two rows are blank.
    text: The result is a 5 × 5 grid where the first three rows contain the numbers
      1‑3 repeated across columns, and the remaining two rows are blank.
  - name: '**Creates an Excel workbook C#** using Aspose.Cells.'
    text: '**Creates an Excel workbook C#** using Aspose.Cells.'
  - name: '**Uses the EXPAND function in Excel** to turn a 3‑row array into a 5 × 5
      block.'
    text: '**Uses the EXPAND function in Excel** to turn a 3‑row array into a 5 × 5
      block.'
  - name: Adds a cotangent formula (`COT(PI()/4)`).
    text: Adds a cotangent formula (`COT(PI()/4)`).
  - name: Saves the file and optionally auto‑fits columns.
    text: Saves the file and optionally auto‑fits columns.
  type: HowTo
- questions:
  - answer: Absolutely. Aspose.Cells targets .NET Standard 2.0, which is compatible
      with both .NET Core and the classic Framework.
    question: Does this work with .NET Framework 4.8?
  - answer: Use `ws.Protect(ProtectionType.All, "yourPassword");` before saving.
    question: What if I need to protect the sheet?
  - answer: 'Yes—`workbook.Save(stream, SaveFormat.Xlsx);` is handy for web APIs that
      return the file as a download. --- ## TL;DR We built a **complete C# console
      app** that: 1. **Creates an Excel workbook C#** using Aspose.Cells. 2. **Uses
      the EXPAND function in Excel** to turn a 3‑row array into a 5 × 5 block.'
    question: Can I write the workbook directly to a `MemoryStream`?
  type: FAQPage
tags:
- csharp
- excel
- aspose-cells
- .net
title: Создание рабочей книги Excel на C# – полное руководство с функцией Expand
url: /ru/net/excel-workbook/create-excel-workbook-c-full-guide-with-expand-function/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание Excel Workbook C# – Полное руководство с функцией Expand

Ever wondered how to **create Excel workbook C#** without wrestling with COM interop or fiddling with XML? You're not the only one. In many .NET projects we need to spit out a spreadsheet, fill it with formulas, and hand it off to non‑technical users. The good news? With a modern library like **Aspose.Cells** the whole process is a piece of cake.

В этом руководстве мы пройдем полный, исполняемый пример, который **creates an Excel workbook C#**, добавляет пару формул — включая то, как **use expand function in Excel** — и сохраняет файл, чтобы вы могли сразу открыть его в Excel. К концу вы будете знать не только *что* вводить, но и *почему* каждая строка важна, и у вас будет шаблон, который можно скопировать в любой проект.

## Предварительные требования

- .NET 6 SDK (или любая недавняя версия .NET) установлен.
- IDE, совместимая с NuGet (Visual Studio, VS Code, Rider и т.д.).
- Пакет NuGet **Aspose.Cells** — он предоставляет классы `Workbook` и `Worksheet`, используемые в коде.
- Базовые знания C#; опыт работы с Excel не требуется.

Все готово? Отлично — приступим.

## Шаг 1: Настройка проекта и добавление Aspose.Cells

Сначала создайте консольное приложение и подключите библиотеку.

```bash
dotnet new console -n ExcelDemo
cd ExcelDemo
dotnet add package Aspose.Cells
```

> **Совет:** Если вы работаете в корпоративной сети, возможно, потребуется настроить прокси для NuGet. Пакет Aspose.Cells лёгкий, поэтому установка завершается за секунды.

Откройте `Program.cs`. Вы увидите метод `Main` по умолчанию — замените его шаблоном ниже.

```csharp
using System;
using Aspose.Cells;

namespace ExcelDemo
{
    class Program
    {
        static void Main()
        {
            // All of our Excel logic will go here.
        }
    }
}
```

Строка `using Aspose.Cells;` импортирует классы для работы с таблицами. Если её забыть, компилятор будет ругаться, что `Workbook` не определён — чего мы позже избегаем.

## Шаг 2: Создание Excel Workbook C# и доступ к первому листу

С готовым проектом мы наконец можем **create Excel workbook C#**. Конструктор `Workbook` создаёт новую пустую книгу, а индекс `Worksheets[0]` возвращает лист по умолчанию (названный «Sheet1»).

```csharp
// Step 2: Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();               // creates an empty .xlsx file in memory
Worksheet ws = workbook.Worksheets[0];            // reference to the first (default) sheet
```

Зачем явно получать первый лист? Потому что многие последующие API (например, установка формул) требуют объект `Worksheet`, а не только `Workbook`. Это также делает код более понятным для будущих читателей.

## Шаг 3: Использование функции Expand в Excel для заполнения динамического диапазона

Теперь звезда шоу: **use expand function in Excel**. Функция `EXPAND` (доступна, начиная с Excel 365) принимает исходный массив и расширяет его до нужного размера. В нашем примере мы начнём с вертикального массива из 3‑х строк, созданного `SEQUENCE(3)`, и расширим его до блока 5 × 5.

```csharp
// Step 3: Insert the EXPAND formula into cell A1
ws.Cells["A1"].Formula = "EXPAND(SEQUENCE(3),5,5)";
```

Что происходит на самом деле?

1. `SEQUENCE(3)` создаёт вертикальный массив `{1;2;3}`.
2. `EXPAND(...,5,5)` указывает Excel расширить массив до 5 строк и 5 столбцов.
3. Результатом является сетка 5 × 5, где первые три строки содержат числа 1‑3, повторяющиеся по столбцам, а оставшиеся две строки пусты.

Поскольку мы записываем формулу как строку, Excel вычисляет её *при открытии файла*, а не во время выполнения. Это делает книгу лёгкой, и любые изменения исходного массива автоматически отразятся.

> **Особый случай:** Если пользователь откроет книгу в более старой версии Excel, не поддерживающей `EXPAND`, ячейка покажет `#NAME?`. Чтобы защититься, можно обернуть формулу в `IFERROR`, но для современных сред безопасно полагаться на эту функцию.

## Шаг 4: Добавление формулы котангенса для полноты

Добавим ещё одну формулу, чтобы показать, как просто добавлять математические выражения. Мы вычислим котангенс π/4, который ровно равен `1`.

```csharp
// Step 4: Insert a cotangent calculation in cell B1
ws.Cells["B1"].Formula = "COT(PI()/4)";
```

Функция `COT` в Excel используется реже, чем `SIN` или `COS`, но она идеальна для тригонометрических задач. При открытии книги ячейка **B1** покажет `1`.

## Шаг 5: Сохранение книги и проверка результата

Вся эта работа была бы бессмысленной, если бы мы не сохраняли файл. Метод `Save` записывает книгу из памяти на диск. Выберите папку, в которую у вас есть права записи, и дайте файлу понятное имя.

```csharp
// Step 5: Save the workbook to the output folder
string outputPath = @"./output.xlsx";
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

Run the program:

```bash
dotnet run
```

Вы должны увидеть сообщение в консоли, подтверждающее сохранение. Откройте `output.xlsx` в Excel, и вы заметите:

- Ячейки **A1:E5** заполнены расширенной последовательностью (1,2,3 в первых трёх строках, пустые в строках 4‑5).
- Ячейка **B1** отображает значение `1` из формулы котангенса.

Это полный цикл: **create excel workbook c#**, внедрение формул и получение готовой таблицы.

![Снимок сгенерированной книги Excel, показывающий расширенный массив и результат котангенса](/images/create-excel-workbook-csharp.png "пример создания excel workbook c#")

*Текст alt изображения: create excel workbook c# – просмотр заполненной таблицы.*

## Шаг 6: Необязательно — Автоматическое подгонка столбцов для аккуратного вида

Если вы планируете распространять файл конечным пользователям, быстрая авто‑подгонка делает его более профессиональным.

```csharp
// Optional: Auto‑fit all columns in the used range
ws.AutoFitColumns(0, ws.Cells.MaxColumn);
```

Эта строка проходит по каждому столбцу с данными и подгоняет его ширину под самое длинное значение. Это небольшая деталь, но она предотвращает нежелательное переполнение «…###», когда числа шире стандартной ширины столбца.

## Шаг 7: Итоги и дальнейшие шаги

Поздравляем — вы только что освоили, как **create excel workbook c#** с нуля и узнали, как **use expand function in excel** для создания динамических массивов. Код преднамеренно минимален, чтобы вы могли скопировать‑вставить его в любой проект, но концепции масштабируются:

- **Dynamic data sources:** Замените `SEQUENCE(3)` ссылкой на другой диапазон или именованную таблицу.
- **Conditional formatting:** Используйте `ws.Cells["A1:E5"].Style` для добавления цветов в зависимости от значений.
- **Charts and graphics:** Aspose.Cells может встраивать диаграммы, изображения и даже сводные таблицы.

Не стесняйтесь экспериментировать — меняйте размеры `EXPAND`, пробуйте `FILTER` или `SORT`, или соединяйте несколько формул вместе. Библиотека справится со всем без необходимости работать с низкоуровневым форматом OpenXML.

---

### Часто задаваемые вопросы

**В: Работает ли это с .NET Framework 4.8?**  
**О:** Абсолютно. Aspose.Cells нацелен на .NET Standard 2.0, который совместим как с .NET Core, так и с классическим Framework.

**В: Что делать, если нужно защитить лист?**  
**О:** Используйте `ws.Protect(ProtectionType.All, "yourPassword");` перед сохранением.

**В: Можно ли записать книгу напрямую в `MemoryStream`?**  
**О:** Да — `workbook.Save(stream, SaveFormat.Xlsx);` удобно для веб‑API, которые возвращают файл как загрузку.

---

## TL;DR

Мы создали **полное консольное приложение C#**, которое:

1. **Creates an Excel workbook C#** using Aspose.Cells.  
2. **Uses the EXPAND function in Excel** to turn a 3‑row array into a 5 × 5 block.  
3. Добавляет формулу котангенса (`COT(PI()/4)`).  
4. Сохраняет файл и при желании автоматически подгоняет ширину столбцов.

Теперь у вас есть надёжная база для любой задачи автоматизации, связанной с генерацией Excel‑файлов из .NET. Приятного кодинга, и пусть ваши таблицы всегда остаются без ошибок!

## Что изучать дальше?

Следующие руководства охватывают тесно связанные темы, которые расширяют техники, продемонстрированные в этом руководстве. Каждый ресурс включает полные работающие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и изучить альтернативные подходы к реализации в своих проектах.

- [Как создать именованные диапазоны уровня книги в Excel с использованием Aspose.Cells .NET](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)
- [Как создать и использовать объединённые диапазоны в Excel с Aspose.Cells .NET (руководство C#)](/cells/english/net/range-management/excel-union-range-aspose-cells-net/)
- [Создание Excel Workbook с диаграммами с использованием Aspose.Cells .NET | Пошаговое руководство](/cells/english/net/charts-graphs/create-excel-workbook-charts-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}