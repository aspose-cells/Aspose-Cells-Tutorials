---
category: general
date: 2026-08-11
description: สร้างแผ่น Excel จาก DataTable ใน C# และส่งออก DataTable ไปยัง Excel พร้อมตั้งชื่อแผ่นอัตโนมัติ
  เรียนรู้วิธีเพิ่มแถวลงใน DataTable และบันทึกเวิร์กบุ๊กเป็นไฟล์ xlsx.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel sheet
- export datatable to excel
- add rows to datatable
- create multiple excel sheets
- save workbook as xlsx
language: th
lastmod: 2026-08-11
og_description: สร้างแผ่นงาน Excel จาก DataTable ใน C# บทเรียนนี้แสดงวิธีส่งออก DataTable
  ไปยัง Excel, เพิ่มแถวใน DataTable, สร้างหลายแผ่นงาน Excel และบันทึกเวิร์กบุ๊กเป็นไฟล์
  xlsx.
og_image_alt: Screenshot of an Excel workbook created from a DataTable with automatically
  renamed sheets
og_title: สร้างแผ่น Excel จาก DataTable ใน C# – คู่มือการเขียนโปรแกรมเต็มรูปแบบ
schemas:
- author: Aspose
  dateModified: '2026-08-11'
  description: Create excel sheet from a DataTable in C# and export datatable to excel
    with automatic sheet naming. Learn how to add rows to datatable and save workbook
    as xlsx.
  headline: Create excel sheet from a DataTable in C# – step‑by‑step guide
  type: TechArticle
tags:
- C#
- Excel automation
- Aspose.Cells
title: สร้างแผ่น Excel จาก DataTable ใน C# – คู่มือขั้นตอนโดยละเอียด
url: /th/net/excel-data-export-retrieval/create-excel-sheet-from-a-datatable-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# สร้างแผ่น Excel จาก DataTable ใน C# – คู่มือขั้นตอนต่อขั้นตอน

หากคุณต้องการ **create excel sheet** จาก `DataTable` ใน C# คู่มือนี้จะแสดงให้คุณเห็นอย่างชัดเจนว่าต้องทำอย่างไร คุณจะได้เห็นวิธี **export datatable to excel**, เพิ่มแถว, จัดการชื่อแผ่นที่ซ้ำกัน, และสุดท้าย **save workbook as xlsx**.

ตัวอย่างนี้ใช้ Aspose.Cells ซึ่งเป็นไลบรารี .NET ที่ใช้กันอย่างกว้างขวางสำหรับการทำงานอัตโนมัติของ Excel แนวคิดเดียวกันสามารถใช้กับไลบรารีอื่นที่รองรับการประมวลผลแบบ SmartMarker ได้เช่นกัน แต่โค้ดด้านล่างทำงานได้ทันทีกับ Aspose.Cells 22.12 หรือใหม่กว่า.

## ข้อกำหนดเบื้องต้น

* ติดตั้ง .NET 6.0 SDK หรือรุ่นที่ใหม่กว่า  
* อ้างอิงไปยังแพ็กเกจ NuGet **Aspose.Cells** (`Install-Package Aspose.Cells`)  
* มีความคุ้นเคยพื้นฐานกับ `DataTable` และแอปพลิเคชันคอนโซล C#  

ข้อกำหนดเหล่านี้ทำให้บทเรียนเป็นอิสระและหลีกเลี่ยงการใช้เครื่องมือภายนอก.

## ขั้นตอนที่ 1: สร้าง DataTable ที่จะถูกส่งออกไปยัง Excel

ขั้นตอนแรกคือการสร้าง `DataTable` ที่สะท้อนข้อมูลที่คุณต้องการในแผ่นงาน ที่นี่เราจะสร้างตารางชื่อ **Sheet1**, เพิ่มคอลัมน์ `Id`, และแทรกสองแถว.

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a DataTable named "Sheet1"
        DataTable dataTable = new DataTable("Sheet1");
        dataTable.Columns.Add("Id", typeof(int));

        // 2️⃣ Add rows to the DataTable
        dataTable.Rows.Add(1);
        dataTable.Rows.Add(2);

        // Subsequent steps are called from here
        ProcessAndSaveWorkbook(dataTable);
    }
```

**ทำไมเรื่องนี้ถึงสำคัญ:**  
`DataTable` เป็นการแสดงข้อมูลแบบตารางในหน่วยความจำที่สะดวก การตั้งชื่อตารางเป็น `"Sheet1"` จะบอก Aspose.Cells ว่าแผ่นใดจะต้องทำการประมวลผล SmartMarkers.

## ขั้นตอนที่ 2: เพิ่มแถวลงใน DataTable (การขยายเพิ่มเติมตามต้องการ)

หากข้อมูลต้นทางของคุณเป็นแบบไดนามิก คุณมักต้องเพิ่มแถวในลูป โค้ดตัวอย่างต่อไปนี้แสดงรูปแบบทั่วไป:

```csharp
        // Example: add rows from a collection
        int[] ids = { 3, 4, 5 };
        foreach (int id in ids)
        {
            dataTable.Rows.Add(id);
        }
```

**เคล็ดลับ:** เมื่อเพิ่มแถวจำนวนมาก ควรพิจารณาปิดการตรวจสอบข้อจำกัด (`dataTable.Constraints.Clear()`) เพื่อเพิ่มประสิทธิภาพ.

## ขั้นตอนที่ 3: กำหนดค่า SmartMarker options เพื่อสร้างหลายแผ่น excel โดยอัตโนมัติ

SmartMarker options ช่วยให้คุณควบคุมวิธีการจัดการชื่อแผ่นที่ซ้ำกัน การตั้งค่า `DetailSheetNewName` เป็น `"Sheet1_{0}"` จะบอก Aspose.Cells ให้เปลี่ยนชื่อแผ่นต่อไปเป็น `Sheet1_1`, `Sheet1_2` เป็นต้น.

```csharp
    private static void ProcessAndSaveWorkbook(DataTable dataTable)
    {
        // 3️⃣ Set SmartMarker options for automatic sheet renaming
        SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions
        {
            // New sheets will be named Sheet1_1, Sheet1_2, etc.
            DetailSheetNewName = "Sheet1_{0}"
        };
```

**ทำไมเรื่องนี้ถึงสำคัญ:**  
เมื่อคุณประมวลผลหลาย `DataTable` ที่มีชื่อเดียวกัน Excel ปกติจะเกิดข้อผิดพลาดเนื่องจากชื่อแผ่นต้องไม่ซ้ำกัน รูปแบบ `DetailSheetNewName` จะกำจัดความขัดแย้งนี้โดยอัตโนมัติ.

## ขั้นตอนที่ 4: ประมวลผล SmartMarkers และ export datatable to excel

ตอนนี้เราจะสร้าง `Workbook` ใหม่, เรียก `ProcessSmartMarkers`, และให้ Aspose.Cells เติมข้อมูลลงในแผ่นงานตาม `DataTable`.

```csharp
        // 4️⃣ Create a workbook and process SmartMarkers
        Workbook workbook = new Workbook();
        workbook.ProcessSmartMarkers(dataTable, smartMarkerOptions);
```

**คำอธิบาย:**  
`ProcessSmartMarkers` จะสแกน workbook เพื่อค้นหา marker เช่น `&=Sheet1!A1` (ไม่ได้แสดงที่นี่) แล้วแทนที่ด้วยข้อมูลจาก `dataTable` เนื่องจากเราเริ่มด้วย workbook ว่างเปล่า Aspose.Cells จะสร้างแผ่นใหม่ที่มีชื่อเดียวกับตารางและเติมข้อมูลด้วยแถวที่เราเพิ่ม.

## ขั้นตอนที่ 5: บันทึก workbook เป็น xlsx

สุดท้ายให้บันทึก workbook ลงดิสก์ด้วยรูปแบบ OpenXML สมัยใหม่ (`.xlsx`). คุณสามารถเปลี่ยนเส้นทางไฟล์ให้เหมาะกับสภาพแวดล้อมของคุณ.

```csharp
        // 5️⃣ Save the workbook as an .xlsx file
        string outputPath = @"YOUR_DIRECTORY\DuplicateSheets.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

**ผลลัพธ์:**  
การรันโปรแกรมจะสร้างไฟล์ Excel ที่มีเนื้อหาดังนี้:

| ชื่อแผ่น | แถว |
|------------|------|
| Sheet1     | 1, 2, 3, 4, 5 |
| Sheet1_1   | (หากมี DataTable อื่นที่มีชื่อเดียวกันถูกประมวลผล) |

ตรรกะการเปลี่ยนชื่อแผ่นทำให้ **create multiple excel sheets** ได้โดยไม่ต้องจัดการชื่อด้วยตนเอง.

## ความแตกต่างทั่วไปและกรณีขอบ

| สถานการณ์ | วิธีจัดการ |
|-----------|------------|
| **ตารางขนาดใหญ่มาก** (≥ 100 000 แถว) | ใช้ `WorkbookSettings.MemorySetting = MemorySetting.MemoryOptimized` ก่อนทำการประมวลผลเพื่อรักษาการใช้หน่วยความจำให้ต่ำ. |
| **ลำดับคอลัมน์ที่กำหนดเอง** | จัดลำดับใหม่ของอ็อบเจ็กต์ `DataColumn` ใน `DataTable` ก่อนเรียก `ProcessSmartMarkers`. |
| **หลาย DataTable ที่มีชื่อแตกต่างกัน** | เรียก `ProcessSmartMarkers` สำหรับแต่ละตาราง; Aspose.Cells จะสร้างแผ่นแยกตามแต่ละชื่อโดยอัตโนมัติ. |
| **ต้องการแถวหัวเรื่องพร้อมการจัดรูปแบบ** | หลังการประมวลผล ให้เข้าถึง `Worksheet.Cells["A1"]` และกำหนดคุณสมบัติ `Style` (ฟอนต์, พื้นหลัง). |
| **บันทึกเป็นสตรีมแทนไฟล์** | แทนที่ `workbook.Save(outputPath, SaveFormat.Xlsx)` ด้วย `workbook.Save(stream, SaveFormat.Xlsx)`. |

**เคล็ดลับระดับมืออาชีพ:** ควรห่อการดำเนินการระบบไฟล์ทั้งหมดในบล็อก `try…catch` เพื่อให้พบปัญหาการอนุญาตได้ตั้งแต่แรก.

## โค้ดเต็ม (พร้อมคัดลอก)

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create the DataTable that will be exported
        DataTable dataTable = new DataTable("Sheet1");
        dataTable.Columns.Add("Id", typeof(int));

        // Add rows – you can replace this with your own data source
        dataTable.Rows.Add(1);
        dataTable.Rows.Add(2);
        int[] extraIds = { 3, 4, 5 };
        foreach (int id in extraIds)
        {
            dataTable.Rows.Add(id);
        }

        // Process SmartMarkers and save the workbook
        ProcessAndSaveWorkbook(dataTable);
    }

    private static void ProcessAndSaveWorkbook(DataTable dataTable)
    {
        // Configure SmartMarkerOptions to rename duplicate sheets automatically
        SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions
        {
            DetailSheetNewName = "Sheet1_{0}"
        };

        // Create a new workbook and populate it from the DataTable
        Workbook workbook = new Workbook();
        workbook.ProcessSmartMarkers(dataTable, smartMarkerOptions);

        // Save the workbook as an .xlsx file
        string outputPath = @"YOUR_DIRECTORY\DuplicateSheets.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

### ผลลัพธ์ที่คาดหวัง

การรันโปรแกรมจะพิมพ์:

```
Workbook saved to YOUR_DIRECTORY\DuplicateSheets.xlsx
```

การเปิดไฟล์ `DuplicateSheets.xlsx` จะเห็นแผ่นที่ชื่อ **Sheet1** มีคอลัมน์ `Id` ที่มีค่า `1, 2, 3, 4, 5`. หากคุณประมวลผล `DataTable` อื่นที่ชื่อ `"Sheet1"` ใน workbook เดียวกันต่อมา Aspose.Cells จะสร้าง **Sheet1_1**, **Sheet1_2**, เป็นต้น โดยอัตโนมัติ.

## สรุป

ตอนนี้คุณรู้วิธี **create excel sheet** จาก `DataTable` ใน C#, **export datatable to excel**, **add rows to datatable**, สร้าง **create multiple excel sheets** ด้วยการตั้งชื่ออัตโนมัติ, และ **save workbook as xlsx** ตัวอย่างที่สมบูรณ์และสามารถรันได้แสดงขั้นตอนการทำงานตั้งแต่ต้นจนจบและให้เคล็ดลับที่เป็นประโยชน์สำหรับชุดข้อมูลขนาดใหญ่และการจัดรูปแบบแบบกำหนดเอง.

### ขั้นตอนต่อไปคืออะไร?

* สำรวจ **cell formatting** (ฟอนต์, สี, เส้นขอบ) โดยเข้าถึง `Worksheet.Cells` หลังจาก `ProcessSmartMarkers`.  
* ใช้ **SmartMarker loops** เพื่อสร้างรายงาน master‑detail ใน workbook เดียว.  
* เปลี่ยนเป็น **CSV export** โดยเปลี่ยน `SaveFormat.Csv` หากคุณต้องการรูปแบบข้อความธรรมดา.  

คุณสามารถปรับโค้ดให้เข้ากับแหล่งข้อมูลของคุณได้ตามต้องการ ไม่ว่าจะเป็นการสืบค้นฐานข้อมูล, การตอบสนองจาก API, หรือคอลเลกชันในหน่วยความจำ ขอให้สนุกกับการเขียนโค้ด!

## คุณควรเรียนรู้อะไรต่อไป?

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งข้อมูลมีตัวอย่างโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายขั้นตอนต่อขั้นตอน เพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจวิธีการนำไปใช้แบบอื่นในโปรเจกต์ของคุณ.

- [วิธีสร้างและบันทึก Excel Workbook เป็น ODS ด้วย Aspose.Cells สำหรับ .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [วิธีสร้างและบันทึก Excel Workbook เป็น SVG ด้วย Aspose.Cells สำหรับ Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)
- [วิธีสร้างและส่งออก Excel เป็น HTML ด้วย Aspose.Cells Java | คู่มือการทำงานของ Workbook](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}