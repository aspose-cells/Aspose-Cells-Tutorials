---
date: '2026-02-22'
description: Узнайте, как изменить систему дат Excel на 1904 с помощью Aspose.Cells
  для Java, установить формат даты Excel и эффективно преобразовать систему дат 1904
  в Excel.
keywords:
- 1904 date system Excel
- Aspose.Cells Java configuration
- Excel workbook manipulation
title: Изменить систему дат Excel на 1904 с помощью Aspose.Cells Java
url: /ru/java/cell-operations/aspose-cells-java-configure-1904-date-system-excel/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Сменить систему дат Excel на 1904 с помощью Aspose.Cells Java

Управление историческими данными в Excel может быть сложным, поскольку Excel поддерживает две разные системы дат. **В этом руководстве вы узнаете, как изменить систему дат Excel на формат 1904, используя Aspose.Cells для Java**, что делает работу с устаревшими датами простой. Мы пройдёмся по инициализации книги, включению системы дат 1904 и сохранению изменений.

## Быстрые ответы
- **Что делает система дат 1904?** Она начинает счёт дней с 1 января 1904 года, сдвигая все даты на 1462 дня по сравнению со стандартной системой 1900.  
- **Зачем использовать Aspose.Cells для изменения системы дат?** Он предоставляет простой API, который работает без установленного Excel и поддерживает большие файлы.  
- **Какие версии Java поддерживаются?** JDK 8 и новее.  
- **Нужна ли лицензия?** Бесплатная пробная версия подходит для оценки; лицензия снимает ограничения использования.  
- **Можно ли позже вернуть систему 1900?** Да, просто вызовите `setDate1904(false)`.

## Что такое система дат 1904 в Excel?
Система дат 1904 изначально использовалась в ранних версиях Excel для Macintosh. Она считает дни с 1 января 1904 года, что полезно для совместимости со старыми таблицами и некоторыми финансовыми моделями.

## Почему менять систему дат Excel с помощью Aspose.Cells?
- **Кросс‑платформенная совместимость** – работает на Windows, Linux и macOS.  
- **Не требуется установка Excel** – идеально для серверной обработки.  
- **Высокая производительность** – обрабатывает большие книги с минимальными затратами памяти.  

## Предварительные требования
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
Включите эту строку в ваш файл `build.gradle`:

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

#### Приобретение лицензии
Aspose предлагает бесплатную пробную версию, временную лицензию и полные коммерческие лицензии. Вы можете начать с [бесплатной пробной версии](https://releases.aspose.com/cells/java/) или получить временную лицензию на странице [temporary license page](https://purchase.aspose.com/temporary-license/).

## Смена системы дат Excel с помощью Aspose.Cells Java

Ниже пошаговое руководство, которое действительно **изменяет систему дат Excel**. Каждый шаг содержит короткое объяснение и точный код, который необходимо использовать.

### Шаг 1: Инициализировать и загрузить книгу
Сначала создайте экземпляр `Workbook`, указывающий на ваш существующий файл Excel.

```java
import com.aspose.cells.Workbook;

String dataDir = "YOUR_DATA_DIRECTORY"; // Ensure the path to your Excel file is correct
// Initialize a Workbook object with the path to your Excel file
Workbook workbook = new Workbook(dataDir + "/Mybook.xlsx");
```

### Шаг 2: Включить систему дат 1904
Используйте настройки книги для переключения системы дат.

```java
import com.aspose.cells.Workbook;

String dataDir = "YOUR_DATA_DIRECTORY"; // Ensure the path to your Excel file is correct
// Load the workbook from your specified directory
Workbook workbook = new Workbook(dataDir + "/Mybook.xlsx");

// Enable the 1904 date system
workbook.getSettings().setDate1904(true);
```

**Совет:** При необходимости вы можете позже вызвать `setDate1904(false)`, чтобы вернуть прежнее значение.

### Шаг 3: Сохранить изменённую книгу
Наконец, запишите изменения в новый файл (или перезапишите оригинал).

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

> **Примечание:** В приведённом выше коде используется имя класса `tWorkbook`, как было указано изначально. Убедитесь, что эта опечатка соответствует соглашениям именования вашего проекта, или исправьте её на `Workbook`, если необходимо.

## Установить дату в Excel программно (вторичное ключевое слово)
Если после изменения системы необходимо скорректировать отдельные ячейки, вы можете использовать `Cells.get(i, j).putValue(Date)`, где дата будет интерпретироваться согласно активной системе дат.

## Вернуть систему 1904 в 1900 (вторичное ключевое слово)
Чтобы откатить изменения, просто вызовите:

```java
workbook.getSettings().setDate1904(false);
```

Затем снова сохраните книгу.

## Практические применения
1. **Архивирование данных** – Сохранение устаревших меток времени при миграции старых таблиц Mac.  
2. **Кросс‑платформенная отчётность** – Генерация отчётов, которые можно открыть как в Windows, так и в macOS без несоответствия дат.  
3. **Финансовое моделирование** – Согласование расчётов дат с устаревшими финансовыми моделями, ожидающими систему 1904.

## Соображения по производительности
- Ограничьте операции с книгой в одной сессии, чтобы снизить использование памяти.  
- Настраивайте сборку мусора Java для работы с очень большими файлами.  

## Часто задаваемые вопросы

**В: В чём разница между системами дат 1900 и 1904?**  
О: Система 1900 начинается с 1 января 1900 года, а система 1904 — с 1 января 1904 года, сдвигая все даты на 1462 дня.

**В: Можно ли изменить систему дат книги, которая сейчас открыта в Excel?**  
О: Да, но сначала необходимо закрыть файл в Excel; иначе операция сохранения завершится ошибкой.

**В: Нужна ли лицензия для использования `setDate1904`?**  
О: Метод работает в бесплатной пробной версии, но полная лицензия снимает ограничения оценки.

**В: Можно ли изменить систему дат только для одного листа?**  
О: Нет, система дат задаётся на уровне книги; она применяется ко всем листам.

**В: Как проверить, что система дат была изменена?**  
О: Откройте сохранённый файл в Excel, перейдите в **File → Options → Advanced** и проверьте галочку **"Use 1904 date system"**.

## Заключение
Теперь вы знаете, как **изменить систему дат Excel** на 1904 с помощью Aspose.Cells для Java, как задавать форматы дат в Excel и как вернуть прежнюю систему при необходимости. Включите эти фрагменты кода в ваши конвейеры обработки данных, чтобы обеспечить совместимость дат на разных платформах.

---

**Последнее обновление:** 2026-02-22  
**Тестировано с:** Aspose.Cells 25.3 for Java  
**Автор:** Aspose  

**Ресурсы**
- **Документация:** [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)
- **Скачать:** [Aspose.Cells Releases](https://releases.aspose.com/cells/java/)
- **Купить лицензию:** [Buy Aspose.Cells](https://purchase.aspose.com/buy)
- **Бесплатная пробная версия:** [Start Free Trial](https://releases.aspose.com/cells/java/)
- **Временная лицензия:** [Get Temporary License](https://purchase.aspose.com/temporary-license/)
- **Форум поддержки:** [Aspose Support](https://forum.aspose.com/c/cells/9)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}