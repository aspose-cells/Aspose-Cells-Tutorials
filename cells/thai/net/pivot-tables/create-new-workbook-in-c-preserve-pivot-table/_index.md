---
category: general
date: 2026-02-15
description: สร้างเวิร์กบุ๊กใหม่ใน C# และคัดลอกตาราง Pivot โดยไม่สูญเสียการกำหนดค่า
  เรียนรู้วิธีคัดลอกแถว, รักษาตาราง Pivot, และทำสำเนาตาราง Pivot ได้อย่างง่ายดาย.
draft: false
keywords:
- create new workbook
- copy pivot table
- preserve pivot table
- how to copy rows
- duplicate pivot table
language: th
og_description: สร้างสมุดงานใหม่ใน C# และคัดลอกพีโวตเทเบิลโดยคงไว้ซึ่งคำนิยามของมัน
  คู่มือแบบขั้นตอนสำหรับนักพัฒนา
og_title: สร้างเวิร์กบุ๊กใหม่ใน C# – รักษาตาราง Pivot
tags:
- Aspose.Cells
- C#
- Excel automation
title: สร้างเวิร์กบุ๊กใหม่ใน C# – รักษาตาราง Pivot
url: /th/net/pivot-tables/create-new-workbook-in-c-preserve-pivot-table/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# สร้าง Workbook ใหม่ใน C# – รักษา Pivot Table

เคยต้องการ **create new workbook** ใน C# ที่มีสำเนาตรงของ pivot table จากไฟล์อื่นหรือไม่? คุณไม่ได้เป็นคนเดียว ในหลาย ๆ กระบวนการรายงาน pivot table เป็นหัวใจของการวิเคราะห์ และการสูญเสียคำนิยามของมันเมื่อย้ายข้อมูลเป็นเรื่องน่ากลัว

ข่าวดีคือ? ด้วยไม่กี่บรรทัดของโค้ด Aspose.Cells คุณสามารถคัดลอกแถว—รวมถึง pivot table—ไปยัง workbook ใหม่และรักษาทุกอย่างไว้ครบถ้วน ด้านล่างคุณจะเห็น **how to copy rows**, **preserve pivot table** settings, และแม้กระทั่ง **duplicate pivot table** ข้ามไฟล์โดยไม่ทำลายสูตรหรือแคช

## สิ่งที่บทเรียนนี้ครอบคลุม

ในบทเรียนนี้เราจะเดินผ่าน:

1. โหลด workbook ต้นฉบับที่มี pivot table อยู่แล้ว  
2. **Create new workbook** objects สำหรับปลายทาง  
3. ใช้ `CopyRows` เพื่อถ่ายโอนช่วงที่มี pivot table  
4. บันทึกผลลัพธ์พร้อมรับประกันว่า pivot table ยังคงทำงานได้  

ไม่ต้องอ้างอิงเอกสารภายนอก—เพียงโค้ด, เหตุผล, และเคล็ดลับปฏิบัติที่คุณสามารถวางลงในโปรเจคของคุณได้ทันที

> **Pro tip:** Aspose.Cells ทำงานกับ .NET Core, .NET Framework, และแม้แต่ Xamarin, ดังนั้นโค้ดส่วนนั้นจะทำงานได้ทุกที่ที่คุณต้องการ

---

![Create new workbook with copied pivot table](/images/create-new-workbook-pivot.png "create new workbook with copied pivot table")

## ขั้นตอนที่ 1 – สร้าง Workbook ใหม่และโหลดไฟล์ต้นฉบับ

สิ่งแรกที่เราทำคือ **create new workbook** objects หนึ่งเก็บข้อมูลต้นฉบับ อีกหนึ่งจะรับช่วงที่คัดลอก

```csharp
using Aspose.Cells;

// Load the source workbook that already contains a pivot table
var sourceWorkbook = new Workbook(@"C:\Data\source.xlsx");

// Create an empty workbook that will become the destination
var destinationWorkbook = new Workbook();
```

*ทำไมเรื่องนี้ถึงสำคัญ:*  
`Workbook` เป็นจุดเริ่มต้นสำหรับการจัดการ Excel ใด ๆ ใน Aspose.Cells โดยการสร้าง workbook ใหม่ เรารับประกันว่ามีพื้นฐานที่สะอาด—ไม่มีสไตล์ที่ซ่อนอยู่หรือ worksheet ที่หลงเหลือซึ่งอาจรบกวนในภายหลัง

## ขั้นตอนที่ 2 – วิธีคัดลอกแถวรวมถึง Pivot Table

ต่อไปคือหัวใจของปัญหา: **how to copy rows** ที่ครอบคลุม pivot table โดยไม่ทำให้แบนลง `CopyRows` ทำหน้าที่นั้นได้อย่างแม่นยำ

```csharp
// Copy the first 20 rows (adjust as needed) from the source to the destination
// Parameters: startRow, totalRows, targetCells, targetStartRow
sourceWorkbook.Worksheets[0].Cells.CopyRows(
    startRow: 0,
    totalRows: 20,
    targetCells: destinationWorkbook.Worksheets[0].Cells,
    targetStartRow: 0);
```

สิ่งที่ควรทราบ:

* `startRow` และ `totalRows` กำหนดบล็อกที่มี pivot table.  
* เมธอดนี้คัดลอก **ทั้ง** ข้อมูลดิบและ pivot cache ทำให้ workbook ปลายทางรู้วิธีสร้าง pivot table ใหม่แบบทันที  
* หาก pivot ของคุณเริ่มที่ตำแหน่งลึกลงในแผ่นงาน เพียงเปลี่ยนดัชนี—ไม่ต้องเรียก API อื่น  

> **Common question:** *Will the copied pivot lose its source data reference?*  
> ไม่. Aspose.Cells ฝัง cache ลงใน worksheet โดยตรง ทำให้ pivot เป็นอิสระในไฟล์ใหม่

## ขั้นตอนที่ 3 – รักษา Pivot Table เมื่อบันทึกไฟล์ปลายทาง

หลังจากที่แถวถูกคัดลอก pivot table จะอยู่ใน workbook ปลายทางเช่นเดียวกับในต้นฉบับ การบันทึกไฟล์ทำได้อย่างง่ายดาย

```csharp
// Save the destination workbook; the pivot table remains functional
destinationWorkbook.Save(@"C:\Data\destination.xlsx");
```

เมื่อคุณเปิด `destination.xlsx` ใน Excel คุณจะเห็น pivot table พร้อมรีเฟรช พฤติกรรม **preserve pivot table** จะทำงานอัตโนมัติเนื่องจาก cache มาพร้อมกับแถว

### ตรวจสอบผลลัพธ์

เปิดไฟล์และ:

1. คลิกที่ pivot table.  
2. สังเกตว่ารายการฟิลด์ปรากฏ—หมายความว่า cache ยังสมบูรณ์  
3. ลองรีเฟรช; ข้อมูลอัปเดตโดยไม่มีข้อผิดพลาด  

หากคุณเจอข้อผิดพลาด *#REF!* ให้ตรวจสอบอีกครั้งว่าช่วงที่คัดลอกรวมแถว cache ที่ซ่อนอยู่ (มักอยู่หลังข้อมูลที่มองเห็น)

## ขั้นตอนที่ 4 – ทำสำเนา Pivot Table ไปยังหลาย Workbook (ทางเลือก)

บางครั้งคุณต้องการ pivot เดียวกันในหลาย ๆ รายงาน รูปแบบที่เราใช้ข้างต้นขยายได้ดี—เพียงทำซ้ำการคัดลอกสำหรับแต่ละ workbook ใหม่

```csharp
string[] targets = {
    @"C:\Reports\Q1.xlsx",
    @"C:\Reports\Q2.xlsx",
    @"C:\Reports\Q3.xlsx"
};

foreach (var path in targets)
{
    var wb = new Workbook(); // fresh workbook each loop
    sourceWorkbook.Worksheets[0].Cells.CopyRows(0, 20, wb.Worksheets[0].Cells, 0);
    wb.Save(path);
}
```

โค้ดส่วนนี้ **duplicates pivot table** สามครั้งด้วยลูปเดียว ปรับอาร์เรย์ `targets` ให้ตรงกับตารางการรายงานของคุณ

### กรณีขอบที่ควรคำนึงถึง

| Situation | What to Watch For | Fix |
|-----------|-------------------|-----|
| Pivot ใช้แหล่งข้อมูลภายนอก | Cache อาจอ้างอิงการเชื่อมต่อที่ไม่มีในเครื่องใหม่ | ฝังแหล่งข้อมูลหรือสร้างการเชื่อมต่อใหม่ใน workbook ปลายทาง |
| Pivot ขนาดใหญ่มาก ( > 100 k แถว ) | `CopyRows` อาจใช้หน่วยความจำมาก | ใช้ `CopyRows` เป็นส่วน ๆ หรือพิจารณา `Copy` กับ `PasteOptions` เพื่อลดการใช้หน่วยความจำ |
| Worksheet มีแถว/คอลัมน์ที่ซ่อนอยู่ | แถว cache ที่ซ่อนอาจถูกข้ามหากคุณคัดลอกเฉพาะแถวที่มองเห็น | ควรคัดลอกช่วงแถวที่มี cache อย่างแม่นยำ ไม่ใช่แค่พื้นที่ที่มองเห็น |

## ตัวอย่างการทำงานเต็มรูปแบบ

รวมทั้งหมดเข้าด้วยกัน นี่คือโปรแกรมที่ทำงานอิสระซึ่งคุณสามารถใส่ลงในแอปคอนโซลได้

```csharp
using System;
using Aspose.Cells;

namespace PivotCopyDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load source workbook (contains the original pivot)
            var sourcePath = @"C:\Data\source.xlsx";
            var sourceWorkbook = new Workbook(sourcePath);

            // 2️⃣ Prepare destination workbook
            var destinationWorkbook = new Workbook();

            // 3️⃣ Copy rows that include the pivot (adjust range as needed)
            sourceWorkbook.Worksheets[0].Cells.CopyRows(
                startRow: 0,
                totalRows: 20,
                targetCells: destinationWorkbook.Worksheets[0].Cells,
                targetStartRow: 0);

            // 4️⃣ Save – the pivot table is preserved
            var destPath = @"C:\Data\destination.xlsx";
            destinationWorkbook.Save(destPath);

            Console.WriteLine("Pivot table successfully copied!");
        }
    }
}
```

รันโปรแกรม เปิด `destination.xlsx` แล้วคุณจะเห็น pivot table เดียวกันพร้อมที่จะสไลซ์และจัดการข้อมูลของคุณ ไม่ต้องสร้างใหม่ด้วยตนเอง

---

## สรุป

เราเพิ่งแสดงวิธี **create new workbook** ใน C# และ **copy pivot table** พร้อมรักษาการตั้งค่าทั้งหมดไว้ ด้วยการใช้ `CopyRows` คุณจะได้วิธีที่เชื่อถือได้ในการ **preserve pivot table** ทำงาน ตอบคำถามเก่าแก่ “**how to copy rows**” และแม้กระทั่ง **duplicate pivot table** ไปยังหลายรายงานด้วยโค้ดเพียงเล็กน้อย

ขั้นตอนต่อไป? ลองเปลี่ยนช่วงที่คัดลอกให้รวมแผนภูมิที่อ้างอิง pivot เดียวกัน หรือทดลองใช้ `PasteOptions` เพื่อรักษาการจัดรูปแบบอย่างแม่นยำ รูปแบบเดียวกันทำงานกับวัตถุ Aspose.Cells อื่น ๆ เช่น ตารางและ named ranges ดังนั้นคุณสามารถขยายต่อได้ตามต้องการ

มีปัญหาอื่นที่คุณกำลังต่อสู้—เช่น pivot ที่ดึงข้อมูลจาก DB ภายนอก หรือ workbook ที่อยู่บนคลาวด์? แสดงความคิดเห็นด้านล่าง แล้วเราจะช่วยกันแก้ไข ขอให้สนุกกับการเขียนโค้ด!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}