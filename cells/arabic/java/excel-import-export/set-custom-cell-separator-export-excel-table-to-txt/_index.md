---
category: general
date: 2026-07-16
description: تعيين فاصل خلايا مخصص عند تصدير جدول إكسل إلى TXT باستخدام Aspose.Cells.
  تعلم كيفية تصدير صيغ إكسل إلى نص وحفظ ورقة العمل كملف txt.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set custom cell separator
- export excel table to txt
- export excel formulas to text
- save worksheet as txt file
- export excel data as plain text
language: ar
lastmod: 2026-07-16
og_description: تحديد فاصل خلايا مخصص في Aspose.Cells يتيح لك تصدير جدول Excel إلى
  TXT بتنسيق دقيق. صدّر صيغ Excel إلى نص واحفظ ورقة العمل كملف TXT بسهولة.
og_image_alt: Screenshot showing set custom cell separator option in Aspose.Cells
  export settings
og_title: تعيين فاصل خلايا مخصص – تصدير جدول إكسل إلى TXT
schemas:
- author: Aspose
  dateModified: '2026-07-16'
  description: Set custom cell separator when exporting Excel table to TXT using Aspose.Cells.
    Learn how to export Excel formulas to text and save worksheet as txt file.
  headline: Set Custom Cell Separator – Export Excel Table to TXT
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel Export
title: تعيين فاصل خلايا مخصص – تصدير جدول إكسل إلى TXT
url: /ar/java/excel-import-export/set-custom-cell-separator-export-excel-table-to-txt/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تعيين فاصل خلايا مخصص – تصدير جدول إكسل إلى TXT

تعيين فاصل خلايا مخصص هو السر الذي تحتاجه عندما تريد استخراج نص منظم من ورقة إكسل. هل تساءلت يوماً كيف **تصدير جدول إكسل إلى txt** دون أن ينتهي بك الأمر بملف مليء بفواصل commas وفواصل أسطر عشوائية؟ في هذا الدرس سنستعرض العملية بالكامل باستخدام Aspose.Cells for Java، من تحميل المصنف إلى **حفظ ورقة العمل كملف txt** باستخدام الفاصل الذي تختاره.

## ما ستتعلمه

- كيفية **تعيين فاصل خلايا مخصص** لتصدير النصوص.
- الخطوات الدقيقة لـ **تصدير صيغ إكسل إلى نص** بحيث تُنقل القيم المُقيمة معك.
- طرق **تصدير بيانات إكسل كنص عادي** مع الحفاظ على التخطيط.
- عينة كود كاملة جاهزة للتنفيذ يمكنك نسخها ولصقها في مشروعك.

بنهاية هذا الدليل ستتمكن من أخذ أي مصنف إكسل، واختيار عمود (|) أو تبويب (\t) أو أي حرف تفضله، وإنتاج ملف نصي مُفصل نظيف تحبه الأنظمة اللاحقة.

### المتطلبات المسبقة

- تثبيت Java 8 أو أحدث.
- Maven (أو أي أداة بناء) لجلب مكتبة Aspose.Cells for Java.
- مصنف تجريبي (`TableDemo.xlsx`) يحتوي على جدول بصيغ.

إذا كان لديك كل ذلك، لنبدأ—بدون إطالة، فقط خطوات عملية.

## الخطوة 1: إضافة Aspose.Cells إلى مشروعك

قبل أن تتمكن من **تعيين فاصل خلايا مخصص**, تحتاج إلى وجود ملف JAR الخاص بـ Aspose.Cells على مسار الفئة. أسهل طريقة هي عبر Maven:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- Check Maven Central for the latest version -->
</dependency>
```

إذا كنت تفضل Gradle، استبدل XML بما يعادل `implementation 'com.aspose:aspose-cells:24.10'`. بمجرد حل الاعتماد، ستكون جاهزاً لكتابة كود Java يتعامل مع ملفات إكسل.

## الخطوة 2: تحميل المصنف – التحضير لتصدير جدول إكسل إلى TXT

السطر الأول من الكود يكون دائماً هو نفسه: فتح المصنف الذي يحتوي على الجدول الذي تريد تصديره.

```java
import com.aspose.cells.*;

public class ExportTableWithOptions {
    public static void main(String[] args) throws Exception {
        // Load the workbook containing the table
        Workbook workbook = new Workbook("YOUR_DIRECTORY/TableDemo.xlsx");
        Worksheet worksheet = workbook.getWorksheets().get(0);
```

هنا نأخذ أول ورقة عمل (`get(0)`). إذا كانت بياناتك في ورقة مختلفة، فقط غيّر الفهرس أو استخدم `get("SheetName")`. هذه الخطوة أساسية لـ **تصدير جدول إكسل إلى txt** لأن المُصدِّر يعمل على مستوى ورقة العمل.

## الخطوة 3: تعيين فاصل خلايا مخصص – جوهر عملية التصدير

الآن يأتي نجم العرض: تكوين `ExportTableOptions`. هذا الكائن يتيح لك تحديد بالضبط كيف سيظهر كل خلية في الملف النصي النهائي.

```java
        // Define how the table should be exported
        ExportTableOptions exportTableOptions = new ExportTableOptions();

        // 1️⃣ Export cell contents as plain strings (no rich formatting)
        exportTableOptions.setExportAsString(true);

        // 2️⃣ Include the evaluated formula result, not the formula itself
        exportTableOptions.setFormulaValueInCell(true);

        // 3️⃣ Set the custom separator – this is where we set custom cell separator
        exportTableOptions.setCellValueSeparator("|"); // you can use any char you like
```

لماذا **نُعيّن فاصل خلايا مخصص**؟ لأن الفاصل الافتراضي هو تبويب، وقد يتعارض مع البيانات التي تحتوي بالفعل على تبويبات. باختيار عمود (|) أو فاصلة منقوطة، تضمن أن كل عمود يبقى مميزاً عندما يقرأ محلل لاحق الملف.

### تصدير صيغ إكسل إلى نص

السطر `setFormulaValueInCell(true)` يخبر Aspose.Cells بكتابة **تصدير صيغ إكسل إلى نص** كنتيجة الصيغة، وليس نص الصيغة نفسه. إذا حذفت هذا السطر، خلية تحتوي على `=SUM(A1:A5)` ستظهر كـ `=SUM(A1:A5)` في ملف TXT، وهو ما نادرًا ما يكون مرغوبًا.

## الخطوة 4: ربط خيارات التصدير بخيارات حفظ TXT

الآن نربط خيارات الجدول هذه بإعدادات تصدير TXT العامة.

```java
        // Attach the table export options to TXT save options
        TxtSaveOptions txtSaveOptions = new TxtSaveOptions();
        txtSaveOptions.setExportTableOptions(exportTableOptions);
```

`TxtSaveOptions` هو الكائن الشامل الذي يتحكم في كيفية كتابة ورقة العمل بالكامل. بربط `exportTableOptions` به، تضمن أن كل جدول في الورقة يلتزم بقاعدة **تعيين فاصل خلايا مخصص**.

## الخطوة 5: حفظ ورقة العمل كملف TXT – إكمال عملية التصدير

أخيرًا، نكتب الملف إلى القرص.

```java
        // Save the worksheet as a TXT file using the configured options
        workbook.save("YOUR_DIRECTORY/TableExported.txt", txtSaveOptions);
    }
}
```

تشغيل هذا البرنامج ينشئ `TableExported.txt`. كل صف من جدول إكسل الأصلي سيظهر الآن كسطر من القيم المفصولة بالعمود (|)، مثل:

```
Name|Quantity|Price|Total
Apple|10|0.50|5.00
Banana|5|0.30|1.50
```

لاحظ كيف تم تقييم الصيغة في عمود **Total** قبل الكتابة—بفضل `setFormulaValueInCell(true)`. هذا هو جوهر **تصدير بيانات إكسل كنص عادي** مع الحفاظ على النتائج المحسوبة.

## الخطوة 6: التحقق من النتيجة – هل تبدو صحيحة؟

افتح الملف `TableExported.txt` المُولد في أي محرر نصوص. يجب أن ترى:

- سطر واحد لكل صف إكسل.
- أعمدة مفصولة بالحرف العمودي الذي حددته باستخدام `setCellValueSeparator`.
- لا توجد فواصل commas أو تبويبات غير مرغوب فيها إلا إذا كانت جزءًا من قيم الخلايا الأصلية.
- نتائج الصيغ، وليس الصيغ نفسها.

إذا لاحظت أي أحرف غير متوقعة، أعد فحص الفاصل الذي اخترته. بعض الأحرف (مثل العمود) آمنة لمعظم المحللات بنمط CSV، لكن إذا كانت بياناتك تحتوي بالفعل على أعمدة، فكر في فاصل مختلف مثل `~` أو تبويب (`\t`).

## نصائح، حالات خاصة، وأفضل الممارسات – تصدير بيانات إكسل كنص عادي

| الحالة | ما الذي يجب فعله |
|-----------|------------|
| **البيانات تحتوي بالفعل على الفاصل الذي اخترته** | استبدل بفاصل أقل شيوعًا (`^`، `~`، أو أحرف Unicode غير مطبوعة). |
| **تحتاج إلى ترميز UTF‑8** |  |

## ما الذي ينبغي أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [حفظ إكسل كملف نصي بفاصل مخصص باستخدام Aspose.Cells](/cells/english/net/workbook-operations/save-excel-text-custom-separator-aspose-cells-net/)
- [حفظ إكسل نص مخصص الفاصل Aspose Cells Net](/cells/german/net/workbook-operations/save-excel-text-custom-separator-aspose-cells-net/)
- [حفظ إكسل نص مخصص الفاصل Aspose Cells Net](/cells/french/net/workbook-operations/save-excel-text-custom-separator-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}