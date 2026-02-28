---
category: general
date: 2026-02-28
description: Быстро удаляйте строки в таблице Excel с помощью C#. Узнайте, как добавить
  именованный диапазон в Excel, получить доступ к листу по имени и избежать ошибок
  дублирования имен.
draft: false
keywords:
- delete rows excel table
- add named range excel
- access worksheet by name
- how to add defined name
- named range on another sheet
language: ru
og_description: Удаление строк в таблице Excel с помощью C#. Этот учебник также показывает,
  как добавить именованный диапазон в Excel и получить доступ к листу по имени.
og_title: Удаление строк в таблице Excel с помощью C# – Полное руководство
tags:
- C#
- Excel
- DevExpress Spreadsheet
title: Удаление строк в таблице Excel с помощью C# – пошаговое руководство
url: /ru/net/row-and-column-management/delete-rows-excel-table-with-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Удаление строк из таблицы Excel с помощью C# – Полный учебный материал

Когда‑нибудь нужно было **delete rows excel table** из рабочей книги, но вы не знали, какой вызов API использовать? Вы не одиноки — большинство разработчиков сталкиваются с тем же самым, когда впервые пытаются программно уменьшить таблицу.  

В этом руководстве мы пройдём полный, готовый к запуску пример, который не только удаляет строки из таблицы Excel, но и показывает, **как добавить определённое имя** (aka *named range*), **как получить лист по имени**, а также почему добавление дублирующего имени на другом листе вызывает `InvalidOperationException`.  

К концу статьи вы сможете:

* Получить лист, используя его название вкладки.  
* Безопасно удалить строки данных из первой таблицы на этом листе.  
* Создать именованный диапазон, указывающий на конкретный адрес.  
* Понять подводные камни дублирующих имён между листами.

Никакой внешней документации не требуется — всё, что нужно, находится здесь.

---

## Что понадобится

* **DevExpress Spreadsheet** (или любая библиотека, предоставляющая объекты `Workbook`, `Worksheet`, `ListObject` и `Names`).  
* Проект .NET, целящийся на **.NET 6** или новее (код также компилируется с .NET Framework 4.8).  
* Базовое знакомство с C# — если вы умеете писать `foreach`‑цикл, вам подойдёт.

> **Pro tip:** Если вы используете бесплатную Community Edition от DevExpress, используемые ниже API идентичны коммерческой версии.

---

## Шаг 1 – Получить лист по имени

Первое, что нужно сделать, — найти лист, содержащий таблицу, которую вы хотите изменить.  
Большинство разработчиков по привычке используют `Worksheets[0]`, но это связывает ваш код с порядком листов и ломается, как только кто‑то переименует вкладку.

```csharp
using DevExpress.Spreadsheet;

// Assume 'workbook' is an already‑loaded Workbook instance
Worksheet worksheet = workbook.Worksheets["Sheet1"];   // <-- access worksheet by name
```

*Почему это важно:* Используя **имя** листа вместо его индекса, вы избегаете случайных правок не того листа, когда структура книги меняется.  

Если указанное имя не существует, библиотека бросает `KeyNotFoundException`, который можно перехватить и вывести дружелюбное сообщение об ошибке.

---

## Шаг 2 – Delete Rows Excel Table (Безопасный способ)

Теперь, когда у вас правильный лист, удалим строки данных из первой таблицы.  
Распространённая ошибка — вызвать `DeleteRows(1, rowCount‑1)`. Начиная с **DevExpress 22.2** эта перегрузка **запрещена** и бросает `InvalidOperationException`. Библиотека ожидает, что вы будете удалять строки **внутри диапазона данных таблицы**, а не заголовка.

```csharp
// Grab the first table (ListObject) on the sheet
var table = worksheet.ListObjects[0];

// Calculate how many data rows we actually have (excluding the header)
int dataRowCount = table.DataRange.RowCount;

// Delete only the data rows – keep the header intact
if (dataRowCount > 0)
{
    // DeleteRows(startRow, rowCount) – startRow is zero‑based within the table
    table.DeleteRows(0, dataRowCount);
}
```

> **Что если таблица пуста?** Условие `if` предотвращает вызов с `rowCount = 0`, который иначе вызвал бы исключение.

### Визуальный обзор  

![delete rows excel table example](image.png "Скриншот, показывающий удаление строк из таблицы Excel")  

*Alt text: пример удаления строк из таблицы Excel в коде C#*

---

## Шаг 3 – Как добавить определённое имя (Создать именованный диапазон)

После очистки таблицы вы можете захотеть позже ссылаться на конкретный диапазон — например, для диаграммы или списка проверки данных. Здесь и пригодится **add named range excel**.

```csharp
// Define a name that points to A1:C5 on Sheet1
workbook.Names.Add("MyTable", "Sheet1!$A$1:$C$5");

// Verify that the name exists
Name definedName = workbook.Names["MyTable"];
Console.WriteLine($"Defined name '{definedName.Name}' points to {definedName.RefersTo}");
```

Метод `Names.Add` принимает два параметра: идентификатор и адрес в стиле A1.  
Поскольку мы ранее использовали **access worksheet by name**, строка адреса может безопасно ссылаться на любой лист без опасений по поводу изменения индексов.

---

## Шаг 4 – Именованный диапазон на другом листе – избежание ошибок дублирования имён

Вы можете подумать, что можно переиспользовать тот же идентификатор на другом листе, например так:

```csharp
// Attempt to add the same name on Sheet2 – this will throw
workbook.Names.Add("MyTable", "Sheet2!$A$1:$C$5");
```

К сожалению, область имён в Excel **охватывает всю книгу**, а не отдельный лист. Вызов выше приводит к `InvalidOperationException` с сообщением *“A name with the same identifier already exists.”*  

### Как обойти проблему

1. **Выберите уникальное имя** (`MyTable_Sheet2`).  
2. **Удалите существующее имя** перед повторным добавлением (только если действительно хотите его заменить).  

```csharp
// Option A – use a unique name
workbook.Names.Add("MyTable_Sheet2", "Sheet2!$A$1:$C$5");

// Option B – replace the existing name (use with caution)
if (workbook.Names.Contains("MyTable"))
    workbook.Names.Remove("MyTable");

workbook.Names.Add("MyTable", "Sheet2!$A$1:$C$5");
```

---

## Полный, готовый к запуску пример

Объединив всё вместе, получаем самостоятельное консольное приложение, которое можно вставить в Visual Studio и запустить против примера `sample.xlsx`.

```csharp
using System;
using DevExpress.Spreadsheet;

class Program
{
    static void Main()
    {
        // Load an existing workbook (replace with your file path)
        Workbook workbook = new Workbook();
        workbook.LoadDocument("sample.xlsx");

        // -------------------------------------------------
        // Step 1 – Access the worksheet by its tab name
        // -------------------------------------------------
        Worksheet worksheet = workbook.Worksheets["Sheet1"]; // primary sheet

        // -------------------------------------------------
        // Step 2 – Delete rows excel table (safe method)
        // -------------------------------------------------
        var table = worksheet.ListObjects[0];
        int dataRows = table.DataRange.RowCount;
        if (dataRows > 0)
            table.DeleteRows(0, dataRows); // removes only data rows

        // -------------------------------------------------
        // Step 3 – Add a defined name (named range) on Sheet1
        // -------------------------------------------------
        workbook.Names.Add("MyTable", "Sheet1!$A$1:$C$5");

        // -------------------------------------------------
        // Step 4 – Demonstrate duplicate‑name handling
        // -------------------------------------------------
        try
        {
            workbook.Names.Add("MyTable", "Sheet2!$A$1:$C$5");
        }
        catch (InvalidOperationException ex)
        {
            Console.WriteLine("Duplicate name error: " + ex.Message);
            // Use a unique identifier instead
            workbook.Names.Add("MyTable_Sheet2", "Sheet2!$A$1:$C$5");
        }

        // Save the modified workbook
        workbook.SaveDocument("sample_modified.xlsx");
        Console.WriteLine("Workbook updated successfully.");
    }
}
```

**Ожидаемый результат**

* Все строки данных из первой таблицы на **Sheet1** исчезают, остаётся только строка заголовка.  
* Имя **MyTable** теперь указывает на `Sheet1!$A$1:$C$5`.  
* Второе имя **MyTable_Sheet2** безопасно ссылается на диапазон на **Sheet2** без выбрасывания исключения.

---

## Часто задаваемые вопросы и особые случаи

| Вопрос | Ответ |
|----------|--------|
| *Что если в книге несколько таблиц?* | Получите нужный `ListObject` по индексу (`worksheet.ListObjects[1]`) или по имени (`worksheet.ListObjects["MyTable"]`). |
| *Можно ли удалить строки из таблицы, охватывающей несколько листов?* | Нет — таблицы ограничены одним листом. Нужно повторить логику удаления для каждого листа. |
| *Есть ли способ удалить только часть строк?* | Да — используйте `table.DeleteRows(startRow, count)`, где `startRow` считается с нуля внутри области данных таблицы. |
| *Сохраняются ли именованные диапазоны после сохранения?* | Абсолютно. После вызова `SaveDocument` имена становятся частью XML‑структуры книги. |
| *Как вывести список всех определённых имён в книге?* | Пройдитесь `foreach (var name in workbook.Names) Console.WriteLine(name.Name);`. |

---

## Заключение

Мы рассмотрели **delete rows excel table** с помощью C#, продемонстрировали **add named range excel** и показали правильный способ **access worksheet by name**, избегая злополучного исключения дублирования имён.  

Полное решение находится в кодовом фрагменте выше — скопируйте, вставьте и запустите его на своих файлах. Отсюда вы можете расширять логику для работы с несколькими таблицами, динамическими вычислениями диапазонов или даже интегрировать её в пользовательский интерфейс.

**Следующие шаги**, которые стоит исследовать:

* Использовать **named range on another sheet** для построения серий диаграмм.  
* Скомбинировать логику удаления с **ExcelDataReader** для импорта данных перед их очисткой.  
* Автоматизировать массовые обновления в десятках книг с помощью простого цикла `foreach (var file in Directory.GetFiles(...))`.

Есть дополнительные вопросы по автоматизации Excel в C#? Оставляйте комментарий, и давайте продолжать обсуждение. Счастливого кодинга!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}