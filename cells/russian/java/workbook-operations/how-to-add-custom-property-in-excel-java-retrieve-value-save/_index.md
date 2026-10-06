---
category: general
date: 2026-06-18
description: Как добавить пользовательское свойство в Excel с помощью Java. Узнайте,
  как получить значение пользовательского свойства и сохранить книгу в формате XLSB
  с полным, исполняемым примером.
draft: false
keywords:
- how to add custom property
- retrieve custom property value
- save workbook as xlsb
- create custom property in excel
language: ru
og_description: Как добавить пользовательское свойство в Excel с помощью Java. Это
  руководство показывает, как получить значение пользовательского свойства и сохранить
  книгу в формате XLSB.
og_title: Как добавить пользовательское свойство в Excel (Java) — пошагово
schemas:
- author: Aspose
  dateModified: '2026-06-18'
  description: How to add custom property in Excel using Java. Learn to retrieve custom
    property value and save workbook as XLSB with a complete, runnable example.
  headline: How to Add Custom Property in Excel (Java) – Retrieve Value & Save as
    XLSB
  type: TechArticle
tags:
- Java
- Excel
- Aspose.Cells
title: Как добавить пользовательское свойство в Excel (Java) – получить значение и
  сохранить как XLSB
url: /ru/java/workbook-operations/how-to-add-custom-property-in-excel-java-retrieve-value-save/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как добавить пользовательское свойство в Excel (Java) – Получить значение и сохранить как XLSB

Как добавить пользовательское свойство в Excel с помощью Java — это частая необходимость, когда нужно пометить листы метаданными. В этом руководстве мы также получим значение пользовательского свойства и **сохраним книгу в формате XLSB**, чтобы вы получили полное решение «от начала до конца», которое можно внедрить в любой проект.

Представьте, что вы создаёте движок отчётности, который генерирует десятки электронных таблиц каждую ночь. Было бы удобно внедрить «ProjectId» или «ReportVersion» непосредственно в файл, чтобы downstream‑системы могли позже фильтровать или проводить аудит. Именно это и дают пользовательские свойства — небольшие кусочки данных, хранящиеся внутри книги без захламления видимых ячеек.

Мы рассмотрим:

* Создание пользовательского свойства в Excel (пример «ProjectId»).  
* Получение значения этого свойства для проверки его работы.  
* Сохранение изменённой книги как **XLSB**‑файла, бинарного формата, который уменьшает размер файла и ускоряет загрузку.  

**Требования**

* Java 17 или новее.  
* Aspose.Cells for Java (библиотека, позволяющая работать с Excel‑файлами без Microsoft Office).  
* Действующая лицензия Aspose.Cells – бесплатная оценочная версия подходит для этой демонстрации, но лицензия убирает водяной знак оценки.  

Если вы никогда не работали с Aspose.Cells, не переживайте. API прост, а код ниже готов к запуску после добавления JAR‑файла в classpath.

![как добавить пользовательское свойство в Excel с помощью Java](image-url-placeholder "Как добавить пользовательское свойство в Excel с помощью Java")

---

## Как добавить пользовательское свойство – Шаг 1

Сначала нужно загрузить существующую книгу (или создать новую), а затем прикрепить пользовательское свойство к первому листу. Свойство представляет собой пару ключ/значение, хранящуюся в коллекции `CustomProperties` листа.

```java
import com.aspose.cells.*;

public class CustomPropertyDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the workbook from a file (you can also create a new workbook)
        Workbook workbook = new Workbook("YOUR_DIRECTORY/custom.xlsb");

        // Step 2: Access the first worksheet
        Worksheet sheet = workbook.getWorksheets().get(0);

        // Step 3: Add a custom property named "ProjectId" with a numeric value
        // This is the core of how to add custom property in Excel.
        sheet.getCustomProperties().add("ProjectId", 12345);

        // Step 4: Retrieve the value of the custom property we just added
        // (We'll also show you how to retrieve custom property value later.)
        Object projectIdValue = sheet.getCustomProperties().get("ProjectId").getValue();

        // Step 5: Display the retrieved value on the console
        System.out.println("ProjectId = " + projectIdValue);

        // Step 6: Save the modified workbook to a new file in XLSB format
        // This demonstrates how to save workbook as XLSB.
        workbook.save("YOUR_DIRECTORY/customOut.xlsb", SaveFormat.XLSB);
    }
}
```

**Почему это работает**

* `Workbook` — точка входа для любого Excel‑файла, своего рода контейнер для всех листов, стилей и метаданных.  
* `Worksheet.getCustomProperties()` возвращает коллекцию, работающую как словарь; вызов `.add(name, value)` создаёт свойство, если его ещё нет.  
* Значение свойства может быть любого примитивного типа (int, double, String, boolean) – Aspose.Cells выполнит конвертацию за вас.  

При запуске программа выводит:

```
ProjectId = 12345
```

Теперь вы успешно **добавили пользовательское свойство** и подтвердили его наличие.

---

## Получить значение пользовательского свойства

Возможно, вы задаётесь вопросом: «Как прочитать свойство позже, возможно, в другом модуле?» Та же коллекция `CustomProperties` позволяет получить значение по имени. Ниже приведён фокусированный фрагмент, демонстрирующий **получение значения пользовательского свойства** без повторного добавления.

```java
// Assume workbook is already loaded and sheet points to the correct worksheet
CustomPropertyCollection props = sheet.getCustomProperties();

// Check if the property exists to avoid NullPointerException
if (props.contains("ProjectId")) {
    Object value = props.get("ProjectId").getValue();
    System.out.println("Retrieved ProjectId = " + value);
} else {
    System.out.println("ProjectId property not found.");
}
```

**Ключевые моменты**

* `contains` — защита; в реальном коде всегда проверяйте существование свойства перед чтением.  
* Возвращаемый `Object` можно привести к ожидаемому типу, если нужны арифметические операции (например, `(int) value`).  

Этот небольшой шаблон решает большинство сценариев аудита, когда нужно извлечь метаданные из книги, созданной несколько недель назад.

---

## Сохранить книгу как XLSB

Почему стоит выбирать XLSB вместо более распространённого XLSX? Бинарные файлы XLSB обычно **на 30‑40 % меньше** и открываются быстрее, особенно при больших объёмах данных. Aspose.Cells делает сохранение в этом формате однострочным, как показано в **Шаге 6** первого блока кода.

Если нужно держать книгу в памяти (например, чтобы отправить её через веб‑службу), можно записать её в `ByteArrayOutputStream`:

```java
ByteArrayOutputStream baos = new ByteArrayOutputStream();
workbook.save(baos, SaveFormat.XLSB);
byte[] xlsbBytes = baos.toByteArray();
// Now you can attach xlsbBytes to an email, upload to S3, etc.
```

Перечисление `SaveFormat.XLSB` гарантирует бинарный формат, и тот же вызов работает для любой книги, независимо от того, добавляли ли вы только пользовательское свойство или выполняли сложные расчёты.

---

## Создание пользовательского свойства в Excel – Полный пример от начала до конца

Ниже представлена готовая, автономная программа, объединяющая **добавление пользовательского свойства**, **получение его значения** и **сохранение книги как XLSB**. Скопируйте‑вставьте её в IDE, скорректируйте пути к файлам и запустите.

```java
import com.aspose.cells.*;

public class ExcelCustomPropertyExample {
    public static void main(String[] args) {
        try {
            // 1️⃣ Load an existing XLSB workbook (or create a new one)
            Workbook workbook = new Workbook("YOUR_DIRECTORY/custom.xlsb");

            // 2️⃣ Grab the first worksheet – you could loop through all sheets if needed
            Worksheet sheet = workbook.getWorksheets().get(0);

            // 3️⃣ Create a custom property called "ProjectId"
            // This is the essential step for how to add custom property.
            sheet.getCustomProperties().add("ProjectId", 12345);
            System.out.println("Custom property 'ProjectId' added.");

            // 4️⃣ Retrieve the property to prove it works – demonstrates retrieve custom property value
            CustomPropertyCollection props = sheet.getCustomProperties();
            if (props.contains("ProjectId")) {
                Object val = props.get("ProjectId").getValue();
                System.out.println("Retrieved ProjectId = " + val);
            }

            // 5️⃣ Optionally, add another property (string type) to show flexibility
            sheet.getCustomProperties().add("ReportVersion", "v2.1");
            System.out.println("Added ReportVersion property.");

            // 6️⃣ Save the workbook as an XLSB file – this is the save workbook as XLSB step.
            workbook.save("YOUR_DIRECTORY/customOut.xlsb", SaveFormat.XLSB);
            System.out.println("Workbook saved as XLSB at YOUR_DIRECTORY/customOut.xlsb");

        } catch (Exception e) {
            // Real‑world code should log the exception; here we just print stack trace.
            e.printStackTrace();
        }
    }
}
```

**Ожидаемый вывод в консоль**

```
Custom property 'ProjectId' added.
Retrieved ProjectId = 12345
Added ReportVersion property.
Workbook saved as XLSB at YOUR_DIRECTORY/customOut.xlsb
```

Откройте `customOut.xlsb` в Excel, перейдите в **Файл → Сведения → Свойства → Дополнительные свойства → Пользовательские**, и вы увидите оба свойства `ProjectId` и `ReportVersion` — доказательство того, что **создание пользовательского свойства в Excel** действительно произошло.

---

## Распространённые ошибки и профессиональные советы

| Ошибка | Почему происходит | Как исправить |
|--------|-------------------|---------------|
| Забыл вызвать `workbook.save(...)` | Без сохранения изменения остаются только в памяти | Убедитесь, что после всех изменений вызываете `workbook.save("path/to/file.xlsb", SaveFormat.XLSB);` |
| Использование неверного типа данных для свойства | Aspose.Cells пытается конвертировать, но может бросить исключение | Перед добавлением свойства проверяйте тип и при необходимости приводите к поддерживаемому (int, double, String, boolean) |
| Не проверяете наличие свойства перед чтением | При отсутствии свойства будет `KeyNotFoundException` | Всегда используйте `if (worksheet.getCustomProperties().contains("PropertyName")) { … }` |
| Сохраняете в XLSX, а ожидаете уменьшения размера | Формат XLSX — XML‑текстовый, размер может быть больше | Переключитесь на `SaveFormat.XLSB` для бинарного сжатия |
| Путь к файлу содержит русские символы без правильной кодировки | Может привести к `IOException` при сохранении | Используйте абсолютный путь в UTF‑8 или избегайте нелатинских символов в пути |

---

## Что изучать дальше?

Следующие руководства охватывают смежные темы, расширяющие техники, продемонстрированные в этом руководстве. Каждый ресурс содержит полностью работающие примеры кода с пошаговыми объяснениями, чтобы вы могли освоить дополнительные возможности API и исследовать альтернативные подходы в своих проектах.

- [Excel Workbook Custom Property Management Using Aspose.Cells .NET](/cells/english/net/workbook-operations/excel-workbook-property-management-aspose-cells-net/)
- [How to Export Custom Excel Properties to PDF Using Aspose.Cells for Java](/cells/english/java/workbook-operations/export-excel-custom-properties-pdf-aspose-cells-java/)
- [How to Access Custom Document Properties in Excel Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/access-custom-excel-properties-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}