---
category: general
date: 2026-11-16
description: كيفية نسخ الخلايا بين دفاتر Excel في Java – تحميل دفتر العمل، نسخ النطاق
  بين دفاتر العمل (بما في ذلك جدول محوري)، وحفظ ملف دفتر العمل.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy cells
- copy range between workbooks
- copy pivot table workbook
- save workbook file
- load excel workbook java
language: ar
lastmod: 2026-11-16
og_description: كيفية نسخ الخلايا بين دفاتر Excel في Java. تعلم كيفية تحميل دفتر Excel،
  نسخ نطاق (بما في ذلك جدول محوري) بين الدفاتر، وحفظ ملف الدفتر.
og_image_alt: Screenshot of Java code copying a cell range from one Excel workbook
  to another
og_title: كيفية نسخ الخلايا بين ملفات إكسل في جافا – دليل كامل
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: How to copy cells between Excel workbooks in Java – load a workbook,
    copy range between workbooks (including a pivot table), and save the workbook
    file.
  headline: How to copy cells between Excel workbooks in Java
  type: TechArticle
- description: How to copy cells between Excel workbooks in Java – load a workbook,
    copy range between workbooks (including a pivot table), and save the workbook
    file.
  name: How to copy cells between Excel workbooks in Java
  steps:
  - name: Load the source workbook
    text: '```java import com.aspose.cells.*;'
  - name: Define the range that includes the pivot table
    text: '```java // Define the cell range that you want to copy. // Adjust "A1:G20"
      to match the area that contains your data/pivot table. Range srcRange = srcWs.getCells().createRange("A1:G20");
      ```'
  - name: Create the destination workbook
    text: '```java // Create a new, empty workbook that will receive the copied range.
      Workbook destWb = new Workbook(); // defaults to a single empty sheet Worksheet
      destWs = destWb.getWorksheets().get(0); ```'
  - name: Copy the range to the destination workbook
    text: '```java // Copy the source range to cell A1 of the destination worksheet.
      destWs.getCells().copyRange(srcRange, destWs.getCells().get("A1")); ```'
  - name: Save the destination workbook
    text: '```java // Save the new workbook to disk. destWb.save("YOUR_DIRECTORY/dest.xlsx");
      } } ```'
  type: HowTo
tags:
- Java
- Excel
- Aspose.Cells
- Workbook manipulation
title: كيفية نسخ الخلايا بين دفاتر Excel في Java
url: /ar/java/workbook-operations/how-to-copy-cells-between-excel-workbooks-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية نسخ الخلايا بين دفاتر Excel في Java

إذا كنت بحاجة إلى **نسخ الخلايا** من دفتر Excel إلى آخر باستخدام Java، فإن هذا الدليل يوضح لك طريقة موثوقة للقيام بذلك. ستتعلم كيفية **تحميل دفتر Excel في Java**، نسخ نطاق قد يحتوي على جدول محوري، وأخيرًا **حفظ ملف الدفتر** بالبيانات المنسوخة.

يغطي هذا الدرس:

* تحميل دفتر مصدر واختيار ورقة عمل.  
* تحديد النطاق الدقيق الذي تريد نقله (بما في ذلك جدول محوري).  
* إنشاء دفتر هدف ونسخ النطاق.  
* حفظ ملف الهدف.  

يستخدم المثال مكتبة Aspose.Cells for Java، التي تعمل مع ملفات Excel دون الحاجة إلى Microsoft Office. يعمل الكود على Java 8+ وأي بيئة تطوير حديثة (IntelliJ IDEA, Eclipse, VS Code, إلخ).

---

## المتطلبات المسبقة

| المتطلب | السبب |
|-------------|--------|
| Java Development Kit (JDK) 8 or newer | مطلوب لتجميع وتشغيل الكود. |
| Maven or Gradle build tool | يبسط إضافة تبعية Aspose.Cells. |
| Aspose.Cells for Java library (latest version) | يوفر الفئات `Workbook` و `Worksheet` و `Range` المستخدمة في المثال. |
| Two Excel files (`source.xlsx` and an empty folder for `dest.xlsx`) | يجب أن يحتوي ملف المصدر على البيانات، وبشكل اختياري، جدول محوري تريد نسخه. |

أضف تبعية Aspose.Cells إلى ملف `pom.xml` (Maven) أو `build.gradle` (Gradle). مثال لـ Maven:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- use the latest version -->
</dependency>
```

---

## كيفية نسخ الخلايا باستخدام Aspose.Cells

الخطوات التالية تقودك عبر العملية الكاملة. كل خطوة تتضمن كود Java، شرح **لماذا** هذه الخطوة مهمة، ونصيحة لتجنب الأخطاء الشائعة.

### الخطوة 1: تحميل دفتر المصدر

```java
import com.aspose.cells.*;

public class ExcelCopyDemo {
    public static void main(String[] args) throws Exception {
        // Load the source Excel file (replace with your actual path)
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/source.xlsx");

        // Get the first worksheet (index 0)
        Worksheet srcWs = srcWb.getWorksheets().get(0);
```

**لماذا؟**  
`Workbook` يمثل ملف Excel بالكامل. تحميله يمنحك الوصول إلى جميع أوراق العمل، الخلايا، والكائنات مثل الجداول المحورية. استخدام الورقة الأولى شائع، لكن يمكنك اختيار أي ورقة بالاسم (`srcWb.getWorksheets().get("Sheet2")`).

**نصيحة احترافية:**  
إذا كان ملف المصدر كبيرًا، فكر في تحميله بوضع *كفاءة الذاكرة*: `new Workbook("file.xlsx", new LoadOptions(LoadFormat.XLSX) {{ setMemorySetting(MemorySetting.MEMORY_PREFERENCE); }});`

### الخطوة 2: تحديد النطاق الذي يتضمن الجدول المحوري

```java
        // Define the cell range that you want to copy.
        // Adjust "A1:G20" to match the area that contains your data/pivot table.
        Range srcRange = srcWs.getCells().createRange("A1:G20");
```

**لماذا؟**  
كائن `Range` يجسد كتلة مستطيلة من الخلايا. بتحديد `"A1:G20"` تخبر Aspose.Cells بالضبط أي خلايا—بما في ذلك أي جدول محوري مدمج—تريد نسخها. المكتبة تنسخ تلقائيًا البيانات الأساسية، الأنماط، وتعريفات الجداول المحورية.

**حالة خاصة:**  
إذا كان الجدول المحوري يمتد خارج النطاق المحدد، قم بتوسيع العنوان (مثلاً `"A1:Z100"`). يمكنك أيضًا استخدام `srcWs.getCells().getMaxDataColumn()` و `getMaxDataRow()` لحساب المنطقة المستخدمة ديناميكيًا.

### الخطوة 3: إنشاء دفتر الهدف

```java
        // Create a new, empty workbook that will receive the copied range.
        Workbook destWb = new Workbook();               // defaults to a single empty sheet
        Worksheet destWs = destWb.getWorksheets().get(0);
```

**لماذا؟**  
دفتر جديد يضمن عدم وجود تنسيقات غير مرغوب فيها أو أوراق مخفية تتداخل مع المحتوى المنسوخ. الدفتر الافتراضي يحتوي بالفعل على ورقة عمل واحدة، والتي سنستخدمها كهدف.

### الخطوة 4: نسخ النطاق إلى دفتر الهدف

```java
        // Copy the source range to cell A1 of the destination worksheet.
        destWs.getCells().copyRange(srcRange, destWs.getCells().get("A1"));
```

**لماذا؟**  
`copyRange` يتعامل مع جميع سمات الخلية: القيم، الصيغ، التنسيقات، وحتى مخازن الجداول المحورية. بنسخ إلى `"A1"` تضع النطاق في الزاوية العليا اليسرى من ورقة الهدف، مع الحفاظ على التخطيط الأصلي.

**سؤال شائع:** *هل سيظل الجدول المحوري فعالًا؟*  
نعم. Aspose.Cells ينسخ تعريف الجدول المحوري ومخزنه، لذا يعمل الجدول المحوري تمامًا كما في دفتر المصدر.

### الخطوة 5: حفظ دفتر الهدف

```java
        // Save the new workbook to disk.
        destWb.save("YOUR_DIRECTORY/dest.xlsx");
    }
}
```

**لماذا؟**  
استدعاء `save` يكتب دفتر العمل الموجود في الذاكرة إلى ملف `.xlsx` فعلي. يمكنك أيضًا حفظه بصيغ أخرى (`.xls`, `.csv`, `.pdf`) بتغيير امتداد الملف أو باستخدام `SaveOptions`.

**نصيحة:**  
إذا كنت بحاجة إلى بث الملف إلى استجابة ويب، استخدم `destWb.save(OutputStream, SaveFormat.XLSX);` بدلاً من مسار ملف.

---

## نسخ النطاق بين دفاتر العمل – الكود الكامل

فيما يلي الفئة Java الكاملة الجاهزة للتنفيذ. استبدل `YOUR_DIRECTORY` بالمجلد الفعلي على جهازك.

```java
import com.aspose.cells.*;

public class ExcelCopyDemo {
    public static void main(String[] args) throws Exception {
        // Load the source workbook
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/source.xlsx");
        Worksheet srcWs = srcWb.getWorksheets().get(0);

        // Define the range that includes the data and pivot table
        Range srcRange = srcWs.getCells().createRange("A1:G20");

        // Create a new destination workbook
        Workbook destWb = new Workbook();
        Worksheet destWs = destWb.getWorksheets().get(0);

        // Copy the defined range to the destination workbook
        destWs.getCells().copyRange(srcRange, destWs.getCells().get("A1"));

        // Save the destination workbook
        destWb.save("YOUR_DIRECTORY/dest.xlsx");
    }
}
```

**النتيجة المتوقعة:**  
`dest.xlsx` يحتوي على نسخة مطابقة تمامًا للنطاق `A1:G20` من `source.xlsx`. إذا كان النطاق المصدر يحتوي على جدول محوري، فإن ملف الهدف يعرض نفس الجدول مع ربط مصدر البيانات بشكل صحيح إلى الخلايا المنسوخة.

يمكنك فتح `dest.xlsx` في Excel أو LibreOffice أو أي عارض يدعم `.xlsx` للتحقق من أن القيم، التنسيقات، ووظيفة الجدول المحوري محفوظة.

---

## نسخ دفتر جدول محوري – ما يجب أن تعرفه

* **Pivot cache is copied automatically.** المكتبة تنقل المخزن الأساسي، لذا لا يحتاج الجدول المحوري إلى تحديث يدوي.
* **External data sources are not transferred.** إذا كان الجدول المحوري يجلب بيانات من قاعدة بيانات خارجية، يجب التأكد من أن دفتر الهدف يمكنه الوصول إلى نفس المصدر، أو إعادة إنشاء المخزن محليًا.
* **Large pivot tables may increase memory usage.** للدفاتر الكبيرة جدًا، فكر في زيادة حجم heap للـ JVM (`-Xmx2g`) لتجنب `OutOfMemoryError`.

---

## حفظ ملف الدفتر بصيغ مختلفة

Aspose.Cells يتيح لك حفظ النتيجة إلى صيغ متعددة دون تعديل الكود:

```java
// Save as XLS (Excel 97-2003)
destWb.save("dest.xls");

// Save as CSV (first worksheet only)
destWb.save("dest.csv");

// Save as PDF (visual representation)
destWb.save("dest.pdf");
```

اختر الصيغة التي تتطابق مع عملية المعالجة اللاحقة. منطق `copyRange` نفسه يعمل بغض النظر عن الصيغة النهائية.

---

## تحميل دفتر Excel في Java – نصائح إضافية

* **Loading encrypted files:** استخدم `LoadOptions` مع كلمة مرور:  
  ```java
  LoadOptions opt = new LoadOptions(LoadFormat.XLSX);
  opt.setPassword("myPassword");
  Workbook wb = new Workbook("encrypted.xlsx", opt);
  ```
* **Reading only specific sheets:**  
  ```java
  LoadOptions opt = new LoadOptions(LoadFormat.XLSX);
  opt.setLoadDataOnly(true); // faster if you only need values
  Workbook wb = new Workbook("file.xlsx", opt);
  ```

هذه الخيارات يمكن أن تسرّع خطوة **load excel workbook java**، خاصةً للملفات الكبيرة.

---

## الخلاصة

أنت الآن تعرف **كيفية نسخ الخلايا** بين دفاتر Excel في Java، وكيفية **نسخ النطاق بين دفاتر العمل** الذي يحتوي على **جدول محوري**، وكيفية **حفظ ملف الدفتر** بالصيغ التي تحتاجها. باتباع الخطوات أعلاه، يمكنك دمج معالجة بيانات Excel في أي تطبيق Java—سواء كنت تبني محرك تقارير، خط أنابيب ETL، أو أداة تحويل ملفات بسيطة.

**الخطوات التالية** التي قد تستكشفها:

* استخدم **copy range between workbooks** لدمج تقارير متعددة في

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك الخاصة.

- [حفظ دفتر جديد في Java – دليل نسخ النطاق بين دفاتر العمل](/cells/english/java/workbook-operations/save-new-workbook-in-java-copy-range-between-workbooks-tutor/)
- [كيفية نسخ الجداول المحورية بين دفاتر Excel في Java](/cells/english/java/excel-pivot-tables/how-to-copy-pivot-tables-between-excel-workbooks-in-java/)
- [كيفية نسخ النطاق في Java – نسخ جدول محوري باستخدام Aspose.Cells](/cells/english/java/excel-pivot-tables/how-to-copy-range-in-java-copy-pivot-table-with-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}