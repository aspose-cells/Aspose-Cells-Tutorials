---
category: general
date: 2026-08-20
description: Создайте книгу Excel в Java с использованием Aspose.Cells, установите
  формат валюты, добавьте полужирный шрифт и импортируйте массив стилей для стилизованных
  ячеек.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- set currency format
- format cells currency
- how to import style
- add bold font
language: ru
lastmod: 2026-08-20
og_description: Создайте книгу Excel на Java, установите формат валюты, добавьте полужирный
  шрифт и узнайте, как импортировать стиль с помощью Aspose.Cells.
og_image_alt: Screenshot of an excel workbook created with currency format and bold
  font using Aspose.Cells
og_title: Создать книгу Excel с оформленными ячейками валюты в Java
schemas:
- author: Aspose
  dateModified: '2026-08-20'
  description: Create excel workbook in Java using Aspose.Cells, set currency format,
    add bold font, and import style array for styled cells.
  headline: How to create excel workbook with currency format and bold font in Java
  type: TechArticle
- description: Create excel workbook in Java using Aspose.Cells, set currency format,
    add bold font, and import style array for styled cells.
  name: How to create excel workbook with currency format and bold font in Java
  steps:
  - name: Initialise the workbook and worksheet
    text: Creating a fresh workbook gives you a clean container for all subsequent
      formatting.
  - name: Build a DataTable with numeric data
    text: A `DataTable` mimics a database table, making it easy to import rows in
      bulk.
  - name: Define a style – currency format and bold font
    text: Here we **set currency format** and **add bold font** to a `Style` object.
  - name: Configure import options to use the style array
    text: Aspose.Cells lets you pass a `Style[]` via `ImportTableOptions`. This is
      the official **how to import style** method.
  - name: Import the DataTable into the worksheet
    text: Now we bring the data into the sheet at cell `A1`, applying the style array
      automatically.
  - name: Save the workbook to disk
    text: Finally, write the in‑memory workbook to a physical file.
  - name: Expected output
    text: 'When you open `DataTableWithStyleArray.xlsx` in Microsoft Excel, you should
      see:'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel
- Formatting
title: Как создать Excel‑книгу с форматом валюты и полужирным шрифтом в Java
url: /ru/java/formatting/how-to-create-excel-workbook-with-currency-format-and-bold-f/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как создать Excel‑книгу с форматом валюты и полужирным шрифтом в Java

Если вам нужно **создать Excel‑книгу** программно, это руководство покажет, как это сделать. Мы пройдемся по созданию книги, применению формата валюты, добавлению полужирного шрифта и использованию функции **how to import style** в Aspose.Cells, чтобы каждая импортированная ячейка выглядела одинаково.

В конце вы получите готовый файл `DataTableWithStyleArray.xlsx`, в котором числа отображаются в долларах и выделены полужирным шрифтом. Ручное форматирование в Excel не требуется.

## Предварительные требования

Прежде чем начать, убедитесь, что у вас есть:

- Java 17 или новее.
- Лицензия Aspose.Cells for Java (или бесплатный оценочный ключ).
- Maven или Gradle для управления зависимостью `aspose-cells`.
- Базовые знания коллекций Java и `DataTable`.

```xml
<!-- Maven dependency -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version>
</dependency>
```

> **Pro tip:** Если вы получаете `LicenseException`, разместите файл лицензии в classpath и вызовите `License license = new License(); license.setLicense("Aspose.Total.Java.lic");` перед созданием книги.

## Как создать Excel‑книгу со стилизованными ячейками валюты

В этом разделе представлены основные шаги. Каждый шаг объясняет **почему** он важен, а не только **что** нужно ввести.

### Шаг 1: Инициализировать книгу и лист

Создание новой книги дает чистый контейнер для всей последующей форматировки.

```java
// Step 1: Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();                     // creates an empty .xlsx file in memory
Worksheet worksheet = workbook.getWorksheets().get(0); // first sheet is index 0
Cells cells = worksheet.getCells();                     // shortcut to work with cells
```

> **Почему:** Объект `Workbook` представляет весь файл Excel. Доступ к первому `Worksheet` позволяет сразу начинать заполнять данные.

### Шаг 2: Сформировать DataTable с числовыми данными

`DataTable` имитирует таблицу базы данных, что упрощает массовый импорт строк.

```java
// Step 2: Build a DataTable with sample numeric data
DataTable dataTable = new DataTable();
dataTable.getColumns().add("Amount", DataType.DOUBLE); // column type DOUBLE ensures numeric handling
dataTable.getRows().add(new Object[]{1234.56});
dataTable.getRows().add(new Object[]{7890.12});
```

> **Почему:** Использование `DOUBLE` гарантирует сохранение десятичных знаков, что необходимо для последующего **format cells currency**.

### Шаг 3: Определить стиль – формат валюты и полужирный шрифт

Здесь мы **устанавливаем формат валюты** и **добавляем полужирный шрифт** в объект `Style`.

```java
// Step 3: Define a style (currency format and bold font) for the imported cells
Style currencyStyle = workbook.createStyle();                // create a reusable style instance
currencyStyle.getNumber().setFormat("$#,##0.00");            // set currency format (e.g., $1,234.56)
currencyStyle.getFont().setBold(true);                      // make the font bold
Style[] styleArray = new Style[] { currencyStyle };          // style array required by ImportTableOptions
```

> **Почему:** Строка формата `Number` `$#,##0.00` сообщает Excel, что ячейка содержит денежное значение, а `setBold(true)` привлекает внимание к числам. Помещение стиля в массив готовит нас к шагу **how to import style**.

### Шаг 4: Настроить параметры импорта для использования массива стилей

Aspose.Cells позволяет передать `Style[]` через `ImportTableOptions`. Это официальный метод **how to import style**.

```java
// Step 4: Set up import options to use the style array
ImportTableOptions importOptions = new ImportTableOptions();
importOptions.setStyleArray(styleArray); // tells the importer to apply our currencyStyle to every column
```

> **Почему:** Без `ImportTableOptions` импортированные ячейки получат стиль по умолчанию, и формат валюты с полужирным шрифтом будет утерян.

### Шаг 5: Импортировать DataTable в лист

Теперь мы переносим данные на лист, начиная с ячейки `A1`, автоматически применяя массив стилей.

```java
// Step 5: Import the DataTable into the worksheet at A1, applying the style
cells.importDataTable(dataTable, true, "A1", importOptions);
```

- `true` указывает, что первая строка `DataTable` содержит заголовки столбцов.
- `"A1"` — верхний‑левый угол, с которого начинается импорт.

> **Почему:** Импорт с массивом стилей гарантирует, что каждая импортированная ячейка получит подготовленный стиль **format cells currency**.

### Шаг 6: Сохранить книгу на диск

Наконец, записываем книгу из памяти в физический файл.

```java
// Step 6: Save the workbook to a file
String outputPath = "YOUR_DIRECTORY/DataTableWithStyleArray.xlsx";
workbook.save(outputPath);
System.out.println("Workbook saved to: " + outputPath);
```

> **Почему:** Сохранение фиксирует форматирование, позволяя вам или последующим процессам открыть файл в Excel с нужным внешним видом.

## Полный исходный код

Ниже приведён полностью готовый к запуску Java‑класс. Скопируйте его в свою IDE, замените `YOUR_DIRECTORY` на существующую папку и выполните.

```java
import com.aspose.cells.*;

public class StyleArrayImportTutorial {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);
        Cells cells = worksheet.getCells();

        // Step 2: Build a DataTable with sample numeric data
        DataTable dataTable = new DataTable();
        dataTable.getColumns().add("Amount", DataType.DOUBLE);
        dataTable.getRows().add(new Object[]{1234.56});
        dataTable.getRows().add(new Object[]{7890.12});

        // Step 3: Define a style (currency format and bold font) for the imported cells
        Style currencyStyle = workbook.createStyle();
        currencyStyle.getNumber().setFormat("$#,##0.00");   // set currency format
        currencyStyle.getFont().setBold(true);             // add bold font
        Style[] styleArray = new Style[] { currencyStyle };

        // Step 4: Set up import options to use the style array
        ImportTableOptions importOptions = new ImportTableOptions();
        importOptions.setStyleArray(styleArray);           // how to import style

        // Step 5: Import the DataTable into the worksheet at A1, applying the style
        cells.importDataTable(dataTable, true, "A1", importOptions);

        // Step 6: Save the workbook to a file
        workbook.save("YOUR_DIRECTORY/DataTableWithStyleArray.xlsx");
        System.out.println("Workbook created successfully.");
    }
}
```

### Ожидаемый результат

При открытии `DataTableWithStyleArray.xlsx` в Microsoft Excel вы увидите:

| Сумма |
|-------|
| **$1,234.56** |
| **$7,890.12** |

- Числа отображаются в **формате валюты** (знак `$`, два знака после запятой).
- Шрифт обеих ячеек **полужирный**, что делает их более заметными.

## Распространённые варианты и граничные случаи

| Сценарий | Что изменить | Причина |
|----------|--------------|---------|
| **Другая валюта** | `currencyStyle.getNumber().setFormat("€#,##0.00");` | Использовать символ евро или любой другой локализованный формат. |
| **Несколько столбцов с разными стилями** | Создать несколько объектов `Style`, заполнить `styleArray` в том же порядке, что и столбцы. | Каждый столбец может иметь собственный числовой формат, шрифт, фон и т.д. |
| **Большие наборы данных** | `cells.importDataTable(dataTable, false, "A1", importOptions);` и установить `importOptions.setImportDataOptions(ImportDataOptions.DATA_ONLY);` | Повышает производительность, пропуская заголовки строк или лишние метаданные. |
| **Применение стиля после импорта** | `cells.get("A2").setStyle(currencyStyle);` для отдельных ячеек. | Полезно, когда только часть строк требует специального форматирования. |

## Советы для продакшн‑использования

- **Лицензировать заранее**: Зарегистрируйте лицензию Aspose.Cells до создания книги, чтобы избежать водяного знака оценки.
- **Потокобезопасность**: Экземпляры `Workbook` **не** являются потокобезопасными. Создавайте отдельный объект на каждый поток, если генерируете много файлов одновременно.
- **Управление памятью**: Для очень больших листов рассматривайте потоковый API `Workbook` (`Workbook` → `WorkbookDesigner`), чтобы снизить потребление памяти.
- **Тестирование**: Добавьте юнит‑тест, который открывает сохранённый файл с помощью Apache POI и проверяет, что формат числа стиля ячейки соответствует `"$#,##0.00"`.

## Заключение

Теперь вы знаете, как **создать Excel‑книгу** в Java, **установить формат валюты**, **добавить полужирный шрифт** и правильно выполнить **how to import style** с помощью `ImportTableOptions` в Aspose.Cells. Это сквозное решение устраняет ручные шаги в Excel и гарантирует, что каждая импортированная ячейка использует одинаковый стиль **format cells currency**.

Готовы к следующему вызову? Попробуйте добавить условное форматирование, встроить диаграммы или экспортировать книгу в PDF — всё это с тем же приёмом массивов стилей. Приятного кодинга!

## Что изучать дальше?

Следующие руководства охватывают тесно связанные темы, расширяющие техники, продемонстрированные в этом руководстве. Каждый ресурс содержит полностью работающие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы в собственных проектах.

- [Create an Excel Workbook using Aspose.Cells in Java: A Step-by-Step Guide](/cells/english/java/getting-started/create-excel-workbook-aspose-cells-java/)
- [How to Create & Format Excel Cells Using Aspose.Cells for Java: A Step-by-Step Guide](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)
- [How to Style Excel Cells and Add Hyperlinks Using Aspose.Cells for Java](/cells/english/java/formatting/style-excel-cells-hyperlinks-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}