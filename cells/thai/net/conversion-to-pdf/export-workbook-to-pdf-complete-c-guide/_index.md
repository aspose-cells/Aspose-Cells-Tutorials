---
category: general
date: 2026-02-26
description: ส่งออกเวิร์กบุ๊กเป็น PDF พร้อมฝังฟอนต์และส่งออกแผนภูมิเป็น PowerPoint
  ด้วย C#. เรียนรู้วิธีคัดลอกแผ่นงาน Pivot Table และบันทึกเวิร์กบุ๊กเป็น PPTX.
draft: false
keywords:
- export workbook to pdf
- export charts to powerpoint
- copy pivot table worksheet
- embed fonts pdf export
- save workbook as pptx
language: th
og_description: ส่งออกเวิร์กบุ๊กเป็น PDF พร้อมฝังฟอนต์และส่งออกแผนภูมิเป็น PowerPoint
  ด้วย C#. ปฏิบัติตามคู่มือขั้นตอนต่อขั้นตอนเพื่อคัดลอกตาราง Pivot และบันทึกเป็น PPTX.
og_title: ส่งออกเวิร์กบุ๊กเป็น PDF – คู่มือ C# ฉบับสมบูรณ์
tags:
- Aspose.Cells
- Aspose.Slides
- C#
- Reporting
title: ส่งออกเวิร์กบุ๊กเป็น PDF – คู่มือ C# ฉบับสมบูรณ์
url: /th/net/conversion-to-pdf/export-workbook-to-pdf-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ส่งออก Workbook เป็น PDF – คู่มือ C# ฉบับสมบูรณ์

การส่งออก workbook เป็น PDF เป็นความต้องการทั่วไปเมื่อคุณต้องการแชร์รายงานกับผู้มีส่วนได้ส่วนเสียที่อาจไม่มี Excel ติดตั้งอยู่ ในบทเรียนนี้เราจะสาธิตวิธี **export charts to PowerPoint**, คัดลอก **pivot table worksheet**, และฝังฟอนต์เพื่อให้ PDF มีลักษณะเหมือนกับการออกแบบบนหน้าจอของคุณอย่างแม่นยำ  

เคยสงสัยไหมว่าทำไมบาง PDF ถึงสูญเสียการจัดวางเดิมหรือทำไมสไลด์ PowerPoint ถึงขาดรูปร่างบางอย่าง? คำตอบมักอยู่ที่ตัวเลือกที่ขาดหายระหว่างกระบวนการส่งออก เมื่อจบบทเรียนนี้คุณจะมีเมธอด C# เดียวที่ใช้ซ้ำได้ซึ่งจัดการกับปัญหาเหล่านั้นทั้งหมด—ไม่ต้องคัดลอก‑วางด้วยมือหรือปรับตั้งค่าการส่งออกอีกต่อไป  

## สิ่งที่คุณจะได้เรียนรู้

- วิธีสร้าง workbook, เพิ่ม Smart Marker expressions, และประมวลผลมัน  
- วิธี **copy a pivot table worksheet** โดยไม่ทำให้แหล่งข้อมูลเสียหาย  
- วิธี **export charts, shapes, and text boxes** ไปยังการนำเสนอ PowerPoint พร้อมคงความสามารถในการแก้ไข  
- วิธี **embed standard fonts** ระหว่างการส่งออก PDF เพื่อให้การแสดงผลสม่ำเสมอบนเครื่องใดก็ได้  
- วิธี **save the workbook as PPTX** โดยใช้วิธี `save workbook as pptx`  

ทั้งหมดนี้ทำงานร่วมกับไลบรารี Aspose.Cells และ Aspose.Slides .NET รุ่นล่าสุด (เวอร์ชัน 23.11 ณ เวลาที่เขียน) ไม่ต้องใช้เครื่องมือภายนอก ไม่ต้องสคริปต์หลังการประมวลผล—เพียง C# แท้ ๆ  

> **Pro tip:** หากคุณใช้ Aspose อยู่แล้วในโปรเจกต์ของคุณ คุณสามารถวางโค้ดสแนปช็อตได้เลย; หากไม่มีก็ให้เพิ่มแพคเกจ NuGet `Aspose.Cells` และ `Aspose.Slides` ก่อน  

## ข้อกำหนดเบื้องต้น

- .NET 6.0 หรือใหม่กว่า (โค้ดยังทำงานบน .NET Framework 4.7.2 ด้วย)  
- Visual Studio 2022 (หรือ IDE ใดก็ได้ที่คุณชอบ)  
- Aspose.Cells .NET และ Aspose.Slides .NET ที่ติดตั้งผ่าน NuGet  
- ความคุ้นเคยพื้นฐานกับ C# และแนวคิดของ Excel เช่น Smart Markers และ PivotTables  

---

![แผนภาพการส่งออก workbook เป็น PDF](export-workbook-to-pdf.png "เวิร์กโฟว์การส่งออก workbook เป็น PDF แสดงผลลัพธ์เป็น PDF และ PPTX")

## ส่งออก Workbook เป็น PDF – การดำเนินการทีละขั้นตอน

ด้านล่างเป็นตัวอย่างเต็มรูปแบบที่พร้อมรัน มันสร้าง workbook, แทรก Smart Marker expressions, ประมวลผล, คัดลอกช่วง pivot table, และสุดท้ายบันทึกเป็นไฟล์ PDF และ PowerPoint  

```csharp
using System;
using Aspose.Cells;
using Aspose.Slides.Export;

namespace ReportExportDemo
{
    class Program
    {
        static void Main()
        {
            // -------------------------------------------------
            // Step 1: Build the workbook and add Smart Markers
            // -------------------------------------------------
            var reportWorkbook = new Workbook();
            Worksheet dataSheet = reportWorkbook.Worksheets[0];

            // Header with a variable department name
            dataSheet.Cells["A1"].PutValue("Report for ${$dept=Department}");

            // Conditional text based on department
            dataSheet.Cells["A2"].PutValue("${if $dept == \"Sales\"}Sales Summary${else}Other Summary${/if}");

            // Table header for orders – this will be repeated for each order
            dataSheet.Cells["A5:D5"].PutValue("${Orders.Product}|${Orders.Quantity}|${Orders.Price}");

            // -------------------------------------------------
            // Step 2: Process Smart Markers and name the detail sheet
            // -------------------------------------------------
            reportWorkbook.SmartMarkerProcessor.Options.DetailSheetNewName = "Orders_${$dept}";
            reportWorkbook.SmartMarkerProcessor.Process();

            // -------------------------------------------------
            // Step 3: Copy the range that contains the pivot table
            // -------------------------------------------------
            // Assume the pivot table lives in A1:G30 on the original sheet
            Range sourceRange = dataSheet.Cells.CreateRange("A1", "G30");
            Worksheet copySheet = reportWorkbook.Worksheets.Add("Copy");
            sourceRange.Copy(copySheet.Cells["A1"]);   // Pivot table is duplicated intact

            // -------------------------------------------------
            // Step 4: Export to PowerPoint (keep charts, shapes, text boxes)
            // -------------------------------------------------
            var pptOptions = new PresentationOptions
            {
                ExportCharts = true,
                ExportShapes = true,
                ExportTextBoxes = true
            };
            string pptPath = @"C:\Temp\FinalPresentation.pptx";
            reportWorkbook.Save(pptPath, SaveFormat.Pptx, pptOptions);

            // -------------------------------------------------
            // Step 5: Export to PDF and embed standard fonts
            // -------------------------------------------------
            var pdfOptions = new PdfSaveOptions { EmbedStandardFonts = true };
            string pdfPath = @"C:\Temp\FinalReport.pdf";
            reportWorkbook.Save(pdfPath, pdfOptions);

            Console.WriteLine("Export completed:");
            Console.WriteLine($" • PDF saved to {pdfPath}");
            Console.WriteLine($" • PowerPoint saved to {pptPath}");
        }
    }
}
```

### ทำไมวิธีนี้ถึงได้ผล

1. **Smart Marker processing** ช่วยให้คุณเติมข้อมูลลงใน workbook จากแหล่งข้อมูลใดก็ได้ (JSON, DataTables ฯลฯ) โดยไม่ต้องเขียนลูป  
2. **DetailSheetNewName** สร้างแผ่นงานแยกสำหรับแต่ละแผนก ทำให้คุณได้แท็บที่เป็นระเบียบตามแผนก  
3. **Copying the range** (`sourceRange.Copy`) ทำสำเนา pivot table *รวมถึง* แคชของมัน ทำให้แผ่นงานที่คัดลอกทำงานเหมือนต้นฉบับ  
4. **PresentationOptions** พร้อม `ExportCharts`, `ExportShapes`, และ `ExportTextBoxes` บอก Aspose ให้เรนเดอร์วัตถุเหล่านั้นเป็นองค์ประกอบ PowerPoint แบบดั้งเดิม เพื่อคงความสามารถในการแก้ไข  
5. **PdfSaveOptions.EmbedStandardFonts** ทำให้ PDF มีลักษณะเหมือนกันบนเครื่องที่ไม่มีฟอนต์ต้นฉบับติดตั้ง  

ผลลัพธ์คือไฟล์สองไฟล์—`FinalReport.pdf` และ `FinalPresentation.pptx`—ซึ่งสามารถส่งอีเมล, เก็บเป็นเอกสาร, หรือเปิดดูในโปรแกรมใดก็ได้โดยไม่สูญเสียคุณภาพ  

## ส่งออกแผนภูมิไปยัง PowerPoint (บันทึก Workbook เป็น PPTX)

หากรายงานของคุณมีแผนภูมิ คุณอาจต้องการให้แผนภูมิเหล่านั้นแก้ไขได้ใน PowerPoint คลาส `PresentationOptions` คือกุญแจ นี่คือตัวอย่างสแนปช็อตที่เน้นส่วนการส่งออกแผนภูมิเท่านั้น  

```csharp
// Assuming reportWorkbook already contains charts
var pptExportOptions = new PresentationOptions
{
    ExportCharts = true,      // Convert Excel charts to PowerPoint chart objects
    ExportShapes = false,    // Skip shapes if you don’t need them
    ExportTextBoxes = true   // Keep any text boxes editable
};

string pptFile = @"C:\Temp\ChartsOnly.pptx";
reportWorkbook.Save(pptFile, SaveFormat.Pptx, pptExportOptions);
```

**What happens under the hood?** Aspose แปลงแต่ละแผนภูมิ Excel ให้เป็นแผนภูมิ PowerPoint แบบดั้งเดิม คง series, ชื่อแกน, และการจัดรูปแบบ นี่ดีกว่าการส่งออกเป็นภาพคงที่มาก เพราะผู้ชมของคุณสามารถปรับจุดข้อมูลได้ในภายหลัง  

## คัดลอก Pivot Table Worksheet โดยไม่สูญเสียข้อมูล

Pivot table มักเป็นส่วนที่ท้าทายที่สุดของการส่งออก เพราะพึ่งพาแคชที่ซ่อนอยู่ วิธี `Copy` ง่าย ๆ ทำงานได้เพราะ Aspose คัดลอกทั้งช่วงที่มองเห็น **และ** วัตถุแคชพื้นฐาน  

```csharp
// Copy the whole sheet (including pivot table) to a new workbook
Workbook clone = new Workbook();
reportWorkbook.Worksheets[0].CopyTo(clone.Worksheets[0]);
clone.Save(@"C:\Temp\PivotCopy.xlsx", SaveFormat.Xlsx);
```

> **Note:** หากคุณต้องการ pivot table เพียงบนแผ่นงานใหม่ภายใน workbook เดียวกัน วิธี `sourceRange.Copy` ก่อนหน้านี้จะเบากว่าและหลีกเลี่ยงการสร้าง workbook ใหม่ทั้งหมด  

## ฝังฟอนต์สำหรับการส่งออก PDF – ทำไมจึงสำคัญ

เมื่อคุณเปิด PDF บนเครื่องที่ไม่มีฟอนต์ต้นฉบับ ตัวอักษรอาจเคลื่อนที่, การตัดบรรทัดเปลี่ยน, หรืออักขระหายไป การตั้งค่า `EmbedStandardFonts = true` บอก Aspose ให้ฝังฟอนต์ที่พบบ่อยที่สุด (Arial, Times New Roman ฯลฯ) ลงในสตรีม PDF โดยตรง  

หากคุณใช้ฟอนต์กำหนดเอง ให้สลับเป็น `PdfSaveOptions.FontEmbeddingMode = FontEmbeddingMode.EmbedAll` ตัวอย่างดังนี้  

```csharp
var pdfOpts = new PdfSaveOptions
{
    EmbedStandardFonts = true,
    FontEmbeddingMode = FontEmbeddingMode.EmbedAll   // For custom fonts
};
reportWorkbook.Save(@"C:\Temp\CustomFontReport.pdf", pdfOpts);
```

ตอนนี้ผู้รับทุกคนจะเห็นการจัดวางเดียวกันกับที่คุณออกแบบ—ไม่มีความประหลาดใจ  

## สรุปตัวอย่างการทำงานเต็มรูปแบบ

การรวมทุกอย่างเข้าด้วยกัน โปรแกรมเต็มรูปแบบ (ที่แสดงก่อนหน้านี้) ทำตามขั้นตอนต่อไปนี้:

1. **Creates** สร้าง workbook พร้อม Smart Marker placeholders.  
2. **Processes** ประมวลผล markers, สร้าง detail sheet ที่ตั้งชื่อตามแผนก.  
3. **Copies** คัดลอกช่วงที่มี pivot table ไปยังแผ่นงานใหม่, คงฟังก์ชันการทำงาน.  
4. **Exports** ส่งออก workbook ไปยัง PowerPoint, คงแผนภูมิ, รูปร่าง, และ text boxes ที่แก้ไขได้.  
5. **Exports** ส่งออก workbook เดียวกันเป็น PDF พร้อมฝังฟอนต์มาตรฐานเพื่อการเรนเดอร์ที่เชื่อถือได้.  

รันโปรแกรม, เปิดไฟล์ที่สร้างขึ้น, แล้วคุณจะเห็น:

- **PDF**: ตารางคมชัด, ฟอนต์ฝัง, และสไตล์ภาพเดียวกับแหล่ง Excel  
- **PowerPoint**: แผนภูมิที่แก้ไขได้ที่คุณสามารถคลิกขวา → *Edit Data* ใน PowerPoint, และรูปร่างที่ยังคงสามารถจัดการได้เต็มที่  

---

## คำถามที่พบบ่อย (FAQ)

**Q: ทำงานกับ .NET Core ได้หรือไม่?**  
ใช่—Aspose.Cells และ Aspose.Slides รองรับหลายแพลตฟอร์ม เพียงตั้งเป้าหมายเป็น .NET 6 หรือใหม่กว่า แล้วโค้ดเดียวกันก็ทำงานบน Windows, Linux, หรือ macOS  

**Q: ถ้าต้องการส่งออกเฉพาะบางแผ่นงานล่ะ?**  
ใช้ `Workbook.Save` พร้อม `SaveOptions` ที่ให้คุณระบุ `SheetNames` ตัวอย่าง: `new PresentationOptions { SheetNames = new[] { "Copy" } }`  

**Q: สามารถเข้ารหัส PDF ได้หรือไม่?**  
แน่นอน ตั้งค่า `PdfSaveOptions.EncryptionDetails` พร้อมรหัสผ่านก่อนเรียก `Save`  

**Q: Pivot table ของฉันใช้แหล่งข้อมูลภายนอก—การคัดลอกจะทำให้ลิงก์เสียหรือไม่?**  
การคัดลอกจะรวมแคช แต่ไม่รวมการเชื่อมต่อภายนอก Pivot จะทำงานแบบออฟไลน์ต่อไป แต่จะไม่รีเฟรชจากแหล่งต้นฉบับ หากต้องการรีเฟรชแบบเรียลไทม์ ให้ส่งออกข้อมูลแหล่งพร้อมกับ workbook  

## ขั้นตอนต่อไป & หัวข้อที่เกี่ยวข้อง

- **Dynamic Data Sources** – เรียนรู้วิธีป้อน JSON หรือ DataTable เข้าไปใน Smart Markers เพื่อการรายงานแบบเรียลไทม์  
- **Advanced PDF Styling** – Explore `

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}