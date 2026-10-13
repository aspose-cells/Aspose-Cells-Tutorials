---
category: general
date: 2026-03-30
description: วิธีคัดลอกแผ่นงานใน C# ด้วย Aspose.Cells – คู่มือขั้นตอนโดยละเอียดที่ครอบคลุมการคัดลอกช่วงเซลล์,
  การคัดลอกคอลัมน์ระหว่างแผ่นงาน, การคัดลอกตาราง Pivot ของแผ่นงาน และการเพิ่มโค้ดแผ่นงานใหม่
draft: false
keywords:
- how to copy worksheet
- copy cell range
- copy columns between sheets
- copy worksheet pivot table
- add new worksheet code
language: th
og_description: เรียนรู้วิธีคัดลอกแผ่นงานใน C# ด้วย Aspose.Cells คู่มือนี้แสดงการคัดลอกช่วงเซลล์,
  รักษาตาราง Pivot, คัดลอกคอลัมน์ระหว่างแผ่นงาน, และเพิ่มโค้ดสร้างแผ่นงานใหม่
og_title: วิธีคัดลอกแผ่นงานใน C# – บทเรียน Aspose.Cells อย่างเต็มรูปแบบ
tags:
- Aspose.Cells
- C#
- Excel Automation
title: วิธีคัดลอกแผ่นงานใน C# ด้วย Aspose.Cells – คู่มือฉบับสมบูรณ์
url: /th/net/excel-copy-worksheet/how-to-copy-worksheet-in-c-with-aspose-cells-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีคัดลอก Worksheet ใน C# ด้วย Aspose.Cells – คู่มือฉบับสมบูรณ์

เคยสงสัย **how to copy worksheet** ใน C# โดยไม่สูญเสีย Pivot Table หรือสูตรใดเลยหรือไม่? คุณไม่ได้เป็นคนเดียว—นักพัฒนาหลายคนเจออุปสรรคเมื่อจำเป็นต้องทำสำเนาแผ่นงานโดยยังคงรักษาข้อมูลทั้งหมดไว้ครบถ้วน ในบทแนะนำนี้เราจะพาคุณผ่านโซลูชันเชิงปฏิบัติแบบครบวงจร ที่ไม่เพียงคัดลอกข้อมูล แต่ยังคง **copy worksheet pivot table**, จัดการ **copy cell range**, และแสดง **add new worksheet code** ที่คุณต้องการ

เราจะครอบคลุมทุกอย่างตั้งแต่การโหลดเวิร์กบุ๊กต้นฉบับจนถึงการบันทึกไฟล์ปลายทาง เพื่อให้คุณสามารถ **copy columns between sheets**, รักษาวัตถุต่าง ๆ, และทำให้โค้ดของคุณสะอาดตา ไม่มีการอ้างอิงที่คลุมเครือ เพียงตัวอย่างที่ทำงานได้เต็มรูปแบบที่คุณสามารถนำไปใช้ในโปรเจกต์ของคุณได้ทันที

## สิ่งที่บทแนะนำนี้ครอบคลุม

- การโหลดไฟล์ Excel ที่มีอยู่แล้วด้วย Aspose.Cells  
- การใช้ **add new worksheet code** เพื่อสร้างแผ่นงานเป้าหมาย  
- การกำหนด **copy cell range** ที่รวม Pivot Table  
- การตั้งค่า **CopyOptions** เพื่อรักษาชาร์ต, สูตร, และ Pivot Table ไว้ครบถ้วน  
- การดำเนินการ **copy columns between sheets** ด้วยความแม่นยำระดับแถว  
- การบันทึกผลลัพธ์และตรวจสอบว่า Worksheet ถูกคัดลอกอย่างถูกต้อง  

เมื่อจบการอ่านคุณจะสามารถตอบคำถาม “how to copy worksheet” ได้อย่างมั่นใจ ไม่ว่าจะเป็นการอัตโนมัติรายงานหรือการสร้าง UI ที่ขับเคลื่อนด้วยสเปรดชีต

## วิธีคัดลอก Worksheet – ภาพรวม

ก่อนที่เราจะลงลึกในโค้ด ให้มาดูขั้นตอนระดับสูงกันเป็นสูตรอาหาร:

1. **Load** เวิร์กบุ๊กต้นฉบับ (`Source.xlsx`).  
2. **Add** แผ่นงานใหม่เพื่อเก็บสำเนา (`add new worksheet code`).  
3. **Define** พื้นที่ที่ต้องการทำสำเนา (`copy cell range`).  
4. **Configure** ตัวเลือกการคัดลอกเพื่อให้ Pivot Table อยู่รอด (`copy worksheet pivot table`).  
5. **Copy** แถวและคอลัมน์ (`copy columns between sheets`).  
6. **Save** เวิร์กบุ๊กใหม่ (`Destination.xlsx`).  

เท่านี้—หกขั้นตอน ไม่มีเวทมนตร์ ทุกขั้นตอนจะอธิบายพร้อมโค้ดสแนปและเหตุผลเบื้องหลัง

## ขั้นตอนที่ 1 – โหลดเวิร์กบุ๊กต้นฉบับ

สิ่งแรกที่ต้องทำคือสร้างอินสแตนซ์ `Workbook` ที่ชี้ไปยังไฟล์ที่ต้องการทำสำเนา ขั้นตอนนี้สำคัญเพราะ Aspose.Cells ทำงานโดยตรงกับระบบไฟล์ ไม่ใช่กับ UI ของ Office

```csharp
using Aspose.Cells;

// Path to the original file
string sourcePath = "YOUR_DIRECTORY/Source.xlsx";
string destinationPath = "YOUR_DIRECTORY/Destination.xlsx";

// Load the workbook – this is the starting point for how to copy worksheet
Workbook workbook = new Workbook(sourcePath);
```

*ทำไมขั้นตอนนี้ถึงสำคัญ:* การโหลดไฟล์จะสร้างการแสดงผลในหน่วยความจำของทุกแผ่นงาน, เซลล์, และวัตถุต่าง ๆ หากไม่มีขั้นตอนนี้ จะไม่มีอะไรให้คัดลอกและการเรียก `add new worksheet code` ต่อไปจะล้มเหลวเพราะข้อมูลต้นฉบับไม่มีอยู่

## ขั้นตอนที่ 2 – เพิ่มแผ่นงานใหม่ (add new worksheet code)

ต่อไปเราต้องมีที่สำหรับวางข้อมูลที่คัดลอก นี่คือจุดที่ **add new worksheet code** มีประโยชน์ คุณสามารถตั้งชื่อแผ่นงานได้ตามต้องการ ที่นี่เราใช้ชื่อ `"Copy"`

```csharp
// Grab the first worksheet (the one we want to copy)
Worksheet sourceSheet = workbook.Worksheets[0];

// Add a fresh worksheet to receive the copy
Worksheet copySheet = workbook.Worksheets.Add("Copy");
```

*เคล็ดลับ:* หากต้องการคัดลอกหลายแผ่นงาน ให้เรียก `Worksheets.Add` ภายในลูปและตั้งชื่อแต่ละแผ่นให้เป็นเอกลักษณ์ วิธีนี้จะช่วยหลีกเลี่ยงการชนชื่อและทำให้เวิร์กบุ๊กของคุณเป็นระเบียบ

## ขั้นตอนที่ 3 – กำหนด Copy Cell Range

**copy cell range** บอก Aspose.Cells ว่าแถวและคอลัมน์ใดบ้างที่ต้องการทำสำเนา ในหลายกรณีจริง ๆ ช่วงนี้จะรวม Pivot Table ดังนั้นต้องระบุอย่างแม่นยำ

```csharp
// Define the area that contains the pivot table (A1:G20)
CellArea sourceRange = new CellArea
{
    StartRow = 0,      // Row 1 (zero‑based)
    StartColumn = 0,   // Column A
    EndRow = 19,       // Row 20
    EndColumn = 6      // Column G
};

// Destination range – we start at the same top‑left corner
CellArea destinationRange = new CellArea
{
    StartRow = 0,
    StartColumn = 0,
    EndRow = 19,
    EndColumn = 6
};
```

*ทำไมต้องกำหนดช่วงนี้:* การระบุช่วงอย่างชัดเจนช่วยหลีกเลี่ยงการคัดลอกทั้งแผ่นงาน (ซึ่งอาจเสียเวลา) และทำให้แน่ใจว่า Pivot Table อยู่ภายในพื้นที่ที่คัดลอก นี่คือหัวใจของ **how to copy worksheet** เมื่อคุณต้องการเพียงบางส่วนของแผ่นงาน

## ขั้นตอนที่ 4 – ตั้งค่า Copy Options (preserve copy worksheet pivot table)

Aspose.Cells มีอ็อบเจ็กต์ `CopyOptions` ที่ควบคุมสิ่งที่ถูกวางลงไป เพื่อรักษา Pivot Table, ชาร์ต, และสูตร เราตั้งค่า `PasteType.All` และเปิดใช้งาน `PasteSpecial`

```csharp
CopyOptions copyOptions = new CopyOptions
{
    PasteType = PasteType.All,   // Copy everything: values, formats, objects
    PasteSpecial = true          // Enable special paste to retain pivot tables
};
```

*คำอธิบาย:* `PasteType.All` เป็นตัวเลือกที่ครอบคลุมที่สุด ส่วน `PasteSpecial` บอกเอนจินให้จัดการกับวัตถุซับซ้อนเช่น Pivot Table อย่างถูกต้อง การข้ามขั้นตอนนี้เป็นข้อผิดพลาดทั่วไปที่ทำให้แผ่นงานที่คัดลอกสูญเสียฟีเจอร์เชิงโต้ตอบ

## ขั้นตอนที่ 5 – คัดลอกแถวและคอลัมน์ (copy columns between sheets)

ต่อไปเป็นขั้นตอนที่หนักที่สุด: ย้ายข้อมูลจริง เราจะใช้ `CopyRows` และ `CopyColumns` เพื่อจัดการ **copy columns between sheets** การทำทั้งสองอย่างช่วยให้การรวมเซลล์และความกว้างของคอลัมน์ถูกคงไว้

```csharp
// Copy rows from the source to the destination sheet
sourceSheet.Cells.CopyRows(
    sourceRange.StartRow,
    sourceRange.EndRow,
    copySheet.Cells,
    destinationRange.StartRow,
    copyOptions);

// Copy columns from the source to the destination sheet
sourceSheet.Cells.CopyColumns(
    sourceRange.StartColumn,
    sourceRange.EndColumn,
    copySheet.Cells,
    destinationRange.StartColumn,
    copyOptions);
```

*สิ่งที่เกิดขึ้น:* `CopyRows` ย้ายข้อมูลแถวต่อแถว ส่วน `CopyColumns` ทำเช่นเดียวกันในระดับคอลัมน์ การทำทั้งสองอย่างร่วมกันรับประกันว่าบล็อกสี่เหลี่ยมผืนผ้าทั้งหมดถูกทำสำเนาอย่างครบถ้วน ซึ่งจำเป็นเมื่อคุณต้อง **copy columns between sheets** ที่มีความกว้างของคอลัมน์หรือคอลัมน์ที่ซ่อนต่างกัน

## ขั้นตอนที่ 6 – บันทึกเวิร์กบุ๊ก

สุดท้าย เขียนการเปลี่ยนแปลงกลับไปยังดิสก์ ขั้นตอนนี้ทำให้กระบวนการ **how to copy worksheet** เสร็จสมบูรณ์

```csharp
// Save the workbook with the newly copied sheet
workbook.Save(destinationPath);
```

*เคล็ดลับการตรวจสอบ:* เปิด `Destination.xlsx` แล้วตรวจสอบว่าแผ่นงาน `"Copy"` มีลักษณะเหมือนต้นฉบับ, Pivot Table ทำงานได้, และความกว้างของคอลัมน์ตรงกัน หากมีสิ่งใดผิดพลาด ให้กลับไปตรวจสอบการตั้งค่า `CopyOptions`

## กรณีขอบและรูปแบบที่พบบ่อย

### การคัดลอกหลาย Worksheet

หากต้องการทำสำเนาหลายแผ่นงาน ให้ใส่ตรรกะข้างต้นไว้ในลูป `foreach`:

```csharp
foreach (Worksheet ws in workbook.Worksheets)
{
    Worksheet newWs = workbook.Worksheets.Add(ws.Name + "_Copy");
    // Re‑use sourceRange/destinationRange or calculate per sheet
    // Then call CopyRows/CopyColumns as shown earlier
}
```

### การรักษาสูตรระหว่างเวิร์กบุ๊กที่ต่างกัน

เมื่อเวิร์กบุ๊กต้นฉบับและปลายทางมี Named Range ที่แตกต่างกัน ให้ตั้งค่า `copyOptions` เป็น `PasteType.Formulas` เพิ่มเติมจาก `All`:

```csharp
copyOptions.PasteType = PasteType.All | PasteType.Formulas;
```

### ช่วงข้อมูลขนาดใหญ่และประสิทธิภาพ

สำหรับชุดข้อมูลขนาดมหาศาล (หลายแสนแถว) พิจารณาใช้เฉพาะ `CopyRows` และละเว้น `CopyColumns` หากความกว้างของคอลัมน์ไม่สำคัญ วิธีนี้สามารถลดเวลาได้หลายวินาที

## ตัวอย่างทำงานเต็มรูปแบบ

ด้านล่างเป็นโปรแกรมเต็มรูปแบบที่พร้อมรัน คุณเพียงแค่วางลงในแอปคอนโซล ปรับเส้นทางไฟล์ แล้วกด **F5**

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // ---------- Step 1: Load the source workbook ----------
        string sourcePath = "YOUR_DIRECTORY/Source.xlsx";
        string destinationPath = "YOUR_DIRECTORY/Destination.xlsx";
        Workbook workbook = new Workbook(sourcePath);

        // ---------- Step 2: Add a new worksheet (add new worksheet code) ----------
        Worksheet sourceSheet = workbook.Worksheets[0];
        Worksheet copySheet = workbook.Worksheets.Add("Copy");

        // ---------- Step 3: Define the copy cell range ----------
        CellArea sourceRange = new CellArea
        {
            StartRow = 0,
            StartColumn = 0,
            EndRow = 19,
            EndColumn = 6
        };
        CellArea destinationRange = new CellArea
        {
            StartRow = 0,
            StartColumn = 0,
            EndRow = 19,
            EndColumn = 6
        };

        // ---------- Step 4: Set copy options (preserve copy worksheet pivot table) ----------
        CopyOptions copyOptions = new CopyOptions
        {
            PasteType = PasteType.All,
            PasteSpecial = true
        };

        // ---------- Step 5: Copy rows and columns (copy columns between sheets) ----------
        sourceSheet.Cells.CopyRows(
            sourceRange.StartRow,
            sourceRange.EndRow,
            copySheet.Cells,
            destinationRange.StartRow,
            copyOptions);

        sourceSheet.Cells.CopyColumns(
            sourceRange.StartColumn,
            sourceRange.EndColumn,
            copySheet.Cells,
            destinationRange.StartColumn,
            copyOptions);

        // ---------- Step 6: Save the workbook ----------
        workbook.Save(destinationPath);
    }
}
```

**ผลลัพธ์ที่คาดหวัง:** เปิด `Destination.xlsx` จะเห็นแผ่นงานชื่อ **Copy** ที่สะท้อนแผ่นงานแรกของ `Source.xlsx` อย่างครบถ้วน รวมถึง Pivot Table, การจัดรูปแบบ, และความกว้างของคอลัมน์ ไฟล์ต้นฉบับจะไม่ถูกแก้ไข

## คำถามที่พบบ่อย

**Q: โค้ดนี้ทำงานกับไฟล์ .xlsx ที่สร้างโดย Excel 2019 หรือไม่?**  
A: ทำได้แน่นอน Aspose.Cells รองรับรูปแบบ Excel สมัยใหม่ทั้งหมด ดังนั้นโค้ดเดียวกันจึงทำงานได้กับไฟล์ `.xlsx`, `.xlsm` และแม้แต่ไฟล์ `.xls` เก่า

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}