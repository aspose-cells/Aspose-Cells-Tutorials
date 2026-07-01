---
category: general
date: 2026-06-30
description: كيفية تصدير جدول محوري في Java وحفظ النطاق كصورة PNG باستخدام Aspose.Cells.
  دليل خطوة بخطوة مع الكود الكامل والنصائح.
draft: false
keywords:
- how to export pivot
- save range as png
- Aspose.Cells export image
- Java pivot table image
- workbook to PNG
language: ar
og_description: تعرّف على كيفية تصدير جدول محوري في جافا وحفظ النطاق كملف PNG. مثال
  كامل، شروحات، ونصائح لأفضل الممارسات.
og_title: كيفية تصدير جدول Pivot كملف PNG – دليل جافا
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: How to export pivot table in Java and save range as PNG using Aspose.Cells.
    Step‑by‑step guide with full code and tips.
  headline: How to Export Pivot Table as PNG – Complete Java Guide
  type: TechArticle
tags:
- Aspose.Cells
- Java
- PivotTable
- ImageExport
title: كيفية تصدير جدول محوري كصورة PNG – دليل جافا الكامل
url: /ar/java/excel-pivot-tables/how-to-export-pivot-table-as-png-complete-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تصدير جدول محوري كصورة PNG – دليل Java كامل

هل تساءلت يومًا **كيف تصدر بيانات الجدول المحوري** من مصنف Excel دون فقدان تنسيقه؟ ربما تحتاج إلى مخطط الجدول المحوري لتقرير، مرفق بريد إلكتروني، أو صورة مصغرة سريعة على لوحة تحكم. في هذا الدرس سنستعرض الخطوات الدقيقة **لحفظ النطاق كصورة PNG** باستخدام Aspose.Cells for Java، وسنشرح لماذا كل سطر مهم. لا إطالة، مجرد حل قابل للتنفيذ يمكنك نسخه‑ولصقه اليوم.

ستنتهي من هذا الدليل ببرنامج Java مستقل يقوم بتحميل ملف `.xlsx`، يلتقط أول جدول محوري، ويكتبها مباشرةً إلى صورة PNG مع الحفاظ على النمط البصري للجدول المحوري. جاهز؟ لنبدأ.

---

## ما الذي ستحتاجه

- **Java 8+** (الكود يُترجم مع JDK 8 وما بعده)
- **Aspose.Cells for Java** library – version 23.10 أو أحدث (قم بتنزيله من الموقع الرسمي أو استخدم Maven)
- مصنف Excel (`pt.xlsx`) يحتوي على جدول محوري واحد على الأقل
- مجلد لديك فيه صلاحيات القراءة/الكتابة (سنسميه `YOUR_DIRECTORY`)

إذا كان أي من ذلك غير مألوف لك، لا تقلق. تثبيت تبعية Maven سهل كإضافة سطر واحد إلى `pom.xml`. إليك المقتطف:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
    <classifier>jdk17</classifier>
</dependency>
```

استبدل `jdk17` بالمُصنِّف المناسب لإصدار JDK الخاص بك. هذا كل شيء—مشروعك جاهز للتعامل مع ملفات Excel.

## الخطوة 1 – تحميل المصنف الذي يحتوي على الجدول المحوري

أول شيء علينا القيام به هو فتح ملف Excel. Aspose.Cells يج abstracts نظام الملفات بحيث يمكنك العمل مع الملفات المحلية، أو التدفقات، أو حتى التخزين السحابي. في هذا المثال سنبقي الأمور بسيطة ونقرأ من القرص.

```java
import com.aspose.cells.*;

public class ExportPivotAsPng {
    public static void main(String[] args) throws Exception {
        // Load the workbook that holds the pivot table
        Workbook workbook = new Workbook("YOUR_DIRECTORY/pt.xlsx");
```

> **لماذا هذا مهم:** كائن `Workbook` هو البوابة إلى كل ورقة، جدول، مخطط، وجدول محوري في الملف. إذا تعذر فتح الملف، يتوقف باقي العملية، لذا معالجة `Exception` مبكرًا توفر عليك وقت التصحيح.

## الخطوة 2 – الوصول إلى الورقة الأولى

معظم المصنفات لديها ورقة افتراضية حيث يقع الجدول المحوري. سنأخذ الورقة الأولى (الفهرس 0). إذا كان جدولك المحوري موجودًا في ورقة مختلفة، فقط غير الفهرس أو استخدم `getSheetByName`.

```java
        // Get the first worksheet (index 0)
        Worksheet worksheet = workbook.getWorksheets().get(0);
```

> **نصيحة:** استخدم `worksheet.getName()` لطباعة اسم الورقة إذا لم تكن متأكدًا من مكان وجود الجدول المحوري. هذا الفحص الصغير يمكن أن يمنع مفاجآت “null pointer” لاحقًا.

## الخطوة 3 – استرجاع نطاق أول جدول محوري

يمكن للجدول المحوري أن يمتد عبر عدة صفوف وأعمدة، لكن Aspose.Cells يتيح لك جلب نطاقه الدقيق باستدعاء واحد. هذا النطاق هو ما سنحول إلى صورة.

```java
        // Retrieve the range of the first pivot table on the worksheet
        PivotTable pivotTable = worksheet.getPivotTables().get(0);
        Range pivotRange = pivotTable.getPivotTableRange();
```

> **لماذا نستخدم `getPivotTableRange()`:** إنه يُعيد كتلة الخلايا الدقيقة التي يشغلها الجدول المحوري، بما في ذلك العناوين والمجاميع الكلية. تصدير الورقة بأكملها سيُخرج الكثير من البيانات غير المرتبطة، بينما تصدير الجدول المحوري فقط يحافظ على صورة PNG نظيفة ومركزة.

## الخطوة 4 – ضبط خيارات الصورة للحفاظ على نمط الجدول المحوري

بشكل افتراضي، قد تقوم Aspose.Cells بعرض الجدول المحوري دون تنسيقه المدمج. للحفاظ على المظهر (التظليل، الخطوط، الحدود) نُفعّل `RenderPivotTableStyle`.

```java
        // Set image options to keep the pivot’s visual style
        ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
        imgOptions.setRenderPivotTableStyle(true);   // critical for preserving style
```

> **حالة خاصة:** إذا كنت تصدر جدولًا محوريًا يستخدم سمات مخصصة، قد تحتاج أيضًا إلى ضبط `setRenderGridLines(true)` للاحتفاظ بخطوط الشبكة. جرّب هذه الإعدادات حتى يتطابق الناتج مع توقعاتك.

## الخطوة 5 – تصدير نطاق الجدول المحوري كملف PNG

الآن لحظة الحقيقة: نكتب النطاق إلى ملف PNG. طريقة `toImage` تتولى العمل الشاق، حيث تحول الخلايا إلى بكسلات في الخلفية.

```java
        // Export the pivot range to a PNG image
        String outputPath = "YOUR_DIRECTORY/pivot.png";
        pivotRange.toImage(outputPath, imgOptions);

        System.out.println("Pivot table exported successfully to " + outputPath);
    }
}
```

> **النتيجة التي سترىها:** صورة `pivot.png` واضحة تبدو تمامًا كالجدول المحوري في Excel، مع الشرائح، التنسيق الشرطي، والمجاميع. افتحها بأي عارض صور للتحقق.

## اختياري – تصدير جداول محورية متعددة أو مناطق محددة

إذا كان مصنفك يحتوي على عدة جداول محورية، يمكنك التكرار عليها:

```java
        for (int i = 0; i < worksheet.getPivotTables().getCount(); i++) {
            PivotTable pt = worksheet.getPivotTables().get(i);
            Range rng = pt.getPivotTableRange();
            String fileName = "YOUR_DIRECTORY/pivot_" + i + ".png";
            rng.toImage(fileName, imgOptions);
        }
```

> **متى تستخدم هذا:** إنشاء صور مصغرة لبوابة تقارير، أو أرشفة كل جدول محوري في نموذج مالي. منطق `save range as png` نفسه يُطبق—فقط كرره داخل حلقة.

## المشكلات الشائعة & نصائح احترافية

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **صورة فارغة** | `RenderPivotTableStyle` تركت `false` أو الجدول المحوري مخفي. | تأكد من `setRenderPivotTableStyle(true)` وأن الجدول المحوري ليس مُفلترًا لإخفاء جميع الصفوف. |
| **خطوط مشوهة** | قيمة DPI الافتراضية 96، قد تبدو صغيرة على الشاشات عالية الدقة. | استدعِ `imgOptions.setResolution(150);` لزيادة DPI. |
| **الملف غير موجود** | مسار `YOUR_DIRECTORY` غير صحيح أو نقص في صلاحيات الكتابة. | استخدم `new File("YOUR_DIRECTORY").mkdirs();` قبل التصدير. |
| **نفاد الذاكرة للجداول المحورية الضخمة** | النطاقات الكبيرة تُنتج صورًا نقطية ضخمة. | صدّر منطقة أصغر (`pivotRange.setFirstRow`, `setLastRow`) أو زد حجم الذاكرة المخصصة للـ JVM (`-Xmx2g`). |

## مثال كامل جاهز للتنفيذ (نسخ‑لصق)

```java
import com.aspose.cells.*;

public class ExportPivotAsPng {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/pt.xlsx");

        // 2️⃣ Access the first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // 3️⃣ Get the first pivot table's range
        PivotTable pivotTable = worksheet.getPivotTables().get(0);
        Range pivotRange = pivotTable.getPivotTableRange();

        // 4️⃣ Prepare image options – keep style, set DPI if needed
        ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
        imgOptions.setRenderPivotTableStyle(true);
        imgOptions.setResolution(150);           // optional: sharper image

        // 5️⃣ Export to PNG
        String outPath = "YOUR_DIRECTORY/pivot.png";
        pivotRange.toImage(outPath, imgOptions);

        System.out.println("✅ Pivot exported! Check: " + outPath);
    }
}
```

شغّل الفئة، وستجد `pivot.png` في المكان الذي حددته بـ `YOUR_DIRECTORY`. افتحه—بوم، لقد **حفظت النطاق كصورة PNG** دون مغادرة Excel.

## الخاتمة

لقد غطينا **كيفية تصدير بيانات الجدول المحوري** من مصنف Excel باستخدام Java، وأظهرنا لك بالضبط كيف **تحفظ النطاق كصورة PNG** مع الحفاظ على التنسيق. العملية بسيطة: تحميل، تحديد الموقع، الحصول على النطاق، ضبط خيارات الصورة، وكتابة الملف. باتباع الخطوات أعلاه تتجنب المشكلات الشائعة مثل الصور الفارغة أو المخرجات منخفضة الدقة.

ما التالي؟ جرّب إضافة علامات مائية، دمج صور جداول محورية متعددة في PDF، أو أتمتة كامل خط السير في خدمة ويب. المفاهيم نفسها—`Workbook`، `PivotTable`، `ImageOrPrintOptions`—تنطبق على تلك السيناريوهات، لذا أنت الآن مجهز لاستكشاف المزيد.

إذا واجهت مشكلة، تحقق مرة أخرى من مسارات الملفات، تأكد من أنك تستخدم أحدث نسخة من Aspose.Cells، وتذكر النصائح الاحترافية في الجدول. برمجة سعيدة، ولتكن صور PNG الخاصة بك دائمًا واضحة!

![مثال على تصدير الجدول المحوري](pivot_export_example.png "مثال على تصدير الجدول المحوري – تصدير PNG باستخدام Java Aspose.Cells")

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [كيفية تصدير ورقة عمل Excel إلى PNG باستخدام Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-to-png-aspose-cells-java/)
- [تصدير مصنف Excel كصورة باستخدام Aspose.Cells for Java: دليل خطوة بخطوة](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)
- [كيفية إنشاء جداول محورية في Excel باستخدام Aspose.Cells for Java: دليل شامل](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}