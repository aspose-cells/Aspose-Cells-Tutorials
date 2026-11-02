---
category: general
date: 2026-03-22
description: เรียนรู้วิธีส่งออก Excel ไปยัง PowerPoint ตั้งค่าพื้นที่พิมพ์ใน Excel
  และบันทึก Excel เป็นไฟล์ PPTX พร้อมแผนภูมิที่แก้ไขได้และวัตถุ OLE เพียงไม่กี่ขั้นตอน.
draft: false
keywords:
- export excel to powerpoint
- set print area excel
- save excel as pptx
- editable charts PowerPoint
- OLE objects export
language: th
og_description: ส่งออก Excel ไปยัง PowerPoint อย่างรวดเร็ว บทเรียนนี้แสดงวิธีตั้งค่าพื้นที่พิมพ์ใน
  Excel และบันทึก Excel เป็นไฟล์ PPTX พร้อมแผนภูมิที่แก้ไขได้และวัตถุ OLE.
og_title: ส่งออก Excel ไปยัง PowerPoint – คู่มือ C# ฉบับสมบูรณ์
tags:
- Aspose.Cells
- C#
- Office Automation
title: ส่งออก Excel ไปยัง PowerPoint – คู่มือ C# ฉบับสมบูรณ์
url: /th/net/converting-excel-files-to-other-formats/export-excel-to-powerpoint-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ส่งออก Excel ไปยัง PowerPoint – คู่มือ C# ฉบับสมบูรณ์

ต้องการ **export Excel to PowerPoint** หรือไม่? คุณมาถูกที่แล้ว ไม่ว่าคุณจะกำลังสร้างชุดสไลด์การขายประจำสัปดาห์หรือทำระบบอัตโนมัติสำหรับการรายงาน การแปลงแผ่นงาน Excel ให้เป็นชุดสไลด์ PowerPoint สามารถประหยัดเวลาการคัดลอก‑และ‑วางหลายชั่วโมงได้  

ในบทแนะนำนี้ เราจะพาคุณผ่านตัวอย่างเชิงปฏิบัติที่ไม่เพียงแต่ **export excel to powerpoint** แต่ยังแสดงวิธี **set print area Excel** และ **save excel as pptx** เพื่อให้สไลด์ที่ได้คงแผนภูมิและวัตถุ OLE ที่แก้ไขได้อย่างเต็มที่ เมื่อเสร็จสิ้นคุณจะได้โปรแกรม C# ที่พร้อมรันซึ่งสร้างไฟล์ `.pptx` ที่ดูเป็นมืออาชีพโดยไม่ต้องปรับแต่งด้วยมือเลย  

## สิ่งที่คุณต้องการ

- **.NET 6+** (runtime .NET ล่าสุดใดก็ได้; โค้ดใช้ไวยากรณ์ C# 10)
- **Aspose.Cells for .NET** – ไลบรารีที่ทำหน้าที่ส่งออก คุณสามารถดาวน์โหลดได้จาก NuGet (`Install-Package Aspose.Cells`).
- ไฟล์ Excel workbook ที่มีอย่างน้อยหนึ่งแผนภูมิและ/หรือวัตถุ OLE (ไฟล์ตัวอย่าง `ChartAndOle.xlsx` ถูกใช้ในโค้ด).
- IDE ที่คุณชื่นชอบ (Visual Studio, Rider หรือ VS Code – ตามที่คุณต้องการ).

แค่นั้นเอง ไม่ต้องใช้ COM interop ไม่ต้องติดตั้ง Office  

> **ทำไมต้องใช้ไลบรารี?**  
> Office Interop ที่มาพร้อมนั้นเปราะบาง ต้องมี Office บนเซิร์ฟเวอร์ และมักสร้างภาพแบบราสเตอร์เมื่อคุณต้องการรูปแบบเวกเตอร์ที่แก้ไขได้ Aspose.Cells จัดการงานหนักและทำให้ทุกอย่างแก้ไขได้ใน PowerPoint.  

---

## ขั้นตอนที่ 1: โหลด Excel Workbook  

ก่อนอื่นเรานำไฟล์ต้นทางเข้ามาในหน่วยความจำ คลาส `Workbook` ทำหน้าที่เป็นตัวแทนของไฟล์ Excel ทั้งหมด ให้เราสามารถเข้าถึง worksheets, แผนภูมิ และวัตถุ OLE ได้  

```csharp
using Aspose.Cells;

try
{
    // Load the Excel file that contains the chart and OLE object.
    // Adjust the path to point to your own workbook.
    Workbook workbook = new Workbook(@"C:\MyProjects\ChartAndOle.xlsx");
}
catch (Exception ex)
{
    Console.WriteLine($"Failed to load workbook: {ex.Message}");
    return;
}
```

**ทำไมเรื่องนี้สำคัญ:** การโหลด workbook เป็นพื้นฐาน หากเส้นทางผิดหรือไฟล์เสียหาย ส่วนที่เหลือของ pipeline จะไม่ทำงาน บล็อก `try…catch` จะให้ข้อผิดพลาดที่เป็นมิตรแทนการพัง.  

---

## ขั้นตอนที่ 2: ตั้งค่า Print Area ใน Excel  

ก่อนทำการส่งออก คุณมักต้องการจำกัดผลลัพธ์ให้อยู่ในช่วงเฉพาะ นี่คือจุดที่ **set print area excel** เข้ามา ทำการกำหนด print area จะบอก Aspose.Cells ว่าเซลล์ใด (และวัตถุที่เกี่ยวข้อง) ควรปรากฏบนสไลด์.  

```csharp
// Assuming we want to export only the range A1:H30 on the first worksheet.
Worksheet sheet = workbook.Worksheets[0];
sheet.PageSetup.PrintArea = "A1:H30";
```

> **เคล็ดลับ:** หากคุณมีหลาย worksheets ให้ทำการกำหนด `PrintArea` ซ้ำสำหรับแต่ละแผ่นที่คุณต้องการส่งออก การไม่ตั้งค่า print area จะทำให้ส่งออกทั้งแผ่น ซึ่งอาจทำให้ไฟล์ PowerPoint ใหญ่ขึ้น.  

---

## ขั้นตอนที่ 3: กำหนดค่า Export Options – รักษาแผนภูมิและ OLE ให้แก้ไขได้  

Aspose.Cells มีอ็อบเจกต์ `ImageOrPrintOptions` ที่หลากหลาย โดยการสลับ `ExportChartObjects` และ `ExportOleObjects` เราจะคงลักษณะเวกเตอร์ของแผนภูมิและความสามารถแก้ไขแบบสดของวัตถุ OLE (เช่น เอกสาร Word หรือ PDF ที่ฝังอยู่).  

```csharp
ImageOrPrintOptions pptExportOptions = new ImageOrPrintOptions
{
    SaveFormat = SaveFormat.Pptx,   // We want a PPTX, not a PNG or PDF.
    ExportChartObjects = true,      // Charts stay editable in PowerPoint.
    ExportOleObjects = true         // OLE objects remain live (you can double‑click to edit).
};
```

**อะไรเกิดขึ้นเบื้องหลัง?**  
เมื่อ `ExportChartObjects` เป็น `true` Aspose จะเปลี่ยนแผนภูมิเป็นรูปแบบแผนภูมิ PowerPoint ดั้งเดิม คง series, axes, และการจัดรูปแบบไว้ เมื่อเปิดใช้งาน `ExportOleObjects` วัตถุที่ฝังจะถูกแทรกเป็นกรอบ OLE ดังนั้นการดับเบิลคลิกใน PowerPoint จะเปิดแอปพลิเคชันต้นฉบับ (Word, Excel ฯลฯ) เพื่อแก้ไข.  

---

## ขั้นตอนที่ 4: บันทึก Worksheet เป็นไฟล์ PowerPoint ที่แก้ไขได้  

ตอนนี้เราจะเชื่อมทุกอย่างเข้าด้วยกัน เมธอด `Save` จะเขียนไฟล์ `.pptx` โดยใช้ตัวเลือกที่เราตั้งค่า ผลลัพธ์คือชุดสไลด์ที่แต่ละ worksheet กลายเป็นสไลด์ (หรือหลายสไลด์หาก print area ครอบหลายหน้า).  

```csharp
// Save the first worksheet as an editable PowerPoint presentation.
workbook.Save(@"C:\MyProjects\EditableChartOle.pptx", pptExportOptions);
Console.WriteLine("Export completed! Check EditableChartOle.pptx.");
```

### ผลลัพธ์ที่คาดหวัง

- **ตำแหน่งไฟล์:** `C:\MyProjects\EditableChartOle.pptx`
- **เนื้อหา:**  
  - สไลด์ที่แสดงช่วง `A1:H30` ตรงตามที่แสดงใน Excel.  
  - แผนภูมิทั้งหมดเป็นวัตถุแผนภูมิ PowerPoint—คลิกแถบเพื่อแก้ไขข้อมูล.  
  - วัตถุ OLE (เช่น เอกสาร Word ที่ฝัง) สามารถเปิดและแก้ไขโดยตรงจากสไลด์.  

หากคุณเปิดไฟล์ PPTX ใน PowerPoint คุณจะเห็นสไลด์ที่สะอาดตาพร้อมส่วนประกอบที่แก้ไขได้เต็มที่—ไม่มีภาพสกรีนช็อตแบบราสเตอร์.  

---

## กรณีขอบและรูปแบบต่าง ๆ  

### หลาย Worksheet → หลายสไลด์  
หากคุณต้องการให้แต่ละ worksheet กลายเป็นสไลด์ของตนเอง เพียงวนลูปผ่าน `workbook.Worksheets` และเรียก `Save` ด้วย `SheetToImageOptions` ที่ระบุดัชนีแผ่นเฉพาะ Aspose จะสร้างสไลด์ใหม่โดยอัตโนมัติสำหรับแต่ละรอบ.  

```csharp
for (int i = 0; i < workbook.Worksheets.Count; i++)
{
    ImageOrPrintOptions opts = new ImageOrPrintOptions
    {
        SaveFormat = SaveFormat.Pptx,
        ExportChartObjects = true,
        ExportOleObjects = true,
        OnePagePerSheet = true   // Ensures each sheet starts on a new slide.
    };
    workbook.Save($"Sheet{i + 1}.pptx", opts);
}
```

### ช่วงขนาดใหญ่และประสิทธิภาพ  
การส่งออก print area ขนาดใหญ่ (เช่น `A1:Z1000`) อาจทำให้การใช้หน่วยความจำเพิ่มขึ้น เพื่อบรรเทาให้พิจารณา:
- แบ่งช่วงเป็นส่วนย่อย ๆ แล้วส่งออกเป็นสไลด์แยกกัน.  
- ใช้ `WorkbookSettings` เพื่อเพิ่มค่า `MemorySetting` หากเจอ `OutOfMemoryException`.  

### ข้อกังวลเรื่องความเข้ากันได้  
PPTX ที่สร้างขึ้นทำงานได้กับ PowerPoint 2016 ขึ้นไป เวอร์ชันเก่าอาจเปิดไฟล์ได้แต่บางคุณลักษณะแผนภูมิขั้นสูงอาจหายไป ควรทดสอบบนเวอร์ชัน Office ที่เป้าหมายหากคุณจะแจกจ่ายชุดสไลด์อย่างกว้างขวาง.  

---

## ตัวอย่างทำงานเต็มรูปแบบ (พร้อมคัดลอก‑วาง)

```csharp
// ---------------------------------------------------------------
// Export Excel to PowerPoint – Complete C# Example
// ---------------------------------------------------------------

using System;
using Aspose.Cells;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the workbook.
            string excelPath = @"C:\MyProjects\ChartAndOle.xlsx";
            Workbook workbook;
            try
            {
                workbook = new Workbook(excelPath);
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Error loading Excel file: {ex.Message}");
                return;
            }

            // 2️⃣ Set the print area (set print area excel).
            Worksheet sheet = workbook.Worksheets[0];
            sheet.PageSetup.PrintArea = "A1:H30";

            // 3️⃣ Configure export options – keep charts & OLE objects editable.
            ImageOrPrintOptions pptExportOptions = new ImageOrPrintOptions
            {
                SaveFormat = SaveFormat.Pptx,
                ExportChartObjects = true,
                ExportOleObjects = true
            };

            // 4️⃣ Save as PPTX (save excel as pptx).
            string pptxPath = @"C:\MyProjects\EditableChartOle.pptx";
            try
            {
                workbook.Save(pptxPath, pptExportOptions);
                Console.WriteLine($"Success! PPTX created at: {pptxPath}");
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Failed to save PPTX: {ex.Message}");
            }
        }
    }
}
```

> **เคล็ดลับ:** แทนที่เส้นทางที่กำหนดแบบคงที่ด้วยค่าการกำหนดค่า หรืออาร์กิวเมนต์บรรทัดคำสั่ง เพื่อให้เครื่องมือยืดหยุ่นมากขึ้น.  

---

## คำถามที่พบบ่อย  

**Q: ฉันสามารถส่งออกเฉพาะแผนภูมิโดยไม่รวมเซลล์รอบข้างได้หรือไม่?**  
A: ได้ ใช้ `ExportChartObjects` เพียงอย่างเดียวและตั้งค่า print area ให้ครอบแผนภูมิ แผนภูมิจะปรากฏตรงกลางสไลด์.  

**Q: ถ้า workbook ของฉันมีแมโครล่ะ?**  
A: Aspose.Cells จะละเลยแมโคร VBA ระหว่างการส่งออก หากคุณต้องการฟังก์ชันแมโครใน PowerPoint คุณต้องสร้างใหม่โดยใช้ PowerPoint VBA หรือแอด‑อิน.  

**Q: ทำงานบน Linux/macOS ได้หรือไม่?**  
A: ได้แน่นอน Aspose.Cells เป็นไลบรารี .NET แท้ ๆ; ตราบใดที่คุณมี .NET runtime โค้ดก็ทำงานข้ามแพลตฟอร์ม.  

---

## สรุป  

คุณเพิ่งเรียนรู้วิธี **export Excel to PowerPoint** พร้อมกับการ **set print area excel** อย่างแม่นยำและ **save excel as pptx** ที่มีแผนภูมิและวัตถุ OLE ที่แก้ไขได้เต็มที่ ขั้นตอนสำคัญคือการโหลด workbook, กำหนด print area, ตั้งค่า `ImageOrPrintOptions` และสุดท้ายบันทึกเป็น PPTX.  

จากนี้คุณสามารถสำรวจต่อได้:
- ส่งออกหลาย worksheet ไปยังชุดสไลด์เดียว.  
- เพิ่มหัวข้อสไลด์หรือโน้ตแบบกำหนดเองโดยโปรแกรม.  
- แปลง PPTX เป็น PDF เพื่อแจกจ่าย (ใช้ `SaveFormat.Pdf`).  

ลองรันโค้ด ปรับ print area แล้วดูข้อมูล Excel ของคุณปรากฏใน PowerPoint อย่างมหัศจรรย์—ไม่ต้องคัดลอก‑วางด้วยมือ หากพบปัญหา ให้ตรวจสอบเอกสาร Aspose.Cells หรือแสดงความคิดเห็นด้านล่าง ขอให้เขียนโค้ดสนุก!  

![Diagram showing export excel to powerpoint workflow](/images/export-excel-to-powerpoint.png "export excel to powerpoint workflow")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}