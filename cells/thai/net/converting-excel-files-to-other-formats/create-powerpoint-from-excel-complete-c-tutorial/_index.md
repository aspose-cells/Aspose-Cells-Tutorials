---
category: general
date: 2026-02-21
description: สร้าง PowerPoint จาก Excel อย่างรวดเร็ว เรียนรู้วิธีส่งออก Excel ไปยัง
  PowerPoint พร้อมข้อความและแผนภูมิที่แก้ไขได้โดยใช้ Aspose.Cells เพียงไม่กี่บรรทัดของ
  C#
draft: false
keywords:
- create powerpoint from excel
- export excel to powerpoint
- export editable text
- export excel chart powerpoint
- convert excel chart powerpoint
language: th
og_description: สร้าง PowerPoint จาก Excel พร้อมข้อความและแผนภูมิที่แก้ไขได้ ทำตามคู่มือโดยละเอียดนี้เพื่อส่งออก
  Excel ไปยัง PowerPoint ด้วย Aspose.Cells.
og_title: สร้าง PowerPoint จาก Excel – คู่มือ C# ทีละขั้นตอน
tags:
- C#
- Aspose.Cells
- PowerPoint
- Excel Automation
title: สร้าง PowerPoint จาก Excel – บทเรียน C# ฉบับสมบูรณ์
url: /th/net/converting-excel-files-to-other-formats/create-powerpoint-from-excel-complete-c-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# สร้าง PowerPoint จาก Excel – คำแนะนำ C# ฉบับสมบูรณ์

เคยต้องการ **create PowerPoint from Excel** แต่ไม่แน่ใจว่าจะใช้ API ไหนหรือไม่? คุณไม่ได้เป็นคนเดียว นักพัฒนาหลายคนเจออุปสรรคเมื่ออยากแปลง worksheet ที่เต็มไปด้วยข้อมูลให้เป็นสไลด์ที่ดูเป็นมืออาชีพ โดยเฉพาะเมื่อพวกเขาต้องการให้กล่องข้อความยังคงแก้ไขได้หลังการแปลง  

ในคู่มือนี้ เราจะสาธิตวิธี **export Excel to PowerPoint** พร้อมคงไว้ซึ่งข้อความที่แก้ไขได้ ความแม่นยำของแผนภูมิ และการจัดวาง — ทั้งหมดด้วยไม่กี่บรรทัดของ C# เมื่อเสร็จคุณจะได้ไฟล์ PPTX ที่พร้อมใช้งานซึ่งคุณสามารถปรับแต่งใน PowerPoint ได้เช่นเดียวกับสไลด์ที่สร้างด้วยมือ

## สิ่งที่คุณจะได้เรียนรู้

- วิธีโหลด Excel workbook ที่มีแผนภูมิและรูปร่าง.  
- วิธีกำหนดค่า `PresentationExportOptions` เพื่อให้กล่องข้อความยังคงแก้ไขได้ (`export editable text`).  
- วิธี **export Excel chart PowerPoint** อย่างแท้จริงและได้สไลด์เด็คที่สะอาด.  
- การปรับเปลี่ยนเล็กน้อยที่คุณสามารถใช้เมื่อจำเป็นต้อง **convert Excel chart PowerPoint** สำหรับการตั้งค่าหน้าต่างต่าง ๆ หรือหลาย worksheet.  

### ข้อกำหนดเบื้องต้น

- สภาพแวดล้อมการพัฒนา .NET (Visual Studio 2022 หรือใหม่กว่า).  
- Aspose.Cells for .NET (รุ่นทดลองฟรีหรือเวอร์ชันที่มีลิขสิทธิ์).  
- ไฟล์ Excel (`ChartWithShape.xlsx`) ที่มีอย่างน้อยหนึ่งแผนภูมิและรูปร่างที่คุณต้องการให้คงแก้ไขได้.  

หากคุณมีทั้งหมดนี้แล้ว มาเริ่มกันเลย—ไม่มีเนื้อหาเกินความจำเป็น เพียงโซลูชันที่ใช้งานได้จริง

## สร้าง PowerPoint จาก Excel – ขั้นตอนทีละขั้น

ด้านล่างแต่ละขั้นตอน เราจะใส่โค้ดสั้น ๆ อธิบาย **ทำไม** เราถึงทำเช่นนั้นและชี้ให้เห็นข้อผิดพลาดทั่วไป อย่าลังเลที่จะคัดลอก‑วางตัวอย่างเต็มที่ด้านล่างของหน้า

### ขั้นตอน 1: โหลด Excel Workbook

ก่อนอื่นเราต้องโหลด workbook ต้นฉบับเข้าสู่หน่วยความจำ Aspose.Cells จะอ่านไฟล์และสร้างโมเดลวัตถุที่สมบูรณ์เพื่อให้เราสามารถจัดการได้

```csharp
// Step 1: Load the Excel workbook that contains the chart and shape
Workbook workbook = new Workbook("YOUR_DIRECTORY/ChartWithShape.xlsx");

// Quick sanity check – make sure the workbook actually loaded
if (workbook.Worksheets.Count == 0)
    throw new InvalidOperationException("The workbook appears to be empty.");
```

**ทำไมเรื่องนี้สำคัญ:**  
การโหลด workbook เป็นพื้นฐาน หากเส้นทางไฟล์ผิดหรือ workbook เสียหาย ขั้นตอน `export excel to powerpoint` ถัดไปทั้งหมดจะล้มเหลว การตรวจสอบความสมบูรณ์จะให้ฟีดแบ็กตั้งแต่ต้นแทนข้อความ “file not found” ที่ไม่ชัดเจนในภายหลัง

### ขั้นตอน 2: เตรียม Export Options

Aspose.Cells จะให้คุณใช้วัตถุ `PresentationExportOptions` ที่ควบคุมลักษณะของ PPTX นี่คือจุดที่คุณตัดสินใจว่าต้องการให้ข้อความยังคงแก้ไขได้หรือไม่

```csharp
// Step 2: Create export options for PowerPoint conversion
PresentationExportOptions exportOptions = new PresentationExportOptions();

// Optional: tweak the slide size (default is 10in x 7.5in)
exportOptions.SlideSize = new SizeF(10, 7.5f);
```

**ทำไมเรื่องนี้สำคัญ:**  
หากไม่ได้กำหนดค่า `PresentationExportOptions` ไลบรารีจะใช้ค่าเริ่มต้นซึ่งอาจไม่ตรงกับเทมเพลตสไลด์ขององค์กรของคุณ การปรับขนาดสไลด์ล่วงหน้าช่วยป้องกันการต้องปรับขนาดด้วยตนเองในภายหลัง

### ขั้นตอน 3: เปิดใช้งาน Editable Text Boxes

แฟล็กพิเศษ `ExportEditableTextBoxes` บอก Aspose.Cells ให้เก็บรูปทรงข้อความใด ๆ เป็นกล่องข้อความของ PowerPoint ไม่ใช่ภาพคงที่

```csharp
// Step 3: Enable editability of text boxes in the resulting presentation
exportOptions.ExportEditableTextBoxes = true;
```

**ทำไมเรื่องนี้สำคัญ:**  
หากข้ามบรรทัดนี้ PPTX ที่ได้จะมีข้อความเป็นภาพราสเตอร์ — หมายความว่าคุณไม่สามารถแก้ไขป้ายหรือคำบรรยายใน PowerPoint ได้ การตั้งค่า `export editable text` คือกุญแจสู่สไลด์เด็คที่ใช้งานซ้ำได้จริง

### ขั้นตอน 4: ส่งออก Worksheet ไปเป็น PPTX

ตอนนี้เราจะเขียนไฟล์ PPTX จริง ๆ คุณสามารถเลือก worksheet ใดก็ได้; ที่นี่เราใช้อันแรก (`Worksheets[0]`).

```csharp
// Step 4: Export the first worksheet's page setup to a PPTX file
workbook.Worksheets[0].PageSetup.SaveToPptx("YOUR_DIRECTORY/Result.pptx", exportOptions);
```

**ทำไมเรื่องนี้สำคัญ:**  
`SaveToPptx` เคารพการตั้งค่าหน้ากระดาษ (ขอบ, แนวตั้ง/แนวนอน) ที่คุณกำหนดใน Excel ดังนั้นสไลด์จะแสดงผลเหมือนกับการจัดวางที่คุณออกแบบไว้แล้ว นี่คือหัวใจของ **export excel chart powerpoint**.

### ขั้นตอน 5: ตรวจสอบผลลัพธ์ (ไม่บังคับแต่แนะนำ)

หลังจากการแปลง เปิดไฟล์ `Result.pptx` ที่สร้างขึ้นใน PowerPoint และตรวจสอบ:

1. แผนภูมิดูคมชัดและคงข้อมูลชุดข้อมูลไว้  
2. กล่องข้อความสามารถเลือกและแก้ไขได้  
3. ขนาดสไลด์ตรงกับที่คุณคาดหวัง  

หากมีสิ่งใดไม่ตรง ให้ตรวจสอบ `exportOptions` อีกครั้ง — ตัวอย่างเช่น คุณอาจต้องตั้งค่า `exportOptions.IncludePrintArea = true` เพื่อให้เคารพพื้นที่พิมพ์ที่ตั้งชื่อไว้

```csharp
// Optional: open the PPTX automatically (requires System.Diagnostics)
System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo
{
    FileName = "YOUR_DIRECTORY/Result.pptx",
    UseShellExecute = true
});
```

### ขั้นตอน 6: การปรับเปลี่ยนขั้นสูง (ส่งออกหลาย Sheet)

บ่อยครั้งคุณอาจต้องการ **convert excel chart powerpoint** สำหรับหลาย worksheet พร้อมกัน ให้วนลูปผ่านคอลเลกชันและตั้งชื่อสไลด์แต่ละอันให้เป็นเอกลักษณ์:

```csharp
for (int i = 0; i < workbook.Worksheets.Count; i++)
{
    string outputPath = $"YOUR_DIRECTORY/Result_Sheet{i + 1}.pptx";
    workbook.Worksheets[i].PageSetup.SaveToPptx(outputPath, exportOptions);
}
```

**เคล็ดลับ:** หากคุณต้องการให้ทุก sheet อยู่ใน *ไฟล์* PPTX เดียว ให้สร้างวัตถุ `Presentation` ใหม่ นำเข้าทุกสไลด์ แล้วบันทึกครั้งเดียว นี่อาจซับซ้อนขึ้นเล็กน้อยแต่ช่วยคุณหลีกเลี่ยงการจัดการไฟล์หลายไฟล์

## ตัวอย่างทำงานเต็มรูปแบบ

นี่คือโปรแกรมทั้งหมดที่คุณสามารถคัดลอกไปวางในแอปคอนโซลและรันได้ทันที

```csharp
using System;
using System.Drawing;
using Aspose.Cells;
using Aspose.Cells.Export;

class Program
{
    static void Main()
    {
        // 1️⃣ Load workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/ChartWithShape.xlsx");
        if (workbook.Worksheets.Count == 0)
        {
            Console.WriteLine("Workbook is empty – aborting.");
            return;
        }

        // 2️⃣ Set up export options
        PresentationExportOptions exportOptions = new PresentationExportOptions
        {
            SlideSize = new SizeF(10, 7.5f),          // optional custom size
            ExportEditableTextBoxes = true           // <‑‑ keep text boxes editable
        };

        // 3️⃣ Export first worksheet
        string outputPath = "YOUR_DIRECTORY/Result.pptx";
        workbook.Worksheets[0].PageSetup.SaveToPptx(outputPath, exportOptions);
        Console.WriteLine($"PowerPoint created at: {outputPath}");

        // 4️⃣ Open the result automatically (Windows only)
        try
        {
            System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo
            {
                FileName = outputPath,
                UseShellExecute = true
            });
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Could not open PPTX automatically: {ex.Message}");
        }
    }
}
```

**ผลลัพธ์ที่คาดหวัง:**  
เมื่อคุณเปิด `Result.pptx` คุณจะเห็นสไลด์ที่สะท้อนการจัดวางของ worksheet ใน Excel แผนภูมิใด ๆ ที่คุณใส่ใน Excel จะปรากฏเป็นแผนภูมของ PowerPoint โดยตรง และคำบรรยายที่คุณเพิ่มเป็นรูปร่างจะกลายเป็นกล่องข้อความที่แก้ไขได้เต็มที่

## คำถามทั่วไป & กรณีขอบ

- **ทำงานกับ workbook ที่เปิดใช้งานแมโคร (`.xlsm`) หรือไม่?**  
  ใช่ Aspose.Cells จะอ่านแมโครแต่ไม่ทำการรัน กระบวนการแปลงจะละเว้น VBA ดังนั้นคุณยังคงได้เนื้อหาภาพรวม  

- **ถ้า worksheet ของฉันมีหลายแผนภูมิจะเป็นอย่างไร?**  
  แผนภูมิที่มองเห็นทั้งหมดจะถูกย้ายไปยังสไลด์เดียว หากคุณต้องการให้แต่ละแผนภูมิอยู่บนสไลด์แยกกัน ให้แยก worksheet หรือใช้ลูปที่แสดงในขั้นตอน 6  

- **ฉันสามารถคงธีม PowerPoint ที่กำหนดเองได้หรือไม่?**  
  ไม่ได้โดยตรงในระหว่างการส่งออก หลังจากการแปลงคุณสามารถใช้ธีมใน PowerPoint หรือโดยโปรแกรมผ่าน Aspose.Slides  

- **มีวิธีส่งออกเฉพาะช่วงที่เลือกหรือไม่?**  
  ตั้งพื้นที่พิมพ์ที่ตั้งชื่อใน Excel (`Page Layout → Print Area`) แล้วเปิด `exportOptions.IncludePrintArea = true`.  

## สรุป

ตอนนี้คุณรู้วิธี **create PowerPoint from Excel** ด้วย Aspose.Cells พร้อมการควบคุมเต็มที่บนข้อความที่แก้ไขได้ ความแม่นยำของแผนภูมิ และขนาดสไลด์ โค้ดสั้นที่เราแชร์ครอบคลุมสถานการณ์ที่พบบ่อยที่สุด และเคล็ดลับเพิ่มเติมให้ความยืดหยุ่นเมื่อคุณต้อง **export excel to powerpoint** สำหรับหลาย sheet หรือการจัดวางที่กำหนดเอง  

พร้อมสำหรับความท้าทายต่อไปหรือยัง? ลองผสานวิธีนี้กับ **Aspose.Slides** เพื่อเพิ่มการเปลี่ยนสไลด์, โน้ตผู้พูด, หรือแม้กระทั่งฝังสไลด์ที่สร้างขึ้นในงานนำเสนอที่ใหญ่ขึ้น หรือทดลองแปลง workbook ทั้งหมดเป็นชุดสไลด์หลายหน้า — เหมาะสำหรับกระบวนการรายงานอัตโนมัติ  

มีคำถามหรือพบวิธีปรับปรุงที่ชาญฉลาด? แสดงความคิดเห็นด้านล่าง แล้วขอให้เขียนโค้ดอย่างสนุก!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}