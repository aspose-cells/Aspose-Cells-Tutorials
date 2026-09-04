---
date: '2026-02-22'
description: تعلم كيفية أتمتة تقارير Excel باستخدام Aspose.Cells في Java عن طريق استخدام
  CopyOptions وPasteOptions للحفاظ على دقة الصيغ ولصق القيم الظاهرة فقط.
keywords:
- Aspose.Cells Java
- CopyOptions ReferToDestinationSheet
- PasteOptions Excel
title: أتمتة تقارير Excel – إتقان CopyOptions و PasteOptions في Java باستخدام Aspose.Cells
url: /ar/java/cell-operations/aspose-cells-java-copy-paste-options/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# أتمتة إعداد تقارير Excel باستخدام Aspose.Cells: CopyOptions & PasteOptions في Java

هل تبحث عن **أتمتة إعداد تقارير Excel** باستخدام Java؟ مع Aspose.Cells يمكنك نسخ ولصق وتعديل الصيغ برمجياً بحيث تظل تقاريرك دقيقة ويتم نقل البيانات التي تحتاجها فقط. في هذا البرنامج التعليمي سنستعرض ميزتين أساسيتين—**CopyOptions.ReferToDestinationSheet** و **PasteOptions**—اللتين تتيحان لك الحفاظ على مراجع الصيغ ولصق القيم من الخلايا الظاهرة فقط.

## إجابات سريعة
- **ما هو دور `CopyOptions.ReferToDestinationSheet`؟** يضبط الصيغ لتشير إلى ورقة الوجهة عند نسخ البيانات.  
- **كيف يمكنني لصق الخلايا الظاهرة فقط؟** اضبط `PasteOptions.setOnlyVisibleCells(true)` مع `PasteType.VALUES`.  
- **ما هو إصدار المكتبة المطلوب؟** Aspose.Cells 25.3 أو أحدث.  
- **هل أحتاج إلى ترخيص للإنتاج؟** نعم، الترخيص الدائم أو المؤقت يزيل حدود التقييم.  
- **هل يمكنني استخدام Maven أو Gradle؟** كلاهما مدعومان؛ راجع مقتطفات الاعتماد أدناه.

## ما معنى “أتمتة إعداد تقارير Excel”؟
تعني أتمتة إعداد تقارير Excel إنشاء وتوحيد وتنسيق دفاتر عمل Excel برمجياً، مما يلغي خطوات النسخ‑اللصق اليدوية ويقلل الأخطاء. توفر Aspose.Cells واجهة برمجة تطبيقات غنية تتيح لمطوري Java التعامل مع جداول البيانات على نطاق واسع.

## لماذا نستخدم CopyOptions و PasteOptions في إعداد التقارير؟
- **الحفاظ على سلامة الصيغ** عند نقل البيانات بين الأوراق.  
- **استبعاد الصفوف/الأعمدة المخفية** للحفاظ على نظافة وتركيز التقارير.  
- **تحسين الأداء** عن طريق نسخ البيانات الضرورية فقط بدلاً من النطاقات الكاملة.

## المتطلبات المسبقة
- Java 8 أو أعلى.  
- Maven أو Gradle لإدارة الاعتمادات.  
- Aspose.Cells 25.3+ (ترخيص تجريبي، مؤقت، أو دائم).

## إعداد Aspose.Cells لـ Java

أضف المكتبة إلى مشروعك باستخدام أحد الخيارات التالية:

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

### الحصول على الترخيص
- **Free Trial** – مجموعة كاملة من الميزات للتقييم.  
- **Temporary License** – يزيل قيود النسخة التجريبية أثناء الاختبار.  
- **Permanent License** – موصى به لأعباء العمل الإنتاجية.

تهيئة Aspose.Cells في كود Java الخاص بك:

```java
import com.aspose.cells.Workbook;

Workbook workbook = new Workbook("path/to/your/excel/file.xlsx");
```

## دليل خطوة بخطوة

### 1. CopyOptions مع ReferToDestinationSheet

#### نظرة عامة
ضبط `CopyOptions.ReferToDestinationSheet` على `true` يعيد كتابة مراجع الصيغ بحيث تشير إلى الورقة الجديدة بعد عملية النسخ.

#### الخطوة 1: تهيئة Workbook و Worksheets
```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;

String dataDir = "YOUR_DATA_DIRECTORY";
Workbook wb = new Workbook(dataDir + "/book1.xlsx");
Worksheet source = wb.getWorksheets().get(0);
Worksheet destination = wb.getWorksheets().add("DestSheet");
```

#### الخطوة 2: تكوين CopyOptions
```java
import com.aspose.cells.CopyOptions;

CopyOptions options = new CopyOptions();
options.setReferToDestinationSheet(true); // Adjust formulas to the destination sheet
```

#### الخطوة 3: تنفيذ عملية النسخ
```java
destination.getCells().copyRows(source.getCells(), 0, 0, source.getCells().getMaxDisplayRange().getRowCount(), options, null);
wb.save("YOUR_OUTPUT_DIRECTORY/destination.xlsx");
```
*لماذا هذا مهم*: الصيغ التي كانت تشير أصلاً إلى `Sheet1` ستشير الآن بشكل صحيح إلى `DestSheet`، مما يحافظ على موثوقية تقاريرك المؤتمتة.

**نصيحة استكشاف الأخطاء**: إذا استمرت الصيغ في الإشارة إلى الورقة القديمة، تأكد من استدعاء `setReferToDestinationSheet(true)` **قبل** عملية النسخ.

### 2. PasteOptions للقيم فقط من الخلايا الظاهرة

#### نظرة عامة
`PasteOptions` يتيح لك تحديد ما يتم لصقه. باستخدام `PasteType.VALUES` مع `onlyVisibleCells=true` يتم نسخ القيم المعروضة فقط، مع تجاهل الصفوف/الأعمدة المخفية والتنسيق.

#### الخطوة 1: تهيئة Workbook و Worksheets
```java
Workbook wb = new Workbook(dataDir + "/book1.xlsx");
Worksheet source = wb.getWorksheets().get(0);
Worksheet destination = wb.getWorksheets().add("DestSheet");
```

#### الخطوة 2: تكوين PasteOptions
```java
import com.aspose.cells.PasteOptions;
import com.aspose.cells.PasteType;

PasteOptions pasteOptions = new PasteOptions();
pasteOptions.setPasteType(PasteType.VALUES); // Copy only values
pasteOptions.setOnlyVisibleCells(true); // Include only visible cells
```

#### الخطوة 3: تنفيذ عملية اللصق
```java
destination.getCells().copyRows(source.getCells(), 0, 0, source.getCells().getMaxDisplayRange().getRowCount(), null, pasteOptions);
wb.save("YOUR_OUTPUT_DIRECTORY/destination.xlsx");
```
*لماذا هذا مهم*: مثالي لاستخراج البيانات المصفاة أو إنشاء تقارير نظيفة دون صفوف مخفية أو ضوضاء تنسيق.

**نصيحة استكشاف الأخطاء**: تأكد من أن الصفوف/الأعمدة مخفية فعلياً في Excel قبل النسخ؛ وإلا سيتم تضمينها.

## تطبيقات عملية
1. **Financial Consolidation** – دمج الأوراق الشهرية في دفتر عمل رئيسي مع الحفاظ على دقة جميع الصيغ.  
2. **Filtered Data Export** – استخراج الصفوف الظاهرة فقط من جدول مُصفى إلى ورقة ملخص.  
3. **Scheduled Report Generation** – أتمتة إنشاء تقارير Excel الليلية بقيم خلايا دقيقة ومراجع صحيحة.

## اعتبارات الأداء
- **Dispose of Workbooks** عند الانتهاء (`wb.dispose();`) لتحرير الموارد الأصلية.  
- **Batch Operations** – تجميع عدة عمليات نسخ/لصق لتقليل الحمل.  
- **Monitor Memory** – قد تتطلب دفاتر العمل الكبيرة زيادة حجم الذاكرة (`-Xmx2g`).

## الأسئلة المتكررة

**س1: ما هو الغرض من `CopyOptions.ReferToDestinationSheet`؟**  
ج: يعيد كتابة مراجع الصيغ بحيث تشير إلى ورقة الوجهة بعد النسخ، مما يضمن بقاء صيغ التقارير صحيحة.

**س2: كيف يمكنني لصق الخلايا الظاهرة فقط؟**  
ج: اضبط `PasteOptions.setOnlyVisibleCells(true)` واختر `PasteType.VALUES`.

**س3: هل يمكنني استخدام Aspose.Cells دون شراء ترخيص؟**  
ج: نعم، يتوفر نسخة تجريبية مجانية أو ترخيص مؤقت للتقييم، لكن الترخيص الدائم مطلوب للإنتاج.

**س4: لماذا لا تزال بعض المراجع خاطئة بعد النسخ؟**  
ج: تأكد من تمكين `ReferToDestinationSheet` **قبل** عملية النسخ وأن صيغ المصدر لا تحتوي على روابط إلى دفاتر عمل خارجية.

**س5: ما هي أفضل ممارسات إدارة الذاكرة التي يجب اتباعها؟**  
ج: قم بتحرير كائنات `Workbook` عند الانتهاء، عالج الملفات الكبيرة على دفعات، وراقب استخدام ذاكرة JVM.

**س6: هل يمكن دمج CopyOptions و PasteOptions في عملية واحدة؟**  
ج: نعم، يمكنك ربطهما أولاً بالنسخ باستخدام `CopyOptions` ثم تطبيق `PasteOptions` على النطاق المستهدف.

## الموارد
- **الوثائق**: [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)  
- **التنزيل**: [Aspose.Cells Releases for Java](https://releases.aspose.com/cells/java/)  
- **الشراء**: [Buy Aspose.Cells](https://purchase.aspose.com/buy)  
- **نسخة تجريبية مجانية**: [Aspose.Cells Free Trial](https://releases.aspose.com/cells/java/)  
- **ترخيص مؤقت**: [Apply for a Temporary License](https://purchase.aspose.com/temporary-license/)  
- **منتدى الدعم**: [Aspose Support](https://forum.aspose.com/c/cells)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

---

**آخر تحديث:** 2026-02-22  
**تم الاختبار مع:** Aspose.Cells 25.3 for Java  
**المؤلف:** Aspose