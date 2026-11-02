---
category: general
date: 2026-06-30
description: สร้างการจัดรูปแบบตามเงื่อนไขในเวิร์กบุ๊ก Excel ด้วย Aspose.Cells เรียนรู้วิธีตั้งพื้นหลังของเซลล์
  จัดอันดับเซลล์ และสร้างไฟล์โดยโปรแกรมmatically.
draft: false
keywords:
- create conditional formatting
- create excel workbook
- set cell background
- how to rank cells
- how to use aspose
language: th
og_description: สร้างการจัดรูปแบบตามเงื่อนไขในเวิร์กบุ๊ก Excel ด้วย Aspose.Cells.
  ทำตามบทแนะนำฉบับเต็มนี้เพื่อกำหนดพื้นหลังของเซลล์, จัดอันดับเซลล์, และทำงานอัตโนมัติใน
  Excel.
og_title: สร้างการจัดรูปแบบตามเงื่อนไขใน Excel ด้วย Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Create conditional formatting in an Excel workbook using Aspose.Cells.
    Learn how to set cell background, rank cells, and build the file programmatically.
  headline: Create Conditional Formatting in Excel with Aspose.Cells – Step‑by‑Step
    Guide
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: สร้างการจัดรูปแบบตามเงื่อนไขใน Excel ด้วย Aspose.Cells – คู่มือขั้นตอนโดยละเอียด
url: /th/net/excel-conditional-formatting/create-conditional-formatting-in-excel-with-aspose-cells-ste/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# สร้าง Conditional Formatting ใน Excel ด้วย Aspose.Cells – คู่มือขั้นตอนโดยละเอียด

เคยสงสัยไหมว่าจะ **สร้าง conditional formatting** ในไฟล์ Excel โดยไม่ต้องเปิด UI? คุณไม่ได้อยู่คนเดียว นักพัฒนาหลายคนต้อง **สร้าง excel workbook** แบบไดนามิก และการทำเช่นนั้นด้วยโค้ดช่วยประหยัดเวลามาก ในบทเรียนนี้เราจะแสดงให้คุณเห็นอย่างละเอียดว่า **สร้าง conditional formatting** อย่างไร, ปรับสไตล์เซลล์, และแม้กระทั่งจัดอันดับค่าที่สูงที่สุด—ทั้งหมดด้วยไลบรารี Aspose.Cells สำหรับ .NET

เราจะเดินผ่านตัวอย่างจริง: สร้างสกอร์ชีต, ไฮไลท์คะแนนสูงด้วยสีเขียวอ่อน, และใส่พื้นหลังสีทองให้ผู้ทำคะแนนสูงสุด 3 คน สุดท้ายคุณจะรู้ **วิธีตั้งพื้นหลังเซลล์**, **วิธีจัดอันดับเซลล์**, และ **วิธีใช้ Aspose** สำหรับการอัตโนมัติ Excel ขั้นสูง ไม่ฟุ่มเฟือย เพียงโซลูชันที่ทำงานได้เต็มรูปแบบและสามารถนำไปใช้ในโปรเจกต์ C# ใดก็ได้

## สิ่งที่คุณจะได้เรียน

- วิธี **สร้าง excel workbook** ด้วย Aspose.Cells  
- วิธีเติมช่วงด้วยข้อมูลสุ่ม (คะแนน)  
- วิธี **ตั้งพื้นหลังเซลล์** ด้วยสีทึบ  
- วิธีใช้กฎแบบสูตรเพื่อ **จัดอันดับเซลล์** และไฮไลท์สามอันดับแรก  
- วิธีบันทึกผลลัพธ์เป็นไฟล์ .xlsx  

ข้อกำหนดเบื้องต้น: .NET 6+ (หรือ .NET Framework 4.6+), Visual Studio (หรือ IDE C# ใดก็ได้) และอ้างอิงแพ็กเกจ Aspose.Cells จาก NuGet หากคุณยังไม่เคยใช้ Aspose ไม่ต้องกังวล—we’ll cover **วิธีใช้ Aspose** ตั้งแต่ต้น

---

![ตัวอย่างการสร้าง conditional formatting](https://example.com/images/create-conditional-formatting.png "ภาพหน้าจอแสดง conditional formatting ในไฟล์ Excel ที่สร้างขึ้น")

*ข้อความแทนรูป: ตัวอย่างการสร้าง conditional formatting ใน Excel workbook ที่สร้างด้วย Aspose.Cells.*

## วิธีสร้าง Excel Workbook ด้วย Aspose.Cells

ขั้นแรกคุณต้องมีอ็อบเจกต์ workbook เพื่อทำงาน Aspose.Cells ทำให้ขั้นตอนนี้เป็นบรรทัดเดียว

```csharp
using Aspose.Cells;
using System.Drawing;

void CreateConditionalFormattingWorkbook()
{
    // Step 1: Instantiate a new workbook and give the first sheet a friendly name
    Workbook workbook = new Workbook();                 // creates an empty workbook
    Worksheet sheet = workbook.Worksheets[0];           // grab the default worksheet
    sheet.Name = "Scores";                              // rename it to something meaningful
```

ทำไมต้องเปลี่ยนชื่อชีต? ชื่อที่ชัดเจน (เช่น **Scores**) ทำให้การอ้างอิงในภายหลังง่ายขึ้น โดยเฉพาะเมื่อแชร์ไฟล์ให้ผู้ใช้ที่ไม่ใช่เทคนิค  

เมื่อ workbook ถูกสร้างแล้ว ให้เติมคอลัมน์ A ด้วยคะแนนสุ่ม

## วิธีเติมข้อมูล – สร้างคะแนนสุ่ม

```csharp
    // Step 2: Populate A2:A21 with random values between 40 and 99
    Random random = new Random();
    for (int i = 0; i < 20; i++)               // 20 rows of data
    {
        sheet.Cells[i + 1, 0].PutValue(random.Next(40, 100));
    }
```

หมายเหตุสั้น ๆ: `PutValue` ตรวจจับประเภทข้อมูลโดยอัตโนมัติ จึงไม่ต้องแคสท์เป็น `int` ลูปเริ่มที่ `i = 0` แต่เขียนลงแถว `i + 1` เพราะแถวใน Excel เริ่มจาก 1 ส่วนคอลเลกชัน `Cells` เริ่มจาก 0

## วิธีตั้งพื้นหลังเซลล์สำหรับคะแนนสูง

ต่อไปเราจะ **สร้าง conditional formatting** ที่ทาสีเซลล์ใดที่คะแนน ≥ 80 ด้วยสีเขียวอ่อน

```csharp
    // Step 3: Define a conditional formatting range (A2:A21)
    int firstRow = 1, lastRow = 20;                     // zero‑based indices for rows 2‑21
    int cfIndex = sheet.ConditionalFormattings.Add(firstRow, 0, lastRow, 0);
    ConditionalFormatting cf = sheet.ConditionalFormattings[cfIndex];

    // Add a rule: cell value >= 80 → light‑green background
    FormatCondition highScoreCondition = cf.AddCondition(
        FormatConditionType.CellValue,
        OperatorType.GreaterOrEqual,
        "80");

    highScoreCondition.Style.ForegroundColor = Color.LightGreen;
    highScoreCondition.Style.Pattern = BackgroundType.Solid;
```

คุณสมบัติ `ForegroundColor` ควบคุมสีเติม, ส่วน `Pattern = BackgroundType.Solid` บอก Excel ให้ใช้การเติมสีทึบ ไม่ใช่ไล่สีหรือแพทเทิร์น นี่คือหัวใจของ **วิธีตั้งพื้นหลังเซลล์** ตามเกณฑ์เชิงตัวเลข

## วิธีจัดอันดับเซลล์และไฮไลท์ 3 อันดับแรก

การจัดอันดับค่อนข้างซับซ้อน เพราะต้องใช้สูตรที่ประเมินแต่ละเซลล์เทียบกับช่วงทั้งหมด Aspose.Cells ให้คุณใช้ไวยากรณ์สูตร Excel เดิมที่คุณพิมพ์ใน UI

```csharp
    // Step 4: Add a formula‑based rule to color the top‑3 scores gold
    FormatCondition topThreeCondition = cf.AddCondition(
        FormatConditionType.Formula,
        null,
        null);

    // The formula uses the RANK function; note the absolute references ($) lock the range
    topThreeCondition.Formula1 = "=RANK(A2,$A$2:$A$21)<=3";

    topThreeCondition.Style.ForegroundColor = Color.Gold;
    topThreeCondition.Style.Pattern = BackgroundType.Solid;
```

ทำไมถึงใช้ `A2` ในสูตร? Aspose ประเมินสูตรโดยอิงตามแต่ละเซลล์ในช่วง ดังนั้น `A2` จะเปลี่ยนเป็น `A3`, `A4` ฯลฯ ตามแถวที่กฎถูกนำไปใช้ ฟังก์ชัน `RANK` คืนตำแหน่งของค่าภายในช่วงที่กำหนด, ส่วน `<=3` ทำให้เฉพาะสามคะแนนสูงสุดเท่านั้นที่ได้รับสีพื้นหลังสีทอง

## วิธีบันทึก Workbook

```csharp
    // Step 5: Persist the workbook to disk
    workbook.Save("YOUR_DIRECTORY/Scores_ConditionalFormatting.xlsx");
}
```

แทนที่ `YOUR_DIRECTORY` ด้วยพาธแบบ absolute หรือ relative ที่แอปพลิเคชันของคุณสามารถเขียนได้ หลังจากรันเมธอดแล้ว เปิดไฟล์ใน Excel แล้วคุณจะเห็น:

- เซลล์สีเขียวอ่อนสำหรับคะแนน ≥ 80  
- เซลล์สีทองสำหรับสามคะแนนสูงสุด ไม่ว่าจะคะแนนนั้น ≥ 80 หรือไม่ก็ตาม  

นี่คือขั้นตอน **สร้าง conditional formatting** อย่างครบถ้วน

---

## ตัวอย่างเต็มที่สามารถรันได้

นี่คือเมธอดทั้งหมดอีกครั้ง พร้อมคัดลอก‑วางลงใน console app หรือคลาส C# ใดก็ได้:

```csharp
using Aspose.Cells;
using System.Drawing;

void CreateConditionalFormattingWorkbook()
{
    // Step 1: Create a new workbook and name the first worksheet
    Workbook workbook = new Workbook();
    Worksheet sheet = workbook.Worksheets[0];
    sheet.Name = "Scores";

    // Step 2: Fill column A (A2:A21) with random scores between 40 and 99
    Random random = new Random();
    for (int i = 0; i < 20; i++)
    {
        sheet.Cells[i + 1, 0].PutValue(random.Next(40, 100));
    }

    // Step 3: Highlight scores >= 80 with a light‑green background
    int firstRow = 1, lastRow = 20;
    int cfIndex = sheet.ConditionalFormattings.Add(firstRow, 0, lastRow, 0);
    ConditionalFormatting cf = sheet.ConditionalFormattings[cfIndex];
    FormatCondition highScoreCondition = cf.AddCondition(
        FormatConditionType.CellValue,
        OperatorType.GreaterOrEqual,
        "80");
    highScoreCondition.Style.ForegroundColor = Color.LightGreen;
    highScoreCondition.Style.Pattern = BackgroundType.Solid;

    // Step 4: Color the top‑3 scores with a gold background using a formula rule
    FormatCondition topThreeCondition = cf.AddCondition(
        FormatConditionType.Formula,
        null,
        null);
    topThreeCondition.Formula1 = "=RANK(A2,$A$2:$A$21)<=3";
    topThreeCondition.Style.ForegroundColor = Color.Gold;
    topThreeCondition.Style.Pattern = BackgroundType.Solid;

    // Step 5: Save the workbook
    workbook.Save("YOUR_DIRECTORY/Scores_ConditionalFormatting.xlsx");
}
```

### ผลลัพธ์ที่คาดหวัง

เมื่อคุณเปิด `Scores_ConditionalFormatting.xlsx`:

- เซลล์ที่มีค่า **80** หรือมากกว่า จะสว่างเป็นสีเขียวอ่อน  
- สามค่าที่สูงที่สุด (แม้จะต่ำกว่า 80) จะมีพื้นหลัง **สีทอง**  
- เซลล์อื่น ๆ จะคงพื้นหลังสีขาวตามค่าเริ่มต้น

สัญญาณภาพนี้บอกผู้จัดการได้ทันทีว่าใครเป็นผู้ทำคะแนนสูงสุดโดยไม่ต้องจัดเรียงด้วยมือ

---

## คำถามที่พบบ่อย & กรณีขอบ

**ถ้าต้องการมากกว่า 3 คะแนนสูงสุดล่ะ?**  
เปลี่ยนส่วน `<=3` ของสูตรเป็น `<=5` (หรือจำนวนที่ต้องการ) กฎจะปรับอัตโนมัติ

**สามารถใช้หลายช่วงการฟอร์แมตได้หรือไม่?**  
ทำได้แน่นอน เรียก `sheet.ConditionalFormattings.Add` อีกครั้งพร้อมช่วงใหม่ แล้วเพิ่มเงื่อนไขให้กับอ็อบเจกต์ `ConditionalFormatting` ใหม่นั้น

**สำหรับเวอร์ชัน Excel เก่า ๆ ล่ะ?**  
Aspose.Cells บันทึกเป็นฟอร์แมต `.xlsx` โดยค่าเริ่มต้น ซึ่งเข้ากันได้กับ Excel 2007 ขึ้นไป หากต้องการ `.xls` ให้ส่ง `SaveFormat.Excel97To2003` ไปยังเมธอด `Save`

**มีผลต่อประสิทธิภาพเมื่อทำงานกับชีตขนาดใหญ่หรือไม่?**  
Conditional formatting ถูกเก็บเป็นเมตาดาต้า จึงไม่เพิ่มขนาดไฟล์อย่างมีนัยสำคัญ อย่างไรก็ตาม การสร้างแถวหลายแสนแถวอาจเพิ่มการใช้หน่วยความจำ—พิจารณาแบ่งการประมวลผลเป็นชุด

---

## ขั้นตอนต่อไป

เมื่อคุณเชี่ยวชาญ **วิธีสร้าง conditional formatting** แล้ว คุณอาจอยากสำรวจ:

- **วิธีสร้างแผนภูมิ Excel** ด้วยโค้ด (อีกหนึ่งความสามารถของ Aspose.Cells)  
- **วิธีตั้งพื้นหลังเซลล์** ตามค่าข้อความ (เช่น “Pass/Fail”)  
- **วิธีใช้ Aspose.Cells สำหรับการตรวจสอบข้อมูล** และรายการดรอป‑ดาวน์  

หัวข้อเหล่านี้ต่อยอดจากพื้นฐานที่คุณเพิ่งเรียนรู้ ทำให้คุณรู้สึกคุ้นเคยทันที

---

## สรุป

เราได้เดินผ่านตัวอย่างครบวงจรตั้งแต่ **สร้าง conditional formatting** ใน Excel workbook ด้วย Aspose.Cells ตั้งแต่การเริ่มต้น workbook, เติมข้อมูล, **ตั้งพื้นหลังเซลล์**, จัดอันดับผู้ทำคะแนนสูงสุด, จนถึงการบันทึกไฟล์ ทุกขั้นตอนครอบคลุมทั้ง **วิธีจัดอันดับเซลล์** และ **วิธีใช้ Aspose** ให้คุณลองรันโค้ด ปรับค่าเกณฑ์ และดูว่าคุณสามารถสร้างรายงานที่ดูเป็นมืออาชีพได้เร็วแค่ไหน มีไอเดียหรือวิธีปรับปรุงเพิ่มเติม? แสดงความคิดเห็นด้านล่าง—ขอให้สนุกกับการเขียนโค้ด!

## สิ่งที่คุณควรเรียนต่อ

บทเรียนต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งรวมโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายขั้นตอนเพื่อให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจวิธีการทำงานแบบต่าง ๆ ในโปรเจกต์ของคุณ

- [Automate Excel Conditional Formatting Using Aspose.Cells for Java&#58; A Complete Guide](/cells/english/java/formatting/automate-conditional-formatting-excel-aspose-cells-java/)
- [How to Create & Format Excel Cells Using Aspose.Cells for Java&#58; A Step‑By‑Step Guide](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)
- [Create an Excel Workbook using Aspose.Cells in Java&#58; A Step‑By‑Step Guide](/cells/english/java/getting-started/create-excel-workbook-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}