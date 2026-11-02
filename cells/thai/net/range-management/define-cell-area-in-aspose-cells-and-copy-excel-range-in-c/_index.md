---
category: general
date: 2026-08-04
description: กำหนดพื้นที่เซลล์ใน Aspose.Cells และเรียนรู้วิธีคัดลอกตาราง Pivot, คัดลอกช่วง
  Excel ด้วย C#, และคัดลอกช่วงในแผ่นเดียวอย่างมีประสิทธิภาพ.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- define cell area
- how to copy pivot
- copy excel range c#
- copy range same sheet
- aspose.cells copy range
language: th
lastmod: 2026-08-04
og_description: กำหนดพื้นที่เซลล์ใน Aspose.Cells และคัดลอกช่วง Excel ด้วย C# พร้อมคงรักษาตาราง
  Pivot ไว้ตามเดิม ปฏิบัติตามคู่มือขั้นตอนต่อขั้นตอนนี้เพื่อผลลัพธ์ที่เชื่อถือได้
og_image_alt: Screenshot showing how to define cell area and copy range in Aspose.Cells
og_title: กำหนดพื้นที่เซลล์ใน Aspose.Cells – คัดลอกช่วง Excel ใน C#
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Define cell area in Aspose.Cells and learn how to copy pivot tables,
    copy Excel range C#, and copy range same sheet efficiently.
  headline: Define cell area in Aspose.Cells and copy Excel range in C#
  type: TechArticle
- description: Define cell area in Aspose.Cells and learn how to copy pivot tables,
    copy Excel range C#, and copy range same sheet efficiently.
  name: Define cell area in Aspose.Cells and copy Excel range in C#
  steps:
  - name: The range A61:J110 contains a copy of the original data.
    text: The range A61:J110 contains a copy of the original data.
  - name: A new pivot table appears at the top of the copied range.
    text: A new pivot table appears at the top of the copied range.
  - name: Refreshing the pivot reflects changes in the source data, confirming that
      **how to copy pivot** succeeded.
    text: Refreshing the pivot reflects changes in the source data, confirming that
      **how to copy pivot** succeeded.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
- Pivot tables
title: กำหนดพื้นที่เซลล์ใน Aspose.Cells และคัดลอกช่วง Excel ด้วย C#
url: /th/net/range-management/define-cell-area-in-aspose-cells-and-copy-excel-range-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# กำหนดพื้นที่เซลล์ใน Aspose.Cells และคัดลอกช่วง Excel ด้วย C#

หากคุณต้องการ **define cell area** สำหรับช่วงแล้วคัดลอกช่วงนั้นในแผ่นงานเดียวกัน คู่มือนี้จะแสดงวิธีทำอย่างละเอียดด้วย Aspose.Cells สำหรับ .NET ไม่ว่าคุณจะย้ายรายงานที่ขับเคลื่อนด้วย pivot หรือทำสำเนาบล็อกข้อมูล คุณจะได้เรียนรู้กระบวนการทั้งหมดในไม่กี่ขั้นตอน

คุณยังจะได้ค้นพบ **how to copy pivot** ตารางโดยไม่สูญเสียการเชื่อมต่อ และเห็นตัวอย่างที่ชัดเจนของ **copy excel range c#** ที่ทำงานในสถานการณ์ **copy range same sheet** ไม่ต้องใช้เครื่องมือภายนอก—แค่ Aspose.Cells และบรรทัดโค้ด C# ไม่กี่บรรทัด

## สิ่งที่คุณต้องเตรียม

- .NET 6.0 หรือใหม่กว่า (โค้ดนี้ยังทำงานกับ .NET Framework 4.7+)
- Aspose.Cells for .NET (NuGet package `Aspose.Cells`)
- ไฟล์ Excel workbook (`input.xlsx`) ที่มีตาราง pivot อยู่ในช่วง A1:J50
- สภาพแวดล้อมการพัฒนา เช่น Visual Studio 2022

## ขั้นตอนที่ 1: กำหนดพื้นที่เซลล์สำหรับช่วงต้นทาง

งานแรกคือ **define cell area** ที่แสดงบล็อกที่คุณต้องการคัดลอก Aspose.Cells ใช้โครงสร้าง `CellArea` ซึ่งเก็บดัชนีแถวและคอลัมน์แบบศูนย์‑ฐาน

```csharp
using Aspose.Cells;

// Load the source workbook
Workbook srcWorkbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

// Define the source range that contains the pivot table (A1:J50)
CellArea sourceRange = new CellArea
{
    StartRow = 0,      // Row 1 (zero‑based)
    StartColumn = 0,   // Column A
    EndRow = 49,       // Row 50
    EndColumn = 9      // Column J
};
```

**ทำไมเรื่องนี้สำคัญ:** `CellArea` บอก Aspose.Cells ว่าจะทำงานกับเซลล์ใดโดยตรง การใช้ดัชนีศูนย์‑ฐานช่วยหลีกเลี่ยงข้อผิดพลาด off‑by‑one ที่พบบ่อยเมื่อแปลงการอ้างอิงแบบ A1 ของ Excel ไปเป็นโค้ด

## ขั้นตอนที่ 2: กำหนดพื้นที่เซลล์ปลายทางบนแผ่นงานเดียวกัน

เพื่อ **copy range same sheet** คุณต้องระบุตำแหน่งที่ข้อมูลจะวางด้วย ปลายทางสามารถเริ่มที่แถวใดก็ได้ ในที่นี้เราเริ่มที่แถว 61 (ดัชนีศูนย์‑ฐาน 60) เพื่อเว้นบัฟเฟอร์ว่าง

```csharp
// Define the destination area on the same sheet (starting at row 61)
CellArea destinationRange = new CellArea
{
    StartRow = 60,     // Row 61
    StartColumn = 0,   // Column A
    EndRow = 109,      // Row 110 (same height as source)
    EndColumn = 9      // Column J (same width as source)
};
```

**ทำไมเรื่องนี้สำคัญ:** การทำให้มิติของปลายทางตรงกับต้นทางทำให้บล็อกที่คัดลอกพอดีโดยไม่มีการตัดทอน

## ขั้นตอนที่ 3: คัดลอกช่วงพร้อมคงรักษาตาราง pivot

ตอนนี้คุณสามารถ **how to copy pivot** อย่างปลอดภัย คลาส `CopyOptions` มีแฟล็ก `CopyPivotTables` ที่คงรักษาการกำหนด pivot, แหล่งข้อมูล, และรูปแบบ

```csharp
// Copy the range while preserving pivot tables
srcWorkbook.Worksheets[0].Cells.CopyRange(
    sourceRange,
    destinationRange,
    new CopyOptions
    {
        CopyPivotTables = true   // Ensure pivot tables are retained
    });
```

**ทำไมเรื่องนี้สำคัญ:** หากไม่ได้ตั้งค่า `CopyPivotTables = true` pivot จะกลายเป็นภาพนิ่งสูญเสียการโต้ตอบ ตัวเลือกนี้คัดลอกแคชและการเชื่อมต่อพื้นฐาน ทำให้ pivot ใหม่ทำงานเหมือนต้นฉบับ

## ขั้นตอนที่ 4: บันทึกเวิร์กบุ๊ก

สุดท้ายให้เขียนการเปลี่ยนแปลงกลับไปยังดิสก์ ไฟล์ผลลัพธ์แสดงว่าตาราง pivot ถูกทำสำเนาในแผ่นงานเดียวกัน

```csharp
// Save the modified workbook
srcWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx");
```

**เคล็ดลับ:** ใช้ `srcWorkbook.Save("CopyWithPivot.xlsx", SaveFormat.Xlsx)` หากคุณต้องการบังคับใช้รูปแบบเฉพาะ โดยเฉพาะเมื่อทำงานกับเวอร์ชัน Excel เก่า

## ขั้นตอนที่ 5: ตรวจสอบตาราง pivot ที่คัดลอก

เปิด `CopyWithPivot.xlsx` ใน Excel แล้วตรวจสอบดังต่อไปนี้:

1. ช่วง A61:J110 มีสำเนาของข้อมูลต้นฉบับ
2. ตาราง pivot ใหม่ปรากฏที่ด้านบนของช่วงที่คัดลอก
3. การรีเฟรช pivot แสดงการเปลี่ยนแปลงในข้อมูลต้นทาง ยืนยันว่า **how to copy pivot** สำเร็จ

หาก pivot ไม่รีเฟรช ให้ตรวจสอบว่าช่วงข้อมูลต้นทางในการกำหนดของ pivot ยังชี้ไปยังพื้นที่เวิร์กบุ๊กต้นฉบับอยู่หรือไม่ Aspose.Cells จะอัปเดตการอ้างอิงต้นทางโดยอัตโนมัติเมื่อ `CopyPivotTables` เป็น true

## กรณีขอบและการเปลี่ยนแปลง

| สถานการณ์ | สิ่งที่ต้องเปลี่ยน |
|-----------|----------------|
| **คัดลอกไปยังแผ่นงานอื่น** | แทนที่ `srcWorkbook.Worksheets[0]` ด้วยดัชนีหรือชื่อแผ่นงานเป้าหมาย และปรับ `destinationRange` ให้สอดคล้อง |
| **คัดลอกบล็อกเซลล์ที่รวมกัน** | ตั้งค่า `CopyOptions.PasteType = PasteType.All` เพื่อคงรักษาเซลล์ที่รวมและรูปแบบ |
| **คัดลอกเฉพาะค่า ไม่ใช่สูตร** | ใช้ `CopyOptions.PasteType = PasteType.Values` เพื่อหลีกเลี่ยงการคัดลอกสูตรที่อ้างอิงแผ่นงานต้นฉบับ |
| **ช่วงใหญ่ ( > 10,000 แถว )** | พิจารณาใช้ `Workbook.Copy` สำหรับแผ่นงานทั้งหมดเพื่อเพิ่มประสิทธิภาพ แล้วลบแถวที่ไม่ต้องการ |

การเปลี่ยนแปลงเหล่านี้แสดงให้เห็นว่าตรรกะ **aspose.cells copy range** เดียวกันสามารถปรับใช้กับสถานการณ์จริงหลายแบบ

## ตัวอย่างทำงานเต็มรูปแบบ

ด้านล่างเป็นโปรแกรมที่สมบูรณ์พร้อมรัน แทนที่ `YOUR_DIRECTORY` ด้วยเส้นทางโฟลเดอร์จริงบนเครื่องของคุณ

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Load the source workbook
        Workbook srcWorkbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Step 1: Define the source cell area (A1:J50)
        CellArea sourceRange = new CellArea
        {
            StartRow = 0,
            StartColumn = 0,
            EndRow = 49,
            EndColumn = 9
        };

        // Step 2: Define the destination cell area on the same sheet (A61:J110)
        CellArea destinationRange = new CellArea
        {
            StartRow = 60,
            StartColumn = 0,
            EndRow = 109,
            EndColumn = 9
        };

        // Step 3: Copy the range while preserving pivot tables
        srcWorkbook.Worksheets[0].Cells.CopyRange(
            sourceRange,
            destinationRange,
            new CopyOptions { CopyPivotTables = true });

        // Step 4: Save the modified workbook
        srcWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx");
    }
}
```

**ผลลัพธ์ที่คาดหวัง:** หลังจากรันโปรแกรม `CopyWithPivot.xlsx` จะมีข้อมูลต้นฉบับพร้อมบล็อกที่เหมือนกันเริ่มที่แถว 61 พร้อมตาราง pivot ที่ทำงานได้

## สรุป

ตอนนี้คุณรู้วิธี **define cell area** ใน Aspose.Cells, **copy excel range c#**, และ **copy range same sheet** พร้อมคงรักษาฟังก์ชันของ pivot ทั้งหมด เทคนิคนี้ขจัดข้อผิดพลาดจากการคัดลอก‑วางด้วยมือและสามารถขยายไปยังเวิร์กบุ๊กขนาดใหญ่ได้

ต่อไปสำรวจหัวข้อที่เกี่ยวข้องเช่น **how to copy pivot** ข้ามหลายแผ่นงาน หรือใช้ **aspose.cells copy range** เพื่อทำสำเนาแผ่นงานทั้งหมดพร้อมรูปแบบ ทดลองตั้งค่า `CopyOptions` ต่าง ๆ เพื่อปรับพฤติกรรมการคัดลอกให้ตรงกับความต้องการของโครงการของคุณ

ขอให้เขียนโค้ดอย่างสนุกสนาน!

## คุณควรเรียนรู้อะไรต่อไป?

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งข้อมูลมีตัวอย่างโค้ดทำงานครบถ้วนพร้อมคำอธิบายทีละขั้นตอน เพื่อช่วยคุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจวิธีการทำงานทางเลือกในโครงการของคุณ

- [Excel Aspose Cells Dotnet คัดลอกข้อมูลช่วง](/cells/hindi/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)
- [Excel Aspose Cells Dotnet คัดลอกข้อมูลช่วง](/cells/spanish/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)
- [Excel Aspose Cells Dotnet คัดลอกข้อมูลช่วง](/cells/german/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}