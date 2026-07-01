---
category: general
date: 2026-06-30
description: ตั้งค่ารูปแบบตัวเลขแบบกำหนดเองใน Excel ด้วย Java. เรียนรู้วิธีสร้างเวิร์กบุ๊ก
  Excel ด้วย Java, ดึงค่าวันที่และเวลาออกจากเซลล์, คำนวณสูตรในเวิร์กบุ๊กและแสดงค่าตัววันเวลาออกมา.
draft: false
keywords:
- set custom number format
- get datetime from cell
- create excel workbook java
- calculate workbook formulas
- output datetime value
language: th
og_description: ตั้งค่ารูปแบบตัวเลขแบบกำหนดเองใน Excel ด้วย Java คู่มือนี้แสดงวิธีสร้าง
  workbook Excel ด้วย Java ดึงค่า datetime จากเซลล์ คำนวณสูตรใน workbook และแสดงค่าตัว
  datetime.
og_title: ตั้งค่ารูปแบบตัวเลขแบบกำหนดเองใน Excel ด้วย Java – บทเรียนเต็ม
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Set custom number format in Excel using Java. Learn how to create Excel
    workbook Java, get datetime from cell, calculate workbook formulas and output
    datetime value.
  headline: Set Custom Number Format in Excel with Java – Complete Guide
  type: TechArticle
- description: Set custom number format in Excel using Java. Learn how to create Excel
    workbook Java, get datetime from cell, calculate workbook formulas and output
    datetime value.
  name: Set Custom Number Format in Excel with Java – Complete Guide
  steps:
  - name: The **set custom number format** was applied (you can open the generated
      `.xlsx` in Excel to see “令和2年4月1日”).
    text: The **set custom number format** was applied (you can open the generated
      `.xlsx` in Excel to see “令和2年4月1日”).
  - name: The **calculate workbook formulas** step succeeded, turning the era string
      into a real date.
    text: The **calculate workbook formulas** step succeeded, turning the era string
      into a real date.
  - name: The **get datetime from cell** call returned a proper `Calendar`, which
      we then **output datetime value** to the console.
    text: The **get datetime from cell** call returned a proper `Calendar`, which
      we then **output datetime value** to the console.
  type: HowTo
tags:
- Java
- Excel
- Aspose.Cells
- DateTime
title: ตั้งค่ารูปแบบตัวเลขแบบกำหนดเองใน Excel ด้วย Java – คู่มือฉบับสมบูรณ์
url: /th/java/formatting/set-custom-number-format-in-excel-with-java-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ตั้งค่ารูปแบบตัวเลขแบบกำหนดเองใน Excel ด้วย Java – คู่มือเต็ม

เคยต้องการ **set custom number format** ในแผ่น Excel ขณะทำงานด้วย Java หรือไม่? คุณไม่ได้เป็นคนเดียว ไม่ว่าคุณจะกำลังสร้างเครื่องมือรายงานหรือเพียงแค่ต้องการแสดงวันที่ตามสมัยญี่ปุ่นอย่างถูกต้อง การเชี่ยวชาญเทคนิคนี้จะช่วยคุณประหยัดเวลาการประมวลผลหลังจากนั้นเป็นจำนวนมาก ในบทเรียนนี้เราจะเดินผ่านตัวอย่างจากโลกจริงที่ **creates Excel workbook Java**, ใช้รูปแบบตามโลคัล, คำนวณสูตรใหม่, และสุดท้าย **gets DateTime from cell** เพื่อ **output datetime value**.

เราจะใช้ไลบรารี Aspose.Cells for Java ที่เป็นที่นิยม เพราะมันจัดการรูปแบบตัวเลขและวันที่ที่รับรู้วัฒนธรรมโดยอัตโนมัติ เมื่อตอนจบบทเรียนคุณจะมีโปรแกรมที่ทำงานได้เองและสามารถใส่ลงในโปรเจค Maven หรือ Gradle ใดก็ได้ ไม่ต้องพึ่ง “ดูเอกสาร” ที่คลุมเครือ—แค่โค้ดที่มั่นคงและคำอธิบายที่ชัดเจน

---

## สิ่งที่คุณจะได้เรียนรู้

- วิธี **create Excel workbook Java** อย่างโปรแกรมเมติก
- ขั้นตอนที่แม่นยำในการ **set custom number format** สำหรับวันที่ตามสมัยญี่ปุ่น
- ทำไมการเรียก **calculate workbook formulas** จึงสำคัญก่อนดึงค่ามา
- วิธีที่ถูกต้องในการ **get datetime from cell** และ **output datetime value**
- ข้อผิดพลาดทั่วไป (ขาดโลคัล, สูตรค้าง) และวิธีแก้อย่างรวดเร็ว

---

## ข้อกำหนดเบื้องต้น

- Java 8 หรือใหม่กว่า ติดตั้งบนเครื่องของคุณ  
- Aspose.Cells for Java 23.11 (หรือเวอร์ชันล่าสุด)  
- IDE หรือ text editor เบื้องต้น—IntelliJ IDEA, Eclipse, VS Code, หรืออะไรก็ได้ที่คุณชอบ  

หากคุณยังไม่ได้เพิ่ม Aspose.Cells เข้าในโปรเจคของคุณ ให้คัดลอกส่วน Maven ด้านล่างนี้ไปวางในไฟล์ `pom.xml` ของคุณ:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.11</version>
</dependency>
```

ผู้ใช้ Gradle สามารถเพิ่มได้ดังนี้:

```gradle
implementation 'com.aspose:aspose-cells:23.11'
```

เมื่อสภาพแวดล้อมพร้อมแล้ว ไปที่โค้ดกันเลย

---

## ขั้นตอนที่ 1: Set Custom Number Format – ภาพรวม

ก่อนจะเขียน Java ใด ๆ เราควรจินตนาการว่าต้องการอะไร ลองนึกถึงเซลล์ Excel ที่ควรแสดง **“令和2年4月1日”** แทนสตริง ISO‑8601 “2020‑04‑01” ค่าเดิมยังคงเป็นวันที่จริง (สูตรยังทำงานได้) แต่ *การแสดงผล* จะตามรูปแบบสมัยญี่ปุ่น นี่คือสิ่งที่การทำ **set custom number format** ทำให้สำเร็จ

ด้านล่างเป็นไฟล์ซอร์สเต็มรูปแบบ คัดลอก‑วางลงใน `src/main/java/SetCustomNumberFormatDemo.java` ได้เลย

```java
// File: SetCustomNumberFormatDemo.java
import com.aspose.cells.*;

public class SetCustomNumberFormatDemo {
    public static void main(String[] args) throws Exception {
        // -------------------------------------------------
        // 1️⃣ Create Excel workbook Java – a fresh workbook
        // -------------------------------------------------
        Workbook workbook = new Workbook();               // in‑memory workbook, no file yet

        // -------------------------------------------------
        // 2️⃣ Access the first worksheet
        // -------------------------------------------------
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // -------------------------------------------------
        // 3️⃣ Retrieve cell A1 where we’ll store the date string
        // -------------------------------------------------
        Cell cellA1 = worksheet.getCells().get("A1");

        // -------------------------------------------------
        // 4️⃣ Insert a Japanese era date string (Reiwa 2‑04‑01)
        // -------------------------------------------------
        // Note: Aspose.Cells will treat this as a text value until we recalc.
        cellA1.putValue("R02-04-01");

        // -------------------------------------------------
        // 5️⃣ Apply the custom number format (our primary goal)
        // -------------------------------------------------
        // [$-ja-JP] tells Excel to use the Japanese locale.
        // ggge年m月d日 renders as "令和2年4月1日".
        cellA1.setNumberFormat("[$-ja-JP]ggge年m月d日");

        // -------------------------------------------------
        // 6️⃣ Calculate workbook formulas – crucial step!
        // -------------------------------------------------
        // Without this, the cell remains a plain string and the
        // DateTime conversion below will fail.
        workbook.calculateFormula();

        // -------------------------------------------------
        // 7️⃣ Get DateTime from cell – now the value is a true date
        // -------------------------------------------------
        // The getDateTime() method returns a java.util.Calendar instance.
        java.util.Calendar dt = cellA1.getDateTime();

        // -------------------------------------------------
        // 8️⃣ Output datetime value – see the result in console
        // -------------------------------------------------
        System.out.println("Converted DateTime: " + dt.getTime()); // → Tue Apr 01 00:00:00 UTC 2020
    }
}
```

### ทำไมวิธีนี้ถึงได้ผล

- **`setNumberFormat`** บอก Excel ว่าให้ *แสดง* ค่าตัวเลขพื้นฐานอย่างไร สตริงรูปแบบ `[$-ja-JP]ggge年m月d日` คือกุญแจ; `ggg` เลือกชื่อสมัย, `e` ปีภายในสมัย, ตามด้วยเดือนและวันเป็นตัวอักษร
- **`calculateFormula`** บังคับให้ Aspose.Cells แปลข้อความ “R02-04-01” เป็นวันที่ตามปฏิทินญี่ปุ่น หากข้ามขั้นตอนนี้ เซลล์จะเหลือเป็นข้อความธรรมดาและ `getDateTime()` จะโยนข้อยกเว้น
- **`getDateTime`** ดึงอ็อบเจ็กต์ `java.util.Calendar` ที่เป็นค่าจริงออกมา ซึ่งคุณสามารถจัดการ, ฟอร์แมต, หรือเก็บไว้ที่อื่นได้

---

## ขั้นตอนที่ 2: Create Excel Workbook Java – รายละเอียดลึก

เมื่อคุณ **create Excel workbook Java** คุณไม่ได้แค่จองหน่วยความจำเท่านั้น แต่ยังตั้งค่า style เริ่มต้น, worksheet เริ่มต้น, และวัฒนธรรมเริ่มต้น (โดยทั่วไปคือโลคัลของระบบ) หากต้องการโลคัลเริ่มต้นที่ต่างออกไป คุณสามารถส่งอ็อบเจ็กต์ `LoadOptions` เข้าไปได้:

```java
LoadOptions opts = new LoadOptions(LoadFormat.XLSX);
opts.setLocale(new java.util.Locale("ja", "JP"));
Workbook workbook = new Workbook(opts);
```

สำหรับสถานการณ์ส่วนใหญ่ ตัวสร้างแบบง่ายก็เพียงพอ แต่การรู้ทางเลือกนี้ก็เป็นประโยชน์—โดยเฉพาะเมื่อคุณต้องจัดการหลายโลคัลในแอปเดียว

*เคล็ดลับ:* ควรเก็บ workbook ไว้ในหน่วยความจำจนกว่าจะทำการฟอร์แมตเสร็จแล้ว การเขียนลงดิสก์หลังการเปลี่ยนแปลงแต่ละครั้งจะทำให้เกิด I/O ที่ไม่จำเป็น

---

## ขั้นตอนที่ 3: Get DateTime from Cell – จัดการผลลัพธ์

บรรทัด `java.util.Calendar dt = cellA1.getDateTime();` ทำงานหนักอยู่เบื้องหลัง Aspose.Cells แปลงหมายเลขซีเรียลภายใน (จำนวนวันตั้งแต่ 1899‑12‑31) ให้เป็น `Calendar` การแปลงนี้เคารพโลคัลของ workbook ดังนั้นคุณจะได้วันที่ Gregorian ที่ถูกต้องแม้การแสดงผลจะใช้สมัยญี่ปุ่น

หากต้องการ `java.time.LocalDate` (API ใหม่) ให้แปลงดังนี้:

```java
java.time.LocalDate localDate = dt.toInstant()
        .atZone(java.time.ZoneId.systemDefault())
        .toLocalDate();
System.out.println("LocalDate: " + localDate); // 2020-04-01
```

วิธีนี้ทำให้คุณตอบสนองความต้องการ **output datetime value** ได้อย่างทันสมัย

---

## ขั้นตอนที่ 4: Calculate Workbook Formulas – เมื่อจำเป็น

คุณอาจสงสัย: *“ฉันต้องเรียก `calculateFormula()` จริงหรือไม่?”* คำตอบคือ **ต้อง** เว้นแต่คุณจะใส่ค่า `Date` ของ Java ลงในเซลล์ตั้งแต่แรก เมื่อคุณ **set custom number format** บนสตริงข้อความ Excel (และ Aspose.Cells) จะถือว่าเป็นการแสดงสูตรที่ต้องประเมิน หากไม่ทำการคำนวณใหม่ `getDateTime()` จะคืนค่าเริ่มต้น `1900‑01‑00` หรือโยน `CellValueException`

หาก workbook ของคุณมีสูตรซับซ้อนที่อ้างอิงเซลล์ที่เพิ่งฟอร์แมตใหม่ ให้เรียก `calculateFormula()` **หนึ่งครั้ง** หลังจากทำการเปลี่ยนแปลงทั้งหมด การเรียกหลายครั้งจะทำให้ประสิทธิภาพลดลง

---

## ขั้นตอนที่ 5: Output DateTime Value – ตรวจสอบผลลัพธ์

การรัน demo จะพิมพ์ข้อความคล้ายดังนี้:

```
Converted DateTime: Tue Apr 01 00:00:00 UTC 2020
```

บรรทัดนี้ยืนยันสามประการ:

1. **set custom number format** ถูกนำไปใช้ (คุณสามารถเปิดไฟล์ `.xlsx` ที่สร้างขึ้นใน Excel เพื่อดู “令和2年4月1日”)
2. ขั้นตอน **calculate workbook formulas** สำเร็จ ทำให้สตริงสมัยแปลงเป็นวันที่จริง
3. การเรียก **get datetime from cell** คืนค่า `Calendar` ที่ถูกต้อง ซึ่งเราจึง **output datetime value** ไปที่คอนโซล

หากคุณเปิด workbook ด้วยโปรแกรมสเปรดชีต คุณจะเห็นข้อความที่ฟอร์แมตแล้ว แต่ค่าที่อยู่ภายในเซลล์ยังคงเป็นเลขซีเรียล `43831` (ตัวแทนของ 2020‑04‑01 ใน Excel) ความเป็นสองเท่านี้คือสิ่งที่ทำให้ Excel มีพลัง

---

## ข้อผิดพลาดทั่วไป & กรณีขอบ

| Issue | Why It Happens | Fix |
|-------|----------------|-----|
| `cellA1.getDateTime()` throws `CellValueException` | เซลล์ยังเป็นสตริงเพราะข้าม `calculateFormula()` | ต้องเรียก `workbook.calculateFormula()` หลังจากตั้งค่าวันที่แบบข้อความที่ต้องแปลง |
| Japanese era not displayed correctly | โค้ดโลคัลหายหรือไม่ถูกต้อง | ใช้ `[$-ja-JP]` ในสตริงรูปแบบ หรือกำหนดโลคัล workbook ผ่าน `LoadOptions` |
| Format shows “#VALUE!” in Excel | สตริงรูปแบบผิดรูป | ตรวจสอบวงเล็บและอักขระ; รูปแบบ `ggge年m月d日` จำเป็นสำหรับปีสมัย |
| Time component appears (e.g., “00:00:00”) | สตริงต้นทางมีเวลา หรือสไตล์เซลล์เพิ่มเวลา | ตัดส่วนเวลาออกจากสตริงต้นทางหรือปรับรูปแบบเป็น `ggge年m月d日;@` |

---

## ตัวอย่างทำงานเต็มรูปแบบ – คลิกเดียว

หากคุณต้องการไฟล์เดียวโดยไม่มีคอมเมนต์เพิ่มเติม นี่คือเวอร์ชันที่เหลือน้อยที่สุด:



## คุณควรเรียนรู้อะไรต่อไป?

บทเรียนต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งรวมโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายขั้นตอน‑ขั้นตอน เพื่อช่วยคุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการทำงานอื่น ๆ ในโปรเจคของคุณ

- [Create an Excel Workbook using Aspose.Cells in Java: A Step-by-Step Guide](/cells/english/java/getting-started/create-excel-workbook-aspose-cells-java/)
- [Mastering Data Presentation in Excel: Number and Custom Date Formatting with Aspose.Cells for Java](/cells/english/java/formatting/aspose-cells-java-data-formatting-excel/)
- [How to Create & Format Excel Cells Using Aspose.Cells for Java: A Step-by-Step Guide](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}