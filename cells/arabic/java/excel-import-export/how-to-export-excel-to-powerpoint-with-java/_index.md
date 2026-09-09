---
category: general
date: 2026-09-08
description: تعلم كيفية تصدير Excel إلى PowerPoint باستخدام Java و Aspose.Cells، مع
  الحفاظ على مربعات النص القابلة للتحرير في ملف PPTX الناتج.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to powerpoint
- Aspose.Cells Java
- editable text boxes
- ImageOrPrintOptions
- Workbook save
- PowerPoint PPTX export
language: ar
lastmod: 2026-09-08
og_description: تصدير Excel إلى PowerPoint باستخدام Java و Aspose.Cells. يوضح لك هذا
  الدليل كيفية الحفاظ على نص المخطط قابلًا للتحرير وإنشاء ملف PPTX في دقائق.
og_image_alt: Screenshot of Java code exporting an Excel worksheet to a PowerPoint
  slide
og_title: تصدير إكسل إلى باوربوينت باستخدام جافا – دليل خطوة بخطوة
schemas:
- author: Aspose
  dateModified: '2026-09-08'
  description: Learn how to export Excel to PowerPoint using Java and Aspose.Cells,
    preserving editable text boxes in the PPTX output.
  headline: How to export Excel to PowerPoint with Java
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel
- PowerPoint
title: كيفية تصدير Excel إلى PowerPoint باستخدام Java
url: /ar/java/excel-import-export/how-to-export-excel-to-powerpoint-with-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تصدير Excel إلى PowerPoint باستخدام Java

إذا كنت بحاجة إلى **export Excel to PowerPoint**، فإن هذا الدرس يوضح لك حلاً نظيفًا باستخدام Java. باستخدام **Aspose.Cells Java** يمكنك الحفاظ على تنسيق المخططات وتمكين **editable text boxes** في ملف PPTX المُولد.

تصدير جدول بيانات إلى عرض تقديمي هو طلب شائع عندما تريد إعادة استخدام المخططات المستندة إلى البيانات في شرائح العرض. في هذا الدليل ستتعلم كيفية:

* تحميل ملف Excel موجود يحتوي على مخطط.
* تهيئة **ImageOrPrintOptions** بحيث يبقى مربع النص في الشريحة المُصدَّر قابلاً للتحرير.
* حفظ ورقة العمل كملف **PowerPoint PPTX** باستدعاء طريقة واحدة.
* تشغيل مثال كامل ومستقل يمكنك نسخه إلى مشروعك الخاص.

المتطلبات المسبقة الوحيدة هي بيئة تشغيل Java 8 (أو أحدث) ورخصة صالحة لـ Aspose.Cells for Java. إذا كنت تستخدم نسخة التقييم المجانية، سيحتوي الناتج على علامة مائية، لكن الشيفرة تعمل بنفس الطريقة.

---

## تصدير Excel إلى PowerPoint – إعداد بيئة التطوير

قبل كتابة الكود، تأكد من أن لديك ما يلي:

| العنصر | السبب |
|------|--------|
| **Java Development Kit (JDK) 8+** | مطلوب لتجميع وتشغيل المثال. |
| **Aspose.Cells for Java** library | يوفر الفئات `Workbook` و `ImageOrPrintOptions` و `SaveFormat` المستخدمة في التحويل. |
| **A valid Aspose.Cells license** (optional) | يزيل علامات مائية التقييم ويفتح كامل الوظائف. |
| **An Excel file (`chartSheet.xlsx`)** with at least one chart | ملف Excel المصدر (`chartSheet.xlsx`) الذي يحتوي على مخطط واحد على الأقل. |

أضف ملف JAR الخاص بـ Aspose.Cells إلى مسار الفئات (classpath) في مشروعك. إذا كنت تستخدم Maven، أدرج الاعتماد:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- Use the latest version -->
</dependency>
```

---

## تهيئة ImageOrPrintOptions لمربعات النص القابلة للتحرير

تتحكم الفئة `ImageOrPrintOptions` في كيفية عرض ورقة العمل عند التصدير. ضبط `setExportEditableTextBox(true)` يخبر Aspose.Cells بالحفاظ على عناصر النص داخل المخططات كـ **editable text boxes** في PowerPoint، بدلاً من تحويلها إلى صورة ثابتة.

```java
// Create export options for PowerPoint
ImageOrPrintOptions exportOptions = new ImageOrPrintOptions();
exportOptions.setSaveFormat(SaveFormat.PPTX);          // Target format is PPTX
exportOptions.setExportEditableTextBox(true);        // Keep chart text editable
```

سبب أهمية ذلك: عندما تفتح ملف PPTX لاحقًا في PowerPoint، يمكنك النقر على تسمية المخطط وتعديل محتواها مباشرة، وهو أمر أساسي للعروض التي تحتاج إلى تعديلات فورية.

---

## تحميل دفتر العمل وتصديره كملف PPTX

الآن قم بتحميل ملف Excel، وطبق الخيارات من الخطوة السابقة، واستدعِ `save`. طريقة `Workbook.save` تقبل مسار الإخراج وكائن `ImageOrPrintOptions`، وتتعامل مع التحويل داخليًا.

```java
// Load the workbook that contains the chart
Workbook workbook = new Workbook("YOUR_DIRECTORY/chartSheet.xlsx");

// Export the first worksheet to PowerPoint using the configured options
workbook.save("YOUR_DIRECTORY/output.pptx", exportOptions);
```

**نقاط رئيسية**

* `Workbook` تمثل ملف Excel بالكامل. يمكنك أيضًا اختيار ورقة معينة باستخدام `workbook.getWorksheets().get(0)` إذا كنت تريد تصدير ورقة واحدة فقط.
* طريقة `save` تكتب ملف PPTX يحتوي على شريحة واحدة لكل ورقة عمل بشكل افتراضي.
* إذا كان دفتر العمل يحتوي على عدة أوراق وتحتاج فقط إلى ورقة المخطط، احذف الأوراق غير المرغوب فيها قبل الحفظ أو استخدم `ExportOptions.setOnePagePerSheet(false)` للتحكم في ترقيم الصفحات.

---

## مثال كامل قابل للتنفيذ

فيما يلي برنامج Java بسيط وقابل للتنفيذ بالكامل يوضح التدفق الكامل. استبدل `YOUR_DIRECTORY` بمسار مطلق أو نسبي يشير إلى ملفاتك.

```java
import com.aspose.cells.*;

public class ExcelToPowerPointDemo {
    public static void main(String[] args) {
        try {
            // 1. Load the Excel workbook that holds the chart
            Workbook workbook = new Workbook("YOUR_DIRECTORY/chartSheet.xlsx");

            // 2. Prepare export options for PowerPoint and enable editable text boxes
            ImageOrPrintOptions exportOptions = new ImageOrPrintOptions();
            exportOptions.setSaveFormat(SaveFormat.PPTX);          // Export as PPTX
            exportOptions.setExportEditableTextBox(true);        // Keep text boxes editable

            // 3. Export the worksheet(s) to a PPTX file
            workbook.save("YOUR_DIRECTORY/output.pptx", exportOptions);

            System.out.println("Export completed successfully. Check output.pptx.");
        } catch (Exception e) {
            System.err.println("Error during export: " + e.getMessage());
            e.printStackTrace();
        }
    }
}
```

**الناتج المتوقع**

تشغيل البرنامج يطبع:

```
Export completed successfully. Check output.pptx.
```

عند فتح `output.pptx` في Microsoft PowerPoint، سترى شريحة تعكس مخطط Excel. انقر مزدوجًا على أي تسمية مخطط ويمكنك تعديل النص مباشرة، مما يؤكد أن **editable text boxes** نشطة.

---

## معالجة الاختلافات الشائعة وحالات الحافة

| الحالة | النهج الموصى به |
|-----------|----------------------|
| **عدة أوراق عمل لكن يجب تصدير ورقة المخطط الوحيدة** | استخدم `workbook.getWorksheets().removeAt(index)` لحذف الأوراق غير المرغوب فيها قبل استدعاء `save`، أو اضبط `exportOptions.setOnePagePerSheet(false)` ثم اختر يدويًا الورقة التي تريد عرضها. |
| **ملفات Excel الكبيرة التي تسبب ضغطًا على الذاكرة** | فعّل وضع البث مع `loadOptions.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` عند إنشاء `Workbook`. |
| **لم يتم تعيين الرخصة (نسخة التقييم)** | سيحتوي PPTX المُولد على علامة مائية. أضف `License license = new License(); license.setLicense("Aspose.Cells.lic");` في بداية `main` لإزالتها. |
| **الحاجة لتصدير نطاق محدد فقط** | أنشئ ورقة عمل مؤقتة، وانسخ النطاق المطلوب باستخدام `worksheet.getCells().copyRange(...)`، ثم صدّر تلك الورقة المؤقتة. |
| **توافق نسخة PowerPoint** | Aspose.Cells يولد دائمًا Office Open XML (PPTX) الذي يعمل مع PowerPoint 2007 وما بعده. للحصول على صيغة PPT القديمة، غيّر `SaveFormat.PPT` (مع العلم أن مربعات النص القابلة للتحرير مدعومة فقط في PPTX). |

---

## نصائح احترافية للاستخدام الإنتاجي

* **Batch conversion** – قم بالتكرار عبر دليل يحتوي على ملفات Excel، مع إعادة استخدام كائن `ImageOrPrintOptions` واحد لتقليل عبء إنشاء الكائنات.
* **Performance profiling** – قس الوقت المستغرق بواسطة `workbook.save` للملفات الكبيرة؛ فكر في زيادة حجم الذاكرة المخصصة للـ JVM (`-Xmx2g`) إذا واجهت `OutOfMemoryError`.
* **Custom slide layout** – بعد التصدير، يمكنك تعديل ملف PPTX باستخدام Aspose.Slides for Java لإضافة عناوين، تذييلات، أو تطبيق شريحة رئيسية.

---

## الخلاصة

الآن تعرف كيف **export Excel to PowerPoint** باستخدام Java، مع الحفاظ على دقة المخطط وتمكين **editable text boxes** عبر `ImageOrPrintOptions`. المثال الكامل يوضح تحميل دفتر العمل، تهيئة خيارات التصدير، وحفظ ملف PPTX في ثلاث خطوات مختصرة فقط.

من هنا يمكنك استكشاف المواضيع ذات الصلة مثل **Aspose.Cells Java chart manipulation**، **PowerPoint PPTX export** باستخدام قوالب مخصصة، أو **batch processing multiple spreadsheets**. جرّب قيم `SaveFormat` المختلفة، اجمع هذا النهج مع Aspose.Slides، ودمج سير العمل في خط أنابيب التقارير الخاص بك.

![كود Java لتصدير Excel إلى PowerPoint](/images/export-excel-to-powerpoint.png){: .responsive-img alt="لقطة شاشة لكود Java يصدّر ورقة عمل Excel إلى شريحة PowerPoint"}

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مصدر يتضمن أمثلة شيفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [كيفية إنشاء وتكوين مربعات النص في Excel باستخدام Aspose.Cells Java لتحسين عرض البيانات](/cells/english/java/images-shapes/create-text-boxes-excel-aspose-cells-java/)
- [كيفية تصدير مخططات Excel كـ SVG باستخدام Aspose.Cells Java للرسومات المتجهة القابلة للتوسيع](/cells/english/java/charts-graphs/export-excel-charts-svg-aspose-cells-java/)
- [كيفية تصدير ورقة عمل Excel إلى PNG باستخدام Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-to-png-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}