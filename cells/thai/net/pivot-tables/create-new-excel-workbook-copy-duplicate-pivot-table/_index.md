---
category: general
date: 2026-02-09
description: สร้างสมุดงาน Excel ใหม่และเรียนรู้วิธีคัดลอก Pivot Table อย่างง่ายดาย
  คู่มือนี้แสดงวิธีทำสำเนา Pivot Table และบันทึกสมุดงานเป็นไฟล์ใหม่
draft: false
keywords:
- create new excel workbook
- how to copy pivot
- duplicate pivot table
- save workbook as new
- how to copy worksheet
language: th
og_description: สร้างไฟล์ Excel ใหม่ใน C# และคัดลอก Pivot Table ทันที เรียนรู้วิธีทำสำเนา
  Pivot Table และบันทึกไฟล์เป็นไฟล์ใหม่พร้อมตัวอย่างโค้ดเต็มรูปแบบ
og_title: สร้างสมุดงาน Excel ใหม่ – คัดลอก Pivot ทีละขั้นตอน
tags:
- excel
- csharp
- aspose.cells
- automation
title: สร้างเวิร์กบุ๊ก Excel ใหม่ – คัดลอกและทำสำเนาตาราง Pivot
url: /th/net/pivot-tables/create-new-excel-workbook-copy-duplicate-pivot-table/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# สร้างเวิร์กบุ๊ก Excel ใหม่ – คัดลอกและทำสำเนาตาราง Pivot

เคยต้อง **สร้างเวิร์กบุ๊ก Excel ใหม่** ที่นำตาราง Pivot ซับซ้อนจากไฟล์เดิมมาด้วยหรือไม่? คุณไม่ได้เป็นคนเดียว—นักพัฒนาหลายคนเจออุปสรรคนี้เมื่อต้องทำอัตโนมัติของ pipeline รายงาน ข่าวดีคือด้วยไม่กี่บรรทัดของ C# และไลบรารี Aspose.Cells คุณสามารถ **วิธีคัดลอก Pivot** อย่างรวดเร็ว, **ทำสำเนาตาราง Pivot**, และ **บันทึกเวิร์กบุ๊กเป็นไฟล์ใหม่** โดยไม่ต้องเปิด Excel ด้วยตนเอง

ในคู่มือนี้เราจะเดินผ่านกระบวนการทั้งหมด ตั้งแต่การโหลดเวิร์กบุ๊กต้นทางจนถึงการบันทึกเวอร์ชันที่ทำสำเนาไว้ สุดท้ายคุณจะได้สคริปต์ที่พร้อมรันและสามารถใส่ลงในโปรเจกต์ .NET ใดก็ได้ ไม่มีส่วนเกิน เพียงวิธีแก้ปัญหาที่ใช้งานได้จริงที่คุณสามารถทดสอบได้ทันที

## สิ่งที่บทเรียนนี้ครอบคลุม

* **ข้อกำหนดเบื้องต้น** – .NET 6+ (หรือ .NET Framework 4.6+), Visual Studio, และแพ็กเกจ NuGet Aspose.Cells for .NET
* โค้ดขั้นตอน‑โดย‑ขั้นตอนที่ **สร้างเวิร์กบุ๊ก Excel ใหม่**, คัดลอก Pivot, และเขียนผลลัพธ์ลงดิสก์
* คำอธิบาย **ทำไม** แต่ละบรรทัดถึงสำคัญ, ไม่ใช่แค่ **ทำอะไร**
* เคล็ดลับการจัดการกรณีขอบเช่นแผ่นงานที่ซ่อนหรือช่วงข้อมูลขนาดใหญ่
* มุมมองสั้น ๆ เกี่ยวกับ **วิธีคัดลอกแผ่นงาน** หากคุณต้องการคัดลอกทั้งแผ่นแทน Pivot เพียงอย่างเดียว

พร้อมหรือยัง? ไปดูกันเลย

![create new excel workbook illustration](image.png "Diagram showing source workbook, pivot copy, and destination workbook")

## ขั้นตอนที่ 1: ตั้งค่าโปรเจกต์และติดตั้ง Aspose.Cells

ก่อนที่เราจะ **สร้างเวิร์กบุ๊ก Excel ใหม่** เราต้องมีโปรเจกต์ที่อ้างอิงไลบรารีที่ถูกต้อง

```csharp
// Install the Aspose.Cells package via NuGet:
//   dotnet add package Aspose.Cells
using Aspose.Cells;   // Provides Workbook, Worksheet, Range, etc.
using System;        // For basic .NET types
```

*ทำไมเรื่องนี้สำคัญ:* Aspose.Cells ทำงานทั้งหมดในหน่วยความจำ ดังนั้นคุณไม่ต้องเปิด Excel บนเซิร์ฟเวอร์เลย มันยังคงรักษาข้อมูลแคชของ Pivot ไว้ซึ่งจำเป็นต่อการทำ **สำเนาตาราง Pivot** ที่แท้จริง

> **Pro tip:** หากคุณกำลังพัฒนาเป็น .NET Core ให้ตรวจสอบให้แน่ใจว่า Runtime Identifier (RID) ของโปรเจกต์ตรงกับแพลตฟอร์มที่คุณจะทำการดีพลอย; มิฉะนั้นอาจเจอข้อผิดพลาดการโหลดไลบรารีแบบเนทีฟ

## ขั้นตอนที่ 2: โหลดเวิร์กบุ๊กต้นทางที่มี Pivot

ต่อไปเราจะ **วิธีคัดลอก Pivot** จากไฟล์ที่มีอยู่แล้ว เวิร์กบุ๊กต้นทางอาจอยู่บนดิสก์, เป็นสตรีม, หรือแม้กระทั่งเป็นอาเรย์ไบต์

```csharp
// Step 2: Load the source workbook that contains the pivot table
string sourcePath = @"C:\Reports\source.xlsx";
Workbook sourceWorkbook = new Workbook(sourcePath);

// Grab the first worksheet (adjust the index if your pivot lives elsewhere)
Worksheet sourceSheet = sourceWorkbook.Worksheets[0];

// Define the range that encloses the pivot table – A1:D20 in this example
Range sourceRange = sourceSheet.Cells.CreateRange("A1:D20");
```

*ทำไมเราถึงเลือกช่วง:* ตาราง Pivot อยู่ภายในช่วงเซลล์ปกติ แต่มีข้อมูลแคชที่ซ่อนอยู่เชื่อมกับแผ่นงาน การคัดลอกช่วง **รวม Pivot** ทำให้ Aspose.Cells ย้ายแคชไปด้วย ให้คุณได้ **สำเนาตาราง Pivot** ที่ทำงานได้เต็มที่ในไฟล์ปลายทาง

## ขั้นตอนที่ 3: สร้างเวิร์กบุ๊ก Excel ใหม่เพื่อรับข้อมูลที่คัดลอก

นี่คือขั้นตอนที่เราจริง ๆ **สร้างเวิร์กบุ๊ก Excel ใหม่** ที่จะเก็บ Pivot ที่ทำสำเนาไว้

```csharp
// Step 3: Create a fresh workbook (empty) for the destination
Workbook destinationWorkbook = new Workbook(); // Starts with a default empty sheet
Worksheet destinationSheet = destinationWorkbook.Worksheets[0];

// Destination starts at A1 – you could offset if you need space for other data
Range destinationRange = destinationSheet.Cells.CreateRange("A1");
```

> **ทำไมต้องเวิร์กบุ๊กใหม่?** การเริ่มจากศูนย์รับประกันว่าไม่มีการจัดรูปแบบหรือออบเจกต์ที่ซ่อนอยู่แทรกแซง Pivot ที่คัดลอก นอกจากนี้ไฟล์ที่ได้จะมีขนาดเล็กลง ซึ่งสะดวกสำหรับการแนบอีเมลอัตโนมัติ

## ขั้นตอนที่ 4: คัดลอกช่วง Pivot ไปยังเวิร์กบุ๊กใหม่

ต่อไปเราจะทำการ **วิธีคัดลอก Pivot** จริง

```csharp
// Step 4: Copy the range (including the pivot) from source to destination
sourceRange.Copy(destinationRange);
```

บรรทัดเดียวนี้ทำงานหนักทั้งหมด:

* ค่าของเซลล์, สูตร, และการจัดรูปแบบถูกถ่ายโอน
* แคชของ Pivot ถูกทำสำเนา ทำให้ Pivot ใหม่ทำงานได้เต็มที่
* การอ้างอิงแบบ relative ภายใน Pivot จะปรับอัตโนมัติตามตำแหน่งใหม่

### การจัดการกรณีขอบ

* **แผ่นงานที่ซ่อน:** หากแผ่นงานต้นทางถูกซ่อน Pivot ยังคัดลอกได้ดี แต่คุณอาจต้องทำให้แผ่นงานปลายทางแสดงเพื่อให้ผู้ใช้มองเห็น:
  ```csharp
  destinationSheet.IsVisible = true;
  ```
* **ชุดข้อมูลขนาดใหญ่:** สำหรับช่วงที่มีแถวหลายพัน ให้พิจารณาใช้ `CopyTo` พร้อม `CopyOptions` เพื่อสตรีมการทำงานและลดความกดดันของหน่วยความจำ

## ขั้นตอนที่ 5: บันทึกเวิร์กบุ๊กปลายทางเป็นไฟล์ใหม่

สุดท้ายเราจะ **บันทึกเวิร์กบุ๊กเป็นไฟล์ใหม่** และตรวจสอบผลลัพธ์

```csharp
// Step 5: Save the destination workbook with the duplicated pivot table
string destPath = @"C:\Reports\copied.xlsx";
destinationWorkbook.Save(destPath, SaveFormat.Xlsx);

// Quick verification – open the file manually or read a cell value
Console.WriteLine($"Workbook saved to {destPath}");
```

หากคุณเปิด `copied.xlsx` จะเห็นสำเนาตรงของ Pivot ดั้งเดิม พร้อมใช้งานต่อหรือแจกจ่ายได้ทันที

### ตัวเลือกเสริม: วิธีคัดลอกแผ่นงานแทน Pivot เพียงอย่างเดียว

บางครั้งคุณต้องการคัดลอกทั้งแผ่น ไม่ใช่แค่ Pivot API เดียวกันทำให้ทำได้ง่าย:

```csharp
// Copy the whole worksheet (including all charts, tables, etc.)
sourceSheet.CopyTo(destinationWorkbook, 0); // Inserts at index 0
destinationWorkbook.Save(@"C:\Reports\full_copy.xlsx");
```

วิธีนี้ตอบโจทย์ **วิธีคัดลอกแผ่นงาน** และเป็นประโยชน์เมื่อคุณต้องการรักษาการตั้งค่าระดับแผ่นเพิ่มเติมไว้

## ตัวอย่างทำงานเต็มรูปแบบ

รวมทุกขั้นตอนเข้าด้วยกัน นี่คือแอปคอนโซลแบบอิสระที่คุณสามารถคอมไพล์และรันได้

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // 1️⃣ Load source workbook
        string sourcePath = @"C:\Reports\source.xlsx";
        Workbook sourceWorkbook = new Workbook(sourcePath);
        Worksheet sourceSheet = sourceWorkbook.Worksheets[0];
        Range sourceRange = sourceSheet.Cells.CreateRange("A1:D20");

        // 2️⃣ Create destination workbook
        Workbook destinationWorkbook = new Workbook();
        Worksheet destinationSheet = destinationWorkbook.Worksheets[0];
        Range destinationRange = destinationSheet.Cells.CreateRange("A1");

        // 3️⃣ Copy the pivot (range)
        sourceRange.Copy(destinationRange);

        // 4️⃣ Save as new file
        string destPath = @"C:\Reports\copied.xlsx";
        destinationWorkbook.Save(destPath, SaveFormat.Xlsx);

        Console.WriteLine($"✅ Successfully created new Excel workbook with duplicated pivot table at {destPath}");
    }
}
```

**ผลลัพธ์ที่คาดหวัง:** คอนโซลจะแสดงข้อความสำเร็จ และไฟล์ `copied.xlsx` จะปรากฏใน `C:\Reports` พร้อม Pivot ที่ทำงานได้เหมือนกับใน `source.xlsx`

## คำถามทั่วไปและข้อควรระวัง

* **สูตรภายใน Pivot จะพังหรือไม่?** ไม่—เพราะแคชของ Pivot ถูกยกมาด้วย ฟิลด์ที่คำนวณทั้งหมดจะคงอยู่
* **ถ้า Pivot ต้นทางใช้การเชื่อมต่อข้อมูลภายนอกล่ะ?** การเชื่อมต่อเหล่านั้น *ไม่* ถูกคัดลอก คุณต้องสร้างใหม่ในเวิร์กบุ๊กปลายทางหรือแปลง Pivot เป็นตารางคงที่ก่อน
* **สามารถคัดลอก Pivot หลายตัวพร้อมกันได้หรือไม่?** ทำได้—เพียงกำหนดช่วงที่ใหญ่พอเพื่อครอบคลุม Pivot ทั้งหมด, หรือวนลูปผ่านแต่ละอ็อบเจกต์ `PivotTable` ใน `sourceSheet.PivotTables` แล้วคัดลอกทีละอัน
* **ต้องทำการ Dispose ของอ็อบเจกต์ `Workbook` หรือไม่?** พวกมัน implements `IDisposable` ดังนั้นการห่อไว้ใน `using` เป็นนิสัยที่ดี โดยเฉพาะในบริการที่ต้องประมวลผลจำนวนมาก

## สรุป

ตอนนี้คุณรู้แล้วว่า **วิธีสร้างเวิร์กบุ๊ก Excel ใหม่**, คัดลอก Pivot, **ทำสำเนาตาราง Pivot**, และ **บันทึกเวิร์กบุ๊กเป็นไฟล์ใหม่** ด้วย C# และ Aspose.Cells ขั้นตอนง่าย ๆ คือ โหลด, สร้าง, คัดลอก, และบันทึก ด้วยสคริปต์ **วิธีคัดลอกแผ่นงาน** เสริม คุณยังมีทางเลือกสำหรับการทำสำเนาเต็มแผ่นอีกด้วย

ต่อไปคุณอาจอยากสำรวจ:

* เพิ่มการจัดรูปแบบแบบกำหนดเองให้กับ Pivot ที่ทำสำเนา
* รีเฟรชแคชของ Pivot โดยโปรแกรมหลังจากเปลี่ยนแปลงข้อมูล
* ส่งออกเวิร์กบุ๊กเป็น PDF หรือ CSV สำหรับระบบ downstream

ลองใช้ ปรับช่วงตามต้องการ แล้วให้การอัตโนมัติทำงานหนักให้คุณในกระบวนการรายงานของคุณเอง Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}