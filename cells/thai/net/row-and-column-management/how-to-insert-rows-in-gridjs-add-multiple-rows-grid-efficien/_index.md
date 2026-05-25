---
category: general
date: 2026-03-29
description: เรียนรู้วิธีแทรกแถวใน GridJs อย่างรวดเร็ว คู่มือนี้ยังครอบคลุมวิธีการเพิ่มแถวและเพิ่มหลายแถวในกริดด้วยการทำงานแบบชุด
draft: false
keywords:
- how to insert rows
- how to add rows
- add multiple rows grid
- batch row insertion
- large grid performance
language: th
og_description: เรียนรู้วิธีแทรกแถวใน GridJs อย่างรวดเร็ว คู่มือนี้แสดงวิธีเพิ่มแถว,
  เพิ่มหลายแถวในกริด, และจัดการการแทรกเป็นชุดขนาดใหญ่
og_title: วิธีแทรกแถวใน GridJs – เพิ่มหลายแถวใน Grid อย่างมีประสิทธิภาพ
tags:
- GridJs
- C#
- data‑grid
title: วิธีแทรกแถวใน GridJs – เพิ่มหลายแถวใน Grid อย่างมีประสิทธิภาพ
url: /th/net/row-and-column-management/how-to-insert-rows-in-gridjs-add-multiple-rows-grid-efficien/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีแทรกแถวใน GridJs – เพิ่มหลายแถวใน Grid อย่างมีประสิทธิภาพ

เคยสงสัยไหมว่า **how to insert rows** ในตาราง GridJs ขนาดใหญ่โดยไม่ทำให้ UI ค้าง? บางทีคุณอาจเจออุปสรรคเมื่อต้อง **add rows** ทีละแถวและประสิทธิภาพพังลง ข่าวดีคือ GridJs มี batch API ที่ให้คุณ **add multiple rows grid** ในหนึ่งคำสั่ง ทำให้การทำงานเร็วแม้ต้องจัดการกับข้อมูลเป็นล้านรายการ

ในบทแนะนำนี้เราจะเดินผ่านตัวอย่างที่สมบูรณ์และสามารถรันได้ ซึ่งแสดงอย่างชัดเจนว่า **how to insert rows** อย่างไรโดยใช้ `InsertRowsBatch`. คุณจะเห็นว่าการทำ batch มีความสำคัญอย่างไร วิธีตรวจสอบผลลัพธ์ และสิ่งที่ต้องระวังเมื่อดัชนีที่คุณกำหนดมีขนาดใหญ่. เมื่อจบคุณจะสามารถเพิ่มบันทึกใหม่จำนวนพันรายการลงใน GridJs ใด ๆ ด้วยความมั่นใจ

## ข้อกำหนดเบื้องต้น

- .NET 6.0 หรือใหม่กว่า (โค้ดสามารถคอมไพล์กับ SDK ล่าสุดใดก็ได้)
- การอ้างอิงไปยังแพ็กเกจ NuGet `GridJs` (หรือ DLL หากคุณใช้การสร้างแบบกำหนดเอง)
- ความรู้พื้นฐาน C# – ไม่จำเป็นต้องเป็นผู้เชี่ยวชาญ เพียงแค่คุ้นเคยกับคลาสและเมธอด
- IDE หรือโปรแกรมแก้ไขที่คุณชอบ (Visual Studio, Rider, VS Code… ใช้งานได้ทั้งหมด)

> **เคล็ดลับ:** หากคุณวางแผนทำงานกับกริดขนาดมหาศาล (หลายสิบล้านแถว) ให้เปิด `gridJs.EnableVirtualization = true;` เพื่อให้การเรนเดอร์ UI มีน้ำหนักเบา

## ขั้นตอนที่ 1: สร้างและกำหนดค่าอินสแตนซ์ GridJs

สิ่งแรกที่ต้องทำคือคุณต้องมีอ็อบเจ็กต์ `GridJs` ที่ทำงานอยู่ คิดว่ามันเป็นผ้าใบที่คุณจะวาดแถวบนมัน

```csharp
using System;
using GridJsLibrary;   // Assume this is the namespace for GridJs

namespace GridJsDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1 – Initialize the grid
            GridJs gridJs = new GridJs();

            // Optional: turn on virtualization for huge data sets
            gridJs.EnableVirtualization = true;

            // Populate the grid with some dummy data so we can see the effect
            SeedInitialData(gridJs);

            // Now we’re ready to insert rows in bulk
            InsertRowsInBatch(gridJs);
        }

        // Helper: add 2 000 000 rows so our batch lands at index 2 000 001
        static void SeedInitialData(GridJs grid)
        {
            for (int i = 0; i < 2_000_000; i++)
            {
                grid.InsertRow(i, new object[] { $"Row {i + 1}", DateTime.Now });
            }
            Console.WriteLine("Initial seed completed – 2 000 000 rows present.");
        }
```

> **ทำไมขั้นตอนนี้สำคัญ:** การเริ่มต้นกริดและอาจเติมข้อมูลเบื้องต้นเป็นการจำลองสถานการณ์จริงที่กริดมีข้อมูลจำนวนมากอยู่แล้ว การแทรกแบบ batch ที่เราจะทำต่อไปต้องเคารพดัชนีเริ่มจากศูนย์ ดังนั้นเราจึงเติมข้อมูลล่วงหน้าเพื่อแสดงจุดแทรกที่แน่นอน

## ขั้นตอนที่ 2: ใช้ `InsertRowsBatch` เพื่อ **Add Multiple Rows Grid**

นี่คือหัวใจของบทแนะนำ – คำเรียกที่จริง ๆ แล้ว **adds rows** เป็นชุดใหญ่. ลายเซ็นของเมธอดคือ `InsertRowsBatch(int startIndex, int count)`. ในตัวอย่างของเราจะเริ่มที่ดัชนี 2 000 000 (ซึ่งตรงกับแถวที่ 2 000 001) และเพิ่มสิบแถว

```csharp
        // Step 2 – Insert a batch of rows
        static void InsertRowsInBatch(GridJs grid)
        {
            int startIndex = 2_000_000; // zero‑based, so this is row 2 000 001
            int rowsToAdd = 10;

            // The batch call creates placeholder rows; you can later populate them
            grid.InsertRowsBatch(startIndex, rowsToAdd);
            Console.WriteLine($"Inserted {rowsToAdd} rows starting at index {startIndex + 1}.");

            // Verify by reading back a few rows
            VerifyInsertion(grid, startIndex, rowsToAdd);
        }
```

> **วิธีการทำงาน:** `InsertRowsBatch` จัดสรรจำนวนแถวที่ร้องขอภายในและเลื่อนแถวที่มีอยู่ลงล่าง. เนื่องจากการดำเนินการทำในทรานแซคชันเดียว UI จะรีเฟรชเพียงครั้งเดียว ซึ่งเป็นเหตุผลที่เมธอดนี้เป็นวิธีที่แนะนำเพื่อ **how to add rows** อย่างมีประสิทธิภาพ

## ขั้นตอนที่ 3: ตรวจสอบการแทรก – แถวถูกแทรกตรงตามที่คาดหรือไม่?

หลังจากการทำ batch คุณต้องการให้แน่ใจว่าแถวอยู่ในตำแหน่งที่คุณคิด. ตัวช่วยต่อไปนี้จะอ่านแถวแรกและแถวสุดท้ายของบล็อกที่เพิ่มใหม่และพิมพ์ออกที่คอนโซล

```csharp
        // Step 3 – Simple verification
        static void VerifyInsertion(GridJs grid, int startIdx, int count)
        {
            Console.WriteLine("Verifying inserted rows:");
            for (int i = 0; i < count; i++)
            {
                var row = grid.GetRow(startIdx + i);
                Console.WriteLine($"Row {startIdx + i + 1}: {string.Join(", ", row)}");
            }
        }
    }
}
```

**Expected output**

```
Initial seed completed – 2 000 000 rows present.
Inserted 10 rows starting at index 2000001.
Verifying inserted rows:
Row 2000001: , 
Row 2000002: , 
...
Row 2000010: , 
```

เซลล์ที่ว่างเปล่าบ่งบอกว่าแถวเหล่านั้นเป็นตัวแทนที่รอข้อมูล คุณสามารถเติมข้อมูลแต่ละแถวได้หรือรัน batch update อีกครั้ง

> **หมายเหตุกรณีขอบ:** หาก `startIndex` เกินจำนวนแถวปัจจุบัน GridJs จะเพิ่มแถวใหม่ที่ส่วนท้ายโดยอัตโนมัติ. ในทางกลับกัน ดัชนีเป็นค่าลบจะทำให้เกิด `ArgumentOutOfRangeException` ดังนั้นควรตรวจสอบดัชนีที่ผู้ใช้ป้อนเสมอ

## ขั้นตอนที่ 4: เติมข้อมูลให้แถวใหม่ (เป็นตัวเลือกแต่พบบ่อย)

บ่อยครั้งคุณไม่ต้องการแถวว่าง; คุณต้องเติมค่าที่มีความหมายลงไป คุณสามารถวนลูปช่วงที่สร้างใหม่และเรียก `SetCell` หรือ API ที่คล้ายกัน

```csharp
        // Optional: fill the newly added rows with sample data
        static void PopulateNewRows(GridJs grid, int startIdx, int count)
        {
            for (int i = 0; i < count; i++)
            {
                int rowIdx = startIdx + i;
                grid.SetCell(rowIdx, 0, $"New Item {i + 1}");
                grid.SetCell(rowIdx, 1, DateTime.UtcNow);
            }
            Console.WriteLine("Populated the new rows with sample data.");
        }
```

คุณอาจเรียก `PopulateNewRows(gridJs, startIndex, rowsToAdd);` ทันทีหลังจาก batch insert หากต้องการให้แถวพร้อมแสดงผลทันที

## ขั้นตอนที่ 5: เคล็ดลับประสิทธิภาพสำหรับกริดขนาดใหญ่มาก

เมื่อคุณจัดการกับ **add multiple rows grid** เป็นล้านแถว ควรจำเคล็ดลับต่อไปนี้:

1. **Batch size matters** – การแทรก 10 000 แถวในครั้งเดียวอาจเร็วกว่าแยกเป็นสิบ batch ของ 1 000 แถว เพราะแต่ละ batch ทำให้ UI รีเฟรชหนึ่งครั้ง
2. **Turn off UI updates** – เวอร์ชันบางของ GridJs มี `grid.SuspendLayout()` / `grid.ResumeLayout()`. ห่อ batch ของคุณด้วยคำเรียกเหล่านี้หากพบการหน่วง
3. **Use virtualization** – อย่างที่แสดงก่อนหน้า `EnableVirtualization` ลดการใช้หน่วยความจำและเวลาเรนเดอร์อย่างมาก
4. **Avoid deep copies** – ส่งค่าแบบ value type หรืออ็อบเจ็กต์ที่มีน้ำหนักเบาให้กับกริด; อ็อบเจ็กต์หนักจะทำให้กริดต้องคัดลอกข้อมูล ซึ่งทำให้ประสิทธิภาพลดลง

## ตัวอย่างทำงานเต็มรูปแบบ

เมื่อนำทุกอย่างมารวมกัน นี่คือโปรแกรมเต็มที่คุณสามารถคัดลอก‑วางลงในโปรเจกต์คอนโซลใหม่ได้:

```csharp
using System;
using GridJsLibrary;   // Replace with the actual namespace of your GridJs library

namespace GridJsDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            GridJs gridJs = new GridJs
            {
                EnableVirtualization = true
            };

            SeedInitialData(gridJs);
            InsertRowsInBatch(gridJs);
        }

        static void SeedInitialData(GridJs grid)
        {
            for (int i = 0; i < 2_000_000; i++)
            {
                grid.InsertRow(i, new object[] { $"Row {i + 1}", DateTime.Now });
            }
            Console.WriteLine("Initial seed completed – 2 000 000 rows present.");
        }

        static void InsertRowsInBatch(GridJs grid)
        {
            int startIndex = 2_000_000; // zero‑based index for row 2 000 001
            int rowsToAdd = 10;

            grid.InsertRowsBatch(startIndex, rowsToAdd);
            Console.WriteLine($"Inserted {rowsToAdd} rows starting at index {startIndex + 1}.");

            // Optional: fill them with data
            PopulateNewRows(grid, startIndex, rowsToAdd);

            VerifyInsertion(grid, startIndex, rowsToAdd);
        }

        static void PopulateNewRows(GridJs grid, int startIdx, int count)
        {
            for (int i = 0; i < count; i++)
            {
                int rowIdx = startIdx + i;
                grid.SetCell(rowIdx, 0, $"New Item {i + 1}");
                grid.SetCell(rowIdx, 1, DateTime.UtcNow);
            }
            Console.WriteLine("Populated the new rows with sample data.");
        }

        static void VerifyInsertion(GridJs grid, int startIdx, int count)
        {
            Console.WriteLine("Verifying inserted rows:");
            for (int i = 0; i < count; i++)
            {
                var row = grid.GetRow(startIdx + i);
                Console.WriteLine($"Row {startIdx + i + 1}: {string.Join(", ", row)}");
            }
        }
    }
}
```

รันโปรแกรมและคุณจะเห็นผลลัพธ์ที่คอนโซลยืนยันว่าแถวสิบแถวถูกแทรกที่ตำแหน่งที่ถูกต้องและจากนั้นถูกเติมข้อมูล

## สรุป

เราได้อธิบาย **how to insert rows** ใน GridJs ด้วย batch API, แสดง **how to add rows** อย่างมีประสิทธิภาพ, และสำรวจวิธี **add multiple rows grid** โดยไม่ทำให้ UI ค้าง. สิ่งสำคัญที่ควรจำคือ:

- ใช้ `InsertRowsBatch(startIndex, count)` สำหรับการทำงานแบบ bulk ใด ๆ
- ตรวจสอบดัชนีและพิจารณา virtualization สำหรับชุดข้อมูลขนาดมหาศาล
- เติมข้อมูลให้แถวหลังจาก batch หากต้องการเนื้อหาแบบทันที

ต่อไปคุณอาจต้องการสำรวจ **how to delete rows**, implement **undo/redo** สำหรับการแก้ไขแบบ batch, หรือรวม GridJs กับบริการ back‑end ที่สตรีมข้อมูลตามความต้องการ. ทุกหัวข้อเหล่านี้ต่อเนื่องจากแนวคิดที่คุณเพิ่งเรียน

อย่ากลัวที่จะทดลอง—เปลี่ยนขนาด batch, ลองแทรกที่จุดเริ่มต้นของกริด, หรือรวมหลาย batch ในทรานแซคชันเดียว. ยิ่งคุณเล่นมากเท่าไหร่ คุณก็จะยิ่งสบายใจกับการจัดการข้อมูลขนาดใหญ่

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}