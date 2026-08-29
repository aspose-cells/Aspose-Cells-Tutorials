---
date: 2026-07-26
description: เรียนรู้วิธีคำนวณความแตกต่างของวันที่ใน Java ด้วยฟังก์ชันวันที่ของ Aspose.Cells
  Excel. รวมตัวอย่างการหาวันสุดท้ายของเดือน, TODAY, และ DATEDIF.
keywords:
- calculate date difference java
- end of month java
- add excel date formula
- implement excel date functions
- retrieve current date excel
lastmod: 2026-07-26
linktitle: คำนวณความแตกต่างของวันที่ใน Java – ฟังก์ชันวันที่ของ Excel
og_description: คำนวณความแตกต่างของวันที่ใน Java ด้วยฟังก์ชันวันที่ของ Aspose.Cells
  Excel. คู่มือนี้แสดงวิธีเพิ่มสูตรวันที่ของ Excel, ดึงวันที่ปัจจุบัน, และรับค่าวันสุดท้ายของเดือนอย่างมีประสิทธิภาพ.
og_image_alt: 'Guide: calculate date difference in Java with Aspose.Cells Excel functions'
og_title: คำนวณความแตกต่างของวันที่ใน Java – ฟังก์ชันวันที่ของ Excel
schemas:
- author: Aspose
  dateModified: '2026-07-26'
  description: Learn how to calculate date difference in Java using Aspose.Cells Excel
    date functions. Includes end of month, TODAY, and DATEDIF examples.
  headline: Calculate Date Difference in Java – Excel Date Functions
  type: TechArticle
- description: Learn how to calculate date difference in Java using Aspose.Cells Excel
    date functions. Includes end of month, TODAY, and DATEDIF examples.
  name: Calculate Date Difference in Java – Excel Date Functions
  steps:
  - name: '**Download and Install Aspose.Cells:** Visit [Aspose.Cells for Java](https://releases.aspose.com/cells/java/)
      and download the latest release.'
    text: '**Download and Install Aspose.Cells:** Visit [Aspose.Cells for Java](https://releases.aspose.com/cells/java/)
      and download the latest release.'
  - name: '**Add the Library to Your Project:** Include the JAR file in your build
      path or add the Maven dependency.'
    text: '**Add the Library to Your Project:** Include the JAR file in your build
      path or add the Maven dependency.'
  - name: '**License Configuration:** Place your license file (`Aspose.Cells.lic`)
      in the project resources and load it at runtime to unlock full features.'
    text: '**License Configuration:** Place your license file (`Aspose.Cells.lic`)
      in the project resources and load it at runtime to unlock full features.'
  - name: '**Download the library [here](https://releases.aspose.com/cells/java/).**'
    text: '**Download the library [here](https://releases.aspose.com/cells/java/).**'
  type: HowTo
- questions:
  - answer: Create a `Style` object, set its `Number` property to `"dd-MM-yyyy"`,
      and apply it to the target cell via `cell.setStyle(style)`. **`Style` defines
      formatting such as number format, font, and alignment for a cell.**
    question: How do I format a cell to display dates in `dd‑MM‑yyyy` format?
  - answer: Yes, you can retrieve the `Date` objects from two cells, convert them
      to `java.time.LocalDate`, and use `ChronoUnit.DAYS.between(start, end)` for
      precise control.
    question: Can I calculate date differences without using the DATEDIF formula?
  - answer: Absolutely. All built‑in Excel date functions, including DATEDIF and EOMONTH,
      correctly handle leap years according to the Gregorian calendar.
    question: Does Aspose.Cells support leap‑year calculations?
  - answer: Iterate through each `Worksheet` in the `Workbook`, set the required formulas,
      and call `calculateFormula()` once per workbook for optimal performance.
    question: Is it possible to batch‑process multiple worksheets for date calculations?
  - answer: All functions are available from **Aspose.Cells 23.9** onward; the latest
      release (as of 2026) adds performance optimizations for large datasets.
    question: What version of Aspose.Cells is required for these features?
  type: FAQPage
second_title: Aspose.Cells Java Excel Processing API
tags:
- excel date functions
- aspose cells
- java excel processing
- date calculations
- java tutorial
title: คำนวณความแตกต่างของวันที่ใน Java – ฟังก์ชันวันที่ของ Excel
url: /th/java/basic-excel-functions/excel-date-functions-tutorial/
weight: 19
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# บทแนะนำฟังก์ชันวันที่ใน Excel

ในบทแนะนำที่ครอบคลุมนี้, **calculate date difference java** คือจุดสนใจหลักของเรา เราจะอธิบายวิธีใช้ Aspose.Cells for Java เพื่อทำงานกับฟังก์ชันวันที่ของ Excel ตั้งแต่การสร้างวันที่จนถึงการดึงวันที่ปัจจุบัน, การคำนวณความแตกต่าง, และการหาวันสิ้นเดือน ไม่ว่าคุณจะกำลังปรับแต่งเครื่องมือรายงานหรือทำอัตโนมัติสเปรดชีต เทคนิคเหล่านี้จะช่วยประหยัดเวลาและลดข้อผิดพลาด มาเริ่มกันเลย!

## คำตอบเร็ว
- **ฉันจะคำนวณความแตกต่างของวันที่ใน Java อย่างไร?** ใช้ฟังก์ชัน DATEDIF ผ่าน Aspose.Cells และระบุหน่วย (วัน, เดือน, ปี).  
- **ฉันจะดึงวันที่ปัจจุบันใน Excel จาก Java อย่างไร?** เรียกใช้ฟังก์ชัน TODAY ผ่าน Aspose.Cells หรือกำหนดค่าเซลล์เป็น `new Date()`.  
- **เมธอดใดที่คืนค่าวันสุดท้ายของเดือน?** ใช้ฟังก์ชัน EOMONTH; Aspose.Cells จะประเมินโดยอัตโนมัติ.  
- **ฉันต้องมีไลเซนส์สำหรับ Aspose.Cells หรือไม่?** ใช่, ไลเซนส์ที่ถูกต้องจะลบลายน้ำการประเมินและเปิดใช้งานฟังก์ชันทั้งหมด.  
- **เวอร์ชัน Java ใดที่รองรับ?** Aspose.Cells ทำงานกับ Java 8 และรุ่นใหม่กว่า.

## ฟังก์ชันวันที่ของ Excel คืออะไร?
ฟังก์ชันวันที่ของ Excel เป็นสูตรในตัวที่สร้าง, ปรับเปลี่ยน, หรือประเมินวันที่ภายในแผ่นงาน พวกมันช่วยให้คุณทำการคำนวณเชิงคณิตศาสตร์, ดึงวันที่ปัจจุบัน, หรือคำนวณขอบเขตของเดือนโดยไม่ต้องทำการคำนวณด้วยตนเอง โดยใช้ฟังก์ชันเหล่านี้คุณสามารถเพิ่มหรือลบวัน, เดือน, หรือปี, กำหนดจำนวนวันระหว่างสองวันที่, และปรับอัตโนมัติสำหรับปีอธิกสุรทินและความยาวของเดือนที่แตกต่างกัน ทั้งหมดนี้ยังคงข้อมูลในรูปแบบที่ Excel เข้าใจและสามารถแสดงตามการตั้งค่าภูมิภาคได้.

## ทำไมต้องใช้ Aspose.Cells for Java เพื่อใช้งานฟังก์ชันวันที่ของ Excel?
Aspose.Cells รองรับ **50+** รูปแบบการนำเข้าและส่งออก, ประมวลผลสเปรดชีต **ได้ถึง 1 000 หน้า** โดยไม่ต้องโหลดไฟล์ทั้งหมดเข้าสู่หน่วยความจำ, และทำการคำนวณสูตรได้เร็ว **ถึง 3×** เมื่อเทียบกับ Excel ดั้งเดิมบนฮาร์ดแวร์เดียวกัน การเพิ่มประสิทธิภาพนี้สำคัญสำหรับสายงานข้อมูลขนาดใหญ่.

## ทำความเข้าใจฟังก์ชันวันที่ใน Excel

Excel มีชุดฟังก์ชันวันที่ที่หลากหลายซึ่งทำให้การคำนวณซับซ้อนง่ายขึ้น ด้านล่างเราจะเน้นฟังก์ชันที่พบบ่อยที่สุดและแสดงให้เห็นว่า Aspose.Cells ประเมินผลโดยอัตโนมัติอย่างไร

### ฟังก์ชัน DATE
ฟังก์ชัน `DATE` สร้างค่าที่เป็นวันที่จากส่วนปี, เดือน, และวัน.  
**คำตอบโดยตรง:** `=DATE(2023, 12, 31)` คืนค่าตัวเลขซีเรียลสำหรับ 31 ธันวาคม 2023 ซึ่ง Excel จะแสดงเป็นวันที่ ใน Java คุณสามารถตั้งสูตรของเซลล์เป็นสตริงนี้และ Aspose.Cells จะคำนวณวันที่ที่ถูกต้องเมื่อบันทึกหรือคำนวณใหม่เวิร์กบุ๊ก.

### ฟังก์ชัน TODAY
ฟังก์ชัน `TODAY` คืนค่าวันที่ระบบปัจจุบันโดยไม่มีส่วนเวลา.  
**คำตอบโดยตรง:** `=TODAY()` จะสะท้อนวันที่เวิร์กบุ๊กถูกเปิดหรือคำนวณใหม่เสมอ ทำให้เหมาะสำหรับรายงานแบบไดนามิก.

### ฟังก์ชัน DATEDIF
ฟังก์ชัน `DATEDIF` คำนวณความแตกต่างระหว่างสองวันที่ในวัน, เดือน, หรือปี.  
**คำตอบโดยตรง:** `=DATEDIF(A1, B1, "d")` ให้จำนวนวันระหว่างวันที่ในเซลล์ A1 และ B1 นี่คือหัวใจของสถานการณ์ **calculate date difference java** ของเรา.

### ฟังก์ชัน EOMONTH
ฟังก์ชัน `EOMONTH` คืนค่าวันสุดท้ายของเดือนสำหรับวันที่เริ่มต้นที่กำหนด, โดยออฟเซ็ตจำนวนเดือนที่ระบุ.  
**คำตอบโดยตรง:** `=EOMONTH(A1, 0)` ให้วันสุดท้ายของเดือนที่มีวันที่ใน A1.

## การทำงานกับ Aspose.Cells for Java

ตอนนี้เราได้ครอบคลุมพื้นฐานแล้ว, มาดูวิธีตั้งค่า Aspose.Cells และใช้ฟังก์ชันเหล่านี้ด้วยโปรแกรม

### การตั้งค่า Aspose.Cells

ก่อนเขียนโค้ด, ตรวจสอบให้แน่ใจว่ากล่องเครื่องของคุณพร้อม:

1. **ดาวน์โหลดและติดตั้ง Aspose.Cells:** เยี่ยมชม [Aspose.Cells for Java](https://releases.aspose.com/cells/java/) และดาวน์โหลดเวอร์ชันล่าสุด.  
2. **เพิ่มไลบรารีลงในโปรเจคของคุณ:** ใส่ไฟล์ JAR ในเส้นทางการสร้างหรือเพิ่ม dependency ของ Maven.  
3. **การตั้งค่าไลเซนส์:** วางไฟล์ไลเซนส์ของคุณ (`Aspose.Cells.lic`) ในโฟลเดอร์ resources ของโปรเจคและโหลดใน runtime เพื่อเปิดฟีเจอร์เต็ม.  
4. **ดาวน์โหลดไลบรารี [ที่นี่](https://releases.aspose.com/cells/java/).**  

### วิธีคำนวณความแตกต่างของวันที่ใน Java ด้วย Aspose.Cells?

`Workbook` แทนไฟล์ Excel ทั้งไฟล์ในหน่วยความจำ ประกอบด้วยเวิร์กชีต, เซลล์, และสไตล์  
โหลดเวิร์กบุ๊กของคุณ, ตั้งสูตร DATEDIF, และประเมินผล  
**คำตอบโดยตรง:** สร้าง `Workbook`, กำหนดสูตร `=DATEDIF(A2,B2,"d")` ให้กับเซลล์, เรียก `calculateFormula()`, จากนั้นอ่านค่าตัวเลขที่ได้ ซึ่งให้จำนวนวันที่แม่นยำระหว่างสองวันที่ในหนึ่งการเรียก API

```java
// Create a new workbook
Workbook workbook = new Workbook();

// Access the first worksheet
Worksheet worksheet = workbook.getWorksheets().get(0);

// Set the date using the DATE function
worksheet.getCells().get("A1").putValue("=DATE(2023, 9, 7)");

// Get the calculated date value
String calculatedDate = worksheet.getCells().get("A1").getStringValue();

// Print the result
System.out.println("Calculated Date: " + calculatedDate);
```

### การใช้ฟังก์ชัน DATE กับ Aspose.Cells

**คำตอบโดยตรง:** ตั้งสูตรของเซลล์เป็น `=DATE(2024, 5, 15)`; หลังจากเรียก `calculateFormula()`, เซลล์จะแสดง `15‑May‑2024` ตาม locale ของเวิร์กบุ๊ก.

```java
// Create a new workbook
Workbook workbook = new Workbook();

// Access the first worksheet
Worksheet worksheet = workbook.getWorksheets().get(0);

// Use the TODAY function to get the current date
worksheet.getCells().get("A1").setFormula("=TODAY()");

// Get the current date value
String currentDate = worksheet.getCells().get("A1").getStringValue();

// Print the result
System.out.println("Current Date: " + currentDate);
```

### การทำงานกับฟังก์ชัน TODAY

**คำตอบโดยตรง:** กำหนด `=TODAY()` ให้กับเซลล์, เรียก `calculateFormula()`, และเซลล์จะมีวันที่ปัจจุบันทุกครั้งที่เวิร์กบุ๊กถูกเปิดหรือคำนวณใหม่.

```java
// Create a new workbook
Workbook workbook = new Workbook();

// Access the first worksheet
Worksheet worksheet = workbook.getWorksheets().get(0);

// Set two date values
worksheet.getCells().get("A1").putValue("2023-09-07");
worksheet.getCells().get("A2").putValue("2023-08-01");

// Calculate the difference using DATEDIF
worksheet.getCells().get("A3").setFormula("=DATEDIF(A1, A2, \"d\")");

// Get the difference in days
int daysDifference = worksheet.getCells().get("A3").getIntValue();

// Print the result
System.out.println("Days Difference: " + daysDifference);
```

### การคำนวณความแตกต่างของวันที่ด้วย DATEDIF

**คำตอบโดยตรง:** ใส่ `=DATEDIF(C2,D2,"m")` ในเซลล์เพื่อรับค่าความแตกต่างเป็นเดือน, หรือเปลี่ยน `"m"` เป็น `"y"` หรือ `"d"` สำหรับปีหรือวันตามลำดับ หลังจากคำนวณ, อ่านผลลัพธ์ตัวเลขผ่าน `cell.getIntValue()`.

```java
// Create a new workbook
Workbook workbook = new Workbook();

// Access the first worksheet
Worksheet worksheet = workbook.getWorksheets().get(0);

// Set a date value
worksheet.getCells().get("A1").putValue("2023-09-07");

// Calculate the end of the month using EOMONTH
worksheet.getCells().get("A2").setFormula("=EOMONTH(A1, 0)");

// Get the end-of-month date
String endOfMonth = worksheet.getCells().get("A2").getStringValue();

// Print the result
System.out.println("End of Month: " + endOfMonth);
```

### การหาวันสิ้นเดือน

**คำตอบโดยตรง:** ตั้งสูตรของเซลล์เป็น `=EOMONTH(E2,0)`; หลังจากประเมินสูตร, เซลล์จะมีวันสุดท้ายของเดือนของวันที่ใน E2.

## ข้อผิดพลาดทั่วไปและเคล็ดลับ

- **การคำนวณสูตรใหม่:** ควรเรียก `workbook.calculateFormula()` เสมอหลังจากตั้งหรือแก้ไขสูตร; มิฉะนั้นเซลล์จะคงค่าที่เก่า.  
- **ตัวเลขซีเรียลของวันที่:** Excel เก็บวันที่เป็นตัวเลขซีเรียล; เมื่ออ่านค่าให้ใช้ `cell.getDateValue()` เพื่อรับอ็อบเจ็กต์ `java.util.Date`.  
- **ปัญหา Locale:** การจัดรูปแบบวันที่เคารพ locale ของเวิร์กบุ๊ก ตั้งสไตล์โดยเจาะจงหากต้องการรูปแบบแสดงผลเฉพาะ.  
- **เวิร์กบุ๊กขนาดใหญ่:** สำหรับไฟล์ที่มี **หลายแสนแถว**, เปิดใช้งาน `WorkbookSettings.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` เพื่อรักษาการใช้หน่วยความจำให้ต่ำ.  
- `WorkbookSettings` กำหนดค่าการใช้หน่วยความจำและตัวเลือกการคำนวณสำหรับ `Workbook`.

## คำถามที่พบบ่อย

**ถาม: ฉันจะตั้งรูปแบบเซลล์ให้แสดงวันที่ในรูปแบบ `dd‑MM‑yyyy` อย่างไร?**  
A: สร้างอ็อบเจ็กต์ `Style`, ตั้งค่า property `Number` เป็น `"dd-MM-yyyy"`, แล้วนำไปใช้กับเซลล์เป้าหมายโดยใช้ `cell.setStyle(style)`.  
**`Style` กำหนดการจัดรูปแบบเช่นรูปแบบตัวเลข, ฟอนต์, และการจัดแนวสำหรับเซลล์.**

**ถาม: ฉันสามารถคำนวณความแตกต่างของวันที่โดยไม่ใช้สูตร DATEDIF ได้หรือไม่?**  
A: ได้, คุณสามารถดึงอ็อบเจ็กต์ `Date` จากสองเซลล์, แปลงเป็น `java.time.LocalDate`, แล้วใช้ `ChronoUnit.DAYS.between(start, end)` เพื่อควบคุมอย่างแม่นยำ.

**ถาม: Aspose.Cells รองรับการคำนวณปีอธิกสุรทินหรือไม่?**  
A: แน่นอน. ฟังก์ชันวันที่ใน Excel ทั้งหมดรวมถึง DATEDIF และ EOMONTH จัดการปีอธิกสุรทินได้อย่างถูกต้องตามปฏิทินเกรกอเรียน.

**ถาม: สามารถประมวลผลหลายเวิร์กชีตพร้อมกันสำหรับการคำนวณวันที่ได้หรือไม่?**  
A: วนลูปผ่านแต่ละ `Worksheet` ใน `Workbook`, ตั้งสูตรที่ต้องการ, แล้วเรียก `calculateFormula()` หนึ่งครั้งต่อเวิร์กบุ๊กเพื่อประสิทธิภาพสูงสุด.

**ถาม: ต้องใช้เวอร์ชันของ Aspose.Cells ใดสำหรับฟีเจอร์เหล่านี้?**  
A: ฟังก์ชันทั้งหมดพร้อมใช้งานตั้งแต่ **Aspose.Cells 23.9** เป็นต้นไป; รุ่นล่าสุด (จนถึงปี 2026) เพิ่มการปรับปรุงประสิทธิภาพสำหรับชุดข้อมูลขนาดใหญ่.

## สรุป

บทแนะนำนี้ได้ให้ข้อมูลเชิงลึกเกี่ยวกับฟังก์ชันวันที่ของ Excel และแสดงวิธี **calculate date difference java** ด้วย Aspose.Cells for Java คุณได้เรียนรู้วิธีตั้งค่าห้องสมุด, ใช้สูตร DATE, TODAY, DATEDIF, และ EOMONTH, รวมถึงการจัดการปัญหาทั่วไปเช่นการจัดรูปแบบ locale และการประมวลผลขนาดใหญ่ นำรูปแบบเหล่านี้ไปใช้ในแอปพลิเคชัน Java ของคุณเพื่อทำอัตโนมัติการรายงานและการวิเคราะห์ที่ขับเคลื่อนด้วยวันที่ด้วยความมั่นใจ

---

**Last Updated:** 2026-07-26  
**Tested With:** Aspose.Cells 24.11 for Java  
**Author:** Aspose  
**Related Resources:** API Reference [here](https://reference.aspose.com/cells/java/) | Download Free Trial [here](https://releases.aspose.com/cells/java/)

{{< blocks/products/products-backtop-button >}}

## บทแนะนำที่เกี่ยวข้อง

- [ทำความเข้าใจระบบวันที่ 1904 ใน Excel ด้วย Aspose.Cells Java เพื่อการดำเนินการเซลล์ที่มีประสิทธิภาพ](/cells/java/cell-operations/aspose-cells-java-configure-1904-date-system-excel/)
- [เชี่ยวชาญการนำเสนอข้อมูลใน Excel: การจัดรูปแบบตัวเลขและวันที่แบบกำหนดเองด้วย Aspose.Cells for Java](/cells/java/formatting/aspose-cells-java-data-formatting-excel/)
- [บทแนะนำสูตรและฟังก์ชัน Excel สำหรับ Aspose.Cells Java](/cells/java/formulas-functions/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

```java
// Create a date style
Style dateStyle = workbook.createStyle();
dateStyle.setCustom("dd-MM-yyyy");

// Apply the style to a cell
worksheet.getCells().get("A1").setStyle(dateStyle);
```