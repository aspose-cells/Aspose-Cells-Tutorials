---
category: general
date: 2026-08-14
description: نسخ نطاق بين المصنفات باستخدام Java و Aspose.Cells. تعلم كيفية نسخ مصنف
  جدول محوري، وتصدير صورة إلى PowerPoint، وإزالة AutoFilter من جدول Excel.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy range between workbooks
- copy pivot table workbook
- export picture to powerpoint
- copy excel range to new workbook
- remove autofilter from excel table
language: ar
lastmod: 2026-08-14
og_description: نسخ نطاق بين دفاتر العمل في جافا. يوضح هذا الدليل كيفية نسخ دفتر عمل
  جدول محوري، وتصدير صورة إلى PowerPoint، وإزالة AutoFilter من جدول Excel.
og_image_alt: Screenshot of Java code copying range between workbooks with Aspose.Cells
og_title: نسخ نطاق بين دفاتر العمل في جافا – دليل Aspose.Cells الكامل
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: Copy range between workbooks with Java using Aspose.Cells. Learn to
    copy pivot table workbook, export picture to PowerPoint and remove AutoFilter
    from Excel table.
  headline: Copy range between workbooks in Java – step‑by‑step guide
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel automation
- PowerPoint export
title: نسخ نطاق بين دفاتر العمل في جافا – دليل خطوة بخطوة
url: /ar/java/range-management/copy-range-between-workbooks-in-java-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# نسخ نطاق بين دفاتر العمل في جافا – دليل خطوة بخطوة

إذا كنت بحاجة إلى **نسخ نطاق بين دفاتر العمل** في جافا، توفر Aspose.Cells واجهة برمجة تطبيقات نظيفة تتعامل مع الكائنات المعقدة مثل جداول المحور (pivot tables) والصور. يوضح هذا الدليل كيفية **نسخ دفتر عمل جدول المحور**، **تصدير الصورة إلى PowerPoint**، و**إزالة AutoFilter من جدول Excel** مع الحفاظ على سهولة قراءة وصيانة الشيفرة.

ستتعلم كيف تقوم بـ:

* تحميل دفتر عمل مصدر وتحديد النطاق المصدر.  
* إنشاء دفتر عمل وجهة ونسخ النطاق بحيث يبقى جدول المحور سليماً.  
* تصدير الصورة الأولى في الورقة ككائن PowerPoint قابل للتحرير.  
* إزالة AutoFilter من أول جدول Excel.  
* تحميل دفتر عمل باستخدام `SmartMarkerOptions` لمعالجة مصفوفات JSON كقيمة خلية واحدة.

المثال يستخدم Aspose.Cells 23.10 لجافا، لكن المفاهيم تنطبق على الإصدارات السابقة كذلك.

---

## المتطلبات المسبقة

| المتطلب | لماذا يهم |
|-------------|----------------|
| Java 17 أو أحدث | مطلوب من قبل أحدث بيئة تشغيل Aspose.Cells. |
| Aspose.Cells for Java (Maven artifact `com.aspose:aspose-cells`) | يوفر الفئات `Workbook`، `Worksheet`، `Range`، والفئات المرتبطة المستخدمة في الشيفرة. |
| ملف Excel مصدر (`src.xlsx`) يحتوي على جدول محور، صورة، وجدول مع AutoFilter. | يقوم الدليل بالتعامل مع هذه الكائنات لتوضيح كل ميزة. |

أضف تبعية Maven إلى ملف `pom.xml` الخاص بك:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
    <classifier>jdk17</classifier>
</dependency>
```

---

## نسخ نطاق بين دفاتر العمل – تحميل المصدر والوجهة

الخطوة الأولى هي فتح دفتر العمل المصدر، اختيار النطاق الذي يحتوي على البيانات التي تريد نسخها، وإنشاء دفتر عمل وجهة فارغ.

```java
import com.aspose.cells.*;

public class CopyRangeDemo {
    public static void main(String[] args) throws Exception {
        // Load the source workbook that holds the pivot table, picture, and table.
        Workbook sourceWb = new Workbook("YOUR_DIRECTORY/src.xlsx");
        Worksheet sourceWs = sourceWb.getWorksheets().get(0);

        // Define the range that includes the pivot table (A1:G20 in this example).
        Range sourceRange = sourceWs.getCells().createRange("A1:G20");

        // Create a new workbook that will receive the copied range.
        Workbook destWb = new Workbook();
        Worksheet destWs = destWb.getWorksheets().get(0);
        Range destRange = destWs.getCells().createRange("A1");
```

> **لماذا هذا مهم:** باستخدام `Range.copy`، تقوم Aspose.Cells بنسخ ليس فقط قيم الخلايا الخام بل أيضاً ذاكرة التخزين المؤقت لجدول المحور، مما يبقي جدول المحور فعالاً في دفتر العمل الوجهة.

---

## نسخ دفتر عمل جدول المحور أثناء نسخ النطاق

الآن قم بنسخ النطاق المحدد من دفتر العمل المصدر إلى دفتر العمل الوجهة. يتم الحفاظ على جدول المحور تلقائياً لأن النطاق يتضمن ذاكرة التخزين المؤقت لجدول المحور.

```java
        // Copy the source range to the destination range.
        destRange.copy(sourceRange);

        // Save the intermediate workbook to verify that the pivot table was copied.
        destWb.save("YOUR_DIRECTORY/destination.xlsx");
```

> **النتيجة:** فتح `destination.xlsx` يظهر نفس تخطيط جدول المحور كما في `src.xlsx`. لا يلزم أي شفرة إضافية لإعادة بناء ذاكرة التخزين المؤقت لجدول المحور.

---

## تصدير الصورة إلى PowerPoint

يمكن لـ Aspose.Cells وضع علامة على صورة لتصديرها إلى كائن PowerPoint قابل للتحرير. الشيفرة التالية تختار الصورة الأولى في ورقة الوجهة وتضبط علم التصدير.

```java
        // Retrieve the first picture on the destination sheet.
        Shape picture = destWs.getPictures().get(0);

        // Instruct Aspose.Cells to export this picture as a PowerPoint object.
        picture.getPictureFormat().setExportToPptx(true);

        // Optionally, save the workbook as PPTX to see the result.
        destWb.save("YOUR_DIRECTORY/destination.pptx");
```

> **ما تراه:** فتح `destination.pptx` في PowerPoint يظهر الصورة كشكل أصلي يمكنك تحريره، تغيير حجمه، أو تحريكه.

---

## إزالة AutoFilter من جدول Excel

إذا كانت الورقة المصدر تحتوي على جدول مع AutoFilter، قد ترغب في إزالته بعد النسخ. الشيفرة أدناه تصل إلى أول جدول وتزيل الفلتر الخاص به.

```java
        // Access the first table on the destination sheet.
        Table table = destWs.getTables().get(0);

        // Remove the AutoFilter by assigning null.
        table.setAutoFilter(null);

        // Save the final workbook.
        destWb.save("YOUR_DIRECTORY/final_output.xlsx");
```

> **التأثير:** يبقى الجدول في دفتر العمل، لكن أسهم الفلتر المنسدلة تختفي، مما يمنحك عرض بيانات نظيف.

---

## تحميل دفتر عمل مع خيارات SmartMarker – معالجة مصفوفات JSON كخلية واحدة

عند إنشاء تقرير من JSON، يمكن لـ Aspose.Cells معالجة مصفوفة كاملة كقيمة خلية واحدة. هذا مفيد لتضمين سلاسل JSON في قالب دون توسيعها إلى خلايا متعددة.

```java
        // Configure LoadOptions to enable SmartMarker array handling.
        LoadOptions loadOptions = new LoadOptions();
        SmartMarkerOptions smOptions = new SmartMarkerOptions();
        smOptions.setArrayAsSingle(true);
        loadOptions.setSmartMarkerOptions(smOptions);

        // Load a template workbook using the configured options.
        Workbook smartMarkerWb = new Workbook("YOUR_DIRECTORY/template.xlsx", loadOptions);

        // Continue processing (e.g., populate markers) as needed.
        // ...

        // Save the processed workbook.
        smartMarkerWb.save("YOUR_DIRECTORY/template_filled.xlsx");
    }
}
```

> **لماذا قد تستخدم هذا:** إذا كان حمولة JSON الخاصة بك تحتوي على مصفوفة يجب أن تظهر كسلسلة JSON في خلية واحدة، فإن `setArrayAsSingle(true)` يمنع Aspose.Cells من توسيع المصفوفة إلى صفوف أو أعمدة منفصلة.

![نسخ نطاق بين دفاتر العمل في جافا – مثال كود Aspose.Cells](copy-range-workbooks.png)

*نص بديل للصورة:* **نسخ نطاق بين دفاتر العمل في جافا – مثال كود Aspose.Cells** (يتطابق مع الكلمة الرئيسية الأساسية).

---

## النتيجة المتوقعة

| اسم الملف                | المحتوى |
|--------------------------|----------|
| `destination.xlsx`       | نطاق منسوخ مع جدول محور فعال. |
| `destination.pptx`       | صورة مُصدرة كشكل PowerPoint قابل للتحرير. |
| `final_output.xlsx`      | جدول بدون أسهم AutoFilter. |
| `template_filled.xlsx`   | مصفوفة JSON مخزنة كقيمة خلية واحدة. |

افتح كل ملف في التطبيق المناسب (Excel أو PowerPoint) للتحقق من نجاح العمليات.

---

## الخلاصة

أنت الآن تعرف كيفية **نسخ نطاق بين دفاتر العمل** في جافا باستخدام Aspose.Cells، مع الحفاظ على جدول المحور، تصدير صورة إلى PowerPoint، وإزالة AutoFilter من جدول Excel. يمكن توسيع النمط نفسه لنسخ أي نطاق Excel إلى دفتر عمل جديد، معالجة مصفوفات JSON عبر SmartMarker، أو ربط تحويلات إضافية.

الخطوات التالية التي قد تستكشفها:

* **نسخ نطاق Excel إلى دفتر عمل جديد** مع أوراق عمل متعددة.  
* استخدم **تصدير الصورة إلى PowerPoint** لاستخراج الصور على دفعات.  
* طبّق **إزالة AutoFilter من جدول Excel** في خطوط تقارير أكبر.  
* دمج هذه التقنيات مع Aspose.Slides لأتمتة كاملة من Excel إلى PowerPoint.

لا تتردد في تجربة عناوين نطاق مختلفة، جداول محور متعددة، أو صيغ صور مخصصة. تم تصميم Aspose.Cells API لتوفير مرونة برمجية، لذا يمكنك تعديل الأنماط المعروضة هنا لتناسب أي سيناريو أتمتة Excel مؤسسي.

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شيفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك الخاصة.

- [نسخ الصور بين الأوراق في Excel باستخدام Aspose.Cells لجافا: دليل شامل](/cells/english/java/images-shapes/copy-images-between-sheets-excel-aspose-cells-java/)
- [نسخ إعدادات تخطيط الصفحة بين أوراق العمل في Excel باستخدام Aspose.Cells جافا](/cells/english/java/headers-footers/copy-page-setup-excel-aspose-cells-java/)
- [نسخ أوراق العمل في Excel بين دفاتر العمل](/cells/english/net/excel-copy-worksheet/excel-copy-worksheets-between-workbooks/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}