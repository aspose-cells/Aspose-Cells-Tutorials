---
category: general
date: 2026-07-20
description: تطبيق تنسيق الأرقام في إكسل باستخدام جافا و Aspose.Cells. تعلم كيفية
  تطبيق نمط العملة في إكسل، إنشاء دفتر عمل إكسل بجافا، واستيراد جدول البيانات إلى
  إكسل بكفاءة.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- apply number format excel
- apply currency style excel
- create excel workbook java
- import datatable to excel
language: ar
lastmod: 2026-07-20
og_description: تطبيق تنسيق الأرقام في إكسل باستخدام جافا. يوضح لك هذا الدليل كيفية
  تطبيق نمط العملة في إكسل، إنشاء دفتر عمل إكسل بجافا، واستيراد جدول البيانات إلى
  إكسل خطوة بخطوة.
og_image_alt: Screenshot of an Excel workbook where apply number format excel has
  been applied to a currency column
og_title: تطبيق تنسيق الأرقام في Excel باستخدام Java – دليل كامل لـ Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-07-20'
  description: Apply number format excel using Java and Aspose.Cells. Learn how to
    apply currency style excel, create excel workbook java, and import datatable to
    excel efficiently.
  headline: Apply Number Format Excel in Java – Complete Aspose.Cells Guide
  type: TechArticle
- questions:
  - answer: Absolutely. Open the workbook with `new Workbook("Existing.xlsx")`, fetch
      the target worksheet, and follow steps 3‑5 to apply the style array to new data.
    question: Can I apply the number format to an existing workbook?
  - answer: Use a different built‑in number index (`14` for short date, `22` for long
      date) or a custom format like `yyyy‑mm‑dd`. The workflow stays the same.
    question: What if I need to format dates instead of currency?
  - answer: 'Yes. Just change the file extension in `workbook.save("MyFile.xls")`.
      Aspose will automatically switch to the binary format. ## Wrap‑Up – What We
      Achieved We have **applied number format excel** to a column of monetary values,
      demonstrated how to **apply currency style excel**, shown the simplest wa'
    question: Does this work with older Excel versions (.xls)?
  type: FAQPage
tags:
- Aspose.Cells
- Java
- Excel Automation
title: تطبيق تنسيق الأرقام في Excel باستخدام Java – دليل Aspose.Cells الكامل
url: /ar/java/formatting/apply-number-format-excel-in-java-complete-aspose-cells-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تطبيق تنسيق الأرقام في Excel باستخدام Java – دليل Aspose.Cells الكامل

هل تساءلت يومًا كيف **تطبيق تنسيق الأرقام في Excel** مباشرة من كود Java؟ ربما تقوم بإعداد تقارير مالية أو تحتاج إلى طريقة سريعة لتنسيق عمود من القيم دون فتح Excel يدويًا. الخبر السار؟ باستخدام Aspose.Cells يمكنك فعل ذلك في بضع أسطر، وستتعلم أيضًا كيف **تطبيق تنسيق العملة في Excel**، **إنشاء مصنف Excel باستخدام Java**، و**استيراد جدول بيانات إلى Excel** كل ذلك في روتين واحد منظم.

في هذا الدرس سنستعرض مثالًا واقعيًا: قائمة من القيم المخزنة في `List<Map<String,Object>>` في Java تُستورد إلى مصنف جديد، العمود الأول يحصل على تنسيق عملة مدمج، ثم يُحفظ الملف جاهزًا للتوزيع. هل أنت مستعد لرؤية مدى السهولة؟ لنبدأ.

## المتطلبات المسبقة – ما ستحتاجه

قبل أن نبدأ، تأكد من وجود ما يلي:

- **Java Development Kit (JDK) 8+** – الكود يعمل على أي JDK حديث.
- مكتبة **Aspose.Cells for Java** (حزمة Maven `com.aspose:aspose-cells`) – هذه هي المحرك الذي يتيح لنا تعديل ملفات Excel دون الحاجة إلى تثبيت Office.
- **IDE مفضلة** (IntelliJ IDEA، Eclipse، VS Code…) – أي محرر سيؤدي المهمة، لكن الـ IDE يسرّع عملية التصحيح.
- إلمام أساسي بـ **مجموعات Java** – سنستخدم `List` من `Map` لمحاكاة DataTable.

هذا كل شيء. لا خدمات خارجية، لا تثبيت Excel، فقط Java صافية.

## الخطوة 1: إنشاء مصنف Excel باستخدام Java – إنشاء كائن Workbook

أول شيء نحتاجه هو كائن المصنف. فكر فيه كقماش فارغ سيحمل كل شيء.

```java
// Step 1: Create a new workbook instance
Workbook workbook = new Workbook(); // creates an in‑memory Excel file
```

لماذا ننشئ المصنف أولًا؟ Aspose.Cells يعمل بالكامل في الذاكرة، لذا يمكنك إضافة أوراق، أنماط، وبيانات قبل لمس القرص. هذا الأسلوب سريع ويحافظ على قابلية اختبار الكود.

## الخطوة 2: تحضير البيانات – استيراد جدول بيانات إلى Excel باستخدام قائمة من الخرائط

في العديد من التطبيقات المؤسسية تأتي البيانات من قواعد البيانات على شكل جداول. هنا نحاكي ذلك باستخدام `List<Map<String,Object>>`. كل خريطة تمثل صفًا، والمفتاح `"Amount"` يربط بقيمة رقمية.

```java
// Step 2: Build a DataTable‑like structure (list of maps)
List<Map<String, Object>> dataRows = new ArrayList<>();

// Row 1
dataRows.add(new HashMap<>() {{
    put("Amount", 1234.56);
}});
// Row 2
dataRows.add(new HashMap<>() {{
    put("Amount", 7890.12);
}});
```

قد تتساءل، “لماذا لا أستخدم `ResultSet` أو POJOs؟” طريقة `importDataTable` تقبل أي مجموعة تتصرف كجدول بيانات، وقائمة الخرائط هي أبسط طريقة لتوضيح الفكرة دون إضافة تبعيات إضافية.

## الخطوة 3: تعريف تنسيق الرقم – تطبيق تنسيق العملة في Excel

الآن يأتي قلب الدرس: **تطبيق تنسيق الأرقام في Excel**. Aspose.Cells يأتي مع تنسيقات أرقام مدمجة؛ تنسيق العملة هو الفهرس 5. نأخذ النمط الافتراضي من الورقة الأولى، نعدل تنسيق الرقم، ونخزنه للاستخدام لاحقًا.

```java
// Step 3: Get the default style and set a currency number format
Style currencyStyle = workbook.getWorksheets().get(0).getCells().getDefaultStyle();
currencyStyle.setNumber(5); // 5 = built‑in currency format ($#,##0.00)
```

لماذا نستخدم النمط الافتراضي كأساس؟ لأنه يحتوي بالفعل على الخط الافتراضي للمصنف، والمحاذاة، وإعدادات أخرى، لذا تحتاج فقط لتغيير ما يهمك—في هذه الحالة تنسيق الرقم. إذا احتجت تنسيقًا مخصصًا (مثلاً “€#,##0.00”) يمكنك استدعاء `currencyStyle.setCustom("#,##0.00 €")` بدلاً من ذلك.

## الخطوة 4: إعداد خيارات الاستيراد – ربط مصفوفة الأنماط

Aspose.Cells يسمح لك بتمرير مصفوفة من كائنات `Style` تتطابق مع الأعمدة المستوردة. بما أن بياناتنا تحتوي على عمود واحد فقط، نوفر مصفوفة ذات عنصر واحد تحتوي على نمط العملة.

```java
// Step 4: Configure import options with the style array
ImportTableOptions importOptions = new ImportTableOptions();
importOptions.setStyleArray(new Style[] { currencyStyle });
```

إذا احتجت يومًا لتنسيق أعمدة متعددة بشكل مختلف، فقط وسّع المصفوفة: `new Style[] { styleForCol1, styleForCol2, … }`. ترتيب الأنماط يطابق ترتيب الأعمدة في البيانات المصدر.

## الخطوة 5: استيراد البيانات – جلب جدول البيانات إلى الورقة

مع المصنف جاهزًا، والبيانات محضرة، والأنماط معرفة، نأتي أخيرًا إلى **استيراد جدول بيانات إلى Excel**. نبدأ من الخلية `A1`، نضمّن رؤوس الأعمدة (`true`)، ونعطي `ImportTableOptions`.

```java
// Step 5: Perform the import
Worksheet worksheet = workbook.getWorksheets().get(0);
worksheet.getCells().importDataTable(dataRows, true, "A1", importOptions);
```

لاحظ العلامة `true`—Aspose.Cells سيولد تلقائيًا صفًا للرأس بناءً على مفاتيح الخريطة (`"Amount"`). إذا ضبطتها على `false`، سيُحذف الرأس، مما يمنحك مزيدًا من التحكم في التخطيط النهائي.

## الخطوة 6: حفظ الملف – إنشاء مصنف Excel باستخدام Java على القرص

القطعة الأخيرة من اللغز هي حفظ المصنف الموجود في الذاكرة إلى ملف فعلي. يمكنك اختيار أي تنسيق تدعمه Aspose (`.xlsx`, `.xls`, `.csv`, …). هنا نحفظ كملف XLSX.

```java
// Step 6: Save the workbook to disk
String outputPath = "DataTableWithCurrencyStyle.xlsx";
workbook.save(outputPath);
System.out.println("Workbook saved to " + outputPath);
```

بعد تشغيل البرنامج، افتح الملف الناتج. سترى عمود `"Amount"` مُنسق بعلامة الدولار، منزلتين عشريتين، وفواصل آلاف صحيحة—تمامًا ما تتوقعه عندما **تطبق تنسيق الأرقام في Excel** للقيم النقدية.

## النتيجة المتوقعة

| المبلغ |
|--------|
| $1,234.56 |
| $7,890.12 |

يظهر عنوان العمود “المبلغ” بالخط العريض (النمط الافتراضي)، وكل خلية تحته تُظهر تنسيق العملة الذي حددناه. لا حاجة لتنسيق يدوي في Excel.

## نصائح احترافية ومخاطر شائعة

- **إعادة استخدام الأنماط بحكمة** – الأنماط خفيفة الوزن، لكن إنشاء `Style` جديد لكل خلية قد يبطئ الأداء. أعد استخدام كائن النمط عندما تطبق نفس التنسيق على عدة خلايا، كما فعلنا مع `currencyStyle`.
- **التنسيقات المخصصة** – إذا كان إقلمك يستخدم رمز عملة مختلف، استبدل `currencyStyle.setNumber(5)` بـ `currencyStyle.setCustom("€#,##0.00")`. اختبر التنسيق في Excel للتأكد من سلوكه.
- **مجموعات البيانات الكبيرة** – لآلاف الصفوف، فكر في استخدام `importDataTable` مع العلامة `ImportTableOptions.setImportDataOnly(true)` لتخطي توليد الرأس وتسريع الاستيراد.
- **سلامة الخيوط** – كائنات Aspose.Cells **غير** آمنة للاستخدام المتعدد الخيوط. أنشئ `Workbook` منفصل لكل خيط إذا كنت تولد تقارير بشكل متوازي.

## الأسئلة المتكررة

**س: هل يمكنني تطبيق تنسيق الرقم على مصنف موجود؟**  
ج: بالتأكيد. افتح المصنف بـ `new Workbook("Existing.xlsx")`، احصل على الورقة المستهدفة، واتبع الخطوات 3‑5 لتطبيق مصفوفة الأنماط على البيانات الجديدة.

**س: ماذا لو أردت تنسيق تواريخ بدلًا من عملة؟**  
ج: استخدم فهرس رقم مدمج مختلف (`14` للتاريخ القصير، `22` للتاريخ الطويل) أو تنسيق مخصص مثل `yyyy‑mm‑dd`. سيرتبط سير العمل بنفس الطريقة.

**س: هل يعمل هذا مع إصدارات Excel القديمة (.xls)؟**  
ج: نعم. فقط غيّر امتداد الملف في `workbook.save("MyFile.xls")`. سيتحول Aspose تلقائيًا إلى الصيغة الثنائية.

## الخلاصة – ما أنجزناه

لقد **طبقنا تنسيق الأرقام في Excel** على عمود من القيم المالية، وأظهرنا كيف **تطبيق تنسيق العملة في Excel**، ووضحنا أبسط طريقة لـ **إنشاء مصنف Excel باستخدام Java**، واستخدمنا Aspose.Cells لـ **استيراد جدول بيانات إلى Excel** دون الحاجة إلى واجهة المستخدم. كل ذلك تم في برنامج مختصر، مستقل، يمكنك نسخه، لصقه، وتشغيله.

ما الخطوة التالية؟ جرب توسيع المثال:

- أضف أعمدة أخرى (مثل “Date”، “Description”) وعيّن أنماطًا مختلفة لكل عمود.
- صدّر نفس البيانات إلى CSV وقارن كيف تُفقد تنسيقات الأرقام.
- دمج الكود في خدمة Spring Boot تُعيد المصنف كاستجابة HTTP قابلة للتحميل.

لا تتردد في التجربة، وإذا واجهت أي صعوبات، اترك تعليقًا أدناه. Happy coding!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مصدر يتضمن أمثلة شاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [How to Apply Styles to Excel Cells Using Aspose.Cells for Java - Complete Guide](/cells/english/java/formatting/apply-styles-excel-aspose-cells-java/)
- [Merge Cells & Apply Styles in Excel using Aspose.Cells for Java - A Complete Guide](/cells/english/java/formatting/merge-cells-apply-styles-aspose-cells-java/)
- [Aspose.Cells for Java&#58; How to Create and Format Excel Workbooks Efficiently](/cells/english/java/getting-started/aspose-cells-java-workbook-creation-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}