---
category: general
date: 2026-10-01
description: เพิ่มแผนภูมิลงใน Word ด้วย Aspose เพียงไม่กี่นาที เรียนรู้การฝังแผนภูมิ
  Excel ใน Word, การส่งออกแผนภูมิจาก Excel ไปยัง Word, การสร้างเอกสาร Word ด้วย Aspose,
  และการบันทึกแผนภูมิในเอกสาร Word.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add chart to word
- embed excel chart word
- export chart excel word
- create word document aspose
- save chart word document
language: th
lastmod: 2026-10-01
og_description: เพิ่มแผนภูมิลงใน Word ด้วย Aspose ภายในไม่กี่นาที คู่มือนี้แสดงวิธีฝังแผนภูมิ
  Excel ใน Word, ส่งออกแผนภูมิจาก Excel ไปยัง Word, สร้างเอกสาร Word ด้วย Aspose,
  และบันทึกแผนภูมิในเอกสาร Word.
og_image_alt: Screenshot illustrating how to add chart to Word using Aspose
og_title: เพิ่มแผนภูมิลงใน Word ด้วย Aspose – ฝังแผนภูมิ Excel
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Add chart to Word with Aspose in just minutes. Learn to embed Excel
    chart in Word, export chart Excel Word, create Word document Aspose, and save
    chart Word document.
  headline: How to add chart to Word with Aspose – embed Excel chart
  type: TechArticle
- description: Add chart to Word with Aspose in just minutes. Learn to embed Excel
    chart in Word, export chart Excel Word, create Word document Aspose, and save
    chart Word document.
  name: How to add chart to Word with Aspose – embed Excel chart
  steps:
  - name: '**Loading the workbook** – `Workbook` parses the Excel file and gives you
      programmatic access to its worksheets and charts.'
    text: '**Loading the workbook** – `Workbook` parses the Excel file and gives you
      programmatic access to its worksheets and charts.'
  - name: '**Creating the Word document** – `Document` is the Aspose.Words entry point
      for any Word‑processing task.'
    text: '**Creating the Word document** – `Document` is the Aspose.Words entry point
      for any Word‑processing task.'
  - name: '**DocumentBuilder** – This helper class lets you insert content (text,
      images, charts) at the current cursor position.'
    text: '**DocumentBuilder** – This helper class lets you insert content (text,
      images, charts) at the current cursor position.'
  - name: '**InsertChart** – The overload that accepts an `Aspose.Cells.Chart` object
      copies the chart’s data, formatting, and series directly into the Word file.
      No intermediate image conversion is required, preserving vector quality.'
    text: '**InsertChart** – The overload that accepts an `Aspose.Cells.Chart` object
      copies the chart’s data, formatting, and series directly into the Word file.
      No intermediate image conversion is required, preserving vector quality.'
  - name: '**Save** – `Save` writes the .docx package to disk, completing the **save
      chart word document** step.'
    text: '**Save** – `Save` writes the .docx package to disk, completing the **save
      chart word document** step.'
  type: HowTo
tags:
- Aspose
- C#
- Word automation
title: วิธีเพิ่มแผนภูมิลงใน Word ด้วย Aspose – ฝังแผนภูมิ Excel
url: /th/net/chart-rendering-and-conversion/how-to-add-chart-to-word-with-aspose-embed-excel-chart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีเพิ่มแผนภูมิลงใน Word ด้วย Aspose – ฝังแผนภูมิ Excel

หากคุณต้องการ **เพิ่มแผนภูมิลงใน Word** อย่างรวดเร็ว บทแนะนำนี้จะให้โซลูชันที่พร้อมใช้งานและทำงานได้ทันที คุณจะได้เห็นวิธีฝังแผนภูมิ Excel ลงในไฟล์ Word, ส่งออกแผนภูมิจาก Excel ไปยัง Word, และสุดท้าย **บันทึกเอกสาร Word ที่มีแผนภูมิ** เพียงไม่กี่บรรทัดของ C#.

การฝังแผนภูมิมักเป็นความต้องการทั่วไปเมื่อคุณสร้างรายงาน, ใบแจ้งหนี้ หรือแดชบอร์ดโดยอัตโนมัติ ภายในคู่มือนี้ คุณจะสามารถ **สร้างเอกสาร Word ด้วย Aspose** ที่มีแผนภูมิใด ๆ จากเวิร์กบุ๊ก Excel ได้โดยไม่ต้องคัดลอก‑วางด้วยมือ

## ข้อกำหนดเบื้องต้น

- .NET 6.0 หรือใหม่กว่า (โค้ดนี้ยังทำงานได้กับ .NET Framework 4.7+)
- แพคเกจ NuGet ของ Aspose.Cells และ Aspose.Words (ติดตั้งด้วย `dotnet add package Aspose.Cells` และ `dotnet add package Aspose.Words`)
- ไฟล์ Excel ที่มีอยู่แล้ว (`Chart.xlsx`) ซึ่งต้องมีอย่างน้อยหนึ่งแผนภูมิ
- สภาพแวดล้อมการพัฒนา เช่น Visual Studio 2022 หรือ VS Code

## เพิ่มแผนภูมิลงใน Word ด้วย Aspose

ด้านล่างเป็นโปรแกรมเต็มรูปแบบที่ทำงานได้เอง คัดลอกไปยังโปรเจกต์คอนโซลใหม่, ทำการ restore แพคเกจ, แล้วรัน โปรแกรมจะโหลดเวิร์กบุ๊ก Excel, สร้างเอกสาร Word, แทรกแผนภูมิแรก, และบันทึกผลลัพธ์

```csharp
using System;
using Aspose.Cells;
using Aspose.Words;
using Aspose.Words.Drawing;

namespace AddChartToWordDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Load the Excel workbook that contains the chart
            var workbookPath = @"YOUR_DIRECTORY\Chart.xlsx";
            var workbook = new Workbook(workbookPath);

            // Step 2: Create a new Word document that will receive the chart
            var wordDoc = new Document();

            // Step 3: Initialise a DocumentBuilder for the Word document
            var builder = new DocumentBuilder(wordDoc);

            // Step 4: Insert the first chart from the first worksheet into the Word document
            // This uses Aspose.Words' InsertChart overload that accepts an Aspose.Cells chart object
            builder.InsertChart(workbook.Worksheets[0].Charts[0]);

            // Step 5: Save the resulting Word document
            var outputPath = @"YOUR_DIRECTORY\Chart.docx";
            wordDoc.Save(outputPath);

            Console.WriteLine($"Chart successfully added and saved to '{outputPath}'.");
        }
    }
}
```

### ทำไมแต่ละบรรทัดจึงสำคัญ

1. **Loading the workbook** – `Workbook` ทำการพาร์สไฟล์ Excel และให้คุณเข้าถึง worksheets และ charts ได้แบบโปรแกรมเมติก  
2. **Creating the Word document** – `Document` เป็นจุดเริ่มต้นของ Aspose.Words สำหรับงานประมวลผล Word ใด ๆ  
3. **DocumentBuilder** – คลาสช่วยเหลือนี้ทำให้คุณแทรกเนื้อหา (ข้อความ, รูปภาพ, แผนภูมิ) ที่ตำแหน่งเคอร์เซอร์ปัจจุบันได้  
4. **InsertChart** – overload ที่รับอ็อบเจ็กต์ `Aspose.Cells.Chart` จะคัดลอกข้อมูล, การจัดรูปแบบ, และ series ของแผนภูมิเข้าไปในไฟล์ Word โดยตรง ไม่ต้องแปลงเป็นภาพกลางใด ๆ ทำให้คุณภาพเวกเตอร์คงอยู่  
5. **Save** – `Save` จะเขียนแพ็กเกจ .docx ลงดิสก์, เสร็จสิ้นขั้นตอน **save chart word document**

#### ผลลัพธ์ที่คาดหวัง

หลังจากรันโปรแกรมแล้ว, เปิด `Chart.docx` คุณจะเห็นแผนภูมิเดียวกันที่ถูกเก็บไว้ใน `Chart.xlsx` ปรากฏที่ตำแหน่งที่ builder ถูกวาง (จุดเริ่มต้นของเอกสาร) แผนภูมอยังคงแก้ไขได้เต็มที่ใน Word (คุณสามารถปรับขนาด, เปลี่ยนสี, หรือแก้ไขแหล่งข้อมูล)

## ฝังแผนภูมิ Excel ลงใน Word

หากต้องการฝังหลายแผนภูมิ ให้เรียก `InsertChart` ซ้ำสำหรับแต่ละอ็อบเจ็กต์แผนภูมิ ตัวอย่างเช่น การฝังแผนภูมิทั้งหมดจาก worksheet แรก:

```csharp
var sheet = workbook.Worksheets[0];
foreach (Chart chart in sheet.Charts)
{
    builder.InsertChart(chart);
    builder.Writeln(); // add a line break between charts
}
```

**เคล็ดลับ:** ใช้ `builder.Writeln()` เพื่อแทรกการขึ้นบรรทัดใหม่, ทำให้แต่ละแผนภูมิเริ่มที่บรรทัดใหม่

## ส่งออกแผนภูมิ Excel Word – จัดการหลาย Worksheet

เมื่อแผนภูมิกระจายอยู่หลาย worksheet, ให้วนลูปผ่านคอลเลกชัน `Worksheets` ของเวิร์กบุ๊ก:

```csharp
foreach (Worksheet ws in workbook.Worksheets)
{
    foreach (Chart chart in ws.Charts)
    {
        builder.InsertChart(chart);
        builder.Writeln();
    }
}
```

วิธีนี้ทำ **export chart Excel Word** สำหรับโครงสร้างเวิร์กบุ๊กใด ๆ ทำให้โซลูชันทนทานต่อรายงานที่ซับซ้อน

## สร้างเอกสาร Word Aspose – ปรับแต่งลักษณะ

คุณสามารถควบคุมขนาดและตำแหน่งของแต่ละแผนภูมิที่แทรกโดยแก้ไข `Shape` ที่คืนค่าจาก `InsertChart`:

```csharp
Shape chartShape = builder.InsertChart(chart);
chartShape.Width = 500;   // width in points
chartShape.Height = 300;  // height in points
chartShape.WrapType = WrapType.Inline; // make the chart flow with text
```

การตั้งค่า `WrapType` เป็น `Inline` จะทำให้แผนภูมิโปร่งเป็นย่อหน้าปกติ, ซึ่งมักต้องการสำหรับการสร้างเอกสารอัตโนมัติ

## บันทึกเอกสาร Word ที่มีแผนภูมิ – แนวทางปฏิบัติที่ดีที่สุด

- **ใช้ชื่อไฟล์ที่บ่งบอก** (`Report_Q1_2026.docx`) เพื่อให้ง่ายต่อการเวอร์ชัน  
- **Dispose objects** เมื่อเสร็จ, โดยเฉพาะในกระบวนการแบตช์ขนาดใหญ่:

```csharp
wordDoc.Dispose();
workbook.Dispose();
```

- **Validate the result** ด้วยโค้ด หากคุณสร้างไฟล์จำนวนมาก:

```csharp
if (System.IO.File.Exists(outputPath))
{
    Console.WriteLine("File saved successfully.");
}
else
{
    Console.Error.WriteLine("Failed to save the document.");
}
```

## คำถามที่พบบ่อย & กรณีขอบ

| Question | Answer |
|----------|--------|
| *Can I insert a chart that is not the first one on the sheet?* | ใช่. เข้าถึงโดยใช้ดัชนี: `sheet.Charts[2]` สำหรับแผนภูมิที่สาม |
| *What if the Excel chart uses a data source that isn’t in the workbook?* | Aspose.Cells ฝังข้อมูลโดยตรงลงในอ็อบเจ็กต์แผนภูมิ, ดังนั้นแผนภูมิยังทำงานได้แม้แหล่งข้อมูลจะถูกลบออก |
| *Do I need a license for Aspose?* | สามารถใช้รุ่นประเมินได้ฟรี, แต่เวอร์ชันที่มีลิขสิทธิ์จะลบลายน้ำและเปิดฟีเจอร์เต็ม |
| *Will the chart be editable in Word after insertion?* | แผนภูมิถูกแทรกเป็นแผนภูมิ Word ดั้งเดิม, ผู้ใช้จึงแก้ไข series, ชื่อเรื่อง, และสไตล์ได้ผ่าน UI ของ Word |
| *How to insert a chart as a picture instead of a native chart?* | ใช้ `builder.InsertImage(chart.ToImage())` เพื่อฝังเป็นภาพ raster. วิธีนี้เหมาะเมื่อคุณต้องการรักษาการแสดงผลที่แม่นยำโดยไม่ต้องการให้แก้ไขในระดับ Word |

## ตัวอย่างทำงานเต็ม (copy‑paste)

```csharp
using System;
using Aspose.Cells;
using Aspose.Words;
using Aspose.Words.Drawing;

class AddChartToWord
{
    static void Main()
    {
        // Load Excel workbook
        var wb = new Workbook(@"C:\Data\Chart.xlsx");

        // Create Word document
        var doc = new Document();
        var builder = new DocumentBuilder(doc);

        // Insert every chart from every worksheet
        foreach (Worksheet ws in wb.Worksheets)
        {
            foreach (Chart ch in ws.Charts)
            {
                Shape shape = builder.InsertChart(ch);
                shape.Width = 500;
                shape.Height = 300;
                builder.Writeln(); // separate charts
            }
        }

        // Save the document
        var outPath = @"C:\Data\ReportWithCharts.docx";
        doc.Save(outPath);
        Console.WriteLine($"Document saved to {outPath}");
    }
}
```

เมื่อรันโค้ดจะสร้างไฟล์ Word (`ReportWithCharts.docx`) ที่มีผลลัพธ์ **add chart to word** สำหรับทุกแผนภูมิในเวิร์กบุ๊กต้นฉบับ

## สรุป

ตอนนี้คุณรู้วิธี **add chart to Word** ด้วย Aspose.Cells และ Aspose.Words, วิธี **embed Excel chart word**, **export chart Excel Word**, **create Word document Aspose**, และสุดท้าย **save chart word document**. วิธีนี้ทำงานได้ทั้งกรณีแผนภูมิเดียวและเวิร์กบุ๊กที่ซับซ้อนพร้อมแผนภูมิหลายรายการบนหลาย worksheet

ขั้นตอนต่อไปที่คุณอาจสนใจสำรวจ:

- ปรับสไตล์แผนภูมิที่แทรก (สี, ฟอนต์) ผ่าน API `Chart`  
- ผสานการแทรกแผนภูมิพร้อมการสร้างข้อความเพื่อผลิตรายงานอัตโนมัติเต็มรูปแบบ  
- ใช้ Aspose.Slides หากคุณต้องการ

## What Should You Learn Next?

The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Save DOCX from Excel – Complete Guide to Export Charts to Word](/cells/english/net/converting-excel-files-to-other-formats/how-to-save-docx-from-excel-complete-guide-to-export-charts/)
- [Create Excel Workbook with Pie Chart Using Aspose.Cells .NET - Comprehensive Guide](/cells/english/net/charts-graphs/create-excel-workbook-pie-chart-aspose-cells-net/)
- [Create a Bubble Chart in Excel Using Aspose.Cells .NET&#58; A Step-by-Step Guide](/cells/english/net/charts-graphs/create-bubble-chart-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}