---
category: general
date: 2026-08-14
description: ส่งออก Excel ไปยัง PowerPoint ด้วย Aspose.Cells และเรียนรู้วิธีคำนวณสูตร
  Excel ในโค้ด ตัวอย่าง C# ทีละขั้นตอนพร้อมซอร์สโค้ดเต็ม
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to powerpoint
- calculate excel formulas in code
- Aspose.Cells copy pivot table
- export editable objects pptx
- dynamic array EXPAND function
- C# workbook automation
language: th
lastmod: 2026-08-14
og_description: ส่งออก Excel ไปยัง PowerPoint ด้วย Aspose.Cells และคำนวณสูตร Excel
  ในโค้ด ปฏิบัติตามคู่มือฉบับเต็มนี้เพื่อสร้างไฟล์ PPTX ที่แก้ไขได้จากเวิร์กบุ๊ก.
og_image_alt: Screenshot showing an Excel sheet being exported to a PowerPoint slide
  with editable textboxes
og_title: ส่งออก Excel ไปยัง PowerPoint ด้วย Aspose.Cells – บทเรียนเต็ม C#
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: Export Excel to PowerPoint using Aspose.Cells and learn how to calculate
    Excel formulas in code. Step‑by‑step C# example with full source.
  headline: Export Excel to PowerPoint with Aspose.Cells – complete programming guide
  type: TechArticle
- description: Export Excel to PowerPoint using Aspose.Cells and learn how to calculate
    Excel formulas in code. Step‑by‑step C# example with full source.
  name: Export Excel to PowerPoint with Aspose.Cells – complete programming guide
  steps:
  - name: Why this works
    text: '* **`Workbook`** loads the entire Excel file into memory, giving you full
      API access. * **`CopyRange`** with `CopyPivotTable = true` ensures the pivot
      table’s data source, cache, and layout are duplicated exactly—something older
      versions of Aspose.Cells could not do. * Adding a new worksheet (`Copy`'
  - name: Explanation
    text: '* **`WorkbookDesigner`** is a high‑level helper that prepares the workbook
      for export, handling Smart Markers, named ranges, and layout adjustments. *
      Setting `ExportEditableObjects = true` tells Aspose.Cells to translate Excel
      drawings into PowerPoint shapes rather than flattening them into images.'
  - name: Why you might use this
    text: '* **Uniform data type:** Exporting as strings avoids type‑mismatch errors
      when the consumer expects text. * **Custom formatting:** Replace `value.ToString()`
      with any custom formatter (e.g., `value.ToString("yyyy-MM-dd")` for dates).'
  - name: How the calculation engine works
    text: '* The `Formula` property stores the expression exactly as you would type
      it in Excel. * `CalculateFormula()` triggers a full workbook recalculation,
      respecting dependencies between cells. * The `EXPAND` function (available in
      Excel 365) returns a spill range based on the source cell (`B1`) and the s'
  - name: What to verify
    text: '* Open `result.xlsx` in Excel to confirm the pivot table copy, the `EXPAND`
      formula result, and any custom‑exported strings. * Open `output.pptx` in PowerPoint;
      you should see a slide that mirrors the Excel layout, and all charts/textboxes
      should be editable.'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
- PowerPoint export
- Office 365 functions
title: ส่งออก Excel ไปยัง PowerPoint ด้วย Aspose.Cells – คู่มือการเขียนโปรแกรมฉบับสมบูรณ์
url: /th/net/converting-excel-files-to-other-formats/export-excel-to-powerpoint-with-aspose-cells-complete-progra/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ส่งออก Excel ไปยัง PowerPoint ด้วย Aspose.Cells – คู่มือการเขียนโปรแกรมแบบครบถ้วน

หากคุณต้องการ **ส่งออก Excel ไปยัง PowerPoint** อย่างอัตโนมัติ คู่มือนี้จะแสดงให้คุณเห็นขั้นตอนการทำด้วย Aspose.Cells สำหรับ .NET อย่างชัดเจน คุณยังจะได้เรียนรู้วิธี **คำนวณสูตร Excel ในโค้ด**, คัดลอก Pivot Table โดยไม่สูญเสียการกำหนดค่า, และใช้ฟังก์ชัน EXPAND ของ Office‑365 สำหรับอาเรย์แบบไดนามิก

ในส่วนต่อไปนี้ เราจะเดินผ่านตัวอย่าง C# จากโลกจริง, อธิบายเหตุผลที่แต่ละบรรทัดสำคัญ, และครอบคลุมข้อผิดพลาดทั่วไปเพื่อให้คุณสามารถปรับใช้โซลูชันนี้ในโครงการของคุณได้

## สิ่งที่บทเรียนนี้ครอบคลุม

* โหลดเวิร์กบุ๊กที่มีอยู่ (`input.xlsx`)  
* คัดลอกช่วงที่มี Pivot Table พร้อมคงการกำหนดค่าไว้  
* ส่งออกเวิร์กบุ๊กเป็นไฟล์ PowerPoint (`.pptx`) พร้อมกล่องข้อความและรูปร่างที่สามารถแก้ไขได้  
* ส่งออกช่วงเซลล์เป็นสตริงโดยใช้ตรรกะแบบกำหนดเอง  
* คำนวณสูตร Excel ในโค้ด รวมถึงฟังก์ชัน EXPAND ของ Office‑365  
* บันทึกเวิร์กบุ๊กขั้นสุดท้ายพร้อมการเปลี่ยนแปลงทั้งหมดที่ได้ทำ  

**ข้อกำหนดเบื้องต้น**  
* .NET 6.0 หรือใหม่กว่า (โค้ดนี้ยังทำงานกับ .NET Framework 4.7.2+)  
* Aspose.Cells สำหรับ .NET v25.11 หรือใหม่กว่า (ตัวเลือก `CopyPivotTable` ถูกแนะนำใน v25.11)  
* ความเข้าใจพื้นฐานเกี่ยวกับ C# และแนวคิดของ Excel เช่น ช่วง, Pivot Table, และสูตร  

> **เคล็ดลับมืออาชีพ:** ติดตั้ง Aspose.Cells ผ่าน NuGet (`Install-Package Aspose.Cells`) เพื่อให้โครงการของคุณอัปเดตด้วยฟีเจอร์ล่าสุด

## ส่งออก Excel ไปยัง PowerPoint ด้วย Aspose.Cells

งานหลักแรกคือการแปลงเวิร์กบุ๊กเป็นงานนำเสนอ PowerPoint พร้อมคงองค์ประกอบภาพทั้งหมดให้สามารถแก้ไขได้ นี่เป็นสิ่งสำคัญเมื่อคุณต้องการสร้างสไลด์เด็คจากรายงานการเงินหรือแดชบอร์ดโดยอัตโนมัติ

```csharp
using Aspose.Cells;
using Aspose.Cells.Export;      // ExportTableOptions, ExportOptions, etc.
using Aspose.Cells.Pivot;      // Pivot‑table APIs
using Aspose.Cells.Drawing;    // Shapes, textboxes, etc.

// Step 1: Load the workbook
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

// Step 2: Copy a range that contains a pivot table (preserves the definition)
Worksheet sourceSheet = workbook.Worksheets["Source"];
Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");   // includes a pivot table
Worksheet destinationSheet = workbook.Worksheets.Add("Copy");
destinationSheet.Cells.CopyRange(sourceRange, destinationSheet.Cells, new CopyOptions
{
    CopyPivotTable = true   // new option in v25.11
});
```

### ทำไมวิธีนี้ถึงได้ผล

* **`Workbook`** โหลดไฟล์ Excel ทั้งหมดเข้าสู่หน่วยความจำ, ให้คุณเข้าถึง API อย่างเต็มที่  
* **`CopyRange`** พร้อม `CopyPivotTable = true` ทำให้แหล่งข้อมูล, แคช, และการจัดวางของ Pivot Table ถูกคัดลอกอย่างแม่นยำ—สิ่งที่เวอร์ชันเก่าของ Aspose.Cells ไม่สามารถทำได้  
* การเพิ่มเวิร์กชีตใหม่ (`Copy`) ทำให้คุณสามารถเก็บแผ่นงานต้นฉบับไม่เปลี่ยนแปลง, ซึ่งเป็นประโยชน์สำหรับการตรวจสอบ  

## ส่งออกเวิร์กบุ๊กเป็น PowerPoint พร้อมวัตถุที่สามารถแก้ไขได้

ตอนนี้เราจะแปลงเวิร์กบุ๊กเป็นไฟล์ PowerPoint โดยการเปิดใช้งาน `ExportEditableObjects` ทุกแผนภูมิ, รูปร่าง, หรือกล่องข้อความจะกลายเป็นวัตถุ PowerPoint ดั้งเดิมที่ผู้ใช้สามารถแก้ไขได้โดยตรงหลังการส่งออก

```csharp
// Step 3: Export the workbook to PowerPoint with editable textboxes/shapes
WorkbookDesigner designer = new WorkbookDesigner(workbook);
designer.Process();   // processes Smart Markers if present
designer.ExportToPptx("YOUR_DIRECTORY/output.pptx", new ExportOptions
{
    ExportEditableObjects = true   // makes objects editable in the PPTX
});
```

### คำอธิบาย

* **`WorkbookDesigner`** เป็นตัวช่วยระดับสูงที่เตรียมเวิร์กบุ๊กสำหรับการส่งออก, จัดการ Smart Markers, ช่วงที่ตั้งชื่อ, และการปรับแต่งเลย์เอาต์  
* การตั้งค่า `ExportEditableObjects = true` บอก Aspose.Cells ให้แปลงภาพวาดของ Excel เป็นรูปร่าง PowerPoint แทนการแปลงเป็นภาพนิ่ง ซึ่งทำให้ได้สไลด์เด็คที่ **สามารถแก้ไขได้อย่างเต็มที่**  

> **กรณีขอบ:** หากเวิร์กบุ๊กของคุณมีแผนภูมิที่ซับซ้อนซึ่งสร้างจากการเชื่อมต่อข้อมูลภายนอก, โปรดตรวจสอบให้แน่ใจว่าการเชื่อมต่อเหล่านั้นได้รับการแก้ไขก่อนเรียก `ExportToPptx`, มิฉะนั้นแผนภูมิอาจแสดงเป็นสีขาว  

## ส่งออกช่วงเป็นสตริงโดยใช้ตรรกะแบบกำหนดเอง

บางครั้งคุณอาจต้องการค่าสตริงดิบสำหรับการประมวลผลต่อเนื่อง (เช่น การป้อนให้กับตัวแยกวิเคราะห์ CSV). คลาส `ExportTableOptions` ให้คุณควบคุมวิธีการแปลงแต่ละเซลล์

```csharp
// Step 4: Export a range as strings using custom logic
ExportTableOptions tableOptions = new ExportTableOptions
{
    ExportAsString = true,
    CustomExport = (cell, value) => value.ToString()   // simple conversion for each cell
};
workbook.Worksheets[0].Cells.ExportTableAsString(tableOptions, "A1:D10");
```

### ทำไมคุณอาจใช้วิธีนี้

* **ประเภทข้อมูลสม่ำเสมอ:** การส่งออกเป็นสตริงช่วยหลีกเลี่ยงข้อผิดพลาดการไม่ตรงกันของประเภทเมื่อผู้รับคาดหวังข้อความ  
* **การจัดรูปแบบแบบกำหนดเอง:** แทนที่ `value.ToString()` ด้วยฟอร์แมตเตอร์ที่กำหนดเองใด ๆ (เช่น `value.ToString("yyyy-MM-dd")` สำหรับวันที่)  

## คำนวณสูตร Excel ในโค้ด

ความต้องการทั่วไปคือ **คำนวณสูตร Excel ในโค้ด** โดยไม่ต้องเปิด Excel. Aspose.Cells มีเครื่องมือคำนวณในตัวที่ทำงานแบบออฟไลน์และรองรับฟังก์ชัน Office‑365 ล่าสุด, รวมถึง `EXPAND`

```csharp
// Step 5: Use the new Office‑365 EXPAND function to create a dynamic array
Worksheet firstSheet = workbook.Worksheets[0];
firstSheet.Cells["A1"].Formula = "EXPAND(B1,5,3)";   // expands array starting at B1
workbook.CalculateFormula();   // forces recalculation of the formula
```

### วิธีการทำงานของเครื่องมือคำนวณ

* คุณสมบัติ `Formula` เก็บนิพจน์ไว้เหมือนที่คุณพิมพ์ใน Excel  
* `CalculateFormula()` เริ่มการคำนวณใหม่ทั้งหมดของเวิร์กบุ๊ก, เคารพการพึ่งพาระหว่างเซลล์  
* ฟังก์ชัน `EXPAND` (ใช้ได้ใน Excel 365) คืนค่าช่วงที่ขยายออกมาจากเซลล์ต้นทาง (`B1`) ตามจำนวนแถว (`5`) และคอลัมน์ (`3`) ที่ระบุ  

> **เคล็ดลับ:** หากคุณต้องการคำนวณเฉพาะส่วนย่อยของเวิร์กบุ๊ก, ใช้ `Worksheet.CalculateFormula()` เพื่อจำกัดขอบเขตและเพิ่มประสิทธิภาพ  

## บันทึกเวิร์กบุ๊กพร้อมการเปลี่ยนแปลงทั้งหมด

สุดท้าย, เขียนเวิร์กบุ๊กที่แก้ไขแล้วกลับไปยังดิสก์. คุณสามารถบันทึกในรูปแบบที่รองรับใดก็ได้ (`.xlsx`, `.xls`, `.csv`, ฯลฯ) โดยเปลี่ยนนามสกุลไฟล์

```csharp
// Step 6: Save the workbook with all changes applied
workbook.Save("YOUR_DIRECTORY/result.xlsx");
```

### สิ่งที่ต้องตรวจสอบ

* เปิด `result.xlsx` ใน Excel เพื่อตรวจสอบการคัดลอก Pivot Table, ผลลัพธ์ของสูตร `EXPAND`, และสตริงที่ส่งออกแบบกำหนดเองใด ๆ  
* เปิด `output.pptx` ใน PowerPoint; คุณควรเห็นสไลด์ที่สะท้อนเลย์เอาต์ของ Excel, และแผนภูมิ/กล่องข้อความทั้งหมดควรสามารถแก้ไขได้  

## คำถามทั่วไปและการแก้ไขปัญหา

| Question | Answer |
|----------|--------|
| **ฉันต้องการไลเซนส์เพื่อใช้ Aspose.Cells หรือไม่?** | ใช่. รุ่นทดลองใช้ได้สำหรับการประเมิน, แต่ไลเซนส์เต็มจะลบลายน้ำการประเมินและเปิดใช้งานฟีเจอร์ `CopyPivotTable` |
| **ถ้าไฟล์ PPTX ที่ส่งออกแสดงรูปร่างเป็นสีขาวจะทำอย่างไร?** | ตรวจสอบว่าวัตถุการวาดของเวิร์กบุ๊กไม่ได้ถูกซ่อน (`Visible = true`) และลิงก์รูปภาพภายนอกทั้งหมดได้ถูกฝังไว้ก่อนการส่งออก |
| **ฉันสามารถส่งออกหลายเวิร์กชีตเป็นสไลด์ PPTX แยกกันได้หรือไม่?** | ใช้ `WorkbookDesigner.ExportToPptx` ในลูป, ระบุ `ExportOptions` ที่แตกต่างกันสำหรับแต่ละเวิร์กชีต, หรือรวมเป็นงานนำเสนอเดียวโดยเพิ่มสไลด์ด้วยตนเองผ่าน Aspose.Slides |
| **`CalculateFormula` ปลอดภัยต่อการทำงานหลายเธรดหรือไม่?** | ไม่. ทำการคำนวณบนเธรดเดียวหรือทำสำเนาเวิร์กบุ๊กต่อเธรดเพื่อหลีกเลี่ยงเงื่อนไขการแข่งขัน |

## สรุป

ตอนนี้คุณมี **โซลูชันครบวงจรสำหรับการส่งออก Excel ไปยัง PowerPoint** ด้วย Aspose.Cells, และคุณเข้าใจวิธี **คำนวณสูตร Excel ในโค้ด**—รวมถึงฟังก์ชัน `EXPAND` สมัยใหม่. บทเรียนนี้ครอบคลุมการโหลดเวิร์กบุ๊ก, การคัดลอก Pivot Table, การส่งออกเป็น PowerPoint ที่แก้ไขได้, การส่งออกสตริงแบบกำหนดเอง, การคำนวณสูตร, และการบันทึกขั้นสุดท้าย

จากนี้คุณสามารถ:

* ขยายการส่งออกเพื่อรวมหลายสไลด์ต่อเวิร์กชีต (คีย์เวิร์ดรอง: *calculate Excel formulas in code* สามารถใช้ซ้ำเมื่อติดตั้งข้อมูลแผนภูมิ)  
* รวม Aspose.Slides เพื่อเพิ่มแอนิเมชันหรือเลย์เอาต์สไลด์หลัก  
* แทนที่ delegate `CustomExport` แบบง่ายด้วยการจัดรูปแบบที่รับรู้ตามภาษาท้องถิ่นสำหรับโครงการระดับนานาชาติ  

อย่าลังเลที่จะทดลองกับช่วงต่าง ๆ, สำรวจฟังก์ชัน Office‑365 อื่น ๆ (เช่น `FILTER`, `SORT`), และรวมเวิร์กโฟลว์นี้กับการส่งอีเมลอัตโนมัติเพื่อสร้างสายงานรายงานที่ทำงานโดยอัตโนมัติเต็มรูปแบบ

---

## คุณควรเรียนรู้อะไรต่อไป?

บทเรียนต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดซึ่งต่อยอดจากเทคนิคที่แสดงในคู่มือนี้. แต่ละแหล่งข้อมูลมีตัวอย่างโค้ดทำงานครบถ้วนพร้อมคำอธิบายทีละขั้นตอนเพื่อช่วยคุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการนำไปใช้ทางเลือกในโครงการของคุณ

- [อัตโนมัติการส่งออกข้อมูล Excel ด้วย Aspose.Cells สำหรับ .NET: คู่มือขั้นตอนที่ละเอียด](/cells/english/net/automation-batch-processing/automate-excel-data-export-aspose-cells-net/)
- [วิธีส่งออกแผนภูมิ Excel ไปยัง PDF ด้วย Aspose.Cells สำหรับ .NET: คู่มือขั้นตอนที่ละเอียด](/cells/english/net/workbook-operations/export-excel-charts-pdf-aspose-cells-net/)
- [ส่งออกเซลล์ Excel เป็นภาพด้วย Aspose.Cells .NET: คู่มือขั้นตอนที่ละเอียด](/cells/english/net/import-export/export-excel-cells-to-image-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}