---
category: general
date: 2026-07-17
description: ใช้ฟังก์ชัน lambda ใน Java เพื่อสร้างเวิร์กบุ๊ก Excel, แสดงการทำงานของฟังก์ชัน
  EXPAND และ REDUCE, และคำนวณฟังก์ชันอาเรย์ใน Excel ด้วย Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- use lambda function java
- create excel workbook java
- use reduce function excel
- use expand function excel
- calculate array functions excel
language: th
lastmod: 2026-07-17
og_description: ใช้ฟังก์ชัน lambda ใน Java เพื่อสร้างเวิร์กบุ๊ก Excel, ใช้ EXPAND
  และ REDUCE, และคำนวณฟังก์ชันอาเรย์ใน Excel – คู่มือขั้นตอนเต็มรูปแบบ.
og_image_alt: Screenshot of use lambda function java creating Excel workbook with
  formulas
og_title: ใช้ฟังก์ชัน Lambda ใน Java – สร้างสมุดงาน Excel ด้วย Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-07-17'
  description: Use lambda function java to create an Excel workbook, demonstrate EXPAND
    and REDUCE functions, and calculate array functions in Excel with Aspose.Cells.
  headline: Use Lambda Function Java to Create Excel Workbook Example
  type: TechArticle
tags:
- Java
- Aspose.Cells
- Excel Automation
- Lambda
title: ใช้ Lambda Function ใน Java เพื่อสร้างตัวอย่าง Excel Workbook
url: /th/java/workbook-operations/use-lambda-function-java-to-create-excel-workbook-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ใช้ Lambda Function Java เพื่อสร้างตัวอย่าง Excel Workbook

ต้องการ **use lambda function java** เพื่อสร้าง Excel workbook? ในบทแนะนำนี้เราจะเดินผ่านตัวอย่างครบวงจรโดยใช้ Aspose.Cells ที่ไม่เพียงสร้างไฟล์เท่านั้น แต่ยังแสดงวิธี **use expand function excel**, **use reduce function excel**, และ **calculate array functions excel** ในสคริปต์เดียวที่ทำตามได้ง่าย.

หากคุณเคยจ้องมองสเปรดชีตและคิดว่า “ต้องมีวิธีการเชิงโปรแกรมเพื่อขยายอาร์เรย์นี้หรือทำให้ตัวเลขเหล่านี้ลดลง” คุณอยู่ในที่ถูกต้อง. เมื่อจบคู่มือคุณจะมีโปรแกรม Java ที่รันได้ซึ่งสร้างไฟล์ Excel, แทรกสูตรสำหรับ EXPAND, REDUCE, COT, และ COTH, แล้วบันทึกผลลัพธ์ที่คำนวณแล้ว — ทั้งหมดนี้แสดงพลังของวิธี **lambda function java**.

---

## ข้อกำหนดเบื้องต้น – สิ่งที่คุณต้องมีก่อนเริ่ม

- **Java Development Kit (JDK) 8+** – โค้ดใช้ lambda expression ดังนั้นต้องแน่ใจว่าคุณใช้ JDK 8 หรือใหม่กว่า.  
- **Aspose.Cells for Java** – ไลบรารีเชิงพาณิชย์ที่ช่วยให้คุณจัดการไฟล์ Excel ได้โดยไม่ต้องติดตั้ง Office. ดาวน์โหลด JAR ล่าสุดจากเว็บไซต์ Aspose แล้วเพิ่มเข้าไปใน classpath ของโปรเจกต์.  
- IDE ธรรมดา (IntelliJ IDEA, Eclipse, VS Code) – ใดก็ได้, แต่ IDE ที่รองรับ Maven/Gradle จะทำให้การจัดการ dependency ง่ายขึ้น.  

ไม่ต้องติดตั้งเพิ่มเติม; ไลบรารีจะจัดการงานหนักทั้งหมดให้คุณ.

---

## ขั้นตอนที่ 1: ตั้งค่าโปรเจกต์และนำเข้า Dependencies

สร้างโปรเจกต์ Maven ใหม่ (หรือ Gradle หากคุณต้องการ) แล้วเพิ่ม dependency ของ Aspose.Cells:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- check for the latest version -->
</dependency>
```

หากคุณไม่ได้ใช้ Maven เพียงวางไฟล์ `aspose-cells-24.10.jar` ลงในโฟลเดอร์ `libs` ของคุณและเพิ่มเข้าไปใน build path.

> **Pro tip:** คอยอัปเดต dependencies ของคุณให้เป็นรุ่นล่าสุด. เวอร์ชันใหม่มักมาพร้อมการปรับปรุงประสิทธิภาพและแก้บั๊กสำหรับฟังก์ชันอย่าง EXPAND และ REDUCE.

---

## ใช้ Lambda Function Java เพื่อสร้าง Excel Workbook

ตอนนี้สภาพแวดล้อมพร้อมแล้ว, เรามา **use lambda function java** เพื่อฝัง LAMBDA expression ลงในสูตร Excel โดยตรง. ฟังก์ชัน REDUCE ใน Excel ต้องการ lambda, และการจัดการสตริงของ Java ทำให้ทำได้ง่าย.

```java
import com.aspose.cells.*;

public class Office365FunctionsDemo {
    public static void main(String[] args) throws Exception {

        // Step 2: Create a new workbook and obtain the first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.getWorksheets().get(0);

        // Step 3: Demonstrate the EXPAND function – expands a seed array to a larger size
        sheet.getCells().get("A1").setFormula("=EXPAND({1,2,3},5,1)");
        // Explanation: EXPAND turns the 3‑element seed into a 5‑row, 1‑column array.

        // Step 4: Demonstrate the REDUCE function – aggregates an array into a single value
        // Here we **use lambda function java** inside the Excel formula.
        sheet.getCells().get("A2").setFormula(
            "=REDUCE(0,{1,2,3,4},LAMBDA(a,b,a+b))"
        );
        // Explanation: Starting at 0, the lambda (a,b) → a+b adds each element together.

        // Step 5: Use the COT function to calculate the cotangent of π/4
        sheet.getCells().get("A3").setFormula("=COT(PI()/4)");

        // Step 6: Use the COTH function to calculate the hyperbolic cotangent of 1
        sheet.getCells().get("A4").setFormula("=COTH(1)");

        // Step 7: Recalculate all formulas so the results are stored in the cells
        workbook.calculateFormula();

        // Step 8: Save the workbook with the evaluated results
        workbook.save("Office365Funcs.xlsx");
    }
}
```

### ทำไมวิธีนี้ถึงได้ผล

- **`Workbook`** คือจุดเริ่มต้นสำหรับงาน **create excel workbook java**. มันเป็นตัวแทนของไฟล์ทั้งหมดในหน่วยความจำ.  
- **`Worksheet`** ให้เรามีแผ่นงานเพื่อทำงาน; workbook เริ่มต้นมาพร้อมแผ่นงานหนึ่งแล้ว.  
- **`setFormula`** แทรกสตริงสูตร Excel ดิบ. สังเกตว่าในบรรทัด REDUCE มีส่วน `LAMBDA(a,b,a+b)` – นี่คือที่เรา **use lambda function java** เพื่อบอก Excel ว่าจะรวมค่าต่าง ๆ อย่างไร.  
- **`calculateFormula()`** บังคับให้ Aspose.Cells ประเมินสูตรทั้งหมด, ดังนั้นค่าที่ได้จะถูกบันทึกลงไฟล์โดยตรง. หากไม่เรียกเมธอดนี้ เซลล์จะมีเพียงข้อความสูตรเท่านั้น.  

---

## วิธีใช้ Expand Function Excel – การขยายอาร์เรย์แบบไดนามิก

ตัวอย่าง **use expand function excel** อยู่ในเซลล์ `A1`. มาดูรายละเอียดของสูตรกัน:

```excel
=EXPAND({1,2,3},5,1)
```

- `{1,2,3}` คืออาร์เรย์ต้นแบบ (สามตัวเลข).  
- `5` บอก Excel ให้ขยายผลลัพธ์เป็นห้าบรรทัด.  
- `1` กำหนดจำนวนคอลัมน์ (เพียงคอลัมน์เดียว).  

เมื่อเปิด workbook ใน Excel, `A1:A5` จะแสดงผลดังนี้:

| A |
|---|
| 1 |
| 2 |
| 3 |
| 0 |
| 0 |

ศูนย์ที่ต่อท้ายเป็นค่ากรอกเพราะอาร์เรย์ต้นแบบไม่มีจำนวนเพียงพอที่จะเติมเต็มขนาดที่ร้องขอ.

> **Common pitfall:** หากลืมเรียก `workbook.calculateFormula()` คุณจะเห็นข้อความสูตรดิบ `=EXPAND(...)` แทนตัวเลขที่ขยายแล้ว.

---

## วิธีใช้ Reduce Function Excel – การบวกด้วย Lambda

บรรทัด **use reduce function excel** อยู่ในเซลล์ `A2`. สูตรมีลักษณะดังนี้:

```excel
=REDUCE(0,{1,2,3,4},LAMBDA(a,b,a+b))
```

- `0` คือค่าตัวสะสมเริ่มต้น.  
- `{1,2,3,4}` คืออาร์เรย์ที่เราต้องการลด.  
- `LAMBDA(a,b,a+b)` บอก Excel ให้บวกแต่ละองค์ประกอบ (`b`) กับผลรวมที่กำลังดำเนินอยู่ (`a`).  

หลังจากคำนวณ, `A2` จะมีค่า **10**. หากต้องการผลคูณแทนผลบวก เพียงเปลี่ยน `a+b` เป็น `a*b` – รูปแบบ **use lambda function java** ยังคงใช้ได้เช่นเดิม.

---

## การคำนวณ Array Functions Excel – COT และ COTH

แม้จะไม่ใช่แบบอาร์เรย์โดยตรง, ฟังก์ชัน COT

## คุณควรเรียนรู้อะไรต่อไป?

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดเทคนิคที่แสดงในคู่มือนี้. แต่ละแหล่งรวมโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายทีละขั้นตอนเพื่อช่วยคุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการทำงานอื่น ๆ ในโปรเจกต์ของคุณ.

- [วิธีใช้ Aspose Cells – บทแนะนำ Excel Engine สำหรับ Java](/cells/english/java/calculation-engine/)
- [Custom SUM Function in Excel using Aspose.Cells Java&#58; Enhance Your Calculations](/cells/english/java/formulas-functions/custom-sum-function-excel-aspose-cells-java/)
- [วิธีใช้ Aspose.Cells สำหรับการทำ Automation ของ Excel Slicer ใน Java](/cells/english/java/advanced-features/excel-slicer-modifications-java-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}