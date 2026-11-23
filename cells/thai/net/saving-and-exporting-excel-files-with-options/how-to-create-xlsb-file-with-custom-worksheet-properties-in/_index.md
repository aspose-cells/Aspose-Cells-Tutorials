---
category: general
date: 2026-11-22
description: สร้างไฟล์ xlsb ด้วย C# และเรียนรู้วิธีเพิ่มคุณสมบัติให้กับแผ่นงาน Excel;
  บันทึกเวิร์กบุ๊กเป็น xlsb โดยใช้ Aspose.Cells เพื่อการจัดเก็บแบบไบนารีที่รวดเร็ว.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create xlsb file
- how to add properties
- excel worksheet custom properties
- custom worksheet properties
- save workbook as xlsb
language: th
lastmod: 2026-11-22
og_description: สร้างไฟล์ xlsb ด้วย C# โดยใช้ Aspose.Cells บทเรียนนี้แสดงวิธีเพิ่มคุณสมบัติให้กับแผ่นงาน
  Excel และบันทึกสมุดงานเป็น xlsb เพื่อการจัดเก็บแบบไบนารีที่เร็วขึ้น.
og_image_alt: Screenshot of an Excel workbook saved as .xlsb with custom worksheet
  properties displayed in the file explorer
og_title: สร้างไฟล์ xlsb พร้อมคุณสมบัติกำหนดเอง – คู่มือ C#
schemas:
- author: Aspose
  dateModified: '2026-11-22'
  description: Create xlsb file in C# and learn how to add properties to an Excel
    worksheet; save workbook as xlsb using Aspose.Cells for fast binary storage.
  headline: How to create xlsb file with custom worksheet properties in C#
  type: TechArticle
- description: Create xlsb file in C# and learn how to add properties to an Excel
    worksheet; save workbook as xlsb using Aspose.Cells for fast binary storage.
  name: How to create xlsb file with custom worksheet properties in C#
  steps:
  - name: Open your preferred IDE (Visual Studio, Rider, or VS Code).
    text: Open your preferred IDE (Visual Studio, Rider, or VS Code).
  - name: 'Create a new console project:'
    text: 'Create a new console project:'
  - name: 'Add the Aspose.Cells NuGet package:'
    text: 'Add the Aspose.Cells NuGet package:'
  - name: Open the file.
    text: Open the file.
  - name: Right‑click the sheet tab and choose **View Code** → **Properties** (or
      use the *File → Info → Properties* dialog).
    text: Right‑click the sheet tab and choose **View Code** → **Properties** (or
      use the *File → Info → Properties* dialog).
  - name: You will see the `Department` and `Reviewed` entries.
    text: You will see the `Department` and `Reviewed` entries.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: วิธีสร้างไฟล์ xlsb พร้อมคุณสมบัติกระดานงานแบบกำหนดเองใน C#
url: /th/net/saving-and-exporting-excel-files-with-options/how-to-create-xlsb-file-with-custom-worksheet-properties-in/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีสร้างไฟล์ xlsb พร้อมคุณสมบัติแผ่นงานที่กำหนดเองใน C#

หากคุณต้องการ **สร้างไฟล์ xlsb** ด้วยโปรแกรม คำแนะนำนี้จะให้วิธีแก้ไขที่สมบูรณ์ คุณจะได้เห็น **วิธีเพิ่มคุณสมบัติ** ให้กับแผ่นงาน Excel แล้ว **บันทึกเวิร์กบุ๊กเป็น xlsb** ด้วย Aspose.Cells ขั้นตอนเหล่านี้ทำงานกับ .NET 6 ขึ้นไป และไม่ต้องติดตั้ง Excel ด้วยตนเอง

บทเรียนนี้ครอบคลุมการตั้งค่าโครงการ, การสร้างเวิร์กบุ๊ก, การเพิ่มคุณสมบัติแผ่นงานที่กำหนดเอง, การบันทึกไฟล์ในรูปแบบ Excel แบบไบนารี, และการตรวจสอบผลลัพธ์ เมื่อเสร็จสิ้นคุณจะสามารถสร้างเวิร์กบุ๊ก *.xlsb* ขนาดกะทัดรัดที่บรรจุเมตาดาต้า เช่น แผนกหรือสถานะการตรวจสอบ

## สร้างไฟล์ xlsb – ภาพรวม

การสร้างไฟล์ *.xlsb* แตกต่างจากรูปแบบ *.xlsx* แบบคลาสสิกเพียงขั้นตอนการบันทึกสุดท้าย โครงสร้างเวิร์กบุ๊ก, แผ่นงาน, และข้อมูลเซลล์นั้นเหมือนกัน; รูปแบบไบนารีช่วยลดขนาดไฟล์และเพิ่มความเร็วในการเปิดใน Excel ตัวอย่างโค้ดด้านล่างแสดงวงจรชีวิตเต็มรูปแบบ ตั้งแต่เวิร์กบุ๊กเปล่าจนถึงไฟล์ *.xlsb* ที่บรรจุ **excel worksheet custom properties**  

## ตั้งค่า Aspose.Cells ในโครงการ C# ของคุณ

1. เปิด IDE ที่คุณชื่นชอบ (Visual Studio, Rider หรือ VS Code)  
2. สร้างโปรเจกต์คอนโซลใหม่:

   ```bash
   dotnet new console -n XlsbDemo
   cd XlsbDemo
   ```

3. เพิ่มแพ็กเกจ NuGet ของ Aspose.Cells:

   ```bash
   dotnet add package Aspose.Cells
   ```

   แพ็กเกจนี้จะให้คลาส `Workbook`, `Worksheet`, และ `CustomPropertyCollection` ที่จำเป็นสำหรับบทเรียนนี้

## วิธีเพิ่มคุณสมบัติให้กับแผ่นงาน Excel

คุณสมบัติแผ่นงานที่กำหนดเองช่วยให้คุณเก็บเมตาดาต้าใด ๆ ควบคู่กับแผ่นงาน ใช้สำหรับการประมวลผลต่อ, การตรวจสอบ, หรือเป็นคำแนะนำใน UI โค้ดต่อไปนี้สร้างเวิร์กบุ๊ก, เข้าถึงแผ่นงานแรก, และเพิ่มสองคุณสมบัติ: สตริง `Department` และบูลีน `Reviewed`

```csharp
using Aspose.Cells;

class XlsbCustomPropsDemo
{
    static void Main()
    {
        // Step 1: Create a new workbook and get its first worksheet
        Workbook workbook = new Workbook();                 // workbook is the container for all sheets
        Worksheet worksheet = workbook.Worksheets[0];       // the default sheet is at index 0

        // Step 2: Add custom properties to the worksheet
        // These are *excel worksheet custom properties* that travel with the sheet.
        worksheet.CustomProperties.Add("Department", "Finance");
        worksheet.CustomProperties.Add("Reviewed", true);

        // Step 3: Save the workbook in binary Excel format (.xlsb)
        // The file will contain the custom properties defined above.
        workbook.Save("CustomProps.xlsb");
    }
}
```

**เหตุผลที่บรรทัดเหล่านี้สำคัญ**

- `Workbook()` สร้างตัวแทนของไฟล์ Excel ในหน่วยความจำ  
- `worksheet.CustomProperties.Add` เก็บคู่คีย์‑ค่า ที่ Excel สามารถอ่านได้ผ่านกล่องโต้ตอบ *Custom Properties*  
- `workbook.Save` พร้อมส่วนขยาย `.xlsb` ทำให้เกิดการ **save workbook as xlsb** โดยอัตโนมัติใช้รูปแบบไบนารี  

คุณสามารถเพิ่มคุณสมบัติได้ตามจำนวนที่ต้องการ; คอลเลกชันรับสตริง, ตัวเลข, วันที่, และบูลีน หากต้องการอ่านค่าในภายหลัง ให้ใช้ `worksheet.CustomProperties["Department"]`

## บันทึกเวิร์กบุ๊กเป็น xlsb

เมธอด `Save` กำหนดรูปแบบไฟล์จากส่วนขยาย การระบุ `"CustomProps.xlsb"` จะสั่งให้ Aspose.Cells เขียนเวิร์กบุ๊กแบบไบนารี ขั้นตอนนี้เป็นจุดเดียวที่ปรากฏ **save workbook as xlsb** ในโค้ด แต่ผลลัพธ์จะเห็นได้จากขนาดไฟล์และความเร็วในการเปิด

หากต้องการควบคุมรูปแบบอย่างชัดเจน สามารถใช้วัตถุ `SaveOptions`:

```csharp
// Alternative: specify the save format with SaveOptions
var options = new XlsbSaveOptions(SaveFormat.Xlsb);
workbook.Save("CustomPropsExplicit.xlsb", options);
```

ทั้งสองวิธีจะสร้างไฟล์ *.xlsb* ที่ถูกต้องซึ่งบรรจุ **custom worksheet properties** ที่คุณกำหนดไว้

## ตรวจสอบคุณสมบัติแผ่นงานที่กำหนดเอง

เมื่อโปรแกรมทำงานเสร็จ ให้เปิดไฟล์ `CustomProps.xlsb` ที่สร้างขึ้นใน Excel:

1. เปิดไฟล์  
2. คลิกขวาที่แท็บแผ่นงานและเลือก **View Code** → **Properties** (หรือใช้เมนู *File → Info → Properties*)  
3. คุณจะเห็นรายการ `Department` และ `Reviewed`

การมีรายการเหล่านี้แสดงว่า **excel worksheet custom properties** ถูกฝังอย่างถูกต้อง

### ผลลัพธ์ที่คาดหวัง

การรันโปรแกรมจะสร้างไฟล์สองไฟล์ในโฟลเดอร์โปรเจกต์:

- `CustomProps.xlsb` – เวิร์กบุ๊กไบนารีพร้อมคุณสมบัติที่กำหนดเอง  
- `CustomPropsExplicit.xlsb` – เนื้อหาเดียวกัน แต่บันทึกผ่าน `XlsbSaveOptions`

ทั้งสองไฟล์เปิดใน Excel ได้โดยไม่มีคำเตือนและแสดงเมตาดาต้าที่กำหนดเมื่อทำการตรวจสอบ

## ข้อผิดพลาดทั่วไปและเคล็ดลับปฏิบัติที่ดีที่สุด

- **ห้ามผสมส่วนขยายไฟล์** การใช้ `.xlsx` พร้อม `XlsbSaveOptions` จะทำให้ไฟล์เสียหาย ควรให้ส่วนขยายตรงกับรูปแบบที่เลือกเสมอ  
- **ชื่อคุณสมบัติมีความแตกต่างตามตัวอักษร** ในคอลเลกชัน ให้เข้าถึงด้วยคีย์ที่พิมพ์ตรงกับที่ใช้เพิ่ม  
- **เวิร์กบุ๊กขนาดใหญ่จะได้ประโยชน์จากรูปแบบไบนารี** เนื่องจากขนาดไฟล์อาจลดลงได้ถึง 50 % เมื่อเทียบกับ `.xlsx` โดยเฉพาะเมื่อมีสูตรหรือสไตล์จำนวนมาก  
- **ความปลอดภัยของเธรด:** อินสแตนซ์ `Workbook` ไม่ปลอดภัยต่อหลายเธรด สร้างอินสแตนซ์แยกสำหรับแต่ละเธรดหากต้องสร้างไฟล์หลายไฟล์พร้อมกัน  

## ขั้นตอนต่อไป

ตอนนี้คุณสามารถ **สร้างไฟล์ xlsb** พร้อม **custom worksheet properties** แล้ว คุณอาจต้องการสำรวจต่อ:

- การเพิ่ม **excel worksheet custom properties** ให้หลายแผ่นงานในเวิร์กบุ๊กเดียว  
- การใช้ **how to add properties** สำหรับแถวหรือเซลล์ผ่านคอลเลกชัน `Cell.CustomProperties`  
- การส่งออกเวิร์กบุ๊กเป็น PDF หรือ HTML พร้อมคงเมตาดาต้าไว้  
- การทำอัตโนมัติใน Web API ที่ส่งสตรีม *.xlsb* ตรงกลับไปยังไคลเอนต์  

การขยายเหล่านี้ช่วยให้คุณสร้างสายงานอัตโนมัติของ Excel ที่ใช้ประโยชน์จากความเร็วของรูปแบบไบนารีและความยืดหยุ่นของเมตาดาต้าที่กำหนดเอง

---

*คุณได้เรียนรู้วิธีสร้างเวิร์กบุ๊ก *.xlsb* ใน C#, เพิ่มคุณสมบัติแผ่นงานที่กำหนดเอง, และบันทึกไฟล์ด้วย Aspose.Cells นำรูปแบบเหล่านี้ไปใช้กับรายงาน, แดชบอร์ด, หรือบริการแลกเปลี่ยนข้อมูลของคุณเอง*


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Create Excel Workbook C# – Add Custom Property & Save XLSB](/cells/english/net/document-properties/create-excel-workbook-c-add-custom-property-save-xlsb/)
- [How to Save XLSB and Add Custom Document Properties in C#](/cells/english/net/document-properties/how-to-save-xlsb-and-add-custom-document-properties-in-c/)
- [How to Save XLSB with Custom Properties in C# – Step‑by‑Step Guide](/cells/english/net/document-properties/how-to-save-xlsb-with-custom-properties-in-c-step-by-step-gu/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}