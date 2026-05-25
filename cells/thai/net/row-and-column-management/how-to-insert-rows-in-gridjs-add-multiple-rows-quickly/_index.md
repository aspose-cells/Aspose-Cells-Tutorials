---
category: general
date: 2026-03-01
description: วิธีแทรกแถวใน GridJs อย่างง่าย—เรียนรู้การเพิ่ม 100 แถว, สร้างแถวว่าง,
  และตรวจสอบจำนวนแถวทั้งหมดด้วยไม่กี่บรรทัดของ C#
draft: false
keywords:
- how to insert rows
- add multiple rows
- add 100 rows
- create empty rows
- check total rows
language: th
og_description: วิธีแทรกแถวใน GridJs อย่างรวดเร็ว คู่มือนี้จะแสดงวิธีเพิ่มหลายแถว
  สร้างแถวว่างเปล่า และตรวจสอบจำนวนแถวทั้งหมดด้วยโค้ด C# ที่สะอาด.
og_title: วิธีแทรกแถวใน GridJs – คู่มือเร็ว
tags:
- C#
- GridJs
- data‑grid
title: วิธีแทรกแถวใน GridJs – เพิ่มหลายแถวอย่างรวดเร็ว
url: /th/net/row-and-column-management/how-to-insert-rows-in-gridjs-add-multiple-rows-quickly/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีแทรกแถวใน GridJs – เพิ่มหลายแถวอย่างรวดเร็ว

เคยสงสัย **how to insert rows** ลงใน data‑grid ของ GridJs โดยไม่ต้องเขียนลูปที่ยาวนานไหม? คุณไม่ได้เป็นคนเดียว ในแอประดับองค์กรหลาย ๆ แอปคุณจะเจอจุดที่ต้องการสร้างพื้นที่สำหรับการนำเข้าข้อมูลจำนวนมาก, แม่แบบ, หรือเพียงแค่ตัวแทนสำหรับข้อมูลในอนาคต ข่าวดีคือ GridJs มีเมธอดเดียวที่ทำงานหนักให้คุณ

ในบทแนะนำนี้เราจะเดินผ่านตัวอย่างที่สมบูรณ์และสามารถรันได้ ซึ่งจะแสดงวิธี **add 100 rows**, **create empty rows**, และ **check total rows** หลังจากดำเนินการ เสร็จแล้วคุณจะมีรูปแบบที่มั่นคงซึ่งสามารถนำไปใช้ในโปรเจกต์ C# ใด ๆ ที่ใช้ GridJs

## ข้อกำหนดเบื้องต้น

- .NET 6.0 หรือใหม่กว่า (API ทำงานเช่นเดียวกันบน .NET Framework 4.8 แต่ SDK ที่ใหม่กว่าให้เครื่องมือที่ดีกว่า)
- การอ้างอิงไปยังแพ็กเกจ NuGet `GridJs` หรือไฟล์ DLL ที่คอมไพล์ซึ่งมีคลาส `GridJs`
- ความคุ้นเคยพื้นฐานกับไวยากรณ์ C# — ไม่ซับซ้อน เพียงแค่คำสั่ง `using` มาตรฐานและพื้นฐานของการเขียนแบบออบเจกต์

หากมีข้อใดข้อหนึ่งทำให้คุณกังวล ให้หยุดสักครู่และจัดการให้เรียบร้อย ขั้นตอนต่อไปสมมติว่าอ็อบเจ็กต์ grid ได้ถูกสร้างแล้วและพร้อมรับแถว

![how to insert rows illustration](gridjs-insert-rows.png)

## ขั้นตอนที่ 1: ตั้งค่าอินสแตนซ์ของ Grid

สิ่งแรกที่ต้องทำคือคุณต้องมีอ็อบเจ็กต์ `GridJs` ในแอปจริง ๆ นี้อาจมาจากชั้นบริการหรือถูกฉีดผ่าน dependency injection แต่เพื่อความชัดเจนเราจะสร้างมันในระดับโลคัล

```csharp
using System;
using GridJsLibrary;   // <-- replace with the actual namespace of GridJs

namespace GridJsDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Create or obtain the grid you want to modify
            GridJs gridJs = new GridJs();   // replace with your actual grid initialization
```

> **ทำไมเรื่องนี้สำคัญ:** การสร้างอินสแตนซ์ของ grid ทำให้คุณได้สภาพแวดล้อมที่สะอาด ป้องกันไม่ให้ตรรกะการแทรกแถวชนกับสถานะที่เหลือจากการรันก่อนหน้า

## ขั้นตอนที่ 2: แทรก 100 แถวที่ตำแหน่งเฉพาะ

ต่อไปคือหัวใจของ **how to insert rows** เมธอด `InsertRows` รับอาร์กิวเมนต์สองค่า: ดัชนีเริ่มต้นที่นับจากศูนย์และจำนวนแถวที่ต้องการเพิ่ม เรามาแทรก 100 แถวโดยเริ่มที่แถว 5

```csharp
            // Step 2: Insert 100 rows starting at row index 5 (zero‑based)
            // This pushes existing rows down and creates space for new data.
            gridJs.InsertRows(5, 100);
```

> **เคล็ดลับ:** หากคุณต้องการเพิ่มแถวที่ส่วนสุดท้ายของ grid คุณสามารถใช้ `gridJs.RowCount` เป็นดัชนีเริ่มต้นได้ วิธีนี้คุณจะทำการ “ต่อท้าย” แทนการแทรก

### สิ่งที่เกิดขึ้นภายใน

- **Memory Allocation:** `InsertRows` จัดสรรบล็อกของอ็อบเจ็กต์แถวเปล่าภายใน ดังนั้นคุณไม่ต้องสร้างแต่ละแถวด้วยตนเอง
- **Index Shifting:** แถวทั้งหมดที่อยู่ที่ดัชนี 5 หรือหลังจากนั้นจะเลื่อนลง 100 ตำแหน่ง โดยคงข้อมูลเดิมไว้
- **Performance:** เนื่องจากการดำเนินการทำในหนึ่งคำเรียกเดียว มักจะเร็วกว่าการวนลูป `InsertRow` 100 ครั้ง

## ขั้นตอนที่ 3: ตรวจสอบการแทรก (Check Total Rows)

หลังจากที่คุณเพิ่มแถวแล้ว การ **check total rows** เป็นนิสัยที่ดีเพื่อยืนยันว่าการดำเนินการสำเร็จ property `RowCount` ให้จำนวนแถวปัจจุบันใน grid

```csharp
            // Step 3: (Optional) Verify the insertion or continue processing
            int newRowCount = gridJs.RowCount; // example property to check total rows
            Console.WriteLine($"Grid now contains {newRowCount} rows.");
```

หากคุณเริ่มต้นด้วยเช่น 20 แถว คุณควรเห็น `120` ปรากฏบนคอนโซล ขั้นตอนการตรวจสอบง่าย ๆ นี้สามารถประหยัดเวลาการดีบักหลายชั่วโมงในภายหลัง

## ขั้นตอนที่ 4: เติมข้อมูลให้แถวเปล่าที่สร้างใหม่ (Optional)

บ่อยครั้งคุณอาจต้องการเติมข้อมูลในแถวที่สร้างใหม่เหล่านั้นด้วยข้อมูลตัวแทนหรืออ็อบเจ็กต์ค่าเริ่มต้น เนื่องจาก `InsertRows` ให้บล็อกของแถวเปล่า คุณสามารถวนลูปช่วงนั้นและกำหนดค่าได้

```csharp
            // Optional: Fill the newly created rows with default values
            for (int i = 5; i < 5 + 100; i++)
            {
                var row = gridJs.GetRow(i); // assume GetRow returns a mutable row object
                row["Name"] = $"Placeholder {i - 4}";
                row["CreatedOn"] = DateTime.UtcNow;
            }

            // Verify a sample row
            var sample = gridJs.GetRow(5);
            Console.WriteLine($"First inserted row name: {sample["Name"]}");
        }
    }
}
```

> **เหตุผลที่คุณอาจทำเช่นนี้:** การสร้างแถวเปล่าเป็นประโยชน์เมื่อคุณต้องการแม่แบบสำหรับการป้อนข้อมูลของผู้ใช้, ตัวแทนการอัปโหลดเป็นชุด, หรือเพียงแค่ต้องการสำรองพื้นที่สำหรับการคำนวณในอนาคต

## ความแปรผันทั่วไปและกรณีขอบ

### การเพิ่มแถวน้อยกว่า 100 แถว

หากคุณต้องการ **add multiple rows** เพียง 10 หรือ 25 แถว การเรียก `InsertRows` เดียวกันก็ใช้ได้; เพียงเปลี่ยน `100` เป็นจำนวนที่ต้องการ

```csharp
gridJs.InsertRows(startIndex, 25); // adds 25 rows
```

### แทรกที่ด้านบนของ Grid

ต้องการเพิ่มแถวที่ด้านบน? ใช้ `0` เป็นดัชนีเริ่มต้น:

```csharp
gridJs.InsertRows(0, 5); // adds 5 rows at the very beginning
```

### การจัดการดัชนีที่อยู่นอกช่วง

การส่งดัชนีที่ใหญ่กว่า `RowCount` จะทำให้เกิด `ArgumentOutOfRangeException` ป้องกันเหตุการณ์นี้ได้โดย:

```csharp
int safeIndex = Math.Min(requestedIndex, gridJs.RowCount);
gridJs.InsertRows(safeIndex, 100);
```

### การจัดการ Grid ที่เป็นแบบอ่านอย่างเดียว

การตั้งค่า GridJs บางอย่างอาจเปิดมุมมองแบบอ่านอย่างเดียว ในกรณีนั้นคุณต้องสลับไปยังอินสแตนซ์ที่เขียนได้หรือปิดฟล็อกอ่านอย่างเดี๋ยวก่อนเรียก `InsertRows`

## เคล็ดลับประสิทธิภาพ

- **Batch Operations:** หากคุณแทรกแถวหลายครั้งในลูป ให้รวมเป็นการเรียก `InsertRows` ครั้งเดียวเมื่อเป็นไปได้ จะลดการจัดสรรรายการภายในใหม่
- **Avoid UI Refreshes:** ใน grid ที่ผูกกับ UI ให้หยุดการเรนเดอร์ (`gridJs.BeginUpdate()`) ก่อนแทรกแถวและเริ่มใหม่ (`gridJs.EndUpdate()`) หลังจากนั้นเพื่อป้องกันการกระพริบ
- **Memory Profiling:** การแทรกจำนวนมาก (เช่น >10,000 แถว) อาจทำให้การใช้หน่วยความจำพุ่งสูง ควรพิจารณาการแบ่งหน้า หรือสตรีมข้อมูลแทนการแทรกครั้งเดียวขนาดใหญ่

## สรุปตัวอย่างทำงานเต็มรูปแบบ

รวมทุกอย่างเข้าด้วยกัน นี่คือตัวโปรแกรมที่สมบูรณ์พร้อมคัดลอก‑วาง:

```csharp
using System;
using GridJsLibrary;   // replace with the actual namespace

namespace GridJsDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Create the grid instance
            GridJs gridJs = new GridJs();

            // Insert 100 rows starting at index 5
            gridJs.InsertRows(5, 100);

            // Verify insertion
            int newRowCount = gridJs.RowCount;
            Console.WriteLine($"Grid now contains {newRowCount} rows.");

            // Optional: Fill new rows with placeholder data
            for (int i = 5; i < 5 + 100; i++)
            {
                var row = gridJs.GetRow(i);
                row["Name"] = $"Placeholder {i - 4}";
                row["CreatedOn"] = DateTime.UtcNow;
            }

            // Show a sample row
            var sample = gridJs.GetRow(5);
            Console.WriteLine($"First inserted row name: {sample["Name"]}");
        }
    }
}
```

รันโปรแกรมนี้แล้วคุณจะเห็นผลลัพธ์บนคอนโซลที่ยืนยันจำนวนแถวและชื่อของแถวตัวแทนแรก นั่นคือคำตอบทั้งหมดสำหรับ **how to insert rows** ใน GridJs พร้อมการตรวจสอบและการเติมข้อมูลแบบเลือก

## สรุป

เราได้อธิบายวิธีแก้ปัญหาแบบครบวงจรสำหรับ **how to insert rows** ใน GridJs ครอบคลุมการ **add 100 rows**, **create empty rows**, และ **check total rows** หลังการดำเนินการ รูปแบบนี้สามารถขยายได้ — เพียงปรับดัชนีเริ่มต้นและจำนวนเพื่อ **add multiple rows** ที่คุณต้องการ

ขั้นตอนต่อไป? ลองผสานเทคนิคนี้กับการนำเข้าข้อมูลจำนวนมากจากไฟล์ CSV หรือทดลองสร้างแถวตามเงื่อนไขจากการป้อนข้อมูลของผู้ใช้ หากคุณสนใจการลบแถว, การจัดเรียง, หรือการใช้รูปแบบตามเงื่อนไข สิ่งเหล่านั้นเป็นการต่อยอดจาก API เดียวกัน

ขอให้เขียนโค้ดอย่างสนุกสนานและขอให้ Grid ของคุณมีขนาดพอดีเสมอ!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}