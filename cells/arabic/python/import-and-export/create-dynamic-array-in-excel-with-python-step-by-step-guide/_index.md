---
category: general
date: 2026-06-21
description: إنشاء مصفوفة ديناميكية باستخدام بايثون ودالة SEQUENCE في إكسل. تعلم قراءة
  نتيجة الصيغة، وإعادة حساب صيغ إكسل، ورؤية مثال على دالة SEQUENCE في إكسل.
draft: false
keywords:
- create dynamic array
- sequence function excel
- read formula result
- recalculate excel formulas
- excel sequence example
language: ar
og_description: إنشاء مصفوفة ديناميكية في إكسل باستخدام بايثون. يوضح هذا الدرس كيفية
  استخدام دالة SEQUENCE، وإعادة حساب صيغ إكسل، وقراءة نتيجة الصيغة.
og_title: إنشاء مصفوفة ديناميكية في إكسل باستخدام بايثون – دليل كامل
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Create dynamic array using Python and the SEQUENCE function in Excel.
    Learn to read formula result, recalculate Excel formulas, and see an Excel SEQUENCE
    example.
  headline: Create Dynamic Array in Excel with Python – Step‑by‑Step Guide
  type: TechArticle
tags:
- excel
- python
- xlwings
- dynamic arrays
title: إنشاء مصفوفة ديناميكية في إكسل باستخدام بايثون – دليل خطوة بخطوة
url: /ar/python/import-and-export/create-dynamic-array-in-excel-with-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء مصفوفة ديناميكية في Excel باستخدام Python – دليل كامل

هل تساءلت يومًا كيف يمكنك **إنشاء مصفوفة ديناميكية** في Excel دون مغادرة سكريبت Python الخاص بك؟ لست الوحيد. سواءً كنت تقوم بأتمتة تقرير شهري أو تبني محرك بيانات خفيف الوزن، فإن القدرة على إدراج صيغة `SEQUENCE` في مصنف، وإعادة الحساب، وسحب نطاق الانسكاب مرةً أخرى إلى Python تُغيّر قواعد اللعبة.

في هذا الدرس سنستعرض مثالًا عمليًا **excel sequence example**، ونوضح لك كيفية **قراءة نتيجة الصيغة**، ونشرح أفضل طريقة لـ **إعادة حساب صيغ Excel** بعد حقن منطق جديد. في النهاية ستحصل على سكريبت مستقل يمكنك نسخه‑ولصقه، تشغيله، وتكييفه وفق احتياجاتك.

## ما ستتعلمه

- كيف تعمل دالة `SEQUENCE` ولماذا هي مثالية لإنشاء المصفوفات.
- الفرق بين قيمة خلية عادية وعنوان نطاق الانسكاب.
- استخدام `wb.calculate_formula()` (أو ما يعادله) لإجبار Excel على تقييم الصيغ الجديدة.
- استخراج عنوان المصفوفة الديناميكية باستخدام `ANCHORARRAY`.
- مثال كامل وقابل للتنفيذ بلغة Python يمكنك إدراجه في أي مشروع.

لا تحتاج إلى أي خبرة مسبقة في محرك المصفوفات الديناميكية الجديد في Excel—فقط إلمام أساسي بـ Python ومكتبة مثل **xlwings** التي يمكنها التواصل مع Excel.

---

## كيفية إنشاء مصفوفة ديناميكية باستخدام SEQUENCE في Excel عبر Python

الخطوة الأولى هي كتابة صيغة **dynamic array** مباشرةً في خلية ورقة العمل. في Excel الحديث، يمكن لدالة `SEQUENCE` إنشاء مصفوفة من الأرقام فورًا. إليك الصيغة التي سنستخدمها:

```python
# Step 1: Write a dynamic array formula that generates a 3×2 matrix starting at 10 with step 5
ws.cells["A1"].formula = "=SEQUENCE(3,2,10,5)"   # Returns a 3×2 array
```

**لماذا `SEQUENCE`؟**  
فكر فيها كدالة `range()` المدمجة في Excel للجداول. تسمح لك بتحديد عدد الصفوف، الأعمدة، قيمة البداية، والزيادة—كل ذلك في سطر واحد مرتب. في حالتنا نطلب 3 صفوف و2 عمود، بدءًا من 10 وزيادة قدرها 5، مما ينتج:

|   | A | B |
|---|---|---|
|1|10|15|
|2|20|25|
|3|30|35|

لأن الصيغة موجودة في `A1`، يقوم Excel تلقائيًا بـ “انسكاب” النتيجة إلى الخلايا المجاورة `A1:B3`. هذا الانسكاب هو ما سنسترجعه لاحقًا.

---

## استخدام دالة SEQUENCE في Excel – مثال سريع على Excel Sequence

إذا فتحت Excel يدويًا وكتبت `=SEQUENCE(3,2,10,5)` في خلية، سترى نفس المصفوفة تظهر فورًا. هذه الدالة هي جزء من محرك **dynamic array** في Excel الذي تم تقديمه في Office 365، مما يعني:

- لا حاجة لاستخدام Ctrl+Shift+Enter.
- يمكن للنتيجة أن تتوسع أو تتقلص تلقائيًا.
- يمكنك الإشارة إلى نطاق الانسكاب بالكامل باستخدام دوال مثل `@` أو `#`.

في Python، الاختلاف الوحيد هو أننا نعيّن الصيغة كسلسلة نصية إلى خاصية `.formula` للخلية. المكتبة تتولى الباقي.

---

## استرجاع عنوان نطاق الانسكاب باستخدام ANCHORARRAY

بمجرد إنشاء المصفوفة الديناميكية، غالبًا ما تحتاج إلى معرفة المكان الذي وضع فيه Excel القيم فعليًا. هنا يبرز دور `ANCHORARRAY`. فهو يُعيد عنوان الخلية العلوية اليسرى لنطاق الانسكاب—وهو بالضبط ما نحتاجه لقراءته مرةً أخرى في السكريبت.

```python
# Step 2: Retrieve the address of the spill range produced by the formula in A1
ws.cells["C1"].formula = "=ANCHORARRAY(A1)"      # Returns the address of the spill range
```

وضع هذه الصيغة في `C1` يعطينا سلسلة نصية مثل `"A1:B3"`. لاحظ أننا **نقرأ نتيجة الصيغة** كقيمة عادية، وليس كصيغة أخرى. هذه الحيلة الصغيرة تتجنب الحاجة إلى تحليل ورقة العمل يدويًا.

---

## إعادة حساب صيغ Excel وقراءة النتيجة

Excel لا يعيد الحساب دائمًا فورًا عندما تُحقن صيغة جديدة من سكريبت خارجي. لضمان أن المصنف يعكس أحدث التغييرات، نقوم بتحفيز عملية حساب صريحة.

```python
# Step 3: Recalculate all formulas in the workbook and read the result
wb.calculate_formula()               # Forces Excel to evaluate pending formulas
print(ws.cells["C1"].value)          # → "A1:B3"
```

**لماذا نستدعي `calculate_formula()`؟**  
إذا تخطيت هذه الخطوة، قد لا يزال `ws.cells["C1"].value` يُعيد `None` أو عنوانًا قديمًا لأن Excel لا يزال مشغولًا بتحديث شجرة الاعتماديات. من خلال فرض إعادة حساب نضمن أن **قراءة نتيجة الصيغة** تكون محدثة.

---

## السكريبت الكامل – من البداية إلى النهاية

فيما يلي مثال كامل وجاهز للتنفيذ يربط كل شيء معًا. يفترض أن لديك **xlwings** مثبتًا (`pip install xlwings`) وأن Excel متاح على جهازك.

```python
import xlwings as xw

def create_dynamic_array_example():
    # Open a new workbook (or attach to an existing one)
    wb = xw.Book()               # Creates a fresh Excel workbook
    ws = wb.sheets[0]            # Grab the first worksheet

    # 1️⃣ Write the SEQUENCE formula – this creates a 3×2 matrix starting at 10, step 5
    ws.cells["A1"].formula = "=SEQUENCE(3,2,10,5)"

    # 2️⃣ Use ANCHORARRAY to capture the spill range address in C1
    ws.cells["C1"].formula = "=ANCHORARRAY(A1)"

    # 3️⃣ Force Excel to recalculate so that the ANCHORARRAY result is current
    wb.calculate_formula()

    # 4️⃣ Read back the address – this is our **read formula result** step
    spill_address = ws.cells["C1"].value
    print(f"The dynamic array spills into: {spill_address}")

    # 5️⃣ Optionally, fetch the actual values from the spill range
    # xlwings can read a range by address, so we demonstrate that too
    data = ws.range(spill_address).value
    print("Matrix values:")
    for row in data:
        print(row)

    # Clean up – close without saving to keep the demo tidy
    wb.close(save=False)

if __name__ == "__main__":
    create_dynamic_array_example()
```

### النتيجة المتوقعة

```
The dynamic array spills into: A1:B3
Matrix values:
[10, 15]
[20, 25]
[30, 35]
```

تشغيل السكريبت سيفتح Excel، يحقن صيغة `SEQUENCE`، يعيد الحساب، ثم يطبع كلًا من عنوان الانسكاب والمصفوفة نفسها. لا حاجة للنقرات اليدوية.

---

## الأخطاء الشائعة والنصائح الاحترافية

- **المشكلة:** نسيان استدعاء `wb.calculate_formula()`.  
  *النتيجة:* يبقى `C1` فارغًا أو يظهر عنوانًا قديمًا.  
  *الحل:* دائمًا قم بتحفيز حساب بعد كتابة صيغ جديدة.

- **المشكلة:** استخدام نسخة قديمة من Excel لا تدعم دالة `SEQUENCE`.  
  *النتيجة:* خطأ `#NAME?`.  
  *الحل:* تأكد من أنك تستخدم Office 365 أو Excel 2021+.

- **نصيحة احترافية:** إذا كنت بحاجة إلى نطاق الانسكاب لمعالجة إضافية (مثل الرسم البياني)، يمكنك تمرير العنوان مباشرةً إلى `ws.range(spill_address)` كما هو موضح أعلاه.

- **نصيحة احترافية:** `ANCHORARRAY` يعمل مع أي مصفوفة ديناميكية، ليس فقط `SEQUENCE`. استبدلها بـ `=SORT(A2:A10)` أو `=FILTER(...)` وستحصل دائمًا على عنوان الانسكاب الصحيح.

- **حالة خاصة:** عندما تكون المنطقة المستهدفة مشغولة بالفعل، سيُرجع Excel خطأ `#SPILL!`. في هذه الحالة، إما قم بمسح نطاق الوجهة أولًا أو انقل الصيغة إلى خلية أخرى.

---

## توسيع المثال – ما التالي؟

الآن بعد أن عرفت كيفية **إنشاء مصفوفة ديناميكية**، **قراءة نتيجة الصيغة**، و**إعادة حساب صيغ Excel**، يمكنك استكشاف سيناريوهات أكثر تقدمًا:

- **بيانات مخطط ديناميكي** – إدخال نطاق الانسكاب كمصدر للمخطط والسماح للمخطط بالنمو تلقائيًا.
- **تنسيق شرطي** – تطبيق قواعد على نطاق الانسكاب باستخدام عنوانه.
- **مراجع عبر المصنفات** – كتابة مصفوفة ديناميكية في مصنف واحد وسحب البيانات إلى آخر عبر روابط `xlwings`.

كل من هذه يبني على المفاهيم الأساسية التي تم تغطيتها هنا، لذا لا تتردد في التجربة. الحد الوحيد هو خيالك (وربما الحد الأقصى للصفوف/الأعمدة في Excel).

---

## الخلاصة

لقد استعرضنا للتو سير عمل كامل لإنشاء صيغ **dynamic array** في Excel من خلال Python، واستخدام **دالة SEQUENCE**، واسترجاع نطاق الانسكاب باستخدام **ANCHORARRAY**، و**إعادة حساب صيغ Excel**، وأخيرًا **قراءة نتيجة الصيغة** مرةً أخرى في السكريبت الخاص بك. يوضح المثال القصير مدى قوة محرك المصفوفات الديناميكية الجديد في Excel عندما يُدمج مع أدوات الأتمتة مثل **xlwings**.

جرّبه في مشاريعك الخاصة، عدّل أبعاد المصفوفة، أو استبدل `SEQUENCE` بأي دالة ديناميكية أخرى. كلما ارتحت أكثر، ستجد أن أتمتة Excel تصبح ليست ممكنة فحسب، بل سهلة وممتعة.

هل لديك أسئلة أو ترغب في مشاركة كيفية توسيعك لهذا النمط؟ اترك تعليقًا أدناه، وتمنياتنا لك بالبرمجة السعيدة!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مصدر يتضمن أمثلة شاملة من الكود مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [معالجة البيانات باستخدام دالة المصفوفة في Excel](/cells/english/net/excel-formulas-and-calculation-options/processing-data-using-array-function/)
- [إنشاء مخططات خطية ديناميكية في Excel باستخدام Aspose.Cells لـ .NET: دليل خطوة بخطوة](/cells/english/net/charts-graphs/create-line-charts-excel-aspose-cells-dotnet/)
- [إنشاء مخططات Excel ديناميكية باستخدام Aspose.Cells Java: دليل شامل للمطورين](/cells/english/java/charts-graphs/aspose-cells-java-dynamic-excel-charts/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}