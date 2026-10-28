---
category: general
date: 2026-08-04
description: Создайте таблицу Excel в Java и узнайте, как отключить автофильтр, задать
  диапазон ячеек и сохранить книгу в формате xlsx с полным примером кода.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel table
- turn off autofilter
- define cell range
- save workbook as xlsx
- disable autofilter in excel
language: ru
lastmod: 2026-08-04
og_description: Создайте таблицу Excel в Java, отключите автофильтр, задайте диапазон
  ячеек и сохраните книгу в формате xlsx. Следуйте этому полному руководству, чтобы
  освоить автоматизацию Excel.
og_image_alt: Image showing how to create excel table without autofilter using Java
og_title: Создать таблицу Excel в Java – полный разбор кода
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Create excel table in Java and learn how to turn off autofilter, define
    cell range, and save workbook as xlsx with a complete code example.
  headline: Create excel table in Java – step‑by‑step guide
  type: TechArticle
- description: Create excel table in Java and learn how to turn off autofilter, define
    cell range, and save workbook as xlsx with a complete code example.
  name: Create excel table in Java – step‑by‑step guide
  steps:
  - name: Define cell range for the table
    text: Next, you must specify the exact area that will become the table. The **define
      cell range** step tells Aspose.Cells which rows and columns to include.
  - name: Add the table and enable its default AutoFilter
    text: Now you add a `ListObject` (the Aspose.Cells representation of an Excel
      table). By default, a new table includes an AutoFilter dropdown for each column.
  - name: Turn off autofilter for the table
    text: If you want a clean table without filter dropdowns, you must **turn off
      autofilter** (or **disable autofilter in excel**). The API call is straightforward.
  - name: Save workbook as xlsx file
    text: Finally, persist the workbook to disk. The **save workbook as xlsx** call
      writes a standard Office Open XML file that any modern spreadsheet program can
      open.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Создание Excel‑таблицы в Java – пошаговое руководство
url: /ru/java/tables-structured-references/create-excel-table-in-java-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создать таблицу Excel в Java – пошаговое руководство

Если вам нужно **создать таблицу Excel** в Java, этот учебник покажет, как это сделать. Вы научитесь **определять диапазон ячеек**, **отключать автофильтр** и **сохранять книгу в формате xlsx** с помощью одной готовой к запуску программы.

В примере используется библиотека Aspose.Cells for Java, которая предоставляет высокоуровневый API для автоматизации Excel. Дополнительные зависимости не требуются, кроме JAR‑файла Aspose.Cells. К концу руководства у вас будет автономное решение, которое можно добавить в любой проект Java.

## Что вы создадите

* Новая книга, содержащая один лист.  
* Таблица (ListObject), охватывающая определённый **диапазон ячеек** (A1:D5).  
* AutoFilter таблицы отключён **off** (т.е. **disable autofilter in excel**).  
* Книга сохранена в виде файла **xlsx** на диске.

## Предварительные требования

* Установлен Java 8 или новее.  
* Aspose.Cells for Java (скачайте с официального сайта или добавьте через Maven).  
* Базовое знакомство с синтаксисом Java и IDE, такими как IntelliJ IDEA или Eclipse.

---

## Как создать таблицу Excel без автофильтра в Java

Первый основной шаг — создать объект `Workbook` и получить лист по умолчанию. Это дает вам чистый холст, на котором можно разместить таблицу.

```java
import com.aspose.cells.*;

public class CreateExcelTable {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);
```

**Почему это важно:**  
`Workbook` представляет весь файл Excel. Первый лист (`get(0)`) создаётся автоматически, поэтому вам не нужно добавлять его вручную. Начало с чистого листа гарантирует, что оставшиеся данные не помешают создаваемой таблице.

### Определить диапазон ячеек для таблицы

Далее необходимо указать точную область, которая станет таблицей. Шаг **define cell range** сообщает Aspose.Cells, какие строки и столбцы включить.

```java
        // Step 2: Define the cell range that will become the table (A1:D5)
        CellArea tableRange = CellArea.createCellArea("A1", "D5");
```

**Почему это важно:**  
`CellArea` кодирует верхний‑левый и нижний‑правый углы диапазона. Используя `"A1"` и `"D5"`, вы создаёте блок 5 строк × 4 столбцов, что типично для простой таблицы данных.

### Добавить таблицу и включить её AutoFilter по умолчанию

Теперь вы добавляете `ListObject` (представление таблицы Excel в Aspose.Cells). По умолчанию новая таблица включает выпадающий список AutoFilter для каждого столбца.

```java
        // Step 3: Add a table (ListObject) to the worksheet and enable its AutoFilter
        ListObject table = worksheet.getListObjects().add("MyTable", tableRange, true);
        table.setShowAutoFilter(true); // AutoFilter is turned on by default
```

**Почему это важно:**  
Включение `setShowAutoFilter(true)` имитирует поведение Excel по умолчанию, делая таблицу сразу фильтруемой. Этот шаг необязателен, но уточняет состояние перед отключением.

### Отключить автофильтр для таблицы

Если вам нужна чистая таблица без выпадающих списков фильтра, необходимо **отключить автофильтр** (или **disable autofilter in excel**). Вызов API прост.

```java
        // Step 4: Disable the AutoFilter for the table
        table.setShowAutoFilter(false);
```

**Почему это важно:**  
Отключение AutoFilter улучшает читаемость при использовании таблицы для отчётов или печати. Это также уменьшает загромождение интерфейса для конечных пользователей, которым не нужен интерактивный фильтр.

### Сохранить книгу в файл xlsx

Наконец, сохраняем книгу на диск. Вызов **save workbook as xlsx** записывает стандартный файл Office Open XML, который может открыть любая современная табличная программа.

```java
        // Step 5: Save the workbook to a file
        workbook.save("TableNoAutoFilter.xlsx", SaveFormat.XLSX);
    }
}
```

**Почему это важно:**  
Выбор формата `XLSX` обеспечивает совместимость с Excel 2007+ и облачными сервисами, такими как Google Sheets. Имя файла `TableNoAutoFilter.xlsx` явно указывает, что AutoFilter отключён.

---

## Полный обзор исходного кода

Объединяя все фрагменты, получаем полную, готовую к запуску программу:

```java
import com.aspose.cells.*;

public class CreateExcelTable {
    public static void main(String[] args) throws Exception {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Define the cell range that will become the table (A1:D5)
        CellArea tableRange = CellArea.createCellArea("A1", "D5");

        // Add a table (ListObject) to the worksheet and enable its AutoFilter
        ListObject table = worksheet.getListObjects().add("MyTable", tableRange, true);
        table.setShowAutoFilter(true); // AutoFilter is on by default

        // Disable the AutoFilter for the table
        table.setShowAutoFilter(false);

        // Save the workbook to a file (xlsx format)
        workbook.save("TableNoAutoFilter.xlsx", SaveFormat.XLSX);
    }
}
```

**Ожидаемый результат:**  
Когда вы откроете `TableNoAutoFilter.xlsx` в Microsoft Excel, вы увидите таблицу с именем **MyTable**, охватывающую ячейки A1:D5. На заголовках столбцов не будет стрелок фильтра, что подтверждает успешное выполнение шага **turn off autofilter**.

---

## Часто задаваемые вопросы и особые случаи

| Question | Answer |
|----------|--------|
| *Могу ли я добавить данные перед созданием таблицы?* | Да. Сначала заполните ячейки в определённом диапазоне; таблица автоматически включит эти данные. |
| *Что если лист уже содержит данные?* | Выберите другой **cell range**, который не пересекается с существующим содержимым, или очистите область с помощью `worksheet.getCells().clear(A1, D5)`. |
| *Можно ли оставить AutoFilter только для некоторых столбцов?* | Aspose.Cells не поддерживает переключение AutoFilter для отдельных столбцов; его можно либо включить для всей таблицы, либо отключить полностью. |
| *Как изменить стиль таблицы?* | Используйте `table.setTableStyleType( TableStyleType.TABLE_STYLE_MEDIUM_2 );` перед сохранением. |
| *Будет ли это работать в более старых версиях Excel (xls)?* | Сохраните с `SaveFormat.XLS` вместо `XLSX`, но имейте в виду, что некоторые новые функции (например, ListObject) могут быть ограничены. |

**Совет:** Всегда вызывайте `workbook.save(..., SaveFormat.XLSX)` после завершения всех изменений таблицы. Многократное сохранение может ненужно увеличить размер файла.

---

## Следующие шаги

Теперь, когда вы знаете, как **создать таблицу Excel**, **определять диапазон ячеек**, **отключать автофильтр** и **сохранять книгу в формате xlsx**, вы можете расширить решение:

* **Добавить формулы** в вычисляемые столбцы с помощью `table.getListColumns().get(i).setFormula("=SUM(...)")`.  
* **Применить условное форматирование** для выделения строк, соответствующих определённым критериям.  
* **Экспортировать книгу в PDF** с помощью `workbook.save("Table.pdf", SaveFormat.PDF)` для целей отчётности.  

Каждая из этих тем опирается на основные концепции, рассмотренные в этом учебнике, и дополнительно демонстрирует, как **disable autofilter in excel** при необходимости.

---

## Заключение

Теперь у вас есть полный, готовый к использованию пример, показывающий, как **создать таблицу Excel** в Java, **определять диапазон ячеек**, **отключать автофильтр** и **сохранять книгу в формате xlsx**. Следуя пошаговому коду и объяснениям, вы сможете интегрировать создание таблиц Excel в любое Java‑приложение и программно управлять поведением AutoFilter. Приятного кодирования!

## Что стоит изучить дальше?

Следующие учебники охватывают тесно связанные темы, которые развивают техники, продемонстрированные в этом руководстве. Каждый ресурс включает полные рабочие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в своих проектах.

- [Как создать и сохранить книгу Excel в формате SVG с помощью Aspose.Cells for Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)
- [Создать и сохранить книгу Excel Aspose Cells Java](/cells/hindi/java/workbook-operations/create-save-excel-workbook-aspose-cells-java/)
- [Создать и сохранить книгу Excel Aspose Cells Java](/cells/german/java/workbook-operations/create-save-excel-workbook-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}