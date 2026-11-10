---
category: general
date: 2026-08-07
description: ลบ autofilter จาก Excel ใน C# อย่างรวดเร็ว เรียนรู้วิธีปิดฟิลเตอร์ของ
  Excel, ลบฟิลเตอร์ของตาราง Excel, และล้าง autofilter ของตาราง Excel ด้วย Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- remove autofilter from excel
- how to turn off excel filter
- delete excel table filter
- clear excel table autofilter
language: th
lastmod: 2026-08-07
og_description: ลบ autofilter จาก Excel ด้วย C# และดูวิธีปิดฟิลเตอร์ของ Excel, ลบฟิลเตอร์ตาราง
  Excel, และล้าง autofilter ของตาราง Excel ด้วย Aspose.Cells.
og_image_alt: Screenshot showing an Excel sheet after remove autofilter from excel
og_title: ลบ autofilter จาก Excel ใน C# – สอนทีละขั้นตอน
schemas:
- author: Aspose
  dateModified: '2026-08-07'
  description: Remove autofilter from Excel in C# quickly. Learn how to turn off Excel
    filter, delete Excel table filter, and clear Excel table autofilter with Aspose.Cells.
  headline: Remove autofilter from Excel in C# – complete guide
  type: TechArticle
- description: Remove autofilter from Excel in C# quickly. Learn how to turn off Excel
    filter, delete Excel table filter, and clear Excel table autofilter with Aspose.Cells.
  name: Remove autofilter from Excel in C# – complete guide
  steps:
  - name: Expected output
    text: 'Open `output.xlsx` in Excel:'
  - name: Multiple tables in the same worksheet
    text: 'If the worksheet contains more than one table, iterate over the collection:'
  - name: Removing filter from a specific column only
    text: 'Aspose.Cells does not expose a column‑level `AutoFilter` removal, but you
      can recreate the table without the filter:'
  - name: Working with older Excel formats (*.xls)
    text: Aspose.Cells supports the legacy binary format automatically. The same code
      works; just ensure the file extension matches the input file.
  - name: Handling large workbooks
    text: For files larger than 100 MB, enable the **LoadOptions** to use the **MemoryOptimized**
      mode, which reduces memory pressure while still allowing table manipulation.
  type: HowTo
tags:
- Excel
- C#
- Aspose.Cells
title: การลบ Autofilter จาก Excel ด้วย C# – คู่มือฉบับสมบูรณ์
url: /th/net/excel-autofilter-validation/remove-autofilter-from-excel-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ลบ autofilter จาก Excel ด้วย C# – คู่มือเต็ม

หากคุณต้องการ **remove autofilter from Excel** ขณะประมวลผลไฟล์โดยอัตโนมัติ คู่มือนี้จะแสดงให้คุณเห็นอย่างชัดเจน คุณจะได้เรียนรู้วิธีที่เร็วที่สุดในการ turn off Excel filter, delete Excel table filter, และ clear Excel table autofilter ด้วยไลบรารี Aspose.Cells

บทเรียนนี้ครอบคลุมทุกอย่างตั้งแต่การตั้งค่าโครงการจนถึงการตรวจสอบว่า workbook ที่ส่งออกไม่แสดงลูกศรตัวกรองอีกต่อไป ไม่ต้องทำขั้นตอนด้วยตนเอง และโค้ดทำงานกับไฟล์ .xlsx ใด ๆ ที่มีตารางพร้อม AutoFilter

## ข้อกำหนดเบื้องต้น

ก่อนเริ่มทำงาน ให้แน่ใจว่าคุณมี:

- .NET 6.0 หรือใหม่กว่า ติดตั้งแล้ว  
- Visual Studio 2022 (หรือ IDE สำหรับ C# ใดก็ได้)  
- ไลเซนส์สำหรับ **Aspose.Cells for .NET** (รุ่นทดลองฟรีใช้สำหรับทดสอบได้)  
- ไฟล์ Excel (`input.xlsx`) ที่มีอย่างน้อยหนึ่งตารางพร้อม AutoFilter ที่ใช้งานอยู่  

คุณยังต้องเพิ่มแพคเกจ NuGet ของ Aspose.Cells ไปยังโครงการของคุณด้วย:

```bash
dotnet add package Aspose.Cells
```

> **เคล็ดลับ:** เก็บ workbook ไว้ในโฟลเดอร์ที่แอปพลิเคชันของคุณสามารถอ่าน/เขียนได้โดยไม่ต้องยกระดับสิทธิ์เพื่อหลีกเลี่ยง `UnauthorizedAccessException`.

![remove autofilter from excel](/assets/remove-autofilter.png "remove autofilter from excel – Excel sheet without filter arrows")

## ลบ autofilter จาก Excel – ขั้นตอนที่ 1: โหลด workbook

การดำเนินการแรกคือเปิด workbook ต้นฉบับ การโหลดไฟล์เข้าสู่หน่วยความจำทำให้คุณเข้าถึง worksheets, tables และคุณสมบัติต่าง ๆ ได้เต็มที่

```csharp
using Aspose.Cells;

// Step 1: Load the workbook containing a table with an AutoFilter
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

*ทำไมเรื่องนี้ถึงสำคัญ:* `Workbook` คืออ็อบเจกต์หลักใน Aspose.Cells มันทำการแยกแพคเกจ XLSX และสร้างโมเดลอ็อบเจกต์ที่สะท้อนโครงสร้างภายในของ Excel ทำให้คุณสามารถจัดการตารางโดยตรงได้

## วิธี turn off Excel filter – ขั้นตอนที่ 2: เข้าถึง worksheet เป้าหมาย

ไฟล์ Excel สามารถมีหลาย worksheet ได้ แต่ตัวอย่างนี้มุ่งเน้นที่ใบแรก ปรับดัชนีหากข้อมูลของคุณอยู่ในตำแหน่งอื่น

```csharp
// Step 2: Access the first worksheet (index 0)
Worksheet worksheet = workbook.Worksheets[0];
```

*ทำไมเรื่องนี้ถึงสำคัญ:* แต่ละ `Worksheet` มีคอลเลกชันของตารางของตนเอง การดึง worksheet ที่ถูกต้องทำให้คุณมั่นใจว่ากำลังแก้ไขตารางที่ต้องการ

## Delete Excel table filter – ขั้นตอนที่ 3: ค้นหาตารางแรก

ตารางจะถูกเก็บไว้ในคอลเลกชัน `Tables` ของ worksheet คุณสามารถวนลูปผ่านตารางได้ แต่เพื่อความง่าย เราจะดึงตารางแรกมาใช้งาน

```csharp
// Step 3: Retrieve the first table on the worksheet
Table table = worksheet.Tables[0];
```

*ทำไมเรื่องนี้ถึงสำคัญ:* อ็อบเจกต์ `Table` มีคุณสมบัติ `AutoFilter` ที่ควบคุม UI ของตัวกรอง การเข้าถึงตารางเป็นขั้นตอนก่อนหน้าที่จำเป็นสำหรับการลบตัวกรอง

## Clear Excel table autofilter – ขั้นตอนที่ 4: ลบ AutoFilter

การตั้งค่าคุณสมบัติ `AutoFilter` ให้เป็น `null` จะลบ UI ตัวกรองออกอย่างสมบูรณ์ ข้อมูลพื้นฐานยังคงไม่เปลี่ยนแปลง

```csharp
// Step 4: Remove the AutoFilter by setting it to null
table.AutoFilter = null;
```

*ทำไมเรื่องนี้ถึงสำคัญ:* เมื่อ `AutoFilter` เป็น `null` Excel จะไม่แสดงลูกศรดรอป‑ดาวน์อีกต่อไป และเงื่อนไขตัวกรองที่เคยตั้งไว้จะถูกล้าง นี่คือการดำเนินการหลักสำหรับ **delete excel table filter**

## Save the workbook – ขั้นตอนที่ 5: ตรวจสอบผลลัพธ์

สุดท้ายให้เขียน workbook ที่แก้ไขแล้วลงดิสก์ ไฟล์ที่บันทึกจะเปิดใน Excel โดยไม่มีลูกศรตัวกรองใด ๆ

```csharp
// Step 5: Save the workbook; the table is now a plain data table without filter UI
workbook.Save("YOUR_DIRECTORY/output.xlsx");
```

### ผลลัพธ์ที่คาดหวัง

เปิด `output.xlsx` ใน Excel:

- ตารางจะแสดงเป็นข้อมูลทั่วไป—ไม่มีลูกศรตัวกรองปรากฏในแถวหัวตาราง  
- แถวทั้งหมดจะมองเห็นได้ ชี้ให้เห็นว่าตัวกรองได้ถูกล้างแล้ว  

หากคุณยังเห็นลูกศรอยู่ ให้ตรวจสอบว่าไฟล์ต้นฉบับมี AutoFilter จริง ๆ และคุณได้เลือกดัชนีตารางที่ถูกต้องหรือไม่

## ความแปรผันทั่วไปและกรณีขอบ

### ตารางหลายตารางใน worksheet เดียว

หาก worksheet มีมากกว่าหนึ่งตาราง ให้วนลูปผ่านคอลเลกชัน:

```csharp
foreach (Table tbl in worksheet.Tables)
{
    tbl.AutoFilter = null; // clear filter for each table
}
```

### ลบตัวกรองจากคอลัมน์เฉพาะเท่านั้น

Aspose.Cells ไม่ได้เปิดเผยการลบ `AutoFilter` ระดับคอลัมน์โดยตรง แต่คุณสามารถสร้างตารางใหม่โดยไม่มีตัวกรองได้:

```csharp
// Capture existing data range
CellArea range = table.DisplayRange;

// Remove the table (including filter)
worksheet.Tables.RemoveAt(table.Index);

// Re‑add the table without AutoFilter
Table newTable = worksheet.Tables[worksheet.Tables.Add(range.StartRow, range.StartColumn, range.EndRow, range.EndColumn, true)];
```

### ทำงานกับรูปแบบ Excel รุ่นเก่า (*.xls)

Aspose.Cells รองรับรูปแบบไบนารีแบบเก่าโดยอัตโนมัติ โค้ดเดียวกันทำงานได้; เพียงตรวจสอบให้ส่วนขยายไฟล์ตรงกับไฟล์อินพุต

### จัดการ workbook ขนาดใหญ่

สำหรับไฟล์ที่ใหญ่กว่า 100 MB ให้เปิดใช้ **LoadOptions** เพื่อใช้โหมด **MemoryOptimized** ซึ่งลดความกดดันของหน่วยความจำในขณะที่ยังคงสามารถจัดการตารางได้

```csharp
LoadOptions options = new LoadOptions(LoadFormat.Xlsx) { MemoryOptimization = true };
Workbook largeWorkbook = new Workbook("large_input.xlsx", options);
```

## ตัวอย่างเต็มที่สามารถรันได้

ด้านล่างเป็นโปรแกรมเต็มที่คุณสามารถคัดลอก วาง และรันเป็นแอปพลิเคชันคอนโซล

```csharp
using System;
using Aspose.Cells;

namespace RemoveExcelAutoFilter
{
    class Program
    {
        static void Main()
        {
            // Define file paths
            string inputPath = @"YOUR_DIRECTORY\input.xlsx";
            string outputPath = @"YOUR_DIRECTORY\output.xlsx";

            // Load the workbook
            Workbook workbook = new Workbook(inputPath);

            // Access the first worksheet
            Worksheet worksheet = workbook.Worksheets[0];

            // Ensure the worksheet contains at least one table
            if (worksheet.Tables.Count == 0)
            {
                Console.WriteLine("No tables found on the first worksheet.");
                return;
            }

            // Retrieve the first table and clear its AutoFilter
            Table table = worksheet.Tables[0];
            table.AutoFilter = null;

            // Save the modified workbook
            workbook.Save(outputPath);

            Console.WriteLine($"AutoFilter removed. Saved to {outputPath}");
        }
    }
}
```

รันโปรแกรมแล้วเปิด `output.xlsx` คุณจะเห็นว่าการ **remove autofilter from excel** สำเร็จและแผ่นงานแสดงตารางข้อมูลแบบธรรมดา

## สรุป

ตอนนี้คุณรู้วิธี **remove autofilter from Excel** ด้วย C# แล้ว โดยการโหลด workbook, เข้าถึงตารางเป้าหมาย, และตั้งค่า `AutoFilter` ให้เป็น `null` คุณสามารถ **turn off Excel filter**, **delete Excel table filter**, และ **clear Excel table autofilter** ได้ในขั้นตอนเดียวที่เชื่อถือได้  

ต่อไปลองสำรวจหัวข้อที่เกี่ยวข้อง เช่น **formatting Excel tables with Aspose.Cells**, **exporting filtered data to CSV**, หรือ **applying conditional formatting programmatically** แต่ละหัวข้อสร้างบนโมเดลอ็อบเจกต์เดียวกันที่คุณเพิ่งเชี่ยวชาญ

อย่ากลัวที่จะทดลองกับหลายตาราง, workbook ขนาดใหญ่, หรือรูปแบบไฟล์ต่าง ๆ—ทักษะใหม่ของคุณจะทำให้การอัตโนมัติ Excel ราบรื่นและคาดเดาได้ง่ายขึ้น ขอให้สนุกกับการเขียนโค้ด!

## ควรเรียนรู้อะไรต่อไป?

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งข้อมูลมีตัวอย่างโค้ดทำงานครบถ้วนพร้อมคำอธิบายขั้นตอนเพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการทำงานอื่น ๆ ในโครงการของคุณเอง

- [ลบ UI ตัวกรองใน Excel ด้วย C# – ปุ่ม Remove AutoFilter](/cells/english/net/excel-autofilter-validation/clear-filter-ui-in-excel-with-c-remove-autofilter-button/)
- [วิธีใช้ AutoFilter ใน Excel ด้วย Aspose.Cells for .NET (คู่มือการวิเคราะห์ข้อมูล)](/cells/english/net/data-analysis/implement-autofilter-excel-aspose-cells-dotnet/)
- [วิธีใช้ Excel Autofilter 'EndsWith' ด้วย Aspose.Cells for .NET](/cells/english/net/data-analysis/implement-autofilter-endswith-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}