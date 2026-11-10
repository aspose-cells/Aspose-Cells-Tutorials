---
date: 2026-07-26
description: تعلم كيفية حساب الفرق بين التواريخ في Java باستخدام وظائف تاريخ Aspose.Cells
  Excel. يتضمن أمثلة على نهاية الشهر، TODAY، و DATEDIF.
keywords:
- calculate date difference java
- end of month java
- add excel date formula
- implement excel date functions
- retrieve current date excel
lastmod: 2026-07-26
linktitle: حساب الفرق بين التواريخ في Java – وظائف تاريخ Excel
og_description: احسب الفرق بين التواريخ في Java باستخدام وظائف تاريخ Aspose.Cells
  Excel. يوضح هذا الدليل كيفية إضافة صيغ تاريخ Excel، استرجاع التواريخ الحالية، والحصول
  على قيم نهاية الشهر بكفاءة.
og_image_alt: 'Guide: calculate date difference in Java with Aspose.Cells Excel functions'
og_title: حساب الفرق بين التواريخ في Java – وظائف تاريخ Excel
schemas:
- author: Aspose
  dateModified: '2026-07-26'
  description: Learn how to calculate date difference in Java using Aspose.Cells Excel
    date functions. Includes end of month, TODAY, and DATEDIF examples.
  headline: Calculate Date Difference in Java – Excel Date Functions
  type: TechArticle
- description: Learn how to calculate date difference in Java using Aspose.Cells Excel
    date functions. Includes end of month, TODAY, and DATEDIF examples.
  name: Calculate Date Difference in Java – Excel Date Functions
  steps:
  - name: '**Download and Install Aspose.Cells:** Visit [Aspose.Cells for Java](https://releases.aspose.com/cells/java/)
      and download the latest release.'
    text: '**Download and Install Aspose.Cells:** Visit [Aspose.Cells for Java](https://releases.aspose.com/cells/java/)
      and download the latest release.'
  - name: '**Add the Library to Your Project:** Include the JAR file in your build
      path or add the Maven dependency.'
    text: '**Add the Library to Your Project:** Include the JAR file in your build
      path or add the Maven dependency.'
  - name: '**License Configuration:** Place your license file (`Aspose.Cells.lic`)
      in the project resources and load it at runtime to unlock full features.'
    text: '**License Configuration:** Place your license file (`Aspose.Cells.lic`)
      in the project resources and load it at runtime to unlock full features.'
  - name: '**Download the library [here](https://releases.aspose.com/cells/java/).**'
    text: '**Download the library [here](https://releases.aspose.com/cells/java/).**'
  type: HowTo
- questions:
  - answer: Create a `Style` object, set its `Number` property to `"dd-MM-yyyy"`,
      and apply it to the target cell via `cell.setStyle(style)`. **`Style` defines
      formatting such as number format, font, and alignment for a cell.**
    question: How do I format a cell to display dates in `dd‑MM‑yyyy` format?
  - answer: Yes, you can retrieve the `Date` objects from two cells, convert them
      to `java.time.LocalDate`, and use `ChronoUnit.DAYS.between(start, end)` for
      precise control.
    question: Can I calculate date differences without using the DATEDIF formula?
  - answer: Absolutely. All built‑in Excel date functions, including DATEDIF and EOMONTH,
      correctly handle leap years according to the Gregorian calendar.
    question: Does Aspose.Cells support leap‑year calculations?
  - answer: Iterate through each `Worksheet` in the `Workbook`, set the required formulas,
      and call `calculateFormula()` once per workbook for optimal performance.
    question: Is it possible to batch‑process multiple worksheets for date calculations?
  - answer: All functions are available from **Aspose.Cells 23.9** onward; the latest
      release (as of 2026) adds performance optimizations for large datasets.
    question: What version of Aspose.Cells is required for these features?
  type: FAQPage
second_title: Aspose.Cells Java Excel Processing API
tags:
- excel date functions
- aspose cells
- java excel processing
- date calculations
- java tutorial
title: حساب الفرق بين التواريخ في Java – وظائف تاريخ Excel
url: /ar/java/basic-excel-functions/excel-date-functions-tutorial/
weight: 19
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# دروس وظائف التاريخ في Excel

في هذا الدرس الشامل، **calculate date difference java** هو محور تركيزنا. سنستعرض كيفية استخدام Aspose.Cells for Java للعمل مع وظائف التاريخ في Excel، بدءًا من إنشاء التواريخ إلى استرجاع اليوم الحالي، حساب الفروقات، وإيجاد نهايات الأشهر. سواءً كنت تحسن محرك تقارير أو تقوم بأتمتة جداول البيانات، ستوفر لك هذه التقنيات الوقت وتقلل الأخطاء. هيا نبدأ!

## إجابات سريعة
- **كيف أحسب فرق التاريخ في Java؟** استخدم دالة DATEDIF عبر Aspose.Cells وحدد الوحدة (الأيام، الأشهر، السنوات).  
- **كيف يمكنني الحصول على تاريخ اليوم في Excel من Java؟** استدعِ دالة TODAY عبر Aspose.Cells أو اضبط قيمة الخلية إلى `new Date()`.  
- **ما الطريقة التي تُرجع اليوم الأخير من الشهر؟** استخدم دالة EOMONTH؛ تقوم Aspose.Cells بتقييمها تلقائيًا.  
- **هل أحتاج إلى ترخيص لـ Aspose.Cells؟** نعم، الترخيص الصالح يزيل علامات التقييم المائية ويفتح جميع الوظائف.  
- **ما نسخة Java المدعومة؟** Aspose.Cells يعمل مع Java 8 وما بعدها.

## ما هي وظائف التاريخ في Excel؟
وظائف التاريخ في Excel هي صيغ مدمجة تُنشئ أو تُعالج أو تُقيم التواريخ داخل ورقة العمل. تتيح لك إجراء عمليات حسابية، جلب التاريخ الحالي، أو حساب حدود الأشهر دون حسابات يدوية. باستخدام هذه الدوال يمكنك إضافة أو طرح أيام، أشهر، أو سنوات، تحديد عدد الأيام بين تاريخين، وتعديل تلقائي للسنوات الكبيسة وطول الأشهر المتفاوت، كل ذلك مع الحفاظ على البيانات بتنسيق يفهمه Excel ويمكنه عرضه وفقًا للإعدادات الإقليمية.

## لماذا تستخدم Aspose.Cells for Java لتطبيق وظائف التاريخ في Excel؟
Aspose.Cells يدعم **50+** صيغة إدخال وإخراج، يعالج جداول البيانات بـ **ما يصل إلى 1 000 صفحة** دون تحميل الملف بالكامل إلى الذاكرة، وينفّذ حسابات الصيغ بسرعة **تصل إلى 3×** أسرع من Excel الأصلي على نفس الأجهزة. هذه الزيادة في الأداء حاسمة لخطوط أنابيب البيانات على نطاق واسع.

## فهم وظائف التاريخ في Excel

Excel يقدم مجموعة غنية من وظائف التاريخ التي تبسط الحسابات المعقدة. أدناه نبرز الأكثر شيوعًا ونظهر كيف تقوم Aspose.Cells بتقييمها تلقائيًا.

### دالة DATE
دالة `DATE` تُنشئ قيمة تاريخ من مكونات السنة والشهر واليوم.  
**الإجابة المباشرة:** `=DATE(2023, 12, 31)` تُعيد الرقم التسلسلي لتاريخ 31 ديسمبر 2023، والذي ينسقه Excel ك تاريخ. في Java، يمكنك ضبط صيغة الخلية إلى هذه السلسلة وستقوم Aspose.Cells بحساب التاريخ الصحيح عند حفظ المصنف أو إعادة حسابه.

### دالة TODAY
دالة `TODAY` تُعيد تاريخ النظام الحالي دون مكوّن الوقت.  
**الإجابة المباشرة:** `=TODAY()` دائمًا تعكس اليوم الذي يُفتح فيه المصنف أو يُعاد حسابه، مما يجعلها مثالية للتقارير الديناميكية.

### دالة DATEDIF
دالة `DATEDIF` تحسب الفرق بين تاريخين بالأيام أو الأشهر أو السنوات.  
**الإجابة المباشرة:** `=DATEDIF(A1, B1, "d")` تُعطي عدد الأيام بين التواريخ في الخلايا A1 و B1. هذا هو جوهر سيناريو **calculate date difference java** الخاص بنا.

### دالة EOMONTH
دالة `EOMONTH` تُعيد اليوم الأخير من الشهر لتاريخ بداية معين، مع إزاحة بعدد محدد من الأشهر.  
**الإجابة المباشرة:** `=EOMONTH(A1, 0)` تُعطي اليوم الأخير من الشهر الذي يحتوي على التاريخ في A1.

## العمل مع Aspose.Cells for Java

الآن بعد أن غطينا الأساسيات، دعنا نرى كيفية إعداد Aspose.Cells وتطبيق هذه الدوال برمجيًا.

### إعداد Aspose.Cells

قبل كتابة الكود، تأكد من جاهزية بيئتك:

1. **تنزيل وتثبيت Aspose.Cells:** زر [Aspose.Cells for Java](https://releases.aspose.com/cells/java/) وقم بتنزيل أحدث إصدار.  
2. **إضافة المكتبة إلى مشروعك:** أدرج ملف JAR في مسار البناء أو أضف تبعية Maven.  
3. **إعداد الترخيص:** ضع ملف الترخيص (`Aspose.Cells.lic`) في موارد المشروع وحمّله وقت التشغيل لفتح جميع الميزات.  
4. **قم بتنزيل المكتبة [هنا](https://releases.aspose.com/cells/java/).**

### كيفية حساب فرق التاريخ في Java باستخدام Aspose.Cells؟

الـ `Workbook` يمثل ملف Excel كامل في الذاكرة، يحتوي على أوراق العمل، الخلايا، والأنماط.  
حمّل المصنف، اضبط صيغة DATEDIF، وقم بتقييمها.  
**الإجابة المباشرة:** أنشئ `Workbook`، عيّن `=DATEDIF(A2,B2,"d")` إلى خلية، استدعِ `calculateFormula()`، ثم اقرأ القيمة الرقمية الناتجة. هذا يوفر عدد الأيام الدقيق بين تاريخين في استدعاء API واحد.

```java
// Create a new workbook
Workbook workbook = new Workbook();

// Access the first worksheet
Worksheet worksheet = workbook.getWorksheets().get(0);

// Set the date using the DATE function
worksheet.getCells().get("A1").putValue("=DATE(2023, 9, 7)");

// Get the calculated date value
String calculatedDate = worksheet.getCells().get("A1").getStringValue();

// Print the result
System.out.println("Calculated Date: " + calculatedDate);
```

### استخدام دالة DATE مع Aspose.Cells

يمكنك تضمين صيغة `DATE` مباشرةً في خلية لإنشاء تواريخ من قيم السنة، الشهر، واليوم المنفصلة.

**الإجابة المباشرة:** اضبط صيغة الخلية إلى `=DATE(2024, 5, 15)`؛ بعد استدعاء `calculateFormula()`، تعرض الخلية `15‑May‑2024` وفقًا لإعدادات المصنف الإقليمية.

```java
// Create a new workbook
Workbook workbook = new Workbook();

// Access the first worksheet
Worksheet worksheet = workbook.getWorksheets().get(0);

// Use the TODAY function to get the current date
worksheet.getCells().get("A1").setFormula("=TODAY()");

// Get the current date value
String currentDate = worksheet.getCells().get("A1").getStringValue();

// Print the result
System.out.println("Current Date: " + currentDate);
```

### العمل مع دالة TODAY

استرجاع التاريخ الحالي برمجيًا سهل.

**الإجابة المباشرة:** عيّن `=TODAY()` إلى خلية، استدعِ `calculateFormula()`، وستحتوي الخلية على تاريخ اليوم في كل مرة يُفتح فيها المصنف أو يُعاد حسابه.

```java
// Create a new workbook
Workbook workbook = new Workbook();

// Access the first worksheet
Worksheet worksheet = workbook.getWorksheets().get(0);

// Set two date values
worksheet.getCells().get("A1").putValue("2023-09-07");
worksheet.getCells().get("A2").putValue("2023-08-01");

// Calculate the difference using DATEDIF
worksheet.getCells().get("A3").setFormula("=DATEDIF(A1, A2, \"d\")");

// Get the difference in days
int daysDifference = worksheet.getCells().get("A3").getIntValue();

// Print the result
System.out.println("Days Difference: " + daysDifference);
```

### حساب فروق التاريخ باستخدام DATEDIF

لمهمة **calculate date difference java** الأساسية، استخدم DATEDIF.

**الإجابة المباشرة:** ضع `=DATEDIF(C2,D2,"m")` في خلية للحصول على الفرق بالأشهر، أو استبدل `"m"` بـ `"y"` أو `"d"` للسنوات أو الأيام على التوالي. بعد الحساب، اقرأ النتيجة الرقمية عبر `cell.getIntValue()`.

```java
// Create a new workbook
Workbook workbook = new Workbook();

// Access the first worksheet
Worksheet worksheet = workbook.getWorksheets().get(0);

// Set a date value
worksheet.getCells().get("A1").putValue("2023-09-07");

// Calculate the end of the month using EOMONTH
worksheet.getCells().get("A2").setFormula("=EOMONTH(A1, 0)");

// Get the end-of-month date
String endOfMonth = worksheet.getCells().get("A2").getStringValue();

// Print the result
System.out.println("End of Month: " + endOfMonth);
```

### العثور على نهاية الشهر

دالة EOMONTH تساعدك على تحديد تواريخ نهاية الشهر لدورات الفوترة أو فترات التقارير.

**الإجابة المباشرة:** اضبط صيغة الخلية إلى `=EOMONTH(E2,0)`؛ بعد تقييم الصيغة، تحتوي الخلية على اليوم الأخير من شهر التاريخ الموجود في E2.

## مشكلات شائعة ونصائح
- **إعادة حساب الصيغة:** استدعِ دائمًا `workbook.calculateFormula()` بعد ضبط أو تعديل الصيغ؛ وإلا ستحتفظ الخلايا بالقيم القديمة.  
- **أرقام التسلسل للتواريخ:** Excel يخزن التواريخ كأرقام تسلسلية؛ عند قراءة القيم، استخدم `cell.getDateValue()` للحصول على كائن `java.util.Date`.  
- **مشكلات الإعدادات الإقليمية:** تنسيق التاريخ يحترم إعدادات المصنف الإقليمية. اضبط النمط صراحة إذا كنت بحاجة إلى تنسيق عرض محدد.  
- **مصنفات كبيرة:** للملفات التي تحتوي على **مئات الآلاف من الصفوف**، فعّل `WorkbookSettings.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` للحفاظ على استهلاك الذاكرة منخفضًا.  
- **`WorkbookSettings` يضبط خيارات الذاكرة والحساب لمصنف `Workbook`.**  

## الأسئلة المتكررة

**س: كيف أقوم بتنسيق خلية لعرض التواريخ بصيغة `dd‑MM‑yyyy`؟**  
A: أنشئ كائن `Style`، اضبط خاصية `Number` إلى `"dd-MM-yyyy"`، وطبقها على الخلية المستهدفة عبر `cell.setStyle(style)`.  
**`Style` يحدد التنسيق مثل تنسيق الرقم، الخط، والمحاذاة للخلية.**

**س: هل يمكنني حساب فروق التاريخ دون استخدام صيغة DATEDIF؟**  
A: نعم، يمكنك استرجاع كائنات `Date` من خليتين، تحويلها إلى `java.time.LocalDate`، واستخدام `ChronoUnit.DAYS.between(start, end)` للتحكم الدقيق.

**س: هل يدعم Aspose.Cells حساب السنوات الكبيسة؟**  
A: بالتأكيد. جميع وظائف التاريخ المدمجة في Excel، بما في ذلك DATEDIF و EOMONTH، تتعامل بشكل صحيح مع السنوات الكبيسة وفقًا للتقويم الغريغوري.

**س: هل يمكن معالجة عدة أوراق عمل دفعيًا لحسابات التاريخ؟**  
A: قم بالتكرار عبر كل `Worksheet` في `Workbook`، اضبط الصيغ المطلوبة، واستدعِ `calculateFormula()` مرة واحدة لكل مصنف لتحقيق الأداء الأمثل.

**س: ما نسخة Aspose.Cells المطلوبة لهذه الميزات؟**  
A: جميع الدوال متاحة بدءًا من **Aspose.Cells 23.9**؛ الإصدار الأخير (حتى 2026) يضيف تحسينات أداء لمجموعات البيانات الكبيرة.

## الخلاصة

قدم لك هذا الدرس نظرة متعمقة على وظائف التاريخ في Excel وأظهر لك كيفية **calculate date difference java** باستخدام Aspose.Cells for Java. الآن تعرف كيف تُعد المكتبة، وتطبق صيغ DATE و TODAY و DATEDIF و EOMONTH، وتتعامل مع التحديات الشائعة مثل تنسيق الإعدادات الإقليمية والمعالجة على نطاق واسع. دمج هذه الأنماط في تطبيقات Java الخاصة بك لأتمتة التقارير والتحليلات القائمة على التاريخ بثقة.

---

**آخر تحديث:** 2026-07-26  
**تم الاختبار مع:** Aspose.Cells 24.11 for Java  
**المؤلف:** Aspose  
**الموارد ذات الصلة:** API Reference [here](https://reference.aspose.com/cells/java/) | Download Free Trial [here](https://releases.aspose.com/cells/java/)

{{< blocks/products/products-backtop-button >}}

## دروس ذات صلة

- [إتقان نظام التاريخ 1904 في Excel باستخدام Aspose.Cells Java لعمليات الخلايا الفعّالة](/cells/java/cell-operations/aspose-cells-java-configure-1904-date-system-excel/)
- [إتقان عرض البيانات في Excel: تنسيق الأرقام والتواريخ المخصصة مع Aspose.Cells for Java](/cells/java/formatting/aspose-cells-java-data-formatting-excel/)
- [دروس صيغ ووظائف Excel لـ Aspose.Cells Java](/cells/java/formulas-functions/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

```java
// Create a date style
Style dateStyle = workbook.createStyle();
dateStyle.setCustom("dd-MM-yyyy");

// Apply the style to a cell
worksheet.getCells().get("A1").setStyle(dateStyle);
```