---
date: '2026-11-16'
description: Узнайте, как добавить зависимость Maven Aspose.Cells, получать, перечислять
  и управлять соединениями данных Excel, а также извлекать данные SQL в Excel с помощью
  Java.
keywords:
- create excel data connections
- pull sql data excel
- manage excel external connections
- Aspose.Cells
- Java Excel integration
lastmod: '2026-11-16'
og_description: Создавайте соединения данных Excel с помощью Aspose.Cells for Java.
  Узнайте, как добавить зависимость Maven, получать соединения, извлекать данные SQL
  в Excel и эффективно управлять внешними соединениями.
og_image_alt: Guide showing how to create excel data connections using Aspose.Cells
  Java API
og_title: Создайте соединения данных Excel с Aspose.Cells for Java
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Learn how to add Aspose.Cells Maven dependency, retrieve, list, and
    manage Excel data connections, and pull SQL data into Excel using Java.
  headline: Create excel data connections with Aspose.Cells for Java
  type: TechArticle
- description: Learn how to add Aspose.Cells Maven dependency, retrieve, list, and
    manage Excel data connections, and pull SQL data into Excel using Java.
  name: Create excel data connections with Aspose.Cells for Java
  steps:
  - name: load your workbook
    text: The `Workbook` class represents an entire Excel file in memory. Loading
      it is the first step before any connection work.
  - name: retrieve connections
    text: '`workbook.getDataConnections()` returns an `ExternalConnectionCollection`
      containing every defined connection.'
  - name: loop through connections
    text: '`DBConnection` is a subclass of `ExternalConnection` that represents a
      database connection and provides properties such as command text, connection
      string, and parameters. Iterate over the collection, cast each entry to `DBConnection`,
      and read its properties.'
  - name: access parameters
    text: Each `DBConnection` exposes a `getParameters()` method that returns a list
      of name/value pairs.
  type: HowTo
- questions:
  - answer: It is the Maven artifact (`com.aspose:aspose-cells`) that provides the
      Java APIs for reading, writing, and managing Excel files, including external
      data connections.
    question: What is Aspose.Cells Maven dependency?
  - answer: Call `workbook.getDataConnections()` and iterate over the returned `ExternalConnectionCollection`.
    question: How can I list excel data connections in my workbook?
  - answer: Cast each connection to `DBConnection` and use methods like `getCommand()`,
      `getConnectionDescription()`, and `getParameters()`.
    question: How do I extract database connection details from a DBConnection object?
  - answer: Yes, use a standard `for` loop over the collection, cast each to the appropriate
      type, and apply changes as needed.
    question: Can I loop through excel connections to modify them?
  - answer: A valid Aspose.Cells license removes evaluation limitations and enables
      full functionality.
    question: Do I need a license to use these features in production?
  type: FAQPage
tags:
- create excel data connections
- Aspose.Cells
- Java Excel data
- external data connections
title: Создайте соединения данных Excel с Aspose.Cells for Java
url: /ru/java/advanced-features/aspose-cells-java-excel-external-data-connections/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание соединений данных Excel с помощью Aspose.Cells для Java

В современных приложениях, ориентированных на данные, **create excel data connections** программно, чтобы вы могли напрямую вытягивать живые данные из баз данных в рабочие книги. Добавление зависимости Aspose.Cells Maven предоставляет единый, хорошо документированный API, который управляет всем: от перечисления существующих соединений до извлечения полных строк подключения — без необходимости установки Microsoft Office на сервере. Этот учебник проведёт вас через настройку, получение и практическое использование, чтобы вы могли уверенно интегрировать Excel с вашим SQL‑бэкендом.

## Краткие ответы
- **Какой основной способ добавить Aspose.Cells в Java‑проект?** Добавьте Maven‑артефакт `com.aspose:aspose-cells` в ваш `pom.xml`.  
- **Могу ли я перечислить все соединения данных Excel?** Да — вызовите `workbook.getDataConnections()` и пройдитесь по возвращённой коллекции.  
- **Как извлечь детали соединения с базой данных?** Преобразуйте каждый `ExternalConnection` к типу `DBConnection` и прочитайте его свойства, такие как текст команды и строка подключения.  
- **Можно ли перебрать соединения Excel?** Конечно — используйте обычный цикл `for` по `ExternalConnectionCollection`.  
- **Нужна ли лицензия для использования в продакшене?** Действительная лицензия Aspose.Cells снимает ограничения оценки и открывает полный функционал.

## Чему вы научитесь
- Как **создавать соединения данных Excel** и извлекать их из существующей рабочей книги с помощью Aspose.Cells для Java.  
- Как извлекать подробную информацию о каждом соединении, включая детали базы данных и параметры.  
- Реальные сценарии извлечения данных SQL в Excel и автоматизации генерации отчетов.  
- Советы по оптимизации производительности при работе с большими рабочими книгами в Java.

## Зачем добавлять зависимость Aspose.Cells Maven? – преимущества и варианты использования
**Вы добавляете Maven‑артефакт, чтобы получить программный контроль над файлами Excel без установленного Office.** Aspose.Cells поддерживает **более 50 форматов ввода и вывода** и может обрабатывать рабочие книги с **до 10 000 строк**, удерживая использование памяти ниже 150 MB за счёт загрузки только необходимых частей. Это делает его идеальным для рабочих процессов **pull sql data excel**, автоматической генерации отчетов и централизованного управления соединениями в корпоративных средах.

## Требования
- **Aspose.Cells for Java** (версия 25.3 или новее).  
- Среда сборки Maven или Gradle.  
- Установлен Java 8 или новее.  

### Необходимые библиотеки
- **Aspose.Cells for Java** – основная библиотека, позволяющая работать с файлами Excel и управлять соединениями данных.

### Настройка окружения
- Убедитесь, что ваша IDE или система сборки поддерживает Maven или Gradle.  
- Убедитесь, что Java 8 или новее находится в вашем `PATH`.

## Как добавить зависимость Aspose Cells Maven
Загрузите библиотеку, добавив одну строку зависимости в ваш `pom.xml`. Это сразу даст вам доступ к полному набору API Excel.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

Если вы предпочитаете Gradle, эквивалентное объявление выглядит так:

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

### Шаги получения лицензии
- **Free trial** – Исследуйте библиотеку бесплатно.  
- **Temporary license** – Продлите период оценки.  
- **Purchase** – Откройте полный набор функций для производственных нагрузок.

## Базовая инициализация и настройка
После разрешения зависимости вы можете начать использовать Aspose.Cells в вашем Java‑коде:

```java
import com.aspose.cells.Workbook;

// Load an Excel workbook
Workbook workbook = new Workbook("path_to_your_excel_file.xlsx");
```

## Руководство по реализации

### Функция 1: получение внешних соединений данных
**What is it?** Эта функция позволяет **перечислять соединения данных Excel**, чтобы вы точно знали, от каких внешних источников зависит ваша рабочая книга.

#### Шаг 1: загрузите вашу рабочую книгу
Класс `Workbook` представляет весь файл Excel в памяти. Его загрузка — первый шаг перед работой с соединениями.

```java
String sourceDir = "YOUR_DATA_DIRECTORY";
Workbook workbook = new Workbook(sourceDir + "/sampleRetrievingSQLConnectionData.xlsx");
```

#### Шаг 2: извлеките соединения
`workbook.getDataConnections()` возвращает `ExternalConnectionCollection`, содержащий все определённые соединения.

```java
import com.aspose.cells.ExternalConnectionCollection;

ExternalConnectionCollection connections = workbook.getDataConnections();
int connectionCount = connections.getCount();
```

### Функция 2: извлечение деталей соединения с базой данных
**Why use it?** Чтобы **извлечь детали соединения с базой данных**, такие как команды, описания и строки подключения, для аудита или динамического изменения.

#### Шаг 1: переберите соединения
`DBConnection` — подкласс `ExternalConnection`, представляющий соединение с базой данных и предоставляющий свойства, такие как текст команды, строка подключения и параметры.  
Пройдитесь по коллекции, преобразуйте каждый элемент к `DBConnection` и прочитайте его свойства.

```java
import com.aspose.cells.DBConnection;

for (int i = 0; i < connectionCount; i++) {
    Object connection = connections.get(i);
    if (connection instanceof DBConnection) {
        DBConnection dbConn = (DBConnection) connection;
        
        // Display details
        System.out.println("Command: " + dbConn.getCommand());
        System.out.println("Description: " + dbConn.getConnectionDescription());
        // Add more fields as needed...
    }
}
```

### Функция 3: извлечение деталей параметров соединения
**How does it help?** Это позволяет вам **интегрировать Excel с базой данных**, получая каждый параметр, необходимый для соединения, например токены аутентификации или аргументы запросов.

#### Шаг 1: доступ к параметрам
Каждый `DBConnection` предоставляет метод `getParameters()`, который возвращает список пар имя/значение.

```java
import com.aspose.cells.ConnectionParameterCollection;
import com.aspose.cells.ConnectionParameter;

for (int i = 0; i < connectionCount; i++) {
    Object connection = connections.get(i);
    if (connection instanceof DBConnection) {
        DBConnection dbConn = (DBConnection) connection;
        ConnectionParameterCollection parameters = dbConn.getParameters();
        
        for (int j = 0; j < parameters.getCount(); j++) {
            ConnectionParameter param = parameters.get(j);
            
            // Display parameter details
            System.out.println("Name: " + param.getName());
            System.out.println("Value: " + param.getValue());
            // Continue displaying other properties...
        }
    }
}
```

## Практические применения
1. **Data integration** – Автоматически синхронизировать данные Excel с внешними базами данных.  
2. **Automated reporting** – Получать живые данные для актуальных отчетов без ручного обновления.  
3. **System monitoring** – Отслеживать изменения в соединениях баз данных для проверок состояния.  
4. **Data validation** – Проверять внешние данные перед их импортом в рабочую книгу.

## Соображения по производительности
- Загружайте большие рабочие книги экономно, чтобы снизить использование памяти.  
- Используйте эффективные циклы (как показано) и избегайте ненужного создания объектов.  
- Используйте настройку сборки мусора Java для длительно работающих сервисов.

## Распространённые проблемы и устранение неполадок
- **Null connections** – Убедитесь, что рабочая книга действительно содержит внешние соединения; иначе `getDataConnections()` вернёт пустую коллекцию.  
- **License not set** – Без действующей лицензии вы можете увидеть предупреждения об оценочной версии или ограниченный функционал.  
- **Unsupported data source** – Некоторые устаревшие ODBC‑соединения могут потребовать установки дополнительных драйверов на хост‑машине.

## Часто задаваемые вопросы

**Q: Что такое зависимость Aspose.Cells Maven?**  
A: Это Maven‑артефакт (`com.aspose:aspose-cells`), который предоставляет Java‑API для чтения, записи и управления файлами Excel, включая внешние соединения данных.

**Q: Как могу я перечислить соединения данных Excel в моей рабочей книге?**  
A: Вызовите `workbook.getDataConnections()` и пройдитесь по возвращённому `ExternalConnectionCollection`.

**Q: Как извлечь детали соединения с базой данных из объекта DBConnection?**  
A: Преобразуйте каждое соединение к `DBConnection` и используйте методы вроде `getCommand()`, `getConnectionDescription()` и `getParameters()`.

**Q: Можно ли перебрать соединения Excel для их изменения?**  
A: Да, используйте обычный цикл `for` по коллекции, преобразуйте каждый элемент к соответствующему типу и при необходимости применяйте изменения.

**Q: Нужна ли лицензия для использования этих функций в продакшене?**  
A: Действительная лицензия Aspose.Cells снимает ограничения оценки и открывает полный функционал.

## Ресурсы
- [Документация](https://reference.aspose.com/cells/java/)
- [Скачать последнюю версию](https://releases.aspose.com/cells/java/)
- [Купить лицензию](https://purchase.aspose.com/buy)
- [Доступ к бесплатной пробной версии](https://releases.aspose.com/cells/java/)
- [Информация о временной лицензии](https://purchase.aspose.com/temporary-license/)
- [Форум поддержки](https://forum.aspose.com/c/cells/9)

---

**Последнее обновление:** 2026-11-16  
**Тестировано с:** Aspose.Cells 25.3 (Java)  
**Автор:** Aspose

## Связанные руководства

- [Извлечение URL из Excel с помощью Aspose.Cells для Java – загрузка соединений данных](/cells/java/advanced-features/aspose-cells-java-excel-data-connections/)
- [Aspose.Cells Java: Мастерство соединений рабочей книги Excel для интеграции данных и анализа](/cells/java/import-export/aspose-cells-java-excel-connections/)
- [Изменение соединений данных Excel с Aspose.Cells для Java – пошаговое руководство](/cells/java/advanced-features/master-excel-data-connections-aspose-cells-java/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}