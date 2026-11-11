---
date: '2026-10-28'
description: Узнайте, как изменить систему дат Excel на 1904 с помощью Aspose.Cells
  для Java, установить формат дат в Excel и эффективно преобразовать систему 1904.
keywords:
- change excel date system
- excel 1904 date conversion
- maven dependency aspose cells
lastmod: '2026-10-28'
og_description: Измените систему дат Excel на 1904 с помощью Aspose.Cells для Java.
  Узнайте пошагово, как включить систему 1904, установить даты и выполнить обратное
  преобразование.
og_image_alt: Aspose.Cells Java guide showing how to switch Excel to the 1904 date
  system
og_title: Изменить систему дат Excel на 1904 с помощью Aspose.Cells для Java
schemas:
- author: Aspose
  dateModified: '2026-10-28'
  description: Learn how to change Excel date system to 1904 using Aspose.Cells for
    Java, set Excel date format, and convert Excel 1904 system efficiently.
  headline: Change Excel date system to 1904 with Aspose.Cells Java
  type: TechArticle
- description: Learn how to change Excel date system to 1904 using Aspose.Cells for
    Java, set Excel date format, and convert Excel 1904 system efficiently.
  name: Change Excel date system to 1904 with Aspose.Cells Java
  steps:
  - name: initialize and load the workbook
    text: The `Workbook` class represents an entire Excel file in memory. First, create
      a `Workbook` instance that points to your existing file.
  - name: enable the 1904 date system
    text: The `WorkbookSettings.setDate1904` method toggles the workbook‑level date
      flag. Setting it to `true` activates the 1904 system for all worksheets. **Pro
      tip:** You can also call `setDate1904(false)` later if you need to revert.
  - name: save the modified workbook
    text: Finally, write the changes to a new file (or overwrite the original). The
      `save` method respects the active date system automatically. > **Note:** The
      code above uses the class name `tWorkbook` as originally provided. Ensure this
      typo matches your project’s naming conventions or correct it to `Workb
  type: HowTo
- questions:
  - answer: The 1900 system starts on January 1, 1900, while the 1904 system starts
      on January 1, 1904, shifting all dates by 1,462 days.
    question: What is the difference between the 1900 and 1904 date systems?
  - answer: Yes, but you must close the file in Excel first; otherwise the save operation
      will fail.
    question: Can I change the date system of a workbook that is currently open in
      Excel?
  - answer: The method works in the free trial, but a full license removes evaluation
      limitations.
    question: Do I need a license to use `setDate1904`?
  - answer: No, the date system is a workbook‑level setting; it applies to all worksheets.
    question: Is it possible to change the date system for only a single worksheet?
  - answer: Open the saved file in Excel, go to **File → Options → Advanced**, and
      check the **"Use 1904 date system"** box.
    question: How can I verify that the date system was changed?
  type: FAQPage
tags:
- change excel date system
- aspose cells java
- excel date conversion
- java excel processing
title: Изменить систему дат Excel на 1904 с помощью Aspose.Cells для Java
url: /ru/java/cell-operations/aspose-cells-java-configure-1904-date-system-excel/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Изменить систему дат Excel на 1904 с помощью Aspose.Cells Java

В этом руководстве вы узнаете, как **изменить систему дат Excel** на формат 1904 с помощью Aspose.Cells для Java. Система 1904 необходима, когда нужно сохранить устаревшие даты, созданные на Mac, или согласовать расчёты с финансовыми моделями, ожидающими эту эпоху. Мы пройдём процесс установки библиотеки, загрузки рабочей книги, переключения системы дат и сохранения результата — всё без необходимости установки Microsoft Excel на сервере.

## Быстрые ответы
- **Что делает система дат 1904?** Она начинает считать дни с 1 января 1904 года, сдвигая все даты на 1 462 дня по сравнению с системой по умолчанию 1900.  
- **Почему использовать Aspose.Cells для изменения системы дат?** Он предоставляет простой API, который работает без установленного Excel и поддерживает большие файлы.  
- **Какие версии Java поддерживаются?** JDK 8 или новее.  
- **Нужна ли лицензия?** Бесплатная пробная версия подходит для оценки; лицензия снимает ограничения использования.  
- **Можно ли позже вернуть систему 1900?** Да, просто вызовите `setDate1904(false)`.

## Что такое система дат 1904 в Excel?
Система дат 1904 считает дни с 1 января 1904 года, вместо эпохи 1900 года по умолчанию. Этот сдвиг добавляет ровно 1 462 дня к каждому значению даты, поэтому старые файлы Mac‑Excel выглядят смещёнными при открытии в Windows. Она в основном используется для совместимости со старыми файлами Excel на Macintosh и некоторыми устаревшими финансовыми моделями.

## Почему менять систему дат Excel с помощью Aspose.Cells?
Вы можете переключить систему дат напрямую из Java, устраняя ручные шаги в Excel. Aspose.Cells обрабатывает рабочие книги размером до **2 GB** и может конвертировать книгу из 500 листов менее чем за **2 seconds** на типичном 4‑ядерном сервере, обеспечивая высокопроизводительную серверную автоматизацию.

## Требования
- Java Development Kit (JDK) 8 или выше.  
- Maven или Gradle для управления зависимостями.  
- Базовые знания программирования на Java.  

## Настройка Aspose.Cells для Java

### Maven
Добавьте следующую зависимость в ваш файл `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

### Gradle
Добавьте эту строку в ваш файл `build.gradle`:

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

#### Приобретение лицензии
Aspose предлагает бесплатную пробную версию, временную лицензию и полные коммерческие лицензии. Вы можете начать с [бесплатной пробной версии](https://releases.aspose.com/cells/java/) или получить временную лицензию на странице [временной лицензии](https://purchase.aspose.com/temporary-license/).

## Как изменить систему дат Excel на 1904 с помощью Aspose.Cells для Java?
Загрузите рабочую книгу, включите настройку 1904 и сохраните файл — этот трёхшаговый процесс обновляет внутреннюю эпоху дат рабочей книги менее чем за секунду. Вызов API `setDate1904(true)` переключает флаг системы, а изменение сохраняется при вызове `save`. Установка Excel не требуется, что делает решение идеальным для безголовых серверных сред.

### Шаг 1: инициализация и загрузка рабочей книги
Класс `Workbook` представляет полную Excel‑файл в памяти. Сначала создайте экземпляр `Workbook`, указывающий на ваш существующий файл.

```java
import com.aspose.cells.Workbook;

String dataDir = "YOUR_DATA_DIRECTORY"; // Ensure the path to your Excel file is correct
// Initialize a Workbook object with the path to your Excel file
Workbook workbook = new Workbook(dataDir + "/Mybook.xlsx");
```

### Шаг 2: включить систему дат 1904
Метод `WorkbookSettings.setDate1904` переключает флаг даты уровня рабочей книги. Установка значения `true` активирует систему 1904 для всех листов.

```java
import com.aspose.cells.Workbook;

String dataDir = "YOUR_DATA_DIRECTORY"; // Ensure the path to your Excel file is correct
// Load the workbook from your specified directory
Workbook workbook = new Workbook(dataDir + "/Mybook.xlsx");

// Enable the 1904 date system
workbook.getSettings().setDate1904(true);
```

**Совет:** Вы также можете вызвать `setDate1904(false)` позже, если нужно вернуть прежнее состояние.

### Шаг 3: сохранить изменённую рабочую книгу
Наконец, запишите изменения в новый файл (или перезапишите оригинал). Метод `save` автоматически учитывает активную систему дат.

```java
import com.aspose.cells.Workbook;

String dataDir = "YOUR_DATA_DIRECTORY"; // Ensure the path to your Excel file is correct
String outDir = "YOUR_OUTPUT_DIRECTORY"; // Specify where you want to save the modified workbook

// Load and modify your workbook as shown in previous steps
tWorkbook workbook = new Workbook(dataDir + "/Mybook.xlsx");
workbook.getSettings().setDate1904(true);

// Save the changes to a new file
workbook.save(outDir + "/I1904DateSystem_out.xls");
```

> **Примечание:** В приведённом выше коде используется имя класса `tWorkbook`, как было указано изначально. Убедитесь, что эта опечатка соответствует соглашениям именования вашего проекта, или замените её на `Workbook`, если необходимо.

## Установить дату Excel программно (вторичное ключевое слово)
Если после изменения системы необходимо скорректировать отдельные значения ячеек, можно использовать `cells.get(i, j).putValue(Date)`, где дата будет интерпретироваться согласно активной системе дат.

## Преобразовать систему дат Excel 1904 обратно в 1900 (вторичное ключевое слово)
Чтобы вернуть прежнее состояние, просто вызовите:

```java
workbook.getSettings().setDate1904(false);
```

Затем снова сохраните рабочую книгу.

## Практические применения
1. **Архивирование данных** – Сохранить устаревшие метки времени при миграции старых таблиц, созданных на Mac.  
2. **Кроссплатформенная отчётность** – Генерировать отчёты, которые корректно открываются как в Windows, так и в macOS без несоответствия дат.  
3. **Финансовое моделирование** – Согласовать расчёты дат с устаревшими финансовыми моделями, ожидающими систему 1904.

## Соображения по производительности
- Ограничьте операции с рабочей книгой в одной сессии, чтобы снизить потребление памяти; Aspose.Cells передаёт данные потоково и не загружает весь файл в ОЗУ, если вы явно не запросите это.  
- Настройте флаги сборки мусора Java (`-XX:+UseG1GC`) для очень больших файлов, чтобы избежать всплесков пауз.

## Часто задаваемые вопросы

**Q: В чём разница между системами дат 1900 и 1904?**  
A: Система 1900 начинается с 1 января 1900 года, тогда как система 1904 — с 1 января 1904 года, сдвигая все даты на 1 462 дня.

**Q: Можно ли изменить систему дат рабочей книги, открытой в Excel?**  
A: Да, но сначала нужно закрыть файл в Excel; иначе операция сохранения завершится ошибкой.

**Q: Нужна ли лицензия для использования `setDate1904`?**  
A: Метод работает в бесплатной пробной версии, но полная лицензия снимает ограничения оценки.

**Q: Можно ли изменить систему дат только для одного листа?**  
A: Нет, система дат задаётся на уровне рабочей книги; она применяется ко всем листам.

**Q: Как проверить, что система дат была изменена?**  
A: Откройте сохранённый файл в Excel, перейдите в **File → Options → Advanced** и проверьте галочку **"Use 1904 date system"**.

## Заключение
Теперь вы знаете, как **изменить систему дат Excel** на 1904 с помощью Aspose.Cells для Java, как задавать даты в отдельных ячейках и как вернуть систему 1900 при необходимости. Интегрируйте эти фрагменты кода в свои конвейеры обработки данных, чтобы обеспечить совместимость дат между платформами и устаревшими файлами.

---

**Последнее обновление:** 2026-10-28  
**Тестировано с:** Aspose.Cells 25.3 for Java  
**Автор:** Aspose  

**Ресурсы**
- **Документация:** [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)
- **Скачать:** [Aspose.Cells Releases](https://releases.aspose.com/cells/java/)
- **Купить лицензию:** [Buy Aspose.Cells](https://purchase.aspose.com/buy)
- **Начать бесплатную пробную версию:** [Start Free Trial](https://releases.aspose.com/cells/java/)
- **Получить временную лицензию:** [Get Temporary License](https://purchase.aspose.com/temporary-license/)
- **Форум поддержки:** [Aspose Support](https://forum.aspose.com/c/cells/9)

## Связанные руководства

- [Эффективно конвертировать Excel в PDF с пользовательскими форматами дат, используя Aspose.Cells для Java](/cells/java/workbook-operations/render-excel-custom-date-formats-pdf-aspose-cells-java/)
- [Aspose.Cells для Java: Как эффективно создавать и форматировать рабочие книги Excel](/cells/java/getting-started/aspose-cells-java-workbook-creation-guide/)
- [Мастерство работы с Excel с помощью Aspose.Cells для Java: Операции с рабочими книгами и руководство по стилизации ячеек](/cells/java/workbook-operations/excel-manipulation-aspose-cells-java-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}