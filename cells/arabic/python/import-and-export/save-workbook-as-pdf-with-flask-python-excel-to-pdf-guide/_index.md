---
category: general
date: 2026-06-21
description: احفظ دفتر العمل كملف PDF باستخدام Flask و Aspose.Cells في بايثون – تعلّم
  كيفية تحويل XLSX إلى PDF، وضبط أعمدة إكسل تلقائيًا، وإرجاع الملف باستخدام flask
  send_file pdf.
draft: false
keywords:
- save workbook as pdf
- convert xlsx to pdf
- python excel to pdf
- auto fit excel columns
- flask send_file pdf
language: ar
og_description: احفظ المصنف كملف PDF باستخدام بايثون وFlask. يوضح هذا الدليل خطوة
  بخطوة كيفية تحويل XLSX إلى PDF، وضبط أعمدة Excel تلقائيًا، وتقديم النتيجة باستخدام flask send_file pdf.
og_title: حفظ دفتر العمل كملف PDF باستخدام Flask – دليل Python الكامل
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Save workbook as PDF using Flask and Aspose.Cells in Python – learn
    how to convert XLSX to PDF, auto‑fit Excel columns, and return the file with flask
    send_file pdf.
  headline: Save Workbook as PDF with Flask – Python Excel to PDF Guide
  type: TechArticle
- description: Save workbook as PDF using Flask and Aspose.Cells in Python – learn
    how to convert XLSX to PDF, auto‑fit Excel columns, and return the file with flask
    send_file pdf.
  name: Save Workbook as PDF with Flask – Python Excel to PDF Guide
  steps:
  - name: Why Each Piece Matters
    text: '- **`request.files.get("file")`** – Safely fetches the uploaded file; using
      `.get` avoids a `KeyError` if the field is missing. - **`io.BytesIO`** – Keeps
      everything in RAM, so we never write temporary files to disk. This is crucial
      for scalability. - **`auto_fit_columns()`** – Without this, column '
  - name: Manual Test with cURL
    text: '```bash curl -X POST http://localhost:5000/convert  -F "file=@sample.xlsx"  -o
      result.pdf ```'
  - name: Automated Test with Python’s `requests`
    text: '```python import requests'
  type: HowTo
tags:
- flask
- python
- excel
- pdf
- aspose-cells
title: حفظ دفتر العمل كملف PDF باستخدام Flask – دليل بايثون لتحويل Excel إلى PDF
url: /ar/python/import-and-export/save-workbook-as-pdf-with-flask-python-excel-to-pdf-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# حفظ دفتر العمل كملف PDF باستخدام Flask – دليل Python لتحويل Excel إلى PDF

هل تحتاج إلى **حفظ دفتر العمل كملف PDF** من خدمة ويب؟ لست الوحيد الذي يتساءل عن كيفية تحويل ملف Excel تم تحميله إلى PDF أنيق في الوقت الفعلي. في هذا الدليل سنستعرض عملية حفظ دفتر العمل كملف PDF باستخدام Flask و Aspose.Cells، بالإضافة إلى شرح كيفية **تحويل XLSX إلى PDF**، ضبط أعمدة Excel تلقائيًا، وأخيرًا تسليم النتيجة باستخدام `flask send_file pdf`.

سنبدأ بمشروع Flask جديد، نضيف بعض النصائح العملية، وسننتهي بنقطة نهاية (endpoint) تعمل بالكامل ويمكن لأي عميل استدعاؤها. بحلول الوقت الذي تنتهي فيه، ستكون قادرًا على تحويل أي جدول بيانات إلى PDF ببضع أسطر فقط من كود Python.

## ما الذي ستحتاجه

- **Python 3.8+** (الكود يعمل على 3.9، 3.10، والإصدارات الأحدث)
- **Flask** (`pip install flask`) – إطار عمل الويب الخفيف الذي يشغل API الخاص بنا
- **Aspose.Cells for Python via .NET** (`pip install aspose-cells`) – المكتبة التي تقرأ XLSX وتكتب PDF فعليًا
- فهم أساسي لطلبات HTTP `POST` (بدون تعقيدات)

إذا كنت تمتلك هذه المكونات بالفعل، عظيم—لنبدأ. إذا لم تكن كذلك، خطوة “تثبيت الاعتماديات” ستجهزك.

## الخطوة 1 – إعداد مشروع Flask

أولاً، أنشئ مجلدًا جديدًا للمشروع وقم بإنشاء بيئة افتراضية. هذا يحافظ على تنظيم الاعتماديات.

```bash
mkdir flask_excel_pdf && cd flask_excel_pdf
python -m venv venv
source venv/bin/activate   # Windows: venv\Scripts\activate
pip install flask aspose-cells
```

الآن أنشئ ملفًا باسم `app.py`. سيحتوي هذا الملف على منطق **حفظ دفتر العمل كملف PDF** بالكامل.

## الخطوة 2 – تهيئة تطبيق Flask

نبدأ باستيراد المكونات التي نحتاجها وإنشاء كائن تطبيق Flask. لاحظ مدى اختصار كتلة الاستيراد—لا توجد وحدات غير مستخدمة، مما يقلل من زمن بدء التشغيل.

```python
# app.py
from flask import Flask, request, send_file
import aspose.cells as cells
import io

app = Flask(__name__)
```

> **نصيحة احترافية:** احتفظ بـ `app = Flask(__name__)` في أعلى الملف؛ فهذا يجعل اختبار التطبيق لاحقًا باستخدام أدوات مثل `pytest-flask` سهلًا للغاية.

## الخطوة 3 – بناء نقطة النهاية للتحويل (convert xlsx to pdf)

هذا هو جوهر الدرس: نقطة نهاية تستقبل جدول بيانات عبر `POST`، وتحمله في دفتر عمل Aspose.Cells، وتجهزه لتصدير PDF.

```python
@app.route("/convert", methods=["POST"])
def convert():
    # 1️⃣ Grab the uploaded file from the request
    uploaded = request.files.get("file")
    if not uploaded:
        return {"error": "No file provided"}, 400

    # 2️⃣ Read the file into memory (binary)
    file_bytes = uploaded.read()

    # 3️⃣ Load the spreadsheet into a workbook object
    workbook = cells.Workbook(io.BytesIO(file_bytes))

    # 4️⃣ Auto‑fit all columns in the first sheet (auto fit excel columns)
    workbook.worksheets[0].auto_fit_columns()

    # 5️⃣ Save the workbook as PDF into an in‑memory stream
    pdf_stream = io.BytesIO()
    workbook.save(pdf_stream, cells.SaveFormat.PDF)
    pdf_stream.seek(0)

    # 6️⃣ Return the PDF using flask send_file pdf
    return send_file(
        pdf_stream,
        mimetype="application/pdf",
        as_attachment=True,
        download_name="output.pdf"
    )
```

### لماذا كل جزء مهم

- **`request.files.get("file")`** – يجلب الملف المرفوع بأمان؛ استخدام `.get` يتجنب حدوث `KeyError` إذا كان الحقل مفقودًا.
- **`io.BytesIO`** – يحتفظ بكل شيء في الذاكرة RAM، لذا لا نكتب ملفات مؤقتة على القرص. هذا أمر حاسم للتوسع.
- **`auto_fit_columns()`** – بدون هذا، قد تظهر أعمدة PDF ضيقة. هذه الطريقة توسع كل عمود ليتناسب مع أطول خلية فيه، مما يعطي مظهرًا احترافيًا.
- **`workbook.save(..., cells.SaveFormat.PDF)`** – هذه الدالة الوحيدة تقوم بالتحويل الفعلي من XLSX إلى PDF. Aspose.Cells يتعامل مع الصيغ، الرسوم البيانية، وحتى الخلايا المدمجة.
- **`flask send_file pdf`** – يرسل ملف PDF إلى العميل مع رؤوس مناسبة، مما يفتح نافذة تنزيل باسم `output.pdf`.

## الخطوة 4 – تشغيل خادم Flask

أضف “حارس التشغيل” التقليدي في أسفل `app.py` حتى يمكن تنفيذ السكريبت مباشرة.

```python
if __name__ == "__main__":
    # Listening on all interfaces makes testing from Docker or another machine easy
    app.run(host="0.0.0.0", port=5000, debug=True)
```

تشغيل `python app.py` سيبدأ الخادم على `http://localhost:5000`. علامة `debug=True` مفيدة أثناء التطوير؛ تذكر إيقافها في بيئة الإنتاج.

## الخطوة 5 – اختبار نقطة النهاية (يدويًا وآليًا)

### اختبار يدوي باستخدام cURL

```bash
curl -X POST http://localhost:5000/convert \
  -F "file=@sample.xlsx" \
  -o result.pdf
```

إذا سارت الأمور بشكل جيد، سيحتوي `result.pdf` على نسخة منسقة بشكل جميل من `sample.xlsx`، مع ضبط جميع الأعمدة تلقائيًا.

### اختبار آلي باستخدام `requests` في Python

```python
import requests

with open("sample.xlsx", "rb") as f:
    response = requests.post(
        "http://localhost:5000/convert",
        files={"file": f}
    )
    response.raise_for_status()
    with open("downloaded.pdf", "wb") as out:
        out.write(response.content)

print("PDF saved as downloaded.pdf")
```

كلا الطريقتين توضحان سير عمل **python excel to pdf** الكامل—من التحميل إلى التنزيل—دون الحاجة إلى التعامل مع نظام الملفات على جانب الخادم.

## الخطوة 6 – الحالات الحدية والمشكلات الشائعة

| الحالة | ما الذي يجب مراقبته | الحل |
|-----------|-------------------|-----|
| ملفات XLSX الكبيرة ( > 50 MB ) | ضغط الذاكرة على الخادم | بثّ التحميل إلى ملف مؤقت واستخدام `Workbook(file_path)` بدلاً من `BytesIO`. |
| دفتر عمل محمي بكلمة مرور | `Workbook` يرمي استثناءً | تمرير كلمة المرور إلى مُنشئ `Workbook`: `Workbook(io.BytesIO(file_bytes), cells.LoadOptions(password="secret"))`. |
| عدم استدعاء `auto_fit_columns()` | أعمدة PDF تظهر مقصوصة | دائمًا استدعِ `auto_fit_columns()` **قبل** `save()`. |
| العميل يتوقع خطأ بصيغة JSON | Flask يعيد صفحة خطأ HTML | إرجاع قاموس JSON مع رمز الحالة المناسب كما هو موضح في نقطة النهاية (السطر `return {"error": "No file provided"}, 400`). |

## الخطوة 7 – النشر في بيئة الإنتاج

عندما تكون جاهزًا لإطلاق الخدمة، ضع في اعتبارك هذه التعديلات المناسبة للإنتاج:

- **استخدام خادم WSGI** مثل `gunicorn` (`gunicorn -w 4 app:app`) بدلاً من الخادم المدمج في Flask.
- **تفعيل HTTPS** عبر وكيل عكسي (NGINX) لحماية عمليات تحميل الملفات.
- **تحديد حد لحجم الطلب** (`app.config["MAX_CONTENT_LENGTH"] = 20 * 1024 * 1024`) لتجنب هجمات حجب الخدمة.
- **تسجيل الأخطاء** باستخدام مسجل منظم (مثل `structlog`) لتتمكن من تتبع فشل التحويل.

جميع هذه الخطوات تحافظ على منطق **save workbook as pdf** الأساسي مع جعل الخدمة جاهزة للإنتاج.

## النتيجة المتوقعة

عند استدعاء نقطة النهاية `/convert` بملف XLSX صالح، سيقوم الاستجابة بـ:

1. احتواء رأس `Content-Type: application/pdf`.
2. طلب من المتصفح (أو العميل) تنزيل ملف باسم `output.pdf`.
3. عرض جدول البيانات مع أعمدة مُحَددَة تلقائيًا وفق محتواها، بفضل استدعاء `auto fit excel columns`.

افتح ملف PDF الذي تم تنزيله—يجب أن ترى كل عمود مرئي بالكامل، الصيغ مُحسوبة، وأي صور مدمجة محفوظة.

## الخلاصة

أصبح لديك الآن مثال كامل وجاهز للإنتاج يوضح كيفية **save workbook as pdf** باستخدام Flask و Aspose.Cells وPython النقي. غطى الدرس كل شيء من إعداد البيئة، **convert xlsx to pdf**، ضبط الأعمدة تلقائيًا، وأخيرًا تسليم النتيجة باستخدام `flask send_file pdf`.

بعد ذلك، قد ترغب في استكشاف إضافة **تنسيق مخصص**، دمج الخلايا، أو حتى تحويل عدة أوراق عمل إلى ملف PDF متعدد الصفحات. النمط نفسه يعمل مع أنواع ملفات أخرى—فقط استبدل تعداد `SaveFormat`.

هل لديك أسئلة حول الحالات الحدية أو النشر؟ اترك تعليقًا أدناه، ونتمنى لك برمجة سعيدة!

## ما الذي ينبغي أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مصدر يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [كيفية حفظ صفحات محددة من ملف Excel كملف PDF باستخدام Aspose.Cells لـ .NET](/cells/english/net/workbook-operations/save-specific-excel-pages-pdf-aspose-cells-net/)
- [حفظ دفتر عمل Excel كملف PDF مع خطوط مخصصة باستخدام Aspose.Cells لـ .NET](/cells/english/net/workbook-operations/save-excel-workbook-pdf-custom-fonts-aspose-cells-net/)
- [تحويل Excel إلى PDF مع ضبط الأعمدة في Java باستخدام Aspose.Cells](/cells/english/java/workbook-operations/convert-excel-to-pdf-fit-columns-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}