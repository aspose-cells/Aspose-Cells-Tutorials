---
category: general
date: 2026-08-14
description: Как установить разделитель и сохранить в CSV с помощью Aspose.Cells,
  ограничить количество цифр, экспортировать строки CSV и пересчитать формулы в Java.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to set delimiter
- save as csv
- recalculate formulas
- how to export csv
- how to limit digits
language: ru
lastmod: 2026-08-14
og_description: Как установить разделитель и сохранить как CSV с помощью Aspose.Cells,
  ограничить количество цифр, экспортировать строки CSV и пересчитывать формулы в
  Java.
og_image_alt: Screenshot of Java code that sets a CSV delimiter and saves an Excel
  workbook as CSV using Aspose.Cells
og_title: Как установить разделитель и сохранить как CSV – руководство Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: How to set delimiter and save as CSV using Aspose.Cells, limit digits,
    export CSV strings, and recalculate formulas in Java.
  headline: How to set delimiter and save as CSV with Aspose.Cells
  type: TechArticle
- description: How to set delimiter and save as CSV using Aspose.Cells, limit digits,
    export CSV strings, and recalculate formulas in Java.
  name: How to set delimiter and save as CSV with Aspose.Cells
  steps:
  - name: Why this works
    text: "- `CsvSaveOptions.setDelimiter(char)` tells Aspose.Cells which character
      separates fields. By default it’s a comma, but any character (tab `'\t'`, pipe
      `'|'`, etc.) works. - `setSignificantDigits(int)` limits numeric precision,
      satisfying the **how to limit digits** requirement without manually form"
  - name: When to use this
    text: '- Returning CSV from a REST endpoint (`@RestController` in Spring) - Embedding
      CSV data into an email attachment without writing to disk - Performing quick
      sanity checks during unit tests'
  - name: Why recalculate?
    text: '- Formulas may reference external data or volatile functions (`NOW()`,
      `RAND()`) that need fresh values. - Dynamic‑array formulas (e.g., `=SORT(A1:A10)`)
      are evaluated automatically, but calling `calculateFormula()` guarantees consistency
      across all sheets.'
  - name: Verifying the result
    text: 1. Open `output.csv` in a text editor – you should see a semicolon (`;`)
      separating each column. 2. Confirm that numeric columns display at most five
      significant digits. 3. The console output will print the CSV string generated
      in step 4. 4. Open `japan_updated.xlsx` in Excel – any formulas that pre
  type: HowTo
tags:
- Aspose.Cells
- Java
- CSV export
- Excel automation
title: Как установить разделитель и сохранить в CSV с помощью Aspose.Cells
url: /ru/java/excel-import-export/how-to-set-delimiter-and-save-as-csv-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как установить разделитель и сохранить как CSV с Aspose.Cells

Если вам нужно **how to set delimiter** при экспорте данных из книги Excel, это руководство покажет полное решение от начала до конца с использованием Aspose.Cells for Java. Вы узнаете, как настроить разделитель CSV, ограничить количество значимых цифр, экспортировать строку CSV и обновить формулы динамического массива после загрузки книги.

В руководстве описано всё, что необходимо для запуска кода на вашем компьютере, включая работу со специальными календарями, такими как правление японского императора. По завершении вы сможете генерировать точные CSV‑файлы, контролировать числовую точность и обеспечивать актуальность формул.

## Предварительные требования

- Java 17 или новее (код также компилируется с JDK 11+)
- Aspose.Cells for Java 23.9 или новее – загрузите с [Aspose website](https://products.aspose.com/cells/java/)
- Базовые знания Maven или Gradle для управления зависимостями
- IDE (IntelliJ IDEA, Eclipse, VS Code) или простой текстовый редактор и командная строка

> **Pro tip:** Используйте отдельную папку `libs` или Maven Central, чтобы держать JAR‑файл Aspose.Cells в classpath. Приведённые ниже примеры предполагают Maven‑проект.

## Шаг 1: Настройка Maven‑проекта

Создайте `pom.xml` с зависимостью Aspose.Cells:

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0" 
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 
                             http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.example</groupId>
    <artifactId>aspose-csv-demo</artifactId>
    <version>1.0.0</version>
    <properties>
        <maven.compiler.source>17</maven.compiler.source>
        <maven.compiler.target>17</maven.compiler.target>
    </properties>

    <dependencies>
        <dependency>
            <groupId>com.aspose</groupId>
            <artifactId>aspose-cells</artifactId>
            <version>23.9</version>
            <classifier>jdk17</classifier>
        </dependency>
    </dependencies>
</project>
```

Запустите `mvn clean compile`, чтобы загрузить библиотеку и убедиться, что сборка прошла успешно.

## Шаг 2: Как установить разделитель и сохранить как CSV

Основная цель — изменить разделитель по умолчанию (запятая) на пользовательский символ (например, точка с запятой) при сохранении книги Excel в CSV. Aspose.Cells предоставляет `CsvSaveOptions` для этой задачи.

```java
package com.example;

import com.aspose.cells.*;

public class CsvDelimiterDemo {
    public static void main(String[] args) throws Exception {
        // Load an existing workbook (replace the path with your file)
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Configure CSV save options
        CsvSaveOptions csvOptions = new CsvSaveOptions();
        // Primary requirement: set a custom delimiter
        csvOptions.setDelimiter(';');               // <-- how to set delimiter
        // Optional: limit the number of significant digits
        csvOptions.setSignificantDigits(5);         // <-- how to limit digits

        // Save the workbook as CSV using the configured options
        workbook.save("YOUR_DIRECTORY/output.csv", csvOptions);

        System.out.println("CSV file saved with ';' delimiter and 5‑digit precision.");
    }
}
```

### Почему это работает

- `CsvSaveOptions.setDelimiter(char)` указывает Aspose.Cells, какой символ разделяет поля. По умолчанию это запятая, но работает любой символ (табуляция `'\t'`, вертикальная черта `'|'` и т.д.).
- `setSignificantDigits(int)` ограничивает числовую точность, удовлетворяя требованию **how to limit digits** без ручного форматирования каждой ячейки.

#### Ожидаемый вывод

Файл `output.csv` будет содержать строки, подобные:

```
Name;Amount;Date
Alice;123.46;2024-01-15
Bob;78.90;2024-01-16
```

Обратите внимание, что числа округляются до пяти значимых цифр (например, `123.45678` → `123.46`).

## Шаг 3: Как ограничить количество цифр при сохранении CSV

Если требуется более строгий контроль над числовым форматированием, вы также можете использовать экземпляр `CsvSaveOptions` для указания пользовательской строки формата числа.

```java
CsvSaveOptions csvOptions = new CsvSaveOptions();
csvOptions.setDelimiter(',');                // standard comma delimiter
csvOptions.setNumberFormat("0.####");        // up to 4 decimal places
csvOptions.setSignificantDigits(6);          // overall significant digits
```

- `setNumberFormat` использует шаблоны в стиле .NET, которые поддерживает Aspose.Cells.
- Комбинация `setNumberFormat` и `setSignificantDigits` обеспечивает предсказуемое округление в разных локалях.

## Шаг 4: Как экспортировать CSV как строку с пользовательским разделителем

Иногда вам не нужен физический файл; нужны данные CSV в памяти (например, для отправки в HTTP‑ответе). Класс `ExportTableOptions` позволяет экспортировать диапазон в виде строки.

```java
// Export a range (rows 0‑9, columns 0‑4) as a CSV string
ExportTableOptions exportOptions = new ExportTableOptions();
exportOptions.setExportAsString(true);   // return a string instead of a file
exportOptions.setDelimiter(',');         // <-- how to set delimiter for export
exportOptions.setIncludeColumnNames(true);

String csvData = workbook.getWorksheets()
                         .get(0)                     // first worksheet
                         .getCells()
                         .exportDataTableAsString(0, 0, 10, 5, exportOptions);

System.out.println("Exported CSV string:");
System.out.println(csvData);
```

### Когда использовать это

- Возврат CSV из REST‑endpoint'а (`@RestController` в Spring)
- Встраивание данных CSV в вложение письма без записи на диск
- Быстрая проверка корректности во время модульных тестов

## Шаг 5: Как пересчитать формулы после загрузки книги

Если ваша книга содержит формулы — особенно **dynamic‑array formulas**, появившиеся в последних версиях Excel, их необходимо пересчитать после загрузки файла. Aspose.Cells автоматически обновляет результаты динамических массивов, но для обычных формул всё равно нужно вызвать `calculateFormula()`.

```java
// Load a workbook that uses the Japanese Emperor calendar (optional step)
LoadOptions loadOptions = new LoadOptions();
loadOptions.setCalendar(CalendarType.JAPANESE_EMPEROR_REIGN);
Workbook japaneseWorkbook = new Workbook("YOUR_DIRECTORY/japan.xlsx", loadOptions);

// Recalculate all formulas in the workbook
japaneseWorkbook.calculateFormula();   // <-- recalculate formulas

// Save the refreshed workbook (preserves the original calendar)
japaneseWorkbook.save("YOUR_DIRECTORY/japan_updated.xlsx");
System.out.println("Formulas recalculated and workbook saved.");
```

### Почему пересчитывать?

- Формулы могут ссылаться на внешние данные или использовать волатильные функции (`NOW()`, `RAND()`), которым требуются актуальные значения.
- Формулы динамических массивов (например, `=SORT(A1:A10)`) вычисляются автоматически, но вызов `calculateFormula()` гарантирует согласованность на всех листах.

## Шаг 6: Полный пример от начала до конца

Ниже представлен один класс, демонстрирующий **how to set delimiter**, **save as CSV**, **limit digits**, **export a CSV string**, **load a workbook with a special calendar**, и **recalculate formulas**. Код готов к копированию и вставке в ваш проект.

```java
package com.example;

import com.aspose.cells.*;

public class AsposeCsvFullDemo {
    public static void main(String[] args) throws Exception {
        // -----------------------------------------------------------------
        // 1. Load an existing workbook
        // -----------------------------------------------------------------
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // -----------------------------------------------------------------
        // 2. Configure CSV save options (delimiter + digit limit)
        // -----------------------------------------------------------------
        CsvSaveOptions csvOptions = new CsvSaveOptions();
        csvOptions.setDelimiter(';');          // <-- how to set delimiter
        csvOptions.setSignificantDigits(5);    // <-- how to limit digits

        // -----------------------------------------------------------------
        // 3. Save the workbook as CSV
        // -----------------------------------------------------------------
        workbook.save("YOUR_DIRECTORY/output.csv", csvOptions);
        System.out.println("Saved CSV with ';' delimiter.");

        // -----------------------------------------------------------------
        // 4. Export a range as a CSV string (custom delimiter)
        // -----------------------------------------------------------------
        ExportTableOptions exportOptions = new ExportTableOptions();
        exportOptions.setExportAsString(true);
        exportOptions.setDelimiter(',');       // <-- how to set delimiter for export
        exportOptions.setIncludeColumnNames(true);

        String csvString = workbook.getWorksheets()
                                   .get(0)
                                   .getCells()
                                   .exportDataTableAsString(0, 0, 10, 5, exportOptions);
        System.out.println("CSV string exported:");
        System.out.println(csvString);

        // -----------------------------------------------------------------
        // 5. Load a workbook that uses the Japanese Emperor calendar
        // -----------------------------------------------------------------
        LoadOptions loadOptions = new LoadOptions();
        loadOptions.setCalendar(CalendarType.JAPANESE_EMPEROR_REIGN);
        Workbook japaneseWorkbook = new Workbook("YOUR_DIRECTORY/japan.xlsx", loadOptions);

        // -----------------------------------------------------------------
        // 6. Recalculate formulas (including dynamic‑array formulas)
        // -----------------------------------------------------------------
        japaneseWorkbook.calculateFormula();   // <-- recalculate formulas

        // -----------------------------------------------------------------
        // 7. Save the refreshed workbook
        // -----------------------------------------------------------------
        japaneseWorkbook.save("YOUR_DIRECTORY/japan_updated.xlsx");
        System.out.println("Japanese workbook refreshed and saved.");
    }
}
```

### Проверка результата

1. Откройте `output.csv` в текстовом редакторе — вы должны увидеть точку с запятой (`;`), разделяющую каждый столбец.
2. Убедитесь, что числовые столбцы отображают не более пяти значимых цифр.
3. Вывод в консоль покажет строку CSV, сгенерированную на шаге 4.
4. Откройте `japan_updated.xlsx` в Excel — любые формулы, ранее показывавшие `#REF!` или устаревшие значения, теперь отобразятся корректно.

## Распространённые подводные камни и как их избежать

| Issue | Cause | Fix |
|-------|-------|-----|
| CSV показывает лишние кавычки | Ячейки содержат запятые, тогда как разделитель тоже запятая | Используйте другой разделитель (`;` или `\t`) через `setDelimiter` |
| Числа округляются неправильно | `setSignificantDigits` применяется после пользовательского формата числа | Примените `setNumberFormat` **до** `setSignificantDigits` |

## Что изучать дальше?

Следующие руководства охватывают тесно связанные темы, основанные на техниках, продемонстрированных в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в своих проектах.

- [Как загрузить и сохранить Excel как CSV с использованием Aspose.Cells для Java: Полное руководство](/cells/english/java/workbook-operations/aspose-cells-java-load-save-excel-csv/)
- [Как загрузить CSV‑файл с использованием Aspose.Cells для Java: Полное руководство](/cells/english/java/workbook-operations/load-csv-aspose-cells-java-tutorial/)
- [Как загружать CSV‑файлы с помощью пользовательских парсеров в Java с Aspose.Cells](/cells/english/java/import-export/load-csv-files-custom-parsers-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}