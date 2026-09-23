---
category: general
date: 2026-03-18
description: Учебник по преобразованию листа Excel в PNG, показывающий, как экспортировать
  сводную таблицу, установить область печати сводной таблицы и экспортировать изображение
  диапазона Excel с использованием Aspose.Cells.
draft: false
keywords:
- excel sheet to png
- how to export pivot
- set print area pivot
- export excel range image
- export worksheet to image
language: ru
og_description: Учебник по преобразованию листа Excel в PNG, который пошагово покажет,
  как экспортировать сводные таблицы, установить область печати сводной таблицы и
  экспортировать изображение диапазона Excel с помощью C#.
og_title: Excel лист в PNG – Полное руководство по экспорту сводных таблиц
tags:
- Aspose.Cells
- C#
- Excel automation
title: Excel лист в PNG – экспорт сводной таблицы в PNG на C#
url: /ru/net/conversion-and-rendering/excel-sheet-to-png-export-a-pivot-table-as-png-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# excel sheet to png – Экспорт сводной таблицы в PNG в C#

Когда‑то вам нужно было превратить **excel sheet to png**, но вы не знали, как захватить только сводную таблицу? Вы не одиноки. Во многих конвейерах отчетности визуализация свода — звезда, а экспорт её в PNG позволяет вставлять её в письма, дашборды или документацию без необходимости включать всю книгу.

В этом руководстве мы покажем, **как экспортировать pivot**, **установить область печати pivot**, и, наконец, **экспортировать excel range image**, чтобы вы получили чистый файл **export worksheet to image**. Никаких загадочных ссылок на внешние документы — только полностью готовый фрагмент кода и объяснение каждой строки.

## Что понадобится

- **Aspose.Cells for .NET** (пакет NuGet `Aspose.Cells` – версия 23.12 или новее).  
- Среда разработки .NET (Visual Studio, Rider или `dotnet` CLI).  
- Файл Excel (`input.xlsx`), содержащий хотя бы одну сводную таблицу.

Вот и всё. Если у вас есть всё перечисленное, приступаем.

## Шаг 1 – Загрузить книгу и получить первый лист

Прежде чем работать со сводом, нам нужна книга в памяти.

```csharp
using Aspose.Cells;
using System.Drawing.Imaging;

namespace PivotToPngDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Load the workbook from disk
            Workbook workbook = new Workbook(@"C:\Data\input.xlsx");

            // Get the first worksheet (index 0)
            Worksheet worksheet = workbook.Worksheets[0];
```

*Почему это важно:* Загрузка файла дает доступ ко всем объектам (таблицам, диаграммам, сводам). Использование первого листа — простая настройка по умолчанию; при необходимости можно заменить `0` на реальный индекс листа или его имя.

## Шаг 2 – Получить диапазон сводной таблицы

Сводная таблица живёт внутри блока ячеек. Нам нужен этот блок, чтобы указать Excel, что печатать.

```csharp
            // Assume the first pivot table on the sheet
            PivotTable pivot = worksheet.PivotTables[0];

            // The range that the pivot occupies (e.g., A1:D20)
            CellArea pivotRange = pivot.PivotTableRange;
```

*Зачем это делаем:* `PivotTableRange` сообщает точные начальные и конечные строки/столбцы. Без него экспорт включил бы весь лист, что противоречит цели **set print area pivot**.

## Шаг 3 – Определить область печати, чтобы отрисовалась только сводная таблица

Механизм печати Excel учитывает свойство `PrintArea`. Сузив его до свода, мы избегаем лишних данных или пустых ячеек.

```csharp
            // Build the address string: "StartRow,StartColumn:EndRow,EndColumn"
            string printArea = $"{pivotRange.StartRow},{pivotRange.StartColumn}:" +
                               $"{pivotRange.EndRow},{pivotRange.EndColumn}";

            worksheet.PageSetup.PrintArea = printArea;
```

*Совет:* Если на том же листе несколько сводов, их диапазоны можно объединить через запятую (`"0,0:10,5,12,0:22,5"`). Это и есть техника **export excel range image** для нескольких блоков.

## Шаг 4 – Настроить параметры экспорта изображения (формат PNG)

Aspose.Cells позволяет точно настроить вывод. PNG — без потерь, идеально подходит для чётких визуалов свода.

```csharp
            // Configure image export options
            ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
            {
                ImageFormat = ImageFormat.Png,
                // Optional: increase resolution for sharper output
                HorizontalResolution = 300,
                VerticalResolution = 300
            };
```

*Почему PNG?* В отличие от JPEG, PNG сохраняет резкость текста и поддерживает прозрачный фон, что делает его предпочтительным для сценариев **excel sheet to png**.

## Шаг 5 – Экспортировать лист (область свода) в файл PNG

Теперь происходит магия — рендерим определённую область печати в изображение.

```csharp
            // Export the first page (index 0) of the worksheet to an image
            // The page corresponds to the print area we set earlier
            worksheet.ToImage(0, imgOptions).Save(@"C:\Data\pivot.png");

            // Inform the user
            System.Console.WriteLine("Pivot exported to PNG successfully!");
        }
    }
}
```

*Что вы увидите:* Файл `pivot.png`, содержащий только сводную таблицу, без лишних строк и столбцов. Откройте его в любом просмотрщике изображений — и у вас будет готовый к использованию визуал.

---

## Часто задаваемые вопросы и особые случаи

### Что делать, если в книге **несколько сводных таблиц**?

Получите `PivotTableRange` каждой сводной, объедините диапазоны и присвойте полученную строку свойству `PrintArea`. Пример:

```csharp
string combinedArea = "";
foreach (PivotTable pt in worksheet.PivotTables)
{
    CellArea ca = pt.PivotTableRange;
    combinedArea += $"{ca.StartRow},{ca.StartColumn}:{ca.EndRow},{ca.EndColumn},";
}
combinedArea = combinedArea.TrimEnd(','); // Remove trailing comma
worksheet.PageSetup.PrintArea = combinedArea;
```

### Можно ли экспортировать в **другие форматы изображений**?

Конечно. Замените `imgOptions.ImageFormat = ImageFormat.Jpeg;` на `Bmp`, `Gif`, `Tiff` и т.д. Учтите, что JPEG вводит артефакты сжатия — обычно не подходит для текстовых сводов.

### Как работать с **большими сводами**, охватывающими несколько страниц?

Установите `imgOptions.OnePagePerSheet = false;`, чтобы разрешить многостраничный рендер, а затем пройдитесь по страницам в цикле:

```csharp
int pageCount = worksheet.PageCount;
for (int i = 0; i < pageCount; i++)
{
    worksheet.ToImage(i, imgOptions).Save($@"C:\Data\pivot_page{i + 1}.png");
}
```

### Что происходит с **скрытыми строками/столбцами**?

Aspose учитывает настройки видимости листа. Если нужно игнорировать скрытые элементы, временно сделайте их видимыми перед экспортом или скорректируйте `PrintArea` вручную.

---

## Полный рабочий пример (готов к копированию)

```csharp
using Aspose.Cells;
using System.Drawing.Imaging;

namespace PivotToPngDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load workbook & select sheet
            Workbook workbook = new Workbook(@"C:\Data\input.xlsx");
            Worksheet worksheet = workbook.Worksheets[0];

            // 2️⃣ Get the first pivot table's range
            PivotTable pivot = worksheet.PivotTables[0];
            CellArea pivotRange = pivot.PivotTableRange;

            // 3️⃣ Set print area to the pivot only
            string printArea = $"{pivotRange.StartRow},{pivotRange.StartColumn}:" +
                               $"{pivotRange.EndRow},{pivotRange.EndColumn}";
            worksheet.PageSetup.PrintArea = printArea;

            // 4️⃣ Prepare PNG export options
            ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
            {
                ImageFormat = ImageFormat.Png,
                HorizontalResolution = 300,
                VerticalResolution = 300
            };

            // 5️⃣ Export to PNG
            worksheet.ToImage(0, imgOptions).Save(@"C:\Data\pivot.png");

            System.Console.WriteLine("✅ Pivot exported to PNG at C:\\Data\\pivot.png");
        }
    }
}
```

Запустите программу, и файл `pivot.png` появится там, куда вы указали. Откройте его — вы увидите чёткую отрисовку только сводной таблицы, без лишних элементов.

---

## Заключение

Теперь у вас есть **полное, сквозное решение** для превращения **excel sheet to png**, сосредоточенного исключительно на сводной таблице. Установив **print area pivot**, настроив **image export options** и используя метод `ToImage` из Aspose.Cells, вы можете автоматизировать генерацию отчётов, встраивать визуалы в веб‑страницы или просто архивировать снимки аналитики.

Что дальше? Попробуйте заменить PNG на высоко‑разрешённый PDF (`ImageFormat.Pdf`), поэкспериментируйте с несколькими сводами на одном листе или комбинируйте этот подход с экспортом диаграмм для полноценного конвейера экспорта дашборда.

Есть свои находки? Оставляйте комментарий или переходите к следующему уроку, где мы разберём **export worksheet to image** для снимков всего листа, включая диаграммы и условное форматирование. Приятного кодинга!  

<img src="pivot.png" alt="пример excel sheet to png экспорта сводной таблицы">

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}