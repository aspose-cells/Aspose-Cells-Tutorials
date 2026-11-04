---
category: general
date: 2026-10-20
description: คัดลอก Pivot Table ไปยังเวิร์กบุ๊กใหม่โดยใช้ Aspose.Cells และเรียนรู้วิธีส่งออกรูปร่างที่แก้ไขได้ไปยัง
  PowerPoint ในคู่มือเดียว
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table to new workbook
- copy rows between worksheets
- Aspose.Cells copy rows
- export shape to PowerPoint
- editable textbox in PowerPoint
language: th
lastmod: 2026-10-20
og_description: คัดลอก Pivot Table ไปยังเวิร์กบุ๊กใหม่โดยใช้ Aspose.Cells และส่งออกรูปทรงที่แก้ไขได้ไปยัง
  PowerPoint—โค้ดขั้นตอนต่อขั้นตอนที่คุณสามารถรันได้วันนี้
og_image_alt: Screenshot showing copy pivot table to new workbook using Aspose.Cells
og_title: คัดลอกตาราง Pivot ไปยังเวิร์กบุ๊กใหม่, ส่งออกรูปร่างไปยัง PowerPoint
schemas:
- author: Aspose
  dateModified: '2026-10-20'
  description: Copy pivot table to new workbook using Aspose.Cells and learn how to
    export an editable shape to PowerPoint in a single guide.
  headline: Copy pivot table to new workbook, export shape to PowerPoint
  type: TechArticle
- description: Copy pivot table to new workbook using Aspose.Cells and learn how to
    export an editable shape to PowerPoint in a single guide.
  name: Copy pivot table to new workbook, export shape to PowerPoint
  steps:
  - name: – Load the source workbook and select the first worksheet
    text: '```csharp // Load the workbook that already contains the pivot table Workbook
      srcWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");'
  - name: – Define the cell area that includes the pivot table
    text: '```csharp // CellArea(startRow, startColumn, endRow, endColumn) // Here
      we copy rows 0‑20 and columns 0‑10, which covers the whole pivot table CellArea
      sourceArea = new CellArea(0, 0, 20, 10); ```'
  - name: – Create the destination workbook and get its first worksheet
    text: '```csharp // Create an empty workbook that will receive the copied range
      Workbook destWorkbook = new Workbook();'
  - name: – Copy the rows from the source area to the destination sheet
    text: '```csharp // CopyRows(startRow, endRow, destinationCells, destinationStartRow)
      srcWorksheet.Cells.CopyRows( sourceArea.StartRow, sourceArea.EndRow, destWorksheet.Cells,
      0); // start at row 0 in the destination sheet ```'
  - name: – Save the new workbook
    text: '```csharp destWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx"); ```'
  - name: – Create a new workbook and access its first worksheet
    text: '```csharp Workbook workbook = new Workbook(); // Empty workbook Worksheet
      worksheet = workbook.Worksheets[0]; // First (and only) sheet ```'
  - name: – Add a textbox shape to the worksheet
    text: '```csharp // AddTextBox(startRow, startColumn, width, height, text) int
      shapeIndex = worksheet.Shapes.AddTextBox(10, 10, 200, 50, "Editable text");
      ```'
  - name: – Retrieve the shape and modify its text
    text: '```csharp Shape textShape = worksheet.Shapes[shapeIndex]; textShape.Text
      = "Change me in PowerPoint"; ```'
  - name: – Save the workbook as a PowerPoint presentation
    text: '```csharp workbook.Save("YOUR_DIRECTORY/Presentation.pptx", SaveFormat.Pptx);
      ```'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Pivot Table
- PowerPoint Export
title: คัดลอกตาราง Pivot ไปยังสมุดงานใหม่, ส่งออกรูปร่างไปยัง PowerPoint
url: /th/net/pivot-tables/copy-pivot-table-to-new-workbook-export-shape-to-powerpoint/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# คัดลอก pivot table ไปยัง workbook ใหม่, ส่งออก shape ไปยัง PowerPoint

หากคุณต้องการ **คัดลอก pivot table ไปยัง workbook ใหม่** พร้อมคงไว้ซึ่งการทำงานของมัน คู่มือนี้จะแสดงให้คุณเห็นอย่างชัดเจนว่าทำอย่างไรด้วย Aspose.Cells คุณยังจะได้เห็นวิธีที่เร็วที่สุดในการ **ส่งออก shape ที่แก้ไขได้ไปยัง PowerPoint** เพื่อให้ textbox ยังคงสามารถแก้ไขได้หลังการแปลง

หลายนักพัฒนาสมมติว่าการคัดลอกช่วงที่มี pivot table จะทำให้สูญเสียตรรกะของ pivot, หรือว่า shape จะกลายเป็นภาพคงที่เมื่อบันทึกเป็น PPTX บทแนะนำนี้ทำลายความเชื่อนั้นและให้คุณได้โซลูชันที่เชื่อถือได้พร้อมใช้งานในระดับการผลิต

ในส่วนต่อไปนี้คุณจะได้:

* โหลด workbook ต้นฉบับและคัดลอกช่วงที่รวม pivot table
* สร้าง workbook ปลายทางที่มี pivot table เดียวกัน
* เพิ่ม shape textbox, แก้ไขข้อความของมัน, แล้วบันทึก workbook เป็นไฟล์ PowerPoint ที่ textbox ยังคงแก้ไขได้
* เข้าใจว่าทำไมต้องเรียกใช้ API แต่ละตัวและหลีกเลี่ยงข้อผิดพลาดทั่วไป

**Prerequisites**

* .NET 6.0 หรือใหม่กว่า (โค้ดนี้ยังทำงานกับ .NET Framework 4.7+)
* ติดตั้ง Aspose.Cells for .NET (`Install-Package Aspose.Cells`)
* ความรู้พื้นฐานเกี่ยวกับ C# และ Visual Studio (หรือ IDE ใด ๆ ที่คุณชอบ)

---

## คัดลอก pivot table ไปยัง workbook ใหม่

ส่วนนี้จะแสดงขั้นตอนการคัดลอกช่วงที่มี pivot table และคงไว้ซึ่งการกำหนด pivot ในไฟล์ใหม่

### Step 1 – Load the source workbook and select the first worksheet

```csharp
// Load the workbook that already contains the pivot table
Workbook srcWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");

// The first worksheet (index 0) holds the pivot table we want to copy
Worksheet srcWorksheet = srcWorkbook.Worksheets[0];
```

*ทำไม?*  
`Workbook` คือจุดเริ่มต้นสำหรับการจัดการ Excel ใด ๆ ใน Aspose.Cells การเลือก worksheet ที่ถูกต้องทำให้เราทำงานกับตำแหน่งของ pivot table อย่างแม่นยำ

### Step 2 – Define the cell area that includes the pivot table

```csharp
// CellArea(startRow, startColumn, endRow, endColumn)
// Here we copy rows 0‑20 and columns 0‑10, which covers the whole pivot table
CellArea sourceArea = new CellArea(0, 0, 20, 10);
```

*ทำไม?*  
pivot table อยู่ภายในบล็อกของเซลล์เฉพาะ การระบุ `CellArea` ที่ครอบคลุม pivot อย่างเต็มที่ทำให้ Aspose.Cells รู้ว่าจะคัดลอก pivot cache ที่อยู่เบื้องหลังด้วย

### Step 3 – Create the destination workbook and get its first worksheet

```csharp
// Create an empty workbook that will receive the copied range
Workbook destWorkbook = new Workbook();

// Destination worksheet (also index 0)
Worksheet destWorksheet = destWorkbook.Worksheets[0];
```

*ทำไม?*  
การสร้าง workbook ใหม่ช่วยรับประกันว่าจะไม่มี named range หรือ pivot ที่ขัดแย้ง ทำให้การคัดลอกสะอาดตา

### Step 4 – Copy the rows from the source area to the destination sheet

```csharp
// CopyRows(startRow, endRow, destinationCells, destinationStartRow)
srcWorksheet.Cells.CopyRows(
    sourceArea.StartRow,
    sourceArea.EndRow,
    destWorksheet.Cells,
    0); // start at row 0 in the destination sheet
```

*ทำไม?*  
`CopyRows` เป็นส่วนหนึ่งของ **Aspose.Cells copy rows** API มันคัดลอกทั้งค่าของเซลล์และ pivot cache ที่ซ่อนอยู่ ทำให้ pivot table ยังคงทำงานได้หลังการย้าย

### Step 5 – Save the new workbook

```csharp
destWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx");
```

*Result*  
เปิด `CopyWithPivot.xlsx` ใน Excel pivot table จะปรากฏเหมือนเดิมในไฟล์ต้นฉบับ และคุณสามารถรีเฟรชหรือแก้ไขได้ตามปกติ

---

## ส่งออก shape ที่แก้ไขได้ไปยัง PowerPoint

ต่อไปเราจะเพิ่ม shape textbox, เปลี่ยนเนื้อหา, แล้วบันทึก workbook เป็นไฟล์ PPTX shape จะคงอยู่ในรูปแบบที่สามารถแก้ไขได้เต็มที่เมื่อเปิดใน PowerPoint

### Step 1 – Create a new workbook and access its first worksheet

```csharp
Workbook workbook = new Workbook();          // Empty workbook
Worksheet worksheet = workbook.Worksheets[0]; // First (and only) sheet
```

### Step 2 – Add a textbox shape to the worksheet

```csharp
// AddTextBox(startRow, startColumn, width, height, text)
int shapeIndex = worksheet.Shapes.AddTextBox(10, 10, 200, 50, "Editable text");
```

*ทำไม?*  
`AddTextBox` สร้าง **editable textbox in PowerPoint**‑compatible shape พิกัดใช้หน่วยเป็น point; ปรับให้เหมาะกับเลย์เอาต์ของคุณ

### Step 3 – Retrieve the shape and modify its text

```csharp
Shape textShape = worksheet.Shapes[shapeIndex];
textShape.Text = "Change me in PowerPoint";
```

*ทำไม?*  
การเข้าถึงอ็อบเจกต์ `Shape` โดยตรงทำให้คุณเปลี่ยนคุณสมบัติต่าง ๆ เช่น `Text`, `Font` หรือ `Fill` ขั้นตอนนี้แสดงวิธีตั้งค่าข้อความเริ่มต้นโดยโปรแกรม

### Step 4 – Save the workbook as a PowerPoint presentation

```csharp
workbook.Save("YOUR_DIRECTORY/Presentation.pptx", SaveFormat.Pptx);
```

*Result*  
เปิด `Presentation.pptx` ใน Microsoft PowerPoint textbox จะปรากฏบนสไลด์แรก และคุณสามารถดับเบิล‑คลิกเพื่อแก้ไขข้อความได้เช่นเดียวกับ shape พื้นฐานของ PowerPoint

---

## Expected output

| File | What you’ll see |
|------|-----------------|
| `CopyWithPivot.xlsx` | Worksheet ที่มี pivot table ดั้งเดิม, ทำงานเต็มรูปแบบ (รีเฟรชได้) |
| `Presentation.pptx` | สไลด์เดียวที่มี textbox ที่แก้ไขได้และแสดงข้อความ “Change me in PowerPoint” |

---

## Common pitfalls and best‑practice tips

* **Pivot cache loss** – หากคุณคัดลอกเฉพาะค่าของเซลล์ (เช่นใช้ `CopyRows` พร้อม `PasteOptions` ตั้งค่าเป็น `PasteValues`) pivot cache จะถูกละเว้นและตารางจะกลายเป็นสถิติกับการคัดลอกใช้ overload เริ่มต้นของ `CopyRows` ตามที่แสดงเสมอ
* **Shape positioning** – `AddTextBox` ใช้หน่วย point ไม่ใช่ดัชนีเซลล์ของ Excel ทดสอบพิกัดบนไฟล์ตัวอย่างเพื่อหลีกเลี่ยงการวางผิดตำแหน่งบนสไลด์
* **File format mismatch** – การบันทึก workbook เป็น PPTX ด้วย `SaveFormat.Pptx` จะทำการแปลง shape ที่รองรับทั้งหมดโดยอัตโนมัติ การพยายามบันทึกเป็น `Pdf` จะทำให้ shape ถูกแปลงเป็นภาพและไม่สามารถแก้ไขได้

---

## Conclusion

คุณได้เรียนรู้วิธี **คัดลอก pivot table ไปยัง workbook ใหม่** และวิธี **ส่งออก shape ที่แก้ไขได้ไปยัง PowerPoint** ด้วย Aspose.Cells for .NET ตัวอย่างโค้ดที่ทำงานได้เต็มรูปแบบครอบคลุมทุกการเรียก API ที่จำเป็น, อธิบายเหตุผลของแต่ละขั้นตอน, และแสดงผลลัพธ์ที่คาดหวัง

ต่อไปคุณอาจสำรวจ:

* **Working with charts** – คัดลอกแผนภูมิพร้อมกับ pivot tables (`Aspose.Cells copy rows between worksheets`).
* 

## What Should You Learn Next?

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งข้อมูลมีตัวอย่างโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายขั้นตอนเพื่อช่วยคุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการทำงานอื่น ๆ ในโครงการของคุณ

- [Create New Workbook – How to Copy a Worksheet with a Pivot Table](/cells/english/net/excel-copy-worksheet/create-new-workbook-how-to-copy-a-worksheet-with-a-pivot-tab/)
- [Copy pivot table and export Excel to PPTX with Aspose.Cells](/cells/english/net/converting-excel-files-to-other-formats/copy-pivot-table-and-export-excel-to-pptx-with-aspose-cells/)
- [Create New Workbook in C# – Copy Pivot Table](/cells/english/net/pivot-tables/create-new-workbook-in-c-copy-pivot-table/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}