---
category: general
date: 2026-10-01
description: เรียนรู้วิธีเพิ่มคุณสมบัติกำหนดเองลงในเวิร์กบุ๊ก Excel ด้วย Aspose.Cells
  คู่มือนี้ยังแสดงวิธีเพิ่มรหัสโครงการและอ่านคุณสมบัติกำหนดเอง
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add custom properties
- how to add custom
- excel custom properties
- add project id
- read custom properties
language: th
lastmod: 2026-10-01
og_description: เพิ่มคุณสมบัติเฉพาะให้กับไฟล์ Excel ด้วย Aspose.Cells. ทำตามบทเรียนฉบับเต็มนี้เพื่อเพิ่มรหัสโครงการ,
  ตั้งค่าข้อมูลผู้ตรวจสอบ, และอ่านคุณสมบัติเฉพาะโดยโปรแกรม.
og_image_alt: Screenshot of an Excel worksheet displaying custom properties added
  via Aspose.Cells
og_title: เพิ่มคุณสมบัติกำหนดเองในเวิร์กบุ๊ก Excel – คู่มือแบบทีละขั้นตอน
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Learn how to add custom properties to an Excel workbook using Aspose.Cells.
    This guide also shows how to add project ID and read custom properties.
  headline: How to add custom properties to an Excel workbook
  type: TechArticle
- description: Learn how to add custom properties to an Excel workbook using Aspose.Cells.
    This guide also shows how to add project ID and read custom properties.
  name: How to add custom properties to an Excel workbook
  steps:
  - name: Open the saved `DataWithProps.xlsb` file in Microsoft Excel.
    text: Open the saved `DataWithProps.xlsb` file in Microsoft Excel.
  - name: Go to **File → Info → Properties → Advanced Properties**.
    text: Go to **File → Info → Properties → Advanced Properties**.
  - name: Select the **Custom** tab.
    text: Select the **Custom** tab.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: วิธีเพิ่มคุณสมบัติที่กำหนดเองในเวิร์กบุ๊ก Excel
url: /th/net/document-properties/how-to-add-custom-properties-to-an-excel-workbook/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีเพิ่มคุณสมบัติเฉพาะลงในไฟล์ Excel workbook

หากคุณต้องการ **เพิ่มคุณสมบัติเฉพาะ** ลงในไฟล์ Excel workbook คำแนะนำนี้จะแสดงวิธีทำอย่างละเอียดด้วย Aspose.Cells for .NET คุณจะได้เรียนรู้วิธีเพิ่ม Project ID ตั้งชื่อผู้ตรวจสอบ และในภายหลัง **อ่านคุณสมบัติเฉพาะ** จากไฟล์

การทำงานกับเมตาดาต้าชนิดกำหนดเองช่วยให้คุณฝังข้อมูลเฉพาะธุรกิจลงในสเปรดชีตโดยตรง ทำให้ติดตามเจ้าของ รุ่น หรือบริบทอื่น ๆ ได้ง่ายโดยไม่ต้องดูแลฐานข้อมูลแยกต่างหาก ขั้นตอนต่อไปนี้ครอบคลุมกระบวนการทำงานตั้งแต่การสร้าง workbook จนถึงการบันทึกคุณสมบัติใหม่

## ข้อกำหนดเบื้องต้น

ก่อนเริ่มทำงาน โปรดตรวจสอบว่าคุณมี:

* .NET 6.0 หรือใหม่กว่า  
* ใบอนุญาต Aspose.Cells for .NET ที่ถูกต้อง (หรือทดลองใช้ฟรี)  
* Visual Studio 2022 (หรือ IDE สำหรับ C# ใดก็ได้)  

ไม่จำเป็นต้องติดตั้ง NuGet package เพิ่มเติมนอกจาก `Aspose.Cells`

## ขั้นตอนที่ 1: ตั้งค่าโครงการและนำเข้าเนมสเปซ

สร้างแอปพลิเคชันคอนโซลใหม่และเพิ่มการอ้างอิง Aspose.Cells:

```csharp
using System;
using Aspose.Cells;

namespace ExcelCustomPropertiesDemo
{
    class Program
    {
        static void Main()
        {
            // The rest of the code lives here
        }
    }
}
```

เนมสเปซ `Aspose.Cells` มีคลาส `Workbook` , `Worksheet` และ `CustomPropertyCollection` ที่เราจะใช้

## ขั้นตอนที่ 2: โหลด workbook ที่มีอยู่ (หรือสร้างใหม่)

คุณสามารถเริ่มจากไฟล์ `.xlsb` ที่มีอยู่หรือสร้าง workbook ใหม่ ตัวอย่างด้านล่างโหลดไฟล์ชื่อ **Data.xlsb** ที่อยู่ในโฟลเดอร์ `YOUR_DIRECTORY`

```csharp
// Load the existing workbook
var workbookPath = @"YOUR_DIRECTORY\Data.xlsb";
var workbook = new Workbook(workbookPath);
```

หากไฟล์ไม่มีอยู่ ให้เปลี่ยนโค้ดเป็น `new Workbook();` เพื่อสร้าง workbook ว่าง

## ขั้นตอนที่ 3: เพิ่มคุณสมบัติเฉพาะลงใน worksheet แรก

การดำเนินการหลักคือ **เพิ่มคุณสมบัติเฉพาะ** ลงใน worksheet Aspose.Cells เก็บคุณสมบัติเฉพาะในคอลเลกชันที่ทำงานคล้ายพจนานุกรม

```csharp
// Get the first worksheet (index 0)
var worksheet = workbook.Worksheets[0];

// Add a numeric ProjectId property
worksheet.CustomProperties.Add("ProjectId", 12345);

// Add a string Reviewer property
worksheet.CustomProperties.Add("Reviewer", "John Doe");

// Optional: add a DateTime property for the creation timestamp
worksheet.CustomProperties.Add("CreatedOn", DateTime.UtcNow);
```

เหตุผลที่เราใช้ `CustomProperties.Add` แทน `CustomProperties["Name"] = value` คือเมธอด `Add` จะสร้างรายการหากไม่มีอยู่และรับประกันว่าชนิดข้อมูลที่เก็บถูกต้อง วิธีนี้ช่วยป้องกันการไม่ตรงกันของชนิดข้อมูลที่อาจทำให้เกิดข้อผิดพลาดขณะรันเมื่ออ่านค่าในภายหลัง

## ขั้นตอนที่ 4: บันทึก workbook พร้อมคุณสมบัติใหม่

หลังจากที่คุณแทรกเมตาดาต้าแล้ว ให้บันทึกการเปลี่ยนแปลงลงไฟล์ใหม่เพื่อไม่ให้ไฟล์ต้นฉบับถูกแก้ไข

```csharp
// Save the workbook with the custom properties
var outputPath = @"YOUR_DIRECTORY\DataWithProps.xlsb";
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

ตอนนี้ไฟล์ Excel จะมีเมตาดาต้าเฉพาะที่คุณกำหนดไว้ คุณสามารถตรวจสอบคุณสมบัติโดยทำตามขั้นตอนในส่วนต่อไป

## ขั้นตอนที่ 5: อ่านคุณสมบัติเฉพาะจาก workbook

การอ่าน **excel custom properties** ใช้รูปแบบคอลเลกชันเดียวกัน โค้ดสั้นนี้แสดงวิธีดึงค่าที่คุณเพิ่งเก็บไว้

```csharp
// Load the workbook that contains custom properties
var loadedWorkbook = new Workbook(outputPath);
var loadedWorksheet = loadedWorkbook.Worksheets[0];
var props = loadedWorksheet.CustomProperties;

// Retrieve each property safely
int projectId = props["ProjectId"] != null ? (int)props["ProjectId"].Value : -1;
string reviewer = props["Reviewer"] != null ? props["Reviewer"].Value.ToString() : "Unknown";
DateTime createdOn = props["CreatedOn"] != null ? (DateTime)props["CreatedOn"].Value : DateTime.MinValue;

Console.WriteLine($"ProjectId: {projectId}");
Console.WriteLine($"Reviewer: {reviewer}");
Console.WriteLine($"CreatedOn (UTC): {createdOn:u}");
```

อินเด็กเซอร์ของ `CustomPropertyCollection` คืนค่าเป็นอ็อบเจกต์ `CustomProperty`; การเข้าถึงคุณสมบัติ `Value` จะให้ข้อมูลที่เก็บไว้ในชนิดดั้งเดิม การตรวจสอบ `null` ก่อนทำการแคสต์ช่วยหลีกเลี่ยง `NullReferenceException` หากไม่มีคุณสมบัตินั้น

### ผลลัพธ์ที่คาดว่าจะเห็นในคอนโซล

```
ProjectId: 12345
Reviewer: John Doe
CreatedOn (UTC): 2026-10-01 12:34:56Z
```

ค่า timestamp จะสะท้อนช่วงเวลาที่คุณเรียก `Add` ในขั้นตอนที่ 3

## เคล็ดลับพิเศษ: การอัปเดตคุณสมบัติเฉพาะที่มีอยู่แล้ว

หากต้องการ **how to add custom** ข้อมูลในภายหลัง (เช่น การเปลี่ยนผู้ตรวจสอบ) ให้ใช้ตัวตั้งค่าของ `CustomPropertyCollection`:

```csharp
// Change the reviewer name
if (props["Reviewer"] != null)
{
    props["Reviewer"].Value = "Jane Smith";
}
else
{
    // Property does not exist; add it
    props.Add("Reviewer", "Jane Smith");
}
```

รูปแบบนี้ทำให้แน่ใจว่าคุณสมบัตินั้นจะถูกอัปเดตหรือสร้างใหม่ ซึ่งมีประโยชน์ในเวิร์กโฟลว์ที่ทำซ้ำ เช่น การสร้างรายงานอัตโนมัติ

## ขั้นตอนที่ 6: ตรวจสอบคุณสมบัติภายใน Excel (ตัวเลือก)

คุณยังสามารถดูคุณสมบัติเฉพาะโดยตรงใน Excel:

1. เปิดไฟล์ `DataWithProps.xlsb` ที่บันทึกไว้ใน Microsoft Excel  
2. ไปที่ **File → Info → Properties → Advanced Properties**  
3. เลือกแท็บ **Custom**  

คุณจะเห็นรายการ `ProjectId`, `Reviewer` และ `CreatedOn` พร้อมค่าที่กำหนดไว้

## ตัวอย่างทำงานเต็มรูปแบบ

ด้านล่างเป็นโปรแกรมที่สมบูรณ์และทำงานอิสระซึ่งรวมโค้ดส่วนต่าง ๆ ไว้ด้วยกัน คัดลอกไปยัง `Program.cs` แล้วรัน; คอนโซลจะแสดงค่าที่ดึงมา

```csharp
using System;
using Aspose.Cells;

namespace ExcelCustomPropertiesDemo
{
    class Program
    {
        static void Main()
        {
            // Paths (adjust to your environment)
            var sourcePath = @"YOUR_DIRECTORY\Data.xlsb";
            var resultPath = @"YOUR_DIRECTORY\DataWithProps.xlsb";

            // Load or create workbook
            var workbook = new Workbook(sourcePath);
            var worksheet = workbook.Worksheets[0];

            // Add custom properties
            worksheet.CustomProperties.Add("ProjectId", 12345);
            worksheet.CustomProperties.Add("Reviewer", "John Doe");
            worksheet.CustomProperties.Add("CreatedOn", DateTime.UtcNow);

            // Save the workbook
            workbook.Save(resultPath);
            Console.WriteLine($"Saved workbook with custom properties to {resultPath}");

            // Load the saved workbook to read properties
            var loadedWorkbook = new Workbook(resultPath);
            var loadedWorksheet = loadedWorkbook.Worksheets[0];
            var props = loadedWorksheet.CustomProperties;

            // Read properties
            int projectId = props["ProjectId"] != null ? (int)props["ProjectId"].Value : -1;
            string reviewer = props["Reviewer"] != null ? props["Reviewer"].Value.ToString() : "Unknown";
            DateTime createdOn = props["CreatedOn"] != null ? (DateTime)props["CreatedOn"].Value : DateTime.MinValue;

            Console.WriteLine($"ProjectId: {projectId}");
            Console.WriteLine($"Reviewer: {reviewer}");
            Console.WriteLine($"CreatedOn (UTC): {createdOn:u}");
        }
    }
}
```

การรันโปรแกรมนี้จะให้ผลลัพธ์ในคอนโซลตามที่แสดงก่อนหน้าและสร้างไฟล์ `DataWithProps.xlsb` ที่มีเมตาดาต้าแฝงอยู่

## คำถามที่พบบ่อยและกรณีขอบ

| คำถาม | คำตอบ |
|---|---|
| **สามารถเก็บประเภทข้อมูลที่ไม่ใช่ primitive ได้หรือไม่?** | Aspose.Cells รองรับ `string`, `int`, `double`, `DateTime` และ `bool` สำหรับอ็อบเจกต์ซับซ้อน ให้ทำการแปลงเป็น JSON หรือ XML แล้วเก็บเป็นสตริง |
| **ถ้า workbook ถูกตั้งรหัสผ่านจะทำอย่างไร?** | เปิด workbook ด้วยรหัสผ่าน (`new Workbook(path, password)`) ก่อนเข้าถึง `CustomProperties` คุณสมบัติก็ยังเข้าถึงได้หลังจากถอดรหัส |
| **คุณสมบัติเฉพาะจะคงอยู่หลังการแปลงรูปแบบหรือไม่?** | เมื่อบันทึกเป็นรูปแบบอื่น (เช่น `.xlsx`) Aspose.Cells จะคงคุณสมบัติเฉพาะไว้ตราบใดที่รูปแบบเป้าหมายรองรับ |
| **จะลบคุณสมบัติเฉพาะได้อย่างไร?** | ใช้ `worksheet.CustomProperties.Remove("PropertyName");` เพื่อลบรายการจากคอลเลกชัน |

## ขั้นตอนต่อไป

ตอนนี้คุณรู้วิธี **add custom properties** แล้ว คุณอาจสำรวจหัวข้อที่เกี่ยวข้องต่อไปนี้:

* **excel custom properties** สำหรับการจัดการเวอร์ชันเอกสาร  
* **read custom properties** จากหลาย worksheet ใน workbook เดียว  
* การใช้ **Aspose.Cells** เพื่อสร้าง pivot table ที่อ้างอิงเมตาดาต้าชนิดกำหนดเอง  
* การส่งออก workbook เป็น PDF พร้อมคงคุณสมบัติเฉพาะไว้  

ลองทดลองใช้ประเภทข้อมูลต่าง ๆ ผสานคุณสมบัติเฉพาะกับคอมเมนต์ในเซลล์ หรือบูรณาการเมตาดาต้าเข้าสู่ระบบจัดการเอกสารขนาดใหญ่ของคุณ

---

**พร้อมที่จะอัตโนมัติการรายงาน Excel ของคุณหรือยัง?** เพิ่มโค้ดข้างต้นลงในโครงการของคุณ ปรับชื่อคุณสมบัติตามความต้องการของธุรกิจ และคุณจะได้สเปรดชีตที่อธิบายตัวเองพร้อมสำหรับการประมวลผลต่อไป

## สิ่งที่คุณควรเรียนต่อไป

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคในคู่มือนี้ แต่ละแหล่งข้อมูลมีตัวอย่างโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายขั้นตอนเพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการใช้งานอื่น ๆ ในโครงการของคุณ

- [Create Excel Workbook – Add Custom Properties and Save as XLSB](/cells/english/net/document-properties/create-excel-workbook-add-custom-properties-and-save-as-xlsb/)
- [How to Access Custom Document Properties in Excel Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/access-custom-excel-properties-aspose-cells-net/)
- [Master Excel Custom Properties Using Aspose.Cells .NET for Enhanced Data Management](/cells/english/net/data-manipulation/excel-custom-properties-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}