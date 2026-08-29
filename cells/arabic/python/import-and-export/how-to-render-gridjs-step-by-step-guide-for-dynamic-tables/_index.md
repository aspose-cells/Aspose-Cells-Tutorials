---
category: general
date: 2026-07-03
description: تعلم كيفية عرض Gridjs في دقائق باستخدام مثال كامل بـ HTML/JS. يتضمن CDN
  لمكتبة Gridjs، التحميل الكسول، ونصائح تكوين JSON.
draft: false
keywords:
- how to render gridjs
- gridjs configuration JSON
- gridjs lazy loading
- gridjs library CDN
- gridjs render method
language: ar
og_description: 'كيفية عرض Gridjs بسرعة: استخدم CDN، احصل على ملف JSON للإعدادات،
  واستدعِ طريقة render. مثالي لجداول البيانات الديناميكية.'
og_title: كيفية عرض Gridjs – دليل التنفيذ الكامل
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Learn how to render Gridjs in minutes with a full HTML/JS example.
    Includes Gridjs library CDN, lazy loading, and configuration JSON tips.
  headline: How to Render Gridjs – Step‑by‑Step Guide for Dynamic Tables
  type: TechArticle
- description: Learn how to render Gridjs in minutes with a full HTML/JS example.
    Includes Gridjs library CDN, lazy loading, and configuration JSON tips.
  name: How to Render Gridjs – Step‑by‑Step Guide for Dynamic Tables
  steps:
  - name: Why Use the CDN?
    text: '- **Performance:** Browsers cache the file across sites, so returning visitors
      may already have it. - **Simplicity:** No bundler configuration, just a single
      `<script>` tag. - **Lazy loading:** You can defer the script with `defer` or
      load it only when needed, which ties into our next step.'
  - name: Breaking Down the Code
    text: '| Line | What It Does | Why It Matters | |------|--------------|----------------|
      | `fetch(''YOUR_DIRECTORY/lazygrid.json'')` | Retrieves the configuration JSON
      via HTTP GET. | Keeps the HTML clean and allows you to change the grid layout
      without touching the page code. | | `.then(response => response'
  - name: Sample `lazygrid.json`
    text: Below is a minimal yet functional configuration file. Save it as `lazygrid.json`
      in the same directory as your HTML (or adjust the fetch path accordingly).
  - name: 1. Using Custom Render Functions
    text: 'Sometimes you need to format a cell—say, add a badge for ages over 28.
      Extend the column definition:'
  - name: 2. Server‑Side Pagination
    text: If your dataset is huge, fetching the entire JSON can be slow. Gridjs supports
      server‑side pagination—just set `pagination.server` to `true` and implement
      an API endpoint that returns slices of data based on `page` and `limit` query
      parameters.
  - name: 3. Styling with CSS Variables
    text: 'The Mermaid theme uses CSS variables for colors. Override them in a `<style>`
      block:'
  - name: 4. Accessibility Considerations
    text: Gridjs adds ARIA attributes automatically, but you can enhance keyboard
      navigation by ensuring your placeholder `<div>` is focusable (`tabindex="0"`).
      This helps screen‑reader users interact with the table.
  type: HowTo
tags:
- JavaScript
- Front‑end
- Data Tables
title: كيفية عرض Gridjs – دليل خطوة بخطوة للجداول الديناميكية
url: /ar/python/import-and-export/how-to-render-gridjs-step-by-step-guide-for-dynamic-tables/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية عرض Gridjs – دليل خطوة بخطوة للجداول الديناميكية

هل تساءلت يومًا **كيف تعرض Gridjs** على صفحة HTML بسيطة دون استدعاء إطار عمل ثقيل؟ لست وحدك. يحتاج العديد من المطورين إلى جدول خفيف الوزن وقابل للفرز يمكن إمداده بالبيانات من ملف JSON، وGridjs يجعل ذلك سهلًا للغاية. في هذا الدرس سنستعرض كل سطر تحتاجه، بدءًا من تحميل مكتبة Gridjs عبر CDN إلى جلب تكوين JSON بشكل كسول وأخيرًا استدعاء طريقة render.

سنضيف أيضًا بعض نصائح الممارسات الأفضل—مثل لماذا يمكن لتحميل تكوين Gridjs بشكل كسول أن يحسن سرعة الصفحة، وكيفية هيكلة ملف JSON بحيث تعمل طريقة render الخاصة بـ Gridjs بسلاسة. في النهاية ستحصل على شبكة كاملة الوظائف يمكنك إدراجها في أي مشروع.

## ما ستبنيه

- صفحة HTML بسيطة تجلب Gridjs من CDN  
- ملف `lazygrid.json` يحدد الأعمدة والبيانات والإضافات الاختيارية  
- جافاسكريبت يجلب الـ JSON، ينشئ مثال Gridjs، ويعرضه في عنصر نائب  

بدون أدوات بناء، بدون npm، مجرد HTML بسيط وقليل من جافاسكريبت الفانيليا. مثالي للمواقع الثابتة، بوابات الوثائق، أو النماذج الأولية السريعة.

## المتطلبات المسبقة

- فهم أساسي لـ HTML و JavaScript (بدون أطر عمل مطلوبة)  
- خادم ويب أو بيئة تطوير محلية يمكنها خدمة الملفات الثابتة (مثل VS Code Live Server)  
- ملف `lazygrid.json` موجود في مكان يمكن للمتصفح الوصول إليه  

إذا كنت مرتاحًا مع هذه المتطلبات، لنبدأ.

## الخطوة 1: تضمين مكتبة Gridjs عبر CDN

أسرع طريقة للحصول على Gridjs في الصفحة هي الإشارة إلى حزمة UMD الخاصة به من CDN. هذا يلغي الحاجة لتثبيت npm ويحافظ على خفة الدرس.

```html
<!-- Step 1: Include the Gridjs library -->
<script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
<link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet" />
```

> **نصيحة احترافية:** ورقة الأنماط `theme/mermaid.min.css` تضيف مظهرًا نظيفًا وعصريًا. استبدلها بموضوع آخر إذا كنت تفضل نمطًا مختلفًا.

### لماذا نستخدم CDN؟

- **الأداء:** المتصفحات تخزن الملف في الذاكرة المؤقتة عبر المواقع، لذا قد يكون الزوار العائدون قد حصلوا عليه بالفعل.  
- **البساطة:** لا حاجة لإعداد bundler، مجرد وسم `<script>` واحد.  
- **التحميل الكسول:** يمكنك تأخير تحميل السكريبت باستخدام `defer` أو تحميله فقط عند الحاجة، وهذا يتماشى مع الخطوة التالية.

## الخطوة 2: إضافة عنصر نائب للشبكة

يحتاج Gridjs إلى عقدة DOM لتثبيت الجدول. أنشئ `<div>` بمعرف فريد—هذا هو المكان الذي ستُحقن فيه طريقة render الخاصة بـ Gridjs علامة الجدول.

```html
<!-- Step 2: Placeholder where Gridjs will appear -->
<div id="grid"></div>
```

يمكنك تنسيق هذا الحاوية باستخدام CSS إذا احتجت إلى عرض أو هوامش مخصصة. في الوقت الحالي، سيحافظ النمط الافتراضي من الثيم على ترتيب الأمور.

## الخطوة 3: تحميل ملف JSON لتكوين Gridjs وعرض الشبكة

هنا يحدث السحر. سنجلب ملف JSON (`lazygrid.json`) الذي يصف الأعمدة، صفوف البيانات، وأي إضافات تريدها. ثم سننشئ مثال Gridjs بهذا التكوين ونستدعي طريقة render.

```html
<!-- Step 3: Fetch config and render Gridjs -->
<script>
  // Step 3.1: Pull the JSON config (replace the path as needed)
  fetch('YOUR_DIRECTORY/lazygrid.json')
    .then(response => {
      if (!response.ok) {
        throw new Error('Network response was not ok');
      }
      return response.json();
    })
    .then(config => {
      // Step 3.2: Create a Gridjs instance using the fetched configuration
      const grid = new GridJs(config);
      // Step 3.3: Render the grid inside the placeholder element
      grid.render(document.getElementById('grid'));
    })
    .catch(error => console.error('Error loading Gridjs config:', error));
</script>
```

### تحليل الكود

| السطر | ما يفعله | لماذا يهم |
|------|--------------|----------------|
| `fetch('YOUR_DIRECTORY/lazygrid.json')` | يجلب ملف JSON الخاص بالتكوين عبر طلب HTTP GET. | يحافظ على نظافة HTML ويسمح لك بتغيير تخطيط الشبكة دون تعديل كود الصفحة. |
| `.then(response => response.json())` | يحوّل الاستجابة إلى كائن JavaScript. | يضمن أنك تمرر كائنًا صحيحًا إلى Gridjs. |
| `new GridJs(config)` | ينشئ مثال Gridjs باستخدام التكوين المقدم. | هذه هي نقطة دخول **طريقة render الخاصة بـ gridjs**؛ التكوين يحدد الأعمدة والبيانات والإضافات. |
| `grid.render(document.getElementById('grid'))` | يدرج الجدول داخل `<div id="grid">`. | الخطوة النهائية التي **تظهر Gridjs** على الشاشة. |
| `.catch(...)` | يتعامل مع أخطاء الشبكة أو التحليل بشكل لطيف. | يمنع تحطم الصفحة بصمت ويعطيك معلومات تصحيح الأخطاء. |

### مثال `lazygrid.json`

فيما يلي ملف تكوين بسيط ولكنه عملي. احفظه باسم `lazygrid.json` في نفس دليل ملف HTML (أو عدل مسار الـ fetch وفقًا لذلك).

```json
{
  "columns": [
    "Name",
    "Email",
    { "id": "age", "name": "Age", "type": "number" }
  ],
  "data": [
    ["Alice", "alice@example.com", 30],
    ["Bob", "bob@example.com", 25],
    ["Carol", "carol@example.com", 27]
  ],
  "search": true,
  "pagination": {
    "enabled": true,
    "limit": 5
  }
}
```

- **gridjs configuration JSON**: يمكن أن يحتوي مصفوفة `columns` على سلاسل نصية بسيطة أو كائنات لمزيد من التحكم (مثل renderers مخصصة).  
- **gridjs lazy loading**: بتخزين هذا الـ JSON منفصلًا، يمكنك استبداله دون الحاجة لإعادة نشر صفحة HTML.  
- **gridjs render method**: استدعاء `grid.render(...)` يقرأ هذا التكوين ويبني الجدول ديناميكيًا.

## الخطوة 4: التحقق من النتيجة

افتح ملف HTML في المتصفح. يجب أن ترى جدولًا قابلًا للبحث، مع ترقيم للصفحات، يتطابق مع البيانات في `lazygrid.json`. يضيف الثيم Mermaid تأثيرات تظليل خفيفة وتأثيرات تمرير الفأرة.

**الناتج المتوقع:**

| الاسم  | البريد الإلكتروني   | العمر |
|-------|----------------------|-------|
| Alice | alice@example.com   | 30    |
| Bob   | bob@example.com     | 25    |
| Carol | carol@example.com   | 27    |

إذا لم تظهر الجدول:

1. افتح وحدة تحكم المتصفح (F12) وابحث عن الأخطاء.  
2. تأكد من أن المسار في `fetch('YOUR_DIRECTORY/lazygrid.json')` يشير إلى الموقع الصحيح.  
3. تحقق من تحميل سكريبت CDN (افحص تبويب Network).  

## نصائح متقدمة وحالات خاصة

### 1. استخدام دوال render مخصصة

أحيانًا تحتاج إلى تنسيق خلية—مثلاً، إضافة شارة للأعمار فوق 28. قم بتمديد تعريف العمود:

```json
{
  "id": "age",
  "name": "Age",
  "formatter": (cell) => {
    return cell > 28 ? `<span style="color:red;">${cell}</span>` : cell;
  }
}
```

> **ملاحظة:** يجب أن يكون الـ formatter دالة JavaScript، لذا ستحتاج إلى تضمين التكوين مباشرة في السكريبت أو تحميله كـ module إذا أردت الاحتفاظ به في JSON.

### 2. الترميز الجانبي للخادم (Server‑Side Pagination)

إذا كان مجموعة البيانات ضخمة، قد يكون جلب الـ JSON بالكامل بطيئًا. يدعم Gridjs الترميز الجانبي للخادم—فقط عيّن `pagination.server` إلى `true` ونفّذ نقطة API تُعيد أجزاء من البيانات بناءً على معلمات `page` و `limit`.

### 3. التنسيق باستخدام متغيرات CSS

يستخدم ثيم Mermaid متغيرات CSS للألوان. يمكنك تجاوزها داخل وسم `<style>`:

```html
<style>
  :root {
    --gridjs-header-bg: #2c3e50;
    --gridjs-header-color: #ecf0f1;
  }
</style>
```

### 4. اعتبارات إمكانية الوصول

يضيف Gridjs سمات ARIA تلقائيًا، لكن يمكنك تحسين التنقل عبر لوحة المفاتيح بالتأكد من أن العنصر `<div>` النائب قابل للتركيز (`tabindex="0"`). هذا يساعد مستخدمي قارئات الشاشة على التفاعل مع الجدول.

## مثال عملي كامل

بجمع كل ما سبق، إليك ملف HTML واحد يمكنك نسخه ولصقه وتشغيله محليًا.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>How to Render Gridjs Demo</title>
  <!-- Gridjs library CDN -->
  <script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
  <link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet" />
  <style>
    /* Optional custom theme tweaks */
    :root {
      --gridjs-header-bg: #34495e;
      --gridjs-header-color: #ecf0f1;
    }
  </style>
</head>
<body>
  <!-- Placeholder for the grid -->
  <div id="grid"></div>

  <!-- Fetch config and render Gridjs -->
  <script>
    fetch('lazygrid.json')
      .then(r => r.ok ? r.json() : Promise.reject('Failed to load'))
      .then(cfg => {
        const grid = new GridJs(cfg);
        grid.render(document.getElementById('grid'));
      })
      .catch(err => console.error(err));
  </script>

  <!-- Optional screenshot for documentation -->
  <img src="gridjs-screenshot.png" alt="Screenshot demonstrating how to render Gridjs grid" style="display:none;">
</body>
</html>
```

احفظه باسم `index.html` بجوار `lazygrid.json`، افتحه في المتصفح، وستظهر الشبكة فورًا.

## الخلاصة

الآن لديك إجابة واضحة من البداية إلى النهاية حول **كيفية عرض Gridjs**: تحميل مكتبة Gridjs عبر CDN، توفير `gridjs configuration JSON`، جلبه بشكل كسول، إنشاء كائن Gridjs، واستدعاء `gridjs render method`. هذه الطريقة تحافظ على نظافة HTML، تستفيد من التحميل الكسول لأداء أفضل، وتمنحك تحكمًا كاملًا في الأعمدة والبيانات والإضافات.

ما التالي؟ جرّب إضافة:

- **gridjs lazy loading** لمجموعات بيانات كبيرة عبر الترميز الجانبي للخادم.  
- renderers مخصصة للخلايا لعرض مخططات أو أشرطة تقدم.  
- إضافات تصدير لتمكين المستخدمين من تنزيل ملفات CSV أو Excel.  

لا تتردد في التجربة، وإذا واجهت أي صعوبات، اترك تعليقًا أدناه. Happy coding!

## ماذا يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مصدر يتضمن أمثلة شاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [How to Render Excel Sheets as Images Using Aspose.Cells .NET for Seamless Data Visualization](/cells/english/net/import-export/render-excel-sheets-images-aspose-cells-dotnet/)
- [How to Render Excel Sheets as Images Using Aspose.Cells for Java (Workbook Operations)](/cells/english/java/workbook-operations/render-excel-sheets-images-aspose-cells-java/)
- [How to Efficiently Filter Data While Loading Excel Workbooks Using Aspose.Cells in Java](/cells/english/java/data-analysis/filter-data-excel-aspose-cells-java-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}