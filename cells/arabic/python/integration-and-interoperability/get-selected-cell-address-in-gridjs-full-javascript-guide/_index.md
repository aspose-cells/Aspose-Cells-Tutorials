---
category: general
date: 2026-06-30
description: تعلم كيفية الحصول على عنوان الخلية المحددة، وتحديث قيمة خلية الشبكة،
  وقراءة قيمة الإدخال باستخدام JavaScript و GridJs. كود خطوة بخطوة ونصائح.
draft: false
keywords:
- get selected cell address
- update grid cell value
- read input value with javascript
language: ar
og_description: احصل على عنوان الخلية المحددة، وقم بتحديث قيمة خلية الشبكة وقراءة
  قيمة الإدخال باستخدام JavaScript. اتبع هذا الدليل الكامل للحصول على تكامل سلس مع
  GridJs.
og_title: احصل على عنوان الخلية المحددة – دليل GridJs JavaScript الكامل
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Learn how to get selected cell address, update grid cell value and
    read input value with JavaScript using GridJs. Step‑by‑step code and tips.
  headline: Get Selected Cell Address in GridJs – Full JavaScript Guide
  type: TechArticle
tags:
- GridJs
- JavaScript
- DOM manipulation
title: الحصول على عنوان الخلية المحددة في GridJs – دليل JavaScript الكامل
url: /ar/python/integration-and-interoperability/get-selected-cell-address-in-gridjs-full-javascript-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# الحصول على عنوان الخلية المحددة – دليل GridJs الكامل لجافاسكريبت

هل احتجت يومًا إلى **الحصول على عنوان الخلية المحددة** من جدول GridJs لكنك لم تكن متأكدًا من أي استدعاء API تستخدمه؟ لست وحدك. في العديد من لوحات الإدارة، ينقر المستخدمون على خلية، يحرّرون قيمة في نافذة منبثقة، ويتوقعون أن يعكس الجدول التغيير فورًا. يوضح لك هذا الدليل بالضبط كيفية استرجاع ذلك العنوان، قراءة السعر الجديد من حقل الإدخال، و**تحديث قيمة خلية الجدول** دون إعادة تحميل الصفحة.

سنغطي أيضًا **قراءة قيمة الإدخال باستخدام جافاسكريبت** بالطريقة الصحيحة، معالجة الحالات الحدية، وإغلاق النافذة المنبثقة بمجرد انتهاء التحديث. في النهاية ستحصل على مقتطف مستقل يمكنك إدراجه في أي مشروع يستخدم GridJs.

## ما ستبنيه

- جدول HTML بسيط مدعوم من GridJs.
- نافذة تعديل تظهر عند النقر على خلية.
- جافاسكريبت تقوم **بالحصول على عنوان الخلية المحددة**، وتلتقط السعر الذي يدخله المستخدم، **تحديث قيمة خلية الجدول**، وأخيرًا تخفي النافذة.

لا تحتاج إلى مكتبات خارجية بخلاف GridJs، والكود يعمل على المتصفحات الحديثة (Chrome 102+، Edge، Firefox). إذا كان لديك بالفعل مثيل GridJs على الصفحة، يمكنك نسخ‑لصق الأجزاء ذات الصلة مباشرة.

## المتطلبات المسبقة

- معرفة أساسية بجافاسكريبت وDOM.
- مكتبة GridJs محملة (عبر CDN أو npm).
- صفحة تعرض شبكة GridJs بالفعل (سنظهر مثالًا بسيطًا).

إذا كان أي من هذه غير مألوف لك، لا تقلق—كل خطوة تتضمن ملخصًا سريعًا.

---

## الخطوة 1: إعداد هيكل HTML

أولاً، ضع حاوية الجدول، النافذة المخفية، وحقل إدخال السعر. سيتم إظهار النافذة باستخدام فئات CSS بسيطة.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>GridJs Edit Example</title>
  <link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet"/>
  <style>
    /* Quick modal styling – feel free to replace with your UI framework */
    #editModal { display:none; position:fixed; top:20%; left:50%; transform:translateX(-50%);
                 background:#fff; padding:1rem; border:1px solid #ccc; box-shadow:0 4px 8px rgba(0,0,0,.1);}
    #editModal.active { display:block; }
  </style>
</head>
<body>

<div id="grid"></div>

<div id="editModal">
  <h3>Edit Price</h3>
  <input type="number" id="price" placeholder="Enter new price"/>
  <button id="saveBtn">Save</button>
  <button id="cancelBtn">Cancel</button>
</div>

<script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
<script src="script.js"></script>
</body>
</html>
```

> **نصيحة احترافية:** يستخدم العنصر `#editModal` حيلة CSS بسيطة—فقط أضف الفئة `active` لإظهاره. يمكنك استبدال ذلك بـ Bootstrap أو Tailwind أو أي مكوّن نافذة منبثقة تستخدمه بالفعل.

---

## الخطوة 2: تهيئة GridJs والتقاط نقرات الخلايا

الآن سننشئ شبكة ببيانات تجريبية ونستمع لاختيارات الخلايا. عندما ينقر المستخدم على خلية، سنقوم **بالحصول على عنوان الخلية المحددة** وفتح النافذة.

```javascript
// script.js
const grid = new gridjs.Grid({
  columns: ['Item', 'Quantity', 'Price'],
  data: [
    ['Apple', 10, 0.5],
    ['Banana', 5, 0.3],
    ['Cherry', 20, 0.2]
  ],
  pagination: { limit: 5 },
  sort: true,
  // Enable cell selection – GridJs provides a helper for this
  style: {
    table: {
      'width': '100%'
    }
  }
}).render(document.getElementById('grid'));

// Helper to store the address of the last clicked cell
let lastSelectedCell = null;

// GridJs emits a 'cell' event when any cell is clicked
grid.on('cell', (event) => {
  // Step 2a: Get selected cell address
  const address = GridJs.getSelectedCell(); // <-- primary operation
  lastSelectedCell = address; // remember for later update

  // Show the modal
  document.getElementById('editModal').classList.add('active');

  // Optional: pre‑fill the input with the current cell value
  const currentValue = event.target.innerText;
  document.getElementById('price').value = currentValue;
});
```

> **لماذا يعمل هذا:** تُعيد الدالة `GridJs.getSelectedCell()` سلسلة مثل `"C2"` (العمود C، الصف 2). تخزينها في المتغيّر `lastSelectedCell` يتيح لنا الإشارة إلى الموقع الدقيق عندما نقوم لاحقًا **بتحديث قيمة خلية الجدول**.

---

## الخطوة 3: قراءة السعر الجديد من حقل الإدخال

عند نقر المستخدم على **Save**، نحتاج إلى **قراءة قيمة الإدخال باستخدام جافاسكريبت** بأمان. تتضمن هذه الخطوة أيضًا التحقق من أن السعر المدخل هو رقم موجب.

```javascript
document.getElementById('saveBtn').addEventListener('click', () => {
  // Step 3a: Grab the raw string from the input
  const raw = document.getElementById('price').value;

  // Step 3b: Convert to a number and validate
  const newPrice = parseFloat(raw);
  if (isNaN(newPrice) || newPrice < 0) {
    alert('Please enter a valid positive number.');
    return;
  }

  // Proceed to update the cell
  updateSelectedCell(newPrice);
});
```

> **ملاحظة:** يضمن استخدام `parseFloat` قبول الكسور العشرية (مثال: `1.99`). الحماية `isNaN` تمنع الإرسال الفارغ غير المقصود.

---

## الخطوة 4: تحديث قيمة الخلية المحددة

الآن نُحدّث **قيمة خلية الجدول** باستخدام العنوان الذي تم التقاطه مسبقًا. تُعيد طريقة `updateCell` في GridJs وعدًا (Promise)، لذا يمكننا ربط إجراء إغلاق النافذة به.

```javascript
function updateSelectedCell(value) {
  if (!lastSelectedCell) {
    console.warn('No cell selected – nothing to update.');
    return;
  }

  // Step 4a: Call GridJs.updateCell(address, newValue)
  GridJs.updateCell(lastSelectedCell, value)
    .then(() => {
      // Step 4b: Close the modal once the grid refreshes
      document.getElementById('editModal').classList.remove('active');
      // Reset stored address
      lastSelectedCell = null;
    })
    .catch(err => {
      console.error('Failed to update cell:', err);
      alert('Could not save the new price. Try again.');
    });
}
```

> **لماذا نستخدم وعدًا؟** قد تحتاج GridJs إلى إعادة رسم الجدول أو المزامنة مع الخادم. بالانتظار حتى يُستكمل الوعد نضمن إخفاء الواجهة فقط بعد أن يعكس الجدول القيمة الجديدة.

---

## الخطوة 5: معالجة الإلغاء والحالات الحدية

الحل القوي دائمًا ما يمنح المستخدم مخرجًا. زر **Cancel** ببساطة يخفي النافذة ويُفرغ أي عنوان مخزن.

```javascript
document.getElementById('cancelBtn').addEventListener('click', () => {
  document.getElementById('editModal').classList.remove('active');
  lastSelectedCell = null;
});
```

### ماذا لو لم يتم اختيار خلية؟

إذا قام المستخدم بطريقة ما بتفعيل زر **Save** دون النقر على خلية أولًا (ربما فتح النافذة برمجيًا)، سيكون `lastSelectedCell` قيمته `null`. الإرجاع المبكر في `updateSelectedCell` يمنع حدوث خطأ وقت التشغيل ويسجل تحذيرًا مفيدًا.

### التعامل مع الشبكات الكبيرة

بالنسبة للشبكات التي تستخدم الترميز الصفحي، لا تزال الدالة `GridJs.getSelectedCell()` تُعيد العنوان المطلق (مثال: `"B12"`)، وليس الصف الظاهر فقط. هذا يعني أن التحديث يعمل حتى لو كان الصف المُعدَّل موجودًا في صفحة أخرى. فقط ضع في اعتبارك أن الواجهة لن تنتقل تلقائيًا إلى الصفحة المناسبة بعد التحديث—إذا كنت بحاجة إلى ذلك، استدعِ `grid.forceUpdate()` أو انتقل إلى الصفحة المطلوبة يدويًا.

---

## مثال عملي كامل

فيما يلي الكود الكامل الذي يمكنك نسخه‑لصقه في ملف HTML واحد. افتحه في المتصفح، انقر على أي خلية، غيّر السعر، وسترى الجدول يتحدّث فورًا.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Get Selected Cell Address – GridJs Demo</title>
  <link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet"/>
  <style>
    #editModal { display:none; position:fixed; top:20%; left:50%; transform:translateX(-50%);
                 background:#fff; padding:1rem; border:1px solid #ccc; box-shadow:0 4px 8px rgba(0,0,0,.1);}
    #editModal.active { display:block; }
  </style>
</head>
<body>

<div id="grid"></div>

<div id="editModal" aria-modal="true" role="dialog">
  <h3>Edit Price</h3>
  <input type="number" id="price" placeholder="Enter new price"/>
  <button id="saveBtn">Save</button>
  <button id="cancelBtn">Cancel</button>
</div>

<script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
<script>
  // Initialise the grid
  const grid = new gridjs.Grid({
    columns: ['Item', 'Quantity', 'Price'],
    data: [
      ['Apple', 10, 0.5],
      ['Banana', 5, 0.3],
      ['Cherry', 20, 0.2]
    ],
    pagination: { limit: 5 },
    sort: true
  }).render(document.getElementById('grid'));

  let lastSelectedCell = null;

  // Capture cell clicks – this is where we **get selected cell address**
  grid.on('cell', (event) => {
    const address = GridJs.getSelectedCell();   // primary keyword usage
    lastSelectedCell = address;
    document.getElementById('editModal').classList.add('active');
    document.getElementById('price').value = event.target.innerText;
  });

  // Save button – **read input value with JavaScript**
  document.getElementById('saveBtn').addEventListener('click', () => {
    const raw = document.getElementById('price').value;
    const newPrice = parseFloat(raw);
    if (isNaN(newPrice) || newPrice < 0) {
      alert('Please enter a valid positive number.');
      return;
    }
    updateSelectedCell(newPrice);
  });

  // Core update logic – **update grid cell value**
  function updateSelectedCell(value) {
    if (!lastSelectedCell) {
      console.warn('No cell selected – nothing to update.');
      return;
    }
    GridJs.updateCell(lastSelectedCell, value)
      .then(() => {
        document.getElementById('editModal').classList


## ماذا يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [Get Address, Cell Count, and Offset for Entire Excel Range](/cells/english/net/excel-range-address-calculation/get-address-cell-count-and-offset-for-entire-excel-range/)
- [Get Address Cell Count And Offset For Entire Excel Range](/cells/german/net/excel-range-address-calculation/get-address-cell-count-and-offset-for-entire-excel-range/)
- [Get Address Cell Count And Offset For Entire Excel Range](/cells/french/net/excel-range-address-calculation/get-address-cell-count-and-offset-for-entire-excel-range/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}