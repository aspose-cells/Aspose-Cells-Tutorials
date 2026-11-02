---
category: general
date: 2026-02-26
description: วิธีส่งออก Excel เป็นไฟล์ txt ที่คั่นด้วยแท็บโดยใช้ C#. เรียนรู้การส่งออก
  Excel เป็นแท็บ, แปลง Excel เป็น txt, และส่งออก Excel ด้วยตัวคั่นในสามขั้นตอนง่าย
  ๆ.
draft: false
keywords:
- how to export excel
- export excel as tab
- convert excel to txt
- export excel with delimiter
- export excel range
language: th
og_description: วิธีส่งออก Excel ไปเป็นไฟล์ txt ที่คั่นด้วยแท็บโดยใช้ C# บทเรียนนี้แสดงการส่งออก
  Excel เป็นแท็บ, แปลง Excel เป็น txt, และส่งออก Excel พร้อมตัวคั่น.
og_title: วิธีส่งออก Excel – คู่มือข้อความแยกด้วยแท็บ
tags:
- csharp
- excel
- file-conversion
title: วิธีส่งออก Excel – คู่มือข้อความแยกด้วยแท็บ
url: /th/net/converting-excel-files-to-other-formats/how-to-export-excel-tab-delimited-text-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีการส่งออก Excel – คำแนะนำเต็ม C# 

เคยสงสัยไหมว่า **วิธีการส่งออก excel** ข้อมูลเป็นไฟล์ข้อความธรรมดาโดยไม่สูญเสียรูปแบบ? บางทีคุณอาจต้องการ TSV (ค่าที่คั่นด้วยแท็บ) อย่างรวดเร็วสำหรับสายงานข้อมูล, หรือคุณกำลังส่งข้อมูลให้ระบบเก่าที่อ่านได้เฉพาะ `.txt` เท่านั้น. ไม่ว่ากรณีใด คุณก็ไม่ได้อยู่คนเดียว—นักพัฒนามักเจออุปสรรคนี้เมื่อนำข้อมูลออกจากสเปรดชีต.

ข่าวดีคืออะไร? เพียงสามขั้นตอนง่าย ๆ คุณสามารถ **export excel as tab**‑delimited text, **convert excel to txt**, และแม้แต่เลือกตัวคั่นแบบกำหนดเองหากคุณเปลี่ยนใจในภายหลัง. ด้านล่างคุณจะเห็นตัวอย่าง C# ที่สามารถรันได้เต็มรูปแบบ, เหตุผลที่แต่ละบรรทัดสำคัญ, และเคล็ดลับหลายอย่างเพื่อหลีกเลี่ยงข้อผิดพลาดทั่วไป.

> **Pro tip:** วิธีนี้ทำงานกับไลบรารี Aspose.Cells ที่เป็นที่นิยม, แต่แนวคิดสามารถนำไปใช้กับ .NET Excel API ใดก็ได้ที่มีเมธอดแบบ `ExportTable`‑style.

## สิ่งที่คุณต้องการ

- **.NET 6+** (หรือ .NET Framework 4.6+). โค้ดจะคอมไพล์บนรันไทม์ที่ทันสมัยใดก็ได้.
- **Aspose.Cells for .NET** (ทดลองใช้ฟรีหรือแบบมีลิขสิทธิ์). ติดตั้งผ่าน NuGet: `dotnet add package Aspose.Cells`.
- ไฟล์เวิร์กบุ๊กอินพุตชื่อ `input.xlsx` ที่วางไว้ในโฟลเดอร์ที่คุณควบคุม.
- ความอยากรู้อยากเห็นเล็กน้อย—ไม่จำเป็นต้องเข้าใจโครงสร้างภายในของ Excel อย่างลึกซึ้ง.

หากคุณมีทั้งหมดนี้แล้ว, ไปที่ขั้นตอนการแก้ปัญหาตรงต่อกันเลย.

## ขั้นตอนที่ 1 – โหลดเวิร์กบุ๊กที่คุณต้องการส่งออก

ก่อนอื่นเราจะสร้างอ็อบเจ็กต์ `Workbook` ที่ชี้ไปยังไฟล์ต้นทาง. อ็อบเจ็กต์นี้แทนไฟล์ Excel ทั้งไฟล์, รวมถึงแผ่นงานทั้งหมด, ช่วงที่ตั้งชื่อ, และการจัดรูปแบบ.

```csharp
using Aspose.Cells;

// Step 1: Load the workbook that contains the data to export
Workbook workbook = new Workbook(@"C:\Data\input.xlsx");
```

*ทำไมสิ่งนี้ถึงสำคัญ:*  
การโหลดเวิร์กบุ๊กทำให้คุณเข้าถึงคอลเลกชันแผ่นงาน (`workbook.Worksheets`). หากไม่มีอ็อบเจ็กต์นี้คุณจะไม่สามารถอ้างอิงเซลล์, ช่วง, หรือการตั้งค่าการส่งออกได้.

> **Note:** หากไฟล์ของคุณอยู่บนแชร์เครือข่าย, ให้เพิ่ม `\\` หรือใช้เส้นทาง UNC—Aspose.Cells จะจัดการได้อย่างดี.

## ขั้นตอนที่ 2 – กำหนดค่าตัวเลือกการส่งออก (ค่าเป็นสตริง & ตัวคั่นแท็บ)

ต่อไปเราจะบอกไลบรารีว่าต้องการให้ข้อมูลเขียนออกมาอย่างไร. การตั้งค่า `ExportAsString = true` จะบังคับให้ทุกเซลล์ถูกจัดการเป็นสตริงธรรมดา, ซึ่งจะขจัดรูปแบบตัวเลขที่ขึ้นกับภาษาของ Excel. ส่วน `Delimiter = "\t"` คือหัวใจของ **export excel as tab**.

```csharp
// Step 2: Configure the export options – export values as strings and use a tab delimiter
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true,   // ensures numbers become plain text, not scientific notation
    Delimiter = "\t"         // tab character – perfect for TSV files
};
```

*ทำไมสิ่งนี้ถึงสำคัญ:*  
หากคุณละเว้น `ExportAsString`, เซลล์ที่มีค่า `12345` อาจกลายเป็น `12,345` ในบางภาษาท้องถิ่น, ทำให้ตัวแยกข้อมูลลำดับถัดไปทำงานผิดพลาด. ตัวคั่นสามารถเปลี่ยนเป็นคอมม่า, พาย (`|`), หรืออักขระใดก็ได้หากคุณในภายหลังต้องการ **export excel with delimiter** ที่ไม่ใช่แท็บ.

## ขั้นตอนที่ 3 – ส่งออกช่วงเฉพาะไปยังไฟล์ข้อความ

สุดท้ายเราจะเลือกช่วงที่ต้องการ (`A1:D10` ในตัวอย่างนี้) และเขียนลงใน `out.txt`. เมธอด `ExportTable` ทำงานหนักทั้งหมด: อ่านเซลล์, ใช้ตัวเลือก, และสตรีมผลลัพธ์ไปยังดิสก์.

```csharp
// Step 3: Export the range A1:D10 from the first worksheet to a text file
Worksheet sheet = workbook.Worksheets[0]; // first worksheet (index 0)
sheet.Cells.ExportTable("A1", "D10", @"C:\Data\out.txt", exportOptions);
```

หลังจากรันเสร็จ, คุณจะพบไฟล์ `out.txt` ที่มีเนื้อหาแบบนี้:

```
Name    Age    City    Score
Alice   30     NY      85
Bob     25     LA      90
...
```

แต่ละคอลัมน์ถูกคั่นด้วย **แท็บ**, ทำให้พร้อมใช้กับ `awk`, `PowerShell`, หรือเครื่องมือที่รองรับ CSV ใด ๆ ที่ยอมรับแท็บ.

### การตรวจสอบอย่างรวดเร็ว

เปิดไฟล์ที่สร้างขึ้นในโปรแกรมแก้ไขข้อความธรรมดา (Notepad, VS Code) แล้วตรวจสอบ:

1. คอลัมน์จัดเรียงตรงกันเมื่อเปิด “Show whitespace”.
2. ไม่พบเครื่องหมายอัญประกาศหรือคอมม่าเพิ่มเติม.
3. เซลล์ตัวเลขทั้งหมดแสดงผลตรงกับที่อยู่ใน Excel (ขอบคุณ `ExportAsString`).

หากมีสิ่งใดดูแปลก, ตรวจสอบอีกครั้งว่าเวิร์กบุ๊กต้นทางไม่ได้ซ่อนแถว/คอลัมน์, และตรวจสอบว่าคุณอ้างอิงดัชนีแผ่นงานที่ถูกต้อง.

## การเปลี่ยนแปลงทั่วไป & กรณีขอบ

### การส่งออกแผ่นงานทั้งหมด

หากคุณต้องการ **export excel range** ที่ครอบคลุมทั้งแผ่นงาน, คุณสามารถใช้ `sheet.Cells.MaxDisplayRange`:

```csharp
var maxRange = sheet.Cells.MaxDisplayRange;
sheet.Cells.ExportTable(maxRange.FirstRow, maxRange.FirstColumn,
                       maxRange.RowCount, maxRange.ColumnCount,
                       @"C:\Data\fullSheet.txt", exportOptions);
```

### การใช้ตัวคั่นอื่น

การเปลี่ยนจากแท็บเป็นพาย (`|`) ทำได้ง่ายเพียงเปลี่ยนบรรทัดเดียว:

```csharp
exportOptions.Delimiter = "|"; // now we have a pipe‑delimited file
```

ซึ่งทำให้สอดคล้องกับสถานการณ์ **export excel with delimiter** โดยไม่ต้องเขียนโค้ดอื่นใหม่.

### การจัดการไฟล์ขนาดใหญ่ (> 100 MB)

สำหรับเวิร์กบุ๊กขนาดใหญ่, ควรสตรีมการส่งออกเพื่อหลีกเลี่ยงการโหลดทั้งหมดเข้าสู่หน่วยความจำ:

```csharp
using (FileStream fs = new FileStream(@"C:\Data\largeOut.txt", FileMode.Create, FileAccess.Write))
{
    sheet.Cells.ExportTable("A1", "Z5000", fs, exportOptions);
}
```

### การแปลงหลายแผ่นงานในหนึ่งรอบ

หากคุณต้องการ **convert excel to txt** สำหรับหลายแผ่นงาน, ให้วนลูปผ่านแต่ละแผ่น:

```csharp
for (int i = 0; i < workbook.Worksheets.Count; i++)
{
    string outPath = $@"C:\Data\Sheet{i + 1}.txt";
    workbook.Worksheets[i].Cells.ExportTable("A1", "D10", outPath, exportOptions);
}
```

แต่ละแผ่นจะได้ไฟล์ TSV ของตัวเอง—สะดวกสำหรับงานแบบแบตช์.

## ตัวอย่างทำงานเต็มรูปแบบ (พร้อมคัดลอก‑วาง)

ด้านล่างเป็นโปรแกรมทั้งหมด, พร้อมคอมไพล์. เพียงเปลี่ยนเส้นทางไฟล์ให้เป็นของคุณเอง.

```csharp
using System;
using Aspose.Cells;

namespace ExcelToTxtDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the workbook
            string inputPath = @"C:\Data\input.xlsx";
            Workbook workbook = new Workbook(inputPath);

            // 2️⃣ Set export options – strings + tab delimiter
            ExportTableOptions exportOptions = new ExportTableOptions
            {
                ExportAsString = true,
                Delimiter = "\t"
            };

            // 3️⃣ Export range A1:D10 from the first worksheet
            Worksheet sheet = workbook.Worksheets[0];
            string outputPath = @"C:\Data\out.txt";
            sheet.Cells.ExportTable("A1", "D10", outputPath, exportOptions);

            Console.WriteLine($"Export complete! Check {outputPath}");
        }
    }
}
```

**ผลลัพธ์ที่คาดหวัง:** ไฟล์ชื่อ `out.txt` ที่แต่ละคอลัมน์คั่นด้วยอักขระแท็บ, และค่าของทุกเซลล์แสดงผลตรงกับที่อยู่ใน Excel.

## คำถามที่พบบ่อย

- **ทำงานกับไฟล์ .xls หรือไม่?**  
  ใช่. Aspose.Cells ตรวจจับรูปแบบโดยอัตโนมัติ, ดังนั้นคุณสามารถชี้ `Workbook` ไปที่ `.xls` เก่าและใช้โค้ดเดียวกันได้.

- **ถ้าข้อมูลของฉันมีแท็บล่ะ?**  
  แท็บภายในเซลล์จะถูกเก็บไว้, ซึ่งอาจทำให้ตัวแยก TSV ทำงานผิดพลาด. ในกรณีนั้น, พิจารณาเปลี่ยนเป็นตัวคั่นพาย (`|`) โดยอัปเดต `exportOptions.Delimiter`.

- **ฉันสามารถส่งออกสูตรแทนค่าปกติได้หรือไม่?**  
  ตั้งค่า `exportOptions.ExportAsString = false` และใช้ overload ของ `ExportTableOptions` ที่รวม `ExportFormula = true`. ผลลัพธ์จะมีข้อความสูตรดิบ.

- **มีวิธีข้ามแถวที่ซ่อนอยู่หรือไม่?**  
  มี. ตั้งค่า `exportOptions.ExportHiddenRows = false` (ค่าเริ่มต้นคือ `true`). แถวที่ซ่อนจะถูกละเว้นจากไฟล์ข้อความสุดท้าย.

## สรุป

ตอนนี้คุณมีสูตรที่มั่นคงและพร้อมใช้งานในระดับผลิตสำหรับ **how to export excel** ข้อมูลเป็นไฟล์ข้อความที่คั่นด้วยแท็บ, วิธี **export excel as tab**, และวิธี **convert excel to txt** พร้อมการควบคุมเต็มรูปแบบของตัวคั่นและการเลือกช่วง. ด้วยการใช้เมธอด `ExportTable` ของ Aspose.Cells คุณจะหลีกเลี่ยงการสร้าง CSV ด้วยตนเอง, รักษาความถูกต้องของข้อมูล, และทำให้ฐานโค้ดของคุณสะอาด.

พร้อมสำหรับความท้าทายต่อไปหรือยัง? ลอง:

- ส่งออกโดยตรงไปยัง `MemoryStream` สำหรับเว็บ API.  
- เพิ่มแถวหัวเรื่องแบบไดนามิกตามเนื้อหาแถวแรก.  
- ผสานรวมขั้นตอนนี้เข้าสู่ Azure Function ที่เฝ้าดู bucket ที่เก็บไฟล์ Excel ใหม่.

ลองใช้งาน, ปรับตัวคั่นตามต้องการ, แล้วให้ข้อมูลไหลไปยังที่ที่คุณต้องการ. ขอให้เขียนโค้ดอย่างสนุก!  

<img src="export-excel.png" alt="ตัวอย่างวิธีส่งออก excel" style="max-width:100%; height:auto;" />

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}