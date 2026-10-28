---
category: general
date: 2026-06-08
description: مثال على دالة REDUCE في Excel يوضح كيفية استخدام دالة SEQUENCE في Excel،
  وإنشاء تسلسل في صيغة Excel، واسترجاع قيمة الخلية باستخدام Python.
draft: false
keywords:
- excel reduce function example
- how to use sequence function excel
- generate sequence in excel formula
- retrieve cell value python
language: ar
og_description: مثال على دالة REDUCE في Excel يوضح كيفية استخدام SEQUENCE في Excel،
  وإنشاء تسلسل في صيغة Excel، واسترجاع النتيجة باستخدام Python.
og_title: 'مثال على دالة REDUCE في Excel: حساب الفاكتوريال باستخدام بايثون'
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Excel REDUCE function example showing how to use the SEQUENCE function
    in Excel, generate a sequence in an Excel formula, and retrieve cell value with
    Python.
  headline: 'Excel REDUCE Function Example: Compute Factorial with Python'
  type: TechArticle
tags:
- excel
- python
- aspose-cells
- formula
title: 'مثال على دالة REDUCE في Excel: حساب الفاكتوريال باستخدام بايثون'
url: /ar/python/formulas-and-functions/excel-reduce-function-example-compute-factorial-with-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# مثال على دالة Excel REDUCE: حساب العامل الضربي باستخدام Python

هل تساءلت يومًا كيف تحصل على **مثال على دالة Excel REDUCE** نظيف دون التعامل مع ماكرو VBA؟ لست وحدك. في هذا الدليل سنستعرض استخدام دالة REDUCE مع دالة SEQUENCE لحساب العامل الضربي — كل ذلك من خلال سكريبت Python يتواصل مع مصنف Excel.

ما الفائدة؟ ستشاهد مقطعًا كاملًا قابلًا للتنفيذ **ينتج تسلسلًا في صيغة Excel**، يدمجه في REDUCE، يجبر على إعادة الحساب، وأخيرًا **يسترجع قيمة الخلية باستخدام Python**. لا نسخ‑لصق يدوي، لا خطوات مخفية — مجرد كود نقي يمكنك إدراجه في مشروعك.

## ما ستحتاجه

قبل أن نبدأ، تأكد من وجود ما يلي:

* Python 3.8+ مثبت (أي نسخة حديثة تعمل)
* حزمة `aspose-cells` (`pip install aspose-cells`) — هي الجسر الذي يسمح لـ Python بقراءة/كتابة ملفات Excel.
* فهم أساسي لصيغ Excel — إذا كتبت مسبقًا `=SUM(A1:A5)` فأنت جاهز.
* بيئة تطوير أو محرر نصوص — VS Code، PyCharm، أو حتى Notepad بسيط يكفي.

هذا كل شيء. لا تحتاج إلى DLLs إضافية، ولا إلى تثبيت Office. لننطلق.

## الخطوة 1: إعداد المصنف – مثال على دالة Excel REDUCE

أولًا ننشئ مصنفًا جديدًا في الذاكرة ونستخرج الورقة الافتراضية. هنا سيحدث السحر.

```python
import aspose.cells as cells

# Create a new workbook and reference the first sheet
workbook = cells.Workbook()
worksheet = workbook.worksheets[0]
```

*لماذا هذا مهم*: `aspose-cells` يوفّر لنا محرك Excel كامل الميزات دون تشغيل Excel نفسه. كائن `Workbook` هو بيئتك المعزولة؛ كل ما تضيفه يبقى في الذاكرة RAM حتى تقرّر حفظه.

## الخطوة 2: كيفية استخدام دالة SEQUENCE في Excel

دالة SEQUENCE يمكنها إنتاج قائمة أرقام بصيغة واحدة. هنا نخزن طول تلك القائمة — “n” للعامل الضربي — في الخلية **A1**.

```python
# Put the number of terms (5) into cell A1
worksheet.cells["A1"].put_value(5)   # n = 5
```

الآن A1 يحتوي على القيمة 5، والتي تخبر كل من SEQUENCE وREDUCE بعدد الأرقام التي سيعملون معها. إذا احتجت إلى عامل ضربي مختلف، غير القيمة هنا فقط. بسيط، أليس كذلك؟

## الخطوة 3: تطبيق REDUCE لتوليد التسلسل في صيغة Excel

هذا هو جوهر **مثال دالة excel reduce**. نكتب صيغة في B1 تُنشئ تسلسلًا من 1 إلى *n* وتدمجه في حاصل ضرب.

```python
# Set a REDUCE formula in B1 that multiplies the sequence 1..n (computes factorial)
worksheet.cells["B1"].formula = "=REDUCE(1, SEQUENCE(A1,1,1,1), LAMBDA(acc, x, acc*x))"
```

نشرح ما يحدث:

* `SEQUENCE(A1,1,1,1)` – يبدأ من 1، بخطوة 1، ويخلق *A1* صفًا (أي 5 صفوف: 1,2,3,4,5).
* `REDUCE(1, …, LAMBDA(acc, x, acc*x))` – يبدأ بمجمع بقيمة 1 ويضرب كل عنصر (`x`) فيه، وبالتالي يحسب `1*2*3*4*5`.

إذا كنت جديدًا على `LAMBDA`، فكر فيها كدالة مضمنة تستقبل حجتين: القيمة المتراكمة (`acc`) والعنصر الحالي (`x`). الجملة `acc*x` تخبر Excel كيف يجمعهما.

## الخطوة 4: إعادة حساب الصيغ واسترجاع قيمة الخلية باستخدام Python

Aspose لن يقوم بتقييم الصيغ تلقائيًا؛ نحتاج إلى تشغيل عملية حساب.

```python
# Recalculate all formulas in the workbook
workbook.calculate_formula()
```

الآن المحرك أجرى الحساب، وB1 يحمل نتيجة العامل الضربي. لنسترجع هذه القيمة إلى Python.

```python
# Retrieve and display the result (120)
result = worksheet.cells["B1"].value
print(result)   # → 120
```

سترى **120** مطبوعًا في وحدة التحكم — بالضبط ما يساوي 5!. هذا السطر يوضح خطوة **retrieve cell value python** بطريقة نظيفة ومختصرة.

## الخطوة 5: التحقق من النتيجة وتجربة تنويعات

تحقق سريع: غيّر القيمة في A1 إلى 7، أعد تشغيل الحساب، وستحصل على 5040. هذه هي روعة **generate sequence in excel formula** — منطق REDUCE نفسه يعمل لأي حجم.

```python
worksheet.cells["A1"].put_value(7)   # Change n to 7
workbook.calculate_formula()
print(worksheet.cells["B1"].value)  # → 5040
```

*نصيحة محترف*: إذا كنت تخطط لتصدير المصنف للاستخدام البشري، استدعِ `workbook.save("factorial.xlsx")` بعد الحساب. سيحتوي الملف على الصيغة والقيمة المحسوبة، جاهزًا للفتح في أي برنامج جداول.

## المشكلات الشائعة وحالات الحافة

| المشكلة | سبب حدوثها | الحل |
|-------|----------------|-----|
| **الصيغة لا تُحدّث** | قمت باستدعاء `put_value` لكن نسيت `calculate_formula()` | احرص على إعادة الحساب بعد أي تغيير في البيانات. |
| **قيمة *n* الكبيرة تسبب تجاوز السعة** | دقة الأرقام في Excel تصل إلى حوالي 10^308؛ العامل الضربي ينمو بسرعة. | استخدم دقة `DOUBLE` أو انتقل إلى حسابات تعتمد على `LOG` للأعداد الضخمة. |
| **غياب رخصة Aspose** | الإصدار التجريبي المجاني يُظهر شريط تحذير. | اشترِ رخصة أو استخدم النسخة التجريبية للاختبار غير التجاري. |

## ما التالي؟

الآن بعد أن لديك **مثال excel reduce function** قوي، فكر في هذه التوسعات:

* **حسابات على مستوى المصفوفة** — استخدم REDUCE للجمع، المتوسط، أو دمج النص عبر تسلسل مُولد.
* **نطاقات ديناميكية** — استبدل الإشارة الثابتة `A1` بنطاق مسمى يمكن للمستخدمين تحريره.
* **تكامل متعدد اللغات** — استبدل Python بـ C# أو Java مع الحفاظ على نفس صيغة REDUCE؛ المصنف يبقى مستقلاً عن اللغة.

إذا كنت مهتمًا بدوال Excel أخرى، فإن دالة `SCAN` تعمل جنبًا إلى جنب مع `REDUCE` للحصول على نتائج تراكمية، و`LET` يمكنها تنظيم الصيغ المعقدة. جميعها يمكن تشغيلها من Python باستخدام النمط نفسه الذي عرضناه.

---

### ملخص

بدأنا بـ **مثال excel reduce function** واضح، أظهرنا **كيفية استخدام دالة sequence في Excel** لبناء قائمة رقمية، **ولدنا تسلسلًا في صيغة Excel** يغذي REDUCE، أجبرنا على إعادة الحساب، وأخيرًا **استرجعنا قيمة الخلية باستخدام Python**. يكتمل سير العمل في بضع أسطر مختصرة، لكنه يوضح قوة صيغ Excel الحديثة عندما تُدمج مع API قوي.

لا تتردد في نسخ الكود، تعديل قيمة `A1`، أو دمج المقتطف في خط أنابيب معالجة بيانات أكبر. السماء هي الحد — سواء كنت تُؤتمت تقارير، تحلل نماذج مالية، أو تلعب بالجداول للمتعة.

هل لديك أسئلة أو تريد مشاركة تنويعاتك؟ اترك تعليقًا أدناه، وتمنياتنا لك ببرمجة سعيدة!

## ماذا تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تُبني على التقنيات التي استعرضناها في هذا الدليل. كل مورد يتضمن أمثلة شاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف نهج تنفيذ بديلة في مشاريعك.

- [How to Use Excel IF Function](/cells/english/java/basic-excel-functions/how-to-use-excel-if-function/)
- [How To Use Excel If Function](/cells/german/java/basic-excel-functions/how-to-use-excel-if-function/)
- [How To Use Excel If Function](/cells/french/java/basic-excel-functions/how-to-use-excel-if-function/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}