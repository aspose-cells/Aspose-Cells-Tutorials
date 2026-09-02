---
date: '2026-09-02'
description: تعلم كيفية إضافة slicer إلى ملفات Excel باستخدام Aspose.Cells for Java،
  مما يتيح تصفية بيانات قوية، ولوحات تحكم تفاعلية، وتحليل أسرع.
keywords:
- how to add slicer
- load excel workbook java
- filter data excel slicer
- insert slicer worksheet
- aspose cells filtering
lastmod: '2026-09-02'
og_description: كيفية إضافة slicer إلى Excel باستخدام Aspose.Cells for Java – دليل
  خطوة بخطوة يوضح لك كيفية تحميل workbook، إرفاق slicer تفاعلي، وحفظ الملف لتقارير
  ديناميكية.
og_image_alt: Developer guide showing Java code that adds an Excel slicer using Aspose.Cells
og_title: كيفية إضافة slicer إلى Excel باستخدام Aspose.Cells for Java
schemas:
- author: Aspose
  dateModified: '2026-09-02'
  description: Learn how to add slicer to Excel workbooks using Aspose.Cells for Java,
    enabling powerful data filtering, interactive dashboards, and faster analysis.
  headline: How to add slicer to Excel with Aspose.Cells for Java
  type: TechArticle
- description: Learn how to add slicer to Excel workbooks using Aspose.Cells for Java,
    enabling powerful data filtering, interactive dashboards, and faster analysis.
  name: How to add slicer to Excel with Aspose.Cells for Java
  steps:
  - name: '**Free trial:** Download the library and experiment with its capabilities.'
    text: '**Free trial:** Download the library and experiment with its capabilities.'
  - name: '**Temporary license:** Request a temporary license for extended testing
      at [Aspose''s Temporary License Page](https://purchase.aspose.com/temporary-license/).'
    text: '**Temporary license:** Request a temporary license for extended testing
      at [Aspose''s Temporary License Page](https://purchase.aspose.com/temporary-license/).'
  - name: '**Purchase license:** For production use, buy a full license from [Aspose
      Purchase](https://purchase.aspose.com/buy).'
    text: '**Purchase license:** For production use, buy a full license from [Aspose
      Purchase](https://purchase.aspose.com/buy).'
  - name: '**Financial reporting:** Filter quarterly sales figures with a single click
      to spot trends.'
    text: '**Financial reporting:** Filter quarterly sales figures with a single click
      to spot trends.'
  - name: '**Inventory management:** View stock levels by product category without
      rebuilding queries.'
    text: '**Inventory management:** View stock levels by product category without
      rebuilding queries.'
  - name: '**HR analytics:** Quickly compare employee performance across departments.'
    text: '**HR analytics:** Quickly compare employee performance across departments.'
  type: HowTo
- questions:
  - answer: Yes – call `worksheet.getSlicers().add` repeatedly with different column
      indexes or positions.
    question: Can I add multiple slicers to the same table?
  - answer: Absolutely – the same `add` method works with pivot tables as long as
      they exist on the worksheet.
    question: Does Aspose.Cells support slicers for PivotTables?
  - answer: You can modify properties such as `setStyle`, `setCaption`, `setWidth`,
      and `setHeight` after creation.
    question: Is it possible to customize slicer style programmatically?
  - answer: Aspose.Cells for Java 25.3 supports Java 8 and newer, including Java 11,
      17, and later LTS releases.
    question: What Java versions are compatible?
  - answer: Use `worksheet.getSlicers().removeAt(index)`, where `index` corresponds
      to the slicer’s position in the collection.
    question: How do I remove a slicer that is no longer needed?
  type: FAQPage
tags:
- add slicer
- Aspose.Cells
- Java Excel automation
- data filtering
- Excel slicer
title: كيفية إضافة slicer إلى Excel باستخدام Aspose.Cells for Java
url: /ar/java/advanced-features/add-slicers-excel-aspose-cells-java-guide/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية إضافة مقطع إلى Excel باستخدام Aspose.Cells for Java

## مقدمة

في التطبيقات الحديثة المعتمدة على البيانات، **how to add slicer** إلى دفاتر Excel هو طلب شائع للمطورين الذين يحتاجون إلى تقارير تفاعلية جاهزة للتصفية. يتيح لك Aspose.Cells for Java إدراج المقاطع برمجياً في الجداول، مما يمنح المستخدمين النهائيين نفس تجربة النقر للتصفية التي يحصلون عليها في واجهة المستخدم المكتبية. في هذا الدليل ستتعرف على سبب أهمية المقاطع، وكيفية إعداد المكتبة، والكود الدقيق المطلوب لتحميل مصنف، إرفاق مقطع، وحفظ النتيجة.

**What you’ll learn**
- كيفية عرض نسخة Aspose.Cells for Java الحالية  
- كيفية **load Excel workbook Java** والوصول إلى الورقة المستهدفة  
- كيفية تحديد جدول معين وإرفاق مقطع  
- كيفية استخدام المقطع لتطبيق **filter data Excel slicer** النمط  
- كيفية حفظ المصنف المعدل  

قبل أن تبدأ، تأكد من وجود المتطلبات المسبقة المذكورة أدناه.

## إجابات سريعة
- **ما هو المقطع؟** مرشح بصري تفاعلي يتيح للمستخدمين تضييق البيانات في جدول أو جدول محوري بنقرة واحدة.  
- **ما نسخة Aspose.Cells المطلوبة؟** Aspose.Cells for Java 25.3 أو أحدث.  
- **هل أحتاج إلى ترخيص؟** نسخة تجريبية مجانية تعمل للتقييم؛ الترخيص إلزامي للنشر في بيئات الإنتاج.  
- **هل يمكنني تحميل مصنف موجود؟** نعم – استدعِ `new Workbook("path/to/file.xlsx")`.  
- **هل سيتصرف المقطع مثل المقطع الأصلي في Excel؟** بالتأكيد – يقدم نفس واجهة المستخدم وإمكانيات التصفية.

## كيفية إضافة مقطع إلى Excel باستخدام Aspose.Cells for Java؟

لإضافة مقطع، أولاً قم بتحميل المصنف المستهدف، ثم أنشئ كائن مقطع مرتبط بعمود الجدول المطلوب، وضع المقطع على ورقة العمل، وأخيراً احفظ المصنف. توضح الخطوات أدناه كل إجراء من هذه الإجراءات، مع مقتطفات كود لإعداد المشروع، إنشاء المقطع، وضعه، وإخراج الملف.

### المتطلبات المسبقة

قبل تنفيذ Aspose.Cells for Java، تأكد من وجود:

#### المكتبات المطلوبة والإصدارات

قم بتضمين Aspose.Cells كاعتماد باستخدام Maven أو Gradle:

**Maven:**
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

**Gradle:**
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

#### متطلبات إعداد البيئة
- Java Development Kit (JDK) 8 أو أحدث مثبت.  
- بيئة تطوير متكاملة مثل IntelliJ IDEA أو Eclipse لتحرير وتشغيل الكود.

#### المتطلبات المعرفية
يتطلب معرفة أساسية ببرمجة Java؛ الإلمام بهياكل ملفات Excel مفيد لكنه ليس إلزامياً.

### إعداد Aspose.Cells for Java

أولاً، احصل على ترخيص تجريبي أو دائم من الموقع الرسمي:

#### خطوات الحصول على الترخيص
1. **Free trial:** تحميل المكتبة وتجربة إمكانياتها.  
2. **Temporary license:** طلب ترخيص مؤقت لاختبار موسع على [Aspose's Temporary License Page](https://purchase.aspose.com/temporary-license/).  
3. **Purchase license:** للاستخدام الإنتاجي، اشترِ ترخيصًا كاملاً من [Aspose Purchase](https://purchase.aspose.com/buy).

#### التهيئة الأساسية
تهيئة Aspose.Cells في تطبيق Java الخاص بك:
```java
import com.aspose.cells.*;

public class SetupAsposeCells {
    public static void main(String[] args) throws Exception {
        // Set license if available
        License license = new License();
        license.setLicense("path/to/your/license/file.lic");

        System.out.println("Aspose.Cells is ready to use!");
    }
}
```
مع تهيئة المكتبة، أنت جاهز للعمل مع ملفات Excel.

## لماذا نستخدم المقاطع في Excel؟

توفر المقاطع تصفية فورية بنقرة دون الحاجة إلى كتابة صيغ أو كود VBA. إنها تحسن قابلية قراءة اللوحات، تمكّن من استكشاف البيانات بسرعة، وتقلل الحاجة إلى تقارير ثابتة متعددة. في عمليات النشر على نطاق واسع، يمكن للمقاطع تقليل وقت التحليل حتى 70 % لأن المستخدمين لم يعودوا بحاجة إلى إعادة بناء الاستعلامات يدويًا.

## تصفية البيانات باستخدام المقطع

المقاطع هي الطريقة البصرية لتطبيق **filter data Excel slicer**. بمجرد إرفاقها بجدول، ينقر المستخدمون على أزرار المقطع لإخفاء أو إظهار الصفوف التي تلبي المعايير المحددة—بدون صيغ. يوضح هذا القسم لماذا تُعد المقاطع نقطة تحول للتقارير التفاعلية في Excel.

## دليل التنفيذ

فيما يلي دليل خطوة بخطوة يوضح بالضبط كيفية إضافة مقطع إلى جدول Excel.

### عرض نسخة Aspose.Cells for Java

توفر فئة `VersionInfo` نسخة المكتبة الحالية، وهو أمر مفيد للتصحيح والدعم.

`VersionInfo` هي فئة مساعدة تُعيد سلسلة نسخة Aspose.Cells.  
```java
System.out.println("Aspose.Cells version: " + com.aspose.cells.VersionInfo.getVersion());
```
معرفة النسخة تساعدك على التأكد من أنك تستخدم إصدار يدعم المقاطع (متاح منذ 20.9 فصاعدًا).

### تحميل مصنف Excel موجود  

للتعامل مع مصنف، أولاً أنشئ كائن `Workbook`.

`Workbook` يمثل ملف Excel كامل في الذاكرة، مكشوفًا عن الأوراق والجداول والمكونات الأخرى.  
```java
Workbook workbook = new Workbook("input.xlsx");
```
يقوم هذا بتحميل الملف دون قفل المصدر، مما يسمح بعمليات القراءة والكتابة.

### الوصول إلى ورقة عمل وجدول محددين  

بعد التحميل، حدد ورقة العمل التي تحتوي على الجدول المستهدف.

`Worksheet` هو الكائن الذي يحمل الصفوف والأعمدة والجداول لورقة واحدة.  
```java
Worksheet sheet = workbook.getWorksheets().get("SalesData");
Table table = sheet.getTables().get(0); // assumes the first table is the target
```
إذا كان المصنف يحتوي على جداول متعددة، عدّل الفهرس أو استخدم اسم الجدول.

### إضافة مقطع إلى جدول Excel  

الآن سنقوم **add a slicer** لتصفية الجدول حسب عمود “Region” ووضعه في الخلية `H5`.

`Slicer` هي الفئة التي تنشئ واجهة التصفية التفاعلية.  
```java
int slicerIndex = sheet.getSlicers().add(table.getIndex(), 2, "H5"); // column index 2 = Region
Slicer slicer = sheet.getSlicers().get(slicerIndex);
slicer.setCaption("Region");
slicer.setStyle(SlicerStyle.Light1);
```
يظهر المقطع تمامًا حيث تحدده، ويمكنك تخصيص العنوان، النمط، والحجم برمجياً.

### حفظ المصنف المعدل  

أخيرًا، اكتب التغييرات إلى القرص.

`Workbook.save` يحفظ التمثيل في الذاكرة إلى ملف فعلي.  
```java
workbook.save("output_with_slicer.xlsx");
```
تذكر استدعاء `workbook.dispose()` في الخدمات طويلة التشغيل لتحرير الموارد الأصلية.

## التطبيقات العملية

إضافة المقاطع باستخدام Aspose.Cells for Java تعزز تحليل البيانات في العديد من السيناريوهات:

1. **Financial reporting:** تصفية أرقام المبيعات ربع السنوية بنقرة واحدة لتحديد الاتجاهات.  
2. **Inventory management:** عرض مستويات المخزون حسب فئة المنتج دون إعادة بناء الاستعلامات.  
3. **HR analytics:** مقارنة أداء الموظفين عبر الأقسام بسرعة.  

يمكنك دمج إنشاء المقاطع مع استيراد البيانات الآلي من قواعد البيانات أو خدمات الويب لإنشاء خطوط تقارير شاملة من البداية إلى النهاية.

## اعتبارات الأداء

عند معالجة مصنفات كبيرة، ضع في اعتبارك النصائح التالية:

- **Memory management:** استدعاء `workbook.dispose()` بعد الانتهاء لتحرير الذاكرة الأصلية.  
- **Batch processing:** تقسيم الملفات الكبيرة إلى أجزاء أصغر للحفاظ على حجم الذاكرة تحت السيطرة.  
- **Streaming API:** للملفات التي تزيد عن 200 MB، استخدم وضع البث `LoadOptions` لتجنب تحميل المصنف بالكامل في الذاكرة.

يمكن لـ Aspose.Cells معالجة **أكثر من 100 تنسيق إدخال وإخراج** ومعالجة مصنفات مئات الصفحات بأقل من 200 MB من RAM عندما يكون البث مفعلاً.

## المشكلات الشائعة والحلول

| المشكلة | الحل |
|-------|----------|
| **Slicer not visible** | تأكد من أن الجدول المستهدف يحتوي على عمود واحد على الأقل بقيم متميزة؛ تحتاج المقاطع إلى عناصر فريدة للعرض. |
| **Exception on `add` method** | تحقق من أن مرجع الخلية (مثل `"H5"`) ضمن نطاق الورقة المستخدمة وأن فهرس العمود يطابق عمودًا موجودًا في الجدول. |
| **License not applied** | تأكد من صحة مسار ملف الترخيص وأن السطر `License license = new License(); license.setLicense("Aspose.Total.Java.lic");` يُنفّذ قبل أي استدعاءات لـ Aspose.Cells. |

## الأسئلة المتكررة

**س: هل يمكنني إضافة مقاطع متعددة إلى نفس الجدول؟**  
ج: نعم – استدعِ `worksheet.getSlicers().add` بشكل متكرر مع فهارس أعمدة أو مواضع مختلفة.

**س: هل يدعم Aspose.Cells المقاطع لجداول PivotTables؟**  
ج: بالتأكيد – تعمل نفس طريقة `add` مع الجداول المحورية طالما أنها موجودة على الورقة.

**س: هل من الممكن تخصيص نمط المقطع برمجياً؟**  
ج: يمكنك تعديل خصائص مثل `setStyle`، `setCaption`، `setWidth`، و `setHeight` بعد الإنشاء.

**س: ما إصدارات Java المتوافقة؟**  
ج: يدعم Aspose.Cells for Java 25.3 إصدارات Java 8 وما فوق، بما فيها Java 11، 17، وإصدارات LTS اللاحقة.

**س: كيف يمكنني إزالة مقطع لم يعد مطلوباً؟**  
ج: استخدم `worksheet.getSlicers().removeAt(index)`، حيث يشير `index` إلى موقع المقطع في المجموعة.

**آخر تحديث:** 2026-09-02  
**تم الاختبار مع:** Aspose.Cells 25.3 for Java  
**المؤلف:** Aspose  









```java
import com.aspose.cells.*;

public class DisplayAsposeCellsVersion {
    public static void main(String[] args) throws Exception {
        String version = CellsHelper.getVersion();
        System.out.println("Aspose.Cells for Java Version: " + version);
    }
}
```

```java
import com.aspose.cells.*;

public class LoadExcelWorkbook {
    public static void main(String[] args) throws Exception {
        String dataDir = "YOUR_DATA_DIRECTORY";
        Workbook workbook = new Workbook(dataDir + "/sampleCreateSlicerToExcelTable.xlsx");
    }
}
```

```java
import com.aspose.cells.*;

public class AccessWorksheetAndTable {
    public static void main(String[] args) throws Exception {
        String dataDir = "YOUR_DATA_DIRECTORY";
        Workbook workbook = new Workbook(dataDir + "/sampleCreateSlicerToExcelTable.xlsx");
        
        Worksheet worksheet = workbook.getWorksheets().get(0);
        ListObject table = worksheet.getListObjects().get(0);
    }
}
```

```java
import com.aspose.cells.*;

public class AddSlicerToExcelTable {
    public static void main(String[] args) throws Exception {
        String dataDir = "YOUR_DATA_DIRECTORY";
        Workbook workbook = new Workbook(dataDir + "/sampleCreateSlicerToExcelTable.xlsx");
        
        Worksheet worksheet = workbook.getWorksheets().get(0);
        ListObject table = worksheet.getListObjects().get(0);
        
        int idx = worksheet.getSlicers().add(table, 0, "H5");
    }
}
```

```java
import com.aspose.cells.*;

public class SaveExcelWorkbookWithSlicer {
    public static void main(String[] args) throws Exception {
        String dataDir = "YOUR_DATA_DIRECTORY";
        String outDir = "YOUR_OUTPUT_DIRECTORY";
        
        Workbook workbook = new Workbook(dataDir + "/sampleCreateSlicerToExcelTable.xlsx");
        
        Worksheet worksheet = workbook.getWorksheets().get(0);
        ListObject table = worksheet.getListObjects().get(0);
        
        int idx = worksheet.getSlicers().add(table, 0, "H5");
        
        workbook.save(outDir + "/outputCreateSlicerToExcelTable.xlsx", SaveFormat.XLSX);
    }
}
```

## دروس ذات صلة

- [إدارة دفاتر Excel والمقاطع باستخدام Aspose.Cells for Java&#58; دليل شامل](/cells/java/workbook-operations/manage-excel-workbooks-aspose-cells-java/)
- [إتقان جداول Pivot في Excel باستخدام Aspose.Cells for Java&#58; دليل شامل لتحليل البيانات](/cells/java/data-analysis/excel-pivot-tables-aspose-cells-java-tutorial/)
- [كيفية تصفية البيانات بفعالية أثناء تحميل دفاتر Excel باستخدام Aspose.Cells في Java](/cells/java/data-analysis/filter-data-excel-aspose-cells-java-tutorial/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}