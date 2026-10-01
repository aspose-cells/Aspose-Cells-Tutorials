---
category: general
date: 2026-02-21
description: Сохраните Excel в формате txt с точным контролем значимых цифр. Экспортируйте
  Excel в txt на C# и легко задавайте значимые цифры.
draft: false
keywords:
- save excel as txt
- export excel to txt
- set significant digits
- save workbook as text
- export numbers to txt
language: ru
og_description: Быстро сохраняйте Excel в txt. Узнайте, как экспортировать Excel в
  txt, задавать значимые цифры и управлять выводом текста с помощью C#.
og_title: Сохранить Excel как txt – экспортировать числа со значимыми цифрами в C#
tags:
- C#
- Aspose.Cells
- Excel automation
title: Сохранить Excel в txt – Полное руководство C# по экспорту чисел с значимыми
  цифрами
url: /ru/net/converting-excel-files-to-other-formats/save-excel-as-txt-complete-c-guide-to-export-numbers-with-si/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Сохранить Excel как txt – Полное руководство C# по экспорту чисел с значимыми цифрами

Когда‑то вам нужно **сохранить Excel как txt**, но вы боитесь, что числа потеряют точность? Вы не одиноки. Многие разработчики сталкиваются с проблемой при экспорте Excel в txt и получают либо слишком много знаков после запятой, либо «округлённый» беспорядок.  

В этом руководстве мы покажем простой способ **экспортировать Excel в txt**, одновременно **устанавливая значимые цифры**, чтобы результат выглядел точно так, как вам нужно. К концу вы получите готовый к запуску фрагмент C#, который сохраняет рабочую книгу как текст, экспортирует числа в txt и даёт полный контроль над числовым форматом.

## Что вы узнаете

- Как создать новую рабочую книгу и записать числовые данные.  
- Правильный способ **установки значимых цифр** с помощью `TxtSaveOptions`.  
- Как **сохранить рабочую книгу как текст** и проверить результат.  
- Обработка граничных случаев (большие числа, отрицательные значения, проблемы с локалью).  
- Быстрые советы по дальнейшему улучшению вывода (изменение разделителя, кодировка).

### Предварительные требования

- .NET 6.0 или новее (код также работает на .NET Framework 4.6+).  
- Пакет NuGet **Aspose.Cells** (`Install-Package Aspose.Cells`).  
- Базовое понимание синтаксиса C# — глубокие знания Excel‑interop не требуются.

> **Pro tip:** Если вы используете Visual Studio, включите *nullable reference types* (`<Nullable>enable</Nullable>`), чтобы заранее отлавливать потенциальные ошибки с null.

---

## Шаг 1: Инициализировать Workbook и записать число

Сначала нам нужен объект рабочей книги. Считайте его в‑памяти представлением файла Excel.  

```csharp
using Aspose.Cells;
using System;

// Create a new workbook (starts with one worksheet by default)
var workbook = new Workbook();
var worksheet = workbook.Worksheets[0];

// Write a numeric value into cell A1 (row 0, column 0)
worksheet.Cells[0, 0].PutValue(12345.6789);
```

**Почему это важно:**  
Создание рабочей книги программно избавляет от накладных расходов COM‑interop, а `PutValue` автоматически определяет тип данных, гарантируя, что ячейка рассматривается как число, а не как строка.

---

## Шаг 2: Настроить TxtSaveOptions для управления значимыми цифрами

Класс `TxtSaveOptions` — это место, где происходит магия. Устанавливая `SignificantDigits`, вы говорите Aspose.Cells, сколько значимых цифр сохранять при записи файла.

```csharp
// Configure text save options – keep only 4 significant digits
var txtSaveOptions = new TxtSaveOptions
{
    // 4 significant digits means 12345.6789 becomes 12350
    SignificantDigits = 4,

    // Optional: change delimiter if you need CSV‑style output
    // Delimiter = ',',

    // Optional: force UTF‑8 encoding for broader character support
    // Encoding = System.Text.Encoding.UTF8
};
```

**Зачем это нужно:**  
При **экспорте чисел в txt** часто требуется компактное представление (например, для систем отчётности, принимающих только определённую точность). Свойство `SignificantDigits` гарантирует одинаковое округление независимо от длины исходного числа.

---

## Шаг 3: Сохранить рабочую книгу как текстовый файл

Теперь запишем рабочую книгу на диск, используя только что определённые параметры.

```csharp
// Define the output path – adjust to your environment
string outputPath = @"C:\Temp\Numbers.txt";

// Save the workbook as a .txt file with the configured options
workbook.Save(outputPath, txtSaveOptions);

Console.WriteLine($"Workbook saved as txt at: {outputPath}");
```

**Что вы увидите:**  
Откройте `Numbers.txt` — в нём будет одна строка:

```
12350
```

Исходное `12345.6789` было округлено до **четырёх значимых цифр**, как и требовалось.

---

## Шаг 4: Проверить результат (необязательно, но рекомендуется)

Автоматические тесты — хорошая привычка. Вот быстрая проверка, которую можно выполнить сразу после сохранения:

```csharp
// Read back the file to confirm the content
string fileContent = System.IO.File.ReadAllText(outputPath).Trim();

if (fileContent == "12350")
{
    Console.WriteLine("✅ Export succeeded – significant digits applied correctly.");
}
else
{
    Console.WriteLine($"⚠️ Unexpected output: {fileContent}");
}
```

Запуск этого блока выведет зелёную галочку, если всё совпадает, давая уверенность, что операция **save excel as txt** прошла корректно.

---

## Распространённые варианты и граничные случаи

### Экспорт нескольких ячеек или диапазонов

Если нужно **export excel to txt** для целого диапазона, просто заполните больше ячеек перед сохранением:

```csharp
worksheet.Cells[0, 1].PutValue(0.000123456);
worksheet.Cells[0, 2].PutValue(-98765.4321);
```

Тот же `TxtSaveOptions` применит правило 4‑х цифр к каждому значению, получив:

```
12350
0.0001235
-98800
```

### Изменение разделителя

Некоторые системы ожидают табуляцию в качестве разделителя. Измените его так:

```csharp
txtSaveOptions.Delimiter = '\t'; // Tab character
```

Теперь каждая ячейка в строке будет разделена табом.

### Обработка локаль‑специфичных десятичных разделителей

Если ваша аудитория использует запятые в качестве десятичных знаков, задайте культуру:

```csharp
txtSaveOptions.CultureInfo = new System.Globalization.CultureInfo("fr-FR");
```

Вывод будет учитывать локаль, превращая `12350` в `12 350` (пробел как разделитель тысяч во французском).

---

## Полный рабочий пример (готов к копированию)

```csharp
using Aspose.Cells;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // 1️⃣ Create workbook and write numbers
        var workbook = new Workbook();
        var sheet = workbook.Worksheets[0];
        sheet.Cells[0, 0].PutValue(12345.6789);
        sheet.Cells[0, 1].PutValue(0.000123456);
        sheet.Cells[0, 2].PutValue(-98765.4321);

        // 2️⃣ Configure save options – 4 significant digits
        var txtOptions = new TxtSaveOptions
        {
            SignificantDigits = 4,
            // Delimiter = '\t',               // Uncomment for TSV
            // Encoding = System.Text.Encoding.UTF8,
            // CultureInfo = new System.Globalization.CultureInfo("en-US")
        };

        // 3️⃣ Save to text file
        string path = Path.Combine(Environment.GetFolderPath(Environment.SpecialFolder.Desktop), "Numbers.txt");
        workbook.Save(path, txtOptions);
        Console.WriteLine($"File saved to {path}");

        // 4️⃣ Verify result (optional)
        string result = File.ReadAllText(path).Trim();
        Console.WriteLine($"File content: {result}");
    }
}
```

**Ожидаемое содержимое `Numbers.txt` (разделитель по умолчанию, 4 значимые цифры):**

```
12350	0.0001235	-98800
```

Табуляция (`\t`) видна, потому что мы оставили разделитель по умолчанию (таб). При желании замените её запятой для CSV.

---

## Заключение

Теперь вы точно знаете, **как сохранить Excel как txt**, контролируя количество значимых цифр. Шаги — создание рабочей книги, установка `TxtSaveOptions.SignificantDigits` и сохранение — это всё, что нужно для надёжного **export excel to txt**.  

Дальше вы можете:

- **Export numbers to txt** для больших наборов данных.  
- Настраивать разделители, кодировку или параметры культуры под любые downstream‑системы.  
- Комбинировать этот подход с другими возможностями Aspose.Cells (стили, формулы) перед экспортом.

Попробуйте, измените `SignificantDigits` на 2 или 6 и посмотрите, как меняется вывод. Гибкость **save workbook as text** делает её полезным инструментом в любой цепочке обмена данными.

---

### Связанные темы, которые могут быть интересны

- **Export Excel to CSV** с пользовательским порядком столбцов.  
- **Read txt files back into a workbook** (`Workbook.Load` с `LoadOptions`).  
- **Batch processing** нескольких листов и их объединение в один txt‑файл.  
- **Performance tuning** для экспорта больших объёмов (стриминг vs. in‑memory).

Не стесняйтесь оставлять комментарии, если столкнётесь с проблемами, или делиться тем, как вы кастомизировали экспорт в своих проектах. Приятного кодинга!  

---  

*Image: A screenshot of the generated `Numbers.txt` file showing rounded values.*  
*Alt text: “Numbers.txt file displaying 12350, 0.0001235, and -98800 after saving Excel as txt with 4 significant digits.”*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}