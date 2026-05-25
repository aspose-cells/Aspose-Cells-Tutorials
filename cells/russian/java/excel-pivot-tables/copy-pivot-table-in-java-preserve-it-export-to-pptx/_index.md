---
category: general
date: 2026-03-01
description: Копировать сводную таблицу в Java, сохраняя её структуру, затем экспортировать
  Excel в PPTX, отключить AutoFilter в Excel и использовать Smart Marker для массивов
  JSON — полное пошаговое руководство.
draft: false
keywords:
- copy pivot table
- preserve pivot table
- use smart marker
- disable excel autofilter
- export excel to pptx
language: ru
og_description: Копировать сводную таблицу в Java, сохранить определение сводной таблицы,
  экспортировать в PPTX, отключить AutoFilter и использовать Smart Marker — полное
  руководство для разработчиков.
og_title: Копировать сводную таблицу в Java — сохранить её, экспортировать в PPTX
tags:
- Aspose.Cells
- Java
- Excel Automation
title: Копировать сводную таблицу в Java — сохранить её, экспортировать в PPTX
url: /ru/java/excel-pivot-tables/copy-pivot-table-in-java-preserve-it-export-to-pptx/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Копировать сводную таблицу в Java – Сохранить её, экспортировать в PPTX

Когда‑нибудь нужно было **скопировать сводную таблицу** из одной книги в другую, не теряя исходное определение сводной? Вы не одиноки в этом. Во многих реальных проектах вам придётся перемещать данные, и последнее, чего вы хотите, — это сломанная сводная таблица, вызывающая ошибки во время выполнения.  

В этом руководстве мы пройдем полное решение, которое не только **скопирует сводную таблицу**, но и покажет, как **сохранить сводную таблицу** при копировании, **экспортировать Excel в PPTX**, **отключить AutoFilter в Excel** и **использовать smart marker**, чтобы поместить массив JSON в одну ячейку. К концу у вас будет единая исполняемая Java‑программа, охватывающая все четыре сценария.

## Требования

- Java 8 или новее (код также работает с Java 11)  
- библиотека Aspose.Cells for Java (версия 23.9 или новее) — её можно получить из Maven Central  
- базовое знакомство с концепциями Excel, такими как сводные таблицы, таблицы и текстовые поля  

Если у вас отсутствует JAR‑файл Aspose.Cells, добавьте следующее в ваш `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
</dependency>
```

Теперь давайте погрузимся.

## Шаг 1: Копировать сводную таблицу – Сохранение определения сводной

Если просто скопировать диапазон ячеек, содержащий сводную таблицу, метаданные сводной часто остаются позади. Aspose.Cells предоставляет удобный способ сохранить определение, используя `copyRange` с экземпляром `CopyOptions`.

```java
import com.aspose.cells.*;

public class PivotCopyDemo {

    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the source workbook that contains the pivot table
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/src.xlsx");
        Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);

        // 2️⃣ Define the range that includes the pivot (A1:G20 is just an example)
        Range pivotRange = sourceSheet.getCells().createRange("A1:G20");

        // 3️⃣ Prepare the destination workbook
        Workbook destWorkbook = new Workbook();
        Worksheet destSheet = destWorkbook.getWorksheets().get(0);

        // 4️⃣ Copy the range – the pivot definition travels with it
        destSheet.getCells().copyRange(pivotRange,
                new CellArea(0, 0, 19, 6), // destination area (rows 0‑19, cols 0‑6)
                new CopyOptions());

        // 5️⃣ Save the result
        destWorkbook.save("YOUR_DIRECTORY/dest.xlsx");
    }
}
```

**Почему это работает:** `CopyOptions` указывает Aspose.Cells перенести всё, включая кэш сводной и настройки полей. Без него вы получите только значения и потеряете возможность обновлять сводную.

**Пограничный случай:** Если ваша исходная сводная охватывает больше, чем жёстко заданный диапазон `A1:G20`, скорректируйте диапазон соответственно или используйте `sourceSheet.getPivotTables().get(0).getDataRange()` для динамического получения.

![Пример копирования сводной таблицы](image.png "Копирование сводной таблицы в Java")

*Текст изображения: диаграмма копирования сводной таблицы в Java*

## Шаг 2: Экспорт листа с редактируемым TextBox в PPTX

Часто требуется превратить лист Excel в слайд PowerPoint — например, еженедельные дашборды, которые нужно представить. Aspose.Cells может напрямую сохранить лист как файл PPTX, сохраняя такие формы, как текстовые поля.

```java
import com.aspose.cells.*;

public class ExportToPptxDemo {

    public static void main(String[] args) throws Exception {
        // Load workbook that contains a TextBox shape
        Workbook wb = new Workbook("YOUR_DIRECTORY/textbox.xlsx");

        // Export the first worksheet to PPTX
        wb.save("YOUR_DIRECTORY/output.pptx", SaveFormat.PPTX);

        System.out.println("Worksheet exported to PPTX successfully.");
    }
}
```

**Что происходит:** Метод `save` с параметром `SaveFormat.PPTX` преобразует весь лист, включая любой редактируемый TextBox, в слайд PowerPoint. Текст внутри поля остаётся редактируемым при открытии PPTX в PowerPoint.

**Подсказка:** Если у вас несколько листов и нужен только определённый, вызовите `wb.getWorksheets().removeAt(index)` для остальных перед сохранением.

## Шаг 3: Отключить AutoFilter в Excel для таблицы

AutoFilter удобен для конечных пользователей, но иногда его нужно отключить программно — возможно, перед экспортом данных или при создании чистого отчёта. Вот как **отключить excel autofilter** для таблицы Excel.

```java
import com.aspose.cells.*;

public class DisableAutoFilterDemo {

    public static void main(String[] args) throws Exception {
        Workbook wb = new Workbook("YOUR_DIRECTORY/textbox.xlsx");
        Worksheet sheet = wb.getWorksheets().get(0);

        // Assume the first table in the sheet is the target
        Table table = sheet.getTables().get(0);

        // Turn off the AutoFilter arrows
        table.setShowAutoFilter(false);

        // Save the modified workbook
        wb.save("YOUR_DIRECTORY/noFilter.xlsx");
        System.out.println("AutoFilter disabled and workbook saved.");
    }
}
```

**Зачем это может понадобиться:** При экспорте в форматы, не поддерживающие AutoFilter (например, CSV или PDF), могут появиться лишние значки фильтра. Отключение обеспечивает чистый вывод.

**Распространённая ошибка:** Если на листе нет таблиц, `getTables().get(0)` вызовет `IndexOutOfBoundsException`. В продакшн‑коде всегда проверяйте `sheet.getTables().size()` сначала.

## Шаг 4: Использовать Smart Marker – Вставить массив JSON как значение одной ячейки

Smart Marker — это шаблонизатор от Aspose. Один полезный приём — рассматривать весь массив JSON как значение одной ячейки, что идеально подходит для логирования или передачи структурированных данных дальше. Давайте **используем smart marker** для этого.

```java
import com.aspose.cells.*;

public class SmartMarkerDemo {

    public static void main(String[] args) throws Exception {
        Workbook wb = new Workbook("YOUR_DIRECTORY/textbox.xlsx");

        // Initialise the SmartMarker processor with the workbook
        SmartMarkerProcessor processor = new SmartMarkerProcessor(wb);

        // JSON array we want to embed
        String jsonArray = "[{\"Name\":\"John\",\"Age\":30},{\"Name\":\"Anna\",\"Age\":28}]";

        // Configure the processor to treat arrays as a single cell
        processor.setOptions(SmartMarkerOptions.ArrayAsSingle);

        // Apply the marker – assume cell A1 contains the marker ${json}
        processor.apply(jsonArray);

        // Save the result
        wb.save("YOUR_DIRECTORY/smartMarkerResult.xlsx");
        System.out.println("JSON array inserted via Smart Marker.");
    }
}
```

**Как это работает:** Маркер `${json}` в книге заменяется полной строкой JSON, потому что мы задали `ArrayAsSingle`. Без этой опции Aspose попытался бы развернуть каждый элемент массива в отдельные строки.

**Вариант:** Если нужен массив, разбитый по строкам, просто опустите `ArrayAsSingle`, и Smart Marker автоматически выполнит развертывание.

## Полный рабочий пример — все шаги вместе

Ниже приведён один Java‑класс, объединяющий все операции, которые мы рассмотрели. Запустите его как обычный метод `main`; просто скорректируйте пути к файлам под вашу среду.

```java
import com.aspose.cells.*;

public class CompleteExcelAutomation {

    public static void main(String[] args) throws Exception {
        // ----------- Step 1: Copy Pivot Table -----------
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/src.xlsx");
        Worksheet srcSheet = srcWb.getWorksheets

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}