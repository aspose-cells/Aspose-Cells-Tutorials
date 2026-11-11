---
category: general
date: 2026-10-26
description: ExportTableOptions ที่กำหนดเองเมื่อใช้ ExportAsStrin ช่วยให้คุณส่งออกข้อมูล
  Excel เป็นสตริงใน C# ทำตามคู่มือขั้นตอนต่อขั้นตอนเพื่อกำหนดค่าและรันการส่งออก.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- Custom ExportTableOptions when ExportAsStrin
- how to export excel as string
- ExportTableOptions C#
- Excel to DataTable string conversion
- Aspose.Cells export as string
language: th
lastmod: 2026-10-26
og_description: ExportTableOptions แบบกำหนดเองเมื่อ ExportAsStrin เปิดใช้งานการส่งออก
  Excel แบบสตริงเท่านั้น เรียนรู้ขั้นตอนที่แน่นอนในการกำหนดค่าและเรียกใช้การส่งออกใน
  C#
og_image_alt: Code snippet showing ExportTableOptions configuration for string export
og_title: ตัวเลือก ExportTableOptions แบบกำหนดเองเมื่อ ExportAsString – ส่งออก Excel
  เป็นสตริงใน C#
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Custom ExportTableOptions when ExportAsStrin lets you export Excel
    data as strings in C#. Follow the step‑by‑step guide to configure and run the
    export.
  headline: Custom ExportTableOptions when ExportAsStrin for Excel
  type: TechArticle
tags:
- C#
- Aspose.Cells
- Excel
- DataTable
title: กำหนดค่า ExportTableOptions เองเมื่อใช้ ExportAsStrin สำหรับ Excel
url: /th/net/excel-data-export-retrieval/custom-exporttableoptions-when-exportasstrin-for-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Custom ExportTableOptions when ExportAsStrin – ส่งออก Excel เป็นสตริงใน C#

หากคุณต้องการ **Custom ExportTableOptions when ExportAsStrin** เพื่อให้ได้ค่าของแต่ละเซลล์เป็นสตริงธรรมดา คู่มือฉบับนี้จะแสดงวิธีทำอย่างละเอียด ไม่ว่าคุณจะกำลังสร้าง pipeline การนำเข้าข้อมูลหรือจำเป็นต้องได้ไฟล์ CSV ที่สะอาด คุณจะเห็นว่าการกำหนดค่าตัวเลือกแบบนี้ช่วยหลีกเลี่ยงความประหลาดใจจากการแปลงประเภทได้อย่างไร

ในบทแนะนำนี้คุณจะได้เรียนรู้ **how to export excel as string** ด้วยไลบรารี Aspose.Cells ดูโค้ดที่สมบูรณ์และสามารถรันได้ และเข้าใจเหตุผลเบื้องหลังแต่ละการตั้งค่า ไม่จำเป็นต้องอ้างอิงเอกสารภายนอก – ทุกอย่างที่คุณต้องการอยู่ที่นี่

## ข้อกำหนดเบื้องต้น

* .NET 6.0 SDK หรือรุ่นที่ใหม่กว่า ติดตั้งแล้ว  
* Visual Studio 2022 (หรือ IDE ใดก็ได้ที่รองรับ .NET)  
* แพ็คเกจ Aspose.Cells for .NET (ติดตั้งผ่าน NuGet: `Install-Package Aspose.Cells`)  
* ไฟล์ Excel workbook (`sample.xlsx`) ที่วางไว้ในโฟลเดอร์รากของโปรเจกต์  

รายการเหล่านี้เป็นเพียง dependencies ที่จำเป็น; โค้ดสามารถทำงานบน Windows, Linux หรือ macOS ได้โดยไม่ต้องใช้ไลบรารีเพิ่มเติม

## ขั้นตอนที่ 1: โหลด workbook ที่ต้องการส่งออก

สิ่งแรกที่คุณทำเมื่อใช้ **Custom ExportTableOptions when ExportAsStrin** คือการรับอ็อบเจ็กต์ `Worksheet` จาก workbook ที่โหลดแล้ว อ็อบเจ็กต์นี้ให้คุณเข้าถึงแถว, คอลัมน์, และ API การส่งออก

```csharp
using Aspose.Cells;
using System.Data;

// Load the workbook from disk
Workbook workbook = new Workbook("sample.xlsx");

// Get the first worksheet (index 0)
Worksheet worksheet = workbook.Worksheets[0];
```

*ทำไมเรื่องนี้ถึงสำคัญ:*  
`Workbook` อ่านไฟล์เพียงครั้งเดียวและเก็บข้อมูลการจัดรูปแบบทั้งหมดไว้ในหน่วยความจำ การเลือก `Worksheet` เฉพาะช่วยจำกัดขอบเขตการส่งออกและหลีกเลี่ยงการประมวลผลแผ่นงานที่ซ่อนอยู่โดยไม่จำเป็น

## ขั้นตอนที่ 2: กำหนดค่า ExportTableOptions ด้วย ExportAsString = true

หัวใจของ **Custom ExportTableOptions when ExportAsStrin** คืออ็อบเจ็กต์ `ExportTableOptions` การตั้งค่า `ExportAsString` จะบังคับให้ตัวส่งออกถือว่าแต่ละเซลล์เป็นสตริง ไม่ว่าประเภทข้อมูลเดิมจะเป็นอะไร (วันที่, ตัวเลข, บูลีน ฯลฯ) การเปิดใช้งาน `PreserveFormatting` จะรักษารูปแบบการแสดงผล (เช่น สัญลักษณ์สกุลเงิน) ในสตริงที่ได้

```csharp
// Create and configure the export options
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true,          // Export every cell value as a string
    PreserveFormatting = true      // Keep the original cell formatting
};
```

*ทำไมเรื่องนี้ถึงสำคัญ:*  
เมื่อคุณเรียก `ExportDataTable` ภายหลัง ไลบรารีจะพยายามสรุปประเภท .NET ของแต่ละคอลัมน์ตามปกติ ด้วย `ExportAsString = true` ขั้นตอนการสรุปประเภทจะถูกข้ามไป ทำให้หลีกเลี่ยงการแปลง `DateTime` หรือ `double` ที่ไม่คาดคิดซึ่งอาจทำให้ตัวแยกวิเคราะห์ CSV ด้านล่างล้มเหลว

## ขั้นตอนที่ 3: ส่งออกช่วงข้อมูลเป็น DataTable โดยใช้ตัวเลือกที่กำหนดเอง

ตอนนี้คุณสามารถส่งออกช่วงสี่เหลี่ยม (แถว 0‑9, คอลัมน์ 0‑4) จาก worksheet ได้ วิธีนี้จะคืนค่า `DataTable` ที่ทุกฟิลด์เป็น `string`

```csharp
// Export rows 0‑9 and columns 0‑4 (5 columns total) as a DataTable
DataTable dataTable = worksheet.ExportDataTable(
    startRow: 0,
    startColumn: 0,
    totalRows: 10,
    totalColumns: 5,
    options: exportOptions);
```

*ทำไมเรื่องนี้ถึงสำคัญ:*  
`ExportDataTable` เป็นวิธีที่สะดวกที่สุดในการย้ายข้อมูล Excel ไปยังโครงสร้างเชิงสัมพันธ์ที่หลาย API ของ .NET เข้าใจอยู่แล้ว (เช่น Entity Framework, Dapper) โดยการส่งผ่าน **Custom ExportTableOptions when ExportAsStrin** คุณรับประกันได้ว่า `DataColumn.DataType` ของแต่ละคอลัมน์จะเป็น `typeof(string)`

## ขั้นตอนที่ 4: ตรวจสอบผลลัพธ์ – ค่าทั้งหมดเป็นสตริง

เป็นแนวปฏิบัติที่ดีในการยืนยันว่าการส่งออกทำงานตามที่คาดหวัง ลูปต่อไปนี้จะแสดงแต่ละเซลล์และประเภทของมันในขณะรัน

```csharp
Console.WriteLine("Exported DataTable (all values as strings):");
foreach (DataRow row in dataTable.Rows)
{
    for (int i = 0; i < dataTable.Columns.Count; i++)
    {
        object value = row[i];
        Console.Write($"{value} ({value.GetType().Name})\t");
    }
    Console.WriteLine();
}
```

**ผลลัพธ์ที่คาดหวัง**

```
123 (String)    2023‑01‑15 (String)    $45.67 (String)    TRUE (String)    Sample text (String)
...
```

ทุกเซลล์แสดง `String` เป็นประเภทของมัน ยืนยันว่า **Custom ExportTableOptions when ExportAsStrin** ทำงานอย่างถูกต้อง

## ขั้นตอนที่ 5: ตัวเลือก – เขียน DataTable ไปเป็น CSV

หากเป้าหมายสุดท้ายของคุณคือไฟล์ข้อความธรรมดา คุณสามารถทำการ serialize `DataTable` ไปเป็น CSV ได้อย่างง่ายดาย:



## สิ่งที่คุณควรเรียนต่อไป

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดซึ่งต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งข้อมูลรวมตัวอย่างโค้ดที่ทำงานได้สมบูรณ์พร้อมคำอธิบายทีละขั้นตอน เพื่อช่วยให้คุณเชี่ยวชาญคุณลักษณะ API เพิ่มเติมและสำรวจแนวทางการนำไปใช้แบบอื่นในโครงการของคุณ

- [ส่งออก HTML Strings จาก Excel ไปยัง DataTable ด้วย Aspose.Cells for .NET: คู่มือแบบขั้นตอน](/cells/english/net/import-export/export-html-strings-excel-datatable-aspose-cells-net/)
- [ส่งออก Custom Properties จาก Excel เป็น PDF ด้วย Aspose Cells Net](/cells/hongkong/net/workbook-operations/export-custom-properties-excel-pdf-aspose-cells-net/)
- [Aspose Cells Java Custom Load Filters การส่งออก Excel](/cells/hongkong/java/import-export/aspose-cells-java-custom-load-filters-excel-export/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}