---
category: general
date: 2026-02-15
description: Создайте новую книгу в C# и узнайте, как добавить таблицу, включить фильтр
  и сохранить книгу в формате xlsx. Быстрое, полное руководство по автоматизации Excel.
draft: false
keywords:
- create new workbook
- save workbook as xlsx
- how to create workbook
- how to add table
- how to enable filter
language: ru
og_description: Создайте новую книгу в C# и сразу добавьте таблицу, включите фильтры,
  затем сохраните её в формате xlsx. Следуйте этому краткому практическому руководству.
og_title: Создание новой рабочей книги в C# – Полное руководство по программированию
tags:
- C#
- Aspose.Cells
- Excel Automation
title: Создание новой рабочей книги в C# – пошаговое руководство
url: /ru/net/excel-workbook/create-new-workbook-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание новой книги Excel в C# – Полное руководство по программированию

Когда‑то вам нужно было **create new workbook** в C#, но вы не знали, с какими объектами начинать? Вы не одиноки; многие разработчики сталкиваются с этим при автоматизации файлов Excel. В этом руководстве мы пройдёмся по созданию новой книги, вставке таблицы, включению авто‑фильтра и, наконец, **save workbook as xlsx** — всё с понятным, готовым к запуску кодом.

Мы также ответим на часто задаваемые вопросы «как добавить таблицу» и «как включить фильтр», которые обычно возникают после первоначального создания книги. К концу вы получите автономный пример, который можно вставить в любой .NET‑проект без лишних дополнений.

## Предварительные требования и настройка

Прежде чем погрузиться в детали, убедитесь, что у вас есть:

- **.NET 6** (или любая современная версия .NET) установлен.
- Пакет NuGet **Aspose.Cells for .NET** (`Install-Package Aspose.Cells`) — эта библиотека предоставляет классы `Workbook`, `Worksheet` и `ListObject`, используемые ниже.
- Любая удобная среда разработки (Visual Studio, VS Code, Rider — выбирайте, что нравится).

Дополнительная конфигурация не требуется; код работает сразу после подключения пакета.

![Скриншот, показывающий только что созданную книгу Excel – create new workbook](image.png)

*Текст alt: “create new workbook screenshot in Excel”*

## Шаг 1: Создание новой книги и доступ к первому листу

Первое, что нужно сделать, — создать объект `Workbook`. Представьте себе открытие совершенно нового файла Excel, который сейчас содержит один лист по умолчанию. Затем получите ссылку на лист, чтобы начать его заполнять.

```csharp
using Aspose.Cells;

public class WorkbookDemo
{
    public static void Main()
    {
        // Step 1: Create a new workbook (this is the "create new workbook" part)
        Workbook workbook = new Workbook();

        // Access the first worksheet – by default it is named "Sheet1"
        Worksheet worksheet = workbook.Worksheets[0];
```

**Почему это важно:** Создание книги даёт чистый холст; доступ к первому листу гарантирует, что у вас есть цель для будущей таблицы. Если пропустить этот шаг, любые последующие вызовы `ListObject` вызовут ошибку null reference.

## Шаг 2: Как добавить таблицу на лист

Теперь, когда у нас есть лист, вставим таблицу, охватывающую ячейки **A1:C5**. В Aspose.Cells коллекция `ListObjects` управляет таблицами (также называемыми *list objects*). Добавление таблицы происходит в два шага: вызываем `Add` для её создания, затем сохраняем результат в переменную `ListObject` для удобного управления.

```csharp
        // Step 2: Add a table named "MyTable" covering the range A1:C5
        int tableIndex = worksheet.ListObjects.Add("MyTable", "A1:C5", true);
        ListObject table = worksheet.ListObjects[tableIndex];
```

**Что происходит «под капотом»?** Метод `Add` регистрирует таблицу во внутреннем движке Excel, присваивая ей уникальный индекс. Сохранив этот индекс в `tableIndex`, мы можем получить реальный экземпляр `ListObject`, который даёт полный контроль над свойствами таблицы.

### Совет профессионала
Если планируете создавать несколько таблиц, храните их индексы в списке — это упростит последующие обновления.

## Шаг 3: Как включить фильтр в таблице

Таблицы в Excel по умолчанию имеют строку авто‑фильтра, но в зависимости от способа создания таблицы её может потребоваться включить явно. Свойство `ShowAutoFilter` переключает эту строку включено/выключено.

```csharp
        // Step 3: Enable the auto‑filter for the table
        table.ShowAutoFilter = true;
```

После включения пользователи могут нажимать стрелки‑выпадающие в строке заголовков, чтобы фильтровать строки по значениям. Это особенно удобно для больших наборов данных.

### А если фильтр не нужен?
Просто установите `ShowAutoFilter` в `false`, и стрелки исчезнут. Следующая строка демонстрирует обратное действие:

```csharp
        // Disable (remove) the auto‑filter
        table.ShowAutoFilter = false;
```

## Шаг 4: Сохранить книгу как XLSX

Все тяжёлые операции выполнены; теперь сохраняем книгу на диск. Метод `Save` принимает полный путь и автоматически определяет формат файла по расширению. Здесь мы явно **save workbook as xlsx**.

```csharp
        // Step 4: Save the workbook to a file
        string outputPath = @"C:\Temp\NoFilter.xlsx"; // Change to your desired folder
        workbook.Save(outputPath);
    }
}
```

Когда откроете `NoFilter.xlsx`, вы увидите один лист с таблицей под именем **MyTable**, охватывающей A1:C5, и — поскольку мы установили `ShowAutoFilter` в `false` — стрелки фильтра не будут видны.

### Ожидаемый результат
- Файл `NoFilter.xlsx` в указанной вами папке.
- На листе Sheet1 таблица 5 строк × 3 столбца с данными по умолчанию (пустые ячейки, если вы их не заполняете).
- Строка авто‑фильтра не отображается.

## Вариации и граничные случаи

### Оставить фильтр включённым
Если вам нужен постоянный фильтр, просто опустите строку, где устанавливается `ShowAutoFilter = false`. Таблица появится со стрелками фильтра, готовыми к использованию.

### Добавление нескольких таблиц
Можно повторить **Шаг 2** с другими диапазонами и именами:

```csharp
int secondTableIdx = worksheet.ListObjects.Add("SecondTable", "E1:G10", true);
ListObject secondTable = worksheet.ListObjects[secondTableIdx];
secondTable.ShowAutoFilter = true;
```

### Заполнение таблицы данными
Aspose.Cells позволяет записывать значения непосредственно в ячейки до или после создания таблицы. Например, чтобы заполнить первый столбец числами:

```csharp
for (int i = 0; i < 5; i++)
{
    worksheet.Cells[i, 0].PutValue(i + 1); // A1‑A5 = 1‑5
}
```

### Примечание о совместимости
Код работает с **Aspose.Cells 23.9** и новее. Если вы используете более старую версию, сигнатура метода `Add` может немного отличаться — проверьте примечания к выпуску библиотеки.

## Частые ошибки и как их избежать

- **Не подключён Aspose.Cells** — компилятор будет ругаться на неизвестные типы. Убедитесь, что пакет установлен и в начале файла есть `using Aspose.Cells;`.
- **Неправильная строка диапазона** — диапазоны Excel нечувствительны к регистру, но должны быть корректными (например, `"A1:C5"`, а не `"A1:C"`). Ошибка вызовет `CellsException`.
- **Проблемы с правами доступа к пути** — попытка сохранить файл в защищённую папку (например, `C:\Program Files`) приведёт к `UnauthorizedAccessException`. Используйте записываемый каталог, такой как `%TEMP%` или ваш профиль пользователя.

## Полный рабочий пример (готов к копированию)

```csharp
using Aspose.Cells;

public class WorkbookDemo
{
    public static void Main()
    {
        // 1️⃣ Create new workbook
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ Add a table named "MyTable" covering A1:C5
        int tableIdx = worksheet.ListObjects.Add("MyTable", "A1:C5", true);
        ListObject table = worksheet.ListObjects[tableIdx];

        // 3️⃣ Enable auto‑filter (you can skip this if you don't need it)
        table.ShowAutoFilter = true;

        // OPTIONAL: Disable the filter if you don't want it visible
        // table.ShowAutoFilter = false;

        // 4️⃣ Save workbook as xlsx
        string outputPath = @"C:\Temp\NoFilter.xlsx";
        workbook.Save(outputPath);
    }
}
```

Запустите программу, откройте сгенерированный файл, и вы увидите точно такой же результат, как описано выше.

## Итоги

Мы начали с **create new workbook**, затем узнали **how to add table**, переключили **how to enable filter**, и наконец **save workbook as xlsx**. Каждый шаг был объяснён с указанием *почему* он важен, а не только *что* писать, чтобы вы могли адаптировать шаблон под более сложные сценарии.

## Что дальше?

- **Стилизация таблицы** — исследуйте `TableStyleType`, чтобы придать данным профессиональный вид.
- **Вставка формул** — используйте `Cells[i, j].Formula = "=SUM(A2:A5)"` для расчётов.
- **Экспорт в PDF** — Aspose.Cells также может сохранять книгу в PDF одним вызовом `Save`.
- **Чтение существующих книг** — замените `new Workbook()` на `new Workbook("ExistingFile.xlsx")`, чтобы модифицировать файлы «на лету».

Экспериментируйте с этими идеями и не стесняйтесь оставлять комментарии, если что‑то непонятно. Приятного кодинга и наслаждайтесь автоматизацией Excel с C#!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}