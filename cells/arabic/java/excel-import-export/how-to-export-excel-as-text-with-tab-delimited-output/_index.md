---
category: general
date: 2026-11-22
description: تعلم كيفية تصدير Excel كنص وإنشاء ملف مفصول بعلامات جدولة. يوضح هذا الدليل
  ضبط اقتباس جميع الحقول وحفظ نص الجدول بكفاءة.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel as text
- quote all fields
- create tab-delimited file
- save spreadsheet text
- export spreadsheet tab-delimited
language: ar
lastmod: 2026-11-22
og_description: تصدير Excel كنص وإنشاء ملف مفصول بعلامات التبويب. اتبع هذا الدليل
  خطوة بخطوة لتضمين جميع الحقول وحفظ نص جدول البيانات باستخدام Java.
og_image_alt: Screenshot showing Java code that exports an Excel workbook as a tab‑delimited
  text file
og_title: دليل تصدير إكسل كنص – ملف مفصول بعلامات التبويب
schemas:
- author: Aspose
  dateModified: '2026-11-22'
  description: Learn how to export Excel as text and create a tab‑delimited file.
    This guide shows setting quote all fields and saving spreadsheet text efficiently.
  headline: How to export Excel as text with tab‑delimited output
  type: TechArticle
- description: Learn how to export Excel as text and create a tab‑delimited file.
    This guide shows setting quote all fields and saving spreadsheet text efficiently.
  name: How to export Excel as text with tab‑delimited output
  steps:
  - name: Prepare the workbook and sample data
    text: Creating a workbook gives you something to export. In a real project you
      would load an existing file with `new Workbook("input.xlsx")`; here we generate
      a tiny sheet so the example runs out‑of‑the‑box.
  - name: Configure export options – delimiter, quoting, and output mode
    text: The core of **export spreadsheet tab‑delimited** lies in `ExportTableOptions`.
      You set the delimiter to a tab (`'\t'`) and enable `setQuoteAllFields(true)`
      so every cell is wrapped in double quotes. This eliminates ambiguity when a
      cell itself contains a tab or newline.
  - name: Save the workbook as a tab‑delimited text file
    text: Now you actually **export excel as text**. The `save` method takes the target
      path and the `ExportOptions` you configured.
  type: HowTo
tags:
- export excel as text
- quote all fields
- tab-delimited file
- spreadsheet export
- Java
title: كيفية تصدير Excel كنص مع إخراج مفصول بعلامات تبويب
url: /ar/java/excel-import-export/how-to-export-excel-as-text-with-tab-delimited-output/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تصدير Excel كنص مع إخراج مفصول بعلامات جدولة

إذا كنت بحاجة إلى **export Excel as text**، فإن هذا البرنامج التعليمي يشرح لك العملية الكاملة لإنشاء ملف مفصول بعلامات جدولة من دفتر عمل. سواءً كنت تبني خط أنابيب لترحيل البيانات أو تحتاج إلى تفريغ سريع على نمط CSV للمعالجة اللاحقة، فإن الخطوات أدناه تسمح لك **save spreadsheet text** مع تحكم كامل في الفواصل والاقتباس.

تصدير بيانات الجدول كملف نص عادي غالبًا ما يكون أكثر قابلية للنقل من الحفاظ على تنسيق `.xlsx` الأصلي. في هذا الدليل ستتعلم أيضًا كيفية **quote all fields**، مما يضمن أن القيم التي تحتوي على علامات جدولة أو فواصل أو فواصل أسطر تكون محصورة بأمان.

## ما ستحتاجه

* Java 17 أو أحدث مثبت.  
* مكتبة Aspose.Cells for Java (الكود يستخدم `ExportOptions` و `ExportTableOptions` من هذه المكتبة). يمكنك إضافتها عبر Maven:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version>
</dependency>
```

* بيئة تطوير متكاملة (IDE) أو محرر نصوص بسيط لتجميع وتشغيل برنامج Java.

## تصدير Excel كنص – خطوة بخطوة

الأقسام التالية تقسم المهمة إلى ثلاث خطوات منطقية. كل خطوة تشرح **why** أهميتها، وليس فقط **what** ما يجب كتابته.

### الخطوة 1: إعداد دفتر العمل والبيانات النموذجية

إنشاء دفتر عمل يمنحك شيئًا لتصديره. في مشروع حقيقي، كنت ستحمل ملفًا موجودًا باستخدام `new Workbook("input.xlsx")`؛ هنا نقوم بإنشاء ورقة صغيرة بحيث يعمل المثال مباشرةً.

```java
import com.aspose.cells.*;

public class ExportExcelAsText {
    public static void main(String[] args) throws Exception {
        // Load an existing workbook or create a new one
        Workbook wb = new Workbook();
        Worksheet sheet = wb.getWorksheets().get(0);

        // Populate sample data – this will be part of the exported text
        sheet.getCells().get("A1").setValue("Name");
        sheet.getCells().get("B1").setValue("Age");
        sheet.getCells().get("A2").setValue("Alice");
        sheet.getCells().get("B2").setValue(30);
        sheet.getCells().get("A3").setValue("Bob, Jr."); // contains a comma
        sheet.getCells().get("B3").setValue(25);
```

*Why this step?*  
دفتر العمل هو الكائن المصدر لأي عملية تصدير. بإضافة بعض الصفوف يمكنك التحقق من أن خيار **quote all fields** يحمي الفواصل وغيرها من الأحرف الخاصة فعلاً.

### الخطوة 2: تكوين خيارات التصدير – الفاصل، الاقتباس، ووضع الإخراج

جوهر **export spreadsheet tab‑delimited** يكمن في `ExportTableOptions`. تقوم بتعيين الفاصل إلى علامة جدولة (`'\t'`) وتفعيل `setQuoteAllFields(true)` بحيث يتم تغليف كل خلية بعلامات اقتباس مزدوجة. هذا يزيل الغموض عندما تحتوي الخلية نفسها على علامة جدولة أو سطر جديد.

```java
        // Step 2: Create table export options and configure delimiter and quoting
        ExportTableOptions tableExportOptions = new ExportTableOptions();
        tableExportOptions.setDelimiter('\t');            // Use a tab as the field separator
        tableExportOptions.setQuoteAllFields(true);      // Quote every field for safety

        // Create overall export options and attach the table options
        ExportOptions exportOptions = new ExportOptions();
        exportOptions.setExportTableOptions(tableExportOptions);
        exportOptions.setExportAsString(true);            // Produce plain‑text output
```

*Why this step?*  
- **Delimiter** يحدد كيفية فصل الأعمدة. علامة الجدولة (`\t`) تنشئ **tab‑delimited file** تقبله العديد من أدوات معالجة البيانات.  
- **Quote all fields** يضمن أنه حتى إذا احتوت الخلية على فاصل، يظل النص الناتج قابلًا للتحليل.  
- ضبط `ExportAsString` يخبر Aspose.Cells بإنشاء سلسلة نصية بدلاً من دفتر عمل ثنائي، وهو بالضبط ما تحتاجه لـ **save spreadsheet text**.

### الخطوة 3: حفظ دفتر العمل كملف نص مفصول بعلامات جدولة

الآن تقوم فعليًا بـ **export excel as text**. طريقة `save` تأخذ مسار الهدف و `ExportOptions` التي قمت بتكوينها.

```java
        // Step 3: Save the workbook as a tab‑delimited text file
        wb.save("output/table.txt", exportOptions);
    }
}
```

عند انتهاء البرنامج، ستجد `output/table.txt` يحتوي على:

```
"Name"	"Age"
"Alice"	"30"
"Bob, Jr."	"25"
```

*Why this step?*  
نداء `save` يكتب **tab‑delimited file** إلى القرص، مما يؤدي فعليًا إلى **saving spreadsheet text** بصيغة يمكن فتحها بواسطة Excel أو Notepad أو أي أداة استيراد بيانات تفهم علامات الجدولة.

## كيفية اقتباس جميع الحقول عند تصدير Excel كنص

إذا تجاهلت `setQuoteAllFields(true)`، فإن الخلايا التي تحتوي على علامات جدولة أو فواصل أو فواصل أسطر ستكسر بنية ملف الإخراج. على سبيل المثال، الصف `Bob, Jr.` سيتقسم إلى عمودين، مما يفسد مجموعة البيانات. دائمًا فعّل الاقتباس عندما:

* قد تحتوي بيانات المصدر على فواصل أو علامات جدولة أو فواصل أسطر.  
* يتوقع المحللون اللاحقون ملفات CSV/TSV مقتبسة.  
* تحتاج إلى تصدير حتمي بغض النظر عن محتوى الخلية.

## إنشاء ملف مفصول بعلامات جدولة بدون Aspose.Cells (اختياري)

إذا كنت تفضل حلًا بحتًا بلغة Java بدون مكتبات طرف ثالث، يمكنك التكرار على الصفوف وكتابتها يدويًا:

```java
try (PrintWriter pw = new PrintWriter(new FileWriter("output/manual.txt"))) {
    for (int r = 0; r < sheet.getCells().getMaxDataRow() + 1; r++) {
        List<String> rowValues = new ArrayList<>();
        for (int c = 0; c < sheet.getCells().getMaxDataColumn() + 1; c++) {
            String value = sheet.getCells().get(r, c).getStringValue();
            // Quote all fields manually
            rowValues.add('"' + value.replace("\"", "\"\"") + '"');
        }
        pw.println(String.join("\t", rowValues));
    }
}
```

هذا المقتطف يوضح نفس منطق **export spreadsheet tab‑delimited**: فاصل جدولة، اقتباس كل حقل، وكتابة النتيجة كنص عادي. ومع ذلك، استخدام Aspose.Cells يبسط التعامل مع دفاتر عمل كبيرة، يحافظ على التنسيق، ويقلل من الشيفرة المتكررة.

## المشكلات الشائعة ونصائح الخبراء

| Issue | Why it happens | Fix |
|-------|----------------|-----|
| **Missing tabs in output** | تم ترك الفاصل على الفاصلة الافتراضية. | استدعِ `setDelimiter('\t')` صراحةً. |
| **Unquoted commas break columns** | `quoteAllFields` غير مفعّل. | استخدم `setQuoteAllFields(true)` أو اقتبس يدويًا. |
| **File not created** | دليل الإخراج غير موجود. | تأكد من وجود مجلد `output/` أو استخدم `Files.createDirectories`. |
| **Encoding problems** | قد يتسبب الترميز الافتراضي للمنصة في إفساد الأحرف غير ASCII. | مرّر `ExportOptions.setEncoding(Encoding.getUTF8())` إذا لزم الأمر. |

## اختبار النتيجة

بعد تشغيل البرنامج:

1. افتح `output/table.txt` في محرر نص عادي. يجب أن ترى كل قيمة محاطة بعلامات اقتباس مزدوجة والأعمدة مفصولة بحرف جدولة واحد.  
2. استورد الملف إلى Excel (`Data → From Text/CSV`). اختر **Tab** كفاصل؛ سيقوم Excel بوضع كل قيمة مقتبسة في خلية خاصة بها بشكل صحيح.  
3. تحقق من أن الأحرف الخاصة (الفواصل، فواصل الأسطر

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة شاملة من الشيفرة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [how to export excel – Tab‑Delimited Text Guide](/cells/english/net/converting-excel-files-to-other-formats/how-to-export-excel-tab-delimited-text-guide/)
- [Save Excel as Text File with Custom Separator using Aspose.Cells](/cells/english/net/workbook-operations/save-excel-text-custom-separator-aspose-cells-net/)
- [How to save Excel as text with Aspose.Cells – step‑by‑step guide](/cells/english/net/converting-excel-files-to-other-formats/how-to-save-excel-as-text-with-aspose-cells-step-by-step-gui/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}