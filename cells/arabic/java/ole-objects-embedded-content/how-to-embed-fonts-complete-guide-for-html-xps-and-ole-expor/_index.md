---
category: general
date: 2026-03-01
description: تعلم كيفية تضمين الخطوط في HTML وغيرها من الصيغ. دليل خطوة بخطوة يغطي
  تضمين الخطوط في HTML، تحويل Excel إلى HTML، كيفية تصدير OLE، وتحويل Excel إلى XPS.
draft: false
keywords:
- how to embed fonts
- embed fonts in html
- convert excel to html
- how to export ole
- convert excel to xps
language: ar
og_description: كيفية تضمين الخطوط في تصديرات HTML و XPS و OLE. تعلّم سير العمل الكامل،
  شاهد كود Java القابل للتنفيذ، وتقن تضمين الخطوط في HTML لتحويلات Excel.
og_title: كيفية تضمين الخطوط – دليل جافا الكامل
tags:
- Aspose.Cells
- Java
- Document Export
title: كيفية تضمين الخطوط – دليل شامل لتصدير HTML و XPS و OLE
url: /ar/java/ole-objects-embedded-content/how-to-embed-fonts-complete-guide-for-html-xps-and-ole-expor/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تضمين الخطوط – دليل كامل لتصدير HTML و XPS و OLE

هل تساءلت يومًا **how to embed fonts** عندما تحول مصنف Excel إلى صفحة ويب أو مستند قابل للطباعة؟ لست وحدك. يواجه العديد من المطورين مشكلة عندما يبدو الناتج جيدًا على جهازهم ولكنه يتعطل على جهاز آخر بسبب عدم وجود الخطوط المطلوبة.  

في هذا الدرس سنستعرض سيناريو واقعي باستخدام Aspose.Cells for Java: سنضمّن الخطوط في HTML، نحافظ على محددات تنوع الرموز التعبيرية أثناء التحويل إلى XPS، وحتى نجعل كائن OLE قابلاً للتحرير عند التصدير إلى PPTX. في النهاية ستحصل على حل جاهز للنسخ واللصق يجيب على سؤال “how to embed fonts” ويتطرق أيضًا إلى **embed fonts in html**, **convert excel to html**, **how to export ole**, و **convert excel to xps**.

## المتطلبات المسبقة

- Java 17 (أو أي JDK حديث)  
- Aspose.Cells for Java 25.x أو أحدث  
- بيئة تطوير متكاملة (IDE) (IntelliJ IDEA، Eclipse، أو VS Code)  
- إلمام أساسي بهياكل بيانات Excel  

لا توجد خدمات خارجية مطلوبة—كل شيء يعمل محليًا.

## نظرة عامة على الحل

1. **Create a workbook** واستخدام دالة `WRAPCOLS` لتحويل نطاق عمودي إلى تخطيط من ثلاثة أعمدة.  
2. **Save the workbook as XPS** مع تفعيل محددات تنوع الخطوط بحيث تبقى الرموز التعبيرية سليمة.  
3. **Export to HTML** مع خطوط مضمّنة، لضمان أن تظهر الصفحة بنفس الشكل في كل مكان.  
4. **Export a workbook containing an OLE object to PPTX** مع الحفاظ على إمكانية التحرير.  
5. **Apply a Smart Marker template** الذي يوضح ربط البيانات master‑detail.  

كل خطوة معزولة في قسم H2 خاص بها، مما يجعل الدليل سهل التصفح لكل من محركات البحث ومساعدي الذكاء الاصطناعي.

![رسم توضيحي لكيفية تضمين الخطوط](image.png "كيفية تضمين الخطوط")

*نص بديل للصورة: مخطط يوضح سير العمل من Excel إلى HTML و XPS و PPTX.*

---

## الخطوة 1 – إنشاء مصنف واستخدام WRAPCOLS (لماذا هذا مهم لـ embed fonts in html)

قبل أن نتحدث عن تضمين الخطوط، نحتاج إلى مصنف يحتوي فعليًا على بيانات. دالة `WRAPCOLS` طريقة مفيدة لتقسيم عمود واحد إلى عدة أعمدة، مما يجعل HTML النهائي أكثر قابلية للقراءة غالبًا.

```java
import com.aspose.cells.*;

public class EmbedFontsDemo {
    public static void main(String[] args) throws Exception {
        // Initialize a new workbook
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.getWorksheets().get(0);

        // Populate A2:A10 with sample data
        for (int i = 2; i <= 10; i++) {
            sheet.getCells().get("A" + i).putValue("Item " + (i - 1));
        }

        // Use WRAPCOLS to create a 3‑column block starting at A1
        Cell resultCell = sheet.getCells().get("A1");
        resultCell.setFormula("=WRAPCOLS(A2:A10,3)");
        workbook.calculateFormula();

        System.out.println("WRAPCOLS result: " + resultCell.getStringValue());
        // -----------------------------------------------------------------
        // The rest of the steps are demonstrated after this point.
        // -----------------------------------------------------------------
```

**لماذا هذه الخطوة؟**  
استدعاء `WRAPCOLS` يولد نطاقًا متعدد الأعمدة يظهر لاحقًا في HTML كجدول. عندما نقوم لاحقًا **embed fonts in html**، سيعتمد تنسيق الجدول على الخطوط التي نضمّنها، مما يضمن عرضًا متسقًا عبر المتصفحات.

---

## الخطوة 2 – حفظ المصنف كـ XPS مع الحفاظ على الرموز التعبيرية (convert excel to xps)

إذا كنت بحاجة إلى تنسيق جاهز للطباعة، فإن XPS خيار قوي. ومع ذلك، غالبًا ما تحتوي المستندات الحديثة على رموز تعبيرية أو رموز تستخدم محددات التنوع. تفعيل `EnableFontVariationSelectors` يضمن بقاء هذه الأحرف بعد التحويل.

```java
        // --------------------------------------------------------------
        // Step 2: Save as XPS with font variation selectors enabled
        // --------------------------------------------------------------
        WorkbookSettings settings = workbook.getSettings();
        settings.setEnableFontVariationSelectors(true); // crucial for emoji

        String xpsPath = "output/withVariations.xps";
        workbook.save(xpsPath, SaveFormat.XPS);
        System.out.println("Workbook saved as XPS at: " + xpsPath);
```

**ما ستحصل عليه:**  
ملف XPS يعرض أي رمز تعبيري مضمّن تمامًا كما هو في المصنف الأصلي. هذا يلبي متطلب **convert excel to xps** ويظهر أن معالجة الخطوط لا تقتصر على HTML.

---

## الخطوة 3 – تصدير إلى HTML مع خطوط مضمّنة (how to embed fonts & embed fonts in html)

الآن نصل إلى جوهر الدرس: **how to embed fonts** عند تحويل Excel إلى HTML. يتيح Aspose.Cells تضمين الخطوط مباشرةً داخل ملف HTML المُولد، مما يلغي الحاجة إلى ملفات خطوط خارجية.

```java
        // --------------------------------------------------------------
        // Step 3: Export to HTML with embedded fonts
        // --------------------------------------------------------------
        HtmlSaveOptions htmlOptions = new HtmlSaveOptions();
        htmlOptions.setEmbedFonts(true); // this is the key line for embed fonts in html
        htmlOptions.setExportImagesAsBase64(true); // optional, keeps all assets in one file

        String htmlPath = "output/embeddedFonts.html";
        workbook.save(htmlPath, htmlOptions);
        System.out.println("HTML with embedded fonts saved at: " + htmlPath);
```

**كيف يعمل:**  
`setEmbedFonts(true)` يخبر المُعالج بقراءة ملفات الخطوط المستخدمة في المصنف وتضمينها كقواعد `@font-face` مُشفّرة بـ Base64 داخل وسم `<style>`. يصبح HTML الناتج مستقلًا، بحيث يمكنك وضعه على أي خادم وستظهر الخطوط بشكل صحيح—وهو بالضبط ما يبحث عنه المطورون عندما يكتبون **how to embed fonts**.

**مقتطف الإخراج المتوقع (داخل `embeddedFonts.html`):**

```html
<style>
@font-face{font-family:"Arial";src:url(data:font/ttf;base64,AAEAAA... ) format('truetype');}
</style>
<table>
  <tr><td>Item 1</td><td>Item 4</td><td>Item 7</td></tr>
  <tr><td>Item 2</td><td>Item 5</td><td>Item 8</td></tr>
  <tr><td>Item 3</td><td>Item 6</td><td>Item 9</td></tr>
</table>
```

لاحظ قاعدة `@font-face`—هذه هي الإجابة الملموسة على **embed fonts in html**.

---

## الخطوة 4 – تصدير مصنف يحتوي على كائن OLE إلى PPTX (how to export ole)

العديد من التقارير التجارية تضم مستندات Word أو PDFs أو أوراق Excel أخرى ككائنات OLE. عند تصدير مثل هذا المصنف إلى PowerPoint، غالبًا ما تفقد القدرة على تحرير ذلك الكائن. يحافظ Aspose.Cells على إمكانية التحرير مباشرةً.

```java
        // --------------------------------------------------------------
        // Step 4: Export a workbook with an OLE object to PPTX
        // --------------------------------------------------------------
        // Load a workbook that already contains an OLE object.
        Workbook oleWorkbook = new Workbook("input/oleObject.xlsx");

        String pptxPath = "output/oleEditable.pptx";
        oleWorkbook.save(pptxPath, SaveFormat.PPTX);
        System.out.println("PPTX with editable OLE object saved at: " + pptxPath);
```

**لماذا هذا مهم:**  
إذا كنت تبحث عن **how to export ole**, يوضح هذا المقتطف استدعاء API الدقيق. الشريحة الناتجة في PowerPoint تحتوي على كائن OLE كعنصر حي يمكن النقر المزدوج لتعديله—دون الحاجة إلى معالجة لاحقة.

---

## الخطوة 5 – تطبيق قالب Smart Marker (master‑detail) وإنهاء العرض التجريبي

تتيح Smart Markers ربط مصدر بيانات (Map، JSON، DataTable) مباشرةً بقالب Excel. إليك مثالًا بسيطًا يطبع صفوف master‑detail.

```java
        // --------------------------------------------------------------
        // Step 5: Apply Smart Marker template (master‑detail)
        // --------------------------------------------------------------
        String smartMarkerTemplate = "${Orders.Master:OrderID,Customer}\n${Orders.Detail:Product,Qty,Price}";
        // Simulated data source
        java.util.Map<String, Object> dataSource = new java.util.HashMap<>();
        java.util.List<java.util.Map<String, Object>> master = new java.util.ArrayList<>();
        java.util.Map<String, Object> masterRow = new java.util.HashMap<>();
        masterRow.put("OrderID", 1001);
        masterRow.put("Customer", "Acme Corp");
        master.add(masterRow);
        dataSource.put("Orders.Master", master);

        java.util.List<java.util.Map<String, Object>> detail = new java.util.ArrayList<>();
        java.util.Map<String, Object> detailRow = new java.util.HashMap<>();
        detailRow.put("Product", "Widget");
        detailRow.put("Qty", 5);
        detailRow.put("Price", 9.99);
        detail.add(detailRow);
        dataSource.put("Orders.Detail", detail);

        SmartMarkerProcessor processor = new SmartMarkerProcessor(new Workbook());
        processor.apply(smartMarkerTemplate, dataSource);
        processor.getWorkbook().save("output/smartMarkerResult.xlsx");
        System.out.println("Smart Marker workbook saved.");
    }
}
```

**ما تراه:**  
مصنف جديد (`smartMarkerResult.xlsx`) حيث تم استبدال عناصر النماذج بالبيانات. هذه الخطوة ليست متعلقة مباشرةً بالخطوط، لكنها تكمل الدرس بإظهار سير عمل تقارير شائع غالبًا ما يسبق تصدير **embed fonts in html**.

---

## المشكلات الشائعة & نصائح احترافية (ضمان نجاح تضمين الخطوط)

| المشكلة | لماذا يحدث | الحل |
|---------|------------|------|
| الخطوط مفقودة في ملف HTML | المصنف يستخدم خط نظام غير مثبت على الخادم. | استخدم `Workbook.getSettings().setDefaultFont("Arial")` قبل تحميل البيانات، أو قم بتضمين ملفات الخط المطلوبة يدويًا. |
| ملف HTML الناتج كبير | تضمين العديد من الخطوط الكبيرة يزيد من حجم الملف. | قصر التضمين على الخطوط التي تستخدمها فعليًا: `htmlOptions.setFontEmbeddingMode(HtmlFontEmbeddingMode.EmbedSubset)`. |
| الرموز التعبيرية تختفي بعد تحويل XPS | محددات التنوع تُحذف افتراضيًا. | فعّل `settings.setEnableFontVariationSelectors(true)` كما هو موضح في الخطوة 2. |
| كائن OLE يتحول إلى صورة ثابتة في PPTX | تم حفظ المصنف المصدر باستخدام `setSuppressOLEObjects(true)`. | تأكد من **عدم** قمع كائنات OLE عند الحفظ إلى PPTX. |

---

## التحقق من النتائج

1. افتح `embeddedFonts.html` في Chrome/Firefox. يجب أن يعرض الجدول الخط المضمّن (مثل Arial) حتى وإن لم يكن هذا الخط مثبتًا على الجهاز.  
2. افتح `withVariations.xps` في عارض Windows XPS. يجب أن تُظهر الرموز التعبيرية مثل 👍 بشكل صحيح.  
3. افتح `oleEditable.pptx` في PowerPoint. انقر مزدوجًا على شكل OLE؛  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}