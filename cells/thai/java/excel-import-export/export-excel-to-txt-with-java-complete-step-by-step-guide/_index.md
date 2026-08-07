---
category: general
date: 2026-07-16
description: ส่งออก Excel เป็น TXT ด้วย Aspose.Cells ใน Java. เรียนรู้วิธีตั้งค่าตัวเลขที่สำคัญ,
  บันทึก Excel เป็นไฟล์ข้อความ, และควบคุมรูปแบบผลลัพธ์.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to txt
- how to set significant digits
- save excel as text file
- save workbook as txt
language: th
lastmod: 2026-07-16
og_description: ส่งออก Excel เป็น TXT ใน Java ด้วย Aspose.Cells บทแนะนำนี้จะแสดงวิธีตั้งค่าตัวเลขสำคัญ,
  บันทึก Excel เป็นไฟล์ข้อความ, และรับผลลัพธ์ที่เชื่อถือได้.
og_image_alt: Screenshot of Java code exporting an Excel workbook to a TXT file with
  4 significant digits
og_title: ส่งออก Excel เป็น TXT ใน Java – คู่มือขั้นตอนต่อขั้นตอน
schemas:
- author: Aspose
  dateModified: '2026-07-16'
  description: Export Excel to TXT using Aspose.Cells in Java. Learn how to set significant
    digits, save Excel as text file, and control the output format.
  headline: Export Excel to TXT with Java – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Export Excel to TXT using Aspose.Cells in Java. Learn how to set significant
    digits, save Excel as text file, and control the output format.
  name: Export Excel to TXT with Java – Complete Step‑by‑Step Guide
  steps:
  - name: Prerequisites
    text: '- Java Development Kit (JDK) 8 or newer. - Maven or Gradle to manage the
      Aspose.Cells dependency (we’ll show the Maven snippet). - A basic understanding
      of Java syntax (if you’ve written a “Hello World”, you’re good).'
  - name: Understanding `setSignificantDigits`
    text: '- **Definition:** The number of digits that remain after the decimal point,
      *including* leading digits. For `123.456789` with `4` significant digits, the
      output becomes `123.5`. - **When to use:** If the downstream system expects
      a fixed precision (e.g., scientific data files), or you need to trunca'
  - name: Folder Considerations
    text: '- The `output` folder must exist, or you’ll get an `IOException`. You can
      create it programmatically:'
  - name: 1️⃣ What if I need a different delimiter?
    text: "`TxtSaveOptions` also offers `setSeparator('\t')` for tabs or `setSeparator(',')`
      for CSV‑style output. Example:"
  - name: 2️⃣ How does locale affect decimal separators?
    text: 'By default Aspose uses the system locale. If you need a period (`.`) regardless
      of locale, set:'
  - name: 3️⃣ Large worksheets – memory concerns?
    text: Aspose.Cells streams data to disk when working with worksheets larger than
      1 GB, so you usually won’t hit an `OutOfMemoryError`. Still, avoid loading massive
      sheets into memory if you only need a subset; use `Workbook.getWorksheets().get(index)`
      to target a specific sheet.
  - name: 4️⃣ Can I export only a range?
    text: Yes. Use `txtOptions.setExportRange("A1:B10")` to restrict the output to
      a specific area. This reduces file size and speeds up the export.
  - name: 5️⃣ What if I don’t have a license?
    text: The evaluation mode adds a watermark line (`"Aspose.Cells for Java Evaluation
      Version"`). For production you’ll need a license; otherwise the watermark may
      break downstream parsers.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: ส่งออก Excel เป็น TXT ด้วย Java – คู่มือขั้นตอนเต็มรูปแบบ
url: /th/java/excel-import-export/export-excel-to-txt-with-java-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ส่งออก Excel เป็น TXT ด้วย Java – คู่มือขั้นตอนเต็ม

เคยสงสัย **วิธีส่งออก Excel เป็น TXT** โดยไม่สูญเสียความแม่นยำของตัวเลขหรือไม่? บางครั้งคุณอาจต้องการไฟล์ข้อความธรรมดาสำหรับระบบเก่า หรือกำลังป้อนข้อมูลเข้าสู่สายงานวิทยาศาสตร์ที่ต้องการจำนวนหลักสำคัญที่แน่นอน ในบทเรียนนี้เราจะพาคุณผ่าน **ตัวอย่าง Java ที่ทำงานได้เต็มรูปแบบ** ที่แสดงให้เห็นขั้นตอนทั้งหมด — รวมถึง **การตั้งค่าหลักสำคัญ**, **การบันทึก Excel เป็นไฟล์ข้อความ**, และ **การบันทึกเวิร์กบุ๊กเป็น txt** ด้วย Aspose.Cells

เราจะครอบคลุมทุกอย่างตั้งแต่การตั้งค่าโปรเจกต์จนถึงขั้นตอนตรวจสอบสุดท้าย เพื่อให้คุณคัดลอก‑วางโค้ด, รันมัน, และเห็นผลลัพธ์ทันที ไม่มีการพึ่งพาเอกสารภายนอกหรือ “ดูที่ docs” เพียงแค่โซลูชันครบวงจรที่ชัดเจน

---

## สิ่งที่คุณจะได้เรียนรู้

- วิธีสร้างเวิร์กบุ๊กโดยโปรแกรมด้วย Aspose.Cells
- คำเรียก API ที่ใช้ **ตั้งค่าหลักสำคัญ** สำหรับการส่งออกเป็น TXT
- ความแตกต่างระหว่าง `TxtSaveOptions` กับตัวเลือกการบันทึกอื่น ๆ
- วิธี **บันทึก Excel เป็นไฟล์ข้อความ** บนทุกระบบปฏิบัติการ (Windows, macOS, Linux)
- ปัญหาที่พบบ่อย (ตัวคั่นทศนิยมตามโลคัล, เวิร์กชีตขนาดใหญ่) และวิธีหลีกเลี่ยง
- คลาส Java เต็มรูปแบบพร้อมรันที่คุณสามารถปรับใช้ในโปรเจกต์ของคุณได้ทันที

### ข้อกำหนดเบื้องต้น

- Java Development Kit (JDK) 8 หรือใหม่กว่า
- Maven หรือ Gradle เพื่อจัดการ dependency ของ Aspose.Cells (เราจะให้ตัวอย่าง Maven)
- ความเข้าใจพื้นฐานของไวยากรณ์ Java (ถ้าคุณเคยเขียน “Hello World” ก็พอ)

---

## ขั้นตอนที่ 1: ตั้งค่าโปรเจกต์และเพิ่ม Aspose.Cells

ก่อนอื่นให้เพิ่มไลบรารีเข้าไปในบิลด์ของคุณ หากคุณใช้ Maven ให้เพิ่มส่วนนี้ลงใน `pom.xml` ของคุณ:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest stable version -->
</dependency>
```

> **เคล็ดลับ:** Aspose มีไลเซนส์ทดลองฟรี 30 วัน ให้วางไฟล์ `Aspose.Total.lic` ไว้ที่รูทของโปรเจกต์ หรือเรียก `License.setLicense("path/to/license")` ก่อนใช้ API ใด ๆ

เมื่อ dependency ถูกดึงมาแล้ว คุณก็พร้อมเริ่มเขียนโค้ด หากคุณชอบ Gradle ตัวเลือกเทียบเคียงคือ:

```gradle
implementation 'com.aspose:aspose-cells:24.9'
```

---

## ขั้นตอนที่ 2: ส่งออก Excel เป็น TXT – สร้างเวิร์กบุ๊ก

ต่อไปเราจะสร้างเวิร์กบุ๊กใหม่, ใส่ค่าตัวเลข, และเตรียมพร้อมสำหรับการส่งออก นี่คือหัวใจของ **export excel to txt**.

```java
import com.aspose.cells.*;

public class ExportExcelToTxtDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create a fresh workbook (in‑memory Excel file)
        Workbook workbook = new Workbook();

        // 2️⃣ Grab the first worksheet – it's created by default
        Worksheet sheet = workbook.getWorksheets().get(0);

        // 3️⃣ Put a numeric value into cell A1
        Cell cell = sheet.getCells().get("A1");
        cell.putValue(123.456789); // Example number with many decimals
```

**ทำไมจึงสำคัญ:** การสร้างเวิร์กบุ๊กด้วยโค้ดช่วยหลีกเลี่ยงการฟอร์แมตที่ซ่อนอยู่จากไฟล์เทมเพลต `putValue` จะตรวจจับชนิดข้อมูลโดยอัตโนมัติ ทำให้เซลล์เป็น **numeric** ไม่ใช่ string

---

## ขั้นตอนที่ 3: วิธีตั้งค่าหลักสำคัญสำหรับการส่งออกเป็น TXT

เมื่อส่งออกเป็นข้อความธรรมดา Aspose.Cells จะเขียนค่าตัวเลขดิบโดยค่าเริ่มต้น เพื่อจำกัดผลลัพธ์ให้เหลือ **4 หลักสำคัญ** คุณต้องปรับ `TxtSaveOptions`.

```java
        // 4️⃣ Configure TXT save options – this is where we set the precision
        TxtSaveOptions txtOptions = new TxtSaveOptions();
        txtOptions.setSignificantDigits(4); // <-- controls significant digits
```

### ทำความเข้าใจ `setSignificantDigits`

- **คำนิยาม:** จำนวนหลักที่คงเหลือหลังจุดทศนิยม *รวม* หลักนำหน้า ตัวอย่าง `123.456789` กับ `4` หลักสำคัญ จะได้ผลลัพธ์เป็น `123.5`
- **เมื่อใดใช้:** หากระบบปลายทางต้องการความแม่นยำคงที่ (เช่นไฟล์ข้อมูลวิทยาศาสตร์) หรือคุณต้องการตัดทอนเพื่อหลีกเลี่ยง noise ของ floating‑point
- **กรณีขอบ:** หากตัวเลขมีหลักน้อยกว่าที่กำหนด Aspose จะคงค่าต้นฉบับไว้ (ไม่มีการเติมศูนย์)

> **ทำไมไม่ใช้ `setDecimalPlaces`?** คุณสมบัตินี้ควบคุม *เฉพาะ* หลักหลังจุดทศนิยม ไม่รวมหลักนำหน้า สำหรับข้อมูลวิทยาศาสตร์ `significantDigits` มักเป็นตัวเลือกที่เหมาะกว่า

---

## ขั้นตอนที่ 4: บันทึก Excel เป็นไฟล์ข้อความ (TXT)

เมื่อกำหนดตัวเลือกเรียบร้อยแล้ว เราจะเขียนเวิร์กบุ๊กลงไฟล์ `.txt` นี่คือขั้นตอน **save workbook as txt**.

```java
        // 5️⃣ Persist the workbook as a TXT file
        String outputPath = "output/SignificantDigits.txt";
        workbook.save(outputPath, txtOptions);

        System.out.println("Excel exported to TXT at: " + outputPath);
    }
}
```

### พิจารณาโฟลเดอร์

- โฟลเดอร์ `output` ต้องมีอยู่ก่อน มิฉะนั้นจะเกิด `IOException` คุณสามารถสร้างโฟลเดอร์โดยโปรแกรมได้:

```java
new java.io.File("output").mkdirs();
```

- บน Linux/macOS เส้นทางเป็น case‑sensitive; บน Windows ไม่เป็นเช่นนั้น ควรใช้ชื่อโฟลเดอร์เป็นตัวพิมพ์เล็กทั้งหมดเพื่อความปลอดภัยข้ามแพลตฟอร์ม

---

## ขั้นตอนที่ 5: ตรวจสอบผลลัพธ์

รันโปรแกรม (`mvn compile exec:java -Dexec.mainClass=ExportExcelToTxtDemo`) แล้วเปิด `output/SignificantDigits.txt` คุณควรเห็น:

```
123.5
```

บรรทัดเดียวนี้ยืนยันว่า:

- เวิร์กบุ๊กถูก **บันทึกเป็นไฟล์ข้อความ** อย่างสำเร็จ
- ค่าตัวเลขปฏิบัติตาม **4 หลักสำคัญ** ที่เราตั้งไว้
- ไม่มีคอมม่า, แท็บ หรือเมตาดาต้าเฉพาะของ Excel แทรกเข้ามาในไฟล์

หากต้องการรูปแบบที่คั่นด้วยแท็บสำหรับหลายคอลัมน์ เพียงเติมเซลล์เพิ่มและ Aspose จะใส่แท็บให้โดยอัตโนมัติ

---

## คำถามทั่วไป & กรณีขอบ

### 1️⃣ ต้องการตัวคั่นอื่น?

`TxtSaveOptions` มี `setSeparator('\t')` สำหรับแท็บ หรือ `setSeparator(',')` สำหรับ CSV ตัวอย่าง:

```java
txtOptions.setSeparator('\t'); // Tab delimiter
```

### 2️⃣ โลคัลมีผลต่อเครื่องหมายทศนิยมอย่างไร?

โดยค่าเริ่มต้น Aspose ใช้โลคัลของระบบ หากต้องการจุด (`.`) เสมอไม่ว่าภาษาใด ให้ตั้งค่า:

```java
txtOptions.setCultureInfo(java.util.Locale.US);
```

### 3️⃣ เวิร์กชีตขนาดใหญ่ – ปัญหาเมมโมรี?

Aspose.Cells จะสตรีมข้อมูลลงดิสก์เมื่อทำงานกับเวิร์กชีตใหญ่กว่า 1 GB ดังนั้นคุณมักจะไม่เจอ `OutOfMemoryError` อย่างไรก็ตาม ควรหลีกเลี่ยงการโหลดชีตขนาดมหาศาลทั้งหมด หากต้องการเฉพาะบางส่วน ให้ใช้ `Workbook.getWorksheets().get(index)` เพื่อเลือกชีตที่ต้องการ

### 4️⃣ สามารถส่งออกเฉพาะช่วงได้หรือไม่?

ทำได้ ใช้ `txtOptions.setExportRange("A1:B10")` เพื่อจำกัดผลลัพธ์ให้เฉพาะพื้นที่ที่กำหนด ช่วยลดขนาดไฟล์และเร่งความเร็วการส่งออก

### 5️⃣ หากไม่มีไลเซนส์จะเป็นอย่างไร?

โหมดประเมินผลจะเพิ่มบรรทัดลายน้ำ (`"Aspose.Cells for Java Evaluation Version"`) หากใช้ในผลิตภัณฑ์จริงต้องซื้อไลเซนส์; มิฉะนั้นลายน้ำอาจทำให้ตัวแยกข้อมูลล้มเหลว

---

## ตัวอย่างทำงานเต็มรูปแบบ (พร้อมคัดลอก‑วาง)

```java
import com.aspose.cells.*;

import java.io.File;

public class ExportExcelToTxtDemo {
    public static void main(String[] args) throws Exception {
        // Ensure output directory exists
        new File("output").mkdirs();

        // 1️⃣ Create workbook and get first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.getWorksheets().get(0);

        // 2️⃣ Put several numbers to illustrate formatting
        sheet.getCells().get("A1").putValue(123.456789);
        sheet.getCells().get("A2").putValue(0.0012345);
        sheet.getCells().get("A3").putValue(98765.4321);

        // 3️⃣ Configure TXT options – 4 significant digits, tab delimiter
        TxtSaveOptions txtOptions = new TxtSaveOptions();
        txtOptions.setSignificantDigits(4);
        txtOptions.setSeparator('\t'); // optional, defaults to tab
        txtOptions.setCultureInfo(java.util.Locale.US); // enforce dot as decimal separator

        // 4️⃣ Save as TXT
        String outPath = "output/SignificantDigits.txt";
        workbook.save(outPath, txtOptions);

        System.out.println("Export completed: " + outPath);
    }
}
```

รันโค้ดด้านบนจะได้ไฟล์ `output/SignificantDigits.txt` ที่มี:

```
123.5
0.001235
98770
```

สังเกตว่าตัวเลขทุกตัวปฏิบัติตามกฎ **4 หลักสำคัญ** แม้ค่าที่เล็กหรือใหญ่มาก

---

## สรุป

เราได้แสดง **วิธีส่งออก Excel เป็น TXT** อย่างครบวงจรด้วย Java และ Aspose.Cells ครอบคลุม **การตั้งค่าหลักสำคัญ**, **การบันทึก Excel เป็นไฟล์ข้อความ**, และ **การบันทึกเวิร์กบุ๊กเป็น txt** จุดสำคัญที่ควรจำ:

- ใช้ `TxtSaveOptions.setSignificantDigits` เพื่อควบคุมความแม่นยำของตัวเลข
- ปรับตัวคั่น, ภูมิภาค, และช่วงการส่งออกตามความต้องการ
- โค้ดทำงานบนทุกแพลตฟอร์ม, ต้องการไลบรารีเดียว, และสร้างไฟล์ข้อความที่สะอาดพร้อมใช้ต่อได้ทันที

พร้อมก้าวต่อหรือยัง? ลองเพิ่มหลายคอลัมน์, ทดลองตัวคั่นต่าง ๆ, หรือผสานการส่งออกนี้เข้าไปใน pipeline ETL ขนาดใหญ่ หากเจอปัญหา เช่น ปัญหาโลคัลหรือชีตขนาดใหญ่ ให้กลับไปอ่านส่วน “คำถามทั่วไป & กรณีขอบ” อีกครั้ง

มีกรณีการใช้งานที่อยากแบ่งปันไหม? แสดงความคิดเห็น, หรือ fork repository แล้วเปิด pull request. Happy coding, และสนุกกับการแปลงสเปรดชีตเป็นข้อความธรรมดา!

## คุณควรเรียนรู้อะไรต่อไป?

บทเรียนต่อไปนี้เกี่ยวข้องอย่างใกล้ชิดและต่อยอดเทคนิคที่แสดงในคู่มือนี้ ทุกแหล่งรวมโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายขั้นตอนเพื่อให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจวิธีการทำงานแบบอื่นในโปรเจกต์ของคุณ

- [How to Save Excel Files in Various Formats Using Aspose.Cells Java](/cells/english/java/workbook-operations/save-excel-files-aspose-cells-java/)
- [How to Load and Save Excel as CSV Using Aspose.Cells for Java&#58; A Comprehensive Guide](/cells/english/java/workbook-operations/aspose-cells-java-load-save-excel-csv/)
- [How to Create and Export Excel to HTML Using Aspose.Cells Java | Workbook Operations Guide](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}