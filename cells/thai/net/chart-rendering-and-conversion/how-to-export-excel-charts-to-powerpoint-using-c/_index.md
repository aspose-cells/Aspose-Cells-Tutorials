---
category: general
date: 2026-10-26
description: เรียนรู้วิธีส่งออกแผนภูมิ Excel ไปยัง PowerPoint ด้วย C# รักษาความสามารถในการแก้ไขรูปทรงและบันทึกเป็น
  PPTX ด้วยไม่กี่บรรทัดของโค้ด.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel charts to powerpoint
- Aspose.Cells export
- C# Excel to PowerPoint conversion
- preserve shape editability
- SaveFormat.Pptx
- Workbook.Save method
language: th
lastmod: 2026-10-26
og_description: ส่งออกแผนภูมิ Excel ไปยัง PowerPoint ด้วย C# คู่มือนี้จะแสดงวิธีทำให้รูปทรงแก้ไขได้และบันทึกเป็น
  PPTX ด้วย Aspose.Cells.
og_image_alt: Export Excel charts to PowerPoint example showing a chart transferred
  from Excel to a slide
og_title: ส่งออกแผนภูมิ Excel ไปยัง PowerPoint ด้วย C# – คู่มือขั้นตอนโดยละเอียด
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn how to export Excel charts to PowerPoint with C#. Preserve shape
    editability and save as PPTX in a few lines of code.
  headline: How to export Excel charts to PowerPoint using C#
  type: TechArticle
- description: Learn how to export Excel charts to PowerPoint with C#. Preserve shape
    editability and save as PPTX in a few lines of code.
  name: How to export Excel charts to PowerPoint using C#
  steps:
  - name: Load the Excel workbook
    text: '```csharp using Aspose.Cells;'
  - name: (Optional) Adjust workbook settings
    text: In most cases the default settings are sufficient for a clean export. However,
      if you need to change the calculation mode, page setup, or hide certain sheets,
      you can do it here.
  - name: Save the workbook as a PowerPoint file
    text: '```csharp // Export the workbook to PPTX while keeping chart shapes editable
      workbook.Save(@"C:\Projects\Shapes.pptx", SaveFormat.Pptx); ```'
  - name: Verify the result
    text: 'Open `Shapes.pptx` in PowerPoint and:'
  - name: 'Edge case: Exporting multiple worksheets with separate charts'
    text: If your Excel file contains several worksheets, each with its own chart,
      Aspose.Cells creates a separate slide for each chart automatically. You can
      control slide order by rearranging worksheets before the save operation.
  - name: 'Performance tip: Stream the output instead of writing to disk'
    text: When generating PowerPoint files in a web API, avoid temporary files by
      writing to a `MemoryStream`.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel
- PowerPoint
title: วิธีส่งออกแผนภูมิ Excel ไปยัง PowerPoint ด้วย C#
url: /th/net/chart-rendering-and-conversion/how-to-export-excel-charts-to-powerpoint-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีส่งออกแผนภูมิ Excel ไปยัง PowerPoint ด้วย C#

หากคุณต้องการ **export Excel charts to PowerPoint** คู่มือนี้จะพาคุณผ่านโซลูชันที่สมบูรณ์และพร้อมใช้งาน ไม่ว่าคุณจะสร้างแดชบอร์ดรายงานหรือทำการอัตโนมัติของสไลด์เด็ค คุณจะได้เห็นว่าบรรทัดโค้ด C# เพียงไม่กี่บรรทัดทำให้รูปทรงแผนภูมิของคุณยังคงแก้ไขได้อย่างเต็มที่หลังการแปลง

ในบทเรียนนี้คุณจะได้เรียนรู้วิธี:

* โหลดเวิร์กบุ๊ก Excel ที่มีแผนภูมิอยู่แล้ว  
* (โดยออปชัน) ปรับแต่งการตั้งค่าเวิร์กบุ๊กก่อนการแปลง  
* บันทึกเวิร์กบุ๊กเป็นไฟล์ PowerPoint พร้อมคงความสามารถในการแก้ไขรูปทรง  

ทั้งหมดนี้ทำได้ด้วย **Aspose.Cells for .NET** ซึ่งเป็นไลบรารีที่จัดการการแปลง Excel‑to‑PowerPoint โดยไม่ต้องใช้ Microsoft Office บนเซิร์ฟเวอร์

## สิ่งที่คุณต้องมี

| ความต้องการ | เหตุผล |
|-------------|--------|
| .NET 6.0 หรือใหม่กว่า | รันไทม์สมัยใหม่พร้อมคุณสมบัติของภาษาเต็มรูปแบบ |
| Visual Studio 2022 (หรือ IDE ใดก็ได้) | ตัวแก้ไขและดีบักเกอร์ที่สะดวก |
| **Aspose.Cells for .NET** NuGet package | ให้คลาส `Workbook` และการสนับสนุน `SaveFormat.Pptx` |
| ไฟล์ Excel (`ChartAndShapes.xlsx`) ที่มีอย่างน้อยหนึ่งแผนภูมิ | แหล่งที่มาของแผนภูมิที่คุณต้องการส่งออก |

> **Pro tip:** ใช้เวอร์ชัน **Aspose.Cells Evaluation** ฟรีเพื่อทดสอบโค้ด; คีย์ไลเซนส์จะลบลายน้ำการประเมินออก

```bash
dotnet add package Aspose.Cells
```

## ส่งออกแผนภูมิ Excel ไปยัง PowerPoint – กระบวนการเต็มรูปแบบ

ด้านล่างเป็นโค้ดแบบครบวงจรที่ทำการส่งออกพร้อม **preserving shape editability** แต่ละขั้นตอนจะอธิบายรายละเอียด

### ขั้นตอนที่ 1: โหลดเวิร์กบุ๊ก Excel

```csharp
using Aspose.Cells;

// Load the workbook that holds the charts you want to export
Workbook workbook = new Workbook(@"C:\Projects\ChartAndShapes.xlsx");
```

*คลาส `Workbook` แทนไฟล์ Excel ทั้งไฟล์ การโหลดไฟล์จะอ่านทุกแผ่นงาน, แผนภูมิ, และรูปทรงเข้าสู่หน่วยความจำ ซึ่งจำเป็นสำหรับการจัดการต่อไป*

### ขั้นตอนที่ 2: (ออปชัน) ปรับการตั้งค่าเวิร์กบุ๊ก

ในหลายกรณีการตั้งค่าเริ่มต้นก็เพียงพอสำหรับการส่งออกที่สะอาด อย่างไรก็ตาม หากคุณต้องการเปลี่ยนโหมดการคำนวณ, การตั้งค่าหน้ากระดาษ, หรือซ่อนแผ่นงานบางแผ่น คุณสามารถทำได้ที่นี่

```csharp
// Example: ensure all formulas are calculated before export
workbook.CalculateFormula();

// Example: hide a sheet that you don’t want in the PowerPoint
workbook.Worksheets["SecretData"].IsVisible = false;
```

> **Why this matters:** การปรับการตั้งค้าก่อนการแปลงรับประกันว่าหนังสือสไลด์ที่สร้างขึ้นจะแสดงสถานะที่คุณต้องการอย่างแม่นยำ โดยเฉพาะเมื่อสูตรหรือแผ่นงานที่ซ่อนอยู่อาจส่งผลต่อข้อมูลแผนภูมิ

### ขั้นตอนที่ 3: บันทึกเวิร์กบุ๊กเป็นไฟล์ PowerPoint

```csharp
// Export the workbook to PPTX while keeping chart shapes editable
workbook.Save(@"C:\Projects\Shapes.pptx", SaveFormat.Pptx);
```

*ค่าคงที่ `SaveFormat.Pptx` บอก Aspose.Cells ให้เขียนเป็นพรีเซนเทชัน PowerPoint ภายในไลบรารีจะทำการแปลงแต่ละแผนภูมิ Excel เป็นรูปทรง PowerPoint ที่ยังคงแก้ไขได้เต็มที่ใน Microsoft PowerPoint*

### ขั้นตอนที่ 4: ตรวจสอบผลลัพธ์

เปิด `Shapes.pptx` ใน PowerPoint แล้ว:

1. เลือกแผนภูมิบนสไลด์ใดสไลด์หนึ่ง  
2. คลิกขวา → **Edit Data**  
3. ยืนยันว่าตารางข้อมูลของแผนภูมิเกิดขึ้นและคุณสามารถแก้ไขค่าได้  

หากแผนภูมิเปิดหน้าต่าง **Edit Data** การแปลงสำเร็จและ **shape editability** ถูกคงไว้

![Export Excel charts to PowerPoint example](export-excel-charts-to-powerpoint.png){.img-fluid alt="ตัวอย่างการส่งออกแผนภูมิ Excel ไปยัง PowerPoint"}

## ปัญหาที่พบบ่อยและวิธีหลีกเลี่ยง

| ปัญหา | สาเหตุ | วิธีแก้ |
|-------|-------|----------|
| แผนภูมิเจอเป็นภาพคงที่ | ใช้เวอร์ชันเก่าของ Aspose.Cells ที่ไม่มีการสนับสนุนการส่งออกเป็น PPTX | อัปเกรดเป็น Aspose.Cells รุ่นล่าสุด 23.x หรือใหม่กว่า |
| ข้อมูลหายในแผนภูมิ PowerPoint | เวิร์กบุ๊กไม่ได้คำนวณเต็มที่ก่อนการส่งออก | เรียก `workbook.CalculateFormula()` ก่อน `Save` |
| รูปทรงไม่สามารถแก้ไขได้ | บันทึกด้วย `SaveFormat.Xlsx` แทน `SaveFormat.Pptx` | ตรวจสอบให้แน่ใจว่าคุณส่งค่า `SaveFormat.Pptx` ให้กับ `Workbook.Save` |
| ข้อยกเว้นไลเซนส์ขณะรันไทม์ | เวอร์ชันประเมินโดยไม่มีไลเซนส์ที่ลงทะเบียน | ลงทะเบียนไลเซนส์ด้วย `License license = new License(); license.SetLicense("Aspose.Cells.lic");` |

### กรณีขอบ: ส่งออกหลายแผ่นงานพร้อมแผนภูมิแยกกัน

หากไฟล์ Excel ของคุณมีหลายแผ่นงานและแต่ละแผ่นงานมีแผนภูมิของตนเอง Aspose.Cells จะสร้างสไลด์แยกสำหรับแต่ละแผนภูมิโดยอัตโนมัติ คุณสามารถควบคุมลำดับสไลด์ได้โดยจัดเรียงแผ่นงานก่อนทำการบันทึก

```csharp
// Move the worksheet that should appear first in the slide deck
workbook.Worksheets.MoveTo(2, 0); // move sheet index 2 to position 0
```

### เคล็ดลับประสิทธิภาพ: สตรีมผลลัพธ์แทนการเขียนลงดิสก์

เมื่อสร้างไฟล์ PowerPoint ในเว็บ API ควรหลีกเลี่ยงไฟล์ชั่วคราวโดยเขียนลง `MemoryStream`

```csharp
using (MemoryStream pptStream = new MemoryStream())
{
    workbook.Save(pptStream, SaveFormat.Pptx);
    // Return the stream as a file download
    FileContentResult result = new FileContentResult(pptStream.ToArray(),
        "application/vnd.openxmlformats-officedocument.presentationml.presentation")
    {
        FileDownloadName = "Charts.pptx"
    };
    return result;
}
```

## ตัวอย่างเต็มที่พร้อมรัน

```csharp
using System;
using Aspose.Cells;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main()
        {
            // 1. Load the workbook containing charts
            string excelPath = @"C:\Projects\ChartAndShapes.xlsx";
            Workbook workbook = new Workbook(excelPath);

            // 2. (Optional) Ensure formulas are up‑to‑date
            workbook.CalculateFormula();

            // 3. Export to PowerPoint while preserving shape editability
            string pptxPath = @"C:\Projects\Shapes.pptx";
            workbook.Save(pptxPath, SaveFormat.Pptx);

            Console.WriteLine($"Export complete. PowerPoint saved to: {pptxPath}");
        }
    }
}
```

**Expected output:** คอนโซลจะแสดงข้อความยืนยัน และ `Shapes.pptx` จะเปิดใน PowerPoint โดยแต่ละแผนภูมิ Excel ปรากฏบนสไลด์ของตนเอง การเลือกแผนภูมิจะทำให้คุณแก้ไขข้อมูลได้ ยืนยันว่า **shape editability** ถูกเก็บไว้

## สรุปและขั้นตอนต่อไป

คุณได้เรียนรู้วิธี **export Excel charts to PowerPoint** ด้วย C# พร้อมคงความสามารถในการแก้ไขแผนภูมิทั้งหมด ส่วนสำคัญของโซลูชันคือเมธอด `Workbook.Save` พร้อม `SaveFormat.Pptx` ซึ่งเป็นฟีเจอร์ของ **Aspose.Cells export** ที่ทำให้คุณไม่ต้องจัดการกับ Open XML ที่ซับซ้อน

จากนี้คุณอาจสำรวจต่อ:

* เพิ่มหัวข้อสไลด์หรือโน้ตแบบกำหนดเองด้วย API **Aspose.Slides**  
* แปลงวัตถุ Excel อื่น ๆ (ตาราง, รูปภาพ) ควบคู่กับแผนภูมิ  
* ทำการประมวลผลแบบแบตช์ของหลายเวิร์กบุ๊กในบริการพื้นหลัง

ลองปรับแต่งการตั้งค่าออปชันที่แสดงด้านบนและผสานรูปแบบนี้เข้ากับสายงานรายงานของคุณเพื่อการสร้าง PowerPoint ที่รวดเร็วและเชื่อถือได้

## คุณควรเรียนรู้อะไรต่อไป?

บทเรียนต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งข้อมูลมีโค้ดตัวอย่างทำงานเต็มรูปแบบพร้อมคำอธิบายทีละขั้นตอนเพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการทำงานทางเลือกในโครงการของคุณเอง

- [Export Excel chart to PowerPoint with C# – complete Aspose.Cells guide](/cells/english/net/chart-rendering-and-conversion/export-excel-chart-to-powerpoint-with-c-complete-aspose-cell/)
- [How to Export Excel to PowerPoint with C# – Complete Guide](/cells/english/net/converting-excel-files-to-other-formats/how-to-export-excel-to-powerpoint-with-c-complete-guide/)
- [How to Export Shapes from Excel to PowerPoint – Complete Guide](/cells/english/net/drawing-objects/how-to-export-shapes-from-excel-to-powerpoint-complete-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}