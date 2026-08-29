---
category: general
date: 2026-08-20
description: Научитесь экспортировать Excel в TXT, ограничивая количество знаков после
  запятой, сохраняя значимые цифры и сохранять книгу в формате TXT с помощью Java.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to txt
- limit decimal places
- keep significant digits
- save workbook as txt
language: ru
lastmod: 2026-08-20
og_description: Экспорт Excel в TXT с помощью Aspose.Cells. Это руководство показывает,
  как ограничить количество знаков после запятой, сохранить значимые цифры и сохранить
  рабочую книгу в формате TXT на Java.
og_image_alt: Result of export excel to txt showing limited decimal places and kept
  significant digits
og_title: Экспорт Excel в TXT на Java – контроль количества знаков после запятой и
  значимых цифр
schemas:
- author: Aspose
  dateModified: '2026-08-20'
  description: Learn to export Excel to TXT while limiting decimal places, keeping
    significant digits, and saving workbook as TXT using Java.
  headline: How to export Excel to TXT with Aspose.Cells and control decimal precision
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel
- Text export
title: Как экспортировать Excel в TXT с помощью Aspose.Cells и контролировать точность
  десятичных знаков
url: /ru/java/excel-import-export/how-to-export-excel-to-txt-with-aspose-cells-and-control-dec/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как экспортировать Excel в TXT с помощью Aspose.Cells и контролировать точность десятичных знаков

Если вам нужно **экспортировать Excel в TXT** и гарантировать, что вывод будет соответствовать определённому количеству десятичных знаков, это руководство предоставляет полное решение. Вы увидите, как ограничить количество десятичных знаков, сохранить значимые цифры и **сохранить книгу как TXT** с помощью библиотеки Aspose.Cells для Java.

В учебнике рассматривается создание книги, вставка значения высокой точности, настройка параметров сохранения TXT и запись файла на диск. К концу вы сможете генерировать текстовый файл, содержащий именно ту точность, которая вам нужна, без ручной пост‑обработки.

## Что понадобится

- Java 17 (или любой поддерживаемый JDK)
- Aspose.Cells for Java 23.10 или новее
- IDE или система сборки (Maven/Gradle) для управления зависимостями
- Права записи в целевой каталог

## Шаг 1: Создать книгу и получить доступ к первому листу

Создание книги — первый шаг, когда вы хотите **экспортировать Excel в TXT**. Класс `Workbook` представляет весь файл Excel, а `Worksheet` даёт доступ к ячейкам.

```java
import com.aspose.cells.*;

public class ExportExcelToTxtDemo {
    public static void main(String[] args) throws Exception {
        // Initialize a new workbook
        Workbook workbook = new Workbook();

        // Get the first worksheet (index 0)
        Worksheet sheet = workbook.getWorksheets().get(0);
```

*Почему это важно*: объект книги содержит все данные, стили и метаданные. Начало с новой книги гарантирует, что скрытое форматирование не будет влиять на экспорт текста.

## Шаг 2: Добавить числовое значение и ограничить десятичные знаки

Вставьте число с большим количеством десятичных знаков, чтобы продемонстрировать, как **ограничить десятичные знаки** при экспорте.

```java
        // Put a high‑precision number into cell A1
        sheet.getCells().putValue("A1", 0.000123456789);
```

*Почему это важно*: Excel хранит полную точность, но при последующем экспорте вы можете захотеть усечь или округлить значение. Параметр `limit decimal places` выполнит это автоматически.

## Шаг 3: Настроить параметры сохранения TXT для сохранения значимых цифр

Aspose.Cells предоставляет `TxtSaveOptions`. Установка `significantDigits` сообщает экспортеру сохранять только требуемое количество значимых цифр, игнорируя ведущие нули.

```java
        // Configure TXT export options
        TxtSaveOptions txtOptions = new TxtSaveOptions();

        // Keep exactly 5 significant digits (e.g., 0.00012346)
        txtOptions.setSignificantDigits(5);
```

*Почему это важно*: опция **keep significant digits** гарантирует, что выходной файл будет содержать предсказуемое количество точности, что необходимо для downstream‑систем, ожидающих фиксированный числовой формат.

## Шаг 4: Сохранить книгу как TXT

Наконец, запишите книгу в текстовый файл. Метод `save` учитывает настроенные параметры, поэтому полученный файл будет содержать ограниченное десятичное представление.

```java
        // Define the output path (replace with your own directory)
        String outputPath = "output/SignificantDigits.txt";

        // Export the workbook to TXT using the configured options
        workbook.save(outputPath, txtOptions);

        System.out.println("Export completed: " + outputPath);
    }
}
```

*Почему это важно*: использование **save workbook as txt** с подготовленными `TxtSaveOptions` гарантирует, что экспортированный файл соответствует ограничениям точности, заданным на предыдущем шаге.

### Ожидаемое содержимое `SignificantDigits.txt`

```
0.00012346
```

Значение показывает пять значимых цифр (`12346`) после округления, а ведущие нули сохраняются согласно формату TXT.

## Вариации и граничные случаи

| Сценарий | Корректировка |
|----------|---------------|
| **Другое количество значимых цифр** | Вызовите `txtOptions.setSignificantDigits(n)`, где `n` от 1 до 15. |
| **Экспорт диапазона вместо всего листа** | Используйте `txtOptions.setExportRange("A1:B10")` перед сохранением. |
| **Сохранение разделителей столбцов** | Установите `txtOptions.setSeparator('\t')` для табуляции. |
| **Большие листы** | Увеличьте `txtOptions.setMemorySetting(MemorySetting.MEMORY_PREFERENCES)`, чтобы избежать `OutOfMemoryError`. |

## Распространённые подводные камни и профессиональные советы

- **Не путайте значимые цифры с десятичными знаками**. Ведущие нули не считаются значимыми; используйте `setSignificantDigits` для смысловой точности и `setDecimalPlaces`, если нужен фиксированный набор цифр после запятой.
- **Всегда указывайте абсолютный путь вывода** при запуске из IDE, чтобы избежать ошибок доступа.
- **Проверьте сгенерированный файл** с помощью простого вызова `java.nio.file.Files.readAllLines(Paths.get(outputPath))`, чтобы убедиться, что содержимое соответствует ожиданиям перед передачей в downstream‑процессы.

## Полный исходный код для справки

```java
import com.aspose.cells.*;

public class ExportExcelToTxtDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.getWorksheets().get(0);

        // Step 2: Insert a high‑precision number (will be limited later)
        sheet.getCells().putValue("A1", 0.000123456789);

        // Step 3: Set TXT options – keep 5 significant digits
        TxtSaveOptions txtOptions = new TxtSaveOptions();
        txtOptions.setSignificantDigits(5);   // keep significant digits

        // Step 4: Save the workbook as TXT
        String outputPath = "output/SignificantDigits.txt";
        workbook.save(outputPath, txtOptions);

        System.out.println("Export completed: " + outputPath);
    }
}
```

Запуск программы создаёт `SignificantDigits.txt` с единственной строкой `0.00012346`, демонстрируя, что процесс **export excel to txt** учитывает как **limit decimal places**, так и **keep significant digits**.

## Заключение

Теперь вы знаете, как **экспортировать Excel в TXT** с помощью Aspose.Cells для Java, контролируя числовую точность. Настраивая `TxtSaveOptions`, вы можете **ограничить десятичные знаки**, **сохранить значимые цифры** и надёжно **сохранить книгу как txt** без дополнительной пост‑обработки.

Далее вы можете изучить:

- Экспорт нескольких листов в отдельные TXT‑файлы (`save workbook as txt` для каждого листа)
- Использование `setSeparator` для создания CSV‑совместимого вывода
- Автоматизацию пакетных конвертаций для больших наборов данных

Не стесняйтесь экспериментировать с различным количеством цифр и разделителями, чтобы точно соответствовать требованиям вашего проекта. Приятного кодинга!

## Что стоит изучить дальше?

Следующие учебники охватывают тесно связанные темы, расширяющие техники, продемонстрированные в этом руководстве. Каждый ресурс включает полностью рабочие примеры кода с пошаговыми объяснениями, помогая вам освоить дополнительные возможности API и исследовать альтернативные подходы в собственных проектах.

- [Как создать и экспортировать Excel в HTML с помощью Aspose.Cells Java | Руководство по операциям с книгой](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)
- [Сохранить Excel как текст – Полное руководство C# по экспорту Excel в TXT](/cells/english/net/converting-excel-files-to-other-formats/save-excel-as-text-complete-c-guide-to-export-excel-to-txt/)
- [Экспорт книги Excel как изображения с помощью Aspose.Cells for Java: Пошаговое руководство](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}