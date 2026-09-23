---
category: general
date: 2026-02-15
description: Создайте новую книгу и экспортируйте Excel в TXT, задавая числовую точность.
  Узнайте, как установить значимые цифры и ограничить их в C#.
draft: false
keywords:
- create new workbook
- export excel to txt
- set significant digits
- limit significant digits
- set numeric precision
language: ru
og_description: Создайте новую книгу и экспортируйте Excel в TXT, задавая значимые
  цифры для числовой точности. Пошаговое руководство на C#.
og_title: Создать новую рабочую книгу – экспортировать Excel в TXT с точностью
tags:
- C#
- Aspose.Cells
- Excel automation
title: Создать новую книгу и экспортировать Excel в TXT с точностью
url: /ru/net/excel-data-export-retrieval/create-new-workbook-and-export-excel-to-txt-with-precision/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание новой книги – Экспорт Excel в TXT с точным числовым форматированием

Ever wondered how to **create new workbook** objects in C# and instantly dump them to a plain‑text file? You're not the only one. In many data‑pipeline scenarios we need to **export Excel to TXT** while keeping numbers readable, which means limiting the number of digits that appear after the decimal point.  

In this tutorial we’ll walk through the whole process: from spinning up a fresh workbook, to configuring the export so it **sets significant digits** (aka limiting significant digits), and finally writing the file to disk. By the end you’ll have a ready‑to‑run snippet that respects your **numeric precision** requirements—no extra libraries, no magic.

> **Pro tip:** Если вы уже используете Aspose.Cells, классы, показанные ниже, являются частью этой библиотеки. Если вы работаете на другой платформе, концепции остаются применимыми; просто замените вызовы API.

---

## Что понадобится

- .NET 6+ (код компилируется как на .NET Core, так и на .NET Framework)  
- Aspose.Cells for .NET (бесплатная пробная версия или лицензия) – установить через NuGet: `dotnet add package Aspose.Cells`  
- Любая IDE по вашему выбору (Visual Studio, Rider, VS Code)  

Вот и всё. Нет дополнительных файлов конфигурации, нет скрытых шагов.

---

## Шаг 1: Создание новой книги

The very first thing is to **create new workbook**. Think of the `Workbook` class as an empty Excel file waiting for sheets, cells, and data.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Instantiate a fresh workbook – this is the core of create new workbook logic
        Workbook workbook = new Workbook();

        // (Optional) Add some sample data so you can see the effect of numeric precision later
        Worksheet sheet = workbook.Worksheets[0];
        sheet.Cells["A1"].PutValue(12345.678901);
        sheet.Cells["A2"].PutValue(0.000123456);
        sheet.Cells["A3"].PutValue(Math.PI);
```

> **Why this matters:** Начав с чистой книги, вы избегаете скрытого форматирования, которое могло бы помешать настройкам точности позже.

---

## Шаг 2: Настройка параметров сохранения текста — Установка значимых цифр

Now we tell Aspose.Cells how many **significant digits** we want when we write to a `.txt` file. The `TxtSaveOptions` class exposes a `SignificantDigits` property that does exactly that.

```csharp
        // Step 2: Prepare save options – limit numeric precision to 5 significant digits
        TxtSaveOptions txtOptions = new TxtSaveOptions
        {
            // This limits the output to 5 digits that matter, rounding the rest
            SignificantDigits = 5
        };
```

> **Explanation:** `SignificantDigits = 5` означает, что экспортёр сохранит пять самых значимых цифр любого числа, независимо от положения десятичной точки. Это удобный способ **set numeric precision** без ручного форматирования каждой ячейки.

---

## Шаг 3: Сохранение книги в виде обычного текстового файла

With the workbook and options ready, we finally **export Excel to txt**. The `Save` method takes the file path and the options object we just configured.

```csharp
        // Step 3: Write the workbook out as a TXT file using our precision settings
        string outputPath = @"C:\Temp\numbers.txt";
        workbook.Save(outputPath, txtOptions);

        System.Console.WriteLine($"Workbook exported to {outputPath} with 5 significant digits.");
    }
}
```

Running the program produces a file that looks like this:

```
12346
0.00012346
3.1416
```

Notice how each number respects the **limit significant digits** rule we set earlier.

---

## Шаг 4: Проверка результата (необязательно, но рекомендуется)

It’s easy to open the generated `numbers.txt` in any editor, but you might want to automate the verification step, especially in CI pipelines.

```csharp
        // Quick verification – read back the file and print each line
        foreach (var line in System.IO.File.ReadAllLines(outputPath))
        {
            System.Console.WriteLine($"Line: {line}");
        }
```

If the console shows the three lines above, you’ve successfully **set significant digits** and the export works as intended.

---

## Распространённые подводные камни и как их избежать

| Проблема | Почему происходит | Решение |
|----------|-------------------|---------|
| Числа отображаются с слишком большим количеством знаков после запятой | `SignificantDigits` оставлен по умолчанию (0) | Явно задайте `SignificantDigits` нужное количество |
| Создаётся пустой файл | Книга не получила данных перед сохранением | Заполните ячейки **before** вызова `Save` |
| Путь к файлу вызывает `UnauthorizedAccessException` | Попытка записать в защищённую папку | Используйте папку, в которую у вас есть права записи (например, `C:\Temp` или `%USERPROFILE%\Documents`) |
| Точность кажется неверной для очень маленьких чисел | Количество значимых цифр включает ведущие нули после запятой | Помните, что “significant” игнорирует ведущие нули; 0.000123456 с 5 цифрами становится `0.00012346` |

---

## Полный рабочий пример (готовый к копированию и вставке)

Below is the complete, self‑contained program. Paste it into a new console project and hit **Run**.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new workbook
        Workbook workbook = new Workbook();

        // Populate with sample numbers
        Worksheet sheet = workbook.Worksheets[0];
        sheet.Cells["A1"].PutValue(12345.678901);
        sheet.Cells["A2"].PutValue(0.000123456);
        sheet.Cells["A3"].PutValue(Math.PI);

        // 2️⃣ Set up export options – limit significant digits to 5
        TxtSaveOptions txtOptions = new TxtSaveOptions
        {
            SignificantDigits = 5
        };

        // 3️⃣ Export to TXT
        string outputPath = @"C:\Temp\numbers.txt";
        workbook.Save(outputPath, txtOptions);

        Console.WriteLine($"✅ Export completed: {outputPath}");
        Console.WriteLine("🔎 Verifying content:");
        foreach (var line in System.IO.File.ReadAllLines(outputPath))
        {
            Console.WriteLine($"   {line}");
        }
    }
}
```

**Ожидаемый вывод в консоль**

```
✅ Export completed: C:\Temp\numbers.txt
🔎 Verifying content:
   12346
   0.00012346
   3.1416
```

And the `numbers.txt` file will contain the three lines shown above.

---

## Следующие шаги: выход за пределы базового

- **Export other formats** – Aspose.Cells также поддерживает CSV, HTML и PDF. При необходимости замените `TxtSaveOptions` на `CsvSaveOptions` или `PdfSaveOptions`.  
- **Dynamic precision** – вы можете вычислять `SignificantDigits` во время выполнения на основе ввода пользователя или файлов конфигурации.  
- **Multiple worksheets** – пройдитесь по `workbook.Worksheets` и экспортируйте каждый лист в отдельный файл `.txt`.  
- **Localization** – контролируйте разделитель десятичных (`.` vs `,`) через `CultureInfo`, если нужно соответствовать региональным настройкам.  

All of these extensions still rely on the core idea we covered: **create new workbook**, configure the export, and **set numeric precision** to match your reporting requirements.

---

## Итоги

We’ve taken a fresh **create new workbook** instance, filled it with data, and demonstrated how to **export Excel to TXT** while **setting significant digits** to limit the output precision. The full example runs out‑of‑the‑box, and the explanation covered the *why* behind each line so you can adapt it to your own projects.

Feel free to experiment—change the `SignificantDigits` value, add more sheets, or switch the output format. If you hit a snag, check the Aspose.Cells documentation or drop a comment below. Happy coding!

---

![Пример создания новой книги](/images/create-new-workbook.png "Скриншот, показывающий IDE C# с кодом создания новой книги")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}