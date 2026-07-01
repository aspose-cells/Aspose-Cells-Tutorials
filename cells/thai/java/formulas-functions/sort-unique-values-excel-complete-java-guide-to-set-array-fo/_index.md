---
category: general
date: 2026-06-30
description: จัดเรียงค่าที่ไม่ซ้ำใน Excel ด้วย Java. เรียนรู้วิธีตั้งสูตร, คำนวณสูตรใหม่,
  และสร้างรายการที่ไม่ซ้ำใน Excel ด้วย Aspose.Cells.
draft: false
keywords:
- sort unique values excel
- how to set formula
- how to recalculate formulas
- generate unique list excel
- set array formula
language: th
og_description: จัดเรียงค่าที่ไม่ซ้ำใน Excel ด้วย Java คู่มือนี้แสดงวิธีตั้งสูตร,
  คำนวณสูตรใหม่, และสร้างรายการที่ไม่ซ้ำใน Excel ภายในไม่กี่นาที.
og_title: การจัดเรียงค่าที่ไม่ซ้ำใน Excel – บทเรียน Java สำหรับสูตรอาเรย์
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Sort unique values Excel using Java. Learn how to set formula, recalculate
    formulas, and generate unique list Excel with Aspose.Cells.
  headline: Sort Unique Values Excel – Complete Java Guide to Set Array Formulas
  type: TechArticle
- description: Sort unique values Excel using Java. Learn how to set formula, recalculate
    formulas, and generate unique list Excel with Aspose.Cells.
  name: Sort Unique Values Excel – Complete Java Guide to Set Array Formulas
  steps:
  - name: How It Works
    text: '- `UNIQUE(B1:B10)` scans the range and returns a vertical array of distinct
      strings. - `SORT(...)` takes that array and orders it in ascending order. -
      Wrapping the whole thing in `=` and calling `setFormulaArray` tells Aspose.Cells
      to treat the result as a **spilled array**, just like Excel would.'
  - name: Empty Cells in the Source Range
    text: 'If `B1:B10` contains blanks, `UNIQUE` will treat them as a distinct entry.
      To ignore blanks, wrap the range with `FILTER`:'
  - name: Non‑Contiguous Data
    text: 'When your data lives in multiple columns, you can join them with `CHOOSE`
      or `TEXTJOIN` before applying `UNIQUE`. For example:'
  - name: ' ## What Should You Learn Next?


      The following tutorials cover closely related topics that build on the techniques
      demonstrated in this guide. Each resource includes complete working code examples
      with step-by-step explanations to help you master additional API features and
      explore alternative implementation approaches in your own projects.

      - [How to Sort Excel Files by Cell Color Using Aspose.Cells Java&#58; A Comprehensive
      Guide](/cells/english/java/data-analysis/excel-file-sorting-aspose-cells-java/)
      - [Mastering Aspose.Cells Java&#58; How to Interrupt Formula Calculation in
      Excel Workbooks](/cells/english/java/calculation-engine/master-aspose-cells-java-interrupt-formula-calculation-workbook/)
      - [How to Create an Excel Data Validation List with Aspose.Cells for Java&#58;
      A Step-by-Step Guide](/cells/english/java/data-validation/excel-data-validation-aspose-cells-java/)

      {{< /blocks/products/pf/tutorial-page-section >}}'
    text: '{{< /blocks/products/pf/main-container >}} {{< /blocks/products/pf/main-wrap-class
      >}} {{< blocks/products/products-backtop-button >}}'
  type: HowTo
- questions:
  - answer: The `SORT` and `UNIQUE` functions are part of the Dynamic Array engine
      introduced in Excel 365. For legacy files you’d need to use classic array formulas
      like `{=INDEX(..., MATCH(0, COUNTIF($A$1:A1, $B$1:$B$10), 0))}`. Aspose.Cells
      can still evaluate them, but the syntax is more verbose.
    question: Does this work with older Excel versions (pre‑Office 365)?
  - answer: Absolutely. Just change the address in `cells.get("A1")`. The spilled
      array will always start at the cell you specify and expand right‑and‑down as
      needed.
    question: Can I set the array formula on a range other than `A1`?
  - answer: 'Replace the static range with a dynamic one, e.g., `B:B` or a named range.
      The formula becomes `=SORT(UNIQUE(B:B))`. Be cautious with whole‑column references
      on very large sheets; they can impact performance. --- ## Conclusion We’ve just
      covered **how to set formula** in Java to **sort unique values'
    question: What if my source data is larger than `B1:B10`?
  type: FAQPage
tags:
- Excel automation
- Java
- Aspose.Cells
title: จัดเรียงค่าที่ไม่ซ้ำใน Excel – คู่มือ Java ฉบับสมบูรณ์สำหรับตั้งสูตรอาเรย์
url: /th/java/formulas-functions/sort-unique-values-excel-complete-java-guide-to-set-array-fo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# เรียงลำดับค่าที่ไม่ซ้ำใน Excel – คู่มือ Java ฉบับสมบูรณ์สำหรับการตั้งสูตรแบบอาเรย์

เคยสงสัยไหมว่า **sort unique values Excel** ทำอย่างไรโดยไม่ต้องลากสูตรไปมา? คุณไม่ได้เป็นคนเดียว ในหลายสถานการณ์การรายงานคุณต้องการรายการที่สะอาดและเรียงตามตัวอักษรของรายการที่ไม่ซ้ำกัน และการทำด้วยตนเองเป็นเรื่องยุ่งยาก.  

ข่าวดีคืออะไร? ด้วยไม่กี่บรรทัดของโค้ด Java คุณสามารถ **set array formula** บนแผ่นงาน แล้ว **recalculate formulas** เพื่อให้ช่วงที่ spill เติมเต็มโดยอัตโนมัติ ในบทแนะนำนี้เราจะพาคุณผ่านทุกขั้นตอน—from การสร้าง workbook ถึงการสร้างรายการที่ไม่ซ้ำในสไตล์ Excel—เพื่อให้คุณสามารถฝังโซลูชันนี้ลงในแอปพลิเคชันของคุณได้โดยตรง.

> **Pro tip:** หากคุณใช้ Maven อยู่แล้ว การเพิ่ม Aspose.Cells เป็น dependency จะช่วยคุณหลีกเลี่ยงการจัดการไฟล์ JAR ด้วยตนเอง.

---

## ข้อกำหนดเบื้องต้น

| ข้อกำหนด | เหตุผลที่สำคัญ |
|-------------|----------------|
| Java 8 หรือใหม่กว่า | Aspose.Cells รองรับ Java 8+. |
| Maven (หรือ Gradle) | ทำให้การจัดการ dependency ง่ายขึ้น. |
| Aspose.Cells for Java | ให้ `Workbook`, `Worksheet` และ API สูตรที่เราจะใช้. |
| ความคุ้นเคยพื้นฐานกับฟังก์ชัน Excel | การเข้าใจ `SORT` และ `UNIQUE` ช่วยให้คุณปรับโค้ดได้. |

> *หากคุณยังไม่มี Aspose.Cells ให้เพิ่มสิ่งนี้ลงใน `pom.xml` ของคุณ*:  

```xml
<!-- Aspose.Cells for Java -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- latest as of June 2026 -->
</dependency>
```

---

## ขั้นตอนที่ 1: สร้าง Workbook ใหม่ (เริ่มต้นการตั้งสูตร)

ก่อนอื่นเราต้องการ workbook ว่าง คิดว่าเป็นผืนผ้าเปล่าที่เราจะ later **set array formula** ที่เซลล์ `A1`.

> *ทำไมต้องสร้าง workbook ใหม่?*  
> มันรับประกันสภาพแวดล้อมที่สะอาด ป้องกันสูตรที่ซ่อนอยู่ซึ่งอาจรบกวนข้อมูลทดสอบของเรา.

```java
import com.aspose.cells.*;

public class UniqueSortExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook
        Workbook workbook = new Workbook();

        // The rest of the steps follow...
```

---

## ขั้นตอนที่ 2: เติมข้อมูลตัวอย่าง (ไม่บังคับแต่เป็นประโยชน์)

เพื่อดูผลลัพธ์อย่างชัดเจน ให้เติมคอลัมน์ **B** ด้วยรายการที่ซ้ำกันบางรายการ.

```java
        // Step 2: Get the first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);
        Cells cells = worksheet.getCells();

        // Sample data in B1:B10
        String[] rawData = { "Apple", "Banana", "Apple", "Cherry", "Banana",
                             "Date", "Elderberry", "Fig", "Date", "Grape" };
        for (int i = 0; i < rawData.length; i++) {
            cells.get("B" + (i + 1)).putValue(rawData[i]);
        }
```

> *ทำไมต้องใช้คอลัมน์ B?*  
> สูตรที่เราจะเขียนอ้างอิง `B1:B10` ดังนั้นการเก็บข้อมูลที่นั่นจะสอดคล้องกับตัวอย่างคลาสสิกของ Excel.

---

## ขั้นตอนที่ 3: ตั้งสูตรอาเรย์ที่ **Sort Unique Values Excel**

ตอนนี้จุดมหัศจรรย์เกิดขึ้น เราเชื่อม `UNIQUE` (เพื่อลบรายการซ้ำ) กับ `SORT` (เพื่อเรียงตามตัวอักษร) ผลลัพธ์ที่ได้เป็น **array formula** ซึ่งหมายความว่าจะ spill ไปยังเซลล์ข้างเคียงโดยอัตโนมัติ.

```java
        // Step 3: Set an array formula that sorts the unique values from B1:B10
        // This is the core of “how to set formula” for our scenario.
        cells.get("A1").setFormulaArray("=SORT(UNIQUE(B1:B10))");
```

### วิธีการทำงาน

- `UNIQUE(B1:B10)` สแกนช่วงและคืนค่าอาเรย์แนวตั้งของสตริงที่แตกต่างกัน.  
- `SORT(...)` นำอาเรย์นั้นมาจัดเรียงในลำดับจากน้อยไปมาก.  
- การใส่ `=` รอบทั้งหมดและเรียก `setFormulaArray` บอก Aspose.Cells ให้ถือผลลัพธ์เป็น **spilled array**, เหมือน Excel.

> **Note:** หากคุณใช้ Excel เวอร์ชันเก่าที่ไม่มี `SORT` หรือ `UNIQUE` คุณสามารถย้อนกลับไปใช้ `SORT(UNIQUE(...))` กับฟังก์ชัน **LET** หรือใช้สูตรอาเรย์แบบเก่า (`=INDEX(...)`). บทแนะนำนี้เน้นวิธีแบบอาเรย์ไดนามิกสมัยใหม่เพราะเป็นวิธีที่สะอาดที่สุดในการ **generate unique list Excel** วันนี้.

---

## ขั้นตอนที่ 4: คำนวนสูตรใหม่เพื่อให้ช่วงที่ spill ถูกเติมเต็ม

หลังจากสูตรถูกใส่แล้ว workbook จะไม่ประเมินผลโดยอัตโนมัติ นี่คือจุดที่ขั้นตอน **how to recalculate formulas** เข้ามา.

```java
        // Step 4: Recalculate formulas so the spilled range is populated automatically
        workbook.calculateFormula();
```

การเรียก `calculateFormula()` จะบังคับให้ Aspose.Cells รันเอนจินของ Excel เติมค่าในเซลล์ `A1`, `A2`, … ด้วยค่าที่เรียงและไม่ซ้ำ.

> *ทำไมไม่พึ่งพาการประเมินแบบ lazy?*  
> ในบริบทฝั่งเซิร์ฟเวอร์คุณมักต้องการข้อมูลพร้อมส่งออก (CSV, PDF ฯลฯ) ทันทีหลังการคำนวน ดังนั้นการเรียกอย่างชัดเจนจึงรับประกันความสอดคล้อง.

---

## ขั้นตอนที่ 5: ตรวจสอบผลลัพธ์ (ดีบักแบบไม่บังคับ)

เป็นความคิดที่ดีเสมอที่จะพิมพ์ค่าที่ spill ไปยังคอนโซล—โดยเฉพาะเมื่อคุณกำลังเรียนรู้ API ใหม่.

```java
        // Step 5: Output the spilled range to the console
        System.out.println("Sorted unique list:");
        int row = 0;
        while (true) {
            String value = cells.get(row, 0).getStringValue(); // column A = index 0
            if (value == null || value.isEmpty()) break; // stop at first empty cell
            System.out.println("- " + value);
            row++;
        }

        // Optionally, save the workbook to inspect in Excel
        workbook.save("SortedUniqueValues.xlsx");
    }
}
```

การรันโปรแกรมจะแสดงผล:

```
Sorted unique list:
- Apple
- Banana
- Cherry
- Date
- Elderberry
- Fig
- Grape
```

เปิดไฟล์ `SortedUniqueValues.xlsx` แล้วคุณจะเห็นข้อมูลเดียวกันที่ spill จาก `A1` ลงล่าง.

---

## การจัดการกรณีขอบ

### เซลล์ว่างในช่วงต้นทาง

หาก `B1:B10` มีช่องว่าง `UNIQUE` จะถือว่ามันเป็นรายการที่แตกต่างกัน เพื่อไม่สนใจช่องว่าง ให้ใส่ช่วงนั้นใน `FILTER`:

```java
cells.get("A1").setFormulaArray("=SORT(UNIQUE(FILTER(B1:B10, B1:B10<>\"\")))");
```

### ข้อมูลที่ไม่ต่อเนื่อง

เมื่อข้อมูลของคุณอยู่หลายคอลัมน์ คุณสามารถรวมด้วย `CHOOSE` หรือ `TEXTJOIN` ก่อนใช้ `UNIQUE` ตัวอย่างเช่น:

```java
cells.get("A1").setFormulaArray(
    "=SORT(UNIQUE(CHOOSE({1,2}, B1:B10, C1:C10)))"
);
```

การปรับแต่งเหล่านี้แสดงให้เห็นถึงความยืดหยุ่นของ **how to set formula** สำหรับสถานการณ์ที่ซับซ้อนกว่า.

---

## ตัวอย่างทำงานเต็มรูปแบบ (รวมทุกขั้นตอน)

ด้านล่างเป็นโปรแกรม Java ที่สมบูรณ์และสามารถรันได้ คัดลอก‑วางลงใน IDE ของคุณ เพิ่ม dependency ของ Aspose.Cells แล้วกด *Run*.

```java
import com.aspose.cells.*;

public class UniqueSortExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook
        Workbook workbook = new Workbook();

        // Step 2: Get the first worksheet and fill sample data
        Worksheet worksheet = workbook.getWorksheets().get(0);
        Cells cells = worksheet.getCells();

        String[] rawData = { "Apple", "Banana", "Apple", "Cherry", "Banana",
                             "Date", "Elderberry", "Fig", "Date", "Grape" };
        for (int i = 0; i < rawData.length; i++) {
            cells.get("B" + (i + 1)).putValue(rawData[i]);
        }

        // Step 3: Set an array formula that sorts the unique values from B1:B10
        cells.get("A1").setFormulaArray("=SORT(UNIQUE(B1:B10))");

        // Step 4: Recalculate formulas so the spilled range is populated automatically
        workbook.calculateFormula();

        // Step 5: Output the spilled range to the console
        System.out.println("Sorted unique list:");
        int row = 0;
        while (true) {
            String value = cells.get(row, 0).getStringValue(); // column A = index 0
            if (value == null || value.isEmpty()) break;
            System.out.println("- " + value);
            row++;
        }

        // Save the workbook for visual verification
        workbook.save("SortedUniqueValues.xlsx");
    }
}
```

**ผลลัพธ์ที่คาดหวัง** (แสดงในคอนโซล) ตรงกับรายการที่เรียงและลบซ้ำที่เราพูดถึงก่อนหน้า การเปิดไฟล์ Excel ที่สร้างขึ้นจะแสดงค่าที่เดียวกันที่ spill จาก `A1` ลงล่าง.

---

## คำถามที่พบบ่อย

**Q: วิธีนี้ทำงานกับ Excel เวอร์ชันเก่า (ก่อน Office 365) หรือไม่?**  
A: ฟังก์ชัน `SORT` และ `UNIQUE` เป็นส่วนหนึ่งของเครื่องมือ Dynamic Array ที่แนะนำใน Excel 365 สำหรับไฟล์เก่า คุณต้องใช้สูตรอาเรย์คลาสสิกเช่น `{=INDEX(..., MATCH(0, COUNTIF($A$1:A1, $B$1:$B$10), 0))}` Aspose.Cells ยังคงสามารถประเมินได้ แต่ไวยากรณ์จะยาวกว่า.

**Q: ฉันสามารถตั้งสูตรอาเรย์ในช่วงอื่นที่ไม่ใช่ `A1` ได้หรือไม่?**  
A: แน่นอน เพียงเปลี่ยนที่อยู่ใน `cells.get("A1")` อาเรย์ที่ spill จะเริ่มจากเซลล์ที่คุณระบุและขยายไปทางขวาและลงตามต้องการ.

**Q: ถ้าข้อมูลต้นทางของฉันใหญ่กว่า `B1:B10` จะทำอย่างไร?**  
A: แทนที่ช่วงคงที่ด้วยช่วงไดนามิก เช่น `B:B` หรือชื่อช่วง สูตรจะเป็น `=SORT(UNIQUE(B:B))` ระวังการอ้างอิงทั้งคอลัมน์ในชีตขนาดใหญ่มาก เพราะอาจส่งผลต่อประสิทธิภาพ.

---

## สรุป

เราได้อธิบาย **how to set formula** ใน Java เพื่อ **sort unique values Excel**, วิธี **recalculate formulas**, และวิธี **generate unique list Excel** ด้วย API ที่ทรงพลังของ Aspose.Cells ขั้นตอนง่าย ๆ: สร้าง workbook, เติมข้อมูล, ใส่สูตรอาเรย์, เรียกการคำนวน, และตรวจสอบผลลัพธ์  

จากนี้คุณสามารถต่อยอด—เพิ่มการจัดรูปแบบตามเงื่อนไข, ส่งออกเป็น PDF, หรือรวมวิธีการนี้เข้าในเว็บเซอร์วิสที่ให้รายงานพร้อมใช้ แนวคิดหลักยังคงเหมือนเดิม: ให้ฟังก์ชันของ Excel ทำงานหนัก แล้วให้ Java ควบคุมกระบวนการ  

พร้อมที่จะยกระดับการอัตโนมัติ Excel ของคุณหรือยัง? ลองเปลี่ยน `SORT` เป็น `SORTBY` เพื่อเรียงตามคอลัมน์รอง หรือทดลองใช้ `FILTER` เพื่อตัดแถวที่ไม่ตรงกับกฎธุรกิจ ความเป็นไปได้แทบไม่มีที่สิ้นสุด.

###

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}