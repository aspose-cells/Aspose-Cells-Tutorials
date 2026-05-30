---
category: general
date: 2026-05-30
description: วิธีใช้ AutoFilter ในการทำงานอัตโนมัติของ Excel ด้วย C# เรียนรู้วิธีสร้างเวิร์กบุ๊ก
  Excel, กรองแถวตามค่า, และทำให้งานสเปรดชีตของคุณเป็นระเบียบและมีประสิทธิภาพมากขึ้น.
draft: false
keywords:
- how to use autofilter
- create excel workbook
- filter rows by value
- filter column b
- excel automation c#
language: th
og_description: วิธีใช้ AutoFilter ในการทำงานอัตโนมัติของ Excel ด้วย C# เชี่ยวชาญการสร้างไฟล์
  Excel, การกรองแถวตามค่า, และการทำงานอัตโนมัติของสเปรดชีตอย่างง่ายดาย.
og_title: วิธีใช้ AutoFilter ในการทำอัตโนมัติ Excel ด้วย C# – คู่มือฉบับสมบูรณ์
schemas:
- author: Aspose
  dateModified: '2026-05-30'
  description: How to use AutoFilter in C# Excel automation. Learn how to create Excel
    workbook, filter rows by value, and streamline your spreadsheet tasks.
  headline: How to Use AutoFilter in C# Excel Automation – Full Step‑by‑Step Guide
  type: TechArticle
- description: How to use AutoFilter in C# Excel automation. Learn how to create Excel
    workbook, filter rows by value, and streamline your spreadsheet tasks.
  name: How to Use AutoFilter in C# Excel Automation – Full Step‑by‑Step Guide
  steps:
  - name: '**Creating the workbook** – `new Workbook()` gives you a clean file; `Worksheets[0]`
      grabs the default sheet.'
    text: '**Creating the workbook** – `new Workbook()` gives you a clean file; `Worksheets[0]`
      grabs the default sheet.'
  - name: '**Filling sample data** – We write a tiny dataset so you can see the filter
      in action.'
    text: '**Filling sample data** – We write a tiny dataset so you can see the filter
      in action.'
  - name: '**Adding a table** – `ListObjects.Add` converts the range into an Excel
      table, which automatically supports filtering and styling.'
    text: '**Adding a table** – `ListObjects.Add` converts the range into an Excel
      table, which automatically supports filtering and styling.'
  - name: '**Applying AutoFilter** – `table.AutoFilter.Filter(1, "Apple")` tells the
      engine: “Show only rows where the second column (B) equals *Apple*.”'
    text: '**Applying AutoFilter** – `table.AutoFilter.Filter(1, "Apple")` tells the
      engine: “Show only rows where the second column (B) equals *Apple*.”'
  - name: '**Saving files** – Two files are written: one filtered, one with the filter
      removed, proving that `RemoveAutoFilter()` works as expected.'
    text: '**Saving files** – Two files are written: one filtered, one with the filter
      removed, proving that `RemoveAutoFilter()` works as expected.'
  type: HowTo
- questions:
  - answer: Yes. Aspose.Cells can save to both `.xlsx` and `.xls` by changing the
      file extension or using `SaveOptions`.
    question: Does this work with older .xls files?
  - answer: Load the file with `new Workbook("path.xlsx")`, apply the filter, then
      `Save` again.
    question: What if I need to filter *after* the workbook is already saved?
  - answer: 'Absolutely. Use `worksheet.AutoFilter.Range = "A1:C5";` and then `worksheet.AutoFilter.ApplyFilter();`.
      However, tables give you built‑in styling and easier column referencing. ---
      ## Image – Visual Confirmation ![Screenshot showing AutoFilter applied to column
      B in an Excel workbook created with C#'
    question: Can I apply a filter to a *range* that isn’t a table?
  type: FAQPage
tags:
- C#
- Excel
- Automation
title: วิธีใช้ AutoFilter ในการทำอัตโนมัติ Excel ด้วย C# – คู่มือเต็มขั้นตอนโดยละเอียด
url: /th/net/excel-autofilter-validation/how-to-use-autofilter-in-c-excel-automation-full-step-by-ste/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีใช้ AutoFilter ในการทำอัตโนมัติ Excel ด้วย C# – คู่มือฉบับสมบูรณ์

เคยสงสัย **วิธีใช้ AutoFilter** เมื่อต้องสร้างไฟล์ Excel จากโค้ด C# หรือไม่? คุณไม่ได้เป็นคนเดียว—นักพัฒนาหลายคนเจอปัญหานี้เมื่อต้องซ่อนแถวที่ไม่ตรงกับเงื่อนไขบางอย่าง.  

ในบทเรียนนี้เราจะเดินผ่านตัวอย่างที่เป็นรูปธรรมและสามารถรันได้ ซึ่ง **สร้าง Excel workbook**, เพิ่มตาราง, แล้ว **กรองแถวตามค่า** ในคอลัมน์ B. เมื่อจบคุณจะได้สแนปช็อตที่สะอาดและนำกลับมาใช้ใหม่ได้ในโปรเจกต์ C# ใด ๆ ที่ต้องการการทำอัตโนมัติ Excel.

## สิ่งที่คุณจะได้เรียนรู้

- ตั้งค่าโปรเจกต์ C# พร้อมไลบรารี Aspose.Cells (หรือ Microsoft.Office.Interop)  
- **Create Excel workbook** ด้วยโปรแกรมและเพิ่มตารางที่มีสไตล์  
- ใช้ **AutoFilter** เพื่อแสดงเฉพาะแถวที่ **column B** มีค่าเท่ากับสตริงที่กำหนด  
- ลบฟิลเตอร์ทั้งหมดเพื่อคืนข้อมูลเต็มชุด  
- เคล็ดลับการจัดการกรณีขอบเช่นคอลัมน์หายหรือหลายเงื่อนไขการกรอง

ไม่จำเป็นต้องมีประสบการณ์ Excel‑VBA มาก่อน; เพียงแค่มีพื้นฐาน C# และแพ็กเกจ NuGet.

---

## ข้อกำหนดเบื้องต้น

| ข้อกำหนด | เหตุผลที่สำคัญ |
|-------------|----------------|
| .NET 6.0 or later (or .NET Framework 4.7+) | รันไทม์สมัยใหม่ให้ประสิทธิภาพที่ดีกว่าและการจัดการแพ็กเกจที่ง่ายขึ้น. |
| Aspose.Cells for .NET (or Microsoft.Office.Interop.Excel) installed via NuGet | ไลบรารีนี้ให้เราได้อ็อบเจ็กต์ `Workbook`, `Worksheet`, และ `Table` ที่ใช้ในโค้ด. |
| A code editor (Visual Studio, VS Code, Rider, etc.) | คุณจะต้องคอมไพล์และรันตัวอย่างนี้. |
| Basic C# knowledge | บทเรียนอธิบาย *เหตุผล* ที่แต่ละบรรทัดมีอยู่ ไม่ใช่แค่ *ทำอะไร* |

You can install Aspose.Cells with:

```bash
dotnet add package Aspose.Cells
```

---

## วิธีใช้ AutoFilter กับ Aspose.Cells ใน C#

Below is the full, self‑contained program. Save it as `Program.cs` in a console project and run – you’ll get `FilteredWorkbook.xlsx` in the output folder.

```csharp
using System;
using Aspose.Cells;

namespace ExcelAutoFilterDemo
{
    class Program
    {
        static void Main()
        {
            // -------------------------------------------------
            // Step 1: Create an Excel workbook and grab the first worksheet
            // -------------------------------------------------
            Workbook workbook = new Workbook();               // creates a new, empty workbook
            Worksheet sheet = workbook.Worksheets[0];         // the default sheet is named "Sheet1"

            // Populate the sheet with sample data (A‑C columns, 5 rows)
            sheet.Cells["A1"].PutValue("ID");
            sheet.Cells["B1"].PutValue("Fruit");
            sheet.Cells["C1"].PutValue("Quantity");

            sheet.Cells["A2"].PutValue(1);
            sheet.Cells["B2"].PutValue("Apple");
            sheet.Cells["C2"].PutValue(10);

            sheet.Cells["A3"].PutValue(2);
            sheet.Cells["B3"].PutValue("Banana");
            sheet.Cells["C3"].PutValue(15);

            sheet.Cells["A4"].PutValue(3);
            sheet.Cells["B4"].PutValue("Apple");
            sheet.Cells["C4"].PutValue(7);

            sheet.Cells["A5"].PutValue(4);
            sheet.Cells["B5"].PutValue("Cherry");
            sheet.Cells["C5"].PutValue(20);

            // -------------------------------------------------
            // Step 2: Convert the range into a ListObject (Excel table)
            // -------------------------------------------------
            // Parameters: firstRow, firstColumn, totalRows, totalColumns, hasHeaders
            int tableIdx = sheet.ListObjects.Add(0, 0, 5, 3, true);
            ListObject table = sheet.ListObjects[tableIdx];
            table.TableStyleType = TableStyleType.TableStyleMedium2; // nice built‑in styling

            // -------------------------------------------------
            // Step 3: Apply an AutoFilter to show only rows where column B = "Apple"
            // -------------------------------------------------
            // The AutoFilter is attached to the table’s range automatically.
            // We target column B (index 1) and set the criteria.
            table.AutoFilter.Filter(1, "Apple"); // 1 = zero‑based column index for B

            // -------------------------------------------------
            // Step 4: Save the filtered workbook to disk
            // -------------------------------------------------
            workbook.Save("FilteredWorkbook.xlsx");

            // -------------------------------------------------
            // Step 5: (Optional) Remove the AutoFilter completely
            // -------------------------------------------------
            // This demonstrates that you can revert to the full dataset without re‑loading.
            table.RemoveAutoFilter();   // clears the filter
            workbook.Save("UnfilteredWorkbook.xlsx");

            Console.WriteLine("Workbook created and filtered successfully.");
        }
    }
}
```

### วิธีการทำงานของโค้ด

1. **Creating the workbook** – `new Workbook()` ให้ไฟล์เปล่า; `Worksheets[0]` ดึงชีตเริ่มต้น.  
2. **Filling sample data** – เราเขียนชุดข้อมูลขนาดเล็กเพื่อให้คุณเห็นการทำงานของฟิลเตอร์.  
3. **Adding a table** – `ListObjects.Add` แปลงช่วงให้เป็นตาราง Excel ซึ่งรองรับการกรองและสไตล์โดยอัตโนมัติ.  
4. **Applying AutoFilter** – `table.AutoFilter.Filter(1, "Apple")` บอกเอ็นจิ้นว่า: “แสดงเฉพาะแถวที่คอลัมน์ที่สอง (B) มีค่าเท่ากับ *Apple*.”  
5. **Saving files** – เขียนไฟล์สองไฟล์: หนึ่งไฟล์ที่มีฟิลเตอร์, อีกหนึ่งไฟล์ที่ลบฟิลเตอร์แล้ว, เพื่อพิสูจน์ว่า `RemoveAutoFilter()` ทำงานตามที่คาด.

> **Pro tip:** หากต้องการกรองด้วยหลายเงื่อนไข (เช่น “Apple” *or* “Banana”) ให้ใช้ overload `Filter(int columnIndex, string criteria1, string criteria2)` หรือส่งอาร์เรย์ของสตริง.

---

## การกรองแถวตามค่า – รูปแบบทั่วไป

แม้ว่าตัวอย่างข้างต้นจะเน้นที่ **filter column B** คุณอาจต้องการกรองคอลัมน์อื่นหรือใช้เงื่อนไขเชิงตัวเลข นี่คือชีทสรุปเร็ว:

| ตัวกรองที่ต้องการ | โค้ดตัวอย่าง |
|----------------|--------------|
| ตรงข้อความในคอลัมน์ C | `table.AutoFilter.Filter(2, "Cherry");` |
| ตัวเลขมากกว่า 10 ในคอลัมน์ C | `table.AutoFilter.CustomFilter(2, "10", OperatorType.GreaterThan);` |
| หลายค่าในคอลัมน์ B | `table.AutoFilter.Filter(1, new[] { "Apple", "Banana" });` |

**Edge case:** หากหัวคอลัมน์สะกดผิดหรือดัชนีคอลัมน์อยู่นอกช่วง, Aspose.Cells จะโยน `ArgumentException`. ป้องกันโดยตรวจสอบ `table.ListColumns.Count` ก่อนทำการกรอง.

---

## การลบ AutoFilter – เมื่อใดควรรีเซ็ต

บางครั้งคุณต้องการแสดงข้อมูลเต็มชุดอีกครั้ง (เช่น หลังจากผู้ใช้ลบข้อความค้นหา). การเรียก `table.RemoveAutoFilter()` ทำได้ในบรรทัดเดียว. หากใช้ Microsoft.Office.Interop แทน, คุณจะเรียก `worksheet.AutoFilterMode = false;`.

---

## สรุปตัวอย่างทำงานเต็ม

Below is the *entire* program again, stripped of comments for those who prefer a concise view:

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];

        ws.Cells["A1"].PutValue("ID");
        ws.Cells["B1"].PutValue("Fruit");
        ws.Cells["C1"].PutValue("Quantity");

        ws.Cells["A2"].PutValue(1); ws.Cells["B2"].PutValue("Apple");  ws.Cells["C2"].PutValue(10);
        ws.Cells["A3"].PutValue(2); ws.Cells["B3"].PutValue("Banana"); ws.Cells["C3"].PutValue(15);
        ws.Cells["A4"].PutValue(3); ws.Cells["B4"].PutValue("Apple");  ws.Cells["C4"].PutValue(7);
        ws.Cells["A5"].PutValue(4); ws.Cells["B5"].PutValue("Cherry"); ws.Cells["C5"].PutValue(20);

        int idx = ws.ListObjects.Add(0, 0, 5, 3, true);
        ListObject tbl = ws.ListObjects[idx];
        tbl.TableStyleType = TableStyleType.TableStyleMedium2;

        tbl.AutoFilter.Filter(1, "Apple");
        wb.Save("FilteredWorkbook.xlsx");

        tbl.RemoveAutoFilter();
        wb.Save("UnfilteredWorkbook.xlsx");
    }
}
```

Running this yields two files:

- **FilteredWorkbook.xlsx** – เฉพาะแถวที่มี *Apple* ปรากฏ.  
- **UnfilteredWorkbook.xlsx** – ข้อมูลต้นฉบับถูกคืนค่า.

---

## คำถามที่พบบ่อย

**Q: Does this work with older .xls files?**  
A: Yes. Aspose.Cells can save to both `.xlsx` and `.xls` by changing the file extension or using `SaveOptions`.

**Q: What if I need to filter *after* the workbook is already saved?**  
A: Load the file with `new Workbook("path.xlsx")`, apply the filter, then `Save` again.

**Q: Can I apply a filter to a *range* that isn’t a table?**  
A: Absolutely. Use `worksheet.AutoFilter.Range = "A1:C5";` and then `worksheet.AutoFilter.ApplyFilter();`. However, tables give you built‑in styling and easier column referencing.

---

## รูปภาพ – การยืนยันด้วยภาพ

![ภาพหน้าจอแสดง AutoFilter ที่ใช้กับคอลัมน์ B ในไฟล์ Excel ที่สร้างด้วย C#](/images/autofilter-column-b.png "AutoFilter บนคอลัมน์ B")

*(ภาพนี้แสดงมุมมองที่กรองแล้วซึ่งมีเพียงแถวที่มี “Apple” เท่านั้นที่เหลืออยู่.)*

---

## สรุป

เราเพิ่งครอบคลุม **วิธีใช้ AutoFilter** ในสถานการณ์การทำอัตโนมัติ Excel ด้วย C# ตั้งแต่ **การสร้าง Excel workbook** ไปจนถึง **การกรองแถวตามค่า** ใน **column B**, และสุดท้าย **การลบฟิลเตอร์** เมื่อไม่ต้องการอีกต่อไป. ขั้นตอนหลัก—เริ่มต้น, เพิ่มตาราง, ใช้ฟิลเตอร์, และทำความสะอาด—สามารถนำกลับมาใช้ใหม่ได้ในทุกโปรเจกต์ที่ต้องการ **excel automation c#**.

พร้อมสำหรับความท้าทายต่อไป? ลอง:

- เพิ่ม conditional formatting เพื่อไฮไลท์แถวที่กรอง.  
- ส่งออกข้อมูลที่กรองเป็น CSV เพื่อการประมวลผลต่อไป.  
- รวมหลายฟิลเตอร์ (เช่น “Apple” *and* quantity > 8).

ทดลอง, ทำให้พัง, แล้วแก้ไขมัน—

## สิ่งที่คุณควรเรียนต่อไป

- [วิธีทำ Implement AutoFilter ใน Excel ด้วย Aspose.Cells สำหรับ .NET (คู่มือการวิเคราะห์ข้อมูล)](/cells/english/net/data-analysis/implement-autofilter-excel-aspose-cells-dotnet/)
- [วิธีใช้ Autofilter Not Contains ใน Aspose.Cells .NET สำหรับการวิเคราะห์ข้อมูล Excel](/cells/english/net/data-analysis/master-autofilter-not-contains-aspose-cells-net/)
- [วิธีทำ Implement Excel Autofilter 'EndsWith' ด้วย Aspose.Cells สำหรับ .NET](/cells/english/net/data-analysis/implement-autofilter-endswith-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}