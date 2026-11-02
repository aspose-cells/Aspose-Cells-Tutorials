---
category: general
date: 2026-10-07
description: สร้างแผ่นรายละเอียดที่ซ้ำกันใน Excel ด้วย C# เรียนรู้วิธีสร้างหลายแผ่นงานและสร้างรายงานจากตารางในครั้งเดียว.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create duplicated detail sheets
- how to generate multiple worksheets
- generate excel report from tables
language: th
lastmod: 2026-10-07
og_description: สร้างแผ่นรายละเอียดซ้ำใน Excel ด้วย C# บทเรียนนี้แสดงวิธีสร้างหลายแผ่นงานและผลิตรายงาน
  Excel ฉบับเต็มจากตาราง.
og_image_alt: Screenshot of an Excel file that has create duplicated detail sheets
  output
og_title: สร้างแผ่นรายละเอียดซ้ำใน Excel – คู่มือ C# ทีละขั้นตอน
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Create duplicated detail sheets in Excel using C#. Learn how to generate
    multiple worksheets and build a report from tables in a single run.
  headline: Create duplicated detail sheets in Excel using C#
  type: TechArticle
- description: Create duplicated detail sheets in Excel using C#. Learn how to generate
    multiple worksheets and build a report from tables in a single run.
  name: Create duplicated detail sheets in Excel using C#
  steps:
  - name: '**Obtain the data source** that contains a master table and two detail
      tables.'
    text: '**Obtain the data source** that contains a master table and two detail
      tables.'
  - name: '**Configure the Smart‑marker processor** so each duplicated detail sheet
      receives a unique name.'
    text: '**Configure the Smart‑marker processor** so each duplicated detail sheet
      receives a unique name.'
  - name: '**Create a new workbook** and place a smart‑marker that references the
      master table.'
    text: '**Create a new workbook** and place a smart‑marker that references the
      master table.'
  - name: '**Run the processor** to generate the master sheet and all detail sheets.'
    text: '**Run the processor** to generate the master sheet and all detail sheets.'
  - name: '**Save the workbook** – each detail sheet now has a distinct name.'
    text: '**Save the workbook** – each detail sheet now has a distinct name.'
  type: HowTo
tags:
- C#
- Excel automation
- Aspose.Cells
title: สร้างแผ่นรายละเอียดซ้ำใน Excel ด้วย C#
url: /th/net/excel-copy-worksheet/create-duplicated-detail-sheets-in-excel-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# สร้างแผ่นรายละเอียดที่ซ้ำกันใน Excel ด้วย C#

หากคุณต้อง **สร้างแผ่นรายละเอียดที่ซ้ำกัน** ในเวิร์กบุ๊กของ Excel คำแนะนำนี้จะพาคุณผ่านกระบวนการทั้งหมด คุณจะได้เห็นวิธี **สร้างหลายแผ่นงาน** จากชุดข้อมูล master‑detail และสร้างรายงาน Excel ที่ดูเป็นมืออาชีพโดยตรงจากตาราง

การสร้างรายงาน Excel จากตารางเป็นความต้องการทั่วไปสำหรับระบบบิลลิ่ง, แดชบอร์ดสินค้าคงคลัง, หรือสถานการณ์ใด ๆ ที่บันทึกหลักมีหลายแถวรายละเอียดที่เกี่ยวข้อง เมื่อจบบทเรียนนี้คุณจะมีโปรแกรม C# ที่สามารถรันได้ซึ่งสร้างเวิร์กบุ๊กที่มีแผ่นหลักและแผ่นที่มีชื่อเฉพาะสำหรับแต่ละกลุ่มรายละเอียด

## ข้อกำหนดเบื้องต้น

ก่อนเริ่มทำงาน โปรดตรวจสอบว่าคุณมี:

* .NET 6.0 (หรือใหม่กว่า) ที่ติดตั้งแล้ว  
* Visual Studio 2022 หรือ IDE ที่รองรับ C# ใด ๆ  
* แพ็กเกจ **Aspose.Cells for .NET** จาก NuGet (ให้ `SmartMarkerProcessor`)  

คุณสามารถเพิ่มแพ็กเกจได้ด้วยคำสั่งต่อไปนี้:

```bash
dotnet add package Aspose.Cells
```

## ภาพรวมของโซลูชัน

โซลูชันนี้ทำตามขั้นตอนห้าขั้นตอน:

1. **ดึงแหล่งข้อมูล** ที่มีตาราง master และสองตาราง detail  
2. **กำหนดค่า Smart‑marker processor** เพื่อให้แต่ละแผ่นรายละเอียดที่ซ้ำกันได้รับชื่อที่ไม่ซ้ำกัน  
3. **สร้างเวิร์กบุ๊กใหม่** และวาง smart‑marker ที่อ้างอิงตาราง master  
4. **เรียกใช้ processor** เพื่อสร้างแผ่น master และแผ่น detail ทั้งหมด  
5. **บันทึกเวิร์กบุ๊ก** – ตอนนี้แต่ละแผ่น detail มีชื่อที่แตกต่างกันแล้ว  

แต่ละขั้นตอนจะอธิบายรายละเอียดต่อไปนี้ พร้อมโค้ดและเหตุผลที่เกี่ยวข้อง

## ขั้นตอนที่ 1: ดึงแหล่งข้อมูลที่มีตาราง master และสองตาราง detail

งานแรกคือสร้าง `DataSet` ที่จำลองข้อมูลที่คุณอาจดึงจากฐานข้อมูล `DataSet` ต้องมีตารางชื่อ **Master** และหนึ่งหรือหลายตารางชื่อ **Detail** เครื่องยนต์ Smart‑marker จะใช้ชื่อตารางเหล่านี้เป็นมาร์กเกอร์เพื่อเติมข้อมูลในเวิร์กบุ๊ก

```csharp
using System.Data;

/// <summary>
/// Returns a DataSet with a master table and two detail tables.
/// In a real application you would fill these tables from a database.
/// </summary>
static DataSet GetReportDataSet()
{
    var ds = new DataSet();

    // Master table – one row per invoice
    var master = new DataTable("Master");
    master.Columns.Add("InvoiceId", typeof(int));
    master.Columns.Add("CustomerName", typeof(string));
    master.Columns.Add("InvoiceDate", typeof(DateTime));
    master.Rows.Add(101, "Acme Corp", new DateTime(2024, 12, 01));
    master.Rows.Add(102, "Beta Ltd.", new DateTime(2024, 12, 03));
    ds.Tables.Add(master);

    // Detail table – multiple rows per invoice
    var detail = new DataTable("Detail");
    detail.Columns.Add("InvoiceId", typeof(int));
    detail.Columns.Add("Product", typeof(string));
    detail.Columns.Add("Quantity", typeof(int));
    detail.Columns.Add("Price", typeof(decimal));

    // Detail rows for Invoice 101
    detail.Rows.Add(101, "Widget A", 5, 9.99m);
    detail.Rows.Add(101, "Widget B", 2, 19.95m);

    // Detail rows for Invoice 102
    detail.Rows.Add(102, "Gadget X", 1, 99.00m);
    detail.Rows.Add(102, "Gadget Y", 3, 49.50m);
    ds.Tables.Add(detail);

    return ds;
}
```

**เหตุผลที่สำคัญ:**  
*Smart‑marker* ทำงานกับอ็อบเจ็กต์ `DataSet`; ชื่อตารางแต่ละอันจะกลายเป็นมาร์กเกอร์ที่เครื่องยนต์สามารถแทนที่ได้ การจัดโครงสร้างข้อมูลแบบนี้ทำให้ processor สามารถทำสำเนาแผ่นรายละเอียดสำหรับแต่ละ `InvoiceId` ได้โดยอัตโนมัติ

## ขั้นตอนที่ 2: กำหนดค่า Smart‑marker processor เพื่อให้แต่ละแผ่นรายละเอียดที่ซ้ำกันมีชื่อเฉพาะ

เมื่อ processor พบมาร์กเกอร์ detail มันจะสร้างแผ่นงานใหม่สำหรับแต่ละกลุ่มแถว โดยค่าเริ่มต้นแผ่นใหม่ทั้งหมดจะใช้ชื่อเดียวกัน ซึ่งจะทำให้เกิดความขัดแย้งในการตั้งชื่อ การตั้งค่า `DetailSheetNewName` จะบอกเครื่องยนต์วิธีตั้งชื่อแต่ละสำเนา

```csharp
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

/// <summary>
/// Configures the SmartMarkerProcessor to rename duplicated detail sheets.
/// The placeholder {0} is replaced with a sequential number (1, 2, …).
/// </summary>
static SmartMarkerProcessor ConfigureProcessor()
{
    var processor = new SmartMarkerProcessor();

    // The pattern "Detail_{0}" becomes Detail_1, Detail_2, …
    processor.Options.DetailSheetNewName = "Detail_{0}";

    // Optional: keep the original sheet as a template (if you have one)
    processor.Options.KeepTemplateSheet = false;

    return processor;
}
```

**เหตุผลที่สำคัญ:**  
หากไม่มีรูปแบบการตั้งชื่อที่เป็นเอกลักษณ์ เวิร์กบุ๊กจะโยนข้อยกเว้นเมื่อ processor พยายามเพิ่มแผ่นรายละเอียดที่สอง ตัวแปร `{0}` ทำให้แต่ละแผ่นได้รับชื่อที่แตกต่างและคาดเดาได้

## ขั้นตอนที่ 3: สร้างเวิร์กบุ๊กใหม่และวาง smart‑marker ที่อ้างอิงตาราง master

ตอนนี้คุณสร้าง `Workbook` ใหม่, เพิ่มมาร์กเกอร์ที่ชี้ไปที่ตาราง **Master**, และอาจจัดรูปแบบแถวหัวตารางตามต้องการ

```csharp
/// <summary>
/// Creates a workbook with a single cell that contains the master smart‑marker.
/// </summary>
static Workbook CreateTemplateWorkbook()
{
    var workbook = new Workbook();
    var sheet = workbook.Worksheets[0];

    // Put the master smart‑marker in cell A1.
    // The double braces {{ }} tell SmartMarker to replace the content with the Master table.
    sheet.Cells["A1"].PutValue("{{Master}}");

    // Optional: add a header row for visual clarity.
    sheet.Cells["A2"].PutValue("Invoice ID");
    sheet.Cells["B2"].PutValue("Customer");
    sheet.Cells["C2"].PutValue("Date");
    sheet.Cells["A2:C2"].Style.Font.IsBold = true;

    return workbook;
}
```

**เหตุผลที่สำคัญ:**  
มาร์กเกอร์ `{{Master}}` บอก processor ให้ขยายตาราง master เริ่มที่ `A1` แถวต่อมาจะกลายเป็นแถวข้อมูลสำหรับแต่ละบันทึก master นี่คือจุดเริ่มต้นสำหรับ **generate excel report from tables**

## ขั้นตอนที่ 4: เรียกใช้ smart‑marker processor เพื่อสร้างแผ่น master และแผ่น detail

เมื่อมีแหล่งข้อมูล, processor, และเทมเพลตพร้อมแล้ว คุณเรียก `Process` เครื่องยนต์จะขยายมาร์กเกอร์ master แล้วสร้างแผ่น detail แยกต่างหากสำหรับแต่ละ `InvoiceId` ที่ไม่ซ้ำกัน

```csharp
static void GenerateReport()
{
    // 1️⃣ Obtain data
    DataSet reportData = GetReportDataSet();

    // 2️⃣ Configure processor
    SmartMarkerProcessor processor = ConfigureProcessor();

    // 3️⃣ Create template workbook
    Workbook workbook = CreateTemplateWorkbook();

    // 4️⃣ Process the smart‑markers – this creates the master sheet and duplicated detail sheets
    processor.Process(workbook, reportData);

    // 5️⃣ Save the file
    string outputPath = Path.Combine(
        Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
        "DuplicatedDetailSheets.xlsx");
    workbook.Save(outputPath);

    Console.WriteLine($"Report generated successfully: {outputPath}");
}
```

**เหตุผลที่สำคัญ:**  
`processor.Process` ทำงานหนัก: อ่านแถว master, สร้างแผ่น detail สำหรับแต่ละคีย์ที่ไม่ซ้ำ, และเปลี่ยนชื่อแผ่นตามรูปแบบที่กำหนดไว้ก่อนหน้านี้ ผลลัพธ์คือเวิร์กบุ๊กที่ตอบสนองความต้องการ **how to generate multiple worksheets**

## ขั้นตอนที่ 5: บันทึกเวิร์กบุ๊กที่ได้ – ตอนนี้แต่ละแผ่น detail มีชื่อที่แตกต่างกันแล้ว

คำสั่ง `Save` จะเขียนไฟล์ลงดิสก์ เมื่อคุณเปิดเวิร์กบุ๊กจะเห็น:

* **Sheet1** – แผ่น master ที่มีหัวบิล (invoice headers)  
* **Detail_1**, **Detail_2**, … – แต่ละแผ่นมีแถวจากตาราง **Detail** ที่เกี่ยวข้องกับบิลเฉพาะ

ด้านล่างเป็นภาพจำลองของโครงสร้างเวิร์กบุ๊กที่คาดหวัง (ภาพเป็นตัวอย่าง; คุณสามารถแทนที่ด้วยสกรีนช็อตจริงได้หากต้องการ)

![ภาพหน้าจอของไฟล์ Excel ที่สร้างแผ่นรายละเอียดที่ซ้ำกัน](https://example.com/images/duplicated-detail-sheets.png)

### ผลลัพธ์ที่คาดหวัง

| ชื่อแผ่นงาน | รายละเอียดเนื้อหา |
|------------|-------------------|
| **Sheet1** | แถว master: InvoiceId, CustomerName, InvoiceDate |
| **Detail_1** | แถว detail ที่ `InvoiceId = 101` |
| **Detail_2** | แถว detail ที่ `InvoiceId = 102` |

การเปิดไฟล์ `DuplicatedDetailSheets.xlsx` ควรแสดงโครงสร้างเช่นนี้อย่างตรงไปตรงมา

## โค้ดเต็ม (พร้อมคัดลอก)

```csharp
using System;
using System.Data;
using System.IO;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

namespace ExcelDetailSheetsDemo
{
    class Program
    {
        static void Main()
        {
            GenerateReport();
        }

        // ------------------------------------------------------------
        // Step 1 – data source
        // ------------------------------------------------------------
        static DataSet GetReportDataSet()
        {
            var ds = new DataSet();

            var master = new DataTable("Master");
            master.Columns.Add("InvoiceId", typeof(int));
            master.Columns.Add("CustomerName", typeof(string));
            master.Columns.Add("InvoiceDate", typeof(DateTime));
            master.Rows.Add(101, "Acme Corp", new DateTime(2024, 12, 01));
            master.Rows.Add(102, "Beta Ltd.", new DateTime(2024, 12, 03));
            ds.Tables.Add(master);

            var detail = new DataTable("Detail");
            detail.Columns.Add("InvoiceId", typeof(int));
            detail.Columns.Add("Product", typeof(string));
            detail.Columns.Add("Quantity", typeof(int));
            detail.Columns.Add("Price", typeof(decimal));
            detail.Rows.Add(101, "Widget A", 5, 9.99m);
            detail.Rows.Add(101, "Widget B", 2, 19.95m);
            detail.Rows.Add(102, "Gadget X", 1, 99.00m);
            detail.Rows.Add(102, "Gadget Y", 3, 49.50m);
            ds.Tables.Add(detail);

            return ds;
        }

        // ------------------------------------------------------------
        // Step 2 – processor configuration
        // ------------------------------------------------------------
        static SmartMarkerProcessor ConfigureProcessor()
        {
            var processor = new SmartMarkerProcessor();
            processor.Options.DetailSheetNewName = "Detail_{0}";
            processor.Options.KeepTemplate


## คุณควรเรียนรู้อะไรต่อไป?

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งข้อมูลมีโค้ดตัวอย่างทำงานครบถ้วนพร้อมคำอธิบายทีละขั้นตอน เพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจวิธีการทำงานแบบต่าง ๆ ในโปรเจกต์ของคุณเอง

- [How to Name Sheets Automatically – Generate Multiple Sheets in C#](/cells/english/net/smart-markers-dynamic-data/how-to-name-sheets-automatically-generate-multiple-sheets-in/)
- [How to Create Worksheets – Step‑by‑Step Guide for Dynamic Excel Generation](/cells/english/net/worksheet-operations/how-to-create-worksheets-step-by-step-guide-for-dynamic-exce/)
- [How to Generate Excel Report in C# – Full Guide Using SmartMarker](/cells/english/net/smart-markers-dynamic-data/how-to-generate-excel-report-in-c-full-guide-using-smartmark/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}