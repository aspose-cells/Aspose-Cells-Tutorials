---
category: general
date: 2026-06-05
description: วิธีส่งออกแผนภูมิจาก PowerPoint ด้วย C# รวมถึงการส่งออกวัตถุ OLE และทำให้แผนภูมิสามารถแก้ไขได้ในไฟล์
  PPTX ที่ได้ – ขั้นตอนโดยละเอียด
draft: false
keywords:
- how to export charts
- export ole objects
- how to export ole
- make charts editable
language: th
og_description: วิธีส่งออกแผนภูมิจาก PowerPoint ด้วย C# เรียนรู้การส่งออกวัตถุ OLE
  และทำให้แผนภูมิแก้ไขได้ในไฟล์ PPTX ที่บันทึก – ทีละขั้นตอน
og_title: วิธีส่งออกแผนภูมิ – คู่มือ PowerPoint C# ฉบับสมบูรณ์
schemas:
- author: Aspose
  dateModified: '2026-06-05'
  description: How to export charts from PowerPoint using C#. Includes export OLE
    objects and make charts editable in the resulting PPTX – step‑by‑step.
  headline: How to Export Charts – Complete PowerPoint C# Guide
  type: TechArticle
- description: How to export charts from PowerPoint using C#. Includes export OLE
    objects and make charts editable in the resulting PPTX – step‑by‑step.
  name: How to Export Charts – Complete PowerPoint C# Guide
  steps:
  - name: Full Working Example
    text: Below is the complete, self‑contained program you can compile and run. It
      includes `using` statements, proper disposal, and comments that explain each
      line.
  - name: What if the source file has no charts?
    text: The code will still run; `ExportEditableCharts` simply has no effect because
      there’s nothing to convert. No error is thrown.
  - name: Can I export only specific charts?
    text: Yes. Instead of using the global `ExportEditableCharts` flag, you can iterate
      through `presentation.Slides` and set `Chart.IsEditable = true` on individual
      chart objects before saving. This gives you granular control.
  - name: Does enabling OLE export increase file size?
    text: A little. The binary OLE streams are stored verbatim, so the resulting PPTX
      can be a few kilobytes larger. In most business scenarios the trade‑off is worth
      it because you retain full editability.
  - name: Which PowerPoint versions can open the resulting file?
    text: Any version that supports the OOXML standard (PowerPoint 2007 and later).
      The editable chart feature relies on the native chart editor introduced in Office
      2007, so older binaries like `.ppt` won’t benefit.
  type: HowTo
tags:
- PowerPoint
- C#
- Aspose.Slides
- OLE
- Charts
title: วิธีส่งออกแผนภูมิ – คู่มือ PowerPoint C# ฉบับสมบูรณ์
url: /th/net/chart-rendering-and-conversion/how-to-export-charts-complete-powerpoint-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีส่งออกแผนภูมิ – คู่มือ PowerPoint C# ฉบับสมบูรณ์

เคยสงสัย **how to export charts** จากไฟล์ PowerPoint โดยไม่สูญเสียความสามารถในการแก้ไขภายหลังหรือไม่? คุณไม่ได้เป็นคนเดียวที่คิดเช่นนั้น ในหลายกระบวนการรายงานข้อมูลของแผนภูมิจะอยู่ภายในไฟล์ PPTX และเมื่อคุณส่งไฟล์ให้ผู้รับ ผู้รับมักต้องปรับค่าหรือเปลี่ยนป้ายชื่อบ้าง ข่าวดีคือด้วยไม่กี่บรรทัดของ C# คุณสามารถรักษาความสามารถในการแก้ไขได้ และยังสามารถส่งออกวัตถุ OLE ที่ฝังอยู่พร้อมกันได้

ในบทแนะนำนี้ เราจะพาคุณผ่านตัวอย่างที่ใช้งานได้จริงและพร้อมรัน ที่แสดง **how to export charts**, วิธี **export OLE objects**, และวิธี **make charts editable** ในไฟล์ผลลัพธ์ เมื่อจบคุณจะได้โค้ดส่วนนำกลับมาใช้ใหม่ที่สามารถใส่ลงในโปรเจกต์ .NET ใด ๆ ที่ใช้ไลบรารี Aspose.Slides

> **Pro tip:** หากคุณใหม่กับ Aspose.Slides อย่าลืมเพิ่มแพคเกจ NuGet `Aspose.Slides.NET` ลงในโปรเจกต์ของคุณ—หากไม่ทำ โค้ดจะไม่คอมไพล์

## สิ่งที่คุณต้องการ

| ความต้องการ | เหตุผล |
|-------------|--------|
| .NET 6+ (or .NET Framework 4.7+) | Runtime สมัยใหม่ให้ประสิทธิภาพที่ดีกว่าและการจัดการแพคเกจที่ง่ายขึ้น |
| Aspose.Slides for .NET (latest version) | ไลบรารีนี้ให้คลาส `Presentation` และ `PptxSaveOptions` ที่เราจะใช้ |
| A sample PowerPoint file with at least one chart | ตัวอย่างทำงานกับไฟล์ `.pptx` ใด ๆ ที่มีแผนภูมิ; คุณจะเห็นความสามารถในการแก้ไขหลังการส่งออก |
| An IDE (Visual Studio, Rider, or VS Code) | มีประโยชน์สำหรับการดีบักอย่างรวดเร็วและดูไฟล์ที่สร้างขึ้น |

ไม่มีเครื่องมือของบุคคลที่สามเพิ่มเติมที่จำเป็น—ทุกอย่างจัดการโดย Aspose API

## ขั้นตอนที่ 1 – โหลดไฟล์นำเสนอต้นฉบับ

ก่อนอื่นเราต้องนำไฟล์ PPTX ดั้งเดิมเข้ามาในหน่วยความจำ คิดว่าเป็นการเปิดเอกสารใน Word ก่อนเริ่มแก้ไข

```csharp
using Aspose.Slides;

// Step 1: Load the source presentation
Presentation presentation = new Presentation(@"C:\MyProjects\input.pptx");
```

> **Why this matters:** วัตถุ `Presentation` เป็นจุดเริ่มต้นสำหรับการดำเนินการต่อไปทั้งหมด มันจะทำการพาร์สไฟล์, สร้างโมเดลวัตถุของสไลด์, รูปร่าง, แผนภูมิและ OLE objects, และเก็บทุกอย่างในสถานะที่สามารถแก้ไขได้

## ขั้นตอนที่ 2 – สร้างตัวเลือกการบันทึกและเปิดใช้งาน Editable Charts

โดยค่าเริ่มต้นเมื่อคุณเรียก `Save` ไลบรารีจะทำให้แผนภูมิกลายเป็นภาพคงที่ เพื่อให้ยังแก้ไขได้คุณต้องสลับแฟล็ก `ExportEditableCharts`

```csharp
// Step 2: Create PPTX save options and enable editable charts
PptxSaveOptions saveOptions = new PptxSaveOptions
{
    // This tells Aspose to keep chart data in a format PowerPoint can edit.
    ExportEditableCharts = true
};
```

> **How it works:** เมื่อ `ExportEditableCharts` เป็น `true` ไลบรารีจะเขียนคำนิยาม XML ของแผนภูมิ (`chart.xml`) ลงใน PPTX แทนการแปลงเป็นภาพ PowerPoint จะอ่าน XML นั้นและให้ผู้ใช้เปิดตัวแก้ไขแผนภูมิได้

## ขั้นตอนที่ 3 – เปิดการส่งออก OLE Objects ที่ฝังอยู่

หลายการนำเสนอฝังแผ่นงาน Excel, แผนภาพ Visio หรือแม้แต่ไฟล์ PDF เป็น OLE objects หากคุณต้องการให้วัตถุเหล่านี้คงอยู่ตลอดการส่งต่อ ให้เปิดใช้งาน `ExportOLEObjects`

```csharp
// Step 3: Enable export of embedded OLE objects
saveOptions.ExportOLEObjects = true;
```

> **What “export OLE objects” really means:** แพ็กเกจ OLE จะถูกเก็บเป็นบล็อบไบนารีภายใน PPTX การตั้งค่าแฟล็กนี้จะรักษาไบนารีเดิมไว้ ทำให้ผู้รับสามารถดับเบิลคลิกวัตถุและเปิดในแอปพลิเคชันเดิม (เช่น Excel) หากไม่ตั้งค่า OLE object จะถูกตัดออก ทำให้ลิงก์เสียและข้อมูลหายไป

## ขั้นตอนที่ 4 – บันทึกไฟล์นำเสนอด้วยตัวเลือกที่กำหนด

เมื่อเราเตรียมตัวเลือกเรียบร้อยแล้ว เพียงบอก Aspose ให้เขียนไฟล์ออก

```csharp
// Step 4: Save the presentation with the configured options
presentation.Save(@"C:\MyProjects\editable.pptx", saveOptions);
```

> **Result:** `editable.pptx` มีสไลด์เดียวกับ `input.pptx` แต่แผนภูมิใด ๆ สามารถแก้ไขได้โดยตรงใน PowerPoint และ OLE objects ที่ฝังอยู่ยังคงอยู่ครบถ้วน

### ตัวอย่างทำงานเต็มรูปแบบ

ด้านล่างเป็นโปรแกรมที่สมบูรณ์และเป็นอิสระที่คุณสามารถคอมไพล์และรันได้ รวมถึง `using` statements, การจัดการทรัพยากรอย่างเหมาะสม, และคอมเมนต์อธิบายแต่ละบรรทัด

```csharp
using System;
using Aspose.Slides;

namespace ExportChartsDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Path to the source PPTX
            string sourcePath = @"C:\MyProjects\input.pptx";
            // Path where the edited PPTX will be saved
            string destPath = @"C:\MyProjects\editable.pptx";

            // Load the presentation
            using (Presentation presentation = new Presentation(sourcePath))
            {
                // Configure save options
                PptxSaveOptions options = new PptxSaveOptions
                {
                    ExportEditableCharts = true,   // make charts editable
                    ExportOLEObjects = true        // export OLE objects such as embedded Excel sheets
                };

                // Save the new file
                presentation.Save(destPath, options);
            }

            Console.WriteLine("Presentation saved with editable charts and OLE objects.");
        }
    }
}
```

**Expected output:** หลังจากรันโปรแกรมแล้ว เปิด `editable.pptx` ใน PowerPoint คลิกขวาแผนภูมิใด ๆ → *Edit Data* → ตัวแก้ไขแผนภูมิจะเปิดขึ้น ยืนยันว่า **make charts editable** ทำงานสำเร็จ ดับเบิลคลิกแผ่นงาน Excel ที่ฝังอยู่ จะเปิดใน Excel แสดงว่า **export OLE objects** ทำงานได้

![แผนภาพวิธีส่งออกแผนภูมิ](https://example.com/images/export-charts.png "วิธีส่งออกแผนภูมิ – PowerPoint หลังการส่งออก")

*(ข้อความแทนภาพ: วิธีส่งออกแผนภูมิ – ภาพหน้าจอ PowerPoint ที่มีแผนภูมิแก้ไขได้และวัตถุ OLE)*

## คำถามทั่วไป & กรณีขอบ

### ถ้าไฟล์ต้นฉบับไม่มีแผนภูมิจะเป็นอย่างไร?

โค้ดจะยังคงทำงาน; `ExportEditableCharts` จะไม่มีผลใด ๆ เพราะไม่มีแผนภูมิให้แปลง ไม่เกิดข้อผิดพลาดใด ๆ

### ฉันสามารถส่งออกเฉพาะแผนภูมิที่ต้องการได้หรือไม่?

ได้ แทนการใช้แฟล็ก `ExportEditableCharts` ทั้งหมด คุณสามารถวนลูปผ่าน `presentation.Slides` และตั้งค่า `Chart.IsEditable = true` บนแผนภูมิแต่ละอันก่อนบันทึก ซึ่งให้การควบคุมระดับละเอียด

```csharp
foreach (ISlide slide in presentation.Slides)
{
    foreach (IChart chart in slide.Shapes.OfType<IChart>())
    {
        chart.IsEditable = true; // enable editability only for this chart
    }
}
```

### การเปิดใช้งานการส่งออก OLE ทำให้ไฟล์ใหญ่ขึ้นหรือไม่?

เพิ่มเล็กน้อย เนื่องจากสตรีม OLE ไบนารีจะถูกเก็บไว้ตามเดิม ดังนั้น PPTX ที่ได้อาจใหญ่กว่าประมาณหลายกิโลไบต์ ในหลายสถานการณ์ธุรกิจ การแลกเปลี่ยนขนาดไฟล์เพิ่มเล็กน้อยถือว่าคุ้มค่าเพราะได้ความสามารถในการแก้ไขเต็มรูปแบบ

### เวอร์ชัน PowerPoint ใดบ้างที่สามารถเปิดไฟล์ผลลัพธ์ได้?

ทุกเวอร์ชันที่รองรับมาตรฐาน OOXML (PowerPoint 2007 ขึ้นไป) ฟีเจอร์แผนภูมิแก้ไขได้อาศัยตัวแก้ไขแผนภูมิดั้งเดิมที่แนะนำใน Office 2007 ดังนั้นไฟล์แบบเก่าเช่น `.ppt` จะไม่ได้รับประโยชน์

## เคล็ดลับสำหรับโค้ดพร้อมใช้งานใน Production

| เคล็ดลับ | เหตุผล |
|----------|--------|
| ใช้บล็อก `using` (ตามตัวอย่าง) เพื่อกำจัดวัตถุ `Presentation` | ป้องกันการรั่วของหน่วยความจำ โดยเฉพาะเมื่อประมวลผลไฟล์จำนวนมากในแบตช์ |
| ตรวจสอบเส้นทางไฟล์ก่อนโหลด | ป้องกัน `FileNotFoundException` ที่อาจทำให้บริการเบื้องหลังล่ม |
| บันทึกการตั้งค่า `ExportEditableCharts` และ `ExportOLEObjects` | มีประโยชน์ในการแก้ปัญหาเมื่อผู้ใช้รายงานว่าแผนภูมิไม่สามารถแก้ไขได้ |
| ดักจับ `Aspose.Slides.Exception` แยกต่างหาก | ให้ข้อความข้อผิดพลาดที่ชัดเจนจากไลบรารี (เช่น ชนิดแผนภูมิที่ไม่รองรับ) |
| พิจารณา `PptxCompressionLevel` หากขนาดไฟล์เป็นเรื่องสำคัญ | สามารถบีบอัดผลลัพธ์ได้ในขณะที่ยังคงรักษาความสามารถในการแก้ไข |

## สรุป – สิ่งที่เราได้ทำ

เราเริ่มต้นด้วยคำถามที่ชัดเจน: **how to export charts** จากไฟล์ PowerPoint พร้อมคงความสามารถในการแก้ไขและรักษา OLE objects ที่ฝังอยู่ โดยการโหลดไฟล์นำเสนอ, ตั้งค่า `PptxSaveOptions` (`ExportEditableCharts = true` และ `ExportOLEObjects = true`), แล้วบันทึกไฟล์ เราจึงได้ PPTX ที่ตอบสนองความต้องการทั้งสองแบบ รูปแบบเดียวกันนี้สามารถนำไปใช้ซ้ำสำหรับการแปลงเป็นชุด, CI pipelines, หรือเครื่องมือรายงานอัตโนมัติใด ๆ

## สิ่งที่ควรสำรวจต่อไป?

- ส่งออกแผนภูมิเป็นภาพสำหรับรายงานแบบคงที่ (`saveOptions.ExportEditableCharts = false`).  
- แปลง PPTX เป็น PDF พร้อมรักษากราฟิกเวกเตอร์ (`PdfSaveOptions`).  
- จัดการข้อมูลแผนภูมิด้วยโปรแกรม (เช่น ปรับค่าชุดข้อมูลก่อนส่งออก).  
- ผสานกับ Azure Functions เพื่อให้บริการ API ส่งออกแผนภูมิตามความต้องการ

## สิ่งที่คุณควรเรียนต่อไป?

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งข้อมูลมีตัวอย่างโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายขั้นตอนเพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการทำงานอื่น ๆ ในโปรเจกต์ของคุณ

- [วิธีส่งออกแผนภูมิ Excel เป็น PDF ด้วย Aspose.Cells for .NET: คู่มือขั้นตอนโดยละเอียด](/cells/english/net/workbook-operations/export-excel-charts-pdf-aspose-cells-net/)
- [วิธีแปลงแผนภูมิ Excel เป็น SVG ด้วย Aspose.Cells for .NET (คู่มือขั้นตอนโดยละเอียด)](/cells/english/net/charts-graphs/convert-excel-chart-to-svg-aspose-cells-net/)
- [วิธีใช้ธีมกับแผนภูมิ Excel ด้วย Aspose.Cells .NET: คู่มือขั้นตอนโดยละเอียด](/cells/english/net/charts-graphs/apply-themes-charts-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}