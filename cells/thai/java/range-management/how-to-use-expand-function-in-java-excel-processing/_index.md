---
category: general
date: 2026-10-10
description: เรียนรู้วิธีใช้ฟังก์ชัน expand ขณะอ่านและเขียนไฟล์ Excel ด้วย Java คู่มือขั้นตอนโดยละเอียดพร้อมโค้ดเต็มและคำอธิบาย
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use expand function
- read and write excel file java
- Java Excel formula
- Aspose.Cells expand
- Excel dynamic range Java
language: th
lastmod: 2026-10-10
og_description: วิธีใช้ฟังก์ชัน expand ขณะอ่านและเขียนไฟล์ Excel ใน Java. ติดตามบทเรียนฉบับเต็มนี้เพื่อเพิ่มช่วงข้อมูลแบบไดนามิกด้วย
  Aspose.Cells.
og_image_alt: Screenshot of Java code using the EXPAND function on an Excel worksheet
og_title: วิธีใช้ฟังก์ชัน expand ในการประมวลผล Excel ด้วย Java – คู่มือเต็ม
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Learn how to use expand function while reading and writing Excel files
    in Java. Step‑by‑step guide with complete code and explanations.
  headline: How to use expand function in Java Excel processing
  type: TechArticle
tags:
- Java
- Excel
- Aspose.Cells
- Formula
title: วิธีใช้ฟังก์ชัน expand ในการประมวลผล Excel ด้วย Java
url: /th/java/range-management/how-to-use-expand-function-in-java-excel-processing/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีใช้ฟังก์ชัน EXPAND ในการประมวลผล Excel ด้วย Java

หากคุณต้องการ **วิธีใช้ฟังก์ชัน EXPAND** ขณะทำงานกับไฟล์ Excel ใน Java คู่มือนี้จะแสดงให้คุณเห็นอย่างชัดเจน เมื่อจบบทเรียนคุณจะสามารถอ่านและเขียนโครงการ Java ที่จัดการไฟล์ Excel ที่ขยายช่วงเซลล์แบบไดนามิกด้วยสูตร `EXPAND` ได้

การทำงานกับสเปรดชีต Excel มักหมายถึงการจัดการสูตรที่ปรับให้เข้ากับขนาดข้อมูลที่เปลี่ยนแปลง ฟังก์ชัน `EXPAND` ที่เปิดตัวในเวอร์ชันล่าสุดของ Excel ช่วยให้คุณขยายการอ้างอิงตามจำนวนแถวและคอลัมน์ที่กำหนดได้ เมื่อรวมกับไลบรารี Java ที่แข็งแรง คุณสามารถทำงานนี้อัตโนมัติโดยไม่ต้องออกจากโค้ดของคุณ

ในบทเรียนนี้คุณจะ:

* โหลดเวิร์กบุ๊กที่มีอยู่ (`read and write excel file java` scenario)  
* ใส่สูตร `EXPAND` ลงในเซลล์  
* คำนวณสูตรใหม่เพื่อให้ค่าที่อัปเดตปรากฏ  
* บันทึกเวิร์กบุ๊กที่อัปเดต  

## สิ่งที่คุณต้องการ

| รายการ | เหตุผล |
|------|--------|
| JDK 17+ | ฟีเจอร์ภาษาใหม่และประสิทธิภาพที่ดีกว่า |
| Maven/Gradle | การรวมไลบรารีง่ายดาย |
| Aspose.Cells for Java | ให้บริการ `Workbook`, `Worksheet`, และเครื่องยนต์สูตร |
| ไฟล์ Excel (`input.xlsx`) | แหล่งที่มาสำหรับสาธิตฟังก์ชัน `EXPAND` |

เพิ่ม Aspose.Cells ไปยังโปรเจกต์ของคุณด้วย Maven:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- Use the latest stable version -->
</dependency>
```

หรือด้วย Gradle:

```groovy
implementation 'com.aspose:aspose-cells:23.12'
```

## ขั้นตอนที่ 1: โหลดเวิร์กบุ๊ก (วิธีใช้ฟังก์ชัน EXPAND – การเริ่มต้น)

การดำเนินการแรกคือการเปิดไฟล์ Excel ที่คุณต้องการแก้ไข `Workbook` แทนไฟล์ทั้งหมดในหน่วยความจำ

```java
import com.aspose.cells.*;

public class ExpandFunctionDemo {
    public static void main(String[] args) throws Exception {
        // Load the workbook from the file system
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

**ทำไมเรื่องนี้ถึงสำคัญ:** การโหลดเวิร์กบุ๊กทำให้คุณเข้าถึงทุกแผ่นงาน, เซลล์, และเครื่องยนต์สูตรภายใน หากไม่มีการโหลดเวิร์กบุ๊กคุณก็ไม่สามารถอ่านหรือเขียนข้อมูล Excel file java ได้

## ขั้นตอนที่ 2: เข้าถึงแผ่นงานเป้าหมาย

เวิร์กบุ๊กส่วนใหญ่มีหลายแผ่น; ตัวอย่างนี้ใช้แผ่นแรก (index 0) คุณยังสามารถดึงแผ่นโดยชื่อได้

```java
        // Access the first worksheet (index 0)
        Worksheet worksheet = workbook.getWorksheets().get(0);
```

**คำอธิบาย:** วัตถุ `Worksheet` เปิดเผยคอลเลกชัน `Cells` ซึ่งเป็นที่ที่คุณตั้งสูตร หากต้องการเป้าหมายแผ่นอื่น ให้เปลี่ยนดัชนีเป็นหมายเลขที่เหมาะสมหรือเรียก `get("SheetName")`

## ขั้นตอนที่ 3: ตั้งค่าฟอร์มูล่า EXPAND (วิธีใช้ฟังก์ชัน EXPAND ในการปฏิบัติ)

ตอนนี้เราจะเขียนสูตร `EXPAND` ลงในเซลล์ **B1** สูตรนี้ขยายการอ้างอิง `A1` โดย **5 rows** และ **1 column** ผลลัพธ์เป็นช่วง `A1:A6` ที่เลื่อนหนึ่งคอลัมน์ไปทางขวา

```java
        // Apply the EXPAND formula to B1
        // =EXPAND(A1,5,1) expands A1 by 5 rows and 1 column
        worksheet.getCells().get("B1").setFormula("=EXPAND(A1,5,1)");
```

**ทำไมวิธีนี้ถึงได้ผล:** `setFormula` เก็บสตริงสูตร; Aspose.Cells จะไม่ประเมินสูตรทันที ฟังก์ชัน `EXPAND` จะถูกประเมินในภายหลังเมื่อเราทริกเกอร์การคำนวณ

## ขั้นตอนที่ 4: คำนวณสูตรใหม่ (สรุปการใช้ฟังก์ชัน EXPAND)

หลังจากใส่สูตรแล้ว ให้สั่งให้เวิร์กบุ๊กคำนวณเซลล์ที่ขึ้นกับสูตรทั้งหมด ขั้นตอนนี้ทำให้ค่าที่อัปเดตปรากฏในแผ่นงาน

```java
        // Recalculate all formulas so the EXPAND result is evaluated
        workbook.calculateFormula();
```

**สิ่งที่เกิดขึ้นเบื้องหลัง:** เครื่องยนต์การคำนวณจะพาร์สนิพจน์ `EXPAND`, กำหนดช่วงใหม่, แล้วเขียนอาเรย์ค่าที่ได้กลับไปยังแผ่นงาน หาก `A1` มีตัวเลข ช่วงที่ขยายจะทำซ้ำตัวเลขนั้นในเซลล์ใหม่ทั้งหมด

## ขั้นตอนที่ 5: บันทึกเวิร์กบุ๊กที่อัปเดต

สุดท้ายให้เขียนเวิร์กบุ๊กที่แก้ไขแล้วกลับไปยังดิสก์ (หรือสตรีมเอาต์พุต) ขั้นตอนนี้ทำให้วงจร **read and write excel file java** เสร็จสมบูรณ์

```java
        // Save the workbook with the new formula evaluated
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

การรันโปรแกรมจะสร้าง `output.xlsx` ที่เซลล์ **B1** ตอนนี้มีช่วง spill ที่สะท้อนค่าของ `A1` ไปยังห้าแถวและหนึ่งคอลัมน์ เปิดไฟล์ใน Excel เพื่อดูอาเรย์ไดนามิกทำงาน

### ผลลัพธ์ที่คาดหวัง

สมมติว่า `A1` มีค่าเลข `42` เซลล์ที่ได้จะเป็น:

| B1 | B2 | B3 | B4 | B5 | B6 |
|----|----|----|----|----|----|
| 42 | 42 | 42 | 42 | 42 | 42 |

หาก `A1` มีข้อความเดียวกัน ข้อความนั้นจะ spill ไปยังช่วงที่ขยาย

## ความแปรผันทั่วไปและกรณีขอบ

| Scenario | Adjustment |
|----------|------------|
| **Different start cell** | Change `"B1"` to any address, e.g., `"C3"` |
| **Expand by columns only** | Use `=EXPAND(A1,0,3)` to grow three columns |
| **Dynamic row count** | Replace the static `5` with a cell reference like `D1` that holds the desired row count |
| **Using a named range** | Replace `A1` with a defined name, e.g., `=EXPAND(MyRange,5,1)` |
| **Formula errors** | Ensure the workbook is saved in a format that supports dynamic arrays (`.xlsx`). Older `.xls` files will truncate the spill. |

### การจัดการสเปรดชีตขนาดใหญ่

เมื่อทำงานกับเวิร์กบุ๊กขนาดใหญ่มาก ให้เรียก `workbook.calculateFormula(CalcOptions)` พร้อมอ็อบเจกต์ `CalcOptions` ที่กำหนดเองเพื่อจำกัดการใช้หน่วยความจำหรือเปิดใช้งานการคำนวณแบบหลายเธรด

```java
CalcOptions options = new CalcOptions();
options.setCalculateOnOpen(true); // Faster if you only need the result later
workbook.calculateFormula(options);
```

## โค้ดเต็ม (พร้อมคัดลอก‑วาง)

```java
import com.aspose.cells.*;

public class ExpandFunctionDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Step 2: Access the first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Step 3: Set a formula that expands the range of A1 by 5 rows and 1 column
        worksheet.getCells().get("B1").setFormula("=EXPAND(A1,5,1)");

        // Step 4: Recalculate all formulas so the new value is evaluated
        workbook.calculateFormula();

        // Step 5: Save the workbook with the updated data
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

> **Note:** Replace `YOUR_DIRECTORY` with the absolute or relative path to your Excel files. The code works on any platform supported by Java (Windows, macOS, Linux).

## สรุป

คุณตอนนี้รู้ **วิธีใช้ฟังก์ชัน EXPAND** ในสภาพแวดล้อม Java เพื่อขยายการอ้างอิงเซลล์แบบไดนามิกแล้ว และได้เห็นเวิร์กโฟลว์ **read and write excel file java** ที่สมบูรณ์โดยใช้ Aspose.Cells ขั้นตอน—การโหลดเวิร์กบุ๊ก, การใส่สูตร `EXPAND`, การคำนวณใหม่, และการบันทึก—ครอบคลุมวงจรชีวิตทั้งหมดของการอัตโนมัติ Excel

**ขั้นตอนต่อไป** ที่คุณอาจสำรวจ:

* ผสาน `EXPAND` กับฟังก์ชัน dynamic‑array อื่น ๆ เช่น `FILTER` หรือ `SORT`.  
* ใช้รูปแบบเดียวกันเพื่อ **read and write excel file java** ข้อมูลจากฐานข้อมูลหรือ REST API.  
* ทดลองใช้การจัดรูปแบบตามเงื่อนไขโดยอิงช่วงที่ขยาย  

Feel free to adapt the example to your own projects, and let the `EXPAND` function simplify any scenario where data size changes over time.

--- 

*เขียนโค้ดให้สนุก!*

## สิ่งที่คุณควรเรียนต่อไป

บทเรียนต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งรวมตัวอย่างโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายขั้นตอนเพื่อช่วยคุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการทำงานทางเลือกในโปรเจกต์ของคุณ

- [วิธีใช้ SEQUENCE ใน Java Excel Workbook – คู่มือขั้นตอนโดยละเอียด](/cells/english/java/formulas-functions/how-to-use-sequence-in-java-excel-workbook-step-by-step-guid/)
- [วิธีใช้ WRAPCOLS ใน Java – ตัวอย่าง Excel WRAPCOLS ครบถ้วน](/cells/english/java/formulas-functions/how-to-use-wrapcols-in-java-complete-excel-wrapcols-example/)
- [วิธีใช้ Reduce ใน Excel ด้วย Java – คู่มือสูตร Lambda](/cells/english/java/formulas-functions/how-to-use-reduce-in-excel-with-java-lambda-formula-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}