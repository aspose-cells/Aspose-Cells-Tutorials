---
date: '2026-10-28'
description: تعلم كيفية لصق القيم باستخدام خيارات النسخ واللصق في Aspose.Cells بلغة
  Java، مع كود خطوة بخطوة، وإعداد تبعية Maven، ونصائح الترخيص.
keywords:
- how to paste values
- aspose cells maven dependency
- java generate excel report
- aspose cells license java
- copyoptions refertodestinationsheet
lastmod: '2026-10-28'
og_description: تعلم كيفية لصق القيم باستخدام خيارات النسخ واللصق في Aspose.Cells
  بلغة Java، مع كود خطوة بخطوة، وإعداد تبعية Maven، ونصائح الترخيص.
og_image_alt: Developer guide showing Java code for copying and pasting Excel data
  with Aspose.Cells
og_title: كيفية لصق القيم باستخدام خيارات النسخ واللصق في Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-10-28'
  description: Learn how to paste values using Aspose.Cells copy and paste options
    in Java, with step‑by‑step code, Maven dependency setup, and licensing tips.
  headline: How to paste values with Aspose.Cells copy and paste options
  type: TechArticle
- questions:
  - answer: It rewrites formula references so they point to the destination sheet
      after a copy, ensuring reporting formulas stay correct.
    question: What is `CopyOptions.ReferToDestinationSheet` used for?
  - answer: Set `PasteOptions.setOnlyVisibleCells(true)` and choose `PasteType.VALUES`.
    question: How do I paste only visible cells?
  - answer: Yes, a free trial or temporary license is available for evaluation, but
      a permanent license is required for production.
    question: Can I use Aspose.Cells without purchasing a license?
  - answer: Double‑check that `ReferToDestinationSheet` is enabled **before** the
      copy operation and that the source formulas don’t contain external workbook
      links.
    question: Why are some references still wrong after copying?
  - answer: Dispose of `Workbook` objects when finished, process large files in chunks,
      and monitor JVM heap usage.
    question: What memory‑management best practices should I follow?
  type: FAQPage
tags:
- paste values
- Aspose.Cells
- Java Excel automation
- copy options
- paste options
title: كيفية لصق القيم باستخدام خيارات النسخ واللصق في Aspose.Cells
url: /ar/java/cell-operations/aspose-cells-java-copy-paste-options/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية لصق القيم باستخدام خيارات النسخ واللصق في Aspose.Cells

Automating Excel reporting in Java means you can generate, consolidate, and format workbooks without ever opening Excel manually. With **Aspose.Cells** you get full control over formulas, hidden rows, and cell values, so your reports stay accurate and lightweight. In this tutorial you’ll learn how to use **CopyOptions.ReferToDestinationSheet** to keep formulas correct and **PasteOptions** to paste only the visible values you need.

## إجابات سريعة
- **ما الذي يفعله `CopyOptions.ReferToDestinationSheet`؟** يعيد كتابة الصيغ بحيث تشير إلى ورقة الوجهة بعد عملية النسخ.  
- **كيف يمكنني لصق الخلايا المرئية فقط؟** استدعِ `PasteOptions.setOnlyVisibleCells(true)` مع `PasteType.VALUES`.  
- **ما إصدار المكتبة المطلوب؟** Aspose.Cells 25.3 أو أحدث.  
- **هل أحتاج إلى ترخيص للإنتاج؟** نعم – الترخيص الدائم أو المؤقت يزيل حدود التقييم.  
- **هل يمكنني استخدام Maven أو Gradle؟** كلاهما مدعومان؛ راجع مقتطفات الاعتماد أدناه.

## ما هو “أتمتة إعداد تقارير Excel”؟
أتمتة إعداد تقارير Excel تعني إنشاء وتحديث المصنفات برمجيًا، مما يتيح لك إنشاء ودمج وتنسيق التقارير دون النسخ واللصق اليدوي، مما يقلل الأخطاء ويوفر ساعات من العمل المتكرر. هذا النهج مثالي للوظائف الدُفعية المجدولة، ولوحات التحكم المدفوعة بالبيانات، وأنابيب توحيد المالية.

## لماذا نستخدم CopyOptions و PasteOptions للتقارير؟
هاتان الفئتان تسمحان لك بالحفاظ على مراجع الصيغ سليمة أثناء نسخ البيانات **و** استخراج الخلايا المرئية فقط بعد التصفية أو إخفاء الصفوف. باستخدامهما معًا يقلل حجم البيانات المنقولة بنسبة تصل إلى 80 % في سيناريوهات الجداول المصفاة عادةً ويضمن استمرار حساب الصيغ بشكل صحيح في ورقة الوجهة.

## المتطلبات المسبقة
- Java 8 أو أعلى.  
- Maven أو Gradle لإدارة الاعتمادات.  
- Aspose.Cells 25.3+ (ترخيص تجريبي، مؤقت، أو دائم).  

## إعداد Aspose.Cells للـ Java

Add the library to your project with one of the following:

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
- **Free trial** – مجموعة كاملة من الميزات للتقييم.  
- **Temporary license** – يزيل حدود التجربة أثناء الاختبار.  
- **Permanent license** – يوصى به لأعباء العمل الإنتاجية.

تهيئة Aspose.Cells في كود Java الخاص بك:  
```java
import com.aspose.cells.Workbook;

Workbook workbook = new Workbook("path/to/your/excel/file.xlsx");
```

## دليل خطوة بخطوة

### 1. copyOptions مع referToDestinationSheet

#### نظرة عامة
`CopyOptions` هو كائن التكوين في Aspose.Cells الذي يتحكم في كيفية معالجة الصيغ ومراجع الخلايا أثناء عملية النسخ. ضبط `CopyOptions.ReferToDestinationSheet` على `true` يعيد كتابة مراجع الصيغ بحيث تشير إلى الورقة الجديدة بعد عملية النسخ.

#### الخطوة 1: تهيئة المصنف وأوراق العمل  
```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;

String dataDir = "YOUR_DATA_DIRECTORY";
Workbook wb = new Workbook(dataDir + "/book1.xlsx");
Worksheet source = wb.getWorksheets().get(0);
Worksheet destination = wb.getWorksheets().add("DestSheet");
```

#### الخطوة 2: تكوين copyOptions  
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
*لماذا هذا مهم*: الصيغ التي كانت تشير أصلاً إلى `Sheet1` ستشير الآن بشكل صحيح إلى `DestSheet`، مما يحافظ على موثوقية تقاريرك الآلية.

**نصيحة استكشاف الأخطاء**: إذا استمرت الصيغ في الإشارة إلى الورقة القديمة، تأكد من استدعاء `setReferToDestinationSheet(true)` **قبل** النسخ.

### 2. pasteOptions للقيم فقط من الخلايا المرئية

#### نظرة عامة
`PasteOptions` هو كائن الإعدادات في Aspose.Cells الذي يحدد ما يتم لصقه. باستخدام `PasteType.VALUES` مع `onlyVisibleCells=true` يتم نسخ القيم المعروضة فقط، مع تجاهل الصفوف/الأعمدة المخفية والتنسيق.

#### الخطوة 1: تهيئة المصنف وأوراق العمل  
```java
Workbook wb = new Workbook(dataDir + "/book1.xlsx");
Worksheet source = wb.getWorksheets().get(0);
Worksheet destination = wb.getWorksheets().add("DestSheet");
```

#### الخطوة 2: تكوين pasteOptions  
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

**نصيحة استكشاف الأخطاء**: تأكد من أن الصفوف/الأعمدة مخفية فعلاً في Excel قبل النسخ؛ وإلا سيتم تضمينها.

## تطبيقات عملية
1. **Financial consolidation** – دمج الأوراق الشهرية في مصنف رئيسي مع الحفاظ على دقة جميع الصيغ.  
2. **Filtered data export** – استخراج الصفوف المرئية فقط من جدول مفلتر إلى ورقة ملخص.  
3. **Scheduled report generation** – أتمتة إنشاء تقارير Excel الليلية بقيم خلايا دقيقة ومراجع صحيحة.

## اعتبارات الأداء
- **Dispose of workbooks** عندما تنتهي (`wb.dispose();`) لتحرير الموارد الأصلية.  
- **Batch operations** – جمع عدة عمليات نسخ/لصق لتقليل الحمل.  
- **Monitor memory** – قد تتطلب المصنفات الكبيرة زيادة حجم الذاكرة (`-Xmx2g`).  
- Aspose.Cells يدعم **أكثر من 50 تنسيق إدخال وإخراج** ويمكنه معالجة المصنفات التي تحتوي على **ما يصل إلى 2 مليون صف** دون تحميل الملف بالكامل في الذاكرة، مما يوفر أداءً عالي السرعة لأعباء العمل المؤسسية.

## الأسئلة المتكررة

**س: ما هو الغرض من `CopyOptions.ReferToDestinationSheet`؟**  
ج: يعيد كتابة مراجع الصيغ بحيث تشير إلى ورقة الوجهة بعد النسخ، مما يضمن بقاء صيغ التقارير صحيحة.

**س: كيف يمكنني لصق الخلايا المرئية فقط؟**  
ج: اضبط `PasteOptions.setOnlyVisibleCells(true)` واختر `PasteType.VALUES`.

**س: هل يمكنني استخدام Aspose.Cells دون شراء ترخيص؟**  
ج: نعم، يتوفر نسخة تجريبية مجانية أو ترخيص مؤقت للتقييم، لكن الترخيص الدائم مطلوب للإنتاج.

**س: لماذا لا تزال بعض المراجع خاطئة بعد النسخ؟**  
ج: تحقق مرة أخرى من أن `ReferToDestinationSheet` مفعّل **قبل** عملية النسخ وأن صيغ المصدر لا تحتوي على روابط لمصنفات خارجية.

**س: ما هي أفضل ممارسات إدارة الذاكرة التي يجب اتباعها؟**  
ج: قم بتفريغ كائنات `Workbook` عند الانتهاء، عالج الملفات الكبيرة على دفعات، وراقب استهلاك الذاكرة في JVM.

**س: هل يمكن دمج CopyOptions و PasteOptions في عملية واحدة؟**  
ج: نعم، يمكنك ربطهما أولاً بالنسخ باستخدام `CopyOptions` ثم تطبيق `PasteOptions` على النطاق المستهدف.

## الموارد
- **الوثائق**: [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)  
- **التنزيل**: [Aspose.Cells releases for Java](https://releases.aspose.com/cells/java/)  
- **الشراء**: [Buy Aspose.Cells](https://purchase.aspose.com/buy)  
- **الإصدار التجريبي**: [Aspose.Cells free trial](https://releases.aspose.com/cells/java/)  
- **الترخيص المؤقت**: [Apply for a temporary license](https://purchase.aspose.com/temporary-license/)  
- **منتدى الدعم**: [Aspose support](https://forum.aspose.com/c/cells)

---

**آخر تحديث:** 2026-10-28  
**تم الاختبار مع:** Aspose.Cells 25.3 for Java  
**المؤلف:** Aspose

## دروس ذات صلة

- [قراءة ملف Excel Java – التحكم المتقدم في خلايا المصنف باستخدام Aspose.Cells](/cells/java/cell-operations/aspose-cells-java-workbook-cell-manipulation/)
- [إضافة بيانات إلى خلية في Excel باستخدام Aspose.Cells للـ Java](/cells/java/cell-operations/aspose-cells-java-set-active-cell-excel/)
- [تحويل مؤشرات صف وعمود خلية Excel باستخدام Aspose.Cells Java](/cells/java/cell-operations/convert-excel-cell-names-to-indices-aspose-cells-java/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}