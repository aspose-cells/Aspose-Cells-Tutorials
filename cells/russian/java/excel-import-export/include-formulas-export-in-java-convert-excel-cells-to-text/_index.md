---
category: general
date: 2026-07-03
description: Включите экспорт формул в Java для преобразования ячеек Excel в текст
  с помощью Aspose.Cells. Узнайте, как эффективно вывести диапазон Excel и получить
  строковые значения ячеек.
draft: false
keywords:
- include formulas export
- convert excel cells text
- print excel range
- export table options
- get cell values string
language: ru
og_description: Включите экспорт формул в Java для преобразования ячеек Excel в текст.
  Пошаговое руководство, показывающее, как вывести диапазон Excel и получить значения
  ячеек в виде строки.
og_title: Включить экспорт формул в Java – преобразовать ячейки Excel в текст
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Include formulas export in Java to convert Excel cells to text using
    Aspose.Cells. Learn how to print Excel range and get cell values string efficiently.
  headline: Include Formulas Export in Java – Convert Excel Cells to Text
  type: TechArticle
- description: Include formulas export in Java to convert Excel cells to text using
    Aspose.Cells. Learn how to print Excel range and get cell values string efficiently.
  name: Include Formulas Export in Java – Convert Excel Cells to Text
  steps:
  - name: Prerequisites
    text: '- Java 17 or newer (the code compiles with older versions but we’ll stick
      to the latest LTS). - Aspose.Cells for Java 23.10 (or any recent release)—you
      can grab it from Maven Central. - A sample `input.xlsx` placed in a folder you
      control (the path is hard‑coded in the example for clarity).'
  - name: Optional Tweaks
    text: '- `eto.setExportHiddenRows(true);` – include rows hidden in Excel. - `eto.setExportHiddenColumns(true);`
      – same for columns. - `eto.setExportAsHTML(true);` – get HTML instead of plain
      text.'
  - name: Expected Output (sample)
    text: '``` =SUM(A2:A3) 42 Hello =IF(B1>10,"Yes","No") =AVERAGE(C1:C3) =VLOOKUP(A1,Sheet2!A:B,2,FALSE)
      ```'
  - name: What if the range contains merged cells?
    text: Merged cells are treated as the value of the top‑left cell. The rest of
      the merged area will appear as empty strings. If you need the merged region’s
      address, query `Cell.getMergedRange()` before export.
  - name: Can I export a massive sheet (hundreds of thousands of rows)?
    text: Yes, but beware of memory consumption. Use `Workbook.getSettings().setMemorySetting(MemorySetting.MEMORY_PREFERENCE)`
      to let Aspose.Cells stream data to disk. Also, consider exporting in chunks
      (e.g., 10 000 rows at a time) to keep the string manageable.
  - name: How do I change the column delimiter?
    text: '`ExportTableOptions` exposes `setSeparator(char separator)`. For CSV‑style
      output, set it to `'',''`:'
  - name: Do formulas respect external references?
    text: If a formula points to another workbook, Aspose.Cells will keep the reference
      text (`='[Other.xlsx]Sheet1'!A1`). It won’t evaluate the external value unless
      you load that workbook as well.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel
- Export
title: Включить экспорт формул в Java — преобразовать ячейки Excel в текст
url: /ru/java/excel-import-export/include-formulas-export-in-java-convert-excel-cells-to-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Включение экспорта формул в Java – Преобразование ячеек Excel в текст

Когда‑нибудь вам нужно было **включить экспорт формул** при извлечении данных из рабочей книги Excel? Возможно, вы создаёте сервис отчетности, который должен сохранять оригинальные формулы, одновременно предоставляя аккуратный текстовый блок. В этом случае вы попали по адресу. В этом руководстве мы покажем, как преобразовать ячейки Excel в обычный текст — *включая* любые встроенные формулы — с помощью Aspose.Cells for Java.

Мы также коснёмся того, как **распечатать диапазон Excel**, настроить **параметры экспорта таблицы**, и, наконец, **получить строку значений ячеек**, которую можно записать в журнал, отправить через API или сохранить в базе данных. К концу вы получите полностью исполняемый фрагмент кода и чёткое понимание причин каждого вызова.

## Что вы получите

- Полностью готовая к копированию и вставке Java‑программа, которая читает файл `.xlsx`, выбирает диапазон и экспортирует его в виде отформатированной строки.
- Понимание класса `ExportTableOptions` и того, почему важно переключать `setExportAsString` и `setIncludeFormula`.
- Советы по работе с большими листами, обработке различных типов данных и настройке формата вывода.
- Краткий чек‑лист распространённых подводных камней (слияние ячеек, скрытые строки и локаль‑специфичные форматы чисел).

### Предварительные требования

- Java 17 или новее (код компилируется и в более старых версиях, но мы будем использовать последнюю LTS).
- Aspose.Cells for Java 23.10 (или любой более новый релиз) — можно получить из Maven Central.
- Пример файла `input.xlsx`, размещённый в папке, к которой у вас есть доступ (путь захардкожен в примере для наглядности).

Если всё готово, давайте приступим.

## Шаг 1: Настройка проекта и добавление зависимостей

Сначала создайте Maven‑проект (или Gradle, если предпочитаете). Добавьте зависимость Aspose.Cells в ваш `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
    <classifier>jdk17</classifier>
</dependency>
```

> **Совет:** Если вы используете корпоративный прокси, убедитесь, что репозиторий доступен; иначе сборка завершится ошибкой «Could not resolve dependencies».

После того как Maven завершит загрузку, вы готовы писать Java‑код.

## Шаг 2: Загрузка рабочей книги и получение нужного листа

Первая строка примера кода показывает, как открыть существующую рабочую книгу:

```java
// Step 1: Load the workbook
Workbook wb = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

Замените `YOUR_DIRECTORY` на абсолютный или относительный путь к вашему файлу. Конструктор `Workbook` автоматически определяет формат файла (XLS, XLSX, CSV и т.д.), поэтому указывать его не требуется.

Далее получаем первый лист:

```java
// Step 2: Get the first worksheet
Worksheet ws = wb.getWorksheets().get(0);
```

Почему первый лист? Во многих шаблонах данные находятся на первой вкладке, но вы можете передать любой индекс или даже использовать `get("SheetName")`, если предпочитаете именованный подход.

## Шаг 3: Определение диапазона для экспорта

Теперь наступает основная часть операции **convert excel cells text**. Вы указываете Aspose.Cells, какие ячейки извлекать, создавая объект `Range`:

```java
// Step 3: Create a range covering cells A1 to C3
Range rng = ws.getCells().createRange("A1:C3");
```

Строка `"A1:C3"` — классический адрес в стиле A1. Его также можно построить программно:

```java
int firstRow = 0, firstCol = 0, totalRows = 3, totalCols = 3;
Range rng = ws.getCells().createRange(firstRow, firstCol, totalRows, totalCols);
```

Эта гибкость полезна, когда размер диапазона динамический — например, вы определяете последнюю использованную строку с помощью `ws.getCells().getMaxDataRow()`.

## Шаг 4: Настройка Export Table Options для включения формул

Здесь и происходит магия **include formulas export**. По умолчанию Aspose.Cells возвращает *отображаемые* значения. Если ячейка содержит `=SUM(A1:A3)`, вы получите вычисленное число, а не текст формулы. Чтобы изменить это, настройте `ExportTableOptions`:

```java
// Step 4: Set up export options to return the range as a string and include formulas
ExportTableOptions eto = new ExportTableOptions();
eto.setExportAsString(true);      // Forces the result to be a single string
eto.setIncludeFormula(true);      // Includes the underlying formula instead of the evaluated value
```

Зачем оба флага? `setExportAsString(true)` указывает API объединять ячейки, используя разделитель по умолчанию (табуляция для столбцов, перевод строки для строк). `setIncludeFormula(true)` переключает источник значения с «отображаемого значения» на «сырую формулу». Если нужны только значения, оставьте `false`.

### Дополнительные настройки

- `eto.setExportHiddenRows(true);` – включить строки, скрытые в Excel.  
- `eto.setExportHiddenColumns(true);` – то же для столбцов.  
- `eto.setExportAsHTML(true);` – получить HTML вместо обычного текста.

Не стесняйтесь экспериментировать; класс параметров — это игровая площадка **export table options**.

## Шаг 5: Получение диапазона в виде отформатированной строки

Теперь извлекаем данные:

```java
// Step 5: Retrieve the range values as a formatted string using the options
String txt = rng.getValueAsString(eto);
```

Возвращённый `txt` выглядит примерно так (при условии, что A1:C3 содержит смесь значений и формул):

```
=SUM(A2:A3)	42	"Hello"
=IF(B1>10,"Yes","No")	=AVERAGE(C1:C3)	=VLOOKUP(A1,Sheet2!A:B,2,FALSE)
```

Обратите внимание, что табуляция (`\t`) разделяет столбцы, а перевод строки (`\n`) — строки. При необходимости вы можете разбить строку позже, получив двумерный массив:

```java
String[] rows = txt.split("\n");
for (String row : rows) {
    String[] cells = row.split("\t");
    // Process each cell...
}
```

## Шаг 6: Вывод результата — простое «Print Excel Range»

Наконец, выводим строку в консоль:

```java
// Step 6: Print the resulting string
System.out.println(txt);
```

Запуск программы выводит точно такой же результат, как показано выше. Далее вы можете записать строку в файл журнала, отправить её по HTTP или сохранить в документ NoSQL.

## Полный готовый к запуску пример

Объединив всё вместе, представляем полный код программы. Скопируйте, вставьте и нажмите **Run** — все импорты включены.

```java
import com.aspose.cells.*;

public class ExportFormulaRange {
    public static void main(String[] args) throws Exception {
        // Load the workbook
        Workbook wb = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Grab the first worksheet
        Worksheet ws = wb.getWorksheets().get(0);

        // Define the range A1:C3 (adjust as needed)
        Range rng = ws.getCells().createRange("A1:C3");

        // Configure export options: string output + include formulas
        ExportTableOptions eto = new ExportTableOptions();
        eto.setExportAsString(true);
        eto.setIncludeFormula(true);

        // Get the string representation of the range
        String txt = rng.getValueAsString(eto);

        // Print the resulting text
        System.out.println(txt);
    }
}
```

### Ожидаемый вывод (пример)

```
=SUM(A2:A3)	42	Hello
=IF(B1>10,"Yes","No")	=AVERAGE(C1:C3)	=VLOOKUP(A1,Sheet2!A:B,2,FALSE)
```

Если в вашей рабочей книге числа отформатированы как даты, они будут отображаться в формате, специфичном для локали (например, `2026‑07‑03`). Чтобы принудительно использовать ISO‑формат дат, можно настроить `ExportTableOptions` с пользовательским `NumberFormat`.

## Обработка граничных случаев и часто задаваемые вопросы

### Что делать, если диапазон содержит объединённые ячейки?

Объединённые ячейки рассматриваются как значение верхней‑левой ячейки. Остальная часть объединённой области будет отображаться как пустые строки. Если нужен адрес объединённого региона, запросите `Cell.getMergedRange()` перед экспортом.

### Можно ли экспортировать огромный лист (сотни тысяч строк)?

Да, но следует учитывать потребление памяти. Используйте `Workbook.getSettings().setMemorySetting(MemorySetting.MEMORY_PREFERENCE)`, чтобы Aspose.Cells записывал данные на диск. Также рассмотрите экспорт частями (например, по 10 000 строк), чтобы строка оставалась управляемой.

### Как изменить разделитель столбцов?

`ExportTableOptions` предоставляет метод `setSeparator(char separator)`. Для вывода в стиле CSV установите его в `','`:

```java
eto.setSeparator(',');
```

### Учитывают ли формулы внешние ссылки?

Если формула ссылается на другую рабочую книгу, Aspose.Cells сохранит текст ссылки (`='[Other.xlsx]Sheet1'!A1`). Она не будет вычислять внешнее значение, если только вы не загрузите эту рабочую книгу.

## Профессиональные советы для кода, готового к продакшну

- **Кешировать рабочую книгу** если вы читаете её

## Что изучать дальше?

Следующие руководства охватывают тесно связанные темы, построенные на техниках, продемонстрированных в этом руководстве. Каждый ресурс содержит полностью работающие примеры кода с пошаговыми объяснениями, помогающими освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [Как создать и экспортировать Excel в HTML с помощью Aspose.Cells Java | Руководство по операциям с рабочей книгой](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)
- [Как конвертировать Excel в PDF в Java с помощью Aspose.Cells: пошаговое руководство](/cells/english/java/workbook-operations/convert-excel-to-pdf-aspose-cells-java/)
- [Экспорт рабочей книги Excel в виде изображения с помощью Aspose.Cells for Java: пошаговое руководство](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}