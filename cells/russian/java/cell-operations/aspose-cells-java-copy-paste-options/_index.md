---
date: '2026-02-22'
description: Узнайте, как автоматизировать создание отчетов Excel с помощью Aspose.Cells
  в Java, используя CopyOptions и PasteOptions, чтобы сохранять точность формул и
  вставлять только видимые значения.
keywords:
- Aspose.Cells Java
- CopyOptions ReferToDestinationSheet
- PasteOptions Excel
title: Автоматизация отчетов Excel – освоение CopyOptions и PasteOptions в Java с
  Aspose.Cells
url: /ru/java/cell-operations/aspose-cells-java-copy-paste-options/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Автоматизация отчетности Excel с помощью Aspose.Cells: CopyOptions & PasteOptions в Java

Ищете способ **автоматизировать отчетность Excel** с использованием Java? С Aspose.Cells вы можете программно копировать, вставлять и корректировать формулы, чтобы ваши отчёты оставались точными, а передавались только необходимые данные. В этом руководстве мы рассмотрим две важные функции — **CopyOptions.ReferToDestinationSheet** и **PasteOptions**, которые позволяют сохранять ссылки формул и вставлять значения только из видимых ячеек.

## Быстрые ответы
- **Что делает `CopyOptions.ReferToDestinationSheet`?** Перенастраивает формулы так, чтобы они указывали на лист назначения при копировании данных.  
- **Как вставить только видимые ячейки?** Установите `PasteOptions.setOnlyVisibleCells(true)` вместе с `PasteType.VALUES`.  
- **Какая версия библиотеки требуется?** Aspose.Cells 25.3 или новее.  
- **Нужна ли лицензия для продакшна?** Да, постоянная или временная лицензия снимает ограничения оценки.  
- **Можно ли использовать Maven или Gradle?** Оба поддерживаются; см. примеры зависимостей ниже.

## Что такое «автоматизировать отчетность Excel»?
Автоматизация отчетности Excel означает программную генерацию, консолидацию и форматирование рабочих книг Excel, исключая ручные операции копирования‑вставки и уменьшая количество ошибок. Aspose.Cells предоставляет богатый API, позволяющий Java‑разработчикам работать с электронными таблицами в масштабе.

## Почему стоит использовать CopyOptions и PasteOptions для отчетности?
- **Сохранение целостности формул** при перемещении данных между листами.  
- **Исключение скрытых строк/столбцов** для чистоты и фокусировки отчётов.  
- **Повышение производительности** за счёт копирования только необходимых данных вместо целых диапазонов.

## Предварительные требования
- Java 8 или выше.  
- Maven или Gradle для управления зависимостями.  
- Aspose.Cells 25.3+ (триальная, временная или постоянная лицензия).  

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
- **Бесплатная пробная версия** – полный набор функций для оценки.  
- **Временная лицензия** – снимает ограничения пробной версии во время тестирования.  
- **Постоянная лицензия** – рекомендуется для производственных нагрузок.

Инициализируйте Aspose.Cells в вашем Java‑коде:

```java
import com.aspose.cells.Workbook;

Workbook workbook = new Workbook("path/to/your/excel/file.xlsx");
```

## Пошаговое руководство

### 1. CopyOptions с ReferToDestinationSheet

#### Обзор
Установка `CopyOptions.ReferToDestinationSheet` в `true` переписывает ссылки формул так, чтобы они указывали на новый лист после операции копирования.

#### Шаг 1: Инициализация Workbook и Worksheets  
```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;

String dataDir = "YOUR_DATA_DIRECTORY";
Workbook wb = new Workbook(dataDir + "/book1.xlsx");
Worksheet source = wb.getWorksheets().get(0);
Worksheet destination = wb.getWorksheets().add("DestSheet");
```

#### Шаг 2: Настройка CopyOptions  
```java
import com.aspose.cells.CopyOptions;

CopyOptions options = new CopyOptions();
options.setReferToDestinationSheet(true); // Adjust formulas to the destination sheet
```

#### Шаг 3: Выполнение операции копирования  
```java
destination.getCells().copyRows(source.getCells(), 0, 0, source.getCells().getMaxDisplayRange().getRowCount(), options, null);
wb.save("YOUR_OUTPUT_DIRECTORY/destination.xlsx");
```
*Почему это важно*: Формулы, которые изначально ссылались на `Sheet1`, теперь корректно указывают на `DestSheet`, что делает ваши автоматизированные отчёты надёжными.

**Совет по устранению неполадок**: Если формулы всё ещё ссылаются на старый лист, убедитесь, что `setReferToDestinationSheet(true)` вызывается **до** копирования.

### 2. PasteOptions для вставки только значений из видимых ячеек

#### Обзор
`PasteOptions` позволяет задать, что именно будет вставлено. Использование `PasteType.VALUES` вместе с `onlyVisibleCells=true` копирует только отображаемые значения, игнорируя скрытые строки/столбцы и форматирование.

#### Шаг 1: Инициализация Workbook и Worksheets  
```java
Workbook wb = new Workbook(dataDir + "/book1.xlsx");
Worksheet source = wb.getWorksheets().get(0);
Worksheet destination = wb.getWorksheets().add("DestSheet");
```

#### Шаг 2: Настройка PasteOptions  
```java
import com.aspose.cells.PasteOptions;
import com.aspose.cells.PasteType;

PasteOptions pasteOptions = new PasteOptions();
pasteOptions.setPasteType(PasteType.VALUES); // Copy only values
pasteOptions.setOnlyVisibleCells(true); // Include only visible cells
```

#### Шаг 3: Выполнение операции вставки  
```java
destination.getCells().copyRows(source.getCells(), 0, 0, source.getCells().getMaxDisplayRange().getRowCount(), null, pasteOptions);
wb.save("YOUR_OUTPUT_DIRECTORY/destination.xlsx");
```
*Почему это важно*: Идеально подходит для извлечения отфильтрованных данных или создания чистых отчётов без скрытых строк и лишнего форматирования.

**Совет по устранению неполадок**: Убедитесь, что строки/столбцы действительно скрыты в Excel перед копированием; иначе они будут включены.

## Практические применения
1. **Финансовая консолидация** – объединение месячных листов в мастер‑книгу с сохранением точных формул.  
2. **Экспорт отфильтрованных данных** – копирование только видимых строк из отфильтрованной таблицы в сводный лист.  
3. **Плановое создание отчётов** – автоматизация ночного создания Excel‑отчётов с точными значениями ячеек и правильными ссылками.

## Соображения по производительности
- **Освобождайте Workbooks** после завершения (`wb.dispose();`) для освобождения нативных ресурсов.  
- **Пакетные операции** – группируйте несколько вызовов копирования/вставки, чтобы снизить накладные расходы.  
- **Контролируйте память** – большие книги могут требовать увеличения кучи (`-Xmx2g`).

## Часто задаваемые вопросы

**Вопрос 1: Для чего используется `CopyOptions.ReferToDestinationSheet`?**  
Ответ: Переписывает ссылки формул так, чтобы они указывали на лист назначения после копирования, обеспечивая корректность формул в отчётах.

**Вопрос 2: Как вставить только видимые ячейки?**  
Ответ: Установите `PasteOptions.setOnlyVisibleCells(true)` и выберите `PasteType.VALUES`.

**Вопрос 3: Можно ли использовать Aspose.Cells без покупки лицензии?**  
Ответ: Да, доступна бесплатная пробная версия или временная лицензия для оценки, но для продакшна требуется постоянная лицензия.

**Вопрос 4: Почему некоторые ссылки всё ещё неверны после копирования?**  
Ответ: Проверьте, что `ReferToDestinationSheet` включён **до** операции копирования и что исходные формулы не содержат внешних ссылок на другие книги.

**Вопрос 5: Какие лучшие практики управления памятью следует соблюдать?**  
Ответ: Освобождайте объекты `Workbook` после использования, обрабатывайте большие файлы порциями и следите за использованием кучи JVM.

**Вопрос 6: Можно ли объединить CopyOptions и PasteOptions в одной операции?**  
Ответ: Да, можно сначала выполнить копирование с `CopyOptions`, а затем применить `PasteOptions` к целевому диапазону.

## Ресурсы
- **Документация**: [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)  
- **Скачать**: [Aspose.Cells Releases for Java](https://releases.aspose.com/cells/java/)  
- **Купить**: [Buy Aspose.Cells](https://purchase.aspose.com/buy)  
- **Бесплатная пробная версия**: [Aspose.Cells Free Trial](https://releases.aspose.com/cells/java/)  
- **Временная лицензия**: [Apply for a Temporary License](https://purchase.aspose.com/temporary-license/)  
- **Форум поддержки**: [Aspose Support](https://forum.aspose.com/c/cells)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

---

**Последнее обновление:** 2026-02-22  
**Тестировано с:** Aspose.Cells 25.3 for Java  
**Автор:** Aspose