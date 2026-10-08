---
category: general
date: 2026-06-21
description: إنشاء جدول الضرب في إكسل باستخدام بايثون. تعلم كيفية استخدام اللامبدا،
  وكيفية استخدام makearray، وعرض مصفوفة إكسل وقراءة قيم إكسل بايثون في دليل خطوة بخطوة.
draft: false
keywords:
- create multiplication table
- how to use lambda
- how to use makearray
- display excel array
- read excel values python
language: ar
og_description: إنشاء جدول الضرب في Excel باستخدام Python. يوضح هذا الدرس كيفية استخدام
  lambda، makearray، عرض مصفوفة Excel وقراءة قيم Excel باستخدام Python بكفاءة.
og_title: إنشاء جدول الضرب في إكسل باستخدام بايثون – دليل شامل
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Create multiplication table in Excel using Python. Learn how to use
    lambda, how to use makearray, display excel array and read excel values python
    in a step‑by‑step tutorial.
  headline: Create multiplication table in Excel with Python – Full Guide
  type: TechArticle
tags:
- python
- excel
- openpyxl
title: إنشاء جدول الضرب في إكسل باستخدام بايثون – دليل كامل
url: /ar/python/import-and-export/create-multiplication-table-in-excel-with-python-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء جدول الضرب في Excel باستخدام Python – دليل كامل

هل تساءلت يومًا كيف **تنشئ جدول الضرب** في Excel دون الحاجة إلى كتابة كل خلية يدويًا؟ لست وحدك. في العديد من سيناريوهات التقارير تحتاج إلى شبكة منتجات 5×5 (أو أكبر) بسرعة، والقيام بذلك يدويًا يضيع الوقت.  

في هذا الدرس سنستعرض طريقة نظيفة مدفوعة بـ Python لتوليد ذلك الجدول، تضمينه بصيغة `MAKEARRAY`، ثم سحب النتائج مرة أخرى إلى السكريبت الخاص بك. على طول الطريق سنجيب على **كيفية استخدام lambda**، نعرض **كيفية استخدام makearray**، ونوضح **display excel array** بالإضافة إلى **read excel values python**—كل ذلك في مثال واحد متكامل.

في النهاية ستحصل على مقتطف قابل لإعادة الاستخدام يعمل مع أي مصنف، وستفهم لماذا هذه الطريقة سريعة ومؤمنة للمستقبل.

## ما ستحتاجه

- Python 3.8+ (أحدث إصدار مستقر يكفي)
- مكتبة `openpyxl` (أو أي مكتبة تدعم Excel وتتعامل مع الصيغ)
- فهم أساسي لتعبيرات lambda في Python
- لا تحتاج إلى إضافات خاصة لـ Excel؛ دالة `MAKEARRAY` الأصلية (المتوفرة في Excel 365) تقوم بالعمل الشاق

إذا كان أي من هذه مفقودًا، فقط نفّذ `pip install openpyxl` وستكون جاهزًا.

## إنشاء جدول الضرب – نظرة عامة

الفكرة الأساسية بسيطة: ننشئ مصنفًا جديدًا، نكتب صيغة `MAKEARRAY` تُنشئ مصفوفة ضرب 5 × 5، نجبر Excel على حسابها، وأخيرًا نقرأ القيم الناتجة مرة أخرى إلى Python.

```python
from openpyxl import Workbook

# Step 1: Create a new workbook and get the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

# Step 2: Insert a MAKEARRAY formula that builds a 5×5 multiplication table
# The formula uses a LAMBDA that returns r*c for each row (r) and column (c)
worksheet["A1"] = "=MAKEARRAY(5,5, LAMBDA(r,c, r*c))"

# Step 3: Calculate all formulas so the array is materialized in the sheet
workbook.calculate_formula()

# Step 4: Read and display the top‑left 5×5 block of values
for row_index in range(1, 6):
    row_values = [worksheet.cell(row=row_index, column=col_index).value
                  for col_index in range(1, 6)]
    print(row_values)
```

تشغيل السكريبت يطبع:

```
[1, 2, 3, 4, 5]
[2, 4, 6, 8, 10]
[3, 6, 9, 12, 15]
[4, 8, 12, 16, 20]
[5, 10, 15, 20, 25]
```

هذا هو **create multiplication table** كامل الوظائف في Excel، تم توليده بالكامل من خلال Python.

### لماذا نستخدم `MAKEARRAY` بدلاً من حلقة Python؟

- **الأداء**: Excel يتعامل مع الحساب أصلاً، وهو أسرع للمصفوفات الكبيرة.
- **التحديث الحي**: إذا غيرت الأبعاد في الصيغة لاحقًا، سيعيد الورقة حسابها تلقائيًا.
- **قابلية القراءة**: الصيغة تعبر عن النية (“إنشاء مصفوفة”) مباشرة، مما يبقي كود Python منظمًا.

## كيفية استخدام lambda في Python لصيغ Excel

الجزء `LAMBDA` في استدعاء `MAKEARRAY` هو دالة مجهولة على جانب Excel، وليس lambda في Python. ومع ذلك، المفهوم هو نفسه: تعرف قطعة صغيرة من المنطق داخل الصيغة تأخذ `r` (فهرس الصف) و `c` (فهرس العمود) وتعيد `r*c`.  

إذا كنت جديدًا على **how to use lambda** في عالم Excel، ففكر فيها كدالة مصغرة تعيش فقط داخل الصيغة. لا حاجة لتعريف دالة منفصلة في مكان آخر. في Python ندمج السلسلة ببساطة:

```python
worksheet["A1"] = "=MAKEARRAY(5,5, LAMBDA(r,c, r*c))"
```

هذا السطر يخبر Excel: *“لكل خلية في كتلة 5‑بـ‑5، احسب الصف × العمود.”*  

نظرًا لأن lambda يتم تقييمها بواسطة Excel، لا تحتاج للقلق بشأن صياغة lambda في Python هنا—فقط صياغة Excel.

## كيفية استخدام makearray لتوليد المصفوفات

`MAKEARRAY` إضافة حديثة نسبيًا إلى مكتبة دوال Excel (متوفرة في Microsoft 365 منذ 2022). تحل محل الحيل القديمة مثل `INDEX` + `ROW`/`COLUMN`. التوقيع هو:

```
MAKEARRAY(rows, columns, lambda)
```

- **rows** – عدد الصفوف المطلوب.
- **columns** – عدد الأعمدة المطلوب.
- **lambda** – دالة Excel LAMBDA تستقبل `(row, column)` وتعيد قيمة.

في مثالنا مررنا `5,5` لإنشاء جدول ضرب كلاسيكي، لكن يمكنك بسهولة تغيير هذه الأرقام:

```python
worksheet["A1"] = "=MAKEARRAY(10,10, LAMBDA(r,c, r*c))"
```

سيعطيك ذلك جدولًا 10 × 10 دون الحاجة إلى أي حلقات Python. هذا يوضح **how to use makearray** لأي شبكة محددة، سواء كانت جدول بحث، خريطة حرارة، أو جدول مالي.

## Display excel array – سحب البيانات مرة أخرى إلى Python

بعد أن يحسب Excel الصيغة، القيم الناتجة تتواجد في الورقة كما هي أي خلية مُدخلة يدويًا. لــ **display excel array**، نكرر النطاق ونطبع كل صف:

```python
for row_index in range(1, 6):
    row_values = [worksheet.cell(row=row_index, column=col_index).value
                  for col_index in range(1, 6)]
    print(row_values)
```

بعض النصائح:

- استخدم `worksheet.cell(row, column).value` بدلاً من الفهرسة على شكل قاموس إذا كنت تحتاج للتعامل مع نطاقات أكبر؛ فهو أسرع قليلًا.
- إذا أردت جدولًا أكثر جمالية، فكر في استخدام `tabulate` أو `pandas.DataFrame` لتنسيق المخرجات.

فيما يلي لقطة شاشة للورقة الناتجة (نص alt يحتوي على الكلمة المفتاحية الأساسية لتحسين SEO):

![لقطة شاشة تُظهر إنشاء جدول الضرب في Excel باستخدام Python](/images/multiplication-table-excel.png)

## Read excel values python – استخراج المصفوفة لمعالجة إضافية

غالبًا ما تكون الخطوة التالية بعد **display excel array** هي تمرير تلك الأرقام إلى خط أنابيب تحليل بيانات. هنا يتألق **read excel values python**. يمكن إعادة استخدام الحلقة التي استخدمناها للطباعة لبناء قائمة قوائم، مصفوفة NumPy، أو DataFrame من Pandas:

```python
import pandas as pd

# Build a list of rows
data = []
for row_index in range(1, 6):
    row = [worksheet.cell(row=row_index, column=col_index).value
           for col_index in range(1, 6)]
    data.append(row)

# Convert to DataFrame for easy manipulation
df = pd.DataFrame(data, columns=[f"Col{c}" for c in range(1, 6)],
                  index=[f"Row{r}" for r in range(1, 6)])

print(df)
```

المخرجات:

```
      Col1  Col2  Col3  Col4  Col5
Row1     1     2     3     4     5
Row2     2     4     6     8    10
Row3     3     6     9    12    15
Row4     4     8    12    16    20
Row5     5    10    15    20    25
```

الآن لديك DataFrame مكتمل الأنواع يمكنك رسمه، تصديره إلى CSV، أو إمداده إلى نموذج تعلم آلي. هذا يُكمل جزء **read excel values python** من سير العمل.

## الحالات الخاصة والنصائح العملية

- **إعادة حساب الصيغة**: إذا عدلت المصنف بعد استدعاء `calculate_formula()` الأول، يجب استدعاؤه مرة أخرى؛ وإلا ستظل المصفوفة المخزنة قديمة.
- **Excel غير 365**: الإصدارات القديمة من Excel لا تدعم `MAKEARRAY`. في هذه الحالة عُد إلى جدول مولد بـ Python واكتب كل خلية على حدة.
- **الجداول الكبيرة**: للمصفوفات التي تتجاوز ~100 × 100، فكر في تدفق البيانات لتجنب تحميل الورقة بالكامل في الذاكرة.
- **معالجة الأخطاء**: غلف خطوات الحساب والقراءة بكتل `try/except` لالتقاط `InvalidFileException` أو `FormulaError`.

## الخلاصة

لقد أظهرنا لك كيف **create multiplication table** في Excel باستخدام Python، مستفيدين من قوة **how to use lambda** و **how to use makearray**. رأيت كيف **display excel array**، وكيف تقرأ تلك القيم باستخدام **read excel values python**، وحتى كيفية تحويل النتيجة إلى DataFrame من Pandas للتحليل اللاحق.

هل تريد التعمق أكثر؟ جرّب استبدال منطق الضرب بشيء أكثر تعقيدًا—ربما مصفوفة مسافات، جدول احتمالات، أو شبكة تسعير ديناميكية. النمط نفسه ينطبق: سطر واحد من `MAKEARRAY`، استدعاء سريع لـ `calculate_formula()`، وعدد قليل من حلقات Python لسحب البيانات.

إذا وجدت هذا الدليل مفيدًا، أعطه نجمة على GitHub، شاركه مع زملائك، أو اترك تعليقًا بحالتك الخاصة. برمجة سعيدة، واستمتع بإنشاء جداول Excel بصيغة واحدة فقط!

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [How to Create and Configure Excel Workbooks with Aspose.Cells .NET: A Step‑By‑Step Guide](/cells/english/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)
- [Aspose.Cells .NET Tutorial: How to Create and Modify Excel Workbooks Easily](/cells/english/net/workbook-operations/aspose-cells-net-create-modify-excel-workbooks/)
- [How to Create and Style Named Ranges in Excel Using Aspose.Cells .NET | Step‑By‑Step Guide](/cells/english/net/range-management/create-style-named-ranges-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}