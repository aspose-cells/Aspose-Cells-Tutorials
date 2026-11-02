---
category: general
date: 2026-03-30
description: Узнайте, как форматировать числа с разделителем с помощью Aspose.Cells
  в C#. Включает установку пользовательского числового формата, добавление разделителя
  тысяч, форматирование десятичных знаков и способы форматирования ячейки.
draft: false
keywords:
- format number with separator
- set custom number format
- add thousands separator
- format decimal places
- how to format cell
language: ru
og_description: Форматирование числа с разделителем в C#. Это руководство показывает,
  как установить пользовательский числовой формат, добавить разделитель тысяч, отформатировать
  десятичные знаки и как отформатировать ячейку с помощью Aspose.Cells.
og_title: Форматирование числа с разделителем в C# – учебник Aspose.Cells
tags:
- C#
- Aspose.Cells
- Number Formatting
title: Форматирование чисел с разделителем в C# – Полное руководство по Aspose.Cells
url: /ru/net/excel-custom-number-date-formatting/format-number-with-separator-in-c-complete-aspose-cells-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Форматирование числа с разделителем в C# – Полное руководство Aspose.Cells

Когда‑то вам нужно было **format number with separator** в таблице, но вы не знали, какой вызов API использовать? Вы не одиноки — разработчики постоянно сталкиваются с тысячными разделителями, десятичными знаками и пользовательскими шаблонами при экспорте данных.  

Хорошая новость: Aspose.Cells делает это проще простого. В этом руководстве мы пройдем реальный пример, который **устанавливает пользовательский числовой формат**, **добавляет тысячный разделитель**, **форматирует десятичные знаки** и показывает, **как format cell** вывод в виде строки. К концу у вас будет готовый фрагмент кода, который можно вставить в любой .NET‑проект.

## Что покрывает это руководство

* Точный NuGet‑пакет, который нужен, и как его установить.  
* Пошаговый код, который создает книгу, записывает числовое значение и применяет пользовательский формат.  
* Почему `ExportTableOptions.ExportAsString` — предпочтительный способ получить отформатированное значение.  
* Распространённые подводные камни — например, забыть включить `ExportAsString` или использовать неправильную маску формата.  
* Как изменить маску формата, если вам нужно другое количество десятичных знаков или иной стиль разделителя.

Внешних ссылок на документацию не требуется; всё, что нужно, находится здесь. Приступим.

---

## Предварительные требования

| Требование | Причина |
|------------|---------|
| .NET 6.0 или новее | Aspose.Cells 23.10+ нацелен на .NET Standard 2.0+, поэтому .NET 6 безопасен и актуален. |
| Visual Studio 2022 (или любой IDE для C#) | Делает отладку и управление пакетами простыми. |
| NuGet‑пакет Aspose.Cells for .NET | Предоставляет классы `Workbook`, `Worksheet` и `ExportTableOptions`, которые мы будем использовать. |

Установить пакет можно через консоль диспетчера пакетов:

```powershell
Install-Package Aspose.Cells
```

И всё — никаких дополнительных DLL, без COM‑interop, только одна ссылка на NuGet.

---

## Шаг 1: Инициализация новой книги (How to Format Cell)

Первое, что мы делаем, — создаём новый экземпляр `Workbook`. Представьте его как пустой файл Excel, готовый принять данные.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create a new workbook – this is where we’ll format the cell.
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];
```

> **Почему это важно:** `Workbook` — точка входа для любой операции в Aspose.Cells. Получив первый лист (`Worksheets[0]`), мы получаем чистый холст без необходимости задавать имя листа.

---

## Шаг 2: Запись числового значения в целевую ячейку

Далее помещаем «сырой» номер в ячейку **A1**. Значение пока не отформатировано — это просто `double`.

```csharp
        // Step 2: Insert a raw numeric value.
        worksheet.Cells["A1"].PutValue(12345.6789);
```

> **Pro tip:** Используйте `PutValue` вместо `PutString`, если планируете позже применять числовое форматирование. Это сохраняет исходный тип данных, позволяя выполнять совместимые с Excel вычисления.

---

## Шаг 3: Установка пользовательского числового формата (Add Thousands Separator & Format Decimal Places)

Теперь к делу: определяем маску формата, которая указывает Aspose.Cells, как отображать число. Маска `#,##0.00` делает три вещи:

1. **`#,##0`** — добавляет тысячный разделитель (по умолчанию запятая).  
2. **`.00`** — фиксирует ровно два десятичных знака.  

Если нужно другое количество знаков после запятой, просто измените количество `0` после точки.

```csharp
        // Step 3: Configure the custom number format.
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,          // Return the value as a formatted string.
            NumberFormat = "#,##0.00"       // Add thousands separator and fix to 2 decimals.
        };
```

> **Почему мы используем `ExportAsString`**: По умолчанию `ExportString` возвращает «сырое» значение. Установка `ExportAsString = true` заставляет API применить маску `NumberFormat` перед преобразованием в текст. Это критично, когда требуется точное строковое представление для отчётов, JSON‑payload'ов или отображения в UI.

---

## Шаг 4: Экспорт отформатированного текста (How to Format Cell)

С готовыми параметрами вызываем `ExportString` для той же ячейки. Метод учитывает только что заданную маску и возвращает красиво отформатированную строку.

```csharp
        // Step 4: Export the formatted value.
        string formattedCellText = worksheet.Cells["A1"].ExportString(exportOptions);

        // Step 5: Show the result.
        Console.WriteLine(formattedCellText); // Expected output: 12,345.68
    }
}
```

Запуск программы выводит **`12,345.68`** в консоль — точно тот формат, который мы задали.

> **Edge case:** Если исходное число имеет более двух десятичных знаков, маска округляет его. Если требуется усечение вместо округления, предварительно обработайте значение с помощью `Math.Truncate` перед вызовом `PutValue`.

---

## Шаг 5: Настройка формата — распространённые варианты

### 5.1 Изменить точность десятичных знаков

Нужны три знака после запятой? Просто замените маску:

```csharp
NumberFormat = "#,##0.000"   // → 12,345.679
```

### 5.2 Использовать иной тысячный разделитель

В некоторых локалях предпочитают пробел или точку. Можно вставить символ напрямую:

```csharp
NumberFormat = "# ##0.00"    // Uses a non‑breaking space as separator.
```

Или полагаться на настройки культуры книги:

```csharp
workbook.Settings.CultureInfo = new System.Globalization.CultureInfo("de-DE");
NumberFormat = "#.##0,00";   // German style: 12.345,68
```

### 5.3 Префикс или суффикс (валюта, процент)

Добавьте знак доллара или процент прямо в маску:

```csharp
NumberFormat = "$#,##0.00";   // → $12,345.68
NumberFormat = "0.00%";       // → 1,234,568.00%
```

> **Note:** Маска чувствительна к регистру. `$` и `%` — буквальные символы; они не влияют на само числовое значение.

---

## Шаг 6: Полный рабочий пример (Copy‑Paste Ready)

Ниже полностью готовая программа, которую можно скопировать в новое консольное приложение. В ней присутствуют все шаги, комментарии и проверка конечного вывода.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialise workbook and worksheet.
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ Write raw numeric value to A1.
        worksheet.Cells["A1"].PutValue(12345.6789);

        // 3️⃣ Define custom format: thousands separator + two decimals.
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            NumberFormat = "#,##0.00"
        };

        // 4️⃣ Export the formatted string.
        string result = worksheet.Cells["A1"].ExportString(exportOptions);

        // 5️⃣ Display the outcome.
        Console.WriteLine(result); // Output: 12,345.68

        // Optional: keep console open.
        Console.WriteLine("Press any key to exit...");
        Console.ReadKey();
    }
}
```

Запустите программу (`dotnet run` в терминале или нажмите F5 в Visual Studio) — увидите отформатированное число, выведенное точно как в примере.

---

## Часто задаваемые вопросы (FAQ)

**Q: Работает ли это со старыми версиями Excel?**  
A: Да. Маска формата следует нативному синтаксису Excel, поэтому любая версия, понимающая `#,##0.00`, отобразит одинаковую строку.

**Q: Что делать, если нужно отформатировать диапазон ячеек?**  
A: Пройдитесь в цикле по нужному диапазону и примените те же `ExportTableOptions` к каждой ячейке, либо задайте свойство `Style.Custom` для диапазона и затем вызовите `ExportString` у одной ячейки.

**Q: Можно ли экспортировать напрямую в CSV с применёнными форматами?**  
A: Конечно. После установки формата в каждой ячейке выполните `Workbook.Save("output.csv", SaveFormat.CSV);`. Aspose.Cells учитывает `Style` ячейки при генерации CSV.

---

## Заключение

Мы только что показали, как **format number with separator** в C# с помощью Aspose.Cells, охватив всё от **set custom number format** до **add thousands separator**, **format decimal places** и важного **how to format cell** для экспорта в строку. Код полностью автономный, работает с .NET 6+ и может быть адаптирован под любую локаль или требуемую точность.

Дальше вы можете изучить:

* Применение той же техники к датам и времени (`NumberFormat = "dd‑MMM‑yyyy"`).  
* Автоматизацию массового экспорта, где каждый столбец требует своей маски.  
* Интеграцию отформатированных строк в PDF‑отчёты с помощью Aspose.Words.

Попробуйте, и вы быстро станете экспертом по форматированию таблиц в своей команде. Happy coding!   ![Screenshot showing formatted number with separator in Aspose.Cells](image-placeholder.png){alt="Отформатированное число с разделителем, отображаемое в выводе Aspose.Cells"} 

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}