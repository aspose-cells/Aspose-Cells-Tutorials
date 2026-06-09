---
category: general
date: 2026-06-08
description: إنشاء دفتر عمل رئيسي وتفصيلي في Java باستخدام Aspose.Cells Smart Marker.
  تعلم خطوة بخطوة كيفية ربط البيانات الرئيسية بورقة تفصيلية وتصدير Excel.
draft: false
keywords:
- create master detail workbook
- Aspose.Cells Smart Marker
- Java Excel export
- master‑detail relationship
- Smart Marker data source
language: ar
og_description: إنشاء دفتر عمل رئيسي وتفصيلي في Java باستخدام Aspose.Cells Smart Marker.
  اتبع هذا الدليل الكامل لربط البيانات الرئيسية بورقة تفصيلية وإنشاء ملفات Excel.
og_title: إنشاء دفتر عمل رئيسي وتفصيلي باستخدام Aspose.Cells (Java)
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Create master detail workbook in Java using Aspose.Cells Smart Marker.
    Learn step‑by‑step how to bind master data to a detail sheet and export Excel.
  headline: Create master detail workbook with Aspose.Cells (Java)
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel
title: إنشاء دفتر عمل رئيسي وتفصيلي باستخدام Aspose.Cells (Java)
url: /ar/java/templates-reporting/create-master-detail-workbook-with-aspose-cells-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء دفتر عمل رئيس‑تفصيل باستخدام Aspose.Cells (Java)

إذا كنت بحاجة إلى **إنشاء دفتر عمل رئيس‑تفصيل** في Java، فقد وجدت المكان المناسب. سواء كنت تبني لوحة تحكم مبيعات، مولد فواتير، أو أي أداة تقارير تتطلب عرض رئيس‑تفصيل، سيوضح لك هذا الدليل العملية بالكامل—بدون حشو، فقط كود صلب وقابل للتنفيذ.

في هذا الشرح سنستخدم **Aspose.Cells Smart Marker**، وهي ميزة قوية تتيح لك إدراج نواقل بيانات مباشرة في قالب Excel. بحلول النهاية، ستفهم كيفية إعداد علاقة الرئيس‑التفصيل، ربط قائمة POJO كمصدر للبيانات، وتصدير ملف .xlsx نظيف جاهز للاستخدام اللاحق.

## ما ستتعلمه

- كيفية تهيئة دفتر عمل وإضافة ورقة عمل تفصيلية.  
- كيفية إدراج Smart Marker يربط صفوف الرئيس بورقة التفصيل.  
- كيفية توفير قائمة من كائنات `Order` كمصدر بيانات للـ Smart Marker.  
- كيفية إعادة حساب الصيغ التي تعتمد على البيانات المدخلة.  
- كيفية حفظ الملف النهائي مع الحفاظ على علاقة الرئيس‑التفصيل.  

**المتطلبات المسبقة:** Java 17 (أو أحدث)، Maven أو Gradle، ورخصة صالحة لـ Aspose.Cells for Java (الإصدار التجريبي المجاني يكفي للاختبار). إذا لم تتعامل مع Aspose.Cells من قبل، لا تقلق—هذا الدليل يفترض فقط معرفة أساسية بـ Java.

---

![إنشاء مخطط دفتر عمل رئيس‑تفصيل](create_master_detail_workbook.png "مخطط يوضح تدفق دفتر عمل رئيس‑تفصيل")

## إنشاء دفتر عمل رئيس‑تفصيل – الخطوة 1: تهيئة دفتر العمل

أول شيء نحتاجه هو نسخة جديدة من `Workbook`. فكر في دفتر العمل كقماش ستعيش عليه كل من ورقتي الرئيس والتفصيل.

```java
import com.aspose.cells.*;

public class MasterDetailExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook and add the master and detail worksheets
        Workbook workbook = new Workbook();                 // empty workbook with a default sheet
        Worksheet masterSheet = workbook.getWorksheets().get(0); // the first sheet becomes the master
        Worksheet detailSheet = workbook.getWorksheets().add("Details"); // add a detail sheet
```

*لماذا هذا مهم:* Aspose.Cells دائمًا ينشئ ورقة افتراضية، لذا نعيد استخدامها كالرئيس. إضافة ورقة تفصيل مسماة (`"Details"`) تجعل إشارة الـ Smart Marker اللاحقة أوضح وتحافظ على تنظيم الملف.

> **نصيحة احترافية:** إذا كان لديك ملف قالب بالفعل، استبدل `new Workbook()` بـ `new Workbook("template.xlsx")`. بقية الخطوات تبقى كما هي.

## إدراج Smart Marker – الخطوة 2: ربط صفوف الرئيس بورقة التفصيل

Smart Markers هي نواقل مكانية تقوم Aspose.Cells باستبدالها بالبيانات أثناء التشغيل. الصيغة `${DataSource,DetailSheet=SheetName}` تخبر المحرك أي بيانات سحب وأين وضع صفوف التفصيل.

```java
        // Step 2: Insert the Smart Marker that links the master data to the detail sheet
        masterSheet.getCells().get("A2").putValue("${Orders,DetailSheet=Details}");
```

*لماذا هذا مهم:* وضع العلامة في `A2` يعني أن صف الرئيس سيبدأ مباشرةً أسفل صف العنوان (عادةً `A1`). الجزء `DetailSheet=Details` ينشئ **علاقة رئيس‑تفصيل** تلقائيًا—كل صف رئيس يولد كتلة من الصفوف في ورقة `Details`.

> **سؤال شائع:** *هل يمكنني وضع العلامة في عمود مختلف؟* بالتأكيد. فقط عدل إشارة الخلية (`B2`, `C2`, إلخ) وتأكد من أن تخطيط القالب يتطابق.

## توفير مصدر البيانات – الخطوة 3: ربط POJOs بالـ Smart Marker

الآن نزود الـ Smart Marker ببيانات حقيقية. في هذا المثال نستخدم قائمة من كائنات `Order` POJO التي تُرجعها فئة مساعدة `DataFactory`.

```java
        // Step 3: Provide the data source for the Smart Marker (a list of Order objects)
        List<Order> orders = DataFactory.getOrders();   // your POJO list
        workbook.getSmartMarkers().setDataSource("Orders", orders);
```

*لماذا هذا مهم:* المفتاح `"Orders"` يجب أن يتطابق مع الاسم المستخدم داخل النواقل `${...}`. Aspose.Cells سي iterates عبر القائمة، مُنشئًا صف رئيس لكل `Order` ومُستخرجًا البيانات الفرعية المرتبطة (إن وجدت) إلى ورقة التفصيل.

> **حالة حافة:** إذا كانت القائمة فارغة، سيترك الـ Smart Marker منطقة الرئيس فارغة—لن يُرمى استثناء. ومع ذلك، قد ترغب في فحص `orders.isEmpty()` مسبقًا لتقرر ما إذا كنت ستولد ملفًا أم لا.

## إعادة حساب الصيغ – الخطوة 4: الحفاظ على تحديث الحسابات

غالبًا ما تحتوي أوراق الرئيس‑تفصيل على صيغ تجمع الكميات، تحسب الإجماليات، أو تطبق الضرائب. بعد أن يحقن الـ Smart Marker البيانات، نحتاج إلى إعادة حساب تلك الصيغ.

```java
        // Step 4: Recalculate any formulas that may depend on the inserted data
        workbook.calculateFormula();
```

*لماذا هذا مهم:* بدون هذا الاستدعاء الخلايا التي تشير إلى الصفوف المُدخلة حديثًا ستظل تُظهر القيم القديمة (أو #DIV/0!). `calculateFormula()` يمر عبر كامل دفتر العمل، مُضمنًا أن كل خلية معتمدة تعكس البيانات الجديدة.

> **ملاحظة أداء:** بالنسبة لدفاتر العمل الضخمة يمكنك تحديد إعادة الحساب إلى ورقة معينة باستخدام `worksheet.calculateFormula()`. في معظم سيناريوهات الرئيس‑تفصيل استدعاء كامل دفتر العمل يكون كافيًا.

## حفظ الملف – الخطوة 5: تصدير دفتر عمل الرئيس‑تفصيل

أخيرًا، اكتب دفتر العمل إلى القرص. يمكنك اختيار أي تنسيق مدعوم (`.xlsx`, `.xls`, `.csv`, إلخ)—هنا نستخدم `.xlsx` الحديث.

```java
        // Step 5: Save the workbook with the master‑detail relationship applied
        workbook.save("output/master-detail.xlsx"); // adjust path as needed
    }
}
```

*لماذا هذا مهم:* الملف المحفوظ الآن يحتوي على ورقتين: **Sheet1** (الرئيس) و **Details** (التفصيل). فتحه في Excel سيظهر عرض رئيس‑تفصيل منسق بشكل جميل، مع جميع الصيغ التي أعدت حسابها.

> **ملاحظة:** إذا نسيت استدعاء `calculateFormula()` قبل الحفظ، سيعيد Excel الحساب عند الفتح، مما قد يكون أبطأ وقد ينتج نتائج مختلفة إذا كان دفتر العمل يحتوي على دوال متقلبة.

---

## الكود الكامل (قابل للتنفيذ)

بجمع جميع الأجزاء معًا، إليك البرنامج الكامل الذي يمكنك نسخه‑ولصقه في بيئة التطوير المتكاملة الخاصة بك:

```java
import com.aspose.cells.*;
import java.util.List;

public class MasterDetailExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Initialize workbook and worksheets
        Workbook workbook = new Workbook();
        Worksheet masterSheet = workbook.getWorksheets().get(0);
        Worksheet detailSheet = workbook.getWorksheets().add("Details");

        // Optional: Add headers to master sheet
        masterSheet.getCells().get("A1").putValue("Order ID");
        masterSheet.getCells().get("B1").putValue("Customer");
        masterSheet.getCells().get("C1").putValue("Total");

        // Step 2: Insert Smart Marker linking to detail sheet
        masterSheet.getCells().get("A2").putValue("${Orders,DetailSheet=Details}");

        // Step 3: Supply data source (list of Order POJOs)
        List<Order> orders = DataFactory.getOrders(); // assume this returns a populated list
        workbook.getSmartMarkers().setDataSource("Orders", orders);

        // Step 4: Recalculate formulas (if any)
        workbook.calculateFormula();

        // Step 5: Save the resulting workbook
        workbook.save("output/master-detail.xlsx");
    }
}
```

**الناتج المتوقع:** افتح `master-detail.xlsx` وسترى:

- **Sheet1** (الرئيس) تُظهر كل معرف طلب، اسم العميل، والإجمالي.  
- ورقة **Details** تحتوي على الصفوف التي تنتمي إلى كل طلب (مثلاً بنود الفاتورة).  
- أي صيغ إجمالي أو ضريبة مُعبأة بشكل صحيح.

---

## الأسئلة المتكررة والاختلافات

| السؤال | الجواب |
|----------|--------|
| *هل يمكنني استخدام قالب بدلاً من دفتر عمل فارغ؟* | نعم. حمّله باستخدام `new Workbook("template.xlsx")` وضع الـ Smart Marker في الخلية المناسبة. |
| *ماذا لو كانت بيانات التفصيل في قائمة منفصلة؟* | يمكنك تعشيق Smart Markers: `${Orders.Details,DetailSheet=Details}` حيث `Details` هي خاصية لكل `Order` تُعيد قائمة من بنود السطر. |
| *كيف يمكنني تنسيق صفوف التفصيل؟* | طبق نمطًا على أول صف تفصيل في القالب؛ ستقوم Aspose.Cells بنسخ هذا النمط لكل صف يتم إنشاؤه. |
| *هل هناك طريقة لإخفاء ورقة التفصيل حتى يتم توسيع صف الرئيس؟* | ليس مباشرة عبر Smart Markers، لكن يمكنك ضبط خاصية `Visible` للورقة إلى `false` وتبديلها باستخدام VBA بعد الفتح. |

## الخلاصة

الآن تعرف **كيفية إنشاء دفتر عمل رئيس‑تفصيل** في Java باستخدام Aspose.Cells Smart Marker. من تهيئة دفتر العمل، إدراج الـ Smart Marker، ربط قائمة POJO، إعادة حساب الصيغ، وحتى حفظ الملف—تم شرح كل خطوة مع *سببها*، لتتمكن من تعديل النمط وفقًا لمشاريعك الخاصة.

Next, try extending this example:

- أضف تنسيقًا شرطيًا لتسليط الضوء على الطلبات ذات القيمة العالية.  
- صدّر دفتر العمل كملف PDF باستخدام `workbook.save("report.pdf", SaveFormat.PDF)`.  
- دمج أقسام رئيس‑تفصيل متعددة في ملف واحد باستخدام أسماء Smart Marker مختلفة.

The concepts of **master‑

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مصدر يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك الخاصة.

- [إنشاء دفتر عمل Excel باستخدام Aspose.Cells في Java: دليل خطوة بخطوة](/cells/english/java/getting-started/create-excel-workbook-aspose-cells-java/)
- [معالجة ملفات Excel المتقدمة باستخدام Aspose.Cells for Java \| دليل عمليات دفتر العمل](/cells/english/java/workbook-operations/master-excel-manipulation-aspose-cells-java/)
- [كيفية إنشاء وتصدير Excel إلى HTML باستخدام Aspose.Cells Java \| دليل عمليات دفتر العمل](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}