---
category: general
date: 2026-06-30
description: كيفية إنشاء GridJS بسهولة مع مثال كامل بلغة JavaScript، يغطي تكوين GridJS،
  إعداد الحاوية، وعملية العرض.
draft: false
keywords:
- how to create gridjs
- gridjs configuration
- gridjs render
- gridjs JavaScript
- gridjs container
language: ar
og_description: كيفية إنشاء gridjs بسهولة مع مثال كامل بلغة JavaScript، يغطي تكوين
  gridjs، إعداد الحاوية، وعملية العرض.
og_title: كيفية إنشاء Gridjs – دليل كامل لشبكة جافاسكريبت
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: How to create gridjs easily with a full JavaScript example, covering
    gridjs configuration, container setup, and render process.
  headline: How to Create Gridjs – Complete JavaScript Grid Guide
  type: TechArticle
- description: How to create gridjs easily with a full JavaScript example, covering
    gridjs configuration, container setup, and render process.
  name: How to Create Gridjs – Complete JavaScript Grid Guide
  steps:
  - name: Why this configuration matters
    text: '- **Columns** – define the header text and optional width. Without this,
      Gridjs would infer column names from the first data row, which is often less
      readable. - **Data** – an array of rows, each row being an array of cell values.
      You could also supply an async function that fetches data from an API'
  - name: Expected Output
    text: '``` +----+----------------+---------------------+--------+ | ID | Name
      | Email | Role | +----+----------------+---------------------+--------+ | 1
      | Alice Johnson | alice@example.com | Admin | | 2 | Bob Smith | bob@example.com
      | Editor | +----+----------------+---------------------+--------+ [←] [1]'
  - name: Loading Data Asynchronously
    text: 'If your data lives on a server, replace the static `data` array with a
      function that returns a Promise:'
  - name: Custom Cell Rendering
    text: 'Sometimes you need icons, buttons, or formatted dates inside cells. Use
      the `formatter` property on a column:'
  - name: Multiple Grids on One Page
    text: 'Just repeat steps 2‑5 with different container IDs:'
  type: HowTo
tags:
- gridjs
- JavaScript
- web‑development
title: كيفية إنشاء Gridjs – دليل شامل لشبكة JavaScript
url: /ar/python/integration-and-interoperability/how-to-create-gridjs-complete-javascript-grid-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية إنشاء Gridjs – دليل كامل لشبكة JavaScript

هل تساءلت يومًا **how to create gridjs** ورأيت جدول بيانات أنيق على صفحتك فورًا؟ لست وحدك. يواجه العديد من المطورين صعوبة عندما يحاولون إعداد Gridjs لأول مرة، خاصةً حول كائن التكوين واستدعاء render. الخبر السار؟ الأمر سهل جدًا بمجرد معرفة الخطوات الصحيحة.

في هذا البرنامج التعليمي سنستعرض مثالًا واقعيًا يوضح **how to create gridjs** من الصفر، وكيفية إنشاء **gridjs configuration** صحيحة، وكيفية ربط الشبكة بـ **gridjs container**، وأخيرًا كيفية تشغيل **gridjs render**. في النهاية ستحصل على شبكة كاملة الوظائف يمكنك إدراجها في أي مشروع—بدون غموض، فقط كود واضح.

## ما ستتعلمه

- إعداد صفحة HTML بسيطة جاهزة لـ Gridjs.
- كتابة كائن **gridjs configuration** يحدد الأعمدة والبيانات والخيارات.
- إرفاق نسخة Gridjs بعنصر **gridjs container**.
- استدعاء **gridjs render** لعرض الجدول.
- تعديل الإعدادات الشائعة (التصفية، الترتيب، التنسيق) وتجنب الأخطاء الشائعة.

لا تحتاج إلى أدوات بناء خارجية؛ كل شيء يعمل في المتصفح باستخدام وسم script واحد. لنبدأ.

## المتطلبات المسبقة

قبل أن نبدأ، تأكد من أن لديك:

1. متصفح حديث (Chrome, Edge, Firefox, Safari) – أي متصفح يدعم ES6.
2. معرفة أساسية بـ HTML و JavaScript – لا تحتاج إلى إطار عمل.
3. الوصول إلى مكتبة Gridjs – سنجلبها من CDN، لذا لا حاجة لتثبيت npm.

هذا كل شيء. إذا كان لديك صفحة تريد تحسينها، يمكنك لصق المقاطع مباشرةً.

## الخطوة 1: إضافة موارد Gridjs إلى صفحتك

أولاً، نحتاج إلى تحميل ملفات CSS و JavaScript الخاصة بـ Gridjs. نسخة CDN خفيفة ومثالية للعروض السريعة.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>How to Create Gridjs Example</title>
  <!-- Gridjs CSS -->
  <link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet" />
</head>
<body>
  <!-- The grid will appear inside this div -->
  <div id="grid"></div>

  <!-- Gridjs JS -->
  <script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
```

> **نصيحة احترافية:** يمنح نمط Mermaid الجدول مظهرًا نظيفًا وعصريًا دون أي CSS إضافي. يمكنك استبداله بـ `classic.min.css` إذا كنت تفضل نمطًا مختلفًا.

## الخطوة 2: تعريف **gridjs container**

**gridjs container** هو مجرد `<div>` عادي سيستضيف الجدول المُعرض. في الشيفرة أعلاه أنشأنا بالفعل `<div id="grid"></div>`. سمة `id` مهمة لأنها ستُستخدم لربط نسخة Gridjs لاحقًا.

إذا كنت بحاجة إلى عدة شبكات على نفس الصفحة، أعط كل حاوية معرفًا فريدًا (`grid1`, `grid2`, …) وكرر منطق الربط لكل واحدة.

## الخطوة 3: إنشاء كائن **gridjs configuration**

الآن يأتي جوهر **how to create gridjs** – التكوين. هذا الكائن البسيط في JavaScript يخبر Gridjs ما هي الأعمدة التي يجب عرضها، وما هي البيانات التي يجب ملؤها، وأي الميزات يجب تمكينها.

```html
<script>
  // Step 3: Your gridjs configuration (replace with real data)
  const config = {
    columns: [
      { name: 'ID', width: '50px' },
      { name: 'Name' },
      { name: 'Email' },
      { name: 'Role' }
    ],
    data: [
      [1, 'Alice Johnson', 'alice@example.com', 'Admin'],
      [2, 'Bob Smith', 'bob@example.com', 'Editor'],
      [3, 'Carol White', 'carol@example.com', 'Viewer'],
      [4, 'David Brown', 'david@example.com', 'Admin']
    ],
    pagination: {
      limit: 2   // Show 2 rows per page
    },
    search: true,          // Enable client‑side search box
    sort: true,            // Allow column sorting
    language: {
      'search': {
        'placeholder': '🔍 Search…'
      },
      'pagination': {
        'previous': '←',
        'next': '→',
        'showing': 'Showing',
        'results': () => 'records'
      }
    }
  };
</script>
```

### لماذا هذا التكوين مهم

- **Columns** – تحديد نص العنوان والعرض الاختياري. بدون ذلك، سيستنتج Gridjs أسماء الأعمدة من الصف الأول من البيانات، وهو غالبًا أقل قابلية للقراءة.
- **Data** – مصفوفة من الصفوف، كل صف هو مصفوفة من قيم الخلايا. يمكنك أيضًا توفير دالة غير متزامنة تجلب البيانات من API؛ المكتبة ستتعامل مع الوعود تلقائيًا.
- **Pagination** – يحد عدد الصفوف في كل صفحة، مما يمنع الجداول الضخمة من إغراق واجهة المستخدم.
- **Search & Sort** – تشغيل الميزات التفاعلية باستخدام قيمة منطقية واحدة، مما يوفر عليك كتابة معالجات مخصصة.
- **Language** – تخصيص سلاسل واجهة المستخدم، مثالي للتعريب أو العلامة التجارية.

لا تتردد في استبدال مصفوفة البيانات الثابتة بنداء fetch لاحقًا؛ بقية الخطوات ستظل كما هي.

## الخطوة 4: إنشاء نسخة Gridjs وربطها بـ **gridjs container**

مع إعداد التكوين، ننشئ كائنًا جديدًا `GridJs.Grid` (اسم الصنف هو `gridjs.Grid` في بناء UMD) ونشير إليه إلى عنصر الحاوية الخاص بنا.

```html
<script>
  // Step 4: Create a Gridjs instance bound to the container
  const grid = new gridjs.Grid(document.getElementById('grid'), config);
</script>
```

لاحظ أننا استخدمنا `document.getElementById('grid')`—هذا هو **gridjs container** الذي عرفناه سابقًا. إذا كان لديك عدة حاويات، كرر هذا السطر مع المعرف المناسب.

## الخطوة 5: تشغيل استدعاء **gridjs render**

القطعة الأخيرة من اللغز هي طريقة **gridjs render**. تأخذ التكوين الذي مررناه سابقًا وتُدرج `<table>` مُنسق بالكامل داخل الحاوية.

```html
<script>
  // Step 5: Render the grid inside the container
  grid.render();
</script>
</body>
</html>
```

هذا كل شيء! عند فتح الصفحة في المتصفح، سترى جدولًا قابلًا للبحث ومقسمًا إلى صفحات يحتوي على الأربعة صفوف التي عرفناها. يظهر صندوق البحث تلقائيًا في الأعلى، وتظهر أدوات التصفية في الأسفل.

### النتيجة المتوقعة

```
+----+----------------+---------------------+--------+
| ID | Name           | Email               | Role   |
+----+----------------+---------------------+--------+
| 1  | Alice Johnson  | alice@example.com   | Admin  |
| 2  | Bob Smith      | bob@example.com     | Editor |
+----+----------------+---------------------+--------+
[←] [1] [2] [→]   Search: 🔍 Search…
```

ستتغير واجهة المستخدم عندما تكتب في صندوق البحث أو تنقر على رؤوس الأعمدة للترتيب.

## الاختلافات الشائعة وحالات الحافة

### تحميل البيانات بشكل غير متزامن

إذا كانت بياناتك موجودة على خادم، استبدل مصفوفة `data` الثابتة بدالة تُعيد Promise:

```js
const config = {
  columns: ['ID', 'Name', 'Email', 'Role'],
  data: () => fetch('/api/users')
                .then(res => res.json())
                .then(users => users.map(u => [u.id, u.name, u.email, u.role])),
  pagination: { limit: 10 },
  search: true,
  sort: true
};
```

سيعرض Gridjs مؤشر تحميل حتى يتم حل الـ Promise، ثم يُظهر الجدول تلقائيًا.

### تخصيص عرض الخلايا

أحيانًا تحتاج إلى أيقونات أو أزرار أو تواريخ مُنسقة داخل الخلايا. استخدم خاصية `formatter` في العمود:

```js
{
  name: 'Role',
  formatter: (cell) => {
    const color = cell === 'Admin' ? 'red' : 'gray';
    return gridjs.h('span', { style: { color } }, cell);
  }
}
```

المساعد `gridjs.h` ينشئ عناصر DOM افتراضية دون الحاجة إلى استيراد React.

### عدة شبكات في صفحة واحدة

ما عليك سوى تكرار الخطوات 2‑5 باستخدام معرفات حاويات مختلفة:

```html
<div id="usersGrid"></div>
<div id="ordersGrid"></div>

<script>
  const usersGrid = new gridjs.Grid(document.getElementById('usersGrid'), usersConfig);
  const ordersGrid = new gridjs.Grid(document.getElementById('ordersGrid'), ordersConfig);
  usersGrid.render();
  ordersGrid.render();
</script>
```

كل شبكة تعمل بشكل مستقل، لذا يمكنك دمج حدود التصفية، مجموعات الأعمدة، وحتى الأنماط.

## نصائح احترافية ومخاطر يجب تجنبها

- **لا تنسَ CSS** – بدون ورقة الأنماط سيظهر الجدول كجدول HTML عادي، مما يفقده جميع التنسيقات الجميلة وعناصر التحكم في التصفية.
- **تجنب تكرار المعرفات** – يجب أن يكون لكل **gridjs container** معرف فريد؛ وإلا سيستبدل Gridjs النسخة الأولى.
- **راقب بنية البيانات** – يجب أن يتطابق عدد الأعمدة مع عدد الخلايا في كل صف؛ المصفوفات غير المتطابقة تسبب أخطاء تخطيط صامتة.
- **استخدم `gridjs.h` للخلايا المعقدة** – محاولة حقن سلاسل HTML خام قد تُعطّل خوارزمية مقارنة الـ Virtual DOM.
- **انتبه إلى الإصدار** – رابط CDN أعلاه يشير إلى أحدث إصدار 5.x (حتى يونيو 2026). إذا قمت بتثبيت نسخة أقدم، قد تكون بعض الخيارات (مثل `language`) مفقودة.

## مثال كامل يعمل (نسخ‑لصق)

فيما يلي ملف HTML كامل يمكنك حفظه باسم `gridjs-demo.html` وفتحه مباشرةً في المتصفح.



## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مصدر يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [Aspose.Cells for Java&#58; كيفية إنشاء وتنسيق دفاتر Excel بكفاءة](/cells/english/java/getting-started/aspose-cells-java-workbook-creation-guide/)
- [كيفية إنشاء وتصدير Excel إلى HTML باستخدام Aspose.Cells Java | دليل عمليات دفتر العمل](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)
- [كيفية إنشاء ودمج دفاتر Excel باستخدام Aspose.Cells for Java | دليل كامل](/cells/english/java/workbook-operations/create-merge-excel-workbooks-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}