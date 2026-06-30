---
category: general
date: 2026-06-30
description: Создайте условное форматирование в рабочей книге Excel с помощью Aspose.Cells.
  Узнайте, как задать фон ячейки, ранжировать ячейки и программно сформировать файл.
draft: false
keywords:
- create conditional formatting
- create excel workbook
- set cell background
- how to rank cells
- how to use aspose
language: ru
og_description: Создайте условное форматирование в рабочей книге Excel с помощью Aspose.Cells.
  Следуйте этому полному руководству, чтобы задать фон ячеек, ранжировать их и автоматизировать
  работу с Excel.
og_title: Создайте условное форматирование в Excel с помощью Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Create conditional formatting in an Excel workbook using Aspose.Cells.
    Learn how to set cell background, rank cells, and build the file programmatically.
  headline: Create Conditional Formatting in Excel with Aspose.Cells – Step‑by‑Step
    Guide
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: Создание условного форматирования в Excel с помощью Aspose.Cells – пошаговое
  руководство
url: /ru/net/excel-conditional-formatting/create-conditional-formatting-in-excel-with-aspose-cells-ste/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание условного форматирования в Excel с помощью Aspose.Cells – пошаговое руководство

Когда‑то задавались вопросом, как **создать условное форматирование** в файле Excel без открытия пользовательского интерфейса? Вы не одиноки. Многие разработчики нуждаются в **создании excel workbook** «на лету», и программный подход экономит часы ручной работы. В этом руководстве мы покажем, как **создать условное форматирование**, оформить ячейки и даже ранжировать лучшие значения — все это с помощью мощной библиотеки Aspose.Cells для .NET.

Мы пройдём реальный пример: генерацию листа оценок, подсветку высоких баллов светло‑зеленым и заливку золотым цветом топ‑3 исполнителей. К концу вы будете знать **как задать фон ячейки**, **как ранжировать ячейки** и **как использовать Aspose** для сложной автоматизации Excel. Без лишних слов, только готовое, исполняемое решение, которое можно вставить в любой C#‑проект.

## Что вы узнаете

- Как **создать excel workbook** с помощью Aspose.Cells  
- Как заполнить диапазон случайными данными (оценками)  
- Как **задать фон ячейки** сплошными цветами  
- Как применить правило на основе формулы для **ранжирования ячеек** и подсветки трёх лучших  
- Как сохранить результат в файл .xlsx  

Предварительные требования: .NET 6+ (или .NET Framework 4.6+), Visual Studio (или любой C# IDE) и ссылка на пакет Aspose.Cells NuGet. Если вы никогда не работали с Aspose, не переживайте — мы расскажем, **как использовать Aspose** с нуля.

---

![Create conditional formatting example](https://example.com/images/create-conditional-formatting.png "Screenshot showing conditional formatting in the generated Excel file")

*Текст альтернативы изображения: пример создания условного форматирования в рабочей книге Excel, сгенерированной с помощью Aspose.Cells.*

## Как создать Excel Workbook с помощью Aspose.Cells

Первое, что нужно: объект рабочей книги. Aspose.Cells делает это однострочным вызовом.

```csharp
using Aspose.Cells;
using System.Drawing;

void CreateConditionalFormattingWorkbook()
{
    // Step 1: Instantiate a new workbook and give the first sheet a friendly name
    Workbook workbook = new Workbook();                 // creates an empty workbook
    Worksheet sheet = workbook.Worksheets[0];           // grab the default worksheet
    sheet.Name = "Scores";                              // rename it to something meaningful
```

Зачем мы переименовываем лист? Ясное имя (например, **Scores**) упрощает дальнейшее обращение, особенно когда файл передаётся пользователям без технической подготовки.  

Теперь, когда рабочая книга существует, заполним столбец A случайными оценками.

## Как заполнить данные – создание случайных оценок

```csharp
    // Step 2: Populate A2:A21 with random values between 40 and 99
    Random random = new Random();
    for (int i = 0; i < 20; i++)               // 20 rows of data
    {
        sheet.Cells[i + 1, 0].PutValue(random.Next(40, 100));
    }
```

Краткое замечание: `PutValue` автоматически определяет тип данных, поэтому не требуется приводить к `int`. Цикл начинается с `i = 0`, но записывает в строку `i + 1`, потому что строки Excel нумеруются с 1, а коллекция `Cells` — с 0.

## Как задать фон ячейки для высоких оценок

Теперь мы **создадим условное форматирование**, которое закрасит любую оценку ≥ 80 светло‑зеленым оттенком.

```csharp
    // Step 3: Define a conditional formatting range (A2:A21)
    int firstRow = 1, lastRow = 20;                     // zero‑based indices for rows 2‑21
    int cfIndex = sheet.ConditionalFormattings.Add(firstRow, 0, lastRow, 0);
    ConditionalFormatting cf = sheet.ConditionalFormattings[cfIndex];

    // Add a rule: cell value >= 80 → light‑green background
    FormatCondition highScoreCondition = cf.AddCondition(
        FormatConditionType.CellValue,
        OperatorType.GreaterOrEqual,
        "80");

    highScoreCondition.Style.ForegroundColor = Color.LightGreen;
    highScoreCondition.Style.Pattern = BackgroundType.Solid;
```

Свойство `ForegroundColor` управляет цветом заливки, а `Pattern = BackgroundType.Solid` указывает Excel использовать сплошную заливку вместо градиента или узора. Это и есть ядро **как задать фон ячейки** в зависимости от числового порога.

## Как ранжировать ячейки и подсветить топ‑3

Ранжирование чуть сложнее, потому что нам нужна формула, оценивающая каждую ячейку относительно всего диапазона. Aspose.Cells позволяет использовать ту же синтаксис формул Excel, что и в пользовательском интерфейсе.

```csharp
    // Step 4: Add a formula‑based rule to color the top‑3 scores gold
    FormatCondition topThreeCondition = cf.AddCondition(
        FormatConditionType.Formula,
        null,
        null);

    // The formula uses the RANK function; note the absolute references ($) lock the range
    topThreeCondition.Formula1 = "=RANK(A2,$A$2:$A$21)<=3";

    topThreeCondition.Style.ForegroundColor = Color.Gold;
    topThreeCondition.Style.Pattern = BackgroundType.Solid;
```

Почему в формуле используется `A2`? Aspose оценивает формулу относительно каждой ячейки диапазона, поэтому `A2` автоматически смещается в `A3`, `A4` и т.д., когда правило применяется построчно. Функция `RANK` возвращает позицию значения в указанном диапазоне, а часть `<=3` гарантирует, что только три самых высоких результата получат золотую заливку.

## Как сохранить рабочую книгу

```csharp
    // Step 5: Persist the workbook to disk
    workbook.Save("YOUR_DIRECTORY/Scores_ConditionalFormatting.xlsx");
}
```

Замените `YOUR_DIRECTORY` на абсолютный или относительный путь, в который ваше приложение имеет право записи. После выполнения метода откройте файл в Excel, и вы увидите:

- Светло‑зеленые ячейки для любой оценки ≥ 80  
- Золотые ячейки для трёх самых высоких оценок, независимо от того, превышают ли они 80  

Это полностью завершённый pipeline **создания условного форматирования**.

---

## Полный, готовый к запуску пример

Ниже представлен весь метод ещё раз, готовый к копированию‑вставке в консольное приложение или любой C#‑класс:

```csharp
using Aspose.Cells;
using System.Drawing;

void CreateConditionalFormattingWorkbook()
{
    // Step 1: Create a new workbook and name the first worksheet
    Workbook workbook = new Workbook();
    Worksheet sheet = workbook.Worksheets[0];
    sheet.Name = "Scores";

    // Step 2: Fill column A (A2:A21) with random scores between 40 and 99
    Random random = new Random();
    for (int i = 0; i < 20; i++)
    {
        sheet.Cells[i + 1, 0].PutValue(random.Next(40, 100));
    }

    // Step 3: Highlight scores >= 80 with a light‑green background
    int firstRow = 1, lastRow = 20;
    int cfIndex = sheet.ConditionalFormattings.Add(firstRow, 0, lastRow, 0);
    ConditionalFormatting cf = sheet.ConditionalFormattings[cfIndex];
    FormatCondition highScoreCondition = cf.AddCondition(
        FormatConditionType.CellValue,
        OperatorType.GreaterOrEqual,
        "80");
    highScoreCondition.Style.ForegroundColor = Color.LightGreen;
    highScoreCondition.Style.Pattern = BackgroundType.Solid;

    // Step 4: Color the top‑3 scores with a gold background using a formula rule
    FormatCondition topThreeCondition = cf.AddCondition(
        FormatConditionType.Formula,
        null,
        null);
    topThreeCondition.Formula1 = "=RANK(A2,$A$2:$A$21)<=3";
    topThreeCondition.Style.ForegroundColor = Color.Gold;
    topThreeCondition.Style.Pattern = BackgroundType.Solid;

    // Step 5: Save the workbook
    workbook.Save("YOUR_DIRECTORY/Scores_ConditionalFormatting.xlsx");
}
```

### Ожидаемый результат

При открытии `Scores_ConditionalFormatting.xlsx`:

- Ячейки со значениями **80** и выше подсвечиваются светло‑зеленым.  
- Три наивысших числа (даже если они ниже 80) отображаются с **золотым** фоном.  
- Все остальные ячейки сохраняют стандартный белый фон.

Такой визуальный индикатор мгновенно показывает менеджеру, кто является топ‑исполнителем, без необходимости ручной сортировки.

---

## Часто задаваемые вопросы и особые случаи

**Что если нужно более трёх лучших результатов?**  
Просто измените часть формулы `<=3` на `<=5` (или любое другое число). Правило автоматически подстроится.

**Можно ли применить несколько диапазонов форматирования?**  
Конечно. Вызовите `sheet.ConditionalFormattings.Add` ещё раз с другим диапазоном, затем добавьте условия к новому объекту `ConditionalFormatting`.

**Что насчёт более старых версий Excel?**  
Aspose.Cells по умолчанию сохраняет в современном формате `.xlsx`, совместимом с Excel 2007 и новее. Если нужен `.xls`, передайте `SaveFormat.Excel97To2003` в метод `Save`.

**Влияет ли это на производительность больших листов?**  
Условное форматирование хранится как метаданные, поэтому существенно не увеличивает размер файла. Однако генерация сотен тысяч строк может повысить потребление памяти — рекомендуется обрабатывать данные пакетами.

---

## Следующие шаги

Теперь, когда вы освоили **как создать условное форматирование**, можете изучить:

- **Как создавать диаграммы Excel** программно (ещё один «драгоценный камень» Aspose.Cells)  
- **Как задать фон ячейки** на основе текстовых значений (например, “Pass/Fail”)  
- **Как использовать Aspose.Cells для проверки данных** и выпадающих списков  

Каждая из этих тем опирается на те же основы, которые вы только что изучили, так что вам будет легко приступить.

---

## Итоги

Мы прошли полный пример от начала до конца, показывающий, как **создать условное форматирование** в рабочей книге Excel с помощью Aspose.Cells. От инициализации книги, заполнения данными, **задания фона ячейки**, ранжирования топ‑исполнителей до финального сохранения файла — каждый шаг был рассмотрен с учётом **как ранжировать ячейки** и **как использовать Aspose**.  

Запустите код, поиграйте с порогами и наблюдайте, как быстро можно генерировать отшлифованные отчёты для любого бизнес‑сценария. Есть свои идеи? Оставляйте комментарий ниже — приятного кодинга!

## Что изучать дальше?

Следующие руководства охватывают тесно связанные темы, расширяющие техники, продемонстрированные в этом гайде. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, чтобы вы могли освоить дополнительные возможности API и исследовать альтернативные подходы в своих проектах.

- [Automate Excel Conditional Formatting Using Aspose.Cells for Java&#58; A Complete Guide](/cells/english/java/formatting/automate-conditional-formatting-excel-aspose-cells-java/)
- [How to Create & Format Excel Cells Using Aspose.Cells for Java&#58; A Step‑By‑Step Guide](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)
- [Create an Excel Workbook using Aspose.Cells in Java&#58; A Step‑By‑Step Guide](/cells/english/java/getting-started/create-excel-workbook-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}