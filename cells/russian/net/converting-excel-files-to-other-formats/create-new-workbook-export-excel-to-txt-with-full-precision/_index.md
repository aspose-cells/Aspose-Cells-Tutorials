---
category: general
date: 2026-03-18
description: Создайте новую книгу и экспортируйте Excel в TXT, сохраняя числовую точность.
  Узнайте, как сохранить лист как TXT и эффективно преобразовать лист в TXT.
draft: false
keywords:
- create new workbook
- export excel to txt
- save excel as txt
- save worksheet as txt
- convert worksheet to txt
language: ru
og_description: Создайте новую книгу и экспортируйте Excel в TXT с точностью. Этот
  учебник показывает, как сохранить лист как txt и преобразовать лист в txt с помощью
  C#.
og_title: Создать новую рабочую книгу – Руководство по экспорту Excel в TXT
tags:
- Aspose.Cells
- C#
- Excel automation
title: Создать новую книгу – экспортировать Excel в TXT с полной точностью
url: /ru/net/converting-excel-files-to-other-formats/create-new-workbook-export-excel-to-txt-with-full-precision/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создать новую книгу – Экспорт Excel в TXT с полной точностью

Когда‑нибудь нужно было **create new workbook** в C# просто чтобы выгрузить данные в обычный текстовый файл? Возможно, вы извлекаете отчёт из устаревшей системы, а последующий инструмент принимает только поток `.txt`. Хорошая новость? Вам не придётся жертвовать числовой точностью, и вам определённо не нужно вручную формировать CSV‑строки.

В этом руководстве мы пройдём весь процесс **export excel to txt**, от инициализации книги до сохранения нулей после запятой при **save worksheet as txt**. К концу вы получите готовый фрагмент кода, который можно вставить в любой .NET‑проект — без дополнительных утилит.

## Что понадобится

- **ASP.NET/ .NET 6+** (код также работает на .NET Framework 4.6+)  
- **Aspose.Cells for .NET** — библиотека, предоставляющая классы `Workbook`, `Worksheet` и `TxtSaveOptions`. Установить её можно через NuGet: `Install-Package Aspose.Cells`.  
- Базовое понимание C# (если вы уверенно используете `using`, то всё в порядке).  

И всё — без Excel‑interop, без COM‑объектов и без ручного склеивания строк.  

---

## Шаг 1: Инициализировать новую книгу (Primary Keyword)

Первое, что нужно сделать, — **create new workbook**. Представьте книгу как чистый холст, куда позже будут вставлены числа, текст или формулы.

```csharp
using System;
using Aspose.Cells;

namespace ExcelToTxtDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Create a new workbook and get the first worksheet
            Workbook workbook = new Workbook();                 // <‑‑ creates new workbook
            Worksheet worksheet = workbook.Worksheets[0];       // first sheet (index 0)
```

> **Почему это важно:** Создание экземпляра `Workbook` без загрузки файла даёт вам чистый лист. Затем вы можете программно добавлять данные, что идеально подходит для сценариев **convert worksheet to txt**, когда у вас нет готового `.xlsx`.

---

## Шаг 2: Заполнить ячейки — сохранить конечные нули

Распространённая ошибка при выгрузке чисел в текст — потеря конечных нулей (`123.45000` превращается в `123.45`). Если downstream‑системы полагаются на поля фиксированной ширины, такая потеря может всё сломать.

```csharp
            // Step 2: Write a numeric value that contains trailing zeros
            // PutValue respects the data type; we’ll later tell the saver to keep precision.
            worksheet.Cells[0, 0].PutValue(123.45000);
```

> **Совет:** `PutValue` автоматически определяет тип данных. Если нужен строковый вид числа, используйте `PutValue("123.45000")`.

---

## Шаг 3: Настроить параметры сохранения TXT — сохранить числовую точность

Здесь происходит волшебство. Установив `PreserveNumericPrecision`, вы заставляете Aspose.Cells записать точное значение, включая незначимые конечные нули.

```csharp
            // Step 3: Configure TXT save options to keep the original numeric precision
            TxtSaveOptions txtSaveOptions = new TxtSaveOptions(SaveFormat.Txt)
            {
                PreserveNumericPrecision = true   // retain all digits, even trailing zeros
            };
```

> **Зачем включать:** При **save excel as txt** поведение по умолчанию обрезает лишние десятичные знаки. Установка `PreserveNumericPrecision = true` гарантирует, что вывод будет точно соответствовать отображаемому значению ячейки, что критично для финансовых отчётов или научных данных.

---

## Шаг 4: Сохранить лист как TXT — финальный экспорт

Теперь действительно **save worksheet as txt**. Вы можете указать любой путь, где есть права записи; в примере используется относительная папка `output`.

```csharp
            // Step 4: Save the worksheet as a TXT file using the configured options
            string outputPath = "output/num-preserve.txt";
            worksheet.Save(outputPath, txtSaveOptions);

            Console.WriteLine($"File saved to {outputPath}");
        }
    }
}
```

> **Ожидаемый вывод** (`num-preserve.txt`):

```
123.45000
```

Обратите внимание, что конечные нули сохранены — именно то, что требовалось.

---

## Шаг 5: Проверить результат — быстрая проверка

После выполнения программы откройте `num-preserve.txt` в любом текстовом редакторе. Вы должны увидеть одну строку `123.45000`. Если вместо этого видите `123.45`, проверьте, что `PreserveNumericPrecision` установлен в `true` и что вы используете актуальную версию Aspose.Cells (v23.10+).

---

## Распространённые варианты и крайние случаи

### Экспорт нескольких ячеек или диапазонов

Если нужно **export excel to txt** для целого диапазона, просто заполните больше ячеек перед сохранением:

```csharp
worksheet.Cells["A1"].PutValue(100);
worksheet.Cells["A2"].PutValue(200.500);
worksheet.Cells["A3"].PutValue(300.00);
```

Aspose по умолчанию записывает каждую ячейку в новой строке. Вы также можете изменить разделитель (табуляцию, запятую) через `txtSaveOptions.Separator`.

### Конвертация листа в TXT с разными кодировками

Иногда downstream‑системы требуют UTF‑8 BOM или ASCII. Настройте кодировку так:

```csharp
txtSaveOptions.Encoding = System.Text.Encoding.UTF8;
```

### Работа с большими книгами

При работе с массивными листами (сотни тысяч строк) рассмотрите потоковую запись вывода:

```csharp
txtSaveOptions.EnableCache = true; // writes data in chunks to reduce memory footprint
```

---

## Полезные советы и подводные камни

- **Не забудьте создать каталог вывода** перед вызовом `Save`, иначе получите `DirectoryNotFoundException`.  
- **Следите за локальными разделителями десятичных**. Если в вашей среде используется запятая (`1,23`), задайте `txtSaveOptions.DecimalSeparator = '.'`, чтобы принудительно использовать точку.  
- **Совместимость версий**: флаг `PreserveNumericPrecision` появился в Aspose.Cells 20.6. В более старых версиях флага нет, и придётся предварительно форматировать ячейку как текст перед сохранением.

---

![Пример создания новой книги](excel-to-txt.png "Создать новую книгу")

*Текст альтернативы изображения: "Создать новую книгу и экспортировать Excel в TXT с сохранённой числовой точностью"*

---

## Итоги — что мы рассмотрели

- **Create new workbook** с помощью Aspose.Cells.  
- Заполнить ячейку числом с конечными нулями.  
- Установить `TxtSaveOptions.PreserveNumericPrecision = true`, чтобы **save excel as txt** без потери точности.  
- Записать файл на диск и убедиться, что вывод совпадает с исходным значением.  

Это полный рабочий процесс **convert worksheet to txt** в менее чем 50 строк C#.

---

## Следующие шаги и смежные темы

Теперь, когда вы умеете **export excel to txt** с идеальной точностью, можно изучить:

- **Экспорт в CSV** с пользовательскими разделителями (`TxtSaveOptions.Separator`).  
- **Сохранение в другие текстовые форматы** вроде TSV (`SaveFormat.TabDelimited`).  
- **Пакетная обработка** нескольких книг в папке через `Directory.GetFiles`.  
- **Интеграция с Azure Functions** для конвертации по запросу в облаке.

Все эти задачи используют тот же паттерн `Workbook` → `Worksheet` → `TxtSaveOptions`, так что вы будете чувствовать себя как дома.

---

### Заключительная мысль

Если вы прошли весь путь, теперь точно знаете, как **create new workbook**, заполнить её и **save worksheet as txt**, сохранив каждый нужный десятичный разряд. Это небольшая часть кода, но она решает довольно распространённую проблему, когда устаревшие конвейеры требуют текстовых входов.

Попробуйте, поиграйте с параметрами, и пусть данные текут именно так, как вам нужно. Приятного кодинга!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}