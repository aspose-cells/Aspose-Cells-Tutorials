---
category: general
date: 2026-07-20
description: ใช้รูปแบบตัวเลขใน Excel ด้วย Java และ Aspose.Cells เรียนรู้วิธีการใช้สไตล์สกุลเงินใน
  Excel สร้าง workbook Excel ด้วย Java และนำเข้าตารางข้อมูลไปยัง Excel อย่างมีประสิทธิภาพ.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- apply number format excel
- apply currency style excel
- create excel workbook java
- import datatable to excel
language: th
lastmod: 2026-07-20
og_description: ใช้รูปแบบตัวเลขใน Excel ด้วย Java. คู่มือนี้จะแสดงวิธีการใช้สไตล์สกุลเงินใน
  Excel, สร้างไฟล์ Excel ด้วย Java, และนำเข้าตารางข้อมูลไปยัง Excel อย่างเป็นขั้นตอน.
og_image_alt: Screenshot of an Excel workbook where apply number format excel has
  been applied to a currency column
og_title: ใช้รูปแบบตัวเลขใน Excel ด้วย Java – คู่มือ Aspose.Cells อย่างเต็มรูปแบบ
schemas:
- author: Aspose
  dateModified: '2026-07-20'
  description: Apply number format excel using Java and Aspose.Cells. Learn how to
    apply currency style excel, create excel workbook java, and import datatable to
    excel efficiently.
  headline: Apply Number Format Excel in Java – Complete Aspose.Cells Guide
  type: TechArticle
- questions:
  - answer: Absolutely. Open the workbook with `new Workbook("Existing.xlsx")`, fetch
      the target worksheet, and follow steps 3‑5 to apply the style array to new data.
    question: Can I apply the number format to an existing workbook?
  - answer: Use a different built‑in number index (`14` for short date, `22` for long
      date) or a custom format like `yyyy‑mm‑dd`. The workflow stays the same.
    question: What if I need to format dates instead of currency?
  - answer: 'Yes. Just change the file extension in `workbook.save("MyFile.xls")`.
      Aspose will automatically switch to the binary format. ## Wrap‑Up – What We
      Achieved We have **applied number format excel** to a column of monetary values,
      demonstrated how to **apply currency style excel**, shown the simplest wa'
    question: Does this work with older Excel versions (.xls)?
  type: FAQPage
tags:
- Aspose.Cells
- Java
- Excel Automation
title: ใช้รูปแบบตัวเลขใน Excel ด้วย Java – คู่มือ Aspose.Cells ฉบับสมบูรณ์
url: /th/java/formatting/apply-number-format-excel-in-java-complete-aspose-cells-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# การใช้รูปแบบตัวเลขใน Excel ด้วย Java – คู่มือ Aspose.Cells ฉบับสมบูรณ์

เคยสงสัยไหมว่าจะแปลง **apply number format excel** โดยตรงจากโค้ด Java ได้อย่างไร? บางทีคุณอาจกำลังสร้างรายงานการเงินหรือจำเป็นต้องมีวิธีรวดเร็วในการจัดรูปแบบคอลัมน์ของจำนวนเงินโดยไม่ต้องเปิด Excel ด้วยตนเอง. ข่าวดีคือ? ด้วย Aspose.Cells คุณสามารถทำได้ในไม่กี่บรรทัด และคุณยังจะได้เรียนรู้วิธี **apply currency style excel**, **create excel workbook java**, และ **import datatable to excel** ทั้งหมดในขั้นตอนเดียวที่เป็นระเบียบ.

ในบทเรียนนี้เราจะเดินผ่านตัวอย่างจากโลกจริง: รายการจำนวนเงินที่เก็บไว้ใน Java `List<Map<String,Object>>` จะถูกนำเข้าไปยังเวิร์กบุ๊กใหม่ คอลัมน์แรกจะได้รับรูปแบบสกุลเงินที่มีมาในตัว และไฟล์จะถูกบันทึกพร้อมสำหรับการแจกจ่าย. พร้อมที่จะดูว่ามันง่ายแค่ไหนหรือยัง? ไปดูกันเลย.

## ข้อกำหนดเบื้องต้น – สิ่งที่คุณต้องมี

- **Java Development Kit (JDK) 8+** – โค้ดทำงานบน JDK เวอร์ชันล่าสุดใดก็ได้.
- **Aspose.Cells for Java** library (the Maven artifact `com.aspose:aspose-cells`) – นี่คือเอนจินที่ทำให้เราสามารถจัดการไฟล์ Excel ได้โดยไม่ต้องติดตั้ง Office.
- **favorite IDE** (IntelliJ IDEA, Eclipse, VS Code…) – ตัวแก้ไขใดก็ได้ก็ใช้ได้ แต่ IDE จะช่วยเร่งการดีบัก.
- ความคุ้นเคยพื้นฐานกับ **Java collections** – เราจะใช้ `List` ของ `Map` เพื่อจำลอง DataTable.

แค่นั้นแหละ. ไม่มีบริการภายนอก, ไม่ต้องติดตั้ง Excel, เพียงแค่ Java ธรรมดา.

## ขั้นตอนที่ 1: สร้าง Excel Workbook Java – การสร้างอ็อบเจกต์ Workbook

สิ่งแรกที่เราต้องการคืออ็อบเจกต์ workbook. คิดว่าเป็นผ้าใบเปล่าที่ทุกอย่างจะอยู่บนมัน.

```java
// Step 1: Create a new workbook instance
Workbook workbook = new Workbook(); // creates an in‑memory Excel file
```

ทำไมต้องสร้าง workbook ก่อน? Aspose.Cells ทำงานทั้งหมดในหน่วยความจำ ดังนั้นคุณสามารถเพิ่มชีต, สไตล์, และข้อมูลได้ก่อนที่จะเขียนลงดิสก์ วิธีนี้เร็วและทำให้โค้ดของคุณทดสอบได้ง่าย.

## ขั้นตอนที่ 2: เตรียมข้อมูล – นำเข้า Datatable ไปยัง Excel ด้วย List of Maps

ในแอปพลิเคชันองค์กรหลายแห่ง ข้อมูลมาจากฐานข้อมูลในรูปแบบตาราง. ที่นี่เราจำลองด้วย `List<Map<String,Object>>`. แต่ละ map แทนแถวหนึ่ง และคีย์ `"Amount"` จะเชื่อมกับค่าตัวเลข.

```java
// Step 2: Build a DataTable‑like structure (list of maps)
List<Map<String, Object>> dataRows = new ArrayList<>();

// Row 1
dataRows.add(new HashMap<>() {{
    put("Amount", 1234.56);
}});
// Row 2
dataRows.add(new HashMap<>() {{
    put("Amount", 7890.12);
}});
```

คุณอาจถามว่า “ทำไมไม่ใช้ `ResultSet` หรือ POJO?” เมธอด `importDataTable` ยอมรับคอลเลกชันใด ๆ ที่ทำงานเหมือน DataTable และ List of Maps เป็นวิธีที่ตรงไปตรงมาที่สุดในการสาธิตแนวคิดโดยไม่ต้องดึงไลบรารีเพิ่มเติม.

## ขั้นตอนที่ 3: กำหนดรูปแบบตัวเลข – Apply Currency Style Excel

ตอนนี้มาถึงหัวใจของบทเรียน: **apply number format excel**. Aspose.Cells มาพร้อมกับรูปแบบตัวเลขในตัว; รูปแบบสกุลเงินอยู่ที่ดัชนี 5. เราเอาสไตล์เริ่มต้นจากเวิร์กชีตแรก, ปรับรูปแบบตัวเลข, และเก็บไว้ใช้ต่อไป.

```java
// Step 3: Get the default style and set a currency number format
Style currencyStyle = workbook.getWorksheets().get(0).getCells().getDefaultStyle();
currencyStyle.setNumber(5); // 5 = built‑in currency format ($#,##0.00)
```

ทำไมต้องใช้สไตล์เริ่มต้นเป็นฐาน? เพราะมันมีฟอนต์เริ่มต้นของเวิร์กบุ๊ก, การจัดแนว, และการตั้งค่าอื่น ๆ อยู่แล้ว, ดังนั้นคุณแค่เปลี่ยนสิ่งที่สำคัญ – ในกรณีนี้คือรูปแบบตัวเลข. หากคุณต้องการรูปแบบกำหนดเอง (เช่น “€#,##0.00”), คุณสามารถเรียก `currencyStyle.setCustom("#,##0.00 €")` แทนได้.

## ขั้นตอนที่ 4: ตั้งค่า Import Options – เชื่อมโยงอาร์เรย์สไตล์

Aspose.Cells อนุญาตให้คุณส่งอาร์เรย์ของอ็อบเจกต์ `Style` ที่สอดคล้องกับคอลัมน์ที่นำเข้า. เนื่องจากข้อมูลของเรามีเพียงคอลัมน์เดียว, เราจึงส่งอาร์เรย์ที่มีหนึ่งองค์ประกอบซึ่งบรรจุสไตล์สกุลเงิน.

```java
// Step 4: Configure import options with the style array
ImportTableOptions importOptions = new ImportTableOptions();
importOptions.setStyleArray(new Style[] { currencyStyle });
```

หากคุณต้องการจัดรูปแบบหลายคอลัมน์แตกต่างกัน, เพียงขยายอาร์เรย์: `new Style[] { styleForCol1, styleForCol2, … }`. ลำดับของสไตล์จะตรงกับลำดับของคอลัมน์ในข้อมูลต้นฉบับ.

## ขั้นตอนที่ 5: นำเข้าข้อมูล – นำ Datatable เข้าสู่ Worksheet

เมื่อเวิร์กบุ๊กพร้อม, ข้อมูลเตรียมพร้อม, และสไตล์กำหนดแล้ว, เราในที่สุดก็ **import datatable to excel**. เราเริ่มที่เซลล์ `A1`, รวมหัวคอลัมน์ (`true`), และส่งต่อ `ImportTableOptions`.

```java
// Step 5: Perform the import
Worksheet worksheet = workbook.getWorksheets().get(0);
worksheet.getCells().importDataTable(dataRows, true, "A1", importOptions);
```

สังเกตแฟล็ก `true` — Aspose.Cells จะสร้างแถวหัวอัตโนมัติตามคีย์ของ map (`"Amount"`). หากตั้งเป็น `false`, หัวจะถูกละเว้น, ทำให้คุณควบคุมการจัดวางขั้นสุดท้ายได้มากขึ้น.

## ขั้นตอนที่ 6: บันทึกไฟล์ – Create Excel Workbook Java บนดิสก์

ส่วนสุดท้ายของปริศนาคือการบันทึกเวิร์กบุ๊กที่อยู่ในหน่วยความจำลงไฟล์จริง. คุณสามารถเลือกฟอร์แมตใดก็ได้ที่ Aspose รองรับ (`.xlsx`, `.xls`, `.csv`, …). ที่นี่เราบันทึกเป็นไฟล์ XLSX.

```java
// Step 6: Save the workbook to disk
String outputPath = "DataTableWithCurrencyStyle.xlsx";
workbook.save(outputPath);
System.out.println("Workbook saved to " + outputPath);
```

หลังจากรันโปรแกรม, เปิดไฟล์ที่สร้างขึ้น. คุณจะเห็นคอลัมน์ `"Amount"` ถูกจัดรูปแบบด้วยสัญลักษณ์ดอลลาร์, มีสองตำแหน่งทศนิยม, และคั่นหลักพันอย่างเหมาะสม — พอดีกับที่คุณคาดหวังเมื่อ **apply number format excel** สำหรับค่าที่เป็นสกุลเงิน.

## ผลลัพธ์ที่คาดหวัง

| Amount |
|--------|
| $1,234.56 |
| $7,890.12 |

หัวคอลัมน์ “Amount” ปรากฏเป็นตัวหนา (สไตล์เริ่มต้น), และแต่ละเซลล์ด้านล่างแสดงรูปแบบสกุลเงินที่เราตั้งค่าไว้. ไม่ต้องทำการจัดรูปแบบด้วยมือใน Excel.

## เคล็ดลับมืออาชีพและข้อผิดพลาดทั่วไป

- **Reuse Styles Wisely** – สไตล์มีน้ำหนักเบา, แต่การสร้าง `Style` ใหม่สำหรับทุกเซลล์อาจทำให้ประสิทธิภาพลดลง. ควรใช้สไตล์เดียวกันซ้ำเมื่อใช้รูปแบบเดียวกันกับหลายเซลล์, เช่นที่เราใช้ `currencyStyle`.
- **Custom Formats** – หากภาษาของคุณใช้สัญลักษณ์สกุลเงินอื่น, ให้แทนที่ `currencyStyle.setNumber(5)` ด้วย `currencyStyle.setCustom("€#,##0.00")`. ทดสอบรูปแบบใน Excel เพื่อยืนยันว่ามันทำงานตามที่คาดหวัง.
- **Large Datasets** – สำหรับแถวหลายพัน, พิจารณาใช้ `importDataTable` พร้อมแฟล็ก `ImportTableOptions.setImportDataOnly(true)` เพื่อข้ามการสร้างหัวและเร่งความเร็วการนำเข้า.
- **Thread Safety** – อ็อบเจกต์ Aspose.Cells **ไม่** ปลอดภัยต่อการทำงานหลายเธรด. สร้าง `Workbook` แยกต่างหากต่อเธรดหากคุณกำลังสร้างรายงานแบบขนาน.

## คำถามที่พบบ่อย

**Q: สามารถนำรูปแบบตัวเลขไปใช้กับเวิร์กบุ๊กที่มีอยู่แล้วได้หรือไม่?**  
A: แน่นอน. เปิดเวิร์กบุ๊กด้วย `new Workbook("Existing.xlsx")`, ดึง worksheet ที่ต้องการ, แล้วทำตามขั้นตอน 3‑5 เพื่อใช้สไตล์อาร์เรย์กับข้อมูลใหม่.

**Q: ถ้าต้องการจัดรูปแบบวันที่แทนสกุลเงินจะทำอย่างไร?**  
A: ใช้ดัชนีตัวเลขในตัวอื่น (`14` สำหรับวันที่สั้น, `22` สำหรับวันที่ยาว) หรือรูปแบบกำหนดเองเช่น `yyyy‑mm‑dd`. กระบวนการทำงานยังคงเหมือนเดิม.

**Q: วิธีนี้ทำงานกับเวอร์ชัน Excel เก่า (.xls) หรือไม่?**  
A: ใช่. เพียงเปลี่ยนส่วนขยายไฟล์ใน `workbook.save("MyFile.xls")`. Aspose จะสลับไปใช้รูปแบบไบนารีโดยอัตโนมัติ.

## สรุป – สิ่งที่เราได้ทำ

เราได้ **apply number format excel** ให้กับคอลัมน์ของค่าการเงิน, สาธิตวิธี **apply currency style excel**, แสดงวิธีที่ง่ายที่สุดในการ **create excel workbook java**, และใช้ Aspose.Cells เพื่อ **import datatable to excel** โดยไม่ต้องสัมผัส UI. ทั้งหมดนี้ทำในโปรแกรมสั้น ๆ ที่เป็นอิสระซึ่งคุณสามารถคัดลอก, วาง, และรันได้.

ต่อไป? ลองขยายตัวอย่าง:

- เพิ่มคอลัมน์เพิ่มเติม (เช่น “Date”, “Description”) และกำหนดสไตล์ต่าง ๆ ให้แต่ละคอลัมน์.
- ส่งออกข้อมูลเดียวกันเป็น CSV และเปรียบเทียบว่ารูปแบบตัวเลขหายไปอย่างไร.
- ผสานโค้ดเข้ากับบริการ Spring Boot ที่ส่งคืนเวิร์กบุ๊กเป็นการตอบสนอง HTTP ที่ดาวน์โหลดได้.

ทดลองได้ตามสบาย, หากเจอปัญหาใด ๆ ฝากคอมเมนต์ด้านล่าง. Happy coding!

## คุณควรเรียนรู้อะไรต่อไป?

บทเรียนต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดซึ่งต่อยอดจากเทคนิคที่แสดงในคู่มือนี้. แต่ละแหล่งข้อมูลมีตัวอย่างโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายขั้นตอนเพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจวิธีการทำงานทางเลือกในโครงการของคุณ.

- [วิธีการใช้สไตล์กับเซลล์ Excel ด้วย Aspose.Cells for Java - คู่มือฉบับสมบูรณ์](/cells/english/java/formatting/apply-styles-excel-aspose-cells-java/)
- [รวมเซลล์และใช้สไตล์ใน Excel ด้วย Aspose.Cells for Java - คู่มือฉบับสมบูรณ์](/cells/english/java/formatting/merge-cells-apply-styles-aspose-cells-java/)
- [Aspose.Cells for Java&#58; วิธีสร้างและจัดรูปแบบ Excel Workbooks อย่างมีประสิทธิภาพ](/cells/english/java/getting-started/aspose-cells-java-workbook-creation-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}