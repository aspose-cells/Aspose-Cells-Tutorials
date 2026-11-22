---
category: general
date: 2026-11-22
description: Узнайте, как использовать пользовательский числовой формат для оформления
  столбца как валюты в Excel с помощью Java. Быстро задайте числовой формат Excel
  с помощью простого стиля.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- custom number format
- format column as currency
- set excel number format
- set currency format
- style first column
language: ru
lastmod: 2026-11-22
og_description: Примените пользовательский числовой формат в Excel с помощью Java.
  Этот учебник показывает, как задать числовой формат в Excel и оформить первый столбец
  как валюту.
og_image_alt: Java code snippet that applies a custom number format to an Excel column
og_title: Применение пользовательского числового формата в Excel с помощью Java —
  пошаговое руководство
schemas:
- author: Aspose
  dateModified: '2026-11-22'
  description: Learn how to use a custom number format to format a column as currency
    in Excel using Java. Set Excel number format quickly with a simple style.
  headline: How to apply a custom number format in Excel with Java
  type: TechArticle
tags:
- Java
- Excel
- Apache POI
- Spreadsheet Automation
title: Как применить пользовательский числовой формат в Excel с помощью Java
url: /ru/java/formatting/how-to-apply-a-custom-number-format-in-excel-with-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как применить пользовательский числовой формат в Excel с помощью Java

Если вам нужно **пользовательски отформатировать** столбец в листе Excel, это руководство покажет, как сделать это с помощью Java. Независимо от того, создаёте ли вы финансовые отчёты или экспортируете бухгалтерские данные, форматирование первого столбца как валюты делает вывод сразу читаемым.

В примере ниже мы **отформатируем столбец как валюту**, применим стиль к первому столбцу, а затем импортируем `DataTable` в лист. Такой же подход работает для любого числового формата, который вы хотите отобразить.

## Что вы узнаете

* Как создать **пользовательский числовой формат** с помощью объекта `Style` из Apache POI.  
* Как **установить числовой формат Excel** для конкретного столбца, включая случай **установки валютного формата**.  
* Как **оформить первый столбец** при импорте `DataTable`.  
* Как сохранить книгу и проверить, что форматирование отображается корректно.

### Предварительные требования

* Java 17 или новее.  
* Apache POI 5.x (библиотека, предоставляющая `Workbook`, `Worksheet` и `Style`).  
* Реализация `DataTable`, которую можно итерировать, как в примере кода.  
* Базовое знакомство с Java и концепциями Excel.

---

## Шаг 1: Настройка проекта и импорт данных

Сначала добавьте Apache POI в ваш проект. Если вы используете Maven, включите следующую зависимость:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>org.apache.poi</groupId>
    <artifactId>poi-ooxml</artifactId>
    <version>5.2.3</version>
</dependency>
```

Затем получите исходные данные в виде `DataTable`. В реальном сценарии они могут поступать из запроса к базе данных, CSV‑файла или ответа API.

```java
// Step 1: Obtain the source data as a DataTable
DataTable dataTable = getData();   // replace with your own data‑fetching logic
```

> **Pro tip:** Убедитесь, что столбцы `DataTable` имеют правильные типы Java (`Integer`, `Double` и т.д.), потому что числовой формат влияет только на числовые ячейки.

---

## Шаг 2: Создание **пользовательского числового формата** для первого столбца

**Пользовательский числовой формат** указывает Excel, как отображать числовые значения. Чтобы показывать значения как валюту, мы используем встроенный формат `CURRENCY`, но также можно задать шаблоны, например `"$#,##0.00"`.

```java
// Step 2: Prepare a Style array – one entry per column in the DataTable
Style[] columnStyles = new Style[dataTable.getColumns().size()];

// Step 3: Create a style for the first column and set it to display values as currency
// wb – existing Workbook instance (e.g., XSSFWorkbook for .xlsx files)
Workbook wb = new XSSFWorkbook();
columnStyles[0] = wb.createCellStyle();               // style first column
columnStyles[0].setDataFormat(
        wb.createDataFormat().getFormat(Style.CustomNumberFormat.CURRENCY));
```

**Почему это работает:**  
* `createCellStyle()` возвращает переиспользуемый объект стиля.  
* `setDataFormat()` присваивает **установленный валютный формат** стилю, после чего Excel применяет его ко всем ячейкам, использующим этот стиль.  
* Сохраняя стиль в `columnStyles[0]`, мы гарантируем, что только первый столбец получит валютное форматирование.

---

## Шаг 3: Импорт `DataTable` с применением стилей столбцов

Теперь импортируем данные в лист. Метод `importDataTable` принимает массив стилей, позволяя нам **оформить первый столбец** и оставить остальные столбцы с форматированием по умолчанию.

```java
// Step 4: Import the DataTable into the worksheet, applying the column styles
// ws – existing Worksheet instance
Worksheet ws = wb.createSheet("Report");

// true  → import column headers
// 0,0   → start at cell A1
ws.getCells().importDataTable(dataTable, true, 0, 0, columnStyles);
```

Вызов выше **устанавливает числовой формат Excel** только для первого столбца. Все остальные столбцы наследуют стиль книги по умолчанию, что упрощает и ускоряет код.

---

## Шаг 4: Сохранение книги и проверка результата

Наконец, запишите книгу в файл и откройте её в Excel, чтобы убедиться, что первый столбец отображает валютные символы.

```java
// Step 5: Save the workbook to disk
try (FileOutputStream fileOut = new FileOutputStream("FormattedReport.xlsx")) {
    wb.write(fileOut);
}
System.out.println("Workbook saved as FormattedReport.xlsx");
```

**Ожидаемый результат:**  
При открытии *FormattedReport.xlsx* значения в столбце A отображаются с соответствующим валютным символом (например, `$1,234.00`). Все остальные столбцы сохраняют своё исходное числовое представление.

---

## Общие варианты и граничные случаи

| Ситуация | Корректировка |
|-----------|------------|
| **Другая валюта** (например, евро) | Замените `Style.CustomNumberFormat.CURRENCY` на пользовательский шаблон: <br>`wb.createDataFormat().getFormat("\"€\"#,##0.00")` |
| **Более одного стилизованного столбца** | Заполните дополнительные элементы в `columnStyles[]` собственными объектами `CellStyle`. |
| **Большие наборы данных** | Используйте `importDataTable` пакетами или потоково обрабатывайте строки, чтобы избежать `OutOfMemoryError`. |
| **Разделители, зависящие от локали** | Используйте `java.text.NumberFormat` для генерации шаблона, учитывающего локаль, и передайте его в `setDataFormat`. |

> **Осторожно:** Повторное использование одного объекта `CellStyle` в нескольких столбцах может привести к неожиданному форматированию, поскольку Excel ограничивает количество различных стилей в книге. Создавайте отдельный стиль для каждого уникального формата, который вам нужен.

---

## Полный исполняемый пример

Ниже приведена автономная программа, демонстрирующая весь процесс от создания данных до сохранения отформатированной книги.

```java
import java.io.FileOutputStream;
import java.util.ArrayList;
import java.util.List;

import org.apache.poi.ss.usermodel.*;
import org.apache.poi.xssf.usermodel.XSSFWorkbook;

/* Mock DataTable implementation for demonstration purposes */
class DataTable {
    private final List<String> columns = List.of("Amount", "Description");
    private final List<Object[]> rows = new ArrayList<>();

    public DataTable() {
        rows.add(new Object[]{1234.5, "Consulting"});
        rows.add(new Object[]{5678.9, "Licensing"});
    }

    public List<String> getColumns() { return columns; }
    public List<Object[]> getRows() { return rows; }
}

/* Helper that mimics the importDataTable method used in the original snippet */
class WorksheetHelper {
    private final Sheet sheet;
    private final Workbook wb;

    public WorksheetHelper(Workbook wb, Sheet sheet) {
        this.wb = wb;
        this.sheet = sheet;
    }

    public void importDataTable(DataTable dt, boolean includeHeaders,
                                int startRow, int startCol, Style[] styles) {
        int rowIdx = startRow;
        if (includeHeaders) {
            Row header = sheet.createRow(rowIdx++);
            for (int c = 0; c < dt.getColumns().size(); c++) {
                Cell cell = header.createCell(startCol + c);
                cell.setCellValue(dt.getColumns().get(c));
            }
        }
        for (Object[] rowData : dt.getRows()) {
            Row row = sheet.createRow(rowIdx++);
            for (int c = 0; c < rowData.length; c++) {
                Cell cell = row.createCell(startCol + c);
                Object value = rowData[c];
                if (value instanceof Number) {
                    cell.setCellValue(((Number) value).doubleValue());
                } else {
                    cell.setCellValue(value.toString());
                }
                // Apply custom style if provided
                if (styles != null && c < styles.length && styles[c] != null) {
                    cell.setCellStyle((CellStyle) styles[c]);
                }
            }
        }
    }
}

/* Main class that puts everything together */
public class CustomNumberFormatDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Obtain the source data
        DataTable dataTable = new DataTable();

        // 2️⃣ Create a workbook and a sheet
        Workbook wb = new XSSFWorkbook();
        Sheet ws = wb.createSheet("Report");

        // 3️⃣ Prepare a style array – one entry per column
        Style[] columnStyles = new Style[dataTable.getColumns().size()];

        // 4️⃣ Create a style for the first column (currency)
        CellStyle currencyStyle = wb.createCellStyle();
        DataFormat fmt = wb.createDataFormat();
        currencyStyle.setDataFormat(fmt.getFormat("$#,##0.00"));
        columnStyles[0] = currencyStyle;   // style first column

        // 5️⃣ Import the DataTable, applying the column styles
        WorksheetHelper helper = new WorksheetHelper(wb, ws);
        helper.importDataTable(dataTable, true, 0, 0, columnStyles);

        // 6️⃣ Save the workbook
        try (FileOutputStream out = new FileOutputStream("FormattedReport.xlsx")) {
            wb.write(out);
        }
        System.out.println("Workbook written to FormattedReport.xlsx");
    }
}
```

Запуск программы создаёт **FormattedReport.xlsx**, где столбец A (столбец «Amount») отображается с **пользовательским числовым форматом**, показывающим знак доллара и два знака после запятой.

---

## Заключение

Теперь вы знаете, как **пользовательски отформатировать** лист Excel из Java, **отформатировать столбец как валюту** и **оформить первый столбец** при импорте данных. Создавая переиспользуемый `CellStyle` и передавая его в `importDataTable`, вы можете **установить числовой формат Excel** для любого столбца без необходимости проходить по каждой ячейке вручную.

Далее попробуйте:

* Использовать `setDataFormat` с шаблонами, зависящими от локали, чтобы **установить валютный формат**


## Что следует изучить дальше?

Следующие руководства охватывают тесно связанные темы, построенные на техниках, продемонстрированных в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, помогающими освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [Установить числовой формат в Excel на Java – Полное руководство](/cells/english/java/formatting/set-number-format-excel-in-java-complete-guide/)
- [Применить числовой формат в Excel на Java – Полное руководство Aspose.Cells](/cells/english/java/formatting/apply-number-format-excel-in-java-complete-aspose-cells-guid/)
- [Как создать книгу Excel с валютным форматом и жирным шрифтом в Java](/cells/english/java/formatting/how-to-create-excel-workbook-with-currency-format-and-bold-f/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}