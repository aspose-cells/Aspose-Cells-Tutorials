---
category: general
date: 2026-06-27
description: تعلم كيفية استيراد DataTable إلى Excel بألوان أعمدة متناوبة. دليل خطوة
  بخطوة لاستيراد البيانات مع التنسيق وتعيين لون خط العمود باستخدام Java.
draft: false
keywords:
- alternating column colors
- import data with formatting
- import datatable to excel
- set column font color
- how to import datatable
language: ar
og_description: إتقان تلوين الأعمدة المتناوبة عند استيراد DataTable إلى Excel. يوضح
  هذا الدليل كيفية استيراد البيانات مع التنسيق وتعيين لون خط العمود في Java.
og_title: تلوين الأعمدة المتناوبة في إكسل – استيراد جدول البيانات مع التنسيق
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: Learn how to import DataTable to Excel with alternating column colors.
    Step‑by‑step guide on import data with formatting and set column font color using
    Java.
  headline: Alternating Column Colors in Excel – Import DataTable with Formatting
  type: TechArticle
- description: Learn how to import DataTable to Excel with alternating column colors.
    Step‑by‑step guide on import data with formatting and set column font color using
    Java.
  name: Alternating Column Colors in Excel – Import DataTable with Formatting
  steps:
  - name: Prerequisites
    text: '- Java 8+ (the code works with newer releases as well). - Apache POI 5.x
      on your classpath – the library that talks to Excel files. - A `DataTable` implementation
      that offers `getColumns()` and `size()` (or adapt the example to a `ResultSet`).'
  - name: – Obtain the DataTable You Want to Export
    text: First, you need a source of rows and columns. In real projects this might
      be a database query, a CSV parser, or an in‑memory collection. The example assumes
      a helper method `getDataTable()` that returns a ready‑to‑use `DataTable`.
  - name: – Prepare a Style for Each Column
    text: We create a `Style[]` whose length matches the number of columns. Each entry
      will hold a font color that alternates between blue and green.
  - name: – Create Styles with Alternating Font Colors
    text: 'Now the fun part: loop through the array and assign a blue font to even‑indexed
      columns and a green font to odd‑indexed ones. This is where **alternating column
      colors** is implemented.'
  - name: – Import the DataTable with the Style Array
    text: Finally, we hand the `DataTable` and the `columnStyles` array to POI’s `importDataTable`
      method. The `true` flag tells POI to treat the first row as column headers.
  - name: – Save the Workbook (Optional but Recommended)
    text: After the import, you’ll probably want to write the workbook to disk or
      stream it to a client.
  type: HowTo
- questions:
  - answer: Replace `setFontColor` with `setPatternForegroundColor` and call `setPattern(BackgroundType.SOLID)`
      on the style.
    question: What if I need background colors instead of font colors?
  - answer: 'Absolutely—just swap the loop logic: iterate over rows and assign a style
      per row index.'
    question: Can I apply the same color scheme to rows instead of columns?
  - answer: Excel caps at 16,384 columns (XFD). The code will throw an exception once
      you exceed that limit. Guard against it by checking `columnCount` against `SpreadsheetVersion.EXCEL2007.getMaxColumns()`.
    question: What if the DataTable has more columns than the worksheet can handle?
  - answer: Yes, POI abstracts the format. However, the older binary format supports
      fewer colors, so you might see a fallback to the nearest palette entry.
    question: Does this work with .xls (Excel 97‑2003) files?
  type: FAQPage
tags:
- excel
- java
- datatable
- formatting
- apache-poi
title: تلوين الأعمدة المتناوبة في إكسل – استيراد جدول البيانات مع التنسيق
url: /ar/java/excel-import-export/alternating-column-colors-in-excel-import-datatable-with-for/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ألوان الأعمدة المتناوبة في Excel – استيراد DataTable مع التنسيق

هل تساءلت يومًا كيف تضيف لمسة بصرية إلى تصدير Excel الخاص بك دون مغادرة الشيفرة؟ **Alternating column colors** طريقة سريعة لجعل الجداول الكبيرة قابلة للقراءة، ويمكنك القيام بذلك أثناء **import datatable to excel**. في هذا الدرس سنستعرض حلًا كاملاً بلغة Java لا ينقل بياناتك إلى ورقة عمل فحسب، بل يطبق أيضًا نمط خط أزرق‑أخضر عمودًا بعمود.

## ما ستقوم ببنائه

بنهاية هذا الدليل ستحصل على مقتطف Java قابل للتنفيذ يقوم بـ:

1. يسترجع `DataTable` (أو أي مجموعة تشبه `ResultSet`).  
2. يولد مصفوفة `Style` حيث تكون الأعمدة الزوجية باللون الأزرق والفردية باللون الأخضر.  
3. يستدعي `importDataTable` لإدخال البيانات في الخلية **A1** مع تطبيق الأنماط.  

### المتطلبات المسبقة

- Java 8+ (الكود يعمل مع الإصدارات الأحدث أيضًا).  
- Apache POI 5.x على مسار الفئات الخاص بك – المكتبة التي تتعامل مع ملفات Excel.  
- تنفيذ `DataTable` يوفر `getColumns()` و `size()` (أو عدل المثال ليتوافق مع `ResultSet`).  

إذا كنت تستخدم POI بالفعل لمهام Excel أخرى، يمكنك إدراج هذا مباشرة.

---

## ألوان الأعمدة المتناوبة أثناء استيراد DataTable إلى Excel

جوهر الحل يكمن في أربع خطوات مختصرة. لنستعرضها.

### الخطوة 1 – الحصول على DataTable الذي تريد تصديره

أولاً، تحتاج إلى مصدر للصفوف والأعمدة. في المشاريع الحقيقية قد يكون هذا استعلام قاعدة بيانات، أو محلل CSV، أو مجموعة في الذاكرة. يفترض المثال وجود طريقة مساعدة `getDataTable()` تُعيد `DataTable` جاهزًا للاستخدام.

```java
// Step 1: Obtain the data to be imported
DataTable dataTable = getDataTable();   // your own method that fills the table
```

> **لماذا هذا مهم:**  
> الحصول على البيانات أولاً يتيح لك فحص عدد الأعمدة، وهو ما يحدد حجم مصفوفة الأنماط لاحقًا. كما يضمن أن خطوة الاستيراد لديها كائن ملموس للعمل معه.

### الخطوة 2 – إعداد نمط لكل عمود

ننشئ `Style[]` يكون طولها مساويًا لعدد الأعمدة. كل عنصر سيحمل لون خط يتناوب بين الأزرق والأخضر.

```java
// Step 2: Prepare a style for each column (same count as the number of columns)
int columnCount = dataTable.getColumns().size();
Style[] columnStyles = new Style[columnCount];
```

> **نصيحة احترافية:** إذا كان `DataTable` الخاص بك يمكن أن يتغير شكله أثناء التشغيل، أعد حساب `columnCount` في كل مرة تقوم فيها بالتصدير. هذا يمنع حدوث `ArrayIndexOutOfBoundsException`.

### الخطوة 3 – إنشاء أنماط بألوان خطوط متناوبة

الجزء الممتع الآن: حلقة عبر المصفوفة وتعيين خط أزرق للأعمدة ذات الفهرس الزوجي وخط أخضر للأعمدة ذات الفهرس الفردي. هنا يتم تنفيذ **alternating column colors**.

```java
// Step 3: Create styles with alternating font colors for visual distinction
for (int i = 0; i < columnStyles.length; i++) {
    columnStyles[i] = workbook.createStyle();               // create a fresh style
    // Even columns → blue, odd columns → green
    columnStyles[i].setFontColor(
        (i % 2 == 0) ? Color.getBlue() : Color.getGreen()
    );
}
```

> **لماذا الألوان المتناوبة؟**  
> العين البشرية تقرأ الصفوف بسهولة أكبر عندما تبرز الأعمدة المتجاورة. إيقاع أزرق‑أخضر يقلل من إجهاد البصر، خاصة في الجداول الواسعة.

### الخطوة 4 – استيراد DataTable مع مصفوفة الأنماط

أخيرًا، نمرر `DataTable` ومصفوفة `columnStyles` إلى طريقة POI `importDataTable`. العلامة `true` تخبر POI بمعاملة الصف الأول كعناوين أعمدة.

```java
// Step 4: Import the data table into the worksheet starting at cell A1, applying the styles
worksheet.getCells().importDataTable(dataTable, true, "A1", columnStyles);
```

> **ماذا يحدث خلف الكواليس؟**  
> POI يتكرر على كل عمود، يستخرج الـ `Style` المطابق من المصفورة، ويكتب كل خلية باستخدام ذلك النمط. لأننا ضبطنا فقط لون الخط، تبقى الجوانب الأخرى (الحدود، الخلفية) بالقيمة الافتراضية—لا تتردد في توسيع النمط إذا احتجت إلى مزيد من الزخرفة.

### الخطوة 5 – حفظ المصنف (اختياري لكن يُنصح به)

بعد الاستيراد، ربما تريد كتابة المصنف إلى القرص أو بثه إلى عميل.

```java
// Optional: write the workbook to a file
try (FileOutputStream fos = new FileOutputStream("ExportedReport.xlsx")) {
    workbook.save(fos);
}
```

> **حالة حافة:** إذا كان الملف الهدف موجودًا بالفعل، سيقوم `FileOutputStream` بالكتابة فوقه. ضع الاستدعاء داخل فحص أو اطلب تأكيد المستخدم في سياق واجهة المستخدم.

---

## الأسئلة الشائعة والمفاجآت

- **ماذا لو احتجت ألوان خلفية بدلاً من ألوان الخط؟**  
  استبدل `setFontColor` بـ `setPatternForegroundColor` واستدعِ `setPattern(BackgroundType.SOLID)` على النمط.

- **هل يمكنني تطبيق نفس نظام الألوان على الصفوف بدلاً من الأعمدة؟**  
  بالتأكيد—فقط عكس منطق الحلقة: تكرار عبر الصفوف وتعيين نمط لكل فهرس صف.

- **ماذا لو كان لدى DataTable أكثر من عدد الأعمدة التي يمكن للورقة التعامل معها؟**  
  Excel يحد عدد الأعمدة إلى 16,384 عمود (XFD). سيُطلق الكود استثناءً إذا تجاوزت هذا الحد. احمِ نفسك بالتحقق من `columnCount` مقابل `SpreadsheetVersion.EXCEL2007.getMaxColumns()`.

- **هل يعمل هذا مع ملفات .xls (Excel 97‑2003)؟**  
  نعم، POI ي抽抽 الصيغة. ومع ذلك، يدعم التنسيق الثنائي القديم ألوانًا أقل، لذا قد ترى تحويلًا إلى أقرب إدخال في لوحة الألوان.

## مثال كامل يعمل

فيما يلي فئة مستقلة يمكنك لصقها في مشروع Maven يحتوي بالفعل على `org.apache.poi:poi-ooxml:5.2.3`. عدل `getDataTable()` لتعيد مصدر البيانات الفعلي الخاص بك.

```java
import com.aspose.cells.*;
import java.io.FileOutputStream;

public class ExcelAlternatingColorsExport {

    public static void main(String[] args) throws Exception {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // 1️⃣ Obtain the data to be imported
        DataTable dataTable = getDataTable(); // implement this method

        // 2️⃣ Prepare a style for each column
        int columnCount = dataTable.getColumns().size();
        Style[] columnStyles = new Style[columnCount];

        // 3️⃣ Create alternating font colors (blue for even, green for odd)
        for (int i = 0; i < columnStyles.length; i++) {
            columnStyles[i] = workbook.createStyle();
            columnStyles[i].setFontColor(
                (i % 2 == 0) ? Color.getBlue() : Color.getGreen()
            );
        }

        // 4️⃣ Import the data with formatting
        worksheet.getCells().importDataTable(dataTable, true, "A1", columnStyles);

        // 5️⃣ Save the file
        try (FileOutputStream fos = new FileOutputStream("AlternatingColorsReport.xlsx")) {
            workbook.save(fos);
        }

        System.out.println("Export complete – open AlternatingColorsReport.xlsx to see the result.");
    }

    // Dummy implementation – replace with real data retrieval
    private static DataTable getDataTable() {
        DataTable dt = new DataTable();
        dt.getColumns().add("ID");
        dt.getColumns().add("Name");
        dt.getColumns().add("Score");
        dt.getRows().add(new DataRow(new Object[]{1, "Alice", 85}));
        dt.getRows().add(new DataRow(new Object[]{2, "Bob", 92}));
        dt.getRows().add(new DataRow(new Object[]{3, "Carol", 78}));
        return dt;
    }
}
```

**الناتج المتوقع:** افتح `AlternatingColorsReport.xlsx`. العمود A و C (فهارس زوجية) يعرضان النص باللون الأزرق، بينما العمود B (فهرس فردي) يظهر بخط أخضر. الصف الأول غامق كعنوان لأن `importDataTable` يتعامل معه على هذا الأساس.

## الخلاصة

لقد غطينا الآن كل ما تحتاجه لـ **import datatable to excel** مع تطبيق **alternating column colors** و **set column font color** برمجيًا. النهج خفيف الوزن، يعتمد فقط على Apache POI، ويمكن توسيعه لتلبية احتياجات تنسيق أخرى مثل الحدود أو خلفيات الخلايا.

بعد ذلك، فكر في التجربة مع:

- **Import data with formatting** للصفوف (ألوان صفوف متناوبة).  
- إضافة **conditional formatting** لتسليط الضوء على الدرجات العالية.  
- تصدير مباشرةً إلى استجابة HTTP لتطبيقات الويب.

لا تتردد في تعديل النمط ليتناسب مع خط أنابيب التقارير الخاص بك—بمجرد إتقان الأساسيات، لا حدود للإمكانات. برمجة سعيدة!

## ماذا يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مصدر يتضمن أمثلة شيفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [كيفية فرز بيانات Excel حسب لون العمود باستخدام Aspose.Cells Java: دليل كامل](/cells/english/java/formatting/sort-excel-data-by-column-color-aspose-cells-java/)
- [إتقان حماية أعمدة Excel باستخدام Aspose.Cells for Java: دليل شامل](/cells/english/java/security-protection/excel-column-protection-aspose-cells-java/)
- [كيفية إدراج عمود في Excel باستخدام Aspose.Cells for Java - دليل شامل](/cells/english/java/worksheet-management/aspose-cells-java-insert-column-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}