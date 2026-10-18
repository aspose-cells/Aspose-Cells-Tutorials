---
category: general
date: 2026-03-01
description: แปลง Excel เป็น PowerPoint อย่างรวดเร็วด้วย C# . เรียนรู้วิธีสร้าง PowerPoint
  จากไฟล์ Excel ด้วย Aspose.Cells เพียงไม่กี่บรรทัดของโค้ด.
draft: false
keywords:
- convert excel to powerpoint
- generate powerpoint from excel
- convert xlsx to pptx
- how to convert excel
- create pptx from excel
language: th
og_description: แปลง Excel เป็น PowerPoint ด้วย C#. คู่มือนี้จะแสดงวิธีสร้าง PowerPoint
  จากไฟล์ Excel โดยใช้ Aspose.Cells พร้อมโค้ดเต็มและเคล็ดลับ
og_title: แปลง Excel เป็น PowerPoint – คอร์สสอน C# อย่างครบถ้วน
tags:
- C#
- Aspose.Cells
- Excel
- PowerPoint
title: แปลง Excel เป็น PowerPoint – คู่มือ C# ขั้นตอนต่อขั้นตอน
url: /th/net/converting-excel-files-to-other-formats/convert-excel-to-powerpoint-step-by-step-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# แปลง Excel เป็น PowerPoint – คำแนะนำ C# ทีละขั้นตอน

เคยต้องการ **แปลง Excel เป็น PowerPoint** แต่ไม่รู้ว่าจะเริ่มต้นอย่างไรหรือไม่? คุณไม่ได้อยู่คนเดียว—นักพัฒนาหลายคนเจออุปสรรคนี้เมื่อต้องเปลี่ยนสเปรดชีตที่เต็มไปด้วยข้อมูลให้กลายเป็นสไลด์ที่พร้อมนำเสนอ  

ข่าวดีคือ ด้วยไม่กี่บรรทัดของ C# คุณสามารถ **สร้าง PowerPoint จาก Excel** ได้โดยอัตโนมัติ ไม่ต้องคัดลอก‑วางด้วยมือ ในบทแนะนำนี้เราจะเดินผ่านกระบวนการทั้งหมด ตั้งแต่การโหลดไฟล์ `.xlsx` ไปจนถึงการบันทึกไฟล์ `.pptx` ที่พร้อมเปิดใน Microsoft PowerPoint หรือโปรแกรมดูที่รองรับอื่น ๆ

> **สิ่งที่คุณจะได้:** โปรแกรมที่สามารถรันได้ซึ่งโหลดเวิร์กบุ๊ก Excel, ตั้งค่าตัวเลือกการบันทึก PowerPoint, และเขียนไฟล์ PowerPoint ออกมา—ทั้งหมดโดยใช้ไลบรารี Aspose.Cells

## สิ่งที่คุณต้องมี

- **.NET 6.0** หรือใหม่กว่า (โค้ดนี้ยังทำงานบน .NET Framework 4.7+ ด้วย)  
- **Aspose.Cells for .NET** – สามารถติดตั้งจาก NuGet (`Install-Package Aspose.Cells`)  
- ความเข้าใจพื้นฐานของ C# (ไม่มีอะไรซับซ้อน เพียง `using` statements ปกติ)  
- ไฟล์ Excel (`input.xlsx`) ที่คุณต้องการแปลงเป็นชุดสไลด์  

เท่านี้เอง ไม่ต้องใช้เครื่องมือของบุคคลที่สามเพิ่มเติม ไม่ต้องใช้ COM interop ไม่ต้องทำ Automation ของ PowerPoint ที่ยุ่งยาก มาเริ่มกันเลย

![แปลง Excel เป็น PowerPoint workflow](convert-excel-to-powerpoint.png "แปลง Excel เป็น PowerPoint")

*ข้อความแทนภาพ: แผนภาพการทำงานแปลง Excel เป็น PowerPoint*

## แปลง Excel เป็น PowerPoint ด้วย Aspose.Cells

### ขั้นตอนที่ 1 – โหลดเวิร์กบุ๊ก Excel

สิ่งแรกที่ต้องทำคือดึงสเปรดชีตเข้ามาในหน่วยความจำ Aspose.Cells ทำให้เรื่องนี้ง่ายเพียงเรียกคอนสตรัคเตอร์ `Workbook` แล้วส่งพาธของไฟล์เข้าไป

```csharp
using Aspose.Cells;
using System;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Load the Excel workbook
            string inputPath = @"YOUR_DIRECTORY\input.xlsx";
            Workbook workbook = new Workbook(inputPath);
```

**ทำไมจึงสำคัญ:** การโหลดเวิร์กบุ๊กทำให้เราสามารถเข้าถึงทุกแผ่นงาน, แผนภูมิ, และแม้แต่รูปภาพที่ฝังอยู่ จากนั้นเราจึงเลือกว่าจะเก็บหรือทิ้งอะไรก่อนทำการแปลง

### ขั้นตอนที่ 2 – ตั้งค่าตัวเลือกการบันทึก Presentation

Aspose.Cells รองรับหลายรูปแบบการส่งออก และสำหรับ PowerPoint เราใช้ `PresentationSaveOptions` วัตถุนี้ช่วยให้เรากำหนด `SaveFormat.Pptx` และปรับตั้งค่าที่เป็นประโยชน์บางอย่าง เช่น การฝังแมโครหรือการคงความกว้างของคอลัมน์เดิม

```csharp
            // Step 2: Set up presentation save options for PowerPoint format
            PresentationSaveOptions saveOptions = new PresentationSaveOptions(SaveFormat.Pptx)
            {
                // Optional: keep the original Excel formatting as much as possible
                // (true by default, but we set it explicitly for clarity)
                KeepOriginalFormatting = true
            };
```

**ทำไมจึงสำคัญ:** หากไม่ได้ตั้งค่าที่เหมาะสม สไลด์ที่ได้อาจดูบีบอัดหรือสูญเสียสไตล์ การบอก Aspose.Cells ว่าเราต้องการไฟล์ PPTX แท้ ๆ จะทำให้การแปลงรักษาเลย์เอาต์ของ Excel ได้อย่างถูกต้อง

### ขั้นตอนที่ 3 – บันทึกเวิร์กบุ๊กเป็น PowerPoint Presentation

ตอนนี้จุดมุ่งหมายสำเร็จแล้ว การเรียก `Save` ครั้งเดียวจะเขียนไฟล์ `.pptx` ที่สะท้อนแผ่นงานแรกของเวิร์กบุ๊ก (หรือทั้งหมด ขึ้นอยู่กับเวอร์ชันของไลบรารี) สำหรับสถานการณ์ส่วนใหญ่ แผ่นแรกก็เพียงพอ แต่คุณสามารถทดลองเพิ่มได้ในภายหลัง

```csharp
            // Step 3: Save the workbook as a PowerPoint presentation
            string outputPath = @"YOUR_DIRECTORY\output.pptx";
            workbook.Save(outputPath, saveOptions);

            Console.WriteLine($"Success! '{outputPath}' has been created.");
        }
    }
}
```

**สิ่งที่คุณจะเห็น:** เปิด `output.pptx` ใน PowerPoint แล้วคุณจะพบว่าแต่ละแผ่นงานถูกแปลงเป็นสไลด์แล้ว เซลล์ข้อความกลายเป็นกล่องข้อความ, แผนภูมิกลายเป็นแผนภูมิ PowerPoint เนทีฟ, และรูปภาพยังคงความละเอียดเดิม

## เคล็ดลับการตั้งค่าโปรเจกต์เพื่อสร้าง PowerPoint จาก Excel

- **NuGet Install:** รัน `dotnet add package Aspose.Cells` จากโฟลเดอร์โปรเจกต์ของคุณ จะดึงเวอร์ชันล่าสุดที่เสถียร (ณ มีนาคม 2026, เวอร์ชัน 23.10)  
- **Target Platform:** หากคุณใช้ .NET Core ตรวจสอบให้ `csproj` ของคุณมี `<TargetFramework>net6.0</TargetFramework>`  
- **File Paths:** ใช้ `Path.Combine` เพื่อความปลอดภัยข้ามแพลตฟอร์ม โดยเฉพาะเมื่อโค้ดทำงานบนคอนเทนเนอร์ Linux  

```csharp
using System.IO;

// Example of safe path building
string baseDir = AppDomain.CurrentDomain.BaseDirectory;
string inputPath = Path.Combine(baseDir, "input.xlsx");
string outputPath = Path.Combine(baseDir, "output.pptx");
```

## แปลง Xlsx เป็น Pptx – จัดการหลายแผ่นงาน

โดยค่าเริ่มต้น Aspose.Cells จะ **แปลงเฉพาะแผ่นงานที่ใช้งานอยู่** หากคุณต้องการสไลด์ต่อแผ่นงาน สามารถวนลูปผ่านคอลเลกชันและบันทึกแต่ละแผ่นงานแยกกันได้:

```csharp
for (int i = 0; i < workbook.Worksheets.Count; i++)
{
    Worksheet sheet = workbook.Worksheets[i];
    sheet.IsSelected = true; // Make this sheet the active one
    string slidePath = Path.Combine(baseDir, $"Slide_{i + 1}.pptx");
    workbook.Save(slidePath, saveOptions);
}
```

**เคล็ดลับ:** หลังจากแต่ละรอบวนลูป ให้เรียก `workbook.Worksheets[i].IsSelected = false` หากคุณตั้งใจจะใช้วัตถุ `Workbook` เดียวกันสำหรับการทำงานอื่นต่อไป

## วิธีแปลง Excel – จัดการไฟล์ขนาดใหญ่

เวิร์กบุ๊กขนาดใหญ่ (หลายร้อยเมกะไบต์) อาจทำให้หน่วยความจำตึงเครียด เทคนิคต่อไปนี้ช่วยให้กระบวนการทำงานได้อย่างราบรื่น:

1. **เปิดใช้งาน Streaming:** `WorkbookSettings.MemorySetting = MemorySetting.MemoryPreference;` ทำให้ Aspose.Cells ใช้ไฟล์ชั่วคราวแทนการโหลดทั้งหมดเข้าสู่ RAM  
2. **ข้ามแถว/คอลัมน์ที่ว่าง:** ตั้งค่า `saveOptions.IgnoreEmptyRows = true` เพื่อลดความรกของสไลด์  
3. **ปรับขนาดรูปภาพ:** หาก Excel ของคุณมีรูปความละเอียดสูง สามารถลดขนาดก่อนแปลงด้วย `ImageResizeOptions`  

```csharp
workbook.Settings.MemorySetting = MemorySetting.MemoryPreference;
saveOptions.IgnoreEmptyRows = true;
saveOptions.ImageResizeOptions = new ImageResizeOptions
{
    Width = 1024,
    Height = 768,
    ResizeMode = ResizeMode.Proportional
};
```

## สร้าง Pptx จาก Excel – ตรวจสอบผลลัพธ์

หลังจากการเรียก `Save` เสร็จสิ้น คุณควรตรวจสอบว่าไฟล์ใช้งานได้หรือไม่:

```csharp
if (File.Exists(outputPath))
{
    var fileInfo = new FileInfo(outputPath);
    Console.WriteLine($"File size: {fileInfo.Length / 1024} KB");
    // Optionally launch PowerPoint automatically (Windows only)
    System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo
    {
        FileName = outputPath,
        UseShellExecute = true
    });
}
else
{
    Console.Error.WriteLine("Something went wrong – the PPTX was not created.");
}
```

การเปิดไฟล์ควรแสดงชุดสไลด์ที่สะท้อนเลย์เอาต์ของสเปรดชีตต้นฉบับอย่างครบถ้วน รวมถึงแผนภูมิ, ตาราง, และรูปภาพที่ฝังไว้

## คำถามที่พบบ่อย & กรณีขอบเขตพิเศษ

| คำถาม | คำตอบ |
|----------|--------|
| *สามารถคงแมโครของ Excel ไว้ได้หรือไม่?* | ไม่ได้ เนื่องจาก PowerPoint ไม่รองรับ VBA แมโครจาก Excel คุณต้องสร้างการทำงานอัตโนมัติใน PowerPoint เอง |
| *ส่วนคอมเมนต์ของเซลล์ล่ะ?* | จะถูกแปลงเป็นกล่องข้อความแยกบนสไลด์ แต่คุณสามารถซ่อนได้โดยตั้งค่า `saveOptions.IncludeCellComments = false` |
| *สูตรจะถูกประเมินหรือไม่?* | ใช่—Aspose.Cells จะประเมินสูตรก่อนแปลง ดังนั้นสไลด์จะแสดงค่าที่คำนวณแล้ว ไม่ใช่สูตร |
| *มีวิธีปรับแต่งดีไซน์ของสไลด์หรือไม่?* | คุณสามารถใช้เทมเพลต PowerPoint หลังการแปลงโดยใช้คลาส `Presentation` จาก Aspose.Slides แล้วคัดลอกสไลด์ที่สร้างไว้เข้าไปในเทมเพลตนั้น |

## ตัวอย่างทำงานเต็มรูปแบบ (โค้ดทั้งหมดในที่เดียว)

```csharp
using Aspose.Cells;
using System;
using System.IO;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Build safe file paths
            string baseDir = AppDomain.CurrentDomain.BaseDirectory;
            string inputPath = Path.Combine(baseDir, "input.xlsx");
            string outputPath = Path.Combine(baseDir, "output.pptx");

            // Load the Excel workbook
            Workbook workbook = new Workbook(inputPath);

            // Optional: improve memory usage for huge files
            workbook.Settings.MemorySetting = MemorySetting.MemoryPreference;

            // Configure PowerPoint save options
            PresentationSaveOptions saveOptions = new PresentationSaveOptions(SaveFormat.Pptx)
            {
                KeepOriginalFormatting = true,
                IgnoreEmptyRows = true,
                ImageResizeOptions = new ImageResizeOptions
                {
                    Width = 1024,
                    Height = 768,
                    ResizeMode = ResizeMode.Proportional
                }
            };

            // Save as PowerPoint
            workbook.Save(outputPath, saveOptions);

            // Verify the result
            if (File.Exists(outputPath))
            {
                Console.WriteLine($"Success! '{outputPath}' created ({new FileInfo(outputPath).Length / 1024} KB).");
                // Open the file automatically (Windows only)
                System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo
                {
                    FileName = outputPath,
                    UseShellExecute = true
                });
            }
            else
            {
                Console.Error.WriteLine("Failed to create the PowerPoint file.");
            }
        }
    }
}
```

รันโปรแกรม แล้วคุณจะได้ไฟล์ `.pptx` ใหม่พร้อมใช้สำหรับการประชุมกับลูกค้า, การนำเสนอในห้องบอร์ด, หรือการสรุปภายในองค์กร

## สรุป

ตอนนี้คุณรู้แล้วว่า **วิธีแปลง Excel เป็น PowerPoint** ด้วย C# และ Aspose.Cells ขั้นตอนหลัก—โหลดเวิร์กบุ๊ก, ตั้งค่า `PresentationSaveOptions`, และเรียก `Save`—เป็นเรื่องง่าย แม้บทแนะนำนี้จะครอบคลุมรายละเอียดเพิ่มเติมเช่นการจัดการหน่วยความจำ, การสร้าง PowerPoint จาก Excel, และเคล็ดลับอื่น ๆ

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}