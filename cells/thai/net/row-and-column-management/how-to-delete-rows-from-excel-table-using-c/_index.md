---
category: general
date: 2026-09-27
description: เรียนรู้วิธีลบแถวจากตาราง Excel ด้วย C# ผ่านคู่มือขั้นตอนที่แสดงวิธีโหลดไฟล์
  Excel ด้วย C# อย่างรวดเร็ว.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- delete rows from Excel table
- load Excel workbook C#
language: th
lastmod: 2026-09-27
og_description: ลบแถวจากตาราง Excel ด้วย C# พร้อมตัวอย่างที่ชัดเจน บทเรียนนี้ยังครอบคลุมวิธีโหลดไฟล์
  Excel ด้วย C# และจัดการกับกรณีขอบเขตทั่วไป
og_image_alt: Screenshot illustrating delete rows from Excel table using C# code
og_title: ลบแถวจากตาราง Excel ด้วย C# – คู่มือโค้ดเต็ม
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Learn how to delete rows from Excel table in C# with a step‑by‑step
    guide that also shows how to load Excel workbook C# quickly.
  headline: How to delete rows from Excel table using C#
  type: TechArticle
- description: Learn how to delete rows from Excel table in C# with a step‑by‑step
    guide that also shows how to load Excel workbook C# quickly.
  name: How to delete rows from Excel table using C#
  steps:
  - name: What if the table has a different name or position?
    text: '* **Named table:** Use `ws.ListObjects["MyTableName"]` instead of the index.
      * **Multiple tables:** Loop through `ws.ListObjects` and pick the one that matches
      a condition (e.g., column header names). * **Dynamic row count:** You can compute
      `rowCount` at runtime by inspecting `ws.ListObjects[0].Dat'
  - name: Edge‑case handling
    text: '| Situation | Recommended code change | |----------------------------------------|--------------------------------------------------------------|
      | Table is empty or has fewer rows | Check `ws.ListObjects[0].DataRange.RowCount`
      before deleting. | | Rows to delete exceed table size | Clamp `rowCount`'
  - name: How do I delete rows from **all** tables in a workbook?
    text: '```csharp foreach (Worksheet sheet in workbook.Worksheets) { foreach (ListObject
      tbl in sheet.ListObjects) { // Example: delete the first data row of each table
      if (tbl.DataRange.RowCount > 1) tbl.DeleteRows(1, 1); } } ```'
  - name: Can I delete rows based on a **cell value**?
    text: 'Yes. Scan the `DataRange` for matching cells, collect their zero‑based
      indices, then delete in descending order:'
  - name: What if I need to **preserve formatting**?
    text: '`DeleteRows` removes the entire row from the table but retains the table’s
      style for remaining rows. If you need to keep specific formatting on a row you’re
      deleting, copy the style to another row before deletion.'
  - name: Does this work with **.xls** (Excel 97‑2003) files?
    text: Yes. Aspose.Cells automatically detects the file format, so the same code
      works with `.xls`. Just change the file extension in the `Workbook` constructor.
  - name: Next steps
    text: '* Explore **ClosedXML** or **EPPlus** if you prefer a fully open‑source
      stack. * Combine row deletion with **data validation** to clean spreadsheets
      before importing into a database. * Automate the process for a folder of workbooks
      using `Directory.GetFiles` and a loop.'
  type: HowTo
tags:
- Excel
- C#
- .NET
title: วิธีลบแถวจากตาราง Excel ด้วย C#
url: /th/net/row-and-column-management/how-to-delete-rows-from-excel-table-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ลบแถวจากตาราง Excel ใน C# – คู่มือการเขียนโปรแกรมฉบับสมบูรณ์

หากคุณต้องการ **ลบแถวจากตาราง Excel** ในไฟล์ .xlsx นี้เป็นบทแนะนำที่แสดงวิธีทำอย่างละเอียดด้วย C# คุณจะได้เห็นตัวอย่างสั้น ๆ ที่สามารถรันได้ ซึ่งโหลดเวิร์กบุ๊ก Excel, ลบแถวที่ระบุจากตารางแรก, แล้วบันทึกผลลัพธ์ วิธีนี้ทำงานร่วมกับไลบรารี Aspose.Cells ที่เป็นที่นิยมและสามารถปรับใช้กับ .NET Excel API อื่น ๆ ได้

การลบแถวจากตารางเป็นงานทั่วไปเมื่อทำความสะอาดข้อมูลที่นำเข้า, ตัดส่วนของรายงาน, หรือทำการอัปเดตสเปรดชีตโดยอัตโนมัติ เมื่ออ่านคู่มือนี้จนจบแล้วคุณจะสามารถ **load Excel workbook C#**, ค้นหาตาราง (ListObject), ลบแถวใด ๆ ที่ต้องการ, และเขียนไฟล์ที่แก้ไขแล้วกลับไปยังดิสก์ได้

## Prerequisites

ก่อนเริ่มทำงาน โปรดตรวจสอบว่าคุณมี:

* .NET 6.0 หรือใหม่กว่า (โค้ดนี้ยังทำงานได้กับ .NET Framework 4.7+)
* การอ้างอิงไปยังแพคเกจ NuGet **Aspose.Cells** (หรือไลบรารีที่เข้ากันได้ซึ่งมีประเภท `Workbook`, `Worksheet`, และ `ListObject`)
* ไฟล์อินพุตชื่อ `input.xlsx` อยู่ในโฟลเดอร์ที่คุณสามารถอ้างอิงจากโปรเจกต์ได้
* ความคุ้นเคยพื้นฐานกับไวยากรณ์ C# และ Visual Studio (หรือ IDE ที่คุณชื่นชอบ)

> **Pro tip:** หากคุณต้องการใช้ทางเลือกแบบโอเพ่นซอร์สเดียวกัน สามารถใช้ **ClosedXML** แทนได้ – เพียงเปลี่ยนคลาสที่เฉพาะของ Aspose เป็น `XLWorkbook`, `IXLWorksheet`, และ `IXLTable`

## Step 1: Load the Excel workbook in C#

ขั้นตอนแรกคือการอ่านไฟล์ต้นทางเข้าสู่หน่วยความจำ การโหลดเวิร์กบุ๊กเป็นกระบวนการที่เร็วสำหรับขนาดสเปรดชีตทั่วไปและให้คุณเข้าถึง worksheets, tables, และค่าของเซลล์ได้อย่างเต็มที่

```csharp
using Aspose.Cells;

// Step 1: Load the workbook
// Replace YOUR_DIRECTORY with the actual folder path, e.g. @"C:\Data"
Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");
```

*Why this matters:* `Workbook` จะทำการพาร์สโครงสร้าง Open XML ของไฟล์ .xlsx และให้คอลเลกชันของอ็อบเจ็กต์ `Worksheet` หากไฟล์ไม่พบ Aspose จะโยน `FileNotFoundException` ดังนั้นตรวจสอบให้แน่ใจว่าเส้นทางถูกต้อง

## Step 2: Access the target worksheet

สเปรดชีตส่วนใหญ่มีหลายชีต; คุณต้องเลือกชีตที่มีตารางที่ต้องการแก้ไข ที่นี่เราใช้ชีตแรก (`Worksheets[0]`) ซึ่งเป็นค่าเริ่มต้นที่ปลอดภัยสำหรับไฟล์ง่าย ๆ

```csharp
// Step 2: Access the first worksheet
Worksheet ws = workbook.Worksheets[0];
```

*Why this matters:* `Worksheet` เป็นคอนเทนเนอร์ของตาราง (`ListObjects`) การเข้าถึงชีตที่ถูกต้องจะป้องกันการเปลี่ยนแปลงโดยบังเอิญกับข้อมูลที่ไม่เกี่ยวข้อง

## Step 3: Delete rows from Excel table

ตาราง Excel แสดงด้วยอ็อบเจ็กต์ `ListObject` ตารางแรกบนชีตคือ `ListObjects[0]` เมธอด `DeleteRows(startIndex, rowCount)` จะลบแถว **ตามพื้นที่ข้อมูลของตาราง** ไม่ใช่หมายเลขแถวแบบสัมบูรณ์ของชีต

ในตัวอย่างนี้เราลบแถวที่สองและสามของตาราง (หัวตารางอยู่ที่แถว 0 จึงเริ่มที่ดัชนี 1)

```csharp
// Step 3: Delete rows 1 and 2 from the first table (ListObject)
// The first row (index 0) is the header, so we start at index 1
ws.ListObjects[0].DeleteRows(1, 2);
```

### What if the table has a different name or position?

* **Named table:** ใช้ `ws.ListObjects["MyTableName"]` แทนการอ้างอิงด้วยดัชนี
* **Multiple tables:** วนลูป `ws.ListObjects` แล้วเลือกตารางที่ตรงกับเงื่อนไข (เช่น ชื่อคอลัมน์หัวตาราง)
* **Dynamic row count:** สามารถคำนวณ `rowCount` ขณะรันได้โดยตรวจสอบ `ws.ListObjects[0].DataRange.RowCount`

### Edge‑case handling

| สถานการณ์ | การเปลี่ยนแปลงโค้ดที่แนะนำ |
|------------------------------|--------------------------------------------------------------|
| ตารางว่างหรือมีแถวน้อยกว่า | ตรวจสอบ `ws.ListObjects[0].DataRange.RowCount` ก่อนทำการลบ. |
| จำนวนแถวที่ต้องการลบเกินขนาดของตาราง | จำกัด `rowCount` ให้เป็น `DataRange.RowCount - startIndex`. |
| ต้องการลบแถวตามเงื่อนไข (เช่น ค่าที่คอลัมน์ C) | วนลูป `DataRange.Rows` เก็บดัชนีที่ตรงกัน แล้วลบในลำดับย้อนกลับเพื่อคงดัชนีให้คงที่. |

## Step 4: Save the modified workbook

หลังจากลบแถวแล้ว ให้บันทึกเวิร์กบุ๊กกลับไปยังไฟล์ใหม่ (หรือเขียนทับไฟล์เดิมหากต้องการ) การบันทึกจะสร้างไฟล์ .xlsx ใหม่ที่สะท้อนตารางที่อัปเดตแล้ว

```csharp
// Step 4: Save the modified workbook
workbook.Save(@"YOUR_DIRECTORY\output.xlsx");
```

*Why this matters:* `Save` จะทำการซีเรียลไลซ์อ็อบเจ็กต์ในหน่วยความจำลงดิสก์ หากคุณต้องการเก็บไฟล์ต้นฉบับไว้ ควรบันทึกไปยังเส้นทางอื่นเสมอ

## Full, runnable example

รวมทุกขั้นตอนเข้าด้วยกันจะได้โปรแกรมที่พร้อมคัดลอก, วาง, และรันได้

```csharp
using System;
using Aspose.Cells;

class ExcelRowDeletion
{
    static void Main()
    {
        // Adjust the folder path as needed
        const string folder = @"YOUR_DIRECTORY";

        // Load the workbook (load Excel workbook C#)
        Workbook workbook = new Workbook($"{folder}\\input.xlsx");

        // Access the first worksheet
        Worksheet ws = workbook.Worksheets[0];

        // Ensure the worksheet contains at least one table
        if (ws.ListObjects.Count == 0)
        {
            Console.WriteLine("No tables found on the first worksheet.");
            return;
        }

        // Delete rows 1 and 2 from the first table (skip header)
        ListObject table = ws.ListObjects[0];
        int rowsToDelete = Math.Min(2, table.DataRange.RowCount - 1); // guard against short tables
        if (rowsToDelete > 0)
        {
            table.DeleteRows(1, rowsToDelete);
            Console.WriteLine($"Deleted {rowsToDelete} row(s) from table \"{table.Name}\".");
        }
        else
        {
            Console.WriteLine("Table does not have enough rows to delete.");
        }

        // Save the result
        workbook.Save($"{folder}\\output.xlsx");
        Console.WriteLine("Workbook saved as output.xlsx");
    }
}
```

**Expected output** (console):

```
Deleted 2 row(s) from table "Table1".
Workbook saved as output.xlsx
```

เปิด `output.xlsx` – ตารางแรกตอนนี้ไม่มีแถวที่คุณลบออกแล้ว แต่แถวหัวตารางยังคงอยู่ครบถ้วน

## Common questions and variations

### How do I delete rows from **all** tables in a workbook?

```csharp
foreach (Worksheet sheet in workbook.Worksheets)
{
    foreach (ListObject tbl in sheet.ListObjects)
    {
        // Example: delete the first data row of each table
        if (tbl.DataRange.RowCount > 1)
            tbl.DeleteRows(1, 1);
    }
}
```

### Can I delete rows based on a **cell value**?

ใช่. สแกน `DataRange` เพื่อหาค่าเซลล์ที่ตรงกัน, เก็บดัชนีศูนย์‑ฐาน, แล้วลบในลำดับจากมากไปน้อย:

```csharp
var rowsToRemove = new List<int>();
for (int i = 0; i < table.DataRange.RowCount; i++)
{
    var cell = table.DataRange[i, 2]; // column C (zero‑based)
    if (cell.StringValue == "Obsolete")
        rowsToRemove.Add(i);
}

// Delete rows from bottom to top to keep indices valid
rowsToRemove.Sort((a, b) => b.CompareTo(a));
foreach (int rowIdx in rowsToRemove)
    table.DeleteRows(rowIdx, 1);
```

### What if I need to **preserve formatting**?

`DeleteRows` จะลบแถวทั้งหมดจากตารางแต่จะรักษาสไตล์ของตารางสำหรับแถวที่เหลือ หากคุณต้องการเก็บฟอร์แมตเฉพาะของแถวที่กำลังลบ ให้คัดลอกสไตล์ไปยังแถวอื่นก่อนทำการลบ

### Does this work with **.xls** (Excel 97‑2003) files?

ใช่. Aspose.Cells จะตรวจจับรูปแบบไฟล์โดยอัตโนมัติ ดังนั้นโค้ดเดียวกันทำงานได้กับ `.xls` เพียงเปลี่ยนนามสกุลไฟล์ในคอนสตรัคเตอร์ `Workbook`

## Performance tips

* **Batch deletions:** การลบหลายแถวทีละแถวอาจช้าลง ใช้การเรียก `DeleteRows(start, count)` หนึ่งครั้งเมื่อทำได้
* **Avoid UI thread blocking:** หากนำโค้ดนี้ไปใช้ในแอปเดสก์ท็อป ให้ทำการจัดการเวิร์กบุ๊กบนเธรดแบ็กกราวด์เพื่อไม่ให้ UI ค้าง
* **Dispose properly:** แม้ Aspose.Cells จะใช้หน่วยความจำแบบจัดการ แต่ควรห่อ `Workbook` ด้วย `using` หากทำงานกับไฟล์ขนาดใหญ่เพื่อปล่อยทรัพยากรอย่างทันท่วงที

## Conclusion

ตอนนี้คุณมีตัวอย่างที่พร้อมใช้งานในระดับ production เพื่อ **ลบแถวจากตาราง Excel** ด้วย C# คู่มือนี้อธิบายวิธี **load Excel workbook C#**, ค้นหา `ListObject` ที่ต้องการ, ลบแถวอย่างปลอดภัย, และบันทึกไฟล์ที่อัปเดตแล้ว พร้อมคำแนะนำการจัดการ edge‑case และเคล็ดลับประสิทธิภาพ คุณสามารถปรับใช้รูปแบบนี้กับสถานการณ์ที่ซับซ้อนยิ่งขึ้น เช่น การลบตามเงื่อนไข, ตารางหลายตาราง, หรือไลบรารี Excel .NET อื่น ๆ

### Next steps

* สำรวจ **ClosedXML** หรือ **EPPlus** หากคุณต้องการสแตกแบบโอเพ่นซอร์สเต็มรูปแบบ
* ผสานการลบแถวกับ **data validation** เพื่อทำความสะอาดสเปรดชีตก่อนนำเข้าไปยังฐานข้อมูล
* อัตโนมัติกระบวนการสำหรับโฟลเดอร์ของเวิร์กบุ๊กโดยใช้ `Directory.GetFiles` และลูป

ลองทดลองเปลี่ยนช่วงแถว, ชื่อตาราง, และตรรกะเงื่อนไขต่าง ๆ ได้เลย Happy coding!

## What Should You Learn Next?

บทเรียนต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งรวมตัวอย่างโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายขั้นตอนเพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจวิธีการทำงานทางเลือกในโปรเจกต์ของคุณ

- [โหลดไฟล์ Excel C# – วิธีลบแถวและลบแถวเฉพาะ](/cells/english/net/row-and-column-management/load-excel-file-c-how-to-delete-rows-and-remove-specific-row/)
- [วิธีแทรกและลบแถวใน Excel ด้วย Aspose.Cells สำหรับ .NET: คู่มือฉบับสมบูรณ์](/cells/english/net/data-manipulation/aspose-cells-net-insert-delete-excel-rows/)
- [วิธีลบแถวว่างใน Excel ด้วย Aspose.Cells .NET สำหรับการทำความสะอาดข้อมูล](/cells/english/net/data-manipulation/delete-blank-rows-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}