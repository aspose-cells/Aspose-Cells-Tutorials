---
category: general
date: 2026-09-21
description: ส่งออก Excel ไปยัง PowerPoint พร้อมแผนภูมิที่แก้ไขได้โดยใช้ Aspose.Cells.
  ทำตามคู่มือขั้นตอนต่อขั้นตอนนี้เพื่อแปลงแผ่นงานเป็น PPTX พร้อมคงแผนภูมิให้แก้ไขได้.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to powerpoint
- worksheet to powerpoint
- export excel chart pptx
- editable charts pptx
language: th
lastmod: 2026-09-21
og_description: ส่งออก Excel ไปยัง PowerPoint พร้อมแผนภูมิที่แก้ไขได้ด้วย Aspose.Cells
  เรียนรู้วิธีแปลงแผ่นงานเป็น PPTX พร้อมคงความสามารถในการแก้ไขแผนภูมิทั้งหมด.
og_image_alt: Screenshot of a PowerPoint slide showing an editable Excel chart after
  export
og_title: ส่งออก Excel ไปยัง PowerPoint พร้อมแผนภูมิที่แก้ไขได้ – บทเรียน C#
schemas:
- author: Aspose
  dateModified: '2026-09-21'
  description: Export Excel to PowerPoint with editable charts using Aspose.Cells.
    Follow this step‑by‑step guide to convert a worksheet to PPTX while keeping charts
    editable.
  headline: Export Excel to PowerPoint with editable charts in C#
  type: TechArticle
- description: Export Excel to PowerPoint with editable charts using Aspose.Cells.
    Follow this step‑by‑step guide to convert a worksheet to PPTX while keeping charts
    editable.
  name: Export Excel to PowerPoint with editable charts in C#
  steps:
  - name: '**Preserve chart data ranges** – Ensure the chart data source resides in
      the same worksheet you are exporting. Cross‑sheet references are converted to
      static values in the PPTX.'
    text: '**Preserve chart data ranges** – Ensure the chart data source resides in
      the same worksheet you are exporting. Cross‑sheet references are converted to
      static values in the PPTX.'
  - name: '**Use the latest Aspose.Cells version** – New releases improve support
      for additional chart features and fix edge‑case bugs related to PPTX export.'
    text: '**Use the latest Aspose.Cells version** – New releases improve support
      for additional chart features and fix edge‑case bugs related to PPTX export.'
  - name: '**Validate the output** – After conversion, open the generated PPTX in
      PowerPoint and verify that you can edit the chart title, series, and axis labels.
      If any element appears as an image, double‑check that `ExportChartAsEditableText`
      is enabled and that the chart type is supported.'
    text: '**Validate the output** – After conversion, open the generated PPTX in
      PowerPoint and verify that you can edit the chart title, series, and axis labels.
      If any element appears as an image, double‑check that `ExportChartAsEditableText`
      is enabled and that the chart type is supported.'
  - name: '**Batch processing** – For automation scenarios (e.g., generating a slide
      deck from many Excel reports), wrap the conversion logic in a method that accepts
      `Workbook`, `int worksheetIndex`, and `string outputPath`. This isolates the
      **export excel to powerpoint** workflow and makes it reusable.'
    text: '**Batch processing** – For automation scenarios (e.g., generating a slide
      deck from many Excel reports), wrap the conversion logic in a method that accepts
      `Workbook`, `int worksheetIndex`, and `string outputPath`. This isolates the
      **export excel to powerpoint** workflow and makes it reusable.'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel‑to‑PowerPoint
- PPTX export
title: ส่งออก Excel ไปยัง PowerPoint พร้อมแผนภูมิที่แก้ไขได้ใน C#
url: /th/net/converting-excel-files-to-other-formats/export-excel-to-powerpoint-with-editable-charts-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ส่งออก Excel ไปยัง PowerPoint พร้อมแผนภูมิที่แก้ไขได้ใน C#

การส่งออก Excel ไปยัง PowerPoint พร้อมแผนภูมิที่แก้ไขได้เป็นความต้องการทั่วไปเมื่อคุณต้องการใช้ภาพจากสเปรดชีตในงานนำเสนอซ้ำได้ คู่มือฉบับนี้จะแสดงวิธี **ส่งออก Excel ไปยัง PowerPoint** พร้อมคงความสามารถในการแก้ไขแผนภูมิ โดยใช้ Aspose.Cells for .NET

คุณจะได้เรียนรู้วิธี:

* โหลดเวิร์กบุ๊กที่มีแผนภูมิและกล่องข้อความอยู่แล้ว  
* กำหนดค่า options การส่งออก PPTX เพื่อให้แผนภูมิและรูปร่างยังคงแก้ไขได้  
* แปลงเวิร์กชีตเฉพาะเป็นไฟล์ PowerPoint ที่สามารถเปิดและแก้ไขใน Microsoft PowerPoint ได้

บทเรียนนี้สมมติว่าคุณมีความรู้พื้นฐานด้าน C# และใช้ .NET เวอร์ชันล่าสุด (≥ .NET 6) ไม่จำเป็นต้องมีประสบการณ์กับ Aspose.Cells มาก่อน

---

## ภาพรวมการส่งออก Excel ไปยัง PowerPoint

แนวคิดหลักของ **การส่งออก Excel ไปยัง PowerPoint** คือการถือว่าแต่ละเวิร์กชีตเป็นแหล่งภาพที่สามารถเรนเดอร์เป็นสไลด์ PPTX ได้ โดยการสลับแฟล็ก `ExportChartAsEditableText` และ `ExportShapeAsEditableText` Aspose.Cells จะเขียนข้อมูลแผนภูมิพื้นฐานเป็นออบเจ็กต์การวาดของ PowerPoint แทนการเป็นบิตแมพแบน ซึ่งทำให้สไลด์ที่ได้สามารถแก้ไขได้เต็มที่—เหมือนกับแผนภูมิที่สร้างโดยตรงใน PowerPoint

> **ทำไมต้องใช้แผนภูมิที่แก้ไขได้?**  
> แผนภูมิที่แก้ไขได้ช่วยให้ผู้นำเสนอปรับข้อมูล สี หรือป้ายกำกับได้โดยไม่ต้องกลับไปที่ไฟล์ Excel ดั้งเดิม ทำให้การเปลี่ยนแปลงในนาทีสุดท้ายเร็วขึ้นและทำให้กระบวนการทำงานของการนำเสนอราบรื่น

---

## แปลงเวิร์กชีตเป็น PowerPoint (worksheet to PowerPoint)

ด้านล่างเป็นตัวอย่างโค้ดที่สมบูรณ์และสามารถรันได้ ซึ่งสาธิตการแปลง **worksheet to PowerPoint**

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Load the workbook that contains the chart and textbox
            // Replace YOUR_DIRECTORY with the actual folder path on your machine.
            string inputPath = @"YOUR_DIRECTORY\input.xlsx";
            Workbook workbook = new Workbook(inputPath);

            // Step 2: Configure PPTX export options to keep charts and shapes editable
            ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
            {
                ExportType = ExportType.Pptx,               // Target format: PPTX
                ExportChartAsEditableText = true,           // Enable editable charts
                ExportShapeAsEditableText = true            // Enable editable shapes/textboxes
            };

            // Step 3: Export the first worksheet (index 0) to a PowerPoint file
            string outputPath = @"YOUR_DIRECTORY\Worksheet.pptx";
            workbook.Worksheets[0].ConvertToImage(exportOptions, outputPath);

            Console.WriteLine($"Worksheet successfully exported to {outputPath}");
        }
    }
}
```

### คำอธิบายแต่ละขั้นตอน

| ขั้นตอน | โค้ดทำอะไร | ทำไมสำคัญสำหรับ **export excel chart pptx** |
|------|-------------------|----------------------------------------------|
| 1️⃣   | โหลด `input.xlsx` เข้าออบเจ็กต์ `Aspose.Cells.Workbook` | เวิร์กบุ๊กให้การเข้าถึงแผนภูมิที่คุณต้องการส่งออก |
| 2️⃣   | ตั้งค่า `ExportType` เป็น `Pptx` และเปิดใช้งาน `ExportChartAsEditableText` & `ExportShapeAsEditableText` | แฟล็กเหล่านี้เป็นกุญแจสำคัญสำหรับ **editable charts pptx** – บอกไลบรารีให้เขียนเรขาคณิตของแผนภูมิเป็นออบเจ็กต์การวาดของ PowerPoint แทนภาพเรสเตอร์ |
| 3️⃣   | เรียก `ConvertToImage` บนเวิร์กชีตแรก เพื่อสร้าง `Worksheet.pptx` | วิธีนี้ทำการ **export excel to powerpoint** และเขียนไฟล์ PPTX ที่สามารถเปิดได้โดยตรงใน PowerPoint |

> **เคล็ดลับ:** หากต้องการส่งออก *หลาย* เวิร์กชีต ให้วนลูป `workbook.Worksheets` และเรียก `ConvertToImage` สำหรับแต่ละเวิร์กชีต พร้อมตั้งชื่อไฟล์ผลลัพธ์เป็น `Sheet1.pptx`, `Sheet2.pptx` เป็นต้น

---

## เปิดใช้งานแผนภูมิที่แก้ไขได้ใน PPTX (export excel chart pptx)

เมื่อกำหนด `ExportChartAsEditableText` เป็น `true` Aspose.Cells จะเขียนแต่ละแผนภูมิเป็นคอลเลกชันขององค์ประกอบ `<a:graphic>` ภายใน XML ของ PPTX PowerPoint จะมองว่าองค์ประกอบเหล่านั้นเป็นออบเจ็กต์แผนภูมิโดยเนทีฟ ซึ่งคุณสามารถดับเบิล‑คลิกเพื่อเปิดตัวแก้ไขแผนภูมิได้

**ข้อผิดพลาดที่พบบ่อย**

* **ไม่มีไลเซนส์ Aspose.Cells** – หากไม่มีไลเซนส์ ไลบรารีจะใส่ลายน้ำในผลลัพธ์ ลงทะเบียนไลเซนส์ตั้งแต่ต้นโปรแกรม (`License license = new License(); license.SetLicense("Aspose.Cells.lic");`)  
* **ประเภทแผนภูมิที่ไม่รองรับ** – แม้ว่าจะรองรับแผนภูมิ 2‑D ส่วนใหญ่ (คอลัมน์, เส้น, พาย) อย่างเต็มที่ แต่แผนภูมิ 3‑D หรือคอมโบที่ซับซ้อนอาจกลับเป็นภาพ ตรวจสอบประเภทแผนภูมิของคุณหากต้องการความสามารถในการแก้ไขเต็มรูปแบบ  
* **เวิร์กชีตขนาดใหญ่** – การส่งออกเวิร์กชีตขนาดใหญ่อาจใช้หน่วยความจำมาก พิจารณาใช้ `ExportMaxRows` หรือ `ExportMaxColumns` ใน `ImageOrPrintOptions` เพื่อลดพื้นที่ที่ต้องแปลง

---

## เคล็ดลับเพื่อคงแผนภูมิที่แก้ไขได้ (editable charts pptx)

1. **คงช่วงข้อมูลของแผนภูมิ** – ตรวจสอบให้แน่ใจว่าต้นทางข้อมูลของแผนภูมิอยู่ในเวิร์กชีตเดียวกับที่คุณกำลังส่งออก การอ้างอิงข้ามชีตจะถูกแปลงเป็นค่าคงที่ใน PPTX  
2. **ใช้ Aspose.Cells รุ่นล่าสุด** – เวอร์ชันใหม่ปรับปรุงการสนับสนุนคุณสมบัติแผนภูมิเพิ่มเติมและแก้ไขบั๊กที่เกี่ยวกับการส่งออก PPTX  
3. **ตรวจสอบผลลัพธ์** – หลังการแปลง ให้เปิดไฟล์ PPTX ที่สร้างใน PowerPoint และตรวจสอบว่าคุณสามารถแก้ไขชื่อแผนภูมิ, ซีรีส์, และป้ายแกนได้ หากมีองค์ประกอบใดปรากฏเป็นภาพ ให้ตรวจสอบว่าเปิด `ExportChartAsEditableText` แล้วและประเภทแผนภูมินั้นรองรับหรือไม่  
4. **การประมวลผลเป็นชุด** – สำหรับสถานการณ์อัตโนมัติ (เช่น การสร้างสไลด์เด็คจากหลายรายงาน Excel) ให้ห่อหุ้มตรรกะการแปลงในเมธอดที่รับ `Workbook`, `int worksheetIndex`, และ `string outputPath` วิธีนี้จะทำให้ workflow **export excel to powerpoint** แยกออกเป็นโมดูลและนำกลับมาใช้ใหม่ได้ง่าย

---

## สรุปตัวอย่างทำงานเต็มรูปแบบ

รวมทุกอย่างเข้าด้วยกัน นี่คือโปรแกรมขั้นต่ำที่คุณสามารถคัดลอก‑วางลงในโปรเจกต์คอนโซล .NET ใหม่ได้:

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main()
        {
            // Register license (optional but removes evaluation watermark)
            // var license = new License();
            // license.SetLicense("Aspose.Cells.lic");

            string inputPath = @"YOUR_DIRECTORY\input.xlsx";
            string outputPath = @"YOUR_DIRECTORY\Worksheet.pptx";

            Workbook workbook = new Workbook(inputPath);

            ImageOrPrintOptions options = new ImageOrPrintOptions
            {
                ExportType = ExportType.Pptx,
                ExportChartAsEditableText = true,
                ExportShapeAsEditableText = true
            };

            workbook.Worksheets[0].ConvertToImage(options, outputPath);

            Console.WriteLine($"Export complete: {outputPath}");
        }
    }
}
```

**ผลลัพธ์ที่คาดหวัง**

* จะมีไฟล์ชื่อ `Worksheet.pptx` ปรากฏใน `YOUR_DIRECTORY`  
* การเปิดไฟล์ใน Microsoft PowerPoint จะแสดงสไลด์ที่มีแผนภูมิและกล่องข้อความเดิม  
* การดับเบิล‑คลิกที่แผนภูมิจะเปิดตัวแก้ไขแผนภูมิของ PowerPoint ให้คุณเปลี่ยนค่าซีรีส์, สี, หรือชื่อแกน—ยืนยันว่า **editable charts pptx** ทำงานตามที่ต้องการ

---

## สรุป

คุณได้มีโซลูชันครบถ้วนสำหรับ **export Excel to PowerPoint** ที่คงแผนภูมิให้แก้ไขได้แล้ว โดยการกำหนด `ImageOrPrintOptions` พร้อม `ExportChartAsEditableText` และ `ExportShapeAsEditableText` กระบวนการแปลงจะสร้างไฟล์ PPTX เนทีฟที่แผนภูมิเช่นเดียวกับที่สร้างโดยตรงใน PowerPoint  

จากจุดนี้คุณสามารถ:

* ขยายโค้ดเพื่อจัดการหลายเวิร์กชีต (**worksheet to PowerPoint** สำหรับแต่ละชีต)  
* ผสานการส่งออกกับฟีเจอร์ Aspose.Cells อื่น ๆ เช่น การเพิ่มหัวข้อสไลด์หรือแทรกรูปภาพ  
* สำรวจหัวข้อที่เกี่ยวข้องเช่น **export Excel chart PPTX** ด้วยธีมกำหนดเองหรือการอัตโนมัติการสร้างสไลด์เด็คทั้งหมด

ลองทดลองกับประเภทแผนภูมิต่าง ๆ, เพิ่มป้ายข้อมูล, หรือผสาน workflow นี้เข้ากับระบบรายงานที่ใหญ่ขึ้นได้เลย ขอให้สนุกกับการเขียนโค้ด!

## คุณควรเรียนรู้อะไรต่อไป?

บทเรียนต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งข้อมูลมีโค้ดตัวอย่างทำงานครบถ้วนพร้อมคำอธิบายขั้นตอนเพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการทำงานอื่น ๆ ในโครงการของคุณ

- [วิธีแปลง Excel ไปยัง PowerPoint ด้วย Aspose.Cells for .NET: คู่มือฉบับสมบูรณ์](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}