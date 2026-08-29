---
category: general
date: 2026-07-03
description: แยกวิเคราะห์วันที่ด้วยการตั้งค่าท้องถิ่นโดยใช้ Java’s java.time API.
  เรียนรู้การจัดการรูปแบบยุคญี่ปุ่น, การแปลงวันที่ตามท้องถิ่น, และเทคนิคการแยกวิเคราะห์วันที่ใน
  Java อย่างมั่นคง.
draft: false
keywords:
- parse date with locale
- java date parsing
- japanese era format
- locale date conversion
- java time API
language: th
og_description: แปลงวันที่ด้วยโลคัลใน Java โดยใช้ API java.time คู่มือนี้แสดงการจัดการรูปแบบยุคญี่ปุ่น,
  การแปลงวันที่ตามโลคัล, และแนวทางปฏิบัติที่ดีที่สุดสำหรับการแปลงวันที่ที่เชื่อถือได้.
og_title: แปลงวันที่ด้วย Locale ใน Java – บทเรียนการเขียนโปรแกรมเต็ม
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Parse date with locale using Java’s java.time API. Learn Japanese era
    format handling, locale date conversion, and robust java date parsing techniques.
  headline: Parse Date with Locale in Java – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Parse date with locale using Java’s java.time API. Learn Japanese era
    format handling, locale date conversion, and robust java date parsing techniques.
  name: Parse Date with Locale in Java – Complete Step‑by‑Step Guide
  steps:
  - name: Define the Era Date String
    text: First, store the Japanese era string exactly as you receive it (e.g., from
      a CSV file or UI).
  - name: Build a Locale‑Aware Formatter
    text: Java’s **java.time API** lets you tie a `DateTimeFormatter` to a specific
      chronology (calendar system) and `Locale`. For the Japanese era we use `JapaneseChronology`.
  - name: Parse and Convert to Gregorian `LocalDate`
    text: Now we actually parse the string and transform the result into a classic
      `LocalDate` that any Java library can consume.
  - name: What if the input uses a different era symbol?
    text: Japanese eras change roughly every few decades. The formatter automatically
      recognises `M` (Meiji), `T` (Taisho), `S` (Showa), `H` (Heisei), and `R` (Reiwa).
      If you receive an older era not covered by the default `JapaneseChronology`,
      you’ll get a `DateTimeParseException`. In that case, verify the s
  - name: How to support other non‑Gregorian calendars?
    text: 'The pattern is identical; you just swap the chronology and locale. For
      example, Thai Buddhist dates (`BuddhistChronology`) look like this:'
  - name: Can I parse without an era symbol (pure year‑month‑day)?
    text: Yes—simply omit `G` from the pattern and use the default `ISO_LOCAL_DATE`
      formatter. That’s the classic *java date parsing* route for Gregorian strings.
  - name: What about lenient parsing (e.g., missing leading zeros)?
    text: Switch `ResolverStyle.STRICT` to `ResolverStyle.LENIENT`. Be aware that
      lenient mode may silently roll over invalid dates (e.g., `R5/13/40` becomes
      `2024‑02‑09`). For production code, strict mode is usually safer.
  type: HowTo
tags:
- java
- date-time
- localization
title: แปลงวันที่ด้วย Locale ใน Java – คู่มือขั้นตอนเต็ม
url: /th/java/advanced-features/parse-date-with-locale-in-java-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# แปลงวันที่ด้วย Locale ใน Java – คู่มือขั้นตอนเต็ม

เคยต้อง **parse date with locale** ใน Java แต่ไม่แน่ใจว่าจะใช้คลาสใดหรือไม่? คุณไม่ได้อยู่คนเดียว—การจัดการกับปฏิทินที่ไม่ใช่ Gregorian หรือรูปแบบตามภูมิภาคอาจรู้สึกเหมือนการถอดรหัสภาษาลับ ในบทเรียนนี้เราจะอธิบายตัวอย่างจริง: แปลงสตริงยุคญี่ปุ่นเช่น `R5/04/01` ให้เป็นอ็อบเจ็กต์ `Date` Gregorian มาตรฐาน `2023‑04‑01` เมื่อจบคุณจะได้รูปแบบที่นำกลับมาใช้ใหม่ได้สำหรับรูปแบบวันที่ตาม locale ใดก็ได้

เราจะครอบคลุมทุกอย่างตั้งแต่การนำเข้า (imports) ที่จำเป็นจนถึงการจัดการกรณีขอบ และเราจะสอดแทรกแนวคิดที่เกี่ยวข้องบางอย่าง—*java date parsing*, *japanese era format*, *locale date conversion*, และ *java time API* สมัยใหม่—เพื่อให้คุณปรับใช้โซลูชันกับโปรเจกต์ของคุณเอง ไม่ต้องใช้ไลบรารีภายนอก เพียงแค่ Java 8+

---

## สิ่งที่บทเรียนนี้ครอบคลุม

- ตั้งค่าสตริงรูปแบบ **Japanese era** (`Reiwa`)
- ใช้ `DateTimeFormatter` กับ `JapaneseChronology` และ `Locale`
- แปลง `JapaneseDate` ที่ได้เป็น `LocalDate` (Gregorian)
- พิมพ์วันที่ ISO‑8601 สุดท้าย
- ข้อผิดพลาดทั่วไป เช่น ยุคที่ไม่รองรับหรือรูปแบบที่ไม่ตรงกัน
- ตัวแปรอย่างรวดเร็วสำหรับ locale อื่น ๆ (Thai Buddhist, Islamic, ฯลฯ)

**Prerequisites**  
JDK 8 หรือใหม่กว่า, ความคุ้นเคยพื้นฐานกับ `java.time`, และ IDE หรือ CLI เพื่อรันโค้ด Java แค่นั้น—ไม่ต้องมี dependencies ของ Maven เพิ่มเติม

## แปลงวันที่ด้วย Locale – ขั้นตอนต่อขั้นตอน

ด้านล่างเราจะแบ่งวิธีแก้เป็นสามขั้นตอนธรรมชาติ แต่ละขั้นตอนจะมีโค้ดที่ต้องใช้ คำอธิบายสั้น ๆ เกี่ยวกับ *ทำไม* จึงสำคัญ และเคล็ดลับที่คุณอาจไม่พบในเอกสารอย่างเป็นทางการ

### ขั้นตอน 1: กำหนดสตริงวันที่ตามยุค

ก่อนอื่น ให้เก็บสตริงยุคญี่ปุ่นไว้ตามที่คุณได้รับ (เช่น จากไฟล์ CSV หรือ UI)

```java
// Step 1: Define a date string using the Japanese era format (Reiwa 5)
String eraDateString = "R5/04/01";
```

> **Why this matters:**  
> ตัวอักษรนำหน้า `R` หมายถึง *Reiwa* ยุคปัจจุบันของญี่ปุ่น หากคุณละเว้นสัญลักษณ์ยุค ตัวพาร์สเซอร์จะสมมติว่าตรงกับปฏิทิน Gregorian และให้ปีที่ไม่ถูกต้อง

### ขั้นตอน 2: สร้าง Formatter ที่รับรู้ Locale

**java.time API** ของ Java ช่วยให้คุณผูก `DateTimeFormatter` กับ chronology (ระบบปฏิทิน) และ `Locale` ที่ระบุ สำหรับยุคญี่ปุ่นเราจะใช้ `JapaneseChronology`

```java
import java.time.chrono.JapaneseChronology;
import java.time.format.DateTimeFormatter;
import java.time.format.ResolverStyle;
import java.util.Locale;

// Step 2: Create a formatter that understands the Japanese era pattern
DateTimeFormatter japaneseFormatter = new DateTimeFormatterBuilder()
        .parseCaseInsensitive()
        .appendPattern("Gyy/MM/dd")          // G = era symbol, yy = year-of-era
        .toFormatter(Locale.JAPAN)           // Locale for Japanese symbols
        .withChronology(JapaneseChronology.INSTANCE)
        .withResolverStyle(ResolverStyle.STRICT);
```

**Key points**  
- `G` พาร์สข้อความยุค (`R` สำหรับ Reiwa, `H` สำหรับ Heisei, ฯลฯ)  
- `ResolverStyle.STRICT` บังคับให้พาร์สเซอร์ปฏิเสธวันที่ที่เป็นไปไม่ได้เช่น `R0/13/32`  
- การตั้งค่า `Locale` เป็น `Locale.JAPAN` ทำให้สัญลักษณ์ยุคตรงกับแนวปฏิบัติของญี่ปุ่น

> **Pro tip:** หากต้องสนับสนุนรูปแบบยุคหลายแบบ (เช่น `HEISEI` แบบเต็ม) ให้เพิ่ม `.parseCaseInsensitive()` ตามที่แสดง และขยายแพทเทิร์นเป็น `Guuuu` สำหรับชื่อเต็ม

### ขั้นตอน 3: แปลงและแปลงเป็น Gregorian `LocalDate`

ตอนนี้เราจะพาร์สสตริงและแปลงผลลัพธ์ให้เป็น `LocalDate` คลาสสิกที่ไลบรารี Java ใด ๆ ก็ใช้ได้

```java
import java.time.LocalDate;
import java.time.chrono.JapaneseDate;

// Step 3: Parse the era string and convert to Gregorian LocalDate
JapaneseDate japaneseDate = JapaneseDate.from(japaneseFormatter.parse(eraDateString));
LocalDate gregorianDate = LocalDate.from(japaneseDate);

// Verify the conversion
System.out.println(gregorianDate);   // Expected output: 2023-04-01
```

> **Explanation**  
> `JapaneseDate.from(...)` สร้างอ็อบเจ็กต์วันที่ที่อิงกับปฏิทินญี่ปุ่น โดยการเรียก `LocalDate.from(...)` เราจะลบข้อมูลยุคออกและได้วันที่ ISO‑8601 ที่เทียบเท่า—เหมาะสำหรับการจัดเก็บ, การเปรียบเทียบ หรือการเรียก API

> **Why convert?** ฐานข้อมูลส่วนใหญ่, บริการ REST, และไลบรารีของบุคคลที่สามคาดหวังวันที่ Gregorian การทำการแปลงภายในขั้นตอนพาร์สช่วยป้องกันบั๊กที่ซ่อนอยู่ในภายหลัง

## ตัวอย่างการทำงานเต็ม

รวมทุกอย่างเข้าด้วยกัน นี่คือคลาส Java ที่พร้อมรัน เพียงคัดลอก‑วางลงใน `ParseDateWithLocale.java` แล้วดำเนินการ

```java
import java.time.LocalDate;
import java.time.chrono.JapaneseChronology;
import java.time.chrono.JapaneseDate;
import java.time.format.DateTimeFormatter;
import java.time.format.DateTimeFormatterBuilder;
import java.time.format.ResolverStyle;
import java.util.Locale;

public class ParseDateWithLocale {

    public static void main(String[] args) {
        // --- Step 1: Input ---
        String eraDateString = "R5/04/01";

        // --- Step 2: Formatter ---
        DateTimeFormatter japaneseFormatter = new DateTimeFormatterBuilder()
                .parseCaseInsensitive()
                .appendPattern("Gyy/MM/dd")
                .toFormatter(Locale.JAPAN)
                .withChronology(JapaneseChronology.INSTANCE)
                .withResolverStyle(ResolverStyle.STRICT);

        // --- Step 3: Parse & Convert ---
        JapaneseDate japaneseDate = JapaneseDate.from(japaneseFormatter.parse(eraDateString));
        LocalDate gregorianDate = LocalDate.from(japaneseDate);

        // Output
        System.out.println("Original era string: " + eraDateString);
        System.out.println("Converted Gregorian date: " + gregorianDate);
    }
}
```

**ผลลัพธ์ที่คาดหวังในคอนโซล**

```
Original era string: R5/04/01
Converted Gregorian date: 2023-04-01
```

รันโปรแกรมด้วย `javac ParseDateWithLocale.java && java ParseDateWithLocale` หากคุณเห็นสองบรรทัดข้างต้น คุณได้ **parse date with locale** สำเร็จแล้ว

## การจัดการกรณีขอบและคำถามทั่วไป

### What if the input uses a different era symbol?

ยุคของญี่ปุ่นเปลี่ยนประมาณทุกไม่กี่ทศวรรษ Formatter จะรับรู้โดยอัตโนมัติ `M` (Meiji), `T` (Taisho), `S` (Showa), `H` (Heisei) และ `R` (Reiwa) หากคุณได้รับยุคที่เก่ากว่าที่ `JapaneseChronology` เริ่มต้นรองรับ จะเกิด `DateTimeParseException` ในกรณีนั้น ให้ตรวจสอบข้อมูลต้นทางหรือสร้างแมปปิ้งแบบกำหนดเอง

### How to support other non‑Gregorian calendars?

แพทเทิร์นเหมือนเดิม; เพียงสลับ chronology และ locale ตัวอย่างเช่น วันที่ไทยพุทธศักราช (`BuddhistChronology`) จะเป็นดังนี้:

```java
DateTimeFormatter thaiFormatter = new DateTimeFormatterBuilder()
        .appendPattern("Gyy/MM/dd")
        .toFormatter(new Locale("th", "TH"))
        .withChronology(java.time.chrono.ThaiBuddhistChronology.INSTANCE);
```

### Can I parse without an era symbol (pure year‑month‑day)?

ได้—เพียงลบ `G` ออกจากแพทเทิร์นและใช้ `ISO_LOCAL_DATE` formatter เริ่มต้น นั่นคือวิธี *java date parsing* แบบคลาสสิกสำหรับสตริง Gregorian

### What about lenient parsing (e.g., missing leading zeros)?

สลับ `ResolverStyle.STRICT` เป็น `ResolverStyle.LENIENT` ระวังว่าโหมด lenient อาจทำให้วันที่ที่ไม่ถูกต้องกลายเป็นวันที่อื่นโดยอัตโนมัติ (เช่น `R5/13/40` กลายเป็น `2024‑02‑09`) สำหรับโค้ด production ควรใช้โหมด strict จะปลอดภัยกว่า

## เคล็ดลับมืออาชีพสำหรับการแปลงวันที่ Locale ที่มั่นคง

1. **Cache the formatter** – การสร้าง `DateTimeFormatter` ค่อนข้างเบา แต่หากคุณพาร์สหลายพันวันที่ต่อวินาที ควรเก็บไว้ในฟิลด์ `static final`
2. **Validate input length** – การตรวจสอบอย่างรวดเร็ว `if (eraDateString.length() != 8)` สามารถหลีกเลี่ยงข้อยกเว้นจากการพาร์สที่ไม่จำเป็น
3. **Log the original string** – เมื่อดีบักปัญหา locale อินพุตดิบมักเปิดเผยอักขระที่มองไม่เห็น (เช่น zero‑width spaces) ที่ทำให้พาร์สเซอร์ล้มเหลว
4. **Unit‑test each era** – เขียนเทสต์ JUnit สำหรับ `R`, `H`, `S` ฯลฯ เพื่อรับประกันว่าการอัปเดตของ Java ในอนาคตจะไม่เปลี่ยนแปลงการแมป

## สรุป

เราได้สาธิตวิธี **parse date with locale** ใน Java โดยใช้ *java time API* สมัยใหม่, `DateTimeFormatter` ที่รับรู้ locale, และ `JapaneseChronology` ตัวอย่างเต็มแสดงกระบวนการทั้งหมด—from สตริงยุคญี่ปุ่นดิบจนถึง `LocalDate` Gregorian ที่สะอาด—และให้คุณพร้อมปรับรูปแบบนี้สำหรับปฏิทินอื่น ๆ เช่น ระบบไทยพุทธศักราชหรืออิสลาม

ขั้นตอนต่อไป? ลองสลับ `JapaneseChronology` เป็น `ThaiBuddhistChronology` หรือ `HijrahChronology` แล้วดูว่าโครงสร้างโค้ดเดียวกันจัดการกับปฏิทินวัฒนธรรมที่แตกต่างกันอย่างไร คุณอาจอยากลองฟอร์แมต `LocalDate` ที่ได้กลับเป็นสตริงตาม locale ด้วย `DateTimeFormatter.ofLocalizedDate(FormatStyle.FULL)`

มี locale ที่ซับซ้อนหรือข้อผิดพลาดการพาร์สที่ไม่คาดคิด? แสดงความคิดเห็นด้านล่าง แล้วเราจะช่วยกันแก้ไข Happy coding!

## สิ่งที่คุณควรเรียนต่อไป?

บทเรียนต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งรวมตัวอย่างโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายขั้นตอนเพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการทำงานทางเลือกในโปรเจกต์ของคุณเอง

- [เชี่ยวชาญการนำเสนอข้อมูลใน Excel: การจัดรูปแบบตัวเลขและวันที่แบบกำหนดเองด้วย Aspose.Cells สำหรับ Java](/cells/english/java/formatting/aspose-cells-java-data-formatting-excel/)
- [แปลง Excel เป็น PDF อย่างมีประสิทธิภาพด้วยรูปแบบวันที่กำหนดเองโดยใช้ Aspose.Cells สำหรับ Java](/cells/english/java/workbook-operations/render-excel-custom-date-formats-pdf-aspose-cells-java/)
- [เชี่ยวชาญระบบวันที่ 1904 ใน Excel ด้วย Aspose.Cells Java เพื่อการดำเนินการเซลล์ที่มีประสิทธิภาพ](/cells/english/java/cell-operations/aspose-cells-java-configure-1904-date-system-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}