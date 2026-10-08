---
category: general
date: 2026-04-07
description: Записать дату и время в Excel с помощью C#. Узнайте, как вставить дату
  в лист, работать со значением даты в ячейке Excel и преобразовать дату японского
  календаря за несколько шагов.
draft: false
keywords:
- write datetime to excel
- excel cell date value
- insert date into worksheet
- convert japanese calendar date
language: ru
og_description: Быстро записывайте дату и время в Excel. В этом руководстве показано,
  как вставить дату в лист, управлять значением даты в ячейке Excel и конвертировать
  дату японского календаря с помощью C#.
og_title: Запись даты и времени в Excel – пошаговое руководство на C#
tags:
- C#
- Excel automation
- Aspose.Cells
title: Запись даты и времени в Excel — Полное руководство для разработчиков C#
url: /ru/net/excel-custom-number-date-formatting/write-datetime-to-excel-complete-guide-for-c-developers/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Запись даты и времени в Excel – Полное руководство для разработчиков C#

Когда‑то вам нужно **записать дату и время в Excel**, но вы не уверены, какой вызов API действительно сохраняет корректную дату Excel? Вы не одиноки. Во многих корпоративных инструментах приходится помещать объект C# `DateTime` в таблицу, и результат должен вести себя как настоящая дата Excel — сортироваться, фильтроваться и использоваться в сводных таблицах.  

В этом руководстве мы пройдём по точным шагам *вставки даты в лист* с помощью Aspose.Cells, объясним, почему важно задать культуру, и даже покажем, как **преобразовать дату японского календаря** в обычный `DateTime` перед записью. К концу вы получите автономный фрагмент кода, который можно скопировать и вставить в любой .NET‑проект.

## Что вам понадобится

- **.NET 6+** (или любая современная версия .NET; код также работает в .NET Framework)  
- **Aspose.Cells for .NET** — пакет NuGet, позволяющий манипулировать файлами Excel без установленного Office.  
- Базовые знания о `DateTime` в C# и культурах.  

Никаких дополнительных библиотек, COM‑interop и установки Excel не требуется. Если у вас уже есть экземпляр листа (`ws`), вы готовы к работе.

## Шаг 1: Настройка японской культуры (Преобразование даты японского календаря)

Когда вы получаете строку вида `"R02/05/01"` (Reiwa 2, 1 мая), нужно сообщить .NET, как интерпретировать символы эпохи. Японский календарь не является календарём по умолчанию, поэтому мы создаём `CultureInfo`, заменяющий его календарь на `JapaneseCalendar`.

```csharp
using System;
using System.Globalization;
using Aspose.Cells;   // Make sure Aspose.Cells is referenced

// Assume you already have a worksheet instance named "ws"
Worksheet ws = /* your worksheet instance */;

// 1️⃣ Configure a Japanese culture that uses the Japanese calendar
CultureInfo japaneseCulture = new CultureInfo("ja-JP");
japaneseCulture.DateTimeFormat.Calendar = new JapaneseCalendar();
```

**Почему это важно:**  
Если попытаться разобрать строку с культурой по умолчанию, .NET бросит `FormatException`, потому что не сможет сопоставить `R` (эра Reiwa) с годом. Подменив календарь на `JapaneseCalendar`, парсер понимает символы эпохи и переводит их в правильный григорианский год.

## Шаг 2: Разбор строки с эпохой в `DateTime`

Теперь, когда культура готова, можно безопасно вызвать `DateTime.ParseExact`. Формат `"ggyy/MM/dd"` сообщает парсеру:

- `gg` — обозначение эпохи (например, `R` для Reiwa)  
- `yy` — двухзначный год внутри эпохи  
- `MM/dd` — месяц и день.

```csharp
// 2️⃣ Parse a date string in the Japanese era format (ggyy/MM/dd)
string japaneseDate = "R02/05/01";          // Reiwa 2, May 1st
DateTime parsedDate = DateTime.ParseExact(
    japaneseDate,
    "ggyy/MM/dd",
    japaneseCulture,
    DateTimeStyles.None
);
```

**Совет:** Если вы можете получать даты в других форматах (например, `"Heisei 30/12/31"`), оберните разбор в `try/catch` и используйте `DateTime.TryParseExact` в качестве fallback. Это предотвратит падение всей задачи импорта из‑за одной плохой строки.

## Шаг 3: Запись `DateTime` в ячейку Excel (Дата ячейки Excel)

Aspose.Cells рассматривает .NET `DateTime` как нативную дату Excel, когда вы вызываете `PutValue`. Библиотека автоматически преобразует тики в серийный номер Excel (количество дней с 1900‑01‑00). Это значит, что ячейка будет содержать корректное **значение даты ячейки Excel**, которое позже можно отформатировать встроенными стилями даты Excel.

```csharp
// 3️⃣ Write the resulting DateTime value into cell C1 of the worksheet
Cell targetCell = ws.Cells["C1"];
targetCell.PutValue(parsedDate);

// Optional: apply a standard date format so users see "yyyy-MM-dd"
targetCell.Style.Number = 14;   // built‑in Excel format ID for "m/d/yy"
```

**Что вы увидите в Excel:**  
Ячейка C1 теперь содержит серийный номер `44796`, который Excel отображает как `2020‑05‑01` (или в выбранном вами формате). Подлежащим значением является настоящая дата, а не строка, поэтому сортировка работает как ожидается.

## Шаг 4: Сохранение книги (Завершение)

Если вы ещё не сохранили книгу, сделайте это сейчас. Этот шаг не относится напрямую к записи даты, но завершает весь процесс.

```csharp
// Save the workbook to a file (or a MemoryStream if you need it in‑memory)
Workbook workbook = ws.Workbook;   // get the parent workbook
workbook.Save("Output.xlsx", SaveFormat.Xlsx);
```

И всё — четыре лаконичных шага, и вы успешно **записали дату и время в Excel**, одновременно обработав дату японской эпохи.

---

![пример записи даты и времени в excel](/images/write-datetime-to-excel.png "Скриншот, показывающий C#‑проект, записывающий DateTime в ячейку Excel C1")

*На изображении показан итоговый файл Excel с корректно отображённой датой в ячейке C1.*

## Часто задаваемые вопросы и особые случаи

### Что делать, если переменная листа ещё не готова?

Можно создать новую книгу «на лету»:

```csharp
Workbook workbook = new Workbook();
Worksheet ws = workbook.Worksheets[0];   // default first sheet
```

### Как сохранить оригинальную строку японской эпохи в листе?

Если нужны и оригинальная строка, и разобранная дата, запишите их в соседние ячейки:

```csharp
ws.Cells["B1"].PutValue(japaneseDate);   // original text
ws.Cells["C1"].PutValue(parsedDate);     // parsed DateTime
```

### Работает ли это со старыми версиями .NET?

Да. `JapaneseCalendar` существует, начиная с .NET 2.0, а Aspose.Cells поддерживает .NET Framework 4.5+. Просто убедитесь, что подключили правильную сборку.

### А как насчёт часовых поясов?

`DateTime.ParseExact` возвращает **Kind** = `Unspecified`. Если ваши исходные даты в UTC, сначала преобразуйте их:

```csharp
DateTime utcDate = DateTime.SpecifyKind(parsedDate, DateTimeKind.Utc);
DateTime localDate = utcDate.ToLocalTime();
targetCell.PutValue(localDate);
```

### Можно ли задать пользовательский формат даты (например, “yyyy年MM月dd日”)?

Конечно. Используйте свойство `Style.Custom`:

```csharp
targetCell.Style.Custom = "yyyy\"年\"mm\"月\"dd\"日\"";
```

Теперь Excel будет показывать `2020年05月01日`, при этом сохраняется истинное значение даты.

## Итоги

Мы рассмотрели всё, что нужно, чтобы **записать дату и время в Excel** из C#:

1. **Настроить** японскую культуру с `JapaneseCalendar` для **преобразования даты японского календаря**.  
2. **Разобрать** строку с эпохой с помощью `DateTime.ParseExact`.  
3. **Вставить** полученный `DateTime` в ячейку, обеспечив корректное **значение даты ячейки Excel**.  
4. **Сохранить** книгу, чтобы данные сохранились.

Эти четыре шага позволяют безопасно **вставлять дату в лист** независимо от исходного формата. Код полностью готов к запуску, требует только Aspose.Cells и работает на любой современной платформе .NET.

## Что дальше?

- **Массовый импорт:** перебрать строки CSV, разобрать каждую японскую дату и записать их в последовательные ячейки.  
- **Стилизация:** применить условное форматирование для выделения просроченных дат.  
- **Производительность:** использовать `WorkbookDesigner` или кэширование `CellStyle` при работе с тысячами строк.  

Экспериментируйте — заменяйте японскую эпоху на григорианскую, меняйте целевую ячейку или выводите в другой формат (CSV, ODS). Суть остаётся той же: разбор, преобразование и **запись даты и времени в Excel** с уверенностью.

Счастливого кодинга, и пусть ваши таблицы всегда сортируются правильно!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}