---
category: general
date: 2026-08-20
description: Узнайте, как экспортировать диаграмму в docx и преобразовать книгу Excel
  в docx с помощью Aspose.Cells в Java. Пошаговое руководство с полным кодом.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export chart to docx
- convert excel workbook to docx
- Aspose.Cells Java
- editable chart DOCX
- Excel to Word conversion
language: ru
lastmod: 2026-08-20
og_description: Экспортировать диаграмму в docx и преобразовать книгу Excel в docx
  с помощью Aspose.Cells для Java. Следуйте этому полному, готовому к выполнению руководству.
og_image_alt: Screenshot showing a Java code editor exporting an Excel chart to a
  DOCX file
og_title: Экспорт диаграммы в docx с Aspose.Cells – руководство по Java
schemas:
- author: Aspose
  dateModified: '2026-08-20'
  description: Learn how to export chart to docx and convert Excel workbook to docx
    with Aspose.Cells in Java. Step‑by‑step guide with complete code.
  headline: How to export chart to docx from Excel using Aspose.Cells for Java
  type: TechArticle
tags:
- Aspose.Cells
- Java
- DOCX
- Excel
title: Как экспортировать диаграмму в docx из Excel с помощью Aspose.Cells для Java
url: /ru/java/integration-interoperability/how-to-export-chart-to-docx-from-excel-using-aspose-cells-fo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Экспорт диаграммы в docx из рабочей книги Excel с помощью Java

Если вам нужно **export chart to docx** напрямую из файла Excel, этот учебник покажет готовое решение. К концу руководства вы также узнаете, как **convert Excel workbook to docx**, сохраняя редактируемую диаграмму, чтобы полученный документ Word можно было изменять без потери точности.

Экспорт диаграмм часто требуется при создании отчетов, комбинирующих расчеты в таблицах со сложными макетами Word. Aspose.Cells for Java упрощает конвертацию, а API позволяет сохранять диаграмму редактируемой — без статического изображения.

## Что рассматривается в этом учебнике

* Загрузка существующей рабочей книги, содержащей диаграмму.  
* Настройка `ImageOrPrintOptions` для целевого формата DOCX.  
* Включение флага `ExportEditableCharts` (доступно, начиная с версии 25.10).  
* Сохранение рабочей книги как файла DOCX, сохраняющего редактируемую диаграмму.  

Для этого не требуется никаких внешних инструментов, кроме JAR‑файла Aspose.Cells. Код работает с Java 8+ и любой недавней версией Aspose.Cells.

## Требования

| Требование | Почему это важно |
|-------------|----------------|
| **Aspose.Cells for Java** (v25.10 or later) | Функция `setExportEditableCharts` была введена в этом выпуске. |
| **Java Development Kit (JDK) 8 or newer** | Обеспечивает среду выполнения для компиляции и выполнения примера. |
| **An Excel workbook (`.xlsx`) that contains at least one chart** | Диаграмма — объект, который будет экспортирован в DOCX. |
| **A Java IDE or build tool (e.g., Maven, Gradle)** | Упрощает управление зависимостями и выполнение. |

Вы можете скачать последнюю версию Aspose.Cells JAR с [веб‑сайта Aspose](https://products.aspose.com/cells/java/).

## Шаг 1: Настройте проект и добавьте зависимость Aspose.Cells

Если вы используете Maven, добавьте следующую зависимость в ваш `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.10</version> <!-- use the latest version -->
</dependency>
```

Для Gradle добавьте:

```gradle
implementation 'com.aspose:aspose-cells:25.10'
```

> **Pro tip:** Используйте точную версию, в которой была введена `ExportEditableCharts` (25.10) или любую более новую. Более старые версии игнорируют флаг и создают статическое изображение.

## Шаг 2: Загрузите рабочую книгу, содержащую диаграмму

Класс `Workbook` представляет весь файл Excel. Его загрузка выполняется одной строкой:

```java
import com.aspose.cells.*;

public class ExportEditableChartToDocx {
    public static void main(String[] args) throws Exception {
        // Load the workbook with the chart you want to export
        Workbook workbook = new Workbook("YOUR_DIRECTORY/ChartWorkbook.xlsx");
```

> **Почему это важно:** Рабочая книга должна быть полностью загружена, прежде чем вы сможете применить любые параметры экспорта. Если путь к файлу неверен, Aspose.Cells бросает `FileNotFoundException`.

## Шаг 3: Настройте параметры image/print для вывода в DOCX

`ImageOrPrintOptions` управляет тем, как рендерится рабочая книга. Установка формата сохранения в `DOCX` сообщает Aspose.Cells создавать документ Word вместо изображения.

```java
        // Create options and specify DOCX as the target format
        ImageOrPrintOptions options = new ImageOrPrintOptions();
        options.setSaveFormat(SaveFormat.DOCX);
```

Вы также можете настроить размер страницы, DPI или качество изображения, но они необязательны для экспорта диаграмм.

## Шаг 4: Включите экспорт редактируемых диаграмм

Начиная с версии 25.10, Aspose.Cells может встраивать диаграммы как нативные объекты диаграмм Word. Это делает их полностью редактируемыми в Microsoft Word.

```java
        // Turn on the editable chart export flag
        options.setExportEditableCharts(true);
```

> **Edge case:** Если установить этот флаг в `false` (или опустить его), диаграмма будет отрисована как статическое изображение. Используйте `true` только тогда, когда целевая аудитория должна иметь возможность редактировать диаграмму после конвертации.

## Шаг 5: Сохраните рабочую книгу как файл DOCX

Наконец, вызовите `Workbook.save` с настроенными параметрами:

```java
        // Save the workbook as a DOCX document that contains an editable chart
        workbook.save("YOUR_DIRECTORY/ChartEditable.docx", options);
    }
}
```

Когда программа завершится, откройте `ChartEditable.docx` в Microsoft Word. Вы должны увидеть оригинальную диаграмму, и при щелчке правой кнопкой мыши будет доступна опция **Edit Data** — подтверждающая, что диаграмма действительно редактируемая.

## Полный, исполняемый пример

Ниже приведён полный исходный файл. Скопируйте его в свою IDE, замените `YOUR_DIRECTORY` на абсолютный или относительный путь и запустите.

```java
import com.aspose.cells.*;

public class ExportEditableChartToDocx {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the workbook that contains the chart
        Workbook workbook = new Workbook("YOUR_DIRECTORY/ChartWorkbook.xlsx");

        // Step 2: Create image/print options and set the target format to DOCX
        ImageOrPrintOptions options = new ImageOrPrintOptions();
        options.setSaveFormat(SaveFormat.DOCX);

        // Step 3: Enable exporting of editable charts (available from version 25.10)
        options.setExportEditableCharts(true);

        // Step 4: Save the workbook as a DOCX document with the configured options
        workbook.save("YOUR_DIRECTORY/ChartEditable.docx", options);
    }
}
```

**Ожидаемый результат**

* Файл с именем `ChartEditable.docx` в указанном каталоге.  
* Открывая файл в Word, вы видите диаграмму точно такой же, как в Excel, и можете двойным щелчком редактировать её серии данных.

## Распространённые подводные камни и как их избежать

| Симптом | Причина | Решение |
|---------|---------|---------|
| Word показывает **static image** вместо редактируемой диаграммы | `setExportEditableCharts` не вызван или используется версия < 25.10 | Убедитесь, что флаг установлен в `true` и вы используете Aspose.Cells 25.10 или новее. |
| Сгенерированный DOCX **пустой** | Неправильный путь к исходной рабочей книге или недостаточные права | Проверьте путь к рабочей книге и наличие прав чтения/записи. |
| Макет диаграммы выглядит **искажённым** | Настройки страницы в Excel (например, скрытые строки/столбцы) отличаются от стандартных в Word | Отрегулируйте `ImageOrPrintOptions` (например, `setOnePagePerSheet(true)`) для контроля масштабирования. |
| **Performance** ухудшается при больших рабочих книгах | Экспорт большого количества диаграмм или больших наборов данных | Экспортируйте только необходимые листы или используйте `setSheetIndex` для ограничения обработки. |

## Расширение решения

* **Multiple charts:** Переберите все листы и вызовите `worksheet.getCharts()`, чтобы экспортировать каждую диаграмму отдельно.  
* **Custom DOCX styling:** После сохранения используйте Aspose.Words для применения заголовков, колонтитулов или стилей к сгенерированному документу.  
* **Batch conversion:** Оберните код в цикл, который обрабатывает каталог файлов `.xlsx`, создавая DOCX для каждого.

## Заключение

Теперь у вас есть надёжный метод для **export chart to docx** и **convert Excel workbook to docx**, сохраняющий полную редактируемость диаграммы. Ключевые шаги: загрузка рабочей книги, настройка `ImageOrPrintOptions` для DOCX, включение `ExportEditableCharts` и сохранение результата.

Экспериментируйте с дополнительными параметрами — например, задавая поля страницы или встраивая формулы рабочей книги — чтобы адаптировать вывод под ваш процесс создания отчетов. Когда необходимо программно генерировать отчёты Word из данных Excel, этот подход предоставляет чистое, поддерживаемое решение.

--- 

*Готовы попробовать? Склонируйте пример, обновите пути к файлам и запустите программу. Если возникнут проблемы, обратитесь к документации Aspose.Cells for Java или изучите связанные темы ниже.*  

### Связанные темы, которые вы можете изучить дальше

* **convert excel workbook to pdf** – генерировать PDF‑отчёты из той же рабочей книги.  
* **Aspose.Cells chart formatting** – настраивать цвета, маркеры и оси перед экспортом.  
* **Embedding images in DOCX with Aspose.Words** – комбинировать диаграммы с другим содержимым Word.  

Удачной разработки!

## Что вам следует изучить дальше?

Следующие учебники охватывают тесно связанные темы, которые опираются на техники, продемонстрированные в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и изучить альтернативные подходы к реализации в ваших проектах.

- [Как создать диаграмму Excel с линией тренда и экспортировать в изображение с помощью Aspose.Cells for Java](/cells/english/java/advanced-excel-charts/trendline-analysis/)
- [Автоматизация доступа к диаграммам Excel с помощью Aspose.Cells Java: пошаговое руководство](/cells/english/java/charts-graphs/excel-charts-access-aspose-cells-java/)
- [Настройка подписей данных диаграмм Excel с помощью Aspose.Cells for Java: пошаговое руководство](/cells/english/java/charts-graphs/customize-chart-data-labels-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}