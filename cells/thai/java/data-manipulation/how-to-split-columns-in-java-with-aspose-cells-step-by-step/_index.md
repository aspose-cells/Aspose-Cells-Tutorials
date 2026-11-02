---
category: general
date: 2026-10-07
description: วิธีแยกคอลัมน์โดยใช้ Aspose.Cells สำหรับ Java เรียนรู้การแยกสตริงเป็นคอลัมน์,
  ทำให้สูตร Excel ทำงานอัตโนมัติ, และเขียนสูตรลงในเซลล์ด้วยโค้ดเพียงไม่กี่บรรทัด
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to split columns
- split string into columns
- automate excel formula
- write formula to cell
language: th
lastmod: 2026-10-07
og_description: วิธีแยกคอลัมน์ใน Java ด้วย Aspose.Cells บทเรียนนี้จะแสดงวิธีแยกสตริงเป็นคอลัมน์,
  ทำให้การประเมินสูตร Excel เป็นอัตโนมัติ, และเขียนสูตรลงในเซลล์
og_image_alt: Screenshot of Java code that splits columns in an Excel worksheet using
  Aspose.Cells
og_title: วิธีแยกคอลัมน์ใน Java ด้วย Aspose.Cells – บทเรียนสั้น
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: How to split columns using Aspose.Cells for Java. Learn to split string
    into columns, automate Excel formula, and write formula to cell in a few lines
    of code.
  headline: How to split columns in Java with Aspose.Cells – step‑by‑step guide
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel automation
title: วิธีแยกคอลัมน์ใน Java ด้วย Aspose.Cells – คู่มือแบบขั้นตอนต่อขั้นตอน
url: /th/java/data-manipulation/how-to-split-columns-in-java-with-aspose-cells-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีแยกคอลัมน์ใน Java ด้วย Aspose.Cells – คู่มือขั้นตอนโดยละเอียด

หากคุณต้องการ **วิธีแยกคอลัมน์** ในแผ่นงาน Excel อย่างโปรแกรมมิ่ง คู่มือนี้จะแสดงกระบวนการทั้งหมดด้วย Aspose.Cells สำหรับ Java คุณจะได้เรียนรู้วิธี **แยกสตริงเป็นคอลัมน์**, **อัตโนมัติการประเมินสูตร Excel**, และ **เขียนสูตรลงในเซลล์** ด้วยโค้ดที่กระชับและพร้อมใช้งานในผลิตภัณฑ์

การแยกคอลัมน์แบบโปรแกรมมิ่งช่วยขจัดการคัดลอก‑วางด้วยมือ ลดข้อผิดพลาด และทำให้สามารถแปลงข้อมูลในระดับใหญ่ได้ อย่างครบถ้วนในบทเรียนนี้ คุณจะสามารถสร้าง แก้ไข และประเมินสูตรได้ทันที ทำให้ Excel กลายเป็นส่วนสำคัญของแบ็กเอนด์ Java ของคุณ

## ข้อกำหนดเบื้องต้น

ก่อนเริ่มทำงาน ตรวจสอบให้แน่ใจว่าคุณมี:

* ติดตั้ง Java 17 หรือรุ่นที่ใหม่กว่า
* Maven 3.8+ (หรือ Gradle) สำหรับการจัดการ dependencies
* ใบอนุญาต Aspose.Cells for Java (เวอร์ชันทดลองฟรีใช้สำหรับการเรียนรู้ได้)
* ความคุ้นเคยพื้นฐานกับไวยากรณ์ Java และแนวคิดของ Excel

หากขาดรายการใดรายการหนึ่ง ให้ติดตั้งก่อน; ตัวอย่างโค้ดสมมติว่าเป็นโครงการ Maven มาตรฐาน

## ขั้นตอนที่ 1: เพิ่ม Aspose.Cells ไปยังโปรเจกต์ของคุณ

เพิ่ม dependency ต่อไปนี้ในไฟล์ `pom.xml` ของคุณ ซึ่งจะดึงไลบรารี Aspose.Cells รุ่นเสถียรล่าสุด

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest version available -->
</dependency>
```

**ทำไมขั้นตอนนี้สำคัญ:** ไลบรารีนี้ให้คลาส `Workbook`, `Worksheet`, และ `Cell` ที่จำเป็นสำหรับการจัดการไฟล์ Excel โดยไม่ต้องใช้ Microsoft Office หากไม่มี dependency โค้ดจะไม่คอมไพล์

## ขั้นตอนที่ 2: สร้าง workbook และเลือก worksheet แรก

```java
import com.aspose.cells.*;

public class SplitColumnsExample {
    public static void main(String[] args) throws Exception {
        // Step 2: Initialize a new workbook and access the first worksheet
        Workbook workbook = new Workbook();                     // creates an empty .xlsx file in memory
        Worksheet worksheet = workbook.getWorksheets().get(0); // first sheet is index 0
```

อ็อบเจ็กต์ `Workbook` แทนไฟล์ Excel ทั้งหมด การเข้าถึง worksheet แรกทำให้มีจุดเริ่มต้นที่คาดเดาได้สำหรับสูตรที่เราจะเขียน

## ขั้นตอนที่ 3: เขียนสูตร WRAPCOLS ไปยังเซลล์เป้าหมาย

```java
        // Step 3: Identify the target cell (A1) where the formula will be placed
        Cell targetCell = worksheet.getCells().get("A1");

        // Step 3: Write the WRAPCOLS formula to split a long string into three columns
        // WRAPCOLS(string, columns) distributes the string across the specified number of columns.
        targetCell.setFormula("=WRAPCOLS(\"This is a very long string that needs to be split\",3)");
```

**ทำไมเราถึงใช้ `WRAPCOLS`:** ฟังก์ชันในตัวของ Excel `WRAPCOLS` จะทำการแบ่งค่าข้อความเดียวเป็นจำนวนคอลัมน์ที่กำหนดโดยอัตโนมัติ พร้อมจัดการขอบเขตของคำอย่างชาญฉลาด นี่เป็นวิธีที่เชื่อถือได้ที่สุดในการ **แยกสตริงเป็นคอลัมน์** โดยไม่ต้องเขียนตรรกะการแยกเอง

## ขั้นตอนที่ 4: บังคับให้ workbook ประเมินสูตร

```java
        // Step 4: Calculate all formulas in the workbook so the result becomes visible
        workbook.calculateFormula();
```

การเรียก `calculateFormula()` **ทำให้การประเมินสูตร Excel** เป็นอัตโนมัติบนเซิร์ฟเวอร์ หากไม่เรียกเมธอดนี้ เซลล์จะยังคงมีข้อความสูตรอยู่ ไม่ใช่ค่าที่คำนวณแล้ว

## ขั้นตอนที่ 5: ดึงและแสดงผลลัพธ์ที่ถูกแยก

```java
        // Step 5: Retrieve the computed value from the target cell
        String result = targetCell.getStringValue(); // returns the first column of the split result
        System.out.println("First column output: " + result);

        // Optionally, read the other columns created by WRAPCOLS
        String second = worksheet.getCells().get("B1").getStringValue();
        String third  = worksheet.getCells().get("C1").getStringValue();

        System.out.println("Second column output: " + second);
        System.out.println("Third column output: " + third);

        // Save the workbook to verify the split visually (optional)
        workbook.save("SplitColumnsResult.xlsx");
    }
}
```

เมื่อคุณรันโปรแกรม คอนโซลจะแสดงผล:

```
First column output: This is a very long
Second column output: string that needs
Third column output: to be split
```

ไฟล์ `SplitColumnsResult.xlsx` ที่สร้างขึ้นจะแสดงคอลัมน์สามคอลัมน์ที่เต็มด้วยข้อความที่ถูกแยก

## ทำความเข้าใจฟังก์ชัน WRAPCOLS

* **Syntax:** `WRAPCOLS(text, columns, [delimiter])`
* **Parameters:**
  * `text` – สตริงที่คุณต้องการแยก
  * `columns` – จำนวนคอลัมน์ที่จะแบ่งข้อความ
  * `delimiter` (optional) – ตัวอักษรที่ใช้แบ่งสตริง; ค่าเริ่มต้นคือช่องว่าง
* **Return value:** อาเรย์ที่กระจายลงในเซลล์ที่อยู่ติดกัน แต่ละองค์ประกอบมีส่วนของข้อความต้นฉบับ

เนื่องจากฟังก์ชันนี้กระจายแนวนอน คุณเพียงเขียนสูตรลงในเซลล์ซ้ายสุด (A1 ในตัวอย่าง) Excel จะเติมค่าใน B1, C1, … ตามที่จำเป็นโดยอัตโนมัติ

## ความแปรผันทั่วไปและกรณีขอบ

| สถานการณ์ | การปรับแนะนำ |
|-----------|------------------------|
| **จำนวนคอลัมน์แบบแปรผัน** | แทนที่ค่า `3` ที่กำหนดตายตัวด้วยตัวแปร: `targetCell.setFormula(String.format("=WRAPCOLS(\"%s\",%d)", longString, columnCount));` |
| **ตัวคั่นแบบกำหนดเอง** | ใช้พารามิเตอร์ที่สาม เช่น `=WRAPCOLS(A2,4,",")` เพื่อแยกตามเครื่องหมายคอมม่า. |
| **สตริงต้นทางว่าง** | ฟังก์ชันจะคืนค่าเซลล์ว่าง; ตรวจสอบให้แน่ใจว่าไม่ได้เป็น `null` หรือสตริงว่างก่อนตั้งสูตร. |
| **ชุดข้อมูลขนาดใหญ่** | ใช้สูตรในลูปสำหรับแต่ละแถว แล้วเรียก `calculateFormula()` หนึ่งครั้งหลังลูปเพื่อเพิ่มประสิทธิภาพ. |
| **อักขระที่ไม่ใช่ ASCII** | WRAPCOLS ทำงานกับ Unicode; ตรวจสอบให้ไฟล์ซอร์ส Java ของคุณบันทึกเป็น UTF‑8. |

**เคล็ดลับ:** เมื่อประมวลผลหลายแถว ให้เก็บสูตรในตัวแปรสตริงและนำกลับมาใช้ซ้ำเพื่อหลีกเลี่ยงค่าใช้จ่ายจากการต่อสตริงซ้ำหลายครั้ง

## ตัวอย่างเต็มที่สามารถรันได้

ด้านล่างเป็นโปรแกรมเต็มพร้อมคัดลอก‑วาง ซึ่งรวมถึงคำสั่ง import, การจัดการข้อยกเว้น, และการบันทึกแบบเลือกได้

```java
import com.aspose.cells.*;

public class SplitColumnsExample {
    public static void main(String[] args) throws Exception {
        // Create a new workbook and access the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Define the long string and desired column count
        String longString = "This is a very long string that needs to be split";
        int columnCount = 3;

        // Write the WRAPCOLS formula to cell A1
        Cell targetCell = worksheet.getCells().get("A1");
        String formula = String.format("=WRAPCOLS(\"%s\",%d)", longString, columnCount);
        targetCell.setFormula(formula);

        // Evaluate all formulas in the workbook
        workbook.calculateFormula();

        // Read and display each column's result
        System.out.println("First column output: " + worksheet.getCells().get("A1").getStringValue());
        System.out.println("Second column output: " + worksheet.getCells().get("B1").getStringValue());
        System.out.println("Third column output: " + worksheet.getCells().get("C1").getStringValue());

        // Save the workbook for visual verification
        workbook.save("SplitColumnsResult.xlsx");
    }
}
```

การรันโปรแกรมนี้จะให้ผลลัพธ์คอนโซลเดียวกับที่แสดงก่อนหน้าและบันทึกไฟล์ Excel ที่แสดงอย่างชัดเจนว่า **วิธีแยกคอลัมน์**

## รายการตรวจสอบการแก้ไขปัญหา

* **สูตรไม่ประเมินผล** – ตรวจสอบว่าได้เรียก `workbook.calculateFormula()` หลังจากตั้งสูตรแล้ว
* **เซลล์ว่างหลังการแยก** – ยืนยันว่าสตริงต้นทางไม่เป็น `null` หรือว่างเปล่า และจำนวนคอลัมน์มากกว่าศูนย์
* **ข้อยกเว้นใบอนุญาต** – ให้ไฟล์ใบอนุญาต Aspose.Cells ที่ถูกต้อง (`License license = new License(); license.setLicense("Aspose.Total.lic");`) ก่อนสร้าง workbook เพื่อกำจัดลายน้ำการประเมิน
* **ความล่าช้าประสิทธิภาพบนชีตขนาดใหญ่** – เรียก `calculateFormula()` หนึ่งครั้งหลังจากเขียนสูตรทั้งหมดแล้ว ไม่ใช่หลังจากแต่ละเซลล์

## สรุป

ตอนนี้คุณรู้แล้วว่า **วิธีแยกคอลัมน์** ใน Java ด้วย Aspose.Cells, วิธี **แยกสตริงเป็นคอลัมน์** ด้วยฟังก์ชัน `WRAPCOLS`, วิธี **อัตโนมัติการประเมินสูตร Excel**, และวิธี **เขียนสูตรลงในเซลล์** อย่างโปรแกรมมิ่ง เทคนิคนี้ขจัดขั้นตอนการเตรียมข้อมูลด้วยมือและรวมความสามารถการจัดการข้อความของ Excel เข้าไปโดยตรงในแอปพลิเคชัน Java ของคุณ

### ขั้นตอนต่อไป

* สำรวจฟังก์ชันข้อความอื่น ๆ เช่น `TEXTSPLIT` และ `FILTERXML` สำหรับสถานการณ์การแยกที่ซับซ้อนยิ่งขึ้น
* ผสาน `WRAPCOLS` กับ `IFERROR` เพื่อจัดการอินพุตที่ไม่คาดคิดอย่างราบรื่น
* ผสานโซลูชันนี้เข้ากับบริการ Spring Boot ที่รับข้อมูล CSV ผ่าน REST และส่งคืนไฟล์ Excel ที่เติมข้อมูลแล้ว

ด้วยการเชี่ยวชาญรูปแบบเหล่านี้ คุณสามารถสร้างเวิร์กโฟลว์ Excel ที่แข็งแรงและอัตโนมัติที่ขยายตามความต้องการของธุรกิจของคุณ ขอให้เขียนโค้ดอย่างสนุกสนาน!

## สิ่งที่คุณควรเรียนต่อไป?

บทเรียนต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดซึ่งต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งข้อมูลมีตัวอย่างโค้ดทำงานครบถ้วนพร้อมคำอธิบายขั้นตอนเพื่อช่วยให้คุณเชี่ยวชาญคุณลักษณะ API เพิ่มเติมและสำรวจแนวทางการดำเนินการทางเลือกในโครงการของคุณ

- [aspose cells java – แบ่งชื่อเป็นคอลัมน์](/cells/english/java/cell-operations/aspose-cells-java-split-names-columns/)
- [Auto-Fit Excel Columns in Java Using Aspose.Cells](/cells/english/java/formatting/aspose-cells-java-auto-fit-excel-columns-guide/)
- [วิธีลบคอลัมน์ว่างใน Excel ด้วย Aspose.Cells Java: คู่มือฉบับสมบูรณ์](/cells/english/java/worksheet-management/delete-blank-columns-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}