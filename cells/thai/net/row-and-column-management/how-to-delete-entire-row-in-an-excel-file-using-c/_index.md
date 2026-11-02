---
category: general
date: 2026-10-10
description: เรียนรู้วิธีลบแถวทั้งหมดในเวิร์กบุ๊ก Excel ด้วย C# คู่มือขั้นตอนนี้ยังครอบคลุมวิธีลบแถวตามดัชนีและลบแถวตามดัชนีโดยใช้
  Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- delete entire row
- how to delete row
- remove row by index
- delete row excel
- delete row c#
language: th
lastmod: 2026-10-10
og_description: ลบแถวทั้งหมดในเวิร์กบุ๊ก Excel ด้วย C#. ทำตามคู่มือนี้เพื่อเรียนรู้วิธีลบแถวตามดัชนี,
  ลบแถวตามดัชนี, และบันทึกไฟล์อย่างปลอดภัย.
og_image_alt: Screenshot of an Excel worksheet before and after deleting an entire
  row with C# code
og_title: ลบแถวทั้งหมดใน Excel ด้วย C# – คู่มือการเขียนโปรแกรมครบถ้วน
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Learn how to delete entire row in an Excel workbook with C#. This step‑by‑step
    guide also covers how to delete row by index and remove row by index using Aspose.Cells.
  headline: How to delete entire row in an Excel file using C#
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
title: วิธีลบแถวทั้งหมดในไฟล์ Excel ด้วย C#
url: /th/net/row-and-column-management/how-to-delete-entire-row-in-an-excel-file-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ลบแถวทั้งหมดในไฟล์ Excel ด้วย C#

หากคุณต้องการ **delete entire row** ใน workbook ของ Excel คู่มือฉบับนี้จะแสดงให้คุณเห็นอย่างชัดเจนว่าทำอย่างไรด้วย C# ไม่ว่าคุณจะทำความสะอาดข้อมูลที่นำเข้า หรือสร้างเครื่องมือรายงาน ขั้นตอนต่อไปนี้จะช่วยให้คุณลบแถวตามดัชนีและบันทึกผลลัพธ์โดยไม่สูญเสียข้อมูลอื่น

คุณจะได้เห็นว่าการใช้วิธีเดียวกันนี้ตอบคำถาม **how to delete row** ตามดัชนีอย่างไร, วิธี **remove row by index**, และทำไมวิธีนี้จึงทำงานได้ในสถานการณ์ **delete row excel** ด้วย C#

## ข้อกำหนดเบื้องต้น

* .NET 6.0 หรือใหม่กว่า (โค้ดนี้ทำงานกับ .NET Framework 4.6+ ด้วยเช่นกัน)  
* ไลบรารี **Aspose.Cells for .NET** (สามารถติดตั้งผ่าน NuGet: `Install-Package Aspose.Cells`)  
* ความคุ้นเคยพื้นฐานกับโปรเจกต์คอนโซลหรือเดสก์ท็อปของ C#  

ไม่จำเป็นต้องใช้ Excel interop หรือคอมโพเนนต์ COM เพิ่มเติม ซึ่งทำให้โซลูชันมีน้ำหนักเบาและปลอดภัยสำหรับการทำงานบนเซิร์ฟเวอร์

## ขั้นตอนที่ 1: ตั้งค่าโปรเจกต์และนำเข้า namespace

สร้างแอปพลิเคชันคอนโซลใหม่ (หรือเพิ่มโค้ดในโปรเจกต์ที่มีอยู่) แล้วเพิ่ม `using` directives ที่จำเป็น:

```csharp
using System;
using Aspose.Cells;

namespace ExcelRowDeletion
{
    class Program
    {
        static void Main(string[] args)
        {
            // The rest of the tutorial code lives here.
        }
    }
}
```

*ทำไมเรื่องนี้สำคัญ*: การนำเข้า `Aspose.Cells` จะทำให้คุณเข้าถึง `Workbook`, `Worksheet` และเมธอด `DeleteRows` ที่ทำการลบแถวจริง

## ขั้นตอนที่ 2: โหลด workbook และเลือก worksheet

คุณต้องโหลดไฟล์ต้นทาง (`input.xlsx`) และรับ worksheet ที่ต้องการแก้ไข Worksheet แรกสามารถเข้าถึงได้ด้วยดัชนี `0`.

```csharp
// Load the workbook from disk
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

// Get the first worksheet (you can also use workbook.Worksheets["SheetName"])
Worksheet ws = workbook.Worksheets[0];
```

> **เคล็ดลับ**: หากคุณต้องการทำงานกับชีตเฉพาะ ให้เปลี่ยนดัชนีเป็นชื่อชีต: `workbook.Worksheets["Data"]`.

## ขั้นตอนที่ 3: ลบแถวทั้งหมดโดยใช้ดัชนีเริ่มจากศูนย์

Aspose.Cells ใช้การจัดลำดับดัชนีเริ่มจากศูนย์ ดังนั้นแถวแรกคือ `0` เพื่อทำการลบแถว 5 (แถวที่หกที่แสดง) ให้เรียก `DeleteRows` พร้อมกับ `DeleteOptions.DeleteEntireRow`.

```csharp
// Delete one row starting at index 5 (zero‑based) and remove the whole row
ws.Cells[5, 0].DeleteRows(1, DeleteOptions.DeleteEntireRow);
```

*คำอธิบาย*:

* `ws.Cells[5, 0]` ชี้ไปยังเซลล์แรกของแถวที่คุณต้องการลบ.  
* `DeleteRows(1, DeleteOptions.DeleteEntireRow)` บอก Aspose.Cells ให้ลบ **1** แถว และแฟล็ก `DeleteEntireRow` ทำให้ **แถวทั้งหมด** หายไป พร้อมเลื่อนแถวด้านล่างขึ้นด้านบน.

### วิธีลบแถวตามดัชนีในสถานการณ์อื่น

* **Delete multiple consecutive rows** – เปลี่ยนอาร์กิวเมนต์แรกเป็นจำนวนแถวที่ต้องการลบ:

  ```csharp
  // Remove rows 5, 6 and 7 (three rows total)
  ws.Cells[5, 0].DeleteRows(3, DeleteOptions.DeleteEntireRow);
  ```

* **Delete the last row** – ใช้ `ws.Cells.MaxDataRow` เพื่อรับดัชนีของแถวที่มีข้อมูลล่างสุด:

  ```csharp
  int lastRow = ws.Cells.MaxDataRow;
  ws.Cells[lastRow, 0].DeleteRows(1, DeleteOptions.DeleteEntireRow);
  ```

โค้ดส่วนนั้นตอบความต้องการ **remove row by index** ในขณะที่ทำให้โค้ดอ่านง่าย

## ขั้นตอนที่ 4: บันทึก workbook หลังจากลบแถว

หลังจากการลบ ให้เขียน workbook ที่แก้ไขแล้วกลับไปยังดิสก์ คุณสามารถเขียนทับไฟล์ต้นฉบับหรือสร้างไฟล์ใหม่ได้

```csharp
// Save the workbook to a new file (or overwrite the original)
workbook.Save("YOUR_DIRECTORY/output.xlsx");
```

หากคุณต้องการเก็บไฟล์ต้นฉบับไว้ไม่เปลี่ยนแปลง เพียงเปลี่ยนเส้นทางของไฟล์ผลลัพธ์ เมธอด `Save` รองรับหลายรูปแบบ (`.xls`, `.csv`, `.pdf`, ฯลฯ) – เพียงเปลี่ยนนามสกุลไฟล์

## ตัวอย่างการทำงานเต็มรูปแบบ

เมื่อรวมทุกอย่างเข้าด้วยกัน นี่คือตัวอย่างโปรแกรมที่สมบูรณ์และพร้อมรัน:

```csharp
using System;
using Aspose.Cells;

namespace ExcelRowDeletion
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the workbook
            Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

            // 2️⃣ Select the first worksheet
            Worksheet ws = workbook.Worksheets[0];

            // 3️⃣ Delete the entire row at index 5 (sixth visual row)
            ws.Cells[5, 0].DeleteRows(1, DeleteOptions.DeleteEntireRow);

            // 4️⃣ Save the result
            workbook.Save("YOUR_DIRECTORY/output.xlsx");

            Console.WriteLine("Row deleted successfully. Output saved to output.xlsx");
        }
    }
}
```

**ผลลัพธ์ที่คาดหวัง**: หลังจากรันโปรแกรม `output.xlsx` จะมีแถวทั้งหมดเดิมยกเว้นแถวที่เริ่มที่แถวที่ 6 (ตามการแสดงผล) ข้อมูลทั้งหมดด้านล่างแถวที่ลบจะเลื่อนขึ้นโดยอัตโนมัติ รักษาสูตรและการจัดรูปแบบไว้

## ข้อผิดพลาดทั่วไปและวิธีหลีกเลี่ยง

| ปัญหา | สาเหตุ | วิธีแก้ |
|-------|--------|--------|
| **Index out of range** | พยายามลบแถวที่ดัชนีไม่มีอยู่ (เช่น `ws.Cells[1000,0]` ในชีตที่มี 200 แถว) | ใช้ `ws.Cells.MaxDataRow` เพื่อตรวจสอบดัชนีสูงสุดที่ถูกต้องก่อนเรียก `DeleteRows`. |
| **Partial row deletion** | การละเว้น `DeleteOptions.DeleteEntireRow` ทำให้เพียงเนื้อหาเซลล์ถูกลบเท่านั้น | ต้องส่ง `DeleteOptions.DeleteEntireRow` เสมอเมื่อคุณต้องการลบแถวทั้งหมด. |
| **Unexpected formula changes** | การลบแถวที่เป็นส่วนหนึ่งของช่วงสูตรอาจทำให้การอ้างอิงเสียหาย | ประเมินสูตรใหม่หลังการลบ (`workbook.CalculateFormula()`) หาก workbook ของคุณพึ่งพาช่วงสูตรแบบไดนามิก. |
| **Saving to a read‑only location** | `Save` จะโยนข้อยกเว้นหากโฟลเดอร์ถูกป้องกัน | ตรวจสอบให้แน่ใจว่าไดเรกทอรีเป้าหมายสามารถเขียนได้หรือรันโปรแกรมด้วยสิทธิ์ที่เหมาะสม. |

การจัดการข้อกังวลเหล่านี้ทำให้โซลูชันมั่นคงสำหรับการใช้งานในผลิตภัณฑ์และตอบสนองต่อคำถาม **delete row excel** และ **delete row c#**

## ขั้นสูง: การลบแถวตามเงื่อนไข

บางครั้งคุณอาจต้องการลบแถวที่ตรงตามเกณฑ์บางอย่าง (เช่น แถวที่คอลัมน์ A ว่าง) ลูปต่อไปนี้แสดงวิธีสแกนจากล่างขึ้นบนอย่างปลอดภัยและลบแถวที่ตรงเงื่อนไข:

```csharp
int lastRow = ws.Cells.MaxDataRow;
for (int row = lastRow; row >= 0; row--)
{
    // Check if column A (index 0) is empty
    if (ws.Cells[row, 0].StringValue == string.Empty)
    {
        ws.Cells[row, 0].DeleteRows(1, DeleteOptions.DeleteEntireRow);
    }
}
workbook.Save("YOUR_DIRECTORY/cleaned.xlsx");
```

การสแกนจากล่างขึ้นบนช่วยป้องกันปัญหาเปลี่ยนดัชนีที่เกิดขึ้นเมื่อทำการลบแถวขณะวนลูปจากบนลงล่าง

## สรุป

คุณตอนนี้รู้วิธี **delete entire row** ใน workbook ของ Excel ด้วย C# แล้ว คู่มือนี้ครอบคลุม:

* การโหลด workbook และการเลือก worksheet  
* การใช้ `DeleteRows` พร้อม `DeleteOptions.DeleteEntireRow` เพื่อ **how to delete row** ตามดัชนี  
* การบันทึกไฟล์ที่แก้ไขอย่างปลอดภัย  
* การจัดการกรณีขอบ, เคล็ดลับประสิทธิภาพ, และตัวอย่างการลบตามเงื่อนไข  

ด้วยความรู้นี้คุณสามารถนำฟังก์ชัน **remove row by index** ไปใช้ได้อย่างมั่นใจ, ทำการทำความสะอาดข้อมูลอัตโนมัติ, และรวมการจัดการ Excel เข้าไปในแอปพลิเคชัน C# ใดก็ได้  

**ขั้นตอนต่อไป**: สำรวจฟีเจอร์อื่นของ Aspose.Cells เช่น การแทรกแถว, การคัดลอกช่วง, หรือการแปลง workbook เป็น PDF—ทั้งหมดนี้อิงจากอ็อบเจ็กต์ `Workbook` และ `Worksheet` ที่คุณเพิ่งเรียนรู้แล้ว ขอให้สนุกกับการเขียนโค้ด!

## คุณควรเรียนรู้อะไรต่อไป?

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งข้อมูลมีตัวอย่างโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายทีละขั้นตอน เพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจวิธีการนำไปใช้แบบอื่นในโปรเจกต์ของคุณ

- [How to Delete an Excel Row Using Aspose.Cells .NET&#58; A Comprehensive Guide](/cells/english/net/worksheet-management/delete-excel-row-aspose-cells-net-tutorial/)
- [Aspose Cells Delete Rows – Protect Header Row in Excel](/cells/english/net/row-and-column-management/aspose-cells-delete-rows-protect-header-row-in-excel/)
- [Efficient Row Management in Excel using Aspose.Cells for Java&#58; Insert and Delete Rows](/cells/english/java/worksheet-management/aspose-cells-java-row-operations-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}