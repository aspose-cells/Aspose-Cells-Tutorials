---
title: Создание пользовательской проверки данных
linktitle: Создание пользовательской проверки данных
second_title: API обработки Java Excel Aspose.Cells
description: Узнайте, как создать пользовательскую проверку данных с помощью Aspose.Cells для Java. Пошаговое руководство с исходным кодом.
weight: 10
url: /ru/java/data-validation-rules/creating-custom-data-validation/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание пользовательской проверки данных


## Введение

Проверка данных помогает поддерживать целостность данных, не позволяя пользователям вводить неверные или недействительные данные в таблицы Excel. Хотя Excel предлагает встроенные параметры проверки данных, существуют сценарии, в которых вам необходимо определить пользовательские правила проверки. Aspose.Cells for Java позволяет вам эффективно достичь этого.

## Предпосылки

Прежде чем приступить к изучению кода, убедитесь, что у вас выполнены следующие предварительные условия:

-  Aspose.Cells для Java: Загрузите и установите библиотеку с сайта[здесь](https://releases.aspose.com/cells/java/).

## Шаг 1: Настройка вашего проекта Java

Чтобы начать, создайте новый проект Java в предпочитаемой вами интегрированной среде разработки (IDE). Добавьте библиотеку Aspose.Cells for Java в classpath вашего проекта.

## Шаг 2: Создание книги Excel

Начнем с создания новой книги Excel с помощью Aspose.Cells для Java.

```java
// Код Java для создания новой книги Excel
Workbook workbook = new Workbook();
```

## Шаг 3: Добавление рабочего листа

Теперь давайте добавим в книгу рабочий лист, к которому применим нашу пользовательскую проверку данных.

```java
// Код Java для добавления рабочего листа
Worksheet worksheet = workbook.getWorksheets().get(0);
```

## Шаг 4: Определение пользовательских критериев проверки

На этом этапе мы определим пользовательские критерии проверки, которым должны соответствовать наши данные. Допустим, мы хотим ограничить возраст, введенный в ячейку, диапазоном от 18 до 60 лет.

```java
// Код Java для определения пользовательских критериев проверки
Validation validation = worksheet.getValidations().add();
validation.setType(ValidationType.WHOLE);
validation.setOperator(OperatorType.BETWEEN);
validation.setFormula1("18");
validation.setFormula2("60");
validation.setShowError(true);
validation.setAlertStyle(ValidationAlertType.STOP);
validation.setErrorTitle("Invalid Age");
validation.setErrorMessage("Age must be between 18 and 60.");
```

## Шаг 5: Применение проверки данных к диапазону

Теперь, когда мы определили наши пользовательские критерии проверки, давайте применим их к определенному диапазону ячеек.

```java
// Код Java для применения проверки данных к диапазону
CellArea area = new CellArea();
area.startRow = 0;
area.startColumn = 0;
area.endRow = 9; // Применить проверку к первым десяти строкам
area.endColumn = 0;

validation.addArea(area);
```

## Шаг 6: Сохранение файла Excel

Наконец, сохраните файл Excel с примененными пользовательскими правилами проверки данных.

```java
// Код Java для сохранения файла Excel
workbook.save("CustomDataValidation.xlsx");
```

## Заключение

В этом уроке мы изучили, как создавать пользовательские правила проверки данных с помощью Aspose.Cells для Java. Выполняя эти шаги, вы можете гарантировать, что ваши данные Excel соответствуют определенным критериям, что повышает целостность и точность данных.

## Часто задаваемые вопросы

### Как загрузить Aspose.Cells для Java?

 Вы можете загрузить Aspose.Cells для Java с веб-сайта по адресу[здесь](https://releases.aspose.com/cells/java/).

### Можно ли применить пользовательскую проверку данных к нескольким диапазонам на одном листе?

Да, вы можете применить пользовательскую проверку данных к нескольким диапазонам на одном листе, повторив шаг 5 для каждого требуемого диапазона.

### Поддерживаются ли другие типы проверки данных в Aspose.Cells для Java?

Да, Aspose.Cells для Java поддерживает различные типы проверки данных, включая целые числа, десятичные дроби, дату, время, длину текста и многое другое.

### Как настроить сообщение об ошибке, отображаемое при сбое проверки данных?

 Вы можете настроить сообщение об ошибке, изменив`setErrorMessage` метод на шаге 4, где вы определяете критерии проверки.

### Работает ли Aspose.Cells for Java с файлами Excel разных форматов?

Да, Aspose.Cells для Java поддерживает широкий спектр форматов файлов Excel, включая XLS, XLSX, XLSM и другие.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
