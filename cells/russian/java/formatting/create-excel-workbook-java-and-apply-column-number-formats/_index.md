---
category: general
date: 2026-09-27
description: Создать Excel‑книгу в Java, импортировать данные из SQL, установить числовой
  формат столбца и сохранить книгу в формате XLSX с помощью Aspose.Cells в Java.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook java
- save workbook as xlsx
- import sql data excel
- add number format excel
- set number format column
language: ru
lastmod: 2026-09-27
og_description: Создайте Excel‑книгу на Java, импортируйте данные из SQL, задайте
  числовой формат столбца и сохраните книгу в формате XLSX с полностью рабочим примером
  на Java.
og_image_alt: Screenshot of a Java program creating an Excel workbook with styled
  numeric columns
og_title: Создать Excel‑книгу в Java – импортировать данные из SQL и задать числовые
  форматы столбцов
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Create Excel workbook java, import SQL data, set number format column,
    and save workbook as XLSX using Aspose.Cells in Java.
  headline: Create Excel workbook java and apply column number formats
  type: TechArticle
tags:
- Java
- Aspose.Cells
- Excel automation
- Data import
title: Создать Excel‑рабочую книгу на Java и применить числовые форматы столбцов
url: /ru/java/formatting/create-excel-workbook-java-and-apply-column-number-formats/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создать Excel‑книгу Java и применить числовые форматы столбцов

Если вам нужно **create Excel workbook java** и оформить числовые столбцы, это руководство покажет, как это сделать. Вы узнаете, как импортировать данные SQL в Excel, задать числовой формат для каждого столбца и **save workbook as XLSX** с помощью библиотеки Aspose.Cells.

Работа с электронными таблицами из Java часто выглядит фрагментарно — разработчики копируют‑вставляют фрагменты кода, забывают форматировать числа или в итоге получают CSV вместо настоящих файлов Excel. Это руководство устраняет эти трудности, предоставляя единое сквозное решение, которое можно добавить в любой Java‑проект.

К концу статьи вы сможете:

* Подключиться к базе данных и получить `DataTable` (или `ResultSet`)  
* Создать новую книгу с Aspose.Cells  
* Применить единый стиль **add number format excel** ко всем столбцам  
* **Save workbook as XLSX** в выбранное вами место  

Единственное требование — наличие среды разработки Java (рекомендовано JDK 8+ ) и JAR‑файла Aspose.Cells for Java в вашем classpath.

---

## Требования

| Требование | Почему это важно |
|------------|------------------|
| JDK 8 или новее | Предоставляет языковые возможности, используемые в примере. |
| Aspose.Cells for Java (последняя версия) | Обрабатывает создание, стилизацию и сохранение Excel без установленного Office. |
| База данных, совместимая с JDBC (например, MySQL, PostgreSQL) | Поставляет SQL‑данные, которые мы будем импортировать. |
| Maven или Gradle (опционально) | Упрощает управление зависимостями. |

Добавьте Aspose.Cells в ваш `pom.xml` Maven:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- use the latest stable version -->
</dependency>
```

Или скачайте JAR‑файл напрямую с сайта Aspose и добавьте его в classpath вашего проекта.

---

## Шаг 1: Create Excel workbook java

Первый логический блок — создать новый `Workbook`. Этот объект представляет всю Excel‑книгу в памяти и дает доступ к листам, ячейкам и стилям.

```java
// Step 1: Create a new workbook instance
Workbook workbook = new Workbook();
```

Создание книги заранее также предоставляет нам фабрику `Style`, которую мы позже используем при **set number format column**.

---

## Шаг 2: Retrieve data from SQL (import sql data excel)

Ниже мы открываем JDBC‑соединение, выполняем простой запрос `SELECT` и загружаем результат в Aspose `DataTable`. Класс `DataTable` имитирует .NET `DataTable` и без проблем работает с методом `importDataTable`.

```java
// Step 2: Pull data from a database and fill a DataTable
private static DataTable getDataTableFromDb() throws SQLException {
    // Replace with your actual connection string, user, and password
    String url = "jdbc:mysql://localhost:3306/yourdb";
    String user = "your_user";
    String password = "your_password";

    try (Connection conn = DriverManager.getConnection(url, user, password);
         Statement stmt = conn.createStatement();
         ResultSet rs = stmt.executeQuery("SELECT Id, Amount, CreatedDate FROM Payments")) {

        // Aspose.Cells provides a utility to convert ResultSet → DataTable
        return CellsHelper.getDataTableFromResultSet(rs);
    }
}
```

> **Подсказка:** Если у вас уже есть `DataTable` из другого источника (например, парсинг CSV), вы можете пропустить код JDBC и сразу вернуть эту таблицу.

---

## Шаг 3: Prepare a reusable style (add number format excel)

Мы хотим, чтобы каждый числовой столбец отображал числа с двумя знаками после запятой и разделителем тысяч. Вместо стилизации каждой ячейки отдельно, создаём объект `Style` один раз для каждого столбца и переиспользуем его при импорте. Это самый эффективный способ **add number format excel**.

```java
// Step 3: Build a style array – one style per column
private static Style[] buildColumnStyles(Workbook workbook, int columnCount) {
    Style[] styles = new Style[columnCount];
    for (int i = 0; i < columnCount; i++) {
        styles[i] = workbook.createStyle();
        // "0.00" = two decimal places; "#,##0.00" adds thousands separator
        styles[i].setNumber("#,##0.00");
    }
    return styles;
}
```

Вы можете изменить строку формата (`"#,##0.00"`) под любой нужный вам числовой формат Excel. Для дат используйте `styles[i].setCustom("mm-dd-yyyy")` и т.д.

---

## Шаг 4: Import the DataTable and apply the column styles

Теперь собираем всё вместе. Перегрузка `importDataTable` позволяет передать `DataTable`, указать, следует ли рассматривать первую строку как заголовки столбцов, и передать массив стилей. Это автоматически **set number format column** для каждой ячейки соответствующего столбца.

```java
// Step 4: Import data with styles into the first worksheet
private static void importDataWithStyles(Workbook workbook, DataTable dataTable) {
    // Build a style for each column based on the number of columns in the DataTable
    Style[] columnStyles = buildColumnStyles(workbook, dataTable.getColumns().size());

    // Import the DataTable starting at cell A1 (row 0, column 0)
    workbook.getWorksheets().get(0).getCells()
            .importDataTable(dataTable, true, 0, 0, columnStyles);
}
```

Поскольку мы передали `true` для флага `importColumnNames`, первая строка листа содержит имена столбцов из `DataTable`. Каждая последующая строка получает данные, уже отформатированные согласно заданному стилю.

---

## Шаг 5: Save workbook as xlsx

Последний шаг — сохранить книгу из памяти в физический файл. Aspose.Cells поддерживает множество форматов; мы используем современный формат XLSX, который сегодня ожидают большинство приложений.

```java
// Step 5: Save the workbook to an .xlsx file
private static void saveWorkbook(Workbook workbook, String filePath) throws IOException {
    workbook.save(filePath, com.aspose.cells.SaveFormat.XLSX);
}
```

Вы можете изменить `filePath` на любой допустимый путь в вашей системе. Метод бросает `IOException`, если каталог не существует или у вас нет прав на запись.

---

## Полный, готовый к запуску пример

Собрав все части вместе, получаем автономную программу, которую можно сразу скомпилировать и запустить.

```java
import com.aspose.cells.*;
import java.sql.*;

public class CreateExcelWorkbookJava {
    public static void main(String[] args) {
        try {
            // 1️⃣ Obtain data from the database
            DataTable dataTable = getDataTableFromDb();

            // 2️⃣ Create a new workbook that will hold the imported data
            Workbook workbook = new Workbook();

            // 3️⃣ Import the DataTable with a numeric style per column
            importDataWithStyles(workbook, dataTable);

            // 4️⃣ Save the workbook as XLSX
            String outputPath = "DataTableWithNumberFormat.xlsx";
            saveWorkbook(workbook, outputPath);

            System.out.println("Workbook created successfully at: " + outputPath);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    // ---- Helper methods (see earlier sections) ----
    private static DataTable getDataTableFromDb() throws SQLException {
        String url = "jdbc:mysql://localhost:3306/yourdb";
        String user = "your_user";
        String password = "your_password";

        try (Connection conn = DriverManager.getConnection(url, user, password);
             Statement stmt = conn.createStatement();
             ResultSet rs = stmt.executeQuery("SELECT Id, Amount, CreatedDate FROM Payments")) {

            return CellsHelper.getDataTableFromResultSet(rs);
        }
    }

    private static Style[] buildColumnStyles(Workbook workbook, int columnCount) {
        Style[] styles = new Style[columnCount];
        for (int i = 0; i < columnCount; i++) {
            styles[i] = workbook.createStyle();
            styles[i].setNumber("#,##0.00"); // two decimals with thousands separator
        }
        return styles;
    }

    private static void importDataWithStyles(Workbook workbook, DataTable dataTable) {
        Style[] columnStyles = buildColumnStyles(workbook, dataTable.getColumns().size());
        workbook.getWorksheets().get(0).getCells()
                .importDataTable(dataTable, true, 0, 0, columnStyles);
    }

    private static void saveWorkbook(Workbook workbook, String filePath) throws IOException {
        workbook.save(filePath, SaveFormat.XLSX);
    }
}
```

### Ожидаемый результат

Запуск программы создаёт файл **DataTableWithNumberFormat.xlsx** в рабочем каталоге. Откройте его в Microsoft Excel, LibreOffice Calc или любом просмотрщике XLSX, и вы увидите:

| Id | Amount | CreatedDate |
|----|--------|-------------|
| 1  | 1,234.56 | 2023‑01‑15 |
| 2  | 78,900.00 | 2023‑02‑20 |
| …  | … | … |

*Столбец **Amount** отображает числа с двумя знаками после запятой и разделителем тысяч благодаря применённому стилю **add number format excel**.*

---

## Часто задаваемые вопросы и обработка граничных случаев

| Вопрос | Ответ |
|--------|-------|
| **Что если мой запрос не возвращает строк?** | `DataTable` будет пустой, но всё равно будет содержать определения столбцов. Книга будет содержать только строку заголовков, чего часто достаточно для последующей обработки. |
| **Как применить разные форматы для разных столбцов?** | Измените `buildColumnStyles`, чтобы проверять имя столбца или тип данных и назначать пользовательский формат (например, даты, проценты). |
| **Могу ли я записать напрямую в `ByteArrayOutputStream`?** | Да. Замените `workbook.save(filePath, SaveFormat.XLSX);` на |

## Что вам стоит изучить дальше?

Следующие руководства охватывают тесно связанные темы, расширяющие техники, продемонстрированные в этом руководстве. Каждый ресурс содержит полностью работающие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы в ваших проектах.

- [How to Create and Save an Excel Workbook as SVG using Aspose.Cells for Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)
- [Create Save Excel Workbook Aspose Cells Java](/cells/hindi/java/workbook-operations/create-save-excel-workbook-aspose-cells-java/)
- [Create Save Excel Workbook Aspose Cells Java](/cells/german/java/workbook-operations/create-save-excel-workbook-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}