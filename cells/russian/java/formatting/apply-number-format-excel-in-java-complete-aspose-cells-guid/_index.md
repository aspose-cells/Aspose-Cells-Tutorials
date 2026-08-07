---
category: general
date: 2026-07-20
description: Примените числовой формат в Excel с помощью Java и Aspose.Cells. Узнайте,
  как применить стиль валюты в Excel, создать рабочую книгу Excel на Java и эффективно
  импортировать DataTable в Excel.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- apply number format excel
- apply currency style excel
- create excel workbook java
- import datatable to excel
language: ru
lastmod: 2026-07-20
og_description: Применение числового формата в Excel с помощью Java. Это руководство
  показывает, как применить валютный стиль в Excel, создать рабочую книгу Excel на
  Java и импортировать DataTable в Excel шаг за шагом.
og_image_alt: Screenshot of an Excel workbook where apply number format excel has
  been applied to a currency column
og_title: Применение числового формата Excel в Java – Полный учебник по Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-07-20'
  description: Apply number format excel using Java and Aspose.Cells. Learn how to
    apply currency style excel, create excel workbook java, and import datatable to
    excel efficiently.
  headline: Apply Number Format Excel in Java – Complete Aspose.Cells Guide
  type: TechArticle
- questions:
  - answer: Absolutely. Open the workbook with `new Workbook("Existing.xlsx")`, fetch
      the target worksheet, and follow steps 3‑5 to apply the style array to new data.
    question: Can I apply the number format to an existing workbook?
  - answer: Use a different built‑in number index (`14` for short date, `22` for long
      date) or a custom format like `yyyy‑mm‑dd`. The workflow stays the same.
    question: What if I need to format dates instead of currency?
  - answer: 'Yes. Just change the file extension in `workbook.save("MyFile.xls")`.
      Aspose will automatically switch to the binary format. ## Wrap‑Up – What We
      Achieved We have **applied number format excel** to a column of monetary values,
      demonstrated how to **apply currency style excel**, shown the simplest wa'
    question: Does this work with older Excel versions (.xls)?
  type: FAQPage
tags:
- Aspose.Cells
- Java
- Excel Automation
title: Применение числового формата Excel в Java — Полное руководство по Aspose.Cells
url: /ru/java/formatting/apply-number-format-excel-in-java-complete-aspose-cells-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Применение числового формата Excel в Java – Полное руководство по Aspose.Cells

Когда‑нибудь задавались вопросом, как **apply number format excel** напрямую из кода Java? Возможно, вы генерируете финансовые отчёты или вам нужен быстрый способ оформить столбец сумм без ручного открытия Excel. Хорошие новости? С Aspose.Cells вы можете сделать это в паре строк, и вы также узнаете, как **apply currency style excel**, **create excel workbook java**, и **import datatable to excel** в одной удобной процедуре.

В этом руководстве мы пройдём реальный пример: список сумм, хранящийся в Java `List<Map<String,Object>>`, импортируется в новую рабочую книгу, первый столбец получает встроенный валютный формат, и файл сохраняется, готовый к распространению. Готовы увидеть, насколько это просто? Приступим.

## Требования – Что вам понадобится

- **Java Development Kit (JDK) 8+** – код работает на любой современной JDK.
- **Aspose.Cells for Java** library (Maven‑артефакт `com.aspose:aspose-cells`) – это движок, позволяющий работать с файлами Excel без установленного Office.
- **любимая IDE** (IntelliJ IDEA, Eclipse, VS Code…) – любой редактор подойдёт, но IDE ускоряет отладку.
- Базовое знакомство с **Java collections** – мы будем использовать `List` из `Map`, имитирующий DataTable.

Это всё. Никаких внешних сервисов, без установки Excel, только чистый Java.

## Шаг 1: Создание Excel Workbook Java – Инициализация Workbook

Первое, что нам нужно, — объект рабочей книги. Представьте его как пустой холст, где будет размещено всё.

```java
// Step 1: Create a new workbook instance
Workbook workbook = new Workbook(); // creates an in‑memory Excel file
```

Зачем создавать рабочую книгу вначале? Aspose.Cells работает полностью в памяти, поэтому вы можете добавлять листы, стили и данные, не касаясь диска. Такой подход быстрый и делает ваш код тестируемым.

## Шаг 2: Подготовка данных – импорт DataTable в Excel с использованием List of Maps

Во многих корпоративных приложениях данные приходят из баз в виде таблиц. Здесь мы имитируем это с помощью `List<Map<String,Object>>`. Каждый `Map` представляет строку, а ключ `"Amount"` сопоставлен числовому значению.

```java
// Step 2: Build a DataTable‑like structure (list of maps)
List<Map<String, Object>> dataRows = new ArrayList<>();

// Row 1
dataRows.add(new HashMap<>() {{
    put("Amount", 1234.56);
}});
// Row 2
dataRows.add(new HashMap<>() {{
    put("Amount", 7890.12);
}});
```

Вы можете спросить: «Почему не использовать `ResultSet` или POJO?» Метод `importDataTable` принимает любую коллекцию, ведёт себя как DataTable, а список карт — самый простой способ продемонстрировать концепцию без дополнительных зависимостей.

## Шаг 3: Определение числового формата – Apply Currency Style Excel

Теперь переходим к сердцу руководства: **apply number format excel**. Aspose.Cells поставляется со встроенными числовыми форматами; валютный формат имеет индекс 5. Мы берём стиль по умолчанию с первого листа, меняем его числовой формат и сохраняем для дальнейшего использования.

```java
// Step 3: Get the default style and set a currency number format
Style currencyStyle = workbook.getWorksheets().get(0).getCells().getDefaultStyle();
currencyStyle.setNumber(5); // 5 = built‑in currency format ($#,##0.00)
```

Почему используем стиль по умолчанию как основу? Он уже содержит шрифт, выравнивание и другие настройки книги, поэтому меняем только то, что важно — в данном случае числовой формат. Если нужен пользовательский формат (например, “€#,##0.00”), можно вызвать `currencyStyle.setCustom("#,##0.00 €")`.

## Шаг 4: Настройка параметров импорта – связывание массива стилей

Aspose.Cells позволяет передать массив объектов `Style`, соответствующий импортируемым столбцам. Поскольку у наших данных только один столбец, мы передаём массив из одного элемента, содержащий валютный стиль.

```java
// Step 4: Configure import options with the style array
ImportTableOptions importOptions = new ImportTableOptions();
importOptions.setStyleArray(new Style[] { currencyStyle });
```

Если понадобится оформить несколько столбцов по‑разному, просто расширьте массив: `new Style[] { styleForCol1, styleForCol2, … }`. Порядок стилей соответствует порядку столбцов в исходных данных.

## Шаг 5: Импорт данных – загрузка DataTable в лист

С готовой книгой, подготовленными данными и определёнными стилями мы наконец **import datatable to excel**. Начинаем с ячейки `A1`, включаем заголовки столбцов (`true`) и передаём `ImportTableOptions`.

```java
// Step 5: Perform the import
Worksheet worksheet = workbook.getWorksheets().get(0);
worksheet.getCells().importDataTable(dataRows, true, "A1", importOptions);
```

Обратите внимание на флаг `true` — Aspose.Cells автоматически создаст строку заголовка на основе ключей карт (`"Amount"`). Если установить `false`, заголовок будет опущен, что даст больший контроль над конечным макетом.

## Шаг 6: Сохранение файла – Create Excel Workbook Java на диске

Последний шаг — сохранить рабочую книгу из памяти в физический файл. Можно выбрать любой поддерживаемый Aspose формат (`.xlsx`, `.xls`, `.csv`, …). Здесь сохраняем как XLSX.

```java
// Step 6: Save the workbook to disk
String outputPath = "DataTableWithCurrencyStyle.xlsx";
workbook.save(outputPath);
System.out.println("Workbook saved to " + outputPath);
```

После выполнения программы откройте полученный файл. Вы увидите, что столбец `"Amount"` отформатирован с долларовым знаком, двумя знаками после запятой и правильными разделителями тысяч — именно то, что ожидается при **apply number format excel** для валютных значений.

## Ожидаемый результат

| Amount |
|--------|
| $1,234.56 |
| $7,890.12 |

Заголовок “Amount” отображается полужирным (стиль по умолчанию), а каждая ячейка ниже показывает установленный валютный формат. Ручное форматирование в Excel не требуется.

## Полезные советы и распространённые подводные камни

- **Reuse Styles Wisely** – Стили лёгкие, но создание нового `Style` для каждой ячейки может ухудшить производительность. Всегда переиспользуйте объект стиля, когда применяете один и тот же формат к множеству ячеек, как мы сделали с `currencyStyle`.
- **Custom Formats** – Если в вашей локали используется другой валютный символ, замените `currencyStyle.setNumber(5)` на `currencyStyle.setCustom("€#,##0.00")`. Проверьте формат в Excel, чтобы убедиться, что он работает как ожидается.
- **Large Datasets** – Для тысяч строк рассмотрите использование `importDataTable` с флагом `ImportTableOptions.setImportDataOnly(true)`, чтобы пропустить генерацию заголовков и ускорить импорт.
- **Thread Safety** – Объекты Aspose.Cells **не** являются потокобезопасными. Создавайте отдельный `Workbook` для каждого потока, если генерируете отчёты параллельно.

## Часто задаваемые вопросы

**Q: Можно ли применить числовой формат к уже существующей рабочей книге?**  
A: Конечно. Откройте книгу через `new Workbook("Existing.xlsx")`, получите нужный лист и выполните шаги 3‑5, чтобы применить массив стилей к новым данным.

**Q: Что делать, если нужно форматировать даты, а не валюту?**  
A: Используйте другой встроенный числовой индекс (`14` для короткой даты, `22` для полной даты) или пользовательский формат, например `yyyy‑mm‑dd`. Рабочий процесс остаётся тем же.

**Q: Работает ли это с более старыми версиями Excel (.xls)?**  
A: Да. Просто измените расширение в `workbook.save("MyFile.xls")`. Aspose автоматически переключится на бинарный формат.

## Итоги – Что мы достигли

Мы **applied number format excel** к столбцу денежных значений, продемонстрировали, как **apply currency style excel**, показали самый простой способ **create excel workbook java** и использовали Aspose.Cells для **import datatable to excel** без обращения к пользовательскому интерфейсу. Всё это выполнено в компактной, автономной программе, которую можно скопировать, вставить и запустить.

Что дальше? Попробуйте расширить пример:

- Добавьте больше столбцов (например, “Date”, “Description”) и назначьте разные стили каждому столбцу.  
- Экспортируйте те же данные в CSV и сравните, как теряются числовые форматы.  
- Интегрируйте код в сервис Spring Boot, который возвращает рабочую книгу как загружаемый HTTP‑ответ.

Экспериментируйте, и если возникнут сложности, оставляйте комментарий ниже. Приятного кодинга!

## Что стоит изучить дальше?

Следующие руководства охватывают смежные темы, построенные на техниках, продемонстрированных в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, помогающими освоить дополнительные возможности API и исследовать альтернативные подходы в ваших проектах.

- [Как применять стили к ячейкам Excel с помощью Aspose.Cells для Java – Полное руководство](/cells/english/java/formatting/apply-styles-excel-aspose-cells-java/)
- [Объединение ячеек и применение стилей в Excel с помощью Aspose.Cells для Java – Полное руководство](/cells/english/java/formatting/merge-cells-apply-styles-aspose-cells-java/)
- [Aspose.Cells для Java: Как эффективно создавать и форматировать рабочие книги Excel](/cells/english/java/getting-started/aspose-cells-java-workbook-creation-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}