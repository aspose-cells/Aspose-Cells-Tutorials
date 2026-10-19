---
category: general
date: 2026-08-11
description: ส่งออกไฟล์ Excel เป็น txt ใน C# พร้อมคู่มือขั้นตอนโดยละเอียด เรียนรู้วิธีแปลงไฟล์
  xlsx เป็นข้อความธรรมดาโดยใช้ Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to txt
- convert xlsx to plain text
- how to export excel worksheet as text
- export worksheet as text file
language: th
lastmod: 2026-08-11
og_description: ส่งออก Excel เป็น txt ใน C# อย่างรวดเร็ว บทเรียนนี้แสดงวิธีแปลงไฟล์
  xlsx เป็นข้อความธรรมดา การกำหนดรูปแบบ และการจัดการแผ่นงานขนาดใหญ่.
og_image_alt: Code snippet that exports an Excel worksheet to a plain text file using
  C#
og_title: ส่งออก Excel เป็นไฟล์ txt ใน C# – คู่มือแบบขั้นตอนสำหรับนักพัฒนา
schemas:
- author: Aspose
  dateModified: '2026-08-11'
  description: Export excel to txt in C# with a step-by-step guide. Learn how to convert
    xlsx to plain text using Aspose.Cells.
  headline: Export excel to txt in C# – complete programming guide
  type: TechArticle
- description: Export excel to txt in C# with a step-by-step guide. Learn how to convert
    xlsx to plain text using Aspose.Cells.
  name: Export excel to txt in C# – complete programming guide
  steps:
  - name: – load the workbook
    text: '```csharp using Aspose.Cells;'
  - name: – get the first worksheet
    text: '```csharp Worksheet sheet = workbook.Worksheets[0]; ```'
  - name: – define export options for text conversion
    text: '```csharp ExportTableOptions exportOptions = new ExportTableOptions { ExportAsString
      = true, // Export all values as text DateTimeFormat = "yyyy-MM-dd", // Desired
      date format NumberFormat = "#,##0.00" // Desired numeric format }; ```'
  - name: – export worksheet as text file
    text: '```csharp // Apply the options to the worksheet sheet.ExportTableOptions
      = exportOptions;'
  type: HowTo
tags:
- excel
- csharp
- text export
- aspose.cells
title: ส่งออก Excel เป็น txt ใน C# – คู่มือการเขียนโปรแกรมครบถ้วน
url: /th/net/converting-excel-files-to-other-formats/export-excel-to-txt-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ส่งออก Excel เป็นไฟล์ txt ใน C# – คู่มือการเขียนโปรแกรมเต็มรูปแบบ

หากคุณต้องการ **export excel to txt** คุณสามารถทำได้ด้วยไม่กี่บรรทัดของโค้ด C# คู่มือนี้จะแสดงวิธีแปลงเวิร์กบุ๊ก `.xlsx` ให้เป็นไฟล์ plain‑text พร้อมคงรูปแบบข้อมูลที่คุณกำหนดไว้

การส่งออกเวิร์กชีตเป็นไฟล์ข้อความเป็นความต้องการทั่วไปเมื่อระบบ downstream ยอมรับข้อมูลที่คั่นด้วยตัวคั่นเท่านั้น หรือเมื่อคุณต้องการตรวจสอบค่าของเซลล์ดิบ ในส่วนต่อไปนี้คุณจะได้เรียนรู้วิธีกำหนดรูปแบบวันที่และตัวเลข การจัดการแผ่นงานขนาดใหญ่ และหลีกเลี่ยงข้อผิดพลาดทั่วไป

## ข้อกำหนดเบื้องต้นสำหรับการแปลง xlsx เป็น plain text

* .NET 6.0 (หรือรุ่นใหม่กว่า) ติดตั้งแล้ว – โค้ดนี้ตั้งเป้าหมายที่ .NET Standard 2.0 ดังนั้นจึงทำงานได้กับ .NET Framework 4.6+ ด้วย
* ใบอนุญาตสำหรับ **Aspose.Cells** (รุ่นทดลองฟรีสามารถใช้สำหรับการทดสอบได้)
* IDE เช่น Visual Studio 2022 หรือ Visual Studio Code
* ไฟล์ Excel ชื่อ `input.xlsx` ที่วางไว้ในโฟลเดอร์ที่คุณสามารถอ้างอิงจากโปรเจกต์ของคุณ

รายการเหล่านี้เป็นข้อกำหนดภายนอกเพียงอย่างเดียว; บทเรียนนี้ไม่ได้พึ่งพาแพคเกจ NuGet เพิ่มเติม

## วิธีส่งออก excel เป็น txt ด้วย Aspose.Cells

Aspose.Cells มีคลาส `ExportTableOptions` ที่ให้คุณควบคุมวิธีการแปลงค่าของเซลล์เป็นสตริง โดยการตั้งค่า `ExportAsString` เป็น `true` คุณจะบังคับให้ทุกเซลล์ถูกเขียนเป็นข้อความ ซึ่งจำเป็นเมื่อคุณต้องการผลลัพธ์ plain‑text ที่กำหนดได้อย่างแน่นอน

### ขั้นตอนที่ 1 – โหลดเวิร์กบุ๊ก

```csharp
using Aspose.Cells;

string inputPath = @"YOUR_DIRECTORY\input.xlsx";
Workbook workbook = new Workbook(inputPath);
```

*คอนสตรัคเตอร์ `Workbook` จะอ่านไฟล์ Excel เข้าไปในหน่วยความจำ หากไฟล์ไม่พบ จะเกิดข้อยกเว้น ดังนั้นคุณอาจต้องห่อการเรียกนี้ด้วยบล็อก try‑catch สำหรับโค้ดในสภาพการผลิต*

### ขั้นตอนที่ 2 – ดึงเวิร์กชีตแรก

```csharp
Worksheet sheet = workbook.Worksheets[0];
```

*เวิร์กชีตใช้ดัชนีเริ่มจากศูนย์ ดังนั้น index 0 หมายถึงแท็บแรก คุณสามารถแทนที่ดัชนีด้วยชื่อชีต (`workbook.Worksheets["Sheet1"]`) เมื่อคุณต้องการระบุแท็บเฉพาะ*

### ขั้นตอนที่ 3 – กำหนดตัวเลือกการส่งออกสำหรับการแปลงเป็นข้อความ

```csharp
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true,               // Export all values as text
    DateTimeFormat = "yyyy-MM-dd",       // Desired date format
    NumberFormat   = "#,##0.00"          // Desired numeric format
};
```

*`ExportAsString` รับประกันว่าทุกเซลล์ ไม่ว่าจะเป็นประเภทใดเดิม จะกลายเป็นสตริงในไฟล์ผลลัพธ์ คุณสมบัติ `DateTimeFormat` และ `NumberFormat` ให้คุณควบคุมรูปแบบการแสดงวันที่และตัวเลข ซึ่งสำคัญเมื่อคุณ **convert xlsx to plain text** สำหรับระบบที่คาดหวังรูปแบบเฉพาะ*

### ขั้นตอนที่ 4 – ส่งออกเวิร์กชีตเป็นไฟล์ข้อความ

```csharp
// Apply the options to the worksheet
sheet.ExportTableOptions = exportOptions;

// Export the data to a tab‑delimited text file
string outputPath = @"YOUR_DIRECTORY\Exported.txt";
sheet.ExportDataTable(outputPath);
```

*`ExportDataTable` จะเขียนเนื้อหาเวิร์กชีตลงในไฟล์ plain‑text โดยใช้ตัวเลือกที่คุณกำหนด ตัวคั่นเริ่มต้นคืออักขระแท็บ (`\t`). หากคุณต้องการตัวคั่นอื่น คุณสามารถใช้ overload ที่รับอินสแตนซ์ `ExportTableOptions` และระบุ `ExportTableOptions.Separator`. ไฟล์ที่ได้สามารถเปิดด้วยโปรแกรมแก้ไขข้อความใดก็ได้หรือทำการนำเข้าไปยังฐานข้อมูล*

#### ผลลัพธ์ที่คาดหวัง

สมมติว่า `input.xlsx` มีเนื้อหา:

| A            | B       | C          |
|--------------|---------|------------|
| 2023‑05‑01   | 1234.5  | Sample text|

ด้วยตัวเลือกข้างต้นไฟล์ `Exported.txt` จะมีเนื้อหา:

```
2023-05-01	1,234.50	Sample text
```

แต่ละคอลัมน์คั่นด้วยแท็บ วันที่ใช้รูปแบบ `yyyy‑MM‑dd` และตัวเลขใช้คอมม่าเป็นตัวคั่นหลักพันพร้อมสองตำแหน่งทศนิยม

## ข้อผิดพลาดทั่วไปเมื่อคุณส่งออกเวิร์กชีตเป็นไฟล์ข้อความ

| ปัญหา | สาเหตุ | วิธีหลีกเลี่ยง |
|-------|--------|----------------|
| รูปแบบตัวเลขขึ้นกับ Locale | รูปแบบเริ่มต้นเคารพการตั้งค่าภาษาใน OS ซึ่งอาจทำให้คอมม่า หรือจุดทศนิยมแสดงไม่สอดคล้องกัน | ตั้งค่า `NumberFormat` ใน `ExportTableOptions` อย่างชัดเจน |
| แถวหรือคอลัมน์ที่ซ่อนปรากฏในผลลัพธ์ | Aspose.Cells ส่งออกช่วงที่ใช้ทั้งหมดรวมถึงแถวที่ซ่อนอยู่ | ตั้งค่า `ExportTableOptions.ExportHiddenRows = false` และ `ExportHiddenColumns = false` หากต้องการข้ามแถว/คอลัมน์ที่ซ่อน |
| เวิร์กชีตขนาดใหญ่ทำให้หน่วยความจำอัดแน่น | เวิร์กบุ๊กทั้งหมดถูกโหลดเข้าสู่หน่วยความจำก่อนการส่งออก | ใช้ `Workbook.LoadOptions` พร้อม `LoadDataOnly = true` เพื่อลดการใช้หน่วยความจำ หรือประมวลผลไฟล์เป็นชิ้นส่วน |
| เซลล์วันที่ถูกเก็บเป็นข้อความในไฟล์ต้นฉบับ | หากเซลล์มีสตริงที่จัดรูปแบบแล้ว ตัวส่งออกจะถือว่าเป็นข้อความและละเลย `DateTimeFormat` | ตรวจสอบให้แน่ใจว่าเวิร์กบุ๊กต้นฉบับเก็บวันที่เป็นประเภทวันที่ของ Excel อย่างถูกต้อง |

การแก้ไขปัญหาเหล่านี้ทำให้กระบวนการ **how to export excel worksheet as text** มีความน่าเชื่อถือในสภาพแวดล้อมที่ต่างกัน

## การขยายโซลูชัน – ตัวคั่นแบบกำหนดเองและการส่งออกแบบสตรีมมิ่ง

หากคุณต้องการไฟล์ค่าที่คั่นด้วยคอมม่า (CSV) แทนไฟล์ที่คั่นด้วยแท็บ ให้ปรับเปลี่ยนตัวเลือก:

```csharp
exportOptions.Separator = ',';
exportOptions.ExportHiddenRows = false;   // optional
exportOptions.ExportHiddenColumns = false; // optional
sheet.ExportTableOptions = exportOptions;
sheet.ExportDataTable(@"YOUR_DIRECTORY\Exported.csv");
```

สำหรับไฟล์ที่ใหญ่กว่า 500 MB การสตรีมผลลัพธ์จะช่วยป้องกันแอปพลิเคชันจากการใช้ RAM จนเต็ม:

```csharp
using (FileStream stream = new FileStream(@"YOUR_DIRECTORY\LargeExport.txt",
                                          FileMode.Create,
                                          FileAccess.Write,
                                          FileShare.None,
                                          bufferSize: 81920,
                                          useAsync: true))
{
    sheet.ExportDataTable(stream, exportOptions);
}
```

overload ที่รับ `Stream` จะเขียนแถวแบบเพิ่มขึ้นเรื่อย ๆ ซึ่งเหมาะสำหรับงานแบบ batch หรือเว็บเซอร์วิสที่ส่งไฟล์ข้อความโดยตรงให้กับไคลเอนต์

## ตรวจสอบผลลัพธ์โดยโปรแกรม

หลังจากการส่งออกเสร็จสิ้น คุณสามารถอ่านบรรทัดแรกกลับเข้าสู่หน่วยความจำเพื่อยืนยันรูปแบบได้:

```csharp
string firstLine = File.ReadLines(outputPath).First();
Console.WriteLine($"First line: {firstLine}");
```

การรันสคริปต์นี้ควรพิมพ์บรรทัดเดียวกันที่แสดงในส่วน *ผลลัพธ์ที่คาดหวัง* ทำให้คุณมั่นใจว่าการแปลงสำเร็จ

## สรุปโค้ดทั้งหมด

การรวมส่วนต่าง ๆ เข้าด้วยกันจะได้โปรแกรมแบบ self‑contained ที่คุณสามารถคัดลอกไปใส่ในแอปพลิเคชันคอนโซลได้:

```csharp
using System;
using System.IO;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Paths – adjust to your environment
        string inputPath  = @"YOUR_DIRECTORY\input.xlsx";
        string outputPath = @"YOUR_DIRECTORY\Exported.txt";

        // Load workbook
        Workbook workbook = new Workbook(inputPath);
        Worksheet sheet = workbook.Worksheets[0];

        // Configure export options
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            DateTimeFormat = "yyyy-MM-dd",
            NumberFormat   = "#,##0.00",
            Separator      = '\t' // tab delimiter
        };

        // Apply options and export
        sheet.ExportTableOptions = exportOptions;
        sheet.ExportDataTable(outputPath);

        // Simple verification
        string firstLine = File.ReadLines(outputPath).First();
        Console.WriteLine($"Export completed. First line: {firstLine}");
    }
}
```

คอมไพล์และรันโปรแกรม; ไฟล์ `Exported.txt` จะปรากฏในไดเรกทอรีเดียวกับเวิร์กบุ๊กต้นฉบับ

## ขั้นตอนต่อไปและหัวข้อที่เกี่ยวข้อง

* **Export worksheet as text file** – ทดลองใช้ตัวคั่นที่ต่างกัน, การเข้ารหัส (UTF‑8 vs. ASCII) และรูปแบบการขึ้นบรรทัดใหม่เพื่อความเข้ากันได้ข้ามแพลตฟอร์ม
* **Bulk conversion** – วนลูปผ่าน `workbook.Worksheets` เพื่อสร้างไฟล์ข้อความแยกสำหรับแต่ละแท็บ
* **Integration with databases** – ส่งข้อความที่สร้างขึ้นโดยตรงไปยังการดำเนินการ bulk‑insert สำหรับ SQL Server หรือ PostgreSQL
* 

## สิ่งที่คุณควรเรียนต่อไป?

บทเรียนต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดซึ่งต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งข้อมูลมีตัวอย่างโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายขั้นตอนเพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจวิธีการทำงานแบบอื่นในโปรเจกต์ของคุณ

- [วิธีส่งออกไฟล์ Excel ใน .NET ด้วย Aspose.Cells&#58; คู่มือฉบับสมบูรณ์](/cells/english/net/workbook-operations/export-excel-files-net-aspose-cells-guide/)
- [วิธีส่งออกแถว Excel ที่มองเห็นได้ด้วย Aspose.Cells สำหรับ .NET&#58; คู่มือขั้นตอนต่อขั้น](/cells/english/net/workbook-operations/export-visible-rows-aspose-cells-dotnet/)
- [วิธีส่งออกแผนภูมิ Excel เป็น PDF ด้วย Aspose.Cells สำหรับ .NET&#58; คู่มือขั้นตอนต่อขั้น](/cells/english/net/workbook-operations/export-excel-charts-pdf-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}