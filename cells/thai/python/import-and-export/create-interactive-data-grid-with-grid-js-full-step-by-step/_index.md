---
category: general
date: 2026-06-21
description: สร้างกริดข้อมูลแบบโต้ตอบด้วย Grid.js และเรียนรู้วิธีแสดงตารางข้อมูล JSON
  พร้อมการจัดเรียง การแบ่งหน้า และการค้นหา เหมาะสำหรับแดชบอร์ดเว็บ
draft: false
keywords:
- create interactive data grid
- display json data table
- how to use gridjs
language: th
og_description: สร้างกริดข้อมูลแบบโต้ตอบภายในไม่กี่นาที เรียนรู้วิธีใช้ Grid.js เพื่อแสดงตารางข้อมูล
  JSON พร้อมการแบ่งหน้า การจัดเรียง และการค้นหา.
og_title: สร้างกริดข้อมูลเชิงโต้ตอบด้วย Grid.js – บทเรียนเต็มรูปแบบ
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
title: สร้างกริดข้อมูลเชิงโต้ตอบด้วย Grid.js – คู่มือเต็มขั้นตอนต่อขั้นตอน
url: /th/python/import-and-export/create-interactive-data-grid-with-grid-js-full-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# สร้างตารางข้อมูลแบบโต้ตอบด้วย Grid.js – คู่มือเต็มขั้นตอน

เคยสงสัยไหมว่า **การสร้างตารางข้อมูลแบบโต้ตอบ** ที่ให้ผู้ใช้เรียงลำดับ, ค้นหา, และแบ่งหน้าแถวได้โดยไม่ต้องเขียน backend? คุณไม่ได้เป็นคนเดียวที่มีคำถามนี้ ในหลาย ๆ แดชบอร์ด จุดเจ็บปวดที่ใหญ่ที่สุดคือการเปลี่ยนไฟล์ JSON แบบคงที่ให้เป็นตารางที่ลื่นไหลและสามารถค้นหาได้—เหมือนสเปรดชีตแต่ทำงานทั้งหมดในเบราว์เซอร์

ในบทเรียนนี้เราจะอธิบาย **วิธีใช้ Grid.js** เพื่อ **แสดงตารางข้อมูล JSON** บนหน้า HTML ธรรมดา เมื่อเสร็จแล้วคุณจะได้ตัวอย่างที่ทำงานได้และสามารถนำไปใส่ในโปรเจกต์ใดก็ได้ พร้อมเคล็ดลับการปรับแต่งแถบเครื่องมือ, การจัดการชุดข้อมูลขนาดใหญ่, และการหลีกเลี่ยงข้อผิดพลาดทั่วไป

## สิ่งที่คุณจะได้เรียนรู้

- วิธีดึงไฟล์ JSON ที่กำหนดคอลัมน์และแถว
- วิธีเริ่มต้น **Grid.js** พร้อมการแบ่งหน้า, การเรียงลำดับ, การค้นหา, และแถบเครื่องมือแบบกำหนดเอง
- วิธีเรนเดอร์กริดลงในคอนเทนเนอร์เป้าหมาย
- การปรับแต่งเพิ่มเติม: ฟอร์แมตเซลล์แบบกำหนดเอง, การสลับธีม, และการจัดการข้อผิดพลาด
- ตัวอย่างโค้ดที่พร้อมคัดลอก‑วางใช้ได้ทันที

### ข้อกำหนดเบื้องต้น

ก่อนที่เราจะเริ่มลงลึก ตรวจสอบให้แน่ใจว่าคุณมี:

1. เบราว์เซอร์สมัยใหม่ (Chrome, Edge, หรือ Firefox) – Grid.js ใช้คุณสมบัติ ES6
2. โฟลเดอร์ในเครื่องหรือบนเซิร์ฟเวอร์ที่มีไฟล์ `grid_data.json` (เราจะอธิบายรูปแบบ)
3. ความคุ้นเคยพื้นฐานกับ HTML และ JavaScript – ไม่ต้องใช้เทคโนโลยีพิเศษ เพียงเปิดไฟล์ `.html` ในเบราว์เซอร์

ไม่ต้องใช้เครื่องมือสร้าง, ไม่ต้อง `npm install`, ไม่ต้องโค้ดฝั่งเซิร์ฟเวอร์ นั่นแหละคือความสวยงามของ **การสร้างตารางข้อมูลแบบโต้ตอบ** ด้วย Grid.js: ทำงานโดยตรงจาก CDN

---

## ขั้นตอนที่ 1: เตรียม JSON ที่กำหนดตารางของคุณ

สิ่งแรกที่คุณต้องมีคือ payload JSON ที่บอก Grid.js ว่ามีคอลัมน์อะไรบ้างและจะแสดงแถวอย่างไร คิดว่าเป็นแบบแปลนสำหรับ **การแสดงตารางข้อมูล JSON** ตัวอย่างขนาดเล็กนี้สามารถบันทึกเป็น `grid_data.json` ในโฟลเดอร์เดียวกับไฟล์ HTML ของคุณได้:

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

*ทำไมต้องใช้รูปแบบนี้?* Grid.js คาดหวัง `columns` เป็นอาเรย์ของสตริง (หรืออ็อบเจกต์สำหรับการตั้งค่าขั้นสูง) และ `rows` เป็นอาเรย์ของอาเรย์ที่แต่ละอาเรย์ย่อยตรงกับลำดับคอลัมน์ คุณสามารถเพิ่มคอลัมน์หรืออ็อบเจกต์ซ้อนได้ตามต้องการ – Grid.js จะเรนเดอร์ให้ตราบใดที่โครงสร้างสอดคล้องกัน

> **เคล็ดลับมือโปร:** หากคุณดึงข้อมูลจาก API เพียงเปลี่ยน `fetch('grid_data.json')` ให้เป็น URL ของ endpoint ของคุณ ส่วนที่เหลือของโค้ดไม่ต้องแก้ไข

---

## ขั้นตอนที่ 2: เริ่มต้น Grid.js – ใจกลางของ **how to use gridjs**

เมื่อแหล่งข้อมูลพร้อมแล้ว เราต้องนำ Grid.js เข้ามาในหน้าและบอกให้มันทำงานตามที่เราต้องการ ที่นี่คือจุดที่เราจริง ๆ **สร้างตารางข้อมูลแบบโต้ตอบ** ด้วยฟีเจอร์การแบ่งหน้า, การเรียงลำดับ, และปุ่มแถบเครื่องมือที่สะดวก

```html
<!-- Load Grid.js from the CDN -->
<script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
<link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet"/>
```

CDN จะให้คุณเวอร์ชันล่าสุดที่เสถียร, และธีม Meri­maid จะเพิ่มลุคที่สะอาดและทันสมัยโดยอัตโนมัติ คุณสามารถสลับเป็น `gridjs.min.css` หากต้องการสไตล์เริ่มต้น

ต่อไป, ภายในแท็ก `<script>` ให้ดึง JSON แล้วเริ่มต้นกริด:

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

### แยกรายละเอียดตัวเลือก

| ตัวเลือก | ทำอะไร | ทำไมสำคัญ |
|----------|--------|-----------|
| `pagination` | แบ่งแถวเป็นหลายหน้า (ค่าเริ่มต้น 10 แถวต่อหน้า) | ทำให้ตารางขนาดใหญ่ใช้งานได้ง่ายโดยไม่ทำให้ UI หนาแน่น |
| `sort` | คลิกหัวคอลัมน์เพื่อสลับการเรียงจากน้อยไปมากหรือมากไปน้อย | ผู้ใช้สามารถค้นหาแถวที่มีค่ามากที่สุดได้อย่างรวดเร็ว |
| `search` | เพิ่มช่องกรอกข้อความที่กรองแถวแบบเรียลไทม์ | เหมาะสำหรับการค้นหาแบบฉับพลันโดยไม่ต้องโหลดข้อมูลใหม่ |
| `toolbar` | เพิ่มปุ่มหรือดรอปดาวน์ด้านบนกริด | เหมาะสำหรับการทำ “Help”, “Export”, หรือ “Refresh” |
| `formatter` | ให้คุณคืนค่า HTML ดิบสำหรับเซลล์ | ตัวอย่างนี้จะแปลงสตริงอีเมลเป็นลิงก์ mailto ที่คลิกได้ |

> **ทำไมต้องใช้วิธีนี้?** การกำหนดค่ากริดแบบ declarative ทำให้คุณปรับพฤติกรรมได้ง่ายโดยไม่ต้องแก้ไขโลจิกการเรนเดอร์หลัก นี่คือวิธีที่แนะนำสำหรับ **how to use Grid.js** ในโปรเจกต์ส่วนใหญ่

---

## ขั้นตอนที่ 3: เรนเดอร์กริดลงในหน้าเว็บของคุณ

บรรทัดสุดท้ายของสคริปต์—`grid.render(document.getElementById('grid-container'))`—จะฉีดตารางที่ทำงานเต็มรูปแบบเข้าไปใน `<div>` ที่คุณวางไว้ใน `<body>`:

```html
<div id="grid-container"></div>
```

เท่านี้ เมื่อหน้าโหลด เบราว์เซอร์จะดึง JSON, สร้างอินสแตนซ์ Grid.js, และวาดตารางโต้ตอบบนหน้าจอ ไม่มีการรีเฟรชหรือการเรียกเซิร์ฟเวอร์หลังจากโหลดครั้งแรก

---

## ตัวเลือกเสริม: การปรับสไตล์และธีม

หากธีม Meri­maid ไม่ตรงกับสไตล์ของคุณ คุณสามารถสลับเป็นธีมในตัว (`gridjs.min.css`) หรือเขียน CSS ของคุณเอง ตัวอย่างเช่น การทำให้พื้นหลังหัวคอลัมน์เป็นสีเทาอ่อน:

```css
.gridjs-th {
  background-color: #f5f5f5;
}
```

ใส่โค้ดนี้ในแท็ก `<style>` หรือไฟล์สไตล์ชีตภายนอก Grid.js รองรับตัวเลือก CSS มาตรฐาน ดังนั้นคุณจึงควบคุมฟอนต์, สี, และระยะห่างได้เต็มที่

---

## ข้อผิดพลาดที่พบบ่อยและวิธีหลีกเลี่ยง

| ปัญหา | อาการ | วิธีแก้ |
|--------|--------|--------|
| **ข้อผิดพลาด CORS** เมื่อดึง JSON จากโดเมนอื่น | คอนโซลแสดง “Blocked by CORS policy” | ให้โฮสต์ JSON บนโดเมนเดียวกันหรือเปิดใช้งาน CORS บนเซิร์ฟเวอร์ |
| **ชุดข้อมูลขนาดใหญ่ทำให้ช้า** | การเลื่อนหน้าล่าช้า, การแบ่งหน้าช้า | ใช้ `server` pagination (`pagination: { server: { url: (prev, page, limit) => … } }`) หรือโหลดแถวแบบ lazy‑load |
| **ปุ่มแถบเครื่องมือไม่แสดง** | ไม่เห็นปุ่มแม้ว่า `toolbar.enabled: true` จะตั้งค่า | ตรวจสอบว่าคุณใช้ Grid.js เวอร์ชัน 2.0 ขึ้นไป; เวอร์ชันเก่ามี API ของ toolbar แตกต่าง |
| **ลิงก์อีเมลไม่คลิกได้** | Formatter คืนค่าเป็นข้อความธรรมดา | คืนค่า `gridjs.html(...)` แทนสตริงธรรมดา ตามตัวอย่าง |

การจัดการปัญหาเหล่านี้ตั้งแต่ต้นจะช่วยคุณประหยัดเวลาดีบักหลายชั่วโมง

---

## ตัวอย่างทำงานเต็มรูปแบบ (คัดลอก‑วางได้)

ด้านล่างเป็นไฟล์ HTML สมบูรณ์ที่คุณสามารถบันทึกเป็น `index.html` เปิดในเบราว์เซอร์และจะเห็นการสาธิต **การสร้างตารางข้อมูลแบบโต้ตอบ** ที่ **แสดงตารางข้อมูล JSON** พร้อมการเรียงลำดับ, ค้นหา, และปุ่มช่วยเหลือ



## คุณควรเรียนรู้อะไรต่อไป?

บทเรียนต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งรวมโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายขั้นตอนเพื่อช่วยคุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการทำงานอื่น ๆ ในโปรเจกต์ของคุณ

- [วิธีสร้างรายการตรวจสอบข้อมูลใน Excel ด้วย Aspose.Cells สำหรับ Java: คู่มือขั้นตอน](/cells/english/java/data-validation/excel-data-validation-aspose-cells-java/)
- [วิธีสร้างกล่องทำเครื่องหมายใน Excel ด้วย Aspose.Cells สำหรับ .NET | บทเรียนการตรวจสอบข้อมูล](/cells/english/net/data-validation/create-checkboxes-net-excel-aspose-cells/)
- [สร้างและนำเข้า XML ไปยัง Excel ด้วย Aspose.Cells สำหรับ Java](/cells/english/java/import-export/create-import-xml-data-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}