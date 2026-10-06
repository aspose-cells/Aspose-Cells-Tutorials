---
category: general
date: 2026-03-22
description: วิธีใช้ lambda ใน C# เพื่อทำงานกับสูตร Excel เรียนรู้การเขียนสูตรลงในเซลล์,
  แปลงช่วงเป็นอาร์เรย์, แสดงอาร์เรย์ในคอนโซล, และคำนวณโคแทนเจนต์ใน Excel.
draft: false
keywords:
- how to use lambda
- display array in console
- convert range to array
- write formula to cell
- calculate cotangent in excel
language: th
og_description: วิธีใช้ lambda ใน C# เพื่อจัดการสูตร Excel, แปลงช่วงเป็นอาร์เรย์,
  เขียนสูตรลงในเซลล์, แสดงอาร์เรย์ในคอนโซล, และคำนวณคอตานเจนต์ใน Excel.
og_title: วิธีใช้ Lambda ใน C# กับสูตร Excel – ขั้นตอนต่อขั้นตอน
tags:
- C#
- Aspose.Cells
- Excel Automation
- Lambda Expressions
title: วิธีใช้ Lambda ใน C# กับสูตร Excel – คู่มือฉบับสมบูรณ์
url: /th/net/formulas-functions/how-to-use-lambda-in-c-with-excel-formulas-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีใช้ Lambda ใน C# กับสูตร Excel – คู่มือฉบับสมบูรณ์

เคยสงสัย **วิธีใช้ lambda** เมื่อคุณทำงานอัตโนมัติกับ Excel จาก C# หรือไม่? คุณไม่ได้อยู่คนเดียว นักพัฒนาหลายคนเจออุปสรรคเมื่อต้องผสานพลังของฟังก์ชันอาเรย์ไดนามิกใหม่ของ Excel กับความสามารถ `LAMBDA` ของ C# ข่าวดีคือ? มันค่อนข้างตรงไปตรงมามากเมื่อคุณเห็นชิ้นส่วนต่าง ๆ เข้ากันได้

ในบทเรียนนี้เราจะเดินผ่าน **การเขียนสูตรลงในเซลล์**, **การแปลงช่วงเป็นอาเรย์**, **การแสดงอาเรย์ในคอนโซล**, และแม้กระทั่ง **การคำนวณ cotangent ใน Excel** — ทั้งหมดนี้พร้อมแสดง **วิธีใช้ lambda** ภายในการเรียก `REDUCE` สุดท้ายคุณจะได้โค้ดสั้น ๆ ที่สามารถนำไปวางในโปรเจกต์ .NET ใด ๆ ที่อ้างอิง Aspose.Cells (หรือไลบรารีที่คล้ายกัน)

---

## สิ่งที่คุณจะได้เรียนรู้

- วิธี **เขียนสูตรลงในเซลล์** ด้วย C#  
- วิธี **แปลงช่วงเป็นอาเรย์** ด้วยฟังก์ชัน `EXPAND`  
- วิธี **แสดงอาเรย์ในคอนโซล** หลังการคำนวณ  
- วิธี **คำนวณ cotangent ใน Excel** ด้วย `COT` และ `COTH`  
- ไวยากรณ์ที่แม่นยำสำหรับ **วิธีใช้ lambda** ภายในฟังก์ชัน `REDUCE` ของ Excel จาก C#

> **ข้อกำหนดเบื้องต้น:** คุณต้องมี .NET เวอร์ชันล่าสุด (Core 6+ หรือ .NET Framework 4.7+) และไลบรารี Aspose.Cells for .NET ที่ติดตั้งผ่าน NuGet

---

## ขั้นตอนที่ 1: ตั้งค่า Workbook และเขียนสูตรลงในเซลล์

สิ่งแรกที่เราทำคือสร้าง workbook ใหม่และดึง worksheet แรกออกมา จากนั้นเราจะ **เขียนสูตรลงในเซลล์** – ในที่นี้ `A1` จะเก็บผลลัพธ์ของการเรียก `EXPAND`

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Write formula to A1 – we’ll expand B1:C2 into a 4‑by‑5 array later
        worksheet.Cells["A1"].Formula = "=EXPAND(B1:C2, 4, 5)";
```

**ทำไมสิ่งนี้สำคัญ:** การเขียนสูตรโดยตรงจากโค้ดหมายความว่าคุณสามารถสร้างสเปรดชีตที่ซับซ้อนได้แบบอัตโนมัติโดยไม่ต้องเปิด Excel ซึ่งยังเป็นการเตรียมพื้นฐานสำหรับขั้นตอนต่อไปที่เราจะ **แปลงช่วงเป็นอาเรย์**

---

## ขั้นตอนที่ 2: แปลงช่วงเป็นอาเรย์ด้วย EXPAND

`EXPAND` คือวิธีของ Excel ที่ทำให้ช่วงเล็ก ๆ ขยายเป็นเมทริกซ์ขนาดใหญ่กว่า โดยการวางสูตรใน `A1` Excel จะ “spill” บล็อกขนาด 4 × 5 เริ่มจากเซลล์นั้น จาก C# เราไม่ต้องคัดลอกค่าด้วยตนเอง – ไลบรารีจะทำงานหนักให้เมื่อเราเรียก `Calculate`

```csharp
        // The EXPAND formula will spill into A1:E4 (4 rows × 5 columns)
        // No extra code needed – the workbook will handle the spill.
```

**วิธีใช้ lambda:** ยังไม่ได้ใช้ แต่รอให้ข้อมูลอยู่ในชีตก่อน แล้วเราจะลดค่าโดยใช้ lambda

---

## ขั้นตอนที่ 3: ใช้ LAMBDA ภายใน REDUCE – แก่นของ “วิธีใช้ Lambda”

Excel 365 แนะนำ `REDUCE` ซึ่งรับ **ค่าเริ่มต้น**, **ช่วง**, และ **LAMBDA** ที่บอกวิธีรวมแต่ละองค์ประกอบ จาก C# เราเพียงใส่สตริงสูตร; lambda อยู่ภายในสูตรของ Excel ไม่ได้อยู่ในโค้ด C#

```csharp
        // Reduce the spilled array by summing all its values.
        // This demonstrates how to use lambda inside REDUCE.
        worksheet.Cells["E1"].Formula = "=REDUCE(0, A1:D4, LAMBDA(acc, x, acc + x))";
```

**คำอธิบาย:**  
- `0` คือค่าเริ่มต้นของ accumulator (`acc`)  
- `A1:D4` คือช่วงที่เราต้องการประมวลผล (สี่คอลัมน์แรกของ spill)  
- `LAMBDA(acc, x, acc + x)` บอก Excel ให้บวกค่าแต่ละเซลล์ (`x`) ไปยัง accumulator  

นี่คือสาระสำคัญของ **วิธีใช้ lambda** สำหรับการรวมค่าในบริบทของสเปรดชีต

---

## ขั้นตอนที่ 4: คำนวณ Cotangent ใน Excel – จากองศาไปยังไฮเปอร์โบลิก

หากคุณต้องการผลลัพธ์ตรีโกณมิติ ฟังก์ชัน `COT` และ `COTH` ของ Excel ใช้งานง่าย เราจะวางสูตรเหล่านี้ใน `G1` และ `G2` ตามลำดับ

```csharp
        // Demonstrate trigonometric functions – cotangent and hyperbolic cotangent
        worksheet.Cells["G1"].Formula = "=COT(PI()/4)";   // Expected result: 1
        worksheet.Cells["G2"].Formula = "=COTH(1)";      // Hyperbolic cotangent of 1
```

**ทำไมสิ่งนี้เป็นประโยชน์:** การรู้ **คำนวณ cotangent ใน Excel** สามารถช่วยคุณหลีกเลี่ยงการเขียนโค้ดคณิตศาสตร์แบบกำหนดเอง โดยเฉพาะเมื่อ workbook จะถูกแชร์กับผู้ที่ไม่ใช่นักพัฒนา

---

## ขั้นตอนที่ 5: บังคับให้คำนวณและดึงอาเรย์ที่ขยายออกมา

ต่อไปเราจะบอก workbook ให้ประเมินสูตรทั้งหมด แล้วดึงอาเรย์ที่ spill จาก `A1` นี่คือจุดที่เราจะ **แสดงอาเรย์ในคอนโซล**

```csharp
        // Force calculation of all formulas
        workbook.Calculate();

        // Retrieve the spilled array from A1 as a 2‑D object
        var expanded = worksheet.Cells["A1"].Value;

        // Pretty‑print the 2‑D array to the console
        Console.WriteLine("Expanded array from A1 (4×5):");
        if (expanded is object[,] matrix)
        {
            for (int r = 0; r < matrix.GetLength(0); r++)
            {
                for (int c = 0; c < matrix.GetLength(1); c++)
                {
                    Console.Write($"{matrix[r, c]}\t");
                }
                Console.WriteLine();
            }
        }
        else
        {
            Console.WriteLine("Unexpected data type.");
        }

        // Show the result of the REDUCE lambda
        Console.WriteLine($"\nSum of A1:D4 (via REDUCE lambda): {worksheet.Cells["E1"].Value}");

        // Show cotangent results
        Console.WriteLine($"Cotangent of π/4: {worksheet.Cells["G1"].Value}");
        Console.WriteLine($"Hyperbolic cotangent of 1: {worksheet.Cells["G2"].Value}");
    }
}
```

**สิ่งที่คุณจะเห็น:**  
- เมทริกซ์ 4 × 5 ที่จัดรูปแบบอย่างสวยงามพิมพ์ทีละบรรทัด  
- ผลรวมที่คำนวณโดย lambda ของ `REDUCE`  
- ค่าผลลัพธ์ cotangent สองค่า  

ขั้นตอนนี้สรุปการไหลจาก **เขียนสูตรลงในเซลล์** จนถึง **แสดงอาเรย์ในคอนโซล** อย่างครบถ้วน

---

## ตัวอย่างทำงานเต็มรูปแบบ (พร้อมคัดลอก‑วาง)

ด้านล่างเป็นโปรแกรมทั้งหมดที่คุณสามารถวางในแอปคอนโซลได้ อย่าลืมเพิ่มแพคเกจ `Aspose.Cells` ผ่าน NuGet ก่อน (`dotnet add package Aspose.Cells`)

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Initialize workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Step 2: Write EXPAND formula (convert range to array)
        worksheet.Cells["A1"].Formula = "=EXPAND(B1:C2, 4, 5)";

        // Step 3: Use REDUCE with LAMBDA (how to use lambda)
        worksheet.Cells["E1"].Formula = "=REDUCE(0, A1:D4, LAMBDA(acc, x, acc + x))";

        // Step 4: Calculate cotangent values (calculate cotangent in excel)
        worksheet.Cells["G1"].Formula = "=COT(PI()/4)";   // Expected: 1
        worksheet.Cells["G2"].Formula = "=COTH(1)";

        // Step 5: Force calculation
        workbook.Calculate();

        // Step 6: Retrieve and display the expanded array (display array in console)
        var expanded = worksheet.Cells["A1"].Value;
        Console.WriteLine("Expanded array from A1 (4×5):");
        if (expanded is object[,] matrix)
        {
            for (int r = 0; r < matrix.GetLength(0); r++)
            {
                for (int c = 0; c < matrix.GetLength(1); c++)
                {
                    Console.Write($"{matrix[r, c]}\t");
                }
                Console.WriteLine();
            }
        }
        else
        {
            Console.WriteLine("Unexpected data type.");
        }

        // Show REDUCE result
        Console.WriteLine($"\nSum of A1:D4 (via REDUCE lambda): {worksheet.Cells["E1"].Value}");

        // Show cotangent results
        Console.WriteLine($"Cotangent of π/4: {worksheet.Cells["G1"].Value}");
        Console.WriteLine($"Hyperbolic cotangent of 1: {worksheet.Cells["G2"].Value}");
    }
}
```

**ผลลัพธ์ที่คาดว่าจะเห็นในคอนโซล (ค่าจะเปลี่ยนแปลงตามเนื้อหาเริ่มต้นของ B1:C2 ซึ่งโดยปกติเป็น 0):**

```
Expanded array from A1 (4×5):
0   0   0   0   0
0   0   0   0   0
0   0   0   0   0
0   0   0   0   0

Sum of A1:D4 (via REDUCE lambda): 0
Cotangent of π/4: 1
Hyperbolic cotangent of 1: 1.31303528549933
```

คุณสามารถใส่ค่าของคุณเองใน `B1:C2` ก่อนรัน – เมทริกซ์จะสะท้อนค่าที่คุณใส่เข้าไป

---

## เคล็ดลับระดับมืออาชีพ & จุดหลบหลีกทั่วไป

- **เคล็ดลับ:** หากต้องการให้ช่วงที่ spill เริ่มที่ตำแหน่งอื่น เพียงเปลี่ยนเซลล์เป้าหมาย (`A1`) ฟังก์ชัน `EXPAND` จะเคารพจุดยึดนั้น  
- **ระวัง:** เซลล์ว่างในช่วงต้นจะกลายเป็น `0` ในอาเรย์ที่ spill ซึ่งอาจส่งผลต่อผลรวมของ `REDUCE`  
- **กรณีพิเศษ:** เมื่อ workbook มีสูตรที่พึ่งพาฟังก์ชันเปลี่ยนแปลงบ่อย (เช่น `NOW()`) ให้เรียก `workbook.Calculate()` หลังตั้งสูตรทั้งหมดเพื่อให้ข้อมูลเป็นปัจจุบัน  
- **หมายเหตุประสิทธิภาพ:** สำหรับ spill ขนาดใหญ่ ควรจำกัดขนาดในคำสั่ง `EXPAND` มิฉะนั้นอาจใช้หน่วยความจำเกินความจำเป็น  
- **ความเข้ากันได้:** The `

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}