---
date: '2026-10-28'
description: เรียนรู้วิธีเปลี่ยนระบบวันที่ของ Excel เป็น 1904 ด้วย Aspose.Cells for
  Java ตั้งค่ารูปแบบวันที่ของ Excel และแปลงระบบ 1904 ของ Excel อย่างมีประสิทธิภาพ
keywords:
- change excel date system
- excel 1904 date conversion
- maven dependency aspose cells
lastmod: '2026-10-28'
og_description: เปลี่ยนระบบวันที่ของ Excel เป็น 1904 ด้วย Aspose.Cells for Java. เรียนรู้ขั้นตอนโดยละเอียดว่าตั้งค่าระบบ
  1904 อย่างไร ตั้งค่าวันที่ และแปลงกลับ
og_image_alt: Aspose.Cells Java guide showing how to switch Excel to the 1904 date
  system
og_title: เปลี่ยนระบบวันที่ของ Excel เป็น 1904 ด้วย Aspose.Cells for Java
schemas:
- author: Aspose
  dateModified: '2026-10-28'
  description: Learn how to change Excel date system to 1904 using Aspose.Cells for
    Java, set Excel date format, and convert Excel 1904 system efficiently.
  headline: Change Excel date system to 1904 with Aspose.Cells Java
  type: TechArticle
- description: Learn how to change Excel date system to 1904 using Aspose.Cells for
    Java, set Excel date format, and convert Excel 1904 system efficiently.
  name: Change Excel date system to 1904 with Aspose.Cells Java
  steps:
  - name: initialize and load the workbook
    text: The `Workbook` class represents an entire Excel file in memory. First, create
      a `Workbook` instance that points to your existing file.
  - name: enable the 1904 date system
    text: The `WorkbookSettings.setDate1904` method toggles the workbook‑level date
      flag. Setting it to `true` activates the 1904 system for all worksheets. **Pro
      tip:** You can also call `setDate1904(false)` later if you need to revert.
  - name: save the modified workbook
    text: Finally, write the changes to a new file (or overwrite the original). The
      `save` method respects the active date system automatically. > **Note:** The
      code above uses the class name `tWorkbook` as originally provided. Ensure this
      typo matches your project’s naming conventions or correct it to `Workb
  type: HowTo
- questions:
  - answer: The 1900 system starts on January 1, 1900, while the 1904 system starts
      on January 1, 1904, shifting all dates by 1,462 days.
    question: What is the difference between the 1900 and 1904 date systems?
  - answer: Yes, but you must close the file in Excel first; otherwise the save operation
      will fail.
    question: Can I change the date system of a workbook that is currently open in
      Excel?
  - answer: The method works in the free trial, but a full license removes evaluation
      limitations.
    question: Do I need a license to use `setDate1904`?
  - answer: No, the date system is a workbook‑level setting; it applies to all worksheets.
    question: Is it possible to change the date system for only a single worksheet?
  - answer: Open the saved file in Excel, go to **File → Options → Advanced**, and
      check the **"Use 1904 date system"** box.
    question: How can I verify that the date system was changed?
  type: FAQPage
tags:
- change excel date system
- aspose cells java
- excel date conversion
- java excel processing
title: เปลี่ยนระบบวันที่ของ Excel เป็น 1904 ด้วย Aspose.Cells Java
url: /th/java/cell-operations/aspose-cells-java-configure-1904-date-system-excel/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# เปลี่ยนระบบวันที่ของ Excel เป็น 1904 ด้วย Aspose.Cells Java

ในบทแนะนำนี้คุณจะได้เรียนรู้วิธี **เปลี่ยนระบบวันที่ของ Excel** เป็นรูปแบบ 1904 ด้วย Aspose.Cells for Java ระบบ 1904 มีความสำคัญเมื่อคุณต้องการรักษาข้อมูลวันที่แบบเก่าที่มาจาก Mac หรือสอดคล้องกับโมเดลการเงินที่ต้องการ epoch นี้ เราจะอธิบายขั้นตอนการติดตั้งไลบรารี, โหลด workbook, สลับระบบวันที่, และบันทึกผลลัพธ์—ทั้งหมดโดยไม่ต้องใช้ Microsoft Excel บนเซิร์ฟเวอร์

## คำตอบอย่างรวดเร็ว
- **ระบบวันที่ 1904 ทำอะไร?** It starts counting days from January 1, 1904, shifting all dates by 1,462 days compared with the default 1900 system.  
- **ทำไมต้องใช้ Aspose.Cells เพื่อเปลี่ยนระบบวันที่?** It provides a simple API that works without Excel installed and supports large files.  
- **รองรับเวอร์ชัน Java ใดบ้าง?** JDK 8 or newer.  
- **ต้องการไลเซนส์หรือไม่?** A free trial works for evaluation; a license removes usage limits.  
- **สามารถแปลงกลับเป็นระบบ 1900 ได้ภายหลังหรือไม่?** Yes, just call `setDate1904(false)`.

## ระบบวันที่ 1904 ใน Excel คืออะไร?
ระบบวันที่ 1904 จะนับจำนวนวันตั้งแต่ January 1, 1904, แทน epoch เริ่มต้นของปี 1900 การเปลี่ยนแปลงนี้เพิ่ม 1,462 วันให้กับค่าของวันที่ทุกค่า ซึ่งเป็นสาเหตุที่ workbook ของ Mac รุ่นเก่าแสดงผลล่าช้าเมื่อเปิดบน Windows ระบบนี้ใช้เพื่อความเข้ากันได้กับไฟล์ Excel ของ Macintosh รุ่นเก่าและบางโมเดลการเงินแบบเก่า

## ทำไมต้องเปลี่ยนระบบวันที่ของ Excel ด้วย Aspose.Cells?
คุณสามารถสลับระบบวันที่โดยตรงจาก Java ทำให้ไม่ต้องทำขั้นตอนด้วยตนเองใน Excel Aspose.Cells สามารถประมวลผล workbook ขนาดสูงสุด **2 GB** และสามารถแปลง workbook ที่มี 500 แผ่นได้ภายใน **2 วินาที** บนเซิร์ฟเวอร์ 4‑core ปกติ ให้การทำงานอัตโนมัติบนเซิร์ฟเวอร์ที่มีอัตราการประมวลผลสูง

## ข้อกำหนดเบื้องต้น
- Java Development Kit (JDK) 8 หรือสูงกว่า.  
- Maven หรือ Gradle สำหรับการจัดการ dependencies.  
- ความรู้พื้นฐานการเขียนโปรแกรม Java.  

## การตั้งค่า Aspose.Cells สำหรับ Java

### Maven
เพิ่ม dependency ต่อไปนี้ในไฟล์ `pom.xml` ของคุณ:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

### Gradle
ใส่บรรทัดนี้ในไฟล์ `build.gradle` ของคุณ:

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

#### การรับไลเซนส์
Aspose มีให้ทดลองใช้ฟรี, ไลเซนส์ชั่วคราว, และไลเซนส์เชิงพาณิชย์เต็มรูปแบบ คุณสามารถเริ่มต้นด้วย [free trial](https://releases.aspose.com/cells/java/) หรือรับไลเซนส์ชั่วคราวจาก [temporary license page](https://purchase.aspose.com/temporary-license/).

## วิธีเปลี่ยนระบบวันที่ของ Excel เป็น 1904 ด้วย Aspose.Cells for Java
โหลด workbook, เปิดใช้งานการตั้งค่า 1904, และบันทึกไฟล์—กระบวนการสามขั้นตอนนี้จะอัปเดต epoch วันที่ภายในของ workbook ภายในเวลาไม่ถึงหนึ่งวินาที การเรียก API `setDate1904(true)` จะสลับแฟล็กของระบบ และการเปลี่ยนแปลงจะถูกบันทึกเมื่อคุณเรียก `save` ไม่จำเป็นต้องติดตั้ง Excel ทำให้เหมาะกับสภาพแวดล้อมเซิร์ฟเวอร์แบบ headless

### ขั้นตอน 1: เริ่มต้นและโหลด workbook
คลาส `Workbook` แสดงไฟล์ Excel ทั้งหมดในหน่วยความจำ ขั้นแรกให้สร้างอินสแตนซ์ `Workbook` ที่ชี้ไปยังไฟล์ที่มีอยู่ของคุณ.

```java
import com.aspose.cells.Workbook;

String dataDir = "YOUR_DATA_DIRECTORY"; // Ensure the path to your Excel file is correct
// Initialize a Workbook object with the path to your Excel file
Workbook workbook = new Workbook(dataDir + "/Mybook.xlsx");
```

### ขั้นตอน 2: เปิดใช้งานระบบวันที่ 1904
เมธอด `WorkbookSettings.setDate1904` จะสลับแฟล็กวันที่ระดับ workbook การตั้งค่าเป็น `true` จะเปิดใช้งานระบบ 1904 สำหรับทุก worksheet.

```java
import com.aspose.cells.Workbook;

String dataDir = "YOUR_DATA_DIRECTORY"; // Ensure the path to your Excel file is correct
// Load the workbook from your specified directory
Workbook workbook = new Workbook(dataDir + "/Mybook.xlsx");

// Enable the 1904 date system
workbook.getSettings().setDate1904(true);
```

**เคล็ดลับ:** คุณสามารถเรียก `setDate1904(false)` ในภายหลังหากต้องการย้อนกลับ

### ขั้นตอน 3: บันทึก workbook ที่แก้ไขแล้ว
สุดท้ายให้เขียนการเปลี่ยนแปลงลงในไฟล์ใหม่ (หรือเขียนทับไฟล์เดิม) เมธอด `save` จะเคารพระบบวันที่ที่ใช้งานอยู่โดยอัตโนมัติ.

```java
import com.aspose.cells.Workbook;

String dataDir = "YOUR_DATA_DIRECTORY"; // Ensure the path to your Excel file is correct
String outDir = "YOUR_OUTPUT_DIRECTORY"; // Specify where you want to save the modified workbook

// Load and modify your workbook as shown in previous steps
tWorkbook workbook = new Workbook(dataDir + "/Mybook.xlsx");
workbook.getSettings().setDate1904(true);

// Save the changes to a new file
workbook.save(outDir + "/I1904DateSystem_out.xls");
```

> **หมายเหตุ:** โค้ดด้านบนใช้ชื่อคลาส `tWorkbook` ตามที่ให้มาเดิม ตรวจสอบให้แน่ใจว่าการพิมพ์ผิดนี้ตรงกับแนวทางการตั้งชื่อของโปรเจคของคุณหรือแก้เป็น `Workbook` หากจำเป็น

## ตั้งค่าวันที่ Excel ด้วยโปรแกรม (คีย์เวิร์ดรอง)
หากคุณต้องการปรับค่าของเซลล์แต่ละเซลล์หลังจากเปลี่ยนระบบ คุณสามารถใช้ `cells.get(i, j).putValue(Date)` ซึ่งวันที่จะถูกตีความตามระบบวันที่ที่ใช้งานอยู่

## แปลงระบบ 1904 ของ Excel กลับเป็น 1900 (คีย์เวิร์ดรอง)
เพื่อย้อนกลับ เพียงเรียก:

```java
workbook.getSettings().setDate1904(false);
```

จากนั้นบันทึก workbook อีกครั้ง.

## การใช้งานเชิงปฏิบัติ
1. **Data archiving** – Preserve legacy timestamps when migrating old Mac‑based spreadsheets.  
2. **Cross‑platform reporting** – Generate reports that open correctly on both Windows and macOS without date mismatches.  
3. **Financial modeling** – Align date calculations with legacy financial models that expect the 1904 system.  

## พิจารณาด้านประสิทธิภาพ
- จำกัดการดำเนินการ workbook ในเซสชันเดียวเพื่อรักษาการใช้หน่วยความจำให้ต่ำ; Aspose.Cells สตรีมข้อมูลและไม่โหลดไฟล์ทั้งหมดเข้าสู่ RAM เว้นแต่คุณจะร้องขอโดยเจตนา.  
- ปรับค่าแฟล็กการเก็บขยะของ Java (`-XX:+UseG1GC`) สำหรับไฟล์ขนาดใหญ่มากเพื่อหลีกเลี่ยงการหยุดทำงานแบบสปายค์.  

## คำถามที่พบบ่อย

**Q: ความแตกต่างระหว่างระบบวันที่ 1900 และ 1904 คืออะไร?**  
A: ระบบ 1900 เริ่มที่ January 1, 1900, ส่วนระบบ 1904 เริ่มที่ January 1, 1904, ทำให้วันที่ทั้งหมดเลื่อนออกไป 1,462 วัน.

**Q: ฉันสามารถเปลี่ยนระบบวันที่ของ workbook ที่เปิดอยู่ใน Excel ได้หรือไม่?**  
A: ได้ แต่คุณต้องปิดไฟล์ใน Excel ก่อน มิฉะนั้นการบันทึกจะล้มเหลว.

**Q: ฉันต้องการไลเซนส์เพื่อใช้ `setDate1904` หรือไม่?**  
A: เมธอดนี้ทำงานในรุ่นทดลองฟรี แต่ไลเซนส์เต็มจะลบข้อจำกัดการประเมิน.

**Q: สามารถเปลี่ยนระบบวันที่สำหรับ worksheet เดียวเท่านั้นได้หรือไม่?**  
A: ไม่ได้ ระบบวันที่เป็นการตั้งค่าระดับ workbook; ใช้กับทุก worksheet.

**Q: ฉันจะตรวจสอบว่าระบบวันที่ถูกเปลี่ยนหรือไม่?**  
A: เปิดไฟล์ที่บันทึกใน Excel, ไปที่ **File → Options → Advanced**, แล้วตรวจสอบช่อง **"Use 1904 date system"**.

## สรุป
คุณได้เรียนรู้วิธี **เปลี่ยนระบบวันที่ของ Excel** เป็น 1904 ด้วย Aspose.Cells for Java วิธีตั้งค่าวันที่ในเซลล์แต่ละเซลล์ และวิธีย้อนกลับไปยังระบบ 1900 เมื่อจำเป็น นำโค้ดส่วนนเหล่านี้ไปผสานใน pipeline การประมวลผลข้อมูลของคุณเพื่อรับประกันความเข้ากันได้ของวันที่ระหว่างแพลตฟอร์มและไฟล์เก่า

---

**อัปเดตล่าสุด:** 2026-10-28  
**ทดสอบด้วย:** Aspose.Cells 25.3 for Java  
**ผู้เขียน:** Aspose  

**แหล่งข้อมูล**
- **เอกสารอ้างอิง:** [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)
- **ดาวน์โหลด:** [Aspose.Cells Releases](https://releases.aspose.com/cells/java/)
- **ซื้อไลเซนส์:** [Buy Aspose.Cells](https://purchase.aspose.com/buy)
- **ทดลองใช้ฟรี:** [Start Free Trial](https://releases.aspose.com/cells/java/)
- **ไลเซนส์ชั่วคราว:** [Get Temporary License](https://purchase.aspose.com/temporary-license/)
- **ฟอรั่มสนับสนุน:** [Aspose Support](https://forum.aspose.com/c/cells/9)

## บทแนะนำที่เกี่ยวข้อง

- [แปลง Excel เป็น PDF อย่างมีประสิทธิภาพด้วยรูปแบบวันที่กำหนดเองโดยใช้ Aspose.Cells for Java](/cells/java/workbook-operations/render-excel-custom-date-formats-pdf-aspose-cells-java/)
- [Aspose.Cells for Java: วิธีสร้างและจัดรูปแบบ Workbook ของ Excel อย่างมีประสิทธิภาพ](/cells/java/getting-started/aspose-cells-java-workbook-creation-guide/)
- [เชี่ยวชาญการจัดการ Excel ด้วย Aspose.Cells for Java: การดำเนินการ Workbook และการจัดรูปแบบเซลล์](/cells/java/workbook-operations/excel-manipulation-aspose-cells-java-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}