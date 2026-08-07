---
category: general
date: 2026-07-03
description: تعيين اسم الجدول في مصنف Excel باستخدام Java وتعلم كيفية إضافة نطاق مسمى
  للتعامل الديناميكي مع البيانات.
draft: false
keywords:
- set table name
- add named range
- how to create table
- how to add named range
- create excel workbook java
language: ar
og_description: تعيين اسم الجدول في مصنف Excel باستخدام Java وتعلم كيفية إضافة نطاق
  مسمى لمعالجة البيانات الديناميكية.
og_title: تعيين اسم الجدول في إكسل باستخدام جافا – دليل كامل
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Set table name in an Excel workbook using Java and learn how to add
    named range for dynamic data handling.
  headline: Set Table Name in Excel with Java – Complete Guide
  type: TechArticle
- description: Set table name in an Excel workbook using Java and learn how to add
    named range for dynamic data handling.
  name: Set Table Name in Excel with Java – Complete Guide
  steps:
  - name: '**Sheet1** shows a nicely formatted table titled **Sales**. You can click
      any cell inside the table and see the Table Tools ribbon appear.'
    text: '**Sheet1** shows a nicely formatted table titled **Sales**. You can click
      any cell inside the table and see the Table Tools ribbon appear.'
  - name: 'In the **Formulas → Name Manager**, you’ll find two entries:'
    text: 'In the **Formulas → Name Manager**, you’ll find two entries:'
  - name: Try typing `=SUM(TotalSales)` in any cell; Excel will correctly sum the
      quantities, proving that the named range works.
    text: Try typing `=SUM(TotalSales)` in any cell; Excel will correctly sum the
      quantities, proving that the named range works.
  type: HowTo
tags:
- Java
- Excel
- Aspose.Cells
- Workbook
title: تعيين اسم الجدول في إكسل باستخدام جافا – دليل شامل
url: /ar/java/tables-structured-references/set-table-name-in-excel-with-java-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تعيين اسم الجدول في Excel باستخدام Java – دليل كامل

هل تريد **تعيين اسم جدول** في مصنف Excel باستخدام Java؟ أنت في المكان الصحيح. سواءً كنت تبني محرك تقارير أو تحتاج فقط إلى جدول بيانات منظم، فإن معرفة *كيفية إنشاء جدول* والهياكل و*إضافة نطاق مسمى* يجعل كودك أكثر قابلية للصيانة.

في هذا الدرس سنستعرض العملية الكاملة **لإنشاء مصنف Excel في Java**، إضافة جدول، إعطاء هذا الجدول اسمًا ذا معنى، ثم تعريف نطاق مسمى على مستوى المصنف يتعايش بسلاسة. في النهاية ستفهم *كيفية إضافة نطاق مسمى* دون التعارض مع معرف الجدول، وستحصل على مثال شفرة جاهز للتنفيذ يمكنك إدراجه في مشروعك.

> **المتطلبات المسبقة:** Java 17+ (أو أي JDK حديث)، Maven أو Gradle، ومكتبة Aspose.Cells for Java (الإصدار التجريبي المجاني يكفي). لا تحتاج إلى خبرة سابقة في أتمتة Excel—فقط رغبة في التجربة.

---

## كيفية تعيين اسم جدول في مصنف Excel باستخدام Java

أول شيء يجب أن تعرفه هو أن **اسم الجدول** هو في الأساس معرف محصور يعيش داخل ورقة العمل. يتيح لك الإشارة إلى الجدول في الصيغ، VBA، أو أي كود آخر. في Aspose.Cells كائن `Table` يوفر طريقة `setName`، لذا فإن تعيين اسم يكون بسيطًا—*بمجرد أن تحصل على الجدول نفسه*.

```java
import com.aspose.cells.*;

public class SetTableNameDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook (create excel workbook java)
        Workbook workbook = new Workbook();

        // Step 2: Access the first worksheet
        Worksheet sheet = workbook.getWorksheets().get(0);
        sheet.setName("Sheet1");

        // Step 3: Populate some sample data in A1:B5
        String[][] data = {
                {"Product", "Quantity"},
                {"Apples", "30"},
                {"Bananas", "45"},
                {"Cherries", "20"},
                {"Dates", "10"}
        };
        for (int i = 0; i < data.length; i++) {
            for (int j = 0; j < data[i].length; j++) {
                sheet.getCells().get(i, j).putValue(data[i][j]);
            }
        }

        // Step 4: Add a table that covers the data range (how to create table)
        Table salesTable = sheet.getTables().add("A1:B5", true);
        // Now we give the table a friendly identifier
        salesTable.setName("Sales");   // <-- set table name

        // Step 5: Try to add a workbook‑level named range with the same identifier
        try {
            // This will clash because "Sales" is already used by the table
            workbook.getNames().add("Sales", "=Sheet1!$C$1");
        } catch (Exception ex) {
            // Step 6: Handle the conflict – the table already uses the name "Sales"
            System.out.println("Conflict: " + ex.getMessage());
        }

        // Step 7: Add a proper named range that does NOT conflict
        workbook.getNames().add("TotalSales", "=Sheet1!$B$2:$B$5");

        // Save the file so you can inspect it
        workbook.save("SetTableNameDemo.xlsx");
        System.out.println("Workbook created successfully.");
    }
}
```

**لماذا هذا مهم:**  
- `salesTable.setName("Sales")` هو عملية *تعيين اسم الجدول* التي نبحث عنها.  
- السطر التالي `workbook.getNames().add("Sales", …)` يوضح ما يحدث عندما *تضيف نطاقًا مسمى* بمعرف يشغله جدول بالفعل—تقوم Aspose.Cells بإلقاء استثناء بالرسالة “Name already used by a table.”  
- أخيرًا، إنشاء نطاق مسمى مميز (`TotalSales`) يوضح الطريقة الصحيحة لـ *كيفية إضافة نطاق مسمى* دون تعارض.

عند تشغيل البرنامج، سترى سطرين في وحدة التحكم:

```
Conflict: Name already used by a table.
Workbook created successfully.
```

افتح **SetTableNameDemo.xlsx** وستلاحظ جدولًا باسم **Sales** يغطي الخلايا A1:B5، بالإضافة إلى اسم على مستوى المصنف **TotalSales** يشير إلى عمود الكمية. هذا هو سير العمل الكامل لـ *تعيين اسم جدول* و*إضافة نطاق مسمى* في مثال واحد مرتب.

---

## إضافة نطاق مسمى باستخدام Java

**النطاق المسمى** هو اسم عالمي لخلية أو مجموعة خلايا. يكون مفيدًا في الصيغ، التحقق من صحة البيانات، وحتى مصادر المخططات. المفتاح هو التأكد من أن الاسم الذي تختاره غير مستخدم بالفعل من قبل جدول أو نطاق مسمى آخر.

```java
// Example: Adding a named range called "QuarterlyTotal"
workbook.getNames().add("QuarterlyTotal", "=Sheet1!$B$2:$B$5");
```

> **نصيحة محترف:** دائمًا استدعِ `workbook.getNames().add(...)` *بعد* تعريف أي جداول. بهذه الطريقة يمكنك التحقق بـ `workbook.getNames().contains("YourName")` لتجنب التصادمات غير المقصودة.

إذا كنت بحاجة إلى **كيفية إضافة نطاق مسمى** بشكل ديناميكي بناءً على إدخال المستخدم، غلف الاستدعاء داخل كتلة `try/catch` كما فعلنا مع اسم “Sales” المتعارض. معالجة الاستثناء تمنحك طريقة نظيفة لإبلاغ المستخدم بأن الاسم غير متاح.

---

## إنشاء مصنف Excel في Java

قبل أن تتمكن من *تعيين اسم جدول* أو *إضافة نطاق مسمى*، يجب أولًا **إنشاء مصنف Excel في Java**. السطر `Workbook workbook = new Workbook();` يقوم بذلك بالضبط. تحت الغطاء، تقوم Aspose.Cells بإنشاء تمثيل في الذاكرة لملف `.xlsx`، يمكنك لاحقًا حفظه على القرص أو بثه إلى عميل.

إذا كنت تستخدم Maven، أضف الاعتماد إلى ملف `pom.xml` الخاص بك:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version>
    <classifier>jdk17</classifier>
</dependency>
```

يمكن لمستخدمي Gradle استخدام:

```gradle
implementation 'com.aspose:aspose-cells:23.12:jdk17'
```

بمجرد أن تكون المكتبة على مسار الفئة (classpath)، يعمل باقي الكود تمامًا كما هو موضح سابقًا. لا تحتاج إلى أي إعداد إضافي.

---

## المشكلات الشائعة عند تعيين أسماء الجداول

| المشكلة | لماذا يحدث | كيفية التجنب |
|---------|------------|--------------|
| **تعارض الاسم مع جدول** | إضافة اسم على مستوى المصنف يتطابق مع معرف جدول موجود. | دائمًا استعلم `workbook.getNames().contains(name)` *أو* امسك الاستثناء كما هو موضح. |
| **استخدام أحرف غير صالحة** | لا يمكن لأسماء Excel أن تحتوي على مسافات، علامات ترقيم (باستثناء `_`)، أو أن تبدأ برقم. | استخدم أحرفًا أبجدية رقمية وشرطات سفلية؛ ابدأ بحرف. |
| **نسيان تمكين علامة الجدول** | الوسيط الثاني للطريقة `add` (`true`) يخبر Aspose.Cells بأن النطاق يجب أن يُعامل كجدول. إذا استخدمت `false`، يصبح `setName` بلا معنى. | حافظ على القيمة `true` عندما تريد جدولًا فعليًا. |
| **تحديد أسماء الأوراق بشكل ثابت** | إذا تم إعادة تسمية الورقة لاحقًا، قد تتعطل صيغ النطاقات. | استخدم فهرس الورقة (`workbook.getWorksheets().get(0)`) أو استخرج الاسم ديناميكيًا (`sheet.getName()`). |

بمراعاة هذه النقاط، نادراً ما ستواجه أخطاء *كيفية إضافة نطاق مسمى* التي تُربك المبتدئين.

---

## التحقق من النتيجة – ما المتوقع

بعد تشغيل الشيفرة النموذجية، افتح ملف **SetTableNameDemo.xlsx** المُنشأ:

1. **Sheet1** يعرض جدولًا منسقًا بعنوان **Sales**. يمكنك النقر على أي خلية داخل الجدول وستظهر شريط أدوات Table Tools.  
2. في **Formulas → Name Manager**، ستجد مدخلين:
   - **Sales** (النوع: Table) – هذا هو *تعيين اسم الجدول* الذي أنشأناه.  
   - **TotalSales** (النوع: Workbook) – هذا هو *إضافة نطاق مسمى* الذي يشير إلى عمود الكمية.  
3. جرّب كتابة `=SUM(TotalSales)` في أي خلية؛ سيقوم Excel بجمع القيم بشكل صحيح، مما يثبت أن النطاق المسمى يعمل.

إذا حاولت إضافة نطاق مسمى آخر باسم “Sales”، ستظهر رسالة التعارض في وحدة التحكم، وسيبقى المصنف دون تغيير—تمامًا كما أوضحنا.

---

## الخطوات التالية والمواضيع ذات الصلة

- **توسيع الجدول ديناميكيًا:** تعلّم *كيفية إنشاء جدول* ينمو تلقائيًا عند إضافة صفوف (`Table.expand()`).  
- **تنسيق الجداول:** طبّق أنماط الجداول المدمجة (`salesTable.setStyleType(StyleType.TABLE_STYLE_MEDIUM_1)`) للحصول على مظهر أنيق.  
- **استخدام النطاقات المسمَّاة في الصيغ:** دمج *إضافة نطاق مسمى* مع صيغ Excel مثل `VLOOKUP`، `INDEX/MATCH`، أو مصادر بيانات المخططات.  
- **التصدير إلى PDF:** بمجرد تعيين الجدول والنطاقات المسمَّاة، يمكنك تحويل المصنف إلى PDF فورًا باستخدام `workbook.save("output.pdf", SaveFormat.PDF)`.  
- **نصائح الأداء:** بالنسبة لمجموعات البيانات الكبيرة، أعد استخدام كائنات `Style` واكتب الخلايا على دفعات لتقليل استهلاك الذاكرة.  

كل من هذه المواضيع يبني على الأساس الذي لديك الآن—*تعيين اسم جدول* و*إضافة نطاق مسمى*.

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شيفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [كيفية تنفيذ نطاق مسمى بنطاق مصنف في Aspose.Cells Java لإدارة بيانات Excel محسّنة](/cells/english/java/tables-structured-references/implement-named-range-workbook-scope-aspose-cells-java/)
- [كيفية تعيين تعليقات على كائنات قائمة Excel باستخدام Aspose.Cells for Java | دليل خطوة بخطوة](/cells/english/java/comments-annotations/aspose-cells-java-set-comments-excel-list-objects/)
- [كيفية تحديث مصدر جدول محوري في Excel باستخدام Aspose.Cells for Java: دليل شامل](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}