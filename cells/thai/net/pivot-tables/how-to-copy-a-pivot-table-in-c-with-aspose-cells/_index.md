---
category: general
date: 2026-09-27
description: เรียนรู้วิธีคัดลอก Pivot Table ใน C# ด้วย Aspose.Cells รวมถึงการคัดลอกแถวพร้อมการจัดรูปแบบ
  การคัดลอก Pivot Table ไปยังแผ่นงานอื่น และการส่งออก Pivot Table ไปยังเวิร์กบุ๊กใหม่.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot table
- copy rows with formatting
- copy pivot table to another sheet
- how to copy excel rows
- export pivot table to new workbook
language: th
lastmod: 2026-09-27
og_description: วิธีคัดลอก Pivot Table ใน C# ด้วย Aspose.Cells. ทำตามคู่มือขั้นตอนต่อขั้นตอนเพื่อคัดลอกแถวพร้อมรูปแบบ,
  ย้าย Pivot Table ไปยังแผ่นงานอื่น, และส่งออกไปยังเวิร์กบุ๊กใหม่.
og_image_alt: Excel sheet showing a copied pivot table after using Aspose.Cells
og_title: วิธีคัดลอก Pivot Table ใน C# – คู่มือ Aspose.Cells แบบเต็ม
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Learn how to copy a pivot table in C# using Aspose.Cells. Includes
    copy rows with formatting, copy pivot table to another sheet, and export pivot
    table to a new workbook.
  headline: How to copy a pivot table in C# with Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
- Pivot table
title: วิธีคัดลอกตาราง Pivot ใน C# ด้วย Aspose.Cells
url: /th/net/pivot-tables/how-to-copy-a-pivot-table-in-c-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีคัดลอก Pivot Table ใน C# ด้วย Aspose.Cells

หากคุณต้องการ **คัดลอก pivot table** จากแผ่นงานหนึ่งไปยังอีกแผ่นงานหนึ่ง การเรียนรู้ **วิธีคัดลอก pivot table** ใน C# ด้วย Aspose.Cells สามารถช่วยคุณประหยัดเวลาการทำงานด้วยมือหลายชั่วโมง วิธีนี้ยังทำให้คุณ **คัดลอกแถวพร้อมรูปแบบ**, รักษา pivot cache ไว้ไม่เสียหาย, และแม้กระทั่ง **ส่งออก pivot table ไปยังเวิร์กบุ๊กใหม่** เมื่อคุณต้องการไฟล์แยกส่วน

บทแนะนำนี้จะพาคุณผ่านขั้นตอนทั้งหมด:

* สร้างเวิร์กบุ๊ก,  
* คัดลอกช่วงของ pivot‑table พร้อมรักษารูปแบบ,  
* วางข้อมูลที่คัดลอกไว้บนแผ่นงานใหม่, และ  
* บันทึกผลลัพธ์เป็นไฟล์แยก

คุณจะเห็นว่าทำไมเมธอดในตัว `CopyRows` จึงเป็นวิธีที่เชื่อถือได้ที่สุดในการ **คัดลอก pivot table ไปยังแผ่นงานอื่น**, และคุณจะได้รับเคล็ดลับสำหรับการจัดการกรณีขอบเช่นแถวที่ซ่อนหรือแหล่งข้อมูลภายนอก

## ข้อกำหนดเบื้องต้น

ก่อนที่คุณจะเริ่ม, ตรวจสอบให้แน่ใจว่าคุณมี:

| ความต้องการ | ทำไมถึงสำคัญ |
|-------------|----------------|
| .NET 6.0 หรือใหม่กว่า | Aspose.Cells รองรับ .NET 6+ และให้ประสิทธิภาพที่ดีที่สุด |
| Visual Studio 2022 (หรือ IDE C# ใดก็ได้) | คุณต้องการเครื่องมือแก้ไขที่สามารถกู้คืนแพ็กเกจ NuGet |
| Aspose.Cells for .NET (แพ็กเกจ NuGet `Aspose.Cells`) | ไลบรารีนี้ให้ API `CopyRows` ที่ใช้ในตัวอย่าง |
| ไฟล์ Excel ต้นฉบับ (`source.xlsx`) ที่มี pivot table อยู่ในช่วง `A1:G20` | โค้ดจะคัดลอกช่วงนี้; ปรับช่วงหาก pivot table ของคุณใหญ่กว่า |

ติดตั้งไลบรารีด้วย NuGet CLI หรือ Package Manager Console:

```bash
dotnet add package Aspose.Cells
```

## ขั้นตอนที่ 1: โหลดเวิร์กบุ๊กที่มี pivot table

บรรทัดแรกสร้างอ็อบเจกต์ `Workbook` ที่แทนไฟล์ Excel ทั้งไฟล์ การโหลดไฟล์ครั้งเดียวทำให้คุณสามารถอ่าน/เขียนทุกแผ่นงานได้

```csharp
using Aspose.Cells;

// Load the source workbook
Workbook workbook = new Workbook(@"YOUR_DIRECTORY\source.xlsx");
```

> **ทำไมขั้นตอนนี้สำคัญ** – หากไม่ได้โหลดเวิร์กบุ๊ก, การเรียก `CopyRows` ใด ๆ ต่อไปจะไม่สามารถอ้างอิงข้อมูลต้นฉบับหรือ pivot cache ได้

## ขั้นตอนที่ 2: เตรียมแผ่นงานต้นทางและปลายทาง

คุณต้องมีแผ่นงานปลายทางที่คัดลอก pivot table ไปไว้ โค้ดด้านล่างจะดึงแผ่นงานแรก (ที่มี pivot table ดั้งเดิม) และเพิ่มแผ่นงานใหม่ชื่อ **Copy**

```csharp
// Get the source worksheet (index 0 = first sheet)
Worksheet sourceSheet = workbook.Worksheets[0];

// Add a new worksheet that will receive the copied rows
Worksheet destinationSheet = workbook.Worksheets.Add("Copy");
```

> **เคล็ดลับ:** หากแผ่นงานปลายทางมีอยู่แล้ว, ให้เรียก `Worksheets.RemoveAt(index)` ก่อนเพื่อหลีกเลี่ยงชื่อซ้ำ

## ขั้นตอนที่ 3: กำหนด CellArea ที่ล้อมรอบ pivot table

อ็อบเจกต์ `CellArea` ระบุเซลล์ซ้ายบนและขวาล่างของช่วงที่คุณต้องการย้าย ในตัวอย่างนี้ pivot table อยู่ที่ `A1:G20` ปรับพิกัดหากตารางของคุณใหญ่กว่า

```csharp
// Define the range that includes the pivot table (A1:G20)
CellArea sourceArea = CellArea.CreateCellArea("A1", "G20");
```

## ขั้นตอนที่ 4: คัดลอกแถวพร้อมรูปแบบและรักษา pivot cache

เมธอด `CopyRows` จะคัดลอก **แถว** จากแผ่นงานต้นทางไปยังแผ่นงานปลายทาง โดยการส่ง `CopyOptions.CopyAll` คุณจะมั่นใจว่าค่าต่าง ๆ, รูปแบบ, แผนภูมิ, และอ็อบเจกต์ฝังทั้งหมด—ซึ่งเป็นส่วนหนึ่งของ pivot table—จะถูกถ่ายโอน

```csharp
// Copy the rows from the source area to the destination sheet
sourceSheet.CopyRows(
    sourceArea.StartRow,          // start row in the source sheet
    destinationSheet,            // target worksheet
    0,                            // start row in the destination sheet
    sourceArea.RowCount,          // number of rows to copy
    CopyOptions.CopyAll);        // copy everything (values, formats, objects, etc.)
```

### ทำไม `CopyRows` ทำงานได้ดีกว่า `Copy` สำหรับ pivot tables

* `CopyRows` เคารพ pivot cache ภายใน, ดังนั้น pivot table ที่คัดลอกจะยังคงทำงานได้
* มันรักษา **copy rows with formatting** ไว้เหมือนเดิมตามที่แสดงในแผ่นงานต้นฉบับ
* แตกต่างจากการ `Copy` ช่วงธรรมดา, มันยังคัดลอกแถวที่ซ่อนและ slicer ที่เกี่ยวข้องด้วย

## ขั้นตอนที่ 5: บันทึกเวิร์กบุ๊กที่มี pivot table ที่คัดลอกแล้ว

สุดท้าย, เขียนเวิร์กบุ๊กที่แก้ไขแล้วลงดิสก์ ไฟล์ใหม่จะมีแผ่นงานเดิมบวกกับแผ่นงาน **Copy** ที่มีสำเนา pivot table ที่ทำงานเต็มรูปแบบ

```csharp
// Save the workbook to a new file
workbook.Save(@"YOUR_DIRECTORY\pivot_copied.xlsx");
```

### ผลลัพธ์ที่คาดหวัง

เมื่อคุณเปิด `pivot_copied.xlsx`:

* แผ่นงาน **Sheet1** ยังคงมีข้อมูลและ pivot table ดั้งเดิม
* แผ่นงาน **Copy** แสดง pivot table ที่เหมือนกันโดยมีรูปแบบ, ตัวกรอง, และการจัดวางเดียวกัน
* สูตรและการเชื่อมต่อข้อมูลทั้งหมดยังคงอยู่เนื่องจาก pivot cache ถูกคัดลอกพร้อมกับแถว

## วิธีคัดลอก pivot table ไปยังแผ่นงานอื่นในเวิร์กบุ๊กเดียวกัน

หากคุณต้องการ pivot table เพียงในแผ่นงานที่มีอยู่แล้ว (เช่น “Report”), ให้แทนที่ขั้นตอนการสร้างแผ่นงานปลายทางด้วยการอ้างอิงแผ่นงานเป้าหมาย:

```csharp
Worksheet destinationSheet = workbook.Worksheets["Report"]; // existing sheet
sourceSheet.CopyRows(sourceArea.StartRow, destinationSheet, 0,
                     sourceArea.RowCount, CopyOptions.CopyAll);
```

โค้ดส่วนนี้แสดง **copy pivot table to another sheet** โดยไม่ต้องสร้างแผ่นงานใหม่

## ส่งออก pivot table ไปยังเวิร์กบุ๊กใหม่

บางครั้งคุณต้องการ pivot table แยกออกเป็นไฟล์อิสระ หลังจากคัดลอกแล้ว, คุณสามารถลบแผ่นงานทั้งหมดยกเว้นแผ่นงานที่มี pivot table ที่คัดลอกไว้และบันทึก:

```csharp
// Keep only the copied sheet
for (int i = workbook.Worksheets.Count - 1; i >= 0; i--)
{
    if (workbook.Worksheets[i].Name != "Copy")
        workbook.Worksheets.RemoveAt(i);
}

// Save as a new workbook containing only the pivot table
workbook.Save(@"YOUR_DIRECTORY\pivot_only.xlsx");
```

ตอนนี้ `pivot_only.xlsx` มีเพียงแผ่นเดียวที่มี pivot table ที่ทำซ้ำแล้ว, ตอบสนองความต้องการ **export pivot table to new workbook**

## วิธีคัดลอกแถว Excel โดยไม่สูญเสียรูปแบบ

การเรียก `CopyRows` เดียวกันทำงานได้กับช่วงใดก็ได้, ไม่เฉพาะ pivot tables หากคุณต้องการ **copy excel rows** ที่รวมการจัดรูปแบบตามเงื่อนไข, การตรวจสอบข้อมูล, หรือการรวมเซลล์, ให้ใช้เมธอดเดียวกัน:

```csharp
// Example: copy rows 30‑40 from Sheet1 to Sheet2
sourceSheet.CopyRows(29, // zero‑based index for row 30
                     workbook.Worksheets["Sheet2"],
                     0,
                     11, // rows 30‑40 = 11 rows
                     CopyOptions.CopyAll);
```

เพราะ `CopyOptions.CopyAll` ถ่ายโอนทุกอย่าง, แถวปลายทางจะดูเหมือนกับแถวต้นฉบับอย่างสมบูรณ์

## ข้อผิดพลาดทั่วไปและวิธีหลีกเลี่ยง

| ปัญหา | อาการ | วิธีแก้ |
|---------|---------|-----|
| ช่วงต้นทางไม่ได้รวม pivot table ทั้งหมด | Pivot table ที่คัดลอกมาดูถูกตัด | ตรวจสอบให้ `CellArea` ครอบคลุมทุกแถว/คอลัมน์ของ pivot table |
| แผ่นงานปลายทางมีข้อมูลอยู่แล้ว | แถวที่คัดลอกทับข้อมูลทำให้สูญหาย | เลือกแผ่นงานใหม่หรือเริ่มคัดลอกจากแถวที่สูงกว่า |
| Pivot table ใช้แหล่งข้อมูลภายนอก | การคัดลอกทำให้การเชื่อมต่อหาย | หลังคัดลอก, เรียก `pivotTable.RefreshData()` เพื่อเชื่อมต่อใหม่ |
| แถวที่ซ่อนไม่ได้ถูกคัดลอก | บางแถวหายไปในสำเนา | `CopyRows` จะคัดลอกแถวที่ซ่อนโดยอัตโนมัติ; อย่าใช้ `CopyOptions.CopyValuesOnly` |

## ตัวอย่างเต็มที่สามารถรันได้

ด้านล่างเป็นโปรแกรมที่สมบูรณ์ซึ่งคุณสามารถวางลงในโปรเจกต์คอนโซลใหม่ได้ มันแสดงทุกขั้นตอนที่อธิบายไว้ข้างต้น

```csharp
using System;
using Aspose.Cells;

namespace PivotTableCopyDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the workbook that contains the pivot table
            string sourcePath = @"YOUR_DIRECTORY\source.xlsx";
            Workbook workbook = new Workbook(sourcePath);

            // 2️⃣ Get source and destination worksheets
            Worksheet sourceSheet = workbook.Worksheets[0]; // first sheet
            Worksheet destinationSheet = workbook.Worksheets.Add("Copy");

            // 3️⃣ Define the cell area that holds the pivot table (A1:G20)
            CellArea sourceArea = CellArea.CreateCellArea("A1", "G20");

            // 4️⃣ Copy rows with formatting and keep the pivot cache
            sourceSheet.CopyRows(
                sourceArea.StartRow,      // start row index (0‑based)
                destinationSheet,        // target sheet
                0,                        // start row in destination
                sourceArea.RowCount,      // number of rows to copy
                CopyOptions.CopyAll);    // copy everything

            // 5️⃣ Save the workbook with the copied pivot table
            string destPath = @"YOUR_DIRECTORY\pivot_copied.xlsx";
            workbook.Save(destPath);

            Console.WriteLine("Pivot table copied successfully to " + destPath);
        }
    }
}
```

**การรันโปรแกรม** จะสร้าง `pivot_copied.xlsx` พร้อมสำเนา pivot table ดั้งเดิมบนแผ่นงานใหม่ชื่อ **Copy**

## สรุป

คุณได้เรียนรู้ **วิธีคัดลอก pivot table** ใน C# ด้วย

## คุณควรเรียนรู้อะไรต่อไป?

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ ทุกแหล่งข้อมูลมีตัวอย่างโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายทีละขั้นตอน เพื่อช่วยคุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจวิธีการทำงานแบบอื่นในโปรเจกต์ของคุณ

- [Create New Workbook – How to Copy a Worksheet with a Pivot Table](/cells/english/net/excel-copy-worksheet/create-new-workbook-how-to-copy-a-worksheet-with-a-pivot-tab/)
- [Copy Pivot Table in C# – Complete Step‑by‑Step Guide](/cells/english/net/pivot-tables/copy-pivot-table-in-c-complete-step-by-step-guide/)
- [How to copy range with pivot tables in C# – Complete Guide](/cells/english/net/pivot-tables/how-to-copy-range-with-pivot-tables-in-c-complete-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}