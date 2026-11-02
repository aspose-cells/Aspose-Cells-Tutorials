---
category: general
date: 2026-05-30
description: เรียนรู้วิธีสร้างอินสแตนซ์ GridJsOptions และกำหนดค่าตัวเลือกกริดด้วย
  JavaScript สำหรับตารางแบบไดนามิก คู่มือแบบขั้นตอนพร้อมโค้ดเต็ม
draft: false
keywords:
- create gridjsoptions instance
- configure grid options javascript
- gridjs initialization
- javascript data grid settings
- dynamic table configuration
language: th
og_description: สร้างอินสแตนซ์ GridJsOptions และกำหนดค่าตัวเลือกกริดใน JavaScript
  ภายในไม่กี่นาที ตัวอย่างเต็ม คำอธิบาย และเคล็ดลับการปฏิบัติที่ดีที่สุด
og_title: สร้างอินสแตนซ์ GridJsOptions – กำหนดค่าตัวเลือกกริดด้วย JavaScript
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
title: สร้างอินสแตนซ์ GridJsOptions – กำหนดค่าตัวเลือกกริดใน JavaScript
url: /th/net/link-and-configuration-operations/create-gridjsoptions-instance-configure-grid-options-javascr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# สร้าง GridJsOptions Instance – กำหนดค่า Grid Options ด้วย JavaScript

เคยสงสัยไหมว่าจะแนวทางการ **create GridJsOptions instance** อย่างไรโดยไม่ต้องค้นหาเอกสารที่กระ散? คุณไม่ได้เป็นคนเดียว เมื่อคุณต้องการตารางที่เรียบหรูและสามารถเรียงลำดับได้บนหน้าเว็บ การเชี่ยวชาญวิธีการ **configure grid options JavaScript** เป็นขั้นตอนแรกสู่ UI ที่ดูดี

ในบทแนะนำนี้ เราจะพาคุณผ่านโค้ดที่จำเป็นอย่างละเอียด อธิบายว่าการตั้งค่าแต่ละอย่างสำคัญอย่างไร และแสดงตัวอย่างที่สมบูรณ์พร้อมรันได้ เมื่อเสร็จคุณจะรู้สึกสบายใจในการ **create GridJsOptions instance**, ปรับการจัดแนว, การแบ่งหน้า, และแม้กระทั่งตัวแปลงเซลล์แบบกำหนดเอง—ทั้งหมดด้วย JavaScript ธรรมดา

## สิ่งที่คุณจะได้เรียนรู้

- วิธี **create GridJsOptions instance** ตั้งแต่เริ่มต้น
- คุณสมบัติหลักที่ทำให้คุณ **configure grid options JavaScript** (การเรียงลำดับ, การแบ่งหน้า, การจัดรูปแบบตัวเลข ฯลฯ)
- จุดบกพร่องทั่วไป (เช่น การผสมประเภทสตริงและตัวเลข) และวิธีหลีกเลี่ยง
- หน้า HTML เต็มรูปแบบที่คุณสามารถคัดลอก‑วางไปใช้ในโปรเจกต์ใดก็ได้และเห็นผลทันที

### ข้อกำหนดเบื้องต้น

- เบราว์เซอร์สมัยใหม่ (Chrome, Edge, Firefox) – ไม่ต้องใช้เครื่องมือสร้าง
- ความคุ้นเคยพื้นฐานกับ JavaScript (ตัวแปร, อ็อบเจกต์, DOM)
- ไลบรารี Grid.js (เราจะดึงจาก CDN)

หากสิ่งใดเหล่านี้ฟังดูแปลกใหม่ อย่าตื่นตระหนก—แต่ละขั้นตอนมีการทบทวนสั้น ๆ ให้คุณตามไปด้วย

---

## Step 1: Load Grid.js and Prepare the HTML Skeleton

ก่อนที่เราจะ **create GridJsOptions instance** เราต้องมีไลบรารีเอง วิธีที่ง่ายที่สุดคือใช้ CDN อย่างเป็นทางการ ด้านล่างเป็นโครงสร้าง HTML ขั้นต่ำที่ยังสงวน `<div>` ไว้สำหรับการเรนเดอร์กริด

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

> **Pro tip:** Keep the CSS link before your own styles so the grid’s default theme loads correctly.

### ทำไมเรื่องนี้ถึงสำคัญ

การโหลดไลบรารีจาก CDN ทำให้คุณได้เวอร์ชันล่าสุดที่เสถียรเสมอโดยไม่ต้องติดตั้งในเครื่อง `<div id="grid-wrapper">` คือพื้นที่สำรองที่คอนสตรัคเตอร์ของ Grid.js จะทำการเรนเดอร์เมื่อเรา **configure grid options JavaScript**

## Step 2: Create a New GridJsOptions Instance

ตอนนี้มาถึงหัวใจของบทแนะนำ: บรรทัดที่จริง ๆ แล้ว **creates GridJsOptions instance** ในไฟล์แยกชื่อ `grid-config.js` (อ้างอิงจาก HTML ด้านบน) เราจะเขียนว่า:

```javascript
// grid-config.js

// Step 2: Create a new GridJsOptions instance to configure grid behavior
const gridOptions = new GridJsOptions();
```

บรรทัดเดียวนี้ให้คุณได้อ็อบเจกต์ที่สะอาดพร้อมเริ่มเติมค่าการตั้งค่า คิดว่า `gridOptions` เป็นแผงควบคุมสำหรับทุกฟีเจอร์ที่คุณจะเปิดใช้งานต่อไป

### สิ่งที่คุณกำลังกำหนดค่า

- **NumberFormatAlignment** – จัดแนวสตริงตัวเลขโดยอัตโนมัติ
- **Pagination** – ควบคุมขนาดหน้าและการนำทาง
- **Sorting** – เปิด/ปิดการเรียงลำดับคอลัมน์
- **Columns** – กำหนดหัวตาราง, ชนิดข้อมูล, และตัวแปลงแบบกำหนดเอง

## Step 3: Enable Number Alignment (A Common Requirement)

ตารางส่วนใหญ่มีการผสมข้อความและตัวเลข โดยค่าเริ่มต้น Grid.js จะจัดแนวซ้ายทั้งหมด ซึ่งดูแปลกสำหรับค่าการเงิน เพื่อ **configure grid options JavaScript** ให้จัดแนวอย่างถูกต้อง ให้ตั้งค่าแฟล็ก `NumberFormatAlignment`:

```javascript
// Enable left/right alignment for numeric strings
gridOptions.NumberFormatAlignment = true;
```

ทำไมต้องเปิดใช้งาน? เมื่อแฟล็กเป็น `true` Grid.js จะตรวจสอบแต่ละเซลล์; หากดูเหมือนตัวเลข (เช่น “1234”, “12.34%”) จะจัดแนวขวาโดยอัตโนมัติ การปรับเล็ก ๆ นี้ทำให้รายงานอ่านง่ายขึ้นมาก

## Step 4: Add Pagination and Sorting

กริดในโลกจริงมักไม่พอดีกับหน้าจอเดียว เราเปิดการแบ่งหน้า (10 แถวต่อหน้า) และให้ผู้ใช้สามารถเรียงลำดับคอลัมน์ใดก็ได้

```javascript
gridOptions.Pagination = {
  limit: 10,          // rows per page
  enabled: true
};

gridOptions.Sort = true;   // enables click‑to‑sort on all columns
```

### หมายเหตุกรณีขอบ

หากคุณต่อมาจัดหาข้อมูลจากแหล่งข้อมูลที่เองทำการแบ่งหน้าแล้ว คุณควรปิดการแบ่งหน้าที่สร้างโดย Grid.js เพื่อหลีกเลี่ยงการแบ่งหน้าแบบซ้อนกัน เพียงตั้งค่า `gridOptions.Pagination.enabled = false;`

## Step 5: Define Columns and Sample Data

ต่อไปเราจะป้อนข้อมูลจำลองให้กริดและบอกว่าคอลัมน์แต่ละอันหมายถึงอะไร ที่นี่คือจุดที่รูปแบบ **create gridjsoptions instance** ส่องแสงจริง—ทุกอย่างอยู่ในอ็อบเจกต์เดียวที่เรียบร้อย

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

สังเกตว่าเรารักษาค่า `id` ของคอลัมน์ให้ตรงกับคีย์ในแต่ละอ็อบเจกต์ข้อมูล คอนเวนชันนี้ทำให้ Grid.js แมปค่าอัตโนมัติ ลดความจำเป็นในการเขียนฟอร์แมตเตอร์กำหนดเองสำหรับทุกคอลัมน์

## Step 6: Instantiate the Grid with Our Options

เราสุดท้าย **configure grid options javascript** โดยส่งอ็อบเจกต์ `gridOptions` ไปยังคอนสตรัคเตอร์ของ Grid กริดจะเรนเดอร์ภายใน `<div id="grid-wrapper">` ที่เราจัดเตรียมไว้ก่อนหน้า

```javascript
// Create the Grid instance using the previously built options
const grid = new Grid(gridOptions);

// Render the grid into the page
grid.render(document.getElementById("grid-wrapper"));
```

เท่านี้ กระบวนการทั้งหมด—from **create gridjsoptions instance** to rendering—ใช้เวลาเขียนโค้ดไม่ถึงหนึ่งนาที

### ผลลัพธ์ที่คาดหวัง

เมื่อเปิดไฟล์ HTML ในเบราว์เซอร์ คุณควรเห็น:

- แถวหัวตารางที่มี “ID”, “Employee”, “Salary ($)”, “Dept.”
- ตัวเลขเงินเดือนจัดแนวขวา (ขอบคุณ `NumberFormatAlignment`)
- ตัวควบคุมการแบ่งหน้าที่ด้านล่าง (ถ้าคุณเพิ่มแถวมากกว่าสิบแถว)
- หัวคอลัมน์ที่คลิกได้เพื่อเรียงลำดับขึ้น/ลง

หากมีอะไรผิดพลาด ให้เปิดคอนโซลของเบราว์เซอร์ (F12) ตรวจสอบข้อความข้อผิดพลาด—บั๊กส่วนใหญ่มาจาก ID คอลัมน์ไม่ตรงกันหรือสคริปต์ไลบรารีหายไป

## Step 7: Advanced Tweaks (Optional)

ต่อไปนี้เป็นไอเดียสั้น ๆ ที่คุณสามารถทดลองได้เมื่อกริดพื้นฐานทำงานแล้ว

| ฟีเจอร์ | วิธีเปิดใช้งาน | เหตุผลที่ช่วย |
|---------|---------------|--------------|
| **Custom cell renderer** | `gridOptions.Columns[2].formatter = (cell) => \`<b>$${cell}</b>\`;` | เน้นเงินเดือนให้เป็นตัวหนา |
| **Search bar** | `gridOptions.Search = true;` | ให้ผู้ใช้กรองแถวได้ทันที |
| **Server‑side data** | Set `gridOptions.Server = { url: "/api/employees", then: data => data.items };` | รองรับข้อมูลหลายพันแถว |
| **Theme switching** | Add `gridOptions.ClassName = "gridjs-theme-dark";` | เข้ากับดีไซน์โหมดมืด |

คุณสามารถผสมและจับคู่ได้ตามต้องการ—Grid.js ถูกออกแบบให้ยืดหยุ่น อย่าลืมเก็บบรรทัด **create gridjsoptions instance** ด้านบนไว้เสมอ เพราะการปรับแต่งต่อ ๆ มาทั้งหมดอ้างอิงอ็อบเจกต์เดียวนี้

## Conclusion

เราได้พาคุณผ่านเวิร์กโฟลว์ครบวงจรเพื่อ **create GridJsOptions instance** และ **configure grid options JavaScript** สำหรับตารางข้อมูลที่ทำงานได้, เรียงลำดับได้, และแบ่งหน้าได้ จากการเริ่มต้นด้วยหน้า HTML ธรรมดา เราโหลดไลบรารี, สร้างอ็อบเจกต์ตัวเลือก, เปิดการจัดแนวตัวเลข, เพิ่มการแบ่งหน้า, กำหนดคอลัมน์, และสุดท้ายเรนเดอร์กริด

จากจุดนี้คุณสามารถ:

- แทนที่ `sampleData` แบบคงที่ด้วยการเรียก AJAX
- เพิ่มฟอร์แมตเตอร์กำหนดเองสำหรับวันที่, สกุลเงิน, หรือไอคอน
- ผสานกริดเข้ากับเฟรมเวิร์กเช่น React หรือ Vue (อ็อบเจกต์ `gridOptions` เดียวกันทำงานได้เช่นกัน)

ความเป็นไปได้แทบไม่มีที่สิ้นสุด และรูปแบบที่เราใช้—การรวมการตั้งค่าทั้งหมดไว้ใน **GridJsOptions** อินสแตนซ์เดียว—ช่วยให้โค้ดของคุณสะอาดและดูแลได้ง่าย

มีกรณีการใช้งานที่คุณไม่แน่ใจ? ฝากคอมเมนต์มาได้ เราจะสำรวจร่วมกัน ขอให้สนุกกับการเขียนโค้ดและสร้างตารางไดนามิกด้วย Grid.js!

## สิ่งที่คุณควรเรียนต่อ

- [วิธีสร้างและกำหนดค่า Excel Workbooks ด้วย Aspose.Cells .NET: คู่มือขั้นตอนโดยละเอียด](/cells/english/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)
- [วิธีสร้างและจัดรูปแบบ Excel Tables ด้วย Aspose.Cells for .NET | คู่มือขั้นตอนโดยละเอียด](/cells/english/net/tables-structured-references/aspose-cells-net-excel-tables-styling/)
- [วิธีสร้างและฟอร์แมต Excel Cells ด้วย Aspose.Cells for Java: คู่มือขั้นตอนโดยละเอียด](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}