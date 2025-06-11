---
"date": "2025-04-08"
"description": "Узнайте, как использовать Aspose.Cells для Java для добавления текстовых полей и установки межстрочного интервала в книгах Excel. Улучшите презентации книг с помощью стилизованных текстовых фигур."
"title": "Добавить текстовое поле и задать межстрочный интервал в Excel с помощью Aspose.Cells для Java"
"url": "/ru/java/images-shapes/aspose-cells-java-add-text-box-line-spacing/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# Добавьте текстовое поле и установите межстрочный интервал в Excel с помощью Aspose.Cells для Java

## Введение

Создание динамических отчетов Excel часто требует пользовательского форматирования текста, например добавления текстовых полей с определенным межстрочным интервалом. С Aspose.Cells для Java это становится простым и эффективным. Это руководство проведет вас через улучшение презентаций ваших рабочих книг с помощью Aspose.Cells для Java для добавления стилизованных текстовых фигур.

К концу этого руководства вы узнаете, как:
- Создайте новую книгу Excel и получите доступ к ее рабочим листам.
- Добавить форму текстового поля на рабочий лист
- Установите индивидуальный межстрочный интервал внутри текстовой фигуры
- Сохраните отформатированную книгу в формате XLSX.

Давайте начнем с настройки вашей среды.

### Предпосылки

Прежде чем начать, убедитесь, что у вас есть следующее:
- Java Development Kit (JDK), установленный на вашем компьютере
- IDE или редактор для написания кода Java
- Система сборки Maven или Gradle, настроенная для управления зависимостями

Базовые знания программирования на Java и знакомство со структурами файлов Excel будут преимуществом.

## Настройка Aspose.Cells для Java

Включите Aspose.Cells в управление зависимостями вашего проекта с помощью Maven или Gradle:

**Знаток**

Добавьте следующий блок зависимости в ваш `pom.xml` файл:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

**Градл**

Включите это в свой `build.gradle` файл:

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

Затем приобретите лицензию на Aspose.Cells, выбрав бесплатную пробную версию, запросив временную лицензию или купив полную лицензию.

### Инициализация Aspose.Cells

После включения библиотеки в ваш проект инициализируйте ее в вашем приложении Java:

```java
import com.aspose.cells.Workbook;

public class ExcelDemo {
    public static void main(String[] args) {
        // Инициализирует экземпляр Workbook (представляет собой файл Excel)
        Workbook workbook = new Workbook();
        
        System.out.println("Aspose.Cells for Java initialized successfully.");
    }
}
```

## Руководство по внедрению

### Создать рабочую книгу и получить доступ к рабочему листу

Начните с создания новой книги Excel и доступа к ее первому листу. Здесь вы добавите текстовое поле.

#### Обзор

Создание новой рабочей книги предоставляет пустое пространство для добавления данных, фигур и форматирования по мере необходимости.

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;

public class ExcelDemo {
    public static void main(String[] args) {
        // Создать новую рабочую книгу (файл Excel)
        Workbook workbook = new Workbook();
        
        // Доступ к первому рабочему листу
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        System.out.println("Workbook and first worksheet accessed.");
    }
}
```

### Добавить текстовое поле на рабочий лист

Далее добавьте фигуру текстового поля на выбранный вами рабочий лист. Эта фигура может содержать любой текстовый контент, который вам нужен.

#### Обзор

Текстовые поля — это универсальные инструменты для включения пользовательских текстов, таких как примечания или инструкции, непосредственно в таблицу Excel.

```java
import com.aspose.cells.Shape;
import com.aspose.cells.MsoDrawingType;

public class ExcelDemo {
    public static void main(String[] args) {
        // Создать новую рабочую книгу (файл Excel)
        Workbook workbook = new Workbook();
        
        // Доступ к первому рабочему листу
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        // Добавьте на рабочий лист форму текстового поля.
        Shape textBox = sheet.getShapes().addShape(MsoDrawingType.TEXT_BOX, 2, 0, 2, 0, 100, 200);
        
        System.out.println("Text box added.");
    }
}
```

### Установить текст в форме

Как только текстовое поле будет готово, настройте его содержимое и отформатируйте текст внутри него.

```java
import com.aspose.cells.Shape;

public class ExcelDemo {
    public static void main(String[] args) {
        // Создать новую рабочую книгу (файл Excel)
        Workbook workbook = new Workbook();
        
        // Доступ к первому рабочему листу
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        // Добавьте на рабочий лист форму текстового поля.
        Shape textBox = sheet.getShapes().addShape(MsoDrawingType.TEXT_BOX, 2, 0, 2, 0, 100, 200);
        
        // Установить текстовое содержимое внутри фигуры
        textBox.setText("Sign up for your free phone number.\nCall and text online for free.");
        
        System.out.println("Text set in shape.");
    }
}
```

### Доступ к текстовым абзацам в форме

Вы можете получить доступ к отдельным абзацам в текстовом поле, чтобы применить определенное форматирование.

```java
import com.aspose.cells.TextParagraph;

public class ExcelDemo {
    public static void main(String[] args) {
        // Создать новую рабочую книгу (файл Excel)
        Workbook workbook = new Workbook();
        
        // Доступ к первому рабочему листу
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        // Добавьте на рабочий лист форму текстового поля.
        Shape textBox = sheet.getShapes().addShape(MsoDrawingType.TEXT_BOX, 2, 0, 2, 0, 100, 200);
        
        // Установить текстовое содержимое внутри фигуры
        textBox.setText("Sign up for your free phone number.\nCall and text online for free.");
        
        // Доступ ко второму абзацу в форме
        TextParagraph paragraph = textBox.getTextBody().getTextParagraphs().get(1);
        
        System.out.println("Accessed second paragraph in text box.");
    }
}
```

### Установить межстрочный интервал абзаца

Настройка межстрочного интервала может улучшить читаемость. Вот как это сделать:

```java
import com.aspose.cells.LineSpaceSizeType;

public class ExcelDemo {
    public static void main(String[] args) throws Exception {
        // Создать новую рабочую книгу (файл Excel)
        Workbook workbook = new Workbook();
        
        // Доступ к первому рабочему листу
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        // Добавьте на рабочий лист форму текстового поля.
        Shape textBox = sheet.getShapes().addShape(MsoDrawingType.TEXT_BOX, 2, 0, 2, 0, 100, 200);
        
        // Установить текстовое содержимое внутри фигуры
        textBox.setText("Sign up for your free phone number.\nCall and text online for free.");
        
        // Доступ ко второму абзацу в форме
        TextParagraph paragraph = textBox.getTextBody().getTextParagraphs().get(1);

        // Установить межстрочный интервал 20 пунктов.
        paragraph.setLineSpaceSizeType(LineSpaceSizeType.POINTS);
        paragraph.setLineSpace(20); 
        
        // Настройте пробелы до и после абзаца
        paragraph.setSpaceAfterSizeType(LineSpaceSizeType.POINTS);
        paragraph.setSpaceAfter(10);
        
        paragraph.setSpaceBeforeSizeType(LineSpaceSizeType.POINTS);
        paragraph.setSpaceBefore(10);

        System.out.println("Line spacing set.");
    }
}
```

### Сохранить рабочую книгу

Наконец, сохраните книгу с только что добавленным и отформатированным текстовым полем.

```java
import com.aspose.cells.SaveFormat;

public class ExcelDemo {
    public static void main(String[] args) throws Exception {
        // Создать новую рабочую книгу (файл Excel)
        Workbook workbook = new Workbook();
        
        // Доступ к первому рабочему листу
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        // Добавьте на рабочий лист форму текстового поля.
        Shape textBox = sheet.getShapes().addShape(MsoDrawingType.TEXT_BOX, 2, 0, 2, 0, 100, 200);
        
        // Установить текстовое содержимое внутри фигуры
        textBox.setText("Sign up for your free phone number.\nCall and text online for free.");
        
        // Доступ ко второму абзацу в форме
        TextParagraph paragraph = textBox.getTextBody().getTextParagraphs().get(1);

        // Установить межстрочный интервал 20 пунктов.
        paragraph.setLineSpaceSizeType(LineSpaceSizeType.POINTS);
        paragraph.setLineSpace(20); 
        
        // Настройте пробелы до и после абзаца
        paragraph.setSpaceAfterSizeType(LineSpaceSizeType.POINTS);
        paragraph.setSpaceAfter(10);
        
        paragraph.setSpaceBeforeSizeType(LineSpaceSizeType.POINTS);
        paragraph.setSpaceBefore(10);

        // Сохраните рабочую книгу
        workbook.save("StyledTextShape.xlsx", SaveFormat.XLSX);
    }
}
```

## Заключение

Вы успешно научились добавлять текстовое поле и устанавливать межстрочный интервал в книге Excel с помощью Aspose.Cells для Java. Это расширяет ваши возможности по созданию динамических, визуально привлекательных отчетов.

## Рекомендации по ключевым словам
- «Aspose.Cells для Java»
- «Добавить текстовое поле в Excel»
- «Установить межстрочный интервал в Excel»
- «Рабочая книга Excel со стилизованным текстом»
- «Java и Aspose.Cells»


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}