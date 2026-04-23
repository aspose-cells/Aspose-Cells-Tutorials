---
category: general
date: 2026-02-26
description: ส่งออกแผนภูมิจาก Excel ไปยัง PowerPoint ด้วย C#. เรียนรู้วิธีแปลง Excel
  เป็น PowerPoint, บันทึก Excel เป็น PowerPoint และทำให้รูปทรงยังแก้ไขได้
draft: false
keywords:
- export chart to powerpoint
- convert excel to powerpoint
- save excel as powerpoint
- how to convert excel to ppt
- save workbook as pptx
language: th
og_description: ส่งออกแผนภูมิไปยัง PowerPoint จาก Excel ด้วย C# คู่มือนี้แสดงวิธีแปลง
  Excel เป็น PowerPoint บันทึกเวิร์กบุ๊กเป็นไฟล์ PPTX และทำให้รูปทรงยังคงแก้ไขได้
og_title: ส่งออกแผนภูมิไปยัง PowerPoint ด้วย C# – บทเรียนการเขียนโปรแกรมเต็มรูปแบบ
tags:
- Aspose.Cells
- C#
- Office Automation
title: ส่งออกแผนภูมิไปยัง PowerPoint ด้วย C# – คู่มือขั้นตอนเต็ม
url: /th/net/chart-rendering-and-conversion/export-chart-to-powerpoint-with-c-complete-step-by-step-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ส่งออกแผนภูมิไปยัง PowerPoint – บทเรียนการเขียนโปรแกรมแบบครบถ้วน

เคยสงสัยไหมว่า **ส่งออกแผนภูมิไปยัง PowerPoint** อย่างไรโดยไม่สูญเสียความสามารถในการแก้ไข? ในหลายกรณีของการรายงานคุณต้องการแผนภูมิที่ยังคงเป็นแบบไดนามิกภายในสไลด์เด็ค แต่การคัดลอกและวางด้วยมือเป็นเรื่องน่าเบื่อ ข่าวดีคือคุณสามารถทำได้โดยใช้โค้ด C# เพียงไม่กี่บรรทัด

ในคู่มือนี้เราจะเดินผ่านกระบวนการทั้งหมด: ตั้งแต่การโหลดไฟล์ Excel ที่มีแผนภูมิพร้อมกับกล่องข้อความ, การกำหนดค่าการส่งออกเพื่อให้กล่องข้อความและรูปร่างยังคงแก้ไขได้, และสุดท้ายการบันทึกผลลัพธ์เป็นไฟล์ **PowerPoint**. เมื่อเสร็จสิ้นคุณจะรู้วิธี **แปลง Excel เป็น PowerPoint**, **บันทึก Excel เป็น PowerPoint**, และแม้กระทั่งปรับตัวเลือกสำหรับกรณีขอบที่ซับซ้อน

## สิ่งที่คุณต้องมี

- **Aspose.Cells for .NET** (เวอร์ชัน 23.10 หรือใหม่กว่า) เป็นไลบรารีที่ทำให้การแปลงเป็นเรื่องง่าย
- **.NET 6+** runtime – SDK ใดก็ได้ที่เป็นรุ่นล่าสุด
- ไฟล์ Excel อย่างง่าย (`ChartWithTextbox.xlsx`) ที่มีอย่างน้อยหนึ่งแผนภูมิและกล่องข้อความ
- Visual Studio หรือ IDE ที่คุณชื่นชอบ

ไม่จำเป็นต้องติดตั้งแพ็กเกจ NuGet เพิ่มเติมนอกจาก Aspose.Cells, แต่การมีความเข้าใจพื้นฐานเกี่ยวกับไวยากรณ์ C# จะช่วยได้มาก

## ส่งออกแผนภูมิไปยัง PowerPoint – ขั้นตอนโดยละเอียด

ด้านล่างเราจะแบ่งวิธีแก้เป็นขั้นตอนที่แยกจากกันและง่ายต่อการทำตาม แต่ละขั้นตอนจะมีโค้ดที่ต้องใช้พร้อมกับย่อหน้าสั้น ๆ ที่อธิบาย “ทำไม” ของแต่ละขั้นตอน

### ขั้นตอนที่ 1: โหลดเวิร์กบุ๊ก Excel ที่มีแผนภูมิ

ก่อนอื่นเราต้องนำไฟล์ต้นทางเข้ามาในหน่วยความจำ การใช้ `Workbook` จาก Aspose.Cells จะอ่านสเปรดชีตทั้งหมดรวมถึงแผนภูมิ, รูปภาพ, และออบเจ็กต์ฝังอยู่

```csharp
using Aspose.Cells;

// Step 1: Load the Excel workbook that contains the chart with a textbox
Workbook workbook = new Workbook(@"C:\Samples\ChartWithTextbox.xlsx");

// Verify that the workbook actually contains a chart
if (workbook.Worksheets[0].Charts.Count == 0)
{
    throw new InvalidOperationException("No chart found in the first worksheet.");
}
```

*ทำไมจึงสำคัญ:* หากเปิดเวิร์กบุ๊กโดยไม่ได้ระบุพาธอย่างถูกต้อง คุณจะได้รับ `FileNotFoundException`. การตรวจสอบอย่างรวดเร็วนี้ช่วยป้องกันไม่ให้คุณส่งออกสไลด์เปล่าในภายหลัง

### ขั้นตอนที่ 2: เตรียมตัวเลือกการนำเสนอเพื่อให้รูปร่างแก้ไขได้

Aspose.Cells ให้คุณกำหนดได้ว่ากล่องข้อความ, รูปร่าง, และแม้แต่แผนภูมิเองจะคง **editable** หลังการส่งออกหรือไม่ การตั้งค่า `ExportTextBoxes` และ `ExportShapes` เป็น `true` จะทำให้วัตถุเหล่านั้นถูกเก็บเป็นองค์ประกอบ PowerPoint ดั้งเดิมแทนที่จะถูกแปลงเป็นภาพคงที่

```csharp
using Aspose.Cells.Drawing;

// Step 2: Set up presentation options to keep textboxes and shapes editable in the output
PresentationOptions presentationOptions = new PresentationOptions
{
    ExportTextBoxes = true, // Preserve editable textboxes
    ExportShapes    = true  // Preserve shapes such as the chart itself
};
```

*ทำไมจึงสำคัญ:* หากคุณปล่อยให้แฟล็กเหล่านี้อยู่ที่ค่าเริ่มต้น (`false`), สไลด์ที่ได้จะเป็นบิตแมปของแผนภูมิ ทำให้แก้ไขซีรีส์หรือเปลี่ยนคำบรรยายได้ยากในภายหลัง การเปิดใช้งานทั้งสองตัวเลือกจะให้คุณได้แผนภูมิ PowerPoint ที่ทำงานเหมือนที่คุณวาดด้วยมือ

### ขั้นตอนที่ 3: แปลง Excel เป็น PowerPoint และบันทึกไฟล์

ต่อไปเราจะเรียกเมธอด `Save` พร้อมส่งค่า `SaveFormat.Pptx` และตัวเลือกที่เราตั้งค่าไว้ ไลบรารีจะดูแลการแปลงออบเจ็กต์แผนภูมิจาก Excel ให้เป็นรูปร่างแผนภูมิของ PowerPoint

```csharp
// Step 3: Save the workbook as a PowerPoint presentation using the configured options
workbook.Save(@"C:\Samples\Result.pptx", SaveFormat.Pptx, presentationOptions);
```

*ทำไมจึงสำคัญ:* คำสั่ง `Save` ทำงานหนักทั้งหมด—แมปซีรีส์จาก Excel ไปยัง PowerPoint, รักษาการจัดรูปแบบแกน, และคัดลอกกล่องข้อความที่เชื่อมโยง หลังจากบรรทัดนี้ทำงานเสร็จ คุณจะได้ไฟล์ `.pptx` ที่แก้ไขได้เต็มที่พร้อมเปิดใน Microsoft PowerPoint

### ตรวจสอบผลลัพธ์

เปิด `Result.pptx` ใน PowerPoint คุณควรเห็นสไลด์ที่มี:

- แผนภูมิดั้งเดิมที่ยังคงเชื่อมโยงกับข้อมูล (คุณสามารถดับเบิล‑คลิกเพื่อแก้ไขซีรีส์)
- กล่องข้อความใด ๆ ที่อยู่ในชีต Excel, ตอนนี้เป็นกล่องข้อความ PowerPoint ดั้งเดิม
- รูปแบบสไลด์ถูกเลือกโดยอัตโนมัติ (โดยทั่วไปจะเป็นสไลด์เปล่า)

หากพบว่ามีส่วนใดหายไป ให้ตรวจสอบว่าเวิร์กบุ๊กต้นทางมีวัตถุที่มองเห็นจริงและว่าได้ตั้งค่า `ExportTextBoxes` / `ExportShapes` เป็น `true` แล้วหรือยัง

### แปลง Excel เป็น PowerPoint: จัดการหลายแผ่นงาน

บ่อยครั้งที่เวิร์กบุ๊กมีหลายชีต, แต่ละชีตมีแผนภูมิของตนเอง โดยค่าเริ่มต้น Aspose.Cells จะส่งออก **ทั้งหมด** ของ **ทุก** แผ่นงานเป็นสไลด์แยกกัน หากคุณต้องการเพียงบางส่วน สามารถกรองก่อนบันทึกได้:

```csharp
// Example: Export only charts from the first worksheet
Worksheet firstSheet = workbook.Worksheets[0];
foreach (Chart chart in firstSheet.Charts)
{
    chart.IsVisible = true; // Ensure visibility
}

// Hide charts from other sheets
for (int i = 1; i < workbook.Worksheets.Count; i++)
{
    foreach (Chart chart in workbook.Worksheets[i].Charts)
    {
        chart.IsVisible = false;
    }
}
```

*เคล็ดลับ:* การตั้งค่า `chart.IsVisible = false` มีค่าใช้จ่ายน้อยกว่าการลบแผนภูมิออกโดยสิ้นเชิง และทำให้คุณสลับการรวมแผนภูมิได้โดยไม่ต้องแก้ไขไฟล์ต้นฉบับ

### บันทึก Excel เป็น PowerPoint – ปรับขนาดสไลด์

PowerPoint มีขนาดสไลด์เริ่มต้นที่ 10‑inch x 5.63‑inch หากแผนภูมิของคุณดูแออัด คุณสามารถเปลี่ยนมิติของสไลด์ผ่านอ็อบเจ็กต์ `PresentationOptions`:

```csharp
presentationOptions.SlideSize = new SizeF(13.33f, 7.5f); // 16:9 widescreen
```

ตอนนี้แผนภูมิที่ส่งออกจะมีพื้นที่ว่างมากขึ้น, และกล่องข้อความใด ๆ จะคงรูปแบบต้นฉบับไว้

### วิธีแปลง Excel เป็น PPT: จัดการกับวัตถุที่ซ่อนอยู่

แถว, คอลัมน์, หรือรูปร่างที่ซ่อนอยู่บางครั้งอาจแทรกเข้ามาในการส่งออก เพื่อกำจัดออกให้ทำความสะอาดอย่างรวดเร็วก่อนบันทึก:

```csharp
// Remove hidden rows/columns that might affect chart layout
foreach (Worksheet sheet in workbook.Worksheets)
{
    sheet.Cells.HideRows = false;
    sheet.Cells.HideColumns = false;
}
```

ขั้นตอนนี้ไม่จำเป็นเสมอไป, แต่ช่วยป้องกันช่องว่างที่ไม่คาดคิดในสไลด์เด็คสุดท้ายของคุณ

### บันทึกเวิร์กบุ๊กเป็น PPTX – ตัวอย่างทำงานเต็มรูปแบบ

รวมทุกอย่างเข้าด้วยกัน นี่คือโปรแกรมคอนโซลที่พร้อมรันเพื่อสาธิตกระบวนการทั้งหมด:

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing; // For SizeF

class ExportChartDemo
{
    static void Main()
    {
        // Load workbook (Step 1)
        string sourcePath = @"C:\Samples\ChartWithTextbox.xlsx";
        Workbook workbook = new Workbook(sourcePath);

        // Verify chart existence
        if (workbook.Worksheets[0].Charts.Count == 0)
        {
            Console.WriteLine("No chart found. Exiting.");
            return;
        }

        // Configure presentation options (Step 2)
        PresentationOptions options = new PresentationOptions
        {
            ExportTextBoxes = true,
            ExportShapes    = true,
            SlideSize       = new SizeF(13.33f, 7.5f) // optional widescreen
        };

        // Optional: export only first worksheet charts
        for (int i = 1; i < workbook.Worksheets.Count; i++)
        {
            foreach (Chart c in workbook.Worksheets[i].Charts)
                c.IsVisible = false;
        }

        // Save as PowerPoint (Step 3)
        string targetPath = @"C:\Samples\Result.pptx";
        workbook.Save(targetPath, SaveFormat.Pptx, options);

        Console.WriteLine($"Export complete! File saved to {targetPath}");
    }
}
```

การรันโปรแกรมนี้จะสร้าง `Result.pptx` ที่มีแผนภูมิและกล่องข้อความที่แก้ไขได้, เหมือนกับที่คุณคาดหวังเมื่อ **บันทึกเวิร์กบุ๊กเป็น pptx** ด้วยตนเอง

![ส่งออกแผนภูมิไปยัง PowerPoint ตัวอย่าง](/images/export-chart-to-powerpoint.png "ส่งออกแผนภูมิไปยัง PowerPoint – สไลด์ที่แก้ไขได้")

## คำถามทั่วไป & กรณีขอบ

**ถ้าไฟล์ Excel มีแผนภูมิที่เชื่อมโยงกับแหล่งข้อมูลภายนอกจะทำอย่างไร?**  
Aspose.Cells จะคัดลอกค่าข้อมูล *ปัจจุบัน* ไปยังแผนภูมิ PowerPoint. มัน **ไม่** รักษาการเชื่อมโยงภายนอกไว้, เนื่องจาก PowerPoint ไม่สามารถอ้างอิงการเชื่อมต่อข้อมูล Excel ในลักษณะเดียวกันได้. หากต้องการอัปเดตแบบเรียลไทม์, พิจารณาแทรกไฟล์ Excel ดั้งเดิมลงใน PPTX เป็นอ็อบเจ็กต์ OLE แทน

**ฉันสามารถส่งออกแผนภูมิที่ใช้ธีมกำหนดเองได้หรือไม่?**  
ทำได้. ไลบรารีพยายามแมปสีธีมของ Excel ไปยังช่องสีของธีม PowerPoint. สำหรับพาเลตที่กำหนดเองอย่างมาก คุณอาจต้องปรับสีหลังการส่งออกโดยใช้ API ของ PowerPoint (เช่น Aspose.Slides)

**มีขีดจำกัดจำนวนแผนภูมิหรือไม่?**  
โดยปฏิบัติไม่มี—Aspose.Cells ทำการสตรีมข้อมูล, ดังนั้นแม้เวิร์กบุ๊กจะมีหลายสิบแผนภูมิก็ยังส่งออกได้, แม้ว่าขนาดไฟล์ PPTX จะเพิ่มขึ้นตามเชิงเส้น

**ต้องมีลิขสิทธิ์สำหรับ Aspose.Cells หรือไม่?**  
รุ่นประเมินฟรีทำงานได้, แต่จะใส่ลายน้ำบนสไลด์แรก. สำหรับการใช้งานจริง ควรซื้อไลเซนส์เพื่อเอาลายน้ำออกและเปิดประสิทธิภาพเต็มที่

## สรุป

เราได้ครอบคลุมวิธี **ส่งออกแผนภูมิไปยัง PowerPoint** ด้วย C#, แสดงโค้ดที่จำเป็นสำหรับการโหลดเวิร์กบุ๊ก Excel, การกำหนด `PresentationOptions` เพื่อให้กล่องข้อความและรูปร่างแก้ไขได้, และสุดท้ายการบันทึกผลลัพธ์เป็นไฟล์ `.pptx`. คุณยังได้เรียนรู้วิธี **แปลง Excel เป็น PowerPoint**, **บันทึก Excel เป็น PowerPoint**, และตอบคำถาม “**วิธีแปลง Excel เป็น ppt**” ด้วยตัวอย่างที่ทำงานได้เต็มรูปแบบ

## ต่อไปคืออะไร?

- **บันทึกเวิร์กบุ๊กเป็น PPTX** พร้อมหลายสไลด์: วนลูปผ่านแต่ละชีตและเรียก `Save` พร้อม `PresentationOptions` สำหรับแต่ละชีต
- สำรวจ **Aspose.Slides** หากต้องการแก้ไข PPTX ที่สร้างขึ้นเพิ่มเติม (เพิ่มทรานซิชัน, โน้ตผู้พูด ฯลฯ)
- ลองส่งออก **pivot chart** หรือ **3‑D chart**—ตัวเลือกเดียวกันใช้ได้, แต่คุณอาจต้องปรับการจัดรูปแบบแกนหลังการส่งออก

หากพบปัญหาใด ๆ อย่าลังเลที่จะแสดงความคิดเห็นด้านล่างหรือดูเอกสารอย่างเป็นทางการของ Aspose.Cells สำหรับการเปลี่ยนแปลง API ล่าสุด. Happy coding, และสนุกกับการเปลี่ยนแผนภูมิ Excel ให้เป็นงานนำเสนอ PowerPoint ที่ดูเป็นมืออาชีพด้วยเพียงไม่กี่บรรทัดของ C#!

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}