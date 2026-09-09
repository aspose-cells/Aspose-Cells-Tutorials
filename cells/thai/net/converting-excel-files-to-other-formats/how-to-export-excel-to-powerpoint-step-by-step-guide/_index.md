---
category: general
date: 2026-02-21
description: เรียนรู้วิธีส่งออก Excel ไปยัง PowerPoint พร้อมแผนภูมิที่แก้ไขได้ แปลง
  Excel เป็น PowerPoint และสร้าง PowerPoint จาก Excel เพียงไม่กี่บรรทัดของ C#
draft: false
keywords:
- how to export excel
- convert excel to powerpoint
- create powerpoint from excel
- save excel as powerpoint
- how to export charts
language: th
og_description: วิธีส่งออก Excel ไปยัง PowerPoint พร้อมแผนภูมิที่แก้ไขได้ ปฏิบัติตามคู่มือนี้เพื่อแปลง
  Excel เป็น PowerPoint สร้าง PowerPoint จาก Excel และบันทึก Excel เป็น PowerPoint
  อย่างง่ายดาย
og_title: วิธีส่งออก Excel ไปยัง PowerPoint – คู่มือเต็ม
tags:
- C#
- Aspose.Cells
- PowerPoint
title: วิธีส่งออก Excel ไปยัง PowerPoint – คู่มือขั้นตอนโดยละเอียด
url: /th/net/converting-excel-files-to-other-formats/how-to-export-excel-to-powerpoint-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีส่งออก Excel ไปยัง PowerPoint – บทเรียนเต็ม

เคยสงสัยไหมว่า **how to export Excel** ไปยัง PowerPoint โดยไม่ทำให้แผนภูมิที่สวยงามของคุณกลายเป็นภาพคงที่? คุณไม่ได้เป็นคนเดียว ในหลาย ๆ กระบวนการรายงาน ความต้องการ **convert Excel to PowerPoint** ปรากฏทุกวัน และเทคนิคคัดลอก‑วางทั่วไปมักทำให้รูปแบบเสียหายหรือทำให้ข้อมูลแผนภูมิติดขัด  

ในคู่มือนี้เราจะพาคุณผ่านโซลูชันแบบโปรแกรมที่ **creates PowerPoint from Excel** พร้อมให้แผนภูมิแก้ไขได้เต็มที่ เมื่อเสร็จคุณจะสามารถ **save Excel as PowerPoint** ด้วยการเรียกเมธอดเดียวและเข้าใจเหตุผลที่แต่ละบรรทัดสำคัญ

## สิ่งที่คุณจะได้เรียนรู้

- โค้ด C# ที่แม่นยำสำหรับ **export Excel** ไปยังไฟล์ PPTX.
- วิธีทำให้แผนภูมิสามารถแก้ไขได้โดยใช้ `PresentationExportOptions`.
- เมื่อควรเลือกวิธีนี้แทนการส่งออกด้วยตนเองหรือใช้ตัวแปลงของบุคคลที่สาม.
- ข้อกำหนดเบื้องต้น, จุดบกพร่องทั่วไป, และเคล็ดลับพิเศษเพื่อทำให้กระบวนการแน่นหนา.

> **Pro tip:** หากคุณกำลังใช้ Aspose.Cells อยู่แล้วในส่วนอื่นของโปรเจกต์ วิธีนี้จะเพิ่มภาระการทำงานเกือบไม่มีเลย.

### ข้อกำหนดเบื้องต้น

| Requirement | Why it matters |
|-------------|----------------|
| .NET 6.0 or later | รันไทม์สมัยใหม่, ประสิทธิภาพที่ดีกว่า, และการสนับสนุน Aspose.Cells อย่างเต็มรูปแบบ. |
| Aspose.Cells for .NET (NuGet package) | ให้ API `Workbook`, `PresentationExportOptions`, และ `SaveToPptx` ที่เราพึ่งพา. |
| A basic Excel file with at least one chart | ไฟล์ Excel พื้นฐานที่มีอย่างน้อยหนึ่งแผนภูมิ |
| Visual Studio 2022 (or any IDE you like) | ทำให้การดีบักและการจัดการแพคเกจง่ายขึ้น. |

หากคุณมีสิ่งเหล่านี้พร้อมแล้ว, มาเริ่มกันเลย.

## วิธีส่งออก Excel ไปยัง PowerPoint พร้อมแผนภูมิที่แก้ไขได้

ด้านล่างเป็นตัวอย่าง **complete, runnable** ที่แสดงขั้นตอนทั้งหมด แต่ละบล็อกจะอธิบายหลังจากนั้น เพื่อให้คุณคัดลอก‑วางและปรับใช้ได้โดยไม่ต้องค้นหาในเอกสาร

### ขั้นตอน 1: ติดตั้ง Aspose.Cells

เปิดเทอร์มินัลในโฟลเดอร์โปรเจกต์ของคุณและรัน:

```bash
dotnet add package Aspose.Cells
```

### ขั้นตอน 2: โหลดเวิร์กบุ๊ก Excel

```csharp
using Aspose.Cells;
using Aspose.Cells.Export;

// Step 2: Load the Excel workbook
Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");
```

> **Why this matters:** `Workbook` เป็นจุดเริ่มต้นสำหรับการจัดการ Excel ใด ๆ การโหลดไฟล์ก่อนทำให้เรามั่นใจว่าการส่งออกต่อไปทำงานบนข้อมูลและรูปแบบที่คุณเห็นใน Excel อย่างแม่นยำ.

### ขั้นตอน 3: กำหนดค่า PPTX Export Options เพื่อให้แผนภูมิแก้ไขได้

```csharp
// Step 3: Configure PPTX export options to keep charts editable
PresentationExportOptions exportOptions = new PresentationExportOptions
{
    ExportEditableCharts = true   // This flag ensures charts stay editable in PowerPoint
};
```

หากคุณละ `ExportEditableCharts`, Aspose จะทำให้แผนภูมิเป็นภาพราสเตอร์ ซึ่งทำให้เสียวัตถุประสงค์ของ **how to export charts** ในรูปแบบที่แก้ไขได้.

### ขั้นตอน 4: บันทึก Worksheet แรกเป็นไฟล์ PPTX

```csharp
// Step 4: Export the first worksheet as a PPTX file using the options
workbook.Worksheets[0].PageSetup.SaveToPptx(@"YOUR_DIRECTORY\Editable.pptx", exportOptions);
```

เมธอด `SaveToPptx` จะเขียนไฟล์ PowerPoint ที่แต่ละเซลล์ Excel กลายเป็นกล่องข้อความ และแต่ละแผนภูมิกลายเป็นวัตถุแผนภูมิ PowerPoint แท้ คุณสามารถเปิด `Editable.pptx` ใน PowerPoint แล้วดับเบิล‑คลิกแผนภูมิใดก็ได้เพื่อแก้ไขซีรีส์, แกน, หรือสไตล์ได้

### ขั้นตอน 5: ตรวจสอบผลลัพธ์

1. เปิด `Editable.pptx` ใน Microsoft PowerPoint.  
2. ค้นหาสไลด์ที่สอดคล้องกับ Worksheet ที่ส่งออก.  
3. คลิกที่แผนภูมิ → เลือก **Edit Data** → คุณควรเห็นตารางข้อมูลสไตล์ Excel.

หากแผนภูมิยังคงเป็นภาพ, ตรวจสอบให้แน่ใจว่า `ExportEditableCharts` ตั้งค่าเป็น `true` และ Worksheet ต้นทางมีวัตถุแผนภูมิจริง ๆ

![แผนภาพแสดงขั้นตอนจาก Excel ไปยัง PowerPoint – วิธีส่งออก excel](/images/excel-to-pptx-flow.png "ตัวอย่างวิธีส่งออก excel")

## การแปลง Excel ไปยัง PowerPoint – ปัญหาที่พบบ่อยและเคล็ดลับ

แม้จะมีโค้ดที่ถูกต้องแล้ว นักพัฒนาก็อาจเจออุปสรรคบ้าง นี่คือปัญหาที่พบบ่อยที่สุดและวิธีหลีกเลี่ยง

| Issue | Explanation | Fix |
|-------|-------------|-----|
| **No charts appear** | Workbook อาจไม่มีวัตถุแผนภูมิใด ๆ หรือแผนภูมิเช่นนั้นถูกซ่อน. | ตรวจสอบให้แน่ใจว่าแผนภูมิมองเห็นได้และไม่ได้อยู่บนแผ่นที่ซ่อน. |
| **Charts become images** | `ExportEditableCharts` ถูกปล่อยไว้ที่ค่าเริ่มต้น `false`. | ตั้งค่า `ExportEditableCharts = true` อย่างชัดเจนตามที่แสดงในขั้นตอน 3. |
| **File path errors** | ใช้เส้นทางแบบ relative โดยไม่มี `Path.Combine` ที่เหมาะสม. | แนะนำให้ใช้ `Path.Combine(Environment.CurrentDirectory, "input.xlsx")`. |
| **Large files cause OutOfMemory** | การส่งออกเวิร์กบุ๊กที่มีแถวหลายพันและแผนภูมิมากอาจใช้หน่วยความจำสูง. | ใช้ `WorkbookSettings.MemorySetting = MemorySetting.MemoryPreference;` ก่อนโหลด. |
| **Version mismatch** | ใช้เวอร์ชัน Aspose.Cells เก่าที่ไม่มี `PresentationExportOptions`. | อัปเกรดเป็นแพคเกจ NuGet ล่าสุด. |

### โบนัส: ส่งออกหลาย Worksheet

หากคุณต้องการ **create PowerPoint from Excel** สำหรับหลายแผ่น, ให้วนลูปผ่านคอลเลกชัน:

```csharp
for (int i = 0; i < workbook.Worksheets.Count; i++)
{
    string pptxPath = $@"YOUR_DIRECTORY\Sheet{i + 1}.pptx";
    workbook.Worksheets[i].PageSetup.SaveToPptx(pptxPath, exportOptions);
}
```

แต่ละ Worksheet จะกลายเป็นไฟล์ PPTX ของตนเอง โดยคงความสามารถแก้ไขแผนภูมิไว้ทั้งหมด

## บันทึก Excel เป็น PowerPoint – สถานการณ์ขั้นสูง

### ฝังรูปภาพพร้อมกับแผนภูมิ

บางครั้งรายงานต้องผสมแผนภูมิและโลโก้บริษัท Aspose จะจัดการรูปภาพเหมือนกับรูปร่างอื่น ๆ ดังนั้นมันจะปรากฏใน PPTX โดยอัตโนมัติ หากต้องการควบคุมลำดับ, ปรับค่า Z‑index ผ่านคุณสมบัติ `Shape` ก่อนส่งออก

### เค้าโครงสไลด์แบบกำหนดเอง

PowerPoint รองรับมาสเตอร์สไลด์ แม้ว่า `SaveToPptx` จะสร้างเค้าโครงเริ่มต้น คุณก็สามารถนำมาสเตอร์เทมเพลตไปใช้ต่อได้:

```csharp
using Aspose.Slides;

// Load the generated PPTX
Presentation pres = new Presentation(@"YOUR_DIRECTORY\Editable.pptx");

// Apply a master template (must be a .pptx file)
pres.Masters.AddFromFile(@"TEMPLATES\CorporateTemplate.pptx");

// Save the final version
pres.Save(@"YOUR_DIRECTORY\FinalPresentation.pptx", SaveFormat.Pptx);
```

ขั้นตอนนี้ทำให้คุณ **convert Excel to PowerPoint** พร้อมคงแบรนด์ขององค์กรไว้

### การจัดการประเภทแผนภูมิต่าง ๆ

แผนภูมิประเภททั่วไป (Bar, Column, Line, Pie) ส่งออกได้อย่างสมบูรณ์ อย่างไรก็ตาม **how to export charts** เช่น Radar หรือ Stock อาจต้องปรับสไตล์หลังจากนำเข้า ในกรณีนั้นคุณสามารถ:

1. ส่งออกตามที่อธิบายไว้.  
2. เปิดไฟล์ PPTX ด้วย Aspose.Slides.  
3. ปรับคุณสมบัติแผนภูมิ (เช่น `Chart.Type = ChartType.Radar`).

## สรุป & ขั้นตอนต่อไป

เราได้ครอบคลุมทุกอย่างที่คุณต้องรู้เกี่ยวกับ **how to export Excel** ไปยังชุดสไลด์ PowerPoint พร้อมคงความสามารถแก้ไขแผนภูมิไว้ ขั้นตอนหลัก—การติดตั้ง Aspose.Cells, การโหลดเวิร์กบุ๊ก, การกำหนดค่า `PresentationExportOptions`, และการเรียก `SaveToPptx`—ใช้เพียงไม่กี่บรรทัดของ C# แต่แทนที่กระบวนการทำมือทั้งหมด

### สิ่งที่ควรลองต่อไป

- **Convert Excel to PowerPoint** สำหรับเวิร์กบุ๊กทั้งหมดโดยใช้ตัวอย่างลูป.  
- ทดลอง **create PowerPoint from Excel** สำหรับแดชบอร์ดแบบไดนามิกที่อัปเดตทุกคืน.  
- รวมการส่งออกนี้กับ **Aspose.Slides** เพื่อใช้แม่แบบสไลด์แบบกำหนดเองและอัตโนมัติการสร้างแบรนด์.  
- สำรวจเมธอด `ExportAllSheetsAsPptx` หากต้องการ PPTX เดียวที่มีหลาย Worksheet.

ปรับเปลี่ยนเส้นทาง, ปรับตัวเลือกการส่งออก, หรือฝังตรรกะนี้เข้าไปในบริการรายงานขนาดใหญ่ได้ตามต้องการ ขีดจำกัดเดียวคือความคิดสร้างสรรค์ของคุณกับการแสดงผลข้อมูล

*Happy coding! หากคุณเจออุปสรรคใด ๆ ขณะพยายาม **save Excel as PowerPoint**, ฝากคอมเมนต์ด้านล่างหรือดูเอกสาร Aspose.Cells สำหรับอัปเดตล่าสุด.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}