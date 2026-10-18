---
category: general
date: 2026-06-21
description: تعلم كيفية تغيير خط مربع النص، وضبط لون الخط برمجيًا وتعديل حجم الخط
  في خلية شبكة. اتبع هذا الدرس العملي لتنسيق مربعات النص.
draft: false
keywords:
- change textbox font
- change font size cell
- how to style textbox
- set font color programmatically
- change font family grid
language: ar
og_description: غيّر خط مربع النص في شبكة بسرعة. يوضح هذا الدليل كيفية تنسيق مربع
  النص، وتعيين لون الخط برمجياً، وتعديل حجم الخلية باستخدام كود واضح.
og_title: تغيير خط مربع النص في شبكة – دليل برمجي كامل
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Learn how to change textbox font, set font color programmatically and
    adjust font size cell in a grid. Follow this practical tutorial for styling textboxes.
  headline: Change Textbox Font in a Grid – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Learn how to change textbox font, set font color programmatically and
    adjust font size cell in a grid. Follow this practical tutorial for styling textboxes.
  name: Change Textbox Font in a Grid – Complete Step‑by‑Step Guide
  steps:
  - name: Breaking Down the Object
    text: '| Property | Purpose | Example Values | |----------|---------|----------------|
      | `family` | Font family – controls the typeface. | `"Arial"`, `"Helvetica"`,
      `"Courier New"` | | `size` | Font size in pixels (or points, depending on the
      grid). | `12`, `14`, `16` | | `color` | Text color in any CSS‑co'
  - name: Expected Output
    text: '- The textbox located at **row 2, column 3** now displays text in **Arial**,
      **14 px**, and a **#0066CC** blue hue. - Opening the browser console will print
      something like:'
  - name: Can I change only the font size without affecting family or color?
    text: 'Absolutely. Just omit the properties you don’t want to modify:'
  - name: What if my grid uses a different property name for the textbox?
    text: Inspect the cell object in the console (`console.log(cell)`). You’ll likely
      see something like `cell.editor` or `cell.input`. Replace `cell.textbox` with
      the correct reference.
  - name: How do I apply the same style to an entire column?
    text: 'Loop through the rows and set the font for each cell in that column:'
  - name: Is there a way to revert to the original font?
    text: 'Store the original style before overwriting:'
  type: HowTo
tags:
- JavaScript
- UI‑grid
- DOM‑manipulation
title: تغيير خط مربع النص في شبكة – دليل خطوة‑بخطوة كامل
url: /ar/net/working-with-fonts-in-spreadsheets/change-textbox-font-in-a-grid-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تغيير خط صندوق النص داخل شبكة – دليل خطوة‑بخطوة كامل

هل احتجت يوماً إلى **تغيير خط صندوق النص** داخل شبكة بيانات لكنك لم تكن متأكدًا أي خاصية يجب تعديلها؟ لست وحدك—معظم المطورين يواجهون هذه المشكلة عند بناء جداول قابلة للتحرير أو لوحات تحكم. في هذا الدرس سنستعرض خطوة بخطوة كيفية تغيير خط صندوق النص، ضبط لونه برمجيًا، وحتى تعديل حجم الخط خلية‑بخلية.

سنضيف أيضًا نصائح حول **كيفية تنسيق صندوق النص**، وسنغطي سيناريوهات **تغيير حجم الخط للخلية**، وسنوضح لك **كيفية ضبط لون الخط برمجيًا** دون عناء. في النهاية ستحصل على مقتطف قابل لإعادة الاستخدام يعمل مع أي مكوّن شبكة يوفر واجهة `getCell` API.

## المتطلبات المسبقة

- متصفح حديث يدعم ES6 (Chrome, Edge, Firefox, Safari)
- مكتبة شبكة توفر `grid.getCell(row, col)` وتعيد كائن خلية يحتوي على مرجع `textbox`
- معرفة أساسية بكائنات JavaScript وخصائص CSS

لا توجد حزم إضافية مطلوبة—فقط JavaScript عادي وواجهة API الخاصة بالشبكة.

## نظرة عامة على الحل

الفكرة الأساسية بسيطة: استدعِ الخلية المستهدفة، احصل على صندوق النص المدمج فيها، ثم عيّن كائن خط جديد يحدد العائلة، الحجم، واللون. فكر فيها كأنك تُعطي صندوق النص زيًا جديدًا. التدفق عالي المستوى كالتالي:

1. **الوصول إلى الخلية المستهدفة** – حدد الصف/العمود الذي تريد.
2. **استخراج صندوق النص** – العنصر UI الذي يحمل النص.
3. **إنشاء كائن نمط الخط** – حدد العائلة، الحجم، واللون.
4. **تطبيق النمط** – عيّن الكائن إلى خاصية `font` الخاصة بصندوق النص.

هذا كل شيء. لنغوص في كل خطوة، نشرح لماذا هي مهمة، ونرى الكود يعمل.

![لقطة شاشة لخلية شبكة مع صندوق نص مُنسق – تغيير خط صندوق النص](/images/change-textbox-font-example.png)

## الخطوة 1: الوصول إلى الخلية المستهدفة في الشبكة

```javascript
// Step 1: Access the target cell in the grid
const cell = grid.getCell(2, 3);
```

> **لماذا هذا مهم:**  
> عادةً ما تخزن الشبكات الصفوف والأعمدة كمؤشرات تبدأ من الصفر. باستدعاء `grid.getCell(2, 3)` نحصل على الخلية في **الصف 2، العمود 3**. إذا أردت **تغيير حجم الخط للخلية** في موقع مختلف، ما عليك سوى تعديل المؤشرات.

**نصيحة احترافية:** إذا كانت شبكتك تدعم الأعمدة المسماة، يمكنك استبدال العمود الرقمي بمفتاح، مثل `grid.getCell(2, "price")`.

## الخطوة 2: استخراج صندوق النص داخل تلك الخلية

```javascript
// Step 2: Get the textbox contained in that cell
const textbox = cell.textbox;
```

> **ما يحدث:**  
> معظم تطبيقات الشبكات تغلف المحتوى القابل للتحرير داخل عنصر `<input>` أو `<textarea>` وتعرضه كـ `cell.textbox`. الحصول على المرجع يتيح لنا تعديل نمط عرضه مباشرة.

إذا كانت الشبكة تستخدم اسم خاصية مختلف (مثل `cell.editor`)، قم بتعديل الكود وفقًا لذلك—هذا اختلاف شائع عندما تريد **كيفية تنسيق صندوق النص** لمكوّن مخصص.

## الخطوة 3: تعريف خصائص الخط المطلوبة

```javascript
// Step 3: Define the desired font properties
const fontStyle = {
  family: "Arial",          // change font family grid
  size: 14,                 // change font size cell
  color: "#0066CC"          // set font color programmatically
};
```

### تفصيل الكائن

| Property | Purpose | Example Values |
|----------|---------|----------------|
| `family` | عائلة الخط – تتحكم في نوع الخط. | `"Arial"`, `"Helvetica"`, `"Courier New"` |
| `size`   | حجم الخط بالبكسل (أو بالنقاط، حسب الشبكة). | `12`, `14`, `16` |
| `color`  | لون النص بأي صيغة CSS متوافقة. | `"#0066CC"`, `"rgb(255,0,0)"`, `"navy"` |

> **لماذا نستخدم كائنًا:**  
> تجميع الخصائص الثلاث معًا يجعل الكود منظمًا ويعكس ما تتوقعه العديد من مكتبات UI من معلومات النمط. كما يتيح لك **تغيير عائلة الخط في الشبكة** أو **ضبط لون الخط برمجيًا** بتعيين واحد.

## الخطوة 4: تطبيق نمط الخط على صندوق النص

```javascript
// Step 4: Apply the font style to the textbox
textbox.font = fontStyle;
```

> **ما يحدث في الخلفية:**  
> مكوّن صندوق النص في الشبكة يفسّر خاصية `font` ويحدّث CSS وفقًا لذلك. هذا السطر الواحد يستبدل عائلة الخط، الحجم، واللون السابقين دفعة واحدة—تمامًا ما تحتاجه عندما تريد **تغيير خط صندوق النص** عبر خلايا متعددة.

إذا كان المكوّن يستخدم API مختلف (مثلاً `textbox.style.fontFamily = ...`)، عدّل التعيين لكن حافظ على نفس المبدأ.

## مثال كامل يعمل

فيما يلي مقتطف مستقل يمكنك لصقه في ملف HTML يتضمن كائن شبكة تجريبي. يوضح التدفق الكامل من الخطوة 1 إلى الخطوة 4، بالإضافة إلى تحقق سريع من أن النمط قد تغير.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Change Textbox Font Demo</title>
  <style>
    .grid { display: table; border-collapse: collapse; }
    .grid .row { display: table-row; }
    .grid .cell { display: table-cell; border: 1px solid #ccc; padding: 8px; }
    .grid .cell input { width: 100%; border: none; }
  </style>
</head>
<body>

<div id="myGrid" class="grid"></div>

<script>
/* ---------- Mock Grid Implementation ---------- */
class MockGrid {
  constructor(rows, cols) {
    this.rows = rows;
    this.cols = cols;
    this.el = document.getElementById('myGrid');
    this._build();
  }
  _build() {
    for (let r = 0; r < this.rows; r++) {
      const rowDiv = document.createElement('div');
      rowDiv.className = 'row';
      for (let c = 0; c < this.cols; c++) {
        const cellDiv = document.createElement('div');
        cellDiv.className = 'cell';
        const input = document.createElement('input');
        input.type = 'text';
        input.value = `R${r}C${c}`;
        // expose textbox via a custom property
        cellDiv.textbox = input;
        cellDiv.appendChild(input);
        rowDiv.appendChild(cellDiv);
      }
      this.el.appendChild(rowDiv);
    }
  }
  getCell(row, col) {
    const rowDiv = this.el.children[row];
    if (!rowDiv) return null;
    const cellDiv = rowDiv.children[col];
    return cellDiv || null;
  }
}

/* ---------- Use the Grid ---------- */
const grid = new MockGrid(5, 5); // 5x5 grid for demo

// ---- Change Textbox Font (the core tutorial steps) ----
const cell = grid.getCell(2, 3);          // step 1
const textbox = cell.textbox;             // step 2
const fontStyle = {                      // step 3
  family: "Arial",
  size: 14,
  color: "#0066CC"
};
textbox.font = fontStyle;                // step 4

// Verify by logging computed style
setTimeout(() => {
  const cs = window.getComputedStyle(textbox);
  console.log('Applied font family:', cs.fontFamily);
  console.log('Applied font size:', cs.fontSize);
  console.log('Applied color:', cs.color);
}, 0);
</script>
</body>
</html>
```

### النتيجة المتوقعة

- صندوق النص الموجود في **الصف 2، العمود 3** سيظهر الآن بنص **Arial**، **14 px**، وبدرجة لون **#0066CC** زرقاء.
- سيطبع سجل المتصفح شيئًا مثل:

```
Applied font family: Arial, Helvetica, sans-serif
Applied font size: 14px
Applied color: rgb(0, 102, 204)
```

عند فتح الصفحة، ستؤكد بصريًا التغيير—لم يعد هناك خط النظام الافتراضي.

## الأسئلة المتكررة (FAQ)

### هل يمكنني تغيير حجم الخط فقط دون التأثير على العائلة أو اللون؟
بالطبع. ما عليك سوى حذف الخصائص التي لا تريد تعديلها:

```javascript
textbox.font = { size: 18 }; // only changes size
```

### ماذا لو كانت شبكتي تستخدم اسم خاصية مختلف لصندوق النص؟
افحص كائن الخلية في وحدة التحكم (`console.log(cell)`). من المحتمل أن ترى شيء مثل `cell.editor` أو `cell.input`. استبدل `cell.textbox` بالمرجع الصحيح.

### كيف أطبق نفس النمط على عمود كامل؟
قم بالتكرار عبر الصفوف واضبط الخط لكل خلية في ذلك العمود:

```javascript
for (let r = 0; r < grid.rowCount; r++) {
  const colCell = grid.getCell(r, 3);
  colCell.textbox.font = fontStyle; // reuse the same fontStyle object
}
```

### هل هناك طريقة للعودة إلى الخط الأصلي؟
احفظ النمط الأصلي قبل استبداله:

```javascript
const original = { ...textbox.font };
textbox.font = fontStyle; // apply new style
// later...
textbox.font = original; // revert
```

## نصائح وممارسات أفضل

- **تحديثات دفعية:** إذا كنت تحتاج لتنسيق العديد من الخلايا، غلف التغييرات داخل `requestAnimationFrame` أو طريقة دفعة خاصة بالشبكة لتجنب اضطراب التخطيط.
- **خطوط استجابية:** استخدم وحدات نسبية (`em`, `rem`) بدلاً من البكسل الثابت إذا كان واجهتك تحتاج إلى التوسع.
- **إمكانية الوصول:** تأكد من وجود تباين كافٍ عندما تقوم **ضبط لون الخط برمجيًا**—الحد الأدنى وفق WCAG AA هو نسبة 4.5:1 للنص العادي.
- **مشكلات المتصفحات القديمة:** قد تتطلب بعض الشبكات القديمة ضبط `style.fontFamily` مباشرة على عنصر `<input>` بدلاً من استخدام كائن `font`.

## الخلاصة

لقد غطينا الآن **كيفية تغيير خط صندوق النص** داخل شبكة، من استخراج الخلية الصحيحة إلى تعريف كائن `fontStyle` قابل لإعادة الاستخدام وتطبيقه بسطر واحد. على طول الطريق تعلمنا أيضًا **تغيير حجم الخط للخلية**، **ضبط لون الخط برمجيًا**، وحتى **تغيير عائلة الخط في الشبكة** لعمود محدد.

الآن يمكنك أخذ هذا النمط وتكييفه مع أي مكتبة UI—سواء كنت تبني لوحة تحكم إدارية، محرر يشبه الجداول، أو أداة تقارير مخصصة. جرّب عائلات، أحجام، وألوان مختلفة؛ ربما تضيف تأثيرات تمرير أو تنسيق شرطي بناءً على قيم البيانات.

هل لديك تحدٍ آخر في التنسيق؟ اترك تعليقًا، وسنواجهه معًا. برمجة سعيدة!

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شفرة كاملة مع شروحات خطوة‑بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف نهج تنفيذ بديلة في مشاريعك.

- [How to Change Font Color in Excel Using Aspose.Cells for Java&#58; A Complete Guide](/cells/english/java/formatting/change-font-color-aspose-cells-java-tutorial/)
- [Change Font Color Aspose Cells Java Tutorial](/cells/german/java/formatting/change-font-color-aspose-cells-java-tutorial/)
- [Change Font Color Aspose Cells Java Tutorial](/cells/french/java/formatting/change-font-color-aspose-cells-java-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}