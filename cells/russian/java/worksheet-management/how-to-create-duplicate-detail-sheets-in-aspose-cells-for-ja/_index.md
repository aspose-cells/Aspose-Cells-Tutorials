---
category: general
date: 2026-08-17
description: Узнайте, как создавать дублирующие листы деталей с помощью Aspose.Cells
  для Java и разрешать дублирование имён листов, используя SmartMarkerProcessor.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create duplicate detail sheets
- allow duplicate sheet names
language: ru
lastmod: 2026-08-17
og_description: Создайте дублирующие листы деталей в Aspose.Cells для Java и разрешите
  дублирование имён листов. Следуйте этому полному руководству для мгновенных результатов.
og_image_alt: Generated Excel workbook showing multiple detail sheets with the same
  name
og_title: Создание дублирующих листов деталей в Aspose.Cells для Java – пошаговое
  руководство
schemas:
- author: Aspose
  dateModified: '2026-08-17'
  description: Learn how to create duplicate detail sheets with Aspose.Cells for Java
    and allow duplicate sheet names using SmartMarkerProcessor.
  headline: How to create duplicate detail sheets in Aspose.Cells for Java
  type: TechArticle
- description: Learn how to create duplicate detail sheets with Aspose.Cells for Java
    and allow duplicate sheet names using SmartMarkerProcessor.
  name: How to create duplicate detail sheets in Aspose.Cells for Java
  steps:
  - name: Load the master template workbook.
    text: Load the master template workbook.
  - name: Configure `SmartMarkerProcessor` to **allow duplicate sheet names**.
    text: Configure `SmartMarkerProcessor` to **allow duplicate sheet names**.
  - name: Process the workbook so that a new detail sheet is created for each data
      group.
    text: Process the workbook so that a new detail sheet is created for each data
      group.
  - name: Save the resulting workbook that now contains duplicated detail sheets.
    text: Save the resulting workbook that now contains duplicated detail sheets.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Как создать дублирующие листы деталей в Aspose.Cells для Java
url: /ru/java/worksheet-management/how-to-create-duplicate-detail-sheets-in-aspose-cells-for-ja/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как создать дублирующие листы деталей в Aspose.Cells для Java

Если вам нужно **создать дублирующие листы деталей** в рабочей книге Excel, Aspose.Cells for Java делает это простым. В этом руководстве показано, как разрешить дублирование имён листов при генерации листов деталей с помощью SmartMarkerProcessor, чтобы вы могли получить рабочую книгу, содержащую несколько листов с одинаковым именем.

Вы увидите полный, исполняемый пример, разбор каждой опции конфигурации и советы по работе с распространёнными крайними случаями, такими как конфликты имён и большие наборы данных. Внешние ссылки не требуются — всё необходимое включено в код ниже.

## Предварительные требования

Перед началом убедитесь, что у вас есть:

* Java Development Kit (JDK) 8 или новее.
* Maven или Gradle для управления зависимостями.
* Библиотека Aspose.Cells for Java (версия 23.9 или новее). Добавьте следующую зависимость Maven в ваш `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
</dependency>
```

* Главный шаблон рабочей книги (`master_template.xlsx`), содержащий регион Smart Marker для данных деталей.

## Обзор решения

Решение состоит из четырёх логических шагов:

1. Загрузить главный шаблон рабочей книги.
2. Настроить `SmartMarkerProcessor` для **разрешения дублирования имён листов**.
3. Обработать рабочую книгу, чтобы для каждой группы данных создавался новый лист деталей.
4. Сохранить полученную рабочую книгу, которая теперь содержит дублированные листы деталей.

Каждый шаг подробно объясняется ниже, а полный исходный файл предоставлен в конце руководства.

## Шаг 1: Загрузка главного шаблона рабочей книги

Первая операция создаёт экземпляр `Workbook`, представляющий файл шаблона. Шаблон должен содержать заполнитель Smart Marker (например, `&=DetailData`), который указывает процессору, куда вставлять данные.

```java
import com.aspose.cells.*;

public class DuplicateDetailSheet {
    public static void main(String[] args) throws Exception {
        // Load the master template workbook from the file system
        Workbook workbook = new Workbook("YOUR_DIRECTORY/master_template.xlsx");
```

**Почему это важно:** Загрузка шаблона изолирует макет и форматирование от логики генерации данных, что делает код чистым и упрощает повторное использование одного и того же шаблона для разных наборов данных.

## Шаг 2: Настройка SmartMarkerProcessor для разрешения дублирования имён листов

По умолчанию Aspose.Cells генерирует уникальные имена листов при создании листов деталей. Чтобы **разрешить дублирование имён листов**, установите опцию `DetailSheetNewName` в постоянное значение. Процессор будет переиспользовать это имя для каждого созданного листа.

```java
        // Create a SmartMarkerProcessor instance
        SmartMarkerProcessor processor = new SmartMarkerProcessor();

        // Enable duplicate detail sheet names by assigning a fixed name
        processor.getOptions().setDetailSheetNewName("DetailSheet");

        // Optional: if you want to keep the original sheet after processing, set this flag
        // processor.getOptions().setKeepOriginalDetailSheet(true);
```

**Почему это важно:** Установка `DetailSheetNewName` сообщает движку переиспользовать одно и то же имя для каждого листа деталей, что напрямую удовлетворяет требованию **разрешить дублирование имён листов**. Такой подход полезен, когда последующие инструменты определяют листы по их позиции, а не по имени.

## Шаг 3: Обработка рабочей книги для генерации листов деталей

После настройки вызовите `process` для рабочей книги. Процессор читает регион Smart Marker, создаёт новый лист для каждой группы данных и заполняет его соответствующими строками.

```java
        // Process the workbook; this creates the duplicate detail sheets
        processor.process(workbook);
```

**Почему это важно:** Вызов `process` выполняет основную работу — парсинг Smart Markers, клонирование листа шаблона и вставку данных. Поскольку опция `DetailSheetNewName` уже установлена, каждый новый лист получает одинаковое имя, что приводит к дублированию имён листов в конечном файле.

## Шаг 4: Сохранение полученной рабочей книги

Наконец, запишите изменённую рабочую книгу в новый файл. Выходной файл будет содержать столько вкладок “DetailSheet”, сколько есть групп данных.

```java
        // Save the workbook with duplicated detail sheets
        workbook.save("YOUR_DIRECTORY/duplicate_detail.xlsx");
    }
}
```

**Почему это важно:** Сохранение файла завершает изменения, внесённые процессором. Полученную рабочую книгу можно открыть в Microsoft Excel, LibreOffice или любом другом приложении для работы с таблицами, поддерживающем формат XLSX.

## Полный исходный код

Собрав все части вместе, представляем полную программу, которую вы можете скопировать, вставить и запустить:

```java
import com.aspose.cells.*;

public class DuplicateDetailSheet {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the master template workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/master_template.xlsx");

        // Step 2: Create a SmartMarkerProcessor and allow duplicate detail sheet names
        SmartMarkerProcessor processor = new SmartMarkerProcessor();
        processor.getOptions().setDetailSheetNewName("DetailSheet"); // same name allowed for each detail sheet

        // Step 3: Process the workbook to generate the detail sheets
        processor.process(workbook);

        // Step 4: Save the resulting workbook with duplicated detail sheets
        workbook.save("YOUR_DIRECTORY/duplicate_detail.xlsx");
    }
}
```

### Ожидаемый вывод

Когда вы откроете `duplicate_detail.xlsx`, вы увидите несколько вкладок с именем **DetailSheet**. Каждая вкладка содержит набор данных, соответствующий определённой группе Smart Marker в шаблоне. Макет, форматирование и формулы из главного шаблона сохраняются на каждом дублированном листе.

## Обработка распространённых проблем

| Проблема | Объяснение | Решение |
|----------|------------|---------|
| Excel показывает предупреждение о дублирующихся именах листов | Excel допускает дублирование имён, но может отображать предупреждение при открытии файла. | Предупреждение безвредно; рабочая книга работает корректно. Если хотите подавить предупреждение, переименуйте листы после обработки, используя `Workbook.getWorksheets().get(i).setName("DetailSheet" + i);`. |
| Большие наборы данных вызывают высокое использование памяти | Каждый дублированный лист создаёт полную копию шаблона, что может потреблять ОЗУ. | Включите режим потоковой передачи с помощью `Workbook.setMemorySetting(MemorySetting.MEMORY_PREFERENCE);` перед загрузкой шаблона. |
| Регион Smart Marker не найден | Процессор не может найти `&=DetailData` в шаблоне. | Убедитесь, что синтаксис заполнителя соответствует источнику данных и лист шаблона не скрыт. |

## Профессиональный совет: настройка схемы дублирования имён

Если вам нужен предсказуемый шаблон именования при сохранении возможности дублирования, комбинируйте базовое имя с индексом:

```java
processor.getOptions().setDetailSheetNewName("DetailSheet_{0}");
```

Заполнитель `{0}` заменяется индексом листа, создавая имена вроде `DetailSheet_1`, `DetailSheet_2` и т.д. Это всё ещё удовлетворяет требованию **разрешить дублирование имён листов**, поскольку базовое имя остаётся постоянным.

## Следующие шаги

Теперь, когда вы можете **создавать дублирующие листы деталей**, вы можете изучить следующие темы:

* **Заполнять листы деталей изображениями** — используйте объекты `Picture` для встраивания логотипов или диаграмм.
* **Применять условное форматирование** — добавляйте правила `FormatCondition` для подсветки строк в зависимости от значений.
* **Экспортировать в PDF** — вызовите `workbook.save("output.pdf", SaveFormat.PDF);` для создания PDF‑версии дублированных листов.

Каждое из этих расширений основывается на том же рабочем процессе Smart Marker, продемонстрированном здесь, позволяя автоматизировать сложные задачи отчётности в Excel с уверенностью.

---

*Вы узнали, как создавать дублирующие листы деталей в Aspose.Cells for Java и как разрешать дублирование имён листов с помощью SmartMarkerProcessor. Примените код, адаптируйте шаблон и интегрируйте технику в ваши конвейеры отчётности.*

## Что вам следует изучить дальше?

Следующие руководства охватывают тесно связанные темы, построенные на техниках, продемонстрированных в этом руководстве. Каждый ресурс включает полные работающие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [Создание и доступ к листам Excel, добавление PDF‑закладок с помощью Aspose.Cells for Java](/cells/english/java/workbook-operations/create-access-excel-sheets-add-pdf-bookmarks-aspose-cells-java/)
- [Создание доступа к листам Excel, добавление PDF‑закладок Aspose Cells Java](/cells/german/java/workbook-operations/create-access-excel-sheets-add-pdf-bookmarks-aspose-cells-java/)
- [Создание доступа к листам Excel, добавление PDF‑закладок Aspose Cells Java](/cells/french/java/workbook-operations/create-access-excel-sheets-add-pdf-bookmarks-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}