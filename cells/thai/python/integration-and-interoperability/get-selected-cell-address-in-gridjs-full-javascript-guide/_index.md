---
category: general
date: 2026-06-30
description: เรียนรู้วิธีการรับที่อยู่ของเซลล์ที่เลือก, อัปเดตค่าของเซลล์ในกริดและอ่านค่าจากอินพุตด้วย
  JavaScript โดยใช้ GridJs. โค้ดและเคล็ดลับแบบทีละขั้นตอน.
draft: false
keywords:
- get selected cell address
- update grid cell value
- read input value with javascript
language: th
og_description: รับที่อยู่ของเซลล์ที่เลือก, ปรับค่าของเซลล์ในกริดและอ่านค่าจากอินพุตด้วย
  JavaScript. ปฏิบัติตามคู่มือฉบับเต็มนี้เพื่อการรวม GridJs อย่างราบรื่น.
og_title: รับที่อยู่ของเซลล์ที่เลือก – บทเรียน JavaScript GridJs ฉบับสมบูรณ์
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
title: รับที่อยู่ของเซลล์ที่เลือกใน GridJs – คู่มือ JavaScript ฉบับเต็ม
url: /th/python/integration-and-interoperability/get-selected-cell-address-in-gridjs-full-javascript-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# รับที่อยู่เซลล์ที่เลือก – การสอน JavaScript ของ GridJs อย่างครบถ้วน

เคยต้องการ **รับที่อยู่เซลล์ที่เลือก** จากตาราง GridJs แต่ไม่แน่ใจว่าจะใช้ API ใดหรือไม่? คุณไม่ได้เป็นคนเดียว ในหลาย ๆ แผงผู้ดูแลระบบ ผู้ใช้คลิกที่เซลล์ แก้ไขค่าผ่านโมดัล แล้วคาดว่าตารางจะแสดงการเปลี่ยนแปลงทันที การสอนนี้จะแสดงให้คุณเห็นอย่างชัดเจนว่าจะแยกที่อยู่นั้นออกมาอย่างไร อ่านราคาที่ใหม่จากฟิลด์อินพุต และ **อัปเดตค่าของเซลล์ในกริด** โดยไม่ต้องรีโหลดหน้า

เราจะครอบคลุม **การอ่านค่าจากอินพุตด้วย JavaScript** อย่างถูกต้อง จัดการกรณีขอบ และปิดโมดัลเมื่อการอัปเดตเสร็จสิ้น เมื่อจบคุณจะได้สแนปช็อตที่สามารถนำไปใช้ในโปรเจกต์ใด ๆ ที่ใช้ GridJs ได้ทันที

## สิ่งที่คุณจะสร้าง

- ตาราง HTML อย่างง่ายที่ใช้ GridJs
- โมดัลแก้ไขที่ปรากฏเมื่อคลิกที่เซลล์
- JavaScript ที่ **รับที่อยู่เซลล์ที่เลือก**, ดึงราคาที่ผู้ใช้พิมพ์, **อัปเดตค่าของเซลล์ในกริด**, และสุดท้ายซ่อนโมดัล

ไม่ต้องใช้ไลบรารีภายนอกนอกจาก GridJs และโค้ดทำงานได้กับเบราว์เซอร์สมัยใหม่ (Chrome 102+, Edge, Firefox) หากคุณมีอินสแตนซ์ GridJs อยู่แล้วบนหน้า คุณสามารถคัดลอก‑วางส่วนที่เกี่ยวข้องได้โดยตรง

## ข้อกำหนดเบื้องต้น

- ความรู้พื้นฐานเกี่ยวกับ JavaScript และ DOM
- โหลดไลบรารี GridJs (ผ่าน CDN หรือ npm)
- หน้าเว็บที่มีการแสดง GridJs อยู่แล้ว (เราจะแสดงตัวอย่างขั้นต่ำ)

หากส่วนใดส่วนหนึ่งฟังดูแปลกใหม่ อย่าตื่นตระหนก—แต่ละขั้นตอนมีการสรุปสั้น ๆ ให้คุณเข้าใจ

---

## Step 1: Set Up the HTML Skeleton

ก่อนอื่นให้จัดวางคอนเทนเนอร์ของตาราง โมดัลที่ซ่อนอยู่ และฟิลด์อินพุตราคา โมดัลจะถูกสลับด้วยคลาส CSS อย่างง่าย

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

> **Pro tip:** `#editModal` ใช้เทคนิค CSS ขั้นต่ำ—แค่เพิ่มคลาส `active` เพื่อแสดง คุณสามารถเปลี่ยนเป็น Bootstrap, Tailwind หรือคอมโพเนนต์โมดัลใด ๆ ที่คุณใช้อยู่แล้ว

---

## Step 2: Initialise GridJs and Capture Cell Clicks

ต่อไปเราจะสร้างกริดด้วยข้อมูลตัวอย่างและฟังการเลือกเซลล์ เมื่อผู้ใช้คลิกเซลล์ เราจะ **รับที่อยู่เซลล์ที่เลือก** และเปิดโมดัล

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

> **Why this works:** `GridJs.getSelectedCell()` คืนสตริงเช่น `"C2"` (คอลัมน์ C, แถว 2) การเก็บไว้ใน `lastSelectedCell` ทำให้เราสามารถอ้างอิงตำแหน่งที่แน่นอนได้เมื่อเราต้อง **อัปเดตค่าของเซลล์ในกริด** ต่อไป

---

## Step 3: Read the New Price from the Input Field

เมื่อผู้ใช้คลิก **Save** เราต้อง **อ่านค่าจากอินพุตด้วย JavaScript** อย่างปลอดภัย ขั้นตอนนี้ยังตรวจสอบว่าราคาที่ป้อนเป็นจำนวนบวกหรือไม่

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

> **Note:** การใช้ `parseFloat` ทำให้เรารับค่าทศนิยมได้ (เช่น `1.99`) ตัวตรวจสอบ `isNaN` ป้องกันการส่งค่าเปล่าโดยบังเอิญ

---

## Step 4: Update the Selected Cell Value

ตอนนี้เราจะ **อัปเดตค่าของเซลล์ในกริด** โดยใช้ที่อยู่ที่เราจับไว้ก่อนหน้า เมธอด `updateCell` ของ GridJs คืนค่าเป็น promise ดังนั้นเราจึงสามารถต่อการปิดโมดัลได้

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

> **Why use a promise?** GridJs อาจต้องรี‑เรนเดอร์ตารางใหม่หรือซิงค์กับแบ็กเอนด์ การรอ promise ทำให้มั่นใจว่า UI จะซ่อนหลังจากกริดแสดงค่าที่อัปเดตแล้วเท่านั้น

---

## Step 5: Handle Cancel and Edge Cases

โซลูชันที่แข็งแรงต้องให้ผู้ใช้มีทางออก ปุ่ม **Cancel** เพียงซ่อนโมดัลและล้างที่อยู่ที่เก็บไว้

```javascript
document.getElementById('cancelBtn').addEventListener('click', () => {
  document.getElementById('editModal').classList.remove('active');
  lastSelectedCell = null;
});
```

### ถ้าไม่มีเซลล์ที่เลือก?

หากผู้ใช้ทำให้ปุ่ม **Save** ทำงานโดยไม่ได้คลิกเซลล์ก่อน (อาจเปิดโมดัลโดยโปรแกรม) `lastSelectedCell` จะเป็น `null` การคืนค่าเร็วใน `updateSelectedCell` ป้องกันข้อผิดพลาดรันไทม์และบันทึกคำเตือนที่เป็นประโยชน์

### จัดการกับกริดขนาดใหญ่

สำหรับกริดที่มีการแบ่งหน้า `GridJs.getSelectedCell()` ยังคืนที่อยู่แบบเต็ม (เช่น `"B12"`), ไม่ใช่แค่แถวที่มองเห็น ซึ่งหมายความว่าการอัปเดตจะทำงานแม้แถวที่แก้ไขอยู่บนหน้าต่างอื่น เพียงแค่ทราบว่า UI จะไม่สลับหน้าอัตโนมัติหลังอัปเดต—หากต้องการให้สลับหน้า ให้เรียก `grid.forceUpdate()` หรือเปลี่ยนหน้าเองด้วยตนเอง

---

## Complete Working Example

ด้านล่างเป็นโค้ดเต็มที่คุณสามารถคัดลอก‑วางลงในไฟล์ HTML เดียว เปิดในเบราว์เซอร์ คลิกเซลล์ใดก็ได้ เปลี่ยนราคา แล้วดูกริดอัปเดตทันที

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


## What Should You Learn Next?

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งรวมตัวอย่างโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายทีละขั้นตอน เพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจวิธีการทำงานทางเลือกในโปรเจกต์ของคุณเอง

- [รับที่อยู่, จำนวนเซลล์, และออฟเซ็ตสำหรับช่วง Excel ทั้งหมด](/cells/english/net/excel-range-address-calculation/get-address-cell-count-and-offset-for-entire-excel-range/)
- [รับที่อยู่ จำนวนเซลล์ และออฟเซ็ตสำหรับช่วง Excel ทั้งหมด (German)](/cells/german/net/excel-range-address-calculation/get-address-cell-count-and-offset-for-entire-excel-range/)
- [รับที่อยู่ จำนวนเซลล์ และออฟเซ็ตสำหรับช่วง Excel ทั้งหมด (French)](/cells/french/net/excel-range-address-calculation/get-address-cell-count-and-offset-for-entire-excel-range/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}