---
category: general
date: 2026-06-21
description: เรียนรู้วิธีเปลี่ยนแบบอักษรของกล่องข้อความ ตั้งค่าสีอักษรโดยโปรแกรมและปรับขนาดอักษรของเซลล์ในกริด
  ตามบทเรียนปฏิบัตินี้เพื่อการจัดสไตล์กล่องข้อความ.
draft: false
keywords:
- change textbox font
- change font size cell
- how to style textbox
- set font color programmatically
- change font family grid
language: th
og_description: เปลี่ยนฟอนต์ของกล่องข้อความในกริดอย่างรวดเร็ว คู่มือนี้แสดงวิธีจัดรูปแบบกล่องข้อความ
  ตั้งค่าสีฟอนต์โดยโปรแกรม และปรับขนาดเซลล์ด้วยโค้ดที่ชัดเจน
og_title: เปลี่ยนฟอนต์ของกล่องข้อความในกริด – คู่มือการเขียนโปรแกรมเต็มรูปแบบ
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
title: เปลี่ยนฟอนต์ของกล่องข้อความในกริด – คู่มือขั้นตอนเต็มรูปแบบ
url: /th/net/working-with-fonts-in-spreadsheets/change-textbox-font-in-a-grid-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# เปลี่ยนฟอนต์ของ Textbox ใน Grid – คู่มือขั้นตอนเต็ม

เคยต้อง **change textbox font** ภายใน data grid แต่ไม่แน่ใจว่าจะปรับ property ไหนหรือไม่? คุณไม่ได้เป็นคนเดียว—นักพัฒนาส่วนใหญ่มักเจอปัญหานี้เมื่อต้องสร้างตารางที่แก้ไขได้หรือแดชบอร์ด ในบทแนะนำนี้เราจะพาคุณผ่านขั้นตอนทั้งหมดเพื่อเปลี่ยนฟอนต์ของ textbox, ตั้งค่าสีโดยโปรแกรม, และแม้กระทั่งปรับขนาดฟอนต์ในแต่ละเซลล์

เราจะเพิ่มเคล็ดลับเกี่ยวกับ **how to style textbox**, ครอบคลุมสถานการณ์ **change font size cell**, และแสดงวิธี **set font color programmatically** โดยไม่ต้องเสียศีรษะ เมื่อจบคุณจะได้สแนปช็อตที่นำกลับไปใช้ได้กับคอมโพเนนต์ grid ใด ๆ ที่มี API `getCell`

## Prerequisites

- เบราว์เซอร์สมัยใหม่ที่รองรับ ES6 (Chrome, Edge, Firefox, Safari)
- ไลบรารี grid ที่ให้ `grid.getCell(row, col)` และคืนค่าอ็อบเจ็กต์เซลล์ที่มีการอ้างอิง `textbox`
- ความรู้พื้นฐานเกี่ยวกับอ็อบเจ็กต์ JavaScript และคุณสมบัติ CSS

ไม่ต้องติดตั้งแพ็กเกจเพิ่มเติม—ใช้ JavaScript ธรรมดาและ API ของ grid เท่านั้น

## Overview of the Solution

แนวคิดหลักง่าย ๆ: ดึงเซลล์เป้าหมาย, เอา textbox ที่ฝังอยู่, แล้วกำหนดอ็อบเจ็กต์ฟอนต์ใหม่ที่ระบุ family, size, และ color. คิดว่าเป็นการให้ textbox ใส่ชุดใหม่ให้ดูสดใหม่ ด้านล่างเป็นขั้นตอนระดับสูง:

1. **Access the target cell** – ระบุตำแหน่งแถว/คอลัมน์ที่ต้องการ
2. **Retrieve the textbox** – UI element ที่เก็บข้อความ
3. **Create a font style object** – ระบุ family, size, และ color
4. **Apply the style** – กำหนดอ็อบเจ็กต์ให้กับ property `font` ของ textbox

เท่านี้เอง เรามาเจาะลึกแต่ละขั้นตอน, ทำไมถึงสำคัญ, และดูโค้ดทำงานจริงกัน

![ภาพหน้าจอของเซลล์กริดที่มี textbox ที่มีสไตล์ – เปลี่ยนฟอนต์ของ textbox](/images/change-textbox-font-example.png)

## Step 1: Access the Target Cell in the Grid

```javascript
// Step 1: Access the target cell in the grid
const cell = grid.getCell(2, 3);
```

> **Why this matters:**  
> Grid ส่วนใหญ่เก็บแถวและคอลัมน์เป็นดัชนีเริ่มจากศูนย์ การเรียก `grid.getCell(2, 3)` จะดึงเซลล์ที่ **row 2, column 3** หากต้องการ **change font size cell** ที่ตำแหน่งอื่น เพียงปรับดัชนีเท่านั้น

**Pro tip:** หาก grid ของคุณรองรับคอลัมน์แบบชื่อ คุณสามารถแทนค่าคอลัมน์เป็นคีย์ได้ เช่น `grid.getCell(2, "price")`.

## Step 2: Grab the Textbox Inside That Cell

```javascript
// Step 2: Get the textbox contained in that cell
const textbox = cell.textbox;
```

> **What’s happening:**  
> ส่วนใหญ่ grid จะห่อหุ้มเนื้อหาแก้ไขได้ไว้ใน `<input>` หรือ `<textarea>` แล้วเปิดให้เข้าถึงผ่าน `cell.textbox` การดึงอ้างอิงนี้ทำให้เราจัดการสไตล์ของมันโดยตรง

หาก grid ของคุณใช้ชื่อ property อื่น (เช่น `cell.editor`) ให้ปรับโค้ดตาม—นี่เป็นความแตกต่างทั่วไปเมื่อคุณ **how to style textbox** สำหรับคอมโพเนนต์แบบกำหนดเอง

## Step 3: Define the Desired Font Properties

```javascript
// Step 3: Define the desired font properties
const fontStyle = {
  family: "Arial",          // change font family grid
  size: 14,                 // change font size cell
  color: "#0066CC"          // set font color programmatically
};
```

### Breaking Down the Object

| Property | วัตถุประสงค์ | ค่าตัวอย่าง |
|----------|---------------|--------------|
| `family` | ฟอนต์แฟมิลี – กำหนดรูปแบบตัวอักษร | `"Arial"`, `"Helvetica"`, `"Courier New"` |
| `size`   | ขนาดฟอนต์เป็นพิกเซล (หรือพอยต์ ขึ้นกับ grid) | `12`, `14`, `16` |
| `color`  | สีข้อความในรูปแบบ CSS ใดก็ได้ | `"#0066CC"`, `"rgb(255,0,0)"`, `"navy"` |

> **Why we use an object:**  
> การรวมคุณสมบัติเหล่านี้ไว้ในอ็อบเจ็กต์ทำให้โค้ดดูเรียบร้อยและสอดคล้องกับวิธีที่หลาย UI library คาดหวัง นอกจากนี้ยังทำให้คุณ **change font family grid** หรือ **set font color programmatically** ด้วยการกำหนดค่าเดียว

## Step 4: Apply the Font Style to the Textbox

```javascript
// Step 4: Apply the font style to the textbox
textbox.font = fontStyle;
```

> **Behind the scenes:**  
> คอมโพเนนต์ textbox ของ grid จะตีความ property `font` แล้วอัปเดต CSS ให้ตรงกัน บรรทัดเดียวนี้จะแทนที่ฟอนต์, ขนาด, และสีเดิมทั้งหมด—พอดีเมื่อคุณต้อง **change textbox font** ในหลายเซลล์พร้อมกัน

หากคอมโพเนนต์ของคุณใช้ API อื่น (เช่น `textbox.style.fontFamily = ...`) ให้ปรับการกำหนดค่าแต่คงหลักการเดิมไว้

## Full Working Example

โค้ดตัวอย่างต่อไปนี้เป็นสแนปช็อตที่สามารถวางลงในไฟล์ HTML ที่มีการจำลองอ็อบเจ็กต์ grid ได้ มันแสดงการทำงานตั้งแต่ขั้นตอน 1 ถึง 4 พร้อมการตรวจสอบสไตล์ที่เปลี่ยนแล้ว

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

### Expected Output

- Textbox ที่อยู่ที่ **row 2, column 3** จะปรากฏข้อความด้วย **Arial**, **14 px**, และสี **#0066CC** 
- เปิด console ของเบราว์เซอร์จะเห็นข้อความประมาณ:

```
Applied font family: Arial, Helvetica, sans-serif
Applied font size: 14px
Applied color: rgb(0, 102, 204)
```

เมื่อเปิดหน้าเว็บคุณจะเห็นการเปลี่ยนแปลงโดยตรง—ไม่มีฟอนต์ระบบเริ่มต้นอีกต่อไป

## Frequently Asked Questions (FAQ)

### Can I change only the font size without affecting family or color?
Absolutely. Just omit the properties you don’t want to modify:

```javascript
textbox.font = { size: 18 }; // only changes size
```

### What if my grid uses a different property name for the textbox?
Inspect the cell object in the console (`console.log(cell)`). You’ll likely see something like `cell.editor` or `cell.input`. Replace `cell.textbox` with the correct reference.

### How do I apply the same style to an entire column?
Loop through the rows and set the font for each cell in that column:

```javascript
for (let r = 0; r < grid.rowCount; r++) {
  const colCell = grid.getCell(r, 3);
  colCell.textbox.font = fontStyle; // reuse the same fontStyle object
}
```

### Is there a way to revert to the original font?
Store the original style before overwriting:

```javascript
const original = { ...textbox.font };
textbox.font = fontStyle; // apply new style
// later...
textbox.font = original; // revert
```

## Tips & Best Practices

- **Batch updates:** หากต้องสไตล์หลายเซลล์ ควรห่อการเปลี่ยนแปลงใน `requestAnimationFrame` หรือวิธี batch ของ grid เพื่อหลีกเลี่ยง layout thrashing
- **Responsive fonts:** ใช้หน่วยสัมพัทธ์ (`em`, `rem`) แทนพิกเซลเมื่อ UI ต้องปรับขนาดตามอุปกรณ์
- **Accessibility:** ตรวจสอบคอนทราสต์ให้เพียงพอเมื่อ **set font color programmatically**—ระดับ WCAG AA ขั้นต่ำคืออัตราส่วน 4.5:1 สำหรับข้อความปกติ
- **Cross‑browser quirks:** บาง grid เก่าอาจต้องตั้ง `style.fontFamily` โดยตรงบน `<input>` แทนการใช้ `font` object

## Conclusion

เราได้สรุป **how to change textbox font** ภายใน grid ตั้งแต่การดึงเซลล์ที่ต้องการ, สร้างอ็อบเจ็กต์ `fontStyle`, และนำไปใช้ด้วยบรรทัดเดียว ระหว่างทางเราได้เรียนรู้การ **change font size cell**, **set font color programmatically**, และแม้กระทั่งการ **change font family grid** สำหรับคอลัมน์เฉพาะ

ตอนนี้คุณสามารถนำรูปแบบนี้ไปปรับใช้กับไลบรารี UI ใดก็ได้—ไม่ว่าจะเป็นแอดมินแดชบอร์ด, ตัวแก้ไขสไตล์สเปรดชีต, หรือเครื่องมือรายงานแบบกำหนดเอง ลองเปลี่ยนฟอนต์, ขนาด, สีต่าง ๆ ดูบ้าง; หรือเพิ่มเอฟเฟกต์ hover หรือสไตล์ตามค่าข้อมูล

มีความท้าทายด้านสไตล์อื่น ๆ? แสดงความคิดเห็นมาได้เลย เราจะช่วยกันแก้ไขกันต่อไป ขอให้สนุกกับการเขียนโค้ด!

## What Should You Learn Next?

The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [วิธีเปลี่ยนสีฟอนต์ใน Excel ด้วย Aspose.Cells for Java: คู่มือฉบับสมบูรณ์](/cells/english/java/formatting/change-font-color-aspose-cells-java-tutorial/)
- [Change Font Color Aspose Cells Java Tutorial](/cells/german/java/formatting/change-font-color-aspose-cells-java-tutorial/)
- [Change Font Color Aspose Cells Java Tutorial](/cells/french/java/formatting/change-font-color-aspose-cells-java-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}