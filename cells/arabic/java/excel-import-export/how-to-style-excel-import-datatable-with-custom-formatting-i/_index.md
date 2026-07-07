---
category: general
date: 2026-07-03
description: كيفية تنسيق ملفات Excel باستخدام Java. تعلم تنسيق تاريخ العمود في Excel،
  تطبيق تنسيق الأرقام في Excel، تصدير DataTable إلى XLSX واستيراد DataTable إلى Excel
  باستخدام Aspose Cells.
draft: false
keywords:
- how to style excel
- format column date excel
- apply number format excel
- export datatable to xlsx
- import datatable into excel
language: ar
og_description: كيفية تنسيق ملفات Excel في Java. يوضح هذا الدرس كيفية تنسيق تاريخ
  العمود في Excel، تطبيق تنسيق الأرقام في Excel، تصدير DataTable إلى XLSX واستيراد
  DataTable إلى Excel.
og_title: كيفية تنسيق إكسل – دليل جافا لتنسيق الأعمدة المخصص
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: How to style Excel files using Java. Learn to format column date Excel,
    apply number format Excel, export DataTable to XLSX and import DataTable into
    Excel with Aspose Cells.
  headline: How to Style Excel – Import DataTable with Custom Formatting in Java
  type: TechArticle
tags:
- Java
- Excel
- Aspose.Cells
title: كيفية تنسيق إكسل – استيراد DataTable مع تنسيق مخصص في جافا
url: /ar/java/excel-import-export/how-to-style-excel-import-datatable-with-custom-formatting-i/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تنسيق Excel – استيراد DataTable مع تنسيق مخصص في Java

هل تساءلت يومًا **عن كيفية تنسيق Excel** برمجياً دون فتح الملف يدويًا؟ لست وحدك. يحتاج العديد من المطورين إلى إنشاء تقارير يكون فيها العمود الأول غامقًا، والعمود الثاني يعرض تواريخ، والبقية تتبع تخطيطًا نظيفًا. في هذا الدليل سنستعرض مثالًا كاملاً قابلاً للتنفيذ **يستورد DataTable إلى Excel**، يطبق عنوانًا غامقًا، ينسق عمود التاريخ، وأخيرًا **يصدر DataTable إلى XLSX**.  

سنستخدم Aspose.Cells for Java، لكن المفاهيم تنطبق على أي مكتبة تسمح لك بالعمل مع الأنماط. بنهاية الدليل ستحصل على نمط قابل لإعادة الاستخدام لـ **apply number format Excel** الخلايا، **format column date Excel**، وتوزيع مصنف مصقول على مستخدميك.

## المتطلبات المسبقة

- Java 17 (أو أي JDK حديث)  
- Aspose.Cells for Java 23.9 أو أحدث (الإصدار التجريبي المجاني يعمل جيدًا)  
- بنية شبيهة بـ `DataTable` (المثال يستخدم نموذجًا بسيطًا)  
- بيئة التطوير المفضلة لديك (IntelliJ IDEA، Eclipse، VS Code…)

لا توجد إضافات Maven إضافية مطلوبة؛ فقط أضف ملف JAR الخاص بـ Aspose.Cells إلى مسار الفئة (classpath).

---

## الخطوة 1: الحصول على DataTable المصدر – إعداد “Export DataTable to XLSX”

قبل أن نتمكن من **import datatable into excel**، نحتاج إلى كائن `DataTable` يمثل البيانات التي تريد تصديرها. في المشاريع الحقيقية قد تستخرج هذا من قاعدة بيانات، ملف CSV، أو API. لهذا الدرس سنحاكي جدولًا صغيرًا:

```java
import java.util.*;
import com.aspose.cells.*;

public class DemoData {
    public static DataTable getDataTable() {
        // Create a simple table with three columns: ID, Date, Amount
        DataTable dt = new DataTable();
        dt.getColumns().add("ID", DataType.INTEGER);
        dt.getColumns().add("OrderDate", DataType.DATE_TIME);
        dt.getColumns().add("Total", DataType.DOUBLE);

        // Add a few rows
        dt.getRows().add(new Object[]{1, new Date(), 125.50});
        dt.getRows().add(new Object[]{2, new Date(System.currentTimeMillis() - 86400000L), 99.99});
        dt.getRows().add(new Object[]{3, new Date(System.currentTimeMillis() - 2*86400000L), 250.00});
        return dt;
    }
}
```

> **لماذا هذا مهم:** الحصول على البيانات بشكل صحيح في البداية يعني أن منطق التنسيق المتبقي يمكنه التركيز فقط على العرض، لا على معالجة البيانات.

---

## الخطوة 2: إنشاء مصفوفة لتخزين تعريفات الأنماط لكل عمود

تتيح لك Aspose.Cells تمرير مصفوفة **Style[]** عند استيراد `DataTable`. كل عنصر يتطابق مع عمود ويحدد كيف سيظهر ذلك العمود بعد الاستيراد. لنخصص المصفوفة بناءً على عدد الأعمدة:

```java
DataTable dataTable = DemoData.getDataTable();
Style[] columnStyles = new Style[dataTable.getColumns().size()];
```

> **نصيحة:** إذا كان لديك العديد من الأعمدة، فكر في بناء المصفوفة داخل حلقة وإعادة استخدام كائن `Style` واحد حيثما يكون التنسيق متماثلًا. هذا يقلل من استهلاك الذاكرة.

---

## الخطوة 3: تعريف الأنماط – عنوان غامق وتنسيق التاريخ

الآن نجيب على سؤال **format column date excel** الكلاسيكي ونوضح أيضًا **apply number format excel** للأعمدة الأخرى.

```java
// --- Style for the first column (header bold) ---
columnStyles[0] = new Style();
columnStyles[0].getFont().setBold(true);          // Makes header text bold

// --- Style for the second column (date formatting) ---
columnStyles[1] = new Style();
columnStyles[1].setNumber(StyleNumberFormat.DATE); // Uses the built‑in DATE format

// --- Optional: Style for the third column (currency) ---
columnStyles[2] = new Style();
columnStyles[2].setNumber(StyleNumberFormat.CURRENCY_USD);
```

**ما الذي يحدث هنا؟**  
- `StyleNumberFormat.DATE` يخبر Excel بمعالجة قيمة الخلية كتاريخ قصير (مثال: *01/31/2024*).  
- `StyleNumberFormat.CURRENCY_USD` يضيف تلقائيًا رمز `$` ومكانين عشريين.  
- ضبط الخط على غامق في العمود الأول يجعل العنوان بارزًا، وهو طلب شائع عندما تريد **how to style excel** لجداول البيانات لسهولة القراءة.

> **حالة حافة:** إذا كانت بيانات المصدر لديك تحتوي بالفعل على سلاسل منسقة، قد تحتاج إلى تحويلها إلى كائنات `java.util.Date` قبل الاستيراد؛ وإلا سيتعامل Excel معها كنص عادي.

---

## الخطوة 4: إنشاء مصنف جديد والوصول إلى ورقة العمل الأولى

المصنف الجديد يمنحنا لوحة رسم نظيفة. سنأخذ ورقة العمل الأولى، حيث سيقع الاستيراد.

```java
Workbook workbook = new Workbook();               // New empty workbook
Worksheet worksheet = workbook.getWorksheets().get(0); // First sheet (index 0)
```

> **لماذا مصنف جديد؟** البدء من الصفر يضمن عدم وجود أنماط متبقية أو صفوف مخفية تؤثر على النتيجة النهائية—وهو أمر أساسي عندما تريد **how to style excel** الملفات بشكل ثابت عبر تشغيلات متعددة.

---

## الخطوة 5: استيراد DataTable مع أنماط الأعمدة

هذا هو جوهر العملية: تمرير `DataTable` إلى الورقة مع تطبيق مصفوفة الأنماط التي أنشأناها.

```java
// The third argument (true) tells Aspose.Cells to include column headers.
worksheet.getCells().importDataTable(dataTable, true, columnStyles);
```

**شرح:**  
- `importDataTable` ينسخ كلًا من صف العنوان وصفوف البيانات.  
- مصفوفة `columnStyles` تتطابق مع كل عمود، لذا يصبح عنوان العمود الأول غامقًا، والعمود الثاني يظهر تواريخ، والعمود الثالث يظهر كعملة.  
- هذه السطر الواحد يستبدل العشرات من خطوات التنسيق اليدوي للخلية، موضحًا طريقة نظيفة لـ **apply number format excel** برمجيًا.

---

## الخطوة 6: حفظ المصنف المنسق – إكمال “Export DataTable to XLSX”

أخيرًا نقوم بحفظ المصنف على القرص. عدل المسار إلى مجلد قابل للكتابة على جهازك.

```java
String outputPath = "C:/temp/styledImport.xlsx";
workbook.save(outputPath);
System.out.println("Workbook saved to " + outputPath);
```

افتح الملف في Excel وسترى:

- عنوان العمود **ID** غامق.  
- عمود **OrderDate** منسق كتاريخ (مثال: *04/27/2024*).  
- عمود **Total** يظهر برمز الدولار ومكانين عشريين.

> **نصيحة احترافية:** إذا كنت بحاجة لدعم إصدارات Excel أقدم، استدعِ `workbook.save(outputPath, SaveFormat.XLS)` بدلاً من الصيغة الافتراضية XLSX.

---

## الخطوة 7: التحقق من النتيجة وإجراء تعديلات اختيارية

من الممارسات الجيدة مراجعة الملف المُنشأ، خاصةً عند أتمتة التقارير لأصحاب المصلحة.

```java
// Quick verification: read the first cell's style
Cell firstHeader = worksheet.getCells().get(0, 0);
boolean isBold = firstHeader.getStyle().getFont().isBold();
System.out.println("Header bold? " + isBold);
```

إذا طبع `isBold` القيمة `true`، فإن روتين **how to style excel** الخاص بك عمل كما هو متوقع. من هنا يمكنك:

- إضافة تنسيق شرطي (مثال: تمييز القيم > $200).  
- تجميد الصف العلوي لتسهيل التمرير.  
- إدراج مخطط يُشير إلى البيانات المستوردة.

جميع هذه الإضافات تتبع نفس النمط: تعريف `Style`، تطبيقه، ثم حفظ.

---

## أسئلة شائعة وحالات حافة

| السؤال | الجواب |
|----------|--------|
| **هل يمكنني تنسيق أكثر من عمود بنفس الطريقة؟** | نعم—أعد استخدام كائن `Style` واحد لجميع الأعمدة التي تشترك في نفس التنسيق. |
| **ماذا لو كان DataTable يحتوي على أعمدة أكثر من الأنماط؟** | أي عمود لا يملك عنصرًا مطابقًا في `columnStyles` سيستخدم النمط الافتراضي. |
| **كيف أغيّر تنسيق التاريخ إلى “dd‑MMM‑yyyy”?** | استخدم `columnStyles[1].setCustom("#dd-MMM-yyyy#");` بدلاً من `DATE` المدمج. |
| **هل هناك طريقة لتغيير حجم الأعمدة تلقائيًا بعد الاستيراد؟** | استدعِ `worksheet.autoFitColumns();` بعد `importDataTable`. |
| **هل سيعمل هذا على Linux/macOS؟** | بالتأكيد—Aspose.Cells مستقل عن المنصة طالما لديك JDK متوافق. |

---

## الخلاصة

أصبح لديك الآن مثال شامل من البداية إلى النهاية لـ **how to style Excel** عبر **importing datatable into excel**, **format column date excel**, و **apply number format excel** باستخدام Java. يُظهر الكود التدفق الكامل من **export datatable to xlsx** إلى فتح الملف في Excel، موضحًا كلًا من *ما* و *لماذا* وراء كل خطوة.  

جرّبه: عدّل مصفوفة الأنماط، أضف أعمدة أخرى، أو اربط استعلام قاعدة بيانات حقيقي. سيسمح لك النمط نفسه بإنشاء تقارير ذات مظهر احترافي بنقرة زر، دون الحاجة لتنسيق يدوي.

---

![Styled Excel worksheet generated by the tutorial code](https://example.com/images/styled-worksheet.png "Screenshot of styled Excel worksheet created using Java and Aspose.Cells")

*نص بديل للصورة: “ورقة Excel منسقة تم إنشاؤها باستخدام Java وAspose.Cells، تُظهر عنوانًا غامقًا وعمود تاريخ منسق.”*


## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [How to Create & Format Excel Cells Using Aspose.Cells for Java: A Step‑By‑Step Guide](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)
- [How to Style Excel Cells and Add Hyperlinks Using Aspose.Cells for Java](/cells/english/java/formatting/style-excel-cells-hyperlinks-aspose-cells-java/)
- [Aspose.Cells for Java: How to Create and Format Excel Workbooks Efficiently](/cells/english/java/getting-started/aspose-cells-java-workbook-creation-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}