---
category: general
date: 2026-09-08
description: วิธีคัดลอกช่วงใน Java ด้วย Aspose.Cells – เรียนรู้การคัดลอก Pivot Table,
  ทำสำเนา Pivot Table, และส่งออก Pivot Table พร้อมคงรูปแบบ.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy range
- copy pivot table
- duplicate pivot table
- export pivot table
- copy range with formatting
language: th
lastmod: 2026-09-08
og_description: วิธีคัดลอกช่วงใน Java ด้วย Aspose.Cells บทเรียนนี้จะแสดงวิธีคัดลอก
  Pivot Table, ทำสำเนา Pivot Table, และส่งออก Pivot Table พร้อมคงรูปแบบไว้.
og_image_alt: Screenshot of Java code copying a pivot table range in Aspose.Cells
og_title: วิธีคัดลอกช่วงใน Java – คู่มือ Aspose.Cells ฉบับสมบูรณ์
schemas:
- author: Aspose
  dateModified: '2026-09-08'
  description: How to copy range in Java using Aspose.Cells – learn to copy pivot
    table, duplicate pivot table, and export pivot table while preserving formatting.
  headline: How to copy range in Java with Aspose.Cells
  type: TechArticle
- description: How to copy range in Java using Aspose.Cells – learn to copy pivot
    table, duplicate pivot table, and export pivot table while preserving formatting.
  name: How to copy range in Java with Aspose.Cells
  steps:
  - name: Copy pivot table to an existing workbook
    text: 'If you need to **duplicate pivot table** inside a workbook that already
      has data, use the same `copyRange` call but point to a different destination
      address:'
  - name: Export pivot table only (without surrounding data)
    text: 'Sometimes you want just the pivot table, not the source data. Identify
      the pivot table’s display range via its `getPivotTable` method:'
  - name: Preserve conditional formatting
    text: 'Conditional formatting rules are part of the style collection. The `PasteType.ALL`
      flag already copies them, but you can be explicit:'
  - name: Edge cases and troubleshooting
    text: '| Situation | What to watch for | Recommended fix | |-----------|-------------------|-----------------|
      | Source and destination workbooks use different Excel versions | Some newer
      pivot features (e.g., data model) may not render correctly | Use the latest
      Aspose.Cells version and set `Workbook.setF'
  - name: Next steps
    text: '- Explore **copy range with formatting** for charts and images (use `PasteType.PICTURES`).
      - Automate batch processing: loop over multiple source files and consolidate
      their pivot tables into a summary workbook. - Combine this technique with Aspose.Slides
      to generate PowerPoint reports that embed th'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: วิธีคัดลอกช่วงใน Java ด้วย Aspose.Cells
url: /th/java/range-management/how-to-copy-range-in-java-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีคัดลอกช่วงใน Java ด้วย Aspose.Cells

หากคุณต้องการ **how to copy range** ใน Java, Aspose.Cells ทำให้ภารกิจนี้ง่ายขึ้น ไม่ว่าคุณจะย้ายบล็อกเซลล์ทั่วไปหรือพีโวท์เทเบิลที่เต็มรูปแบบ, ไลบรารีจะจัดการการคัดลอกโดยคงสูตร, สไตล์, และแคชพีโวท์ไว้ครบถ้วน ในคู่มือนี้คุณจะได้เรียนรู้การ **copy pivot table**, **duplicate pivot table**, และแม้กระทั่ง **export pivot table** ไปยังเวิร์กบุ๊กใหม่พร้อมการจัดรูปแบบเต็มรูปแบบ

บทเรียนนี้ครอบคลุมทุกอย่างตั้งแต่การตั้งค่าโปรเจกต์จนถึงขั้นตอนการตรวจสอบสุดท้าย, ดังนั้นคุณสามารถรันโค้ดได้ทันทีหลังจากอ่านเสร็จ ไม่จำเป็นต้องใช้เครื่องมือภายนอกใด ๆ นอกจาก Aspose.Cells for Java JAR

## ข้อกำหนดเบื้องต้น

- Java 17 (หรือ JDK ที่รองรับอื่น) ที่ติดตั้งและกำหนดค่าใน IDE ของคุณ
- Maven หรือ Gradle สำหรับการจัดการ dependencies (ตัวอย่างใช้ Maven)
- ไฟล์ Excel ต้นฉบับ (`source.xlsx`) ที่มีพีโวท์เทเบิลในช่วง `A1:H20`
- ความคุ้นเคยพื้นฐานกับการเขียนโปรแกรม Java

## ขั้นตอนที่ 1: เพิ่ม Aspose.Cells ไปยังโปรเจกต์ของคุณ

Aspose.Cells เป็นไลบรารีเชิงพาณิชย์, แต่มีเวอร์ชันประเมินผลฟรีให้ใช้ได้ เพิ่ม dependency ไปยัง `pom.xml` ของคุณ:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest version -->
</dependency>
```

> **เคล็ดลับ:** หากคุณต้องการใช้ Gradle, รายการที่เทียบเท่าคือ:
> ```gradle
> implementation 'com.aspose:aspose-cells:24.9'
> ```

การเพิ่ม JAR จะทำให้คุณเข้าถึงคลาส `Workbook`, `Worksheet`, `Range`, และ `CopyOptions` ที่ใช้ตลอดคู่มือนี้

## ขั้นตอนที่ 2: โหลดเวิร์กบุ๊กต้นฉบับและเลือกแผ่นงานแรก

ส่วนแรกของ **how to copy range** คือการเปิดเวิร์กบุ๊กที่มีข้อมูลที่คุณต้องการย้าย

```java
import com.aspose.cells.*;

public class CopyRangeDemo {
    public static void main(String[] args) throws Exception {
        // Load the source workbook
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
        // Select the first worksheet (index 0)
        Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);
```

> **ทำไมเรื่องนี้สำคัญ:** การเปิดเวิร์กบุ๊กจะสร้างการแสดงผลในหน่วยความจำที่ API สามารถจัดการได้โดยไม่ต้องแก้ไขไฟล์ต้นฉบับบนดิสก์

## ขั้นตอนที่ 3: กำหนดช่วงที่มีพีโวท์เทเบิล

พีโวท์เทเบิลอยู่ภายในบล็อกสี่เหลี่ยม คุณต้องระบุบล็อกนั้นเพื่อให้ Aspose.Cells รู้ว่าจะคัดลอกอะไร

```java
        // Define the range that holds the pivot table and its source data
        Range sourceRange = sourceSheet.getCells().createRange("A1:H20");
```

> **Note:** เมธอด `createRange` **ไม่ได้** คัดลอกอะไรเลยในขณะนี้; มันเพียงสร้างอ็อบเจกต์ `Range` ที่ชี้ไปยังเซลล์ที่คุณตั้งใจจะทำสำเนา

## ขั้นตอนที่ 4: สร้างเวิร์กบุ๊กใหม่และรับแผ่นงานแรกของมัน

ตอนนี้สร้างเวิร์กบุ๊กปลายทางที่ช่วงที่คัดลอกจะถูกวางไว้

```java
        // Create an empty workbook for the destination
        Workbook destWorkbook = new Workbook();
        // Get its first (and only) worksheet
        Worksheet destSheet = destWorkbook.getWorksheets().get(0);
```

> **Why a new workbook?** การใช้ไฟล์ใหม่จะรับประกันว่าไม่มีสไตล์หรือ named range ที่ซ่อนอยู่แทรกแซงการคัดลอก, ซึ่งสำคัญอย่างยิ่งเมื่อคุณ **export pivot table** ไปยังไฟล์แยกต่างหาก

## ขั้นตอนที่ 5: คัดลอกช่วง (รวมถึงพีโวท์เทเบิล) ไปยังแผ่นงานปลายทาง

นี่คือหัวใจของ **how to copy range with formatting**. อ็อบเจกต์ `CopyOptions` บอก Aspose.Cells ให้คงทุกอย่างไว้: ค่า, สูตร, สไตล์, และแคชพีโวท์

```java
        // Prepare copy options – preserve formatting and pivot cache
        CopyOptions copyOptions = new CopyOptions();
        copyOptions.setPasteType(PasteType.ALL); // copies everything
        copyOptions.setSkipBlanks(false);        // keep blank cells

        // Copy the defined range to cell A1 of the destination sheet
        destSheet.getCells().copyRange(sourceRange, "A1", copyOptions);
```

> **Copy pivot table:** เนื่องจากช่วงต้นทางรวมพีโวท์เทเบิล, API จะทำการคัดลอกแคชพีโวท์โดยอัตโนมัติ, ดังนั้นแผ่นงานใหม่จะมีพีโวท์เทเบิลที่ทำงานเต็มรูปแบบและทำงานเหมือนต้นฉบับ

## ขั้นตอนที่ 6: บันทึกเวิร์กบุ๊กปลายทาง

สุดท้าย, เขียนผลลัพธ์ลงดิสก์

```java
        // Save the destination workbook
        destWorkbook.save("YOUR_DIRECTORY/dest.xlsx");
    }
}
```

เมื่อคุณเปิด `dest.xlsx`, คุณจะเห็นสำเนาที่ตรงกับพีโวท์เทเบิลต้นฉบับ, พร้อมการจัดรูปแบบ, slicers, และฟิลด์คำนวณครบถ้วน

## ผลลัพธ์ที่คาดหวัง

- `dest.xlsx` มีแผ่นงานชื่อ **Sheet1**.
- เซลล์ `A1:H20` มีข้อมูลและพีโวท์เทเบิลเดียวกับต้นฉบับ.
- สไตล์ของเซลล์ทั้งหมด (ฟอนต์, สี, เส้นขอบ) ถูกเก็บไว้.
- พีโวท์เทเบิลทำงานแบบโต้ตอบเต็มรูปแบบ; การรีเฟรชจะแสดงข้อมูลพื้นฐานในช่วงที่คัดลอก

## วิธีคัดลอกช่วงพร้อมการจัดรูปแบบ – การเจาะลึก

ตัวอย่างก่อนหน้านี้แสดงสถานการณ์ที่ง่ายที่สุด, แต่คุณอาจเจอกรณีที่ต้องใช้วิธีการที่แตกต่างเล็กน้อย

### คัดลอกพีโวท์เทเบิลไปยังเวิร์กบุ๊กที่มีอยู่แล้ว

หากคุณต้องการ **duplicate pivot table** ภายในเวิร์กบุ๊กที่มีข้อมูลอยู่แล้ว, ใช้การเรียก `copyRange` เดียวกันแต่ชี้ไปยังที่อยู่ปลายทางที่ต่างกัน:

```java
// Assume destWorkbook already contains other sheets
Worksheet targetSheet = destWorkbook.getWorksheets().get(2);
targetSheet.getCells().copyRange(sourceRange, "B5", copyOptions);
```

### ส่งออกพีโวท์เทเบิลเท่านั้น (โดยไม่มีข้อมูลรอบข้าง)

บางครั้งคุณต้องการเพียงพีโวท์เทเบิล, ไม่ใช่ข้อมูลต้นทาง. ระบุช่วงการแสดงผลของพีโวท์เทเบิลผ่านเมธอด `getPivotTable`:

```java
PivotTable pt = sourceSheet.getPivotTables().get(0);
String ptArea = pt.getDisplayRange(); // e.g., "C5:G15"
Range pivotOnly = sourceSheet.getCells().createRange(ptArea);
destSheet.getCells().copyRange(pivotOnly, "A1", copyOptions);
```

### รักษาการจัดรูปแบบตามเงื่อนไข

กฎการจัดรูปแบบตามเงื่อนไขเป็นส่วนหนึ่งของคอลเลกชันสไตล์. ธง `PasteType.ALL` จะคัดลอกมันแล้ว, แต่คุณสามารถระบุให้ชัดเจนได้:

```java
copyOptions.setPasteType(PasteType.FORMATS);
copyOptions.setPasteType(PasteType.ALL); // overrides previous, ensures everything
```

### กรณีขอบและการแก้ไขปัญหา

| สถานการณ์ | สิ่งที่ควรระวัง | วิธีแก้แนะนำ |
|-----------|-------------------|-----------------|
| เวิร์กบุ๊กต้นทางและปลายทางใช้เวอร์ชัน Excel ที่แตกต่างกัน | คุณลักษณะพีโวท์ใหม่บางอย่าง (เช่น data model) อาจไม่แสดงผลอย่างถูกต้อง | ใช้เวอร์ชันล่าสุดของ Aspose.Cells และตั้งค่า `Workbook.setFileFormatType(FileFormatType.XLSX)` สำหรับทั้งสองเวิร์กบุ๊ก |
| พีโวท์เทเบิลขนาดใหญ่มาก (> 10 000 แถว) ทำให้เกิดความกดดันของหน่วยความจำ | เกิดข้อผิดพลาด out‑of‑memory ระหว่างการคัดลอก | เปิดใช้งาน `Workbook.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` ก่อนการโหลด |
| แผ่นงานปลายทางมี named range ที่มีชื่อเดียวกับต้นทางอยู่แล้ว | การชนชื่อทำให้ `CopyOptions` ล้มเหลว | เรียก `copyOptions.setIgnoreNameConflicts(true)` |

## ตัวอย่างเต็มที่สามารถรันได้

ด้านล่างเป็นโปรแกรมเต็มที่คุณสามารถคัดลอกและวางลงในคลาส Java. รวมการนำเข้า, การจัดการข้อผิดพลาด, และคอมเมนต์ทั้งหมด

```java
import com.aspose.cells.*;

public class CopyRangeDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the source workbook
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
        Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);

        // 2️⃣ Define the range that includes the pivot table
        Range sourceRange = sourceSheet.getCells().createRange("A1:H20");

        // 3️⃣ Create a new destination workbook
        Workbook destWorkbook = new Workbook();
        Worksheet destSheet = destWorkbook.getWorksheets().get(0);

        // 4️⃣ Configure copy options to keep everything (values, formulas, formatting, pivot cache)
        CopyOptions copyOptions = new CopyOptions();
        copyOptions.setPasteType(PasteType.ALL);
        copyOptions.setSkipBlanks(false);
        copyOptions.setIgnoreNameConflicts(true); // avoid name collisions

        // 5️⃣ Perform the copy
        destSheet.getCells().copyRange(sourceRange, "A1", copyOptions);

        // 6️⃣ Save the result
        destWorkbook.save("YOUR_DIRECTORY/dest.xlsx");
        System.out.println("Copy completed – dest.xlsx now contains the duplicated pivot table.");
    }
}
```

รันโปรแกรม, จากนั้นเปิด `dest.xlsx` เพื่อตรวจสอบว่าพีโวท์เทเบิลทำงานเหมือนต้นฉบับอย่างแม่นยำ

## สรุป

คุณตอนนี้รู้แล้วว่า **how to copy range** ใน Java ด้วย Aspose.Cells, รวมถึงวิธี **copy pivot table**, **duplicate pivot table**, และ **export pivot table** พร้อมคงการจัดรูปแบบทั้งหมด ไลบรารีช่วยแยกรายละเอียดระดับต่ำของโครงสร้าง XML ของ Excel, ทำให้คุณมุ่งเน้นที่ตรรกะธุรกิจได้เต็มที่

### ขั้นตอนต่อไป

- สำรวจ **copy range with formatting** สำหรับแผนภูมิและรูปภาพ (ใช้ `PasteType.PICTURES`).
- ทำการประมวลผลแบบแบตช์อัตโนมัติ: วนลูปหลายไฟล์ต้นฉบับและรวมพีโวท์เทเบิลของพวกมันเข้าในเวิร์กบุ๊กสรุป.
- ผสานเทคนิคนี้กับ Aspose.Slides เพื่อสร้างรายงาน PowerPoint ที่ฝังพีโวท์ที่คัดลอกไว้

## คุณควรเรียนรู้อะไรต่อไป?

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้. แต่ละแหล่งข้อมูลมีตัวอย่างโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายขั้นตอนเพื่อช่วยคุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการนำไปใช้ทางเลือกในโปรเจกต์ของคุณเอง.

- [วิธีอัปเดตแหล่งข้อมูลพีโวท์เทเบิลใน Excel ด้วย Aspose.Cells สำหรับ Java: คู่มือเชิงลึก](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [เพิ่มประสิทธิภาพการโหลดพีโวท์เทเบิลใน Java ด้วย Aspose.Cells – คู่มือเชิงลึก](/cells/english/java/data-analysis/optimize-pivot-table-loading-aspose-cells-java/)
- [วิธีคัดลอกพีโวท์เทเบิลใน C# – แปลง Excel เป็น PPTX, คัดลอกช่วง & สร้าง Textbox](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}