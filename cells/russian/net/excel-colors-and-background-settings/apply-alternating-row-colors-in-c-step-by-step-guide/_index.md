---
category: general
date: 2026-03-18
description: Узнайте, как применять чередующиеся цвета строк в листе с помощью C#.
  Включает установку фонового цвета строки, добавление светло‑желтого фона и чередование
  цветов строк.
draft: false
keywords:
- apply alternating row colors
- set row background color
- add light yellow background
- set alternating row shading
- color rows alternately
language: ru
og_description: Применяйте чередующиеся цвета строк в C# для улучшения читаемости.
  Это руководство показывает, как установить цвет фона строки, добавить светло‑желтый
  фон и чередовать цвета строк.
og_title: Применение чередующихся цветов строк в C# – Полное руководство
tags:
- C#
- DataTable
- Spreadsheet styling
- UI design
title: Применение чередующихся цветов строк в C# — пошаговое руководство
url: /ru/net/excel-colors-and-background-settings/apply-alternating-row-colors-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Применение чередующихся цветов строк в C# – Полный учебник

Когда‑нибудь вам нужно было **применить чередующиеся цвета строк** к листу, основанному на данных, но вы не знали, с чего начать? Вы не одиноки — большинство разработчиков сталкиваются с этой проблемой, когда впервые пытаются сделать таблицы более дружелюбными. Хорошая новость? Всего за несколько строк C# вы можете **установить цвет фона строки**, добавить **светло‑желтый фон**, и получить отшлифованную сетку, которая мгновенно улучшает читаемость.

В этом учебнике мы пройдем весь процесс, от получения `DataTable` в память до стилизации каждой строки тонкой желто‑белой полосой. К концу вы сможете **окрашивать строки чередующимся образом** с уверенностью, а также увидите несколько удобных вариантов, когда нужны разные оттенки или динамическая тема.

## Что понадобится

- Проект .NET, нацеленный на .NET 6 или новее (код также работает на .NET Framework 4.7+).  
- Библиотека для работы с электронными таблицами, поддерживающая объекты стилей — в примере используется обобщенный API `Workbook`/`Worksheet`, аналогичный библиотекам **Aspose.Cells**, **GemBox.Spreadsheet** или **ClosedXML**.  
- Источник `DataTable` — может быть результатом запроса к базе данных, импортом CSV или любой коллекцией в памяти.  

Дополнительные пакеты NuGet не требуются, кроме самой библиотеки для таблиц. Если вы используете Aspose.Cells, пространство имён — `Aspose.Cells`; для ClosedXML — `ClosedXML.Excel`. Соответственно замените вызовы `CreateStyle` и `ImportDataTable`.

## Шаг 1: Получить исходные данные как DataTable

Сначала — получаем данные, которые нужно отобразить. В реальных приложениях это обычно означает запрос к базе данных, но для наглядности мы создадим заглушку вспомогательного метода `GetData()`, который возвращает заполненный `DataTable`.

```csharp
// Step 1: Retrieve the source data as a DataTable
DataTable dataTable = GetData();   // Replace with your actual data retrieval logic
```

> **Почему это важно:** `DataTable` определяет строки и столбцы, которые позже получат чередующееся затенение. Если таблица пуста, нечего стилизовать, поэтому всегда проверяйте, что `Rows.Count` > 0 перед продолжением.

### Совет профессионала
Если вы получаете данные из Entity Framework, вы можете использовать `DataTable.Load(reader)` после выполнения `SqlCommand`. Это делает код аккуратным и избегает ручного определения столбцов.

## Шаг 2: Выделить массив для хранения стиля каждой строки

Далее нам нужен контейнер, соответствующий количеству строк. Большинство API электронных таблиц позволяют передать массив стилей в метод импорта, поэтому мы создадим `Style[]`, размером точно равным количеству строк.

```csharp
// Step 2: Allocate an array to hold a style for each row
Style[] rowStyles = new Style[dataTable.Rows.Count];
```

> **Объяснение:** Предварительно выделяя массив, мы избегаем создания нового объекта стиля на каждой итерации, что может повысить производительность при работе с тысячами строк.

## Шаг 3: Применить чередующиеся цвета строк (Светло‑желтый / Белый)

Теперь переходим к сути: **применить чередующиеся цвета строк**. Мы пройдемся по каждой строке, создадим новый экземпляр стиля из workbook и установим его фон в зависимости от индекса строки. Четные строки получают светло‑желтую заливку, нечетные остаются белыми.

```csharp
// Step 3: Create alternating background colors (light yellow / white) for the rows
for (int rowIndex = 0; rowIndex < dataTable.Rows.Count; rowIndex++)
{
    // Create a new style instance from the workbook
    rowStyles[rowIndex] = wb.CreateStyle();

    // Apply a light yellow background to even rows, white to odd rows
    rowStyles[rowIndex].ForegroundColor = (rowIndex % 2 == 0)
        ? Color.LightYellow   // add light yellow background
        : Color.White;        // set row background color to white

    rowStyles[rowIndex].Pattern = BackgroundType.Solid; // set alternating row shading
}
```

### Почему это работает
- **`rowIndex % 2 == 0`** проверяет, является ли строка чётной.  
- **`Color.LightYellow`** даёт мягкий, ненавязчивый оттенок, идеальный для таблиц данных.  
- **`BackgroundType.Solid`** гарантирует, что заливка покрывает всю ячейку, достигая эффекта **set row background color**.  

Вы можете заменить `Color.LightYellow` на любой другой оттенок (например, `Color.LightCyan`), если предпочитаете иной вид. Та же логика позволяет **окрашивать строки чередующимся образом** на основе других критериев, таких как флаги статуса.

## Шаг 4: Импортировать DataTable в Worksheet с подготовленными стилями

Наконец, мы помещаем всё в лист. Большинство библиотек предоставляют перегрузку `ImportDataTable`, принимающую массив стилей. Флаг `true` указывает API записать заголовки столбцов, а координаты `0, 0` начинают запись с ячейки в левом верхнем углу.

```csharp
// Step 4: Import the DataTable into the worksheet, applying the prepared row styles
ws.Cells.ImportDataTable(dataTable, true, 0, 0, rowStyles);
```

> **Результат:** Worksheet теперь отображает ваши данные с чистым шаблоном **alternating row shading** — светло‑желтый на чётных строках, белый на нечётных. Пользователи могут просматривать сетку, не перемещая глаза туда‑сюда.

### Ожидаемый результат
Если открыть полученную таблицу, вы увидите примерно следующее:

| ID | Name      | Quantity |
|----|-----------|----------|
| **1** | Apple      | 50       |
| **2** | Banana     | 30       |
| **3** | Cherry     | 20       |
| **4** | Date       | 15       |

Строки 1, 3, 5… имеют **light yellow background**, тогда как строки 2, 4, 6… остаются **white**. Заголовочная строка (строка 0) наследует стиль по умолчанию, если вы не настроите её отдельно.

## Дополнительные варианты и граничные случаи

### 1. Использование другой цветовой палитры
Если светло‑желтый конфликтует с вашим брендингом, просто замените `Color.LightYellow` на другой `System.Drawing.Color`. Для темы в сине‑серых тонах можно использовать:

```csharp
rowStyles[rowIndex].ForegroundColor = (rowIndex % 2 == 0)
    ? Color.FromArgb(220, 235, 247) // soft blue
    : Color.White;
```

### 2. Динамическое затенение на основе данных
Иногда нужно выделить строки, соответствующие условию (например, низкий запас). Скомбинируйте проверку модуля с пользовательским тестом:

```csharp
int quantity = Convert.ToInt32(dataTable.Rows[rowIndex]["Quantity"]);
if (quantity < 20)
{
    rowStyles[rowIndex].ForegroundColor = Color.Salmon; // urgent low‑stock color
}
else
{
    rowStyles[rowIndex].ForegroundColor = (rowIndex % 2 == 0)
        ? Color.LightYellow
        : Color.White;
}
```

### 3. Применение стилей только к определённым столбцам
Если вам нужен **set row background color** только в некоторых столбцах, создайте отдельный стиль для каждого столбца и назначьте его после импорта, используя API диапазона ячеек листа.

```csharp
// Example for column B only
var colBStyle = wb.CreateStyle();
colBStyle.ForegroundColor = Color.LightYellow;
colBStyle.Pattern = BackgroundType.Solid;

// Apply after import
ws.Cells[$"B2:B{dataTable.Rows.Count + 1}"].SetStyle(colBStyle);
```

### 4. Совет по производительности для больших таблиц
При работе с более чем 10 000 строками рассмотрите возможность повторного использования одного объекта стиля для каждого цвета вместо создания нового на каждую строку. Тогда массив будет содержать ссылки на два общих стиля, что значительно уменьшит использование памяти.

```csharp
Style yellowStyle = wb.CreateStyle();
yellowStyle.ForegroundColor = Color.LightYellow;
yellowStyle.Pattern = BackgroundType.Solid;

Style whiteStyle = wb.CreateStyle();
whiteStyle.ForegroundColor = Color.White;
whiteStyle.Pattern = BackgroundType.Solid;

for (int i = 0; i < dataTable.Rows.Count; i++)
    rowStyles[i] = (i % 2 == 0) ? yellowStyle : whiteStyle;
```

## Полный рабочий пример

Ниже приведена автономная программа, которую можно вставить в консольное приложение. Она использует вымышленный API `Workbook`/`Worksheet`; замените типы на те, что предоставляет выбранная вами библиотека.

```csharp
using System;
using System.Data;
using System.Drawing;          // For Color
using YourSpreadsheetLib;     // Replace with actual namespace

class Program
{
    static void Main()
    {
        // Initialize workbook & worksheet
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];

        // Step 1: Retrieve data
        DataTable dataTable = GetData();

        // Step 2: Allocate style array
        Style[] rowStyles = new Style[dataTable.Rows.Count];

        // Step 3: Apply alternating row colors
        for (int i = 0; i < dataTable.Rows.Count; i++)
        {
            rowStyles[i] = wb.CreateStyle();
            rowStyles[i].ForegroundColor = (i % 2 == 0)
                ? Color.LightYellow   // add light yellow background
                : Color.White;        // set row background color
            rowStyles[i].Pattern = BackgroundType.Solid; // set alternating row shading
        }

        // Step 4: Import with styles
        ws.Cells.ImportDataTable(dataTable, true, 0, 0, rowStyles);

        // Save to file
        wb.Save("AlternatingRows.xlsx");
        Console.WriteLine("Workbook saved with alternating row colors.");
    }

    // Sample data generator
    static DataTable GetData()
    {
        var dt = new DataTable();
        dt.Columns.Add("ID", typeof(int));
        dt.Columns.Add("Product", typeof(string));
        dt.Columns.Add("Quantity", typeof(int));

        dt.Rows.Add(1, "Apple", 50);
        dt.Rows.Add(2, "Banana", 30);
        dt.Rows.Add(3, "Cherry", 20);
        dt.Rows.Add(4, "Date", 15);
        dt.Rows.Add(5, "Elderberry", 5);
        return dt;
    }
}
```

**Вывод:** Файл с именем `AlternatingRows.xlsx`, где каждая строка чередуется между светло‑желтой заливкой и белым, делая таблицу более приятной для глаз.

## Часто задаваемые вопросы

**В:** Работает ли этот подход с условным форматированием в стиле Excel?  
**О:** Да. Если ваша библиотека поддерживает условные правила, вы можете перенести ту же логику в правило, проверяющее `MOD(ROW(),2)=0`. Метод, основанный на коде, показанный здесь, более переносим для библиотек, не имеющих встроенного условного форматирования.

**В:** Что если мне нужно **окрашивать строки чередующимся образом** в таблице PDF вместо листа Excel?  
**О:** Большинство генераторов PDF‑таблиц (например, iTextSharp, PdfSharp) позволяют задавать `BackgroundColor` для каждой строки. Тот же расчёт по модулю применяется—

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}