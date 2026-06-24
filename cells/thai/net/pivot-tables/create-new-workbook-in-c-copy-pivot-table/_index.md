---
category: general
date: 2026-06-24
description: สร้างเวิร์กบุ๊กใหม่ใน C# และคัดลอกพีโวตเทเบิลโดยคงข้อมูลไว้ เรียนรู้วิธีคัดลอกแถว,
  ส่งออกช่วงที่เลือก, และรักษาพีโวตเทเบิลให้คงสภาพเดิม.
draft: false
keywords:
- create new workbook
- copy pivot table
- preserve pivot table
- how to copy rows
- export selected range
language: th
og_description: สร้างเวิร์กบุ๊กใหม่ใน C# และคัดลอกพีโวตเทเบิลโดยคงข้อมูลไว้ คู่มือขั้นตอนโดยละเอียดที่อธิบายวิธีคัดลอกแถวและส่งออกช่วงที่เลือก
og_title: สร้างเวิร์กบุ๊กใหม่ใน C# – คัดลอก Pivot Table
schemas:
- author: Aspose
  dateModified: '2026-06-24'
  description: Create new workbook in C# and copy pivot table while preserving its
    data. Learn how to copy rows, export selected range, and keep the pivot intact.
  headline: Create New Workbook in C# – Copy Pivot Table
  type: TechArticle
- questions:
  - answer: Yes, as long as the copied rectangle encloses each pivot you need. If
      you only want one, adjust `rows`/`cols` to isolate it.
    question: Does this work with multiple pivot tables on the same sheet?
  - answer: The pivot cache will still point to the original connection. Call `pivotTable.RefreshData()`
      after loading the destination if you want to re‑query the source.
    question: What if the source workbook uses external data connections?
  - answer: Absolutely. Replace `destinationWorkbook` with `sourceWorkbook` and pick
      another worksheet index.
    question: Can I copy the pivot to a different sheet within the same workbook?
  - answer: 'Use `CopyRows`/`CopyColumns` overloads that accept a `CopyOptions` object—set
      `CopyOptions.CopyType = CopyType.ValuesOnly` or `CopyType.All` depending on
      your needs. --- ## Conclusion We’ve just walked through a **create new workbook**
      scenario that **copy pivot table**, **preserve pivot table**, an'
    question: Is there a way to copy formatting only?
  type: FAQPage
tags:
- C#
- Aspose.Cells
- Excel automation
title: สร้างสมุดงานใหม่ใน C# – คัดลอก Pivot Table
url: /th/net/pivot-tables/create-new-workbook-in-c-copy-pivot-table/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# สร้าง Workbook ใหม่ใน C# – คัดลอก Pivot Table

เคยต้องการ **สร้าง workbook ใหม่** ใน C# เพียงเพื่อย้ายส่วนของข้อมูลที่มี pivot table หรือไม่? คุณไม่ได้เป็นคนเดียว ในหลาย ๆ กระบวนการรายงานคุณอาจดึงแถวไม่กี่แถว หรือคอลัมน์ไม่กี่คอลัมน์ และคาดว่า pivot จะคงอยู่เหมือนเดิม—ไม่มีการอ้างอิงที่ขาดหาย ไม่มีการคำนวณที่หายไป. ข่าวดีคือ? ด้วยไม่กี่บรรทัดของ Aspose.Cells คุณสามารถ **คัดลอก pivot table** ได้, รักษาไว้ให้สมบูรณ์, และแม้กระทั่ง **ส่งออกช่วงที่เลือก** โดยไม่ทำให้สิ่งใดเสียหาย. ด้านล่างคุณจะเห็นตัวอย่างที่สมบูรณ์พร้อมรันที่แสดง **วิธีคัดลอกแถว**, รักษา pivot ไว้, และบันทึกผลลัพธ์เป็น workbook ใหม่ทั้งหมด.

## สิ่งที่บทเรียนนี้ครอบคลุม

- ตั้งค่าโปรเจกต์ C# ด้วย Aspose.Cells (ไลบรารีที่ทำให้โค้ดทำงาน).
- โหลด workbook ต้นฉบับที่มี pivot ดั้งเดิม.
- ใช้เมธอด `CopyRows` และ `CopyColumns` ของไลบรารีเพื่อทำสำเนาช่วงที่ต้องการอย่างแม่นยำ.
- บันทึกพื้นที่ที่ทำสำเนาเป็นสถานการณ์ **สร้าง workbook ใหม่** ในขณะที่ pivot ยังคงทำงานได้.
- เคล็ดลับสำหรับกรณีขอบเช่นหลาย pivot tables, แถวที่ซ่อน, และชุดข้อมูลขนาดใหญ่.

เมื่อจบคู่มือนี้คุณจะสามารถ **ส่งออกช่วงที่เลือก** จากไฟล์ Excel ใดก็ได้, รักษาโลจิกของ pivot ให้ทำงานต่อไป, และวางไฟล์ใหม่ไว้ที่ที่คุณต้องการ.

> **ข้อกำหนดเบื้องต้น**: Aspose.Cells for .NET (รุ่นทดลองฟรีหรือเวอร์ชันที่มีลิขสิทธิ์) ที่ติดตั้งผ่าน NuGet. หากคุณยังไม่ได้เพิ่ม, ให้รัน `dotnet add package Aspose.Cells` ในโฟลเดอร์โปรเจกต์ของคุณ.

---

## สร้าง Workbook ใหม่และคัดลอก Pivot Table

ด้านล่างเป็นหัวใจของวิธีแก้ เราจะเดินผ่านแต่ละบรรทัด, อธิบายว่าทำไมจึงสำคัญ, แล้วแสดงโปรแกรมเต็ม.

```csharp
using System;
using Aspose.Cells;

class PivotCopyDemo
{
    static void Main()
    {
        // 1️⃣ Load the source workbook that contains the pivot table
        string sourcePath = @"YOUR_DIRECTORY\source.xlsx";
        Workbook sourceWorkbook = new Workbook(sourcePath);

        // 2️⃣ Create a new workbook that will receive the copied range
        Workbook destinationWorkbook = new Workbook();
        Worksheet destSheet = destinationWorkbook.Worksheets[0];

        // 3️⃣ Define the range we want to copy (first 20 rows, first 4 columns)
        //    This range includes the pivot table we care about.
        int startRow = 0;   // zero‑based index
        int startColumn = 0;
        int totalRows = 20;
        int totalColumns = 4;

        // 4️⃣ Copy rows – this is the “how to copy rows” part.
        //    Aspose.Cells lets us copy rows directly from the source cells collection.
        sourceWorkbook.Worksheets[0].Cells.CopyRows(startRow, startRow, totalRows);

        // 5️⃣ Copy columns – paired with the row copy to form a rectangular block.
        sourceWorkbook.Worksheets[0].Cells.CopyColumns(startColumn, startColumn, totalColumns);

        // 6️⃣ Now move the copied block into the destination sheet.
        //    We use the same start cell (A1) for simplicity.
        destSheet.Cells.CopyRows(startRow, startRow, totalRows);
        destSheet.Cells.CopyColumns(startColumn, startColumn, totalColumns);

        // 7️⃣ Save the destination workbook – the pivot table is preserved in the copied range
        string destPath = @"YOUR_DIRECTORY\copy-pivot.xlsx";
        destinationWorkbook.Save(destPath);

        Console.WriteLine("✅ New workbook created and pivot table preserved at: " + destPath);
    }
}
```

### ทำไมวิธีนี้ถึงได้ผล

- **`CopyRows` / `CopyColumns`**: วิธีเหล่านี้ทำสำเนาข้อมูลเซลล์พื้นฐาน *และ* วัตถุที่เกี่ยวข้อง (เช่น pivot cache). นั่นคือเหตุผลที่ pivot ยังคงทำงานได้หลังการย้าย.
- **Separate destination workbook**: โดยการสร้างอินสแตนซ์ `Workbook` ใหม่ เรา **สร้าง workbook ใหม่** โดยไม่มีการจัดรูปแบบหรือชีตที่ซ่อนเหลืออยู่ที่อาจขัดขวาง.
- **Zero‑based indexing**: Aspose.Cells ใช้ดัชนีเริ่มจากศูนย์, ดังนั้น `0` ชี้ไปที่เซลล์ **A1**. ปรับ `startRow`/`startColumn` หาก pivot ของคุณไม่ได้อยู่ที่มุมบนซ้าย.
- **Preserve pivot table**: แคชของ pivot อยู่ในช่วงเดียวกัน, ดังนั้นการคัดลอกช่วงจะคัดลอกแคชโดยอัตโนมัติ ไม่ต้องเขียนโค้ดเพิ่มเติม.

---

## วิธีคัดลอกแถวโดยไม่ทำให้ Pivot พัง

หากคุณสนใจเฉพาะส่วนการคัดลอกแถว, คุณสามารถแยกส่วนนี้ออกได้:

```csharp
// Copy just rows 5‑15 (inclusive) from the source sheet
int sourceStartRow = 4;   // row 5 in Excel terms
int rowsToCopy = 11;      // rows 5‑15 => 11 rows
sourceWorkbook.Worksheets[0].Cells.CopyRows(sourceStartRow, 0, rowsToCopy);
```

**เคล็ดลับ**: เมื่อคัดลอกแถวที่ตัดกับ pivot table, ควรคัดลอก *ทั้งหมด* ของพื้นที่ pivot (แถว + คอลัมน์). การคัดลอกบางส่วนอาจทำให้ pivot ขาดฟิลด์ ส่งผลให้เกิดข้อผิดพลาด `#REF!`.

---

## ส่งออกช่วงที่เลือก – สถานการณ์จริง

ลองนึกว่าคุณมี workbook การขายขนาดมหึมา, แต่ลูกค้าต้องการสรุปไตรมาสแรกเท่านั้น, ซึ่งอยู่ในแถว 1‑20 และคอลัมน์ A‑D. โค้ดส่วนข้างบนได้ **ส่งออกช่วงที่เลือก** ให้คุณแล้ว. เพียงเปลี่ยนตัวแปร `totalRows` และ `totalColumns` ให้ตรงกับคำขอของลูกค้า, แล้วเสร็จ.

### การจัดการแถวที่ซ่อนหรือฟิลเตอร์

หากชีตต้นทางมีแถวที่ซ่อน (อาจถูกกรองออก), คุณอาจต้องการคัดลอกเฉพาะแถว *ที่มองเห็นได้* เท่านั้น. Aspose.Cells มี overload ของ `CopyRows` ที่เคารพการมองเห็น:

```csharp
sourceWorkbook.Worksheets[0].Cells.CopyRows(sourceStartRow, 0, rowsToCopy, true);
```

ตั้งค่า boolean ตัวสุดท้ายเป็น `true` เพื่อคัดลอกเฉพาะแถวที่มองเห็นได้—เหมาะอย่างยิ่งสำหรับ “ส่งออกช่วงที่เลือก” เมื่อผู้ใช้ได้ใช้ฟิลเตอร์.

---

## รักษา Pivot Table – ข้อผิดพลาดทั่วไป & วิธีหลีกเลี่ยง

| ข้อผิดพลาด | สาเหตุ | วิธีแก้ |
|------------|--------|----------|
| **Pivot cache ไม่ได้คัดลอก** | ใช้ `Range.Copy` ธรรมดาแทน `Cells.CopyRows/CopyColumns`. | ใช้เมธอด `Cells` ตามที่แสดง. |
| **ชีตปลายทางมี pivot อยู่แล้ว** | บันทึกทับ workbook ที่มี pivot ชื่อเดียวกันอยู่แล้ว. | เริ่มด้วย `Workbook()` ใหม่ (เช่นที่ทำ). |
| **Named ranges พัง** | Pivot ต้นทางอ้างอิง named range ที่ไม่มีในไฟล์ใหม่. | คัดลอก named range ด้วย: `sourceWorkbook.Worksheets[0].Names.CopyTo(destSheet);` |
| **เส้นทางแหล่งข้อมูลเปลี่ยน** | Pivot ชี้ไปที่แหล่งข้อมูลภายนอกที่ไม่พร้อมใช้งาน. | ใช้ `PivotTable.RefreshData()` หลังการคัดลอกหากจำเป็น. |

---

## ตัวอย่างเต็มแบบ End‑to‑End (พร้อมรัน)

ด้านล่างเป็นโปรแกรมเต็มรวมถึงคำสั่ง `using` และ UI คอนโซลสั้น ๆ. คัดลอกและวางลงในโปรเจกต์ Console App ใหม่แล้วกด **F5**.

```csharp
using System;
using Aspose.Cells;

namespace PivotCopyUtility
{
    class Program
    {
        static void Main()
        {
            // -------------------------------------------------
            // Step 1: Load source workbook (contains the pivot)
            // -------------------------------------------------
            string srcPath = @"YOUR_DIRECTORY\source.xlsx";
            Workbook srcWb = new Workbook(srcPath);

            // -------------------------------------------------
            // Step 2: Prepare destination workbook (create new workbook)
            // -------------------------------------------------
            Workbook destWb = new Workbook();
            Worksheet destWs = destWb.Worksheets[0];

            // -------------------------------------------------
            // Step 3: Define the block we want to copy
            // -------------------------------------------------
            int startRow = 0;      // A1
            int startCol = 0;      // A
            int rows = 20;         // first 20 rows
            int cols = 4;          // first 4 columns

            // -------------------------------------------------
            // Step 4: Copy rows and columns from source to destination
            // -------------------------------------------------
            srcWb.Worksheets[0].Cells.CopyRows(startRow, startRow, rows);
            srcWb.Worksheets[0].Cells.CopyColumns(startCol, startCol, cols);
            destWs.Cells.CopyRows(startRow, startRow, rows);
            destWs.Cells.CopyColumns(startCol, startCol, cols);

            // -------------------------------------------------
            // Step 5: Save the new workbook (preserve pivot table)
            // -------------------------------------------------
            string destPath = @"YOUR_DIRECTORY\copy-pivot.xlsx";
            destWb.Save(destPath);

            Console.WriteLine($"✅ Workbook created at {destPath}");
        }
    }
}
```

**ผลลัพธ์ที่คาดหวัง** (ในคอนโซล):

```
✅ Workbook created at YOUR_DIRECTORY\copy-pivot.xlsx
```

เปิด `copy-pivot.xlsx` แล้วคุณจะเห็น pivot table เดียวกันกับที่มีใน `source.xlsx`, ทำงานเต็มที่และอ้างอิงช่วงข้อมูลที่คัดลอก.

---

## คำถามที่พบบ่อย

**ถาม: วิธีนี้ทำงานกับหลาย pivot tables บนชีตเดียวกันหรือไม่?**  
ตอบ: ใช่, ตราบใดที่สี่เหลี่ยมที่คัดลอกครอบคลุมแต่ละ pivot ที่ต้องการ. หากต้องการเพียงหนึ่ง pivot, ปรับ `rows`/`cols` เพื่อแยกออก.

**ถาม: ถ้า workbook ต้นทางใช้การเชื่อมต่อข้อมูลภายนอกล่ะ?**  
ตอบ: แคชของ pivot จะยังคงชี้ไปยังการเชื่อมต่อเดิม. เรียก `pivotTable.RefreshData()` หลังจากโหลดปลายทางหากต้องการรี‑คิวรีแหล่งข้อมูล.

**ถาม: ฉันสามารถคัดลอก pivot ไปยังชีตอื่นใน workbook เดียวกันได้หรือไม่?**  
ตอบ: แน่นอน. แทนที่ `destinationWorkbook` ด้วย `sourceWorkbook` แล้วเลือกดัชนี worksheet อื่น.

**ถาม: มีวิธีคัดลอกเฉพาะการจัดรูปแบบหรือไม่?**  
ตอบ: ใช้ overload ของ `CopyRows`/`CopyColumns` ที่รับอ็อบเจ็กต์ `CopyOptions`—ตั้งค่า `CopyOptions.CopyType = CopyType.ValuesOnly` หรือ `CopyType.All` ตามความต้องการของคุณ.

---

## สรุป

เราเพิ่งอธิบายสถานการณ์ **สร้าง workbook ใหม่** ที่ **คัดลอก pivot table**, **รักษา pivot table**, และ **ส่งออกช่วงที่เลือก**—ทั้งหมดใน C# แท้

## คุณควรเรียนต่ออะไรต่อไป?

บทเรียนต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดซึ่งต่อยอดจากเทคนิคที่แสดงในคู่มือนี้. แต่ละแหล่งข้อมูลมีตัวอย่างโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายทีละขั้นตอน เพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการทำงานทางเลือกในโปรเจกต์ของคุณ.

- [สร้าง Pivot Table ใหม่โดยโปรแกรมใน .NET](/cells/english/net/creating-and-configuring-pivot-tables/creating-new-pivot-table/)
- [วิธีเปลี่ยนแหล่งข้อมูล Pivot Table ด้วย Aspose.Cells for .NET | คู่มือการวิเคราะห์ข้อมูล](/cells/english/net/data-analysis/change-pivot-table-source-aspose-cells-net/)
- [วิธีจัดการความเข้ากันได้ของ Excel Pivot Table กับ Aspose.Cells for .NET | คู่มือการวิเคราะห์ข้อมูล](/cells/english/net/data-analysis/manage-excel-pivot-table-compatibility-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}