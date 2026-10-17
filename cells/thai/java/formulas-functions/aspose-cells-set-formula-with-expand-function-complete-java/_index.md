---
category: general
date: 2026-10-16
description: Aspose.Cells ตั้งสูตรใน Java ด้วยฟังก์ชัน EXPAND. เรียนรู้ตัวอย่างแบบทีละขั้นตอนและดูวิธีใช้
  EXPAND สำหรับช่วงข้อมูลแบบไดนามิก.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- aspose cells set formula
- how to use expand
- expand function example
- Java Excel automation
- dynamic range formula
language: th
lastmod: 2026-10-16
og_description: Aspose.Cells ตั้งสูตรใน Java โดยใช้ฟังก์ชัน EXPAND. ทำตามตัวอย่างครบถ้วนเพื่อขยายช่วงอย่างไดนามิกในเวิร์กบุ๊ก
  Excel.
og_image_alt: Spreadsheet screenshot showing the EXPAND formula applied to cell B2
  via Aspose.Cells
og_title: Aspose.Cells ตั้งสูตรด้วย EXPAND – บทเรียน Java
schemas:
- author: Aspose
  dateModified: '2026-10-16'
  description: Aspose.Cells set formula in Java using the EXPAND function. Learn a
    step‑by‑step example and see how to use expand for dynamic ranges.
  headline: Aspose.Cells set formula with EXPAND function – complete Java guide
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel formulas
- Spreadsheet automation
title: Aspose.Cells ตั้งสูตรด้วยฟังก์ชัน EXPAND – คู่มือ Java ฉบับสมบูรณ์
url: /th/java/formulas-functions/aspose-cells-set-formula-with-expand-function-complete-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cells ตั้งสูตรด้วยฟังก์ชัน EXPAND – คู่มือ Java ฉบับสมบูรณ์

หากคุณต้องการ **aspose cells set formula** อย่างโปรแกรมเมติก คู่มือนี้จะแสดงให้คุณเห็นอย่างชัดเจน คุณจะได้เรียนรู้วิธีใช้ฟังก์ชัน EXPAND เพื่อสร้างช่วงข้อมูลแบบไดนามิกที่ขยายออกเป็นห้าตารางและห้าคอลัมน์จากเซลล์เริ่มต้น ทั้งหมดจากโค้ด Java

การทำงานกับสูตร Excel จาก Java มักรู้สึกยุ่งยาก แต่ Aspose.Cells จะทำให้ซับซ้อนนั้นหายไป ในส่วนต่อไปนี้เราจะเดินผ่านตัวอย่างเต็มที่สามารถรันได้ อธิบายว่าทำไมแต่ละบรรทัดถึงสำคัญ และสำรวจการเปลี่ยนแปลงทั่วไป เช่น การใช้เซลล์เริ่มต้นที่ต่างกันหรือขนาดการขยายที่เป็นตัวแปร

## สิ่งที่คู่มือนี้ครอบคลุม

* โหลดเวิร์กบุ๊กที่มีอยู่แล้วด้วย Aspose.Cells  
* เข้าถึงแผ่นงานและคอลเลกชันของเซลล์  
* **aspose cells set formula** ด้วยฟังก์ชัน `EXPAND`  
* คำนวณใหม่เวิร์กบุ๊กเพื่อให้สูตรทำงาน  
* บันทึกผลลัพธ์และตรวจสอบไฟล์ที่ได้  

ไม่จำเป็นต้องใช้ไลบรารีภายนอกนอกจาก Aspose.Cells และโค้ดสามารถทำงานบน Java 8+ ใดก็ได้ เมื่อเสร็จแล้วคุณจะสามารถปรับใช้รูปแบบนี้กับสูตรไดนามิกอื่น ๆ ได้

## ข้อกำหนดเบื้องต้น

* Java Development Kit (JDK) 8 หรือใหม่กว่า  
* Aspose.Cells for Java (ดาวน์โหลดจาก [official site](https://downloads.aspose.com/cells/java))  
* ไฟล์ Excel เข้า (`input.xlsx`) ที่วางไว้ในไดเรกทอรีที่ทราบตำแหน่ง  
* ความคุ้นเคยพื้นฐานกับไวยากรณ์ Java และ Maven/Gradle สำหรับการจัดการ dependencies  

## ขั้นตอน 1: ตั้งค่าโปรเจกต์และเพิ่ม Aspose.Cells

หากคุณใช้ Maven ให้เพิ่ม dependency ต่อไปนี้ในไฟล์ `pom.xml` ของคุณ:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- use the latest version -->
</dependency>
```

สำหรับ Gradle รูปแบบที่เทียบเท่าคือ:

```gradle
implementation 'com.aspose:aspose-cells:24.10'
```

> **เคล็ดลับ:** ควรใช้เวอร์ชันล่าสุดที่เสถียรเสมอ; รุ่นใหม่มักมีการปรับปรุงประสิทธิภาพสำหรับการคำนวณสูตร

## ขั้นตอน 2: โหลดเวิร์กบุ๊ก

บรรทัดแรกของโซลูชันของเราจะเปิดเวิร์กบุ๊กที่มีอยู่แล้ว แทนที่ `YOUR_DIRECTORY` ด้วยพาธเต็มที่ไฟล์ `input.xlsx` อยู่

```java
import com.aspose.cells.*;

public class ExpandFunctionDemo {
    public static void main(String[] args) throws Exception {
        // Load an existing workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

*ทำไมส่วนนี้สำคัญ*: การโหลดเวิร์กบุ๊กจะสร้างตัวแทนในหน่วยความจำที่ให้คุณจัดการแผ่นงาน, เซลล์, และสูตรโดยไม่ต้องเข้าถึงระบบไฟล์อีกครั้ง

## ขั้นตอน 3: เข้าถึงแผ่นงานเป้าหมายและคอลเลกชันของเซลล์

เราจะทำงานกับแผ่นงานแรก (ดัชนี 0) วัตถุ `Cells` ให้การเข้าถึงเซลล์แต่ละเซลล์โดยอ้างอิงที่อยู่ได้โดยตรง

```java
        // Access the first worksheet
        Worksheet sheet = workbook.getWorksheets().get(0);
        Cells cells = sheet.getCells();
```

หากต้องการแผ่นงานอื่น ให้เปลี่ยนดัชนีหรือใช้ `get("SheetName")`

## ขั้นตอน 4: **aspose cells set formula** – ใช้ฟังก์ชัน EXPAND

ตอนนี้เราจะตั้งสูตรในเซลล์ **B2** ฟังก์ชัน `EXPAND` รับอาร์กิวเมนต์สามค่า: เซลล์อ้างอิง, จำนวนแถวที่จะขยาย, และจำนวนคอลัมน์ที่จะขยาย

```java
        // Apply the EXPAND function to B2, expanding 5 rows and 5 columns from A2
        cells.get("B2").setFormula("=EXPAND(A2,5,5)");
```

### วิธีใช้ EXPAND

* **เซลล์อ้างอิง (`A2`)** – จุดเริ่มต้นของช่วงไดนามิก  
* **แถว (`5`)** – จำนวนแถวที่ช่วงควรขยายลงด้านล่าง  
* **คอลัมน์ (`5`)** – จำนวนคอลัมน์ที่ช่วงควรขยายไปทางขวา  

คุณสามารถแทนค่าต่าง ๆ ด้วยตัวแปรได้หากต้องการโซลูชันที่ยืดหยุ่น

```java
int rows = 10;
int cols = 3;
cells.get("B2").setFormula(String.format("=EXPAND(A2,%d,%d)", rows, cols));
```

## ขั้นตอน 5: คำนวณใหม่เวิร์กบุ๊ก

หลังจากตั้งสูตรแล้ว คุณต้องบอก Aspose.Cells ให้ประเมินสูตร วิธี `calculateFormula()` จะประมวลผลสูตรทั้งหมดในเวิร์กบุ๊ก

```java
        // Recalculate the workbook so the formula is evaluated
        workbook.calculateFormula();
```

> **ทำไมต้องคำนวณใหม่?**  
> หากไม่เรียกเมธอดนี้ สูตรจะยังคงไม่ได้รับการประเมินและไฟล์ผลลัพธ์จะโชว์ข้อความดิบ `=EXPAND(...)` แทนที่จะเป็นอาเรย์ที่ขยายแล้ว

## ขั้นตอน 6: บันทึกเวิร์กบุ๊กที่อัปเดต

สุดท้ายให้เขียนการเปลี่ยนแปลงลงไฟล์ใหม่ ซึ่งจะทำให้เวิร์กบุ๊กต้นฉบับยังคงอยู่สำหรับการเปรียบเทียบ

```java
        // Save the updated workbook
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

เมื่อคุณเปิด `output.xlsx` ใน Excel เซลล์ **B2** จะแสดงบล็อก 5 × 5 ของค่าที่คัดลอกจากพื้นที่ที่เริ่มต้นที่ **A2** หาก **A2** มีค่าเป็น `1` บล็อกจะโชว์ `1` ในทุกเซลล์ เพราะ `EXPAND` ทำสำเนาค่าต้นฉบับไปทั่วช่วงที่ขยาย

## โค้ดเต็มที่สามารถรันได้

```java
import com.aspose.cells.*;

public class ExpandFunctionDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Load an existing workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Step 2: Access the first worksheet and its cells collection
        Worksheet sheet = workbook.getWorksheets().get(0);
        Cells cells = sheet.getCells();

        // Step 3: Apply the EXPAND function to cell B2, referencing A2 and expanding 5 rows and 5 columns
        cells.get("B2").setFormula("=EXPAND(A2,5,5)");

        // Step 4: Recalculate the workbook so the formula is evaluated
        workbook.calculateFormula();

        // Step 5: Save the updated workbook
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

### ผลลัพธ์ที่คาดหวัง

| B2 | C2 | D2 | E2 | F2 |
|----|----|----|----|----|
| 1  | 1  | 1  | 1  | 1  |
| 1  | 1  | 1  | 1  | 1  |
| 1  | 1  | 1  | 1  | 1  |
| 1  | 1  | 1  | 1  | 1  |
| 1  | 1  | 1  | 1  | 1  |

(ค่าจริงจะขึ้นอยู่กับสิ่งที่ `A2` มีในไฟล์ต้นฉบับของคุณ)

## การเปลี่ยนแปลงทั่วไปและกรณีขอบ

| สถานการณ์ | การเปลี่ยนแปลงโค้ด | เหตุผล |
|----------|-------------|--------|
| **เซลล์เริ่มต้นที่แตกต่าง** | `cells.get("C3").setFormula("=EXPAND(D3,3,2)");` | ใช้เซลล์ใดก็ได้เป็นอ้างอิง; สูตรจะขยายสัมพันธ์กับเซลล์นั้น |
| **ขนาดการขยายแบบตัวแปร** | `int rows = 8; int cols = 4; cells.get("B2").setFormula(String.format("=EXPAND(A2,%d,%d)", rows, cols));` | อนุญาตให้กำหนดช่วงขนาดในเวลารันไทม์, มีประโยชน์ในรายงานที่ขับเคลื่อนด้วยข้อมูล |
| **การขยายขนาดศูนย์** | `=EXPAND(A2,0,0)` | คืนค่าเฉพาะค่าของเซลล์ต้นฉบับ; เหมาะสำหรับตรรกะเงื่อนไขที่อาจเพิ่มขนาดในภายหลัง |
| **ใช้ช่วงที่ตั้งชื่อ** | `cells.get("B2").setFormula("=EXPAND(MyRange,5,5)");` | ทำงานเมื่อ `MyRange` ถูกกำหนดในเวิร์กบุ๊ก; ทำให้สูตรอ่านง่ายขึ้น |

> **ระวัง:** ขนาดอาเรย์สูงสุดของ Excel คือ 16,384 คอลัมน์ × 1,048,576 แถว การพยายามขยายเกินขีดจำกัดนี้จะทำให้เกิดข้อผิดพลาดในการคำนวณ

## เคล็ดลับการดีบัก

* **สูตรไม่ประเมินผล?** ตรวจสอบให้แน่ใจว่าได้เรียก `workbook.calculateFormula();` หลังจากทุกครั้งที่ใช้ `setFormula`  
* **ค่าไม่ตรงคาด?** ยืนยันว่าเซลล์อ้างอิง (`A2` ในตัวอย่าง) มีข้อมูลที่คุณต้องการกระจาย  
* **กังวลเรื่องประสิทธิภาพ** – การขยายขนาดใหญ่จะใช้ทรัพยากรสูง หากคุณต้องการเพียงส่วนย่อย ให้ลดค่าแถว/คอลัมน์ลง  

## สรุป

ตอนนี้คุณมีตัวอย่าง **aspose cells set formula** ที่สมบูรณ์ซึ่งแสดง **วิธีใช้ EXPAND** ใน Java โดยการโหลดเวิร์กบุ๊ก, ตั้งสูตร `EXPAND`, คำนวณใหม่, และบันทึก คุณสามารถสร้างช่วงไดนามิกโดยไม่ต้องทำงานกับ Excel ด้วยตนเอง  

ต่อจากนี้คุณอาจสำรวจ:

* ใช้ฟังก์ชันไดนามิกอื่น ๆ เช่น `FILTER` หรือ `SEQUENCE` กับ Aspose.Cells  
* ฝังตรรกะนี้ในเว็บเซอร์วิสเพื่อสร้างรายงานตามความต้องการ  
* ผสาน `EXPAND` กับการจัดรูปแบบตามเงื่อนไขผ่าน API ของ Aspose.Cells  

ลองทดลองกับเซลล์เริ่มต้นที่ต่างกัน, ขนาดตัวแปร, หรือช่วงที่ตั้งชื่อเพื่อให้เข้ากับสถานการณ์อัตโนมัติของคุณ หากคุณพบว่า **ตัวอย่างฟังก์ชัน expand** นี้เป็นประโยชน์ อย่าลืมแชร์ให้ทีมของคุณหรือร่วมปรับปรุงบน GitHub ขอให้เขียนโค้ดอย่างสนุกสนาน!

## สิ่งที่คุณควรเรียนต่อ

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งข้อมูลมีโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายทีละขั้นตอน เพื่อช่วยคุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการทำงานอื่น ๆ ในโปรเจกต์ของคุณ

- [การเชี่ยวชาญ Aspose.Cells Java: วิธีหยุดการคำนวณสูตรใน Excel](/cells/english/java/calculation-engine/master-aspose-cells-java-interrupt-formula-calculation-workbook/)
- [แปลงตาราง Excel เป็นช่วงโดยใช้ Aspose.Cells Java: คู่มือขั้นตอนโดยละเอียด](/cells/english/java/tables-structured-references/convert-excel-tables-ranges-aspose-cells-java/)
- [วิธีตั้งค่าเวอร์ชันเอกสาร Excel ด้วย Aspose.Cells for Java](/cells/english/java/workbook-operations/set-excel-version-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}