---
category: general
date: 2026-06-30
description: تسمح لك صيغ المصفوفات الديناميكية في جافا بإنشاء جداول إكسل قوية. تعلم
  كيفية إنشاء مصنف إكسل باستخدام جافا وحساب جميع الصيغ بسرعة.
draft: false
keywords:
- dynamic array formulas
- calculate all formulas
- use lambda formula
- use expand function
- create excel workbook java
language: ar
og_description: تُبسِّط صيغ المصفوفات الديناميكية في جافا أتمتة إكسل. يوضح هذا الدليل
  كيفية إنشاء مصنف إكسل باستخدام جافا، واستخدام دالة التوسيع، وصيغة لامدا، وحساب جميع
  الصيغ.
og_title: صيغ المصفوفات الديناميكية في جافا – إنشاء دفتر عمل وحساب الصيغ
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Dynamic array formulas in Java let you build powerful Excel sheets.
    Learn to create Excel workbook Java and calculate all formulas quickly.
  headline: 'Dynamic Array Formulas in Java: Create Excel Workbook and Calculate All
    Formulas'
  type: TechArticle
tags:
- Java
- Excel
- Aspose.Cells
title: 'صيغ المصفوفات الديناميكية في جافا: إنشاء مصنف إكسل وحساب جميع الصيغ'
url: /ar/java/calculation-engine/dynamic-array-formulas-in-java-create-excel-workbook-and-cal/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# الصيغ الديناميكية للمصفوفات في جافا: إنشاء مصنف إكسل وحساب جميع الصيغ

هل تساءلت يومًا كيف تعمل **الصيغ الديناميكية للمصفوفات** عندما تقوم بأتمتة إكسل من جافا؟ لست وحدك—العديد من المطورين يواجهون صعوبة عندما يحتاجون إلى إدخال صيغ متقدمة مثل `EXPAND` أو `REDUCE` في مصنف دون فتح إكسل نفسه.

الأخبار السارة؟ ببضع أسطر من كود جافا يمكنك **إنشاء مصنف إكسل جافا**، وإدراج تلك الدوال الحديثة للمصفوفات، ثم **حساب جميع الصيغ** دفعة واحدة. في هذا الدرس سنستعرض كل خطوة، نشرح *لماذا* كل جزء مهم، ونزودك بمثال كامل قابل للتنفيذ يمكنك نسخه ولصقه مباشرةً في مشروعك.

## ما ستتعلمه

- كيفية إنشاء مصنف إكسل جديد باستخدام جافا (نعم، دون الحاجة إلى واجهة إكسل).  
- آلية عمل دالة `EXPAND` وكيفية تحويل نطاق بسيط إلى مصفوفة ديناميكية.  
- كيفية **استخدام صيغة لامبدا** مع `REDUCE` للتجميعات المخصصة.  
- إضافة الدوال المثلثية والزاوية الزائدية (`COT`, `COTH`) التي ينسى الكثيرون وجودها في مجموعة صيغ إكسل.  
- السطر الواحد الذي تحتاجه **لحساب جميع الصيغ** بحيث يعكس المصنف أحدث النتائج.  

> **المتطلبات المسبقة:** Java 8+ (لدعم لامبدا)، مكتبة Aspose.Cells for Java، وفهم أساسي لصيغ إكسل. لا توجد تبعيات أخرى مطلوبة.

## الصيغ الديناميكية للمصفوفات: إعداد المصنف

أولًا وقبل كل شيء—لنحصل على كائن مصنف على الطاولة. فئة `Workbook` من Aspose.Cells هي نقطة الدخول الخاصة بك؛ فكر فيها كقماش فارغ حيث ستعيش كل صيغة مصفوفة ديناميكية.

```java
import com.aspose.cells.*;

public class DynamicArrayDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook and grab the first worksheet
        Workbook workbook = new Workbook();                     // creates an empty .xlsx in memory
        Worksheet worksheet = workbook.getWorksheets().get(0); // default sheet is Sheet1
```

*لماذا هذا مهم:* إنشاء مصنف برمجيًا يمنحك تحكمًا كاملًا في تنسيق الملف، وإعدادات الثقافة،—والأهم من ذلك—تقييم الصيغ دون الحاجة إلى لمس القرص.

## استخدام دالة EXPAND لتوسيع النطاقات

دالة `EXPAND` هي إجابة إكسل على مفهوم “التسرب” لنطاق إلى مساحة أكبر بناءً على الحجم الذي تحدده. إنها مثالية عندما قد يتغير طول البيانات المصدرية أثناء التشغيل.

```java
        // Step 2: Add a formula that expands B1:B3 into a 5‑row, 1‑column array
        worksheet.getCells().get("A1").setFormula("=EXPAND(B1:B3,5,1)");
```

*شرح:*  
- `B1:B3` هو النطاق المصدر.  
- `5` يخبر إكسل بإنتاج خمس صفوف، حتى إذا كان المصدر أقصر.  
- `1` يفرض عمودًا واحدًا.

عند حساب **جميع الصيغ** لاحقًا، ستكون النتيجة في `A1` تسربًا عموديًا لخمس قيم، مع تعبئة فراغات إذا لزم الأمر.

## تطبيق صيغة LAMBDA مع REDUCE

إذا أردت يومًا جمع عمود ولكنك تحتاج أيضًا إلى مُجمع مخصص، فإن `REDUCE` مع **صيغة لامبدا** هو الحل. يبدو التركيب غير مألوف في البداية، لكنه مجرد طريقة جافا لإدراج دالة مجهولة صغيرة داخل صيغة إكسل.

```java
        // Step 3: Add a REDUCE formula that sums the values in B1:B5
        worksheet.getCells().get("A2").setFormula(
            "=REDUCE(0,B1:B5,LAMBDA(a,b,a+b))"
        );
```

*لماذا نستخدمه؟*  
- `0` هو البذرة الأولية (المجموع الابتدائي).  
- `B1:B5` هو المصفوفة التي نُطبق عليها العملية.  
- `LAMBDA(a,b,a+b)` يعني “خذ المُجمع `a` والعنصر التالي `b`، وأرجع مجموعهما.”  

يمكنك استبدال `a+b` بأي منطق مخصص—متوسط، أقصى قيمة، أو حتى دمج نصوص—مما يجعل `REDUCE` وحدة بناء متعددة الاستخدامات.

## إضافة الدوال المثلثية (COT, COTH)

يأتي إكسل مع مجموعة قليلة من الدوال المثلثية التي غالبًا ما تُهمل. إليك كيفية إدراج ظل جيبي بسيط (cotangent) وقريبه الزاوي الزائد (hyperbolic) في الورقة.

```java
        // Step 4: COT of π/4 (equals 1)
        worksheet.getCells().get("A3").setFormula("=COT(PI()/4)");

        // Step 5: COTH of 2 (hyperbolic cotangent)
        worksheet.getCells().get("A4").setFormula("=COTH(2)");
```

*نصيحة:* هذه الدوال تحترم تلقائيًا وضع حساب المصنف، لذا لا تحتاج إلى كود إضافي لتحويل الدرجات إلى راديان—`PI()` يقوم بالعمل الشاق.

## حساب جميع الصيغ في المصنف

الآن بعد وضع الصيغ، نحتاج إلى **حساب جميع الصيغ** حتى تحتوي الخلايا على قيم فعلية بدلاً من مجرد نص الصيغة. تجعل مكتبة Aspose.Cells ذلك من خلال استدعاء طريقة واحدة.

```java
        // Step 6: Force evaluation of every formula in the workbook
        workbook.calculateFormula();

        // Optional: Save to disk to see the result
        workbook.save("DynamicArrayDemo.xlsx");
    }
}
```

*ماذا يحدث خلف الكواليس؟* تقوم المكتبة بزيارة كل خلية، تحل الاعتمادات، وتُسرب نتائج المصفوفة حيث يلزم. إذا كنت تتعامل مع أوراق ضخمة، يمكنك تعديل خيارات الحساب للأداء، لكن الإعداد الافتراضي يعمل بشكل ممتاز لمعظم السيناريوهات.

## مثال كامل يعمل (جاهز للنسخ‑اللصق)

فيما يلي البرنامج الكامل، جاهز لتدمجه في بيئة التطوير المتكاملة. يتضمن الاستيرادات، طريقة `main`، واستدعاء `save` النهائي حتى تتمكن من فتح الملف الناتج في إكسل ورؤية التسربات.

```java
import com.aspose.cells.*;

public class DynamicArrayDemo {
    public static void main(String[] args) throws Exception {
        // Create workbook and get first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Populate source data for demonstration
        worksheet.getCells().get("B1").putValue(10);
        worksheet.getCells().get("B2").putValue(20);
        worksheet.getCells().get("B3").putValue(30);
        worksheet.getCells().get("B4").putValue(40);
        worksheet.getCells().get("B5").putValue(50);

        // EXPAND: spill B1:B3 into a 5‑row array
        worksheet.getCells().get("A1").setFormula("=EXPAND(B1:B3,5,1)");

        // REDUCE with LAMBDA: sum B1:B5
        worksheet.getCells().get("A2").setFormula("=REDUCE(0,B1:B5,LAMBDA(a,b,a+b))");

        // Trig functions
        worksheet.getCells().get("A3").setFormula("=COT(PI()/4)");
        worksheet.getCells().get("A4").setFormula("=COTH(2)");

        // Evaluate everything
        workbook.calculateFormula();

        // Save the file for inspection
        workbook.save("DynamicArrayDemo.xlsx");
    }
}
```

**الناتج المتوقع عند فتح `DynamicArrayDemo.xlsx`:**

| A (النتيجة) | B (المصدر) |
|------------|-----------|
| 10         | 10 |
| 20         | 20 |
| 30         | 30 |
| (فارغ)    | 40 |
| (فارغ)    | 50 |
| 150 (المجموع)  |   |
| 1 (cot)    |   |
| 1.0373… (coth) | |

*لاحظ كيف أن `A1` تُسرب خمس صفوف، رغم أن المصدر كان يحتوي على ثلاث قيم فقط. هذه هي قوة **الصيغ الديناميكية للمصفوفات**.*

## الأخطاء الشائعة & نصائح احترافية

- **لا تنس ضبط وضع الحساب** إذا كنت قد عطلت الحساب التلقائي في مكان آخر؛ وإلا فإن `calculateFormula()` لن يفعل شيئًا.  
- **تصادمات تسرب المصفوفة:** إذا كان خلية أخرى تحتل بالفعل نطاق التسرب، سيُرجع إكسل خطأ `#SPILL!`. في الكود، يمكنك مسح المنطقة المستهدفة مسبقًا باستخدام `worksheet.getCells().clear(0, 0, maxRow, maxColumn)`.  
- **غموض صياغة لامبدا:** دالة `LAMBDA` تتوقع معلمات مفصولة بفواصل، وليس بفواصل منقوطة. إذا فاتك فاصلة، سيفشل تحليل الصيغة بالكامل.  
- **نصيحة أداء:** عند العمل مع آلاف الصفوف، استدعِ `workbook.getSettings().setCalculateFormulaOnOpen(false)` قبل إدخال البيانات بالجملة، ثم أعد تمكينه قبل استدعاء `calculateFormula()` النهائي.

## الخطوات التالية

الآن بعد أن أتقنت **الصيغ الديناميكية للمصفوفات**، فكر في استكشاف:

- **`FILTER`** و **`SORT`** لتشكيل البيانات في الوقت الفعلي.  
- **`SEQUENCE`** لإنشاء مصفوفات رقمية دون أي نطاق مصدر.  
- استخدام **النطاقات المسماة** مع `EXPAND` للحصول على صيغ أنظف وقابلة لإعادة الاستخدام.  

كل هذه تبني على نفس المفاهيم التي غطيناها—فقط استبدل سلسلة الصيغة ودع Aspose.Cells تقوم بالعمل الشاق.

## الخلاصة

في هذا الدليل أظهرنا بالضبط كيفية **create Excel workbook Java**،

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مصدر يتضمن أمثلة كود كاملة قابلة للتنفيذ مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [إنشاء مصنف إكسل باستخدام Aspose.Cells في جافا: دليل خطوة بخطوة](/cells/english/java/getting-started/create-excel-workbook-aspose-cells-java/)
- [حساب صيغ إكسل جافا: تحسين باستخدام Aspose.Cells](/cells/english/java/calculation-engine/optimize-excel-aspose-cells-java-calculation-chains/)
- [إتقان صيغ المصفوفات في إكسل مع Aspose.Cells جافا: تبسيط الحسابات والتنسيق](/cells/english/java/formulas-functions/aspose-cells-java-array-formulas-custom-calculations/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}