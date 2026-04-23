---
category: general
date: 2026-03-01
description: كيفية إنشاء PDF وحفظ المصنف كملف PDF، وتصدير Excel إلى HTML، واستخدام
  وظيفة التوسيع مع Aspose.Cells للغة Java. يتضمن الشرح خطوة بخطوة.
draft: false
keywords:
- how to create pdf
- save workbook as pdf
- export excel to html
- use expand function
language: ar
og_description: كيفية إنشاء ملف PDF من دفتر عمل باستخدام Aspose.Cells للغة Java. تعلم
  كيفية حفظ دفتر العمل كملف PDF، وتصدير Excel إلى HTML، واستخدام دالة EXPAND.
og_title: كيفية إنشاء PDF من دفتر عمل – دليل جافا
tags:
- Aspose.Cells
- Java
- PDF generation
title: كيفية إنشاء ملف PDF من دفتر عمل – دليل جافا الكامل
url: /ar/java/excel-import-export/how-to-create-pdf-from-a-workbook-complete-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية إنشاء PDF من دفتر عمل – دليل Java الكامل

هل تساءلت يومًا **كيف تنشئ PDF** مباشرةً من دفتر عمل Excel دون الحاجة إلى محولات من طرف ثالث؟ أنت لست وحدك. يواجه العديد من المطورين صعوبة عندما يحتاجون إلى تصدير PDF سريع، أو معاينة HTML، أو صيغ مصفوفية متقدمة—كل ذلك في خطوة واحدة.  

في هذا الدرس سنستعرض برنامج Java واحد مستقل يقوم بكل ذلك. سن **نحفظ دفتر العمل كملف PDF**، ونوضح لك كيفية **تصدير Excel إلى HTML** مع الحفاظ على الصفوف المثبتة، ونظهر **استخدام دالة EXPAND** داخل ورقة العمل. في النهاية ستحصل على مشروع قابل للتنفيذ يمكنك إدراجه في أي بناء Maven أو Gradle.

> **نصيحة احترافية:** جميع الشيفرات أدناه تعمل مع Aspose.Cells 23.10 (أو أحدث). إذا كنت تستخدم نسخة أقدم، قد تختلف بعض أسماء الطرق قليلًا.

---

## المتطلبات المسبقة

- **Java 17** (أو أي نسخة LTS) مثبتة ومُعَدَّة.
- مكتبة **Aspose.Cells for Java**. أضف الاعتماد التالي إلى ملف `pom.xml` الخاص بك:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
    <classifier>jdk17</classifier>
</dependency>
```

- بيئة تطوير متكاملة أو محرر نصوص من اختيارك (IntelliJ IDEA، VS Code، Eclipse…).

لا توجد واجهات برمجة تطبيقات خارجية، ولا خدمات ويب—فقط Java صافية وAspose.Cells SDK.

---

## نظرة عامة على الحل

سنقسم التنفيذ إلى **سبع خطوات منطقية**:

1. إنشاء دفتر عمل وعرض دالة **EXPAND**.  
2. تمكين محددات تنوع الخطوط و**حفظ دفتر العمل كملف PDF**.  
3. تصدير نفس دفتر العمل إلى HTML مع الحفاظ على الصفوف المثبتة.  
4. استخدام Smart Marker مع معامل `IF` لإدخال نص شرطي.  
5. تطبيق Smart Marker بنمط رئيس‑تفصيل للبيانات الهرمية.  
6. تحميل ملف Markdown يحتوي على صور مشفّرة بـ Base‑64.  
7. ضبط خيارات GridJs للمحاذاة والحدود، ثم إدراج البيانات.

كل خطوة مُغلفة في طريقة خاصة بها للحفاظ على نظافة طريقة `main` ولتوضيح **لماذا** نفعل ما نفعل، وليس فقط **ماذا** نكتب.

---

## الخطوة 1 – إنشاء دفتر عمل واستخدام دالة EXPAND

دالة **EXPAND** هي صيغة مصفوفة ديناميكية جديدة تم تقديمها في Office 365. تسمح لك بتوسيع نطاق إلى مساحة أكبر دون الحاجة إلى نسخ الخلايا يدويًا.

```java
import com.aspose.cells.*;

public class WorkbookDemo {

    private static void createWorkbookWithExpand() throws Exception {
        // Initialize a new workbook and grab the first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.getWorksheets().get(0);

        // A1 uses EXPAND to turn a 1×3 array into a 5×2 block
        sheet.getCells().get("A1").setFormula("=EXPAND({1,2,3}, 5, 2)");

        // B1 demonstrates a classic trigonometric function (cotangent)
        sheet.getCells().get("B1").setFormula("=COT(PI()/4)");

        // Force calculation so we can read the results immediately
        workbook.calculateFormula();

        // Print the top‑left value to the console – should be 1
        System.out.println("A1 value after EXPAND: " + sheet.getCells().get("A1").getStringValue());
    }
```

**لماذا هذا مهم:**  
- `EXPAND` يضيف فراغات تلقائيًا إلى النتيجة، وهو مثالي عندما تقوم لاحقًا **بحفظ دفتر العمل كملف PDF**—سيظهر الـ PDF جدولًا نظيفًا ومستطيلًا.  
- استدعاء `calculateFormula()` يضمن تشغيل محرك الصيغ قبل أي تصدير.

---

## الخطوة 2 – تمكين محددات تنوع الخطوط و**حفظ دفتر العمل كملف PDF**

إذا كنت بحاجة إلى دعم طباعة متقدمة (مثل الإيموجي أو محددات تنوع CJK)، يجب تفعيل هذه الميزة **قبل** الحفظ.

```java
    private static void saveAsPdf(Workbook workbook) throws Exception {
        // Enable support for variation selectors (useful for emojis, etc.)
        WorkbookSettings settings = workbook.getSettings();
        settings.setEnableFontVariationSelectors(true);

        // Define the output path – adjust to your environment
        String pdfPath = "output/vsPdf.pdf";

        // Save the workbook as a PDF file
        workbook.save(pdfPath, SaveFormat.PDF);
        System.out.println("PDF saved to: " + pdfPath);
    }
```

**نقطة رئيسية:** تم الإجابة على السؤال الأساسي **how to create pdf** هنا—عن طريق استدعاء `workbook.save(..., SaveFormat.PDF)` بعد ضبط الإعدادات.

---

## الخطوة 3 – **تصدير Excel إلى HTML** مع الحفاظ على الصفوف المثبتة

غالبًا ما يطلب أصحاب المصلحة معاينة سريعة على الويب. يمكن لـ Aspose.Cells تصدير إلى HTML، ومع `setPreserveFrozenRows(true)` نحافظ على تجربة التمرير نفسها كما في Excel.

```java
    private static void exportToHtml(Workbook workbook) throws Exception {
        HtmlSaveOptions htmlOptions = new HtmlSaveOptions();
        htmlOptions.setPreserveFrozenRows(true); // keep frozen panes

        String htmlPath = "output/frozenRows.html";
        workbook.save(htmlPath, htmlOptions);
        System.out.println("HTML exported to: " + htmlPath);
    }
```

**لماذا يهمك:** الصفوف المثبتة تُعد ميزة تحسين تجربة الاستخدام؛ بدونها تختفي صفوف العنوان عندما يقوم المستخدمون بالتمرير إلى أسفل الصفحة.

---

## الخطوة 4 – Smart Marker مع معامل IF

تتيح لك Smart Markers دمج البيانات في قالب دون كتابة حلقات. يضيف معامل `if` منطقًا شرطيًا مباشرة داخل العلامة.

```java
    private static void applyConditionalSmartMarker() throws Exception {
        String template = "${if(@IsVIP, 'VIP Customer', 'Regular Customer')}: ${CustomerName}";
        Map<String, Object> data = new HashMap<>();
        data.put("IsVIP", true);
        data.put("CustomerName", "Acme Corp");

        // Create a fresh workbook to host the result
        Workbook markerWorkbook = new Workbook();
        SmartMarkerProcessor processor = new SmartMarkerProcessor(markerWorkbook);
        processor.apply(template, data);

        // Save to see the result
        markerWorkbook.save("output/conditionalMarker.pdf", SaveFormat.PDF);
    }
```

ستظهر النتيجة في ملف PDF كـ **“VIP Customer: Acme Corp”** لأن `IsVIP` يساوي `true`. إذا غيرت العلامة إلى `false` ستحصل على **“Regular Customer: Acme Corp”**—دون الحاجة إلى أي شفرة إضافية.

---

## الخطوة 5 – Smart Marker بنمط رئيس‑تفصيل باستخدام نطاق هرمي

عندما تكون لديك بيانات أب‑ابن (مثل الطلبات وبنودها)، يوفر لك الـ master‑detail marker عناء إدراج الصفوف يدويًا.

```java
    private static void applyMasterDetailSmartMarker() throws Exception {
        // Simulated hierarchical data
        Map<String, Object> hierarchicalData = new HashMap<>();
        List<Map<String, Object>> orders = new ArrayList<>();

        Map<String, Object> order1 = new HashMap<>();
        order1.put("OrderID", 1001);
        order1.put("Date", "2024‑12‑01");
        List<Map<String, Object>> details1 = new ArrayList<>();
        details1.add(Map.of("Product", "Widget A", "Qty", 5));
        details1.add(Map.of("Product", "Widget B", "Qty", 2));
        order1.put("Detail", details1);
        orders.add(order1);

        hierarchicalData.put("Orders", orders);

        String masterDetailTemplate =
                "${Orders.Master:OrderID,Date}\n" +
                "${Orders.Detail:Product,Qty}";

        Workbook mdWorkbook = new Workbook();
        SmartMarkerProcessor mdProcessor = new SmartMarkerProcessor(mdWorkbook);
        mdProcessor.apply(masterDetailTemplate, hierarchicalData);

        mdWorkbook.save("output/masterDetail.pdf", SaveFormat.PDF);
    }
```

**ما ستحصل عليه:** يقوم المحرك بتوسيع الصفوف الرئيسية لكل طلب ويضع تلقائيًا الصفوف التفصيلية تحته—مثالي للفواتير أو تقارير المشتريات.

---

## الخطوة 6 – تحميل مستند Markdown مع صور Base‑64 مدمجة

إذا كانت بيانات المصدر لديك في صيغة Markdown (شائعة في خطوط توثيق المستندات)، يمكن لـ Aspose.Cells تحويلها مباشرة إلى دفتر عمل.

```java
    private static void loadMarkdownWithBase64() throws Exception {
        MarkdownLoadOptions mdOptions = new MarkdownLoadOptions();
        mdOptions.setEnableBase64Images(true); // decode inline images

        // Assume doc.md lives in the project root
        Workbook mdWorkbook = new Workbook("input/doc.md", mdOptions);
        mdWorkbook.save("output/markdownExport.pdf", SaveFormat.PDF);
        System.out.println("Markdown loaded and saved as PDF.");
    }
```

**ملاحظة حالة حافة:** إذا كان سلسلة Base‑64 غير صالحة، سيتخطى Aspose الصورة لكنه سيستمر في معالجة باقي المستند—دون حدوث تعطل.

---

## الخطوة 7 – ضبط خيارات GridJs وإدراج البيانات

GridJs هو شبكة JavaScript خفيفة يمكن لـ Aspose.renderها إلى HTML. تحسين محاذاة الأرقام وتطبيق الحدود يعزز من قابلية القراءة.

```java
    private static void configureGridJs() throws Exception {
        GridJsOptions gridOptions = new GridJsOptions();
        gridOptions.setNumberFormatAlignment(Alignment.Center); // center numbers
        gridOptions.setNumberFormatBorder(BorderLineStyle.Thin); // thin border

        GridJsEngine gridEngine = new GridJsEngine(gridOptions);
        gridEngine.insertRows(0, 10); // create 10 empty rows
        gridEngine.setCellValue(0, 0, "123"); // first cell gets a value

        // Export the GridJs view to HTML for quick inspection
        String htmlPath = "output/gridJs.html";
        gridEngine.save(htmlPath);
        System.out.println("GridJs HTML saved to: " + htmlPath);
    }
```

**لماذا نهتم:** المحاذاة الصحيحة والحدود تجعل الـ HTML الناتج يبدو كجدول بيانات مصقول—مفيد للوحة التحكم.

---

## تجميع كل شيء معًا – طريقة `main`

```java
    public static void main(String[] args) {
        try {
            // Step 1 – create workbook with EXPAND
            Workbook workbook = new Workbook();
            Worksheet sheet = workbook.getWorksheets().get(0);
            sheet.getCells().get("A1").setFormula("=EXPAND({1,2,3}, 5, 2)");
            sheet.getCells().get("B1").setFormula("=COT(PI()/4)");
            workbook.calculateFormula();
            System.out.println("A1 after EXPAND: " + sheet.getCells().get("A1").getStringValue());

            // Step 2 – save as PDF
            saveAsPdf(workbook);

            // Step 3 – export to HTML
            exportToHtml(workbook);

            // Step 4 – conditional Smart Marker
            applyConditionalSmartMarker();

            // Step 5 – master‑detail Smart Marker
            applyMasterDetailSmartMarker();

            // Step 6 – load Markdown with Base‑64 images
            loadMarkdownWithBase64();

            // Step 7 – GridJs configuration
            configureGridJs();

            System.out.println("All tasks completed successfully.");
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}