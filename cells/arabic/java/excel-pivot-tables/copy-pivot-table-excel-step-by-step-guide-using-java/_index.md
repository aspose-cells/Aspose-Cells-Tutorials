---
category: general
date: 2026-06-27
description: نسخ جدول محوري في إكسل باستخدام جافا في دقائق – تعلّم كيفية نسخ النطاق
  إلى مصنف آخر واكتشف كيفية نسخ الجدول المحوري بكفاءة.
draft: false
keywords:
- copy pivot table excel
- copy range to another workbook
- how to copy pivot table
language: ar
og_description: نسخ جدول محوري في إكسل باستخدام جافا. يوضح هذا الدليل كيفية نسخ النطاق
  إلى مصنف آخر ويجيب على سؤال كيفية نسخ الجدول المحوري مع مثال كامل.
og_title: نسخ جدول محوري إكسل – دليل جافا
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: Copy pivot table excel with Java in minutes – learn how to copy range
    to another workbook and discover how to copy pivot table efficiently.
  headline: Copy Pivot Table Excel – Step‑by‑Step Guide Using Java
  type: TechArticle
- description: Copy pivot table excel with Java in minutes – learn how to copy range
    to another workbook and discover how to copy pivot table efficiently.
  name: Copy Pivot Table Excel – Step‑by‑Step Guide Using Java
  steps:
  - name: Expected Result
    text: '- Opening `destination.xlsx` shows a sheet named **CopiedPivot**. - The
      sheet contains a pivot table that can be refreshed, filtered, and rearranged
      just like the original. - No error messages appear in the console, confirming
      that **copy pivot table excel** succeeded.'
  - name: What if the source workbook has multiple pivot tables?
    text: 'You can repeat the range‑selection logic for each pivot table, or you can
      copy the entire worksheet:'
  - name: How to handle external data connections?
    text: 'If your pivot table pulls data from an external database, the destination
      workbook will retain the connection string. To avoid broken links, update the
      connection after copying:'
  - name: Does this work with .xls files?
    text: Yes. Aspose.Cells abstracts the file format, so the same code works for
      `.xls`, `.xlsx`, `.xlsb`, and even `.ods`. Just change the file extension in
      the `Workbook` constructors.
  type: HowTo
tags:
- pivot-table
- excel
- java
- aspose-cells
title: نسخ جدول محوري في إكسل – دليل خطوة بخطوة باستخدام جافا
url: /ar/java/excel-pivot-tables/copy-pivot-table-excel-step-by-step-guide-using-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# نسخ جدول محوري Excel – دليل Java

هل تساءلت يومًا كيف **copy pivot table excel** الملفات دون فقدان اتصالات البيانات الأساسية؟ لست وحدك. يواجه العديد من المطورين صعوبة عندما يحاولون نقل جدول محوري من مصنف إلى آخر، لينتهي بهم الأمر بنطاق ثابت أو مرجع مكسور.  

الأخبار السارة؟ مع بضع أسطر من Java والمكتبة المناسبة، يمكنك **copy pivot table excel** المصنفات بنظافة، مع الحفاظ على كل حقل، مرشح، وتخطيط. في هذا الدليل سنظهر لك أيضًا **how to copy pivot table** باستخدام Aspose.Cells for Java API، وسنضيف نصائح حول **copy range to another workbook** لتلك السيناريوهات الخاصة.

> **ما ستخرج به:** برنامج قابل للتنفيذ بالكامل يقوم بتحميل مصنف المصدر، نسخ النطاق الذي يحتوي على الجدول المحوري، وحفظ مصنف جديد يبدو تمامًا كالأصلي.

## المتطلبات المسبقة

قبل أن نبدأ، تأكد من وجود:

- Java 17 أو أحدث (الكود يُترجم مع أي JDK حديث).
- Aspose.Cells for Java 23.10 أو أحدث – النسخة التجريبية المجانية تعمل جيدًا للاختبار.
- ملف Excel مصدر (`source.xlsx`) يحتوي بالفعل على جدول محوري في ورقة العمل الأولى.
- بيئة تطوير متكاملة (IDE) أو إعداد بناء بسيط عبر سطر الأوامر (Maven/Gradle).

لا توجد تبعيات خارجية أخرى مطلوبة.

## الخطوة 1: إعداد المشروع واستيراد الفئات

أولاً، أنشئ مشروع Maven (أو Gradle إذا كنت تفضل) وأضف تبعية Aspose.Cells:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
    <classifier>jdk17</classifier>
</dependency>
```

الآن استورد الفئات التي سنحتاجها:

```java
import com.aspose.cells.*;
import java.io.IOException;
```

> **نصيحة احترافية:** حافظ على تنظيم مجلد `src/main/resources`؛ ضع `source.xlsx` هناك وأشر إليه بمسار نسبي لتجنب الترميز الصلب للمسارات المطلقة.

## الخطوة 2: تحميل مصنف المصدر الذي يحتوي على الجدول المحوري

السطر الأول في أي عملية **copy pivot table excel** هو تحميل المصنف الذي يحتوي على الجدول المحوري الذي تريد نسخه.

```java
// Step 2: Load the source workbook that contains the pivot table
Workbook srcWb = new Workbook("src/main/resources/source.xlsx");
```

لماذا نقوم بتحميل المصنف بالكامل بدلاً من الورقة فقط؟ لأن ذاكرة التخزين المؤقت للجدول المحوري (pivot cache) تعيش على مستوى المصنف؛ نسخ الورقة فقط سيكسر الذاكرة المؤقتة وسيتحول جدولك المحوري إلى نطاق عادي.

## الخطوة 3: الحصول على ورقة العمل وتعريف نطاق الجدول المحوري

بعد ذلك، نحدد ورقة العمل والكتلة الخلوية الدقيقة التي تحيط بالجدول المحوري. في معظم الحالات يبدأ الجدول المحوري من `A1`، لكن عليك تعديل النطاق ليتطابق مع ملفك.

```java
// Step 3: Access the worksheet where the pivot table resides
Worksheet srcWs = srcWb.getWorksheets().get(0);

// Define the range that includes the pivot table (e.g., A1:E20)
Range srcRange = srcWs.getCells().createRange("A1:E20");
```

إذا لم تكن متأكدًا من النطاق، يمكنك السماح لـ Aspose.Cells بحساب الخلايا المستخدمة:

```java
int maxRow = srcWs.getCells().getMaxDataRow();
int maxCol = srcWs.getCells().getMaxDataColumn();
String autoRange = String.format("A1:%s%d",
        CellsHelper.columnIndexToName(maxCol), maxRow + 1);
Range srcRange = srcWs.getCells().createRange(autoRange);
```

هذا المقتطف الصغير مفيد عندما تحتاج إلى **copy range to another workbook** دون الترميز الصلب للعنوان.

## الخطوة 4: إنشاء مصنف الوجهة

الآن نقوم بإنشاء مصنف جديد سيستقبل الجدول المحوري المنسوخ. هذا هو جوهر **how to copy pivot table** — تنشئ مساحة نظيفة ثم تلصق النطاق.

```java
// Step 4: Create a new destination workbook (or load an existing one)
Workbook dstWb = new Workbook(); // empty workbook by default
```

إذا كان لديك ملف قالب تريد إثرائه، استبدل المنشئ بـ `new Workbook("template.xlsx")`.

## الخطوة 5: إضافة ورقة عمل إلى مصنف الوجهة

على الرغم من أن `Workbook` الجديد يحتوي بالفعل على ورقة افتراضية واحدة، سنضيف ورقة ثانية لتوضيح عملية النسخ إلى موقع محدد.

```java
// Step 5: Add a new worksheet to the destination workbook
Worksheet dstWs = dstWb.getWorksheets().add();
```

يمكنك إعادة تسمية الورقة للوضوح:

```java
dstWs.setName("CopiedPivot");
```

## الخطوة 6: نسخ النطاق – الحفاظ على الجدول المحوري

إليك السطر السحري الذي فعليًا **copy range to another workbook** مع الحفاظ على الجدول المحوري سليمًا. كائن `CopyOptions` يخبر Aspose.Cells بالحفاظ على كل شيء، بما في ذلك ذاكرة التخزين المؤقت للجدول المحوري.

```java
// Step 6: Copy the range—pivot table is preserved—to the new worksheet at A1
CopyOptions copyOptions = new CopyOptions();
copyOptions.setPasteType(PasteType.PASTE_ALL);
dstWs.getCells().copyRange(srcRange, "A1", copyOptions);
```

لماذا نحدد `PasteType.PASTE_ALL`؟ لأن عملية اللصق الافتراضية تنسخ القيم والتنسيق فقط، متجاهلة ذاكرة التخزين المؤقت للجدول المحوري. بطلب `PASTE_ALL` صراحةً، نضمن أن مصنف الوجهة يستقبل جدولًا محوريًا كامل الوظائف.

## الخطوة 7: حفظ مصنف الوجهة

أخيرًا، اكتب الملف الجديد إلى القرص. بعد هذه الخطوة يمكنك فتح `destination.xlsx` في Excel ورؤية الجدول المحوري تمامًا كما ظهر في ملف المصدر.

```java
// Step 7: Save the destination workbook with the copied pivot table
dstWb.save("src/main/resources/destination.xlsx");
```

### النتيجة المتوقعة

- فتح `destination.xlsx` يُظهر ورقة باسم **CopiedPivot**.
- الورقة تحتوي على جدول محوري يمكن تحديثه وتصفيةه وإعادة ترتيبه مثل الأصلي.
- لا تظهر رسائل خطأ في وحدة التحكم، مما يؤكد نجاح **copy pivot table excel**.

## أسئلة شائعة وحالات خاصة

### ماذا لو كان مصنف المصدر يحتوي على جداول محورية متعددة؟

يمكنك تكرار منطق اختيار النطاق لكل جدول محوري، أو يمكنك نسخ الورقة بالكامل:

```java
srcWs.getCells().copy(dstWs.getCells());
```

نسخ الورقة بأكملها ينقل أيضًا جميع ذاكرات التخزين المؤقت للجدول المحوري، مما يجعلها طريقة سريعة لـ **copy range to another workbook** عندما يكون لديك العديد من الجداول.

### كيف تتعامل مع اتصالات البيانات الخارجية؟

إذا كان جدولك المحوري يجلب البيانات من قاعدة بيانات خارجية، سيحتفظ مصنف الوجهة بسلسلة الاتصال. لتجنب الروابط المكسورة، حدّث الاتصال بعد النسخ:

```java
PivotTable pt = dstWs.getPivotTables().get(0);
pt.getPivotCache().setExternalDataSource("newConnectionString");
```

### هل يعمل هذا مع ملفات .xls؟

نعم. Aspose.Cells يج abstracts تنسيق الملف، لذا يعمل نفس الكود مع `.xls`، `.xlsx`، `.xlsb`، وحتى `.ods`. فقط غيّر امتداد الملف في منشئي `Workbook`.

## مثال عملي كامل

لنجمع كل شيء معًا، إليك فئة Java جاهزة للتنفيذ توضح **how to copy pivot table** من مصنف إلى آخر:

```java
import com.aspose.cells.*;

public class CopyPivotTableExcel {
    public static void main(String[] args) throws Exception {
        // Load source workbook containing the pivot table
        Workbook srcWb = new Workbook("src/main/resources/source.xlsx");
        Worksheet srcWs = srcWb.getWorksheets().get(0);

        // Determine the used range automatically (covers the pivot table)
        int maxRow = srcWs.getCells().getMaxDataRow();
        int maxCol = srcWs.getCells().getMaxDataColumn();
        String rangeAddress = String.format("A1:%s%d",
                CellsHelper.columnIndexToName(maxCol), maxRow + 1);
        Range srcRange = srcWs.getCells().createRange(rangeAddress);

        // Create destination workbook and add a sheet
        Workbook dstWb = new Workbook();
        Worksheet dstWs = dstWb.getWorksheets().add();
        dstWs.setName("CopiedPivot");

        // Copy the range with all pivot information preserved
        CopyOptions opts = new CopyOptions();
        opts.setPasteType(PasteType.PASTE_ALL);
        dstWs.getCells().copyRange(srcRange, "A1", opts);

        // Save the result
        dstWb.save("src/main/resources/destination.xlsx");
        System.out.println("Pivot table copied successfully!");
    }
}
```

شغّل الفئة، افتح `destination.xlsx`، وسترى النسخة المطابقة تمامًا للجدول المحوري الأصلي. 🎉

## الخلاصة

لقد استعرضنا للتو سير عمل كامل لـ **copy pivot table excel** باستخدام Java. من خلال تحميل مصنف المصدر، تحديد نطاق الجدول المحوري، واستخدام `CopyOptions` مع `PASTE_ALL`، يمكنك بثقة **copy range to another workbook** مع الحفاظ على كل ميزات الجدول المحوري.  

إذا كنت curious حول **how to copy pivot table** بلغات أخرى، فإن المفاهيم نفسها تنطبق — فقط استبدل Aspose.Cells SDK بالمنصة المناسبة. بعد ذلك، قد تستكشف تحديث الجدول المحوري المنسوخ برمجيًا، أو تصديره إلى PDF لأغراض التقارير.  

هل لديك تعديل على هذا السيناريو؟ ربما تحتاج إلى نسخ مخطط مرتبط بجدول محوري، أو تريد معالجة مجموعة من الملفات دفعة واحدة. تلك المواضيع هي امتدادات طبيعية لما غطينا اليوم.  

جرّب الكود، عدّل النطاق، ودع مغامرات أتمتة Excel تبدأ. Happy coding!

## ما الذي ينبغي أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف نهج تنفيذ بديلة في مشاريعك الخاصة.

- [كيفية تحديث مصدر جدول محوري Excel باستخدام Aspose.Cells for Java: دليل شامل](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [أتمتة تنسيق وحفظ جدول محوري Excel باستخدام Aspose.Cells for Java: دليل شامل](/cells/english/java/data-analysis/excel-pivot-table-styling-saving-aspose-cells-java/)
- [معالجة جدول محوري Excel باستخدام Aspose.Cells Java: دليل شامل](/cells/english/java/data-analysis/excel-pivot-table-manipulation-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}