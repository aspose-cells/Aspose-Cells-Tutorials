---
category: general
date: 2026-07-03
description: วิธีการรักษาแผนภูมิพร้อมกับการคงรูปแบบแผนภูมิโดยใช้ Aspose.Slides ใน
  C# ทำตามคู่มือขั้นตอนต่อขั้นตอนนี้.
draft: false
keywords:
- how to preserve charts
- preserve chart formatting
language: th
og_description: วิธีการเก็บรักษาแผนภูมิและรูปแบบแผนภูมิด้วย Aspose.Slides ใน C# คู่มือฉบับเต็มพร้อมโค้ด
og_title: วิธีเก็บรักษาแผนภูมิ – รักษาการจัดรูปแบบแผนภูมิใน PowerPoint (C#)
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: how to preserve charts while keeping preserve chart formatting using
    Aspose.Slides in C#. Follow this step‑by‑step guide.
  headline: how to preserve charts – preserve chart formatting in PowerPoint C#
  type: TechArticle
- description: how to preserve charts while keeping preserve chart formatting using
    Aspose.Slides in C#. Follow this step‑by‑step guide.
  name: how to preserve charts – preserve chart formatting in PowerPoint C#
  steps:
  - name: Open `EditableCharts.pptx` in PowerPoint.
    text: Open `EditableCharts.pptx` in PowerPoint.
  - name: Click any chart → “Edit Data”.
    text: Click any chart → “Edit Data”.
  - name: The Excel‑like data sheet should appear, letting you modify series values.
    text: The Excel‑like data sheet should appear, letting you modify series values.
  type: HowTo
- questions:
  - answer: Directly no—`ExportEditableObjects` only applies to the PPTX format. Convert
      first, then export.
    question: Does this work with PowerPoint 2003 (PPT) files?
  - answer: Absolutely. The same `ExportEditableObjects` flag keeps SmartArt, tables,
      and diagrams editable.
    question: Can I preserve other objects like SmartArt?
  - answer: 'The slide size is stored in the presentation metadata and isn’t affected
      by these options. No extra code needed. --- ## Next steps – keep the momentum
      Now that you’ve nailed **how to preserve charts**, try exploring: - **preserve
      chart formatting** for specific chart types (e.g., stacked bar vs. rad'
    question: What if I need to keep the original slide size?
  type: FAQPage
tags:
- Aspose.Slides
- C#
- PowerPoint
- chart automation
title: วิธีรักษาแผนภูมิ – รักษาการจัดรูปแบบแผนภูมิใน PowerPoint ด้วย C#
url: /th/net/setting-chart-appearance/how-to-preserve-charts-preserve-chart-formatting-in-powerpoi/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีการรักษาแผนภูมิ – การรักษาการจัดรูปแบบแผนภูมิใน PowerPoint C#

เคยสงสัย **วิธีการรักษาแผนภูมิ** เมื่อคุณต้องการส่งออกหรือจัดการไฟล์ PowerPoint ด้วยโปรแกรมหรือไม่? บางครั้งคุณอาจบันทึกอย่างเร็วแล้วแผนภูมิกลายเป็นภาพคงที่ ทำให้ความสามารถในการแก้ไขหายไป  

ในบทแนะนำนี้ เราจะสาธิต **วิธีการรักษาแผนภูมิ** **และ** ทำให้ **การรักษาการจัดรูปแบบแผนภูมิ** คงอยู่โดยใช้ Aspose.Slides for .NET. เมื่อจบคุณจะได้โค้ด C# ที่พร้อมรันซึ่งสร้างไฟล์ PPTX ที่ทุกแผนภูมิยังคงเป็นวัตถุ OOXML ที่แก้ไขได้—ไม่มีภาพแบนอีกต่อไป

## สิ่งที่คุณจะได้เรียนรู้

- ขั้นตอนที่แม่นยำในการโหลดงานนำเสนอ, ตั้งค่าตัวเลือกการส่งออก, และบันทึกโดย **รักษาการจัดรูปแบบแผนภูมิ**  
- ทำไมฟล็าก `ExportEditableObjects` ถึงสำคัญและมันทำให้แผนภูมิไม่ถูกแปลงเป็นภาพ rasterized อย่างไร  
- ข้อผิดพลาดทั่วไป (เช่น รูปแบบ PPT เก่า, ฟอนต์หาย) และวิธีแก้อย่างรวดเร็ว  

ไม่จำเป็นต้องมีประสบการณ์กับ Aspose มาก่อน; เพียงแค่มีการตั้งค่า C# เบื้องต้นและไฟล์ PowerPoint ที่คุณต้องการให้แผนภูมิยังคงแก้ไขได้

## ข้อกำหนดเบื้องต้น

- .NET 6.0 หรือใหม่กว่า (โค้ดนี้ยังทำงานกับ .NET Framework 4.7+ ด้วย)  
- Aspose.Slides for .NET NuGet package (`Install-Package Aspose.Slides.NET`)  
- ตัวอย่างไฟล์ `input.pptx` ที่มีอย่างน้อยหนึ่งแผนภูมิ  
- Visual Studio, Rider, หรือเครื่องมือแก้ไขใด ๆ ที่คุณชอบ

---

## ขั้นตอนที่ 1: ติดตั้ง Aspose.Slides และสร้างโปรเจกต์คอนโซลใหม่

เริ่มต้นโดยสร้างแอปคอนโซลใหม่และดึงไลบรารีเข้ามา:

```bash
dotnet new console -n PreserveChartsDemo
cd PreserveChartsDemo
dotnet add package Aspose.Slides.NET
```

> **เคล็ดลับ:** หากคุณทำงานอยู่หลังพร็อกซีขององค์กร ให้เพิ่มแฟล็ก `--no-restore` แล้วทำการ restore ภายหลังด้วยการตั้งค่าพร็อกซีของคุณ

## ขั้นตอนที่ 2: โหลดงานนำเสนอต้นฉบับ – จุดแรกที่ต้องใช้ **วิธีการรักษาแผนภูมิ**

เปิดไฟล์ PPTX ของคุณด้วยคลาส `Presentation`. ที่นี่คือจุดเริ่มต้นของ **วิธีการรักษาแผนภูมิ** อย่างแท้จริง

```csharp
using Aspose.Slides;
using Aspose.Slides.Export;

namespace PreserveChartsDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 2: Load the source presentation
            // Replace the path with the location of your PPTX that contains charts.
            Presentation pres = new Presentation(@"YOUR_DIRECTORY\input.pptx");
```

สังเกตว่าเรายังไม่ได้แตะต้องวัตถุแผนภูมิใด ๆ นั่นเป็นการตั้งใจให้ไฟล์ถูกโหลดตามเดิม เพื่อรักษาโครงสร้าง XML ดั้งเดิม ซึ่งเป็นสิ่งสำคัญสำหรับ **การรักษาการจัดรูปแบบแผนภูมิ** ต่อไป

## ขั้นตอนที่ 3: ตั้งค่าตัวเลือกการส่งออก – ใจกลางของ **วิธีการรักษาแผนภูมิ**

Aspose.Slides มีคลาส `PresentationExportOptions`. การตั้งค่า `ExportEditableObjects` เป็น `true` จะบอกเอนจินให้เก็บแผนภูมิ, ตาราง, และ SmartArt เป็นส่วน OOXML ดั้งเดิมแทนการทำให้เป็นภาพ

```csharp
            // Step 3: Configure export options to keep objects editable
            PresentationExportOptions exportOptions = new PresentationExportOptions
            {
                // This flag is the key to how to preserve charts.
                ExportEditableObjects = true
            };
```

ทำไมถึงได้ผล? เมื่อ `ExportEditableObjects` เป็น `false` (ค่าเริ่มต้น) ไลบรารีจะทำ rasterize วัตถุซับซ้อนเพื่อความเข้ากันได้ ซึ่งทำลาย **การรักษาการจัดรูปแบบแผนภูมิ** การเปิดใช้งานฟล็ากนี้จะรักษา XML ของแผนภูมิดั้งเดิม ทำให้ผู้ใช้เปิด PPTX แล้วยังแก้ไขข้อมูลแผนภูมิได้

## ขั้นตอนที่ 4: บันทึกงานนำเสนอด้วยตัวเลือกที่ตั้งค่าไว้

ตอนนี้เราจะเขียนไฟล์ผลลัพธ์ การ overload ของ `Save` ที่รับ `SaveFormat` และ `exportOptions` จะรับประกันว่าแผนภูมิยังคงแก้ไขได้

```csharp
            // Step 4: Save the presentation with the configured options
            pres.Save(@"YOUR_DIRECTORY\EditableCharts.pptx", SaveFormat.Pptx, exportOptions);

            // Optional: Inform the user
            Console.WriteLine("Presentation saved with editable charts at: YOUR_DIRECTORY\\EditableCharts.pptx");
        }
    }
}
```

เมื่อรันโปรแกรมนี้จะได้ไฟล์ `EditableCharts.pptx`. เปิดไฟล์ใน PowerPoint, คลิกขวาที่แผนภูมิ แล้วคุณจะเห็นตัวเลือก “Edit Data” – พิสูจน์ว่าเราได้ **วิธีการรักษาแผนภูมิ** และ **การรักษาการจัดรูปแบบแผนภูมิ** อย่างสำเร็จ

## ขั้นตอนที่ 5: ตรวจสอบผลลัพธ์และแก้ไขปัญหาที่พบบ่อย

### ตรวจสอบ

1. เปิด `EditableCharts.pptx` ใน PowerPoint  
2. คลิกแผนภูมิใดก็ได้ → “Edit Data”  
3. แผ่นข้อมูลแบบ Excel‑like ควรปรากฏให้คุณแก้ไขค่าชุดข้อมูล

หากคุณเห็นเพียงภาพคงที่ ให้ตรวจสอบว่า:

- คุณใช้เวอร์ชันล่าสุดของ Aspose.Slides (เวอร์ชันเก่ามีบั๊กกับ `ExportEditableObjects`)  
- ไฟล์ PPTX ต้นฉบับจริง ๆ มีวัตถุแผนภูมิ (ไม่ใช่ภาพของแผนภูมิ)  
- ไม่มีธีมหรือการแทนที่ฟอนต์ที่ทำให้แผนภูมิแสดงเป็นภาพ

### กรณีพิเศษ

- **ไฟล์ PPT (binary) เก่า:** แปลงเป็น PPTX ก่อน (`pres.Save("temp.pptx", SaveFormat.Pptx)`) แล้วจึงตั้งค่าการส่งออก  
- **งานนำเสนอขนาดใหญ่:** การใช้หน่วยความจำอาจพุ่งสูง; พิจารณาใช้ pattern `Dispose` ของ `Presentation` หรือ API สตรีมมิ่งสำหรับไฟล์ขนาดมหาศาล  
- **ฟอนต์ฝัง:** หากสภาพแวดล้อมเป้าหมายไม่มีฟอนต์ต้นฉบับ PowerPoint อาจ fallback และแปลงแผนภูมิเป็นภาพ ฝังฟอนต์ในไฟล์ต้นฉบับหรือจัดเตรียมฟอนต์พร้อมแอปพลิเคชันของคุณ

---

## คำถามที่พบบ่อย (FAQ)

**Q: ทำงานกับไฟล์ PowerPoint 2003 (PPT) ได้หรือไม่?**  
A: ไม่โดยตรง—`ExportEditableObjects` ใช้ได้เฉพาะรูปแบบ PPTX. ต้องแปลงก่อนแล้วจึงส่งออก

**Q: สามารถรักษาวัตถุอื่น ๆ เช่น SmartArt ได้หรือไม่?**  
A: ได้เลย. ฟล็าก `ExportEditableObjects` เดียวกันทำให้ SmartArt, ตาราง, และไดอะแกรมยังคงแก้ไขได้

**Q: หากต้องการคงขนาดสไลด์เดิมต้องทำอย่างไร?**  
A: ขนาดสไลด์ถูกเก็บในเมตาดาต้าของงานนำเสนอและไม่ได้รับผลกระทบจากตัวเลือกเหล่านี้. ไม่ต้องเขียนโค้ดเพิ่มเติม

---

## ขั้นตอนต่อไป – รักษาโมเมนตัม

เมื่อคุณทำ **วิธีการรักษาแผนภูมิ** ได้แล้ว ลองสำรวจต่อ:

- **การรักษาการจัดรูปแบบแผนภูมิ** สำหรับประเภทแผนภูมิเฉพาะ (เช่น stacked bar vs. radar)  
- ใช้ API `Chart` เพื่อแก้ไขข้อมูลแบบโปรแกรมก่อนบันทึก  
- ส่งออกเป็นรูปแบบอื่น (PDF, HTML) พร้อมให้แผนภูมิใน PPTX ต้นฉบับยังคงแก้ไขได้  

แต่ละหัวข้ออิงจากหลักการเดียวกัน: รักษา OOXML ด้านในให้คงอยู่

---

## สรุป

เราได้อธิบาย **วิธีการรักษาแผนภูมิ** ในไฟล์ PowerPoint ด้วย Aspose.Slides for .NET และแสดงขั้นตอน **การรักษาการจัดรูปแบบแผนภูมิ** ที่จำเป็นเพื่อให้แผนภูมิทั้งหมดยังคงแก้ไขได้ โค้ดเต็มที่อยู่ด้านบนพร้อมนำไปใช้ในโปรเจกต์ C# ใดก็ได้ พร้อมคำอธิบายเหตุผลเบื้องหลังแต่ละบรรทัด—เพื่อให้คุณไม่เพียงคัดลอก‑วาง แต่เข้าใจลึกซึ้ง

ลองใช้งาน ปรับตัวเลือกการส่งออก แล้วคุณจะสามารถอัตโนมัติงานอัปเดตงานนำเสนอโดยไม่สูญเสียความสามารถในการปรับแต่งข้อมูลแผนภูมิอย่างละเอียด Happy coding!

## สิ่งที่คุณควรเรียนต่อ

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคในคู่มือนี้ แต่ละแหล่งรวมโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายขั้นตอน‑ขั้นตอน เพื่อช่วยคุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการทำงานอื่น ๆ ในโปรเจกต์ของคุณ

- [How to Export Excel Charts to PDF Using Aspose.Cells for .NET&#58; A Step-by-Step Guide](/cells/english/net/workbook-operations/export-excel-charts-pdf-aspose-cells-net/)
- [How to Convert Excel Charts to SVG Using Aspose.Cells for .NET (Step-by-Step Guide)](/cells/english/net/charts-graphs/convert-excel-chart-to-svg-aspose-cells-net/)
- [How to Create Charts in Excel Using Aspose.Cells for .NET&#58; A Developer's Guide](/cells/english/net/charts-graphs/create-charts-excel-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}