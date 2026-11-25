---
category: general
date: 2026-11-25
description: เรียนรู้วิธีลบแถวจากตาราง Excel ด้วย C# และลบหลายแถวจากแผ่นงาน Excel
  อย่างมีประสิทธิภาพ
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- delete rows from excel table
- delete multiple rows from excel sheet
language: th
lastmod: 2026-11-25
og_description: ลบแถวจากตาราง Excel ด้วย C# และเรียนรู้การลบหลายแถวจากแผ่นงาน Excel
  ด้วยโค้ดที่สะอาด
og_image_alt: Screenshot of C# code deleting rows from an Excel table
og_title: ลบแถวจากตาราง Excel ด้วย C# – คู่มือเต็ม
schemas:
- author: Aspose
  dateModified: '2026-11-25'
  description: Learn how to delete rows from Excel table in C# and also delete multiple
    rows from Excel sheet efficiently.
  headline: How to delete rows from Excel table with C#
  type: TechArticle
- description: Learn how to delete rows from Excel table in C# and also delete multiple
    rows from Excel sheet efficiently.
  name: How to delete rows from Excel table with C#
  steps:
  - name: Add Aspose.Cells to your project
    text: 'Open the **Package Manager Console** and run:'
  - name: Load the workbook and locate the table
    text: '```csharp using Aspose.Cells;'
  - name: Delete the desired data rows
    text: The `DeleteRows` method expects a **zero‑based** row index relative to the
      table, **including** the header row. Because the header cannot be removed, you
      must start at index 1 for the first data row.
  - name: Save the modified workbook
    text: '```csharp // Save the workbook to a new file to preserve the original workbook.Save(@"C:\Data\table_with_header_modified.xlsx");
      } } ```'
  - name: Full working example
    text: '```csharp using Aspose.Cells;'
  - name: Edge cases and best practices
    text: '| Situation | Recommended handling | |----------------------------------------|----------------------|
      | Deleting rows beyond the last row | Check `worksheet.Rows.Count` before calling
      `RemoveAt`. | | Removing all rows except the header | Delete data rows in a
      loop or use `DeleteRows(1, table.DataRa'
  type: HowTo
tags:
- Excel automation
- C#
- Aspose.Cells
- data manipulation
title: วิธีลบแถวจากตาราง Excel ด้วย C#
url: /th/net/row-and-column-management/how-to-delete-rows-from-excel-table-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีลบแถวจากตาราง Excel ด้วย C#

หากคุณต้องการลบแถวจากตาราง Excel ด้วย C# คู่มือนี้จะแสดงให้คุณเห็นอย่างชัดเจนว่าต้องทำอย่างไร คุณยังจะได้เห็นวิธีลบหลายแถวจากแผ่นงาน Excel โดยไม่กระทบข้อมูลอื่น

การทำงานกับ Excel อย่างโปรแกรมมิ่งมักต้องการการลบบันทึกที่ล้าสมัยหรือไม่ถูกต้อง การลบแถวโดยตรงในแผ่นงานอาจเสี่ยงเพราะแถวหัวตารางของตารางที่มีโครงสร้างต้องคงอยู่ การสอนนี้จะพาคุณผ่านวิธีที่ปลอดภัยซึ่งเคารพหัวตารางและให้คุณลบแถวข้อมูลจำนวนใดก็ได้ในหนึ่งคำสั่ง

## ข้อกำหนดเบื้องต้น

* .NET 6.0 หรือใหม่กว่า ติดตั้งแล้ว  
* Visual Studio 2022 (หรือ IDE ที่เข้ากันได้)  
* แพคเกจ NuGet **Aspose.Cells** (เวอร์ชัน 23.10 หรือใหม่กว่า) – ไลบรารีนี้ให้คลาส `Workbook`, `Worksheet`, และ `ListObject` ที่ใช้ในตัวอย่าง  

คุณไม่จำเป็นต้องติดตั้ง Microsoft Office บนเครื่องพัฒนา เพราะ Aspose.Cells ทำงานกับรูปแบบไฟล์โดยตรง

## ลบแถวจากตาราง Excel – ทีละขั้นตอน

ส่วนต่อไปนี้อธิบายแต่ละขั้นตอนที่จำเป็นในการลบแถวจากตาราง Excel อย่างปลอดภัย คำหลักหลักปรากฏในหัวข้อนี้เพื่อให้เป็นไปตามข้อกำหนด SEO

### ขั้นตอน 1: เพิ่ม Aspose.Cells ไปยังโปรเจคของคุณ

เปิด **Package Manager Console** แล้วรัน:

```powershell
Install-Package Aspose.Cells
```

แพคเกจจะเพิ่ม assembly ที่จำเป็นและทำให้ชนิด `Workbook`, `Worksheet`, และ `ListObject` พร้อมใช้งาน

### ขั้นตอน 2: โหลดเวิร์กบุ๊กและค้นหาตาราง

```csharp
using Aspose.Cells;

class ExcelRowDeletion
{
    static void Main()
    {
        // Load the workbook that contains the table
        var workbook = new Workbook(@"C:\Data\table_with_header.xlsx");

        // Access the first worksheet (index 0)
        var worksheet = workbook.Worksheets[0];

        // Retrieve the first ListObject (structured table) on the sheet
        var table = worksheet.ListObjects[0];
```

*ทำไมเรื่องนี้สำคัญ*: `ListObject` แทนตาราง Excel ที่แท้จริง ซึ่งรักษาแถวหัวของตนเองไว้ การทำงานกับ `ListObject` จะช่วยหลีกเลี่ยงการลบหัวโดยบังเอิญ

### ขั้นตอน 3: ลบแถวข้อมูลที่ต้องการ

เมธอด `DeleteRows` ต้องการดัชนีแถวแบบ **ศูนย์‑ฐาน** (zero‑based) ที่สัมพันธ์กับตาราง **รวมถึง** แถวหัวด้วย เนื่องจากหัวไม่สามารถลบได้ คุณต้องเริ่มที่ดัชนี 1 สำหรับแถวข้อมูลแถวแรก

```csharp
        // Delete two data rows starting after the header (index 1)
        // Parameters: startRow (relative to the table), numberOfRows
        table.DeleteRows(1, 2);
```

หากคุณลองเรียก `table.DeleteRows(0, 2)` Aspose.Cells จะโยนข้อยกเว้นเพราะแถวหัว (ดัชนี 0) ถูกป้องกัน การเริ่มที่ดัชนี 1 จะทำให้ลบเฉพาะแถวข้อมูลเท่านั้น

### ขั้นตอน 4: บันทึกเวิร์กบุ๊กที่แก้ไขแล้ว

```csharp
        // Save the workbook to a new file to preserve the original
        workbook.Save(@"C:\Data\table_with_header_modified.xlsx");
    }
}
```

การรันโปรแกรมจะลบสองแถวที่อยู่ถัดจากหัวโดยคงโครงสร้างตารางไว้ไม่เปลี่ยนแปลง

### ตัวอย่างทำงานเต็มรูปแบบ

```csharp
using Aspose.Cells;

class ExcelRowDeletion
{
    static void Main()
    {
        // 1. Load workbook
        var workbook = new Workbook(@"C:\Data\table_with_header.xlsx");

        // 2. Access first worksheet
        var worksheet = workbook.Worksheets[0];

        // 3. Get the first table (ListObject)
        var table = worksheet.ListObjects[0];

        // 4. Delete two rows after the header (cannot delete header itself)
        table.DeleteRows(1, 2);

        // 5. Save the result
        workbook.Save(@"C:\Data\table_with_header_modified.xlsx");
    }
}
```

**ผลลัพธ์ที่คาดหวัง**: ไฟล์ `table_with_header_modified.xlsx` มีหัวตารางเดิมตามด้วยแถวทั้งหมด ยกเว้นสองแถวที่ถูกลบ ไม่ได้มีการเปลี่ยนแปลงแผ่นงานอื่น

## ลบหลายแถวจากแผ่นงาน Excel

บางครั้งคุณอาจต้องการลบแถวที่ **ไม่** อยู่ในตารางที่มีโครงสร้าง คำหลักรองปรากฏในหัวข้อนี้ วิธีการจะแตกต่างเล็กน้อยเพราะคุณทำงานกับคอลเลกชัน `Rows` ของแผ่นงานแทน `ListObject`

```csharp
using Aspose.Cells;

class SheetRowDeletion
{
    static void Main()
    {
        var workbook = new Workbook(@"C:\Data\plain_sheet.xlsx");
        var worksheet = workbook.Worksheets[0];

        // Delete rows 5 through 9 (inclusive) – zero‑based index
        // The second argument is the count of rows to remove
        worksheet.Rows.RemoveAt(4, 5);

        workbook.Save(@"C:\Data\plain_sheet_modified.xlsx");
    }
}
```

**ทำไมวิธีนี้ถึงได้ผล**: `Rows.RemoveAt(startIndex, count)` จะลบบล็อกแถวต่อเนื่องโดยตรงจากแผ่นงาน ไม่มีการป้องกันหัวจึงสามารถเริ่มที่ดัชนีใดก็ได้ เมธอดนี้มีประสิทธิภาพเพราะอัปเดตโครงสร้างข้อมูลภายในในหนึ่งขั้นตอน ซึ่งเหมาะเมื่อคุณต้องการลบหลายแถวจากแผ่นงาน Excel

### กรณีขอบและแนวทางปฏิบัติที่ดีที่สุด

| Situation                               | Recommended handling |
|----------------------------------------|----------------------|
| Deleting rows beyond the last row      | ตรวจสอบ `worksheet.Rows.Count` ก่อนเรียก `RemoveAt`. |
| Removing all rows except the header    | ลบแถวข้อมูลในลูปหรือใช้ `DeleteRows(1, table.DataRange.RowCount - 1)`. |
| Preserving cell formatting             | การลบผ่าน `ListObject` จะปรับการจัดรูปแบบโดยอัตโนมัติ; สำหรับแผ่นงานดิบให้คัดลอกรูปแบบก่อนลบหากจำเป็น. |
| Large worksheets ( > 10 000 rows)      | ทำการลบในลำดับจากหลังไปหน้าเพื่อหลีกเลี่ยงการเปลี่ยนดัชนี, หรือใช้ `DeleteRows` บนตารางหากทำได้. |

**เคล็ดลับ**: เมื่อคุณต้องการลบแถวตามเงื่อนไข (เช่น แถวที่ค่าคอลัมน์ว่าง) ให้วนผ่าน `DataRange` ของตารางจากหลังไปหน้าและเรียก `DeleteRows` สำหรับแต่ละแถวที่ตรงเงื่อนไข การลบจากหลังจะป้องกันการเบี่ยงเบนของดัชนี

## คำถามที่พบบ่อย

*Does this work with .xlsx files created by Excel 365?*  
ใช่. Aspose.Cells รองรับสเปค Office Open XML เต็มรูปแบบ ดังนั้นโค้ดเดียวกันทำงานกับไฟล์ `.xlsx` สมัยใหม่ใดก็ได้

*What if the workbook contains multiple tables?*  
ดึงตารางที่ต้องการโดยใช้ชื่อ: `var table = worksheet.ListObjects["MyTable"];` แล้วใช้ `DeleteRows` ตามที่แสดง

*Can I delete rows without using a third‑party library?*  
คุณสามารถใช้ Microsoft.Office.Interop.Excel COM interop ได้ แต่ต้องติดตั้ง Excel บนเซิร์ฟเวอร์และมีภาระงาน COM เพิ่มขึ้น Aspose.Cells ให้ทางเลือกที่เบาและปลอดภัยสำหรับเซิร์ฟเวอร์

## สรุป

ตอนนี้คุณรู้วิธีลบแถวจากตาราง Excel อย่างปลอดภัยและวิธีลบหลายแถวจากแผ่นงาน Excel ด้วย C# เทคนิคหลักใช้เมธอด `ListObject.DeleteRows` ซึ่งเคารพหัวตาราง ส่วนเทคนิครองใช้ `Rows.RemoveAt` สำหรับแผ่นงานธรรมดา นำรูปแบบเหล่านี้ไปใช้ทำความสะอาดข้อมูล, อัตโนมัติการสร้างรายงาน, หรือสร้างฟีเจอร์แก้ไขแบบกลุ่มในแอปพลิเคชันของคุณ

**ขั้นตอนต่อไป**

* สำรวจฟีเจอร์อื่นของ Aspose.Cells เช่น การแทรกแถว, คัดลอกสไตล์, หรือการกรองข้อมูล  
* ทดลองทำเช่นเดียวกันด้วย **ClosedXML** หากคุณชอบไลบรารีโอเพนซอร์ส; API คล้ายกันแต่ใช้ `IXLTable` และ `IXLRows`  
* ผสานตรรกะการลบแถวกับ LINQ query เพื่อสร้าง pipeline การทำความสะอาดข้อมูลที่ซับซ้อนยิ่งขึ้น  

ขอให้สนุกกับการเขียนโค้ด!

## คุณควรเรียนรู้อะไรต่อไป?

บทเรียนต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งรวมตัวอย่างโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายทีละขั้นตอนเพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจวิธีการทำงานทางเลือกในโปรเจคของคุณเอง

- [how to delete rows in Excel with C# – protect table header](/cells/english/net/row-and-column-management/how-to-delete-rows-in-excel-with-c-protect-table-header/)
- [How to use Aspose.Cells to delete rows in an Excel table while keeping the](/cells/english/net/row-and-column-management/how-to-use-aspose-cells-to-delete-rows-in-an-excel-table-whi/)
- [Load Excel File C# – How to Delete Rows and Remove Specific Rows](/cells/english/net/row-and-column-management/load-excel-file-c-how-to-delete-rows-and-remove-specific-row/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}