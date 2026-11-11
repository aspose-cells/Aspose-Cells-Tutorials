---
category: general
date: 2026-10-26
description: ปิดการใช้งาน Autofilter ใน Excel ด้วย C# บทเรียนนี้แสดงวิธีการลบ Autofilter
  จากตาราง Excel ด้วยโปรแกรมและรวมตัวอย่างทำงานเต็มรูปแบบ.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- disable autofilter in excel
- remove autofilter from excel table
- Excel automation C#
- Aspose.Cells filter handling
- programmatic Excel editing
language: th
lastmod: 2026-10-26
og_description: ปิดการใช้งาน Autofilter ใน Excel อย่างรวดเร็ว. ทำตามคำแนะนำนี้เพื่อเอา
  Autofilter ออกจากตาราง Excel ด้วย C# และ Aspose.Cells.
og_image_alt: Screenshot of an Excel worksheet where the autofilter has been disabled
og_title: ปิดการใช้งาน Autofilter ใน Excel ด้วย C# – คู่มือแบบทีละขั้นตอน
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: disable autofilter in Excel using C#. This tutorial shows how to remove
    autofilter from Excel table programmatically and includes a full working example.
  headline: How to disable autofilter in Excel with C# – complete guide
  type: TechArticle
- description: disable autofilter in Excel using C#. This tutorial shows how to remove
    autofilter from Excel table programmatically and includes a full working example.
  name: How to disable autofilter in Excel with C# – complete guide
  steps:
  - name: Open the saved file (`Sample_NoFilter.xlsx`) in Microsoft Excel.
    text: Open the saved file (`Sample_NoFilter.xlsx`) in Microsoft Excel.
  - name: Click any column header – you should **not** see the drop‑down filter arrow.
    text: Click any column header – you should **not** see the drop‑down filter arrow.
  - name: 'If you still see arrows, double‑check that the table you targeted is indeed
      the one with the filter. You can list all tables with:'
    text: 'If you still see arrows, double‑check that the table you targeted is indeed
      the one with the filter. You can list all tables with:'
  type: HowTo
tags:
- Excel
- C#
- Aspose.Cells
title: วิธีปิดการใช้งาน Autofilter ใน Excel ด้วย C# – คู่มือครบถ้วน
url: /th/net/excel-autofilter-validation/how-to-disable-autofilter-in-excel-with-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีปิดการใช้งาน Autofilter ใน Excel ด้วย C# – คู่มือฉบับสมบูรณ์

หากคุณต้องการ **ปิดการใช้งาน autofilter ใน Excel** คู่มือนี้จะแสดงวิธีทำอย่างละเอียดจาก C# ไม่ว่าคุณจะกำลังทำความสะอาดรายงานก่อนเผยแพร่หรืออัตโนมัติการส่งออกข้อมูล การลบฟิลเตอร์จะทำให้แผ่นงานแสดงทุกแถวอย่างครบถ้วน คุณยังจะได้เรียนรู้วิธี **remove autofilter from Excel table** ด้วยการเรียกเดียวที่เชื่อถือได้

เราจะใช้ไลบรารี **Aspose.Cells for .NET** ที่เป็นที่นิยม เพราะทำงานได้โดยไม่ต้องติดตั้ง Excel บนเซิร์ฟเวอร์ เมื่อจบบทเรียนนี้คุณจะมีแอปพลิเคชันคอนโซลแบบอิสระที่โหลดเวิร์กบุ๊ก หาเทเบิลแรก และปิดการใช้งาน autofilter ของมัน โซลูชันนี้ทำงานกับไฟล์ .xlsx ที่สร้างด้วย Excel 2007 หรือใหม่กว่า

## สิ่งที่คุณต้องเตรียม

| Prerequisite | Why it matters |
|--------------|----------------|
| .NET 6.0 หรือใหม่กว่า | ให้ runtime สำหรับโค้ด C# |
| Aspose.Cells for .NET (แพ็กเกจ NuGet `Aspose.Cells`) | ให้การเข้าถึงเวิร์กชีต, เทเบิล, และ autofilter ผ่านโปรแกรม |
| ตัวอย่างไฟล์ Excel (`Sample.xlsx`) ที่มีอย่างน้อยหนึ่งเทเบิลพร้อม autofilter | โค้ดทำงานกับเทเบิลแรก; การมีเทเบิลช่วยให้เราสาธิตการปิดฟิลเตอร์ |
| Visual Studio 2022 (หรือ IDE C# ใดก็ได้) | ทำให้การสร้างและดีบักแอปคอนโซลง่ายขึ้น |

> **Pro tip:** หากคุณต้องการทางเลือกฟรี คุณสามารถปรับโค้ดให้ใช้ **ClosedXML** หรือ **EPPlus**; แนวคิดหลัก—การตั้งค่า `AutoFilter` ของเทเบิลเป็น `null`—ยังคงเหมือนเดิม

## ขั้นตอนที่ 1: สร้างโปรเจกต์คอนโซลใหม่

เปิดเทอร์มินัลหรือ Visual Studio command prompt แล้วรัน:

```bash
dotnet new console -n ExcelFilterDemo
cd ExcelFilterDemo
dotnet add package Aspose.Cells
```

คำสั่งนี้จะสร้างโปรเจกต์ใหม่ชื่อ `ExcelFilterDemo` และดึงไลบรารี Aspose.Cells เข้ามา

## ขั้นตอนที่ 2: โหลดเวิร์กบุ๊กและหาเวิร์กชีตแรก

การดำเนินการแรกคือเปิดไฟล์เวิร์กบุ๊ก Aspose.Cells จะอ่านไฟล์เข้าสู่วัตถุ `Workbook` ที่ให้คุณเข้าถึงเวิร์กชีตและเทเบิลโดยตรง

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Path to the Excel file you want to modify
        const string inputPath = "Sample.xlsx";

        // Load the workbook into memory
        Workbook wb = new Workbook(inputPath);

        // Access the first worksheet (index 0)
        Worksheet worksheet = wb.Worksheets[0];
```

> **ทำไมต้องทำขั้นตอนนี้?** การโหลดเวิร์กบุ๊กเป็นสิ่งจำเป็นก่อนที่คุณจะสามารถจัดการกับวัตถุ Excel ใด ๆ ได้ การใช้เวิร์กชีตแรก (`Worksheets[0]`) สะท้อนสถานการณ์ทั่วไปที่ข้อมูลหลักอยู่บนชีตแรก

## ขั้นตอนที่ 3: ดึงเทเบิลแรกที่กำหนดบนเวิร์กชีต

เทเบิลใน Excel (หรือที่เรียกว่า ListObjects) เป็นคอนเทนเนอร์ที่เก็บข้อมูลเชิงโครงสร้าง แต่ละเทเบิลอาจมี autofilter ของตนเอง เพื่อเอาฟิลเตอร์ออกเราต้องอ้างอิงวัตถุเทเบิลก่อน

```csharp
        // Get the first table on the worksheet.
        // If the worksheet has no tables, this will throw an IndexOutOfRangeException.
        Table table = worksheet.Tables[0];
```

> **กรณีขอบ:** หากเวิร์กบุ๊กอาจมีเวิร์กชีตที่ไม่มีเทเบิล ให้ห่อการเข้าถึงด้วยการตรวจสอบ `if (worksheet.Tables.Count > 0)` นี้จะป้องกันข้อผิดพลาดรันไทม์และทำให้โซลูชันมั่นคงยิ่งขึ้น

## ขั้นตอนที่ 4: ปิดการใช้งาน autofilter สำหรับเทเบิล

การปิดจริง ๆ ทำได้ในบรรทัดเดียว: กำหนดค่า `null` ให้กับคุณสมบัติ `AutoFilter` ของวัตถุ `Table` นี้จะล้างเงื่อนไขฟิลเตอร์ทั้งหมดและลบลูกศรดรอปดาวน์จากแถวหัวตาราง

```csharp
        // Disable the autofilter – this clears any applied filter.
        table.AutoFilter = null;
```

หลังจากบรรทัดนี้ทำงานแล้ว เทเบิลจะทำงานเหมือนช่วงข้อมูลธรรมดาโดยไม่มี UI ฟิลเตอร์

## ขั้นตอนที่ 5: บันทึกเวิร์กบุ๊กที่แก้ไขแล้ว

สุดท้ายให้เขียนการเปลี่ยนแปลงกลับไปยังดิสก์ คุณสามารถเขียนทับไฟล์เดิมหรือสร้างไฟล์ใหม่เพื่อเก็บต้นฉบับไว้

```csharp
        // Save the workbook. Use a new file name to avoid overwriting the original.
        const string outputPath = "Sample_NoFilter.xlsx";
        wb.Save(outputPath);

        System.Console.WriteLine($"Autofilter disabled. Saved to {outputPath}");
    }
}
```

### โค้ดต้นฉบับเต็ม

เมื่อรวมทุกส่วนเข้าด้วยกัน โปรแกรมเต็มจะเป็นดังนี้:

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Path to the original Excel file
        const string inputPath = "Sample.xlsx";

        // Load the workbook
        Workbook wb = new Workbook(inputPath);

        // Access the first worksheet
        Worksheet worksheet = wb.Worksheets[0];

        // Ensure the worksheet contains at least one table
        if (worksheet.Tables.Count == 0)
        {
            System.Console.WriteLine("No tables found on the first worksheet.");
            return;
        }

        // Get the first table
        Table table = worksheet.Tables[0];

        // Disable the autofilter – clears any applied filter
        table.AutoFilter = null;

        // Save the modified workbook
        const string outputPath = "Sample_NoFilter.xlsx";
        wb.Save(outputPath);

        System.Console.WriteLine($"Autofilter disabled. Saved to {outputPath}");
    }
}
```

รันโปรแกรมด้วย `dotnet run` หลังจากทำงานเสร็จ เปิดไฟล์ `Sample_NoFilter.xlsx` ใน Excel; คุณจะเห็นว่าลูกศรฟิลเตอร์หายไปและทุกแถวแสดงครบ

## ตรวจสอบว่า autofilter หายจริงหรือไม่

1. เปิดไฟล์ที่บันทึกไว้ (`Sample_NoFilter.xlsx`) ใน Microsoft Excel.  
2. คลิกหัวคอลัมน์ใดก็ได้ – คุณ **ไม่ควร** เห็นลูกศรดรอปดาวน์ของฟิลเตอร์.  
3. หากยังเห็นลูกศร ให้ตรวจสอบว่าคุณได้เลือกเทเบิลที่มีฟิลเตอร์จริง ๆ หรือไม่ คุณสามารถแสดงรายการเทเบิลทั้งหมดด้วย:

```csharp
foreach (var tbl in worksheet.Tables)
{
    System.Console.WriteLine($"Table name: {tbl.Name}, Has AutoFilter: {tbl.AutoFilter != null}");
}
```

ผลลัพธ์ในคอนโซลควรรายงาน `Has AutoFilter: False` สำหรับเทเบิลที่คุณแก้ไข

## ข้อผิดพลาดทั่วไปและวิธีหลีกเลี่ยง

| Symptom | Likely cause | Fix |
|---------|--------------|-----|
| `IndexOutOfRangeException` ที่ `worksheet.Tables[0]` | เวิร์กชีตไม่มีเทเบิล | เพิ่มการตรวจสอบ `if (worksheet.Tables.Count == 0)` ก่อนเข้าถึง |
| ไฟล์ที่บันทึกยังคงแสดงฟิลเตอร์ | แก้ไขเวิร์กชีตหรือเทเบิลผิด | ใช้ `wb.Worksheets["SheetName"]` หรือวนลูป `wb.Worksheets` เพื่อหาเทเบิลที่ต้องการ |
| โปรแกรมพังบน .NET เวอร์ชันเก่า | Aspose.Cells ต้องการ .NET 6.0+ สำหรับแพ็กเกจล่าสุด | อัปเกรด target framework ในไฟล์ `.csproj` |
| NullReferenceException เมื่อ `table.AutoFilter` เป็น null อยู่แล้ว | คุณเรียกโค้ดสองครั้งบนไฟล์เดียวโดยไม่โหลดใหม่ | โหลดเวิร์กบุ๊กใหม่หรือเช็ค `if (table.AutoFilter != null)` ก่อนกำหนดค่า |

## การต่อยอดโซลูชัน

ตอนนี้คุณรู้วิธี **disable autofilter in Excel** แล้ว อาจต้องการ:

* **Remove autofilter from Excel table** เฉพาะเมื่อเงื่อนไขบางอย่างเป็นจริง (เช่น เมื่อผู้ใช้ตั้งค่า flag). เพิ่มเงื่อนไข `if` รอบ `table.AutoFilter = null;`.
* **Apply filter ใหม่** อย่างโปรแกรมเมติกหลังจากล้างฟิลเตอร์เก่าโดยใช้ `table.AutoFilter.Range` และ `table.AutoFilter.AddFilterColumn(...)`.
* **ประมวลผลหลายเทเบิล** ในเวิร์กบุ๊กเดียวโดยวนลูป `worksheet.Tables` และปิดฟิลเตอร์แต่ละอัน

การต่อยอดเหล่านี้ใช้รูปแบบเดียวกับที่แสดงข้างต้นและช่วยให้โค้ดคงความสะอาด

## สรุป

คุณมีวิธีที่กระชับและพร้อมใช้งานในระดับ production เพื่อ **disable autofilter in Excel** ด้วย C# โดยการโหลดเวิร์กบุ๊ก, เข้าถึงเทเบิลแรก, และตั้งค่า `table.AutoFilter = null` คุณจึง **remove autofilter from Excel table** ได้โดยไม่ต้องทำด้วยตนเอง ตัวอย่างเต็มคอมไพล์, รัน, และสร้างไฟล์ที่สะอาดพร้อมสำหรับการอัตโนมัติหรือการแจกจ่ายต่อไป

ลองทดลองกับเทเบิลเพิ่มเติม, เงื่อนไขต่าง ๆ, หรือไลบรารีทางเลือก หากเจอกรณีขอบ ให้กลับไปดูส่วนการแก้ไขปัญหาหรือสำรวจเอกสาร Aspose.Cells ที่ครอบคลุมการจัดการฟิลเตอร์ขั้นสูง ขอให้สนุกกับการเขียนโค้ด!

## คุณควรเรียนรู้อะไรต่อไป?

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคในคู่มือนี้ แต่ละแหล่งรวมโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายทีละขั้นตอนเพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการทำงานอื่น ๆ ในโปรเจกต์ของคุณ

- [วิธีลบ autofilter จากตาราง Excel ด้วย C#](/cells/english/net/excel-autofilter-validation/how-to-remove-autofilter-from-excel-tables-using-c/)
- [ลบ UI ฟิลเตอร์ใน Excel ด้วย C# – ปุ่ม Remove AutoFilter](/cells/english/net/excel-autofilter-validation/clear-filter-ui-in-excel-with-c-remove-autofilter-button/)
- [วิธีใช้ AutoFilter ในการทำ Automation Excel ด้วย C# – คู่มือเต็มขั้นตอน](/cells/english/net/excel-autofilter-validation/how-to-use-autofilter-in-c-excel-automation-full-step-by-ste/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}