---
category: general
date: 2026-10-07
description: تعلم كيفية تحميل JSON إلى Excel وإنشاء ملف XLSX من JSON باستخدام Aspose.Cells.
  يوضح هذا الدليل خطوة بخطوة أيضًا كيفية تعبئة Excel من JSON وحفظ المصنف كملف XLSX.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- load json into excel
- generate xlsx from json
- populate excel from json
- save workbook as xlsx
- create workbook from json
language: ar
lastmod: 2026-10-07
og_description: حمّل JSON إلى Excel وقم بإنشاء ملف XLSX من JSON باستخدام Aspose.Cells
  للغة Java. اتبع هذا الدليل لملء Excel من JSON وحفظ المصنف كملف XLSX.
og_image_alt: Screenshot of an Excel workbook that was loaded with JSON data using
  Aspose.Cells
og_title: تحميل JSON إلى Excel باستخدام Aspose.Cells – دليل Java الكامل
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Learn how to load JSON into Excel and generate XLSX from JSON using
    Aspose.Cells. This step‑by‑step guide also shows how to populate Excel from JSON
    and save workbook as XLSX.
  headline: How to load JSON into Excel with Aspose.Cells for Java
  type: TechArticle
- description: Learn how to load JSON into Excel and generate XLSX from JSON using
    Aspose.Cells. This step‑by‑step guide also shows how to populate Excel from JSON
    and save workbook as XLSX.
  name: How to load JSON into Excel with Aspose.Cells for Java
  steps:
  - name: 'Compile the program:'
    text: 'Compile the program:'
  - name: 'Run it:'
    text: 'Run it:'
  - name: Verify that `JsonSingleCell.xlsx` appears in the working directory and opens
      without errors.
    text: Verify that `JsonSingleCell.xlsx` appears in the working directory and opens
      without errors.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: كيفية تحميل JSON إلى Excel باستخدام Aspose.Cells للـ Java
url: /ar/java/excel-import-export/how-to-load-json-into-excel-with-aspose-cells-for-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تحميل JSON إلى Excel باستخدام Aspose.Cells للـ Java

إذا كنت بحاجة إلى **تحميل JSON إلى Excel**، فإن هذا الدليل يوضح لك طريقة موثوقة للقيام بذلك باستخدام Aspose.Cells للـ Java. ستتعرف على كيفية إنشاء ملف XLSX من JSON، تعبئة Excel من JSON، وأخيرًا **حفظ المصنف كملف XLSX**—كل ذلك في برنامج واحد مكتمل.

يُعد العمل مع JSON في جداول البيانات شائعًا عندما تقوم بتصدير البيانات من خدمات الويب أو الـ APIs أو مخازن NoSQL. بنهاية هذا الدليل ستحصل على فئة Java جاهزة للتنفيذ تُنشئ مصنفًا من JSON وتكتب النتيجة إلى ملف على القرص.

## المتطلبات المسبقة

قبل أن تبدأ، تأكد من وجود ما يلي:

* Java 8 أو أحدث مثبت (الكود يستخدم ميزات Java القياسية).
* مكتبة Aspose.Cells للـ Java (الإصدار 23.10 أو أحدث). يمكنك الحصول عليها من [موقع Aspose](https://downloads.aspose.com/cells/java) أو عبر Maven Central.
* بيئة تطوير متكاملة (IDE) أو محرر نصوص بسيط وواجهة طرفية لتجميع وتشغيل كود Java.
* إلمام أساسي بصيغة JSON ومفاهيم Excel.

> **نصيحة احترافية:** إذا كنت تستخدم Maven، أضف الاعتماد التالي إلى ملف `pom.xml` لتجنب إدارة ملفات JAR يدويًا:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
</dependency>
```

## الخطوة 1: إعداد المشروع واستيراد الفئات المطلوبة

أنشئ فئة Java جديدة تسمى `JsonToExcelDemo`. استورد فئات Aspose.Cells التي ستحتاجها لإنشاء المصنف، معالجة ورقة العمل، ومعالجة Smart Marker.

```java
package com.example.exceljson;

import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;
import com.aspose.cells.SmartMarkerProcessor;
import com.aspose.cells.SaveFormat;

public class JsonToExcelDemo {
    public static void main(String[] args) throws Exception {
        // The full implementation starts in the next step.
    }
}
```

*لماذا هذه الخطوة مهمة:* استيراد الفئات الصحيحة يضمن أن المترجم يستطيع العثور على واجهات Aspose.Cells. فئة `Workbook` تمثل ملف Excel، بينما `SmartMarkerProcessor` تدير عملية تحويل JSON إلى Excel.

## الخطوة 2: تعريف مصدر JSON الذي سيتم تحميله إلى Excel

في هذا المثال نستخدم مصفوفة JSON صغيرة تحتوي على كائنين. في سيناريو واقعي يمكنك قراءة JSON من ملف، نقطة نهاية REST، أو قاعدة بيانات.

```java
// Step 2: Define the JSON data that will be used as the smart‑marker source
String jsonData = "[{\"Name\":\"John\",\"Age\":30},{\"Name\":\"Anna\",\"Age\":25}]";
```

*لماذا هذه الخطوة مهمة:* سلسلة JSON هي مصدر البيانات لعملية **تعبئة Excel من JSON**. إبقاء JSON في متغير `String` يسهل تمريره إلى `SmartMarkerProcessor`.

## الخطوة 3: إنشاء مصنف جديد والحصول على ورقة العمل الأولى

المصنف الجديد يمنحك صفحة نظيفة. ورقة العمل الأولى (الفهرس 0) هي المكان الذي سنُدخل فيه Smart Marker.

```java
// Step 3: Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();               // creates an empty XLSX workbook
Worksheet worksheet = workbook.getWorksheets().get(0);
```

*لماذا هذه الخطوة مهمة:* Aspose.Cells يعمل مع كائن `Workbook` يمكن حفظه لاحقًا كملف XLSX. الوصول إلى أول `Worksheet` يتيح لنا وضع العلامة في عنوان خلية معروف.

## الخطوة 4: إدراج Smart Marker يوضح لـ Aspose.Cells كيفية معالجة JSON

Smart Markers هي نواقل نائبة تستبدلها Aspose.Cells بالبيانات من المصدر. العلامة `&=JSONData.ArrayAsSingle` تُخبر المكتبة بمعالجة مصفوفة JSON بأكملها كقيمة خلية واحدة.

```java
// Step 4: Insert a smart‑marker that tells Aspose.Cells to treat the JSON array as a single cell
worksheet.getCells().putValue(0, 0, "&=JSONData.ArrayAsSingle");
```

*لماذا هذه الخطوة مهمة:* استخدام `ArrayAsSingle` يتجنب السلوك الافتراضي لتوسيع كل عنصر في المصفوفة إلى صفوف منفصلة. هذا مفيد عندما تريد ظهور نص JSON كما هو في خلية، أو عندما تخطط لتقسيمه لاحقًا باستخدام صيغ.

## الخطوة 5: تكوين SmartMarkerProcessor بمصدر بيانات JSON

الآن اربط سلسلة JSON بالاسم المنطقي `JSONData`. سيستبدل المعالج العلامة بالبيانات الفعلية.

```java
// Step 5: Configure the SmartMarkerProcessor with the JSON data source
SmartMarkerProcessor processor = new SmartMarkerProcessor(workbook);
processor.setDataSource("JSONData", jsonData);
processor.process();   // expands the marker and writes JSON into the worksheet
```

*لماذا هذه الخطوة مهمة:* `setDataSource` يربط الاسم المستخدم في العلامة (`JSONData`) بالحمولة الفعلية للـ JSON. `process()` يقوم بالعمل الشاق: تحليل JSON، تطبيق منطق العلامة، وكتابة النتيجة في ورقة العمل.

## الخطوة 6: حفظ المصنف الناتج كملف XLSX

أخيرًا، اكتب المصنف إلى القرص. ثابت `SaveFormat.XLSX` يضمن تنسيق Office Open XML الصحيح.

```java
// Step 6: Save the resulting workbook
String outputPath = "JsonSingleCell.xlsx";   // adjust the path as needed
workbook.save(outputPath, SaveFormat.XLSX);
System.out.println("Workbook saved to " + outputPath);
```

*لماذا هذه الخطوة مهمة:* حفظ الملف يُكمل سير عمل **إنشاء XLSX من JSON**. الملف الناتج يمكن فتحه في Excel أو LibreOffice أو أي برنامج جدول بيانات يدعم XLSX.

### الكود الكامل

بتجميع جميع الأجزاء معًا، إليك البرنامج الكامل القابل للتنفيذ الذي **ينشئ مصنفًا من JSON**، **يملأ Excel من JSON**، و**يحفظ المصنف كملف XLSX**.

```java
package com.example.exceljson;

import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;
import com.aspose.cells.SmartMarkerProcessor;
import com.aspose.cells.SaveFormat;

public class JsonToExcelDemo {
    public static void main(String[] args) throws Exception {
        // 1. JSON source – replace with your own data if needed
        String jsonData = "[{\"Name\":\"John\",\"Age\":30},{\"Name\":\"Anna\",\"Age\":25}]";

        // 2. Create a fresh workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // 3. Place a smart‑marker that treats the JSON array as a single cell
        worksheet.getCells().putValue(0, 0, "&=JSONData.ArrayAsSingle");

        // 4. Bind the JSON string to the marker name and process it
        SmartMarkerProcessor processor = new SmartMarkerProcessor(workbook);
        processor.setDataSource("JSONData", jsonData);
        processor.process();

        // 5. Save the workbook as an XLSX file
        String outputPath = "JsonSingleCell.xlsx";
        workbook.save(outputPath, SaveFormat.XLSX);
        System.out.println("Workbook saved to " + outputPath);
    }
}
```

### النتيجة المتوقعة

عند فتح `JsonSingleCell.xlsx` ستظهر مصفوفة JSON في الخلية **A1** تمامًا كما هي في السلسلة الأصلية:

```
[{"Name":"John","Age":30},{"Name":"Anna","Age":25}]
```

إذا كنت تفضل وضع كل كائن في صف منفصل، استبدل العلامة بـ `&=JSONData` (بدون `.ArrayAsSingle`). سيقوم المعالج حينها بتوسيع المصفوفة إلى صفوف فردية، مما يُظهر تقنية مختلفة لـ **تعبئة Excel من JSON**.

## الاختلافات الشائعة وحالات الحافة

| الحالة | التعديل |
|-----------|------------|
| **حجم JSON كبير ( > 10 MB )** | زيادة حجم الذاكرة المخصصة للـ JVM (`-Xmx2g`) والنظر في تدفق JSON لتجنب `OutOfMemoryError`. |
| **كائنات متداخلة** | استخدام علامات هرمية مثل `&=JSONData.Name` و `&=JSONData.Age` داخل جدول لتعيين كل خاصية إلى عمود. |
| **ملف JSON بدلاً من سلسلة نصية** | قراءة الملف إلى `String` باستخدام `java.nio.file.Files.readString(Path.of("data.json"))` وتمريره إلى `setDataSource`. |
| **الحاجة إلى الحفاظ على تنسيق JSON الأصلي** | احتفظ باللاحقة `.ArrayAsSingle`، أو غلف JSON داخل CDATA إذا كنت تخطط لاستخدام صيغ Excel التي تحلل JSON لاحقًا. |
| **عدة أوراق عمل** | إنشاء أوراق عمل إضافية (`workbook.getWorksheets().add("Sheet2")`) وتكرار إدراج العلامة في كل ورقة. |

> **تحذير:** Smart Markers حساسة لحالة الأحرف. تأكد من أن الاسم المنطقي (`JSONData`) يطابق تمامًا بين العلامة و `setDataSource`.

## اختبار الحل

1. تجميع البرنامج:

   ```bash
   javac -cp ".:aspose-cells-23.10.jar" com/example/exceljson/JsonToExcelDemo.java
   ```

2. تشغيله:

   ```bash
   java -cp ".:aspose-cells-23.10.jar" com.example.exceljson.JsonToExcelDemo
   ```

3. تحقق من ظهور `JsonSingleCell.xlsx` في دليل العمل وفتحها دون أخطاء.

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك الخاصة.

- [Create Excel Workbook from JSON – Complete Aspose.Cells Guide](/cells/english/net/data-loading-and-parsing/create-excel-workbook-from-json-complete-aspose-cells-guide/)
- [Create Excel Workbook C# – Insert JSON and Save as XLSX](/cells/english/net/excel-data-import-export/create-excel-workbook-c-insert-json-and-save-as-xlsx/)
- [Save Excel Workbook from JSON – Complete Guide](/cells/english/net/templates-reporting/save-excel-workbook-from-json-complete-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}