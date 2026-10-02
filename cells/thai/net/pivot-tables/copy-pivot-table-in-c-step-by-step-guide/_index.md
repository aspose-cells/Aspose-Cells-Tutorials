---
category: general
date: 2026-03-18
description: คัดลอก Pivot Table ใน C# ด้วย Aspose.Cells. เรียนรู้วิธีคัดลอกช่วงของ
  Excel, ทำสำเนา Pivot ของ Excel, คัดลอกช่วงไปยังแผ่นงานใหม่และคัดลอก Pivot ไปยังแผ่นงานในเวลาไม่กี่นาที.
draft: false
keywords:
- copy pivot table
- copy excel range
- duplicate excel pivot
- copy range to new
- copy pivot to sheet
language: th
og_description: คัดลอกตาราง Pivot ใน C# ด้วย Aspose.Cells. เรียนรู้การทำสำเนาตาราง
  Pivot ของ Excel, การคัดลอกช่วงข้อมูล Excel ไปยังตำแหน่งใหม่, และการคัดลอก Pivot
  ไปยังแผ่นงานพร้อมตัวอย่างโค้ดเต็ม.
og_title: คัดลอก Pivot Table ใน C# – คู่มือการเขียนโปรแกรมฉบับสมบูรณ์
tags:
- Aspose.Cells
- C#
- Excel automation
title: คัดลอก Pivot Table ใน C# – คู่มือแบบทีละขั้นตอน
url: /th/net/pivot-tables/copy-pivot-table-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# คัดลอก Pivot Table ใน C# – คู่มือการเขียนโปรแกรมฉบับสมบูรณ์

เคยต้องการ **คัดลอก Pivot Table** จากส่วนหนึ่งของเวิร์กบุ๊กไปยังอีกส่วนหนึ่ง แต่ไม่แน่ใจว่าจะทำอย่างไรโดยไม่ทำให้การเชื่อมต่อข้อมูลพื้นฐานหายไปหรือไม่? คุณไม่ได้อยู่คนเดียว นักพัฒนาหลายคนเจออุปสรรคนี้เมื่อต้องอัตโนมัติรายงาน Excel โดยเฉพาะเมื่อ Pivot อยู่ภายในบล็อกข้อมูลที่ใหญ่กว่า ข่าวดีคือ? ด้วย Aspose.Cells คุณสามารถคัดลอก Pivot Table **ได้อย่างตรงตามที่แสดง** และคุณยังจะได้เรียนรู้วิธี **คัดลอก Excel Range**, **ทำซ้ำ Excel Pivot**, และแม้กระทั่ง **คัดลอก Pivot ไปยังแผ่นงาน** เพียงไม่กี่บรรทัดของ C# อีกด้วย

ในบทแนะนำนี้เราจะเดินผ่านสถานการณ์จริง: ย้าย Pivot ที่ครอบคลุม *A1:J20* ไปยังพื้นที่ใหม่ *M1:V20* ในแผ่นงานเดียวกัน เมื่อจบคุณจะมีโปรแกรมที่รันได้ เข้าใจว่าทำไมแต่ละขั้นตอนถึงสำคัญ และรู้วิธีปรับโค้ดสำหรับช่วงอื่นหรือแม้กระทั่งแผ่นงานแยกต่างหาก ไม่ต้องอ้างอิงเอกสารภายนอก—ทุกอย่างอยู่ที่นี่แล้ว

---

## Prerequisites

ก่อนที่เราจะดำเนินการต่อ โปรดตรวจสอบว่าคุณมี:

- **Aspose.Cells for .NET** (เวอร์ชัน 23.9 หรือใหม่กว่า) คุณสามารถติดตั้งผ่าน NuGet: `Install-Package Aspose.Cells`.
- สภาพแวดล้อมการพัฒนา C# เบื้องต้น (Visual Studio 2022, Rider หรือ VS Code พร้อมส่วนขยาย C#).
- ไฟล์ Excel (`source.xlsx`) ที่มี Pivot Table อยู่ในช่วง *A1:J20*.

เท่านี้เอง หากคุณคุ้นเคยกับการสร้างแอปคอนโซล คุณก็พร้อมเริ่มแล้ว

---

## How to copy pivot table in Aspose.Cells

หัวใจของวิธีแก้คือการเรียก `Worksheet.Cells.CopyRange` เพียงครั้งเดียว เมธอดนี้ไม่เพียงคัดลอกค่าของเซลล์เท่านั้น แต่ยังคง Pivot Table, แผนภูมิ และอ็อบเจ็กต์อื่น ๆ ที่ซับซ้อนได้โดยอัตโนมัติ มาแยกย่อยกันดู

### Step 1: Load the source workbook

ก่อนอื่นเราต้องโหลดเวิร์กบุ๊กเข้าสู่หน่วยความจำ

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Load the source workbook from disk
        Workbook sourceWorkbook = new Workbook(@"YOUR_DIRECTORY\source.xlsx");
```

> **Why this matters:** การโหลดเวิร์กบุ๊กจะสร้างตัวแทนในหน่วยความจำที่ Aspose.Cells สามารถจัดการได้โดยไม่ต้องเปิด Excel ทำให้เร็ว ปลอดภัยต่อเธรด และทำงานบนเซิร์ฟเวอร์ได้

### Step 2: Grab the first worksheet

ตัวอย่างส่วนใหญ่ใช้แผ่นงานแรก แต่คุณสามารถเลือกตามดัชนีหรือชื่อใดก็ได้

```csharp
        // Access the first worksheet (index 0)
        Worksheet worksheet = sourceWorkbook.Worksheets[0];
```

> **Tip:** หากคุณต้องการ **copy pivot to sheet** แทนการคัดลอกในแผ่นเดียวกัน เพียงเปลี่ยนการอ้างอิง `worksheet` ไปยังอ็อบเจ็กต์ `Worksheet` อื่น

### Step 3: Define the source and target ranges

เราจะใช้โครงสร้าง `CellArea` เพื่ออธิบายบล็อกที่กำลังย้าย

```csharp
        // Define the source range (A1:J20) that contains the pivot table
        CellArea sourceRange = new CellArea(0, 0, 19, 9);   // rows 0‑19, columns 0‑9

        // Define the target range (M1:V20) where the data will be copied
        CellArea targetRange = new CellArea(0, 12, 19, 21); // rows 0‑19, columns 12‑21
```

> **Explanation:** ดัชนีแถวและคอลัมน์เริ่มจากศูนย์ Column 0 = **A**, column 12 = **M** เป็นต้น ปรับตัวเลขเหล่านี้หาก Pivot ของคุณอยู่ที่อื่น

### Step 4: Perform the copy operation

ตอนนี้จุดสำคัญเกิดขึ้น การตั้งค่าพารามิเตอร์บูลีนสุดท้ายเป็น `true` บอก Aspose.Cells ให้คัดลอกอ็อบเจ็กต์ทั้งหมดรวมถึง Pivot ด้วย

```csharp
        // Copy the source range to the target range; pivot tables are copied automatically
        worksheet.Cells.CopyRange(
            sourceRange.StartRow, sourceRange.StartColumn,
            sourceRange.EndRow, sourceRange.EndColumn,
            targetRange.StartRow, targetRange.StartColumn,
            true);
```

> **Why `true`?** ธงนี้หมายถึง “คัดลอกอ็อบเจ็กต์ทั้งหมด” หากตั้งเป็น `false` จะคัดลค่าเซลล์ธรรมดาเท่านั้นและ Pivot จะหายไป

### Step 5: Save the workbook

สุดท้ายให้บันทึกเวิร์กบุ๊กที่แก้ไขกลับไปยังดิสก์

```csharp
        // Save the workbook with the copied range
        sourceWorkbook.Save(@"YOUR_DIRECTORY\copy-pivot.xlsx");
    }
}
```

> **Result:** `copy-pivot.xlsx` ตอนนี้มี Pivot ดั้งเดิมที่ *A1:J20* **และ** สำเนาเดียวกันที่ *M1:V20* เปิดไฟล์ใน Excel เพื่อตรวจสอบว่าทั้งสอง Pivot ทำงานและยังคงการเชื่อมต่อข้อมูลอยู่

---

## Copy Excel range to a new location – a quick variation

บางครั้งคุณอาจต้องการ **copy excel range** เพียงอย่างเดียวโดยไม่สนใจ Pivot เมธอด `CopyRange` เดิมก็ทำได้—แค่ตั้งอาร์กิวเมนต์สุดท้ายเป็น `false`

```csharp
worksheet.Cells.CopyRange(
    sourceRange.StartRow, sourceRange.StartColumn,
    sourceRange.EndRow, sourceRange.EndColumn,
    targetRange.StartRow, targetRange.StartColumn,
    false); // plain values only
```

> **When to use:** หากคุณกำลังย้ายข้อมูลดิบเพื่อใช้ในแผ่นคำนวณชั่วคราว การปิดการคัดลอกอ็อบเจ็กต์จะช่วยประหยัดหน่วยความจำและเร่งความเร็วของการทำงาน

---

## Duplicate excel pivot across multiple sheets

ต้องการ **duplicate excel pivot** บนแผ่นงานอื่นหรือไม่? แนวทางยังคงเหมือนเดิม; เพียงอ้างอิง `Worksheet` อื่นเป็นปลายทาง

```csharp
// Assume we have a second sheet already created
Worksheet destSheet = sourceWorkbook.Worksheets.Add("PivotCopy");

// Copy the pivot (and its data source) to the new sheet starting at A1
destSheet.Cells.CopyRange(
    sourceRange.StartRow, sourceRange.StartColumn,
    sourceRange.EndRow, sourceRange.EndColumn,
    0, 0, // destination at A1
    true);
```

> **Edge case:** หาก Pivot ต้นทางใช้ตารางที่อยู่บนแผ่นงานเดิม Aspose.Cells จะคัดลอกคำนิยามตารางพื้นฐานด้วย ทำให้ Pivot ใหม่ทำงานได้ทันที

---

## Common pitfalls and how to avoid them

| ข้อผิดพลาด | สาเหตุ | วิธีแก้ |
|------------|--------|----------|
| **Pivot สูญเสียแคช** | ใช้ `CopyRange` กับ `false` หรือกระบวนการคัดลอกแบบกำหนดเองที่ละเว้นอ็อบเจ็กต์ | ควรส่งค่า `true` เสมอเมื่อคุณต้องการ Pivot เอง |
| **เซลล์เป้าหมายมีข้อมูลอยู่แล้ว** | เขียนทับโดยไม่มีการแจ้งเตือน อาจทำให้สูตรที่มีอยู่เสียหาย | ล้างพื้นที่เป้าหมายก่อน: `worksheet.Cells.ClearRange(targetRange.StartRow, targetRange.StartColumn, targetRange.EndRow, targetRange.EndColumn, true);` |
| **ช่วงต้นทางไม่ได้รวม Pivot ทั้งหมด** | Pivot Table มีแถว/คอลัมน์มากกว่าที่คุณคาดคิด (เช่น แถวที่ซ่อนอยู่) | ใช้ `worksheet.PivotTables[0].DataRange` เพื่อดึงขอบเขตที่แน่นอนได้โดยอัตโนมัติ |
| **คัดลอกระหว่างเวิร์กบุ๊ก** | `CopyRange` ทำงานได้เฉพาะภายในเวิร์กบุ๊กเดียว | ใช้ `sourceWorksheet.Cells.CopyRange` ไปยังช่วงชั่วคราว แล้ว `destWorkbook.Worksheets.AddCopy(sourceWorksheet);` |

---

## Expected output & verification

หลังจากรันโปรแกรม:

1. เปิดไฟล์ `copy-pivot.xlsx`.
2. คุณจะเห็น Pivot Table สองตารางที่เหมือนกัน—หนึ่งที่ **A1:J20**, อีกหนึ่งที่ **M1:V20**.
3. รีเฟรช Pivot ใดก็ได้; ทั้งสองควรแสดงข้อมูลพื้นฐานเดียวกัน.
4. หากคุณทำการทำซ้ำไปยังแผ่นงานอื่น แผ่นงานใหม่จะมีสำเนาที่ทำงานได้เช่นกัน.

วิธีตรวจสอบอย่างรวดเร็วด้วยโค้ด:

```csharp
int pivotCount = worksheet.PivotTables.Count; // should be 2 after copy
Console.WriteLine($"Pivot tables on the sheet: {pivotCount}");
```

---

## Pro tip: Automate range detection

การเขียนค่า `CellArea` แบบคงที่ทำได้กับรายงานที่ไม่เปลี่ยนแปลง แต่โค้ดในสภาพแวดล้อมจริงมักต้องค้นหา Pivot อย่างไดนามิก

```csharp
// Find the first pivot table on the sheet
PivotTable pt = worksheet.PivotTables[0];
CellArea ptRange = pt.DataRange;

// Use the detected range for copying
worksheet.Cells.CopyRange(
    ptRange.StartRow, ptRange.StartColumn,
    ptRange.EndRow, ptRange.EndColumn,
    targetRange.StartRow, targetRange.StartColumn,
    true);
```

> **Why bother?** วิธีนี้ทำให้โซลูชันของคุณทนต่อการเปลี่ยนแปลงเลย์เอาต์—ไม่ต้องเจอข้อผิดพลาด “Oops, the pivot moved to B2” อีกต่อไป

---

![ตัวอย่างการคัดลอก Pivot Table](copy-pivot.png){alt="ตัวอย่างการคัดลอก Pivot Table"}

*ภาพหน้าจอ (placeholder) แสดง Pivot ดั้งเดิมทางซ้ายและสำเนาที่ทำซ้ำทางขวา.*

---

## Recap

เราได้อธิบายวิธี **copy pivot table** ใน C# ด้วย Aspose.Cells, สำรวจวิธี **copy excel range**, **duplicate excel pivot**, และแม้กระทั่ง **copy pivot to sheet** ข้ามแผ่นงาน จุดสำคัญที่ควรจำคือ:

- ใช้ `Worksheet.Cells.CopyRange` พร้อมแฟล็ก `true` เพื่อคงอ็อบเจ็กต์ที่ซับซ้อน
- กำหนดอ็อบเจ็กต์ `CellArea` ของต้นทางและปลายทางโดยใช้ดัชนีเริ่มจากศูนย์
- ปรับแผ่นงานปลายทางหากต้องการ **copy pivot to sheet**
- ระวังกรณีขอบเช่นข้อมูลที่มีอยู่แล้ว, แถวที่ซ่อนอยู่, และสถานการณ์การคัดลอกจากเวิร์กบุ๊กอื่น

---

## What’s next?

- **Dynamic pivot discovery**: สร้างตัวช่วยที่สแกนเวิร์กบุ๊กเพื่อค้นหา Pivot ทั้งหมดและทำซ้ำโดยอัตโนมัติ.
- **Export to PDF/HTML**: หลังจากคัดลอก คุณอาจต้องการแปลงแผ่นงานเป็นรูปแบบรายงาน—Aspose.Cells รองรับเช่นกัน.
- **Performance tuning**: สำหรับเวิร์กบุ๊กขนาดใหญ่ ให้พิจารณาปิดการคำนวณก่อนคัดลอกและเปิดใหม่หลังจากนั้น.

ลองทดลองเปลี่ยนพิกัดเป้าหมาย, คัดลอกไปยังเวิร์กบุ๊กใหม่, หรือแม้กระทั่งวนลูปผ่านหลายแผ่นงานเพื่อสร้างรายงานสรุป ความเป็นไปได้ไม่มีที่สิ้นสุด และด้วยพื้นฐานที่คุณมีอยู่ตอนนี้ คุณจะสามารถปรับโค้ดให้เข้ากับงานอัตโนมัติของ Excel ใด ๆ ได้อย่างง่ายดาย

Happy coding, and may your pivots always stay perfectly in sync!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}