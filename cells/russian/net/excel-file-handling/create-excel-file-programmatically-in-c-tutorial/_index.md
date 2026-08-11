---
category: general
date: 2026-08-11
description: Создайте Excel‑файл программно на C# с использованием Aspose.Cells. Разберите
  дату в японском календаре, запишите её в ячейку и сохраните книгу.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel file programmatically
- datetime.parseexact custom format
- write date to excel cell
- how to save excel file c#
language: ru
lastmod: 2026-08-11
og_description: Создайте файл Excel программно на C# с помощью Aspose.Cells. Узнайте,
  как разобрать дату в японской эре с помощью пользовательского формата DateTime.ParseExact,
  записать дату в ячейку Excel и эффективно сохранить книгу.
og_image_alt: Screenshot of an Excel workbook with a parsed Japanese era date in cell
  A1
og_title: Создание Excel‑файла программно на C# – полный учебник
schemas:
- author: Aspose
  dateModified: '2026-08-11'
  description: Create excel file programmatically in C# using Aspose.Cells. Parse
    a Japanese era date, write it to a cell, and save the workbook.
  headline: Create excel file programmatically in C# – tutorial
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
- DateTime parsing
title: Создание Excel‑файла программно на C# – руководство
url: /ru/net/excel-file-handling/create-excel-file-programmatically-in-c-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание Excel‑файла программно на C# – руководство

Если вам нужно **создать Excel‑файл программно**, вы можете сделать это в несколько строк кода C#. В этом руководстве показано, как сгенерировать книгу Excel с помощью Aspose.Cells, разобрать дату в японском императорском формате, используя **кастомный формат DateTime.ParseExact**, записать эту дату в ячейку листа и, наконец, **сохранить Excel‑файл в стиле C#**. К концу у вас будет готовый к использованию файл *.xlsx*, содержащий правильно преобразованную григорианскую дату.

Вы узнаете, как:

* Инициализировать книгу без шаблона.  
* Преобразовать строку с императорским обозначением, например `"R3/04/01"`, в `DateTime`.  
* Вставить значение `DateTime` в конкретную ячейку (`A1`).  
* Сохранить книгу на диск одним вызовом `Save`.

Никакие дополнительные библиотеки, помимо Aspose.Cells и базовой библиотеки классов .NET, не требуются.

---

## Предварительные требования

Перед началом убедитесь, что у вас есть:

* **.NET 6.0** или более поздняя версия (код также работает с .NET Framework 4.6+).  
* Действующая лицензия **Aspose.Cells** или бесплатная оценочная копия.  
* Базовые знания синтаксиса C# и Visual Studio (или любой другой предпочитаемой IDE).

---

## Создание Excel‑файла программно – инициализация книги

Первый шаг – создать пустой объект книги. Aspose.Cells предоставляет класс `Workbook`, который представляет весь Excel‑файл в памяти.

```csharp
using Aspose.Cells;
using System;
using System.Globalization;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook and get the first worksheet
        var workbook = new Workbook();               // creates an empty .xlsx structure
        var worksheet = workbook.Worksheets[0];      // the default first sheet is named "Sheet1"
```

**Почему это важно:**  
Создание книги программно устраняет необходимость в физическом файле‑шаблоне, что уменьшает размер развертываемого приложения и позволяет генерировать файлы «на лету» для отчетов, счетов или экспорта данных.

---

## Использование кастомного формата DateTime.ParseExact для дат в японском императорском календаре

Строки дат, содержащие японские императорские символы (например, `"R"` для Рэйва), нельзя разобрать с помощью стандартного `DateTime.Parse`. Необходимо задать **кастомный формат** и японскую культуру, распознающую обозначение эры.

```csharp
        // Step 2: Define the era‑based date string (Reiwa 3, April 1)
        string eraDate = "R3/04/01";

        // Step 3: Create a CultureInfo that knows Japanese eras
        var japaneseCulture = new CultureInfo("ja-JP");

        // Step 4: Parse the era date using a custom format string
        //   "g"  = era designator (R, H, etc.)
        //   "yy" = two‑digit year within the era
        //   "MM" = month (01‑12)
        //   "dd" = day of month (01‑31)
        DateTime parsedDate = DateTime.ParseExact(
            eraDate,
            "ggy/MM/dd",
            japaneseCulture,
            DateTimeStyles.None);
```

**Почему это важно:**  
`DateTime.ParseExact` гарантирует, что входные данные точно соответствуют указанному шаблону, исключая неоднозначности, зависящие от локали. Шаблон `"ggy/MM/dd"` указывает .NET рассматривать первый символ как эру (`g`), затем двухзначный год (`yy`), месяц и день. Использование `japaneseCulture` обеспечивает корректную интерпретацию символов эры, в результате получаем григорианский `DateTime` (`2021‑04‑01` в примере).

---

## Запись даты в ячейку Excel с помощью Aspose.Cells

Теперь, когда у вас есть экземпляр `DateTime`, его можно разместить в любой ячейке листа. Aspose.Cells автоматически применяет к ячейке стиль даты по умолчанию книги.

```csharp
        // Step 5: Write the DateTime value into cell A1
        worksheet.Cells["A1"].PutValue(parsedDate);

        // Optional: Apply a custom number format if you want a specific display
        worksheet.Cells["A1"].Style.Number = 14; // 14 = "m/d/yyyy" in Excel
```

**Почему это важно:**  
Метод `PutValue` позволяет Aspose.Cells определить тип ячейки (дата, число, текст) исходя из переданного .NET‑типа. Такой подход безопаснее, чем запись отформатированной строки, поскольку Excel сохраняет семантику даты — её можно сортировать, фильтровать и выполнять расчёты по столбцу позже.

---

## Как сохранить Excel‑файл в C# – завершение работы с книгой

Последний шаг — сохранить книгу из памяти в физический файл. Aspose.Cells поддерживает множество форматов; здесь мы используем современный формат `.xlsx`.

```csharp
        // Step 6: Save the workbook to the desired location
        string outputPath = @"C:\Temp\JapaneseEra.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

**Почему это важно:**  
Вызов `Save` с параметром `SaveFormat.Xlsx` записывает стандартизированный файл Office Open XML, который можно открыть в Excel, LibreOffice или любом просмотрщике, поддерживающем этот формат. Метод также автоматически управляет сжатием и упаковкой, так что вам не нужно вручную работать с zip‑потоками.

---

## Ожидаемый результат

При запуске программы:

| Ячейка | Значение (отображение) | Базовый тип |
|--------|------------------------|-------------|
| A1     | 4/1/2021               | Дата (DateTime) |

Файл `JapaneseEra.xlsx` будет содержать один лист с именем **Sheet1**, в ячейке **A1** будет григорианская дата `2021‑04‑01`. Excel будет рассматривать эту ячейку как дату, позволяя выполнять дальнейшие вычисления, например `=A1+30` для добавления 30 дней.

---

## Общие варианты и граничные случаи

| Ситуация | Решение |
|----------|---------|
| **Другая эра** (например, Хэйсэй `H30/12/31`) | Измените входную строку; тот же шаблон `"ggy/MM/dd"` работает, потому что `CultureInfo` для японского языка знает все эры. |
| **Четырехзначный год** (например, `"R2023/04/01"`) | Используйте `"ggyyyy/MM/dd"` в качестве строки формата. |
| **Отсутствует символ эры** | Укажите резервный формат, например `"yyyy/MM/dd"`, и попытайтесь выполнить `DateTime.TryParseExact` с несколькими шаблонами. |
| **Недопустимая дата** (например, `"R3/13/01"`) | Оберните `ParseExact` в блок `try/catch` или используйте `DateTime.TryParseExact` для корректной обработки ошибок парсинга. |

**Pro tip:** Всегда проверяйте полученный `DateTime` перед записью в лист, особенно если исходные данные поступают от пользователя или из внешних файлов.

---

## Итоги

* Вы **создали Excel‑файл программно** с помощью Aspose.Cells.  
* Вы разобрали строку с японской эрой, используя **кастомный формат DateTime.ParseExact**.  
* Вы **записали дату в ячейку Excel** через `PutValue`.  
* Вы узнали, **как сохранить Excel‑файл в C#** одним вызовом `Save`.

Эти четыре шага образуют переиспользуемый шаблон для любых сценариев, где требуется импортировать культурно‑специфичные даты в Excel‑отчеты.

---

## Следующие шаги

* Изучите **оформление ячеек** (шрифты, цвета, границы), чтобы отчеты выглядели более профессионально.  
* Используйте **Workbook.Save** в других форматах (`Csv`, `Pdf`) для экспорта данных различным аудиториям.  
* Объедините эту технику с **массовой вставкой данных** (`Cells.ImportDataTable`) для крупномасштабных импортов.  

Экспериментируйте с разными символами эр, пользовательскими числовыми форматами или несколькими листами. Основная логика — создать, разобрать, записать, сохранить — применима ко всем задачам автоматизации Excel в C#.

---


## Что следует изучить дальше?


Следующие руководства охватывают тесно связанные темы, расширяющие техники, продемонстрированные в этом пособии. Каждый ресурс содержит полностью рабочие примеры кода с пошаговыми объяснениями, помогающими освоить дополнительные возможности API и исследовать альтернативные подходы в ваших проектах.

- [Как создать и сохранить книгу Excel в формате ODS с помощью Aspose.Cells для .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [Как сохранить отдельные страницы Excel‑файла в PDF с помощью Aspose.Cells для .NET](/cells/english/net/workbook-operations/save-specific-excel-pages-pdf-aspose-cells-net/)
- [Как создать и сохранить книгу Excel в формате SVG с помощью Aspose.Cells для Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}