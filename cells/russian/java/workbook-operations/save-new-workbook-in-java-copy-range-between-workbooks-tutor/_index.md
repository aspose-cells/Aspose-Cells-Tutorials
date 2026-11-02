---
category: general
date: 2026-07-29
description: Сохраните новую книгу в Java, копируя диапазон между книгами. Узнайте,
  как перенести диапазон Excel и сохранить форматирование при копировании за несколько
  шагов.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save new workbook
- copy range between workbooks
- transfer excel range
- load excel workbook java
- preserve formatting copy
language: ru
lastmod: 2026-07-29
og_description: Сохраните новую книгу в Java с Aspose.Cells — узнайте, как копировать
  диапазон между книгами, сохраняя форматирование, в лаконичном пошаговом руководстве.
og_image_alt: Java code that saves new workbook after transferring an Excel range
og_title: Сохранить новую рабочую книгу в Java – Копировать диапазон между рабочими
  книгами
schemas:
- author: Aspose
  dateModified: '2026-07-29'
  description: Save new workbook in Java while copy range between workbooks. Learn
    to transfer Excel range and preserve formatting copy in just a few steps.
  headline: Save New Workbook in Java – Copy Range Between Workbooks Tutorial
  type: TechArticle
tags:
- Java
- Excel
- Aspose.Cells
- Workbook
- File I/O
title: Сохранить новую рабочую книгу в Java – учебник по копированию диапазона между
  рабочими книгами
url: /ru/java/workbook-operations/save-new-workbook-in-java-copy-range-between-workbooks-tutor/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Сохранить новую Workbook в Java – Копировать диапазон между Workbook'ами Руководство

Когда‑нибудь вам нужно было **save new workbook** после перемещения данных из одного Excel‑файла в другой, но вы не были уверены, как сохранить оригинальное оформление? Вы не одиноки. Во многих корпоративных приложениях нам необходимо **transfer Excel range** из шаблона в файл, созданный пользователем, и трюк в том, чтобы убедиться, что форматирование сохраняется.

В этом руководстве мы пройдем полный, готовый к запуску пример, который **load Excel workbook java**‑style с использованием Aspose.Cells, **copy range between workbooks**, и наконец **save new workbook** со всеми оригинальными цветами, границами и числовыми форматами. Без лишних слов — только код, который вы можете сразу добавить в свой проект.

> **Pro tip:** Если вы уже используете Maven, добавьте зависимость Aspose.Cells один раз, и вы будете готовы к любой задаче по работе с workbook'ами.

## Предварительные требования

- Java 17 (или любой современный JDK)
- Aspose.Cells for Java (версия 23.10 или новее)
- Базовое знакомство с Java I/O
- Два Excel‑файла: исходный (`source.xlsx`) с данными, которые нужно переместить, и пустой целевой (`dest.xlsx`), который будет создан кодом

Теперь давайте перейдём к шагам.

## Шаг 1 – Загрузка Excel Workbook в стиле Java

Первое, что мы делаем, — **load Excel workbook java**‑wise. Aspose.Cells абстрагирует формат файла, поэтому вам не нужно беспокоиться о нижележащем XML.

```java
import com.aspose.cells.*;

public class ExcelRangeTransfer {
    public static void main(String[] args) throws Exception {
        // Load the source workbook (make sure the path is correct)
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
        // ------------------------------------------------------------
        // At this point the source workbook is fully loaded in memory.
        // ------------------------------------------------------------
```

*Почему это важно:* Загрузка workbook дает доступ ко всем листам, ячейкам и объектам стилей. Если пропустить этот шаг и попытаться копировать напрямую из файлового потока, вы потеряете возможность сохранять форматирование позже.

## Шаг 2 – Определить исходный диапазон (Preserve Formatting Copy)

Далее мы точно указываем область, которую хотим переместить. В нашем примере диапазон `A1:G20` содержит сводную таблицу и несколько строк заголовков. Создавая объект `Range`, мы позже можем сказать Aspose.Cells сохранить каждый стиль — это суть **preserve formatting copy**.

```java
        // Grab the first worksheet
        Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);

        // Define the range that includes the data we want to copy
        // Using createRange ensures we capture formulas, formats, and comments.
        Range sourceRange = sourceSheet.getCells().createRange("A1:G20");
```

*Подсказка:* Если нужно копировать динамическую область, можно вычислить последнюю использованную строку/столбец с помощью `sourceSheet.getCells().getMaxDataRow()` и сформировать строку адреса «на лету».

## Шаг 3 – Создать целевой Workbook (где мы сохраним новую Workbook)

Теперь мы создаём новый workbook, который получит данные. Здесь в конечном итоге произойдёт действие **save new workbook**.

```java
        // Create a brand‑new workbook that will become our destination file
        Workbook destinationWorkbook = new Workbook();

        // Get its first worksheet – this is where we’ll paste the range
        Worksheet destSheet = destinationWorkbook.getWorksheets().get(0);
```

*Почему мы создаём новый:* Начало с чистого workbook гарантирует отсутствие оставшихся стилей, которые могли бы конфликтовать с импортируемым диапазоном. Это также уменьшает итоговый размер файла, поскольку сохраняются только необходимые ресурсы.

## Шаг 4 – Копировать диапазон между Workbook'ами

Это сердце руководства: **copy range between workbooks** с сохранением всех визуальных элементов. Класс `CopyOptions` позволяет указать, что нам нужен полный копирующий режим, а не только значения.

```java
        // Set up copy options to keep everything—values, formulas, formats, comments.
        CopyOptions copyOptions = new CopyOptions();
        copyOptions.setPasteType(PasteType.ALL); // ensures formatting stays

        // Perform the copy. The destination starts at cell A1 (row 0, column 0).
        destSheet.getCells().copyRange(sourceRange, 0, 0, copyOptions);
```

*Распространённый вопрос:* *Что если нужны только значения без форматирования?* Замените `PasteType.ALL` на `PasteType.VALUES`, и форматирование будет проигнорировано.

## Шаг 5 – Сохранить новую Workbook

Наконец мы записываем целевой файл на диск. Это момент, когда мы действительно **save new workbook** и видим результат предыдущих шагов.

```java
        // Persist the destination workbook to the file system
        destinationWorkbook.save("YOUR_DIRECTORY/dest.xlsx");
        System.out.println("Destination workbook saved successfully.");
    }
}
```

Когда вы откроете `dest.xlsx`, вы увидите точно такой же внешний вид, как у оригинального диапазона `source.xlsx` — цвета, границы и числовые форматы полностью сохранены.

<img src="excel-copy.png" alt="Java‑код, сохраняющий новую Workbook после переноса диапазона Excel" />

## Полный рабочий пример (Все шаги вместе)

Ниже приведена полная, самодостаточная программа. Скопируйте её в файл с именем `ExcelRangeTransfer.java`, скорректируйте пути к файлам и запустите с помощью `javac`/`java`.

```java
import com.aspose.cells.*;

public class ExcelRangeTransfer {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the source workbook
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");

        // 2️⃣ Get the first worksheet and define the range we want to copy
        Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);
        Range sourceRange = sourceSheet.getCells().createRange("A1:G20");

        // 3️⃣ Create a fresh destination workbook
        Workbook destinationWorkbook = new Workbook();
        Worksheet destSheet = destinationWorkbook.getWorksheets().get(0);

        // 4️⃣ Copy the defined range – preserving formatting
        CopyOptions copyOptions = new CopyOptions();
        copyOptions.setPasteType(PasteType.ALL);
        destSheet.getCells().copyRange(sourceRange, 0, 0, copyOptions);

        // 5️⃣ Save new workbook to disk
        destinationWorkbook.save("YOUR_DIRECTORY/dest.xlsx");
        System.out.println("Destination workbook saved successfully.");
    }
}
```

**Ожидаемый вывод** при запуске программы:

```
Destination workbook saved successfully.
```

Откройте `dest.xlsx`, и вы увидите точную копию `A1:G20` из исходного файла, полностью со своим оригинальным оформлением.

## Часто задаваемые вопросы и особые случаи

| Вопрос | Ответ |
|----------|--------|
| *Можно ли копировать между workbook'ами, использующими разные версии Excel?* | Да. Aspose.Cells нормализует формат внутри, поэтому источник `.xls` можно скопировать в цель `.xlsx` без дополнительной работы. |
| *Что если в целевом файле уже есть данные?* | Используйте `copyRange` с другими начальной строкой/столбцом (например, `5, 2`), чтобы вставить в другое место, либо очистите лист сначала с помощью `destSheet.getCells().clearAll()`. |
| *Остаются ли формулы привязанными к оригинальному workbook?* | По умолчанию они становятся **relative** к целевому файлу. Если нужны внешние ссылки, установите `copyOptions.setPasteType(PasteType.FORMULAS)` и обработайте ссылки на workbook вручную. |
| *Как сохранить ширину столбцов?* | Ширина столбцов входит в формат; `PasteType.ALL` уже копирует её. Если заметны расхождения, вызовите `destSheet.autoFitColumns()` после копирования. |

## Следующие шаги – Выход за пределы основ

Теперь, когда вы знаете, как **save new workbook**, **copy range between workbooks** и **preserve formatting copy**, вы можете изучить:

- **Batch processing** – цикл по папке исходных файлов и генерация консолидированного отчёта.  
- **Conditional formatting transfer** – используйте `CopyOptions.setPasteType(PasteType.FORMATS)`, чтобы скопировать только стили.  
- **Streaming API** – для огромных файлов класс `Workbook` предлагает режим низкого потребления памяти, который всё ещё поддерживает копирование диапазонов.

Все эти темы естественно развивают концепции, представленные здесь, и вращаются вокруг одной основной идеи: манипулировать Excel‑файлами в Java уверенно и точно.

---

### TL;DR

Мы начали с **load excel workbook java**, определили **transfer excel range**, использовали **copy range between workbooks** с `CopyOptions` для **preserve formatting copy**, создали новый файл и, наконец, **save new workbook**. Результат — полностью рабочий `dest.xlsx`, который точно повторяет исходный диапазон до последнего стиля ячейки.

Попробуйте, измените адрес диапазона и посмотрите, как быстро можно автоматизировать задачи отчётности в Excel на Java. Happy coding!

## Что изучать дальше?

Следующие руководства охватывают тесно связанные темы, построенные на техниках, продемонстрированных в этом руководстве. Каждый ресурс включает полные рабочие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы в ваших проектах.

- [How to Implement a Named Range with Workbook Scope in Aspose.Cells Java for Enhanced Excel Data Management](/cells/english/java/tables-structured-references/implement-named-range-workbook-scope-aspose-cells-java/)
- [Save Excel Workbook with Aspose.Cells for Java – Complete Guide](/cells/english/java/automation-batch-processing/excel-workbook-automation-aspose-cells-java/)
- [Save Excel File Java with Aspose.Cells – Mastering Workbook Automation](/cells/english/java/automation-batch-processing/aspose-cells-java-excel-workbook-automation/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}