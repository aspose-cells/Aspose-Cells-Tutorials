---
category: general
date: 2026-03-30
description: Узнайте, как форматировать дату в ISO, читая значения даты и времени
  из Excel, и извлекать данные даты и времени из Excel с помощью Aspose.Cells на C#.
draft: false
keywords:
- format date iso
- read excel datetime
- extract datetime excel
- Aspose.Cells date parsing
- Japanese era dates
language: ru
og_description: Форматировать дату в ISO из данных Excel с помощью Aspose.Cells. Это
  руководство показывает, как читать дату и время из Excel, извлекать значения даты
  и времени и выводить даты в формате ISO.
og_title: Формат даты ISO из Excel – пошаговое руководство C#
tags:
- C#
- Excel
- DateTime
- Aspose.Cells
title: Формат даты ISO из Excel – Полное руководство по C#
url: /ru/net/excel-custom-number-date-formatting/format-date-iso-from-excel-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Форматирование даты ISO из Excel – Полное руководство C# 

Когда‑нибудь вам нужно было **format date iso** при извлечении дат из листа Excel? Возможно, вы работаете с датами японских эпох, или просто хотите чистую строку `yyyy‑MM‑dd` для полезной нагрузки API. В этом руководстве вы увидите, как **read Excel datetime** ячейки, **extract datetime Excel** значения и преобразовать их в формат ISO‑8601 — без догадок.

Мы пройдем реальный пример, использующий Aspose.Cells, объясним, почему каждая строка важна, и покажем окончательный вывод, который вы можете скопировать и вставить в свой проект. К концу вы сможете обрабатывать странные строки эпох, такие как «令和3年5月1日», и получать стандартную дату ISO, готовую для баз данных, JSON или любого другого места, где она нужна.

## Требования

- .NET 6.0 или новее (код также работает с .NET Framework)
- Aspose.Cells for .NET (бесплатная пробная версия или лицензированная)
- Базовое знакомство с C# и концепциями Excel
- Visual Studio или любой другой редактор C#, который вам нравится

Дополнительные пакеты NuGet не требуются, кроме Aspose.Cells, поэтому настройка довольно проста.

---

## Шаг 1: Создать Workbook и выбрать первый лист

Первое, что вы делаете, — создаёте новый объект `Workbook`. Это даёт вам представление Excel‑файла в памяти, с которым вы затем можете работать или читать данные.

```csharp
using Aspose.Cells;
using System.Globalization;

// Step 1: Initialize a new workbook and grab the first worksheet
Workbook workbook = new Workbook();                 // creates an empty .xlsx
Worksheet worksheet = workbook.Worksheets[0];      // the default sheet is "Sheet1"
```

*Почему это важно:*  
Создание workbook программно позволяет избежать работы с физическими файлами во время тестирования. Это также гарантирует, что ссылка на лист всегда действительна — без неожиданностей с null‑reference позже, когда вы попытаетесь **read Excel datetime** значения.

---

## Шаг 2: Записать строку даты японской эпохи в ячейку

Наша цель — продемонстрировать разбор негригорианской даты. Мы поместим строку эпохи непосредственно в ячейку **A1**.

```csharp
// Step 2: Insert a Japanese era date string into cell A1
worksheet.Cells["A1"].PutValue("令和3年5月1日");
```

*Совет:*  
Если вы извлекаете данные из существующего workbook, вы пропустите вызов `PutValue` и просто обратитесь к ячейке, уже содержащей дату. Главное, чтобы ячейка содержала **string**, представляющую дату в японском лунно‑солярном календаре.

---

## Шаг 3: Настроить культуру, понимающую японский лунно‑солярный календарь

Класс .NET `CultureInfo` позволяет задать, как должны интерпретироваться даты. Заменив календарь по умолчанию Gregorian на `JapaneseLunisolarCalendar`, вы предоставляете парсеру необходимый контекст.

```csharp
// Step 3: Set up a culture using the Japanese lunisolar calendar
CultureInfo japaneseCulture = new CultureInfo("ja-JP");
japaneseCulture.DateTimeFormat.Calendar = new JapaneseLunisolarCalendar();
```

*Почему мы это делаем:*  
Если попытаться разобрать «令和3年5月1日» с культурой по умолчанию, .NET выдаст `FormatException`. Замена на лунно‑солярный календарь сообщает среде выполнения, как точно сопоставить «令和3年» (3‑й год эпохи Reiwa) с григорианским годом 2021.

---

## Шаг 4: Разобрать значение ячейки как `DateTime`, используя настроенную культуру

Теперь наступает основная часть операции — преобразование строки эпохи в корректный объект `DateTime`. Aspose.Cells предоставляет удобный перегруз `GetDateTime`, принимающий `CultureInfo`.

```csharp
// Step 4: Retrieve the cell value as a DateTime, respecting the Japanese culture
DateTime parsedDate = worksheet.Cells["A1"].GetDateTime(japaneseCulture);
```

*Что происходит под капотом:*  
`GetDateTime` читает исходную строку, применяет правила календаря указанной культуры и возвращает `DateTime`, представляющий тот же момент в григорианском календаре. Это тот момент, когда вы **extract datetime Excel** данные в форме, с которой можно работать в .NET.

---

## Шаг 5: Вывести разобранную дату в формате ISO 8601

Наконец, мы форматируем `DateTime` как строку ISO — `yyyy‑MM‑dd` — которая универсально принимается API, базами данных и фронтенд‑фреймворками.

```csharp
// Step 5: Print the date in ISO format (e.g., 2021-05-01)
Console.WriteLine(parsedDate.ToString("yyyy-MM-dd")); // Output: 2021-05-01
```

*Почему ISO?*  
ISO 8601 устраняет неоднозначность. «05/01/2021» может означать 1 мая или 5 января в зависимости от локали. `2021-05-01` абсолютно ясно, поэтому мы **format date iso** почти во всех сценариях интеграции.

---

## Полный рабочий пример

Ниже представлен полный готовый к запуску пример программы. Скопируйте его в проект консольного приложения, добавьте ссылку на Aspose.Cells и нажмите **F5**.

```csharp
using Aspose.Cells;
using System;
using System.Globalization;

class Program
{
    static void Main()
    {
        // 1️⃣ Create workbook and select the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ Write a Japanese era date string into cell A1
        worksheet.Cells["A1"].PutValue("令和3年5月1日");

        // 3️⃣ Set up Japanese lunisolar culture
        CultureInfo japaneseCulture = new CultureInfo("ja-JP");
        japaneseCulture.DateTimeFormat.Calendar = new JapaneseLunisolarCalendar();

        // 4️⃣ Parse the cell value as DateTime using the culture
        DateTime parsedDate = worksheet.Cells["A1"].GetDateTime(japaneseCulture);

        // 5️⃣ Output the date in ISO format
        Console.WriteLine(parsedDate.ToString("yyyy-MM-dd")); // 2021-05-01
    }
}
```

**Ожидаемый вывод**

```
2021-05-01
```

Запустите его один раз, и вы увидите дату в формате ISO, выведенную в консоль. Это весь конвейер от **read Excel datetime** до **format date iso**.

---

## Обработка распространённых граничных случаев

### 1. Ячейки, содержащие реальные числовые даты Excel

Иногда Excel хранит даты как последовательные числа (например, `44204`). В этом случае культура не нужна; просто вызовите `GetDateTime()` без параметров:

```csharp
DateTime serialDate = worksheet.Cells["B2"].GetDateTime(); // B2 holds a numeric date
Console.WriteLine(serialDate.ToString("yyyy-MM-dd"));
```

### 2. Пустые или неверные ячейки

Если ячейка пуста или содержит непарсимую строку, `GetDateTime` выбросит исключение. Оберните вызов в `try/catch` или сначала проверьте `IsDateTime`:

```csharp
if (worksheet.Cells["C3"].Type == CellValueType.IsDateTime)
{
    DateTime safeDate = worksheet.Cells["C3"].GetDateTime();
    Console.WriteLine(safeDate.ToString("yyyy-MM-dd"));
}
else
{
    Console.WriteLine("Cell C3 does not contain a valid date.");
}
```

### 3. Разные форматы эпох

Другие японские эпохи (Heisei, Showa) следуют тому же шаблону. Тот же `JapaneseLunisolarCalendar` обработает их автоматически, так что дополнительная логика не нужна — просто передайте строку.

---

## Полезные советы и подводные камни

- **Performance:** При обработке больших таблиц переиспользуйте один экземпляр `CultureInfo` вместо создания нового в каждом цикле.  
- **Thread Safety:** Объекты `CultureInfo` становятся только для чтения после установки календаря, поэтому их безопасно использовать в разных потоках.  
- **Aspose.Cells Licensing:** Если вы используете бесплатную пробную версию, помните, что некоторые функции могут быть ограничены после окончания пробного периода. Парсинг дат, показанный здесь, работает как в пробной, так и в лицензированной версии.  
- **Time Zones:** Получаемый `DateTime` имеет **unspecified** (без часового пояса). Если нужен UTC, вызовите `DateTime.SpecifyKind(parsedDate, DateTimeKind.Utc)` или выполните преобразование с помощью `TimeZoneInfo`.

---

## Заключение

Мы рассмотрели всё, что нужно для **format date iso** из Excel‑книги с помощью C#. Начиная с сырой строки японской эпохи, мы **read Excel datetime**, настроили правильную культуру, **extract datetime excel** данные и в конце вывели чистую строку ISO‑8601. Этот подход работает с любой датой, которую может выдать Excel, будь то числовой сериал, строка, зависящая от локали, или традиционный формат эпохи.

Что дальше? Попробуйте пройтись по целому столбцу дат, записать результаты ISO обратно в новый лист или сразу передать их в JSON‑полезную нагрузку веб‑сервиса. Если вам интересны другие календарные системы (еврейский, исламский), Aspose.Cells и `CultureInfo` в .NET делают такие эксперименты столь же простыми.

Есть вопросы или сложный формат даты, который не поддаётся? Оставьте комментарий ниже, и удачной разработки!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}