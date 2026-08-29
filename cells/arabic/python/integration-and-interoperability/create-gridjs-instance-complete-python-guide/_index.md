---
category: general
date: 2026-06-30
description: إنشاء كائن GridJs في بايثون مع إعدادات مخصصة للنافذة المنبثقة. تعلم كيفية
  ربط ورقة العمل، وتكوين النافذة المنبثقة، وإخراج JSON للعميل.
draft: false
keywords:
- create gridjs instance
- gridjs custom modal
- gridjs worksheet integration
- gridjs client configuration
- gridjs python api
language: ar
og_description: إنشاء مثيل GridJs في بايثون مع إعدادات نافذة مخصصة. تعليمات خطوة بخطوة
  لتكامل ورقة العمل وتكوين العميل.
og_title: إنشاء مثيل GridJs – دليل بايثون الكامل
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Create GridJs instance in Python with custom modal settings. Learn
    how to bind a worksheet, configure the modal, and output client JSON.
  headline: Create GridJs Instance – Complete Python Guide
  type: TechArticle
tags:
- gridjs
- python
- web‑ui
- data‑grid
title: إنشاء مثيل GridJs – دليل بايثون الكامل
url: /ar/python/integration-and-interoperability/create-gridjs-instance-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء مثيل GridJs – دليل بايثون كامل

هل تساءلت يومًا كيف **create gridjs instance** من بايثون دون أن تشعر بالإحباط؟ لست وحدك. سواءً كنت تبني لوحة تحكم إدارية، أو كتالوج منتجات، أو جدول بيانات سريع النظر، فإن تشغيل GridJs هو العائق الأول.  

في هذا الدرس سنستعرض مثالًا واقعيًا: ربط ورقة عمل، تشغيل نافذة مخصصة تظهر عند النقر المزدوج، وأخيرًا استخراج تكوين JSON من جانب العميل لتتمكن من تمريره إلى الواجهة الأمامية. بنهاية الدرس ستحصل على إعداد GridJs يعمل يمكنك إدراجه في أي مشروع Flask أو Django.

## المتطلبات المسبقة

- Python 3.8+ مثبت محليًا  
- إلمام أساسي بـ OOP في بايثون  
- فئة `Worksheet` بسيطة (سنقوم بمحاكاة واحدة للعرض)  

لا توجد حزمة GridJs خارجية للبايثون، لذا سنحاكي الـ API الذي يعكس مكتبة JavaScript. المفاهيم تُترجم مباشرة إلى الاستخدام الحقيقي لمكتبة GridJs JavaScript.

## الخطوة 1: تعريف فئة GridJs محاكاة (GridJs Python API)

قبل أن نتمكن من **create gridjs instance**، نحتاج إلى غلاف خفيف يحاكي المكتبة الحقيقية. هذا يجعل المثال قابلًا للتنفيذ ويركّز على تدفق التكوين.

```python
# gridjs_mock.py
import json

class Settings:
    """Container for all GridJs settings."""
    def __init__(self):
        self.custom_modal = CustomModal()

class CustomModal:
    """Settings for the double‑click custom modal."""
    def __init__(self):
        self.enabled = False
        self.title = ""
        self.width = "400px"
        self.height = "300px"
        self.url = ""

class GridJs:
    """A lightweight Python representation of a GridJs grid."""
    def __init__(self):
        self._worksheet = None
        self.settings = Settings()

    def set_worksheet(self, worksheet):
        """Bind a Worksheet object to the grid."""
        self._worksheet = worksheet

    def get_client_config(self):
        """Serialize the grid configuration for the front‑end."""
        config = {
            "worksheet": getattr(self._worksheet, "name", "undefined"),
            "custom_modal": {
                "enabled": self.settings.custom_modal.enabled,
                "title": self.settings.custom_modal.title,
                "width": self.settings.custom_modal.width,
                "height": self.settings.custom_modal.height,
                "url": self.settings.custom_modal.url,
            },
        }
        return json.dumps(config, indent=2)
```

> **نصيحة احترافية:** اجعل الغلاف في بايثون خفيفًا—يكفي فقط لتوليد الـ JSON الذي ستمريره إلى جانب JavaScript. الإفراط في هندسة الجسر يضيف عبئ صيانة.

## الخطوة 2: إنشاء كائن ورقة عمل بسيط (تكامل GridJs مع Worksheet)

يمكن أن يكون **gridjs worksheet integration** بسيطًا كفئة تحتوي على خاصية `name`. في تطبيق حقيقي ستجلب البيانات من قاعدة بيانات أو ملف CSV.

```python
# worksheet.py
class Worksheet:
    """Mock worksheet holding tabular data."""
    def __init__(self, name):
        self.name = name
        # Imagine self.rows = [...] here
```

الآن لديك عنصر نائب يمكنك تمريره إلى الشبكة.

## الخطوة 3: تجميع الشبكة – منطق “إنشاء مثيل GridJs” الأساسي

مع الفئات المحاكاة جاهزة، يمكننا أخيرًا **create gridjs instance** وتكوينه خطوة بخطوة.

```python
# main.py
from gridjs_mock import GridJs
from worksheet import Worksheet

# 1️⃣ Create a GridJs instance
grid = GridJs()

# 2️⃣ Associate the worksheet you want to display
worksheet = Worksheet(name="Products")
grid.set_worksheet(worksheet)

# 3️⃣ Enable the custom modal that appears on double‑click
grid.settings.custom_modal.enabled = True
grid.settings.custom_modal.title = "Edit Product"
grid.settings.custom_modal.width = "600px"
grid.settings.custom_modal.height = "400px"

# 4️⃣ Point the modal to an external HTML editor page
grid.settings.custom_modal.url = "/product-editor.html"

# 5️⃣ Retrieve the client‑side configuration JSON and output it
config_json = grid.get_client_config()
print(config_json)
```

### النتيجة المتوقعة (تكوين عميل GridJs)

تشغيل `python main.py` ينتج كائن JSON منسق بشكل جميل:

```json
{
  "worksheet": "Products",
  "custom_modal": {
    "enabled": true,
    "title": "Edit Product",
    "width": "600px",
    "height": "400px",
    "url": "/product-editor.html"
  }
}
```

هذا الـ JSON هو بالضبط ما ستمريره إلى مُنشئ GridJs في الواجهة الأمامية:

```javascript
new Grid({
  data: [],               // will be filled from the worksheet
  customModal: {/* … */} // values from the JSON above
});
```

## الخطوة 4: ربط الـ JSON بصفحة الواجهة الأمامية (تجميع كل شيء)

يمكنك تضمين **gridjs client configuration** الذي طبعتَه في مسار Flask:

```python
# app.py (Flask snippet)
from flask import Flask, render_template_string, jsonify
from main import config_json  # reuse the same grid setup

app = Flask(__name__)

@app.route("/grid-config")
def grid_config():
    return jsonify(json.loads(config_json))

# Simple HTML page loading GridJs from CDN
HTML = """
<!doctype html>
<html>
<head>
  <script src="https://unpkg.com/gridjs/dist/gridjs.umd.js"></script>
  <link href="https://unpkg.com/gridjs/dist/theme/mermaid.min.css" rel="stylesheet"/>
</head>
<body>
  <div id="wrapper"></div>
  <script>
    fetch('/grid-config')
      .then(r => r.json())
      .then(config => {
        new gridjs.Grid({
          columns: ['ID', 'Name', 'Price'],
          data: [], // fetch actual rows based on config.worksheet
          customModal: config.custom_modal
        }).render(document.getElementById('wrapper'));
      });
  </script>
</body>
</html>
"""
@app.route("/")
def index():
    return render_template_string(HTML)

if __name__ == "__main__":
    app.run(debug=True)
```

> **لماذا يعمل هذا:** الخلفية تُزوّد بحمولة JSON تعكس الإعدادات التي عرّفتها في بايثون. الواجهة الأمامية تقرأ نفس الحمولة، مما يضمن أن **gridjs custom modal** يتصرف تمامًا كما تم تكوينه.

## المشكلات الشائعة والحالات الخاصة (GridJs Custom Modal)

| المشكلة | السبب | الحل |
|-------|-------|-----|
| النافذة لا تفتح عند النقر المزدوج | `custom_modal.enabled` تركت `False` | تأكد من ضبط `grid.settings.custom_modal.enabled = True` |
| أبعاد النافذة تبدو غريبة على الجوال | قيم بكسل ثابتة (`600px`) لا تتكيف | استخدم وحدات نسبية CSS (`80%`, `vh`) أو استعلامات وسائط |
| العنوان يُعيد 404 | المسار `/product-editor.html` غير مُقدم | أضف مسارًا ثابتًا في Flask/Django أو استضف الملف على CDN |
| اسم ورقة العمل مفقود في الـ JSON | كائن `Worksheet` يفتقر إلى خاصية `name` | قدّم اسمًا ذا معنى أو وسّع المحاكاة لتشمل بيانات تعريفية |

معالجة هذه القضايا مبكرًا سيوفر لك ساعات من التصحيح لاحقًا.

## توسيع المثال (الخطوات التالية)

- **تحميل بيانات حقيقية**: استبدل `Worksheet` المحاكي بـ pandas DataFrame وسلسلة الصفوف إلى JSON.  
- **تأمين النافذة**: أضف فحوصات توثيق قبل تقديم `/product-editor.html`.  
- **تعيين أعمدة ديناميكي**: استخرج رؤوس الأعمدة من مخطط ورقة العمل بدلاً من كتابة ثابتة.  
- **التعريب**: خزن عناوين النافذة في ملف لغة وادخلها عبر حمولة JSON.

كل هذه التحسينات تبنى على أساس **create gridjs instance** الذي أتممته للتو.

## الخلاصة

غطينا كل ما تحتاجه لـ **create gridjs instance** في بايثون، من ربط ورقة عمل إلى تشغيل نافذة مخصصة وأخيرًا إظهار تكوين JSON نظيف للعميل. النمط بسيط، قابل لإعادة الاستخدام، ويتناسب بسلاسة مع أي إطار ويب حديث.

جرّبه، عدّل أبعاد النافذة، استبدل ورقة العمل باستعلام قاعدة بيانات حقيقي، وستحصل على تكامل GridJs جاهز للإنتاج في وقت قصير. لديك أسئلة؟ اترك تعليقًا، وتمنياتنا لك ببرمجة سعيدة!

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم استعراضها في هذا الدليل. كل مورد يتضمن أمثلة شاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [How to Create and Configure Excel Workbooks with Aspose.Cells .NET: A Step‑By‑Step Guide](/cells/english/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)
- [Create a Custom Size Chart PDF with Aspose.Cells .NET: Step‑by‑Step Guide](/cells/english/net/charts-graphs/create-custom-size-chart-pdf-aspose-cells-net/)
- [How to Create a Custom Static Value Function in Aspose.Cells Java](/cells/english/java/formulas-functions/aspose-cells-java-custom-static-value-function/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}