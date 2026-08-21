---
category: general
date: 2026-08-20
description: เรียนรู้วิธีส่งออก Excel เป็นไฟล์ TXT พร้อมจำกัดจำนวนตำแหน่งทศนิยม รักษาตัวเลขสำคัญ
  และบันทึกเวิร์กบุ๊กเป็นไฟล์ TXT ด้วย Java.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to txt
- limit decimal places
- keep significant digits
- save workbook as txt
language: th
lastmod: 2026-08-20
og_description: ส่งออก Excel เป็น TXT ด้วย Aspose.Cells. คู่มือนี้แสดงวิธีจำกัดตำแหน่งทศนิยม,
  รักษาตัวเลขสำคัญ, และบันทึกเวิร์กบุ๊กเป็น TXT ใน Java.
og_image_alt: Result of export excel to txt showing limited decimal places and kept
  significant digits
og_title: ส่งออก Excel เป็น TXT ใน Java – ควบคุมตำแหน่งทศนิยมและจำนวนหลักสำคัญ
schemas:
- author: Aspose
  dateModified: '2026-08-20'
  description: Learn to export Excel to TXT while limiting decimal places, keeping
    significant digits, and saving workbook as TXT using Java.
  headline: How to export Excel to TXT with Aspose.Cells and control decimal precision
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel
- Text export
title: วิธีส่งออก Excel เป็นไฟล์ TXT ด้วย Aspose.Cells และควบคุมความแม่นยำของทศนิยม
url: /th/java/excel-import-export/how-to-export-excel-to-txt-with-aspose-cells-and-control-dec/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีส่งออก Excel เป็น TXT ด้วย Aspose.Cells และควบคุมความแม่นยำของทศนิยม

หากคุณต้องการ **ส่งออก Excel เป็น TXT** และต้องการให้ผลลัพธ์รักษาจำนวนตำแหน่งทศนิยมที่กำหนดไว้ คู่มือนี้จะให้วิธีแก้ไขที่ครบถ้วน คุณจะได้เห็นวิธีจำกัดตำแหน่งทศนิยม, เก็บหลักสำคัญ, และ **บันทึกเวิร์กบุ๊กเป็น TXT** ด้วยไลบรารี Aspose.Cells สำหรับ Java

บทแนะนำนี้จะพาคุณผ่านการสร้างเวิร์กบุ๊ก, แทรกค่าที่มีความแม่นยำสูง, ตั้งค่าตัวเลือกการบันทึกเป็น TXT, และเขียนไฟล์ลงดิสก์ เมื่อเสร็จแล้วคุณจะสามารถสร้างไฟล์ข้อความที่มีความแม่นยำตามที่ต้องการโดยไม่ต้องทำการประมวลผลเพิ่มเติม

## สิ่งที่คุณต้องมี

- Java 17 (หรือ JDK ที่รองรับเวอร์ชันอื่น)
- Aspose.Cells for Java 23.10 หรือใหม่กว่า
- IDE หรือเครื่องมือสร้าง (Maven/Gradle) เพื่อจัดการ dependencies
- สิทธิ์การเขียนในไดเรกทอรีปลายทาง

## ขั้นตอนที่ 1: สร้างเวิร์กบุ๊กและเข้าถึงแผ่นงานแรก

การสร้างเวิร์กบุ๊กเป็นขั้นตอนแรกเมื่อคุณต้องการ **ส่งออก Excel เป็น TXT** คลาส `Workbook` แทนไฟล์ Excel ทั้งหมด, ส่วน `Worksheet` ให้คุณเข้าถึงเซลล์ต่าง ๆ

```java
import com.aspose.cells.*;

public class ExportExcelToTxtDemo {
    public static void main(String[] args) throws Exception {
        // Initialize a new workbook
        Workbook workbook = new Workbook();

        // Get the first worksheet (index 0)
        Worksheet sheet = workbook.getWorksheets().get(0);
```

*ทำไมจึงสำคัญ*: วัตถุเวิร์กบุ๊กเก็บข้อมูล, สไตล์, และเมตาดาต้าทั้งหมด การเริ่มต้นด้วยเวิร์กบุ๊กใหม่รับประกันว่าจะไม่มีการจัดรูปแบบที่ซ่อนอยู่มาขัดขวางการส่งออกเป็นข้อความ

## ขั้นตอนที่ 2: เพิ่มค่าตัวเลขและจำกัดตำแหน่งทศนิยม

แทรกตัวเลขที่มีตำแหน่งทศนิยมหลายตำแหน่งเพื่อสาธิตวิธี **จำกัดตำแหน่งทศนิยม** ระหว่างการส่งออก

```java
        // Put a high‑precision number into cell A1
        sheet.getCells().putValue("A1", 0.000123456789);
```

*ทำไมจึงสำคัญ*: Excel จะเก็บความแม่นยำเต็มรูปแบบ, แต่เมื่อคุณส่งออกภายหลังอาจต้องการตัดหรือปัดค่าดังกล่าว การตั้งค่า `limit decimal places` จะจัดการให้โดยอัตโนมัติ

## ขั้นตอนที่ 3: ตั้งค่าตัวเลือกการบันทึก TXT เพื่อเก็บหลักสำคัญ

Aspose.Cells มี `TxtSaveOptions` การตั้งค่า `significantDigits` จะบอกตัวส่งออกให้เก็บเฉพาะหลักสำคัญที่ต้องการ, ไม่สนใจศูนย์นำหน้า

```java
        // Configure TXT export options
        TxtSaveOptions txtOptions = new TxtSaveOptions();

        // Keep exactly 5 significant digits (e.g., 0.00012346)
        txtOptions.setSignificantDigits(5);
```

*ทำไมจึงสำคัญ*: ตัวเลือก **keep significant digits** ทำให้ไฟล์ผลลัพธ์มีความแม่นยำที่คาดเดาได้ ซึ่งจำเป็นสำหรับระบบ downstream ที่คาดหวังรูปแบบตัวเลขความกว้างคงที่

## ขั้นตอนที่ 4: บันทึกเวิร์กบุ๊กเป็น TXT

สุดท้ายให้เขียนเวิร์กบุ๊กลงไฟล์ข้อความ เมธอด `save` จะเคารพตัวเลือกที่คุณตั้งค่าไว้ ทำให้ไฟล์ที่ได้มีการแสดงผลลัพธ์ของตำแหน่งทศนิยมที่จำกัด

```java
        // Define the output path (replace with your own directory)
        String outputPath = "output/SignificantDigits.txt";

        // Export the workbook to TXT using the configured options
        workbook.save(outputPath, txtOptions);

        System.out.println("Export completed: " + outputPath);
    }
}
```

*ทำไมจึงสำคัญ*: การใช้ **save workbook as txt** พร้อม `TxtSaveOptions` ที่เตรียมไว้รับประกันว่าไฟล์ที่ส่งออกตรงกับข้อจำกัดความแม่นยำที่คุณกำหนดในขั้นตอนก่อนหน้า

### เนื้อหาที่คาดว่าจะอยู่ใน `SignificantDigits.txt`

```
0.00012346
```

ค่าที่แสดงมีห้าหลักสำคัญ (`12346`) หลังการปัดเศษ, และศูนย์นำหน้าถูกเก็บไว้ตามรูปแบบ TXT

## ความแปรผันและกรณีขอบ

| สถานการณ์ | การปรับเปลี่ยน |
|----------|------------|
| **จำนวนหลักสำคัญที่ต่างกัน** | เรียก `txtOptions.setSignificantDigits(n)` โดยที่ `n` อยู่ในช่วง 1‑15 |
| **ส่งออกช่วงข้อมูลแทนการส่งออกทั้งแผ่น** | ใช้ `txtOptions.setExportRange("A1:B10")` ก่อนบันทึก |
| **รักษาตัวคั่นคอลัมน์** | ตั้งค่า `txtOptions.setSeparator('\t')` เพื่อให้ผลลัพธ์เป็นแบบแยกด้วยแท็บ |
| **แผ่นงานขนาดใหญ่** | เพิ่ม `txtOptions.setMemorySetting(MemorySetting.MEMORY_PREFERENCES)` เพื่อลดความเสี่ยงของ `OutOfMemoryError` |

## ข้อผิดพลาดทั่วไปและเคล็ดลับระดับมืออาชีพ

- **อย่าสับสนระหว่างหลักสำคัญกับตำแหน่งทศนิยม** ศูนย์นำหน้าไม่ถือเป็นหลักสำคัญ; ใช้ `setSignificantDigits` สำหรับความแม่นยำที่มีความหมายและใช้ `setDecimalPlaces` หากต้องการจำนวนตำแหน่งทศนิยมคงที่หลังจุดทศนิยม
- **ระบุเส้นทางออกแบบเต็มเสมอ** เมื่อรันจาก IDE เพื่อหลีกเลี่ยงข้อผิดพลาดเรื่องสิทธิ์
- **ตรวจสอบไฟล์ที่สร้างขึ้น** ด้วยการเรียก `java.nio.file.Files.readAllLines(Paths.get(outputPath))` เพื่อยืนยันว่าเนื้อหาตรงตามที่คาดหวังก่อนนำไปใช้ในกระบวนการต่อไป

## โค้ดต้นฉบับเต็มสำหรับอ้างอิง

```java
import com.aspose.cells.*;

public class ExportExcelToTxtDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.getWorksheets().get(0);

        // Step 2: Insert a high‑precision number (will be limited later)
        sheet.getCells().putValue("A1", 0.000123456789);

        // Step 3: Set TXT options – keep 5 significant digits
        TxtSaveOptions txtOptions = new TxtSaveOptions();
        txtOptions.setSignificantDigits(5);   // keep significant digits

        // Step 4: Save the workbook as TXT
        String outputPath = "output/SignificantDigits.txt";
        workbook.save(outputPath, txtOptions);

        System.out.println("Export completed: " + outputPath);
    }
}
```

การรันโปรแกรมจะสร้างไฟล์ `SignificantDigits.txt` ที่มีบรรทัดเดียวคือ `0.00012346` แสดงให้เห็นว่ากระบวนการ **export excel to txt** ปฏิบัติตามข้อกำหนด **limit decimal places** และ **keep significant digits** อย่างครบถ้วน

## สรุป

ตอนนี้คุณรู้วิธี **ส่งออก Excel เป็น TXT** ด้วย Aspose.Cells for Java พร้อมการควบคุมความแม่นยำของตัวเลข โดยการตั้งค่า `TxtSaveOptions` คุณสามารถ **จำกัดตำแหน่งทศนิยม**, **เก็บหลักสำคัญ**, และ **บันทึกเวิร์กบุ๊กเป็น txt** ได้อย่างมั่นใจโดยไม่ต้องทำการประมวลผลเพิ่มเติม

ต่อไปคุณอาจสนใจ:

- ส่งออกหลายแผ่นเป็นไฟล์ TXT แยกกัน (`save workbook as txt` ต่อแผ่น)
- ใช้ `setSeparator` เพื่อสร้างผลลัพธ์ที่เข้ากันได้กับ CSV
- อัตโนมัติการแปลงเป็นชุดสำหรับชุดข้อมูลขนาดใหญ่

ลองทดลองเปลี่ยนจำนวนหลักและตัวคั่นต่าง ๆ เพื่อให้ตรงกับความต้องการของโครงการของคุณได้เลย ขอให้สนุกกับการเขียนโค้ด!

## สิ่งที่คุณควรเรียนต่อไป

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งข้อมูลมีโค้ดตัวอย่างทำงานเต็มรูปแบบพร้อมคำอธิบายทีละขั้นตอน เพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการนำไปใช้ในโครงการของคุณเอง

- [วิธีสร้างและส่งออก Excel เป็น HTML ด้วย Aspose.Cells Java | คู่มือการทำงานกับเวิร์กบุ๊ก](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)
- [บันทึก Excel เป็น Text – คู่มือ C# ฉบับสมบูรณ์สำหรับการส่งออก Excel เป็น TXT](/cells/english/net/converting-excel-files-to-other-formats/save-excel-as-text-complete-c-guide-to-export-excel-to-txt/)
- [ส่งออกเวิร์กบุ๊ก Excel เป็นภาพด้วย Aspose.Cells for Java&#58; คู่มือขั้นตอนเต็ม](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}