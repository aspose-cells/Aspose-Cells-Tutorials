---
category: general
date: 2026-06-08
description: إنشاء مثال بيثون لملف عمل إكسل يوضح كيفية استخدام لامدا في إكسل، جمع
  الصفوف باستخدام BYROW، وأتمتة الحسابات في بضع خطوات.
draft: false
keywords:
- create excel workbook python
- how to use lambda
- how to sum rows
- use lambda excel
language: ar
og_description: أنشئ دفتر عمل Excel باستخدام Python وتعلم كيفية استخدام الدالة lambda
  في Excel لجمع الصفوف بكفاءة باستخدام صيغ BYROW.
og_title: إنشاء دفتر عمل إكسل بايثون – دليل شامل
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Create Excel workbook Python example that shows how to use lambda in
    Excel, sum rows with BYROW, and automate calculations in a few steps.
  headline: Create Excel Workbook Python – Complete Guide with Lambda
  type: TechArticle
tags:
- python
- excel
- automation
title: إنشاء مصنف إكسل بايثون – دليل كامل مع لامدا
url: /ar/python/formulas-and-functions/create-excel-workbook-python-complete-guide-with-lambda/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء دفتر عمل Excel باستخدام بايثون – دليل شامل مع Lambda

هل تساءلت يومًا كيف تُنشئ سكريبتات **create Excel workbook Python** التي تُ automatis العمليات المملة للرقم؟ لست وحدك—العديد من المطورين يواجهون صعوبة عندما يحتاجون إلى توليد ورقة، وإدراج صيغة، ثم سحب النتائج مرة أخرى إلى الكود الخاص بهم.  

في هذا الدرس سنوضح أيضًا **كيفية استخدام lambda** في Excel، ونشرح **كيفية جمع الصفوف** باستخدام الدالة الحديثة `BYROW`، وسنقدم لك مثالًا متكاملًا يمكنك نسخه ولصقه وتشغيله اليوم.

## ما ستتعلمه

- إعداد دفتر عمل جديد من بايثون دون فتح Excel يدويًا.  
- ملء نطاق بمصفوفة أرقام 3 × 3.  
- إدراج صيغة `BYROW` التي تستفيد من **use lambda excel** لجمع كل صف.  
- إعادة حساب الورقة بحيث يتم تقييم الصيغة، ثم قراءة النتائج مرة أخرى إلى بايثون.  

بنهاية هذا الدليل ستحصل على سكريبت مستقل يمكنك تكييفه للفواتير، بطاقات الأداء، أو أي حالة تحتاج فيها إلى **sum rows** في الوقت الفعلي.

### المتطلبات المسبقة

- تثبيت Python 3.8+.  
- مكتبة `openpyxl` (أو `xlwings` إذا كنت تفضل نهجًا قائمًا على COM). سنستخدم `openpyxl` لأنها بايثون صافية وتعمل على جميع المنصات.  
- نسخة حديثة من Microsoft Excel (365 أو 2021) تدعم دالة `BYROW` وصيغ Lambda.  

ثبت المكتبة باستخدام:

```bash
pip install openpyxl
```

> **نصيحة احترافية:** إذا واجهت مشاكل أذونات على Windows، استخدم `python -m pip install --user openpyxl`.

---

## إنشاء دفتر عمل Excel باستخدام بايثون – تهيئة دفتر العمل

أول شيء نحتاجه هو كائن دفتر عمل جديد تمامًا يعيش في الذاكرة. مع `openpyxl` هذا سطر واحد:

```python
from openpyxl import Workbook

# Step 1: Create a new workbook and grab the first worksheet
wb = Workbook()
ws = wb.active   # .active is the first sheet by default
```

لماذا نستخدم `wb.active` بدلاً من الفهرسة `Worksheets[0]`؟ `openpyxl` تعرض الورقة النشطة مباشرة، وهذا أوضح ويتجنب بحثًا إضافيًا في القائمة. إذا احتجت يومًا للعمل مع أوراق متعددة، يمكنك دائمًا إضافتها باستخدام `wb.create_sheet(title="MySheet")`.

---

## ملء الورقة بالبيانات – مصفوفة بسيطة 3×3

بعد ذلك، نملأ الورقة بمصفوفة صغيرة. هذا يعكس مثال “جمع كل صف” الكلاسيكي ويحافظ على اختصار الكود.

```python
# Step 2: Define a 3×3 matrix of numbers
matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]

# Import the matrix into the worksheet starting at cell A1
for r_idx, row in enumerate(matrix, start=1):
    for c_idx, value in enumerate(row, start=1):
        ws.cell(row=r_idx, column=c_idx, value=value)
```

قد تتساءل لماذا نستخدم حلقة يدوية بدلاً من `ws.append()` أو `ws.values`. الحلقات الصريحة تمنحنا تحكمًا كاملًا في الخلية البداية وتسهّل تعديل الإزاحات لاحقًا—مفيد عندما تريد ترك صف أو عمود عنوان فارغ.

---

## كيفية استخدام Lambda في صيغ Excel

ميزة **use lambda excel** في Excel تتيح لك كتابة دوال مجهولة مباشرة في خلية. فكر فيها كـ `lambda` في بايثون ولكن داخل محرك الجدول. الصيغة هي:

```
=LAMBDA(parameter1, parameter2, …, calculation)
```

عند دمجها مع `BYROW`، يمكنك تطبيق تلك الدالة المجهولة على كل صف من نطاق، وإنتاج عمود من النتائج. هذا هو جوهر حيلة **how to sum rows**.

```python
# Step 3: Insert a BYROW formula that sums each row using a Lambda
ws["D1"] = "=BYROW(A1:C3, LAMBDA(r, SUM(r)))"
```

ما الذي يحدث في الخلفية؟

- `A1:C3` هو نطاق المصدر (مصفوتنا).  
- `LAMBDA(r, SUM(r))` يعرّف دالة مؤقتة تستقبل صفًا واحدًا (`r`) وتعيد مجموعه.  
- `BYROW` تشغّل تلك الدالة لكل **صف** وتفرّغ النتائج في العمود D، بدءًا من `D1`.  

نظرًا لأن `BYROW` هي دالة *مصفوفة ديناميكية*، يقوم Excel تلقائيًا بملء `D1:D3` بالمجاميع الثلاثة.

> **ملاحظة:** صيغ `BYROW` وLambda متاحة فقط في Excel 365/2021 وما بعده. إذا كنت تستخدم نسخة أقدم، سيتعين عليك العودة إلى صيغ `SUM` التقليدية أو VBA.

---

## كيفية جمع الصفوف باستخدام BYROW وLambda

الآن بعد أن الصيغة موجودة في الورقة، يجب أن نخبر Excel بحسابها. `openpyxl` نفسها لا تحسب الصيغ؛ فهي تقرأ/تكتب فقط. لتفعيل الحساب يمكننا إما:

1. حفظ دفتر العمل وفتحه في Excel (يدوي).  
2. استخدام محرك `xlwings` COM لإجبار إعادة الحساب (يتطلب تثبيت Excel).  

لحل بايثون صافي، سنستخدم `xlwings` فقط لخطوة الحساب—ولا شيء أكثر.

```python
import xlwings as xw

# Step 4: Recalculate the workbook so the BYROW formula is evaluated
# Save the workbook to a temporary file first
temp_path = "temp_workbook.xlsx"
wb.save(temp_path)

# Open the file with xlwings, force a calculation, then close
app = xw.App(visible=False)
book = app.books.open(temp_path)
book.api.CalculateFull()          # Full recalculation
book.save()
book.close()
app.quit()
```

لماذا لا نستدعي `wb.calculate()`؟ `openpyxl` لا تملك محركًا أصليًا، لذا نعتمد على Excel نفسه عبر `xlwings`. الحمل الزائد قليل للورقات الصغيرة ويعطينا النتيجة الدقيقة التي سيعرضها Excel.

---

## إعادة الحساب واسترجاع النتائج – سحب المجاميع إلى بايثون

أخيرًا، نقرأ النتائج المفرّغة من العمود D. `openpyxl` تجعل ذلك سهلًا:

```python
# Step 5: Load the recalculated workbook and grab the results
wb = Workbook()  # re‑open the saved file
wb = xw.Book(temp_path).api  # alternative: use xlwings again to read values

# Using xlwings to fetch the range values as a Python list
results = xw.Range('D1:D3').value
print(results)   # Expected output: [6, 15, 24]
```

إذا كنت تفضل البقاء داخل `openpyxl`، يمكنك قراءة الخلايا بعد إعادة حساب Excel:

```python
from openpyxl import load_workbook

wb = load_workbook(temp_path, data_only=True)  # data_only reads calculated values
ws = wb.active
results = [ws[f"D{row}"].value for row in range(1, 4)]
print(results)   # -> [6, 15, 24]
```

كلا الطريقتين تعطيان نفس القائمة `[6, 15, 24]`، مما يؤكد أن **how to sum rows** باستخدام `BYROW` + Lambda يعمل كما هو موضح.

---

## الحالات الخاصة والمشكلات الشائعة

| الحالة | ما يجب مراقبته | الحل |
|-----------|-------------------|-----|
| نسخة Excel أقدم من 365 | تظهر `BYROW` و`LAMBDA` كـ `#NAME?` | استخدم الصيغة الكلاسيكية `=SUM(A1:C1)` وانسخها يدويًا، أو قم بترقية Excel. |
| مصفوفات كبيرة (10 k+ صفوف) | قد يصبح الحساب بطيئًا | استدعِ `book.api.CalculateFullRebuild()` مرة واحدة فقط، أو قسّم دفتر العمل. |
| تشغيل على خادم بدون واجهة (headless) دون Excel | لا يستطيع `xlwings` تشغيل Excel | انتقل إلى مكتبة بايثون صافية مثل `pandas` + `numpy` للعمليات الحسابية، ثم اكتب النتائج. |
| مشاكل الإعداد المحلي (الفاصلة vs الفاصلة المنقوطة) | قد تُرفض الصيغة | استخدم `ws["D1"].value = "=BYROW(A1:C3; LAMBDA(r; SUM(r)))"` للغات التي تستخدم `;`. |

---

## مثال كامل يعمل (جاهز للنسخ واللصق)



## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مصدر يتضمن أمثلة شفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف نهج تنفيذ بديلة في مشاريعك.

- [Create Excel Workbook with Aspose.Cells Java - Complete Guide](/cells/english/java/automation-batch-processing/excel-automation-aspose-cells-java-guide/)
- [Create Excel Workbook & Automate Reports with Aspose.Cells](/cells/english/java/automation-batch-processing/aspose-cells-java-two-three-color-scales/)
- [How to Create and Save an Excel Workbook as ODS Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}