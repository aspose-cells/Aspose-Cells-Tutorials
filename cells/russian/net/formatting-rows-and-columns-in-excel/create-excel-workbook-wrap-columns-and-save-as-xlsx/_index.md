---
category: general
date: 2026-04-07
description: Создать книгу Excel, обернуть столбцы в Excel, вычислить формулы и сохранить
  книгу в формате XLSX с пошаговым кодом на C#.
draft: false
keywords:
- create excel workbook
- wrap columns in excel
- save workbook as xlsx
- how to calculate formulas
- how to save excel
language: ru
og_description: Создайте рабочую книгу Excel, выполните перенос текста в столбцах,
  вычислите формулы и сохраните книгу в формате XLSX. Ознакомьтесь с полным процессом
  с работающим кодом.
og_title: Создать книгу Excel — Полное руководство по C#
tags:
- csharp
- aspnet
- excel
- automation
title: Создать книгу Excel – перенести текст в столбцах и сохранить как XLSX
url: /ru/net/formatting-rows-and-columns-in-excel/create-excel-workbook-wrap-columns-and-save-as-xlsx/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание книги Excel – Обернуть столбцы и сохранить как XLSX

Когда‑нибудь вам нужно было **create Excel workbook** программно и вы задавались вопросом, как разместить данные в красивом многостолбцовом макете? Вы не одиноки. В этом руководстве мы пройдем процесс создания книги, применения формулы `WRAPCOLS` для **wrap columns in Excel**, принудим движок вычислить результат и, наконец, **save workbook as XLSX**, чтобы открыть её в любой программе для работы с таблицами.

Мы также ответим на неизбежные последующие вопросы: *How do I calculate formulas on the fly?* *What if I need to change the number of columns?* и *Is there a quick way to persist the file?* К концу вы получите автономный, готовый к запуску фрагмент C#, который делает всё это, а также несколько дополнительных советов, которые вы можете скопировать в свои проекты.

## Требования

- .NET 6.0 или новее (код также работает на .NET Framework 4.6+)
- Библиотека **Aspose.Cells** (или любой другой пакет для обработки Excel, поддерживающий `WRAPCOLS`; в примере используется Aspose.Cells, потому что он предоставляет простой метод `CalculateFormula`)
- Небольшой опыт работы с C# — если вы умеете писать `Console.WriteLine`, вы готовы приступить

> **Pro tip:** Если у вас ещё нет лицензии на Aspose.Cells, вы можете запросить бесплатный пробный ключ на их сайте; пробная версия прекрасно подходит для обучения.

## Шаг 1: Создание книги Excel

Первое, что вам нужно, — это пустой объект workbook, представляющий файл Excel в памяти. Это ядро операции **create Excel workbook**.

```csharp
using Aspose.Cells;

// Step 1: Instantiate a new workbook
Workbook workbook = new Workbook();

// Grab the first worksheet – it’s already there by default
Worksheet worksheet = workbook.Worksheets[0];
```

*Почему это важно:* Класс `Workbook` является точкой входа для любой работы с Excel. Создав его первым, вы получаете чистый холст, на котором последующие действия — такие как оборачивание столбцов — могут быть применены без побочных эффектов.

## Шаг 2: Заполнение образцовыми данными (необязательно, но полезно)

Прежде чем оборачивать столбцы, загрузим небольшой набор данных в диапазон `A1:D10`. Это отражает реальный сценарий, когда у вас есть сырая таблица, требующая преобразования.

```csharp
// Fill A1:D10 with sample numbers for demonstration
for (int row = 0; row < 10; row++)
{
    for (int col = 0; col < 4; col++)
    {
        worksheet.Cells[row, col].PutValue(row * 4 + col + 1);
    }
}
```

Вы можете пропустить этот блок, если у вас уже есть данные в листе; логика оборачивания работает с любым существующим диапазоном.

## Шаг 3: Оборачивание столбцов в Excel

Теперь на сцену выходит звезда шоу: функция `WRAPCOLS`. Она принимает исходный диапазон и количество столбцов, затем распределяет данные по новому макету. Вот как применить её к ячейке **A1**, чтобы результат занял три столбца.

```csharp
// Apply WRAPCOLS to A1 – the result will spill into a 3‑column layout
worksheet.Cells["A1"].Formula = "=WRAPCOLS(A1:D10,3)";
```

**Что происходит под капотом?**  
`WRAPCOLS(A1:D10,3)` сообщает Excel прочитать 40 ячеек в `A1:D10` и затем записать их построчно в три столбца, автоматически создавая столько строк, сколько потребуется. Это идеально подходит для преобразования длинного списка в более компактный, газетный вид.

## Шаг 4: Как вычислять формулы

Установка формулы — это лишь половина дела; Excel не вычислит результат, пока вы не запустите проход расчёта. В Aspose.Cells это делается с помощью `CalculateFormula()`.

```csharp
// Force the workbook to evaluate all pending formulas
workbook.CalculateFormula();
```

> **Почему это нужно:** Без вызова `CalculateFormula` ячейка `A1` будет содержать лишь строку формулы при открытии файла, и обёрнутый макет не появится, пока пользователь не выполнит пересчёт вручную.

## Шаг 5: Сохранить книгу как XLSX

Наконец, сохраняем книгу на диск. Метод `Save` автоматически определяет формат по расширению файла, поэтому использование **.xlsx** гарантирует получение современного формата Open XML.

```csharp
// Choose a folder you have write access to and save the file
string outputPath = @"C:\Temp\output.xlsx";
workbook.Save(outputPath);
```

Когда вы откроете `output.xlsx` в Excel, вы увидите оригинальные данные аккуратно обёрнутыми в три столбца, начиная с ячейки **A1**. Остальная часть листа останется нетронутой, что удобно, если нужно сохранить исходную таблицу для справки.

### Ожидаемый результат (скриншот)

<img src="images/wrapcols-result.png" alt="create excel workbook example" />

Изображение выше иллюстрирует окончательный макет: числа из `A1:D10` теперь отображаются в трёх столбцах, при этом строки генерируются автоматически, чтобы вместить все значения.

## Общие варианты и граничные случаи

### Изменение количества столбцов

Если вам нужно другое количество столбцов, просто измените второй аргумент функции `WRAPCOLS`:

```csharp
worksheet.Cells["A1"].Formula = "=WRAPCOLS(A1:D10,5)"; // five‑column layout
```

Не забудьте повторно вызвать `CalculateFormula()` после любого изменения.

### Оборачивание несмежных диапазонов

`WRAPCOLS` работает только с непрерывными диапазонами. Если исходные данные разбросаны по нескольким областям, сначала объедините их (например, используя `UNION` в вспомогательном столбце) перед оборачиванием.

### Большие наборы данных

Для очень больших таблиц расчёт может занять несколько секунд. Вы можете повысить производительность, отключив автоматический расчёт перед установкой формулы и включив его снова после.

```csharp
workbook.Settings.CalcMode = CalcMode.Manual;
worksheet.Cells["A1"].Formula = "=WRAPCOLS(A1:D1000,4)";
workbook.CalculateFormula();
workbook.Settings.CalcMode = CalcMode.Automatic;
```

### Сохранение в поток

Если вы создаёте веб‑API и хотите вернуть файл напрямую клиенту, вы можете записать его в `MemoryStream` вместо физического файла:

```csharp
using var ms = new MemoryStream();
workbook.Save(ms, SaveFormat.Xlsx);
ms.Position = 0; // reset for reading
// return ms as a FileResult in ASP.NET Core, for example
```

## Полный рабочий пример

Объединив всё вместе, представляем полностью готовую к копированию программу:

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ Fill A1:D10 with sample data (optional)
        for (int row = 0; row < 10; row++)
        {
            for (int col = 0; col < 4; col++)
            {
                worksheet.Cells[row, col].PutValue(row * 4 + col + 1);
            }
        }

        // 3️⃣ Apply WRAPCOLS to produce a 3‑column layout
        worksheet.Cells["A1"].Formula = "=WRAPCOLS(A1:D10,3)";

        // 4️⃣ Force calculation so the formula result is materialized
        workbook.CalculateFormula();

        // 5️⃣ Save the workbook as XLSX
        string outputPath = @"C:\Temp\output.xlsx";
        workbook.Save(outputPath);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

Запустите эту программу, откройте сгенерированный `output.xlsx`, и вы увидите данные, обёрнутые точно так, как описано.

## Заключение

Теперь вы знаете, как **create Excel workbook** объекты в C#, применять мощную функцию `WRAPCOLS` для **wrap columns in Excel**, **calculate formulas** по требованию и **save workbook as XLSX** для дальнейшего использования. Этот сквозной процесс охватывает самые распространённые сценарии, от простых демонстраций до автоматизации уровня продакшн.

### Что дальше?

- Поэкспериментировать с другими функциями динамических массивов, такими как `FILTER`, `SORT` или `UNIQUE`.
- Скомбинировать `WRAPCOLS` с условным форматированием для выделения определённых строк.
- Интегрировать эту логику в endpoint ASP.NET Core, чтобы пользователи могли скачать настроенный отчёт одним кликом.

Не стесняйтесь менять количество столбцов, исходный диапазон или путь вывода, чтобы они соответствовали требованиям вашего проекта. Если возникнут проблемы, оставьте комментарий ниже — удачной разработки!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}