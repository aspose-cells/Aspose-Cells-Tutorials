---
category: general
date: 2026-08-11
description: Создайте новую рабочую книгу Aspose в Java, добавьте пользовательское
  свойство Excel, затем сохраните книгу в формате XLSB с полным пошаговым примером.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create new workbook aspose
- save workbook as xlsb
- add custom property excel
- Aspose.Cells Java
- custom properties Excel
- workbook serialization
language: ru
lastmod: 2026-08-11
og_description: Создайте новую рабочую книгу Aspose в Java, добавьте пользовательское
  свойство Excel и сохраните её в формате XLSB с полным готовым к запуску примером.
og_image_alt: Java code screenshot that creates a new workbook Aspose, adds a custom
  Excel property, and saves it as an XLSB file
og_title: Создать новую рабочую книгу Aspose – добавить пользовательское свойство
  Excel
schemas:
- author: Aspose
  dateModified: '2026-08-11'
  description: Create new workbook Aspose in Java, add a custom property Excel, then
    save workbook as XLSB with a full step‑by‑step example.
  headline: Create new workbook Aspose – add custom property Excel and save as XLSB
  type: TechArticle
- description: Create new workbook Aspose in Java, add a custom property Excel, then
    save workbook as XLSB with a full step‑by‑step example.
  name: Create new workbook Aspose – add custom property Excel and save as XLSB
  steps:
  - name: What if I need to store a string property?
    text: '```java worksheet.getCustomProperties().add("Owner", "Alice"); ```'
  - name: Can I add multiple custom properties at once?
    text: Yes. Call `add` repeatedly for each name/value pair. Aspose.Cells does not
      limit the number of custom properties, but keep the total size reasonable to
      avoid bloating the file.
  - name: How does the binary format affect performance?
    text: XLSB files load faster because they avoid XML parsing. This is especially
      noticeable for workbooks with many rows, formulas, or embedded images.
  - name: What if I need to work with an existing XLSX file?
    text: Replace the `new Workbook()` constructor with `new Workbook("ExistingFile.xlsx")`.
      The rest of the steps (adding properties, saving as XLSB) remain identical.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel
- XLSB
- Custom Properties
title: Создать новую рабочую книгу Aspose – добавить пользовательское свойство Excel
  и сохранить в формате XLSB
url: /ru/java/spreadsheet-automation/create-new-workbook-aspose-add-custom-property-excel-and-sav/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создать новую книгу Aspose – добавить пользовательское свойство Excel и сохранить как XLSB

Если вам нужно **create new workbook Aspose** в Java‑приложении, это руководство покажет, как именно это сделать. Вы узнаете, как **add custom property Excel**, получить значение и **save workbook as XLSB** без потери каких-либо метаданных.

В этом руководстве рассматривается всё — от настройки проекта до проверки сохранённого файла. Внешняя документация не требуется; просто следуйте шагам и запустите код.

## Предварительные требования

- Java Development Kit (JDK) 8 или выше установлен.
- Maven или Gradle для управления зависимостями (в примере используется Maven).
- Действующая лицензия Aspose.Cells for Java (или используйте бесплатный режим оценки для тестирования).

## Шаг 1: Добавить Aspose.Cells в ваш проект

Добавьте артефакт Aspose.Cells Maven в ваш `pom.xml`. Эта зависимость предоставляет классы, необходимые для объектов **create new workbook Aspose**.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- Use the latest stable version -->
</dependency>
```

> **Pro tip:** Если вы предпочитаете Gradle, замените Maven‑фрагмент на эквивалентную строку `implementation "com.aspose:aspose-cells:23.12"`.

## Шаг 2: Создать новую книгу Aspose

Первый функциональный шаг — создать экземпляр объекта `Workbook`. Этот объект представляет файл Excel в памяти и является точкой входа для всех дальнейших операций.

```java
import com.aspose.cells.*;

public class CustomPropertiesXlsb {

    public static void main(String[] args) throws Exception {
        // Step 2: Create a new workbook Aspose
        Workbook workbook = new Workbook();               // In‑memory workbook
        Worksheet worksheet = workbook.getWorksheets().get(0); // Default first sheet
```

Создание новой книги Aspose предоставляет вам чистую книгу с листом по умолчанию, готовую к настройке.

## Шаг 3: Добавить пользовательское свойство Excel

Пользовательские свойства позволяют хранить произвольные метаданные внутри файла Excel. Здесь мы **add custom property Excel** с именем `ProjectId` и числовым значением.

```java
        // Step 3: Add a custom property named "ProjectId" with a numeric value
        worksheet.getCustomProperties().add("ProjectId", 12345);
```

Метод `add` принимает имя свойства и значение любого поддерживаемого типа (строка, число, дата и т.д.). Эти метаданные перемещаются вместе с файлом, куда бы вы его ни скопировали.

## Шаг 4: Получить и отобразить пользовательское свойство

Чтение свойства обратно подтверждает, что оно было сохранено корректно. Вы также можете использовать полученное значение в своей бизнес‑логике.

```java
        // Step 4: Retrieve the custom property value and display it
        int projectId = (int) worksheet.getCustomProperties()
                                      .get("ProjectId")
                                      .getValue();
        System.out.println("ProjectId = " + projectId);
```

Приведение к `int` работает, потому что мы сохранили числовое значение. Если вы сохраняете строку, используйте `(String)` вместо этого.

## Шаг 5: Сохранить книгу как XLSB

Теперь вы **save workbook as XLSB**. Формат XLSB сохраняет книгу в бинарном представлении, что обеспечивает более быструю загрузку и меньший размер на диске. Все пользовательские свойства сохраняются автоматически.

```java
        // Step 5: Save the workbook as an XLSB file (custom properties are preserved)
        workbook.save("WithCustomProps.xlsb", SaveFormat.XLSB);
    }
}
```

Замените `"WithCustomProps.xlsb"` на абсолютный путь, если вам нужен файл в определённой директории. Перечисление `SaveFormat.XLSB` указывает Aspose.Cells записать файл в бинарном формате.

## Шаг 6: Проверить результат

Запустите программу из вашей IDE или из командной строки:

```bash
mvn compile exec:java -Dexec.mainClass=CustomPropertiesXlsb
```

Вы должны увидеть:

```
ProjectId = 12345
```

Откройте `WithCustomProps.xlsb` в Excel. Перейдите к **File → Info → Properties → Advanced Properties → Custom**. Запись `ProjectId` со значением `12345` будет отображена, подтверждая, что шаг **add custom property excel** выполнен успешно и операция **save workbook as xlsb** сохранила метаданные.

## Часто задаваемые вопросы и особые случаи

### Что если мне нужно сохранить строковое свойство?

```java
worksheet.getCustomProperties().add("Owner", "Alice");
```

Получить его можно с помощью:

```java
String owner = (String) worksheet.getCustomProperties().get("Owner").getValue();
```

### Можно ли добавить несколько пользовательских свойств одновременно?

Да. Вызывайте `add` последовательно для каждой пары имя/значение. Aspose.Cells не ограничивает количество пользовательских свойств, но держите общий размер разумным, чтобы не раздувать файл.

### Как бинарный формат влияет на производительность?

Файлы XLSB загружаются быстрее, поскольку избегают парсинга XML. Это особенно заметно для книг с большим количеством строк, формул или встроенных изображений.

### Что если мне нужно работать с существующим файлом XLSX?

Замените конструктор `new Workbook()` на `new Workbook("ExistingFile.xlsx")`. Остальные шаги (добавление свойств, сохранение как XLSB) остаются идентичными.

## Полный исходный код

Ниже приведён полный готовый к запуску пример. Скопируйте его в файл с именем `CustomPropertiesXlsb.java` в папку `src/main/java` вашего проекта.

```java
import com.aspose.cells.*;

public class CustomPropertiesXlsb {
    public static void main(String[] args) throws Exception {
        // Step 2: Create a new workbook Aspose
        Workbook workbook = new Workbook();                       // In‑memory workbook
        Worksheet worksheet = workbook.getWorksheets().get(0);    // Default first sheet

        // Step 3: Add a custom property named "ProjectId" with a numeric value
        worksheet.getCustomProperties().add("ProjectId", 12345);

        // Step 4: Retrieve the custom property value and display it
        int projectId = (int) worksheet.getCustomProperties()
                                      .get("ProjectId")
                                      .getValue();
        System.out.println("ProjectId = " + projectId);

        // Step 5: Save the workbook as an XLSB file (custom properties are preserved)
        workbook.save("WithCustomProps.xlsb", SaveFormat.XLSB);
    }
}
```

Запуск этого класса создаёт файл XLSB, содержащий пользовательское свойство, который можно открыть в любой современной версии Microsoft Excel.

## Заключение

Теперь вы знаете, как **create new workbook Aspose**, **add custom property Excel** и **save workbook as XLSB** с помощью Java. Пример демонстрирует полный цикл: инициализацию, внедрение метаданных, проверку и бинарную сериализацию.

Далее изучайте связанные темы, такие как **setting document properties**, **working with Excel formulas** или **converting between XLSX and XLSB**. Каждая из них опирается на тот же API Aspose.Cells, который вы только что использовали, поэтому вы можете расширять решение без изучения новых библиотек.

Не стесняйтесь экспериментировать с различными типами данных, несколькими листами или защитой паролем — Aspose.Cells поддерживает все эти сценарии из коробки. Приятного кодинга!

## Что стоит изучить дальше?

Следующие руководства охватывают тесно связанные темы, которые опираются на техники, продемонстрированные в этом руководстве. Каждый ресурс включает полные рабочие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [Create Save Excel Workbook Aspose Cells Java](/cells/english/java/workbook-operations/create-save-excel-workbook-aspose-cells-java/)
- [How to Create and Save an Excel Workbook as SVG using Aspose.Cells for Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)
- [Create Excel Workbook and Add Labels with Aspose.Cells for Java](/cells/english/java/advanced-excel-charts/data-labeling/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}