---
category: general
date: 2026-09-15
description: เรียนรู้วิธีฝังฟอนต์ใน SVG และส่งออกแผนภูมิ Excel ไปยัง PowerPoint รวมถึงการแปลง
  XLSX เป็น SVG และการแปลง XLSX เป็น PPTX พร้อมตัวอย่างโค้ดเต็ม
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- embed fonts in SVG
- export excel chart to powerpoint
- convert xlsx to svg
- convert xlsx to pptx
- save workbook as svg
language: th
lastmod: 2026-09-15
og_description: ฝังฟอนต์ใน SVG และส่งออกแผนภูมิ Excel ไปยัง PowerPoint ด้วยโค้ด C#
  ทีละขั้นตอน แปลง XLSX เป็น SVG และ XLSX เป็น PPTX อย่างรวดเร็วและเชื่อถือได้
og_image_alt: Screenshot showing an Excel chart exported to PowerPoint with embedded
  fonts in the resulting SVG file
og_title: ฝังฟอนต์ใน SVG และส่งออกแผนภูมิ Excel ไปยัง PowerPoint – คู่มือครบถ้วน
schemas:
- author: Aspose
  dateModified: '2026-09-15'
  description: Learn how to embed fonts in SVG and export Excel chart to PowerPoint,
    covering convert XLSX to SVG and convert XLSX to PPTX with full code examples.
  headline: How to embed fonts in SVG when converting Excel files to SVG and PowerPoint
  type: TechArticle
- description: Learn how to embed fonts in SVG and export Excel chart to PowerPoint,
    covering convert XLSX to SVG and convert XLSX to PPTX with full code examples.
  name: How to embed fonts in SVG when converting Excel files to SVG and PowerPoint
  steps:
  - name: Open `EditableChart.pptx` in PowerPoint.
    text: Open `EditableChart.pptx` in PowerPoint.
  - name: Locate the slide containing the chart.
    text: Locate the slide containing the chart.
  - name: Choose **Chart Tools → Design → Edit Data**.
    text: Choose **Chart Tools → Design → Edit Data**.
  - name: Confirm that the Excel‑style data grid appears and that you can change values.
    text: Confirm that the Excel‑style data grid appears and that you can change values.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: วิธีฝังฟอนต์ใน SVG เมื่อแปลงไฟล์ Excel เป็น SVG และ PowerPoint
url: /th/net/converting-excel-files-to-other-formats/how-to-embed-fonts-in-svg-when-converting-excel-files-to-svg/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีฝังฟอนต์ใน SVG เมื่อแปลงไฟล์ Excel เป็น SVG และ PowerPoint  

หากคุณต้องการ **ฝังฟอนต์ใน SVG** ขณะแปลงเวิร์กบุ๊ก Excel คำแนะนำนี้จะแสดงให้คุณเห็นขั้นตอนอย่างละเอียด คุณยังจะได้เรียนรู้วิธี **ส่งออกแผนภูมิ Excel ไปยัง PowerPoint**, วิธี **แปลง XLSX เป็น SVG** และ **แปลง XLSX เป็น PPTX** พร้อมแผนภูมิที่แก้ไขได้  

การทำงานกับข้อมูล Excel อย่างโปรแกรมมิ่งมักหมายถึงการย้ายเนื้อหาภาพเดียวกันระหว่างรูปแบบไฟล์ต่าง ๆ การสร้างแผนภูมิใหม่ใน PowerPoint หรือการใส่ฟอนต์ใหม่ใน SVG ด้วยตนเองนั้นเสี่ยงต่อข้อผิดพลาดและใช้เวลามาก เมื่อจบบทเรียนนี้คุณจะมีโค้ดสแนป C# ที่ใช้ซ้ำได้หนึ่งชุดที่:

* บันทึกเวิร์กบุ๊กเป็นไฟล์ SVG พร้อมฝังฟอนต์และตัวเลือกการแปรผันของฟอนต์  
* ส่งออกเวิร์กบุ๊กเดียวกันเป็นไฟล์ PPTX ที่แผนภูมิยังคงแก้ไขได้  

ข้อกำหนดเบื้องต้นเพียงอย่างเดียวคือเวอร์ชันล่าสุดของ **Aspose.Cells for .NET** (2024‑x หรือใหม่กว่า) และสภาพแวดล้อมการพัฒนา .NET เช่น Visual Studio 2022  

---  

## สิ่งที่คุณต้องการ  

* .NET 6.0 หรือใหม่กว่า (โค้ดนี้ยังทำงานบน .NET Framework 4.8)  
* NuGet package ของ Aspose.Cells for .NET (`Install-Package Aspose.Cells`)  
* ไฟล์ Excel (`input.xlsx`) ที่มีอย่างน้อยหนึ่งแผนภูมิ  
* สิทธิ์การเขียนไปยังไดเรกทอรีปลายทาง  

---  

## ฝังฟอนต์ใน SVG ขณะแปลง XLSX เป็น SVG  

การฝังฟอนต์ทำให้ SVG แสดงผลได้อย่างถูกต้องบนอุปกรณ์ใด ๆ แม้ระบบเป้าหมายจะไม่มีฟอนต์ต้นฉบับ `SvgSaveOptions` มีสองแฟล็กที่ทำให้สิ่งนี้เป็นไปได้: `EmbedFonts` และ `FontVariationSelectors`  

```csharp
using Aspose.Cells;
using Aspose.Cells.Rendering;

// Load the workbook
Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");

// OPTIONAL: Use WRAPCOLS to reshape data before export (demonstrates a formula)
Worksheet sheet = workbook.Worksheets[0];
sheet.Cells["A1"].Formula = "=WRAPCOLS({1,2,3,4,5},2)"; // 2 columns per wrap
sheet.Calculate(); // Force calculation so the formula result appears

// Configure SVG options to embed fonts
SvgSaveOptions svgOptions = new SvgSaveOptions
{
    EmbedFonts = true,                // embed fonts in the SVG
    FontVariationSelectors = true    // include variation selectors for better Unicode handling
};

// Save the workbook as an SVG file
string svgPath = @"YOUR_DIRECTORY\WithFonts.svg";
workbook.Save(svgPath, svgOptions);
```

**ทำไมวิธีนี้ถึงได้ผล:**  
* `EmbedFonts = true` จะคัดลอกไฟล์ฟอนต์เข้าไปในส่วน `<defs>` ของ SVG ทำให้ไม่ต้องพึ่งพาแหล่งภายนอก  
* `FontVariationSelectors = true` จะเพิ่มตัวเลือกที่จำเป็นสำหรับฟอนต์ที่รองรับคุณลักษณะ OpenType เช่น การเชื่อมตัวอักษร (ligatures)  

**ผลลัพธ์ที่คาดหวัง:** เปิด `WithFonts.svg` ในเบราว์เซอร์สมัยใหม่; ข้อความในแผนภูมิหรือเซลล์จะแสดงด้วยฟอนต์เดียวกับที่ใช้ใน Excel แม้บนเครื่องที่ไม่ได้ติดตั้งฟอนต์นั้น  

---  

## ส่งออกแผนภูมิ Excel ไปยัง PowerPoint พร้อมแผนภูมิที่แก้ไขได้  

เมื่อคุณต้องการฝังแผนภูมิลงในสไลด์ PowerPoint แต่ยังให้ผู้รับสามารถแก้ไขข้อมูลแผนภูมิได้ `PptxSaveOptions` ของ Aspose.Cells มีแฟล็ก `ExportEditableChart`  

```csharp
// Configure PPTX options to keep charts editable after export
PptxSaveOptions pptxOptions = new PptxSaveOptions
{
    ExportEditableChart = true   // allow chart editing in PowerPoint
};

// Save the same workbook as a PPTX file
string pptxPath = @"YOUR_DIRECTORY\EditableChart.pptx";
workbook.Save(pptxPath, pptxOptions);
```

**ทำไมเรื่องนี้สำคัญ:**  
การตั้งค่า `ExportEditableChart` เป็น `true` จะบันทึกแผนภูมิเป็นอ็อบเจ็กต์ Office Open XML แทนการเป็นภาพคงที่ เมื่อเปิด `EditableChart.pptx` ใน PowerPoint คุณสามารถคลิกขวาที่แผนภูมิ → **Edit Data** และแก้ไขซีรีส์ได้เหมือนแผนภูมิดั้งเดิมของ PowerPoint  

**ขั้นตอนการตรวจสอบ:**  

1. เปิด `EditableChart.pptx` ใน PowerPoint  
2. ค้นหาสไลด์ที่มีแผนภูมิ  
3. เลือก **Chart Tools → Design → Edit Data**  
4. ยืนยันว่าตารางข้อมูลสไตล์ Excel ปรากฏและคุณสามารถเปลี่ยนค่าได้  

---  

## แปลง XLSX เป็น SVG – สรุปกระบวนการทำงานเต็มรูปแบบ  

ด้านล่างเป็นเวอร์ชันย่อที่รวมการโหลด, การจัดการข้อมูลแบบเลือก, และการบันทึกเป็น SVG ใช้เมื่อคุณต้องการผลลัพธ์เป็น SVG เท่านั้น  

```csharp
public void ConvertXlsxToSvg(string inputPath, string outputPath)
{
    Workbook wb = new Workbook(inputPath);

    // Example: apply a formula to demonstrate cell calculations
    Worksheet ws = wb.Worksheets[0];
    ws.Cells["A1"].Formula = "=WRAPCOLS({1,2,3,4,5},2)";
    ws.Calculate();

    SvgSaveOptions opts = new SvgSaveOptions
    {
        EmbedFonts = true,
        FontVariationSelectors = true
    };

    wb.Save(outputPath, opts);
}
```

เรียกใช้เมธอดดังนี้:  

```csharp
ConvertXlsxToSvg(@"YOUR_DIRECTORY\input.xlsx", @"YOUR_DIRECTORY\Result.svg");
```

**เคล็ดลับกรณีขอบ:** หากเวิร์กบุ๊กของคุณมีฟอนต์กำหนดเองที่ไม่ได้ติดตั้งบนเซิร์ฟเวอร์ ให้ฝังฟอนต์เหล่านั้นด้วยตนเองก่อนเรียก `Save` ใช้ `FontInfoCollection` เพื่อเพิ่มไฟล์ฟอนต์ลงใน `SvgSaveOptions` ผ่านคุณสมบัติ `CustomFonts` (มีใน Aspose.Cells รุ่นใหม่)  

---  

## แปลง XLSX เป็น PPTX – รักษาความสามารถในการแก้ไขแผนภูมิ  

เมธอดช่วยเหลือต่อไปนี้แสดงเส้นทาง **แปลง XLSX เป็น PPTX** พร้อมรับประกันว่าแผนภูมิยังคงแก้ไขได้  

```csharp
public void ConvertXlsxToPptx(string inputPath, string outputPath)
{
    Workbook wb = new Workbook(inputPath);

    // Ensure any chart you want to keep editable is on the first worksheet
    // (Aspose.Cells exports only the first worksheet by default for PPTX)
    PptxSaveOptions opts = new PptxSaveOptions
    {
        ExportEditableChart = true
    };

    wb.Save(outputPath, opts);
}
```

การใช้งาน:  

```csharp
ConvertXlsxToPptx(@"YOUR_DIRECTORY\input.xlsx", @"YOUR_DIRECTORY\Result.pptx");
```

**คำถามที่พบบ่อย:** *ถ้าเวิร์กบุ๊กของฉันมีหลายแผ่นงานที่มีแผนภูมิ?*  
**คำตอบ:** Aspose.Cells จะส่งออกแผ่นงานแรกโดยค่าเริ่มต้น หากต้องการรวมแผ่นงานเพิ่มเติม ให้วนลูป `workbook.Worksheets` คัดลอกแต่ละแผนภูมิไปยังสไลด์ใหม่ และบันทึกแต่ละสไลด์แยกกันโดยใช้อ็อบเจ็กต์ `Presentation` จาก Aspose.Slides สถานการณ์ขั้นสูงนี้อยู่นอกกระบวนการ “บันทึกเวิร์กบุ๊กเป็น SVG” และ “ส่งออกแผนภูมิ Excel ไปยัง PowerPoint” เบื้องต้น แต่แฟล็กหลักยังคงเหมือนเดิม  

---  

## เคล็ดลับและข้อควรระวัง  

* **ประสิทธิภาพ:** การฝังฟอนต์จะเพิ่มขนาดไฟล์ SVG หากขนาดเป็นปัญหาให้ตั้งค่า `EmbedFonts = false` และใช้ฟอนต์ที่ปลอดภัยบนเว็บ  
* **ลิขสิทธิ์ฟอนต์:** ตรวจสอบว่าคุณมีสิทธิ์ฝังฟอนต์ที่ใช้; ฟอนต์เชิงพาณิชย์บางตัวจำกัดการฝัง  
* **ความเข้ากันได้ของแผนภูมิ:** แผนภูมิที่แก้ไขได้จะถูกบันทึกเป็นส่วน `chart.xml` ภายใน PPTX แผนภูมิที่ซับซ้อนมาก (เช่น 3‑D หรือคอมโบ) อาจสูญเสียสไตล์บางอย่างเมื่อแก้ไขใน PowerPoint ทดสอบประเภทแผนภูมิที่ใช้บ่อยที่สุดของคุณ  
* **ความไม่ตรงกันของเวอร์ชัน:** แฟล็ก `ExportEditableChart` ต้องการ Aspose.Cells 20.10 หรือใหม่กว่า หากใช้เวอร์ชันเก่าจะกลับไปใช้ภาพเรสเตอร์โดยอัตโนมัติ  
* **ความปลอดภัยของเธรด:** วัตถุ Workbook ไม่ปลอดภัยต่อการทำงานหลายเธรด สร้างอินสแตนซ์ `Workbook` ใหม่ต่อคำขอในสถานการณ์บริการเว็บ  

---  

## ตัวอย่างเต็มรูปแบบแบบ End‑to‑End  

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;

class ExcelExportDemo
{
    static void Main()
    {
        // Paths – adjust to your environment
        string inputFile = @"YOUR_DIRECTORY\input.xlsx";
        string svgFile   = @"YOUR_DIRECTORY\WithFonts.svg";
        string pptxFile  = @"YOUR_DIRECTORY\EditableChart.pptx";

        // 1. Load workbook
        Workbook workbook = new Workbook(inputFile);

        // 2. Optional: reshape data using WRAPCOLS
        Worksheet sheet = workbook.Worksheets[0];
        sheet.Cells["A1"].Formula = "=WRAPCOLS({1,2,3,4,5},2)";
        sheet.Calculate();

        // 3. Save as SVG with embedded fonts
        SvgSaveOptions svgOpts = new SvgSaveOptions
        {
            EmbedFonts = true,
            FontVariationSelectors = true
        };
        workbook.Save(svgFile, svgOpts);
        Console.WriteLine($"SVG saved with embedded fonts to: {svgFile}");

        // 4. Save as PPTX with editable chart
        PptxSaveOptions pptxOpts = new PptxSaveOptions
        {
            ExportEditableChart = true
        };
        workbook.Save(pptxFile, pptxOpts);
        Console.WriteLine($"PPTX saved with editable chart to: {pptxFile}");
    }
}
```

การรันโปรแกรมนี้จะสร้างไฟล์สองไฟล์:  

* **WithFonts.svg** – SVG ที่แสดงผลเหมือนมุมมองใน Excel พร้อมฟอนต์รวมอยู่  
* **EditableChart.pptx** – งานนำเสนอ PowerPoint ที่แผนภูมิสามารถแก้ไขได้โดยตรง  

---  

## สรุป  

คุณได้เรียนรู้วิธี **ฝังฟอนต์ใน SVG** เมื่อ **แปลง XLSX เป็น SVG** และวิธี **ส่งออกแผนภูมิ Excel ไปยัง PowerPoint** พร้อมให้แผนภูมิแก้ไขได้ โค้ดเดียวกันยังแสดงวิธี **บันทึกเวิร์กบุ๊กเป็น SVG** และ **แปลง XLSX เป็น PPTX** อย่างง่ายดาย  

จากนี้คุณสามารถสำรวจหัวข้อเพิ่มเติมได้ เช่น:  

* การเพิ่มฟอนต์กำหนดเองโดยโปรแกรม (`svgOptions.CustomFonts`)  
* การประมวลผลหลายเวิร์กบุ๊กเป็นชุดในบริการพื้นหลัง  
* การใช้ Aspose.Slides เพื่อสร้างไฟล์ PPTX หลายสไลด์ที่รวมแผนภูมิ Excel หลายรายการ  

ทดลองปรับตัวเลือกต่าง ๆ ปรับสแนปให้เข้ากับโครงการของคุณ และเพลิดเพลินกับการแปลง Excel‑to‑SVG/PPTX ที่เชื่อถือได้โดยไม่ต้องทำการประมวลผลหลังจากแปลงแล้ว ขอให้เขียนโค้ดอย่างสนุกสนาน!  

## สิ่งที่คุณควรเรียนต่อไป  

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งข้อมูลมีตัวอย่างโค้ดทำงานครบถ้วนพร้อมคำอธิบายขั้นตอนเพื่อช่วยคุณเชี่ยวชาญคุณลักษณะ API เพิ่มเติมและสำรวจแนวทางการทำงานอื่น ๆ ในโครงการของคุณ  

- [วิธีแปลงแผนภูมิ Excel เป็น SVG ด้วย Aspose.Cells for .NET (คู่มือขั้นตอน) ](/cells/english/net/charts-graphs/convert-excel-chart-to-svg-aspose-cells-net/)  
- [Convert Excel Chart To Svg Aspose Cells Net](/cells/german/net/charts-graphs/convert-excel-chart-to-svg-aspose-cells-net/)  
- [Convert Excel Chart To Svg Aspose Cells Net](/cells/french/net/charts-graphs/convert-excel-chart-to-svg-aspose-cells-net/)  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}