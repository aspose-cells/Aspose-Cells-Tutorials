---
category: general
date: 2026-01-14
description: วิธีคัดลอก Pivot Table ด้วย Aspose.Cells และเรียนรู้การแปลง Excel เป็น
  PPTX, คัดลอกช่วงข้อมูลไปยังเวิร์กบุ๊กอื่น, และทำให้ TextBox สามารถแก้ไขได้ใน PPTX
  ในบทเรียนเดียว
draft: false
keywords:
- how to copy pivot table
- convert excel to pptx
- copy range to another workbook
- make textbox editable pptx
- save workbook as pptx
language: th
og_description: วิธีคัดลอก Pivot Table แล้วแปลง Excel เป็น PPTX, คัดลอกช่วงข้อมูลไปยังเวิร์กบุ๊กอื่น,
  และทำให้กล่องข้อความใน PPTX สามารถแก้ไขได้—ทั้งหมดด้วย Aspose.Cells.
og_title: วิธีคัดลอก Pivot Table ใน C# – คู่มือครบวงจรจาก Excel ไปยัง PPTX
tags:
- Aspose.Cells
- C#
- Excel automation
- PowerPoint export
title: วิธีคัดลอก Pivot Table ใน C# – แปลง Excel เป็น PPTX, คัดลอกช่วงข้อมูล และทำให้กล่องข้อความแก้ไขได้
url: /th/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีคัดลอก Pivot Table ใน C# – คู่มือครบถ้วนจาก Excel ไปยัง PPTX

การคัดลอก pivot table จากเวิร์กบุ๊กหนึ่งไปยังอีกเวิร์กบุ๊กเป็นคำถามที่พบบ่อยเมื่อคุณทำอัตโนมัติรายงานที่ขับเคลื่อนด้วย Excel ในบทแนะนำนี้เราจะพาคุณผ่านสามสถานการณ์จริงโดยใช้ **Aspose.Cells for .NET**: การคัดลอกช่วง pivot‑table, การส่งออกแผ่นงานเป็นไฟล์ PPTX พร้อมกล่องข้อความที่แก้ไขได้, และการใส่ JSON array ลงในเซลล์เดียวด้วย Smart Markers  

คุณจะได้เห็นวิธี **แปลง Excel เป็น PPTX**, **คัดลอกช่วงไปยังเวิร์กบุ๊กอื่น**, และ **ทำให้กล่องข้อความใน PPTX แก้ไขได้** โดยไม่ทำลายรูปแบบใด ๆ เมื่อเสร็จสิ้นคุณจะมีโค้ดพร้อมรันที่สามารถนำไปใส่ในโปรเจกต์ .NET ใดก็ได้

> **เคล็ดลับ:** ตัวอย่างทั้งหมดใช้ Aspose.Cells 23.12 แต่แนวคิดเดียวกันใช้กับเวอร์ชันก่อนหน้าที่อาจต้องปรับ API เล็กน้อย

![Diagram showing how a pivot table is copied, a worksheet exported to PPTX, and a JSON array inserted – how to copy pivot table workflow](how-to-copy-pivot-table-diagram.png)

---

## สิ่งที่คุณต้องเตรียม

- Visual Studio 2022 (หรือ IDE สำหรับ C# ใดก็ได้)
- .NET 6.0 หรือ runtime เวอร์ชันใหม่กว่า
- Aspose.Cells for .NET NuGet package  
  ```bash
  dotnet add package Aspose.Cells
  ```
- ไฟล์ Excel ตัวอย่างสองไฟล์ (`source.xlsx`, `chartWithTextbox.xlsx`) ที่วางไว้ในโฟลเดอร์ที่คุณควบคุม (แทนที่ `YOUR_DIRECTORY` ด้วยพาธจริงของคุณ)

ไม่มีไลบรารีเพิ่มเติมที่จำเป็น; Assembly `Aspose.Cells` ตัวเดียวจัดการ Excel, PPTX, และ Smart Markers

---

## วิธีคัดลอก Pivot Table พร้อมรักษาข้อมูลไว้

เมื่อคุณคัดลอกช่วงที่มี pivot table พฤติกรรมเริ่มต้นคือการวางเฉพาะ **ค่า** เท่านั้น เพื่อให้คงคำนิยามของ pivot ไว้คุณต้องเปิดใช้งานฟลัก `CopyPivotTable`

### ขั้นตอนทีละขั้นตอน

1. **โหลดเวิร์กบุ๊กต้นทาง** ที่มี pivot table อยู่  
2. **สร้างเวิร์กบุ๊กปลายทางเปล่า** – จะรับช่วงที่คัดลอกมา  
3. **ใช้ `CopyRange` พร้อม `CopyPivotTable = true`** เพื่อให้คำนิยาม pivot ถูกคัดลอกพร้อมข้อมูล  
4. **บันทึกไฟล์ปลายทาง** ไปยังตำแหน่งที่ต้องการ

#### ตัวอย่างโค้ดเต็ม

```csharp
using Aspose.Cells;

class PivotCopyDemo
{
    static void Main()
    {
        // Step 1: Load the source workbook and define the range to copy
        Workbook sourceWorkbook = new Workbook(@"YOUR_DIRECTORY\source.xlsx");
        Worksheet sourceSheet = sourceWorkbook.Worksheets[0];
        // Assuming the pivot table lives inside A1:G20
        Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");

        // Step 2: Create a destination workbook (blank)
        Workbook destinationWorkbook = new Workbook();
        Worksheet destinationSheet = destinationWorkbook.Worksheets[0];

        // Step 3: Copy the range, preserving the pivot table
        destinationSheet.Cells.CopyRange(
            sourceRange,
            "B2", // paste start cell
            new CopyOptions { CopyPivotTable = true });

        // Step 4: Save the result
        destinationWorkbook.Save(@"YOUR_DIRECTORY\copyWithPivot.xlsx");
    }
}
```

**ทำไมวิธีนี้ถึงได้ผล:**  
`CopyOptions.CopyPivotTable` บอก Aspose.Cells ให้คล cloning วัตถุ `PivotTable` ด้านในแทนการคัดลอกค่าแค่ภาพเท่านั้น เวิร์กบุ๊กปลายทางจึงมี pivot ที่ทำงานได้เต็มรูปแบบและคุณสามารถรีเฟรชหรือแก้ไขได้โดยโปรแกรม

**กรณีขอบ:** หากเวิร์กบุ๊กต้นทางใช้แหล่งข้อมูลภายนอก คุณอาจต้องฝังข้อมูลหรือปรับสตริงการเชื่อมต่อหลังการคัดลอก มิฉะนั้น pivot จะแสดง “#REF!”

---

## แปลง Excel เป็น PPTX และทำให้กล่องข้อความแก้ไขได้

การส่งออกแผ่นงานไปยัง PowerPoint มีประโยชน์สำหรับการสร้างสไลด์เด็คโดยตรงจากข้อมูล โดยค่าเริ่มต้นกล่องข้อความที่ส่งออกจะเป็นรูปทรงคงที่ แต่การตั้งค่า `IsTextBoxEditable` จะเปลี่ยนพฤติกรรมนี้

### ขั้นตอนทีละขั้นตอน

1. **เปิดเวิร์กบุ๊ก** ที่มีแผนภูมิและกล่องข้อความที่ต้องการส่งออก  
2. **กำหนด `ImageOrPrintOptions`** ด้วย `SaveFormat = SaveFormat.Pptx`  
3. **กำหนดพื้นที่พิมพ์** ที่รวมกล่องข้อความไว้ด้วย  
4. **เปิด `IsTextBoxEditable`** เพื่อให้ข้อความสามารถแก้ไขได้หลังเปิดไฟล์ PPTX  
5. **บันทึกไฟล์ PPTX**

#### ตัวอย่างโค้ดเต็ม

```csharp
using Aspose.Cells;

class ExcelToPptxDemo
{
    static void Main()
    {
        // Step 1: Load the workbook with chart and textbox
        Workbook chartWorkbook = new Workbook(@"YOUR_DIRECTORY\chartWithTextbox.xlsx");

        // Step 2: Set export options for PPTX
        ImageOrPrintOptions pptxOptions = new ImageOrPrintOptions
        {
            SaveFormat = SaveFormat.Pptx
        };

        // Step 3: Define the print area that captures the textbox (A1:D20)
        chartWorkbook.Worksheets[0].PageSetup.PrintArea = "A1:D20";

        // Step 4: Make the textbox editable in the exported PPTX
        chartWorkbook.Worksheets[0].PageSetup.IsTextBoxEditable = true;

        // Step 5: Export the worksheet to a PPTX file
        chartWorkbook.Save(@"YOUR_DIRECTORY\result.pptx", pptxOptions);
    }
}
```

**ผลลัพธ์:** เปิด `result.pptx` ใน PowerPoint – กล่องข้อความที่คุณวางใน Excel จะกลายเป็นกล่องข้อความปกติที่สามารถพิมพ์ข้อความได้ ไม่ต้องสร้างใหม่ด้วยมือ

**ข้อผิดพลาดทั่วไป:** หากแผ่นงานมีเซลล์ที่ผสานกันและตัดกับพื้นที่พิมพ์ สไลด์ที่ได้อาจเลื่อนตำแหน่ง ปรับพื้นที่พิมพ์หรือยกเลิกการผสานเซลล์ก่อนส่งออก

---

## คัดลอกช่วงไปยังเวิร์กบุ๊กอื่นด้วย Smart Markers (JSON → เซลล์เดียว)

บางครั้งคุณต้องฝัง JSON array ลงในเซลล์ Excel เพียงเซลล์เดียว เช่น เมื่อต้องส่งข้อมูลไปยังระบบ downstream ที่คาดหวังสตริง JSON  Aspose.Cells’ Smart Markers สามารถทำให้ array ถูกจัดเก็บเป็นเซลล์เดียวได้โดยตั้งค่า `ArrayAsSingle = true`

### ขั้นตอนทีละขั้นตอน

1. **โหลดเทมเพลตเวิร์กบุ๊ก** ที่มี placeholder ของ Smart Marker (เช่น `&=Items.Name`)  
2. **เตรียมอ็อบเจ็กต์ข้อมูล** – ชนิดไม่ระบุที่มีอาร์เรย์ `Items`  
3. **สร้าง `SmartMarkerProcessor`** แล้วประยุกต์ข้อมูลด้วย `ArrayAsSingle`  
4. **บันทึกเวิร์กบุ๊กที่เติมข้อมูลแล้ว**

#### ตัวอย่างโค้ดเต็ม

```csharp
using Aspose.Cells;
using System;

class SmartMarkerDemo
{
    static void Main()
    {
        // Step 1: Load the template workbook containing a smart marker like "&=Items.Name"
        Workbook templateWorkbook = new Workbook(@"YOUR_DIRECTORY\SmartMarkerTemplate.xlsx");

        // Step 2: Prepare the data object with an array of items
        var data = new
        {
            Items = new[]
            {
                new { Name = "A" },
                new { Name = "B" }
            }
        };

        // Step 3: Apply the SmartMarkerProcessor with ArrayAsSingle option
        SmartMarkerProcessor processor = new SmartMarkerProcessor(templateWorkbook);
        processor.Apply(data, new SmartMarkerOptions { ArrayAsSingle = true });

        // Step 4: Save the result – the JSON array will appear in a single cell
        templateWorkbook.Save(@"YOUR_DIRECTORY\jsonSingleCell.xlsx");
    }
}
```

**คำอธิบาย:**  
เมื่อ `ArrayAsSingle` เป็น true, Aspose.Cells จะต่อแต่ละค่าใน `Items.Name` เป็นสตริงรูปแบบ JSON (`["A","B"]`) แล้วเขียนลงในเซลล์ที่มี smart marker อยู่ วิธีนี้ช่วยหลีกเลี่ยงการสร้างแถวใหม่สำหรับแต่ละรายการของอาร์เรย์

**เมื่อใดควรใช้:** เหมาะสำหรับการส่งออกตารางการกำหนดค่า, payload ของ API, หรือสถานการณ์ใด ๆ ที่ผู้รับต้องการสตริง JSON แบบกะทัดรัดแทนการจัดเรียงเป็นตาราง

---

## เคล็ดลับเพิ่มเติม & การจัดการกรณีขอบ

| สถานการณ์ | สิ่งที่ควรระวัง | วิธีแก้แนะนำ |
|----------|-------------------|---------------|
| **Pivot Table ขนาดใหญ่** | การใช้หน่วยความจำพุ่งสูงเมื่อคัดลอก cache ขนาดใหญ่ | ตั้งค่า `WorkbookSettings.MemorySetting = MemorySetting.MemoryPreference` ก่อนโหลด |
| **ส่งออกเป็น PPTX พร้อมรูปภาพ** | รูปภาพอาจถูกแปลงเป็น raster ที่ DPI ต่ำ | ตั้งค่า `pptxOptions.ImageResolution = 300` เพื่อให้สไลด์คมชัด |
| **การจัดรูปแบบ JSON ของ Smart Marker** | อักขระพิเศษ (`"` , `\`) ทำให้ JSON ผิดพลาด | ทำการ escape ด้วยตนเองหรือใช้ `JsonSerializer` เพื่อ serialize ก่อนส่งให้ Smart Markers |
| **คัดลอกช่วงระหว่างเวอร์ชัน Excel ต่างกัน** | ไฟล์ `.xls` เก่าอาจสูญเสียรูปแบบ | บันทึกไฟล์ปลายทางเป็น `.xlsx` เพื่อรักษาฟีเจอร์สมัยใหม่ |

---

## สรุป – วิธีคัดลอก Pivot Table และทำสิ่งอื่นได้มากกว่า

เราตอบ **วิธีคัดลอก pivot table** พร้อมคงความทำงานของมันไว้, จากนั้นแสดง **การแปลง Excel เป็น PPTX**, **ทำให้กล่องข้อความแก้ไขได้ใน PPTX**, และสุดท้าย **การคัดลอกช่วงไปยังเวิร์กบุ๊กอื่น** ด้วย Smart Markers เพื่อฝัง JSON array เป็นเซลล์เดียว ทั้งสามโค้ดสแนปเป็นอิสระ; คุณสามารถวางลงในแอปคอนโซลใหม่ ปรับพาธไฟล์ แล้วรันได้ทันที

---

## สิ่งที่ควรทำต่อไป

- **สำรวจรูปแบบการส่งออกอื่น** – Aspose.Cells ยังรองรับ PDF, XPS, และ HTML  
- **รีเฟรช pivot table ด้วยโปรแกรม** โดยใช้ `PivotTable.RefreshData()` หลังการคัดลอก  
- **ผสาน Smart Markers กับแผนภูมิ** เพื่อสร้างแดชบอร์ดแบบไดนามิกที่อัปเดตอัตโนมัติ  

หากคุณสนใจ **บันทึกเวิร์กบุ๊กเป็น PPTX** พร้อมเลย์เอาต์สไลด์แบบกำหนดเอง ให้ดูเอกสาร Aspose.Cells เกี่ยวกับ `SlideOptions`  

อย่ากลัวทดลอง—เปลี่ยนพื้นที่พิมพ์, ลอง `CopyOptions` ต่าง ๆ, หรือป้อน payload JSON ที่ซับซ้อนมากขึ้น API มีความยืดหยุ่นพอสำหรับ pipeline รายงานส่วนใหญ่

---

### คำถามที่พบบ่อย

**ถาม: `CopyPivotTable` คัดลอก slicer ด้วยหรือไม่?**  
ตอบ: ไม่โดยตรง Slicer เป็นอ็อบเจ็กต์แยก คุณต้องสร้างใหม่หรือคัดลอกผ่านคอลเลกชัน `Worksheet.Shapes` หลังการคัดลอก

**ถาม: สามารถส่งออกหลายแผ่นงานเป็นเด็ค PPTX เดียวได้หรือไม่?**  
ตอบ: ได้ ลูปผ่านแต่ละแผ่นงาน, เรียก `Save` ด้วย `ImageOrPrintOptions` เดียวกันและตั้งค่า `pptxOptions.StartSlideNumber` เพื่อให้หมายเลขสไลด์ต่อเนื่อง

**ถาม: ถ้า JSON array มีอ็อบเจ็กต์ซ้อนอยู่จะทำอย่างไร?**  
ตอบ: ตั้งค่า `ArrayAsSingle = false` แล้วใช้เทมเพลตที่กำหนดให้วนลูปผ่านโครงสร้างซ้อนกัน

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}