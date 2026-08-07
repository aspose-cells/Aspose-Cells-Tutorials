---
date: '2026-03-15'
description: Узнайте, как разделить имена на отдельные столбцы и сохранить книгу в
  формате xlsx, используя Aspose.Cells для Java, в пошаговом руководстве.
keywords:
- Aspose.Cells Java
- split names columns
- Excel manipulation
- text to columns Java
- Java Excel processing
title: aspose cells java – Разделить имена по столбцам
url: /ru/java/cell-operations/aspose-cells-java-split-names-columns/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Освоение **aspose cells java**: Разделение имен на столбцы

Добро пожаловать в наш всесторонний учебник по **aspose cells java**. В этом руководстве вы узнаете **как разделять имена**, хранящиеся в одном столбце Excel, на два отдельных столбца — имя и фамилия — с помощью мощной функции text‑to‑columns. Независимо от того, очищаете ли вы список контактов, готовите данные для импорта в CRM или просто нуждаетесь в быстром способе реструктуризации таблиц, это руководство покажет вам точно, как **save workbook xlsx** после преобразования.

## Быстрые ответы
- **Что охватывает это руководство?** Разделение строк полного имени на столбцы имени и фамилии с помощью Aspose.Cells for Java.  
- **Какая версия библиотеки используется?** Последний стабильный релиз (по состоянию на 2026 год).  
- **Нужна ли лицензия?** Бесплатная пробная версия подходит для разработки; для продакшна требуется коммерческая лицензия.  
- **Можно ли разделять по другим разделителям?** Да — просто измените разделитель в `TxtLoadOptions`.  
- **Является ли результат файлом .xlsx?** Безусловно, рабочая книга сохраняется в формате XLSX.

## Что такое **aspose cells java**?
**Aspose.Cells java** — это высокопроизводительный Java API, позволяющий разработчикам создавать, изменять, конвертировать и отображать файлы Excel без необходимости установки Microsoft Office. Он поддерживает все основные форматы Excel и предоставляет расширенные возможности, такие как формулы, диаграммы и работа с данными.

## Почему использовать **aspose cells java** для разделения имен?
- **Zero‑install**: Работает в любой серверной Java‑среде.  
- **Speed**: Обрабатывает большие таблицы быстрее, чем нативный Excel interop.  
- **Precision**: Полный контроль над разделителями, диапазонами столбцов и форматами вывода.  
- **Reliability**: Нет зависимостей от COM или Office, что делает его идеальным для облачных или контейнерных развертываний.

## Требования
- Java Development Kit (JDK) 8 или новее.  
- IDE, например IntelliJ IDEA или Eclipse (необязательно, но рекомендуется).  
- Maven или Gradle для управления зависимостями.  

### Настройка Maven
Добавьте зависимость Aspose.Cells в ваш `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

### Настройка Gradle
Добавьте библиотеку в ваш `build.gradle`:

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

> **Pro tip:** Используйте временную лицензию с портала Aspose, чтобы разблокировать полную функциональность во время разработки.

## Пошаговая реализация

### Шаг 1: Создание рабочей книги и доступ к первому листу
Сначала импортируйте основные классы и создайте новый объект Workbook. Это даст вам чистый файл Excel, готовый для вставки данных.

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;
```

```java
String dataDir = "YOUR_DATA_DIRECTORY"; // Define your directory path here

Workbook wb = new Workbook();
Worksheet ws = wb.getWorksheets().get(0);
```

### Шаг 2: Заполнение листа образцовыми именами
Затем добавьте несколько строк полных имен в столбец **A**. В реальном проекте вы бы считывали их из базы данных или CSV‑файла.

```java
import com.aspose.cells.Cell;

String outDir = "YOUR_OUTPUT_DIRECTORY"; // Define your output directory path here

ws.getCells().get("A1").putValue("John Teal");
ws.getCells().get("A2").putValue("Peter Graham");
ws.getCells().get("A3").putValue("Brady Cortez");
ws.getCells().get("A4").putValue("Mack Nick");
ws.getCells().get("A5").putValue("Hsu Lee");
```

### Шаг 3: Настройка Text Load Options для разделения столбцов
Класс `TxtLoadOptions` указывает Aspose.Cells, как интерпретировать текст. Здесь мы используем пробел (`' '`) в качестве разделителя.

```java
import com.aspose.cells.TxtLoadOptions;

TxtLoadOptions opts = new TxtLoadOptions();
opts.setSeparator(' ');
```

### Шаг 4: Разделение текста на два столбца
Теперь вызовите `textToColumns()` для диапазона ячеек, содержащих имена. Параметры `(0, 0, 5, opts)` означают *начать с строки 0, столбца 0, обработать 5 строк, используя только что определённые параметры*.

```java
ws.getCells().textToColumns(0, 0, 5, opts);
```

После этого вызова столбец A будет содержать имена, а столбец B — фамилии.

### Шаг 5: Сохранение рабочей книги в файл XLSX
Наконец, запишите изменённую рабочую книгу на диск. Перечисление `SaveFormat` гарантирует, что файл будет сохранён в современном формате XLSX.

```java
import com.aspose.cells.SaveFormat;

wb.save(outDir + "outputTextToColumns.xlsx");
```

> **Why this matters:** Используя **save workbook xlsx**, вы гарантируете совместимость с последними версиями Excel, Google Sheets и другими инструментами работы с таблицами.

## Практические применения
- **Data Cleaning:** Быстро разделить объединённые поля перед загрузкой в аналитические конвейеры.  
- **CRM Integration:** Преобразовать плоский список контактов в структурированную таблицу для импорта.  
- **HR Systems:** Разделить полные имена сотрудников для расчёта заработной платы или обработки льгот.

## Соображения по производительности
При работе с тысячами строк:

1. **Batch Updates:** Используйте `ws.getCells().setRowHeight()` или аналогичные пакетные методы для снижения нагрузки.  
2. **Memory Management:** Вызывайте `wb.calculateFormula()` только при необходимости и своевременно освобождайте большие объекты.  
3. **Garbage Collection:** Запускайте JVM с соответствующими настройками кучи (`-Xmx2g` для больших файлов), чтобы избежать ошибок OutOfMemory.

## Распространённые проблемы и решения

| Проблема | Решение |
|----------|----------|
| **Имена содержат средние инициалы** (например, “John A. Doe”) | Измените разделитель или выполните постобработку второго столбца, чтобы извлечь фамилию. |
| **Неожиданные пустые ячейки** | Убедитесь, что исходный диапазон (параметры `textToColumns`) соответствует фактическим строкам данных. |
| **Лицензия не найдена** | Поместите временный файл лицензии (`Aspose.Cells.lic`) в корень проекта или задайте лицензию программно. |

## Часто задаваемые вопросы

**Q: Что такое Aspose.Cells Java?**  
A: Мощная библиотека, позволяющая программно создавать, изменять и конвертировать файлы Excel с помощью Java.

**Q: Можно ли разделять столбцы по другим разделителям, кроме пробелов?**  
A: Да, при необходимости настройте разделитель в `TxtLoadOptions` под ваши данные.

**Q: Как работать с большими наборами данных в Aspose.Cells?**  
A: Оптимизируйте производительность, управляя памятью и минимизируя операции с рабочей книгой, как описано выше.

**Q: Доступна ли поддержка, если я столкнусь с проблемами?**  
A: Посетите [Aspose Forum](https://forum.aspose.com/c/cells/9) для получения помощи от сообщества или свяжитесь напрямую с командой поддержки Aspose.

**Q: В каких форматах Aspose.Cells может сохранять рабочие книги?**  
A: Поддерживает широкий спектр форматов файлов Excel, включая XLSX, XLS, CSV и другие.

## Ресурсы

- **Документация**: [Справочник Aspose.Cells Java](https://reference.aspose.com/cells/java/)
- **Скачать**: [Выпуски Aspose.Cells Java](https://releases.aspose.com/cells/java/)
- **Купить**: [Купить Aspose.Cells](https://purchase.aspose.com/buy)
- **Бесплатная пробная версия**: [Попробовать Aspose.Cells бесплатно](https://releases.aspose.com/cells/java/)
- **Временная лицензия**: [Запросить временную лицензию](https://purchase.aspose.com/temporary-license/)

Приятного кодинга и наслаждайтесь полным использованием возможностей **aspose cells java** в ваших проектах!

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

---

**Последнее обновление:** 2026-03-15  
**Тестировано с:** Aspose.Cells 25.3 for Java  
**Автор:** Aspose