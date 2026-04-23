---
category: general
date: 2026-02-09
description: ลบ UI ตัวกรองใน Excel ด้วย C# โดยการลบปุ่ม AutoFilter เรียนรู้วิธีซ่อนปุ่มตัวกรอง
  แสดงแถวหัวตาราง และทำให้แผ่นงานของคุณเป็นระเบียบ.
draft: false
keywords:
- clear filter UI
- remove autofilter excel
- how to remove autofilter
- show header row
- hide filter button
language: th
og_description: ลบ UI ตัวกรองใน Excel ด้วย C# คู่มือนี้แสดงวิธีซ่อนปุ่มตัวกรอง แสดงแถวหัวตาราง
  และทำให้แผ่นงานสะอาดเรียบร้อย
og_title: ลบ UI ตัวกรองใน Excel ด้วย C# – ลบปุ่ม AutoFilter
tags:
- excel
- csharp
- epplus
- automation
title: เคลียร์ UI ตัวกรองใน Excel ด้วย C# – ลบปุ่ม AutoFilter
url: /th/net/excel-autofilter-validation/clear-filter-ui-in-excel-with-c-remove-autofilter-button/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Clear filter UI in Excel with C# – Remove AutoFilter Button

เคยต้องการ **clear filter UI** ในแผ่น Excel แต่ไม่แน่ใจว่าบรรทัดโค้ดใดที่จริง ๆ แล้วซ่อนลูกศรดรอป‑ดาวน์เล็ก ๆ นั้นหรือไม่? คุณไม่ได้เป็นคนเดียว ปุ่มตัวกรองอาจเป็นสิ่งที่ทำให้ดูรบกวนเมื่อคุณส่งรายงานให้ผู้ใช้ปลายทางที่ไม่ต้องการเปลี่ยนมุมมองเลย  

ในบทเรียนนี้เราจะพาคุณผ่านตัวอย่างที่ทำงานได้เต็มรูปแบบ ซึ่ง **removes the AutoFilter button** จากตาราง, ทำให้แถวหัวตารางยังคงมองเห็นได้, และยังพูดถึงวิธี *hide filter button* อย่างถาวร ด้วยการทำตามขั้นตอนนี้ คุณจะรู้ **how to remove AutoFilter** ใน C# อย่างแม่นยำและเหตุผลที่แต่ละขั้นตอนสำคัญ

## What You’ll Need

- .NET 6+ (หรือ .NET Framework 4.7.2+) – รันไทม์รุ่นใหม่ใดก็ได้
- แพคเกจ NuGet **EPPlus** (เวอร์ชัน 6.x หรือใหม่กว่า) – ให้เราใช้ `ExcelWorksheet`, `ExcelTable` เป็นต้น
- ไฟล์ Excel ง่าย ๆ ที่มีตารางชื่อ **SalesTable** (สร้างได้ในไม่กี่คลิก)

แค่นั้นเอง ไม่ต้องใช้ COM interop, ไม่ต้องมี DLL เพิ่มเติม, เพียงแค่ `using` บางบรรทัดและโค้ดไม่กี่บรรทัด

## Clear filter UI: Removing the AutoFilter Button

แกนหลักของวิธีแก้ปัญหานี้อยู่ในสามคำสั่งสั้น ๆ ให้เรามาแยกแต่ละขั้นตอนเพื่อให้คุณเข้าใจ *ทำไม* จึงต้องทำ, ไม่ใช่แค่ *อะไร* ที่ทำ

### Step 1 – Grab a reference to the table

```csharp
// Step 1: Get a reference to the "SalesTable" in the first worksheet
ExcelTable salesTable = package.Workbook.Worksheets[0].Tables["SalesTable"];
```

ทำไมจึงสำคัญ: EPPlus ทำงานกับ **tables** (`ExcelTable`) ไม่ใช่ช่วงข้อมูลดิบ การดึงอ็อบเจกต์ตารางทำให้เราสามารถเข้าถึงคุณสมบัติ `AutoFilter` ซึ่งควบคุม UI ที่คุณเห็นบนชีต หากคุณพยายามจัดการ worksheet โดยตรง คุณจะส่งผลแค่ค่าข้อมูลเท่านั้น ไม่ได้กระทบปุ่มตัวกรอง

### Step 2 – Remove the AutoFilter button row

```csharp
// Step 2: Remove the AutoFilter button row (clears any applied filter UI)
salesTable.AutoFilter = null;
```

การตั้งค่า `AutoFilter` เป็น `null` บอก EPPlus ให้ลบแถวตัวกรองที่อยู่ด้านล่าง นี่คือการทำ *clear filter UI* ที่นักพัฒนาส่วนใหญ่มองหาเมื่อถามว่า “**how to remove autofilter**” เป็นวิธีแบบบรรทัดเดียวที่ทำงานได้กับทุกเวอร์ชันของ Excel ที่ EPPlus รองรับ

### Step 3 – Keep the header row visible

```csharp
// Step 3: Ensure the header row remains visible after removing the filter
salesTable.ShowHeader = true;
```

เมื่อคุณลบ UI ตัวกรอง Excel บางครั้งอาจซ่อนแถวหัวตารางหากแฟล็ก `ShowHeader` ของตารางเป็น false การตั้งค่าให้เป็น `true` อย่างชัดเจนจะทำให้ชื่อคอลัมน์ยังคงแสดงบนหน้าจอ – รายละเอียดเล็ก ๆ แต่สำคัญสำหรับรายงานที่ดูเป็นมืออาชีพ

### Full, runnable example

ด้านล่างเป็นแอปคอนโซลขนาดเล็กที่เปิด workbook ที่มีอยู่, ทำสามขั้นตอนข้างต้น, แล้วบันทึกผลลัพธ์ คัดลอก‑วาง, กด **F5**, แล้วดูปุ่มตัวกรองหายไป

```csharp
using System;
using System.IO;
using OfficeOpenXml;
using OfficeOpenXml.Table;

class Program
{
    static void Main()
    {
        // EPPlus requires a license context for non‑commercial use.
        ExcelPackage.LicenseContext = LicenseContext.NonCommercial;

        // 1️⃣ Load the workbook (replace with your own path)
        var filePath = Path.Combine(Environment.CurrentDirectory, "SalesReport.xlsx");
        if (!File.Exists(filePath))
        {
            Console.WriteLine($"File not found: {filePath}");
            return;
        }

        using var package = new ExcelPackage(new FileInfo(filePath));

        // 2️⃣ Get a reference to the table named "SalesTable"
        ExcelTable salesTable = package.Workbook.Worksheets[0].Tables["SalesTable"];
        if (salesTable == null)
        {
            Console.WriteLine("Table 'SalesTable' not found in the first worksheet.");
            return;
        }

        // 3️⃣ Remove the AutoFilter button (clear filter UI)
        salesTable.AutoFilter = null;

        // 4️⃣ Ensure the header row stays visible (show header row)
        salesTable.ShowHeader = true;

        // 5️⃣ Save the changes to a new file so you don’t overwrite the original
        var outputPath = Path.Combine(Environment.CurrentDirectory, "SalesReport_NoFilter.xlsx");
        package.SaveAs(new FileInfo(outputPath));

        Console.WriteLine($"Filter button removed. Saved to {outputPath}");
    }
}
```

**Expected result:** เปิด *SalesReport_NoFilter.xlsx* – ลูกศรตัวกรองหายไป, แต่หัวคอลัมน์ยังคงอยู่ ไม่มี UI “click‑to‑filter” ที่รกอีกต่อไป

> **Pro tip:** หากคุณมี **multiple tables** และต้องการ hide filter button สำหรับทุกตาราง, ให้วนลูปผ่าน `worksheet.Tables` แล้วใช้สามบรรทัดเดียวกันภายในลูป

## How to remove AutoFilter in Excel using C# – a deeper dive

คุณอาจสงสัยว่า “ถ้า workbook มีตัวกรองเปิดอยู่แล้ว การตั้งค่า `AutoFilter = null` จะลบแถวที่ถูกกรองด้วยหรือไม่?” คำตอบคือ **yes**. EPPlus จะลบทั้ง UI และเงื่อนไขตัวกรองที่อยู่ภายใต้, ทำให้ข้อมูลกลับไปอยู่ในลำดับเดิม  

หากคุณต้องการ *hide* ปุ่มแต่ยังให้ตัวกรองทำงานอยู่, สามารถตั้งค่า `AutoFilter` เป็น **new empty filter** แทนได้:

```csharp
salesTable.AutoFilter = new ExcelAutoFilter(); // hides button, retains filter logic
```

วิธีนี้สะดวกเมื่อคุณต้องการ *hide filter button* เพื่อให้หน้าตาดูเรียบหรู แต่ยังให้ผู้ใช้ระดับสูงสามารถสลับตัวกรองผ่าน VBA หรือริบบอนได้

### Edge case: Tables without a header row

บางรายงานเก่าใช้ช่วงข้อมูลธรรมดาแทนตาราง ในกรณีนั้น EPPlus จะไม่เปิดเผยอ็อบเจกต์ `ExcelTable`, ดังนั้นโค้ดด้านบนจะเกิดข้อผิดพลาด วิธีแก้คือ **convert the range to a table** ก่อน:

```csharp
var range = worksheet.Cells["A1:D100"];
var table = worksheet.Tables.Add(range, "TempTable");
table.ShowHeader = true;    // ensure header is visible
table.AutoFilter = null;    // clear filter UI
```

ตอนนี้คุณได้ *removed autofilter excel* แบบ UI แม้บนช่วงที่เริ่มต้นไม่มีตารางอย่างเป็นทางการแล้ว

## Show header row after hiding filter button – why it matters

ข้อร้องเรียนทั่วไปคือหลังจากคุณ hide filter UI, แถวหัวตารางบางครั้งหายไป, โดยเฉพาะเมื่อ workbook ถูกสร้างด้วยการตั้งค่า “Hide Header” เปิดอยู่ การตั้งค่า `salesTable.ShowHeader = true;` อย่างชัดเจนจะป้องกันความประหลาดใจนี้  

หากคุณต้องการ **hide filter button** แต่ให้หัวตารางยังคงซ่อนอยู่ (เช่น กำลังสร้างข้อมูลดิบ), เพียงตั้งค่า `salesTable.ShowHeader = false;` หลังจากลบตัวกรอง โค้ดนี้สมมาตร ทำให้สลับได้ง่ายตามแฟล็กการตั้งค่า

## Hide filter button – practical tips and pitfalls

- **Version compatibility:** EPPlus 6+ ทำงานกับไฟล์ `.xlsx` เท่านั้น หากคุณต้องจัดการไฟล์ `.xls` เก่า จะต้องใช้ไลบรารีอื่น (เช่น NPOI) เพราะ API *clear filter UI* ไม่พร้อมใช้งาน
- **Performance:** การโหลด workbook ขนาดใหญ่เพียงเพื่อซ่อนปุ่มเดียวอาจช้า ควรใช้ `ExcelPackage.Load(stream, true)` เพื่อเปิดในโหมด **read‑only**, ทำการเปลี่ยนแปลง, แล้วบันทึก
- **Testing:** ตรวจสอบไฟล์ผลลัพธ์ด้วยตนเองครั้งแรกเสมอ การทดสอบ UI อัตโนมัติสามารถตรวจสอบว่าลูกศรตัวกรองหายจริง (`worksheet.Tables[0].AutoFilter == null`)
- **Licensing:** EPPlus เปลี่ยนเป็นไลเซนส์คู่ในเวอร์ชัน 5 สำหรับโครงการเชิงพาณิชย์คุณจะต้องซื้อไลเซนส์หรือเปลี่ยนไปใช้ไลบรารีอื่น

## Full source file for copy‑paste

ด้านล่างเป็นไฟล์ที่คุณสามารถวางลงในโปรเจกต์คอนโซลใหม่ได้โดยตรง ไม่ต้องมีการพึ่งพาซ่อนใด ๆ ทั้งหมดเป็นอิสระ

```csharp
// File: Program.cs
using System;
using System.IO;
using OfficeOpenXml;
using OfficeOpenXml.Table;

namespace ExcelFilterCleaner
{
    class Program
    {
        static void Main()
        {
            // License context – required for EPPlus 5+
            ExcelPackage.LicenseContext = LicenseContext.NonCommercial;

            // Path to the original workbook (adjust as needed)
            string sourcePath = Path.Combine(Environment.CurrentDirectory, "SalesReport.xlsx");
            if (!File.Exists(sourcePath))
            {
                Console.WriteLine($"Source file not found: {sourcePath}");
                return;
            }

            // Load workbook
            using var package = new ExcelPackage(new FileInfo(sourcePath));

            // Assume the first worksheet contains the table
            var worksheet = package.Workbook.Worksheets[0];
            const string tableName = "SalesTable";

            // Grab the table; abort if missing
            var salesTable = worksheet.Tables[tableName];
            if (salesTable == null)
            {
                Console.WriteLine($"Table '{tableName}' not found.");
                return;
            }

            // ---- Clear filter UI ----
            salesTable.AutoFilter = null;   // removes the filter button row
            salesTable.ShowHeader = true;   // guarantees the header row stays visible

            // Save to a new file so the original stays untouched
            string destPath = Path.Combine(Environment.CurrentDirectory, "SalesReport_NoFilter.xlsx");
            package.SaveAs(new FileInfo(destPath));

            Console.WriteLine($"Successfully cleared filter UI. Output: {destPath}");
        }
    }
}
```

รัน `dotnet add package EPPlus --version 6.0.8` (หรือเวอร์ชันล่าสุด) ก่อนทำการคอมไพล์, แล้วคุณจะได้ชีตที่สะอาดพร้อมแจกจ่าย

## Conclusion

เราได้แสดงให้คุณเห็น **how to remove AutoFilter** และ **clear filter UI** ใน workbook ของ Excel ด้วย C# ส่วนแกนหลักสามบรรทัด (`AutoFilter = null;`, `ShowHeader = true;`) ทำหน้าที่หลัก, ส่วนโค้ดส่วนอื่นช่วยให้วิธีแก้ดูเป็นมืออาชีพ

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}