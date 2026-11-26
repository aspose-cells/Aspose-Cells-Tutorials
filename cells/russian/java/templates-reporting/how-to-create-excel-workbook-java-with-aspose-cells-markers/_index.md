---
category: general
date: 2026-11-25
description: Пример кода на Java для создания рабочей книги Excel с использованием
  умных маркеров Aspose.Cells, позволяющий привязывать массивы JSON как отдельные
  значения.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook java
- Aspose.Cells smart marker
- Java JSON to Excel
- setSmartMarkerData
- Excel export Java
language: ru
lastmod: 2026-11-25
og_description: Создайте Excel‑книгу Java с Aspose.Cells, чтобы легко экспортировать
  массивы JSON в отдельные ячейки. Следуйте пошаговому руководству.
og_image_alt: Screenshot of an Excel workbook created in Java using Aspose.Cells smart
  markers
og_title: Создание Excel‑рабочей книги на Java – руководство по умным маркерам Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-11-25'
  description: Create Excel workbook Java code example using Aspose.Cells smart markers
    to bind JSON arrays as single values.
  headline: How to create Excel workbook Java with Aspose.Cells markers
  type: TechArticle
- description: Create Excel workbook Java code example using Aspose.Cells smart markers
    to bind JSON arrays as single values.
  name: How to create Excel workbook Java with Aspose.Cells markers
  steps:
  - name: '**Creates a fresh workbook** – `new Workbook()` gives you an in‑memory
      Excel file with a default sheet.'
    text: '**Creates a fresh workbook** – `new Workbook()` gives you an in‑memory
      Excel file with a default sheet.'
  - name: '**Places a smart marker in cell A1** – `{{jsonArray:ArrayAsSingle}}` tells
      Aspose.Cells to replace the marker with the *entire* array, joined by commas.'
    text: '**Places a smart marker in cell A1** – `{{jsonArray:ArrayAsSingle}}` tells
      Aspose.Cells to replace the marker with the *entire* array, joined by commas.'
  - name: '**Builds a `Map` data source** – The key `"jsonArray"` matches the marker
      name; the value is a `String[]`.'
    text: '**Builds a `Map` data source** – The key `"jsonArray"` matches the marker
      name; the value is a `String[]`.'
  - name: '**Calls `setSmartMarkerData`** – This binds the map to the marker and performs
      the replacement.'
    text: '**Calls `setSmartMarkerData`** – This binds the map to the marker and performs
      the replacement.'
  - name: '**Saves the file** – `workbook.save(...)` writes `JsonSingleValue.xlsx`
      to disk.'
    text: '**Saves the file** – `workbook.save(...)` writes `JsonSingleValue.xlsx`
      to disk.'
  - name: Open `JsonSingleValue.xlsx` in Microsoft Excel, LibreOffice Calc, or Google
      Sheets.
    text: Open `JsonSingleValue.xlsx` in Microsoft Excel, LibreOffice Calc, or Google
      Sheets.
  - name: Confirm that cell **A1** reads `One, Two, Three`.
    text: Confirm that cell **A1** reads `One, Two, Three`.
  - name: Check that no extra rows or columns were added – the smart marker performed
      an in‑place replacement.
    text: Check that no extra rows or columns were added – the smart marker performed
      an in‑place replacement.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Как создать Excel‑рабочую книгу на Java с маркерами Aspose.Cells
url: /ru/java/templates-reporting/how-to-create-excel-workbook-java-with-aspose-cells-markers/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как создать Excel workbook Java с маркерами Aspose.Cells

Если вам нужно **create Excel workbook Java** код, который записывает массив JSON в одну ячейку, этот учебник покажет, как это сделать. С помощью умных маркеров Aspose.Cells вы можете рассматривать весь массив как одно значение, избегая ручных циклов и записи ячейка‑за‑ячейкой.

Вы узнаете, как настроить книгу, определить умный маркер, привязать источник данных `Map`, содержащий массив в стиле JSON, и наконец сохранить файл. Пример работает с Java 17+, Maven и бесплатной пробной библиотекой Aspose.Cells for Java.

---

![Screenshot of an Excel workbook created in Java using Aspose.Cells smart markers](excel-workbook-java.png){: .center-image alt="Скриншот Excel‑книги, созданной в Java с использованием умных маркеров Aspose.Cells"}

## Требования

| Требование | Почему это важно |
|-------------|-------------------|
| Java 17 или новее | Последние возможности языка и обновления безопасности |
| Maven 3.6+ | Упрощает управление зависимостями |
| Aspose.Cells for Java (v23.12 или новее) | Предоставляет API `Workbook`, `Worksheet` и умных маркеров, используемых в примере |
| Базовые знания коллекций Java | Вам понадобится создать `Map<String, Object>`, который будет источником данных |

Добавьте зависимость Aspose.Cells в ваш `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version>
    <classifier>jdk17</classifier>
</dependency>
```

---

## Создание Excel workbook Java – полный пример

Следующая программа представляет собой **полное, исполняемое** решение. Скопируйте её в файл с именем `ExcelSmartMarkerDemo.java`, скомпилируйте и запустите.

```java
package com.example.excel;

import com.aspose.cells.*;
import java.util.HashMap;
import java.util.Map;

/**
 * Demonstrates how to create Excel workbook Java using Aspose.Cells smart markers.
 * The smart marker "{{jsonArray:ArrayAsSingle}}" treats the whole array as a single cell value.
 */
public class ExcelSmartMarkerDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();                       // empty workbook
        Worksheet worksheet = workbook.getWorksheets().get(0);    // first (default) sheet

        // Step 2: Define a smart marker that treats a JSON array as a single value
        // The "ArrayAsSingle" option concatenates the array elements with commas.
        String smartMarker = "{{jsonArray:ArrayAsSingle}}";
        worksheet.getCells().get("A1").putValue(smartMarker);

        // Step 3: Prepare the data source – a simple string array
        Map<String, Object> dataSource = new HashMap<>();
        dataSource.put("jsonArray", new String[] { "One", "Two", "Three" });

        // Step 4: Bind the data to the smart marker and save the workbook
        worksheet.getCells().get("A1").setSmartMarkerData(dataSource);
        workbook.save("JsonSingleValue.xlsx");   // workbook saved to project root
        System.out.println("Workbook created successfully.");
    }
}
```

### Что делает код

1. **Создаёт новую книгу** – `new Workbook()` создаёт Excel‑файл в памяти с листом по умолчанию.  
2. **Размещает умный маркер в ячейке A1** – `{{jsonArray:ArrayAsSingle}}` указывает Aspose.Cells заменить маркер *весь* массив, объединённый запятыми.  
3. **Создаёт источник данных `Map`** – Ключ `"jsonArray"` совпадает с именем маркера; значение – `String[]`.  
4. **Вызывает `setSmartMarkerData`** – Привязывает карту к маркеру и выполняет замену.  
5. **Сохраняет файл** – `workbook.save(...)` записывает `JsonSingleValue.xlsx` на диск.

Когда вы откроете сгенерированный Excel‑файл, ячейка **A1** будет содержать:

```
One, Two, Three
```

Массив отображается как одна строка, разделённая запятыми, благодаря опции `ArrayAsSingle`.

---

## Использование умного маркера Aspose.Cells для привязки JSON‑данных

Умные маркеры Aspose.Cells – мощный способ напрямую отображать сложные объекты (включая структуры, похожие на JSON) на листы. Синтаксис `{{fieldName:Option}}` работает аналогично шаблонизатору:

* **fieldName** – ключ в вашем источнике данных (`Map`, POJO или `DataTable`).  
* **Option** – управляет обработкой коллекций. `ArrayAsSingle` рассматривает всю коллекцию как одно значение; другие варианты, такие как `Array`, развернут массив по строкам.

**Зачем использовать умный маркер вместо цикла?**  
Цикл требует ручных вычислений адресов ячеек, подвержен ошибкам индексации и требует дополнительного кода для стилизации. Умные маркеры позволяют писать декларативные заполнители, держать Java‑код коротким, а библиотека сама управляет размещением.

---

## Настройка источника данных Java `Map`

`Map<String, Object>` – самый простой контейнер данных для Aspose.Cells:

```java
Map<String, Object> dataSource = new HashMap<>();
dataSource.put("jsonArray", new String[] { "One", "Two", "Three" });
```

*Ключ (`jsonArray`) должен точно соответствовать имени маркера.*  
Вы также можете использовать `List<String>`, пользовательский POJO или даже вложенный `Map` для более сложных JSON‑структур. Aspose.Cells автоматически обойдёт граф объектов.

**Подсказка:** Если нужно отформатировать объединённую строку иначе (например, использовать точку с запятой), предварительно обработайте массив в Java перед добавлением его в карту:

```java
String joined = String.join(";", new String[] {"One","Two","Three"});
dataSource.put("jsonArray", new String[] { joined });
```

---

## Сохранение книги и проверка результата

```java
workbook.save("JsonSingleValue.xlsx");
```

Метод `save` поддерживает множество форматов (`.xlsx`, `.xls`, `.csv`, `.pdf`). В этом учебнике мы оставляем формат Excel Open XML по умолчанию.

**Шаги проверки**

1. Откройте `JsonSingleValue.xlsx` в Microsoft Excel, LibreOffice Calc или Google Sheets.  
2. Убедитесь, что ячейка **A1** содержит `One, Two, Three`.  
3. Проверьте, что не добавлены лишние строки или столбцы – умный маркер выполнил замену «на месте».

Если в ячейке отображается исходный текст маркера (`{{jsonArray:ArrayAsSingle}}`), проверьте следующее:

* Имя маркера точно совпадает с ключом карты (учитывается регистр).  
* `setSmartMarkerData` вызывается **после** размещения маркера.  
* Версия Aspose.Cells поддерживает опцию `ArrayAsSingle` (доступно, начиная с v20.3).

---

## Общие варианты и граничные случаи

| Сценарий | Корректировка |
|----------|----------------|
| **Другой разделитель** | Используйте `ArrayAsSingle` совместно с пользовательским объединением в Java (см. подсказку выше). |
| **Несколько массивов на одном листе** | Разместите дополнительные маркеры, например `{{anotherArray:ArrayAsSingle}}`, в других ячейках и добавьте соответствующие записи в карту. |
| **Вложенные JSON‑объекты** | Передайте вложенный `Map<String, Object>`; обращайтесь к полям через точечную нотацию (`{{parent.child}}`). |
| **Большие наборы данных** | Для тысяч строк предпочтительнее опция `Array`, позволяющая Aspose.Cells автоматически расширять строки. |

## Что изучать дальше?

Следующие учебники охватывают тесно связанные темы, расширяющие техники, продемонстрированные в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы в ваших проектах.

- [Как создать и экспортировать Excel в HTML с помощью Aspose.Cells Java | Руководство по операциям с книгой](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)
- [Экспорт Excel‑книги как изображения с использованием Aspose.Cells for Java: пошаговое руководство](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)
- [Как создать и сохранить Excel‑книгу в формате SVG с помощью Aspose.Cells for Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}