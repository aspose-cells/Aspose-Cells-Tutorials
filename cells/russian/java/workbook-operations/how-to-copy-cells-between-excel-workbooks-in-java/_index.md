---
category: general
date: 2026-11-16
description: Как копировать ячейки между рабочими книгами Excel в Java — загрузить
  рабочую книгу, скопировать диапазон между книгами (включая сводную таблицу) и сохранить
  файл рабочей книги.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy cells
- copy range between workbooks
- copy pivot table workbook
- save workbook file
- load excel workbook java
language: ru
lastmod: 2026-11-16
og_description: Как копировать ячейки между книгами Excel в Java. Узнайте, как загрузить
  книгу Excel, скопировать диапазон (включая сводную таблицу) между книгами и сохранить
  файл книги.
og_image_alt: Screenshot of Java code copying a cell range from one Excel workbook
  to another
og_title: Как копировать ячейки между рабочими книгами Excel в Java — полное руководство
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: How to copy cells between Excel workbooks in Java – load a workbook,
    copy range between workbooks (including a pivot table), and save the workbook
    file.
  headline: How to copy cells between Excel workbooks in Java
  type: TechArticle
- description: How to copy cells between Excel workbooks in Java – load a workbook,
    copy range between workbooks (including a pivot table), and save the workbook
    file.
  name: How to copy cells between Excel workbooks in Java
  steps:
  - name: Load the source workbook
    text: '```java import com.aspose.cells.*;'
  - name: Define the range that includes the pivot table
    text: '```java // Define the cell range that you want to copy. // Adjust "A1:G20"
      to match the area that contains your data/pivot table. Range srcRange = srcWs.getCells().createRange("A1:G20");
      ```'
  - name: Create the destination workbook
    text: '```java // Create a new, empty workbook that will receive the copied range.
      Workbook destWb = new Workbook(); // defaults to a single empty sheet Worksheet
      destWs = destWb.getWorksheets().get(0); ```'
  - name: Copy the range to the destination workbook
    text: '```java // Copy the source range to cell A1 of the destination worksheet.
      destWs.getCells().copyRange(srcRange, destWs.getCells().get("A1")); ```'
  - name: Save the destination workbook
    text: '```java // Save the new workbook to disk. destWb.save("YOUR_DIRECTORY/dest.xlsx");
      } } ```'
  type: HowTo
tags:
- Java
- Excel
- Aspose.Cells
- Workbook manipulation
title: Как копировать ячейки между рабочими книгами Excel на Java
url: /ru/java/workbook-operations/how-to-copy-cells-between-excel-workbooks-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как копировать ячейки между рабочими книгами Excel в Java

Если вам нужно **скопировать ячейки** из одной рабочей книги Excel в другую с помощью Java, это руководство покажет надёжный способ сделать это. Вы узнаете, как **загрузить Excel workbook Java**, скопировать диапазон, который может содержать сводную таблицу, и в конце **сохранить файл рабочей книги** с скопированными данными.

В этом руководстве рассматривается:

* Загрузка исходной рабочей книги и выбор листа.  
* Определение точного диапазона, который нужно переместить (включая сводную таблицу).  
* Создание целевой рабочей книги и копирование диапазона.  
* Сохранение целевого файла.  

Пример использует библиотеку Aspose.Cells for Java, которая работает с файлами Excel без необходимости установки Microsoft Office. Код работает на Java 8+ и в любой современной IDE (IntelliJ IDEA, Eclipse, VS Code и т.д.).

---

## Требования

Перед началом убедитесь, что у вас есть:

| Требование | Причина |
|-------------|--------|
| Java Development Kit (JDK) 8 или новее | Необходимо для компиляции и выполнения кода. |
| Инструмент сборки Maven или Gradle | Упрощает добавление зависимости Aspose.Cells. |
| Aspose.Cells for Java library (последняя версия) | Предоставляет классы `Workbook`, `Worksheet` и `Range`, используемые в примере. |
| Два файла Excel (`source.xlsx` и пустая папка для `dest.xlsx`) | Исходный файл должен содержать данные и, при желании, сводную таблицу, которую нужно скопировать. |

Добавьте зависимость Aspose.Cells в ваш `pom.xml` (Maven) или `build.gradle` (Gradle). Пример для Maven:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- use the latest version -->
</dependency>
```

---

## Как копировать ячейки с помощью Aspose.Cells

Следующие шаги проведут вас через весь процесс. Каждый шаг включает Java‑код, объяснение **почему** шаг важен, и совет, как избежать распространённых подводных камней.

### Шаг 1: Загрузить исходную рабочую книгу

```java
import com.aspose.cells.*;

public class ExcelCopyDemo {
    public static void main(String[] args) throws Exception {
        // Load the source Excel file (replace with your actual path)
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/source.xlsx");

        // Get the first worksheet (index 0)
        Worksheet srcWs = srcWb.getWorksheets().get(0);
```

**Why?**  
`Workbook` представляет всю Excel‑файл. Его загрузка даёт доступ ко всем листам, ячейкам и объектам, таким как сводные таблицы. Использование первого листа — обычный вариант, но вы можете выбрать любой лист по имени (`srcWb.getWorksheets().get("Sheet2")`).

**Pro tip:**  
Если исходный файл большой, рассмотрите загрузку в *memory‑efficient* режиме: `new Workbook("file.xlsx", new LoadOptions(LoadFormat.XLSX) {{ setMemorySetting(MemorySetting.MEMORY_PREFERENCE); }});`

### Шаг 2: Определить диапазон, включающий сводную таблицу

```java
        // Define the cell range that you want to copy.
        // Adjust "A1:G20" to match the area that contains your data/pivot table.
        Range srcRange = srcWs.getCells().createRange("A1:G20");
```

**Why?**  
Объект `Range` абстрагирует прямоугольный блок ячеек. Указывая `"A1:G20"` вы точно сообщаете Aspose.Cells, какие ячейки — включая любую встроенную сводную таблицу — нужно скопировать. Библиотека автоматически копирует данные, стили и определения сводных таблиц.

**Edge case:**  
Если сводная таблица выходит за пределы указанного диапазона, расширьте адрес (например, `"A1:Z100"`). Вы также можете использовать `srcWs.getCells().getMaxDataColumn()` и `getMaxDataRow()` для динамического вычисления используемой области.

### Шаг 3: Создать целевую рабочую книгу

```java
        // Create a new, empty workbook that will receive the copied range.
        Workbook destWb = new Workbook();               // defaults to a single empty sheet
        Worksheet destWs = destWb.getWorksheets().get(0);
```

**Why?**  
Новая рабочая книга гарантирует отсутствие нежелательного форматирования или скрытых листов, которые могли бы помешать скопированному содержимому. По умолчанию в новой книге уже есть один лист, который мы будем использовать в качестве цели.

### Шаг 4: Скопировать диапазон в целевую рабочую книгу

```java
        // Copy the source range to cell A1 of the destination worksheet.
        destWs.getCells().copyRange(srcRange, destWs.getCells().get("A1"));
```

**Why?**  
`copyRange` обрабатывает все атрибуты ячеек: значения, формулы, форматирование и даже кэши сводных таблиц. Копируя в `"A1"` вы размещаете диапазон в левом верхнем углу целевого листа, сохраняя оригинальное расположение.

**Common question:** *Сохранится ли работоспособность сводной таблицы?*  
Да. Aspose.Cells копирует определение сводной таблицы и её кэш, поэтому сводная таблица работает точно так же, как в исходной книге.

### Шаг 5: Сохранить целевую рабочую книгу

```java
        // Save the new workbook to disk.
        destWb.save("YOUR_DIRECTORY/dest.xlsx");
    }
}
```

**Why?**  
Вызов `save` записывает рабочую книгу из памяти в физический файл `.xlsx`. Вы также можете сохранять в другие форматы (`.xls`, `.csv`, `.pdf`), изменив расширение файла или используя `SaveOptions`.

**Tip:**  
Если нужно передать файл в веб‑ответ, используйте `destWb.save(OutputStream, SaveFormat.XLSX);` вместо пути к файлу.

---

## Копировать диапазон между рабочими книгами – полный исходный код

Ниже приведён полностью готовый к запуску Java‑класс. Замените `YOUR_DIRECTORY` реальной папкой на вашем компьютере.

```java
import com.aspose.cells.*;

public class ExcelCopyDemo {
    public static void main(String[] args) throws Exception {
        // Load the source workbook
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/source.xlsx");
        Worksheet srcWs = srcWb.getWorksheets().get(0);

        // Define the range that includes the data and pivot table
        Range srcRange = srcWs.getCells().createRange("A1:G20");

        // Create a new destination workbook
        Workbook destWb = new Workbook();
        Worksheet destWs = destWb.getWorksheets().get(0);

        // Copy the defined range to the destination workbook
        destWs.getCells().copyRange(srcRange, destWs.getCells().get("A1"));

        // Save the destination workbook
        destWb.save("YOUR_DIRECTORY/dest.xlsx");
    }
}
```

**Expected result:**  
`dest.xlsx` содержит точную копию диапазона `A1:G20` из `source.xlsx`. Если исходный диапазон включал сводную таблицу, в целевом файле будет отображаться та же сводная таблица с правильно привязанным источником данных.

Вы можете открыть `dest.xlsx` в Excel, LibreOffice или любом просмотрщике, поддерживающем `.xlsx`, чтобы убедиться, что значения, форматирование и функциональность сводной таблицы сохранены.

---

## Копировать рабочую книгу со сводной таблицей – что нужно знать

* **Pivot cache is copied automatically.** Библиотека переносит подлежащий кэш, поэтому сводную таблицу не требуется вручную обновлять.
* **External data sources are not transferred.** Если сводная таблица получает данные из внешней базы, необходимо обеспечить доступ целевой книги к тому же источнику или воссоздать кэш локально.
* **Large pivot tables may increase memory usage.** Для очень больших книг рекомендуется увеличить размер кучи JVM (`-Xmx2g`), чтобы избежать `OutOfMemoryError`.

---

## Сохранить файл рабочей книги в разных форматах

Aspose.Cells позволяет сохранять результат во множестве форматов без дополнительных изменений кода:

```java
// Save as XLS (Excel 97-2003)
destWb.save("dest.xls");

// Save as CSV (first worksheet only)
destWb.save("dest.csv");

// Save as PDF (visual representation)
destWb.save("dest.pdf");
```

Выберите формат, соответствующий вашему последующему процессу. Та же логика `copyRange` работает независимо от конечного формата.

---

## Загрузка Excel workbook Java – дополнительные советы

* **Loading encrypted files:** Use `LoadOptions` with a password:  
  ```java
  LoadOptions opt = new LoadOptions(LoadFormat.XLSX);
  opt.setPassword("myPassword");
  Workbook wb = new Workbook("encrypted.xlsx", opt);
  ```
* **Reading only specific sheets:**  
  ```java
  LoadOptions opt = new LoadOptions(LoadFormat.XLSX);
  opt.setLoadDataOnly(true); // faster if you only need values
  Workbook wb = new Workbook("file.xlsx", opt);
  ```

Эти параметры могут ускорить шаг **load excel workbook java**, особенно для больших файлов.

---

## Заключение

Теперь вы знаете **как копировать ячейки** между рабочими книгами Excel в Java, как **копировать диапазон между рабочими книгами**, содержащий **сводную таблицу**, и как **сохранить файл рабочей книги** в нужном вам формате. Следуя описанным шагам, вы сможете интегрировать работу с данными Excel в любое Java‑приложение — будь то система отчётности, ETL‑конвейер или простая утилита конвертации файлов.

**Next steps** you might explore:

* Use **copy range between workbooks** to merge multiple reports into

## Что вам стоит изучить дальше?

Следующие руководства охватывают тесно связанные темы, которые развивают техники, продемонстрированные в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы в ваших проектах.

- [Сохранить новую рабочую книгу в Java – руководство по копированию диапазона между рабочими книгами](/cells/english/java/workbook-operations/save-new-workbook-in-java-copy-range-between-workbooks-tutor/)
- [Как копировать сводные таблицы между рабочими книгами Excel в Java](/cells/english/java/excel-pivot-tables/how-to-copy-pivot-tables-between-excel-workbooks-in-java/)
- [Как копировать диапазон в Java – копировать сводную таблицу с Aspose.Cells](/cells/english/java/excel-pivot-tables/how-to-copy-range-in-java-copy-pivot-table-with-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}