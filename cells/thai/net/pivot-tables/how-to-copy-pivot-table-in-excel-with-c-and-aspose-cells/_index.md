---
category: general
date: 2026-10-04
description: เรียนรู้วิธีคัดลอก Pivot Table จากเวิร์กบุ๊กหนึ่งไปยังอีกเวิร์กบุ๊กหนึ่งโดยใช้
  C# คู่มือนี้ยังครอบคลุมวิธีคัดลอกแถว, ทำสำเนา Pivot Table, และคัดลอกช่วงของ Excel
  อย่างมีประสิทธิภาพ.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- how to copy pivot
- copy excel range
- how to copy rows
- duplicate pivot table
language: th
lastmod: 2026-10-04
og_description: คัดลอก Pivot Table ใน Excel ด้วย C# ทำตามบทเรียนฉบับเต็มนี้เพื่อทำสำเนา
  Pivot Table, คัดลอกแถว, และคัดลอกช่วงของ Excel ด้วย Aspose.Cells.
og_image_alt: Screenshot showing a duplicated pivot table in an Excel worksheet after
  using C# code
og_title: คัดลอก Pivot Table ใน Excel ด้วย C# – คู่มือขั้นตอนต่อขั้นตอน
schemas:
- author: Aspose
  dateModified: '2026-10-04'
  description: Learn how to copy pivot table from one workbook to another using C#.
    This guide also covers how to copy rows, duplicate pivot table, and copy Excel
    range efficiently.
  headline: How to copy pivot table in Excel with C# and Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: วิธีคัดลอก Pivot Table ใน Excel ด้วย C# และ Aspose.Cells
url: /th/net/pivot-tables/how-to-copy-pivot-table-in-excel-with-c-and-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีคัดลอก Pivot Table ใน Excel ด้วย C# และ Aspose.Cells

หากคุณต้องการ **คัดลอก pivot table** จากเวิร์กบุ๊กหนึ่งไปยังอีกเวิร์กบุ๊กหนึ่ง บทแนะนำนี้จะแสดงวิธีแก้ไขที่สมบูรณ์และสามารถรันได้ คุณจะได้เห็นขั้นตอนการโหลดไฟล์ต้นทาง, กำหนดช่วงที่มี pivot, คัดลอกแถว (รวมถึงการกำหนด pivot) และบันทึกผล ไม่ว่าคุณจะทำอัตโนมัติการสร้างรายงานหรือสร้างเครื่องมือการย้ายข้อมูล ขั้นตอนต่อไปนี้จะช่วยให้คุณทำสำเนา pivot table ได้ด้วยเพียงไม่กี่บรรทัดของ C#.

การคัดลอก pivot table ไม่ได้เป็นเพียงการคัดลอกค่าของเซลล์; แคชและการตั้งค่าฟิลด์ที่อยู่ภายใต้ต้องถูกคัดลอกไปด้วย ตัวอย่างนี้ใช้ไลบรารี **Aspose.Cells** เนื่องจากมันจัดการเมตาดาต้า pivot โดยอัตโนมัติ ทำให้คุณไม่ต้องสร้างแคชใหม่ด้วยตนเอง เมื่อจบคู่มือคุณจะสามารถ **how to copy pivot**, **copy excel range**, และ **how to copy rows** ได้อย่างปลอดภัย.

## ข้อกำหนดเบื้องต้น

- .NET 6.0 หรือใหม่กว่า (โค้ดนี้ยังทำงานกับ .NET Framework 4.7+)
- ใบอนุญาต Aspose.Cells for .NET ที่ถูกต้องหรือใบอนุญาตทดลองใช้ชั่วคราว
- ไฟล์ Excel สองไฟล์: `Source.xlsx` ที่มี pivot table ที่คุณต้องการทำสำเนา, และโฟลเดอร์ว่างที่ไฟล์ `CopyWithPivot.xlsx` จะถูกเขียน
- Visual Studio 2022 (หรือ IDE ใดก็ได้ที่รองรับ C#)

## ขั้นตอนที่ 1: ตั้งค่าโปรเจกต์และเพิ่ม Aspose.Cells

สร้างโปรเจกต์คอนโซลใหม่และเพิ่มแพคเกจ NuGet ของ Aspose.Cells:

```bash
dotnet new console -n PivotCopyDemo
cd PivotCopyDemo
dotnet add package Aspose.Cells
```

แพคเกจนี้ให้คลาส `Workbook`, `Worksheet`, และ `CellArea` ที่ใช้ในโค้ดด้านล่าง

## ขั้นตอนที่ 2: โหลดเวิร์กบุ๊กต้นทางที่มี pivot table

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // Load the source workbook that holds the pivot you want to duplicate
        Workbook srcWorkbook = new Workbook(@"YOUR_DIRECTORY/Source.xlsx");
```

> **ทำไมเรื่องนี้สำคัญ:** การโหลดเวิร์กบุ๊กจะสร้างการแสดงผลในหน่วยความจำของทุกแผ่นงาน รวมถึงแคช pivot ที่ซ่อนอยู่ หากไม่ได้โหลดไฟล์ คุณจะไม่สามารถอ้างอิงช่วงของ pivot ได้.

## ขั้นตอนที่ 3: กำหนดช่วงเซลล์ที่ครอบคลุม pivot table

คุณต้องบอก Aspose.Cells ว่าแถวและคอลัมน์ใดเป็นของ pivot. โครงสร้าง `CellArea` ให้คุณระบุบล็อกสี่เหลี่ยม.

```csharp
        // Define the rectangle that encloses the pivot table (adjust as needed)
        CellArea sourceRange = new CellArea
        {
            StartRow = 0,      // first row (zero‑based)
            StartColumn = 0,   // first column
            EndRow = 30,       // last row of the pivot
            EndColumn = 10     // last column of the pivot
        };
```

> **เคล็ดลับ:** หากคุณไม่แน่ใจเกี่ยวกับขนาดที่แน่นอน ให้เปิดไฟล์ต้นทางใน Excel, เลือก pivot, แล้วดูช่วงที่แสดงใน Name Box (เช่น `A1:K31`). แปลงพิกัด Excel เป็นดัชนีเริ่มจากศูนย์สำหรับโค้ด.

## ขั้นตอนที่ 4: สร้างเวิร์กบุ๊กปลายทางใหม่และดึงแผ่นงานแรกของมัน

```csharp
        // Create an empty workbook that will receive the copied pivot
        Workbook destWorkbook = new Workbook();
        Worksheet destWorksheet = destWorkbook.Worksheets[0];
```

> **ทำไมขั้นตอนนี้จึงจำเป็น:** เวิร์กบุ๊กปลายทางต้องมีอยู่ก่อนที่คุณจะคัดลอกแถวได้ Aspose.Cells จะสร้างแผ่นงานเริ่มต้นโดยอัตโนมัติ ซึ่งเราจะใช้เป็นเป้าหมาย.

## ขั้นตอนที่ 5: คัดลอกแถว (รวมถึง pivot table) จากต้นทางไปยังปลายทาง

เมธอด `CopyRows` จะคัดลอกทั้งค่าของเซลล์และแคช pivot ที่อยู่ภายใต้.

```csharp
        // Copy rows from source to destination, preserving the pivot definition
        destWorksheet.Cells.CopyRows(
            srcWorkbook.Worksheets[0].Cells,      // source cells
            sourceRange.StartRow,                 // first row to copy
            sourceRange.EndRow - sourceRange.StartRow + 1, // number of rows
            destWorksheet.Cells,                  // target cells
            sourceRange.StartRow);                // target start row
```

> **วิธีการทำงาน:**  
> - `CopyRows` รับแผ่นงานต้นทาง, แถวเริ่มต้น, และจำนวนแถวที่จะคัดลอก  
> - มันยังรับแผ่นงานปลายทางและแถวที่การคัดลอกจะเริ่มต้น  
> - เนื่องจากช่วงต้นทางรวม pivot table เมธอดจึงโอนย้ายแคช, รายการฟิลด์, และรูปแบบของ pivot อย่างครบถ้วน นี่คือหัวใจของ **how to copy pivot** ที่ไม่สูญเสียฟังก์ชัน

### กรณีพิเศษ: การคัดลอก pivot ที่ขยายข้ามหลายแผ่นงาน

หากข้อมูลต้นทางของ pivot อยู่บนแผ่นงานอื่นที่แตกต่างจาก pivot เอง แคชยังคงถูกคัดลอกไปด้วยเนื่องจาก Aspose.Cells เก็บแคชไว้ในระดับเวิร์กบุ๊ก ไม่ใช่ในแผ่นงาน อย่างไรก็ตาม คุณต้องตรวจสอบให้แน่ใจว่าเวิร์กบุ๊กปลายทางมีช่วงข้อมูลต้นทางเดียวกัน; หากไม่เช่นนั้น pivot จะแสดงข้อผิดพลาด `#REF!`. ในกรณีเช่นนี้ ให้คัดลอกช่วงข้อมูลต้นทางก่อน แล้วคัดลอกแถวของ pivot.

## ขั้นตอนที่ 6: บันทึกเวิร์กบุ๊กที่ตอนนี้มี pivot table ที่คัดลอกแล้ว

```csharp
        // Persist the destination workbook to disk
        destWorkbook.Save(@"YOUR_DIRECTORY/CopyWithPivot.xlsx");
        Console.WriteLine("Pivot table copied successfully.");
    }
}
```

การรันโปรแกรมจะสร้างไฟล์ `CopyWithPivot.xlsx` ที่เป็นสำเนาที่ตรงกับ pivot table ต้นฉบับ รวมถึง slicer, filter, และฟิลด์คำนวณทั้งหมด.

### ผลลัพธ์ที่คาดหวัง

เมื่อคุณเปิดไฟล์ `CopyWithPivot.xlsx`:

- Pivot table ปรากฏในตำแหน่งเดียวกัน (เช่น A1:K31) กับใน `Source.xlsx`.
- ป้ายกำกับแถวและคอลัมน์, ผลรวม, และการจัดรูปแบบทั้งหมดถูกเก็บไว้
- การรีเฟรช pivot แสดงข้อมูลเดียวกับต้นทาง ยืนยันว่าแคชถูกคัดลอกอย่างถูกต้อง

## วิธีคัดลอกแถวโดยไม่มี pivot (copy excel range)

หากคุณต้องการ **copy excel range** เพียงอย่างเดียวโดยไม่มีข้อมูล pivot คุณสามารถใช้เมธอด `CopyRows` เดียวกันแต่ชี้ไปยังช่วงที่ไม่มี pivot ตัวอย่างเช่น:

```csharp
// Copy a simple data table from rows 5‑15, columns A‑D
destWorksheet.Cells.CopyRows(
    srcWorkbook.Worksheets[0].Cells,
    4,            // start at row 5 (zero‑based)
    11,           // copy 11 rows (5‑15 inclusive)
    destWorksheet.Cells,
    0);           // paste at the top of the destination sheet
```

นี่แสดงให้เห็น **how to copy rows** สำหรับข้อมูลทั่วไป ยืนยันความหลากหลายของ API เดียวกัน.

## ทำสำเนา pivot table ในเวิร์กบุ๊กเดียวกัน (วิธีทางเลือก)

บางครั้งคุณอาจต้องการ **duplicate pivot table** ภายในเวิร์กบุ๊กเดียวกันแทนการสร้างไฟล์ใหม่ คุณสามารถทำได้โดยคัดลอกแถวไปยังตำแหน่งอื่น:

```csharp
// Duplicate pivot table to start at row 40 in the same worksheet
destWorksheet.Cells.CopyRows(
    srcWorkbook.Worksheets[0].Cells,
    sourceRange.StartRow,
    sourceRange.EndRow - sourceRange.StartRow + 1,
    destWorksheet.Cells,
    40); // destination start row (zero‑based)
```

หลังจากบันทึก เวิร์กบุ๊กจะมี pivot สองอันที่เหมือนกัน—เป็นประโยชน์สำหรับการเปรียบเทียบข้างเคียงหรือสร้างสำเนาสำรอง.

## ข้อผิดพลาดทั่วไปและวิธีหลีกเลี่ยง

| ข้อผิดพลาด | สาเหตุ | วิธีแก้ |
|------------|--------|----------|
| Pivot แสดง `#REF!` หลังการคัดลอก | ช่วงข้อมูลต้นทางไม่มีในเวิร์กบุ๊กปลายทาง | คัดลอกช่วงข้อมูลต้นทางก่อน, หรือใช้ `CopyRows` บนแผ่นข้อมูลต้นทางก่อนคัดลอก pivot |
| การจัดรูปแบบหาย | คัดลอกเฉพาะค่า (เช่น ใช้ `Copy` แทน `CopyRows`) | ใช้ `CopyRows` เสมอ ซึ่งรักษาสไตล์, การจัดรูปแบบ, และเมตาดาต้า pivot |
| การเยื้องแถวที่ไม่คาดคิด | แถวเริ่มต้นของปลายทางไม่ตรงกับแถวเริ่มต้นของต้นทาง | ตรวจสอบว่าแถวเริ่มต้นของ `destWorksheet.Cells` ตรงกับตำแหน่งที่ต้องการ |
| เวิร์กบุ๊กขนาดใหญ่ทำให้ความดันหน่วยความจำ | `CopyRows` โหลดแผ่นงานทั้งหมดเข้าสู่หน่วยความจำ | ประมวลผลการคัดลอกเป็นส่วน ๆ หรือใช้ API สตรีมมิ่งหากทำงานกับแถว >100,000 แถว |

## ตัวอย่างเต็มที่สามารถรันได้

ด้านล่างเป็นโปรแกรมเต็มที่คุณสามารถวางลงใน `Program.cs` และรันได้ทันที (แทนที่ `YOUR_DIRECTORY` ด้วยพาธจริงบนเครื่องของคุณ).

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the source workbook containing the pivot table
        Workbook srcWorkbook = new Workbook(@"YOUR_DIRECTORY/Source.xlsx");

        // 2️⃣ Define the area that encloses the pivot (adjust to your sheet)
        CellArea sourceRange = new CellArea
        {
            StartRow = 0,
            StartColumn = 0,
            EndRow = 30,
            EndColumn = 10
        };

        // 3️⃣ Create the destination workbook (empty) and get its first sheet
        Workbook destWorkbook = new Workbook();
        Worksheet destWorksheet = destWorkbook.Worksheets[0];

        // 4️⃣ Copy rows—including the pivot cache—into the destination
        destWorksheet.Cells.CopyRows(
            srcWorkbook.Worksheets[0].Cells,
            sourceRange.StartRow,
            sourceRange.EndRow - sourceRange.StartRow + 1,
            destWorksheet.Cells,
            sourceRange.StartRow);

        // 5️⃣ Save the result
        destWorkbook.Save(@"YOUR_DIRECTORY/CopyWithPivot.xlsx");
        Console.WriteLine("Pivot table copied successfully.");
    }
}
```

รันโปรแกรมด้วย `dotnet run`. หลังจากทำงานเสร็จ เปิดไฟล์ `CopyWithPivot.xlsx` เพื่อตรวจสอบว่า pivot table ปรากฏตรงกับไฟล์ต้นทาง.

## สรุป

ตอนนี้คุณรู้วิธี **copy pivot table** จากเวิร์กบุ๊ก Excel หนึ่งไปยังอีกเวิร์กบุ๊กหนึ่งโดยใช้ C# และ Aspose.Cells คู่มือได้อธิบายขั้นตอนทั้งหมด—ตั้งแต่การโหลดไฟล์ต้นทาง, กำหนดช่วงเซลล์ของ pivot, คัดลอกแถว, และบันทึกเวิร์กบุ๊กปลายทาง คุณยังได้เรียนรู้ **how to copy rows**, **copy excel range**, และ **duplicate pivot table** ภายในไฟล์เดียวกัน พร้อมกับข้อผิดพลาดทั่วไปและเคล็ดลับการปฏิบัติที่ดีที่สุด.

พร้อมสำหรับขั้นตอนต่อไปหรือยัง? ลองเพิ่มโค้ดเพื่อรีเฟรช pivot ที่คัดลอกโดยอัตโนมัติ, หรือสำรวจการส่งออก pivot เป็น PDF ด้วย Aspose.Cells ทดลองกับช่วงต้นทางต่าง ๆ แล้วคุณจะเชี่ยวชาญการทำอัตโนมัติ Excel ใน .NET อย่างรวดเร็ว.

---

## สิ่งที่คุณควรเรียนต่อไป?

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งข้อมูลมีตัวอย่างโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายทีละขั้นตอน เพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจวิธีการทำงานทางเลือกในโครงการของคุณ.

- [Copy Pivot Table in C# – Complete Step‑by‑Step Guide](/cells/english/net/pivot-tables/copy-pivot-table-in-c-complete-step-by-step-guide/)
- [Create New Excel Workbook – Copy & Duplicate Pivot Table](/cells/english/net/pivot-tables/create-new-excel-workbook-copy-duplicate-pivot-table/)
- [copy rows excel – Preserve Pivot Table While Duplicating Rows](/cells/english/net/pivot-tables/copy-rows-excel-preserve-pivot-table-while-duplicating-rows/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}