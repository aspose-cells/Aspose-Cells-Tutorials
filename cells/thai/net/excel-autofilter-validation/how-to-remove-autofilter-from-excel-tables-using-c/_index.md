---
category: general
date: 2026-10-07
description: เรียนรู้วิธีลบ AutoFilter จากตาราง Excel ด้วย C# คู่มือนี้ยังแสดงวิธีซ่อนลูกศรตัวกรองใน
  Excel และปิดการใช้งานตัวกรองของตาราง Excel
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- remove autofilter from excel
- excel table hide filter
- hide filter arrows excel
- disable excel table filter
language: th
lastmod: 2026-10-07
og_description: ลบ autofilter จากตาราง Excel ด้วย C# เพื่อทำความสะอาดสเปรดชีตของคุณ
  ทำตามบทเรียนฉบับเต็มนี้เพื่อซ่อนลูกศรตัวกรองใน Excel, ปิดการใช้งานตัวกรองตาราง Excel,
  และบันทึกเวิร์กบุ๊กที่สะอาด.
og_image_alt: Screenshot of an Excel worksheet after the autofilter UI has been removed
og_title: ลบ autofilter จากตาราง Excel ใน C# – คู่มือแบบทีละขั้นตอน
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Learn how to remove autofilter from Excel tables with C#. This guide
    also shows how to hide filter arrows Excel and disable Excel table filter.
  headline: How to remove autofilter from Excel tables using C#
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
- Automation
title: วิธีลบ autofilter จากตาราง Excel ด้วย C#
url: /th/net/excel-autofilter-validation/how-to-remove-autofilter-from-excel-tables-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีลบ autofilter จากตาราง Excel ด้วย C#

หากคุณต้องการ **remove autofilter from Excel** คู่มือนี้จะแสดงวิธีทำโดยใช้ C# อย่างโปรแกรมเมติก คุณจะได้เรียนรู้วิธีซ่อนลูกศรตัวกรองใน Excel และปิดการทำงานของตัวกรองตารางเพื่อให้แผ่นงานดูเรียบง่าย

บทแนะนำนี้จะพาคุณผ่านทุกขั้นตอนที่จำเป็น ตั้งแต่การติดตั้งไลบรารีจนถึงการบันทึกไฟล์เวิร์กบุ๊กสุดท้าย เมื่อเสร็จแล้วคุณสามารถเปิดไฟล์ที่บันทึกไว้และเห็นว่ารูปไอคอนดรอปดาวน์ของตัวกรองหายไป ตารางทำงานเหมือนช่วงข้อมูลปกติ และไม่มีองค์ประกอบ UI ใดรบกวนผู้ใช้ ไม่จำเป็นต้องมีประสบการณ์กับ Aspose.Cells API มาก่อน แต่ต้องมีความรู้พื้นฐานของ C# อยู่แล้ว

## ข้อกำหนดเบื้องต้น

ก่อนเริ่มทำงาน โปรดตรวจสอบว่าคุณมี:

* .NET 6.0 SDK หรือรุ่นที่ใหม่กว่า ติดตั้งแล้ว  
* สภาพแวดล้อมการพัฒนา เช่น Visual Studio 2022 หรือ VS Code  
* แพคเกจ NuGet **Aspose.Cells for .NET** (ตัวอย่างโค้ดใช้ไลบรารีนี้)  
* ไฟล์ Excel ที่มีตารางพร้อมตัวกรองที่เปิดใช้งาน (เช่น `TableWithFilter.xlsx`)

คุณสามารถติดตั้ง Aspose.Cells ผ่าน .NET CLI:

```bash
dotnet add package Aspose.Cells
```

> **Pro tip:** ใช้เวอร์ชันล่าสุดที่เสถียรของแพคเกจเพื่อรับประโยชน์จากการแก้บั๊กและการปรับปรุงประสิทธิภาพล่าสุด

## ขั้นตอนที่ 1 – remove autofilter from Excel: โหลด workbook

การดำเนินการแรกคือการโหลดเวิร์กบุ๊กที่มีตารางที่คุณต้องการแก้ไข การโหลดไฟล์จะสร้างการแสดงผลในหน่วยความจำที่คุณสามารถจัดการได้

```csharp
using Aspose.Cells;

string sourcePath = @"C:\Data\TableWithFilter.xlsx";
Workbook workbook = new Workbook(sourcePath);
```

*ทำไมขั้นตอนนี้สำคัญ*: หากไม่ได้โหลดเวิร์กบุ๊ก คุณจะไม่มีการเข้าถึงแผ่นงาน, ตาราง (`ListObject`) หรือการตั้งค่าตัวกรองของมัน คลาส `Workbook` ทำหน้าที่เป็นตัวแทนของไฟล์ Excel ทั้งหมด ทำให้การกระทำต่อไปเป็นเรื่องง่าย

## ขั้นตอนที่ 2 – locate the worksheet containing the table

เวิร์กบุ๊กส่วนใหญ่จะมีแผ่นงานเริ่มต้นชื่อ “Sheet1” คุณสามารถเลือกแผ่นงานโดยใช้ดัชนีหรือชื่อได้ ที่นี่เราใช้แผ่นงานแรก

```csharp
Worksheet worksheet = workbook.Worksheets[0];   // index‑based access
// Alternative: Worksheet worksheet = workbook.Worksheets["Sales"]; // by name
```

*ทำไมขั้นตอนนี้สำคัญ*: ตารางถูกกำหนดขอบเขตไว้ในแผ่นงานเฉพาะ การเข้าถึงแผ่นงานที่ถูกต้องรับประกันว่าคุณจะแก้ไข `ListObject` ที่ต้องการ

## ขั้นตอนที่ 3 – retrieve the ListObject (Excel table) you want to change

ตารางใน Excel แสดงด้วย `ListObject` คุณสามารถดึงมันโดยใช้ชื่อของตาราง ซึ่งสามารถดูได้จากแท็บ “Table Design” ของ Excel

```csharp
// Replace "SalesTable" with the actual table name in your workbook
ListObject salesTable = worksheet.ListObjects["SalesTable"];
```

หากคุณไม่แน่ใจชื่อของตาราง คุณสามารถแสดงรายการตารางทั้งหมดบนแผ่นงานได้:

```csharp
foreach (ListObject tbl in worksheet.ListObjects)
{
    Console.WriteLine($"Found table: {tbl.Name}");
}
```

*ทำไมขั้นตอนนี้สำคัญ*: คุณสมบัติ `AutoFilter` อยู่บน `ListObject` การเลือกตารางที่ถูกต้องทำให้คุณลบ UI ตัวกรองที่ต้องการได้อย่างแม่นยำ

## ขั้นตอนที่ 4 – hide filter arrows Excel by clearing the AutoFilter UI

การดำเนินการหลักคือการตั้งค่าคุณสมบัติ `AutoFilter` ให้เป็น `null` ซึ่งจะลบลูกศรดรอปดาวน์ของตัวกรองออกจากแถวหัวตาราง

```csharp
salesTable.AutoFilter = null;   // removes the filter UI
```

> **Note:** การตั้งค่า `AutoFilter` เป็น `null` มีผลเทียบเท่ากับคำสั่ง “Clear Filter” ใน UI ของ Excel แต่ยังลบลูกศรที่มองเห็นได้ด้วย ซึ่งตอบสนองความต้องการ **excel table hide filter** และ **disable Excel table filter**

### ทางเลือก: ปิดการกรองสำหรับทุกตารางในเวิร์กบุ๊ก

หากเวิร์กบุ๊กของคุณมีหลายตารางและต้องการวิธีแบบครอบคลุม ให้วนลูปผ่านแต่ละ `ListObject`:

```csharp
foreach (Worksheet ws in workbook.Worksheets)
{
    foreach (ListObject tbl in ws.ListObjects)
    {
        tbl.AutoFilter = null;
    }
}
```

## ขั้นตอนที่ 5 – save the modified workbook

หลังจากลบ UI ตัวกรองแล้ว ให้บันทึกการเปลี่ยนแปลงลงไฟล์ใหม่ (หรือเขียนทับไฟล์เดิมหากต้องการ)

```csharp
string targetPath = @"C:\Data\TableNoFilter.xlsx";
workbook.Save(targetPath);
Console.WriteLine($"Workbook saved without autofilter at: {targetPath}");
```

*ทำไมขั้นตอนนี้สำคัญ*: Excel จะสะท้อนการเปลี่ยนแปลงก็ต่อเมื่อไฟล์ถูกบันทึก ไฟล์ใหม่จะเปิดขึ้นโดยมีตารางที่สะอาดไม่มีลูกศรตัวกรองอีกต่อไป

## ผลลัพธ์ที่คาดหวัง

เปิด `TableNoFilter.xlsx` ใน Excel คุณควรเห็น:

* แถวหัวของตารางไม่แสดงลูกศรดรอปดาวน์อีกต่อไป  
* ไม่มีเงื่อนไขตัวกรองใด ๆ ถูกนำไปใช้; แถวทั้งหมดแสดงผล  
* ส่วนอื่นของเวิร์กบุ๊ก (สูตร, การจัดรูปแบบ, แผนภูมิ) ยังคงไม่เปลี่ยนแปลง

## กรณีขอบและข้อผิดพลาดทั่วไป

| สถานการณ์ | วิธีจัดการ |
|-----------|------------|
| **ไม่ทราบชื่อ Table** | ใช้วิธีการ enumerate ที่แสดงในขั้นตอน 3 เพื่อค้นหาชื่อในเวลารัน |
| **หลายตารางในแผ่นเดียวกัน** | ใช้ลูปจากวิธีทางเลือกในขั้นตอน 4 เพื่อเคลียร์ตัวกรองของแต่ละตาราง |
| **รูปแบบ Excel เก่า (`.xls`)** | Aspose.Cells รองรับทั้ง `.xlsx` และ `.xls` โหลดไฟล์ด้วยวิธีเดียวกัน; API จัดการความแตกต่างของรูปแบบให้ |
| **ไฟล์เป็นแบบอ่าน‑อย่างเดียวหรือถูกล็อก** | ตรวจสอบให้กระบวนการมีสิทธิ์เขียนและไฟล์ไม่ได้เปิดอยู่ใน Excel ขณะรันโค้ด |
| **ต้องการเก็บตรรกะของตัวกรองไว้แต่ซ่อนลูกศร** | แทนการตั้งค่า `AutoFilter = null` คุณสามารถเก็บอ็อบเจ็กต์ตัวกรองไว้และตั้งค่า `ShowHideButtons = false` (มีในเวอร์ชันไลบรารีใหม่) |

## ตัวอย่างเต็มที่สามารถรันได้

ด้านล่างเป็นแอปพลิเคชันคอนโซลที่สมบูรณ์ คุณสามารถคัดลอก, วางและรันได้ มันแสดงทุกขั้นตอนตั้งแต่การตั้งค่าโปรเจกต์จนถึงการบันทึกเวิร์กบุ๊กที่ไม่มีตัวกรอง

```csharp
// Program.cs
using System;
using Aspose.Cells;

namespace ExcelFilterRemoval
{
    class Program
    {
        static void Main()
        {
            // 1. Load the workbook containing the table
            string sourcePath = @"C:\Data\TableWithFilter.xlsx";
            Workbook workbook = new Workbook(sourcePath);

            // 2. Access the first worksheet (or specify by name)
            Worksheet worksheet = workbook.Worksheets[0];

            // 3. Retrieve the table you want to modify
            //    Replace "SalesTable" with your actual table name
            ListObject salesTable = worksheet.ListObjects["SalesTable"];

            // 4. Remove the AutoFilter UI from the table
            salesTable.AutoFilter = null;

            // 5. Save the workbook – the table now has no filter UI
            string targetPath = @"C:\Data\TableNoFilter.xlsx";
            workbook.Save(targetPath);

            Console.WriteLine($"Successfully removed autofilter and saved to {targetPath}");
        }
    }
}
```

รันโปรแกรมด้วยคำสั่ง `dotnet run` เมื่อเสร็จแล้วให้เปิดไฟล์ผลลัพธ์เพื่อยืนยันว่าลูกศรตัวกรองได้หายไปแล้ว

## สรุป

คุณได้เรียนรู้วิธี **remove autofilter from Excel** จากตารางด้วย C# คู่มือได้อธิบายการโหลดเวิร์กบุ๊ก, การหาตารางเป้าหมาย, การล้างคุณสมบัติ `AutoFilter` และการบันทึกผลลัพธ์ โดยทำตามขั้นตอนเหล่านี้คุณยังสามารถทำให้ **excel table hide filter**, **hide filter arrows Excel**, และ **disable Excel table filter** ได้ในสคริปต์เดียวที่ทำซ้ำได้

### สิ่งที่ควรสำรวจต่อไป

* **ใช้สไตล์แบบกำหนดเอง** กับตารางหลังจากลบ UI ตัวกรอง  
* **ป้องกันแผ่นงาน** เพื่อป้องกันผู้ใช้จากการเพิ่มตัวกรองใหม่  
* **รวมกับการส่งออกข้อมูล** (เช่น สร้างไฟล์ CSV) เพื่อการประมวลผลต่อไป  

ลองทดลองกับวิธีทางเลือกที่แสดงในตารางกรณีขอบ หากคุณพบสถานการณ์ที่ไม่ได้ครอบคลุมในที่นี้ เอกสาร Aspose.Cells มีวิธีเพิ่มเติมสำหรับการควบคุมพฤติกรรมของตารางอย่างละเอียด ขอให้สนุกกับการเขียนโค้ด!

## สิ่งที่คุณควรเรียนต่อไป?

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งรวมโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายขั้นตอนเพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการทำงานอื่น ๆ ในโปรเจกต์ของคุณ

- [ซ่อนลูกศรตัวกรองใน Excel ด้วย C# – คู่มือเต็ม](/cells/english/net/excel-autofilter-validation/hide-filter-arrows-excel-with-c-complete-guide/)
- [ลบ UI ตัวกรองใน Excel ด้วย C# – ลบปุ่ม AutoFilter](/cells/english/net/excel-autofilter-validation/clear-filter-ui-in-excel-with-c-remove-autofilter-button/)
- [วิธีใช้ AutoFilter ในการทำอัตโนมัติ Excel ด้วย C# – คู่มือเต็มขั้นตอน](/cells/english/net/excel-autofilter-validation/how-to-use-autofilter-in-c-excel-automation-full-step-by-ste/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}