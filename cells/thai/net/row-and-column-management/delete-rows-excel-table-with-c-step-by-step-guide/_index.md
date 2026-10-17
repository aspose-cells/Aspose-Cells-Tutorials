---
category: general
date: 2026-02-28
description: ลบแถวในตาราง Excel ด้วย C# อย่างรวดเร็ว. เรียนรู้วิธีเพิ่ม named range
  ใน Excel, เข้าถึง worksheet ด้วยชื่อ, และหลีกเลี่ยงข้อผิดพลาดชื่อซ้ำ.
draft: false
keywords:
- delete rows excel table
- add named range excel
- access worksheet by name
- how to add defined name
- named range on another sheet
language: th
og_description: ลบแถวในตาราง Excel ด้วย C# . บทเรียนนี้ยังแสดงวิธีเพิ่ม Named Range
  ใน Excel และเข้าถึง Worksheet ตามชื่อ.
og_title: ลบแถวในตาราง Excel ด้วย C# – คู่มือฉบับสมบูรณ์
tags:
- C#
- Excel
- DevExpress Spreadsheet
title: ลบแถวในตาราง Excel ด้วย C# – คู่มือขั้นตอนโดยละเอียด
url: /th/net/row-and-column-management/delete-rows-excel-table-with-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ลบแถวในตาราง Excel ด้วย C# – การสอนโปรแกรมเต็มรูปแบบ

เคยต้อง **delete rows excel table** จาก workbook แต่ไม่แน่ใจว่าจะใช้ API ใด? คุณไม่ได้เป็นคนเดียว—นักพัฒนาส่วนใหญ่เจออุปสรรคเดียวกันเมื่อต้องการตัดตารางโดยโปรแกรม  

ในบทความนี้เราจะเดินผ่านตัวอย่างเต็มที่สามารถรันได้ ซึ่งไม่เพียงลบแถวจากตาราง Excel เท่านั้น แต่ยังแสดง **วิธีเพิ่ม defined name** (หรือ *named range*), **วิธีเข้าถึง worksheet ด้วยชื่อ**, และทำไมการเพิ่มชื่อซ้ำบนชีตอื่นจึงทำให้เกิด `InvalidOperationException`  

เมื่ออ่านจบคุณจะสามารถ:

* ดึง worksheet ด้วยชื่อแท็บของมัน  
* ลบแถวข้อมูลจากตารางแรกบนชีตนั้นอย่างปลอดภัย  
* สร้าง named range ที่ชี้ไปยังที่อยู่เฉพาะ  
* เข้าใจปัญหาชื่อซ้ำระหว่างชีตต่าง ๆ  

ไม่ต้องอ้างอิงเอกสารภายนอก—ทุกอย่างที่คุณต้องการอยู่ที่นี่

---

## สิ่งที่คุณต้องเตรียม

* **DevExpress Spreadsheet** (หรือไลบรารีใด ๆ ที่ให้ `Workbook`, `Worksheet`, `ListObject` และ `Names`)  
* โปรเจกต์ .NET ที่เป้าหมาย **.NET 6** หรือใหม่กว่า (โค้ดนี้ยังคอมไพล์ได้กับ .NET Framework 4.8)  
* ความคุ้นเคยพื้นฐานกับ C#—ถ้าคุณเขียน `foreach` loop ได้ก็พร้อมแล้ว  

> **Pro tip:** หากคุณใช้ Community Edition ฟรีของ DevExpress, API ที่ใช้ด้านล่างเหมือนกับเวอร์ชันเชิงพาณิชย์

---

## ขั้นตอนที่ 1 – Access Worksheet by Name

สิ่งแรกที่ต้องทำคือหาชีตที่มีตารางที่ต้องการแก้ไข  
นักพัฒนาส่วนใหญ่มักใช้ `Worksheets[0]` ตามนิสัย แต่วิธีนี้ทำให้โค้ดผูกติดกับลำดับชีตและจะพังเมื่อมีการเปลี่ยนชื่อแท็บ

```csharp
using DevExpress.Spreadsheet;

// Assume 'workbook' is an already‑loaded Workbook instance
Worksheet worksheet = workbook.Worksheets["Sheet1"];   // <-- access worksheet by name
```

*ทำไมเรื่องนี้ถึงสำคัญ:* การใช้ **ชื่อ** ของชีตแทนการอ้างอิงด้วยดัชนีช่วยหลีกเลี่ยงการแก้ไขผิดชีตเมื่อ workbook มีการเปลี่ยนแปลง  

หากชื่อที่ระบุไม่มีอยู่ใน workbook ไลบรารีจะโยน `KeyNotFoundException` ซึ่งคุณสามารถจับเพื่อแสดงข้อความข้อผิดพลาดที่เป็นมิตรได้

---

## ขั้นตอนที่ 2 – Delete Rows Excel Table (The Safe Way)

เมื่อได้ worksheet ที่ถูกต้องแล้ว เรามาลบแถวข้อมูลจากตารางแรกกัน  
ข้อผิดพลาดทั่วไปคือการเรียก `DeleteRows(1, rowCount‑1)` เนื่องจากตั้งแต่ **DevExpress 22.2** overload นี้ถูก **ห้ามใช้** และจะโยน `InvalidOperationException` ไลบรารีต้องการให้คุณลบแถว **ภายในช่วงข้อมูลของตาราง** ไม่ใช่แถวหัวตาราง

```csharp
// Grab the first table (ListObject) on the sheet
var table = worksheet.ListObjects[0];

// Calculate how many data rows we actually have (excluding the header)
int dataRowCount = table.DataRange.RowCount;

// Delete only the data rows – keep the header intact
if (dataRowCount > 0)
{
    // DeleteRows(startRow, rowCount) – startRow is zero‑based within the table
    table.DeleteRows(0, dataRowCount);
}
```

> **ถ้าตารางว่างเปล่าเป็นอย่างไร?** เงื่อนไข `if` ป้องกันการเรียกด้วย `rowCount = 0` ซึ่งจะทำให้เกิดข้อยกเว้น

### ภาพรวมแบบภาพ  

![delete rows excel table example](image.png "Screenshot showing rows being removed from an Excel table")  

*Alt text: ตัวอย่างการลบแถวในตาราง Excel ด้วยโค้ด C#*

---

## ขั้นตอนที่ 3 – How to Add Defined Name (Create a Named Range)

หลังจากทำความสะอาดตารางแล้ว คุณอาจต้องการอ้างอิงช่วงเฉพาะในภายหลัง—เช่นสำหรับแผนภูมิหรือรายการตรวจสอบข้อมูล นั่นคือจุดที่ **add named range excel** เข้ามาช่วย

```csharp
// Define a name that points to A1:C5 on Sheet1
workbook.Names.Add("MyTable", "Sheet1!$A$1:$C$5");

// Verify that the name exists
Name definedName = workbook.Names["MyTable"];
Console.WriteLine($"Defined name '{definedName.Name}' points to {definedName.RefersTo}");
```

เมธอด `Names.Add` รับพารามิเตอร์สองค่า: ตัวระบุและที่อยู่แบบ A1‑style  
เพราะเราใช้ **access worksheet by name** ก่อนหน้านี้ ที่อยู่สตริงจึงสามารถอ้างอิงชีตใดก็ได้โดยไม่ต้องกังวลเรื่องการเปลี่ยนดัชนี

---

## ขั้นตอนที่ 4 – Named Range on Another Sheet – Avoid Duplicate Name Errors

คุณอาจคิดว่าใช้ตัวระบุเดียวกันบนชีตอื่นได้ เช่นนี้:

```csharp
// Attempt to add the same name on Sheet2 – this will throw
workbook.Names.Add("MyTable", "Sheet2!$A$1:$C$5");
```

แต่จริง ๆ แล้วขอบเขตการตั้งชื่อของ Excel เป็น **ระดับ workbook ทั้งหมด** ไม่ใช่ต่อชีต การเรียกดังกล่าวจะทำให้เกิด `InvalidOperationException` พร้อมข้อความ *“A name with the same identifier already exists.”*  

### วิธีแก้ปัญหา

1. **เลือกชื่อที่ไม่ซ้ำ** (`MyTable_Sheet2`)  
2. **ลบชื่อที่มีอยู่ก่อน** ก่อนที่จะเพิ่มใหม่ (เฉพาะเมื่อคุณต้องการแทนที่จริง ๆ)

```csharp
// Option A – use a unique name
workbook.Names.Add("MyTable_Sheet2", "Sheet2!$A$1:$C$5");

// Option B – replace the existing name (use with caution)
if (workbook.Names.Contains("MyTable"))
    workbook.Names.Remove("MyTable");

workbook.Names.Add("MyTable", "Sheet2!$A$1:$C$5");
```

---

## ตัวอย่างเต็มที่สามารถรันได้

รวมทุกอย่างเข้าด้วยกัน นี่คือแอปคอนโซลที่พร้อมใส่ลง Visual Studio และรันกับไฟล์ `sample.xlsx` ตัวอย่าง

```csharp
using System;
using DevExpress.Spreadsheet;

class Program
{
    static void Main()
    {
        // Load an existing workbook (replace with your file path)
        Workbook workbook = new Workbook();
        workbook.LoadDocument("sample.xlsx");

        // -------------------------------------------------
        // Step 1 – Access the worksheet by its tab name
        // -------------------------------------------------
        Worksheet worksheet = workbook.Worksheets["Sheet1"]; // primary sheet

        // -------------------------------------------------
        // Step 2 – Delete rows excel table (safe method)
        // -------------------------------------------------
        var table = worksheet.ListObjects[0];
        int dataRows = table.DataRange.RowCount;
        if (dataRows > 0)
            table.DeleteRows(0, dataRows); // removes only data rows

        // -------------------------------------------------
        // Step 3 – Add a defined name (named range) on Sheet1
        // -------------------------------------------------
        workbook.Names.Add("MyTable", "Sheet1!$A$1:$C$5");

        // -------------------------------------------------
        // Step 4 – Demonstrate duplicate‑name handling
        // -------------------------------------------------
        try
        {
            workbook.Names.Add("MyTable", "Sheet2!$A$1:$C$5");
        }
        catch (InvalidOperationException ex)
        {
            Console.WriteLine("Duplicate name error: " + ex.Message);
            // Use a unique identifier instead
            workbook.Names.Add("MyTable_Sheet2", "Sheet2!$A$1:$C$5");
        }

        // Save the modified workbook
        workbook.SaveDocument("sample_modified.xlsx");
        Console.WriteLine("Workbook updated successfully.");
    }
}
```

**ผลลัพธ์ที่คาดหวัง**

* แถวข้อมูลทั้งหมดจากตารางแรกบน **Sheet1** จะหายไป เหลือแค่แถวหัวตาราง  
* ชื่อ **MyTable** จะชี้ไปที่ `Sheet1!$A$1:$C$5`  
* ชื่อที่สอง **MyTable_Sheet2** จะอ้างอิงช่วงบน **Sheet2** อย่างปลอดภัยโดยไม่เกิดข้อยกเว้น

---

## คำถามที่พบบ่อย & กรณีขอบ

| Question | Answer |
|----------|--------|
| *What if the workbook has multiple tables?* | ดึง `ListObject` ที่ต้องการโดยใช้ดัชนี (`worksheet.ListObjects[1]`) หรือโดยชื่อ (`worksheet.ListObjects["MyTable"]`) |
| *Can I delete rows from a table that spans multiple worksheets?* | ไม่ได้—ตารางจำกัดอยู่ในชีตเดียว คุณต้องทำซ้ำโลจิกการลบสำหรับแต่ละชีต |
| *Is there a way to delete only a subset of rows?* | มี—ใช้ `table.DeleteRows(startRow, count)` โดย `startRow` เริ่มจากศูนย์ภายในพื้นที่ข้อมูลของตาราง |
| *Do named ranges survive after saving?* | แน่นอน หลังจากเรียก `SaveDocument` ชื่อจะถูกบันทึกเป็นส่วนหนึ่งของ XML ของ workbook |
| *How do I list all defined names in the workbook?* | ใช้ `foreach (var name in workbook.Names) Console.WriteLine(name.Name);` |

---

## สรุป

เราได้ครอบคลุม **delete rows excel table** ด้วย C#, แสดง **add named range excel**, และอธิบายวิธี **access worksheet by name** อย่างถูกต้องพร้อมหลีกเลี่ยงข้อยกเว้นชื่อซ้ำ  

โซลูชันเต็มอยู่ในโค้ดสแนปช็อตด้านบน—คัดลอก, วาง, แล้วรันกับไฟล์ของคุณเอง จากนี้คุณสามารถขยายโลจิกเพื่อจัดการหลายตาราง, คำนวณช่วงแบบไดนามิก, หรือแม้แต่รวมกับ UI  

**ขั้นตอนต่อไป** ที่คุณอาจลอง:

* ใช้ **named range on another sheet** เพื่อขับเคลื่อน series ของแผนภูมิ  
* ผสานโลจิกการลบกับ **ExcelDataReader** เพื่ออ่านข้อมูลก่อนทำความสะอาด  
* อัตโนมัติการอัปเดตเป็นกลุ่มหลาย ๆ workbook ด้วยลูป `foreach (var file in Directory.GetFiles(...))`

มีคำถามเพิ่มเติมเกี่ยวกับการทำงานอัตโนมัติของ Excel ใน C#? แสดงความคิดเห็นได้เลย แล้วเราจะต่อเนื่องกันต่อไป ขอให้สนุกกับการเขียนโค้ด!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}