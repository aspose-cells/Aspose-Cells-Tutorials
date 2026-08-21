---
category: general
date: 2026-08-20
description: تعلم كيفية تعيين منطقة الطباعة في Excel، ثم تصدير Excel إلى PPTX باستخدام
  Aspose.Cells. يشرح هذا الدليل خطوة بخطوة تحويل ورقة العمل إلى PowerPoint وحفظها
  كملف PPTX.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set print area excel
- export excel to pptx
- convert worksheet to powerpoint
- save worksheet as powerpoint
language: ar
lastmod: 2026-08-20
og_description: حدد منطقة الطباعة في Excel ثم صدّر ملف Excel إلى PPTX باستخدام Aspose.Cells.
  اتبع هذا الدليل خطوة بخطوة لتحويل ورقة العمل إلى PowerPoint وحفظها كملف PPTX.
og_image_alt: Screenshot showing Excel print area set and PPTX export using Aspose.Cells
og_title: تحديد منطقة الطباعة في إكسل وتصديرها إلى باوربوينت – دليل كامل
schemas:
- author: Aspose
  dateModified: '2026-08-20'
  description: Learn how to set print area excel, then export excel to pptx with Aspose.Cells.
    This guide walks you through converting a worksheet to PowerPoint and saving it
    as a PPTX.
  headline: How to set print area excel and export to PowerPoint
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel automation
- PowerPoint generation
title: كيفية تحديد منطقة الطباعة في إكسل وتصديرها إلى باوربوينت
url: /ar/java/excel-import-export/how-to-set-print-area-excel-and-export-to-powerpoint/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تعيين منطقة الطباعة في Excel وتصديرها إلى PowerPoint

إذا كنت بحاجة إلى **set print area excel** قبل مشاركة البيانات في عرض شرائح، فإن هذا الدرس يوضح لك بالضبط كيفية القيام بذلك. سترى كيفية تكوين منطقة الطباعة، ثم **export excel to pptx** مع الحفاظ على صناديق النص قابلة للتحرير، بحيث يكون PowerPoint الناتج جاهزًا للمزيد من التعديل.

سنستخدم Aspose.Cells for Java لـ **convert worksheet to PowerPoint** وأخيرًا **save worksheet as PowerPoint** بصيغة PPTX. لا توجد مكتبات إضافية مطلوبة بخلاف Aspose.Cells JAR. بنهاية هذا الدليل يمكنك تشغيل الكود على أي بيئة متوافقة مع Java وإنتاج عرض تقديمي يعكس النطاق المحدد في Excel.

## المتطلبات المسبقة

- Java Development Kit 17 أو أحدث  
- Aspose.Cells for Java (تحميل من الموقع الرسمي لـ Aspose)  
- مصنف Excel يحتوي على أشكال تريد إبقاءها قابلة للتحرير (مثال: `BookWithShapes.xlsx`)  

تأكد من أن Aspose.Cells JAR موجود في مسار الفئة (classpath) الخاص بك:

```bash
javac -cp "aspose-cells-23.12.jar" ExportEditableShapesToPptx.java
java -cp ".:aspose-cells-23.12.jar" ExportEditableShapesToPptx
```

## الخطوة 1: تعيين منطقة الطباعة في Excel باستخدام Aspose.Cells

الخطوة الأولى هي تعريف النطاق الذي سيتم تصديره. ضبط منطقة الطباعة يحد من التحويل إلى الخلايا التي تهمك ويحسن الأداء.

```java
// Load the workbook that contains shapes
Workbook workbook = new Workbook("YOUR_DIRECTORY/BookWithShapes.xlsx");

// Define the print area for the first worksheet (A1:G30)
workbook.getWorksheets().get(0).getPageSetup().setPrintArea("A1:G30");
```

**Why this matters** – طريقة `setPrintArea` تخبر Aspose.Cells أي الخلايا تنتمي إلى الصفحة القابلة للطباعة. عندما تقوم لاحقًا **export excel to pptx**, يتم عرض هذا النطاق فقط، لذا لا تظهر البيانات الزائدة في الشريحة.

### نصيحة احترافية
إذا كنت بحاجة إلى نطاق ديناميكي، يمكنك حساب العنوان برمجيًا:

```java
int lastRow = workbook.getWorksheets().get(0).getCells().getMaxDataRow() + 1;
int lastCol = workbook.getWorksheets().get(0).getCells().getMaxDataColumn() + 1;
String range = String.format("A1:%s%d", CellsHelper.columnIndexToName(lastCol - 1), lastRow);
workbook.getWorksheets().get(0).getPageSetup().setPrintArea(range);
```

## الخطوة 2: تصدير Excel إلى PPTX مع صناديق نص قابلة للتحرير

بعد تعريف منطقة الطباعة، قم بتكوين خيارات التصدير. تمكين `setExportEditableTextBoxes` يحافظ على نص الشكل كحقول قابلة للتحرير في PowerPoint.

```java
// Create export options and enable editable text boxes in the PPTX
ImageOrPrintOptions exportOptions = new ImageOrPrintOptions();
exportOptions.setSaveFormat(SaveFormat.PPTX);
exportOptions.setExportEditableTextBoxes(true);   // keeps text boxes editable
```

**Why this matters** – بشكل افتراضي، تقوم Aspose.Cells بتحويل صناديق النص إلى صورة raster، مما يجعلها جزءًا من الصورة. ضبط `ExportEditableTextBoxes` إلى `true` يحتفظ بأجسام الشكل الأصلية، مما يسمح للمستخدمين بتعديل النص مباشرة في PowerPoint.

## الخطوة 3: تحويل ورقة العمل إلى PowerPoint وحفظ الملف

الآن قم بتنفيذ التحويل الفعلي. طريقة `Workbook.save` تأخذ اسم الملف الهدف والخيارات التي تم إعدادها مسبقًا.

```java
// Export the first worksheet to PPTX using the configured options
workbook.save("YOUR_DIRECTORY/SheetWithEditableShapes.pptx", exportOptions);
```

عند انتهاء الكود، يحتوي `SheetWithEditableShapes.pptx` على شريحة واحدة تعكس منطقة الطباعة المحددة (`A1:G30`). جميع الأشكال، بما في ذلك صناديق النص، تظل قابلة للتحرير.

### النتيجة المتوقعة
افتح ملف PPTX المُولد في Microsoft PowerPoint:

- الشريحة تعرض الخلايا من **A1 إلى G30** تمامًا كما تظهر في Excel.  
- أي أشكال كانت موجودة في ورقة العمل الأصلية تظهر كأشكال PowerPoint.  
- يمكن تحرير النص داخل تلك الأشكال مباشرة في PowerPoint (بدون تحويل إلى صورة raster).

## الخطوة 4: مثال كامل قابل للتنفيذ

فيما يلي البرنامج الكامل. استبدل `YOUR_DIRECTORY` بمسار المجلد الفعلي على جهازك.

```java
import com.aspose.cells.*;

public class ExportEditableShapesToPptx {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the workbook that contains shapes
        Workbook workbook = new Workbook("YOUR_DIRECTORY/BookWithShapes.xlsx");

        // Step 2: Create export options and enable editable text boxes in the PPTX
        ImageOrPrintOptions exportOptions = new ImageOrPrintOptions();
        exportOptions.setSaveFormat(SaveFormat.PPTX);
        exportOptions.setExportEditableTextBoxes(true); // keeps text boxes editable

        // Step 3: Define the print area to limit the exported range
        workbook.getWorksheets().get(0).getPageSetup().setPrintArea("A1:G30");

        // Step 4: Export the first worksheet to PPTX using the configured options
        workbook.save("YOUR_DIRECTORY/SheetWithEditableShapes.pptx", exportOptions);
    }
}
```

شغّل البرنامج كما هو موضح في قسم *المتطلبات المسبقة*. سيتم وضع ملف PowerPoint المُولد في نفس الدليل الذي حددته.

## الأسئلة الشائعة والحالات الخاصة

| السؤال | الجواب |
|----------|--------|
| **هل يمكنني تصدير عدة أوراق عمل؟** | نعم. قم بالتكرار عبر `workbook.getWorksheets()` واستدعِ `save` لكل ورقة، مع إمكانية تغيير اسم ملف الإخراج. |
| **ماذا لو كان مصنف Excel يحتوي على مخططات؟** | يتم عرض المخططات كصور بشكل افتراضي. للحفاظ على إمكانية تحريرها تحتاج إلى تحويلها إلى أشكال PowerPoint يدويًا، وهذا خارج نطاق هذا الدليل. |
| **هل منطقة الطباعة مطلوبة؟** | لا. إذا تخطيت `setPrintArea`، تقوم Aspose.Cells بتصدير النطاق المستخدم بالكامل في ورقة العمل. ضبطها يمنحك تحكمًا دقيقًا. |
| **هل يعمل هذا مع ملفات .xlsx التي تم إنشاؤها بأدوات أخرى؟** | بالطبع. تدعم Aspose.Cells أي مصنف Office Open XML صالح، بغض النظر عن مصدره. |

## الخطوات التالية

- **Save worksheet as PowerPoint** مع تخطيطات شرائح مخصصة: استكشف فئة `Presentation` من Aspose.Slides لدمج الشريحة المصدرة في مجموعة شرائح أكبر.  
- **Export excel to pptx** مع دقات صورة مختلفة: اضبط `exportOptions.setResolution(300)` لإخراج عالي الدقة DPI.  
- **Automate batch conversions**: دمج هذا الكود مع مراقب ملفات لمعالجة عدة ملفات Excel في مجلد.  

من خلال إتقان **set print area excel**, **export excel to pptx**, **convert worksheet to powerpoint**, و **save worksheet as powerpoint**, يمكنك دمج بيانات Excel في عروض الشرائح برمجيًا، مما يبسط عمليات إعداد التقارير ويقلل من العمل اليدوي للنسخ واللصق.

---

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مصدر يتضمن أمثلة شفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [كيفية تعيين منطقة طباعة في Excel باستخدام Aspose.Cells for .NET](/cells/english/net/headers-footers/set-print-area-excel-aspose-cells-net/)
- [تعيين منطقة طباعة Excel Aspose Cells Net](/cells/german/net/headers-footers/set-print-area-excel-aspose-cells-net/)
- [تعيين منطقة طباعة Excel Aspose Cells Net](/cells/french/net/headers-footers/set-print-area-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}