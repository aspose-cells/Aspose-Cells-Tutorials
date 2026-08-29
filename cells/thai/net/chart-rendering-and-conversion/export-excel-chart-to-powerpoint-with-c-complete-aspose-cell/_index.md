---
category: general
date: 2026-08-04
description: ส่งออกแผนภูมิ Excel ไปยัง PowerPoint ด้วย Aspose.Cells ใน C#. ทำตามคู่มือการแปลงจาก
  Excel ไปยัง PowerPoint ทีละขั้นตอนและทำให้รูปทรงยังคงแก้ไขได้
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel chart to powerpoint
- Aspose.Cells PPTX export
- editable shapes in PowerPoint
- Excel to PowerPoint conversion
- C# chart export
language: th
lastmod: 2026-08-04
og_description: ส่งออกแผนภูมิ Excel ไปยัง PowerPoint ด้วย Aspose.Cells ใน C# เรียนรู้วิธีสร้างไฟล์
  PPTX ที่แก้ไขได้ รักษาข้อมูลแผนภูมิ และทำการแปลงจาก Excel ไปยัง PowerPoint อย่างอัตโนมัติ
og_image_alt: Screenshot of an Excel chart rendered as an editable PowerPoint slide
og_title: ส่งออกแผนภูมิ Excel ไปยัง PowerPoint ด้วย C# – บทเรียนเต็มของ Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Export Excel chart to PowerPoint using Aspose.Cells in C#. Follow this
    step‑by‑step Excel to PowerPoint conversion guide and keep shapes editable.
  headline: Export Excel chart to PowerPoint with C# – complete Aspose.Cells guide
  type: TechArticle
- description: Export Excel chart to PowerPoint using Aspose.Cells in C#. Follow this
    step‑by‑step Excel to PowerPoint conversion guide and keep shapes editable.
  name: Export Excel chart to PowerPoint with C# – complete Aspose.Cells guide
  steps:
  - name: Expected output
    text: '| File name | Content on slide | |--------------------------|------------------------------------------|
      | `ShapesExport.pptx` | The chart from `Shapes.xlsx` rendered as an editable
      PowerPoint chart, with axis labels, legends, and data series intact. |'
  - name: Exporting multiple worksheets
    text: If you need a slide for each worksheet, loop through `workbook.Worksheets`
      and call `Save` with a unique file name for each iteration.
  - name: Controlling slide layout
    text: Aspose.Slides lets you add a custom slide layout after the export. Create
      a new presentation, import the generated slide, and then apply a master theme.
  - name: Handling charts with external data sources
    text: If a chart references a data range outside the defined print area, extend
      the `PrintArea` to include those cells. Otherwise the chart may lose data series
      during export.
  - name: Licensing considerations
    text: 'Aspose libraries work in evaluation mode with a watermark. To remove the
      watermark, set the license before any API call:'
  type: HowTo
tags:
- Aspose.Cells
- C#
- PowerPoint
title: ส่งออกแผนภูมิ Excel ไปยัง PowerPoint ด้วย C# – คู่มือ Aspose.Cells ฉบับสมบูรณ์
url: /th/net/chart-rendering-and-conversion/export-excel-chart-to-powerpoint-with-c-complete-aspose-cell/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ส่งออกแผนภูมิ Excel ไปยัง PowerPoint ด้วย C# – คู่มือ Aspose.Cells ฉบับเต็ม

หากคุณต้องการ **ส่งออกแผนภูมิ Excel ไปยัง PowerPoint** บทแนะนำนี้จะแสดงวิธีทำด้วย Aspose.Cells และ Aspose.Slides ใน C# คุณจะได้ไฟล์ PPTX ที่แก้ไขได้เต็มรูปแบบซึ่งคงข้อมูลและรูปร่างของแผนภูมิไว้ ทำให้การแปลงพร้อมสำหรับการออกแบบต่อไป

การส่งออกแผนภูมิจาก Excel ไปยัง PowerPoint เป็นความต้องการที่พบบ่อยเมื่อสร้างสายงานการรายงานอัตโนมัติ, ชุดสไลด์ขาย, หรือสื่อการฝึกอบรม ในคู่มือนี้คุณจะได้เรียนรู้ขั้นตอนที่แน่นอนเพื่อทำ **การแปลง Excel ไปยัง PowerPoint** ที่ทำให้ทุกองค์ประกอบของแผนภูมิสามารถแก้ไขได้ ไม่ต้องคัดลอก‑วางด้วยตนเอง และโค้ดทำงานได้กับ .NET 6+ รวมถึง .NET Framework แบบคลาสสิก

## สิ่งที่ต้องเตรียม

ก่อนเริ่มทำงาน โปรดตรวจสอบว่าคุณมี:

- ใบอนุญาต Aspose.Cells ที่ถูกต้อง (หรือคีย์ทดลองฟรี)  
- Aspose.Slides for .NET ที่เพิ่มเข้าในโครงการ (ไลบรารีนี้จัดการการสร้างไฟล์ PPTX)  
- .NET 6 SDK หรือใหม่กว่า  
- ไฟล์ Excel workbook ที่มีอย่างน้อยหนึ่งแผนภูมิ (ในตัวอย่างนี้เราใช้ `Shapes.xlsx`)  

คุณสามารถติดตั้งแพ็กเกจ NuGet ด้วยคำสั่งต่อไปนี้:

```bash
dotnet add package Aspose.Cells
dotnet add package Aspose.Slides
```

## ขั้นตอนที่ 1: โหลด Excel workbook

การดำเนินการแรกคือการเปิด workbook ที่มีแผนภูมิที่คุณต้องการส่งออก คลาส `Workbook` แทนไฟล์ Excel ทั้งไฟล์

```csharp
using Aspose.Cells;
using Aspose.Slides;   // required for PPTX output

// Load the Excel workbook from disk
Workbook workbook = new Workbook("YOUR_DIRECTORY/Shapes.xlsx");
```

**ทำไมจึงสำคัญ:** การโหลด workbook ทำให้คุณเข้าถึง worksheet, chart, และการจัดรูปแบบต่าง ๆ Aspose.Cells อ่านไฟล์โดยไม่ต้องติดตั้ง Microsoft Office ซึ่งทำให้โซลูชันมีน้ำหนักเบาและเหมาะกับเซิร์ฟเวอร์

## ขั้นตอนที่ 2: เลือก worksheet และกำหนดพื้นที่พิมพ์ (Print Area)

Worksheet อาจมีแผนภูมิจำนวนหลายรายการ แต่คุณมักจะส่งออกเฉพาะส่วนที่ต้องการ การตั้งค่า `PrintArea` บอก Aspose.Cells ว่าเซลล์ใด (รวมถึงแผนภูมิ) ควรถูกเรนเดอร์

```csharp
// Choose the first worksheet (index 0)
Worksheet worksheet = workbook.Worksheets[0];

// Define the area that contains the chart and any supporting data
worksheet.PageSetup.PrintArea = "A1:G30";
```

**ทำไมจึงสำคัญ:** การจำกัดการส่งออกให้เฉพาะพื้นที่พิมพ์ที่กำหนดจะช่วยหลีกเลี่ยงสไลด์เปล่าที่ไม่จำเป็นและทำให้ขนาดไฟล์ PPTX เล็กลง พื้นที่นี้สามารถปรับให้ตรงกับช่วงของแผนภูมิของคุณได้

## ขั้นตอนที่ 3: ตั้งค่าตัวเลือกการส่งออกสำหรับ PPTX ที่แก้ไขได้

Aspose.Cells ใช้คลาส `ImageOrPrintOptions` เพื่อควบคุมรูปแบบผลลัพธ์และความสามารถในการแก้ไข การตั้งค่า `ImageFormat` เป็น `ImageFormat.Pptx` จะสร้างไฟล์ PowerPoint ในขณะที่ `ExportEditableShapes = true` จะคงวัตถุแผนภูมิเป็นรูปร่างที่แก้ไขได้

```csharp
ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
{
    ImageFormat = ImageFormat.Pptx,   // Target format
    ExportEditableShapes = true       // Keep shapes/textboxes editable
};

// Attach the options to the worksheet's print settings
worksheet.PageSetup.PrintOptions = exportOptions;
```

**ทำไมจึงสำคัญ:** ธง `ExportEditableShapes` คือกุญแจสำคัญที่ทำให้ได้ **รูปร่างที่แก้ไขได้ใน PowerPoint** หากไม่ตั้งค่านี้ แผนภูมิจะถูกแปลงเป็นภาพราสเตอร์ ทำให้ไม่สามารถแก้ไขจุดข้อมูลหรือสไตล์ได้ภายหลัง

## ขั้นตอนที่ 4: บันทึก worksheet เป็นงานนำเสนอ PowerPoint

สุดท้ายให้เรียกเมธอด `Save` บนวัตถุ `Workbook` enum `SaveFormat.Pptx` บอก Aspose.Cells ให้สร้างไฟล์ PowerPoint

```csharp
// Export the selected worksheet to a PPTX file
workbook.Save("YOUR_DIRECTORY/ShapesExport.pptx", SaveFormat.Pptx);
```

เมื่อโค้ดทำงานเสร็จ ให้เปิด `ShapesExport.pptx` ใน PowerPoint คุณจะเห็นสไลด์ที่มีแผนภูมิ Excel ดั้งเดิมเป็นวัตถุแผนภูมิ PowerPoint แบบเนทีฟ ดับเบิล‑คลิกที่แผนภูมิเพื่อแก้ไขข้อมูล, เปลี่ยนสี, หรือเพิ่มแอนิเมชัน — เหมือนกับว่าคุณสร้างแผนภูมิโดยตรงใน PowerPoint

### ผลลัพธ์ที่คาดหวัง

| ชื่อไฟล์                | เนื้อหาบนสไลด์                         |
|--------------------------|------------------------------------------|
| `ShapesExport.pptx`      | แผนภูมิจาก `Shapes.xlsx` แสดงเป็นแผนภูมิ PowerPoint ที่แก้ไขได้, พร้อมป้ายแกน, คำอธิบาย, และชุดข้อมูลครบถ้วน |

## ตัวอย่างเต็มที่สามารถรันได้

ด้านล่างเป็นโปรแกรมทั้งหมดที่คุณสามารถคัดลอก, วาง, แล้วรันได้ รวมถึง `using` statements, การจัดการข้อผิดพลาด, และคอมเมนต์

```csharp
using System;
using Aspose.Cells;
using Aspose.Slides;   // Required for PPTX output

class ExcelToPowerPoint
{
    static void Main()
    {
        // Path to the source Excel file – adjust as needed
        const string excelPath = "YOUR_DIRECTORY/Shapes.xlsx";
        // Path for the generated PowerPoint file
        const string pptxPath = "YOUR_DIRECTORY/ShapesExport.pptx";

        try
        {
            // Load the workbook
            Workbook workbook = new Workbook(excelPath);

            // Use the first worksheet (you can change the index or name)
            Worksheet worksheet = workbook.Worksheets[0];

            // Define the area that contains the chart
            worksheet.PageSetup.PrintArea = "A1:G30";

            // Set export options for PPTX with editable shapes
            ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
            {
                ImageFormat = ImageFormat.Pptx,
                ExportEditableShapes = true
            };
            worksheet.PageSetup.PrintOptions = exportOptions;

            // Save as PPTX
            workbook.Save(pptxPath, SaveFormat.Pptx);

            Console.WriteLine($"Export successful. PPTX saved to: {pptxPath}");
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error during export: {ex.Message}");
        }
    }
}
```

**คำอธิบายของแต่ละบล็อก**

| บล็อก | จุดประสงค์ |
|-------|-------------|
| `using` directives | เรียกใช้ namespace ของ Aspose.Cells และ Aspose.Slides |
| `Workbook workbook = new Workbook(excelPath);` | โหลดไฟล์ Excel โดยไม่ต้องติดตั้ง Office |
| `worksheet.PageSetup.PrintArea = "A1:G30";` | จำกัดการส่งออกให้เฉพาะพื้นที่ที่มีแผนภูมิ |
| `ImageOrPrintOptions` | ตั้งค่าการส่งออกเป็น PPTX และเปิดใช้งาน **Aspose.Cells PPTX export** พร้อมรูปร่างที่แก้ไขได้ |
| `workbook.Save(pptxPath, SaveFormat.Pptx);` | เขียนไฟล์ PowerPoint ลงดิสก์ |
| `try / catch` | จัดการข้อผิดพลาดพื้นฐานสำหรับไฟล์ที่หายไปหรือปัญหาใบอนุญาต |

การรันโปรแกรมนี้จะสร้างสไลด์ PowerPoint ที่คุณสามารถเปิดใน Microsoft PowerPoint, Google Slides (หลังแปลง), หรือโปรแกรมดูที่รองรับอื่น ๆ

## ความแปรผันทั่วไปและกรณีขอบ

### ส่งออกหลาย worksheet

หากต้องการสไลด์สำหรับแต่ละ worksheet ให้วนลูป `workbook.Worksheets` และเรียก `Save` พร้อมชื่อไฟล์ที่ไม่ซ้ำกันสำหรับแต่ละรอบ

```csharp
int index = 1;
foreach (Worksheet ws in workbook.Worksheets)
{
    ws.PageSetup.PrintOptions = exportOptions;
    string fileName = $"Slide{index++}.pptx";
    workbook.Save(fileName, SaveFormat.Pptx);
}
```

### ควบคุมเลเอาต์ของสไลด์

Aspose.Slides ให้คุณเพิ่มเลเอาต์สไลด์แบบกำหนดเองหลังการส่งออก สร้างงานนำเสนอใหม่, นำเข้าสตรีดที่สร้าง, แล้วใช้ธีมมาสเตอร์

```csharp
using Aspose.Slides.Export;

// Load the PPTX created by Aspose.Cells
Presentation pres = new Presentation(pptxPath);

// Apply a built‑in layout (e.g., Title and Content)
pres.Slides[0].LayoutSlide = pres.LayoutSlides[(int)SlideLayoutType.TitleAndContent];

// Save the final presentation
pres.Save("FinalPresentation.pptx", SaveFormat.Pptx);
```

### จัดการแผนภูมิที่อ้างอิงแหล่งข้อมูลภายนอก

หากแผนภูมิอ้างอิงช่วงข้อมูลที่อยู่นอก PrintArea ที่กำหนดไว้ ให้ขยาย `PrintArea` ให้รวมเซลล์เหล่านั้น มิฉะนั้นแผนภูมิอาจสูญเสียชุดข้อมูลระหว่างการส่งออก

### พิจารณาเรื่องใบอนุญาต

ไลบรารี Aspose ทำงานในโหมดทดลองพร้อมลายน้ำ หากต้องการลบลายน้ำ ให้ตั้งค่าใบอนุญาตก่อนเรียก API ใด ๆ:

```csharp
var license = new Aspose.Cells.License();
license.SetLicense("Aspose.Cells.lic");
```

ทำเช่นเดียวกันกับ Aspose.Slides หากคุณใช้ฟีเจอร์ขั้นสูงของมัน

## เคล็ดลับระดับมืออาชีพ

- **ใช้ตัวเลือกการส่งออกซ้ำ:** สร้างอินสแตนซ์ `ImageOrPrintOptions` เพียงครั้งเดียวแล้วกำหนดให้กับแต่ละ worksheet เพื่อให้โค้ดเป็น DRY  
- **ประมวลผลเป็นชุด:** สำหรับการรายงานขนาดใหญ่ ให้รวมตรรกะการส่งออกนี้กับ background worker หรือ Azure Function เพื่อสร้างไฟล์ PPTX ตามความต้องการ  
- **ประสิทธิภาพ:** หากคุณต้องการเพียงภาพแผนภูมิ (ไม่ต้องแก้ไข) ให้ตั้งค่า `ExportEditableShapes = false` จะลดการใช้หน่วยความจำและเร่งการแปลง  
- **การทดสอบ:** ตรวจสอบไฟล์ PPTX ที่สร้างบน PowerPoint ของ Windows และ macOS เนื่องจากบางครั้งการเรนเดอร์อาจแตกต่างกันระหว่างแพลตฟอร์ม  

## สรุป

คุณได้มีโซลูชันครบวงจรจากต้นจนจบสำหรับ **การส่งออกแผนภูมิ Excel ไปยัง PowerPoint** ด้วย C# คู่มือนี้ครอบคลุมการโหลด workbook, การเลือก PrintArea, การตั้งค่า **Aspose.Cells PPTX export** พร้อม **รูปร่างที่แก้ไขได้ใน PowerPoint**, และการบันทึกผลลัพธ์เป็นไฟล์ PPTX ที่แก้ไขได้เต็มรูปแบบ  

จากนี้คุณสามารถสำรวจสถานการณ์ **การแปลง Excel ไปยัง PowerPoint** เพิ่มเติม เช่น การส่งออกเป็นชุด, เลเอาต์สไลด์แบบกำหนดเอง, หรือการผสานกระบวนการนี้เข้ากับ Web API ทดลองใช้แผนภูมิประเภทต่าง ๆ, เพิ่มรูปภาพ, หรือรวมหลาย worksheet เป็นงานนำเสนอเดียวเพื่อให้สอดคล้องกับความต้องการของธุรกิจคุณ

พร้อมที่จะทำให้กระบวนการรายงานของคุณเป็นอัตโนมัติหรือยัง? ลองสลับไฟล์ต้นทาง, ปรับ PrintArea, และผสานโค้ดเข้ากับบริการ .NET ของคุณที่มีอยู่แล้ว ขอให้สนุกกับการเขียนโค้ด!

## คุณควรเรียนรู้อะไรต่อไป?

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งข้อมูลมีตัวอย่างโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายขั้นตอนเพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการทำงานอื่น ๆ ในโครงการของคุณ

- [How to Convert Excel to PowerPoint Using Aspose.Cells for .NET: A Complete Guide](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [How to Export Excel Charts to PDF Using Aspose.Cells for .NET: A Step-by-Step Guide](/cells/english/net/workbook-operations/export-excel-charts-pdf-aspose-cells-net/)
- [Export Excel Cells to Image Using Aspose.Cells .NET: A Step-by-Step Guide](/cells/english/net/import-export/export-excel-cells-to-image-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}