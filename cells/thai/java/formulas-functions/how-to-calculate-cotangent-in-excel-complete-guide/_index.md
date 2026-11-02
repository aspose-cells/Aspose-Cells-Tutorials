---
category: general
date: 2026-06-27
description: วิธีคำนวณโคแทนเจนต์ใน Excel ด้วยสูตร เรียนรู้วิธีตั้งสูตร วิธีใช้ EXPAND
  และเชี่ยวชาญสูตรอาร์เรย์ไดนามิกของ Excel
draft: false
keywords:
- how to calculate cotangent
- how to set formula
- how to use expand
- excel dynamic array formula
- add expand function
language: th
og_description: วิธีคำนวณโคแทนเจนต์ใน Excel ด้วยตัวอย่างที่ชัดเจน การสอนนี้แสดงวิธีตั้งสูตร
  ใช้ EXPAND และทำงานกับสูตรอาร์เรย์ไดนามิกของ Excel
og_title: วิธีคำนวณโคแทนเจนต์ใน Excel – คู่มือขั้นตอนโดยละเอียด
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: How to calculate cotangent in Excel using formulas. Learn how to set
    formula, how to use EXPAND, and master the excel dynamic array formula.
  headline: How to Calculate Cotangent in Excel – Complete Guide
  type: TechArticle
- description: How to calculate cotangent in Excel using formulas. Learn how to set
    formula, how to use EXPAND, and master the excel dynamic array formula.
  name: How to Calculate Cotangent in Excel – Complete Guide
  steps:
  - name: '**Workbook creation** – `new Workbook()` gives us a fresh Excel file in
      memory.'
    text: '**Workbook creation** – `new Workbook()` gives us a fresh Excel file in
      memory.'
  - name: '**Source data** – We fill `A2:A5` with numbers 1‑4; these values will be
      expanded later.'
    text: '**Source data** – We fill `A2:A5` with numbers 1‑4; these values will be
      expanded later.'
  - name: '**How to set formula** – `setFormula` attaches the `EXPAND` expression
      to `A1`. The function tells Excel to spill a 5‑row‑by‑2‑column block based on
      the source range.'
    text: '**How to set formula** – `setFormula` attaches the `EXPAND` expression
      to `A1`. The function tells Excel to spill a 5‑row‑by‑2‑column block based on
      the source range.'
  - name: '**How to calculate cotangent** – The `COT` call uses `PI()/4` (45°). This
      is the core answer to *how to calculate cotangent* in Excel.'
    text: '**How to calculate cotangent** – The `COT` call uses `PI()/4` (45°). This
      is the core answer to *how to calculate cotangent* in Excel.'
  - name: '**Recalculation** – `wb.calculateFormula()` forces Aspose.Cells to evaluate
      all formulas, just like pressing **F9** in the UI.'
    text: '**Recalculation** – `wb.calculateFormula()` forces Aspose.Cells to evaluate
      all formulas, just like pressing **F9** in the UI.'
  - name: '**Result output** – We loop through the spill range to prove that `EXPAND`
      actually created a dynamic array.'
    text: '**Result output** – We loop through the spill range to prove that `EXPAND`
      actually created a dynamic array.'
  - name: '**Saving** – The final workbook, `CotangentDemo.xlsx`, can be opened in
      Excel to see the formulas live.'
    text: '**Saving** – The final workbook, `CotangentDemo.xlsx`, can be opened in
      Excel to see the formulas live.'
  type: HowTo
tags:
- Excel
- Formulas
- Java
- Aspose.Cells
title: วิธีคำนวณโคแทนเจนต์ใน Excel – คู่มือครบถ้วน
url: /th/java/formulas-functions/how-to-calculate-cotangent-in-excel-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีคำนวณโคแทนเจนต์ใน Excel – คู่มือฉบับสมบูรณ์

เคยสงสัย **วิธีคำนวณโคแทนเจนต์ใน Excel** โดยไม่ต้องดึงเครื่องคิดเลขวิทยาศาสตร์ออกมาหรือไม่? คุณไม่ได้เป็นคนเดียว ไม่ว่าคุณจะกำลังสร้างโมเดลการเงิน, แผ่นงานฟิสิกส์, หรือแค่ชอบเล่นกับตรีโกณมิติ การเชี่ยวชาญฟังก์ชันโคแทนเจนต์ใน Excel สามารถช่วยคุณประหยัดเวลาได้มาก

ในบทเรียนนี้เราจะยังแสดง **วิธีตั้งสูตร** อย่างโปรแกรมมิ่งโดยใช้ไลบรารี Aspose.Cells ของ Java, เจาะลึก **วิธีใช้ EXPAND**, และอธิบายว่าทำไมฟีเจอร์ **excel dynamic array formula** ถึงสำคัญ สุดท้ายคุณจะได้ตัวอย่างที่สามารถรันได้เต็มรูปแบบซึ่งเพิ่มฟังก์ชัน EXPAND, คำนวณโคแทนเจนต์, และพิมพ์ผลลัพธ์—ทั้งหมดในโค้ดไม่เกินสิบบรรทัด

## สิ่งที่คุณจะได้เรียนรู้

- ไวยากรณ์ของฟังก์ชัน `COT` ของ Excel และเหตุผลที่เป็นวิธีที่เร็วที่สุดในการรับค่าคโทแนนต์  
- วิธี **ตั้งสูตร** บนเซลล์ของเวิร์กชีตโดยใช้โค้ด Java  
- กลไกเบื้องหลัง **วิธีใช้ EXPAND** สำหรับอาเรย์แบบไดนามิก  
- เวลาและวิธี **เพิ่มฟังก์ชัน expand** ลงในเวิร์กบุ๊กสำหรับการคำนวณช่วง‑สเปรด  
- เคล็ดลับการแก้ปัญหาข้อผิดพลาดทั่วไปกับพฤติกรรม **excel dynamic array formula**

> **ข้อกำหนดเบื้องต้น:**  
> - Java 8+ ติดตั้งแล้ว  
> - Aspose.Cells for Java (รุ่นทดลองหรือเวอร์ชันที่มีลิขสิทธิ์)  
> - ความคุ้นเคยพื้นฐานกับฟังก์ชันของ Excel  

ถ้าคุณมีสิ่งเหล่านี้แล้ว ไปกันเลย

---

## วิธีคำนวณโคแทนเจนต์ใน Excel

ฟังก์ชัน `COT` จะคืนค่าคโทแนนต์ของมุมที่ระบุเป็นเรเดียน ไวยากรณ์ง่าย ๆ คือ:

```excel
=COT(number)
```

โดยที่ *number* คือมุมในเรเดียน สำหรับมุม 45° (π/4 เรเดียน) ผลลัพธ์จะเป็น `1` เพราะ `cot(π/4) = 1`

### ทำไมต้องใช้ `COT` แทนการคำนวณด้วยตนเอง?

คุณอาจเขียน `=1/TAN(angle)` แต่จะทำให้ Excel ต้องประเมินสองฟังก์ชันและอาจเกิดข้อผิดพลาดหารด้วยศูนย์เมื่อมุมเป็นหลายเท่าของ π `COT` เป็นฟังก์ชันในตัว, จัดการกรณีขอบได้, และอ่านง่ายกว่า—โดยเฉพาะเมื่อคุณแชร์ชีตกับทีม

---

## ขั้นตอน‑ต่อ‑ขั้นตอน: ตั้งสูตรด้วย Java (วิธีตั้งสูตร)

ด้านล่างเป็น **โปรแกรม Java ที่ทำงานได้เต็มรูปแบบ** ซึ่งสร้างเวิร์กบุ๊ก, เพิ่มสูตร `COT` ไปยังเซลล์ `B1`, และประเมินค่า เราจะใส่ฟังก์ชัน `EXPAND` เพื่อสาธิตอาเรย์แบบไดนามิก

```java
import com.aspose.cells.*;

public class CotangentDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create a new workbook and get the first worksheet
        Workbook wb = new Workbook();
        Worksheet ws = wb.getWorksheets().get(0);
        Cells cells = ws.getCells();

        // 2️⃣ Populate source data for EXPAND (A2:A5)
        for (int i = 0; i < 4; i++) {
            cells.get(i + 1, 0).putValue(i + 1); // A2=1, A3=2, A4=3, A5=4
        }

        // 3️⃣ **How to set formula** – Apply EXPAND to cell A1
        //    EXPAND(source, rows, columns) creates a spill range.
        cells.get("A1").setFormula("=EXPAND(A2:A5,5,2)");

        // 4️⃣ **How to calculate cotangent** – Apply COT to cell B1
        //    COT(PI()/4) = 1 because cot(45°) = 1
        cells.get("B1").setFormula("=COT(PI()/4)");

        // 5️⃣ Recalculate the workbook so formulas resolve
        wb.calculateFormula();

        // 6️⃣ Retrieve and print results
        System.out.println("EXPAND result (A1 spill range):");
        for (int r = 0; r < 5; r++) {
            for (int c = 0; c < 2; c++) {
                System.out.print(cells.get(r, c).getStringValue() + "\t");
            }
            System.out.println();
        }

        System.out.println("\nCotangent of π/4 (B1): " + cells.get("B1").getStringValue());

        // 7️⃣ Save the workbook (optional)
        wb.save("CotangentDemo.xlsx");
    }
}
```

#### คำอธิบายโค้ด

1. **การสร้าง Workbook** – `new Workbook()` ให้ไฟล์ Excel ใหม่ในหน่วยความจำ  
2. **ข้อมูลต้นทาง** – เราเติม `A2:A5` ด้วยตัวเลข 1‑4; ค่าต่าง ๆ นี้จะถูกขยายต่อไป  
3. **วิธีตั้งสูตร** – `setFormula` แนบนิพจน์ `EXPAND` ไปยัง `A1` ฟังก์ชันบอก Excel ให้สเปรดบล็อก 5 แถว × 2 คอลัมน์ตามช่วงต้นทาง  
4. **วิธีคำนวณโคแทนเจนต์** – การเรียก `COT` ใช้ `PI()/4` (45°) นี่คือคำตอบหลักของ *วิธีคำนวณโคแทนเจนต์* ใน Excel  
5. **การคำนวณใหม่** – `wb.calculateFormula()` บังคับให้ Aspose.Cells ประเมินสูตรทั้งหมด เหมือนกด **F9** ใน UI  
6. **การแสดงผล** – เราวนลูปผ่านช่วงสเปรดเพื่อพิสูจน์ว่า `EXPAND` สร้างอาเรย์แบบไดนามิกจริง ๆ  
7. **การบันทึก** – เวิร์กบุ๊กสุดท้าย `CotangentDemo.xlsx` สามารถเปิดใน Excel เพื่อดูสูตรที่ทำงานอยู่  

> **เคล็ดลับ:** หากคุณใช้ Excel รุ่นที่รองรับอาเรย์แบบไดนามิก (Office 365 หรือ Excel 2021+) ฟังก์ชัน `EXPAND` จะ “สเปรด” อัตโนมัติไปยังเซลล์ข้างเคียง รุ่นเก่าจะคืนค่า `#NAME?` — ดังนั้นตรวจสอบเวอร์ชัน Excel ของคุณเสมอเมื่อ **เพิ่มฟังก์ชัน expand**

---

## วิธีใช้ EXPAND – ทำความเข้าใจ Excel Dynamic Array Formula

`EXPAND` เป็นส่วนหนึ่งของตระกูล **อาเรย์แบบไดนามิก** ของ Excel ที่ถูกนำมาแทนที่การกำหนดช่วงด้วยตนเอง ลายเซ็นของมันคือ:

```excel
=EXPAND(array, rows, columns, [pad_with])
```

- **array** – ช่วงต้นทางที่คุณต้องการขยาย  
- **rows** – จำนวนแถวของช่วงสเปรด (ใช้ `0` เพื่อคงความสูงเดิม)  
- **columns** – จำนวนคอลัมน์ของช่วงสเปรด (ใช้ `0` เพื่อคงความกว้างเดิม)  
- **pad_with** – ค่าตัวเลือกเพื่อเติมเซลล์ที่ว่างเปล่า  

เมื่อคุณเขียน `=EXPAND(A2:A5,5,2)` Excel จะอ่านคอลัมน์สี่แถวและขยายเป็นเมทริกซ์ 5 × 2 โดยเติมเซลล์ที่เหลือด้วย `0` ตามค่าเริ่มต้น ผลลัพธ์จะ “สเปรด” ไปยังเซลล์ใกล้เคียง ทำงานเหมือน **excel dynamic array formula**

### เมื่อใดควรเพิ่มฟังก์ชัน EXPAND

- **การทำให้ข้อมูลเป็นมาตรฐาน** – คุณมีคอลัมน์เดียวแต่ต้องการเมทริกซ์สำหรับกราฟ  
- **การเตรียมข้อมูลสำหรับฟังก์ชันอาเรย์อื่น** – ฟังก์ชันเช่น `FILTER` หรือ `SORT` ยอมรับช่วงสเปรดโดยตรง  
- **หลีกเลี่ยงการคัดลอก‑ลงด้วยตนเอง** – อาเรย์แบบไดนามิกปรับอัตโนมัติเมื่อข้อมูลต้นทางเปลี่ยนแปลง  

---

## ข้อผิดพลาดทั่วไป & วิธีแก้

| ปัญหา | ทำไมเกิดขึ้น | วิธีแก้ |
|-------|--------------|--------|
| `#SPILL!` error | เซลล์เป้าหมายมีข้อมูลอยู่แล้ว | ลบข้อมูลในพื้นที่นั้นหรือย้ายสูตรไปยังเซลล์ว่าง |
| `#NAME?` บน `EXPAND` | เวอร์ชัน Excel ไม่รองรับอาเรย์แบบไดนามิก | อัปเกรดเป็น Office 365/Excel 2021 หรือใช้วิธีสำรองเช่น `INDEX` |
| `#DIV/0!` จาก `COT` | มุมเท่ากับ `0` หรือ `π` (โคแทนเจนต์ไม่กำหนด) | ใช้สูตรห่อ: `=IF(MOD(angle,PI())=0,NA(),COT(angle))` |
| สูตรไม่อัปเดตใน Java | ไม่ได้เรียก `Workbook.calculateFormula()` | ตรวจสอบให้เรียก `calculateFormula()` หลังตั้งสูตรทั้งหมด |

---

## ขยายตัวอย่าง – วิธีคำนวณโคแทนเจนต์เพิ่มเติม

หากต้องการโคแทนเจนต์ของค่าที่เป็น **องศา** ให้แปลงเป็นเรเดียนก่อน:

```java
cells.get("C1").setFormula("=COT(RADIANS(30))"); // cot(30°) ≈ 1.732
```

หรือผสาน `COT` กับฟังก์ชันอาเรย์อื่น:

```excel
=MAP(A2:A5, LAMBDA(x, COT(RADIANS(x))))
```

ฟังก์ชัน `MAP` (มีใน Excel รุ่นใหม่) จะนำ `COT` ไปใช้กับแต่ละองค์ประกอบของช่วงและคืนค่าอาเรย์แบบไดนามิกของค่าคโทแนนต์—เหมาะสำหรับการคำนวณจำนวนมาก

---

## สรุปตัวอย่างทำงานเต็มรูปแบบ

ด้านล่างเป็น **ไฟล์ซอร์สทั้งหมด** ที่คุณสามารถคัดลอก‑วางลงใน IDE ของคุณ ไม่มีการพึ่งพาแบบซ่อนอยู่ ทุกอย่างที่ต้องการอยู่ที่นี่แล้ว



## สิ่งที่คุณควรเรียนต่อไป?

บทเรียนต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งรวมตัวอย่างโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายขั้นตอนเพื่อช่วยคุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจวิธีการทำงานทางเลือกในโครงการของคุณ

- [วิธีใช้ฟังก์ชัน IF ของ Excel](/cells/english/java/basic-excel-functions/how-to-use-excel-if-function/)
- [วิธีตั้งค่าเวอร์ชันเอกสาร Excel ด้วย Aspose.Cells for Java](/cells/english/java/workbook-operations/set-excel-version-aspose-cells-java/)
- [วิธีตั้งค่าภาษาในไฟล์ Excel ด้วย Aspose.Cells .NET สำหรับการสนับสนุนหลายภาษา](/cells/english/net/formulas-functions/specify-language-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}