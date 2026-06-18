---
category: general
date: 2026-06-18
description: แปลงวันที่ตามสมัยญี่ปุ่นใน Java ด้วย Aspose.Cells เรียนรู้วิธีอ่านวันที่จากเซลล์
  Excel และดึงข้อมูลวันเวลาออกจากเซลล์ Excel อย่างรวดเร็ว.
draft: false
keywords:
- parse japanese era date
- read date from excel cell
- extract datetime from excel cell
language: th
og_description: แยกวิเคราะห์วันที่ตามยุคญี่ปุ่นใน Java ด้วย Aspose.Cells. คู่มือนี้จะแสดงวิธีการอ่านวันที่จากเซลล์
  Excel และดึงข้อมูลวันเวลาออกจากเซลล์ Excel เพียงไม่กี่ขั้นตอน.
og_title: แยกวันที่สมัยญี่ปุ่นจาก Excel ด้วย Java – คู่มือเต็ม
schemas:
- author: Aspose
  dateModified: '2026-06-18'
  description: Parse Japanese era date in Java using Aspose.Cells. Learn how to read
    date from Excel cell and extract datetime from Excel cell quickly.
  headline: Parse Japanese Era Date from Excel in Java – Full Guide
  type: TechArticle
- description: Parse Japanese era date in Java using Aspose.Cells. Learn how to read
    date from Excel cell and extract datetime from Excel cell quickly.
  name: Parse Japanese Era Date from Excel in Java – Full Guide
  steps:
  - name: Multiple Eras
    text: Japan has had several eras (Meiji, Taishō, Shōwa, Heisei, Reiwa). The `setParseDateUsingJapaneseEra(true)`
      flag covers all of them automatically, but be aware that older dates may fall
      outside the library’s supported range (typically 1868‑present). If you encounter
      a date like “昭和45年12月31日”, the sam
  - name: Blank or Invalid Cells
    text: 'If a cell is empty or contains a malformed string, `cell.getDateTime()`
      throws a `CellsException`. Guard against this with a simple check:'
  - name: Time Component
    text: The example only includes a date, but if your Excel file also stores time
      (e.g., “令和3年5月10日 14:30”), Aspose.Cells will preserve the time portion. The
      `LocalDateTime` you receive will include hours, minutes, and seconds.
  type: HowTo
tags:
- Java
- Excel
- DateTime
title: แยกวันที่ตามสมัยญี่ปุ่นจาก Excel ด้วย Java – คู่มือเต็ม
url: /th/java/cell-operations/parse-japanese-era-date-from-excel-in-java-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# แปลงวันที่ตามสมัยญี่ปุ่นจาก Excel ใน Java – คู่มือเต็ม

เคยต้อง **แปลงวันที่ตามสมัยญี่ปุ่น** ที่เก็บอยู่ในไฟล์ Excel แต่ไม่แน่ใจว่าจะเปลี่ยนให้เป็น `DateTime` ของ Gregorian อย่างไรหรือไม่? คุณไม่ได้อยู่คนเดียว—นักพัฒนาหลายคนเจอปัญหานี้เมื่อต้องทำงานกับแผ่นบัญชีญี่ปุ่นรุ่นเก่าหรือแบบฟอร์มของรัฐบาล ข่าวดีคือด้วยโค้ด Java เพียงไม่กี่บรรทัดและไลบรารีที่เหมาะสม คุณสามารถอ่านวันที่จากเซลล์ Excel และดึงค่า datetime จากเซลล์ Excel ได้โดยไม่ต้องทำการแปลงสตริงด้วยตนเอง

ในบทแนะนำนี้ เราจะเดินผ่านตัวอย่างที่ทำงานได้เต็มรูปแบบซึ่งแสดงให้เห็นอย่างชัดเจนว่า **แปลงวันที่ตามสมัยญี่ปุ่น** เช่น “令和3年5月10日” ให้เป็น `java.time.LocalDateTime` ของ Java เราจะอธิบายการพึ่งพา Maven ที่จำเป็น ทำไมต้องเปิดการแปลงที่รับรู้สมัยญี่ปุ่น และชี้ให้เห็นกับดักทั่วไปที่อาจเจอ หลังจากอ่านจบคุณจะได้โค้ดสแนปช็อตที่พร้อมใช้งานในโปรเจกต์ Java ใด ๆ

## ข้อกำหนดเบื้องต้น

- Java 17 หรือใหม่กว่า (โค้ดทำงานได้บน Java 8+ ด้วย)
- ระบบสร้างโปรเจกต์ Maven หรือ Gradle
- ความคุ้นเคยพื้นฐานกับไฟล์ Excel
- ไลบรารี **Aspose.Cells for Java** (ทดลองใช้ฟรีก็พอสำหรับการทดสอบ)

หากมีส่วนใดที่คุณไม่คุ้นเคย ไม่ต้องกังวล—ผมจะแสดงวิธีเพิ่มไลบรารีและเริ่มต้นอย่างละเอียด

## ขั้นตอนที่ 1: เพิ่ม Aspose.Cells ไปยังโปรเจกต์ของคุณ

สิ่งแรกที่ต้องทำคือเพิ่มไลบรารีที่เข้าใจวันที่ตามสมัยญี่ปุ่น Aspose.Cells จะทำงานหนักให้คุณ

**Maven**:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- check for latest version -->
</dependency>
```

**Gradle**:

```groovy
implementation 'com.aspose:aspose-cells:24.9'
```

เมื่อการพึ่งพาถูกแก้ไขเรียบร้อยแล้ว คุณก็สามารถเริ่มเขียนโค้ดที่ *อ่านวันที่จากเซลล์ Excel* และ *ดึง datetime จากเซลล์ Excel* ได้ทันที

## ขั้นตอนที่ 2: สร้าง Workbook และเลือก Worksheet แรก

เราจะเริ่มด้วยการสร้าง workbook ใหม่ในหน่วยความจำและดึงแผ่นงานแรกออกมา ซึ่งสอดคล้องกับสองบรรทัดแรกของตัวอย่างต้นฉบับ

```java
import com.aspose.cells.*;

public class JapaneseEraDateParser {
    public static void main(String[] args) throws Exception {
        // Step 2: Initialize workbook and worksheet
        Workbook workbook = new Workbook();               // creates a blank workbook
        Worksheet sheet = workbook.getWorksheets().get(0); // first (and only) sheet
```

ทำไมต้องเริ่มจาก workbook ใหม่? เพราะมันรับประกันสภาพแวดล้อมที่สะอาดซึ่งเราควบคุมการตั้งค่าทุกอย่างได้—สิ่งสำคัญเมื่อคุณต้องเปิดการแปลงที่รับรู้สมัยญี่ปุ่นในขั้นตอนต่อไป

## ขั้นตอนที่ 3: ใส่สตริงวันที่ตามสมัยญี่ปุ่นลงในเซลล์ A1

ต่อไปเราจะจำลองไฟล์ Excel ที่มีวันที่ตามสมัยญี่ปุ่นอยู่แล้ว ในชีวิตจริงคุณอาจโหลดไฟล์ `.xlsx` ที่มีอยู่แล้ว แต่เพื่ออธิบาย เราจะ **เขียน** ค่าดังกล่าวด้วยตนเอง

```java
        // Step 3: Insert a Japanese era date string into A1
        Cell cell = sheet.getCells().get("A1");
        cell.putValue("令和3年5月10日"); // Reiwa 3rd year = 2021-05-10
```

สตริงนี้ใช้รูปแบบมาตรฐานของญี่ปุ่น: *สมัย* + *ปี* + *เดือน* + *วัน* หากไม่ได้ตั้งค่าพิเศษ Aspose.Cells จะถือว่าเป็นข้อความธรรมดา ไม่ใช่วันที่

## ขั้นตอนที่ 4: เปิดการแปลงวันที่ที่รับรู้สมัยญี่ปุ่น

นี่คือส่วนสำคัญ: บอก workbook ให้ **แปลงสตริงวันที่ตามสมัยญี่ปุ่น** เมื่อพบ โดยใช้แฟล็ก `ParseDateUsingJapaneseEra`

```java
        // Step 4: Turn on era‑aware parsing
        workbook.getSettings().setParseDateUsingJapaneseEra(true);
```

ทำไมต้องทำเช่นนี้? โดยค่าเริ่มต้น Aspose.Cells จะสมมติว่าปฏิทินเป็น Gregorian ดังนั้น “令和3年5月10日” จะคงเป็นสตริง การเปิดแฟล็กนี้ทำให้เอนจินแปลงเป็น `java.util.Date` (หรือเทียบเท่าใน `java.time`) ภายใน

## ขั้นตอนที่ 5: ดึงค่า DateTime ที่แปลงแล้วออกมา

เมื่อ workbook รู้วิธีตีความสมัยแล้ว เราก็สามารถขอค่า `DateTime` ของเซลล์ได้

```java
        // Step 5: Extract the parsed DateTime
        java.util.Date javaDate = cell.getDateTime(); // returns java.util.Date
        // Convert to java.time.LocalDateTime for modern APIs
        java.time.Instant instant = javaDate.toInstant();
        java.time.ZoneId zone = java.time.ZoneId.systemDefault();
        java.time.LocalDateTime dateTime = java.time.LocalDateTime.ofInstant(instant, zone);
```

สังเกตว่าเรา **อ่านวันที่จากเซลล์ Excel** ด้วย `cell.getDateTime()` วิธีนี้คืนค่า `java.util.Date` ซึ่งเราจะแปลงเป็น `LocalDateTime` ทันทีเพื่อความปลอดภัยของประเภท นี่คือการตอบสนองต่อความต้องการ **ดึง datetime จากเซลล์ Excel** อย่างสะอาดและเป็น idiomatic

## ขั้นตอนที่ 6: ตรวจสอบผลลัพธ์

สุดท้ายพิมพ์วันที่ Gregorian เพื่อยืนยันว่าการแปลงสำเร็จ

```java
        // Step 6: Output the Gregorian date
        System.out.println(dateTime); // Expected output: 2021-05-10T00:00
    }
}
```

เมื่อรันโปรแกรม คุณควรเห็นผลลัพธ์ดังนี้:

```
2021-05-10T00:00
```

ผลลัพธ์นี้พิสูจน์ว่าเราสามารถ **แปลงวันที่ตามสมัยญี่ปุ่น**, **อ่านวันที่จากเซลล์ Excel**, และ **ดึง datetime จากเซลล์ Excel** ได้ในกระบวนการเดียว

## การจัดการกับกรณีขอบเขตในโลกจริง

### หลายสมัย

ญี่ปุ่นมีหลายสมัย (Meiji, Taishō, Shōwa, Heisei, Reiwa) แฟล็ก `setParseDateUsingJapaneseEra(true)` ครอบคลุมทั้งหมดโดยอัตโนมัติ แต่ควรทราบว่าบางวันที่อาจอยู่นอกช่วงที่ไลบรารีสนับสนุน (โดยทั่วไป 1868‑ปัจจุบัน) หากเจอ “昭和45年12月31日” โค้ดเดียวกันจะเปลี่ยนเป็น 1970‑12‑31

### เซลล์ว่างหรือค่าไม่ถูกต้อง

หากเซลล์ว่างหรือมีสตริงที่ผิดรูป `cell.getDateTime()` จะโยน `CellsException` ตรวจสอบด้วยเงื่อนไขง่าย ๆ:

```java
if (cell.getType() == CellValueType.IS_DATE) {
    // safe to call getDateTime()
} else {
    System.out.println("Cell does not contain a parsable date.");
}
```

### ส่วนเวลา

ตัวอย่างนี้มีแค่วันที่เท่านั้น แต่หากไฟล์ Excel ของคุณมีเวลา (เช่น “令和3年5月10日 14:30”) Aspose.Cells จะรักษาส่วนเวลานั้นไว้ `LocalDateTime` ที่ได้จะรวมชั่วโมง นาที และวินาที

## ตัวอย่างทำงานเต็มรูปแบบ

รวมทุกอย่างเข้าด้วยกัน นี่คือโปรแกรมที่พร้อมคัดลอก‑วาง:

```java
import com.aspose.cells.*;
import java.time.*;

public class JapaneseEraDateParser {
    public static void main(String[] args) throws Exception {
        // Create workbook and get first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.getWorksheets().get(0);

        // Insert Japanese era date string into A1
        Cell cell = sheet.getCells().get("A1");
        cell.putValue("令和3年5月10日");

        // Enable era‑aware parsing
        workbook.getSettings().setParseDateUsingJapaneseEra(true);

        // Extract the parsed DateTime
        java.util.Date javaDate = cell.getDateTime();
        LocalDateTime dateTime = javaDate.toInstant()
                                         .atZone(ZoneId.systemDefault())
                                         .toLocalDateTime();

        // Output the Gregorian date
        System.out.println(dateTime); // 2021-05-10T00:00
    }
}
```

บันทึกเป็น `JapaneseEraDateParser.java` คอมไพล์ด้วย `javac` แล้วรันด้วย `java` หากตั้งค่าถูกต้อง คุณจะเห็นวันที่ Gregorian แสดงบนคอนโซล

## เคล็ดลับระดับมืออาชีพ & ข้อควรระวังทั่วไป

- **เคล็ดลับ:** ตั้งค่า `setParseDateUsingJapaneseEra(true)` **ก่อน** อ่านค่าเซลล์ใด ๆ การเปลี่ยนแฟล็กหลังจากอ่านเซลล์แล้วจะไม่แปลงค่าที่อ่านไปแล้ว
- **ระวัง locale:** ไลบรารีแปลงสตริงสมัยโดยอิงอักขระ Unicode จึงไม่จำเป็นต้องตั้ง locale เป็นญี่ปุ่นโดยเฉพาะ
- **ข้อสังเกตเรื่องประสิทธิภาพ:** การเปิดการแปลงสมัยเพิ่มภาระเล็กน้อย หากต้องการเพียงไม่กี่เซลล์ คุณสามารถสลับแฟล็กเปิด‑ปิดได้ตามต้องการ
- **การทดสอบ:** ใช้รุ่นทดลองฟรีของ Aspose เพื่อตรวจสอบกับไฟล์ Excel จริงที่มีหลายสมัย เพื่อให้มั่นใจว่าโค้ดผลิตของคุณทำงานตามที่คาดหวัง

## สรุป

เราได้แสดงวิธี **แปลงวันที่ตามสมัยญี่ปุ่น** โดยตรงจาก workbook ของ Excel ด้วย Java และ Aspose.Cells การเปิดการแปลงที่รับรู้สมัยทำให้คุณสามารถ **อ่านวันที่จากเซลล์ Excel** และ **ดึง datetime จากเซลล์ Excel** ได้อย่างสะอาดและปลอดภัยต่อประเภท วิธีนี้ทำงานกับสมัยญี่ปุ่นสมัยใหม่ทั้งหมด รองรับส่วนเวลา และจัดการกับข้อมูลที่ไม่ถูกต้องอย่างราบรื่น

พร้อมสำหรับความท้าทายต่อไปหรือยัง? ลองโหลดไฟล์ `.xlsx` จริงที่มีการผสมผสานระหว่างวันที่ Gregorian และสมัยญี่ปุ่น หรือทดลองฟอร์แมต `LocalDateTime` ให้ตรงกับ locale ของคุณ คุณอาจลองเขียนวันที่ที่แปลงแล้วกลับไปยัง Excel เพื่อระบบ downstream ที่รับรู้เฉพาะ Gregorian เท่านั้น

มีคำถามหรือเจอกรณีขอบเขตแปลก ๆ? แสดงความคิดเห็นด้านล่าง แล้วขอให้สนุกกับการเขียนโค้ด!

## คุณควรเรียนรู้อะไรต่อไป?

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคในคู่มือนี้ แต่ละแหล่งรวมโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายทีละขั้นตอน เพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการทำงานอื่น ๆ ในโปรเจกต์ของคุณ

- [เชี่ยวชาญระบบวันที่ 1904 ใน Excel ด้วย Aspose.Cells Java สำหรับการจัดการเซลล์ที่มีประสิทธิภาพ](/cells/english/java/cell-operations/aspose-cells-java-configure-1904-date-system-excel/)
- [แปลง Excel เป็น PDF อย่างมีประสิทธิภาพพร้อมรูปแบบวันที่กำหนดเองโดยใช้ Aspose.Cells for Java](/cells/english/java/workbook-operations/render-excel-custom-date-formats-pdf-aspose-cells-java/)
- [วิธีเลือกช่วงเซลล์ใน Excel ด้วย Aspose.Cells for Java (คู่มือ 2023)](/cells/english/java/range-management/aspose-cells-java-select-cell-ranges-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}