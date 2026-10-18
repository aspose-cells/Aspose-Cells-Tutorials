---
category: general
date: 2026-05-30
description: تعلم كيفية إنشاء كائن GridJsOptions وتكوين خيارات الشبكة باستخدام JavaScript
  للجداول الديناميكية. دليل خطوة بخطوة مع الشيفرة الكاملة.
draft: false
keywords:
- create gridjsoptions instance
- configure grid options javascript
- gridjs initialization
- javascript data grid settings
- dynamic table configuration
language: ar
og_description: إنشاء كائن GridJsOptions وتكوين خيارات الشبكة في جافا سكريبت خلال
  دقائق. مثال كامل، شروحات، ونصائح لأفضل الممارسات.
og_title: إنشاء مثيل GridJsOptions – تكوين خيارات الشبكة في JavaScript
schemas:
- author: Aspose
  dateModified: '2026-05-30'
  description: Learn how to create GridJsOptions instance and configure grid options
    JavaScript for dynamic tables. Step‑by‑step guide with full code.
  headline: Create GridJsOptions Instance – Configure Grid Options JavaScript
  type: TechArticle
- description: Learn how to create GridJsOptions instance and configure grid options
    JavaScript for dynamic tables. Step‑by‑step guide with full code.
  name: Create GridJsOptions Instance – Configure Grid Options JavaScript
  steps:
  - name: Prerequisites
    text: '- A modern browser (Chrome, Edge, Firefox) – no build tools required. -
      Basic familiarity with JavaScript (variables, objects, DOM). - The Grid.js library
      (we’ll pull it from a CDN).'
  - name: Why this matters
    text: Loading the library from a CDN ensures you always get the latest stable
      version without a local install. The `<div id="grid-wrapper">` is the placeholder
      that the Grid.js constructor will target once we **configure grid options JavaScript**.
  - name: What you’re configuring
    text: '- **NumberFormatAlignment** – aligns numeric strings automatically. - **Pagination**
      – controls page size and navigation. - **Sorting** – toggles column sorting.
      - **Columns** – defines headers, data types, and custom renderers.'
  - name: Edge‑case note
    text: If you later supply a custom data source that already returns paginated
      results, you’ll want to disable Grid.js’s built‑in pagination to avoid double‑paging.
      Simply set `gridOptions.Pagination.enabled = false;`.
  - name: Expected Output
    text: 'When you open the HTML file in a browser you should see:'
  type: HowTo
tags:
- gridjs
- javascript
- data‑grid
title: إنشاء مثيل GridJsOptions – تكوين خيارات الشبكة في JavaScript
url: /ar/net/link-and-configuration-operations/create-gridjsoptions-instance-configure-grid-options-javascr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء كائن GridJsOptions – تكوين خيارات الشبكة باستخدام JavaScript

هل تساءلت يوماً كيف **تنشئ كائن GridJsOptions** دون البحث في وثائق متفرقة؟ لست وحدك. عندما تحتاج إلى جدول أنيق وقابل للفرز على صفحة ويب، فإن إتقان طريقة **configure grid options JavaScript** هو الخطوة الأولى نحو واجهة مستخدم مصقولة.

في هذا الدرس سنستعرض الشيفرة الدقيقة التي تحتاجها، نشرح لماذا كل إعداد مهم، ونظهر لك مثالًا كاملاً قابلاً للتنفيذ. في النهاية ستشعر بالراحة في إنشاء كائن GridJsOptions، تعديل المحاذاة، التقسيم إلى صفحات، وحتى مُعَدِّلات الخلايا المخصصة—كل ذلك باستخدام JavaScript عادي.

## ما ستتعلمه

- كيفية **إنشاء كائن GridJsOptions** من الصفر.
- الخصائص الأساسية التي تتيح لك **configure grid options JavaScript** (الفرز، التقسيم إلى صفحات، تنسيق الأرقام، إلخ).
- الأخطاء الشائعة (مثل خلط الأنواع النصية والعددية) وكيفية تجنبها.
- صفحة HTML كاملة يمكنك نسخها‑لصقها في أي مشروع ورؤية النتائج فورًا.

### المتطلبات المسبقة

- متصفح حديث (Chrome, Edge, Firefox) – لا حاجة لأدوات بناء.
- معرفة أساسية بـ JavaScript (المتغيرات، الكائنات، DOM).
- مكتبة Grid.js (سنحصل عليها من CDN).

إذا كان أي من ذلك غير مألوف لك، لا تقلق—كل خطوة تتضمن مراجعة سريعة.

---

## الخطوة 1: تحميل Grid.js وإعداد هيكل HTML

قبل أن نتمكن من **إنشاء كائن GridJsOptions**، نحتاج إلى المكتبة نفسها. أسهل طريقة هي استخدام CDN الرسمي. أدناه هيكل HTML بسيط يخصص أيضًا عنصر `<div>` حيث سيُعرض الجدول.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Grid.js Demo – Configuring Options</title>
  <!-- Grid.js CSS -->
  <link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet" />
</head>
<body>
  <h2>Simple Data Grid</h2>
  <div id="grid-wrapper"></div>

  <!-- Grid.js JS -->
  <script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
  <!-- Our custom script will go here -->
  <script src="grid-config.js"></script>
</body>
</html>
```

> **نصيحة احترافية:** ضع رابط CSS قبل أنماطك الخاصة حتى يتم تحميل سمة Grid الافتراضية بشكل صحيح.

### لماذا هذا مهم

تحميل المكتبة من CDN يضمن حصولك دائمًا على أحدث نسخة مستقرة دون تثبيت محلي. العنصر `<div id="grid-wrapper">` هو العنصر النائب الذي سيستهدفه مُنشئ Grid.js بمجرد **configure grid options JavaScript**.

---

## الخطوة 2: إنشاء كائن GridJsOptions جديد

الآن يأتي جوهر الدرس: السطر الذي **ينشئ كائن GridJsOptions** فعليًا. في ملف منفصل يُسمى `grid-config.js` (مُشار إليه في HTML أعلاه) سنكتب:

```javascript
// grid-config.js

// Step 2: Create a new GridJsOptions instance to configure grid behavior
const gridOptions = new GridJsOptions();
```

هذا السطر الواحد يمنحك كائنًا نظيفًا يمكنك البدء بملئه بالإعدادات. فكر في `gridOptions` كلوحة التحكم لكل **feature** ستُفعّلها لاحقًا.

### ما الذي تقوم بتكوينه

- **NumberFormatAlignment** – يضبط محاذاة السلاسل الرقمية تلقائيًا.
- **Pagination** – يتحكم في حجم الصفحة والتنقل بينها.
- **Sorting** – يتيح فرز الأعمدة.
- **Columns** – يحدد رؤوس الأعمدة، أنواع البيانات، ومُعَدِّلات مخصصة.

يمكنك إضافة أي من هذه الخصائص قبل أن تُنشئ الـ Grid فعليًا.

---

## الخطوة 3: تفعيل محاذاة الأرقام (متطلب شائع)

معظم الجداول تحتوي على مزيج من النصوص والأرقام. بشكل افتراضي، يقوم Grid.js بمحاذاة كل شيء إلى اليسار، وهذا يبدو غريبًا **للقيم المالية**. لت **configure grid options JavaScript** بشكل صحيح، فعّل علم `NumberFormatAlignment`:

```javascript
// Enable left/right alignment for numeric strings
gridOptions.NumberFormatAlignment = true;
```

لماذا نفعل ذلك؟ عندما يكون العلم true، يقوم Grid.js بفحص كل خلية؛ إذا بدت كرقم (مثلاً “1234”، “12.34%”)، فإنه يضبط محاذاتها تلقائيًا إلى اليمين. هذه اللمسة الصغيرة تجعل التقارير أكثر قابلية للقراءة.

---

## الخطوة 4: إضافة التقسيم إلى صفحات والفرز

جدول حقيقي نادرًا ما يتسع لشاشة واحدة. لنُفعّل التقسيم إلى صفحات (10 صفوف لكل صفحة) ونسمح للمستخدمين بفرز أي عمود.

```javascript
gridOptions.Pagination = {
  limit: 10,          // rows per page
  enabled: true
};

gridOptions.Sort = true;   // enables click‑to‑sort on all columns
```

### ملاحظة حول الحالات الخاصة

إذا قمت لاحقًا بتوفير مصدر بيانات مخصص يُعيد نتائج مُقسَّمة إلى صفحات بالفعل، فستحتاج إلى تعطيل التقسيم المدمج في Grid.js لتجنب الازدواجية. ببساطة عيّن `gridOptions.Pagination.enabled = false;`.

---

## الخطوة 5: تعريف الأعمدة والبيانات النموذجية

الآن سنزود الجدول ببيانات تجريبية ونخبره ما الذي تمثله كل عمود. هنا يبرز نمط **create gridjsoptions instance**—كل شيء يعيش داخل كائن واحد منظم.

```javascript
// Sample data array of objects
const sampleData = [
  { id: 1, name: "Alice", salary: "54000", department: "Engineering" },
  { id: 2, name: "Bob",   salary: "47000", department: "Marketing" },
  { id: 3, name: "Cara",  salary: "62000", department: "Design" },
  // ...more rows as needed
];

// Column definitions
gridOptions.Columns = [
  { id: "id",   name: "ID",          width: "5%" },
  { id: "name", name: "Employee",    width: "35%" },
  { id: "salary", name: "Salary ($)", width: "20%" },
  { id: "department", name: "Dept.",  width: "40%" }
];

// Attach data source
gridOptions.Data = sampleData;
```

لاحظ أننا حافظنا على قيم `id` للأعمدة متطابقة مع المفاتيح في كل كائن بيانات. هذا الاتفاق يسمح لـ Grid.js بربط القيم تلقائيًا، مما يوفر عليك كتابة مُعَدِّل مخصص لكل عمود.

---

## الخطوة 6: إنشاء الـ Grid باستخدام الخيارات الخاصة بنا

نحن الآن **configure grid options javascript** بتمرير كائن `gridOptions` إلى مُنشئ Grid. سيُعرض الجدول داخل `<div id="grid-wrapper">` الذي أعددناه مسبقًا.

```javascript
// Create the Grid instance using the previously built options
const grid = new Grid(gridOptions);

// Render the grid into the page
grid.render(document.getElementById("grid-wrapper"));
```

هذا كل شيء. العملية بأكملها—من **create gridjsoptions instance** إلى العرض—تستغرق أقل من دقيقة من الترميز.

### النتيجة المتوقعة

عند فتح ملف HTML في المتصفح يجب أن ترى:

- صف رأس يحتوي على “ID”، “Employee”، “Salary ($)”، “Dept.”.
- أرقام الرواتب محاذية إلى اليمين (بفضل `NumberFormatAlignment`).
- أدوات التقسيم إلى صفحات في الأسفل (إذا أضفت أكثر من عشرة صفوف).
- رؤوس أعمدة قابلة للنقر للفرز تصاعديًا/تنازليًا.

إذا ظهر أي شيء غير صحيح، افتح وحدة تحكم المتصفح (F12) وابحث عن رسائل الأخطاء—معظم الأخطاء تنبع من عدم تطابق معرفات الأعمدة أو نقص سكريبتات المكتبة.

---

## الخطوة 7: تعديلات متقدمة (اختياري)

فيما يلي بعض الأفكار السريعة التي يمكنك تجربتها بمجرد أن يعمل الجدول الأساسي.

| الميزة | طريقة التفعيل | لماذا تساعد |
|--------|----------------|--------------|
| **مُعَدِّل خلية مخصص** | `gridOptions.Columns[2].formatter = (cell) => \`<b>$${cell}</b>\`;` | يبرز الرواتب بخط عريض. |
| **شريط البحث** | `gridOptions.Search = true;` | يتيح للمستخدمين تصفية الصفوف فورًا. |
| **بيانات من الخادم** | `gridOptions.Server = { url: "/api/employees", then: data => data.items };` | يتعامل مع آلاف الصفوف بسهولة. |
| **تبديل السمة** | `gridOptions.ClassName = "gridjs-theme-dark";` | يتماشى مع تصاميم الوضع الداكن. |

لا تتردد في الجمع بين هذه الخيارات—Grid.js مرن بطبيعة الحال. فقط تذكر الحفاظ على سطر **create gridjsoptions instance** الأصلي في الأعلى؛ جميع التعديلات اللاحقة تعتمد على ذلك الكائن الواحد.

---

## الخلاصة

لقد استعرضنا سير عمل كامل لـ **create GridJsOptions instance** و**configure grid options JavaScript** لإنشاء جدول بيانات وظيفي، قابل للفرز، ومقسم إلى صفحات. بدءًا من صفحة HTML بسيطة، قمنا بتحميل المكتبة، بناء كائن الخيارات، تفعيل محاذاة الأرقام، إضافة التقسيم إلى صفحات، تعريف الأعمدة، وأخيرًا عرض الجدول.

من هنا يمكنك:

- استبدال `sampleData` الثابت باستدعاء AJAX.
- إضافة مُعَدِّلات مخصصة للتواريخ، العملات، أو الأيقونات.
- دمج الجدول في إطار عمل مثل React أو Vue (كائن `gridOptions` نفسه يعمل هناك أيضًا).

الإمكانات لا حصر لها، والنمط الذي استخدمناه—تجميع جميع الإعدادات في كائن `GridJsOptions` واحد—يحافظ على شفرتك نظيفة وسهلة الصيانة.

هل لديك حالة استخدام غير واضحة؟ اترك تعليقًا وسنستكشفها معًا. برمجة سعيدة، واستمتع بإنشاء جداول ديناميكية باستخدام Grid.js!

## ما الذي يجب أن تتعلمه لاحقًا؟

- [How to Create and Configure Excel Workbooks with Aspose.Cells .NET: A Step‑By‑Step Guide](/cells/english/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)
- [How to Create and Style Excel Tables Using Aspose.Cells for .NET | Step‑By‑Step Guide](/cells/english/net/tables-structured-references/aspose-cells-net-excel-tables-styling/)
- [How to Create & Format Excel Cells Using Aspose.Cells for Java: A Step‑By‑Step Guide](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}