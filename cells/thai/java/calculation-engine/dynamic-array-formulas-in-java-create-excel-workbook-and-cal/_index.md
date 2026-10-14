---
category: general
date: 2026-06-30
description: สูตรอาเรย์แบบไดนามิกใน Java ช่วยให้คุณสร้างชีต Excel ที่ทรงพลังได้ เรียนรู้การสร้าง
  Excel workbook ด้วย Java และคำนวณสูตรทั้งหมดอย่างรวดเร็ว.
draft: false
keywords:
- dynamic array formulas
- calculate all formulas
- use lambda formula
- use expand function
- create excel workbook java
language: th
og_description: สูตรอาร์เรย์แบบไดนามิกใน Java ทำให้การอัตโนมัติ Excel ง่ายขึ้น คู่มือนี้แสดงวิธีสร้างไฟล์งาน
  Excel ด้วย Java, ใช้ฟังก์ชัน expand, สูตร lambda, และคำนวณสูตรทั้งหมด.
og_title: สูตรอาร์เรย์แบบไดนามิกใน Java – สร้างเวิร์กบุ๊กและคำนวณสูตร
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Dynamic array formulas in Java let you build powerful Excel sheets.
    Learn to create Excel workbook Java and calculate all formulas quickly.
  headline: 'Dynamic Array Formulas in Java: Create Excel Workbook and Calculate All
    Formulas'
  type: TechArticle
tags:
- Java
- Excel
- Aspose.Cells
title: 'สูตรอาร์เรย์แบบไดนามิกใน Java: สร้างเวิร์กบุ๊ก Excel และคำนวณสูตรทั้งหมด'
url: /th/java/calculation-engine/dynamic-array-formulas-in-java-create-excel-workbook-and-cal/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# สูตรอาเรย์แบบไดนามิกใน Java: สร้าง Excel Workbook และคำนวณสูตรทั้งหมด

เคยสงสัยไหมว่า **สูตรอาเรย์แบบไดนามิก** ทำงานอย่างไรเมื่อคุณทำการอัตโนมัติ Excel ด้วย Java? คุณไม่ได้เป็นคนเดียว—นักพัฒนาหลายคนเจออุปสรรคเมื่อจำเป็นต้องใส่สูตรซับซ้อนอย่าง `EXPAND` หรือ `REDUCE` ลงในเวิร์กบุ๊กโดยไม่ต้องเปิด Excel เอง.  

ข่าวดีคืออะไร? ด้วยไม่กี่บรรทัดของโค้ด Java คุณสามารถ **create Excel workbook Java** สไตล์, ใส่ฟังก์ชันอาเรย์สมัยใหม่เหล่านั้น, แล้ว **calculate all formulas** ได้ในครั้งเดียว ในบทแนะนำนี้เราจะเดินผ่านทุกขั้นตอน, อธิบาย *ทำไม* แต่ละส่วนจึงสำคัญ, และให้ตัวอย่างที่สมบูรณ์พร้อมรันที่คุณสามารถคัดลอก‑วางตรงเข้าสู่โปรเจคของคุณ.

## สิ่งที่คุณจะได้เรียนรู้

- วิธีสร้าง Excel workbook ใหม่โดยใช้ Java (ใช่, ไม่ต้องใช้ UI ของ Excel).  
- กลไกการทำงานของฟังก์ชัน `EXPAND` และวิธีที่มันเปลี่ยนช่วงข้อมูลธรรมดาให้เป็นอาเรย์แบบไดนามิก.  
- วิธี **use lambda formula** syntax กับ `REDUCE` เพื่อทำการรวมแบบกำหนดเอง.  
- การเพิ่มฟังก์ชันตรีโกณมิติและไฮเปอร์โบลิก (`COT`, `COTH`) ที่หลายคนลืมว่ามีในชุดสูตรของ Excel.  
- บรรทัดเดียวที่คุณต้องการเพื่อ **calculate all formulas** ให้เวิร์กบุ๊กแสดงผลลัพธ์ล่าสุด.  

> **Prerequisites:** Java 8+ (สำหรับการสนับสนุน lambda), ไลบรารี Aspose.Cells for Java, และความเข้าใจพื้นฐานเกี่ยวกับสูตร Excel. ไม่ต้องการ dependencies อื่น.  

---

## สูตรอาเรย์แบบไดนามิก: การตั้งค่า Workbook

สิ่งแรกที่ต้องทำ—ให้เราได้อ็อบเจกต์ workbook มาใช้งาน. คลาส `Workbook` จาก Aspose.Cells คือจุดเริ่มต้นของคุณ; คิดว่าเป็นผืนผ้าเปล่าที่สูตรอาเรย์แบบไดนามิกทุกสูตรจะอาศัยอยู่.

```java
import com.aspose.cells.*;

public class DynamicArrayDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook and grab the first worksheet
        Workbook workbook = new Workbook();                     // creates an empty .xlsx in memory
        Worksheet worksheet = workbook.getWorksheets().get(0); // default sheet is Sheet1
```

*ทำไมสิ่งนี้จึงสำคัญ:* การสร้าง workbook ด้วยโปรแกรมทำให้คุณควบคุมรูปแบบไฟล์, การตั้งค่าภูมิภาค, และ—ที่สำคัญที่สุด—การประเมินสูตรโดยไม่ต้องสัมผัสดิสก์เลย.

---

## การใช้ฟังก์ชัน EXPAND เพื่อขยายช่วง

ฟังก์ชัน `EXPAND` คือคำตอบของ Excel สำหรับการ “spill” (กระจาย) ช่วงข้อมูลไปยังพื้นที่ที่ใหญ่ขึ้นตามขนาดที่คุณระบุ. มันเหมาะอย่างยิ่งเมื่อข้อมูลต้นทางอาจเปลี่ยนความยาวในระหว่างการทำงาน.

```java
        // Step 2: Add a formula that expands B1:B3 into a 5‑row, 1‑column array
        worksheet.getCells().get("A1").setFormula("=EXPAND(B1:B3,5,1)");
```

*คำอธิบาย:*  
- `B1:B3` คือช่วงข้อมูลต้นทาง.  
- `5` บอก Excel ให้สร้างห้าแถว, แม้ว่าต้นทางจะสั้นกว่า.  
- `1` บังคับให้เป็นคอลัมน์เดียว.  

เมื่อคุณต่อมาทำ **calculate all formulas**, ผลลัพธ์ใน `A1` จะเป็นการ spill แนวตั้งของห้าค่าที่เติมช่องว่างหากจำเป็น.

---

## การใช้สูตร LAMBDA กับ REDUCE

หากคุณเคยต้องการรวมค่าคอลัมน์แต่ยังต้องการตัวสะสมแบบกำหนดเอง, `REDUCE` ร่วมกับ **lambda formula** คือวิธีที่เหมาะ. ไวยากรณ์อาจดูแปลกในตอนแรก, แต่เป็นวิธีของ Java ที่ฝังฟังก์ชันนิรนามขนาดเล็กเข้าไปในสูตร Excel.

```java
        // Step 3: Add a REDUCE formula that sums the values in B1:B5
        worksheet.getCells().get("A2").setFormula(
            "=REDUCE(0,B1:B5,LAMBDA(a,b,a+b))"
        );
```

*ทำไมต้องใช้?*  
- `0` คือค่าเริ่มต้น (ผลรวมเริ่มต้น).  
- `B1:B5` คืออาเรย์ที่เรากำลังทำการ fold.  
- `LAMBDA(a,b,a+b)` บอกว่า “รับตัวสะสม `a` และองค์ประกอบถัดไป `b`, คืนค่าผลรวมของพวกมัน.”  

คุณสามารถแทนที่ `a+b` ด้วยตรรกะกำหนดเองใด ๆ—เช่นค่าเฉลี่ย, ค่าสูงสุด, หรือแม้กระทั่งการต่อสตริง—ทำให้ `REDUCE` เป็นบล็อกสร้างที่หลากหลาย.

---

## การเพิ่มฟังก์ชันตรีโกณมิติ (COT, COTH)

Excel มีฟังก์ชันช่วยเหลือด้านตรีโกณมิติหลายอย่างที่มักถูกมองข้าม. นี่คือวิธีใส่ cotangent ง่าย ๆ และญาติไฮเปอร์โบลิกของมันลงในชีต.

```java
        // Step 4: COT of π/4 (equals 1)
        worksheet.getCells().get("A3").setFormula("=COT(PI()/4)");

        // Step 5: COTH of 2 (hyperbolic cotangent)
        worksheet.getCells().get("A4").setFormula("=COTH(2)");
```

*เคล็ดลับ:* ฟังก์ชันเหล่านี้จะเคารพโหมดการคำนวณของ workbook โดยอัตโนมัติ, ดังนั้นคุณไม่ต้องเขียนโค้ดเพิ่มเติมเพื่อแปลงองศาเป็นเรเดียน—`PI()` ทำหน้าที่หนักให้.

---

## การคำนวณสูตรทั้งหมดใน Workbook

ตอนนี้สูตรได้ถูกใส่ไว้แล้ว, เราต้อง **calculate all formulas** เพื่อให้เซลล์มีค่าจริงแทนที่จะเป็นข้อความสูตรเท่านั้น. Aspose.Cells ทำให้สิ่งนี้เป็นการเรียกเมธอดเดียว.

```java
        // Step 6: Force evaluation of every formula in the workbook
        workbook.calculateFormula();

        // Optional: Save to disk to see the result
        workbook.save("DynamicArrayDemo.xlsx");
    }
}
```

*สิ่งที่เกิดขึ้นภายใน:* ไลบรารีจะเดินผ่านทุกเซลล์, แก้ไขการพึ่งพา, และ spill ผลลัพธ์อาเรย์ตามที่ต้องการ. หากคุณทำงานกับชีตขนาดใหญ่, คุณสามารถปรับตัวเลือกการคำนวณเพื่อประสิทธิภาพ, แต่ค่าเริ่มต้นทำงานได้ดีในหลายสถานการณ์.

---

## ตัวอย่างทำงานเต็ม (พร้อมคัดลอก‑วาง)

ด้านล่างเป็นโปรแกรมทั้งหมด, พร้อมให้คุณวางลงใน IDE. มันรวมการ import, เมธอด `main`, และการเรียก `save` สุดท้ายเพื่อให้คุณเปิดไฟล์ที่ได้ใน Excel และเห็นการ spill.

```java
import com.aspose.cells.*;

public class DynamicArrayDemo {
    public static void main(String[] args) throws Exception {
        // Create workbook and get first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Populate source data for demonstration
        worksheet.getCells().get("B1").putValue(10);
        worksheet.getCells().get("B2").putValue(20);
        worksheet.getCells().get("B3").putValue(30);
        worksheet.getCells().get("B4").putValue(40);
        worksheet.getCells().get("B5").putValue(50);

        // EXPAND: spill B1:B3 into a 5‑row array
        worksheet.getCells().get("A1").setFormula("=EXPAND(B1:B3,5,1)");

        // REDUCE with LAMBDA: sum B1:B5
        worksheet.getCells().get("A2").setFormula("=REDUCE(0,B1:B5,LAMBDA(a,b,a+b))");

        // Trig functions
        worksheet.getCells().get("A3").setFormula("=COT(PI()/4)");
        worksheet.getCells().get("A4").setFormula("=COTH(2)");

        // Evaluate everything
        workbook.calculateFormula();

        // Save the file for inspection
        workbook.save("DynamicArrayDemo.xlsx");
    }
}
```

**ผลลัพธ์ที่คาดหวังเมื่อคุณเปิด `DynamicArrayDemo.xlsx`:**

| A (ผลลัพธ์) | B (แหล่งข้อมูล) |
|------------|-----------|
| 10         | 10 |
| 20         | 20 |
| 30         | 30 |
| (ว่าง)    | 40 |
| (ว่าง)    | 50 |
| 150 (ผลรวม)  |   |
| 1 (cot)    |   |
| 1.0373… (coth) | |

*สังเกตว่า `A1` spill ห้ารายแถว, แม้ว่าต้นทางมีเพียงสามค่า. นั่นคือพลังของ **dynamic array formulas**.*

---

## ข้อผิดพลาดทั่วไป & เคล็ดลับระดับมืออาชีพ

- **อย่าลืมตั้งค่าโหมดการคำนวณ** หากคุณได้ปิดการคำนวณอัตโนมัติไว้ที่อื่น; มิฉะนั้น `calculateFormula()` จะไม่มีผล.  
- **การชนกันของการ spill อาเรย์:** หากเซลล์อื่นครอบคลุมช่วงที่ต้องการ spill อยู่, Excel จะคืนค่า error `#SPILL!`. ในโค้ด, คุณสามารถล้างพื้นที่เป้าหมายล่วงหน้าด้วย `worksheet.getCells().clear(0, 0, maxRow, maxColumn)`.  
- **ข้อแปลกของไวยากรณ์ Lambda:** ฟังก์ชัน `LAMBDA` คาดหวังพารามิเตอร์คั่นด้วยคอมม่า, ไม่ใช่เซมิโคลอน. พลาดคอมม่าแล้วสูตรทั้งหมดจะไม่สามารถพาร์สได้.  
- **เคล็ดลับประสิทธิภาพ:** เมื่อทำงานกับหลายพันแถว, เรียก `workbook.getSettings().setCalculateFormulaOnOpen(false)` ก่อนการแทรกข้อมูลจำนวนมาก, แล้วเปิดใช้งานใหม่ก่อนการเรียก `calculateFormula()` สุดท้าย.  

---

## ขั้นตอนต่อไป

ตอนนี้คุณได้เชี่ยวชาญ **dynamic array formulas** แล้ว, พิจารณาสำรวจต่อไป:

- **`FILTER`** และ **`SORT`** ฟังก์ชันสำหรับการจัดรูปแบบข้อมูลแบบเรียลไทม์.  
- **`SEQUENCE`** เพื่อสร้างอาเรย์ตัวเลขโดยไม่ต้องอ้างอิงช่วงข้อมูล.  
- การใช้ **named ranges** ร่วมกับ `EXPAND` เพื่อสูตรที่สะอาดและนำกลับมาใช้ใหม่ได้.  

ทั้งหมดนี้สร้างบนแนวคิดเดียวกันที่เราอธิบาย—เพียงเปลี่ยนสตริงสูตรและให้ Aspose.Cells ทำงานหนักให้.

---

## สรุป

ในคู่มือนี้เราได้แสดงอย่างชัดเจนวิธี **create Excel workbook Java**,

## คุณควรเรียนรู้อะไรต่อไป?

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดซึ่งต่อยอดจากเทคนิคที่แสดงในคู่มือนี้. แหล่งข้อมูลแต่ละรายการมีตัวอย่างโค้ดทำงานครบถ้วนพร้อมคำอธิบายขั้นตอนเพื่อช่วยคุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจวิธีการนำไปใช้แบบอื่นในโปรเจคของคุณ.

- [สร้าง Excel Workbook ด้วย Aspose.Cells ใน Java: คู่มือขั้นตอนต่อขั้น](/cells/english/java/getting-started/create-excel-workbook-aspose-cells-java/)
- [คำนวณสูตร Excel ด้วย Java: ปรับประสิทธิภาพด้วย Aspose.Cells](/cells/english/java/calculation-engine/optimize-excel-aspose-cells-java-calculation-chains/)
- [เชี่ยวชาญสูตรอาเรย์ Excel ด้วย Aspose.Cells Java: ปรับการคำนวณและการจัดรูปแบบ](/cells/english/java/formulas-functions/aspose-cells-java-array-formulas-custom-calculations/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}