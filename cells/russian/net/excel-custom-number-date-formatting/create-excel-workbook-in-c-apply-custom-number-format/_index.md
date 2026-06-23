---
category: general
date: 2026-05-23
description: Создайте рабочую книгу Excel на C# и изучите, как применить пользовательский
  числовой формат, программно задать стиль ячейки, отформатировать ячейку в научной
  нотации, затем сохранить книгу в формате xlsx.
draft: false
keywords:
- create excel workbook
- apply custom number format
- format cell scientific notation
- set cell style programmatically
- save workbook to xlsx
language: ru
og_description: Быстро создайте Excel‑книгу в C#. Научитесь применять пользовательские
  числовые форматы, программно оформлять ячейки, форматировать научную нотацию и сохранять
  в xlsx.
og_title: Создание рабочей книги Excel на C# – Применение пользовательского числового
  формата
schemas:
- author: Aspose
  dateModified: '2026-05-23'
  description: Create excel workbook in C# and learn how to apply custom number format,
    set cell style programmatically, format cell scientific notation, then save workbook
    to xlsx.
  headline: Create Excel Workbook in C# – Apply Custom Number Format
  type: TechArticle
tags:
- C#
- Excel
- Aspose.Cells
- Automation
title: Создание книги Excel в C# – Применение пользовательского числового формата
url: /ru/net/excel-custom-number-date-formatting/create-excel-workbook-in-c-apply-custom-number-format/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание Excel Workbook в C# – Применение пользовательского числового формата

Создать Excel workbook в C# проще, чем вы думаете. В этом руководстве мы пройдемся по применению пользовательского числового формата, форматированию ячейки в научной нотации, программной установке стиля ячейки и, наконец, сохранению книги в файл xlsx.

Если вы когда‑нибудь смотрели на пустую таблицу и задавались вопросом, как автоматизировать весь процесс — от заполнения данными до отображения чисел именно так, как вам нужно — это руководство для вас. К концу вы получите полностью функционирующий Excel‑файл, который можно открыть в любой программе для работы с таблицами, и поймёте **почему** каждый шаг важен, а не только **как** написать код.

## Что понадобится

- **.NET 6+** (или любой современный .NET Framework, поддерживающий библиотеку)  
- **Aspose.Cells for .NET** (или другой API, предоставляющий классы `Workbook`, `Cell` и `CellFormat`)  
- Небольшой опыт работы с C# — если вы умеете писать `Console.WriteLine`, вы готовы к работе.  

Никаких дополнительных файлов конфигурации, без COM‑interop и, конечно же, без необходимости ручной установки Excel.

---

## Создание Excel Workbook – Инициализация объекта Workbook

Первое, что нам нужно сделать, — создать пустую книгу. Представьте класс `Workbook` как чистый холст, на котором вы будете «рисовать» строки, столбцы и стили.

```csharp
using Aspose.Cells;   // Make sure the Aspose.Cells namespace is referenced

// Step 1: Create a new workbook instance
Workbook workbook = new Workbook();
```

Вот и всё — одна строка, и у вас в памяти появляется совершенно новый Excel‑файл. Конструктор `Workbook` создаёт коллекцию листов по умолчанию, так что можно сразу начинать добавлять данные.

> **Pro tip:** Если нужны несколько листов, вызовите `workbook.Worksheets.Add()` перед тем, как заполнять ячейки.

![Create excel workbook example](image-placeholder.png "Create excel workbook screenshot")

*Image alt text: пример создания Excel workbook, показывающий пустой лист Excel в IDE.*

## Применение пользовательского числового формата к ячейке

Теперь, когда книга существует, поместим число в ячейку **A1** и зададим ей пользовательский формат. Пользовательские числовые форматы позволяют контролировать отображение чисел — валюту, проценты, даты или, в нашем случае, научную нотацию.

```csharp
// Step 2: Grab the first worksheet and the cell at A1 (row 0, column 0)
Worksheet sheet = workbook.Worksheets[0];
Cell cell = sheet.Cells[0, 0];

// Step 3: Insert a numeric value
cell.PutValue(12345.6789);

// Step 4: Retrieve the current style so we can modify its Number format
Style style = cell.GetStyle();

// Step 5: Define a custom scientific notation format with two decimal places
style.Custom = "0.00E+00";   // This is the “apply custom number format” part

// Step 6: Push the modified style back onto the cell
cell.SetStyle(style);
```

Зачем сначала получать стиль? Потому что объект `Cell` хранит объект **Style**, содержащий шрифты, границы, выравнивание и числовое форматирование в одном месте. Изменяя свойство `Custom`, мы говорим Excel: «отобрази это значение в научной нотации с двумя знаками после запятой».

> **Common question:** *Можно ли использовать встроенный формат вместо пользовательского?*  
> Да — установите `style.Number = 10` для встроенного научного формата, но пользовательская строка даёт точный контроль над количеством знаков после запятой.

## Программная установка стиля ячейки (бeyond Number Format)

Часто требуется больше, чем просто числовой формат. Добавим полужирный шрифт и светло‑серый фон, чтобы ячейка выделялась.

```csharp
// Optional: Enhance the cell appearance
style.Font.IsBold = true;
style.ForegroundColor = System.Drawing.Color.LightGray;
style.Pattern = BackgroundType.Solid;

// Re‑apply the enriched style
cell.SetStyle(style);
```

Обратите внимание, что мы повторно используем тот же объект `style`, который уже изменяли. В этом и заключается прелесть **set cell style programmatically** — вы получаете стиль один раз, меняете нужные свойства и записываете его обратно. Нет необходимости создавать новые объекты или терять уже установленный числовой формат.

## Форматирование ячейки в научной нотации (Edge‑Case Handling)

Если вы работаете с очень большими или очень малыми числами, научная нотация спасает ситуацию. Пользовательский формат, который мы использовали (`0.00E+00`), гарантирует два знака после запятой и принудительно ставит знак «+» перед экспонентой. Быстрая проверка:

```csharp
// Verify the format by inserting another extreme value
Cell extraCell = sheet.Cells[1, 0]; // B2
extraCell.PutValue(0.00001234);
extraCell.SetStyle(style); // Reuse the same style with scientific notation
```

При открытии полученного файла ячейка B2 будет отображаться как `1.23E-05`, подтверждая, что директива **format cell scientific notation** работает как для больших, так и для крошечных чисел.

## Сохранение книги в XLSX

Все веселье заканчивается, когда вы действительно записываете файл на диск. Метод `Save` берёт на себя тяжёлую работу, преобразуя представление в памяти в корректный пакет `.xlsx`.

```csharp
// Step 7: Persist the workbook
string outputPath = @"C:\Temp\CustomFormatted.xlsx";
workbook.Save(outputPath, SaveFormat.Xlsx);
```

Эта строка реализует цель **save workbook to xlsx**. Если каталог не существует, `Save` выбросит исключение — поэтому убедитесь, что папка создана заранее или оберните вызов в блок try/catch.

```csharp
try
{
    workbook.Save(outputPath, SaveFormat.Xlsx);
    Console.WriteLine($"Workbook saved successfully to {outputPath}");
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Failed to save workbook: {ex.Message}");
}
```

Теперь у вас есть готовый к распространению Excel‑файл с красиво отформатированным научным числом, полужирным стилем и светло‑серым фоном.

## Полный рабочий пример

Ниже представлен полностью готовый к копированию и вставке код, который связывает все части вместе. Он компилируется как консольное приложение, но вы можете перенести логику в любой C#‑проект.

```csharp
using System;
using Aspose.Cells;
using System.Drawing;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new workbook
        Workbook workbook = new Workbook();

        // 2️⃣ Access the first worksheet and target cell A1
        Worksheet sheet = workbook.Worksheets[0];
        Cell cell = sheet.Cells[0, 0];

        // 3️⃣ Insert a numeric value
        cell.PutValue(12345.6789);

        // 4️⃣ Retrieve and customize the cell style
        Style style = cell.GetStyle();
        style.Custom = "0.00E+00";               // apply custom number format (scientific)
        style.Font.IsBold = true;               // set cell style programmatically
        style.ForegroundColor = Color.LightGray;
        style.Pattern = BackgroundType.Solid;

        // 5️⃣ Apply the style back to the cell
        cell.SetStyle(style);

        // 6️⃣ Add another example to prove scientific notation works for tiny numbers
        Cell tinyCell = sheet.Cells[1, 0]; // B2
        tinyCell.PutValue(0.00001234);
        tinyCell.SetStyle(style);

        // 7️⃣ Save the workbook to an XLSX file
        string outputPath = @"C:\Temp\CustomFormatted.xlsx";
        try
        {
            workbook.Save(outputPath, SaveFormat.Xlsx);
            Console.WriteLine($"Workbook saved successfully to {outputPath}");
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Failed to save workbook: {ex.Message}");
        }
    }
}
```

**Expected outcome:** Откройте `CustomFormatted.xlsx`, и вы увидите:

| A1               | B2            |
|------------------|---------------|
| 1.23E+04         | 1.23E-05      |

Обе ячейки полужирные, имеют светло‑серый залив и отображают числа в научной нотации с двумя знаками после запятой.

---

## Wrap‑Up

Мы только что **create excel workbook** с нуля, **apply custom number format**, **format cell scientific notation**, **set cell style programmatically** и **save workbook to xlsx** — всего лишь несколькими строками C#. Подход масштабируем: просто пройдитесь по строкам, клонируйте объект `style`, и у вас будет полностью стилизованный отчёт за секунды.

### Что дальше?

- **Dynamic formatting:** Переключайте форматы в зависимости от величины значения (например, валюта vs. процент).  
- **Multiple sheets:** Используйте `workbook.Worksheets.Add("Summary")` для построения панелей управления.  
- **Advanced styling:** Границы, условное форматирование и проверка данных

## Related Tutorials

- [How to Create and Save an Excel Workbook as ODS Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [Create Save Excel Workbook Aspose Cells Dotnet](/cells/hongkong/net/workbook-operations/create-save-excel-workbook-aspose-cells-dotnet/)
- [Create Save Excel Workbook Pdf Aspnet Aspose Cells](/cells/hongkong/net/workbook-operations/create-save-excel-workbook-pdf-aspnet-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}