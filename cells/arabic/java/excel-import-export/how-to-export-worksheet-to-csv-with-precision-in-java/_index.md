---
category: general
date: 2026-09-27
description: تصدير ورقة العمل إلى CSV في Java باستخدام Aspose.Cells وتعيين الدقة إلى
  5 أرقام معنوية – دليل كامل خطوة بخطوة.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export worksheet to csv
- save workbook as csv
- how to set precision
- save excel as csv
- export excel to csv
language: ar
lastmod: 2026-09-27
og_description: تصدير ورقة العمل إلى CSV في جافا باستخدام Aspose.Cells، تعلّم كيفية
  ضبط الدقة وحفظ المصنف كملف CSV في بضع خطوات فقط.
og_image_alt: Screenshot showing Java code that exports worksheet to CSV with precision
og_title: تصدير ورقة العمل إلى CSV بدقة في جافا – دليل كامل
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Export worksheet to CSV in Java using Aspose.Cells and set precision
    to 5 significant digits – a complete step‑by‑step guide.
  headline: How to export worksheet to CSV with precision in Java
  type: TechArticle
- description: Export worksheet to CSV in Java using Aspose.Cells and set precision
    to 5 significant digits – a complete step‑by‑step guide.
  name: How to export worksheet to CSV with precision in Java
  steps:
  - name: Exporting a specific worksheet
    text: 'If your workbook has multiple sheets and you only want to export one, use
      the `Worksheet` object directly:'
  - name: Exporting without losing leading zeros
    text: 'CSV treats all fields as text, but some parsers may strip leading zeros.
      To preserve them, wrap the value in double quotes:'
  - name: Using a different delimiter
    text: 'If you prefer semicolons instead of commas (common in European locales),
      set the delimiter:'
  - name: Handling large files
    text: 'For workbooks exceeding several hundred megabytes, consider streaming the
      export:'
  - name: Next steps
    text: '* Explore additional `ExportTableOptions` properties such as `setEncoding`,
      `setQuoteAllFields`, and `setSeparator` to fine‑tune your CSV output. * Combine
      the export with Java’s `java.nio.file` APIs to automate batch processing of
      multiple Excel files. * Dive into Aspose.Cells’ **export excel to CS'
  type: HowTo
tags:
- Aspose.Cells
- Java
- CSV export
- Excel automation
title: كيفية تصدير ورقة العمل إلى CSV بدقة في جافا
url: /ar/java/excel-import-export/how-to-export-worksheet-to-csv-with-precision-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تصدير ورقة العمل إلى CSV مع الدقة في Java

إذا كنت بحاجة إلى **export worksheet to CSV** مع التحكم في عدد الأرقام ذات الدلالة، فإن هذا الدليل يوضح لك بالضبط كيفية القيام بذلك باستخدام Aspose.Cells for Java. ستتعلم كيفية تحميل ملف Excel، ضبط الدقة المطلوبة، و **save workbook as CSV** في بضع خطوات بسيطة.

تصدير البيانات إلى CSV هو طلب شائع عند دمج تقارير Excel مع أنظمة أخرى، ويمكن أن يمنع الحفاظ على الدقة العددية الأخطاء في الحسابات اللاحقة. بنهاية هذا البرنامج التعليمي ستكون قادرًا على **save Excel as CSV** بدقة مخصصة، وسترى أيضًا كيف يعمل النهج نفسه في سيناريوهات **export excel to CSV** العامة.

## المتطلبات المسبقة

* Java Development Kit (JDK) 8 أو أحدث مثبت.
* Maven أو Gradle لإدارة التبعيات (سنستخدم Maven في المثال).
* ترخيص Aspose.Cells for Java (التقييم المجاني يكفي للاختبار).
* ملف Excel تجريبي (`Numbers.xlsx`) يحتوي على الأرقام التي تريد تصديرها.

## الخطوة 1: إضافة Aspose.Cells إلى مشروعك

أضف تبعية Aspose.Cells Maven إلى ملف `pom.xml` الخاص بك. هذا يمنحك الوصول إلى الفئات `Workbook` و `ExportTableOptions` و `SaveFormat` اللازمة للتصدير.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest version -->
</dependency>
```

*لماذا هذه الخطوة مهمة*: بدون المكتبة لا يمكنك معالجة ملفات Excel برمجيًا. يضمن استخدام Maven تنزيل ملفات JAR الصحيحة وتحديثها باستمرار.

## الخطوة 2: تحميل المصنف الذي يحتوي على الأرقام

أنشئ كائن `Workbook` يشير إلى ملف Excel المصدر الخاص بك. هذه الخطوة تُعد ورقة العمل للتصدير.

```java
import com.aspose.cells.*;

public class SignificantDigitsExport {
    public static void main(String[] args) throws Exception {
        // Load the workbook containing the numbers
        Workbook workbook = new Workbook("YOUR_DIRECTORY/Numbers.xlsx");
```

*شرح*: تمثل فئة `Workbook` ملف Excel بالكامل. تحميله مرة واحدة يتيح لك إعادة استخدام نفس الكائن لعمليات تصدير متعددة، مثل **save workbook as CSV** بإعدادات مختلفة.

## الخطوة 3: تكوين خيارات التصدير لتحديد الدقة

تتيح لك Aspose.Cells تحديد عدد الأرقام ذات الدلالة عبر `ExportTableOptions`. ضبط هذا بشكل صحيح يُنفّذ متطلب **how to set precision**.

```java
        // Create export options and limit the output to 5 significant digits
        ExportTableOptions exportOptions = new ExportTableOptions();
        exportOptions.setSignificantDigits(5); // keep only 5 significant digits
```

*لماذا هذا مهم*: ملفات CSV تخزن الأرقام كنص عادي. إذا كانت خلايا Excel الأصلية تحتوي على أعداد كبيرة من الأرقام العشرية، قد يصبح ملف CSV غير عملي. من خلال استدعاء `setSignificantDigits`، تضمن أن كل قيمة عددية تُقرب إلى الدقة المحددة قبل كتابتها إلى الملف.

## الخطوة 4: تصدير بيانات ورقة العمل إلى CSV باستخدام الخيارات المُكوَّنة

الآن استدعِ `Workbook.save` مع تعداد `SaveFormat.CSV` ومرّر `exportOptions`. هذا يُجري عملية **export excel to CSV** الفعلية.

```java
        // Export the worksheet data to CSV using the configured options
        workbook.save("YOUR_DIRECTORY/Numbers_SigDigits.csv",
                      SaveFormat.CSV,
                      exportOptions);
    }
}
```

*ما يحدث خلف الكواليس*: تقوم Aspose.Cells بالتكرار على كل خلية، وتطبق قاعدة الدقة، وتكتب النص الناتج إلى تدفق CSV. ملف الإخراج (`Numbers_SigDigits.csv`) يُحفظ في نفس الدليل الذي حددته.

## النتيجة المتوقعة

افترض أن `Numbers.xlsx` يحتوي على القيم التالية في العمود **A**:

| A          |
|------------|
| 123.456789 |
| 0.00123456 |
| 98765.4321 |

بعد تشغيل الكود مع `setSignificantDigits(5)`, سيحتوي `Numbers_SigDigits.csv` على:

```
123.46
0.0012346
98765
```

لاحظ كيف تم تقريب كل رقم إلى خمسة أرقام ذات دلالة، مطابقةً للدقة التي حددتها.

## الخطوة 5: التحقق من ملف CSV

افتح ملف CSV المُولد باستخدام محرر نصوص أو استورده إلى تطبيق آخر (مثل قاعدة بيانات أو أداة تحليل بيانات) لتأكيد ما يلي:

1. تم تنسيق الملف بشكل صحيح (قيم مفصولة بفواصل).
2. القيم العددية تحترم دقة 5 أرقام.
3. لا تظهر علامات اقتباس إضافية أو أحرف هروب ما لم تتطلب البيانات الأصلية ذلك.

إذا كنت بحاجة إلى دقة مختلفة، ما عليك سوى تغيير الوسيط الممرَّر إلى `setSignificantDigits`.

## تنوعات شائعة وحالات حافة

### تصدير ورقة عمل محددة

إذا كان المصنف يحتوي على عدة أوراق وتريد تصدير واحدة فقط، استخدم كائن `Worksheet` مباشرة:

```java
Worksheet sheet = workbook.getWorksheets().get(0); // first sheet
sheet.getCells().exportTableOptions(exportOptions);
sheet.getCells().exportCsv("YOUR_DIRECTORY/Sheet1_SigDigits.csv", exportOptions);
```

### تصدير دون فقدان الأصفار البادئة

يتعامل CSV مع جميع الحقول كنص، لكن بعض المحللات قد تُزيل الأصفار البادئة. للحفاظ عليها، غلف القيمة بعلامتي اقتباس مزدوجتين:

```java
exportOptions.setQuoteAllFields(true);
```

### استخدام فاصل مختلف

إذا كنت تفضّل الفواصل المنقوطة بدلاً من الفواصل (شائع في المناطق الأوروبية)، عيّن الفاصل:

```java
exportOptions.setSeparator(';');
```

### معالجة ملفات كبيرة

للمصنفات التي تتجاوز عدة مئات من الميجابايت، فكر في تصدير تدفقي:

```java
Workbook workbook = new Workbook("largeFile.xlsx", new LoadOptions(LoadFormat.XLSX));
workbook.save("largeFile.csv", SaveFormat.CSV, exportOptions);
```

تقوم Aspose.Cells بمعالجة الملف على دفعات، مما يقلل من استهلاك الذاكرة.

## نصائح احترافية

* **License early** – سجِّل ترخيص Aspose.Cells قبل إنشاء أول `Workbook` لتجنب علامة التقييم.
* **Reuse ExportTableOptions** – إذا كنت بحاجة لتصدير عدة أوراق عمل بنفس الدقة، أنشئ كائن `ExportTableOptions` واحد وأعد استخدامه.
* **Validate numeric columns** – بعد التصدير، شغِّل سكريبت سريع لتأكيد أن عدد الأرقام يطابق توقعك، خاصةً عند التعامل مع الصيغة العلمية.

## الخلاصة

أصبح لديك الآن حل كامل وقابل للتنفيذ لـ **export worksheet to CSV** في Java، مع تحكم كامل في الدقة العددية. من خلال تحميل المصنف، تكوين `ExportTableOptions`، واستدعاء `save` مع `SaveFormat.CSV`، يمكنك **save workbook as CSV** مع تطبيق قاعدة **how to set precision** التي تحتاجها. يعمل هذا النهج لأي مهمة **save excel as CSV** ويمكن توسيعه لتلبية متطلبات تنسيق CSV أخرى.

### الخطوات التالية

* استكشف خصائص `ExportTableOptions` الإضافية مثل `setEncoding` و `setQuoteAllFields` و `setSeparator` لضبط مخرجات CSV بدقة.
* اجمع عملية التصدير مع واجهات برمجة تطبيقات `java.nio.file` في Java لأتمتة معالجة دفعات من ملفات Excel المتعددة.
* تعمق في وثائق Aspose.Cells الخاصة بـ **export excel to CSV** للحصول على سيناريوهات متقدمة مثل تجميع متعدد الأوراق أو الحفاظ على تنسيق الشرط.

برمجة سعيدة، واستمتع بتصدير CSV بدقة مُتحكم فيها!

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مصدر يتضمن أمثلة شاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [كيفية تحميل وحفظ Excel كـ CSV باستخدام Aspose.Cells for Java: دليل شامل](/cells/english/java/workbook-operations/aspose-cells-java-load-save-excel-csv/)
- [كيفية تصدير CSV باستخدام Java – ضبط الأرقام ذات الدلالة وتصدير نطاق إلى CSV](/cells/english/java/excel-import-export/how-to-export-csv-with-java-set-significant-digits-export-ra/)
- [تقليم وحفظ ملفات Excel كـ CSV باستخدام Aspose.Cells في Java](/cells/english/java/workbook-operations/excel-aspose-cells-java-trim-save-csv/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}