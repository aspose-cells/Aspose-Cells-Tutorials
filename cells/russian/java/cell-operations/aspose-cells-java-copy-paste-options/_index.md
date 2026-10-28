---
date: '2026-10-28'
description: Узнайте, как вставлять значения, используя параметры копирования и вставки
  Aspose.Cells в Java, с пошаговым кодом, настройкой зависимости Maven и советами
  по лицензированию.
keywords:
- how to paste values
- aspose cells maven dependency
- java generate excel report
- aspose cells license java
- copyoptions refertodestinationsheet
lastmod: '2026-10-28'
og_description: Узнайте, как вставлять значения, используя параметры копирования и
  вставки Aspose.Cells в Java, с пошаговым кодом, настройкой зависимости Maven и советами
  по лицензированию.
og_image_alt: Developer guide showing Java code for copying and pasting Excel data
  with Aspose.Cells
og_title: Как вставлять значения с помощью параметров копирования и вставки Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-10-28'
  description: Learn how to paste values using Aspose.Cells copy and paste options
    in Java, with step‑by‑step code, Maven dependency setup, and licensing tips.
  headline: How to paste values with Aspose.Cells copy and paste options
  type: TechArticle
- questions:
  - answer: It rewrites formula references so they point to the destination sheet
      after a copy, ensuring reporting formulas stay correct.
    question: What is `CopyOptions.ReferToDestinationSheet` used for?
  - answer: Set `PasteOptions.setOnlyVisibleCells(true)` and choose `PasteType.VALUES`.
    question: How do I paste only visible cells?
  - answer: Yes, a free trial or temporary license is available for evaluation, but
      a permanent license is required for production.
    question: Can I use Aspose.Cells without purchasing a license?
  - answer: Double‑check that `ReferToDestinationSheet` is enabled **before** the
      copy operation and that the source formulas don’t contain external workbook
      links.
    question: Why are some references still wrong after copying?
  - answer: Dispose of `Workbook` objects when finished, process large files in chunks,
      and monitor JVM heap usage.
    question: What memory‑management best practices should I follow?
  type: FAQPage
tags:
- paste values
- Aspose.Cells
- Java Excel automation
- copy options
- paste options
title: Как вставлять значения с помощью параметров копирования и вставки Aspose.Cells
url: /ru/java/cell-operations/aspose-cells-java-copy-paste-options/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как вставлять значения с помощью параметров копирования и вставки Aspose.Cells

Автоматизация создания отчетов Excel на Java позволяет генерировать, консолидировать и форматировать книги без ручного открытия Excel. С **Aspose.Cells** вы получаете полный контроль над формулами, скрытыми строками и значениями ячеек, поэтому ваши отчеты остаются точными и легковесными. В этом руководстве вы узнаете, как использовать **CopyOptions.ReferToDestinationSheet**, чтобы формулы оставались корректными, и **PasteOptions**, чтобы вставлять только видимые значения, которые вам нужны.

## Быстрые ответы
- **Что делает `CopyOptions.ReferToDestinationSheet`?** Переписывает формулы так, чтобы они указывали на лист назначения после операции копирования.  
- **Как вставить только видимые ячейки?** Вызовите `PasteOptions.setOnlyVisibleCells(true)` вместе с `PasteType.VALUES`.  
- **Какая версия библиотеки требуется?** Aspose.Cells 25.3 или новее.  
- **Нужна ли лицензия для продакшна?** Да — постоянная или временная лицензия снимает ограничения оценки.  
- **Можно ли использовать Maven или Gradle?** Оба поддерживаются; см. сниппеты зависимостей ниже.

## Что такое «автоматизация отчетности Excel»?
Автоматизация отчетности Excel означает программное создание и обновление книг Excel, позволяя создавать, объединять и форматировать отчеты без ручного копирования‑вставки, что уменьшает количество ошибок и экономит часы повторяющейся работы. Такой подход идеален для запланированных пакетных задач, панелей управления, основанных на данных, и конвейеров финансовой консолидации.

## Почему использовать CopyOptions и PasteOptions для отчетности?
Эти два класса позволяют сохранять ссылки формул неизменными при копировании данных **и** извлекать только те ячейки, которые видимы после фильтрации или скрытия строк. Их совместное использование снижает объем передаваемых данных до 80 % в типичных сценариях с отфильтрованными таблицами и гарантирует корректный пересчет формул на листе назначения.

## Предварительные требования
- Java 8 или выше.  
- Maven или Gradle для управления зависимостями.  
- Aspose.Cells 25.3+ (пробная, временная или постоянная лицензия).  

## Настройка Aspose.Cells для Java

Добавьте библиотеку в проект одним из способов:

**Maven**  
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

**Gradle**  
```gradle
implementation 'com.aspose:aspose-cells:25.3'
```

### Приобретение лицензии
- **Бесплатная пробная версия** — полный набор функций для оценки.  
- **Временная лицензия** — снимает ограничения пробной версии во время тестирования.  
- **Постоянная лицензия** — рекомендуется для производственных нагрузок.

Инициализируйте Aspose.Cells в вашем Java‑коде:  
```java
import com.aspose.cells.Workbook;

Workbook workbook = new Workbook("path/to/your/excel/file.xlsx");
```

## Пошаговое руководство

### 1. copyOptions с referToDestinationSheet

#### Обзор
`CopyOptions` — объект конфигурации Aspose.Cells, который управляет тем, как обрабатываются формулы и ссылки ячеек во время операции копирования. Установка `CopyOptions.ReferToDestinationSheet` в `true` переписывает ссылки формул так, чтобы они указывали на новый лист после копирования.

#### Шаг 1: инициализировать рабочую книгу и листы  
```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;

String dataDir = "YOUR_DATA_DIRECTORY";
Workbook wb = new Workbook(dataDir + "/book1.xlsx");
Worksheet source = wb.getWorksheets().get(0);
Worksheet destination = wb.getWorksheets().add("DestSheet");
```

#### Шаг 2: настроить copyOptions  
```java
import com.aspose.cells.CopyOptions;

CopyOptions options = new CopyOptions();
options.setReferToDestinationSheet(true); // Adjust formulas to the destination sheet
```

#### Шаг 3: выполнить операцию копирования  
```java
destination.getCells().copyRows(source.getCells(), 0, 0, source.getCells().getMaxDisplayRange().getRowCount(), options, null);
wb.save("YOUR_OUTPUT_DIRECTORY/destination.xlsx");
```  
*Почему это важно*: Формулы, которые изначально ссылались на `Sheet1`, теперь корректно будут ссылаться на `DestSheet`, поддерживая надежность автоматических отчетов.

**Совет по устранению неполадок**: Если формулы всё ещё ссылаются на старый лист, убедитесь, что `setReferToDestinationSheet(true)` вызван **до** копирования.

### 2. pasteOptions для вставки только значений из видимых ячеек

#### Обзор
`PasteOptions` — объект настроек Aspose.Cells, определяющий, что будет вставлено. Использование `PasteType.VALUES` вместе с `onlyVisibleCells=true` копирует только отображаемые значения, игнорируя скрытые строки/столбцы и форматирование.

#### Шаг 1: инициализировать рабочую книгу и листы  
```java
Workbook wb = new Workbook(dataDir + "/book1.xlsx");
Worksheet source = wb.getWorksheets().get(0);
Worksheet destination = wb.getWorksheets().add("DestSheet");
```

#### Шаг 2: настроить pasteOptions  
```java
import com.aspose.cells.PasteOptions;
import com.aspose.cells.PasteType;

PasteOptions pasteOptions = new PasteOptions();
pasteOptions.setPasteType(PasteType.VALUES); // Copy only values
pasteOptions.setOnlyVisibleCells(true); // Include only visible cells
```

#### Шаг 3: выполнить операцию вставки  
```java
destination.getCells().copyRows(source.getCells(), 0, 0, source.getCells().getMaxDisplayRange().getRowCount(), null, pasteOptions);
wb.save("YOUR_OUTPUT_DIRECTORY/destination.xlsx");
```  
*Почему это важно*: Идеально подходит для извлечения отфильтрованных данных или создания чистых отчетов без скрытых строк и лишнего форматирования.

**Совет по устранению неполадок**: Убедитесь, что строки/столбцы действительно скрыты в Excel перед копированием; иначе они будут включены.

## Практические применения
1. **Финансовая консолидация** — объединение месячных листов в мастер‑книгу с сохранением точных формул.  
2. **Экспорт отфильтрованных данных** — копирование только видимых строк из отфильтрованной таблицы в сводный лист.  
3. **Запланированное создание отчетов** — автоматизация ночного создания Excel‑отчетов с точными значениями ячеек и правильными ссылками.

## Соображения по производительности
- **Освобождайте рабочие книги** после использования (`wb.dispose();`), чтобы освободить нативные ресурсы.  
- **Пакетные операции** — группируйте несколько вызовов копирования/вставки для снижения накладных расходов.  
- **Контролируйте память** — большие книги могут потребовать увеличения кучи (`-Xmx2g`).  
- Aspose.Cells поддерживает **более 50 форматов ввода и вывода** и может обрабатывать книги с **до 2 миллионами строк** без полной загрузки файла в память, обеспечивая высокую пропускную способность для корпоративных нагрузок.

## Часто задаваемые вопросы

**В: Для чего используется `CopyOptions.ReferToDestinationSheet`?**  
О: Он переписывает ссылки формул так, чтобы они указывали на лист назначения после копирования, обеспечивая корректность формул в отчетах.

**В: Как вставить только видимые ячейки?**  
О: Установите `PasteOptions.setOnlyVisibleCells(true)` и выберите `PasteType.VALUES`.

**В: Можно ли использовать Aspose.Cells без покупки лицензии?**  
О: Да, доступна бесплатная пробная версия или временная лицензия для оценки, но для продакшна требуется постоянная лицензия.

**В: Почему некоторые ссылки остаются неверными после копирования?**  
О: Проверьте, что `ReferToDestinationSheet` включён **до** операции копирования и что исходные формулы не содержат внешних ссылок на другие книги.

**В: Какие лучшие практики управления памятью следует соблюдать?**  
О: Освобождайте объекты `Workbook` после завершения, обрабатывайте большие файлы порциями и следите за использованием кучи JVM.

**В: Можно ли объединить CopyOptions и PasteOptions в одной операции?**  
О: Да, сначала выполните копирование с `CopyOptions`, а затем примените `PasteOptions` к целевому диапазону.

## Ресурсы
- **Документация**: [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)  
- **Скачать**: [Aspose.Cells releases for Java](https://releases.aspose.com/cells/java/)  
- **Купить**: [Buy Aspose.Cells](https://purchase.aspose.com/buy)  
- **Бесплатная пробная версия**: [Aspose.Cells free trial](https://releases.aspose.com/cells/java/)  
- **Временная лицензия**: [Apply for a temporary license](https://purchase.aspose.com/temporary-license/)  
- **Форум поддержки**: [Aspose support](https://forum.aspose.com/c/cells)

---

**Последнее обновление:** 2026-10-28  
**Тестировано с:** Aspose.Cells 25.3 for Java  
**Автор:** Aspose

## Связанные руководства

- [Read Excel File Java – Master Workbook Cell Manipulation with Aspose.Cells](/cells/java/cell-operations/aspose-cells-java-workbook-cell-manipulation/)
- [Add Data to Cell in Excel Using Aspose.Cells for Java](/cells/java/cell-operations/aspose-cells-java-set-active-cell-excel/)
- [Convert Excel Cell Row Column Indices with Aspose.Cells Java](/cells/java/cell-operations/convert-excel-cell-names-to-indices-aspose-cells-java/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}