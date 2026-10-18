---
category: general
date: 2026-06-21
description: أنشئ شبكة بيانات تفاعلية باستخدام Grid.js وتعلم كيفية عرض جدول بيانات
  JSON مع الترتيب والصفحات والبحث. مثالي للوحة التحكم على الويب.
draft: false
keywords:
- create interactive data grid
- display json data table
- how to use gridjs
language: ar
og_description: أنشئ شبكة بيانات تفاعلية في دقائق. تعلّم كيفية استخدام Grid.js لعرض
  جدول بيانات JSON مع التصفح، والترتيب، والبحث.
og_title: إنشاء شبكة بيانات تفاعلية باستخدام Grid.js – دليل كامل
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Create interactive data grid using Grid.js and learn how to display
    JSON data table with sorting, pagination, and search. Perfect for web dashboards.
  headline: Create Interactive Data Grid with Grid.js – Full Step‑by‑Step Guide
  type: TechArticle
- description: Create interactive data grid using Grid.js and learn how to display
    JSON data table with sorting, pagination, and search. Perfect for web dashboards.
  name: Create Interactive Data Grid with Grid.js – Full Step‑by‑Step Guide
  steps:
  - name: A modern browser (Chrome, Edge, or Firefox) – Grid.js relies on ES6 features.
    text: A modern browser (Chrome, Edge, or Firefox) – Grid.js relies on ES6 features.
  - name: A local or remote folder containing a `grid_data.json` file (we’ll show
      the format).
    text: A local or remote folder containing a `grid_data.json` file (we’ll show
      the format).
  - name: Basic familiarity with HTML and JavaScript – nothing fancy, just the ability
      to open a `.html` file in a browser.
    text: Basic familiarity with HTML and JavaScript – nothing fancy, just the ability
      to open a `.html` file in a browser.
  type: HowTo
tags:
- JavaScript
- Grid.js
- Data Visualization
title: إنشاء شبكة بيانات تفاعلية باستخدام Grid.js – دليل خطوة بخطوة كامل
url: /ar/python/import-and-export/create-interactive-data-grid-with-grid-js-full-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء شبكة بيانات تفاعلية باستخدام Grid.js – دليل خطوة بخطوة كامل

هل تساءلت يوماً كيف **create interactive data grid** يسمح للمستخدمين بالترتيب، البحث، والتنقل بين الصفوف دون الحاجة إلى كتابة خلفية؟ لست وحدك. في العديد من لوحات التحكم، أكبر نقطة ألم هي تحويل تفريغ JSON ثابت إلى جدول أنيق وقابل للبحث—شيء يشبه جداول البيانات لكنه يعمل بالكامل في المتصفح.

في هذا الدرس سنستعرض **how to use Grid.js** ل**display JSON data table** على صفحة HTML بسيطة. في النهاية ستحصل على مثال عملي يمكنك إدراجه في أي مشروع، بالإضافة إلى نصائح لتخصيص شريط الأدوات، التعامل مع مجموعات البيانات الكبيرة، وتجنب الأخطاء الشائعة.

## ما ستتعلمه

- كيفية جلب ملف JSON يحدد الأعمدة والصفوف.  
- كيفية تهيئة **Grid.js** مع الترميز الصفحات، الترتيب، البحث، وشريط أدوات مخصص.  
- كيفية عرض الشبكة داخل حاوية الهدف.  
- تعديلات اختيارية: تنسيق خلايا مخصص، تبديل السمات، ومعالجة الأخطاء.  
- عينة كود كاملة جاهزة للنسخ واللصق.  

### المتطلبات المسبقة

قبل أن نبدأ، تأكد من أن لديك:

1. متصفح حديث (Chrome أو Edge أو Firefox) – يعتمد Grid.js على ميزات ES6.  
2. مجلد محلي أو بعيد يحتوي على ملف `grid_data.json` (سنظهر الصيغة).  
3. إلمام أساسي بـ HTML و JavaScript – لا شيء معقد، فقط القدرة على فتح ملف `.html` في المتصفح.  

لا أدوات بناء، لا تثبيت npm، لا كود جانب الخادم. هذه هي جمال **create interactive data grid** مع Grid.js: يعمل مباشرة من CDN.

---

## الخطوة 1: إعداد ملف JSON الذي يحدد جدولك

أول شيء تحتاجه هو حمولة JSON تخبر Grid.js ما هي الأعمدة الموجودة وما هي الصفوف التي يجب عرضها. فكر فيها كالمخطط الأساسي لـ **display JSON data table**. إليك مثالًا بسيطًا يمكنك حفظه كـ `grid_data.json` في نفس المجلد الذي يحتوي على ملف HTML الخاص بك:

```json
{
  "columns": ["ID", "Name", "Email", "Country"],
  "rows": [
    [1, "Alice Johnson", "alice@example.com", "USA"],
    [2, "Bob Smith", "bob@example.com", "Canada"],
    [3, "Carlos Ruiz", "carlos@example.com", "Mexico"],
    [4, "Diana Lee", "diana@example.com", "UK"]
  ]
}
```

*لماذا هذا التنسيق؟* يتوقع Grid.js أن تكون `columns` مصفوفة من السلاسل (أو كائنات للتكوين المتقدم) وأن تكون `rows` مصفوفة من المصفوفات حيث يتطابق كل مصفوفة داخلية مع ترتيب الأعمدة. يمكنك بالطبع إضافة المزيد من الأعمدة أو كائنات متداخلة – سيقوم Grid.js بعرضها طالما أن الأشكال متطابقة.

> **نصيحة احترافية:** إذا كنت تجلب البيانات من API، استبدل `fetch('grid_data.json')` بعنوان نقطة النهاية الخاصة بك. يبقى باقي الكود كما هو.

---

## الخطوة 2: تهيئة Grid.js – قلب **how to use gridjs**

الآن بعد أن أصبح مصدر البيانات جاهزًا، نحتاج إلى جلب Grid.js إلى الصفحة وإخبارها كيف تتصرف. هنا نضيف فعليًا وظائف **create interactive data grid** مثل الترميز الصفحات، الترتيب، وزر شريط الأدوات المفيد.

```html
<!-- Load Grid.js from the CDN -->
<script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
<link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet"/>
```

يوفر CDN أحدث نسخة مستقرة، وتضيف سمة Meri­maid مظهرًا نظيفًا وعصريًا جاهزًا للاستخدام. يمكنك استبدالها بـ `gridjs.min.css` إذا كنت تفضل النمط الافتراضي.

بعد ذلك، داخل وسم `<script>`، اجلب JSON وابدأ الشبكة:

```javascript
// Step 2: Initialise Grid.js with pagination, sorting, searching, and a toolbar
fetch('grid_data.json')
  .then(response => response.json())
  .then(data => {
    const grid = new gridjs.Grid({
      columns: data.columns,      // Pull column headers from JSON
      data: data.rows,            // Pull row data from JSON
      pagination: { enabled: true, limit: 10 }, // Show 10 rows per page
      sort: true,                 // Enable column sorting
      search: true,               // Add a search box above the grid
      toolbar: {
        enabled: true,
        items: [
          {
            type: 'button',
            text: 'Help',
            onClick: () => alert('Use the search box to filter rows or click column headers to sort.')
          }
        ]
      },
      // Optional: custom cell formatter for the Email column
      // This demonstrates a deeper dive into how to use Grid.js
      // and shows you can embed HTML inside cells.
      columns: data.columns.map(col => {
        if (col === 'Email') {
          return {
            name: col,
            formatter: cell => gridjs.html(`<a href="mailto:${cell}">${cell}</a>`)
          };
        }
        return col; // Simple string for other columns
      })
    });

    // Step 3: Render the grid into the target container
    grid.render(document.getElementById('grid-container'));
  })
  .catch(err => console.error('Failed to load grid data:', err));
```

### تفصيل الخيارات

| الخيار | ما يفعله | لماذا يهم |
|--------|----------|-----------|
| `pagination` | يقسم الصفوف إلى صفحات (الافتراضي 10 صفوف لكل صفحة) | يحافظ على قابلية استخدام الجداول الكبيرة دون إغراق واجهة المستخدم. |
| `sort` | رؤوس الأعمدة القابلة للنقر لتبديل الترتيب تصاعديًا/تنازليًا | يمكن للمستخدمين العثور بسرعة على الصفوف ذات القيمة الأعلى. |
| `search` | يضيف حقل نص لتصفية الصفوف مباشرة | مفيد للبحث السريع دون إعادة تحميل البيانات. |
| `toolbar` | يضيف أزرار أو قوائم منسدلة مخصصة فوق الشبكة | مثالي لإجراءات مثل “مساعدة”، “تصدير”، أو “تحديث”. |
| `formatter` | يسمح بإرجاع HTML خام للخلية | هنا نحول سلاسل البريد الإلكتروني إلى روابط mailto قابلة للنقر. |

> **لماذا هذا النهج؟** من خلال إبقاء تكوين الشبكة إعلانيًا، يمكنك تعديل السلوك بسهولة دون لمس منطق العرض الأساسي. هذا هو الأسلوب الموصى به لـ **how to use Grid.js** لمعظم المشاريع.

---

## الخطوة 3: عرض الشبكة في صفحتك

السطر الأخير من السكريبت—`grid.render(document.getElementById('grid-container'))`—يُدرج الجدول الكامل الوظائف داخل `<div>` وضعته في مكان ما داخل جسم HTML:

```html
<div id="grid-container"></div>
```

هذا كل شيء. عندما تُحمَّل الصفحة، يجلب المتصفح ملف JSON، يبني كائن Grid.js، ويرسم الجدول التفاعلي على الشاشة. لا تحديثات، ولا استدعاءات خادم بعد التحميل الأولي.

---

## اختياري: تعديل الأنماط والسمات

إذا لم تكن سمة Meri­maid الافتراضية تناسب ذوقك، يمكنك استبدالها بأي من السمات المدمجة (`gridjs.min.css`) أو كتابة CSS خاص بك. على سبيل المثال، لجعل خلفية الرأس رمادية فاتحة:

```css
.gridjs-th {
  background-color: #f5f5f5;
}
```

أضف المقتطف داخل وسم `<style>` أو ملف CSS خارجي. يحترم Grid.js محددات CSS القياسية، لذا لديك سيطرة كاملة على الخطوط، الألوان، والمسافات.

---

## الأخطاء الشائعة وكيفية تجنبها

| المشكلة | العَرَض | الحل |
|---------|--------|------|
| **أخطاء CORS** عند جلب JSON من نطاق آخر | تظهر في وحدة تحكم المتصفح رسالة “Blocked by CORS policy” | استضف ملف JSON على نفس الأصل أو فعّل CORS على الخادم. |
| **مجموعات البيانات الكبيرة تسبب بطء** | يصبح التمرير متقطّعًا، والترقيم بطيئًا | استخدم ترقيم الخادم (`pagination: { server: { url: (prev, page, limit) => … } }`) أو تحميل الصفوف بشكل كسول. |
| **زر شريط الأدوات لا يظهر** | لا يظهر أي زر رغم `toolbar.enabled: true` | تأكد من أنك تستخدم Grid.js الإصدار 2.0+؛ الإصدارات القديمة كان لديها واجهة برمجة شريط أدوات مختلفة. |
| **روابط البريد الإلكتروني غير قابلة للنقر** | يُعيد الـ formatter نصًا عاديًا | أرجع `gridjs.html(...)` بدلاً من سلسلة نصية عادية، كما هو موضح في المثال. |

معالجة هذه القضايا مبكرًا توفر عليك ساعات من تصحيح الأخطاء لاحقًا.

---

## مثال كامل يعمل (جاهز للنسخ واللصق)

فيما يلي ملف HTML كامل يمكنك حفظه كـ `index.html`. افتحه في المتصفح، وسترى عرضًا عمليًا لـ **create interactive data grid** ي**display JSON data table** مع الترتيب، البحث، وزر مساعدة.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Create Interactive Data Grid with Grid.js</title>
  <!-- Grid.js core library -->
  <script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
  <!-- Optional theme – Meri­maid -->
  <link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet"/>
  <style>
    /* Simple custom styling */
    body { font-family: Arial, sans-serif; margin: 20px; }
    .gridjs-container { max-width: 900px; margin: auto; }
    .gridjs-th { background-color: #f0f8ff; }
  </style>
</head>
<body>
  <h1>Create Interactive Data Grid with Grid.js</h1>
  <p>This page demonstrates how to <strong>display JSON data table</strong> using Grid.js. Feel free to edit <code>grid_data.json</code> and refresh.</p>

  <!-- Grid will be rendered here -->
  <div id="grid-container"></div>

  <script>
    // Load JSON data and initialise Grid.js
    fetch('grid_data.json')
      .then(r => r.json())
      .then(data => {
        const grid = new gridjs.Grid({
          columns: data.columns.map(col => {
            // Custom formatter for Email column
            if (col === 'Email') {
              return {
                name: col,
                formatter: cell => gridjs.html(`<a href="mailto:${cell}">${cell}</a>`)
              };
            }
            return col;
          }),
          data: data.rows,
          pagination: { enabled: true, limit: 5 },
          sort: true,
          search: true,
          toolbar: {
            enabled: true,
            items: [
              {
                type: 'button',
                text: 'Formula Help',
                onClick: () => alert('Hover over a cell to see its formula description.')
              }
            ]
          }
        });

        // Render the grid
        grid.render(document.getElementById('grid-container'));
      })
      .catch(err => console.error('Error loading grid data:', err));
  </script>
</body>
</html


## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مصدر يتضمن أمثلة كود كاملة تعمل مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف نهج تنفيذ بديلة في مشاريعك الخاصة.

- [كيفية إنشاء قائمة تحقق من صحة البيانات في Excel باستخدام Aspose.Cells للغة Java: دليل خطوة بخطوة](/cells/english/java/data-validation/excel-data-validation-aspose-cells-java/)
- [كيفية إنشاء مربعات اختيار في Excel باستخدام Aspose.Cells لـ .NET | دليل التحقق من صحة البيانات](/cells/english/net/data-validation/create-checkboxes-net-excel-aspose-cells/)
- [إنشاء واستيراد بيانات XML إلى Excel باستخدام Aspose.Cells للغة Java](/cells/english/java/import-export/create-import-xml-data-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}