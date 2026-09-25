---
category: general
date: 2026-03-30
description: สร้าง PowerPoint จาก Excel อย่างรวดเร็วโดยใช้ Aspose.Cells และ Aspose.Slides
  เรียนรู้วิธีส่งออกแผ่นงานเป็นภาพและบันทึกงานนำเสนอเป็น PPTX ด้วย C#
draft: false
keywords:
- create powerpoint from excel
- convert excel to powerpoint
- export worksheet as image
- save presentation as pptx
- export excel chart as picture
language: th
og_description: สร้าง PowerPoint จาก Excel ด้วย C# และ Aspose ส่งออกแผ่นงานเป็นภาพ
  รักษารูปร่างให้แก้ไขได้ และบันทึกผลลัพธ์เป็นไฟล์ PPTX
og_title: สร้าง PowerPoint จาก Excel – คอร์สสอน C# อย่างครบถ้วน
tags:
- Aspose
- C#
- Office Automation
title: สร้าง PowerPoint จาก Excel – คู่มือ C# ขั้นตอนต่อขั้นตอน
url: /th/net/converting-excel-files-to-other-formats/create-powerpoint-from-excel-step-by-step-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# สร้าง PowerPoint จาก Excel – คำแนะนำ C# ฉบับสมบูรณ์

เคยต้อง **สร้าง PowerPoint จาก Excel** แต่ไม่แน่ใจว่าควรใช้ไลบรารีใดที่ทำให้แผนภูมิของคุณยังแก้ไขได้หรือไม่? คุณไม่ได้อยู่คนเดียว ในหลายกรณีของการรายงานคุณอาจต้องการแปลงสเปรดชีตเป็นสไลด์โดยไม่สูญเสียความสามารถในการปรับแก้กล่องข้อความในภายหลัง คู่มือฉบับนี้จะแสดงให้คุณเห็นอย่างละเอียดว่า **แปลง Excel เป็น PowerPoint** อย่างไรโดยใช้ Aspose.Cells และ Aspose.Slides พร้อมทั้งอธิบายวิธี **ส่งออก worksheet เป็นภาพ** และสุดท้าย **บันทึกงานนำเสนอเป็น PPTX** 

เราจะเดินผ่านทุกบรรทัดของโค้ด อธิบาย *ทำไม* การตั้งค่าแต่ละอย่างจึงสำคัญ และแม้แต่การจัดการเมื่อเวิร์กบุ๊กของคุณมีแผนภูมิที่ซับซ้อนที่คุณอยากส่งออกเป็นรูปภาพ เมื่อเสร็จสิ้นคุณจะได้แอปคอนโซล C# ที่พร้อมรัน ซึ่งรับไฟล์ `ShapesDemo.xlsx` แล้วสร้างไฟล์ `Result.pptx` – ทั้งกล่องข้อความที่แก้ไขได้และภาพที่คมชัด

## สิ่งที่คุณต้องเตรียม

- .NET 6.0 หรือใหม่กว่า (API นี้ทำงานกับ .NET Framework ได้เช่นกัน แต่ .NET 6 เป็นจุดที่เหมาะที่สุด)  
- แพคเกจ NuGet **Aspose.Cells** และ **Aspose.Slides** (ไลเซนส์ทดลองฟรีใช้สำหรับการทดสอบ)  
- ความคุ้นเคยพื้นฐานกับไวยากรณ์ C# – หากคุณสามารถเขียน `Console.WriteLine` ได้ คุณก็พร้อมแล้ว  

ไม่มีการใช้ COM interop เพิ่มเติม ไม่ต้องติดตั้ง Office บนเซิร์ฟเวอร์ และไม่มีการคัดลอก‑วางรูปภาพด้วยมือ ทุกอย่างทำโดยโปรแกรม

---

## Create PowerPoint from Excel – Load Workbook and Set Export Options

สิ่งแรกที่เราทำคือเปิดไฟล์ Excel และบอก Aspose.Cells ว่าเราต้องการให้แผ่นทำงานอย่างไร `ImageOrPrintOptions` คือที่ที่เวทมนตร์เกิดขึ้น: เราเปิดใช้งาน `ExportShapes` และ `ExportEditableTextBoxes` เพื่อให้รูปทรงใด ๆ (รวมถึงแผนภูมิ) กลายเป็นส่วนหนึ่งของสไลด์ **และ** ยังคงแก้ไขได้หลังการแปลง

```csharp
using Aspose.Cells;
using Aspose.Slides;

// 1️⃣ Load the Excel workbook
string excelPath = "YOUR_DIRECTORY/ShapesDemo.xlsx";
Workbook workbook = new Workbook(excelPath);
Worksheet worksheet = workbook.Worksheets[0];   // Grab the first sheet

// 2️⃣ Configure image export – keep shapes editable
ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
{
    OnePagePerSheet = true,          // Export the whole sheet as one slide
    ExportShapes = true,             // Include shapes (charts, drawings)
    ExportEditableTextBoxes = true   // Make text boxes editable in PPTX
};
```

**ทำไมต้องตั้งค่าสถานะเหล่านี้?**  
- `OnePagePerSheet` ป้องกันไม่ให้แผ่นถูกแบ่งเป็นหลายสไลด์ – คุณจะได้ภาพขนาดเต็มหน้าเดียว  
- `ExportShapes` บอก Aspose.Cells ให้เรนเดอร์แผนภูมิ *และ* รูปทรงเวกเตอร์เป็นภาพ rasterized, รักษารูปลักษณ์เดิมไว้  
- `ExportEditableTextBoxes` คือสูตรลับที่ทำให้คุณคลิกสองครั้งที่กล่องข้อความใน PowerPoint แล้วแก้ไขข้อความได้โดยไม่ต้องเปิด Excel อีกครั้ง  

> **เคล็ดลับ:** หากคุณต้องการเพียงภาพคงที่ของแผนภูมิเท่านั้น ให้ตั้งค่า `ExportShapes = false` แล้วใช้เมธอด `ExportExcelChartAsPicture` ในภายหลัง (ดูส่วนสุดท้าย)

---

## Convert Excel to PowerPoint – Generate Image from Worksheet

เมื่อกำหนดตัวเลือกเรียบร้อยแล้ว เราจะเปลี่ยน worksheet ให้เป็น `System.Drawing.Image` ตัวแปลง `WorksheetToImageConverter` จะทำงานหนักโดยใช้การตั้งค่าที่เรากำหนดไว้

```csharp
// 3️⃣ Convert the worksheet to an image using the options above
WorksheetToImageConverter converter = new WorksheetToImageConverter(worksheet);
System.Drawing.Image sheetImage = converter.ConvertToImage(0, imageOptions);
```

อาร์กิวเมนต์ `0` หมายถึงหน้าที่หนึ่ง (เรามีเพียงหน้าเดียวเนื่องจาก `OnePagePerSheet`) `sheetImage` ที่ได้จะคง DPI ดั้งเดิมไว้ ทำให้สไลด์ของคุณไม่เบลอแม้บนจอแสดงผลความละเอียดสูง

---

## Save Presentation as PPTX – Insert Image into a Slide

ต่อไปเราจะสร้างไฟล์ PowerPoint ใหม่ เพิ่มสไลด์หนึ่งสไลด์ แล้ววางบิตแมพลงไป Aspose.Slides จะถือรูปภาพนี้เป็นรูปทรง *picture frame* ซึ่งคุณสามารถปรับขนาดหรือย้ายได้เช่นเดียวกับวัตถุ PowerPoint ดั้งเดิม

```csharp
// 4️⃣ Create a new PowerPoint presentation
Presentation presentation = new Presentation();
ISlide slide = presentation.Slides[0];   // The default blank slide

// Add the Excel‑derived image as a picture frame
slide.Shapes.AddPictureFrame(
    ShapeType.Rectangle,                 // Simple rectangle container
    0, 0,                                // Top‑left corner (0,0)
    sheetImage.Width,                    // Width of the picture
    sheetImage.Height,                   // Height of the picture
    sheetImage);                         // The bitmap we generated
```

> **ถ้าภาพใหญ่กว่าขนาดสไลด์จะเกิดอะไรขึ้น?**  
> PowerPoint จะตัดส่วนที่เกินขนาดสไลด์โดยอัตโนมัติ วิธีแก้อย่างรวดเร็วคือปรับสเกลภาพก่อนแทรก:

```csharp
float scale = Math.Min(presentation.SlideSize.Size.Width / (float)sheetImage.Width,
                       presentation.SlideSize.Size.Height / (float)sheetImage.Height);
int newWidth  = (int)(sheetImage.Width * scale);
int newHeight = (int)(sheetImage.Height * scale);
```

จากนั้นคุณสามารถส่งค่า `newWidth` และ `newHeight` ไปยัง `AddPictureFrame` ได้

---

## Export Worksheet as Image – Save the PPTX File

สุดท้ายเราจะบันทึกงานนำเสนอลงดิสก์ ตัวเลือก `SaveFormat.Pptx` รับประกันรูปแบบ OpenXML สมัยใหม่ ซึ่งทำงานได้กับ PowerPoint เวอร์ชันล่าสุดทั้งหมด

```csharp
// 5️⃣ Save the presentation as a PPTX file
string pptxPath = "YOUR_DIRECTORY/Result.pptx";
presentation.Save(pptxPath, SaveFormat.Pptx);
```

เมื่อคุณเปิด `Result.pptx` จะเห็นสไลด์เดียวที่ดูเหมือนกับแผ่น Excel ของคุณอย่างแม่นยำ แต่คุณยังคงสามารถคลิกที่กล่องข้อความใดก็ได้และแก้ไขเนื้อหาโดยตรงใน PowerPoint

---

## Export Excel Chart as Picture – When Raster Images Are Preferred

บางครั้งคุณอาจไม่ต้องการรูปทรงที่แก้ไขได้; PNG คุณภาพสูงของแผนภูมิก็เพียงพอ Aspose.Cells สามารถส่งออกแผนภูมิเฉพาะเป็นภาพได้โดยไม่ต้องแปลงทั้งแผ่น:

```csharp
// Example: Export the first chart on the sheet as a PNG
int chartIndex = 0; // Adjust if you have multiple charts
Chart chart = worksheet.Charts[chartIndex];
ImageOrPrintOptions chartOptions = new ImageOrPrintOptions
{
    ImageFormat = ImageFormat.Png,
    OnePagePerSheet = false
};
chart.ToImage("chart.png", chartOptions);
```

จากนั้นคุณสามารถฝัง `chart.png` ลงในสไลด์ได้เช่นเดียวกับที่เราเพิ่ม `sheetImage` วิธีนี้ช่วยลดขนาดไฟล์ PPTX และเหมาะเมื่อข้อมูลรอบข้างไม่จำเป็นต้องแสดงบนสไลด์

---

## Common Pitfalls & How to Avoid Them

| ปัญหา | สาเหตุ | วิธีแก้ |
|-------|--------|----------|
| **ข้อความดูเบลอ** | ส่งออกที่ DPI ต่ำ (ค่าเริ่มต้น 96) | ตั้งค่า `imageOptions.Dpi = 300;` ก่อนทำการแปลง |
| **รูปทรงหาย** | `ExportShapes` ตั้งเป็น `false` | ตรวจสอบให้ `ExportShapes = true` เมื่อจำเป็นต้องการกราฟิกที่แก้ไขได้ |
| **ขนาดสไลด์ไม่ตรงกัน** | ภาพใหญ่กว่าขนาดสไลด์ | ปรับสเกลภาพ (ดูโค้ดตัวอย่าง) หรือเปลี่ยนขนาดสไลด์ผ่าน `presentation.SlideSize` |
| **License exception** | ใช้เวอร์ชันทดลองโดยไม่ได้เปิดใช้งานอย่างถูกต้อง | เรียก `License license = new License(); license.SetLicense("Aspose.Total.lic");` ตั้งแต่ต้นเมธอด `Main` |

---

## Full Working Example (Copy‑Paste Ready)

ด้านล่างเป็นโปรแกรมทั้งหมด พร้อมคัดลอก‑วางลงในโปรเจกต์คอนโซลใหม่ แทนที่ `YOUR_DIRECTORY` ด้วยโฟลเดอร์ที่เก็บไฟล์ Excel ของคุณ

```csharp
using System;
using Aspose.Cells;
using Aspose.Slides;
using System.Drawing;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // 1️⃣ Load the Excel workbook
            // -----------------------------------------------------------------
            string excelPath = "YOUR_DIRECTORY/ShapesDemo.xlsx";
            Workbook workbook = new Workbook(excelPath);
            Worksheet worksheet = workbook.Worksheets[0];

            // -----------------------------------------------------------------
            // 2️⃣ Set up export options – keep shapes editable
            // -----------------------------------------------------------------
            ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
            {
                OnePagePerSheet = true,
                ExportShapes = true,
                ExportEditableTextBoxes = true,
                Dpi = 300                 // High‑resolution output
            };

            // -----------------------------------------------------------------
            // 3️⃣ Convert worksheet to an image
            // -----------------------------------------------------------------
            WorksheetToImageConverter converter = new WorksheetToImageConverter(worksheet);
            Image sheetImage = converter.ConvertToImage(0, imageOptions);

            // -----------------------------------------------------------------
            // 4️⃣ Create PowerPoint and add the image as a slide
            // -----------------------------------------------------------------
            Presentation presentation = new Presentation();
            ISlide slide = presentation.Slides[0];
            slide.Shapes.AddPictureFrame(
                ShapeType.Rectangle,
                0, 0,
                sheetImage.Width,
                sheetImage.Height,
                sheetImage);

            // -----------------------------------------------------------------
            // 5️⃣ Save the PPTX file
            // -----------------------------------------------------------------
            string pptxPath = "YOUR_DIRECTORY/Result.pptx";
            presentation.Save(pptxPath, SaveFormat.Pptx);

            Console.WriteLine("✅ PowerPoint created successfully at: " + pptxPath);
        }
    }
}
```

**ผลลัพธ์ที่คาดหวัง:**  
เมื่อรันโปรแกรมจะพิมพ์ `✅ PowerPoint created successfully at: YOUR_DIRECTORY/Result.pptx` การเปิดไฟล์ PPTX จะเห็นสไลด์เดียวที่สะท้อนแผ่น Excel ดั้งเดิม พร้อมกล่องข้อความที่แก้ไขได้

---

## Recap & Next Steps

ตอนนี้คุณรู้วิธี **สร้าง PowerPoint จาก Excel** ด้วย API ที่ทรงพลังของ Aspose, วิธี **ส่งออก worksheet เป็นภาพ**, และวิธี **บันทึกงานนำเสนอเป็น PPTX** พร้อมคงความสามารถในการแก้ไข รูปแบบเดียวกันนี้ทำงานได้กับเวิร์กบุ๊กหลายแผ่น – เพียงลูปผ่าน `workbook.Worksheets` แล้วเพิ่มสไลด์ใหม่สำหรับแต่ละแผ่น

**สิ่งที่ควรสำรวจต่อไป?**  

- **Batch conversion:** ลูปผ่านโฟลเดอร์ของไฟล์ Excel แล้วสร้างสไลด์เด็คต่อไฟล์หนึ่งไฟล์  
- **Dynamic layouts:** ใช้ `slide.LayoutSlide` เพื่อใช้เทมเพลต PowerPoint ที่ออกแบบไว้ล่วงหน้า  
- **Chart‑only export:** ผสานส่วน “Export Excel chart as picture” กับ placeholder สไลด์เพื่อสร้างเด็คที่เบากว่า  
- **Advanced styling:** เพิ่มพื้นหลังสไลด์ที่กำหนดเอง, การเปลี่ยนฉาก, หรือแอนิเมชันผ่าน Aspose.Slides  

ลองทดลองเปลี่ยน DPI, สลับ `ShapeType.Ellipse` เป็นกรอบรูปวงกลม, หรือแม้แต่ฝังหลายภาพต่อสไลด์ได้เลย ความเป็นไปได้ไม่มีขีดจำกัดเมื่อคุณมีการควบคุมแบบโปรแกรมเมติก

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}