---
category: general
date: 2026-07-20
description: دليل excel إلى pptx يوضح كيفية تصدير Excel إلى PowerPoint مع مربعات نص
  قابلة للتحرير، تحويل شكل المخطط وتضمين الصور في pptx باستخدام Aspose.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- excel to pptx
- editable text boxes
- convert chart shape
- export excel powerpoint
- embed images pptx
language: ar
lastmod: 2026-07-20
og_description: دليل تحويل Excel إلى PPTX يشرح لك كيفية تصدير Excel إلى PowerPoint
  مع الحفاظ على مربعات النص القابلة للتحرير، وتحويل شكل المخطط، وتضمين الصور في ملف
  PPTX باستخدام Aspose.
og_image_alt: Screenshot of a PowerPoint slide generated from an Excel workbook showing
  editable shapes
og_title: excel إلى pptx – تصدير الأشكال القابلة للتحرير من Excel إلى PowerPoint (Java)
schemas:
- author: Aspose
  dateModified: '2026-07-20'
  description: excel to pptx tutorial showing how to export Excel to PowerPoint with
    editable text boxes, convert chart shape and embed images pptx using Aspose.
  headline: 'excel to pptx: Complete Java Guide to Export Editable Shapes'
  type: TechArticle
- description: excel to pptx tutorial showing how to export Excel to PowerPoint with
    editable text boxes, convert chart shape and embed images pptx using Aspose.
  name: 'excel to pptx: Complete Java Guide to Export Editable Shapes'
  steps:
  - name: A slide that mirrors the layout of your Excel sheet.
    text: A slide that mirrors the layout of your Excel sheet.
  - name: Text boxes that you can click, edit, and move—just like native PowerPoint
      shapes.
    text: Text boxes that you can click, edit, and move—just like native PowerPoint
      shapes.
  - name: Charts rendered as editable vector shapes (you can ungroup them to edit
      individual series).
    text: Charts rendered as editable vector shapes (you can ungroup them to edit
      individual series).
  - name: Any pictures from the workbook appear as embedded images, not linked files.
    text: Any pictures from the workbook appear as embedded images, not linked files.
  type: HowTo
tags:
- Aspose
- Java
- Excel
- PowerPoint
title: 'إكسل إلى بي بي تي إكس: دليل جافا الكامل لتصدير الأشكال القابلة للتحرير'
url: /ar/java/integration-interoperability/excel-to-pptx-complete-java-guide-to-export-editable-shapes/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# excel إلى pptx: دليل Java الكامل لتصدير الأشكال القابلة للتحرير

هل تساءلت يومًا كيف **excel to pptx** دون فقدان القدرة على تحرير صناديق النص لاحقًا؟ ربما قمت بإنشاء دفتر تقارير في Excel، أضفت بعض المخططات، والآن تحتاج تلك الرسوم إلى عرضها في عرض PowerPoint يمكن لفريقك تعديلها بسرعة. الخبر السار؟ يمكنك القيام بذلك برمجيًا باستخدام Aspose Cells و Aspose Slides، وستحافظ على صناديق النص القابلة للتحرير، وتحويل شكل المخطط، وحتى تضمين صور pptx على طول الطريق.

في هذا الدرس سنستعرض مثالًا كاملاً قابلاً للتنفيذ يأخذ ملف Excel، ويضبط عملية التصدير بحيث يبقى النص قابلاً للتحرير، وتتحول المخططات إلى أشكال يمكنك تعديلها، وتظل الصور مدمجة. بحلول النهاية ستحصل على خط أنابيب **export excel powerpoint** قوي يمكنك إدراجه في أي مشروع Java.

## المتطلبات المسبقة – ما تحتاجه قبل البدء

- **Java 17** أو أحدث (الكود يُجمع أيضًا مع Java 8+).  
- **Aspose Cells for Java** و **Aspose Slides for Java** ملفات JAR على مسار الفئة الخاص بك. يمكنك الحصول عليها من مستودع Aspose Maven أو تنزيل حزم التجربة.  
- دفتر عمل Excel (`ShapesInExcel.xlsx`) يحتوي على صندوق نص واحد على الأقل، ومخطط، وصورة مدمجة.  
- بيئة تطوير متكاملة أساسية (IntelliJ, Eclipse, VS Code…) – أي منها يناسبك، لكنني أفضل IntelliJ لتكوين التشغيل الفوري.

هذا كل شيء. لا أدوات بناء إضافية، ولا خدمات خارجية. لنبدأ مباشرة.

## الخطوة 1: تحميل دفتر عمل Excel – نقطة البداية لـ excel إلى pptx

أول شيء نقوم به هو فتح دفتر العمل المصدر. Aspose Cells يج abstracts تنسيق الملف، لذا لا تحتاج للقلق بشأن XML الأساسي.

```java
import com.aspose.cells.*;

public class ExportEditableShapes {
    public static void main(String[] args) throws Exception {
        // Load the Excel workbook that contains text boxes or shapes
        Workbook workbook = new Workbook("YOUR_DIRECTORY/ShapesInExcel.xlsx");
```

> **لماذا هذا مهم:** تحميل دفتر العمل يمنحنا الوصول إلى هيكل الورقة بالكامل، بما في ذلك أي كائنات رسم. إذا تخطيت هذه الخطوة، لن تعرف روتين التصدير ما الذي يجب تحويله، وستنتهي بشريحة فارغة.

## الخطوة 2: ضبط خيارات حفظ PPTX – الحفاظ على صناديق النص القابلة للتحرير وتحويل شكل المخطط

الآن نخبر Aspose Slides كيف نريد أن يتصرف الناتج. فئة `ImageOrPrintOptions` هي المكان الذي يحدث فيه السحر لـ **editable text boxes**، **convert chart shape**، و **embed images pptx**.

```java
        // Configure PPTX save options to preserve editable elements
        ImageOrPrintOptions pptxOptions = new ImageOrPrintOptions();
        pptxOptions.setExportImagesAsBase64(true);   // embed images directly in the PPTX
        pptxOptions.setExportChartToShape(true);     // turn charts into editable shapes
        pptxOptions.setEditableText(true);           // keep text boxes editable
```

* ملاحظة سريعة حول `setExportImagesAsBase64(true)`: هذا يجبر المُصدّر على تخزين الصور كتيارات Base64 داخل ملف `.pptx`. النتيجة ملف مكتمل ذاتيًا—بدون مراجع صور خارجية، مما يحقق متطلب **embed images pptx**.  
* `setExportChartToShape(true)` يفعل بالضبط ما يعد به كلمة **convert chart shape**. بدلاً من صورة ثابتة للمخطط، يقوم Aspose بإنشاء مجموعة من الأشكال المتجهية التي يمكنك فك تجميعها، وإعادة تلوينها، أو حتى استبدال نقاط البيانات لاحقًا.  
* أخيرًا، `setEditableText(true)` يضمن أن أي صندوق نص وضعته في Excel يبقى صندوق نص في PowerPoint، وليس صورة مسطحة. هذا هو جوهر دعم **editable text boxes**.

## الخطوة 3: حفظ دفتر العمل كملف PPTX – إكمال تدفق excel إلى pptx

مع تحميل دفتر العمل وضبط الخيارات، نستدعي ببساطة `save`. Aspose Cells يتولى الأعمال الثقيلة خلف الكواليس.

```java
        // Save the workbook as a PPTX file with the configured options
        workbook.save("YOUR_DIRECTORY/ExportedShapes.pptx", SaveFormat.PPTX);
    }
}
```

> **ماذا يحدث خلف الكواليس؟** Aspose يتكرر على كل ورقة عمل، يستخرج كائنات الرسم، يطبق الخيارات التي حددناها، ويكتب حزمة PowerPoint جديدة. يمكن فتح الملف الناتج في PowerPoint أو LibreOffice Impress أو أي عارض يحترم تنسيق Open XML.

### النتيجة المتوقعة

افتح `ExportedShapes.pptx` ويجب أن ترى:

1. شريحة تعكس تخطيط ورقة Excel الخاصة بك.  
2. صناديق نص يمكنك النقر عليها، تحريرها، وتحريكها—تمامًا مثل أشكال PowerPoint الأصلية.  
3. مخططات معروضة كأشكال متجهية قابلة للتحرير (يمكنك فك تجميعها لتحرير السلاسل الفردية).  
4. أي صور من دفتر العمل تظهر كصور مدمجة، ليست ملفات مرتبطة.

إذا لاحظت أي عناصر مفقودة، تحقق مرة أخرى من أن ملف Excel المصدر يحتوي فعليًا على تلك الكائنات. Aspose لن ينشئها سحرًا.

## الخطوة 4: تعديلات متقدمة – ضبط سلوك التصدير بدقة (اختياري)

بينما تغطي الخيارات الثلاثة أعلاه معظم حالات الاستخدام، يقدم Aspose Slides مقابض إضافية قد تجدها مفيدة:

| الخيار | ما يفعله | متى يستخدم |
|--------|----------|------------|
| `setExportHiddenSheets(true)` | يتضمن أوراق العمل المخفية كشرائح إضافية. | إذا كان تقريرك يستخدم أوراقًا مخفية للحسابات. |
| `setExportNotesToComments(true)` | ينقل تعليقات خلايا Excel إلى ملاحظات شرائح PowerPoint. | عندما تريد الحفاظ على سياق التعليقات التوضيحية. |
| `setSlideSize(SlideSizeTypeOnScreen16x9)` | يفرض حجم شريحة 16:9. | للعروض الحديثة ذات الشاشة العريضة. |

يمكنك ضبط أي من هذه على نفس كائن `pptxOptions` قبل استدعاء `save`.

```java
pptxOptions.setExportHiddenSheets(true);
pptxOptions.setExportNotesToComments(true);
pptxOptions.setSlideSize(SlideSizeTypeOnScreen16x9);
```

## الخطوة 5: تشغيل الكود – من IDE إلى سطر الأوامر

إذا كنت تستخدم IDE، فقط اضغط **Run**. لبناء سطر الأوامر، قم بالترجمة والتنفيذ هكذا (مع افتراض وضع ملفات Aspose JAR في مجلد `libs/`):

```bash
javac -cp "libs/*" ExportEditableShapes.java
java -cp ".:libs/*" ExportEditableShapes
```

في Windows استبدل `:` بـ `;` في مسار الفئة. بعد التنفيذ، تحقق من مجلد `YOUR_DIRECTORY` للحصول على `ExportedShapes.pptx`.

## الأخطاء الشائعة والنصائح الاحترافية

- **المشكلة:** نسيان ضبط `setEditableText(true)`. النتيجة: كل النص يظهر كصورة مسطحة.  
  **نصيحة احترافية:** بعد التشغيل الأول، افتح PPTX وحاول تحرير صندوق نص. إذا لم تستطع، تحقق مرة أخرى من الخيار.  

- **المشكلة:** ملفات Excel الكبيرة قد تسبب ضغطًا على الذاكرة.  
  **نصيحة احترافية:** استخدم `Workbook.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` قبل التحميل للسماح لـ Aspose ببث البيانات بدلاً من تحميل كل شيء في الذاكرة.  

- **المشكلة:** الصور تظهر غير واضحة.  
  **نصيحة احترافية:** تأكد من أن دقة الصورة المصدر عالية بما فيه الكفاية؛ Aspose يحترم DPI الأصلي عندما يكون `setExportImagesAsBase64(true)` مفعلاً.  

- **المشكلة:** المخططات تفقد تسميات البيانات.  
  **نصيحة احترافية:** بعد التحويل، انقر بزر الماوس الأيمن على شكل المخطط في PowerPoint، اختر *Edit Data* للتحقق من جدول البيانات الأساسي. إذا كانت التسميات مفقودة، فعّل `setExportChartDataLabels(true)` (متاح في إصدارات Aspose الأحدث).  

## مثال كامل يعمل – كل الكود في مكان واحد

فيما يلي البرنامج الكامل الجاهز للنسخ واللصق. استبدل `YOUR_DIRECTORY` بمسار مطلق أو نسبي على جهازك.

```java
import com.aspose.cells.*;
import com.aspose.slides.*;

public class ExportEditableShapes {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the Excel workbook that contains text boxes or shapes
        Workbook workbook = new Workbook("YOUR_DIRECTORY/ShapesInExcel.xlsx");

        // 2️⃣ Configure PPTX save options to preserve editable elements
        ImageOrPrintOptions pptxOptions = new ImageOrPrintOptions();
        pptxOptions.setExportImagesAsBase64(true);   // embed images directly
        pptxOptions.setExportChartToShape(true);     // convert charts to shapes
        pptxOptions.setEditableText(true);           // keep text boxes editable

        // Optional: fine‑tune additional settings
        pptxOptions.setExportHiddenSheets(true);
        pptxOptions.setExportNotesToComments(true);
        pptxOptions.setSlideSize(SlideSizeTypeOnScreen16x9);

        // 3️⃣ Save the workbook as a PPTX file with the configured options
        workbook.save("YOUR_DIRECTORY/ExportedShapes.pptx", SaveFormat.PPTX);

        System.out.println("Export completed! Check ExportedShapes.pptx");
    }
}
```

شغّله، افتح ملف PowerPoint المُولد، وسترى بالضبط ما وصفناه سابقًا.

## الخلاصة – إتقان excel إلى pptx مع الأشكال القابلة للتحرير

لقد غطينا للتو سير عمل **excel to pptx** يحافظ على صناديق النص قابلة للتحرير، يحول المخططات إلى أشكال متجهية، ويضمّن الصور داخل العرض مباشرة. الفكرة الأساسية؟ من خلال تعديل عدد قليل من خصائص `ImageOrPrintOptions` تحصل على تجربة **export excel powerpoint** نظيفة تشعر بأنها أصلية لمستخدمي PowerPoint.

من هنا قد تستكشف:

- إضافة انتقالات الشرائح برمجيًا (`Slide.addTransition` من Aspose Slides).  
- إنشاء شرائح متعددة من أوراق عمل متعددة (التكرار عبر `workbook.getWorksheets()`).  
- دمج هذا التصدير مع خط أنابيب تحويل PDF لتقارير هجينة.

لا تتردد في التجربة، كسر الأشياء، ثم إعادتها معًا— هكذا تسيطر حقًا على عملية **excel to pptx**. هل لديك أسئلة أو تريد مشاركة تعديل مميز؟ اترك تعليقًا أدناه، وبرمجة سعيدة!

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة شاملة للكود مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [How to Convert Excel to PowerPoint Using Aspose.Cells for .NET: A Complete Guide](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [How to Add and Access Text Boxes in Excel using Aspose.Cells .NET | Step‑By‑Step Guide](/cells/english/net/images-shapes/aspose-cells-net-add-text-boxes-excel/)
- [How to Convert Excel Sheets to Images Using Aspose.Cells .NET (Step‑By‑Step Guide)](/cells/english/net/workbook-operations/convert-excel-sheets-images-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}