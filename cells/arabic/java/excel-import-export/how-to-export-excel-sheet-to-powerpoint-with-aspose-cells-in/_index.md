---
category: general
date: 2026-09-27
description: كيفية تصدير ورقة Excel إلى PowerPoint باستخدام Aspose.Cells في Java –
  دليل خطوة بخطوة يوضح أيضًا كيفية تحويل دفتر عمل Excel إلى عرض تقديمي PowerPoint.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to export excel sheet to powerpoint
- convert excel workbook to powerpoint presentation
language: ar
lastmod: 2026-09-27
og_description: كيفية تصدير ورقة Excel إلى PowerPoint باستخدام Aspose.Cells في Java.
  تعلم كيفية تحويل مصنف Excel إلى عرض تقديمي PowerPoint مع الشيفرة الكاملة.
og_image_alt: Java code snippet that exports an Excel sheet to a PowerPoint file using
  Aspose.Cells
og_title: كيفية تصدير ورقة إكسل إلى باوربوينت – دليل جافا مع Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: How to export Excel sheet to PowerPoint with Aspose.Cells in Java –
    a step‑by‑step guide that also shows how to convert Excel workbook to PowerPoint
    presentation.
  headline: How to export Excel sheet to PowerPoint with Aspose.Cells in Java
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel
- PowerPoint
- Document conversion
title: كيفية تصدير ورقة Excel إلى PowerPoint باستخدام Aspose.Cells في Java
url: /ar/java/excel-import-export/how-to-export-excel-sheet-to-powerpoint-with-aspose-cells-in/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تصدير ورقة Excel إلى PowerPoint باستخدام Aspose.Cells في Java

إذا كنت بحاجة إلى **كيفية تصدير ورقة Excel إلى PowerPoint**، فإن هذا الدليل يقدم لك حلاً كاملاً وجاهزًا للتنفيذ. ستشاهد بالضبط كيفية **تحويل دفتر عمل Excel إلى عرض تقديمي PowerPoint** مع الحفاظ على مربعات النص القابلة للتحرير والتنسيق الأساسي.

يفترض الدليل أنك تمتلك بيئة تطوير Java تعمل ورخصة صالحة لـ Aspose.Cells for Java. بنهاية المقال ستحصل على برنامج Java يقوم بتحميل دفتر عمل Excel، يصدر ورقة العمل الأولى، ويكتب ملف `.pptx` يمكن فتحه وتعديله في Microsoft PowerPoint.

## المتطلبات المسبقة

| المتطلبات | لماذا يهم |
|-------------|----------------|
| Java 17 أو أحدث | يدعم Aspose.Cells بيئات Java الحديثة ويوفر أداءً أفضل. |
| Aspose.Cells for Java (الإصدار 23.10 أو أحدث) | تحتوي المكتبة على الدالة `Workbook.save(..., SaveFormat.PPTX)` المستخدمة في التحويل. |
| نسخة مرخصة من Aspose.Cells | بدون ترخيص تعمل المكتبة في وضع التقييم وتضيف علامات مائية. |
| ملف Excel يحتوي على صندوق نص قابل للتحرير على الأقل | يحافظ التحويل على صندوق النص كشكل قابل للتحرير في PowerPoint. |
| IDE أو أداة بناء (مثل Maven، Gradle) | لتجميع وتشغيل كود المثال. |

## الخطوة 1: إضافة Aspose.Cells إلى مشروعك

إذا كنت تستخدم Maven، أضف الاعتماد التالي إلى `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
    <classifier>jdk17</classifier>
</dependency>
```

لـ Gradle، ضع هذا المقتطف في `build.gradle`:

```gradle
implementation 'com.aspose:aspose-cells:23.10:jdk17'
```

> **Pro tip:** أعلن عن الاعتماد في نطاق `provided` إذا كنت تحتاج المكتبة فقط وقت التشغيل على الخادم.

## الخطوة 2: إعداد دفتر عمل Excel

أنشئ ملف Excel (`WorkbookWithTextbox.xlsx`) يحتوي على صندوق نص قابل للتحرير في ورقة العمل الأولى. يمكن إدراج صندوق النص في Excel عبر **Insert → Text Box**. احفظ الملف في دليل يمكنك الإشارة إليه من Java، مثل `src/main/resources`.

## الخطوة 3: كتابة كود التحويل

أنشئ فئة Java باسم `ExportEditableTextbox`. يحتوي الكود أدناه على جميع الاستيرادات، ومعالجة الأخطاء، وتعليقات تشرح كل عملية.

```java
package com.example.excel2ppt;

import com.aspose.cells.SaveFormat;
import com.aspose.cells.Workbook;

/**
 * Demonstrates how to export an Excel sheet to PowerPoint while preserving
 * editable text boxes. The example uses Aspose.Cells for Java.
 */
public class ExportEditableTextbox {

    public static void main(String[] args) throws Exception {
        // --------------------------------------------------------------------
        // Step 1: Load the Excel workbook that contains the editable textbox.
        // --------------------------------------------------------------------
        String workbookPath = "src/main/resources/WorkbookWithTextbox.xlsx";
        Workbook workbook = new Workbook(workbookPath);

        // --------------------------------------------------------------------
        // Step 2: Export the first worksheet to a PowerPoint presentation.
        //         The SaveFormat.PPTX option writes a .pptx file that PowerPoint
        //         can open and edit. The textbox remains editable.
        // --------------------------------------------------------------------
        String outputPath = "src/main/resources/Worksheet.pptx";
        workbook.save(outputPath, SaveFormat.PPTX);

        System.out.println("Conversion successful. PowerPoint saved to: " + outputPath);
    }
}
```

### لماذا يعمل هذا

* `Workbook` يمثل ملف Excel بالكامل. تحميله يفسر جميع أوراق العمل، المخططات، والأشكال.  
* `workbook.save(..., SaveFormat.PPTX)` يُشغّل محرك التحويل المدمج في Aspose.Cells. يقوم المحرك بربط خلايا Excel والصفوف والأشكال بشرائح PowerPoint، مع الحفاظ على صناديق النص القابلة للتحرير كأشكال PowerPoint.  
* الطريقة تكتب شريحة واحدة لكل ورقة عمل. في هذا المثال تصبح ورقة العمل الأولى هي الشريحة الوحيدة.

## الخطوة 4: تشغيل البرنامج

قم بتجميع وتنفيذ الفئة باستخدام أداة البناء الخاصة بك:

```bash
mvn compile exec:java -Dexec.mainClass=com.example.excel2ppt.ExportEditableTextbox
```

أو، إذا كنت تستخدم Gradle:

```bash
gradle run --args='com.example.excel2ppt.ExportEditableTextbox'
```

بعد انتهاء البرنامج، افتح `Worksheet.pptx` في Microsoft PowerPoint. يجب أن ترى شريحة تعكس ورقة Excel، وصندوق النص الذي أنشأته في Excel يظهر كشكل قابل للتحرير يمكنك النقر المزدوج عليه وتعديله.

## الخطوة 5: معالجة أوراق عمل متعددة (اختياري)

إذا كنت بحاجة إلى تصدير **جميع** أوراق العمل في دفتر العمل، استبدل استدعاء ورقة العمل الواحدة بحلقة:

```java
for (int i = 0; i < workbook.getWorksheets().getCount(); i++) {
    workbook.save("Worksheet_" + i + ".pptx", SaveFormat.PPTX);
}
```

كل تكرار ينشئ ملف PowerPoint منفصل (`Worksheet_0.pptx`, `Worksheet_1.pptx`, …). لعرض تقديمي واحد يحتوي على عدة شرائح، يضيف Aspose.Cells شريحة تلقائيًا لكل ورقة عمل عند استدعاء `save` مرة واحدة؛ لا يلزم أي كود إضافي.

## حالات خاصة وأفضل الممارسات

| الحالة | النهج الموصى به |
|-----------|----------------------|
| دفتر عمل كبير (مئات الـ MB) | زيادة حجم الذاكرة المخصصة للـ JVM (`-Xmx4g`) والنظر في تصدير أوراق العمل بشكل فردي لتجنب أخطاء نفاد الذاكرة. |
| دفتر عمل محمي بكلمة مرور | استخدم `LoadOptions` لتزويد كلمة المرور قبل التحميل: `new LoadOptions(LoadFormat.XLSX, "pwd")`. |
| الحاجة للحفاظ على صيغ Excel | لا يدعم PowerPoint الصيغ؛ يتم تحويلها إلى قيم ثابتة أثناء التحويل. |
| الحاجة إلى تخطيط شريحة مخصص | بعد التحويل، عدّل ملف `.pptx` الناتج باستخدام Aspose.Slides for Java لضبط القوالب أو إضافة حركات. |
| التشغيل في خدمة ويب | بث الإخراج مباشرة إلى استجابة HTTP بدلاً من كتابة ملف: `workbook.save(response.getOutputStream(), SaveFormat.PPTX);` |

## النتيجة المتوقعة

تشغيل المثال ينتج ملفًا باسم `Worksheet.pptx`. فتحه في PowerPoint يظهر:

* شريحة واحدة تتطابق بصريًا مع ورقة Excel الأولى.  
* صندوق نص قابل للتحرير موضعه بالضبط كما كان في Excel.  
* تنسيق الخلايا الأساسي (حجم الخط، اللون، الحدود) محفوظ.

تطبع وحدة التحكم:

```
Conversion successful. PowerPoint saved to: src/main/resources/Worksheet.pptx
```

## الخلاصة

أنت الآن تعرف **كيفية تصدير ورقة Excel إلى PowerPoint** باستخدام Aspose.Cells for Java، وتفهم أيضًا **كيفية تحويل دفتر عمل Excel إلى عرض تقديمي PowerPoint** في سيناريوهات العالم الحقيقي. الحل يعمل لتصدير ورقة عمل واحدة، دفاتر عمل متعددة الأوراق، ويمكن توسيعه باستخدام Aspose.Slides لمزيد من تخصيص الشرائح.

---

### الخطوات التالية

* استكشف **Aspose.Slides for Java** لإضافة حركات، مخططات، أو قوالب شرائح مخصصة بعد التحويل.  
* جرّب تحويل دفاتر العمل التي تحتوي على مخططات؛ Aspose.Cells يرسم المخططات ككائنات مخطط PowerPoint أصلية.  
* استكشف المعالجة الدفعية بقراءة دليل يحتوي على ملفات Excel وتوليد PowerPoint لكل ملف.

لا تتردد في تجربة الكود، تعديل مسارات الملفات، ودمج التحويل في تطبيقات Java أكبر مثل خدمات التقارير أو خطوط أنابيب المستندات الآلية. Happy coding!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك الخاصة.

- [كيفية تصدير Excel إلى PowerPoint – دليل خطوة بخطوة](/cells/english/net/converting-excel-files-to-other-formats/how-to-export-excel-to-powerpoint-step-by-step-guide/)
- [كيفية تحويل Excel إلى PDF في Java باستخدام Aspose.Cells: دليل خطوة بخطوة](/cells/english/java/workbook-operations/convert-excel-to-pdf-aspose-cells-java/)
- [كيفية تصدير ورقة عمل Excel إلى PNG باستخدام Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-to-png-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}