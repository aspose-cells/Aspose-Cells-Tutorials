---
category: general
date: 2026-03-01
description: نسخ جدول محوري في جافا مع الحفاظ على المحور، ثم تصدير إكسل إلى PPTX،
  وتعطيل AutoFilter في إكسل، واستخدام Smart Marker لمصفوفات JSON – دليل كامل خطوة
  بخطوة.
draft: false
keywords:
- copy pivot table
- preserve pivot table
- use smart marker
- disable excel autofilter
- export excel to pptx
language: ar
og_description: نسخ جدول محوري في جافا، الحفاظ على تعريف المحور، تصدير إلى PPTX، تعطيل
  AutoFilter، واستخدام Smart Marker – دليل كامل للمطورين.
og_title: نسخ جدول محوري في جافا – احتفظ به، صدّر إلى PPTX
tags:
- Aspose.Cells
- Java
- Excel Automation
title: نسخ جدول محوري في جافا – الحفاظ عليه، تصديره إلى PPTX
url: /ar/java/excel-pivot-tables/copy-pivot-table-in-java-preserve-it-export-to-pptx/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# نسخ جدول محوري في Java – الحفاظ عليه، التصدير إلى PPTX

هل احتجت يوماً إلى **نسخ جدول محوري** من مصنف إلى آخر دون فقدان تعريف الجدول المحوري الأساسي؟ لست وحدك من يحاول حل هذه المشكلة. في العديد من المشاريع الواقعية ستجد نفسك تنقل البيانات، وآخر شيء تريده هو جدول محوري معطوب يسبب أخطاء أثناء التشغيل.  

في هذا الدرس سنستعرض حلاً كاملاً لا يقتصر فقط على **نسخ جدول محوري**، بل يوضح لك أيضاً كيفية **الحفاظ على جدول محوري** عند النسخ، **تصدير Excel إلى PPTX**، **تعطيل AutoFilter في Excel**، و**استخدام Smart Marker** لإدخال مصفوفة JSON في خلية واحدة. في النهاية ستحصل على برنامج Java واحد قابل للتنفيذ يغطي جميع السيناريوهات الأربعة.

## المتطلبات المسبقة

- Java 8 أو أحدث (الكود يعمل مع Java 11 أيضاً)  
- مكتبة Aspose.Cells for Java (الإصدار 23.9 أو أحدث) – يمكنك الحصول عليها من Maven Central  
- إلمام أساسي بمفاهيم Excel مثل الجداول المحورية، الجداول، ومربعات النص  

إذا كنت تفتقد ملف Aspose.Cells JAR، أضف هذا إلى ملف `pom.xml` الخاص بك:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
</dependency>
```

الآن، لنبدأ.

## الخطوة 1: نسخ جدول محوري – الحفاظ على تعريف الجدول المحوري

عند نسخ نطاق الخلايا الذي يحتوي على جدول محوري ببساطة، غالباً ما تُترك بيانات التعريف الخاصة بالجدول المحوري خلفك. توفر لنا Aspose.Cells طريقة أنيقة للحفاظ على التعريف سليمًا باستخدام `copyRange` مع كائن `CopyOptions`.

```java
import com.aspose.cells.*;

public class PivotCopyDemo {

    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the source workbook that contains the pivot table
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/src.xlsx");
        Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);

        // 2️⃣ Define the range that includes the pivot (A1:G20 is just an example)
        Range pivotRange = sourceSheet.getCells().createRange("A1:G20");

        // 3️⃣ Prepare the destination workbook
        Workbook destWorkbook = new Workbook();
        Worksheet destSheet = destWorkbook.getWorksheets().get(0);

        // 4️⃣ Copy the range – the pivot definition travels with it
        destSheet.getCells().copyRange(pivotRange,
                new CellArea(0, 0, 19, 6), // destination area (rows 0‑19, cols 0‑6)
                new CopyOptions());

        // 5️⃣ Save the result
        destWorkbook.save("YOUR_DIRECTORY/dest.xlsx");
    }
}
```

**لماذا يعمل هذا:** `CopyOptions` يخبر Aspose.Cells بنقل كل شيء، بما في ذلك ذاكرة التخزين المؤقت للجدول المحوري وإعدادات الحقول. بدونها، ستحصل على قيم عادية وتفقد القدرة على تحديث الجدول المحوري.

**حالة خاصة:** إذا كان الجدول المحوري المصدر يمتد إلى ما هو أبعد من النطاق المحدد صلباً `A1:G20`، عدّل النطاق وفقاً لذلك أو استخدم `sourceSheet.getPivotTables().get(0).getDataRange()` لجلبه ديناميكياً.

![مثال على نسخ جدول محوري](image.png "نسخ جدول محوري في Java")

*نص بديل للصورة: مخطط نسخ جدول محوري في Java*

## الخطوة 2: تصدير ورقة عمل مع مربع نص قابل للتحرير إلى PPTX

غالباً ما تحتاج إلى تحويل ورقة Excel إلى شريحة PowerPoint—فكر في لوحات التحكم الأسبوعية التي تحتاج إلى عرضها. يمكن لـ Aspose.Cells حفظ ورقة عمل مباشرة كملف PPTX مع الحفاظ على الأشكال مثل مربعات النص.

```java
import com.aspose.cells.*;

public class ExportToPptxDemo {

    public static void main(String[] args) throws Exception {
        // Load workbook that contains a TextBox shape
        Workbook wb = new Workbook("YOUR_DIRECTORY/textbox.xlsx");

        // Export the first worksheet to PPTX
        wb.save("YOUR_DIRECTORY/output.pptx", SaveFormat.PPTX);

        System.out.println("Worksheet exported to PPTX successfully.");
    }
}
```

**ما يحدث:** طريقة `save` مع `SaveFormat.PPTX` تحول الورقة بالكامل، بما في ذلك أي TextBox قابل للتحرير، إلى شريحة PowerPoint. يبقى النص داخل المربع قابلاً للتحرير عند فتح ملف PPTX في PowerPoint.

**نصيحة:** إذا كان لديك عدة أوراق وتريد فقط واحدة محددة، استدعِ `wb.getWorksheets().removeAt(index)` للأوراق الأخرى قبل الحفظ.

## الخطوة 3: تعطيل AutoFilter في Excel من جدول

AutoFilter مفيد للمستخدمين النهائيين، لكن أحياناً تحتاج إلى إيقافه برمجياً—ربما قبل تصدير البيانات أو عند إنشاء تقرير نظيف. إليك كيفية **تعطيل AutoFilter في Excel** على جدول Excel.

```java
import com.aspose.cells.*;

public class DisableAutoFilterDemo {

    public static void main(String[] args) throws Exception {
        Workbook wb = new Workbook("YOUR_DIRECTORY/textbox.xlsx");
        Worksheet sheet = wb.getWorksheets().get(0);

        // Assume the first table in the sheet is the target
        Table table = sheet.getTables().get(0);

        // Turn off the AutoFilter arrows
        table.setShowAutoFilter(false);

        // Save the modified workbook
        wb.save("YOUR_DIRECTORY/noFilter.xlsx");
        System.out.println("AutoFilter disabled and workbook saved.");
    }
}
```

**لماذا قد تحتاج هذا:** التصدير إلى صيغ لا تدعم AutoFilter (مثل CSV أو PDF) قد يتسبب في ظهور أيقونات تصفية عشوائية. تعطيله يضمن مخرجات نظيفة.

**مشكلة شائعة:** إذا لم تحتوي الورقة على جداول، فإن `getTables().get(0)` سيُطلق استثناء `IndexOutOfBoundsException`. تأكد دائماً من فحص `sheet.getTables().size()` أولاً في الكود الإنتاجي.

## الخطوة 4: استخدام Smart Marker – إدراج مصفوفة JSON كقيمة خلية واحدة

Smart Marker هو محرك القوالب الخاص بـ Aspose. إحدى الحيل المفيدة هي التعامل مع مصفوفة JSON كاملة كقيمة خلية واحدة، وهو مثالي للتسجيل أو تمرير البيانات المهيكلة لاحقاً. لن **نستخدم Smart Marker** لتحقيق ذلك.

```java
import com.aspose.cells.*;

public class SmartMarkerDemo {

    public static void main(String[] args) throws Exception {
        Workbook wb = new Workbook("YOUR_DIRECTORY/textbox.xlsx");

        // Initialise the SmartMarker processor with the workbook
        SmartMarkerProcessor processor = new SmartMarkerProcessor(wb);

        // JSON array we want to embed
        String jsonArray = "[{\"Name\":\"John\",\"Age\":30},{\"Name\":\"Anna\",\"Age\":28}]";

        // Configure the processor to treat arrays as a single cell
        processor.setOptions(SmartMarkerOptions.ArrayAsSingle);

        // Apply the marker – assume cell A1 contains the marker ${json}
        processor.apply(jsonArray);

        // Save the result
        wb.save("YOUR_DIRECTORY/smartMarkerResult.xlsx");
        System.out.println("JSON array inserted via Smart Marker.");
    }
}
```

**كيف يعمل:** العلامة `${json}` في المصنف تُستبدل بالسلسلة الكاملة للـ JSON لأننا ضبطنا `ArrayAsSingle`. بدون هذا الخيار، ستحاول Aspose توسيع كل عنصر من المصفوفة إلى صفوف منفصلة.

**اختلاف:** إذا كنت بحاجة إلى تقسيم المصفوفة على صفوف، ما عليك سوى حذف `ArrayAsSingle` ودع Smart Marker يتولى التوسيع تلقائياً.

## مثال عملي كامل – جميع الخطوات مجتمعة

فيما يلي فئة Java واحدة تجمع جميع العمليات التي تناولناها. شغّلها كدالة `main` عادية؛ فقط عدّل مسارات الملفات لتتناسب مع بيئتك.

```java
import com.aspose.cells.*;

public class CompleteExcelAutomation {

    public static void main(String[] args) throws Exception {
        // ----------- Step 1: Copy Pivot Table -----------
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/src.xlsx");
        Worksheet srcSheet = srcWb.getWorksheets

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}