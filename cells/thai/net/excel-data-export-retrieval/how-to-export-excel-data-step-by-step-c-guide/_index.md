---
category: general
date: 2026-03-29
description: เรียนรู้วิธีส่งออกตาราง Excel เป็นข้อความธรรมดา, เขียนสตริงลงไฟล์, และแปลงตาราง
  Excel เป็น CSV หรือ TXT ด้วย C# รวมโค้ดเต็มและเคล็ดลับ.
draft: false
keywords:
- how to export excel
- write string to file
- convert excel table
- export table as csv
- save txt file c#
language: th
og_description: วิธีส่งออกตาราง Excel ไปเป็นไฟล์ข้อความใน C# รับโซลูชันเต็ม, โค้ด,
  และแนวปฏิบัติที่ดีที่สุดสำหรับการแปลงตาราง Excel และบันทึกไฟล์ TXT.
og_title: วิธีส่งออกข้อมูล Excel – คอร์สสอน C# อย่างครบถ้วน
tags:
- C#
- Excel
- File I/O
title: วิธีส่งออกข้อมูล Excel – คู่มือ C# ทีละขั้นตอน
url: /th/net/excel-data-export-retrieval/how-to-export-excel-data-step-by-step-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีส่งออกข้อมูล Excel – คู่มือ C# ฉบับสมบูรณ์

เคยสงสัย **how to export Excel** ว่าอย่างไรโดยไม่ต้องเปิดสเปรดชีตด้วยตนเองหรือไม่? บางครั้งคุณอาจต้องการดึงตารางไปเก็บในไฟล์ข้อความง่าย ๆ สำหรับระบบเก่า, หรือคุณต้องการส่งออก CSV อย่างรวดเร็วสำหรับกระบวนการวิเคราะห์ข้อมูล. ในบทเรียนนี้เราจะพาไปผ่านโซลูชันแบบครบวงจรที่ **writes a string to file** และแสดงให้คุณเห็นอย่างชัดเจนว่า **convert Excel table** ทำอย่างไรเป็นรูปแบบข้อความที่คั่นด้วยตัวคั่นโดยใช้ C#.

เราจะครอบคลุมทุกขั้นตอนตั้งแต่การโหลดเวิร์กบุ๊ก, การเลือกตารางที่ต้องการ, การกำหนดค่าตัวเลือกการส่งออก, และสุดท้ายการบันทึกผลลัพธ์เป็นไฟล์ `.txt`. เมื่อจบคุณจะสามารถ **export table as CSV** (หรือใช้ตัวคั่นใดก็ได้ที่คุณเลือก) และคุณยังจะได้เห็นเคล็ดลับเล็ก ๆ สำหรับโครงการ **saving txt file C#**. ไม่ต้องใช้เครื่องมือภายนอก—แค่แพ็กเกจ NuGet ไม่กี่ตัวและโค้ดเล็กน้อย.

---

## สิ่งที่คุณต้องเตรียม

- **.NET 6.0+** (หรือ .NET Framework 4.7.2 หากคุณต้องการแบบคลาสสิก)
- **Syncfusion.XlsIO** NuGet package (คลาส `ExportTableOptions` อยู่ที่นี่)
- IDE C# เบื้องต้น (Visual Studio, VS Code, Rider—ใช้ได้ทุกตัว)
- เวิร์กบุ๊ก Excel ที่มีอย่างน้อยหนึ่งตาราง (เราจะใช้ `ws.Tables[0]` ในตัวอย่าง)

> เคล็ดลับ: หากคุณยังไม่มีไลบรารี Syncfusion, ให้รัน  
> `dotnet add package Syncfusion.XlsIO.Net.Core` จากบรรทัดคำสั่ง.

## ขั้นตอนที่ 1 – เปิดเวิร์กบุ๊กและดึงตารางแรก  

สิ่งแรกที่ต้องทำคือโหลดไฟล์ Excel และรับอ้างอิงไปยังแผ่นงานที่มีตารางนั้น ขั้นตอนนี้สำคัญมากเพราะการทำ **convert excel table** ทำงานบนอ็อบเจกต์ `ITable` ไม่ใช่ช่วงเซลล์ดิบ.

```csharp
using Syncfusion.XlsIO;
using System.IO;

class ExcelExporter
{
    static void Main()
    {
        // Load the workbook (replace with your actual file path)
        using (ExcelEngine excelEngine = new ExcelEngine())
        {
            IApplication application = excelEngine.Excel;
            application.DefaultVersion = ExcelVersion.Xlsx;

            // Open the file
            FileStream stream = new FileStream(@"C:\Data\Sample.xlsx", FileMode.Open, FileAccess.Read);
            IWorkbook workbook = application.Workbooks.Open(stream);
            IWorksheet ws = workbook.Worksheets[0];   // First worksheet
```

*ทำไมจึงสำคัญ:* การเปิดเวิร์กบุ๊กด้วย `using` ทำให้ทรัพยากรที่ไม่ได้จัดการถูกปล่อยออกไป, ป้องกันปัญหาไฟล์ล็อกเมื่อคุณพยายาม **write string to file** ในภายหลัง.

## ขั้นตอนที่ 2 – กำหนดค่าตัวเลือกการส่งออก (ข้อความธรรมดา, ไม่รวมหัวข้อ, ตัวคั่นเซมิโคลอน)  

ตอนนี้เราบอก Syncfusion ว่าเราต้องการให้ตารางถูกแปลงเป็นข้อความอย่างไร `ExportTableOptions` ให้คุณเปิด/ปิดการรวมหัวข้อ, เลือกตัวคั่น, และกำหนดว่าจะรับเป็นสตริงหรืออาร์เรย์ไบต์.

```csharp
            // Step 2: Configure export options – plain text, omit headers, ';' delimiter
            var exportOptions = new ExportTableOptions
            {
                ExportAsString = true,      // Returns a string we can write directly
                IncludeHeaders = false,     // Skip column headers if you don’t need them
                Delimiter = ";"             // Change to ',' for classic CSV
            };
```

*ทำไมจึงสำคัญ:* การตั้งค่า `IncludeHeaders = false` มักสอดคล้องกับความคาดหวังของระบบ downstream ที่รู้ลำดับคอลัมน์แล้ว การเปลี่ยนตัวคั่นคือวิธีที่คุณ **export table as CSV** ด้วยตัวคั่นที่กำหนดเอง.

## ขั้นตอนที่ 3 – ส่งออกตารางเป็นสตริง  

เมื่อกำหนดตัวเลือกเรียบร้อยแล้ว เราเรียก `ExportToString`. เมธอดนี้ดึงตารางทั้งหมด (รวมทุกแถว) และคืนค่าสตริงเดียวที่พร้อมสำหรับการเขียนไฟล์.

```csharp
            // Step 3: Export the first table to a string using the configured options
            ITable firstTable = ws.Tables[0];               // Access the first table
            string tableText = firstTable.ExportToString(exportOptions);
```

*ทำไมจึงสำคัญ:* การเรียก `ExportToString` ทำงานหนักในการแปลงกริด Excel ให้เป็นรูปแบบที่คั่นด้วยตัวคั่น. มันเคารพ `Delimiter` ที่คุณตั้งค่า, ดังนั้นคุณจะได้ผลลัพธ์ **export table as csv** ที่สะอาดโดยไม่ต้องประมวลผลเพิ่มเติม.

## ขั้นตอนที่ 4 – เขียนข้อความที่ส่งออกไปยังไฟล์  

สุดท้ายเราบันทึกสตริงลงดิสก์ `File.WriteAllText` เป็นวิธีที่ง่ายที่สุดสำหรับ **save txt file C#**; มันจะสร้างไฟล์อัตโนมัติหากไฟล์ยังไม่มีและเขียนทับหากมีอยู่แล้ว.

```csharp
            // Step 4: Write the exported text to a file
            string outputPath = @"C:\Data\ExportedTable.txt";
            File.WriteAllText(outputPath, tableText);
            System.Console.WriteLine($"Table exported successfully to {outputPath}");
        }
    }
}
```

*ทำไมจึงสำคัญ:* การเขียนสตริงโดยตรงช่วยให้คุณหลีกเลี่ยงขั้นตอนการแปลงเพิ่มเติม. ไฟล์ตอนนี้มีแถวเช่น `Value1;Value2;Value3`, พร้อมสำหรับตัวแยกข้อมูล downstream ใด ๆ.

## ตัวอย่างทำงานเต็มรูปแบบ (รวมทุกขั้นตอนในที่เดียว)  

ด้านล่างเป็นโปรแกรมที่พร้อมคัดลอก‑วางครบถ้วนซึ่งรวมทุกอย่างที่เราได้พูดถึงไว้ มีการจัดการข้อผิดพลาดและคอมเมนต์เพื่อความชัดเจน.

```csharp
using Syncfusion.XlsIO;
using System;
using System.IO;

class ExcelExporter
{
    static void Main()
    {
        try
        {
            // 1️⃣ Load workbook and get first worksheet
            using (ExcelEngine excelEngine = new ExcelEngine())
            {
                IApplication app = excelEngine.Excel;
                app.DefaultVersion = ExcelVersion.Xlsx;

                string sourcePath = @"C:\Data\Sample.xlsx";
                using (FileStream fs = new FileStream(sourcePath, FileMode.Open, FileAccess.Read))
                {
                    IWorkbook wb = app.Workbooks.Open(fs);
                    IWorksheet ws = wb.Worksheets[0]; // first sheet

                    // 2️⃣ Set export options (plain text, no headers, ';' delimiter)
                    var opts = new ExportTableOptions
                    {
                        ExportAsString = true,
                        IncludeHeaders = false,
                        Delimiter = ";"
                    };

                    // 3️⃣ Export the first table to a string
                    ITable table = ws.Tables[0];
                    string csvText = table.ExportToString(opts);

                    // 4️⃣ Save the string to a .txt file
                    string destPath = @"C:\Data\ExportedTable.txt";
                    File.WriteAllText(destPath, csvText);

                    Console.WriteLine($"✅ Export complete! File saved at: {destPath}");
                }
            }
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"❌ Something went wrong: {ex.Message}");
        }
    }
}
```

**ผลลัพธ์ที่คาดหวัง** (เนื้อหาของ `ExportedTable.txt`):

```
John;Doe;35
Jane;Smith;28
Bob;Brown;42
```

แต่ละบรรทัดสอดคล้องกับแถวจากตาราง Excel ดั้งเดิม, โดยค่าต่าง ๆ คั่นด้วยเซมิโคลอน. หากคุณเปลี่ยน `Delimiter = ","` คุณจะได้ไฟล์ CSV แบบคลาสสิกแทน.

## คำถามทั่วไป & กรณีขอบ

### ถ้าเวิร์กบุ๊กของฉันมีหลายตารางล่ะ?  
คุณสามารถเปลี่ยน `ws.Tables[0]` เป็นดัชนีที่ต้องการ, หรือวนลูปผ่าน `ws.Tables` ได้:

```csharp
foreach (var tbl in ws.Tables)
{
    string txt = tbl.ExportToString(opts);
    // Save each table to a separate file or concatenate as needed
}
```

### จะรวมหัวคอลัมน์อย่างไร?  
ตั้งค่า `IncludeHeaders = true` ใน `ExportTableOptions`. สิ่งนี้มีประโยชน์เมื่อระบบ downstream ต้องการแถวหัวข้อ.

### สามารถส่งออกไปยังโฟลเดอร์อื่นแบบไดนามิกได้ไหม?  
ได้เลย. ใช้ `Path.Combine` กับ `Environment.GetFolderPath(Environment.SpecialFolder.Desktop)` หรือเส้นทางใด ๆ ที่ผู้ใช้ระบุ เพื่อทำให้โซลูชันยืดหยุ่นมากขึ้น.

### ไฟล์ขนาดใหญ่ล่ะ?  
สำหรับตารางขนาดใหญ่, ควรพิจารณา stream ผลลัพธ์แทนการโหลดสตริงทั้งหมดเข้าสู่หน่วยความจำ:

```csharp
using (StreamWriter writer = new StreamWriter(outputPath))
{
    writer.Write(table.ExportToString(opts));
}
```

### ทำงานบน .NET Core ได้หรือไม่?  
ใช่—Syncfusion.XlsIO รองรับ .NET 5/6/7. เพียงอ้างอิงแพ็กเกจ NuGet ที่เหมาะสมแล้วคุณก็พร้อมใช้งาน.

## เคล็ดลับมืออาชีพสำหรับการส่งออกที่เชื่อถือได้  

- **ตรวจสอบเส้นทางไฟล์** ก่อนเขียน. หากไดเรกทอรีหายจะทำให้เกิด `DirectoryNotFoundException`.  
- **ตรวจสอบ `ExportAsString`** เฉพาะเมื่อ ตารางพอใส่ในหน่วยความจำได้อย่างสบาย; หากไม่เช่นนั้นให้ใช้ `ExportToStream` สำหรับชุดข้อมูลขนาดใหญ่.  
- **ใส่ใจวัฒนธรรม**: หากข้อมูลของคุณมีคอมม่าเป็นตัวคั่นทศนิยม, เลือกเซมิโคลอน (`;`) หรือแท็บ (`\t`) เป็นตัวคั่นเพื่อหลีกเลี่ยงข้อผิดพลาดการแยก CSV.  
- **Version lock**: Syncfusion บางครั้งเปลี่ยนลายเซ็น API. ค้างเวอร์ชัน NuGet (`<PackageReference Include="Syncfusion.XlsIO.Net.Core" Version="21.2.0.44" />`) เพื่อให้การสร้างของคุณทำซ้ำได้.

## สรุป  

ในคู่มือนี้เราได้สาธิต **how to export Excel** ตารางเป็นไฟล์ข้อความธรรมดาโดยใช้ C#. ด้วยการโหลดเวิร์กบุ๊ก, กำหนดค่า `ExportTableOptions`, ส่งออกตารางเป็นสตริง, และสุดท้าย **writing the string to file**, คุณจะมีรูปแบบที่มั่นคงสำหรับงาน **convert excel table**, **export table as csv**, และ **save txt file C#**.

อย่าลังเลที่จะทดลอง—เปลี่ยนตัวคั่น, รวมหัวข้อ, หรือวนลูปหลายตาราง. วิธีเดียวกันนี้ใช้ได้สำหรับสร้างรายงาน CSV, ป้อนข้อมูลเข้าสู่ตัวแยกข้อมูลเก่า, หรือเพียงเก็บเนื้อหา spreadsheet เป็นไฟล์ข้อความขนาดเล็ก.

มีสถานการณ์อื่นที่คุณอยากจัดการไหม? บางทีคุณอาจต้องการ **write string to file** แบบอะซิงโครนัส, หรืออยากบีบอัดผลลัพธ์ทันที. ตรวจสอบบทเรียนต่อไปของเราเกี่ยวกับ *asynchronous file I/O in C#* และ *zipping files with .NET* เพื่อรักษาแรงต่อเนื่อง.

ขอให้เขียนโค้ดอย่างสนุก! 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}