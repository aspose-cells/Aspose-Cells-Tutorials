---
category: general
date: 2026-10-26
description: Узнайте, как задать пользовательский числовой формат в файле Excel на
  C#, настроив значимые цифры, создав рабочую книгу Excel и сохранив её как документ
  XLSX.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- custom number format excel
- set significant digits
- how to set number format
- create excel workbook c#
- save workbook xlsx
language: ru
lastmod: 2026-10-26
og_description: Пользовательский числовой формат Excel в C# позволяет управлять значимыми
  цифрами, создавать рабочую книгу Excel и сохранять её в формате XLSX. Следуйте этому
  полному руководству.
og_image_alt: Excel cell A1 displaying a number formatted with 4 significant digits
  using C#
og_title: Пользовательский числовой формат Excel в C# – пошаговое руководство
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn how to set a custom number format excel file in C# by configuring
    significant digits, creating an Excel workbook, and saving it as an XLSX document.
  headline: How to apply a custom number format excel in C#
  type: TechArticle
- description: Learn how to set a custom number format excel file in C# by configuring
    significant digits, creating an Excel workbook, and saving it as an XLSX document.
  name: How to apply a custom number format excel in C#
  steps:
  - name: Using a custom format string instead of global options
    text: 'If you need a format that applies only to a single range, you can assign
      a format string directly:'
  - name: Applying the setting to an entire column
    text: '```csharp // Apply the same significant‑digit rule to column B ws.Cells.Columns[1].ApplyNumberFormatOptions(
      new NumberFormatOptions { SignificantDigits = 4 }); ```'
  - name: Dealing with negative numbers
    text: 'The global `SignificantDigits` option works uniformly for positive and
      negative numbers. If you want a different display for negatives, combine it
      with a custom format:'
  type: HowTo
tags:
- Excel
- C#
- Aspose.Cells
title: Как применить пользовательский числовой формат Excel в C#
url: /ru/net/excel-custom-number-date-formatting/how-to-apply-a-custom-number-format-excel-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как применить custom number format excel в C#

Если вам нужен **custom number format excel**, который отображает определённое количество значимых цифр, это руководство покажет, как сделать это в C#. Вы увидите, как задать значимые цифры, создать рабочую книгу Excel и сохранить её как файл XLSX — всё это с помощью нескольких строк кода.

Работа с файлами Excel программно часто требует контроля над тем, как числа отображаются. С помощью Aspose.Cells для .NET вы можете определить глобальную опцию number‑format, которая заставит каждую числовую ячейку учитывать заданное количество значимых цифр. Это руководство охватывает полный рабочий процесс, от настройки проекта до проверки результата в Excel.

## Требования

Перед началом убедитесь, что у вас есть:

* .NET 6.0 или более поздняя версия (код также работает с .NET Framework 4.7.2+)
* Visual Studio 2022 или любой предпочитаемый вами IDE для C#
* Пакет NuGet **Aspose.Cells** (`Install-Package Aspose.Cells`) — полностью управляемая библиотека для работы с Excel
* Базовое знакомство с синтаксисом C#

## Шаг 1: Создать рабочую книгу Excel в C#

Первая операция — создать новый объект `Workbook`. Этот объект представляет весь файл Excel в памяти.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook instance
        Workbook wb = new Workbook();

        // The workbook now contains a default worksheet named "Sheet1"
        // You can access it via the Worksheets collection.
        Worksheet ws = wb.Worksheets[0];
```

**Почему это важно:** `Workbook` является точкой входа для любой операции с Excel. Создав его первым, вы получаете чистый файл, который позже можно сохранить как XLSX.

## Шаг 2: Настроить числовой формат для задания значимых цифр

Aspose.Cells предоставляет глобальную настройку `NumberFormatOptions`. Установив `SignificantDigits = 4`, каждая числовая ячейка будет отображать до четырёх значимых цифр, если более специфичный формат не переопределит её.

```csharp
        // Step 2: Set the global number‑format option to 4 significant digits
        WorkbookSettings.SetNumberFormatOptions(
            new NumberFormatOptions { SignificantDigits = 4 });
```

**Почему это важно:** Использование `SetNumberFormatOptions` позволяет задать **custom number format excel** без необходимости писать строку формата для каждой ячейки. Это аналог опции «Significant Digits», которую вы находите в диалоговом окне Excel *Format Cells → Number → Custom*.

## Шаг 3: Записать значения и проверить пользовательский числовой формат

Теперь поместите числовое значение в ячейку. Глобальная настройка автоматически применит правило в 4 цифры.

```csharp
        // Step 3: Write a numeric value into cell A1 (row 0, column 0)
        ws.Cells[0, 0].PutValue(123.456789);

        // Optional: Add a label so you can see the effect in Excel
        ws.Cells[0, 1].PutValue("Original value:");
        ws.Cells[0, 2].PutValue(123.456789);
```

При открытии сохранённого файла ячейка **A1** отобразит `123.5` (округлено до четырёх значимых цифр). Исходное значение остаётся неизменным в данных, что можно подтвердить, посмотрев на строку формул.

**Подсказка для граничных случаев:** Если вы сохраняете очень большое число, например `12345678.9`, та же настройка отобразит `1.235E+07` (научная нотация), поскольку Excel выбирает наиболее компактное представление, сохраняя четыре значимых цифры.

## Шаг 4: Сохранить рабочую книгу как XLSX

Наконец, запишите рабочую книгу на диск. Метод `Save` автоматически выбирает формат файла по расширению.

```csharp
        // Step 4: Save the workbook to an XLSX file
        string outputPath = @"C:\Temp\SigDigits.xlsx";
        wb.Save(outputPath);

        // Inform the user
        System.Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

**Почему это важно:** Сохранение как **XLSX** (`save workbook xlsx`) обеспечивает максимальную совместимость с современными версиями Excel, Office 365 и другими табличными инструментами.

## Ожидаемый результат

Откройте *C:\Temp\SigDigits.xlsx* в Microsoft Excel. Вы должны увидеть:

| A          | B               | C               |
|------------|-----------------|-----------------|
| **123.5**  | Исходное значение: | **123.456789**  |

*Ячейка A1* показывает число, округлённое до четырёх значимых цифр, тогда как *C1* сохраняет полную точность для сравнения.

## Общие варианты и как задать числовой формат для конкретных ячеек

### Использование пользовательской строки формата вместо глобальных параметров

Если нужен формат, применимый только к одному диапазону, можно задать строку формата напрямую:

```csharp
ws.Cells["D1"].PutValue(0.0012345);
Style style = wb.CreateStyle();
style.Custom = "0.####"; // shows up to 4 decimal places, not significant digits
ws.Cells["D1"].SetStyle(style);
```

### Применение настройки ко всему столбцу

```csharp
// Apply the same significant‑digit rule to column B
ws.Cells.Columns[1].ApplyNumberFormatOptions(
    new NumberFormatOptions { SignificantDigits = 4 });
```

### Работа с отрицательными числами

Глобальная опция `SignificantDigits` работает одинаково для положительных и отрицательных чисел. Если требуется иной вид отображения для отрицательных, комбинируйте её с пользовательским форматом:

```csharp
Style negStyle = wb.CreateStyle();
negStyle.Custom = "#,##0.###;[Red]-#,##0.###";
ws.Cells["E1"].PutValue(-9876.54321);
ws.Cells["E1"].SetStyle(negStyle);
```

## Полезные советы и подводные камни

* **Pro tip:** Устанавливайте параметры number‑format **до** записи любых данных. Изменение параметра после заполнения ячеек не переоформит уже существующие значения.
* **Watch out for:** Использование `PutValue` со **строкой**, похожей на число (например, `"123.45"`). Excel будет рассматривать её как текст, и пользовательский формат не применится.
* **Performance note:** Глобальные настройки дешёвые, но применение стиля к миллионам ячеек может увеличить использование памяти. По возможности используйте форматирование на уровне столбца.

## Следующие шаги

Теперь, когда вы умеете **custom number format excel** файлы с учётом значимых цифр, вы можете изучить:

* **How to set number format** для дат и валют с использованием `Style.Custom`.
* **Creating charts** которые учитывают ваши пользовательские форматы.
* **Exporting to CSV** с сохранением числовой точности (`save workbook xlsx` → `wb.Save("file.csv", SaveFormat.Csv)`).

Эти темы опираются на те же концепции `Workbook` и `Worksheet`, продемонстрированные здесь.

---

**Итоги**

Вы узнали, как выполнить **custom number format excel**, настроив `NumberFormatOptions` для **set significant digits**, создав рабочую книгу Excel в C#, записав значения и **saved the workbook as an XLSX** файл. Полный, готовый к запуску код выше показывает каждый шаг, объясняет, почему он необходим, и даёт советы по распространённым вариантам. Смело адаптируйте фрагменты под свои проекты и экспериментируйте с другими сценариями форматирования.

## Что вам стоит изучить дальше?

Следующие руководства охватывают тесно связанные темы, построенные на техниках, продемонстрированных в этом руководстве. Каждый ресурс включает полностью рабочие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы в ваших проектах.

- [Пользовательский числовой формат Excel в C# – Полное руководство](/cells/english/net/excel-custom-number-date-formatting/custom-number-format-excel-in-c-complete-guide/)
- [Создание рабочей книги Excel C# – Ограничение значимых цифр в Excel](/cells/english/net/excel-custom-number-date-formatting/create-excel-workbook-c-limit-significant-digits-excel/)
- [Как применить number format excel с Aspose.Cells](/cells/english/net/excel-custom-number-date-formatting/how-to-apply-number-format-excel-with-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}