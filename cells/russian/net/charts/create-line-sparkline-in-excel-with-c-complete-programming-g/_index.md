---
category: general
date: 2026-06-30
description: Быстро создайте линейный спарклайн в Excel с помощью C#. Узнайте, как
  добавить спарклайн, создать рабочую книгу Excel на C# и добавить спарклайн в ячейку
  за несколько шагов.
draft: false
keywords:
- create line sparkline
- how to add sparkline
- add line sparkline
- create excel workbook c#
- add sparkline to cell
language: ru
og_description: Создайте линейный спарклайн в Excel с помощью C#. Этот учебник показывает,
  как добавить спарклайн, создать рабочую книгу Excel на C# и встроить спарклайн в
  ячейку.
og_title: Создание линейного спарклайна в Excel с помощью C# – пошаговое руководство
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Create line sparkline in Excel with C# quickly. Learn how to add sparkline,
    create Excel workbook C#, and add sparkline to cell in a few steps.
  headline: Create line sparkline in Excel with C# – Complete Programming Guide
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: Создание линейного спарклайна в Excel с помощью C# – Полное руководство по
  программированию
url: /ru/net/charts/create-line-sparkline-in-excel-with-c-complete-programming-g/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание линейного спарклайна в Excel с помощью C# – Полное руководство по программированию

Вы когда‑нибудь задумывались, как **создать линейный спарклайн** в файле Excel с помощью C#? Вы не один — разработчики постоянно спрашивают: «как добавить спарклайн в отчет без ручного открытия Excel?» Хорошая новость в том, что с помощью нескольких строк кода вы можете сгенерировать стильный линейный спарклайн прямо внутри книги, без пользовательского интерфейса.

В этом руководстве мы пройдём всё, что вам нужно знать: от основ **create Excel workbook C#**, через заполнение данными, до точных шагов для **add line sparkline** и **add sparkline to cell**. К концу вы получите готовый к использованию файл *.xlsx*, визуализирующий ежемесячные тенденции продаж одним взглядом. Без лишних слов, только практическое, исполняемое решение.

---

## Что вы создадите

- Свежая Excel‑книга с именем *KPI_Sparklines.xlsx*  
- Рабочий лист под названием **KPI**, содержащий примерные данные о продажах  
- **Линейный спарклайн**, размещённый в ячейке **D2**, ссылающийся на диапазон данных **B2:B13**  
- Базовое форматирование (цвет, толщина линии), чтобы спарклайн выделялся  

Требования? Просто .NET SDK (3.1+ или .NET 6) и бесплатная библиотека Aspose.Cells для .NET (доступна через NuGet). Если вы никогда не использовали Aspose.Cells, представьте её как мощный движок Excel, который можно вызывать из кода — без COM‑interop, без необходимости установки Excel.

![Создание линейного спарклайна в Excel с помощью C#](https://example.com/images/create-line-sparkline.png "Создание линейного спарклайна в Excel с C#")

*Текст alt изображения: пример кода создания линейного спарклайна в Excel с помощью C#*

---

## Шаг 1: **Create Excel workbook C#** – Настройка файла и листа

Сначала самое главное. Нам нужен объект книги (workbook) и лист (worksheet), где будут храниться данные. Это основа любой автоматизации Excel, независимо от того, будете ли вы позже **add line sparkline** или писать формулы.

```csharp
using Aspose.Cells;
using System.Drawing;

// Initialize a new workbook
Workbook workbook = new Workbook();

// Grab the first worksheet (index 0) and give it a meaningful name
Worksheet worksheet = workbook.Worksheets[0];
worksheet.Name = "KPI";   // “KPI” will hold our key performance indicators
```

> **Почему это важно:** Класс `Workbook` представляет весь файл, а `Worksheet` — полотно для строк, столбцов и, в конечном итоге, нашего спарклайна. Раннее именование листа делает файл аккуратным и самодокументируемым.

---

## Шаг 2: Заполнение данными – Исходный диапазон для спарклайна

Для построения спарклайна нужны данные. Сымитируем 12‑месячные показатели продаж. Вы могли бы получить их из базы данных, но для наглядности мы сгенерируем их на лету.

```csharp
// Fill column B (index 1) with monthly sales numbers
for (int month = 0; month < 12; month++)
{
    // Example pattern: start at 5,000 and increase by 750 each month
    worksheet.Cells[month + 1, 1].PutValue(5000 + month * 750);
}
```

> **Подсказка:** `PutValue` автоматически определяет тип данных, поэтому нет необходимости приводить к `double` или `int`. Если понадобится форматировать ячейки (валюта, разделители тысяч), вы можете позже применить объект `Style`.

---

## Шаг 3: **Create line sparkline** – Добавление спарклайна в конкретную ячейку

Теперь появляется звезда шоу: **line sparkline**. Aspose.Cells группирует спарклайны, поэтому сначала мы создаём `SparklineGroup` типа `Line`, а затем указываем, где разместить визуализацию.

```csharp
// Add a new SparklineGroup of type Line
int groupIndex = worksheet.SparklineGroups.Add(SparklineType.Line);
SparklineGroup sparklineGroup = worksheet.SparklineGroups[groupIndex];

// Add a sparkline that lives in D2 (row 1, column 3) and reads data from B2:B13
// Parameters: firstRow, firstColumn, lastRow, lastColumn, firstDataRow, lastDataRow
sparklineGroup.Add(1, 3, 1, 3, 1, 12);   // D2 ↔ B2:B13
```

> **Как это работает:**  
> - `firstRow/firstColumn` и `lastRow/lastColumn` определяют *целевую ячейку* (где появляется спарклайн).  
> - `firstDataRow/lastDataRow` указывают на исходный диапазон.  
> Поскольку мы используем **line sparkline**, визуал будет простой тонкой линией, отражающей тенденцию чисел.

### Необязательно: **How to add sparkline** с пользовательским стилем

Если вы хотите, чтобы спарклайн выделялся, настройте несколько свойств:

```csharp
sparklineGroup.LineWeight = 1.0;               // Thickness of the line
sparklineGroup.SeriesColor = Color.DarkBlue;  // Color of the sparkline line
sparklineGroup.ShowMarkers = true;             // Show data markers (optional)
sparklineGroup.MarkerColor = Color.OrangeRed;  // Marker color
```

> **Почему стоит стилизовать?** Тёмно‑синяя линия на белом фоне приятна для глаз, а маркеры дают быстрый сигнал о отдельных точках данных — удобно для презентаций.

---

## Шаг 4: Сохранение книги – Проверка результата

С установленным спарклайном нам осталось только записать файл на диск. Выберите папку, в которую у вас есть права записи; в примере используется путь‑заполнитель, который следует заменить.

```csharp
// Save the workbook as an .xlsx file
string outputPath = @"C:\Temp\KPI_Sparklines.xlsx";
workbook.Save(outputPath);
```

> **Проверка:** Откройте сгенерированный файл в Excel (или любом просмотрщике, поддерживающем .xlsx). Вы должны увидеть **line sparkline** в ячейке **D2**, отражающий растущие цифры продаж в столбце **B**. При наведении курсора на спарклайн появится подсказка с исходными значениями.

---

## Шаг 5: Распространённые подводные камни при **add sparkline to cell**

Даже простой пример может вызвать затруднения у новичков. Вот несколько вещей, на которые стоит обратить внимание:

| Проблема | Почему происходит | Решение |
|----------|-------------------|---------|
| Неправильные координаты ячейки | Целевой спарклайн использует индекс столбца с нулевой базой, а индекс строки — с единичной. | Помните, что `Cells[row, column]`, где `row` — нулевая база, `column` тоже нулевая. В `SparklineGroup.Add` строки и столбцы **1‑based**. |
| Нет данных | Исходный диапазон пуст или содержит нечисловые значения. | Убедитесь, что диапазон (например, `B2:B13`) содержит числа. Используйте `PutValue` с числовыми типами. |
| Спарклайн исчезает после сохранения | Несоответствие версии библиотеки или отсутствие лицензии. | Используйте последнюю версию пакета Aspose.Cells и предоставьте действующую лицензию, если вы превысили ограничения оценки. |
| Форматирование не применилось | Изменения стиля выполнены до добавления спарклайна. | Устанавливайте стиль **после** создания группы, как показано выше. |

---

## Полный исходный код – Всё в одном месте для копирования

Ниже представлен полный готовый к запуску код. Вставьте его в новый консольный проект, добавьте пакет Aspose.Cells через NuGet и нажмите **F5**.

```csharp
using Aspose.Cells;
using System.Drawing;

namespace SparklineDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 1: Create Excel workbook C#
            // -------------------------------------------------
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.Worksheets[0];
            worksheet.Name = "KPI";

            // -------------------------------------------------
            // Step 2: Populate monthly sales data (B2:B13)
            // -------------------------------------------------
            for (int month = 0; month < 12; month++)
            {
                worksheet.Cells[month + 1, 1].PutValue(5000 + month * 750);
            }

            // -------------------------------------------------
            // Step 3: Create line sparkline and add it to D2
            // -------------------------------------------------
            int groupIdx = worksheet.SparklineGroups.Add(SparklineType.Line);
            SparklineGroup sparklineGroup = worksheet.SparklineGroups[groupIdx];
            sparklineGroup.Add(1, 3, 1, 3, 1, 12); // D2 ↔ B2:B13

            // -------------------------------------------------
            // Step 4: Optional formatting (how to add sparkline with style)
            // -------------------------------------------------
            sparklineGroup.LineWeight = 1.0;
            sparklineGroup.SeriesColor = Color.DarkBlue;
            sparklineGroup.ShowMarkers = true;
            sparklineGroup.MarkerColor = Color.OrangeRed;

            // -------------------------------------------------
            // Step 5: Save the workbook
            // -------------------------------------------------
            string outputPath = @"C:\Temp\KPI_Sparklines.xlsx";
            workbook.Save(outputPath);

            System.Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

**Ожидаемый результат:** При открытии *KPI_Sparklines.xlsx* столбец **B** содержит двенадцать чисел (5 000 → 13 250), а ячейка **D2** содержит плавный тёмно‑синий линейный спарклайн, который постепенно растёт. Маркеры отображаются как крошечные оранжево‑красные точки, если вы включили `ShowMarkers`.

---

## Что дальше? Расширение навыков работы со спарклайнами

Теперь, когда вы освоили **create line sparkline** с помощью Aspose.Cells, рассмотрите изучение следующих связанных тем:

- **Add column sparkline** – идеально подходит для отображения накопленных данных.  
- **Create multi‑sparkline groups** на том же листе для сравнения рядом.  
- **Export to PDF** с сохранением спарклайнов (Aspose.Cells поддерживает конвертацию в PDF).  
- **Dynamic data sources** – получать реальные данные о продажах из базы SQL вместо жёстко закодированных значений.  

Каждый из этих пунктов основывается на тех же базовых концепциях: **create Excel workbook C#**, заполнение данными и **add sparkline to cell** в нужном стиле.

---

### TL;DR

Мы показали, как **create line sparkline** в книге Excel с помощью C#. Шаги — *создать книгу, заполнить данными, добавить спарклайн, оформить его и сохранить* — все объединены в одной автономной программе. Не стесняйтесь менять цвета, толщину линии или диапазон источника, чтобы соответствовать требованиям вашего отчёта.

Есть свои идеи, которыми хотите поделиться? Оставьте комментарий ниже, и удачной разработки!

## Что вам стоит изучить дальше?

Следующие руководства охватывают тесно связанные темы, которые развивают техники, продемонстрированные в этом руководстве. Каждый ресурс включает полные работающие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [Автоматизация Excel: Создание книги и добавление ListBox с помощью Aspose.Cells для .NET](/cells/english/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)
- [Автоматизация Excel: Создание книги и добавление ListBox Aspose Cells](/cells/german/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)
- [Автоматизация Excel: Создание книги и добавление ListBox Aspose Cells](/cells/french/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}