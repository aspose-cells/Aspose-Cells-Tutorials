---
category: general
date: 2026-08-17
description: ส่งออกไฟล์ Excel เป็น TXT พร้อมจำกัดจำนวนหลักสำคัญ – เรียนรู้วิธีตั้งค่าจำนวนหลักและแปลง
  Excel เป็นข้อความใน Java ด้วยตัวอย่าง Aspose.Cells ที่ครบถ้วน
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to txt
- how to set digits
- convert excel to text
- how to limit decimals
- limit significant digits
language: th
lastmod: 2026-08-17
og_description: ส่งออก Excel ไปเป็น TXT พร้อมจำกัดจำนวนหลักสำคัญ บทแนะนำนี้แสดงวิธีตั้งค่าจำนวนหลักและแปลง
  Excel เป็นข้อความโดยใช้ Aspose.Cells สำหรับ Java.
og_image_alt: Java code exporting Excel to TXT with 4 significant digits
og_title: ส่งออก Excel เป็น TXT พร้อมจำกัดจำนวนหลักสำคัญ – คู่มือ Java
schemas:
- author: Aspose
  dateModified: '2026-08-17'
  description: Export Excel to TXT while limiting significant digits – learn how to
    set digits and convert Excel to text in Java with a complete Aspose.Cells example.
  headline: How to export Excel to TXT with limited significant digits using Java
  type: TechArticle
- description: Export Excel to TXT while limiting significant digits – learn how to
    set digits and convert Excel to text in Java with a complete Aspose.Cells example.
  name: How to export Excel to TXT with limited significant digits using Java
  steps:
  - name: Prerequisites
    text: '- Java 17 or later (the code compiles with Java 8 as well). - Aspose.Cells
      for Java 25.10 or newer. Download the JAR from the [Aspose website](https://products.aspose.com/cells/java)
      and add it to your project’s classpath. - An IDE or a simple text editor and
      command‑line build tool (Maven/Gradle).'
  - name: How the setting differs from “limit decimals”
    text: '- **limit decimals** (`setDecimalPlaces`) trims digits *after* the decimal
      point, regardless of the integer part. - **significant digits** (`setSignificantDigits`)
      counts digits from the first non‑zero digit, which is useful when numbers vary
      in magnitude.'
  - name: Expected output
    text: '| Cell | Original value | Exported (4 significant digits) | |------|----------------|---------------------------------|
      | A1 | 123.456789 | 123.5 |'
  - name: Exporting a whole range
    text: 'If you want to export more than one cell, simply fill the range before
      saving:'
  - name: Handling locale‑specific decimal separators
    text: 'Aspose.Cells respects the system locale when writing text. To force a dot
      (`.`) as the decimal separator, set the `TxtSaveOptions` culture:'
  - name: Overwriting existing files
    text: 'The `save` method overwrites the target file by default. If you need to
      avoid accidental data loss, check for file existence first:'
  - name: Large workbooks and memory usage
    text: 'When exporting very large worksheets, consider streaming the output:'
  - name: Next steps
    text: "- Explore other `TxtSaveOptions` properties such as `setDelimiter('\t')`
      to customize column separators. - Combine the exporter with `CsvSaveOptions`
      if you need comma‑separated values instead of plain text. - Integrate the routine
      into a web service that accepts uploaded Excel files and returns tri"
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel export
- TXT conversion
title: วิธีส่งออก Excel เป็น TXT ด้วยจำนวนหลักสำคัญที่จำกัดโดยใช้ Java
url: /th/java/excel-import-export/how-to-export-excel-to-txt-with-limited-significant-digits-u/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ส่งออก Excel เป็น TXT ด้วยจำนวนหลักสำคัญที่จำกัดโดยใช้ Java

หากคุณต้องการ **export Excel to TXT** พร้อมควบคุมจำนวนหลักสำคัญ คู่มือฉบับนี้ให้วิธีแก้ที่พร้อมใช้งาน คุณจะได้เรียนรู้วิธีตั้งค่าหลัก, แปลง Excel เป็นข้อความ, และทำให้ผลลัพธ์เรียบร้อยด้วยการเปลี่ยนแปลงการกำหนดค่าเพียงอย่างเดียว

ตัวอย่างใช้ Aspose.Cells for Java 25.10 ซึ่งแนะนำตัวเลือก `setSignificantDigits` เมื่อจบบทเรียนคุณจะสามารถสร้างไฟล์ TXT ที่มีเพียงหลักที่ต้องการโดยไม่ต้องเขียนโค้ดการปัดเศษเพิ่มเติม

## สิ่งที่คุณจะได้ทำ

- สร้าง workbook ด้วยโปรแกรม
- แทรกค่าตัวเลขลงในเซลล์
- กำหนดค่า TXT save options เพื่อจำกัดหลักสำคัญ
- บันทึก workbook เป็นไฟล์ข้อความธรรมดา
- ทำความเข้าใจการทำงานของการตั้งค่า `significantDigits` และวิธีปรับใช้ในสถานการณ์อื่น

### ข้อกำหนดเบื้องต้น

- Java 17 หรือใหม่กว่า (โค้ดยังคอมไพล์ได้กับ Java 8 ด้วย)
- Aspose.Cells for Java 25.10 หรือใหม่กว่า ดาวน์โหลด JAR จาก [Aspose website](https://products.aspose.com/cells/java) แล้วเพิ่มลงใน classpath ของโปรเจค
- IDE หรือเครื่องมือแก้ไขข้อความง่าย ๆ พร้อมเครื่องมือสร้างแบบบรรทัดคำสั่ง (Maven/Gradle)

## ขั้นตอนที่ 1: ตั้งค่าโปรเจคและนำเข้า Aspose.Cells

สร้างโปรเจค Java ใหม่และเพิ่ม Aspose.Cells JAR ลงในเส้นทางการสร้าง หากคุณใช้ Maven ให้เพิ่ม dependency ต่อไปนี้ใน `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.10</version>
    <classifier>jdk17</classifier>
</dependency>
```

> **เคล็ดลับ:** ใช้ classifier `jdk17` สำหรับ Java runtime เวอร์ชันล่าสุด; จะช่วยลดความเสี่ยงของคำเตือนความเข้ากันได้

## ขั้นตอนที่ 2: สร้าง workbook และเขียนค่า

Workbook แทนไฟล์ Excel ในหน่วยความจำ คุณสามารถเพิ่มข้อมูลลงในเซลล์ใดก็ได้โดยใช้เมธอด `putValue`

```java
import com.aspose.cells.*;

public class SignificantDigitsDemo {
    public static void main(String[] args) throws Exception {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Put a numeric value into cell A1
        Cell cell = worksheet.getCells().get("A1");
        cell.putValue(123.456789);
```

ตัวเลข `123.456789` จะเป็นแหล่งข้อมูลสำหรับการส่งออกเป็น TXT ของเรา โดยค่าเริ่มต้น Aspose.Cells จะเขียนทศนิยมทั้งหมด ซึ่งมักทำให้ไฟล์ข้อความมีข้อมูลรบกวน

## ขั้นตอนที่ 3: กำหนดค่า TXT save options เพื่อจำกัดหลักสำคัญ

Aspose.Cells มี `TxtSaveOptions` สำหรับควบคุมการส่งออกข้อความอย่างละเอียด เมธอด `setSignificantDigits` บอกตัวส่งออกว่าจะเก็บกี่หลัก **โดยรวม** ไม่ใช่แค่หลังจุดทศนิยม

```java
        // Configure TXT save options to keep only 4 significant digits
        TxtSaveOptions saveOptions = new TxtSaveOptions();
        saveOptions.setSignificantDigits(4); // new option in 25.10
```

เมื่อกำหนด `significantDigits` เป็น `4` ตัวส่งออกจะปัดค่า `123.456789` เป็น `123.5` พฤติกรรมนี้สอดคล้องกับคำนิยามทางคณิตศาสตร์ของหลักสำคัญ: เก็บสี่หลักที่ไม่เป็นศูนย์แรกสุด

### วิธีการตั้งค่านี้แตกต่างจาก “จำกัดทศนิยม”

- **limit decimals** (`setDecimalPlaces`) ตัดเลข *หลัง* จุดทศนิยมโดยไม่คำนึงถึงส่วนจำนวนเต็ม
- **significant digits** (`setSignificantDigits`) นับเลขตั้งแต่ตัวเลขที่ไม่เป็นศูนย์ตัวแรก ซึ่งมีประโยชน์เมื่อค่าตัวเลขมีขนาดต่างกัน

หากต้องการจำนวนตำแหน่งทศนิยมคงที่แทน ให้แทนบรรทัดด้านบนด้วย:

```java
saveOptions.setDecimalPlaces(2); // keeps two digits after the decimal point
```

## ขั้นตอนที่ 4: บันทึก workbook เป็นไฟล์ TXT

ตอนนี้ให้เขียน workbook ไปยังดิสก์โดยใช้ตัวเลือกที่กำหนดไว้

```java
        // Save the workbook as a TXT file using the configured options
        workbook.save("significant_digits.txt", saveOptions);
    }
}
```

การรันโปรแกรมจะสร้างไฟล์ `significant_digits.txt` ในไดเรกทอรีทำงาน ไฟล์นี้มีบรรทัดเดียว:

```
123.5
```

### ผลลัพธ์ที่คาดหวัง

| เซลล์ | ค่าเดิม | ส่งออก (4 หลักสำคัญ) |
|------|----------|------------------------|
| A1   | 123.456789 | 123.5                 |

หากคุณเปลี่ยน `setSignificantDigits(4)` เป็น `6` ผลลัพธ์จะเป็น `123.457` ทดลองเปลี่ยนค่าต่าง ๆ เพื่อดูการปัดเศษที่ปรับเปลี่ยนตาม

## ขั้นตอนที่ 5: ตัวแปรทั่วไปและกรณีขอบ

### การส่งออกช่วงทั้งหมด

หากต้องการส่งออกมากกว่าหนึ่งเซลล์ เพียงเติมค่าช่วงก่อนบันทึก:

```java
worksheet.getCells().get("B1").putValue(0.0012345);
worksheet.getCells().get("C1").putValue(98765.4321);
```

การตั้งค่า `significantDigits` เดียวกันจะใช้กับทุกเซลล์ตัวเลข เพื่อให้ความแม่นยำสอดคล้องกันทั่วไฟล์

### การจัดการตัวคั่นทศนิยมตามโลคัล

Aspose.Cells เคารพโลคัลของระบบเมื่อเขียนข้อความ หากต้องการบังคับให้ใช้จุด (`.`) เป็นตัวคั่นทศนิยม ให้ตั้งค่าภูมิภาคของ `TxtSaveOptions`:

```java
saveOptions.setCultureInfo(java.util.Locale.US);
```

สิ่งนี้มีประโยชน์เมื่อแอปพลิเคชันเป้าหมายคาดหวังรูปแบบเฉพาะ เช่น ตัวแยก CSV ที่รับเฉพาะ `.` เท่านั้น

### การเขียนทับไฟล์ที่มีอยู่

เมธอด `save` จะเขียนทับไฟล์เป้าหมายโดยค่าเริ่มต้น หากต้องการหลีกเลี่ยงการสูญเสียข้อมูลโดยไม่ตั้งใจ ให้ตรวจสอบการมีไฟล์ก่อน:

```java
java.io.File outFile = new java.io.File("significant_digits.txt");
if (outFile.exists()) {
    throw new IllegalStateException("File already exists. Choose a different name or delete the existing file.");
}
workbook.save(outFile.getPath(), saveOptions);
```

### เวิร์กบุ๊กขนาดใหญ่และการใช้หน่วยความจำ

เมื่อส่งออกเวิร์กชีตขนาดใหญ่มาก ควรพิจารณาการสตรีมผลลัพธ์:

```java
saveOptions.setEnableMemorySaving(true);
```

ตัวเลือกนี้ช่วยลดการใช้ heap โดยการเขียนแถวแบบเพิ่มทีละส่วน

## ตัวอย่างทำงานเต็มรูปแบบ

ด้านล่างเป็นโปรแกรมสมบูรณ์ที่คุณสามารถคัดลอก วาง และรันได้ทันที:

```java
import com.aspose.cells.*;

public class SignificantDigitsDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook and access the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Step 2: Put numeric values into cells
        worksheet.getCells().get("A1").putValue(123.456789);
        worksheet.getCells().get("B1").putValue(0.0012345);
        worksheet.getCells().get("C1").putValue(98765.4321);

        // Step 3: Configure TXT save options
        TxtSaveOptions saveOptions = new TxtSaveOptions();
        saveOptions.setSignificantDigits(4);          // limit to 4 significant digits
        saveOptions.setCultureInfo(java.util.Locale.US); // enforce dot as decimal separator
        saveOptions.setEnableMemorySaving(true);      // optional for large files

        // Step 4: Save the workbook as a TXT file
        workbook.save("significant_digits.txt", saveOptions);
    }
}
```

การรันโค้ดนี้จะสร้างไฟล์ `significant_digits.txt` ด้วยเนื้อหาต่อไปนี้ (คอลัมน์คั่นด้วยแท็บ):

```
123.5	0.001235	98770
```

แต่ละตัวเลขปฏิบัติตามกฎ **4 หลักสำคัญ** แสดงให้เห็นว่าการตั้งค่านี้ทำงานได้กับขนาดต่าง ๆ

## สรุป

คุณตอนนี้รู้วิธี **export Excel to TXT** พร้อมควบคุมจำนวนหลักสำคัญ โดยใช้ `TxtSaveOptions.setSignificantDigits` คุณสามารถ **ตั้งค่าหลัก**, **จำกัดทศนิยม**, และ **จำกัดหลักสำคัญ** ด้วยบรรทัดโค้ดเดียวที่ดูแลได้ง่าย วิธีนี้ทำงานได้กับเซลล์เดี่ยว, ช่วงเต็ม, และเวิร์กบุ๊กขนาดใหญ่เช่นกัน

### ขั้นตอนต่อไป

- สำรวจคุณสมบัติอื่นของ `TxtSaveOptions` เช่น `setDelimiter('\t')` เพื่อปรับแต่งตัวคั่นคอลัมน์
- รวม exporter กับ `CsvSaveOptions` หากต้องการค่าที่คั่นด้วยคอมม่าแทนข้อความธรรมดา
- ผสานกระบวนการนี้เข้ากับเว็บเซอร์วิสที่รับไฟล์ Excel ที่อัปโหลดและส่งคืนผลลัพธ์ TXT ที่ตัดทอนแบบเรียลไทม์

ลองทดลองกับขีดจำกัดหลักและโลคัลต่าง ๆ หากเจอสถานการณ์ที่ตัวเลือกในตัวไม่ตรงกับความต้องการพิเศษ คุณสามารถทำการประมวลผลต่อไฟล์ TXT ที่สร้างขึ้นด้วยยูทิลิตี้ I/O ของ Java มาตรฐานได้เสมอ

Happy coding!

## คุณควรเรียนรู้อะไรต่อไป?

บทเรียนต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งรวมโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายทีละขั้นตอน เพื่อช่วยคุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจวิธีการทำงานทางเลือกในโปรเจคของคุณ

- [วิธีแปลงข้อความเป็นตัวเลขใน Excel ด้วย Aspose.Cells for Java](/cells/english/java/cell-operations/convert-text-to-numbers-excel-aspose-cells-java/)
- [วิธีสร้างและส่งออก Excel เป็น HTML ด้วย Aspose.Cells Java | คู่มือการทำงานกับ Workbook](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)
- [วิธีส่งออกคุณสมบัติเฉพาะของ Excel ไปเป็น PDF ด้วย Aspose.Cells for Java](/cells/english/java/workbook-operations/export-excel-custom-properties-pdf-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}