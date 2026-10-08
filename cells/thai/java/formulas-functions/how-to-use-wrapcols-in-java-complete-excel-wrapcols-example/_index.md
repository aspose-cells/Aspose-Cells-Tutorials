---
category: general
date: 2026-06-21
description: วิธีใช้ WRAPCOLS กับ Aspose.Cells Java เพื่อแปลงอาเรย์เป็นแถว, เขียนสูตรลงในเซลล์,
  และเติมเซลล์ด้วยสูตร – คู่มือขั้นตอนโดยละเอียด
draft: false
keywords:
- how to use wrapcols
- convert array to rows
- write formula to cell
- excel wrapcols example
- populate cells with formula
language: th
og_description: วิธีใช้ WRAPCOLS ใน Java กับ Aspose.Cells เพื่อแปลงอาเรย์เป็นแถว,
  เขียนสูตรลงในเซลล์, และเติมเซลล์ด้วยสูตร—ทั้งหมดในคู่มือเดียว
og_title: วิธีใช้ WRAPCOLS ใน Java – ตัวอย่างเต็มของ Excel WRAPCOLS
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: How to use WRAPCOLS with Aspose.Cells Java to convert array to rows,
    write formula to cell, and populate cells with formula – step‑by‑step guide.
  headline: How to Use WRAPCOLS in Java – Complete Excel WRAPCOLS Example
  type: TechArticle
- description: How to use WRAPCOLS with Aspose.Cells Java to convert array to rows,
    write formula to cell, and populate cells with formula – step‑by‑step guide.
  name: How to Use WRAPCOLS in Java – Complete Excel WRAPCOLS Example
  steps:
  - name: What the Formula Does
    text: '- `{1,2,3}` – a literal array containing three numbers. - `2` – the number
      of columns per row. - Result: - **A1** = 1, **B1** = 2 - **A2** = 3, **B2**
      = (blank)'
  - name: 1. Empty Arrays
    text: 'If the array literal is empty (`{}`), `WRAPCOLS` returns a `#VALUE!` error.
      To avoid breaking your sheet, guard the formula generation:'
  - name: 2. Non‑Numeric Data
    text: '`WRAPCOLS` works with text as well. For example, `WRAPCOLS({"A","B","C","D"},2)`
      produces a two‑column layout of strings. Just remember to quote strings inside
      the array literal.'
  - name: 3. Compatibility
    text: The `WRAPCOLS` function is available in Excel 365 and Excel 2019+ (Office
      2019, Excel for the web). If you need to support older versions, you’ll have
      to fall back to manual looping or use a different spill‑compatible function.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel formulas
- WRAPCOLS
title: วิธีใช้ WRAPCOLS ใน Java – ตัวอย่างครบถ้วนของ Excel WRAPCOLS
url: /th/java/formulas-functions/how-to-use-wrapcols-in-java-complete-excel-wrapcols-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีใช้ WRAPCOLS ใน Java – ตัวอย่าง Excel WRAPCOLS ครบถ้วน

เคยสงสัย **วิธีใช้ WRAPCOLS** เมื่อคุณต้องแปลงอาร์เรย์ง่าย ๆ ให้เป็นตารางที่เป็นระเบียบใน Excel หรือไม่? คุณไม่ได้เป็นคนเดียวที่เจออุปสรรคเมื่อตอนแรกเห็นฟังก์ชัน `WRAPCOLS` แล้วคิดว่า “จะเขียนสูตรนี้ลงในเซลล์จาก Java อย่างไร?” ข่าวดีคือ? มันค่อนข้างตรงไปตรงมาถ้าคุณรู้ขั้นตอนที่ถูกต้อง

ในบทเรียนนี้เราจะเดินผ่านตัวอย่าง Aspose.Cells Java ที่ **แปลงอาร์เรย์เป็นแถว**, เขียนสูตรโดยตรงลงในเซลล์, และแสดงวิธี **เติมเซลล์ด้วยสูตร** สำหรับสถานการณ์จริง เมื่อจบคุณจะเห็นภาพชัดเจนของ **excel wrapcols example** และพร้อมนำไปปรับใช้ในโปรเจกต์ของคุณ

## ข้อกำหนดเบื้องต้น

ก่อนที่เราจะลงลึก, ตรวจสอบให้แน่ใจว่าคุณมี:

- Java 17 หรือใหม่กว่า (โค้ดทำงานกับ JDK ล่าสุดใดก็ได้)
- ไลบรารี Aspose.Cells for Java (คุณสามารถดาวน์โหลด JAR ล่าสุดจาก Maven Central)
- ความเข้าใจพื้นฐานเกี่ยวกับไวยากรณ์ Java และสูตร Excel
- IDE หรือเครื่องมือแก้ไขข้อความธรรมดา—ไม่ต้องการเครื่องมือพิเศษใด ๆ

ทุกอย่างพร้อมหรือยัง? ดีมาก, เริ่มกันเลย

## ขั้นตอนที่ 1: ตั้งค่าโปรเจกต์และโหลด Workbook

สิ่งแรกที่ต้องทำ—สร้างโปรเจกต์ Maven (หรือ Gradle) ใหม่และเพิ่ม dependency ของ Aspose.Cells:

```xml
<!-- pom.xml snippet -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- check for the latest version -->
</dependency>
```

ตอนนี้เราสามารถโหลด Workbook ที่มีอยู่ (หรือสร้างใหม่) และดึง Worksheet แรกออกมาได้:

```java
import com.aspose.cells.*;

public class WrapColsDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the workbook (or create a new one)
        Workbook wb = new Workbook();               // creates a blank workbook
        // Alternatively, load an existing file:
        // Workbook wb = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Step 2: Access the first worksheet
        Worksheet ws = wb.getWorksheets().get(0);
```

> **ทำไมต้องโหลด Workbook** – Aspose.Cells ทำงานกับการแสดงผลในหน่วยความจำของไฟล์ Excel การโหลด (หรือสร้าง) Workbook ทำให้เราสามารถเข้าถึงเซลล์, แถว, และสูตร ซึ่งจำเป็นสำหรับการ **write formula to cell** ใด ๆ

## ขั้นตอนที่ 2: แทรกสูตร WRAPCOLS ลงในเซลล์

หัวใจของบทเรียนอยู่ที่ฟังก์ชัน `WRAPCOLS` มันรับอาร์เรย์หนึ่งมิติและ “ห่อ” ให้เป็นจำนวนคอลัมน์ที่กำหนด, จากนั้นจะ “spill” ค่าที่เหลือไปยังแถวใหม่ นี่คือไวยากรณ์ที่เราจะใช้:

```java
// Step 3: Set a formula that wraps a collection into rows of 2 columns
// The formula WRAPCOLS({1,2,3},2) will produce:
//   Row 1: 1, 2
//   Row 2: 3
ws.getCells().get("A1").setFormula("=WRAPCOLS({1,2,3},2)");
```

สังเกตว่าสูตรเป็นสตริงธรรมดาที่ส่งให้ `setFormula` Aspose.Cells จะทำการประมวลผล—แยกสูตร, คำนวณ, และ spill ผลลัพธ์ลงใน Worksheet นี่เป็นวิธีที่ตรงที่สุดในการ **populate cells with formula** โดยไม่ต้องวนลูปผ่านแถวและคอลัมน์ด้วยตนเอง

### สิ่งที่สูตรทำ

- `{1,2,3}` – อาร์เรย์ลิเทรัลที่มีสามตัวเลข
- `2` – จำนวนคอลัมน์ต่อแถว
- ผลลัพธ์:
  - **A1** = 1, **B1** = 2
  - **A2** = 3, **B2** = (ว่าง)

ถ้าต้องการสามคอลัมน์แทน, เพียงเปลี่ยนอาร์กิวเมนต์ที่สองเป็น `3` แล้วอาร์เรย์จะเติมเต็มแถวเดียว

## ขั้นตอนที่ 3: บันทึก Workbook และตรวจสอบผลลัพธ์

ตอนนี้สูตรอยู่ใน **A1** แล้ว, ให้บันทึก Workbook ลงดิสก์เพื่อให้คุณเปิดใน Excel และดูผลการ spill:

```java
        // (Optional) Save the workbook to see the result
        wb.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

เปิด `output.xlsx` แล้วคุณจะเห็นตามที่คอมเมนต์อธิบาย—สองคอลัมน์ในแถวแรกและค่าที่เหลืออยู่ในแถวที่สอง นี่คือสาระสำคัญของ **excel wrapcols example**

## ขั้นตอนที่ 4: ขยายตัวอย่าง – แปลงอาร์เรย์ขนาดใหญ่ขึ้น

โปรเจกต์จริงมักไม่ใช่แค่สามตัวเลข สมมติว่าคุณมีคอลเลกชันขนาดใหญ่ เช่น `{10,20,30,40,50,60,70}` และต้องการสามคอลัมน์ต่อแถว นี่คือวิธีปรับโค้ด:

```java
String largeArray = "{10,20,30,40,50,60,70}";
int columnsPerRow = 3;
String formula = String.format("=WRAPCOLS(%s,%d)", largeArray, columnsPerRow);
ws.getCells().get("C5").setFormula(formula);
```

ตอนนี้การ spill จะเริ่มที่ **C5**, ให้ผลลัพธ์ดังนี้:

| C5 | D5 | E5 |
|----|----|----|
|10  |20  |30  |
|40  |50  |60  |
|70  |    |    |

นี่แสดงให้เห็นว่าคุณสามารถ **convert array to rows** อย่างไดนามิกได้โดยเพียงแก้ไขสตริงสูตร ไม่ต้องใช้ลูปหรือกำหนดค่าเซลล์ด้วยตนเอง—Aspose.Cells จะจัดการส่วนที่เหลือ

## ขั้นตอนที่ 5: จัดการกรณีขอบและข้อผิดพลาดทั่วไป

### 1. อาร์เรย์ว่าง

ถ้าอาร์เรย์ลิเทรัลว่าง (`{}`), `WRAPCOLS` จะคืนค่า error `#VALUE!` เพื่อหลีกเลี่ยงการทำให้ชีตพัง, ควรตรวจสอบสูตรก่อนสร้าง:

```java
if (arrayContent.isEmpty()) {
    ws.getCells().get("F1").setValue("No data");
} else {
    ws.getCells().get("F1").setFormula(formula);
}
```

### 2. ข้อมูลที่ไม่ใช่ตัวเลข

`WRAPCOLS` ทำงานกับข้อความได้เช่นกัน ตัวอย่าง `WRAPCOLS({"A","B","C","D"},2)` จะสร้างเลย์เอาต์สองคอลัมน์ของสตริง จำไว้ว่าให้ใส่เครื่องหมายคำพูดรอบสตริงภายในอาร์เรย์ลิเทรัล

### 3. ความเข้ากันได้

ฟังก์ชัน `WRAPCOLS` มีใน Excel 365 และ Excel 2019+ (Office 2019, Excel for the web) หากต้องรองรับเวอร์ชันเก่า คุณจะต้องกลับไปใช้การวนลูปด้วยตนเองหรือใช้ฟังก์ชัน spill‑compatible อื่น

## ขั้นตอนที่ 6: เคล็ดลับปฏิบัติและเทคนิคระดับ Pro

- **Pro tip:** ใช้ `Cell.setFormulaLocal` หากต้องการตัวคั่นแบบ locale‑specific (คอมม่า vs เซมิโคลอน) ตามการตั้งค่าภูมิภาคของผู้ใช้
- **ระวัง:** การเขียนทับข้อมูลที่มีอยู่แล้ว พื้นที่ spill จะทับเนื้อหาที่อยู่ในช่วงเป้าหมาย
- **Performance note:** การตั้งสูตรเป็นเรื่องเบา; งานหนักเกิดขึ้นเมื่อคุณ **save** หรือ **recalculate** Workbook หากต้องสร้างสูตรหลายพันสูตร, พิจารณาปิดการคำนวณอัตโนมัติ (`wb.calculateFormula()` ต่อมา) เพื่อเร่งความเร็ว

## ตัวอย่างทำงานเต็มรูปแบบ

ด้านล่างเป็นคลาส Java ที่พร้อมรันครบถ้วนซึ่งรวมทุกอย่างที่เราได้พูดถึง:

```java
import com.aspose.cells.*;

public class WrapColsDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create a new workbook
        Workbook wb = new Workbook();

        // 2️⃣ Grab the first worksheet
        Worksheet ws = wb.getWorksheets().get(0);

        // 3️⃣ Simple WRAPCOLS formula – basic excel wrapcols example
        ws.getCells().get("A1").setFormula("=WRAPCOLS({1,2,3},2)");

        // 4️⃣ Larger array with three columns per row
        String largeArray = "{10,20,30,40,50,60,70}";
        int cols = 3;
        String largeFormula = String.format("=WRAPCOLS(%s,%d)", largeArray, cols);
        ws.getCells().get("C5").setFormula(largeFormula);

        // 5️⃣ Text array demonstration
        ws.getCells().get("G1").setFormula("=WRAPCOLS({\"Apple\",\"Banana\",\"Cherry\",\"Date\"},2)");

        // 6️⃣ Save the result
        wb.save("output.xlsx");
    }
}
```

**ผลลัพธ์ที่คาดหวัง:** เปิด `output.xlsx` แล้วคุณจะเห็นสามพื้นที่ spill แยกกัน:

- **A1:B2** – ตัวเลข 1‑3 ห่อเป็นสองคอลัมน์
- **C5:E7** – ตัวเลข 10‑70 ห่อเป็นสามคอลัมน์
- **G1:H2** – ชื่อผลไม้ห่อเป็นสองคอลัมน์

## สรุป

เราได้ครอบคลุม **วิธีใช้ WRAPCOLS** กับ Aspose.Cells สำหรับ Java, แสดงวิธี **convert array to rows**, **write formula to cell**, และ **populate cells with formula** อย่างสะอาดและทำซ้ำได้ วิธีนี้ขจัดการวนลูปที่น่าเบื่อ, ใช้ประโยชน์จากพฤติกรรม spill ของ Excel, และทำให้โค้ดของคุณกระชับ

พร้อมรับความท้าทายต่อไปหรือยัง? ลองผสาน `WRAPCOLS` กับแหล่งข้อมูลแบบไดนามิก—อาจดึงค่าจากฐานข้อมูล, สร้างสตริงอาร์เรย์แบบเรียลไทม์, แล้วให้ Excel จัดเลย์เอาต์เอง คุณยังสามารถทดลองฟังก์ชัน spill อื่น ๆ เช่น `SEQUENCE` หรือ `FILTER` เพื่อสร้างรายงานที่ลึกซึ้งยิ่งขึ้น

หากเจออุปสรรคใด ๆ, แสดงความคิดเห็นด้านล่างหรือสำรวจเอกสารของ Aspose อย่างละเอียด Happy coding, และสนุกกับพลังของสูตร Excel สมัยใหม่จาก Java!

![ตัวอย่างการใช้ wrapcols](/images/wrapcols-demo.png "วิธีใช้ wrapcols ใน Java – ภาพหน้าจอของข้อมูลที่ spill")

## คุณควรเรียนรู้อะไรต่อไป?

บทเรียนต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งรวมตัวอย่างโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายขั้นตอนเพื่อช่วยคุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการทำงานทางเลือกในโปรเจกต์ของคุณ

- [How to Select Cell Ranges in Excel Using Aspose.Cells for Java (2023 Guide)](/cells/english/java/range-management/aspose-cells-java-select-cell-ranges-excel/)
- [How to Set an Active Cell in Excel Using Aspose.Cells for Java: A Complete Guide](/cells/english/java/cell-operations/aspose-cells-java-set-active-cell-excel/)
- [How to Insert Rows into Excel Workbooks Using Aspose.Cells for Java](/cells/english/java/worksheet-management/aspose-cells-java-insert-rows-excel-workbooks/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}