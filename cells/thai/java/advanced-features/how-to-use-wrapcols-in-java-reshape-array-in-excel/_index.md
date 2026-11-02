---
category: general
date: 2026-08-04
description: วิธีใช้ wrapcols พร้อมตัวอย่าง Java ครบถ้วน, ปรับโครงสร้างอาร์เรย์ใน
  Excel และบันทึกเวิร์กบุ๊กเป็นไฟล์โดยใช้ Aspose.Cells
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use wrapcols
- save workbook to file
- reshape array in excel
- excel wrapcols example
- create excel workbook java
language: th
lastmod: 2026-08-04
og_description: วิธีใช้ wrapcols เพื่อปรับรูปแบบอาเรย์ใน Excel ด้วย Java. เรียนรู้ตัวอย่าง
  wrapcols ของ Excel อย่างครบถ้วน, สร้าง workbook Excel ด้วย Java และบันทึก workbook
  ไปยังไฟล์.
og_image_alt: Screenshot showing how to use WRAPCOLS in Java to reshape an array in
  Excel
og_title: วิธีใช้ wrapcols ใน Java – คู่มือแบบขั้นตอนต่อขั้นตอน
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: how to use wrapcols with a complete Java example, reshape array in
    Excel and save workbook to file using Aspose.Cells
  headline: how to use wrapcols in Java – reshape array in Excel
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel automation
title: วิธีใช้ wrapcols ใน Java – ปรับรูปแบบอาร์เรย์ใน Excel
url: /th/java/advanced-features/how-to-use-wrapcols-in-java-reshape-array-in-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีใช้ wrapcols ใน Java – ปรับรูปแบบอาร์เรย์ใน Excel

หากคุณต้องการ **how to use wrapcols** เพื่อเปลี่ยนรายการค่าที่เป็นแถวเดียวให้เป็นช่วงหลายแถว คู่มือนี้จะแสดงขั้นตอนที่แน่นอน คุณจะได้เห็น **excel wrapcols example** ที่ปรับรูปแบบอาร์เรย์ 1‑D ให้เป็นบล็อก 3‑row × 2‑column และคุณจะได้เรียนรู้วิธี **save workbook to file** ด้วย Aspose.Cells.

เมื่อจบบทแนะนำนี้คุณจะสามารถเขียนโค้ด **create excel workbook java** ที่:

* สร้างเวิร์กบุ๊กใหม่และเลือกเซลล์ A1.  
* ใช้ฟังก์ชัน `WRAPCOLS` เพื่อปรับรูปแบบข้อมูล.  
* บังคับให้คำนวณสูตรเพื่อให้ผลลัพธ์แสดงทันที.  
* ดึงค่าจากอาร์เรย์ที่คำนวณแล้ว.  
* บันทึกเวิร์กบุ๊กลงดิสก์.

ข้อกำหนดเบื้องต้นเพียงอย่างเดียวคือสภาพแวดล้อมการพัฒนา Java (JDK 8 หรือใหม่กว่า) และไลบรารี Aspose.Cells for Java.

---

## ข้อกำหนดเบื้องต้น

* JDK 8 + (หรือเวอร์ชันที่ใหม่กว่า)  
* Maven หรือ Gradle เพื่อจัดการการพึ่งพา Aspose.Cells  
* ความคุ้นเคยพื้นฐานกับไวยากรณ์ Java และสูตร Excel  

```xml
<!-- Maven dependency -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest stable version -->
</dependency>
```

> **Pro tip:** หากคุณใช้ Gradle ให้แทนที่ส่วนของ XML ด้วยบรรทัด `implementation` ที่สอดคล้องกัน.

---

## ขั้นตอนที่ 1: สร้าง Excel workbook ใน Java

การดำเนินการแรกคือการเขียนโค้ด **create excel workbook java** ที่เปิดเวิร์กบุ๊กใหม่และดึงเวิร์กชีตแรกพร้อมเซลล์ A1.

```java
import com.aspose.cells.*;

public class WrapColsDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Initialize a new workbook
        Workbook workbook = new Workbook();

        // Get the first worksheet (index 0)
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Access cell A1 where the formula will be placed
        Cell targetCell = worksheet.getCells().get("A1");
```

การสร้างเวิร์กบุ๊กด้วยวิธีนี้จะให้สภาพแวดล้อมที่สะอาด ปรับให้ตัวอย่างทำงานได้บนเครื่องใดก็ได้โดยไม่ต้องมีไฟล์ที่มีอยู่ก่อน.

---

## ขั้นตอนที่ 2: ใช้ฟังก์ชัน WRAPCOLS – ตัวอย่าง excel wrapcols

`WRAPCOLS` รับอาร์เรย์มิติเดียวและจำนวนคอลัมน์ จากนั้นคืนช่วงที่เติมแถวก่อน นี่คือหัวใจของ **reshape array in excel**.

```java
        // Step 2: Set the WRAPCOLS formula
        // {1,2,3,4,5,6} is the source 1‑D array
        // 2 tells WRAPCOLS to create 2 columns per row
        targetCell.setFormula("=WRAPCOLS({1,2,3,4,5,6}, 2)");
```

ทำไมวิธีนี้ถึงทำงานได้:

* อาร์เรย์ลิเทรัล `{1,2,3,4,5,6}` ให้จำนวนหกตัว.  
* `WRAPCOLS(..., 2)` บอก Excel ให้จัดค่าลงใน 2 คอลัมน์โดยอัตโนมัติสร้างแถวที่เพียงพอ (ในกรณีนี้คือ 3 แถว) เพื่อรองรับรายการทั้งหมด.  
* ช่วงผลลัพธ์จะครอบคลุมเซลล์ **A1:B3**:

| A | B |
|---|---|
| 1 | 2 |
| 3 | 4 |
| 5 | 6 |

---

## ขั้นตอนที่ 3: บังคับการคำนวณเพื่อให้เวิร์กบุ๊กสะท้อนสูตร

Aspose.Cells ไม่ได้ประเมินสูตรโดยอัตโนมัติเมื่อคุณตั้งค่า คุณต้องเรียก `calculateFormula()` เพื่อทำให้ผลลัพธ์ปรากฏ.

```java
        // Step 3: Recalculate all formulas in the workbook
        workbook.calculateFormula();
```

การเรียกเมธอดนี้ทำให้แน่ใจว่าอาร์เรย์ที่สร้างโดย `WRAPCOLS` ถูกเขียนลงในเซลล์ ทำให้คุณสามารถอ่านค่าได้ทันที.

---

## ขั้นตอนที่ 4: ดึงค่าจากอาร์เรย์ที่ปรับรูปแบบแล้ว

เพื่อพิสูจน์ว่าสูตรทำงานได้ ให้อ่านการแสดงผลเป็นสตริงของเซลล์เป้าหมาย เนื่องจาก `WRAPCOLS` คืนค่าเป็นอาร์เรย์ Excel จะแสดง **first element** (ค่า `1`) ในเซลล์ที่สูตรตั้งอยู่.

```java
        // Step 4: Print the first element of the array (cell A1)
        System.out.println("First element: " + targetCell.getStringValue());
```

**ผลลัพธ์คอนโซลที่คาดหวัง**

```
First element: 1
```

หากคุณตรวจสอบเวิร์กชีตใน Excel คุณจะเห็นบล็อก 3 × 2 เต็มที่ถูกเติมตามที่อธิบายไว้ก่อนหน้า.

---

## ขั้นตอนที่ 5: บันทึกเวิร์กบุ๊กลงไฟล์ – how to save workbook to file

การบันทึกเวิร์กบุ๊กทำให้คุณสามารถเปิดไฟล์นี้ในภายหลังด้วย Excel หรือแชร์ให้เพื่อนร่วมงาน ใช้วิธี `save` พร้อมระบุพาธเต็ม.

```java
        // Step 5: Save the workbook to disk
        String outputPath = "WrapFunctions.xlsx"; // adjust directory as needed
        workbook.save(outputPath);
        System.out.println("Workbook saved to " + outputPath);
    }
}
```

การรันโปรแกรมจะสร้างไฟล์ `WrapFunctions.xlsx` ในไดเรกทอรีทำงาน การเปิดไฟล์จะแสดงอาร์เรย์ที่ปรับรูปแบบในเซลล์ A1:B3 ยืนยันว่า **save workbook to file** สำเร็จ.

---

## ตัวอย่างเต็มที่สามารถรันได้

เมื่อรวมส่วนต่าง ๆ เข้าด้วยกัน นี่คือโปรแกรมเต็มที่คุณสามารถคัดลอก‑วางลงใน IDE แล้วรันได้:

```java
import com.aspose.cells.*;

public class WrapColsDemo {
    public static void main(String[] args) throws Exception {
        // Initialize a new workbook
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);
        Cell targetCell = worksheet.getCells().get("A1");

        // Apply WRAPCOLS to reshape a 1‑D array into a 3‑row × 2‑col range
        targetCell.setFormula("=WRAPCOLS({1,2,3,4,5,6}, 2)");

        // Force formula evaluation
        workbook.calculateFormula();

        // Output the first element of the resulting array
        System.out.println("First element: " + targetCell.getStringValue());

        // Save the workbook to a file
        String outputPath = "WrapFunctions.xlsx";
        workbook.save(outputPath);
        System.out.println("Workbook saved to " + outputPath);
    }
}
```

**การตรวจสอบผลลัพธ์**

1. คอนโซลพิมพ์ `First element: 1`.  
2. ไฟล์ `WrapFunctions.xlsx` ที่สร้างขึ้นมี:

| A | B |
|---|---|
| 1 | 2 |
| 3 | 4 |
| 5 | 6 |

หากคุณต้องการอ้างอิงอาร์เรย์ในที่อื่น คุณสามารถอ่านค่าจากเซลล์ใดก็ได้ที่ถูกเติมโดยใช้ `worksheet.getCells().get("B2").getIntValue()` ตัวอย่างเช่น.

---

## คำถามทั่วไปและกรณีขอบ

| Question | Answer |
|----------|--------|
| *WRAPCOLS สามารถจัดการอาร์เรย์ที่ไม่ใช่ตัวเลขได้หรือไม่?* | ได้ คุณสามารถส่งสตริง, วันที่ หรือค่าตรรกะภายในวงเล็บปีกกา และ Excel จะจัดเรียงตามนั้น. |
| *ถ้าฉันต้องการแถวมากกว่าที่ Excel สามารถแสดงได้จะทำอย่างไร?* | WRAPCOLS จะต่อเนื่องเติมแถวเพิ่มเติมจนกว่าอาร์เรย์ต้นทางจะหมด ตรวจสอบให้แน่ใจว่าเวิร์กชีตมีแถวเพียงพอ (ขีดจำกัดเริ่มต้นคือ 1,048,576). |
| *ฉันจะเปลี่ยนจำนวนคอลัมน์ได้อย่างไร?* | แก้ไขอาร์กิวเมนต์ที่สองของ `WRAPCOLS` สำหรับสามคอลัมน์ ใช้ `=WRAPCOLS({1,2,3,4,5,6}, 3)` ซึ่งจะสร้างบล็อก 2 × 3. |
| *สามารถเขียนผลลัพธ์ไปยังเซลล์เริ่มต้นอื่นได้หรือไม่?* | ได้ ตั้งสูตรในเซลล์ใดก็ได้ (เช่น `C5`) แล้วช่วงที่ห่อหุ้มจะขยายตามเซลล์นั้น. |
| *ฉันต้องเรียก `calculateFormula` ทุกครั้งที่เปลี่ยนสูตรหรือไม่?* | ทุกครั้งที่คุณแก้ไขสูตรโดยโปรแกรม ให้เรียก `calculateFormula` หรือ `calculateFormula(true)` เพื่อรีเฟรชเซลล์ที่ขึ้นอยู่. |

---

## สรุป

บทแนะนำนี้ได้สาธิต **how to use wrapcols** ใน Java เพื่อ **reshape array in excel**, ให้ตัวอย่าง **excel wrapcols example** ที่ชัดเจน และแสดงวิธีที่ถูกต้องในการ **save workbook to file** ตอนนี้คุณมีพื้นฐานที่มั่นคงสำหรับโครงการ **create excel workbook java** ที่ต้องการการแปลงอาร์เรย์แบบไดนามิก.

ต่อไปลองสำรวจหัวข้อที่เกี่ยวข้องเช่น **using other array functions** (`TRANSPOSE`, `SEQUENCE`) หรือ **writing large data sets** ด้วย Aspose.Cells streaming API ทดลองใช้แหล่งอาร์เรย์ต่าง ๆ จำนวนคอลัมน์และตำแหน่งเริ่มต้นที่แตกต่างเพื่อปรับรูปแบบให้เข้ากับการรายงานหรือกระบวนการประมวลผลข้อมูลของคุณเอง ขอให้เขียนโค้ดอย่างสนุก!

## สิ่งที่คุณควรเรียนต่อไป?

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดซึ่งต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งข้อมูลมีตัวอย่างโค้ดทำงานครบถ้วนพร้อมคำอธิบายทีละขั้นตอนเพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจวิธีการทำงานแบบอื่นในโครงการของคุณ.

- [วิธีเปิดไฟล์ Excel ด้วย Aspose.Cells สำหรับ Java: คู่มือฉบับสมบูรณ์](/cells/english/java/getting-started/open-excel-aspose-cells-java-guide/)
- [วิธีสร้างและรวม Excel Workbooks ด้วย Aspose.Cells สำหรับ Java | คู่มือฉบับสมบูรณ์](/cells/english/java/workbook-operations/create-merge-excel-workbooks-aspose-cells-java/)
- [วิธีแสดงผล Excel Sheets เป็นภาพด้วย Aspose.Cells สำหรับ Java (Workbook Operations)](/cells/english/java/workbook-operations/render-excel-sheets-images-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}