---
category: general
date: 2026-11-22
description: เรียนรู้วิธีตั้งค่า locale ใน workbook ของ Java, เปลี่ยนภาษาของ workbook,
  และตั้งปฏิทินเป็นภาษาญี่ปุ่น พร้อมตัวอย่างโค้ดที่ชัดเจน
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to set locale
- change workbook language
- set locale to japanese
- how to set calendar
language: th
lastmod: 2026-11-22
og_description: วิธีตั้งค่าโลคัลในเวิร์กบุ๊ก Java อย่างรวดเร็ว ทำตามบทแนะนำนี้เพื่อเปลี่ยนภาษาของเวิร์กบุ๊ก
  ตั้งค่าโลคัลเป็นภาษาญี่ปุ่น และกำหนดค่าปฏิทินญี่ปุ่น
og_image_alt: Screenshot showing how to set locale in a Java workbook
og_title: วิธีตั้งค่าโลเคลในเวิร์กบุ๊ก Java – คู่มือขั้นตอนโดยละเอียด
schemas:
- author: Aspose
  dateModified: '2026-11-22'
  description: Learn how to set locale in a Java workbook, change workbook language,
    and set the calendar to Japanese with clear code examples.
  headline: How to set locale in a Java workbook using Aspose.Cells
  type: TechArticle
- description: Learn how to set locale in a Java workbook, change workbook language,
    and set the calendar to Japanese with clear code examples.
  name: How to set locale in a Java workbook using Aspose.Cells
  steps:
  - name: Run the **FullLocaleExample** class.
    text: Run the **FullLocaleExample** class.
  - name: Open the generated `FullJapaneseLocale.xlsx` in Excel.
    text: Open the generated `FullJapaneseLocale.xlsx` in Excel.
  - name: 'Verify that:'
    text: 'Verify that:'
  type: HowTo
tags:
- Java
- Aspose.Cells
- Internationalization
- Workbook
title: วิธีตั้งค่าโลเคลในเวิร์กบุ๊ก Java ด้วย Aspose.Cells
url: /th/java/workbook-operations/how-to-set-locale-in-a-java-workbook-using-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีตั้งค่า locale ใน Java workbook ด้วย Aspose.Cells

การตั้งค่า locale ใน Java workbook เป็นความต้องการทั่วไปเมื่อคุณต้องการปรับสเปรดชีตให้เข้ากับภูมิภาคต่าง ๆ ในคู่มือนี้คุณจะได้เรียนรู้วิธีตั้งค่า locale, เปลี่ยนภาษา workbook, และตั้งค่าปฏิทินเป็นภาษาญี่ปุ่นโดยใช้ Aspose.Cells API

การทำให้ workbook รองรับหลายภาษาไม่ได้หมายถึงแค่การแปลข้อความเท่านั้น; ยังส่งผลต่อรูปแบบตัวเลข, การแปลงวันที่, และระบบปฏิทินเริ่มต้นด้วย เมื่อจบบทเรียนนี้คุณจะสามารถ:

* กำหนด locale ของ workbook เป็นภาษาญี่ปุ่น (Japan) – **set locale to japanese**.  
* เปลี่ยนภาษา workbook เพื่อให้สูตรและข้อความ UI เคารพวัฒนธรรมเป้าหมาย – **change workbook language**.  
* สลับปฏิทินเป็นปฏิทินจักรพรรดิญี่ปุ่น – **how to set calendar**.  

ขั้นตอนเหล่านี้ทำงานได้กับ Aspose.Cells for Java เวอร์ชันล่าสุด (v23.9 หรือใหม่กว่า) และต้องการสภาพแวดล้อมการพัฒนา Java มาตรฐานเท่านั้น

## ข้อกำหนดเบื้องต้น

| ข้อกำหนด | เหตุผล |
|-------------|--------|
| Java 8 หรือสูงกว่า | ไลบรารีนี้รองรับ Java 8+. |
| Aspose.Cells for Java (v23.9+) | มี `Workbook`, `WorkbookSettings` และยูทิลิตี้สำหรับ locale |
| IDE (IntelliJ IDEA, Eclipse, หรือ VS Code) | สำหรับคอมไพล์และรันตัวอย่าง |
| ความรู้พื้นฐานของ Java | จำเป็นสำหรับการเข้าใจโค้ดสแนปช็อต |

เพิ่ม dependency ของ Aspose.Cells ในไฟล์ `pom.xml` ของคุณ (หรือดาวน์โหลด JAR ด้วยตนเอง):

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
    <classifier>jdk17</classifier> <!-- adjust for your JDK version -->
</dependency>
```

## วิธีตั้งค่า locale และปฏิทินใน workbook

ขั้นตอนแรกคือการสร้างอินสแตนซ์ของ workbook และรับอ็อบเจกต์ settings อ็อบเจกต์ settings จะเปิดเผย API สำหรับ locale และ calendar

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.WorkbookSettings;
import java.util.Locale;
import java.util.Calendar;

public class WorkbookLocaleDemo {
    public static void main(String[] args) {
        // Step 1: Create a new workbook (empty by default)
        Workbook workbook = new Workbook();

        // Step 2: Access the workbook's settings
        WorkbookSettings settings = workbook.getSettings();

        // Step 3: Set the calendar to the Japanese calendar
        // Aspose.Cells uses java.util.Calendar; the Japanese calendar is available via Calendar.JAPANESE
        settings.setCalendar(Calendar.getInstance(Locale.JAPAN));

        // Step 4: Set the locale to Japanese (Japan)
        // This influences number formats, date formats, and built‑in function behaviour.
        settings.setLocale(new Locale("ja", "JP"));

        // Optional: Save the workbook to verify the settings
        workbook.save("LocaleDemo.xlsx");
    }
}
```

### ทำไมแต่ละบรรทัดจึงสำคัญ

* **`new Workbook()`** – สร้าง workbook ว่างเปล่าที่คุณสามารถจัดการก่อนบันทึก  
* **`getSettings()`** – คืนค่าอ็อบเจกต์ `WorkbookSettings`; ตัวเลือกภูมิภาคทั้งหมดอยู่ที่นี่  
* **`setCalendar(...)`** – แทนที่ปฏิทิน Gregorian เริ่มต้นด้วยปฏิทินจักรพรรดิญี่ปุ่น, มีผลต่อการแสดงและการแปลงวันที่  
* **`setLocale(new Locale("ja","JP"))`** – เปลี่ยนภาษาและขนบธรรมเนียมของภูมิภาค (เช่น ชื่อเดือน, เครื่องหมายทศนิยม) นี่คือหัวใจของ **how to set locale** สำหรับ workbook  

เมื่อรันโปรแกรมจะสร้างไฟล์ `LocaleDemo.xlsx` เปิดไฟล์นี้ใน Excel หรือ LibreOffice แล้วคุณจะเห็นชื่อเดือนเป็นภาษาญี่ปุ่น, สัญลักษณ์สกุลเงินเยน, และวันที่ที่จัดรูปแบบตามปฏิทินญี่ปุ่น

## เปลี่ยนภาษา workbook (ตั้งค่า locale เป็นญี่ปุ่น)

หากเป้าหมายหลักของคุณคือ **change workbook language** คุณสามารถโฟกัสที่การเรียก `setLocale` เพียงอย่างเดียว ตัวสแนปช็อตต่อไปนี้แยกขั้นตอนนั้นออกมา:

```java
Workbook workbook = new Workbook();
WorkbookSettings settings = workbook.getSettings();

// Change only the language to Japanese (Japan)
settings.setLocale(new Locale("ja", "JP"));
workbook.save("JapaneseLanguage.xlsx");
```

**อะไรที่เปลี่ยนไป?**  
* สตริงการจัดรูปแบบเซลล์จะเปลี่ยนเป็นภาษาญี่ปุ่น (เช่น `#,##0.00` จะมีสัญลักษณ์เยน)  
* ชื่อฟังก์ชันในตัว (เช่น `SUM`) ยังคงเป็นภาษาอังกฤษ เพราะ locale ของฟังก์ชัน Excel แยกจากกัน, แต่สตริงวันที่และข้อความข้อผิดพลาดจะตามขนบธรรมเนียมญี่ปุ่น  

**เมื่อใดควรใช้?**  
* เมื่อคุณต้องการสเปรดชีตที่แสดงตัวเลขและวันที่สำหรับผู้ใช้ญี่ปุ่น แต่ปฏิทินพื้นฐานยังคงเป็น Gregorian  
* สำหรับรายงานที่ส่งออกเป็น PDF หรือพิมพ์, เพื่อให้ภาษาภาพลักษณ์ตรงกับตลาดเป้าหมาย  

## วิธีตั้งค่าปฏิทินเป็นปฏิทินญี่ปุ่น

บางครั้งความต้องการ **how to set calendar** แยกจาก locale สำหรับระบบเก่าที่เก็บวันที่ในยุคจักรพรรดิญี่ปุ่น คุณต้องตั้งค่าปฏิทินโดยชัดเจนแม้จะคง locale เริ่มต้นไว้ก็ตาม

```java
Workbook workbook = new Workbook();
WorkbookSettings settings = workbook.getSettings();

// Set only the calendar; keep the default (US) locale
settings.setCalendar(Calendar.getInstance(Locale.JAPAN));

// Verify the calendar by creating a date cell
int row = 0, column = 0;
workbook.getWorksheets().get(0).getCells().putValue(row, column, new java.util.Date());

// Save to see the Japanese era (e.g., "R3/04/01" for Reiwa 3)
workbook.save("JapaneseCalendar.xlsx");
```

**จุดสำคัญ:**

* `Calendar.getInstance(Locale.JAPAN)` คืนค่า `java.util.Calendar` ที่กำหนดค่าให้สอดคล้องกับยุคญี่ปุ่น  
* workbook จะเริ่มแสดงวันที่ด้วยสัญลักษณ์ยุค (R สำหรับ Reiwa, H สำหรับ Heisei ฯลฯ)  
* การตั้งค่านี้ **ไม่** มีผลต่อรูปแบบตัวเลขหรือภาษาของ UI; หากต้องการทั้งสองอย่างให้ใช้ร่วมกับ `setLocale`  

## ตัวอย่างครบวงจร (end‑to‑end)

ด้านล่างเป็นโปรแกรมเต็มที่สามารถรันได้ซึ่งสาธิต **how to set locale**, **change workbook language**, และ **set the calendar** ในขั้นตอนเดียวกัน พร้อมเพิ่มเซลล์ตัวอย่างเพื่อแสดงผล

```java
import com.aspose.cells.*;
import java.util.*;

public class FullLocaleExample {
    public static void main(String[] args) throws Exception {
        // Create a new workbook
        Workbook workbook = new Workbook();

        // Access settings
        WorkbookSettings settings = workbook.getSettings();

        // 1️⃣ Set the locale to Japanese (Japan) – changes language & number formats
        settings.setLocale(new Locale("ja", "JP"));

        // 2️⃣ Set the calendar to the Japanese imperial calendar
        settings.setCalendar(Calendar.getInstance(Locale.JAPAN));

        // 3️⃣ Add a sample date and number to visualize the changes
        Worksheet sheet = workbook.getWorksheets().get(0);
        Cells cells = sheet.getCells();

        // Date cell – will show Japanese era after applying the calendar
        cells.putValue(0, 0, new Date());

        // Number cell – will use Japanese Yen symbol and comma separator
        cells.putValue(1, 0, 1234567.89);

        // Apply a style to the number cell for currency formatting
        Style style = cells.getRows().get(1).getStyle();
        style.setNumber(3); // Built‑in currency format
        cells.getRows().get(1).setStyle(style);

        // Save the workbook
        workbook.save("FullJapaneseLocale.xlsx");
        System.out.println("Workbook created with Japanese locale and calendar.");
    }
}
```

**ผลลัพธ์ที่คาดหวัง:**  
เมื่อเปิด `FullJapaneseLocale.xlsx` เซลล์แรกจะแสดงวันที่เช่น `R3/04/01` (Reiwa 3) และเซลล์ที่สองจะจัดรูปแบบเป็น `¥1,234,567.89` สิ่งนี้ยืนยันว่า **how to set locale**, **change workbook language**, และ **how to set calendar** ทำงานร่วมกันได้อย่างถูกต้อง

## ข้อผิดพลาดทั่วไปและวิธีหลีกเลี่ยง

| ข้อผิดพลาด | สาเหตุ | วิธีแก้ |
|---------|----------------|-----|
| ใช้ `Locale.CHINA` แทน `new Locale("ja","JP")` | `Locale.CHINA` ตั้งค่าภาษาจีน ไม่ใช่ญี่ปุ่น | สร้าง `Locale` ด้วย `"ja", "JP"` เสมอสำหรับญี่ปุ่น |
| ลืมเรียก `settings.setCalendar(...)` หลังจาก `setLocale` | ปฏิทินยังคงเป็น Gregorian ทำให้วันที่แสดงในยุคผิด | เรียก `setCalendar` **หลัง** ตั้งค่า locale, หรือกำหนดทั้งสองพร้อมกันตามตัวอย่าง |
| บันทึก workbook ก่อนปรับตั้งค่า | การตั้งค่าถูกนำไปใช้กับอ็อบเจกต์ในหน่วยความจำ; การบันทึกก่อนจะบันทึก locale เริ่มต้น | ปรับการตั้งค่า locale/calendar **ก่อน** เรียก `workbook.save()` |
| ใช้ Aspose.Cells เวอร์ชันเก่า | เวอร์ชันเก่าขาด overload ของ `setCalendar` | อัปเกรดเป็น v23.9+ หรือตรวจสอบ release notes สำหรับการสนับสนุน locale |

## การทดสอบการตั้งค่าของคุณ

1. รันคลาส **FullLocaleExample**  
2. เปิดไฟล์ `FullJapaneseLocale.xlsx` ที่สร้างขึ้นใน Excel  
3. ตรวจสอบว่า:  
   * คอลัมน์วันที่แสดงสัญลักษณ์ยุคญี่ปุ่น (`R`, `H` ฯลฯ)  
   * คอลัมน์ตัวเลขใช้สัญลักษณ์เยนและคั่นด้วยเครื่องหมายคอมม่า  
   * ข้อความข้อผิดพลาดในตัวอย่าง (เช่น `#DIV/0!`) แสดงเป็นภาษาญี่ปุ่นหาก workbook มีข้อผิดพลาด  

หากตรวจสอบไม่ผ่าน ให้ตรวจสอบว่าอ็อบเจกต์ `WorkbookSettings` ที่คุณแก้ไขเป็นอ็อบเจกต์เดียวกับที่ใช้เมื่อบันทึกไฟล์

## ขั้นตอนต่อไป

* **Localize formulas** – แม้ locale จะควบคุมการจัดรูปแบบ, คุณยังสามารถแปลชื่อฟังก์ชันแบบกำหนดเองด้วย `FormulaParser`  
* **Apply locale to existing workbooks** – โหลด workbook ด้วย `new Workbook` แล้วปรับ `WorkbookSettings` ตามที่ต้องการ  

## คุณควรเรียนรู้อะไรต่อไป?

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคในคู่มือนี้ แต่ละแหล่งข้อมูลมีโค้ดตัวอย่างทำงานเต็มรูปแบบพร้อมคำอธิบายขั้นตอนเพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการทำงานอื่น ๆ ในโครงการของคุณ

- [Aspose Cells Date Format: How to Set Custom Date Format in Java](/cells/english/java/formatting/aspose-cells-date-format-how-to-set-custom-date-format-in-ja/)
- [How to Set Language in Excel Files Using Aspose.Cells .NET for Multilingual Support](/cells/english/net/formulas-functions/specify-language-excel-aspose-cells-net/)
- [How to set cell number format and convert Japanese dates in C# using Aspose.Cells](/cells/english/net/excel-custom-number-date-formatting/set-cell-number-format-and-convert-japanese-dates-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}