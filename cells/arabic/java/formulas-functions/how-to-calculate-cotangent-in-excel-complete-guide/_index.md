---
category: general
date: 2026-06-27
description: كيفية حساب القاطع في Excel باستخدام الصيغ. تعلّم كيفية إعداد الصيغة،
  وكيفية استخدام EXPAND، وإتقان صيغة المصفوفة الديناميكية في Excel.
draft: false
keywords:
- how to calculate cotangent
- how to set formula
- how to use expand
- excel dynamic array formula
- add expand function
language: ar
og_description: كيفية حساب الظل المقلوب في Excel مع مثال واضح. يوضح هذا الدرس كيفية
  إعداد الصيغة، واستخدام EXPAND، والعمل مع صيغة المصفوفة الديناميكية في Excel.
og_title: كيفية حساب القاطع في إكسل – دليل خطوة بخطوة
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: How to calculate cotangent in Excel using formulas. Learn how to set
    formula, how to use EXPAND, and master the excel dynamic array formula.
  headline: How to Calculate Cotangent in Excel – Complete Guide
  type: TechArticle
- description: How to calculate cotangent in Excel using formulas. Learn how to set
    formula, how to use EXPAND, and master the excel dynamic array formula.
  name: How to Calculate Cotangent in Excel – Complete Guide
  steps:
  - name: '**Workbook creation** – `new Workbook()` gives us a fresh Excel file in
      memory.'
    text: '**Workbook creation** – `new Workbook()` gives us a fresh Excel file in
      memory.'
  - name: '**Source data** – We fill `A2:A5` with numbers 1‑4; these values will be
      expanded later.'
    text: '**Source data** – We fill `A2:A5` with numbers 1‑4; these values will be
      expanded later.'
  - name: '**How to set formula** – `setFormula` attaches the `EXPAND` expression
      to `A1`. The function tells Excel to spill a 5‑row‑by‑2‑column block based on
      the source range.'
    text: '**How to set formula** – `setFormula` attaches the `EXPAND` expression
      to `A1`. The function tells Excel to spill a 5‑row‑by‑2‑column block based on
      the source range.'
  - name: '**How to calculate cotangent** – The `COT` call uses `PI()/4` (45°). This
      is the core answer to *how to calculate cotangent* in Excel.'
    text: '**How to calculate cotangent** – The `COT` call uses `PI()/4` (45°). This
      is the core answer to *how to calculate cotangent* in Excel.'
  - name: '**Recalculation** – `wb.calculateFormula()` forces Aspose.Cells to evaluate
      all formulas, just like pressing **F9** in the UI.'
    text: '**Recalculation** – `wb.calculateFormula()` forces Aspose.Cells to evaluate
      all formulas, just like pressing **F9** in the UI.'
  - name: '**Result output** – We loop through the spill range to prove that `EXPAND`
      actually created a dynamic array.'
    text: '**Result output** – We loop through the spill range to prove that `EXPAND`
      actually created a dynamic array.'
  - name: '**Saving** – The final workbook, `CotangentDemo.xlsx`, can be opened in
      Excel to see the formulas live.'
    text: '**Saving** – The final workbook, `CotangentDemo.xlsx`, can be opened in
      Excel to see the formulas live.'
  type: HowTo
tags:
- Excel
- Formulas
- Java
- Aspose.Cells
title: كيفية حساب القاطع في إكسل – دليل كامل
url: /ar/java/formulas-functions/how-to-calculate-cotangent-in-excel-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية حساب الظل المقلوب (Cotangent) في Excel – دليل كامل

هل تساءلت يومًا **كيف تحسب الظل المقلوب في Excel** دون الحاجة إلى آلة حاسبة علمية؟ لست وحدك. سواء كنت تبني نموذجًا ماليًا، أو ورقة عمل في الفيزياء، أو مجرد محب للعب بالثلثيات، فإن إتقان دالة الظل المقلوب في Excel يمكن أن يوفر لك الكثير من الوقت.

في هذا الدرس سنظهر أيضًا **كيفية تعيين الصيغة** برمجيًا باستخدام مكتبة Aspose.Cells للغة Java، ونستعرض **كيفية استخدام EXPAND**، ونشرح لماذا ميزة **صيغ المصفوفة الديناميكية في Excel** مهمة. في النهاية ستحصل على مثال كامل قابل للتنفيذ يضيف دالة EXPAND، يحسب الظل المقلوب، ويطبع النتائج—كل ذلك في أقل من عشر أسطر من الشيفرة.

## ما ستتعلمه

- بنية دالة `COT` في Excel ولماذا هي أسرع طريقة للحصول على قيم الظل المقلوب.  
- كيفية **تعيين الصيغة** في خلية ورقة عمل عبر كود Java.  
- الآلية وراء **كيفية استخدام EXPAND** للمصفوفات الديناميكية.  
- متى وكيف **تضيف دالة EXPAND** إلى المصنف لحساب نطاقات الانسكاب.  
- نصائح لتصحيح الأخطاء الشائعة في سلوك **صيغ المصفوفة الديناميكية في Excel**.

> **المتطلبات المسبقة:**  
> - تثبيت Java 8+ .  
> - Aspose.Cells for Java (نسخة تجريبية مجانية أو نسخة مرخصة).  
> - إلمام أساسي بدوال Excel.

إذا كان لديك هذه المتطلبات، فلنبدأ.

---

## كيفية حساب الظل المقلوب في Excel

تُعيد الدالة `COT` الظل المقلوب لزاوية تُعطى بالراديان. صيغتها بسيطة:

```excel
=COT(number)
```

حيث *number* هو الزاوية بالراديان. بالنسبة للزاوية الكلاسيكية 45° (π/4 راديان)، النتيجة هي `1` لأن `cot(π/4) = 1`.

### لماذا نستخدم `COT` بدلاً من الحساب اليدوي؟

يمكنك كتابة `=1/TAN(angle)` لكن ذلك يجبر Excel على تقييم دالتين ويُدخل احتمال حدوث خطأ قسمة على صفر عندما تكون الزاوية مضاعفًا لـ π. `COT` مدمجة، تتعامل مع الحالات الحدية، وأسهل في القراءة—خاصةً عندما تشارك الورقة مع زملائك.

---

## خطوة بخطوة: تعيين الصيغة باستخدام Java (How to Set Formula)

فيما يلي **برنامج Java كامل قابل للتنفيذ** ينشئ مصنفًا، يضيف صيغة `COT` إلى الخلية `B1`، ويقيمها. سنضيف أيضًا دالة `EXPAND` لتوضيح مصفوفة ديناميكية.

```java
import com.aspose.cells.*;

public class CotangentDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create a new workbook and get the first worksheet
        Workbook wb = new Workbook();
        Worksheet ws = wb.getWorksheets().get(0);
        Cells cells = ws.getCells();

        // 2️⃣ Populate source data for EXPAND (A2:A5)
        for (int i = 0; i < 4; i++) {
            cells.get(i + 1, 0).putValue(i + 1); // A2=1, A3=2, A4=3, A5=4
        }

        // 3️⃣ **How to set formula** – Apply EXPAND to cell A1
        //    EXPAND(source, rows, columns) creates a spill range.
        cells.get("A1").setFormula("=EXPAND(A2:A5,5,2)");

        // 4️⃣ **How to calculate cotangent** – Apply COT to cell B1
        //    COT(PI()/4) = 1 because cot(45°) = 1
        cells.get("B1").setFormula("=COT(PI()/4)");

        // 5️⃣ Recalculate the workbook so formulas resolve
        wb.calculateFormula();

        // 6️⃣ Retrieve and print results
        System.out.println("EXPAND result (A1 spill range):");
        for (int r = 0; r < 5; r++) {
            for (int c = 0; c < 2; c++) {
                System.out.print(cells.get(r, c).getStringValue() + "\t");
            }
            System.out.println();
        }

        System.out.println("\nCotangent of π/4 (B1): " + cells.get("B1").getStringValue());

        // 7️⃣ Save the workbook (optional)
        wb.save("CotangentDemo.xlsx");
    }
}
```

#### شرح الشيفرة

1. **إنشاء المصنف** – `new Workbook()` يمنحنا ملف Excel جديد في الذاكرة.  
2. **البيانات المصدرية** – نملأ النطاق `A2:A5` بالأرقام 1‑4؛ هذه القيم ستُوسّع لاحقًا.  
3. **كيفية تعيين الصيغة** – `setFormula` يربط تعبير `EXPAND` بالخلية `A1`. الدالة تخبر Excel بإنشاء كتلة 5 صفوف × 2 عمود بناءً على النطاق المصدر.  
4. **كيفية حساب الظل المقلوب** – استدعاء `COT` يستخدم `PI()/4` (45°). هذه هي الإجابة الأساسية على سؤال *كيف تحسب الظل المقلوب* في Excel.  
5. **إعادة الحساب** – `wb.calculateFormula()` يجبر Aspose.Cells على تقييم جميع الصيغ، تمامًا كما لو ضغطت **F9** في الواجهة.  
6. **إخراج النتيجة** – نمر عبر نطاق الانسكاب لإثبات أن `EXPAND` أنشأت مصفوفة ديناميكية فعلًا.  
7. **الحفظ** – المصنف النهائي، `CotangentDemo.xlsx`، يمكن فتحه في Excel لرؤية الصيغ مباشرة.

> **نصيحة محترف:** إذا كنت تستخدم نسخة من Excel تدعم المصفوفات الديناميكية (Office 365 أو Excel 2021+)، فإن دالة `EXPAND` ستقوم تلقائيًا بـ “الانسكاب” إلى الخلايا المجاورة. الإصدارات القديمة ستعيد خطأ `#NAME?`—لذا تحقق دائمًا من نسخة Excel قبل **إضافة دالة EXPAND**.

---

## كيفية استخدام EXPAND – فهم صيغ المصفوفة الديناميكية في Excel

`EXPAND` هي جزء من عائلة **المصفوفات الديناميكية** في Excel، تم تقديمها لاستبدال تعريفات النطاقات اليدوية المرهقة. توقيعها:

```excel
=EXPAND(array, rows, columns, [pad_with])
```

- **array** – النطاق المصدر الذي تريد توسيعه.  
- **rows** – عدد الصفوف لنطاق الانسكاب (استخدم `0` للحفاظ على الارتفاع الأصلي).  
- **columns** – عدد الأعمدة لنطاق الانسكاب (استخدم `0` للحفاظ على العرض الأصلي).  
- **pad_with** – قيمة اختيارية لملء الخلايا الفارغة.

عند كتابة `=EXPAND(A2:A5,5,2)`، يقرأ Excel العمود المكوّن من أربعة صفوف ويمده إلى مصفوفة 5×2، مع تعبئة الخلايا الإضافية بـ `0` افتراضيًا. النتيجة “تنسكب” إلى الخلايا المجاورة، مت behaving كـ **صيغ المصفوفة الديناميكية في Excel**.

### متى نضيف دالة EXPAND

- **تطبيع البيانات** – لديك عمود واحد وتحتاج إلى مصفوفة لرسم بياني.  
- **التحضير لدوال مصفوفة أخرى** – دوال مثل `FILTER` أو `SORT` تقبل نطاقات الانسكاب مباشرة.  
- **تجنب النسخ اليدوي** – المصفوفات الديناميكية تتكيف تلقائيًا عندما تتغير البيانات المصدرية.

---

## المشكلات الشائعة وكيفية حلها

| المشكلة | السبب | الحل |
|-------|----------------|-----|
| خطأ `#SPILL!` | الخلايا المستهدفة تحتوي على بيانات مسبقة | امسح المنطقة أو انقل الصيغة إلى خلية فارغة. |
| خطأ `#NAME?` على `EXPAND` | نسخة Excel لا تدعم المصفوفات الديناميكية | قم بالترقية إلى Office 365/Excel 2021 أو استخدم بديلًا مثل `INDEX`. |
| خطأ `#DIV/0!` من `COT` | الزاوية تساوي `0` أو `π` (الظل المقلوب غير معرف) | غلف الصيغة: `=IF(MOD(angle,PI())=0,NA(),COT(angle))`. |
| الصيغة لا تتحدث في Java | لم يتم استدعاء `Workbook.calculateFormula()` | تأكد من استدعاء `calculateFormula()` بعد تعيين جميع الصيغ. |

---

## توسيع المثال – طرق إضافية لحساب الظل المقلوب

إذا كنت تحتاج الظل المقلوب لقيمة بالدرجات، حوّلها أولًا:

```java
cells.get("C1").setFormula("=COT(RADIANS(30))"); // cot(30°) ≈ 1.732
```

أو، اجمع `COT` مع دوال مصفوفة أخرى:

```excel
=MAP(A2:A5, LAMBDA(x, COT(RADIANS(x))))
```

دالة `MAP` (متوفرة في إصدارات Excel الأحدث) تطبق `COT` على كل عنصر في نطاق، وتعيد مصفوفة ديناميكية من قيم الظل المقلوب—مثالية للحسابات الجماعية.

---

## ملخص المثال الكامل القابل للتنفيذ

فيما يلي **ملف المصدر بالكامل** يمكنك نسخه ولصقه في بيئة التطوير الخاصة بك. لا توجد تبعيات مخفية، كل ما تحتاجه موجود هنا.

```java
import com.aspose.cells.*;

public class CotangentDemo {
    public static void main(String[] args) throws Exception {
        Workbook wb = new Workbook();
        Worksheet ws = wb.getWorksheets().get(0);
        Cells cells = ws.getCells();

        // Populate source data for EXPAND
        for (int i = 0; i < 4; i++) {
            cells.get(i + 1, 0).putValue(i + 1);
        }

        // Add EXPAND (how to use expand)
        cells.get("A1").setFormula("=EXPAND(A2:A5,5,2)");

        // Calculate cotangent (how to calculate cotangent)
        cells.get("B1").setFormula("=COT(PI()/4)");

        // Optional: cotangent of 30 degrees
        cells.get("C1").setFormula("=COT(RADIANS(30))");

        // Force evaluation
        wb.calculateFormula();

        // Print EXPAND spill range
        System.out.println("EXPAND spill (A1):");


## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [How to Use Excel IF Function](/cells/english/java/basic-excel-functions/how-to-use-excel-if-function/)
- [How to Set Excel Document Version Using Aspose.Cells for Java](/cells/english/java/workbook-operations/set-excel-version-aspose-cells-java/)
- [How to Set Language in Excel Files Using Aspose.Cells .NET for Multilingual Support](/cells/english/net/formulas-functions/specify-language-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}